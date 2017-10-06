---
title: "aaaCollecting данных аналитики журналов с runbook в автоматизации Azure | Документы Microsoft"
description: "Пошаговые руководства, проходит через создание модуля runbook в автоматизации Azure toocollect данные в репозиторий OMS hello для анализа службой аналитики журналов."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: operations-management-suite
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2017
ms.author: bwren
ms.openlocfilehash: e644dc3ef20fb1e930cae02e0fd44ccca31dc13d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="collect-data-in-log-analytics-with-an-azure-automation-runbook"></a>Сбор данных в Log Analytics с использованием модуля runbook в службе автоматизации Azure
В Log Analytics можно собрать значительный объем данных из различных источников, включая [источники данных](../log-analytics/log-analytics-data-sources.md) в агентах и [данные, собранные в Azure](../log-analytics/log-analytics-azure-storage.md).  Существуют сценарии, хотя которых требуется toocollect данных, не доступны через эти стандартные источники.  В этих случаях можно использовать hello [HTTP API-Интерфейс сборщика данных](../log-analytics/log-analytics-data-collector-api.md) tooLog toowrite данных аналитики из любого клиента REST API.  Общие tooperform метод runbook в службе автоматизации Azure использует эту коллекцию.   

Этого учебника вы научитесь hello процесс создания и планирования runbook в автоматизации Azure toowrite данных tooLog Analytics.


## <a name="prerequisites"></a>Предварительные требования
Данный сценарий требует hello следующих ресурсов, настроенных в вашей подписке Azure.  Их можно использовать с бесплатной учетной записью.

- [Рабочая область Log Analytics](../log-analytics/log-analytics-get-started.md).
- [Учетная запись службы автоматизации Azure](../automation/automation-offering-get-started.md).

## <a name="overview-of-scenario"></a>Обзор сценария
В этом руководстве вы создадите модуль runbook, который собирает сведения о заданиях службы автоматизации.  Runbook в автоматизации Azure, реализуются с помощью PowerShell, поэтому начнем с создания и тестирования сценария в редактор Azure Automation hello.  Убедившись, что собираются hello необходимые сведения, будет записывать, tooLog данных аналитики и проверять hello пользовательского типа данных.  Наконец вы создадите расписание toostart hello runbook через регулярные интервалы.

> [!NOTE]
> Вы можете настроить службы автоматизации Azure toosend задания сведения tooLog Analytics без этого модуля runbook.  Этот сценарий является главным образом используется toosupport учебника hello и рекомендуется отправлять hello данных tooa тестовой рабочей области.  


## <a name="1-install-data-collector-api-module"></a>1. Установка модуля API сборщика данных
Каждый [запрос от hello HTTP API-Интерфейс сборщика данных](../log-analytics/log-analytics-data-collector-api.md#create-a-request) должен быть отформатирован должным образом и включать заголовок авторизации.  Это можно сделать в модуле runbook, но могут снизить hello объем кода, необходимо с помощью модуля, который упрощает этот процесс.  Один модуль, который можно использовать является [OMSIngestionAPI модуль](https://www.powershellgallery.com/packages/OMSIngestionAPI) в коллекции PowerShell hello.

toouse [модуль](../automation/automation-integration-modules.md) в модуле runbook, он должен быть установлен в вашей учетной записи автоматизации.  Здравствуйте, любого модуля runbook в hello учетную запись можно использовать функции в модуле hello.  Вы можете установить новый модуль, последовательно выбрав в своей учетной записи службы автоматизации **Ресурсы** > **Модули** > **Добавить модуль**.  

Hello коллекции PowerShell хотя предоставляет быстрый параметр toodeploy модуля напрямую автоматизации tooyour учетной записи, поэтому этот параметр можно использовать для этого учебника.  

![Модуль OMSIngestionAPI](media/operations-management-suite-runbook-datacollect/OMSIngestionAPI.png)

1. Go слишком[коллекции PowerShell](https://www.powershellgallery.com/).
2. Введите в строке поиска **OMSIngestionAPI**.
3. Щелкните hello **tooAzure автоматизации развертывания** кнопки.
4. Выберите учетную запись автоматизации и нажмите кнопку **ОК** tooinstall hello модуля.


## <a name="2-create-automation-variables"></a>2. Создание переменных службы автоматизации
[Переменные службы автоматизации](..\automation\automation-variables.md) содержат значения, которые могут использоваться всеми модулями runbook в учетной записи службы автоматизации.  Они делают модулей Runbook, более гибкую, позволяя toochange эти значения, не изменяя hello фактическое runbook. Каждый запрос из hello HTTP API-Интерфейс сборщика данных требует hello идентификатор и ключ рабочей области OMS hello и ресурсы переменных являются идеальной toostore эти сведения.  

![Переменные](media/operations-management-suite-runbook-datacollect/variables.png)

1. В hello портал Azure перейдите tooyour учетной записи автоматизации.
2. Выберите **Переменные** в разделе **Общие ресурсы**.
2. Нажмите кнопку **добавить переменную** и создайте две переменные hello в hello в следующей таблице.

| Свойство | Значение идентификатора рабочей области | Значение ключа рабочей области |
|:--|:--|:--|
| Имя | WorkspaceId | WorkspaceKey |
| Тип | Строка | Строка |
| Значение | Вставьте идентификатор рабочей области рабочей области аналитики журналов hello. | Вставить с помощью hello первичный или вторичный ключ рабочей области аналитики журналов. |
| зашифрованные; | Нет | Да |



## <a name="3-create-runbook"></a>3. Создание модуля Runbook

Служба автоматизации Azure имеет редактор hello портала, где можно изменить и протестировать модуль runbook.  У вас есть hello параметр toouse hello скрипта редактор toowork с [PowerShell непосредственно](../automation/automation-edit-textual-runbook.md) или [создать графический runbook](../automation/automation-graphical-authoring-intro.md).  В этом руководстве мы будем работать со скриптом PowerShell. 

![Изменение модуля runbook](media/operations-management-suite-runbook-datacollect/edit-runbook.png)

1. Перейдите tooyour учетной записи автоматизации.  
2. Щелкните **Модули Runbook** > **Добавить Runbook** > **Создание нового модуля Runbook**.
3. Введите имя runbook hello, **задания для автоматизации сбор**.  Выберите тип runbook hello **PowerShell**.
4. Нажмите кнопку **создать** toocreate hello runbook и начала hello редактора.
5. Скопируйте и вставьте следующий код в hello runbook hello.  См. объяснение кода hello toohello комментарии в скрипте hello.
    
        # Get information required for hello automation account from parameter values when hello runbook is started.
        Param
        (
            [Parameter(Mandatory = $True)]
            [string]$resourceGroupName,
            [Parameter(Mandatory = $True)]
            [string]$automationAccountName
        )
        
        # Authenticate toohello Automation account using hello Azure connection created when hello Automation account was created.
        # Code copied from hello runbook AzureAutomationTutorial.
        $connectionName = "AzureRunAsConnection"
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         
        Add-AzureRmAccount `
            -ServicePrincipal `
            -TenantId $servicePrincipalConnection.TenantId `
            -ApplicationId $servicePrincipalConnection.ApplicationId `
            -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
        
        # Set hello $VerbosePreference variable so that we get verbose output in test environment.
        $VerbosePreference = "Continue"
        
        # Get information required for Log Analytics workspace from Automation variables.
        $customerId = Get-AutomationVariable -Name 'WorkspaceID'
        $sharedKey = Get-AutomationVariable -Name 'WorkspaceKey'
        
        # Set hello name of hello record type.
        $logType = "AutomationJob"
        
        # Get hello jobs from hello past hour.
        $jobs = Get-AzureRmAutomationJob -ResourceGroupName $resourceGroupName -AutomationAccountName $automationAccountName -StartTime (Get-Date).AddHours(-1)
        
        if ($jobs -ne $null) {
            # Convert hello job data toojson
            $body = $jobs | ConvertTo-Json
        
            # Write hello body tooverbose output so we can inspect it if verbose logging is on for hello runbook.
            Write-Verbose $body
        
            # Send hello data tooLog Analytics.
            Send-OMSAPIIngestionFile -customerId $customerId -sharedKey $sharedKey -body $body -logType $logType -TimeStampField CreationTime
        }


## <a name="4-test-runbook"></a>4. Тестирование модуля runbook
Служба автоматизации Azure включает в себя среду слишком[тестирования модуля runbook](../automation/automation-testing-runbook.md) перед его публикацией.  Можно проверять hello данными, собранными hello runbook и убедитесь, что она записывает tooLog Analytics должным образом, прежде чем публиковать их tooproduction. 
 
![Тестирование модуля runbook](media/operations-management-suite-runbook-datacollect/test-runbook.png)

6. Нажмите кнопку **Сохранить** toosave hello runbook.
1. Нажмите кнопку **области тестов** tooopen hello runbook в тестовой среде hello.
3. Так как модуль runbook имеет параметры, вы tooenter запрашиваемые значения для них.  Введите имя группы ресурсов hello hello и автоматизации hello учетной записи, ваши данные задания постоянной toocollect от.
4. Нажмите кнопку **запустить** toohello запустить hello runbook.
3. Hello runbook будет запущен с состоянием **в очереди** перед его отправкой слишком**под управлением**.  
3. Hello runbook отображать подробные выходные данные с заданиями hello, собранные в формате json.  Если в списке нет заданий, затем возникли нет заданий, созданных в учетной записи автоматизации hello в hello последний час.  Попробуйте запустить любой runbook в учетной записи автоматизации hello, а затем снова выполните тест hello.
4. Убедитесь, что выходные данные hello не показывает все ошибки в hello отправки команды tooLog Analytics.  Необходимо иметь следующее сообщение аналогичные toohello.

    ![Выходные данные POST](media/operations-management-suite-runbook-datacollect/post-output.png)

## <a name="5-verify-records-in-log-analytics"></a>5. Проверка записей в Log Analytics
После завершения hello runbook в тесте, и вы проверили hello выходные данные были успешно получены, можно проверить, что записи hello были созданы с помощью [поиска журналов в службе анализа журналов](../log-analytics/log-analytics-log-searches.md).

![Выходные данные журналов](media/operations-management-suite-runbook-datacollect/log-output.png)

1. В hello портал Azure выберите рабочую область службы анализа журналов.
2. Щелкните **Поиск по журналам**.
3. Тип hello следующую команду `Type=AutomationJob_CL` и нажмите кнопку поиска hello. Обратите внимание, что тип записи hello включает _CL, который не указан в скрипте hello.  Этот суффикс является автоматически добавленных toohello журнала типа tooindicate, он является типом пользовательского журнала.
4. Вы увидите одну или несколько записей, возвращаемых, которое указывает, что hello runbook работает надлежащим образом.


## <a name="6-publish-hello-runbook"></a>6. Публикация hello runbook
После проверки правильности работы этого модуля hello, вам потребуется toopublish его, чтобы можно было запустить в рабочей среде.  Можно продолжить tooedit и тестирования hello runbook без изменения hello опубликованной версии.  

![Публикация модуля runbook](media/operations-management-suite-runbook-datacollect/publish-runbook.png)

1. Возвращает tooyour учетной записи автоматизации.
2. Щелкните **Модули Runbook** и выберите **Collect-Automation-jobs**.
3. Щелкните **Правка** и выберите **Опубликовать**.
4. Нажмите кнопку **Да** при задаваемые tooverify требуется toooverwrite hello ранее опубликованной версии.

## <a name="7-set-logging-options"></a>7. Настройка параметров ведения журнала 
Для проверки, были может tooview [подробный вывод](../automation/automation-runbook-output-and-messages.md#message-streams) так как значение переменной hello $VerbosePreference в скрипте hello.  Для рабочей среды нужны свойства ведения журнала hello tooset для hello runbook, если требуется подробный вывод tooview.  Для runbook hello, используемые в этом учебнике это будет отображаться отправляемых tooLog аналитика данных json hello.

![Ведение журнала и трассировка](media/operations-management-suite-runbook-datacollect/logging.png)

1. В модуле runbook hello свойств выберите **ведения журнала и трассировки** под **параметры Runbook**.
2. Изменение параметров hello для **ведение журнала подробных сообщений** слишком**на**.
3. Щелкните **Сохранить**.

## <a name="8-schedule-runbook"></a>8. Создание расписания для модуля runbook
Hello наиболее распространенных способа toostart runbook, который собирает данные наблюдения является tooschedule его toorun автоматически.  Это делается путем создания [расписания в службе автоматизации Azure](../automation/automation-schedules.md) , подключив ее tooyour runbook.

![Создание расписания для модуля runbook](media/operations-management-suite-runbook-datacollect/schedule-runbook.png)

1. В свойствах hello модуль runbook, выберите **расписания** под **ресурсов**.
2. Нажмите кнопку **Добавить расписание** > **связать runbook расписания tooyour** > **создать новое расписание**.
5. Тип в hello следующие значения для hello расписания и нажмите кнопку **создать**.

| Свойство | Значение |
|:--|:--|
| Имя | AutomationJobs-Hourly |
| Запуск | Выберите любое время, по крайней мере на 5 минут последние hello текущее время. |
| Периодичность | Повторение |
| Повторять каждые | 1 час |
| Срок действия | Нет |

После создания расписания hello, вам потребуется значения параметров tooset hello, которые будут использоваться при каждом запуске hello runbook этого расписания.

6. Щелкните **Настройка параметров и настроек запуска**.
7. Укажите значения для **ResourceGroupName** и **AutomationAccountName**.
8. Нажмите кнопку **ОК**. 

## <a name="9-verify-runbook-starts-on-schedule"></a>9. Проверка запуска модуля runbook по расписанию
При каждом запуске модуля runbook [создается задание](../automation/automation-runbook-execution.md), и все выходные данные записываются в журнал.  На самом деле это сбор и тех же заданий, которые hello runbook hello.  Вы можете подтвердить этого модуля hello запускается как положено, проверив hello задания для модуля hello после истечения времени запуска hello расписании hello.

![Задания](media/operations-management-suite-runbook-datacollect/jobs.png)

1. В свойствах hello модуль runbook, выберите **заданий** под **ресурсов**.
2. Вы увидите список заданий для каждого модуля runbook hello времени была начата.
3. Выберите одну из tooview hello задания сведений о нем.
4. Щелкните **все журналы** tooview hello вывод hello runbook и журналы.
5. Прокрутите toofind нижней toohello входа аналогичные toohello образ ниже.<br>![Подробная информация](media/operations-management-suite-runbook-datacollect/verbose.png)
6. Щелкните эту запись tooview hello подробные данные json, который был отправлен tooLog Analytics.



## <a name="next-steps"></a>Дальнейшие действия
- Используйте [конструктор представлений](../log-analytics/log-analytics-view-designer.md) toocreate отображение представления hello собранными toohello анализа журналов хранилища данных.
- Модуль runbook в пакет [решение для управления](operations-management-suite-solutions-creating.md) toodistribute toocustomers.
- Дополнительные сведения о [Log Analytics](https://docs.microsoft.com/azure/log-analytics/).
- Дополнительные сведения о [службе автоматизации Azure](https://docs.microsoft.com/azure/automation/).
- Дополнительные сведения о hello [HTTP API-Интерфейс сборщика данных](../log-analytics/log-analytics-data-collector-api.md).
