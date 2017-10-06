---
title: "aaaForward tooOMS данных задания службы автоматизации Azure Log Analytics | Документы Microsoft"
description: "В этой статье показано, как toosend задания состояния и runbook задание потоки управления и анализа журналов Operations Management Suite tooMicrosoft toodeliver Дополнительные подробные сведения."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: c12724c6-01a9-4b55-80ae-d8b7b99bd436
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/2017
ms.author: magoedte
ms.openlocfilehash: e78b6c6677d6502711ce828e2d32b7a91922ae26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="forward-job-status-and-job-streams-from-automation-toolog-analytics-oms"></a>Пересылать состояние задания и задания потоков из автоматизации tooLog Analytics (OMS)
Автоматизация может отправлять runbook задания состояние задания потоки tooyour анализа журналов Microsoft Operations Management Suite (OMS) рабочей области и.  Заносит в журнал заданий и потоки задания, отображаются в hello портал Azure, либо с помощью PowerShell, отдельные задания, и позволяет tooperform простой исследования. С помощью Log Analytics теперь можно:

* получить информацию о заданиях службы автоматизации;
* активировать отправку электронного сообщения или оповещения в соответствии с состоянием задания Runbook (например, сбой или приостановка);
* создавать сложные запросы для потоков заданий;
* коррелировать задания и учетные записи службы автоматизации;
* визуализировать журнал задания по прошествии времени.     

## <a name="prerequisites-and-deployment-considerations"></a>Предварительные требования и рекомендации по развертыванию
toostart автоматической отправки журналов tooLog аналитики, необходимо:

1. Здравствуйте, ноябрь 2016 г. или более поздней версии версии [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) (v2.3.0).
2. Рабочая область Log Analytics. Дополнительные сведения см. в статье [Начало работы с Log Analytics](../log-analytics/log-analytics-get-started.md). 
3. Hello ResourceId для вашей учетной записи службы автоматизации Azure

hello toofind ResourceId для вашей учетной записи службы автоматизации Azure и рабочей области аналитики журналов, запустите следующие PowerShell hello:

```powershell
# Find hello ResourceId for hello Automation Account
Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"

# Find hello ResourceId for hello Log Analytics workspace
Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
```

Если у вас несколько учетных записей автоматизации или рабочие области, в выходные данные команды, предшествующие hello hello найти hello *имя* требуется tooconfigure и скопируйте значение hello для *ResourceId*.

Если вам требуется toofind hello *имя* учетной записи автоматизации в hello портала Azure выберите учетную запись автоматизации из hello **учетной записи автоматизации** и выберите **все параметры**.  Из hello **все параметры** колонки в разделе **параметры учетной записи** выберите **свойства**.  В hello **свойства** колонки, эти значения можно обратить внимание.<br> ![Свойства учетной записи службы автоматизации](media/automation-manage-send-joblogs-log-analytics/automation-account-properties.png).

## <a name="set-up-integration-with-log-analytics"></a>Настройка интеграции с Log Analytics
1. На компьютере, запустите **Windows PowerShell** из hello **запустить** экрана.  
2. Скопируйте и вставьте следующий PowerShell hello и измените значение hello для hello `$workspaceId` и `$automationAccountId`.  Для hello `-Environment` параметров, допустимыми значениями являются *облачной* или *AzureUSGovernment* в зависимости от того, вы работаете в среде облака hello.     

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }

# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $automationAccountId -WorkspaceId $workspaceId -Enabled $true

```

После запуска этого сценария вы увидите записи в Log Analytics, добавленные в новый элемент JobLogs или JobStreams за 10 минут.

toosee журналы hello, запустите hello в следующем запросе в поиске по журналам анализа журналов:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="verify-configuration"></a>Проверка конфигурации
tooconfirm отправляет учетной записи автоматизации в журналах рабочей областью аналитики журналов tooyour, проверьте, что диагностики правильно установлены на hello учетной записи автоматизации с помощью следующих PowerShell hello:

```powershell
[cmdletBinding()]
    Param
    (
        [Parameter(Mandatory=$True)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$Environment="AzureCloud"
    )

#Check toosee which cloud environment toosign into.
Switch ($Environment)
   {
       "AzureCloud" {Login-AzureRmAccount}
       "AzureUSGovernment" {Login-AzureRmAccount -EnvironmentName AzureUSGovernment} 
   }
# if you have one Log Analytics workspace you can use hello following command tooget hello resource id of hello workspace
$workspaceId = (Get-AzureRmOperationalInsightsWorkspace).ResourceId

$automationAccountId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.AUTOMATION/ACCOUNTS/DEMO" 

Get-AzureRmDiagnosticSetting -ResourceId $automationAccountId
```

В выходных данных hello убедитесь, что:
+ В разделе *журналы*, hello значение *включено* — *True*
+ Здравствуйте, значение *ИД рабочей области* задано toohello ResourceId рабочей области аналитики журналов


## <a name="log-analytics-records"></a>Записи Log Analytics
При диагностике из службы автоматизации Azure в Log Analytics создаются записи двух типов, которые помечаются как **Type=AzureDiagnostics**.

### <a name="job-logs"></a>Журналы заданий
| Свойство | Описание |
| --- | --- |
| TimeGenerated |Дата и время выполнения задания runbook hello. |
| RunbookName_s |Имя hello runbook Hello. |
| Caller_s |Кто инициировал операцию hello.  Допустимые значения: электронный адрес или system для запланированных заданий. |
| Tenant_g | Идентификатор GUID, определяющий hello клиента для hello вызывающего объекта. |
| JobId_g |Идентификатор GUID, — идентификатор задания runbook hello hello. |
| ResultType |состояние задания runbook hello Hello.  Возможные значения:<br>Started<br>- Остановлена<br>Приостановлено<br>Сбой<br>Завершено |
| Категория | Классификация данных типа hello.  Для автоматизации используется значение hello JobLogs. |
| OperationName | Указывает тип операции, выполняемой в Azure hello.  Для автоматизации используется значение hello задания. |
| Ресурс | Имя учетной записи автоматизации hello |
| SourceSystem | Как служба аналитики журналов сбора данных hello. Всегда имеет значение *Azure* для системы диагностики Azure. |
| ResultDescription |Описывает состояние результата задания runbook hello.  Возможные значения:<br>— Job is started;<br>— Job Failed;<br>- Job Completed. |
| CorrelationId |Идентификатор GUID, который является hello Корреляционный идентификатор задания runbook hello. |
| ResourceId |Указывает идентификатор ресурса учетной записи автоматизации Azure hello hello модуля Runbook. |
| SubscriptionId | Здравствуйте, подписки Azure идентификатор (GUID) для учетной записи автоматизации hello. |
| ResourceGroup | Имя группы ресурсов hello hello учетной записи автоматизации. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |


### <a name="job-streams"></a>Потоки заданий
| Свойство | Описание |
| --- | --- |
| TimeGenerated |Дата и время выполнения задания runbook hello. |
| RunbookName_s |Имя hello runbook Hello. |
| Caller_s |Кто инициировал операцию hello.  Допустимые значения: электронный адрес или system для запланированных заданий. |
| StreamType_s |Тип Hello потока задания. Возможные значения:<br>ход выполнения<br>Выходные данные<br>Предупреждение<br>error<br>debug<br>- Verbose. |
| Tenant_g | Идентификатор GUID, определяющий hello клиента для hello вызывающего объекта. |
| JobId_g |Идентификатор GUID, — идентификатор задания runbook hello hello. |
| ResultType |состояние задания runbook hello Hello.  Возможные значения:<br>- In Progress |
| Категория | Классификация данных типа hello.  Для автоматизации используется значение hello JobStreams. |
| OperationName | Указывает тип операции, выполняемой в Azure hello.  Для автоматизации используется значение hello задания. |
| Ресурс | Имя учетной записи автоматизации hello |
| SourceSystem | Как служба аналитики журналов сбора данных hello. Всегда имеет значение *Azure* для системы диагностики Azure. |
| ResultDescription |Включает в себя hello выходной поток из модуля runbook hello. |
| CorrelationId |Идентификатор GUID, который является hello Корреляционный идентификатор задания runbook hello. |
| ResourceId |Указывает идентификатор ресурса учетной записи автоматизации Azure hello hello модуля Runbook. |
| SubscriptionId | Здравствуйте, подписки Azure идентификатор (GUID) для учетной записи автоматизации hello. |
| ResourceGroup | Имя группы ресурсов hello hello учетной записи автоматизации. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |

## <a name="viewing-automation-logs-in-log-analytics"></a>Просмотр журналов службы автоматизации в Log Analytics
Теперь, когда вы начали отправки задания tooLog журналы аналитики вашей автоматизации, давайте посмотрим, можно сделать с помощью этих журналов в службе анализа журналов.

журналы hello toosee с запуска приветствия при следующем запросе:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION"`

### <a name="send-an-email-when-a-runbook-job-fails-or-suspends"></a>Отправка электронного сообщения при сбое или приостановке задания Runbook
Одно из нашего главного клиента запрашивает предназначен для hello возможность toosend сообщение электронной почты или текстовый при возникновении неполадок с задания runbook.   

правило toocreate предупреждение, сначала нужно создать задание записи, которые следует вызвать предупреждение hello поиска журналов для hello runbook.  Нажмите кнопку hello **предупреждение** кнопку toocreate и настроить правила оповещений hello.

1. На странице приветствия Обзор аналитики журналов нажмите **поиска журналов**.
2. Создайте запрос поиска журнала для оповещения, введя hello, выполнив поиск в поле запроса hello: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended)` задачи можно группировать по hello RunbookName с помощью:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs (ResultType=Failed OR ResultType=Suspended) | measure Count() by RunbookName_s`   

   Если настраивается журналы из более чем одной автоматизации учетная запись или подписка tooyour рабочей области, можно сгруппировать оповещения, подписки и учетной записи автоматизации.  Имя учетной записи автоматизации могут быть производными от поле ресурса hello в поиске hello объекта JobLogs.  
3. tooopen hello **добавить правило оповещения** щелкните **предупреждения** вверху hello страницы приветствия. Для получения сведений о tooconfigure hello hello параметры оповещений в разделе [предупреждения в службе анализа журналов](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-all-jobs-that-have-completed-with-errors"></a>Поиск всех заданий, завершенных с ошибками
В дополнение к этому tooalerting об ошибках можно найти после задания runbook устранимую ошибку. В таких случаях PowerShell создает поток сообщений об ошибках, но не вызвать ваш toosuspend задания или ошибкой hello устранимые ошибки.    

1. В рабочей области Log Analytics щелкните **Поиск по журналу**.
2. Введите в поле запроса hello `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams StreamType_s=Error | measure count() by JobId_g` и нажмите кнопку **поиска**.

### <a name="view-job-streams-for-a-job"></a>Просмотр потоков заданий для задания
При отладке задания можно также toolook в потоки задания hello.  Hello следующий запрос отображает все потоки hello для одного задания с GUID 2ebd22ea-e05e-4eb9 - 9d 76-d73cbd4356e0:   

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobStreams JobId_g="2ebd22ea-e05e-4eb9-9d76-d73cbd4356e0" | sort TimeGenerated | select ResultDescription`

### <a name="view-historical-job-status"></a>Просмотр хронологии состояния задания
Наконец вы можете toovisualize историю задания со временем.  Можно использовать этот запрос toosearch hello состояния заданий со временем.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=JobLogs NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  
<br> ![Диаграмма хронологии состояния задания в OMS](media/automation-manage-send-joblogs-log-analytics/historical-job-status-chart.png)<br>

## <a name="summary"></a>Сводка
Отправляя вашей автоматизации задания состояния и поток данных tooLog Analytics, можно получить более глубокое представление о hello состояние автоматизации заданий по:
+ Настройка оповещений toonotify вы при возникновении проблемы
+ С помощью настраиваемых представлений и запросов toovisualize поиска вашей результатов runbook, состояние задания runbook и других связанных ключевых показателей или метрики.  

Служба аналитики журналов предоставляет больше оперативной видимость tooyour автоматизации заданий и могут помочь быстрее инцидентов адрес.  

## <a name="next-steps"></a>Дальнейшие действия
* toolearn Дополнительные сведения о как журналы с помощью аналитики журналов задания tooconstruct различных поисковые запросы и просмотрите hello автоматизации см [входа поиска аналитики журналов](../log-analytics/log-analytics-log-searches.md)
* toounderstand toocreate и получение выходных данных и сообщения об ошибках из модулей Runbook, в статье [Runbook вывода и сообщений](automation-runbook-output-and-messages.md)
* Дополнительные сведения о выполнение модуля runbook, как toomonitor заданиях и другие технические сведения см. в разделе toolearn [отследить задание runbook](automation-runbook-execution.md)
* в разделе toolearn Дополнительные сведения о службе анализа журналов OMS и коллекцию источников данных, [Azure сбор данных из хранилища в обзоре анализа журналов](../log-analytics/log-analytics-azure-storage.md)
