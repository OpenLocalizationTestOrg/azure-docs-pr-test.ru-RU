---
title: "aaaUnderstand hello веб-перехватчика схемы, используемой в оповещения журнала действий | Документы Microsoft"
description: "Дополнительные сведения о схеме hello hello JSON, URL-адрес веб-перехватчика tooa учитывается при активации оповещения журнала действий."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Веб-перехватчики для оповещений журнала действий Azure
Как часть определения hello группы действий можно настроить веб-перехватчика конечные точки tooreceive активности журнала уведомлений о предупреждениях. С веб-привязок можно направить эти системы tooother уведомлений для выполнения завершающей обработки или пользовательских действий. В этой статье показано, какие полезные данные hello веб-hello HTTP POST tooa перехватчика имеет следующий вид.

Дополнительные сведения об оповещениях журнала действий см. в разделе как слишком[создания предупреждения журнала действий Azure](monitoring-activity-log-alerts.md).

Сведения о группах действия в разделе как слишком[создания групп действий](monitoring-action-groups.md).

## <a name="authenticate-hello-webhook"></a>Проверка подлинности веб-перехватчика hello
веб-перехватчика Hello при необходимости можно использовать токены авторизации для проверки подлинности. Здравствуйте, URI сохраняется маркера идентификатором, например, веб-перехватчика `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>Схема полезных данных
полезные данные JSON Hello, содержащихся в hello операции POST различается в зависимости от полей data.context.activityLog.eventSource hello полезных данных.

###<a name="common"></a>Common
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a>Administrative
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a>ServiceHealth
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

Сведения о конкретной схеме оповещений журнала действий для уведомлений о работоспособности службы см. в статье [Уведомления о работоспособности службы](monitoring-service-notifications.md).

Конкретной схемы на все другие предупреждения журнала действий Подробнее [Обзор журнала действий Azure hello](monitoring-overview-activity-logs.md).

| Имя элемента | Описание |
| --- | --- |
| status |Используется для оповещений на основе метрик. Всегда устанавливайте слишком «активированной» для предупреждения журнала действий. |
| context |Контекст события hello. |
| resourceProviderName |поставщик ресурсов Hello hello влияния ресурсов. |
| conditionType |Всегда имеет значение Event. |
| name |Имя правила оповещения hello. |
| id |Идентификатор ресурса hello предупреждение. |
| Описание |Описание предупреждения, задается при создании предупреждения hello. |
| subscriptionId |Идентификатор подписки Azure. |
| Timestamp |Время, на какие hello было создано событие hello служба Azure, которая обработала запрос hello. |
| resourceId |Идентификатор ресурса hello влияния ресурсов. |
| имя_группы_ресурсов |Имя группы ресурсов hello hello влияния ресурсов. |
| properties |Набор `<Key, Value>` пары (то есть, `Dictionary<String, String>`), содержит сведения о событии hello. |
| event |Элемент, который содержит метаданные о событии hello. |
| authorization |свойства управления доступом на основе ролей Hello hello события. Эти свойства являются действие hello, hello роль и область hello. |
| category |Категория событий hello. Поддерживаются следующие значения: Administrative, Alert, Security, ServiceHealth, Recommendation. |
| caller |Адрес электронной почты hello пользователя, выполнившего операцию hello, утверждение имени участника-пользователя или утверждение имени участника-службы на основе доступности. Может иметь значение NULL для определенных системных вызовов. |
| correlationId |Обычно GUID в строковом формате. События с correlationId принадлежат toohello большего действие и обычно обладают correlationId. |
| eventDescription |Описание статический текст hello события. |
| eventDataId |Уникальный идентификатор для события hello. |
| eventSource |Имя hello службы Azure или инфраструктуры созданный hello события. |
| httpRequest |Hello запрос обычно включает hello clientRequestId, clientIpAddress и метод HTTP (например, ПОМЕСТИТЕ). |
| level |Одно из последующих значений hello: критическое, ошибка, предупреждение, информационное сообщение и Verbose. |
| operationId |Как правило, GUID совместно hello событий, соответствующих toosingle операции. |
| operationName |Имя операции hello. |
| properties |Свойства события hello. |
| status |Строка. Состояние операции hello. Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus |Обычно содержит код состояния HTTP hello hello соответствующего вызова REST. Может также включать другие строки, описывающие подсостояние. Обычные значения подсостояния: OK (код состояния HTTP: 200), Created (код состояния HTTP: 201), Accepted (код состояния HTTP: 202), No Content (код состояния HTTP: 204), Bad Request (код состояния HTTP: 400), Not Found (код состояния HTTP: 404), Conflict (код состояния HTTP: 409), Internal Server Error (код состояния HTTP: 500), Service Unavailable (код состояния HTTP: 503), Gateway Timeout (код состояния HTTP: 504). |

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о журнале действий hello](monitoring-overview-activity-logs.md).
* [Using Azure Automation to take action on Azure Alerts](http://go.microsoft.com/fwlink/?LinkId=627081) (Использование службы автоматизации Azure для выполнения действий по уведомлениям Azure).
* [Используйте логику приложения toosend SMS через Twilio из Azure предупреждения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). Этот пример предназначен для метрики оповещений, но может быть измененный toowork с предупреждением журнала действий.
* [Используйте логику приложения toosend резерв сообщение от Azure предупреждение](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). Этот пример предназначен для метрики оповещений, но может быть измененный toowork с предупреждением журнала действий.
* [Использовать toosend логику приложения, очередь сообщений tooan Azure из Azure предупреждения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). Этот пример предназначен для метрики оповещений, но может быть измененный toowork с предупреждением журнала действий.
