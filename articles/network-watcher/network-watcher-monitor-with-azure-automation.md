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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Мониторинг VPN-шлюзов с помощью средства устранения неполадок Наблюдателя за сетями

Получить полное представление на производительность сети — критический tooprovide toocustomers надежного обмена. Он является таким образом критических toodetect условий сбоя сети быстро и выполнить действия по исправлению toomitigate hello возник простой. Служба автоматизации Azure позволяет tooimplement и выполнять задачу программным образом через модулей Runbook. С помощью службы автоматизации Azure вы можете выполнять упреждающий непрерывный мониторинг сети и создавать оповещения.

## <a name="scenario"></a>Сценарий

сценарием Hello в hello после изображения является многоуровневое приложение с на локальные подключения, с помощью шлюза VPN и туннеля. Счет приветствия VPN-шлюз работает и под управлением — критический toohello производительности приложений.

Runbook создается с toocheck скрипт для hello VPN-туннель, с помощью API Устранение неполадок ресурсов toocheck hello туннеля состояние подключения состояние соединения. Если hello неисправен, триггер электронной почты будет отправлено tooadministrators.

![Пример сценария][scenario]

Вы узнаете:

- Создание runbook вызывающему Привет `Start-AzureRmNetworkWatcherResourceTroubleshooting` состояние подключения tootroubleshoot командлета
- Связать runbook toohello расписания

## <a name="before-you-begin"></a>Перед началом работы

Прежде чем начать этот сценарий, необходимо иметь hello следующие необходимые компоненты:

- Учетная запись службы автоматизации Azure. Убедитесь, что учетная запись автоматизации hello последних модулей hello и также содержит модуль AzureRM.Network hello. модуль AzureRM.Network Hello доступен в коллекции модулей hello, если требуется tooadd его tooyour учетной записи автоматизации.
- Набор учетных данных, настроенных в службе автоматизации Azure. См. дополнительные сведения о [безопасности службы автоматизации Azure](../automation/automation-security-overview.md).
- Допустимый SMTP-сервер (Office 365, локальный или другой адрес электронной почты) и учетные данные, определенные в службе автоматизации Azure.
- Настроенный шлюз виртуальной сети в Azure.
- Регистрирует существующую учетную запись хранения с существующие hello toostore контейнера.

> [!NOTE]
> Инфраструктура Hello, показано hello предшествующий образ предназначен для иллюстрации и не создаются hello шаги, описанные в данной статье.

### <a name="create-hello-runbook"></a>Создание hello runbook

Hello первый шаг tooconfiguring hello пример является toocreate hello runbook. В этом примере используется учетная запись запуска от имени. Посетите toolearn об учетных записях запуска от имени, [проверки подлинности модулей Runbook с помощью учетной записи запуска от имени Azure](../automation/automation-sec-configure-azure-runas-account.md)

### <a name="step-1"></a>Шаг 1

Перейдите tooAzure автоматизации в hello [портал Azure](https://portal.azure.com) и нажмите кнопку **модулей Runbook**

![Обзор учетной записи службы автоматизации][1]

### <a name="step-2"></a>Шаг 2

Нажмите кнопку **добавить модуль runbook** toostart процесс создания hello hello модуля Runbook.

![Колонка модулей runbook][2]

### <a name="step-3"></a>Шаг 3.

В разделе **быстрое создание**, нажмите кнопку **создать новый runbook** toocreate hello runbook.

![Колонка добавления модуля runbook][3]

### <a name="step-4"></a>Шаг 4.

На этом шаге мы назовите hello runbook, в примере hello называется **Get VPNGatewayStatus**. Он представляет собой описательное имя runbook важные toogive hello и рекомендуется присвоить ей имя, следующий стандартный стандарты именования PowerShell. Тип runbook Hello в данном примере — **PowerShell**, hello есть параметры, Graphical рабочий процесс PowerShell и графический PowerShell рабочего процесса.

![Колонка модуля runbook][4]

### <a name="step-5"></a>Шаг 5

На этом шаге hello runbook создается, hello, следующий пример кода предоставляет все hello код, необходимый для примера hello. Здравствуйте, элементы в коде hello, содержащие \<значение\> требуется toobe заменяются значениями hello из вашей подписки.

Используйте следующие hello кода как щелкните **сохранить**

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

### <a name="step-6"></a>Шаг 6

После сохранения hello runbook расписание должно быть связаны tooit tooautomate hello начала hello runbook. процесс toostart hello, нажмите кнопку **расписание**.

![Шаг 6][6]

## <a name="link-a-schedule-toohello-runbook"></a>Связать runbook toohello расписания

Необходимо создать новое расписание. Нажмите кнопку **связать runbook расписания tooyour**.

![Шаг 7][7]

### <a name="step-1"></a>Шаг 1

На hello **расписания** колонка, щелкните **создания нового расписания**

![Шаг 8][8]

### <a name="step-2"></a>Шаг 2

На hello **новое расписание** колонке заполните сведения о расписании hello. Hello можно задать значения в hello после списка:

- **Имя** -hello понятное имя расписания hello.
- **Описание** -описание расписания hello.
- **Запускает** -это значение представляет собой сочетание даты, времени и часового пояса, составляющих запускается расписание hello время hello.
- **Повторение** -это значение определяет hello расписания повторения.  Допустимые значения: **Однократно** или **Периодически**.
- **Повторять каждые** -hello интервал повторения расписания hello в часы, дни, недели или месяцы.
- **Срок действия набора** -hello значение определяет, должно истечь hello расписание или нет. Можно задать слишком**Да** или **нет**. Допустимые дату и время, toobe, если выбирается Да.

> [!NOTE]
> Если вам требуется toohave runbook запуска чаще, чем раз в час, несколько расписаний должны быть созданы различные интервалы (то есть, 15, 30, 45 минут после hello часа)

![Шаг 9.][9]

### <a name="step-3"></a>Шаг 3.

Нажмите кнопку Сохранить toosave hello расписания toohello runbook.

![Шаг 10][10]

## <a name="next-steps"></a>Дальнейшие действия

Теперь, чтобы получить основные сведения о том, как toointegrate Наблюдатель сети Устранение неполадок в службе автоматизации Azure, узнайте, как пакет tootrigger захватывает предупреждения виртуальной Машины, посетив [создать получения оповещений триггеру пакетов с Наблюдатель сети Azure](network-watcher-alert-triggered-packet-capture.md).

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
