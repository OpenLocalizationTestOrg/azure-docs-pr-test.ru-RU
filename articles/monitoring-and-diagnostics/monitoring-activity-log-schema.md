---
title: "Схема событий журнала активности aaaAzure | Документы Microsoft"
description: "Понимание hello схемы событий для данных, которые передаются в журнал действий hello"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Схема событий журнала действий Azure
Hello **журнал действий Azure** — это журнал, позволяет контролировать все события уровня подписки, которые произошли в Azure. Данная статья содержит hello схема событий в категории данных.

## <a name="administrative"></a>Administrative
Эта категория содержит запись hello всех создавать, выполнять операции обновления, удаления и action через диспетчер ресурсов. Примеры типов событий, отображаемые в этой категории относятся hello «создайте виртуальную машину» и «удалить сетевую группу безопасности «всех действий, выполненных пользователем или приложения с помощью диспетчера ресурсов моделируется как операцию для определенного типа ресурсов. Если тип операции hello записи, Delete или действие, hello начала hello и успех или сбой данной операции записываются в hello административную категорию. Административная категория Hello также включает любой элемент управления доступом на основе toorole изменения в подписку.

### <a name="sample-event"></a>Пример события
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>Описания свойств
| Имя элемента | Description (Описание) |
| --- | --- |
| authorization |Большой двоичный объект свойства RBAC события hello. Обычно включает hello свойства «действие», «роль» и «область». |
| caller |Адрес электронной почты пользователя hello, который выполнил операцию hello, утверждение имени участника-пользователя или утверждение имени участника-службы на основе доступности. |
| каналов |Одно из hello следующие значения: «Администратор», «Операция» |
| claims |токен JWT Hello используется Active Directory tooauthenticate hello пользователь или приложение tooperform эту операцию в диспетчер ресурсов. |
| correlationId |Как правило, GUID в строковом формате hello. События, которые совместно используют correlationId принадлежат toohello же действию. |
| Описание |Статическое описание события в текстовом виде. |
| eventDataId |Уникальный идентификатор события. |
| httpRequest |BLOB-объектов описания hello HTTP-запроса. Обычно включает hello «clientRequestId», «clientIpAddress» и «method» (метод HTTP. например PUT). |
| level |Уровень события hello. Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный» |
| имя_группы_ресурсов |Имя группы ресурсов hello hello влияния ресурсов. |
| resourceProviderName |Имя поставщика ресурсов hello hello затронуто ресурсов |
| resourceId |Идентификатор ресурса hello влияния ресурсов. |
| operationId |Идентификатор GUID, совместно используемые hello события, которые соответствуют tooa одной операции. |
| operationName |Имя операции hello. |
| properties |Набор `<Key, Value>` пары (то есть, словарь), описывающий hello подробных сведениях события hello. |
| status |Строка, описывающая состояние hello hello операции. Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus |Обычно hello hello соответствующего вызова REST код состояния HTTP, но может также включать другие строки, описывающие подсостояния, таких как следующие общие значения: OK (код состояния HTTP: 200), созданный (код состояния HTTP: 201) приняты (код состояния HTTP: 202), нет содержимого (HTTP Код состояния: 204), неправильный запрос (код состояния HTTP: 400), не найдено (код состояния HTTP: 404), конфликт (код состояния HTTP: 409), Внутренняя ошибка сервера (код состояния HTTP: 500), служба недоступна (код состояния HTTP: 503), истекло время ожидания шлюза (код состояния HTTP: 504). |
| eventTimestamp |Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello. |
| submissionTimestamp |Отметка времени события hello стало доступно для запросов. |
| subscriptionId |Идентификатор подписки Azure. |

## <a name="service-health"></a>Работоспособность службы
Эта категория содержит запись hello любой службы работоспособности инцидентов, произошедших в Azure. Пример hello тип события, отображаемые в этой категории — «SQL Azure в регионе Восток США испытывает времени простоя». События работоспособности службы бывают пять видов: требуется действие вспомогательная восстановления, инцидент, обслуживания, сведения и безопасности и появятся только при наличии ресурсов, в подписке hello, которое бы повлиять hello событий.

### <a name="sample-event"></a>Пример события
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>Описания свойств
Имя элемента | Описание
-------- | -----------
каналов | Является одним из hello следующие значения: «Администратор», «Операция»
correlationId | Обычно представляет собой идентификатор GUID в строковом формате hello. События, принадлежат toohello же действию обычно обладают hello же correlationId.
Описание | Описание события hello.
eventDataId | Hello уникальный идентификатор события.
eventName | Заголовок события hello Hello.
level | Уровень события hello. Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный»
resourceProviderName | Имя поставщика ресурсов hello hello влияния ресурсов. Если неизвестно, то значение будет null.
тип_ресурса| Тип ресурса hello Hello влияния ресурсов. Если неизвестно, то значение будет null.
subStatus | Обычно для событий работоспособности службы имеет значение null.
eventTimestamp | Метка времени hello журнал событий был создан и отправлен toohello журнал действий.
submissionTimestamp |   Отметка времени события hello стала доступна для hello журнал действий.
subscriptionId | Здравствуйте, подписки Azure, в котором было зарегистрировано это событие.
status | Строка, описывающая состояние hello hello операции. Распространенные значения: Active (Активно), Resolved (Разрешено).
operationName | Имя операции hello. Обычно имеет значение Microsoft.ServiceHealth/incident/action.
category | ServiceHealth
resourceId | Идентификатор ресурса hello влияния ресурсов, если он известен. В противном случае указывается идентификатор подписки.
Properties.title | Hello локализованное название для обмена данными. Используется английский язык по умолчанию hello.
Properties.communication | Подробные сведения о локализации Hello hello связи с разметкой HTML. По умолчанию hello является английский.
Properties.incidentType | Возможные значения: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security.
Properties.trackingId | Определяет инцидент hello, это событие, связанное с. Используйте этот инцидент связанные tooan toocorrelate события hello.
Properties.impactedServices | Escape-blob JSON, описывающий hello служб и регионов, которые влияет инцидент hello. Список служб Services, каждая из которых содержит ServiceName, и список регионов ImpactedRegions, каждый из которых содержит RegionName.
Properties.defaultLanguageTitle | Hello взаимодействие на английском языке
Properties.defaultLanguageContent | Hello взаимодействие на английском языке, как обычный текст или HTML-разметка
Properties.stage | Возможные значения для AssistedRecovery, ActionRequired, Information, Incident, Security: Active, Resolved. Возможные значения для Maintenance: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete.
Properties.communicationId | связи Hello связано это событие.

## <a name="alert"></a>Предупреждение
Эта категория содержит hello записи для всех активаций оповещения Azure. Пример hello тип события, отображаемые в этой категории — «% ЦП на myVM был более чем на 80 для hello за последние 5 минут.» Различные системы Azure работают по принципу оповещений, то есть вы можете определить какое-то правило, и система будет направлять вам уведомление, когда условия этого правила выполняются. Каждый раз, поддерживаемых Azure тип оповещения «активирует,» или hello условия выполнены toogenerate уведомление, запись активации hello также помещается toothis категории hello журнал действий.

### <a name="sample-event"></a>Пример события

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>Описания свойств
| Имя элемента | Описание |
| --- | --- |
| caller | Всегда имеет значение Microsoft.Insights/alertRules. |
| каналов | Всегда имеет значение "Admin, Operation". |
| claims | Большой двоичный объект JSON с hello имени участника-службы (имя участника-службы) или ресурс типа, обработчик оповещений hello. |
| correlationId | Идентификатор GUID в строковом формате hello. |
| Описание |Описание события оповещения hello статический текст. |
| eventDataId |Уникальный идентификатор события hello для оповещения. |
| level |Уровень события hello. Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный» |
| имя_группы_ресурсов |Имя группы ресурсов hello hello влияет ресурсов является метрики предупреждение. Для других типов оповещений это имя hello hello группы ресурсов, содержащий предупреждение hello сам. |
| resourceProviderName |Имя поставщика ресурсов hello hello влияет ресурсов является метрики предупреждение. Другие типы оповещений это hello имя поставщика ресурсов hello для оповещения hello сам. |
| resourceId | Имя ресурса с идентификатором hello hello влияет ресурсов является метрики предупреждение. Другие типы оповещений это идентификатор ресурса hello сам ресурс предупреждения hello. |
| operationId |Идентификатор GUID, совместно используемые hello события, которые соответствуют tooa одной операции. |
| operationName |Имя операции hello. |
| properties |Набор `<Key, Value>` пары (то есть, словарь), описывающий hello подробных сведениях события hello. |
| status |Строка, описывающая состояние hello hello операции. Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus | Обычно для оповещений имеет значение null. |
| eventTimestamp |Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello. |
| submissionTimestamp |Отметка времени события hello стало доступно для запросов. |
| subscriptionId |Идентификатор подписки Azure. |

### <a name="properties-field-per-alert-type"></a>Поле свойств по типу оповещения
поле свойств Hello будет содержать разные значения в зависимости от источника hello hello события для оповещения. Два распространенных поставщика событий оповещений — оповещения журнала действий и оповещения метрик.

#### <a name="properties-for-activity-log-alerts"></a>Свойства оповещений журнала действий
| Имя элемента | Описание |
| --- | --- |
| properties.subscriptionId | Идентификатор подписки Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован. |
| properties.eventDataId | Hello идентификатора данных события в журнал событий hello действие, вызвавшее активации этого правила оповещения toobe действия журнала. |
| properties.resourceGroup | Группа ресурсов Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован. |
| properties.resourceId | Идентификатор ресурса Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован. |
| properties.eventTimestamp | Hello событий отметка времени события журнала действие hello, вызвавший этот toobe правило оповещения журнала активности активирован. |
| properties.operationName | Имя операции Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован. |
| properties.status | состояние Hello из hello действия журнал событий, вызвавший этот toobe правило оповещения журнала активности активирован.|

#### <a name="properties-for-metric-alerts"></a>Свойства оповещений метрик
| Имя элемента | Описание |
| --- | --- |
| properties.RuleUri | Идентификатор ресурса hello метрики правило генерации оповещений сам. |
| properties.RuleName | Имя метрики правило генерации оповещений hello Hello. |
| properties.RuleDescription | Описание Hello правило генерации оповещений метрики hello (как определено правило генерации оповещений hello). |
| properties.Threshold | Пороговое значение Hello вычислении hello hello метрики правила оповещения. |
| properties.WindowSizeInMinutes | размер окна Hello вычислении hello hello метрики правила оповещения. |
| properties.Aggregation | Hello статистической обработки типа, определенного в hello метрики правило оповещения. |
| properties.Operator | условный оператор Hello вычислении hello hello метрики правила оповещения. |
| properties.MetricName | Имя метрики Hello hello метрику, используемую при вычислении hello hello метрики правило оповещения. |
| properties.MetricUnit | Единица измерения Hello метрики для hello метрику, используемую при вычислении hello hello метрики правило оповещения. |

## <a name="autoscale"></a>Autoscale
Эта категория содержит запись hello любой операции toohello связанные события подсистемы автомасштабирования hello соответствии с параметрами автоматического масштабирования, установленных в вашей подписке. Пример hello тип события, отображаемые в этой категории — «Автомасштабирования масштабирования вверх не удалось выполнить действие». С помощью автоматического масштабирования, можно автоматически масштабировать или масштабирования в hello число экземпляров в типе поддерживаемых ресурсов на основе времени дня и/или загрузки данных (метрики), с помощью параметров автоматического масштабирования. При выполнении условий hello tooscale вверх или вниз, hello start и успешно или сбой события будут регистрироваться в этой категории.

### <a name="sample-event"></a>Пример события
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>Описания свойств
| Имя элемента | Описание |
| --- | --- |
| caller | Всегда имеет значение Microsoft.Insights/autoscaleSettings. |
| каналов | Всегда имеет значение "Admin, Operation". |
| claims | Большой двоичный объект JSON с помощью имени участника-службы (имя участника-службы) или ресурс типа подсистемы автомасштабирования hello hello. |
| correlationId | Идентификатор GUID в строковом формате hello. |
| Описание |Описание статический текст hello автомасштабирования события. |
| eventDataId |Уникальный идентификатор события автомасштабирования hello. |
| level |Уровень события hello. Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробный» |
| имя_группы_ресурсов |Имя группы ресурсов hello параметра автомасштабирования hello. |
| resourceProviderName |Имя поставщика ресурсов hello параметра автомасштабирования hello. |
| resourceId |Идентификатор ресурса параметра автомасштабирования hello. |
| operationId |Идентификатор GUID, совместно используемые hello события, которые соответствуют tooa одной операции. |
| operationName |Имя операции hello. |
| properties |Набор `<Key, Value>` пары (то есть, словарь), описывающий hello подробных сведениях события hello. |
| properties.Description | Подробное описание того, какой механизм автоматического масштабирования hello делало. |
| properties.ResourceName | Идентификатор ресурса hello затронуто ресурсов (hello ресурса, на какие hello выполнявшаяся масштабирования) |
| properties.OldInstancesCount | Hello число экземпляров перед выполнением действия автомасштабирования hello действует. |
| properties.NewInstancesCount | Hello число экземпляров после выполнения действия автомасштабирования hello действует. |
| properties.LastScaleActionTime | Hello отметка времени дату и время действия автомасштабирования hello. |
| status |Строка, описывающая состояние hello hello операции. Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus | Обычно для автоматического масштабирования имеет значение null. |
| eventTimestamp |Отметка времени, когда hello событий, созданных hello hello Azure служба обработки запроса соответствующее событие hello. |
| submissionTimestamp |Отметка времени события hello стало доступно для запросов. |
| subscriptionId |Идентификатор подписки Azure. |

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о hello журнал действий (прежнее название — журналы аудита)](monitoring-overview-activity-logs.md)
* [Поток tooEvent журнал действий Azure hello концентраторы](monitoring-stream-activity-logs-event-hubs.md)
