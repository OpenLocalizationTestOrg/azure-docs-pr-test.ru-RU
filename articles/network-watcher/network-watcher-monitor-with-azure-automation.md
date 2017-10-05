---
title: "Мониторинг VPN-шлюзов с помощью средства устранения неполадок Наблюдателя за сетями Azure | Документация Майкрософт"
description: "В этой статье описывается, как диагностировать локальное подключение с помощью службы автоматизации Azure и Наблюдателя за сетями."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 55ec52dd0d94a0347cc67a8785b89611da955111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="29de8-103">Мониторинг VPN-шлюзов с помощью средства устранения неполадок Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="29de8-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="29de8-104">Чтобы предоставлять клиентам надежное обслуживание, вы должны знать все о производительности своей сети.</span><span class="sxs-lookup"><span data-stu-id="29de8-104">Gaining deep insights on your network performance is critical to provide reliable services to customers.</span></span> <span data-ttu-id="29de8-105">Поэтому важно быстро обнаруживать аварийные состояния сети и принимать необходимые меры, чтобы свести к минимуму последствия этих состояний.</span><span class="sxs-lookup"><span data-stu-id="29de8-105">It is therefore critical to detect network outage conditions quickly and take corrective action to mitigate the outage condition.</span></span> <span data-ttu-id="29de8-106">Служба автоматизации Azure позволяет реализовать и выполнить эту задачу программными средствами с помощью модулей runbook.</span><span class="sxs-lookup"><span data-stu-id="29de8-106">Azure Automation enables you to implement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="29de8-107">С помощью службы автоматизации Azure вы можете выполнять упреждающий непрерывный мониторинг сети и создавать оповещения.</span><span class="sxs-lookup"><span data-stu-id="29de8-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="29de8-108">Сценарий</span><span class="sxs-lookup"><span data-stu-id="29de8-108">Scenario</span></span>

<span data-ttu-id="29de8-109">На следующем изображении показано многоуровневое приложение, локальное подключение к которому обеспечивают VPN-шлюз и туннель.</span><span class="sxs-lookup"><span data-stu-id="29de8-109">The scenario in the following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="29de8-110">Для производительности приложений крайне важно обеспечить включение и работу VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="29de8-110">Ensuring the VPN Gateway is up and running is critical to the applications performance.</span></span>

<span data-ttu-id="29de8-111">Модуль runbook создается со скриптом для проверки состояния подключения VPN-туннеля с помощью API устранения неполадок в ресурсах.</span><span class="sxs-lookup"><span data-stu-id="29de8-111">A runbook is created with a script to check for connection status of the VPN tunnel, using the Resource Troubleshooting API to check for connection tunnel status.</span></span> <span data-ttu-id="29de8-112">Если туннель не работает, администраторам электронной почтой отправляется триггер.</span><span class="sxs-lookup"><span data-stu-id="29de8-112">If the status is not healthy, an email trigger is sent to administrators.</span></span>

![Пример сценария][scenario]

<span data-ttu-id="29de8-114">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="29de8-114">This scenario will:</span></span>

- <span data-ttu-id="29de8-115">Как создать модуль runbook, вызывающий командлет `Start-AzureRmNetworkWatcherResourceTroubleshooting` для устранения неполадок подключения.</span><span class="sxs-lookup"><span data-stu-id="29de8-115">Create a runbook calling the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet to troubleshoot connection status</span></span>
- <span data-ttu-id="29de8-116">Как подключить расписание к модулю runbook.</span><span class="sxs-lookup"><span data-stu-id="29de8-116">Link a schedule to the runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="29de8-117">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="29de8-117">Before you begin</span></span>

<span data-ttu-id="29de8-118">Прежде чем приступить к работе с этим сценарием, следует подготовить такие необходимые компоненты:</span><span class="sxs-lookup"><span data-stu-id="29de8-118">Before you start this scenario, you must have the following pre-requisites:</span></span>

- <span data-ttu-id="29de8-119">Учетная запись службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="29de8-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="29de8-120">Убедитесь, что учетная запись службы автоматизации содержит последние версии модулей, а также модуль AzureRM.Network.</span><span class="sxs-lookup"><span data-stu-id="29de8-120">Ensure that the automation account has the latest modules and also has the AzureRM.Network module.</span></span> <span data-ttu-id="29de8-121">Чтобы добавить модуль AzureRM.Network в учетную запись службы автоматизации Модуль, см. коллекцию модулей.</span><span class="sxs-lookup"><span data-stu-id="29de8-121">The AzureRM.Network module is available in the module gallery if you need to add it to your automation account.</span></span>
- <span data-ttu-id="29de8-122">Набор учетных данных, настроенных в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="29de8-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="29de8-123">См. дополнительные сведения о [безопасности службы автоматизации Azure](../automation/automation-security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="29de8-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="29de8-124">Допустимый SMTP-сервер (Office 365, локальный или другой адрес электронной почты) и учетные данные, определенные в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="29de8-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="29de8-125">Настроенный шлюз виртуальной сети в Azure.</span><span class="sxs-lookup"><span data-stu-id="29de8-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="29de8-126">Существующая учетная запись хранения с существующим контейнером для хранения журналов.</span><span class="sxs-lookup"><span data-stu-id="29de8-126">An existing storage account with an existing container to store the logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="29de8-127">Инфраструктура, показанная на предыдущем рисунке, предназначена для иллюстрации. Она не создается с помощью выполнения инструкций из этой статьи.</span><span class="sxs-lookup"><span data-stu-id="29de8-127">The infrastructure depicted in the preceding image is for illustration purposes and are not created with the steps contained in this article.</span></span>

### <a name="create-the-runbook"></a><span data-ttu-id="29de8-128">Создание модуля runbook</span><span class="sxs-lookup"><span data-stu-id="29de8-128">Create the runbook</span></span>

<span data-ttu-id="29de8-129">Чтобы настроить пример, сначала нужно создать модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="29de8-129">The first step to configuring the example is to create the runbook.</span></span> <span data-ttu-id="29de8-130">В этом примере используется учетная запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="29de8-130">This example uses a run-as account.</span></span> <span data-ttu-id="29de8-131">Сведения об учетных записях запуска от имени см. в разделе [Создание учетной записи службы автоматизации на портале Azure](../automation/automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="29de8-131">To learn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="29de8-132">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="29de8-132">Step 1</span></span>

<span data-ttu-id="29de8-133">Перейдите к службе автоматизации Azure на [портале Azure](https://portal.azure.com) и нажмите кнопку **Модули Runbook**.</span><span class="sxs-lookup"><span data-stu-id="29de8-133">Navigate to Azure Automation in the [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Обзор учетной записи службы автоматизации][1]

### <a name="step-2"></a><span data-ttu-id="29de8-135">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="29de8-135">Step 2</span></span>

<span data-ttu-id="29de8-136">Нажмите кнопку **Добавить Runbook**, чтобы начать создание модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="29de8-136">Click **Add a runbook** to start the creation process of the runbook.</span></span>

![Колонка модулей runbook][2]

### <a name="step-3"></a><span data-ttu-id="29de8-138">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="29de8-138">Step 3</span></span>

<span data-ttu-id="29de8-139">В разделе **Быстрое создание**, нажмите кнопку **Создать новый Runbook**, чтобы создать модуль runbook.</span><span class="sxs-lookup"><span data-stu-id="29de8-139">Under **Quick Create**, click **Create a new runbook** to create the runbook.</span></span>

![Колонка добавления модуля runbook][3]

### <a name="step-4"></a><span data-ttu-id="29de8-141">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="29de8-141">Step 4</span></span>

<span data-ttu-id="29de8-142">На этом этапе присвойте модулю runbook имя. В этом примере он называется **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="29de8-142">In this step, we give the runbook a name, in the example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="29de8-143">Необходимо указать описательное имя модуля runbook. Кроме того, рекомендуется присвоить ему имя, которое соответствует стандартам именования PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29de8-143">It is important to give the runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="29de8-144">Тип модуля runbook в этом примере — **PowerShell**. Другие варианты: графический, рабочий процесс PowerShell и графический рабочий процесс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29de8-144">The runbook type for this example is **PowerShell**, the other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![Колонка модуля runbook][4]

### <a name="step-5"></a><span data-ttu-id="29de8-146">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="29de8-146">Step 5</span></span>

<span data-ttu-id="29de8-147">На этом шаге создается модуль runbook. В примере ниже содержится весь необходимый код.</span><span class="sxs-lookup"><span data-stu-id="29de8-147">In this step the runbook is created, the following code example provides all the code needed for the example.</span></span> <span data-ttu-id="29de8-148">Элементы \<value\> в этом коде необходимо заменить значениями из вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="29de8-148">The items in the code that contain \<value\> need to be replaced with the values from your subscription.</span></span>

<span data-ttu-id="29de8-149">Используйте следующий код и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="29de8-149">Use the following code as click **Save**</span></span>

```PowerShell
# Set these variables to the proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<to email address>"
$smtpServer = "<smtp.office365.com>"
$smtpPort = 587
$runAsConnectionName = "<AzureRunAsConnection>"
$subscriptionId = "<subscription id>"
$region = "<Azure region>"
$vpnConnectionName = "<vpn connection name>"
$vpnConnectionResourceGroup = "<resource group name>"
$storageAccountName = "<storage account name>"
$storageAccountResourceGroup = "<resource group name>"
$storageAccountContainer = "<container name>"

# Get credentials for Office 365 account
$cred = Get-AutomationPSCredential -Name $o365AutomationCredential

# Get the connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in to Azure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context to a specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView the logs at $($storagePath) to learn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -To $toEmail `
        -Subject $subject `
        -Body $body `
        -UseSsl `
        -Port $smtpPort `
        -SmtpServer $smtpServer `
        -From $fromEmail `
        -BodyAsHtml `
        -Credential $cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.code)")
    }
```

### <a name="step-6"></a><span data-ttu-id="29de8-150">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="29de8-150">Step 6</span></span>

<span data-ttu-id="29de8-151">После сохранения модуля runbook его необходимо подключить к расписанию, чтобы автоматизировать запуск модуля.</span><span class="sxs-lookup"><span data-stu-id="29de8-151">Once the runbook is saved, a schedule must be linked to it to automate the start of the runbook.</span></span> <span data-ttu-id="29de8-152">Чтобы начать, нажмите кнопку **Расписание**.</span><span class="sxs-lookup"><span data-stu-id="29de8-152">To start the process, click **Schedule**.</span></span>

![Шаг 6][6]

## <a name="link-a-schedule-to-the-runbook"></a><span data-ttu-id="29de8-154">Подключение расписания к модулю runbook</span><span class="sxs-lookup"><span data-stu-id="29de8-154">Link a schedule to the runbook</span></span>

<span data-ttu-id="29de8-155">Необходимо создать новое расписание.</span><span class="sxs-lookup"><span data-stu-id="29de8-155">A new schedule must be created.</span></span> <span data-ttu-id="29de8-156">Щелкните **Связать расписание с модулем runbook**.</span><span class="sxs-lookup"><span data-stu-id="29de8-156">Click **Link a schedule to your runbook**.</span></span>

![Шаг 7][7]

### <a name="step-1"></a><span data-ttu-id="29de8-158">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="29de8-158">Step 1</span></span>

<span data-ttu-id="29de8-159">В колонке **Расписание** щелкните **Создать новое расписание**.</span><span class="sxs-lookup"><span data-stu-id="29de8-159">On the **Schedule** blade, click **Create a new schedule**</span></span>

![Шаг 8][8]

### <a name="step-2"></a><span data-ttu-id="29de8-161">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="29de8-161">Step 2</span></span>

<span data-ttu-id="29de8-162">В колонке **Новое расписание** заполните сведения о расписании.</span><span class="sxs-lookup"><span data-stu-id="29de8-162">On the **New Schedule** blade fill out the schedule information.</span></span> <span data-ttu-id="29de8-163">Вы можете указать значения, перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="29de8-163">The values that can be set are in the following list:</span></span>

- <span data-ttu-id="29de8-164">**Имя** — понятное имя расписания.</span><span class="sxs-lookup"><span data-stu-id="29de8-164">**Name** - The friendly name of the schedule.</span></span>
- <span data-ttu-id="29de8-165">**Описание** — описание расписания.</span><span class="sxs-lookup"><span data-stu-id="29de8-165">**Description** - A description of the schedule.</span></span>
- <span data-ttu-id="29de8-166">**Начало** — это значение включает дату, время и часовой пояс, которые формируют время активации расписания.</span><span class="sxs-lookup"><span data-stu-id="29de8-166">**Starts** - This value is a combination of date, time, and time zone that make up the time the schedule triggers.</span></span>
- <span data-ttu-id="29de8-167">**Повторение** — это значение определяет повторение расписания.</span><span class="sxs-lookup"><span data-stu-id="29de8-167">**Recurrence** - This value determines the schedules repetition.</span></span>  <span data-ttu-id="29de8-168">Допустимые значения: **Однократно** или **Периодически**.</span><span class="sxs-lookup"><span data-stu-id="29de8-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="29de8-169">**Повторять каждые** — интервал повторения расписания в часах, днях, неделях или месяцах.</span><span class="sxs-lookup"><span data-stu-id="29de8-169">**Recur every** - The recurrence interval of the schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="29de8-170">**Установить срок действия** — значение определяет, есть ли у расписания срок действия.</span><span class="sxs-lookup"><span data-stu-id="29de8-170">**Set Expiration** - The value determines if the schedule should expire or not.</span></span> <span data-ttu-id="29de8-171">Возможные варианты: **Да** или **Нет**.</span><span class="sxs-lookup"><span data-stu-id="29de8-171">Can be set to **Yes** or **No**.</span></span> <span data-ttu-id="29de8-172">Если выбран вариант "Да", необходимо указать допустимое значение даты и времени.</span><span class="sxs-lookup"><span data-stu-id="29de8-172">A valid date and time are to be provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="29de8-173">Если модуль runbook необходимо запускать чаще, чем каждый час, необходимо создать несколько расписаний с разными интервалами (то есть 15, 30, 45 минут после часа)</span><span class="sxs-lookup"><span data-stu-id="29de8-173">If you need to have a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after the hour)</span></span>

![Шаг 9.][9]

### <a name="step-3"></a><span data-ttu-id="29de8-175">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="29de8-175">Step 3</span></span>

<span data-ttu-id="29de8-176">Нажмите кнопку "Сохранить", чтобы сохранить расписание для модуля runbook.</span><span class="sxs-lookup"><span data-stu-id="29de8-176">Click Save to save the schedule to the runbook.</span></span>

![Шаг 10][10]

## <a name="next-steps"></a><span data-ttu-id="29de8-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29de8-178">Next steps</span></span>

<span data-ttu-id="29de8-179">Чтобы узнать, как интегрировать средство устранения неполадок Наблюдателя за сетями со службой автоматизации Azure, научитесь активировать захват пакетов на основе предупреждений виртуальной машины. Инструкции см. в статье о том, как [с помощью Наблюдателя за сетями Azure создать захват пакетов, который активируется оповещениями](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="29de8-179">Now that you have an understanding on how to integrate Network Watcher troubleshooting with Azure Automation, learn how to trigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

<!-- images -->
[scenario]: ./media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: ./media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: ./media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: ./media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: ./media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: ./media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: ./media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: ./media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: ./media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: ./media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: ./media/network-watcher-monitor-with-azure-automation/figure10.png
