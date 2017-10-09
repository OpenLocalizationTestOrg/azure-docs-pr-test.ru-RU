---
title: "aaaMonitor VPN-шлюзов с устранением неполадок Наблюдатель сети Azure | Документы Microsoft"
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
ms.openlocfilehash: a607d0c862ea1be63c687717f0c5dc137db58a43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="b8cd8-103">Мониторинг VPN-шлюзов с помощью средства устранения неполадок Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="b8cd8-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="b8cd8-104">Получить полное представление на производительность сети — критический tooprovide toocustomers надежного обмена.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-104">Gaining deep insights on your network performance is critical tooprovide reliable services toocustomers.</span></span> <span data-ttu-id="b8cd8-105">Он является таким образом критических toodetect условий сбоя сети быстро и выполнить действия по исправлению toomitigate hello возник простой.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-105">It is therefore critical toodetect network outage conditions quickly and take corrective action toomitigate hello outage condition.</span></span> <span data-ttu-id="b8cd8-106">Служба автоматизации Azure позволяет tooimplement и выполнять задачу программным образом через модулей Runbook.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-106">Azure Automation enables you tooimplement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="b8cd8-107">С помощью службы автоматизации Azure вы можете выполнять упреждающий непрерывный мониторинг сети и создавать оповещения.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="b8cd8-108">Сценарий</span><span class="sxs-lookup"><span data-stu-id="b8cd8-108">Scenario</span></span>

<span data-ttu-id="b8cd8-109">сценарием Hello в hello после изображения является многоуровневое приложение с на локальные подключения, с помощью шлюза VPN и туннеля.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-109">hello scenario in hello following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="b8cd8-110">Счет приветствия VPN-шлюз работает и под управлением — критический toohello производительности приложений.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-110">Ensuring hello VPN Gateway is up and running is critical toohello applications performance.</span></span>

<span data-ttu-id="b8cd8-111">Runbook создается с toocheck скрипт для hello VPN-туннель, с помощью API Устранение неполадок ресурсов toocheck hello туннеля состояние подключения состояние соединения.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-111">A runbook is created with a script toocheck for connection status of hello VPN tunnel, using hello Resource Troubleshooting API toocheck for connection tunnel status.</span></span> <span data-ttu-id="b8cd8-112">Если hello неисправен, триггер электронной почты будет отправлено tooadministrators.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-112">If hello status is not healthy, an email trigger is sent tooadministrators.</span></span>

![Пример сценария][scenario]

<span data-ttu-id="b8cd8-114">Вы узнаете:</span><span class="sxs-lookup"><span data-stu-id="b8cd8-114">This scenario will:</span></span>

- <span data-ttu-id="b8cd8-115">Создание runbook вызывающему Привет `Start-AzureRmNetworkWatcherResourceTroubleshooting` состояние подключения tootroubleshoot командлета</span><span class="sxs-lookup"><span data-stu-id="b8cd8-115">Create a runbook calling hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet tootroubleshoot connection status</span></span>
- <span data-ttu-id="b8cd8-116">Связать runbook toohello расписания</span><span class="sxs-lookup"><span data-stu-id="b8cd8-116">Link a schedule toohello runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b8cd8-117">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="b8cd8-117">Before you begin</span></span>

<span data-ttu-id="b8cd8-118">Прежде чем начать этот сценарий, необходимо иметь hello следующие необходимые компоненты:</span><span class="sxs-lookup"><span data-stu-id="b8cd8-118">Before you start this scenario, you must have hello following pre-requisites:</span></span>

- <span data-ttu-id="b8cd8-119">Учетная запись службы автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-119">An Azure automation account in Azure.</span></span> <span data-ttu-id="b8cd8-120">Убедитесь, что учетная запись автоматизации hello последних модулей hello и также содержит модуль AzureRM.Network hello.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-120">Ensure that hello automation account has hello latest modules and also has hello AzureRM.Network module.</span></span> <span data-ttu-id="b8cd8-121">модуль AzureRM.Network Hello доступен в коллекции модулей hello, если требуется tooadd его tooyour учетной записи автоматизации.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-121">hello AzureRM.Network module is available in hello module gallery if you need tooadd it tooyour automation account.</span></span>
- <span data-ttu-id="b8cd8-122">Набор учетных данных, настроенных в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-122">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="b8cd8-123">См. дополнительные сведения о [безопасности службы автоматизации Azure](../automation/automation-security-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8cd8-123">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="b8cd8-124">Допустимый SMTP-сервер (Office 365, локальный или другой адрес электронной почты) и учетные данные, определенные в службе автоматизации Azure.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-124">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="b8cd8-125">Настроенный шлюз виртуальной сети в Azure.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-125">A configured Virtual Network Gateway in Azure.</span></span>
- <span data-ttu-id="b8cd8-126">Регистрирует существующую учетную запись хранения с существующие hello toostore контейнера.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-126">An existing storage account with an existing container toostore hello logs in.</span></span>

> [!NOTE]
> <span data-ttu-id="b8cd8-127">Инфраструктура Hello, показано hello предшествующий образ предназначен для иллюстрации и не создаются hello шаги, описанные в данной статье.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-127">hello infrastructure depicted in hello preceding image is for illustration purposes and are not created with hello steps contained in this article.</span></span>

### <a name="create-hello-runbook"></a><span data-ttu-id="b8cd8-128">Создание hello runbook</span><span class="sxs-lookup"><span data-stu-id="b8cd8-128">Create hello runbook</span></span>

<span data-ttu-id="b8cd8-129">Hello первый шаг tooconfiguring hello пример является toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-129">hello first step tooconfiguring hello example is toocreate hello runbook.</span></span> <span data-ttu-id="b8cd8-130">В этом примере используется учетная запись запуска от имени.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-130">This example uses a run-as account.</span></span> <span data-ttu-id="b8cd8-131">Посетите toolearn об учетных записях запуска от имени, [проверки подлинности модулей Runbook с помощью учетной записи запуска от имени Azure](../automation/automation-sec-configure-azure-runas-account.md)</span><span class="sxs-lookup"><span data-stu-id="b8cd8-131">toolearn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md)</span></span>

### <a name="step-1"></a><span data-ttu-id="b8cd8-132">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="b8cd8-132">Step 1</span></span>

<span data-ttu-id="b8cd8-133">Перейдите tooAzure автоматизации в hello [портал Azure](https://portal.azure.com) и нажмите кнопку **модулей Runbook**</span><span class="sxs-lookup"><span data-stu-id="b8cd8-133">Navigate tooAzure Automation in hello [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![Обзор учетной записи службы автоматизации][1]

### <a name="step-2"></a><span data-ttu-id="b8cd8-135">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="b8cd8-135">Step 2</span></span>

<span data-ttu-id="b8cd8-136">Нажмите кнопку **добавить модуль runbook** toostart процесс создания hello hello модуля Runbook.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-136">Click **Add a runbook** toostart hello creation process of hello runbook.</span></span>

![Колонка модулей runbook][2]

### <a name="step-3"></a><span data-ttu-id="b8cd8-138">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-138">Step 3</span></span>

<span data-ttu-id="b8cd8-139">В разделе **быстрое создание**, нажмите кнопку **создать новый runbook** toocreate hello runbook.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-139">Under **Quick Create**, click **Create a new runbook** toocreate hello runbook.</span></span>

![Колонка добавления модуля runbook][3]

### <a name="step-4"></a><span data-ttu-id="b8cd8-141">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-141">Step 4</span></span>

<span data-ttu-id="b8cd8-142">На этом шаге мы назовите hello runbook, в примере hello называется **Get VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-142">In this step, we give hello runbook a name, in hello example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="b8cd8-143">Он представляет собой описательное имя runbook важные toogive hello и рекомендуется присвоить ей имя, следующий стандартный стандарты именования PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-143">It is important toogive hello runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="b8cd8-144">Тип runbook Hello в данном примере — **PowerShell**, hello есть параметры, Graphical рабочий процесс PowerShell и графический PowerShell рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-144">hello runbook type for this example is **PowerShell**, hello other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![Колонка модуля runbook][4]

### <a name="step-5"></a><span data-ttu-id="b8cd8-146">Шаг 5</span><span class="sxs-lookup"><span data-stu-id="b8cd8-146">Step 5</span></span>

<span data-ttu-id="b8cd8-147">На этом шаге hello runbook создается, hello, следующий пример кода предоставляет все hello код, необходимый для примера hello.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-147">In this step hello runbook is created, hello following code example provides all hello code needed for hello example.</span></span> <span data-ttu-id="b8cd8-148">Здравствуйте, элементы в коде hello, содержащие \<значение\> требуется toobe заменяются значениями hello из вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-148">hello items in hello code that contain \<value\> need toobe replaced with hello values from your subscription.</span></span>

<span data-ttu-id="b8cd8-149">Используйте следующие hello кода как щелкните **сохранить**</span><span class="sxs-lookup"><span data-stu-id="b8cd8-149">Use hello following code as click **Save**</span></span>

```PowerShell
# Set these variables toohello proper values for your environment
$o365AutomationCredential = "<Office 365 account>"
$fromEmail = "<from email address>"
$toEmail = "<tooemail address>"
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

# Get hello connection "AzureRunAsConnection "
$servicePrincipalConnection=Get-AutomationConnection -Name $runAsConnectionName

"Logging in tooAzure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context tooa specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $region }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name $vpnConnectionName -ResourceGroupName $vpnConnectionResourceGroup
$sa = Get-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $storageAccountResourceGroup 
$storagePath = "$($sa.PrimaryEndpoints.Blob)$($storageAccountContainer)"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath $storagePath

if($result.code -ne "Healthy")
    {
        $body = "Connection for $($connection.name) is: $($result.code) `n$($result.results[0].summary) `nView hello logs at $($storagePath) toolearn more."
        Write-Output $body
        $subject = "$($connection.name) Status"
        Send-MailMessage `
        -too$toEmail `
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

### <a name="step-6"></a><span data-ttu-id="b8cd8-150">Шаг 6</span><span class="sxs-lookup"><span data-stu-id="b8cd8-150">Step 6</span></span>

<span data-ttu-id="b8cd8-151">После сохранения hello runbook расписание должно быть связаны tooit tooautomate hello начала hello runbook.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-151">Once hello runbook is saved, a schedule must be linked tooit tooautomate hello start of hello runbook.</span></span> <span data-ttu-id="b8cd8-152">процесс toostart hello, нажмите кнопку **расписание**.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-152">toostart hello process, click **Schedule**.</span></span>

![Шаг 6][6]

## <a name="link-a-schedule-toohello-runbook"></a><span data-ttu-id="b8cd8-154">Связать runbook toohello расписания</span><span class="sxs-lookup"><span data-stu-id="b8cd8-154">Link a schedule toohello runbook</span></span>

<span data-ttu-id="b8cd8-155">Необходимо создать новое расписание.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-155">A new schedule must be created.</span></span> <span data-ttu-id="b8cd8-156">Нажмите кнопку **связать runbook расписания tooyour**.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-156">Click **Link a schedule tooyour runbook**.</span></span>

![Шаг 7][7]

### <a name="step-1"></a><span data-ttu-id="b8cd8-158">Шаг 1</span><span class="sxs-lookup"><span data-stu-id="b8cd8-158">Step 1</span></span>

<span data-ttu-id="b8cd8-159">На hello **расписания** колонка, щелкните **создания нового расписания**</span><span class="sxs-lookup"><span data-stu-id="b8cd8-159">On hello **Schedule** blade, click **Create a new schedule**</span></span>

![Шаг 8][8]

### <a name="step-2"></a><span data-ttu-id="b8cd8-161">Шаг 2</span><span class="sxs-lookup"><span data-stu-id="b8cd8-161">Step 2</span></span>

<span data-ttu-id="b8cd8-162">На hello **новое расписание** колонке заполните сведения о расписании hello.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-162">On hello **New Schedule** blade fill out hello schedule information.</span></span> <span data-ttu-id="b8cd8-163">Hello можно задать значения в hello после списка:</span><span class="sxs-lookup"><span data-stu-id="b8cd8-163">hello values that can be set are in hello following list:</span></span>

- <span data-ttu-id="b8cd8-164">**Имя** -hello понятное имя расписания hello.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-164">**Name** - hello friendly name of hello schedule.</span></span>
- <span data-ttu-id="b8cd8-165">**Описание** -описание расписания hello.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-165">**Description** - A description of hello schedule.</span></span>
- <span data-ttu-id="b8cd8-166">**Запускает** -это значение представляет собой сочетание даты, времени и часового пояса, составляющих запускается расписание hello время hello.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-166">**Starts** - This value is a combination of date, time, and time zone that make up hello time hello schedule triggers.</span></span>
- <span data-ttu-id="b8cd8-167">**Повторение** -это значение определяет hello расписания повторения.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-167">**Recurrence** - This value determines hello schedules repetition.</span></span>  <span data-ttu-id="b8cd8-168">Допустимые значения: **Однократно** или **Периодически**.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-168">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="b8cd8-169">**Повторять каждые** -hello интервал повторения расписания hello в часы, дни, недели или месяцы.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-169">**Recur every** - hello recurrence interval of hello schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="b8cd8-170">**Срок действия набора** -hello значение определяет, должно истечь hello расписание или нет.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-170">**Set Expiration** - hello value determines if hello schedule should expire or not.</span></span> <span data-ttu-id="b8cd8-171">Можно задать слишком**Да** или **нет**.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-171">Can be set too**Yes** or **No**.</span></span> <span data-ttu-id="b8cd8-172">Допустимые дату и время, toobe, если выбирается Да.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-172">A valid date and time are toobe provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="b8cd8-173">Если вам требуется toohave runbook запуска чаще, чем раз в час, несколько расписаний должны быть созданы различные интервалы (то есть, 15, 30, 45 минут после hello часа)</span><span class="sxs-lookup"><span data-stu-id="b8cd8-173">If you need toohave a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after hello hour)</span></span>

![Шаг 9.][9]

### <a name="step-3"></a><span data-ttu-id="b8cd8-175">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-175">Step 3</span></span>

<span data-ttu-id="b8cd8-176">Нажмите кнопку Сохранить toosave hello расписания toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="b8cd8-176">Click Save toosave hello schedule toohello runbook.</span></span>

![Шаг 10][10]

## <a name="next-steps"></a><span data-ttu-id="b8cd8-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8cd8-178">Next steps</span></span>

<span data-ttu-id="b8cd8-179">Теперь, чтобы получить основные сведения о том, как toointegrate Наблюдатель сети Устранение неполадок в службе автоматизации Azure, узнайте, как пакет tootrigger захватывает предупреждения виртуальной Машины, посетив [создать получения оповещений триггеру пакетов с Наблюдатель сети Azure](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="b8cd8-179">Now that you have an understanding on how toointegrate Network Watcher troubleshooting with Azure Automation, learn how tootrigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

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
