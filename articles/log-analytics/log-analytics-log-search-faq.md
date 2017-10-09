---
title: "новый поиск журнала aaaLog аналитика часто задаваемые вопросы | Документы Microsoft"
description: "Эта статья содержит часто задаваемые вопросы об обновлении hello анализа журналов toohello новый язык запросов."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a>Вопросы и ответы по новым возможностям поиска по журналам Log Analytics и известные проблемы

Эта статья содержит ответы на вопросы и известных проблемах в отношении hello обновление [toohello анализа журналов нового языка запросов](log-analytics-log-search-upgrade.md).  Следует прочтите эту статью целиком перед внесением tooupgrade hello принятия решений в рабочей области.


## <a name="alerts"></a>Оповещения

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a>Вопрос. У меня много правил генерации оповещений. Требуется toocreate их еще раз в новый язык hello после обновлении?  
Нет, правилами генерации оповещений, новый язык поиска автоматически преобразованный toohello во время обновления.  


## <a name="computer-groups"></a>Группы компьютеров

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a>Вопрос: я получаю ошибок при попытке toouse групп компьютеров.  Их синтаксис изменился?
Да, hello синтаксис для использования компьютера группирует изменения, при обновлении рабочей области.  Дополнительные сведения см. в статье [Использование групп компьютеров при поиске по журналам Log Analytics](log-analytics-computer-groups.md).

### <a name="known-issue-groups-imported-from-active-directory"></a>Известная проблема. Группы, импортированные из Active Directory
В настоящее время вы не можете создать запрос, использующий группы компьютеров, импортированные из Active Directory.  Чтобы избежать этого, пока эта проблема не будет устранена, создайте новую группу компьютеров с помощью hello импортированные группы Active Directory, а затем используйте этой новой группы в запросе.

Ниже приведен пример запроса toocreate новой группы компьютеров, которая включает импортированные группы Active Directory:

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a>Панели мониторинга

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a>Вопрос. Можно ли по-прежнему использовать панели мониторинга в обновленной рабочей области?
Вы можете продолжить toouse любой плитки, которые вы добавили слишком**Моя панель мониторинга** до обновления рабочей области, но нельзя изменять эти плитки или добавить новые.  Можно продолжить toocreate и изменения представлений с [конструктор представлений](log-analytics-view-designer.md) а также для создания панелей мониторинга в hello портал Azure.


## <a name="log-searches"></a>Поиск по журналам

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a>Вопрос. До обновления я сохранял поисковые запросы вне рабочей области. Можно преобразовать их toohello новый язык поиска автоматически?
Можно использовать средство преобразования языка hello в tooconvert страницы поиска журналов hello каждого из них.  Имеется несколько операций поиска без обновления рабочей hello без преобразования tooautomatically метод.

### <a name="question-why-are-my-query-results-not-sorted"></a>Вопрос. Почему результаты запроса не отсортированы?
Результаты не сортируются по умолчанию в hello новый язык запросов.  Используйте hello [оператор sort](https://go.microsoft.com/fwlink/?linkid=856079) toosort результаты по одному или нескольким свойствам.

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a>Известная проблема. Результаты поиска в списке могут содержать свойства без данных
Результаты поиска по журналу в списке могут содержать свойства без данных.  Предыдущий tooupgrade эти свойства не будет включен.  Мы работаем над устранением этой проблемы, после чего они перестанут отображаться.

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a>Известная проблема. При выборе значения на диаграмме не отображаются подробные результаты
Предыдущий tooupgrade при выборе значения в диаграмме, то будет возвращено подробный список записей, соответствующих hello выбранные значения.  После обновления возвращается только hello сводные линию.  В настоящее время мы работаем над решением этой проблемы.

## <a name="log-search-api"></a>API поиска по журналам

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a>Вопрос: Hello API поиска журналов обновляется после обновлении?
Hello [API поиска журналов](log-analytics-log-search-api.md) еще не обновленные toohello новый язык поиска.  Продолжайте toouse hello устаревших запросов языка с интерфейсом API, даже в том случае, после обновления рабочей области.  Обновленная документация станет доступным для hello API поиска журналов, при его обновлении.


## <a name="portals"></a>Порталы

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a>Вопрос: Следует ли использовать новый портал Advanced Analytics hello или сохранить с помощью портала hello поиска журналов?
Вы увидите сравнение двух hello порталов в [порталы для создания и изменения журнала запросов в Azure Log Analytics](log-analytics-log-search-portals.md).  Каждый имеет свои преимущества, поэтому вы можете выбрать hello лучший под конкретные потребности.  Он обобщенных toowrite hello Advanced Analytics портала и вставьте их в других местах, таких как конструктор представлений.  Прочитайте о [выдает tooconsider](log-analytics-log-search-portals.md#advanced-analytics-portal) , при выполнении.


## <a name="power-bi"></a>Power BI

### <a name="question-does-anything-change-with-powerbi-integration"></a>Вопрос. Затронут ли эти изменения интеграцию с Power BI?
Да.  После обновления рабочей области hello процесса экспорта tooPower данных аналитики журналов BI больше не будет работать.  Все существующие расписания, созданные перед обновлением, будут отключены.  После обновления службы анализа журналов Azure использует hello платформы Application Insights и использовать hello же процесс анализа журналов tooexport запросы tooPower бизнес-Аналитики как [tooexport процесса hello Application Insights запрашивает tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).

### <a name="known-issue-power-bi-request-size-limit"></a>Известная проблема. Ограничение размера запроса Power BI
В настоящее время отсутствует ограничение на размер составляет 8 МБ для анализа журналов запроса, который может быть экспортированного tooPower бизнес-Аналитики.  Мы планируем увеличить это ограничение.


##<a name="powershell-cmdlets"></a>Командлеты PowerShell

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a>Вопрос: Командлета PowerShell поиска журнала hello обновляется после обновлении?
Hello [Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) еще не обновленные toohello новый язык поиска.  Продолжайте toouse hello устаревших запросов языка с этим командлетом, даже в том случае, после обновления рабочей области.  Обновленная документация станет доступным для командлета hello при его обновлении.


## <a name="resource-manager-templates"></a>Шаблоны диспетчера ресурсов

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a>Вопрос. Можно ли создать обновленную рабочую область с помощью шаблона Resource Manager?
Да.  Необходимо использовать версию API 2017 г-03-15-preview и включить **функции** раздел в шаблоне как следующий пример hello.

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a>Решения

### <a name="question-will-my-solutions-continue-toowork"></a>Вопрос: My решения будут toowork?
Все решения продолжится toowork обновленной рабочей области, несмотря на то, что их производительность при преобразованный toohello новый язык запросов.  В этом разделе описаны известные проблемы, возникающие с некоторыми имеющимися решениями.

### <a name="known-issue-capacity-and-performance-solution"></a>Известная проблема. Решение "Емкость и производительность"
Некоторые части hello в hello [емкости и производительности](log-analytics-capacity.md) представления может быть пустым.  Проблема с исправление toothis вскоре будут доступны.

### <a name="known-issue-device-health-solution"></a>Известная проблема. Решение "Работоспособность устройств"
Hello [решения работоспособности устройства](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) не будет собирать данные в обновленном рабочей области.  Проблема с исправление toothis вскоре будут доступны.

### <a name="known-issue-application-insights-connector"></a>Известная проблема. Соединитель Application Insights
В настоящее время [Соединитель Application Insights](log-analytics-app-insights-connector.md) не поддерживается в обновленной рабочей области.  Исправление toothis проблему в настоящее время находится в анализ.

## <a name="upgrade-process"></a>Процесс обновления

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a>Вопрос. У меня есть несколько рабочих областей. Можно ли обновить все рабочие области в hello одновременно?  
Нет.  Обновление применяется одной рабочей области tooa каждый раз. В настоящее время не существует возможности обновить сразу несколько рабочих областей. Обратите внимание также касается других пользователей, hello обновление рабочей области.  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a>Вопрос. Изменятся ли после обновления имеющиеся данные в журналах, собранных в рабочей области?  
Нет. Поиск доступных tooyour рабочей области журнала Hello не затрагивается hello обновления. Сохраненные поисковые запросы, предупреждения и представления будут преобразованный toohello новый язык поиска автоматически.  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a>Вопрос. Что произойдет, если не обновлять рабочую область?  
Поиск старых журналов Hello будет считаться устаревшей в hello, поступающих в месяцах. Рабочие области, которые вы не обновите к этому времени, будут обновлены автоматически.

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a>Вопрос: не выбрана tooupgrade, но все равно обновлен мою рабочую область! Что произошло?  
Другой администратор этой рабочей области может обновлены hello рабочей области. Обратите внимание на то, что все рабочие области автоматически обновляются после выхода общедоступной версии hello новый язык.  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a>Вопрос: я выполнено по ошибке, но теперь требуется toocancel его и восстановления всех. Что мне делать?  
Не беспокойтесь.  Мы создали моментальный снимок рабочей области перед обновлением, и вы можете ее восстановить. Имейте в виду, в котором выполняется поиск, предупреждения или представления сохраняться после обновления hello, будут потеряны хотя.  toorestore рабочей среды, выполните процедуру hello на [можно перейти обратно после обновлении?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)


## <a name="views"></a>Views

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a>Вопрос. Как создать представление с помощью конструктора представлений?
Предыдущий tooupgrade можно создать новое представление с помощью конструктора представлений из плитки на главной информационной hello.  После обновления эта плитка удаляется.  Можно создать новое представление с помощью конструктора представлений на портале OMS hello, щелкнув кнопку в левом меню hello + hello зеленый.

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a>Известная проблема. После нажатия кнопки "Показать все" на графиках в представлениях не отображается соответствующий график
При нажатии кнопки на hello *все* параметр hello нижней части диаграммы в представлении в виде строки, решаемой таблицы.  Предыдущий tooupgrade вам будут представлены с графиком.  Мы работаем над решением этой проблемы.


## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о [обновление вашей рабочей области toohello языка запросов новый журнал аналитики](log-analytics-log-search-upgrade.md).
