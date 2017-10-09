---
title: "aaaStarting и остановки виртуальных машин с автоматизацией Azure — рабочий процесс PowerShell | Документы Microsoft"
description: "Сценарий автоматизации Azure, включая модули Runbook toostart и остановить классических виртуальных машин графической версии."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Сценарий для службы автоматизации Azure: запуск и остановка виртуальных машин
Этот сценарий автоматизации Azure включает модули Runbook toostart и остановить классических виртуальных машин.  Этот сценарий можно использовать для следующих hello:  

* Модули Runbook hello без каких-либо используйте в собственной среде.
* Измените функциональность tooperform пользовательские модули Runbook hello.  
* Вызывает hello модулей Runbook из другого модуля runbook как часть общего решения.
* Используйте модули Runbook hello как разработка основные понятия runbook toolearn учебники.

> [!div class="op_single_selector"]
> * [Графический](automation-solution-startstopvm-graphical.md)
> * [Рабочий процесс PowerShell](automation-solution-startstopvm-psworkflow.md)
> 
> 

Это hello версии runbook рабочего процесса PowerShell этого сценария. Также есть статья о [модулях Runbook с графическим интерфейсом](automation-solution-startstopvm-graphical.md).

## <a name="getting-hello-scenario"></a>Начало сценария hello
Этот сценарий состоит из двух Runbook рабочего процесса PowerShell, которые можно загрузить из hello ссылкам.  В разделе hello [графической версии](automation-solution-startstopvm-graphical.md) этого сценария для графических модулей Runbook toohello ссылки.

| Модуль Runbook | Ссылка | Тип | Описание |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[Запуск классических виртуальных машин Azure](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |Рабочий процесс PowerShell |Запуск всех классических виртуальных машин в подписке Azure или всех виртуальных машин с определенным именем службы. |
| Stop-AzureVMs |[Остановка классических виртуальных машин Azure](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |Рабочий процесс PowerShell |Остановка всех классических виртуальных машин в учетной записи службы автоматизации или всех виртуальных машин с определенным именем службы. |

## <a name="installing-and-configuring-hello-scenario"></a>Установка и настройка сценария hello
### <a name="1-install-hello-runbooks"></a>1. Установка модулей Runbook hello
После загрузки модулей Runbook hello, их можно импортировать с помощью процедуры hello в [импорт модуля Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook).

### <a name="2-review-hello-description-and-requirements"></a>2. Просмотрите описание hello и требования
модули Runbook Hello включать текст комментария справки, который включает в себя описание и необходимые активы.  Можно также получить hello же сведения из этой статьи.

### <a name="3-configure-assets"></a>3. Настройка ресурсов
Hello Runbook требуют hello следующие ресурсы, которые необходимо создать и заполнить с соответствующими значениями.

| Тип ресурса | Имя ресурса | Описание |
|:--- |:--- |:--- |:--- |
| Учетные данные |AzureCredential |Содержит учетные данные учетной записи, которая имеет полномочия toostart и остановки виртуальных машин в hello подписки Azure.  Кроме того, можно указать другой ресурс учетных данных в hello **учетные данные** параметр hello **Add-AzureAccount** действия. |
| Переменная |AzureSubscriptionId |Содержит идентификатор подписки hello подписки Azure. |

## <a name="using-hello-scenario"></a>С помощью сценария hello
### <a name="parameters"></a>Параметры
Каждый Hello Runbook имеют hello следующие параметры.  Вам потребуется указать значения всех обязательных параметров и, при необходимости, указать значения дополнительных параметров.

| Параметр | Тип | Обязательно | Описание |
|:--- |:--- |:--- |:--- |
| ServiceName |string |Нет |Если значение указано, запускаются или останавливаются все виртуальные машины с таким именем службы.  Если значение не указано, затем классических виртуальных машин в hello подписки Azure запуска или остановки. |
| AzureSubscriptionIdAssetName |string |Нет |Содержит имя hello hello [переменной активов](#installing-and-configuring-the-scenario) , содержащее идентификатор подписки hello подписки Azure.  Если значение не указано, используется значение *AzureSubscriptionId* . |
| AzureCredentialAssetName |string |Нет |Содержит имя hello hello [актива учетных данных](#installing-and-configuring-the-scenario) , содержащий hello учетные данные для hello runbook toouse.  Если не указать это значение, будет использоваться значение *AzureCredential* . |

### <a name="starting-hello-runbooks"></a>Запуск модулей Runbook hello
Можно использовать любой из методов hello в [запуск runbook в автоматизации Azure](automation-starting-a-runbook.md) toostart либо Runbook hello в этом сценарии.

Следующие примеры команд Hello использует Windows PowerShell toorun **StartAzureVMs** toostart все виртуальные машины с именем службы hello *MyVMService*.

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>Выходные данные
модули Runbook Hello будет [выводить сообщение](automation-runbook-output-and-messages.md) для каждой виртуальной машины, указывающее, ли hello Пуск или инструкция stop успешно отправлен.  Можно найти конкретную строку в результате hello toodetermine hello выходные данные для каждого модуля runbook.  в hello в следующей таблице перечислены строки возможного выхода Hello.

| Модуль Runbook | Условие | Сообщение |
|:--- |:--- |:--- |
| Start-AzureVMs |Виртуальная машина уже запущена |MyVM is already running |
| Start-AzureVMs |Запрос на запуск виртуальной машины успешно отправлен |MyVM has been started |
| Start-AzureVMs |Не удалось выполнить запрос запуска виртуальной машины |Не удалось выполнить MyVM toostart |
| Stop-AzureVMs |Виртуальная машина уже остановлена. |MyVM is already stopped |
| Stop-AzureVMs |Запрос на остановку виртуальной машины успешно отправлен. |MyVM остановлена. |
| Stop-AzureVMs |Не удалось отправить запрос на остановку виртуальной машины. |Не удалось выполнить MyVM toostop |

Например, следующий фрагмент кода из модуля hello пытается toostart все виртуальные машины с именем службы hello *MyServiceName*.  Если любой из hello запускается сбоев запросов, можно предпринять действия при возникновении ошибки.

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>Подробный разбор
Ниже приведен подробный разбор Runbook hello в этом сценарии.  Эти сведения можно использовать tooeither Настройка модулей Runbook hello или просто toolearn из них для создания собственных сценариев автоматизации.

### <a name="parameters"></a>Параметры
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

Hello рабочий процесс запускается путем получения значения hello для hello [входных параметров](#using-the-scenario).  Если имена ресурсов hello не указаны, используются имена по умолчанию.

### <a name="output"></a>Выходные данные
    # Returns strings with status messages
    [OutputType([String])]

Эта строка объявляет, что представляет собой строку hello выходные данные модуля runbook hello.  Это не является обязательным, но рекомендуется для при использовании hello runbook как [дочернего модуля runbook](automation-child-runbooks.md) , чтобы родительский модуль runbook знали вывода hello введите tooexpect.

### <a name="authentication"></a>Аутентификация
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

следующие строки Hello задать hello [учетные данные](automation-credentials.md) и подписку Azure, которая будет использоваться для оставшихся hello hello runbook.
Сперва мы используем **Get-AutomationPSCredential** tooget hello актива, который содержит учетные данные hello с доступом toostart и остановки виртуальных машин в hello подписки Azure. **-AzureAccount** затем использует этот учетных данных ОС tooset hello.  выходные данные Hello назначается фиктивный tooa, чтобы он не включен в выходные данные runbook hello.  

Hello переменной активов с Идентификатором затем извлекается с подпиской hello **Get-AutomationVariable** и hello подписки с **Select-AzureSubscription**.

### <a name="get-vms"></a>Получение виртуальных машин
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-AzureVM** — используется tooretrieve hello виртуальных машин hello runbook будут работать с.  Если значение указано в hello **ServiceName** входных данных извлекаются переменной, а затем только hello виртуальных машин с таким именем службы.  Если значение **ServiceName** пустое, извлекаются все виртуальные машины.

### <a name="startstop-virtual-machines-and-send-output"></a>Запуск и остановка виртуальных машин, отправка выходных данных
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

следующие строки Hello пошаговое выполнение каждой виртуальной машины.  Здравствуйте, сначала **PowerState** hello виртуальной машины — checked toosee, если он уже работает или остановлена в зависимости от hello runbook.  Если он уже находится в состоянии целевой hello, сообщение отправляется toooutput и заканчивается runbook hello.  В противном случае нажмите **Start-AzureVM** или **Stop-AzureVM** используется tooattempt toostart или остановки hello виртуальная машина с результатом hello hello запрос хранимых tooa переменной.  Затем сообщение отправляется указание toooutput ли toostart запрос hello или stop был успешно отправлен.

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о работе с дочерними модулями Runbook в разделе [дочерние модули Runbook в автоматизации Azure](automation-child-runbooks.md)
* Дополнительные сведения о toolearn выходных сообщений во время выполнения runbook и toohelp ведение журнала устранения неполадок см. в разделе [Runbook выходные данные и сообщения в службе автоматизации Azure](automation-runbook-output-and-messages.md)

