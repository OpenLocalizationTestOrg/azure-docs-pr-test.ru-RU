---
title: " Обработка оповещений виртуальной машины Azure с помощью модулей Runbook службы автоматизации | Документация Майкрософт"
description: "В этой статье показано, как интегрировать оповещения виртуальной машины Azure с модулями Runbook службы автоматизации Azure и автоматически устранять проблемы"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: 738959b8e1ee5da989bb996d1ce8148cbf912781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="b22b6-103">Сценарий службы автоматизации Azure: обработка оповещений виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="b22b6-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="b22b6-104">Для службы автоматизации Azure и виртуальных машин Azure доступна новая функция, которая позволяет настроить оповещения виртуальных машин для запуска модулей Runbook службы автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b22b6-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span></span> <span data-ttu-id="b22b6-105">Эта новая возможность позволяет автоматически выполнять стандартное исправление в ответ на оповещения виртуальных машин, например перезапускать или останавливать виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="b22b6-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span></span>

<span data-ttu-id="b22b6-106">Ранее при создании правила оповещений виртуальной машины можно было [указать веб-перехватчик службы автоматизации](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/), запускающий модуль Runbook при возникновении оповещения.</span><span class="sxs-lookup"><span data-stu-id="b22b6-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span></span> <span data-ttu-id="b22b6-107">Но для этого необходимо было создавать модуль Runbook, создавать веб-перехватчик для этого модуля и вставлять веб-перехватчик при создании правила оповещения.</span><span class="sxs-lookup"><span data-stu-id="b22b6-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span></span> <span data-ttu-id="b22b6-108">В этом новом выпуске процесс упростился. Теперь можно непосредственно выбрать модуль Runbook из списка при создании правила оповещения, а также выбрать учетную запись службы автоматизации, которая будет запускать модуль Runbook, или без труда создать такую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="b22b6-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span></span>

<span data-ttu-id="b22b6-109">В этой статье мы покажем, насколько просто настроить оповещение виртуальной машины Azure и модуль Runbook службы автоматизации, чтобы он запускался при инициализации оповещения.</span><span class="sxs-lookup"><span data-stu-id="b22b6-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span></span> <span data-ttu-id="b22b6-110">Примеры сценариев включают перезапуск виртуальной машины, когда использование памяти превышает определенный предел из-за приложения на виртуальной машине с утечкой памяти, или остановку виртуальной машины, если время использования ЦП за последний час составляло меньше 1 % и если ЦП не используется.</span><span class="sxs-lookup"><span data-stu-id="b22b6-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="b22b6-111">Кроме того, мы рассмотрим, как автоматическое создание субъекта-службы в учетной записи службы автоматизации упрощает использование модулей Runbook при обработке оповещений Azure.</span><span class="sxs-lookup"><span data-stu-id="b22b6-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="b22b6-112">Создание оповещения на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="b22b6-112">Create an alert on a VM</span></span>
<span data-ttu-id="b22b6-113">Выполните следующие действия, чтобы настроить оповещение для запуска модуля Runbook, когда достигается пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="b22b6-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="b22b6-114">В этом выпуске поддерживаются только виртуальные машины V2. Поддержка классических виртуальных машин будет добавлена в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="b22b6-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="b22b6-115">Войдите на портал Azure и щелкните элемент **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="b22b6-115">Log in to the Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="b22b6-116">Выберите одну из виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="b22b6-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="b22b6-117">Появится колонка панели мониторинга виртуальной машины, а справа от нее отобразится колонка **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="b22b6-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span></span>  
3. <span data-ttu-id="b22b6-118">В колонке **Параметры**, в разделе "Мониторинг" выберите пункт **Правила оповещения**.</span><span class="sxs-lookup"><span data-stu-id="b22b6-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="b22b6-119">В колонке **Правила оповещения** выберите команду **Добавить оповещение**.</span><span class="sxs-lookup"><span data-stu-id="b22b6-119">On the **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="b22b6-120">Откроется колонка **Добавление правила оповещения** , в которой можно настроить условия для оповещения и выбрать один или все варианты: отправить электронное сообщение, использовать веб-перехватчик для пересылки оповещения в другую систему и/или запустить модуль Runbook службы автоматизации, чтобы попытаться устранить проблему.</span><span class="sxs-lookup"><span data-stu-id="b22b6-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="b22b6-121">Настройка модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="b22b6-121">Configure a runbook</span></span>
<span data-ttu-id="b22b6-122">Чтобы настроить модуль Runbook для запуска при достижении порога оповещения виртуальной машины, выберите пункт **Модуль Runbook службы автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="b22b6-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="b22b6-123">В колонке **Настройка модуля Runbook** можно выбрать модуль Runbook для запуска и учетную запись службы автоматизации, в которой необходимо запускать этот модуль.</span><span class="sxs-lookup"><span data-stu-id="b22b6-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span></span>

![Настройка модуля Runbook службы автоматизации и создание учетной записи службы автоматизации](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="b22b6-125">В этом выпуске можно выбрать один из трех модулей Runbook, предоставляемых службой: "Перезапуск виртуальной машины", "Остановка виртуальной машины" или "Удаление виртуальной машины".</span><span class="sxs-lookup"><span data-stu-id="b22b6-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="b22b6-126">Возможность выбора других или одного из собственных модулей Runbook будет доступна в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="b22b6-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Модули Runbook для выбора](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="b22b6-128">После выбора одного из трех доступных модулей Runbook отобразится раскрывающийся список **Учетная запись службы автоматизации**, где можно выбрать учетную запись службы автоматизации, от имени которой будет запускаться модуль Runbook.</span><span class="sxs-lookup"><span data-stu-id="b22b6-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span></span> <span data-ttu-id="b22b6-129">Модули Runbook должны запускаться в контексте [учетной записи службы автоматизации](automation-security-overview.md), которая находится в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="b22b6-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="b22b6-130">Можно выбрать уже созданную учетную запись службы автоматизации или создать новую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="b22b6-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="b22b6-131">Проверка подлинности предоставленных модулей Runbook выполняется в Azure с помощью субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="b22b6-131">The runbooks that are provided authenticate to Azure using a service principal.</span></span> <span data-ttu-id="b22b6-132">Если вы решили запустить модуль Runbook в одной из существующих учетных записей службы автоматизации, субъект-служба будет создана автоматически.</span><span class="sxs-lookup"><span data-stu-id="b22b6-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span></span> <span data-ttu-id="b22b6-133">Если вы решили создать учетную запись службы автоматизации, субъект-служба будет создана автоматически вместе с учетной записью.</span><span class="sxs-lookup"><span data-stu-id="b22b6-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span></span> <span data-ttu-id="b22b6-134">В обоих случаях в учетной записи службы автоматизации будут созданы два ресурса: ресурс сертификата с именем **AzureRunAsCertificate** и ресурс подключения с именем **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="b22b6-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="b22b6-135">Модули Runbook будут использовать ресурс **AzureRunAsConnection** для проверки подлинности в Azure, чтобы выполнить действие управления для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="b22b6-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="b22b6-136">Субъект-служба создается в области действия подписки и назначается роли участника.</span><span class="sxs-lookup"><span data-stu-id="b22b6-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span></span> <span data-ttu-id="b22b6-137">Эта роль необходима для того, чтобы учетная запись имела разрешение на запуск модулей Runbook службы автоматизации для управления виртуальными машинами Azure.</span><span class="sxs-lookup"><span data-stu-id="b22b6-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span></span>  <span data-ttu-id="b22b6-138">Создание учетной записи службы автоматизации и/или субъекта-службы является одноразовым событием.</span><span class="sxs-lookup"><span data-stu-id="b22b6-138">The creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="b22b6-139">После их создания эту учетную запись можно использовать для запуска модулей Runbook для оповещений других виртуальных машин Azure.</span><span class="sxs-lookup"><span data-stu-id="b22b6-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="b22b6-140">После нажатия кнопки **ОК** выполняется настройка оповещения. Если выбран вариант создания учетной записи службы автоматизации, то она создается вместе с субъектом-службой.</span><span class="sxs-lookup"><span data-stu-id="b22b6-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span></span>  <span data-ttu-id="b22b6-141">Для завершения этого процесса может понадобиться несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="b22b6-141">This can take a few seconds to complete.</span></span>  

![Настройка модуля Runbook](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="b22b6-143">После завершения настройки вы увидите имя модуля Runbook в колонке **Добавление правила оповещения** .</span><span class="sxs-lookup"><span data-stu-id="b22b6-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span></span>

![Модуль Runbook настроен](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="b22b6-145">Нажмите кнопку **ОК** в колонке **Добавление правила оповещения**, и, если виртуальная машина запущена, то будет создано и активировано правило оповещений.</span><span class="sxs-lookup"><span data-stu-id="b22b6-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="b22b6-146">Включение и отключение модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="b22b6-146">Enable or disable a runbook</span></span>
<span data-ttu-id="b22b6-147">Если для оповещения настроен модуль Runbook, его можно отключить, не удаляя конфигурацию модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="b22b6-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span></span> <span data-ttu-id="b22b6-148">Это позволяет продолжить выполнение оповещения и, возможно, проверить некоторые правила оповещения и позже включить модуль Runbook повторно.</span><span class="sxs-lookup"><span data-stu-id="b22b6-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="b22b6-149">Создание модуля Runbook, который работает с оповещениями Azure</span><span class="sxs-lookup"><span data-stu-id="b22b6-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="b22b6-150">При выборе модуля Runbook в качестве части правила генерации оповещений Azure он должен содержать логику для управления данными оповещений, которые в него поступают.</span><span class="sxs-lookup"><span data-stu-id="b22b6-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span></span>  <span data-ttu-id="b22b6-151">При настройке модуля Runbook в правиле генерации оповещений для него создается webhook, который затем используется для запуска модуля Runbook каждый раз, когда активируется оповещение.</span><span class="sxs-lookup"><span data-stu-id="b22b6-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span></span>  <span data-ttu-id="b22b6-152">Фактический вызов для запуска модуля Runbook осуществляется с помощью HTTP-запроса POST на URL-адрес webhook.</span><span class="sxs-lookup"><span data-stu-id="b22b6-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span></span> <span data-ttu-id="b22b6-153">Текст запроса POST содержит объект в формате JSON с полезными свойствами, связанными с оповещением.</span><span class="sxs-lookup"><span data-stu-id="b22b6-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span></span>  <span data-ttu-id="b22b6-154">Как видно ниже, данные оповещения содержат такие сведения, как идентификатор подписки, имя группы ресурсов, имя ресурса и тип ресурса.</span><span class="sxs-lookup"><span data-stu-id="b22b6-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="b22b6-155">Пример данных оповещения</span><span class="sxs-lookup"><span data-stu-id="b22b6-155">Example of Alert data</span></span>
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

<span data-ttu-id="b22b6-156">Когда webhook службы автоматизации получает HTTP-запрос POST, он извлекает данные оповещения и передает их в модуль Runbook в качестве входного параметра WebhookData модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="b22b6-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span></span>  <span data-ttu-id="b22b6-157">Ниже приведен пример модуля Runbook, в котором показано, как использовать параметр WebhookData, извлекать данные оповещения и использовать его для управления ресурсом Azure, активировавшим оповещение.</span><span class="sxs-lookup"><span data-stu-id="b22b6-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="b22b6-158">Пример модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="b22b6-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response to an Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get the data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that the alert status is 'Activated' (alert condition went from false to true)
    # and not 'Resolved' (alert condition went from true to false)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get the info needed to identify the VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is the expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate to Azure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart the VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # The alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant to be started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="b22b6-159">Сводка</span><span class="sxs-lookup"><span data-stu-id="b22b6-159">Summary</span></span>
<span data-ttu-id="b22b6-160">При настройке оповещения на виртуальной машине Azure вы получаете возможность легко настраивать модуль Runbook службы автоматизации для автоматического выполнения действия исправления при инициализации оповещения.</span><span class="sxs-lookup"><span data-stu-id="b22b6-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span></span> <span data-ttu-id="b22b6-161">В этом выпуске можно выбрать модуль Runbook для перезапуска, остановки или удаления виртуальной машины в зависимости от вашего сценария оповещений.</span><span class="sxs-lookup"><span data-stu-id="b22b6-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="b22b6-162">Это только начало использования сценариев, в которых вы управляете действиями (оповещение, устранение неполадок, исправление), автоматически предпринимаемыми при инициализации оповещения.</span><span class="sxs-lookup"><span data-stu-id="b22b6-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b22b6-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b22b6-163">Next Steps</span></span>
* <span data-ttu-id="b22b6-164">Чтобы начать работу с графическими модулями Runbook, см. инструкции в статье [Первый графический Runbook](automation-first-runbook-graphical.md).</span><span class="sxs-lookup"><span data-stu-id="b22b6-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="b22b6-165">Чтобы приступить к работе с модулями Runbook рабочих процессов PowerShell, обратитесь к статье [Мой первый модуль Runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="b22b6-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="b22b6-166">Дополнительные сведения о типах модулей Runbook, их преимуществах и ограничениях см. в статье [Типы модулей Runbook в службе автоматизации Azure](automation-runbook-types.md).</span><span class="sxs-lookup"><span data-stu-id="b22b6-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

