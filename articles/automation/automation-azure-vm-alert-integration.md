---
title: "Предупреждения виртуальной Машины Windows Azure с Runbook автоматизации исправлять AAA» | Документы Microsoft»"
description: "В этой статье показано, как предупреждения toointegrate виртуальной машине Azure с Runbook автоматизации Azure и автоматически устранить проблемы"
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
ms.openlocfilehash: c226368a5c4c51fbfb331f4b97f7f2f239e701c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="d29df-103">Сценарий службы автоматизации Azure: обработка оповещений виртуальной машины Azure</span><span class="sxs-lookup"><span data-stu-id="d29df-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="d29df-104">Новая функция позволяет Runbook автоматизации toorun предупреждения виртуальной машины (VM) tooconfigure выпустили Azure Automation и виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="d29df-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you tooconfigure Virtual Machine (VM) alerts toorun Automation runbooks.</span></span> <span data-ttu-id="d29df-105">Эта новая возможность позволяет tooautomatically выполнение стандартных исправления в оповещениях tooVM ответа, как и перезапуска или остановки hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d29df-105">This new capability allows you tooautomatically perform standard remediation in response tooVM alerts, like restarting or stopping hello VM.</span></span>

<span data-ttu-id="d29df-106">Ранее, при создании правила оповещения виртуальной Машины можно было слишком[укажите перехватчик службы автоматизации](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook в runbook hello порядок toorun всякий раз, когда создано оповещение hello.</span><span class="sxs-lookup"><span data-stu-id="d29df-106">Previously, during VM alert rule creation you were able too[specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) tooa runbook in order toorun hello runbook whenever hello alert triggered.</span></span> <span data-ttu-id="d29df-107">Тем не менее это вам требовалось рабочих hello toodo создания hello, создания hello веб-перехватчика для hello runbook и скопировав и вставив веб-перехватчика hello во время создания правила оповещения.</span><span class="sxs-lookup"><span data-stu-id="d29df-107">However, this required you toodo hello work of creating hello runbook, creating hello webhook for hello runbook, and then copying and pasting hello webhook during alert rule creation.</span></span> <span data-ttu-id="d29df-108">С этот новый выпуск hello процесс намного проще, так как напрямую, можно выбрать из списка runbook во время создания правила оповещения и выбрана учетная запись автоматизации, которая будет выполнять hello runbook или легко создать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d29df-108">With this new release, hello process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run hello runbook or easily create an account.</span></span>

<span data-ttu-id="d29df-109">В этой статье будут показано, как просто можно tooset копирование оповещение виртуальной Машины Azure и настроены toorun runbook автоматизации всякий раз, когда предупреждение hello триггеров.</span><span class="sxs-lookup"><span data-stu-id="d29df-109">In this article, we will show you how easy it is tooset up an Azure VM alert and configure an Automation runbook toorun whenever hello alert triggers.</span></span> <span data-ttu-id="d29df-110">Примеры сценариев включают перезапуск виртуальной Машины, если использование памяти hello превышает некоторое пороговое значение из-за tooan приложение hello виртуальной Машины с утечкой памяти или остановка виртуальной Машины, когда находятся ниже 1% последний час hello ЦП в пользовательском режиме, а не используется.</span><span class="sxs-lookup"><span data-stu-id="d29df-110">Example scenarios include restarting a VM when hello memory usage exceeds some threshold due tooan application on hello VM with a memory leak, or stopping a VM when hello CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="d29df-111">Вы также узнаете, как hello автоматизировать создание субъекта-службы автоматической учетной записи упрощает использование hello модулей Runbook в Azure предупреждения исправления.</span><span class="sxs-lookup"><span data-stu-id="d29df-111">We’ll also explain how hello automated creation of a service principal in your Automation account simplifies hello use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="d29df-112">Создание оповещения на виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="d29df-112">Create an alert on a VM</span></span>
<span data-ttu-id="d29df-113">Выполните hello при порогом выполнены следующие шаги tooconfigure предупреждения toolaunch runbook.</span><span class="sxs-lookup"><span data-stu-id="d29df-113">Perform hello following steps tooconfigure an alert toolaunch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="d29df-114">В этом выпуске поддерживаются только виртуальные машины V2. Поддержка классических виртуальных машин будет добавлена в ближайшее время.</span><span class="sxs-lookup"><span data-stu-id="d29df-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="d29df-115">Войдите в портал Azure toohello и нажмите кнопку **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="d29df-115">Log in toohello Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="d29df-116">Выберите одну из виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d29df-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="d29df-117">Hello колонке панели мониторинга виртуальной машины будет отображаться и hello **параметры** колонке tooits справа.</span><span class="sxs-lookup"><span data-stu-id="d29df-117">hello virtual machine dashboard blade will appear and hello **Settings** blade tooits right.</span></span>  
3. <span data-ttu-id="d29df-118">Из hello **параметры** колонки в списке выберите раздел мониторинг hello **правила предупреждения**.</span><span class="sxs-lookup"><span data-stu-id="d29df-118">From hello **Settings** blade, under hello Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="d29df-119">На hello **предупреждения правила** колонка, щелкните **добавить оповещение**.</span><span class="sxs-lookup"><span data-stu-id="d29df-119">On hello **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="d29df-120">Это открывает hello **Добавление правила оповещения** колонки, где можно настроить условия hello для оповещения hello и выбрать одно или все из этих параметров: Отправка toosomeone электронной почты, использование системы предупреждений tooanother hello tooforward веб-перехватчика, и (или) Запустите runbook автоматизации в выпуске hello tooremediate попытки ответа.</span><span class="sxs-lookup"><span data-stu-id="d29df-120">This opens up hello **Add an alert rule** blade, where you can configure hello conditions for hello alert and choose among one or all of these options: send email toosomeone, use a webhook tooforward hello alert tooanother system, and/or run an Automation runbook in response attempt tooremediate hello issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="d29df-121">Настройка модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="d29df-121">Configure a runbook</span></span>
<span data-ttu-id="d29df-122">tooconfigure toorun runbook, по достижении порога оповещения hello виртуальной Машины, выберите **Runbook службы автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="d29df-122">tooconfigure a runbook toorun when hello VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="d29df-123">В hello **Настройка runbook** колонки, можно выбрать hello runbook toorun и runbook hello toorun учетной записи службы автоматизации hello в.</span><span class="sxs-lookup"><span data-stu-id="d29df-123">In hello **Configure runbook** blade, you can select hello runbook toorun and hello Automation account toorun hello runbook in.</span></span>

![Настройка модуля Runbook службы автоматизации и создание учетной записи службы автоматизации](media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="d29df-125">В этой версии можно выбирать из трех Runbook, которые предоставляет службу hello — перезапуск виртуальной Машины, остановить виртуальную Машину или удалить виртуальную Машину (Удалить).</span><span class="sxs-lookup"><span data-stu-id="d29df-125">For this release you can choose from three runbooks that hello service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="d29df-126">Здравствуйте возможность tooselect другие модули Runbook или один из собственных модулей Runbook будут доступны в будущих выпусках.</span><span class="sxs-lookup"><span data-stu-id="d29df-126">hello ability tooselect other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Модули Runbook toochoose из](media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="d29df-128">Здравствуйте, выбрав один из трех hello, доступные модули Runbook, **учетной записи автоматизации** появляется в раскрывающемся списке, и можно будет выбрать автоматизации runbook hello учетной записи будет выполняться как.</span><span class="sxs-lookup"><span data-stu-id="d29df-128">After you select one of hello three available runbooks, hello **Automation account** drop-down list appears and you can select an automation account hello runbook will run as.</span></span> <span data-ttu-id="d29df-129">Модули Runbook должны toorun в контексте hello [учетной записи автоматизации](automation-security-overview.md) , находящегося в вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="d29df-129">Runbooks need toorun in hello context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="d29df-130">Можно выбрать уже созданную учетную запись службы автоматизации или создать новую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d29df-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="d29df-131">Hello Runbook, которые предоставляются проверки подлинности tooAzure с помощью субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="d29df-131">hello runbooks that are provided authenticate tooAzure using a service principal.</span></span> <span data-ttu-id="d29df-132">Если в одной из существующих учетных записей автоматизации toorun hello runbook, мы будет автоматически создавать hello службы участника.</span><span class="sxs-lookup"><span data-stu-id="d29df-132">If you choose toorun hello runbook in one of your existing Automation accounts, we will automatically create hello service principal for you.</span></span> <span data-ttu-id="d29df-133">При выборе новой учетной записи автоматизации toocreate затем будут автоматически созданы hello учетной записи и hello участника-службы.</span><span class="sxs-lookup"><span data-stu-id="d29df-133">If you choose toocreate a new Automation account, then we will automatically create hello account and hello service principal.</span></span> <span data-ttu-id="d29df-134">В обоих случаях два средства также будет создан в учетной записи автоматизации — ресурс сертификата с именем hello **AzureRunAsCertificate** и средств подключения, с именем **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="d29df-134">In both cases, two assets will also be created in hello Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="d29df-135">будет использовать модули Runbook Hello **AzureRunAsConnection** tooauthenticate с Azure в действие управления tooperform hello порядке по отношению к hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d29df-135">hello runbooks will use **AzureRunAsConnection** tooauthenticate with Azure in order tooperform hello management action against hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="d29df-136">Hello участника-службы в область hello подписки создается и назначается роль участника hello.</span><span class="sxs-lookup"><span data-stu-id="d29df-136">hello service principal is created in hello subscription scope and is assigned hello Contributor role.</span></span> <span data-ttu-id="d29df-137">Эта роль необходима для hello учетной записи toohave разрешение toorun автоматизации модулей Runbook toomanage виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="d29df-137">This role is required in order for hello account toohave permission toorun Automation runbooks toomanage Azure VMs.</span></span>  <span data-ttu-id="d29df-138">Создание Hello машин учетной записи и/или субъекта-службы — однократного события.</span><span class="sxs-lookup"><span data-stu-id="d29df-138">hello creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="d29df-139">После их создания, можно использовать модули Runbook toorun этой учетной записи для других оповещений на виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="d29df-139">Once they are created, you can use that account toorun runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="d29df-140">При нажатии кнопки **ОК** настроено оповещение hello и если вы выбрали параметр hello toocreate учетную запись автоматизации, он будет создан вместе с hello участника-службы.</span><span class="sxs-lookup"><span data-stu-id="d29df-140">When you click **OK** hello alert is configured and if you selected hello option toocreate a new Automation account, it is created along with hello service principal.</span></span>  <span data-ttu-id="d29df-141">Это может занять несколько секунд toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d29df-141">This can take a few seconds toocomplete.</span></span>  

![Настройка модуля Runbook](media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="d29df-143">После завершения настройки hello вы увидите имя hello hello runbook отображаются в hello **Добавление правила оповещения** колонку.</span><span class="sxs-lookup"><span data-stu-id="d29df-143">After hello configuration is completed you will see hello name of hello runbook appear in hello **Add an alert rule** blade.</span></span>

![Модуль Runbook настроен](media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="d29df-145">Нажмите кнопку **ОК** в hello **Добавление правила оповещения** колонки и hello правило оповещения будут создаваться и активировать, если hello виртуальная машина находится в состоянии выполнения.</span><span class="sxs-lookup"><span data-stu-id="d29df-145">Click **OK** in hello **Add an alert rule** blade and hello alert rule will be created and activate if hello virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="d29df-146">Включение и отключение модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="d29df-146">Enable or disable a runbook</span></span>
<span data-ttu-id="d29df-147">Если у вас есть runbook, настроенных для оповещения, его можно отключить без удаления конфигурации runbook hello.</span><span class="sxs-lookup"><span data-stu-id="d29df-147">If you have a runbook configured for an alert, you can disable it without removing hello runbook configuration.</span></span> <span data-ttu-id="d29df-148">Это дает предупреждение hello tookeep под управлением и возможно тестировании некоторых правил оповещения hello и затем повторно включать hello runbook.</span><span class="sxs-lookup"><span data-stu-id="d29df-148">This allows you tookeep hello alert running and perhaps test some of hello alert rules and then later re-enable hello runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="d29df-149">Создание модуля Runbook, который работает с оповещениями Azure</span><span class="sxs-lookup"><span data-stu-id="d29df-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="d29df-150">При выборе модуля в рамках Azure правила генерации оповещений hello модуль должен логики toohave toomanage hello данных предупреждений, передаваемое tooit.</span><span class="sxs-lookup"><span data-stu-id="d29df-150">When you choose a runbook as part of an Azure alert rule, hello runbook needs toohave logic in it toomanage hello alert data that is passed tooit.</span></span>  <span data-ttu-id="d29df-151">Создается при настройке модуля в правиле оповещения веб-перехватчика для hello runbook; Этот веб-перехватчика является, то используется toostart hello runbook каждого предупреждения триггеры hello времени.</span><span class="sxs-lookup"><span data-stu-id="d29df-151">When a runbook is configured in an alert rule, a webhook is created for hello runbook; that webhook is then used toostart hello runbook each time hello alert triggers.</span></span>  <span data-ttu-id="d29df-152">toostart hello Hello реальный вызов runbook является URL-адрес HTTP POST веб-перехватчика запроса toohello.</span><span class="sxs-lookup"><span data-stu-id="d29df-152">hello actual call toostart hello runbook is an HTTP POST request toohello webhook URL.</span></span> <span data-ttu-id="d29df-153">текст Hello hello POST-запрос содержит неверный формат JSON объект, который содержит связанные toohello оповещение полезных свойств.</span><span class="sxs-lookup"><span data-stu-id="d29df-153">hello body of hello POST request contains a JSON-formated object that contains useful properties related toohello alert.</span></span>  <span data-ttu-id="d29df-154">Как можно увидеть ниже, предупреждения данных hello содержит сведения, такие как идентификатор подписки, resourceGroupName, resourceName и типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="d29df-154">As you can see below, hello alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="d29df-155">Пример данных оповещения</span><span class="sxs-lookup"><span data-stu-id="d29df-155">Example of Alert data</span></span>
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

<span data-ttu-id="d29df-156">Получив hello веб-перехватчика службы автоматизации hello HTTP POST он извлекает данные предупреждения hello и передает его toohello runbook в hello WebhookData runbook входного параметра.</span><span class="sxs-lookup"><span data-stu-id="d29df-156">When hello Automation webhook service receives hello HTTP POST it extracts hello alert data and passes it toohello runbook in hello WebhookData runbook input parameter.</span></span>  <span data-ttu-id="d29df-157">Ниже приведен пример модуля runbook, показывающий, как toouse hello параметр WebhookData и извлечения данных о предупреждениях hello и использовать его hello toomanage ресурсов Azure, вызвавшей предупреждение hello.</span><span class="sxs-lookup"><span data-stu-id="d29df-157">Below is a sample runbook that shows how toouse hello WebhookData parameter and extract hello alert data and use it toomanage hello Azure resource that triggered hello alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="d29df-158">Пример модуля Runbook</span><span class="sxs-lookup"><span data-stu-id="d29df-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response tooan Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get hello data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that hello alert status is 'Activated' (alert condition went from false tootrue)
    # and not 'Resolved' (alert condition went from true toofalse)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get hello info needed tooidentify hello VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is hello expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate tooAzure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in hello Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart hello VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # hello alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant toobe started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="d29df-159">Сводка</span><span class="sxs-lookup"><span data-stu-id="d29df-159">Summary</span></span>
<span data-ttu-id="d29df-160">При настройке оповещение на Виртуальной машине Azure, теперь у вас есть tooeasily возможность hello настройки автоматизации runbook tooautomatically действий исправления при hello предупреждение запускает.</span><span class="sxs-lookup"><span data-stu-id="d29df-160">When you configure an alert on an Azure VM, you now have hello ability tooeasily configure an Automation runbook tooautomatically perform remediation action when hello alert triggers.</span></span> <span data-ttu-id="d29df-161">Для этого выпуска можно выбрать из модулей Runbook toorestart, остановить или удаление виртуальной Машины, в зависимости от вашего сценария предупреждения.</span><span class="sxs-lookup"><span data-stu-id="d29df-161">For this release, you can choose from runbooks toorestart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="d29df-162">Это просто hello начало Включение сценариев, где вы управляете действия hello (уведомление, устранение неполадок, исправления), которые будут выполнены автоматически, когда инициирует предупреждение.</span><span class="sxs-lookup"><span data-stu-id="d29df-162">This is just hello beginning of enabling scenarios where you control hello actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d29df-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d29df-163">Next Steps</span></span>
* <span data-ttu-id="d29df-164">tooget к работе с графический Runbook в разделе [Мой первый графический runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="d29df-164">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="d29df-165">tooget к работе с PowerShell модули Runbook рабочего процесса, в разделе [Мой первый runbook рабочего процесса PowerShell](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="d29df-165">tooget started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="d29df-166">в разделе toolearn Дополнительные сведения о типах runbook, их преимущества и ограничения, [типов runbook службы автоматизации Azure](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="d29df-166">toolearn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>

