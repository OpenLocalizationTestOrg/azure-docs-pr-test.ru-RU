---
title: "aaaUsing OMS API аналитики журналов оповещений REST"
description: "Hello API REST предупреждения аналитики журналов позволяет toocreate оповещений и управление ими в службе анализа журналов, являющейся частью Operations Management Suite (OMS).  Эта статья содержит сведения hello API и несколько примеров для выполнения различных операций."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Создание правил генерации оповещений и управление ими в Log Analytics с помощью REST API
Hello API REST предупреждения аналитики журналов позволяет toocreate оповещений и управление ими в Operations Management Suite (OMS).  Эта статья содержит сведения hello API и несколько примеров для выполнения различных операций.

Hello REST API поиска аналитики журналов относится к категории RESTful и может запускаться через REST API диспетчера ресурсов Azure hello. В этом документе вы найдете примеры, когда hello API осуществляется из командной строки PowerShell с помощью [ARMClient](https://github.com/projectkudu/ARMClient), Здравствуйте, средство командной строки с открытым исходным, который упрощает вызов API диспетчера ресурсов Azure. Hello использование ARMClient и PowerShell является одним из многих параметров tooaccess hello API поиска аналитики журналов. С помощью этих средств можно использовать рабочие области tooOMS вызовы toomake API диспетчера ресурсов Azure категории RESTful hello и выполнения команд поиска в них. Hello API будет выдавать tooyou результаты поиска в формате JSON, позволяя результаты поиска hello toouse различными способами программными средствами.

## <a name="prerequisites"></a>Предварительные требования
В настоящее время оповещения могут создаваться только с помощью сохраненного поиска в службе Log Analytics.  Можно ссылаться toohello [REST API поиска журналов](log-analytics-log-search-api.md) для получения дополнительной информации.

## <a name="schedules"></a>Расписания
Сохраненный поиск может включать одно расписание или несколько. Hello расписание определяет частоту hello поиска выполняется и идентифицируется hello интервал времени, через какие критерии hello.
Расписания, имеют свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| Интервал |Как часто hello поиска выполняется. Измеряется в минутах. |
| QueryTimeSpan |интервал времени Hello какие hello для вычисления условия. Должно быть больше интервала равно tooor. Измеряется в минутах. |
| Version (версия) |Здравствуйте, используемой версии API.  В настоящее время это всегда должен иметь значение too1. |

Например, рассмотрим запрос событий с интервалом (свойство Interval) 15 минут и временным диапазоном (свойство TimeSpan) 30 минут. В этом случае hello запрос будет выполняться каждые 15 минут, и будет запускаться оповещение, если критерий hello продолжение tooresolve tootrue через интервал 30 минут.

### <a name="retrieving-schedules"></a>Получение расписаний
Используйте hello получить метод tooretrieve все расписания сохраненного поиска.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Используйте hello Get-метод с tooretrieve идентификатор расписания определенное расписание сохраненного поиска.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

Ниже приведен пример ответа для расписания.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>Создание расписания
Метод Put hello с расписание уникальный идентификатор toocreate новое расписание.  Обратите внимание, что два расписания не может иметь hello таким же Идентификатором даже если они связаны с другой, сохраненные поисковые запросы.  При создании расписания в консоли OMS hello GUID создается для идентификатора расписания hello

> [!NOTE]
> Имя Hello все сохраненные поисковые запросы, отчеты и действия, созданные с помощью hello API аналитики журналов должно быть в нижнем регистре.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Изменение расписания
Метод Put hello с существующим расписанием идентификатор hello же сохраненный поиск toomodify, который в расписании.  текст Hello hello запроса должен содержать etag hello hello расписания.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Удаление расписаний
Метод Delete hello с toodelete идентификатор расписания расписания.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Действия
Расписание может включать несколько действий. Действие может определять одну или несколько tooperform процессов, например отправку почты или запуск runbook, или он может определять пороговое значение, которое определяет, когда hello результатов поиска соответствующих некоторым условиям.  Некоторые действия будут определять, чтобы hello процессы выполняются при достижении порога hello.

Все действия имеют свойства hello в hello в следующей таблице.  Разные типы оповещений имеют различные дополнительные свойства, которые описаны ниже.

| Свойство | Описание |
|:--- |:--- |
| Тип |Тип действия hello.  В настоящее время hello возможные значения: предупреждение и веб-перехватчика. |
| Имя |Отображаемое имя для hello предупреждения. |
| Version (версия) |Здравствуйте, используемой версии API.  В настоящее время это всегда должен иметь значение too1. |

### <a name="retrieving-actions"></a>Получение действий
Используйте hello получить метод tooretrieve все действия для расписания.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Используйте hello Get-метод с hello действия Идентификатором tooretrieve определенное действие для расписания.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Создание или изменение действий
Метод Put hello действия идентификатором, который является уникальным toohello расписание toocreate новое действие.  При создании действия в консоли OMS hello GUID является идентификатором hello действия.

> [!NOTE]
> Имя Hello все сохраненные поисковые запросы, отчеты и действия, созданные с помощью hello API аналитики журналов должно быть в нижнем регистре.

Метод Put hello с существующие действием, идентификатор hello же сохраненный поиск toomodify, который в расписании.  текст Hello hello запроса должен содержать etag hello hello расписания.

Формат запроса Hello для создания нового действия зависит от типа действия, поэтому эти образцы приведены в следующих разделах hello.

### <a name="deleting-actions"></a>Удаление действий
Метод Delete hello с hello действия Идентификатором toodelete действие.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Действия оповещений
Расписание должно включать одно-единственное действие оповещения.  Оповещения имеют один или несколько разделов hello в hello в следующей таблице.  Они более подробно описаны далее.

| Раздел | Описание |
|:--- |:--- |
| Пороговое значение |Критерии, когда выполняется действие hello. |
| EmailNotification |Отправьте почту toomultiple получателей. |
| Исправление |Запуск runbook в автоматизации Azure tooattempt toocorrect обнаружить проблему. |

#### <a name="thresholds"></a>Пороговые значения
Действие оповещения должно включать одно-единственное пороговое значение.  При hello сохраненного поиска совпадения порог hello в действие, связанное с поиска, запускаются другие процессы в это действие.  Действие также может содержать только пороговое значение, чтобы его можно было использовать с действиями других типов, которые не содержат пороговых значений.

Пороговые значения имеют свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| operator |Оператор сравнения hello пороговое значение. <br> gt — больше <br> lt = меньше чем |
| Значение |Значение порога hello. |

Например, рассмотрим запрос событий с интервалом (свойство Interval) 15 минут, временным диапазоном (свойство TimeSpan) 30 минут и пороговым значением больше 10. В этом случае hello запрос будет выполняться каждые 15 минут, и будет запускаться оповещение, если возвращается 10 событий, созданные в течение определенного интервала 30 минут.

Ниже приведен пример ответа для действия, содержащего только пороговое значение.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

Используйте метод Put hello с уникальные действия Идентификатором toocreate новое действие пороговое значение для расписания.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Используйте метод Put hello с существующие идентификатор действия toomodify действия пороговое значение для расписания.  текст Hello hello запроса должен содержать hello etag действие hello.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>Уведомление по электронной почте
Уведомления по электронной почте Отправить почту tooone или нескольких получателей.  Они включают свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| Recipients |Список адресов электронной почты. |
| Субъект |Тема Hello почты hello. |
| Вложение |Вложения пока не поддерживаются, поэтому это свойство всегда будет иметь значение None. |

Ниже приведен пример ответа для действия уведомления по электронной почте с пороговым значением.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Используйте метод Put hello с уникальные действия Идентификатором toocreate новое действие электронной почты для расписания.  Hello следующем примере создается уведомление по электронной почте с пороговым значением, если результаты hello hello сохраненного поиска превышает порог hello отправляется сообщение hello.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Используйте метод Put hello с существующие идентификатор действия toomodify действия электронной почты для расписания.  текст Hello hello запроса должен содержать hello etag действие hello.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Действия исправления
Исправления запустить runbook в автоматизации Azure, которую пытается выполнить toocorrect hello проблему, связанную с hello предупреждение.  Необходимо создать веб-перехватчика для hello runbook, используемых в действие исправления и затем укажите hello URI в hello WebhookUri свойство.  При создании этого действия, с помощью консоли OMS hello, для модуля runbook hello автоматически создается новое веб-перехватчика.

Исправления включены свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| RunbookName |Имя hello runbook. Оно должно совпадать опубликованного модуля runbook в автоматизации hello учетной записи, настроенной в hello решение автоматизации в рабочую область OMS. |
| WebhookUri |URI веб-перехватчика hello. |
| Expiry |Дата окончания срока действия Hello и время веб-перехватчика hello.  Если веб-перехватчика hello не имеет срока действия, это может быть любой допустимый будущую дату. |

Ниже приведен пример ответа для действия исправления с пороговым значением.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

Используйте метод Put hello с уникальным действия Идентификатором toocreate новое действие исправления для расписания.  Hello пример создает исправление с пороговым значением, hello runbook запускается в том случае, если результаты hello hello сохраненного поиска превышает порог hello.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Используйте метод Put hello с существующие toomodify идентификатор действия действие исправления для расписания.  текст Hello hello запроса должен содержать hello etag действие hello.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Пример
Ниже приведен полный пример toocreate новое оповещение по электронной почте.  Создается новое расписание, а также действие, содержащее пороговое значение и сообщение электронной почты.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Действия webhook
Действия веб-перехватчика запустить процесс путем вызова URL-адрес и Дополнительно может предоставлять полезные данные toobe отправлено.  Они являются подобные действия tooRemediation, за исключением того, они предназначены для веб-перехватчиков, который может вызывать процессами, отличными от Runbook автоматизации Azure.  Они также предоставляют hello дополнительную возможность предоставления удаленных процессов toohello toobe доставляется полезных данных.

Действия веб-перехватчика нет порогового значения, но вместо этого следует добавить tooa расписание, которое имеет действие по оповещению с пороговым значением.  Можно добавить несколько действий веб-перехватчика, все выполняемые при достижении порога hello.

Веб-перехватчика действия включают свойства hello в hello в следующей таблице.

| Свойство | Описание |
|:--- |:--- |
| WebhookUri |Тема Hello почты hello. |
| CustomPayload |Настраиваемые полезные данные отправлены toobe toohello веб-перехватчика.  Формат Hello будет зависеть от ожидается какой веб-перехватчика hello. |

Ниже приведен пример ответа для действия webhook и соответствующее действие оповещения с пороговым значением.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>Создание или изменение действий webhook
Используйте метод Put hello с уникальные действия Идентификатором toocreate новое действие веб-перехватчика для расписания.  Hello следующем примере создается действие веб-перехватчика или предупреждений с пороговым значением, чтобы веб-перехватчика hello будут создаваться при hello результаты hello сохраненного поиска превышает порог hello.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Используйте метод Put hello с существующие идентификатор действия toomodify действия веб-перехватчика для расписания.  текст Hello hello запроса должен содержать hello etag действие hello.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Дальнейшие действия
* Используйте hello [REST API поиска журналов tooperform](log-analytics-log-search-api.md) в службе анализа журналов.

