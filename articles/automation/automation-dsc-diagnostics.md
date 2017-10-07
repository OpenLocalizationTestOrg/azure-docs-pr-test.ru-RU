---
title: "aaaForward отчетов tooOMS данных анализа журналов Azure Automation DSC | Документы Microsoft"
description: "В этой статье показано, как toosend требуемого состояния конфигурации (DSC) reporting дополнительные подсказки анализа журналов Operations Management Suite tooMicrosoft toodeliver данных и управления."
services: automation
documentationcenter: 
author: eslesar
manager: carmonm
editor: tysonn
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: eslesar
ms.openlocfilehash: 21f78d5549d53ba3d7e237f55d9086f380cf3351
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="forward-azure-automation-dsc-reporting-data-toooms-log-analytics"></a>Пересылка отчетов tooOMS данных анализа журналов Azure Automation DSC

Автоматизация может отправлять рабочей области аналитики журналов Microsoft Operations Management Suite (OMS) tooyour данных в состояние узла DSC.  
Состояние соответствия виден hello портал Azure, или с помощью PowerShell, для узлов, а также для отдельных ресурсов DSC в конфигурации узла. С помощью Log Analytics можно:

* получать сведения о соответствии требованиям для управляемых узлов и отдельных ресурсов;
* активировать сообщение электронной почты или предупреждение (в зависимости от состояния соответствия);
* создавать сложные запросы к управляемым узлам;
* сопоставлять состояние соответствия в учетных записях службы автоматизации;
* визуализировать журнал соответствия узла с течением времени.

## <a name="prerequisites"></a>Предварительные требования

toostart отправки вашего Automation DSC сообщает tooLog Analytics, вы должны:

* Здравствуйте, ноябрь 2016 г. или более поздней версии версии [Azure PowerShell](/powershell/azure/overview) (v2.3.0).
* Учетная запись службы автоматизации Azure. Дополнительные сведения см. в статье [Приступая к работе со службой автоматизации Azure](automation-offering-get-started.md)
* Рабочая область Log Analytics с предложением службы **Автоматизация и управление**. Дополнительные сведения см. в статье [Начало работы с Log Analytics](../log-analytics/log-analytics-get-started.md).
* Как минимум один узел Azure Automation DSC. Дополнительные сведения см. в статье [Подключение компьютеров для управления с помощью Azure Automation DSC](automation-dsc-onboarding.md). 

## <a name="set-up-integration-with-log-analytics"></a>Настройка интеграции с Log Analytics

toobegin при импорте данных в Azure Automation DSC в службы анализа журналов, полный hello, следующие шаги:

1. Войдите в систему tooyour учетной записи Azure в PowerShell. См. статью [Вход с помощью Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/authenticate-azureps?view=azurermps-4.0.0).
1. Получить hello _ResourceId_ вашей учетной записи автоматизации, выполнив следующую команду PowerShell hello: (если имеется более одной учетной записи автоматизации, выберите hello _ResourceID_ для hello учетной записи tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Automation Account
  Find-AzureRmResource -ResourceType "Microsoft.Automation/automationAccounts"
  ```
1. Получить hello _ResourceId_ рабочей области аналитики журналов, выполнив следующую команду PowerShell hello: (при наличии более чем одной рабочей области, выберите hello _ResourceID_ для hello рабочей области, tooconfigure).

  ```powershell
  # Find hello ResourceId for hello Log Analytics workspace
  Find-AzureRmResource -ResourceType "Microsoft.OperationalInsights/workspaces"
  ```
1. Выполнения hello следующую команду PowerShell, заменив `<AutomationResourceId>` и `<WorkspaceResourceId>` с hello _ResourceId_ значения от всех предыдущих шагов hello:

  ```powershell
  Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $true -Categories "DscNodeStatus"
  ```

Импорт данных из DSC службы автоматизации Azure в службе анализа журналов toostop, выполните следующую команду PowerShell hello.

```powershell
Set-AzureRmDiagnosticSetting -ResourceId <AutomationResourceId> -WorkspaceId <WorkspaceResourceId> -Enabled $false -Categories "DscNodeStatus"
```

## <a name="view-hello-dsc-logs"></a>Просмотр журналов hello DSC

После настройки интеграции с помощью аналитики журналов DSC службы автоматизации данных **поиска журналов** кнопка появится для hello **узлы DSC** колонке учетной записи автоматизации. Нажмите кнопку hello **поиска журналов** кнопку tooview hello в журналах данных узла DSC.

![Кнопка поиска по журналам](media/automation-dsc-diagnostics/log-search-button.png)

Hello **поиска журналов** открывает колонку и вы увидите **DscNodeStatusData** операции для каждого узла DSC и **DscResourceStatusData** операции для каждого [DSC ресурс](https://msdn.microsoft.com/powershell/dsc/resources) вызывается в узле примененных toothat конфигурация узла hello.

Hello **DscResourceStatusData** операция содержит сведения об ошибках для всех ресурсов DSC, которые не удалось.

Щелкните каждой операции в toosee hello hello список данных для этой операции.

Можно также просмотреть журналы hello, [поиск в службе анализа журналов. См. статью [Поиск данных по журналам](../log-analytics/log-analytics-log-searches.md).
Тип hello следующий запрос toofind вашей DSC журналы:`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus"`

Также можно сузить запрос hello, имя операции hello. Например: `Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category = "DscNodeStatus" OperationName = "DscNodeStatusData"

### <a name="send-an-email-when-a-dsc-compliance-check-fails"></a>Отправка сообщения электронной почты при сбое проверки соответствия DSC

Одна из наших top пожеланиям — toosend возможность hello сообщения электронной почты или текстовый при возникновении неполадок с конфигурации DSC.   

toocreate правило оповещения, начните с создания поиска журналов для hello DSC отчета записей, которые следует вызвать предупреждение hello.  Нажмите кнопку hello **предупреждение** кнопку toocreate и настроить правила оповещений hello.

1. На странице приветствия Обзор аналитики журналов нажмите **поиска журналов**.
1. Создайте запрос поиска журналов для оповещения, введя hello, выполнив поиск в поле запроса hello:`Type=AzureDiagnostics Category=DscNodeStatus NodeName_s=DSCTEST1 OperationName=DscNodeStatusData ResultType=Failed`

  Если настраивается журналы из более чем одной автоматизации учетная запись или подписка tooyour рабочей области, можно сгруппировать оповещения, подписки и учетной записи автоматизации.  
  Имя учетной записи автоматизации могут быть производными от поле ресурса hello в поиске hello объекта DscNodeStatusData.  
1. tooopen hello **добавить правило оповещения** щелкните **предупреждения** вверху hello страницы приветствия. Дополнительные сведения о tooconfigure hello hello параметры оповещений в разделе [предупреждения в службе анализа журналов](../log-analytics/log-analytics-alerts.md#alert-rules).

### <a name="find-failed-dsc-resources-across-all-nodes"></a>Поиск ресурсов DSC со сбоями по всем узлам

Одно из преимуществ Log Analytics — возможность поиска проверок со сбоями по узлам.
toofind все экземпляры ресурсов DSC, которые не удалось.

1. На странице приветствия Обзор аналитики журналов нажмите **поиска журналов**.
1. Создайте запрос поиска журналов для оповещения, введя hello, выполнив поиск в поле запроса hello:`Type=AzureDiagnostics Category=DscNodeStatus OperationName=DscResourceStatusData ResultType=Failed`

### <a name="view-historical-dsc-node-status"></a>Просмотр состояния узла DSC за предыдущие периоды

Наконец вы можете toovisualize историю состояние узла DSC со временем.  
Toosearch этот запрос можно использовать для hello состояние состояние узла DSC со временем.

`Type=AzureDiagnostics ResourceProvider="MICROSOFT.AUTOMATION" Category=DscNodeStatus NOT(ResultType="started") | measure Count() by ResultType interval 1hour`  

Это позволит отобразить диаграмму состояние узла hello со временем.

## <a name="log-analytics-records"></a>Записи Log Analytics

При диагностике службы автоматизации Azure в Log Analytics создаются записи двух категорий.

### <a name="dscnodestatusdata"></a>DscNodeStatusData

| Свойство | Описание |
| --- | --- |
| TimeGenerated |Дата и время запуска проверки соответствия hello. |
| OperationName |DscNodeStatusData |
| ResultType |Является ли узел hello является совместимым. |
| NodeName_s |Имя Hello hello управляемого узла. |
| NodeComplianceStatus_s |Является ли узел hello является совместимым. |
| DscReportStatus |Является ли проверка на соответствие hello успешно выполнено. |
| ConfigurationMode | Как узел примененных toohello используется конфигурация hello. Возможные значения: __ApplyOnly__, __ApplyandMonitior__ и __ApplyandAutoCorrect__. <ul><li>__ApplyOnly__: DSC применяет конфигурации hello и не выполняет никаких действий, пока новая конфигурация не будет перенесена toohello целевому узлу или когда новая конфигурация извлекается с сервера. После первоначального применения новой конфигурации DSC не проверяет наличие отклонений от ранее настроенного состояния. DSC пытается tooapply hello конфигурации вплоть до его завершения перед __ApplyOnly__ вступает в силу. </li><li> __ApplyAndMonitor__: это значение по умолчанию hello. Hello LCM применяет все новые конфигурации. После первого применения новой конфигурации Если hello целевой узел отклоняется от hello требуемого состояния, DSC сообщает hello расхождении в журналах. DSC пытается tooapply hello конфигурации вплоть до его завершения перед __ApplyAndMonitor__ вступает в силу.</li><li>__ApplyAndAutoCorrect__ — DSC применяет любые новые конфигурации. После первого применения новой конфигурации Если hello целевой узел отклоняется от hello требуемого состояния, DSC сообщает о расхождении hello в журналах и затем повторно применяет текущую конфигурацию hello.</li></ul> |
| HostName_s | Имя Hello hello управляемого узла. |
| IPAddress | Hello IPv4-адрес hello управляемого узла. |
| Категория | DscNodeStatus |
| Ресурс | Имя Hello hello учетной записи службы автоматизации Azure. |
| Tenant_g | Идентификатор GUID, определяющий hello клиента для hello вызывающего объекта. |
| NodeId_g |Идентификатор GUID, определяющий hello управляемый узел. |
| DscReportId_g |Идентификатор GUID, определяющий hello отчета. |
| LastSeenTime_t |Дата и время, когда последнего просмотра отчетов hello. |
| ReportStartTime_t |Дата и время начала отчета hello. |
| ReportEndTime_t |Дата и время завершения отчета hello. |
| NumberOfResources_d |в узле toohello конфигурацию, примененную hello вызывается Hello количество ресурсов DSC. |
| SourceSystem | Как служба аналитики журналов сбора данных hello. Всегда имеет значение *Azure* для системы диагностики Azure. |
| ResourceId |Указывает учетную запись службы автоматизации Azure hello. |
| ResultDescription | Описание Hello для этой операции. |
| SubscriptionId | Здравствуйте, подписки Azure идентификатор (GUID) для учетной записи автоматизации hello. |
| ResourceGroup | Имя группы ресурсов hello hello учетной записи автоматизации. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |Идентификатор GUID, — идентификатор корреляции отчет о соответствии hello hello. |

### <a name="dscresourcestatusdata"></a>DscResourceStatusData

| Свойство | Описание |
| --- | --- |
| TimeGenerated |Дата и время запуска проверки соответствия hello. |
| OperationName |DscResourceStatusData|
| ResultType |Является ли ресурс hello является совместимым. |
| NodeName_s |Имя Hello hello управляемого узла. |
| Категория | DscNodeStatus |
| Ресурс | Имя Hello hello учетной записи службы автоматизации Azure. |
| Tenant_g | Идентификатор GUID, определяющий hello клиента для hello вызывающего объекта. |
| NodeId_g |Идентификатор GUID, определяющий hello управляемый узел. |
| DscReportId_g |Идентификатор GUID, определяющий hello отчета. |
| DscResourceId_s |Имя экземпляра ресурса hello DSC Hello. |
| DscResourceName_s |Имя ресурса hello DSC Hello. |
| DscResourceStatus_s |Является ли ресурс DSC hello в соответствие. |
| DscModuleName_s |Имя Hello hello модуль PowerShell, который содержит ресурс DSC hello. |
| DscModuleVersion_s |версия Hello hello модуль PowerShell, который содержит ресурс DSC hello. |
| DscConfigurationName_s |Имя Hello hello конфигурации применяется toohello узла. |
| ErrorCode_s | Hello код ошибки, если ошибка ресурса hello. |
| ErrorMessage_s |Hello сообщение об ошибке при сбое ресурса hello. |
| DscResourceDuration_d |Hello время в секундах, в которых была выполнена hello DSC ресурсов. |
| SourceSystem | Как служба аналитики журналов сбора данных hello. Всегда имеет значение *Azure* для системы диагностики Azure. |
| ResourceId |Указывает учетную запись службы автоматизации Azure hello. |
| ResultDescription | Описание Hello для этой операции. |
| SubscriptionId | Здравствуйте, подписки Azure идентификатор (GUID) для учетной записи автоматизации hello. |
| ResourceGroup | Имя группы ресурсов hello hello учетной записи автоматизации. |
| ResourceProvider | MICROSOFT.AUTOMATION |
| ResourceType | AUTOMATIONACCOUNTS |
| CorrelationId |Идентификатор GUID, — идентификатор корреляции отчет о соответствии hello hello. |

## <a name="summary"></a>Сводка

Отправляя tooLog данных к DSC службы автоматизации аналитика, можно получить более глубокое представление о состоянии hello узлы DSC службы автоматизации с:

* Настройка оповещений toonotify вы при возникновении проблемы
* С помощью настраиваемых представлений и запросов toovisualize поиска вашей результатов runbook, состояние задания runbook и других связанных ключевых показателей или метрики.  

Служба аналитики журналов предоставляет больше оперативной видимость tooyour DSC службы автоматизации данные и может помочь быстрее адрес инцидентов.  

## <a name="next-steps"></a>Дальнейшие действия

* см. Дополнительные сведения о как tooconstruct различных поисковые запросы и просмотр hello DSC службы автоматизации журналы с помощью аналитики журналов toolearn [входа поиска аналитики журналов](../log-analytics/log-analytics-log-searches.md)
* toolearn Подробнее об использовании Azure Automation DSC. в разделе [Приступая к работе с Azure Automation DSC](automation-dsc-getting-started.md)
* в разделе toolearn Дополнительные сведения о службе анализа журналов OMS и коллекцию источников данных, [Azure сбор данных из хранилища в обзоре анализа журналов](../log-analytics/log-analytics-azure-storage.md)

