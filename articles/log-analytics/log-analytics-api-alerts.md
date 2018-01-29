---
title: "Использование REST API оповещений Log Analytics в OMS"
description: "REST API оповещений Log Analytics позволяет создавать оповещения и управлять ими в Log Analytics — компоненте Operations Management Suite (OMS).  В этой статье приводятся сведения об интерфейсе API и примеры выполнения различных операций."
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
ms.openlocfilehash: 5ce72ffef4394bf3bbe39fa420c4fcaa965ae35c
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Создание правил генерации оповещений и управление ими в Log Analytics с помощью REST API
REST API оповещений в Log Analytics позволяет создавать оповещения и управлять ими в Operations Management Suite (OMS).  В этой статье приводятся сведения об интерфейсе API и примеры выполнения различных операций.

Для поиска в службе Log Analytics используется REST API категории RESTful — к нему можно получить доступ с помощью REST API Azure Resource Manager. В этом документе вы найдете примеры, когда доступ к API из командной строки PowerShell осуществляется через [ARMClient](https://github.com/projectkudu/ARMClient) — инструмент командной строки с открытым исходным кодом, который упрощает вызов API Azure Resource Manager. Использование ARMClient и PowerShell — это один из множества вариантов получения доступа к API поиска по службе Log Analytics. С помощью этих средств можно использовать API диспетчера ресурсов Azure категории RESTful для осуществления вызовов рабочих областей OMS и выполнения команд поиска в них. API будет выдавать результаты поиска в формате JSON, позволяя программно использовать результаты поиска различными способами.

## <a name="prerequisites"></a>Предварительные требования
В настоящее время оповещения могут создаваться только с помощью сохраненного поиска в службе Log Analytics.  Дополнительные сведения см. в статье [REST API поиска в журналах](log-analytics-log-search-api.md).

## <a name="schedules"></a>Расписания
Сохраненный поиск может включать одно расписание или несколько. Расписание определяет, как часто выполняется поиск, а также интервал времени для определения условий.
У расписаний есть свойства, приведенные в таблице ниже.

| Свойство | Описание |
|:--- |:--- |
| Интервал |Насколько часто выполняется поиск. Измеряется в минутах. |
| QueryTimeSpan |Интервал времени для вычисления условий. Значение должно быть больше или равно значению свойства Interval. Измеряется в минутах. |
| Version (версия) |Используемая версия API.  Сейчас это свойство всегда должно иметь значение 1. |

Например, рассмотрим запрос событий с интервалом (свойство Interval) 15 минут и временным диапазоном (свойство TimeSpan) 30 минут. В этом случае запрос будет выполняться каждые 15 минут, а оповещение будет создаваться, если условие по-прежнему соблюдается по прошествии 30-минутного периода.

### <a name="retrieving-schedules"></a>Получение расписаний
Используйте метод Get для получения всех расписаний для сохраненного поиска.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Чтобы получить конкретное расписание для сохраненного поискового запроса, используйте метод Get с идентификатором расписания.

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
Чтобы создать расписание, используйте метод Put с уникальным идентификатором расписания.  Обратите внимание, что нельзя использовать один и тот же идентификатор для двух расписаний, даже если они связаны с разными сохраненными поисковыми запросами.  При создании расписания в консоли OMS для идентификатора расписания создается GUID.

> [!NOTE]
> Имена всех сохраненных поисковых запросов, отчетов и действий, создаваемых с помощью API Log Analytics, должны быть в нижнем регистре.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Изменение расписания
Чтобы изменить расписание, используйте метод Put с идентификатором существующего расписания для того же сохраненного поискового запроса.  Текст запроса должен содержать Etag расписания.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Удаление расписаний
Чтобы удалить расписание, используйте метод Delete с идентификатором расписания.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Действия
Расписание может включать несколько действий. Действие может определять один выполняемый процесс или несколько (например, отправку почты или запуск модуля Runbook) или задавать пороговое значение, определяющее, когда результаты поиска отвечают некоторым условиям.  Некоторые действия будут определять оба элемента так, чтобы процессы выполнялись при достижении порогового значения.

У всех действий есть свойства, приведенные в таблице ниже.  Разные типы оповещений имеют различные дополнительные свойства, которые описаны ниже.

| Свойство | Описание |
|:--- |:--- |
| Тип |Тип действия.  Сейчас возможными значениями являются Alert и Webhook. |
| Имя |Отображаемое имя оповещения. |
| Version (версия) |Используемая версия API.  Сейчас это свойство всегда должно иметь значение 1. |

### <a name="retrieving-actions"></a>Получение действий
Используйте метод Get для получения всех действий для расписания.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Используйте метод Get с идентификатором действия для получения конкретного действия для расписания.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Создание или изменение действий
Чтобы создать действие, используйте метод Put с идентификатором действия, уникальным для расписания.  При создании действия в консоли OMS для идентификатора действия отображается GUID.

> [!NOTE]
> Имена всех сохраненных поисковых запросов, отчетов и действий, создаваемых с помощью API Log Analytics, должны быть в нижнем регистре.

Чтобы изменить расписание, используйте метод Put с идентификатором существующего действия для того же сохраненного поискового запроса.  Текст запроса должен содержать Etag расписания.

Формат запроса для создания действия зависит от типа действия, поэтому эти примеры приведены в разделах ниже.

### <a name="deleting-actions"></a>Удаление действий
Для удаления действия используйте метод Delete с идентификатором действия.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Действия оповещений
Расписание должно включать одно-единственное действие оповещения.  Действия оповещений включают один или несколько разделов в таблице ниже.  Они более подробно описаны далее.

| Раздел | Описание |
|:--- |:--- |
| Пороговое значение |Условие для запуска действия. |
| EmailNotification |Отправка сообщения нескольким получателям. |
| Исправление |Запуск модуля Runbook в службе автоматизации Azure для попытки исправления выявленной проблемы. |

#### <a name="thresholds"></a>Пороговые значения
Действие оповещения должно включать одно-единственное пороговое значение.  Когда результат сохраненного поиска соответствует пороговому значению в действии, связанном с этим поиском, запускаются другие процессы в этом действии.  Действие также может содержать только пороговое значение, чтобы его можно было использовать с действиями других типов, которые не содержат пороговых значений.

У пороговых значений есть свойства, приведенные в таблице ниже.

| Свойство | Описание |
|:--- |:--- |
| Оператор |Оператор для сравнения порогового значения. <br> gt — больше <br> lt = меньше чем |
| Значение |Пороговое значение. |

Например, рассмотрим запрос событий с интервалом (свойство Interval) 15 минут, временным диапазоном (свойство TimeSpan) 30 минут и пороговым значением больше 10. В этом случае запрос будет выполняться каждые 15 минут, а оповещение будет создаваться при возврате 10 событий, созданных за 30-минутный период.

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

Чтобы создать действие с пороговым значением для расписания, используйте метод Put с уникальным идентификатором действия.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Чтобы изменить действие с пороговым значением для расписания, используйте метод Put с идентификатором существующего действия.  Текст запроса должен содержать Etag действия.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>Уведомление по электронной почте
Уведомления отправляются для одного или нескольких получателей по электронной почте.  Уведомления могут включать свойства, приведенные в таблице ниже.

| Свойство | Описание |
|:--- |:--- |
| Recipients |Список адресов электронной почты. |
| Субъект |Тема сообщения электронной почты. |
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
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Чтобы создать действие почты для расписания, используйте метод Put с уникальным идентификатором действия.  В следующем примере создается уведомление по электронной почте с пороговым значением, которое отправляется в случае, если результаты сохраненного поиска превышают пороговое значение.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Чтобы изменить действие почты для расписания, используйте метод Put с идентификатором существующего действия.  Текст запроса должен содержать Etag действия.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Действия исправления
Служба исправлений запускает модуль Runbook в службе автоматизации Azure, который пытается устранить проблему, указанную в оповещении.  Вам потребуется создать объект webhook для модуля Runbook, используемого в действии исправления, а затем указать его универсальный код ресурса (URI) в свойстве WebhookUri.  При создании этого действия с помощью консоли OMS новый объект webhook для модуля Runbook создается автоматически.

Исправления могут включать свойства, приведенные в таблице ниже.

| Свойство | Описание |
|:--- |:--- |
| RunbookName |Имя модуля Runbook. Оно должно соответствовать имени опубликованного модуля Runbook в учетной записи автоматизации, настроенной в решении автоматизации в рабочей области OMS. |
| WebhookUri |Универсальный код ресурса (URI) объекта webhook. |
| Expiry |Дата и время окончания срока действия объекта webhook.  Если объект webhook не имеет срока действия, это может быть любая допустимая дата в будущем. |

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

Чтобы создать действие исправления для расписания, используйте метод Put с уникальным идентификатором действия.  В следующем примере создается исправление с пороговым значением для запуска модуля Runbook в случае, если результаты сохраненного поиска превышают пороговое значение.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Чтобы изменить действие исправления для расписания, используйте метод Put с идентификатором существующего действия.  Текст запроса должен содержать Etag действия.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Пример
Ниже приведен полный пример создания оповещения по электронной почте.  Создается новое расписание, а также действие, содержащее пороговое значение и сообщение электронной почты.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Действия webhook
Действия webhook запускают процесс путем вызова URL-адреса и, при необходимости, предоставления полезных данных для отправки.  Они похожи на действия исправления, но предназначены для объектов webhook, которые могут вызывать процессы, отличные от модулей Runbook службы автоматизации Azure.  Они также включают дополнительную возможность предоставления полезных данных, доставляемых в удаленный процесс.

Действиям webhook не назначается пороговое значение, однако их необходимо добавлять в расписание, которое включает действие оповещения с пороговым значением.  Можно добавить несколько действий webhook, которые будут выполняться все одновременно при достижении порогового значения.

Действия webhook могут включать свойства, приведенные в таблице ниже.

| Свойство | Описание |
|:--- |:--- |
| WebhookUri |Тема сообщения электронной почты. |
| CustomPayload |Пользовательские полезные данные, отправляемые в объект webhook.  Формат зависит от данных, ожидаемых объектом webhook. |

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
Чтобы создать действие webhook для расписания, используйте метод Put с уникальным идентификатором действия.  В следующем примере создается действие webhook и запускается действие оповещения с пороговым значением, если результаты сохраненного поиска превышают пороговое значение.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Чтобы изменить действие webhook для расписания, используйте метод Put с идентификатором существующего действия.  Текст запроса должен содержать Etag действия.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Дальнейшие действия
* Используйте [REST API для выполнения поиска в журналах](log-analytics-log-search-api.md) в службе Log Analytics.

