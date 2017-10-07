---
title: "веб-перехватчика, журнал действий Azure предупреждения о aaaCall | Документы Microsoft"
description: "Маршрут активности журнала событий tooother служб для пользовательских действий. Например, можно отправлять SMS, вести журнал ошибок или уведомлять команду через службу чата или обмена сообщениями."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>Вызов webhook для оповещений журнала действий Azure
Веб-Перехватчики позволяют tooroute Azure предупреждения системы tooother уведомления для выполнения завершающей обработки или пользовательских действий. Можно использовать веб-перехватчика предупреждения tooroute его tooservices, отправляющие SMS, журнал ошибок, уведомление команды через чат и обмена сообщениями службы либо не любое количество других действий. В этой статье описывается, как tooset toobe веб-перехватчика вызывается, когда срабатывает оповещение журнал действий Azure. Здесь также показано, какие полезные данные hello веб-hello HTTP POST tooa перехватчика имеет следующий вид. Сведения по установке hello и схемы для Azure метрики предупреждения [видите эту страницу вместо](insights-webhooks-alerts.md). Можно также настроить журнал действий toosend оповещений по электронной почте при активации.

> [!NOTE]
> Эта функция в настоящее время находится в предварительной версии и будет удален в одном из будущих hello.
>
>

Можно настроить предупреждения журнал действий по hello [командлеты PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [CLI кросс-платформенных](insights-cli-samples.md#work-with-alerts), или [API REST Azure монитор](https://msdn.microsoft.com/library/azure/dn933805.aspx). В настоящее время невозможно задать один с помощью портала Azure hello.

## <a name="authenticating-hello-webhook"></a>Проверка подлинности веб-перехватчика hello
веб-перехватчика Hello могут проходить проверку подлинности с помощью любого из этих методов:

1. **Авторизация на основе маркера** -hello URI сохраняется маркера идентификатором, например, веб-перехватчика`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **Базовую авторизацию** -hello URI сохраняется имя пользователя и пароль, например, веб-перехватчика`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>Схема полезных данных
Hello операции POST содержит следующие полезные данные JSON и схемы для всех журнал действий оповещения hello. Данная схема предназначена аналогичные toohello один используемые метрики оповещений.

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| Имя элемента | Описание |
| --- | --- |
| status |Используется для оповещений на основе метрик. Всегда устанавливайте слишком «активированной» для предупреждения в журнал действий. |
| context |Контекст события hello. |
| resourceProviderName |поставщик ресурсов Hello hello влияния ресурсов. |
| conditionType |Всегда имеет значение Event. |
| name |Имя правила оповещения hello. |
| id |Идентификатор ресурса hello предупреждение. |
| Описание |Описание предупреждения как набор во время создания оповещения hello. |
| subscriptionId |Идентификатор подписки Azure. |
| Timestamp |Время, на какие hello было создано событие hello служба Azure, которая обработала запрос hello. |
| resourceId |Идентификатор ресурса hello влияния ресурсов. |
| имя_группы_ресурсов |Имя группы ресурсов hello hello затронуто ресурсов |
| properties |Набор `<Key, Value>` пары (т. е. `Dictionary<String, String>`), содержит сведения о событии hello. |
| event |Элемент, который содержит метаданные о событии hello. |
| authorization |Hello свойства RBAC события hello. Обычно они включают hello «действие» и «роль» hello «scope.» |
| category |Категория событий hello. Поддерживаются следующие значения: Administrative, Alert, Security, ServiceHealth, Recommendation. |
| caller |Адрес электронной почты hello пользователя, выполнившего операцию hello, утверждение имени участника-пользователя или утверждение имени участника-службы на основе доступности. Может иметь значение NULL для определенных системных вызовов. |
| correlationId |Обычно GUID в строковом формате. События с correlationId принадлежат toohello большего действие и обычно обладают correlationId. |
| eventDescription |Описание статический текст hello события. |
| eventDataId |Уникальный идентификатор для события hello. |
| eventSource |Имя hello службы Azure или инфраструктуры созданный hello события. |
| httpRequest |Обычно включает hello «clientRequestId», «clientIpAddress» и «method» (метод HTTP, например PUT). |
| level |Одно из hello следующие значения: «Критические», «Ошибка», «Предупреждение», «Информация» и «Подробно». |
| operationId |Как правило, GUID совместно hello событий, соответствующих toosingle операции. |
| operationName |Имя операции hello. |
| properties |Свойства события hello. |
| status |Строка. Состояние операции hello. Обычные значения: Started, In Progress, Succeeded, Failed, Active, Resolved. |
| subStatus |Обычно содержит код состояния HTTP hello hello соответствующего вызова REST. Может также включать другие строки, описывающие подсостояние. Обычные значения подсостояния: OK (код состояния HTTP: 200), Created (код состояния HTTP: 201), Accepted (код состояния HTTP: 202), No Content (код состояния HTTP: 204), Bad Request (код состояния HTTP: 400), Not Found (код состояния HTTP: 404), Conflict (код состояния HTTP: 409), Internal Server Error (код состояния HTTP: 500), Service Unavailable (код состояния HTTP: 503), Gateway Timeout (код состояния HTTP: 504). |

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о hello журнал действий](monitoring-overview-activity-logs.md)
* [Выполнение скриптов службы автоматизации Azure (Runbooks) на основе оповещений Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Используйте логику приложения toosend SMS через Twilio из Azure предупреждения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). В этом примере — для метрики оповещений, но может быть измененный toowork с предупреждением журнал действий.
* [Используйте приложение логики toosend резерв сообщение от Azure предупреждение](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). В этом примере — для метрики оповещений, но может быть измененный toowork с предупреждением журнал действий.
* [Используйте логику приложения toosend tooan сообщения очереди Azure на основе Azure предупреждения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). В этом примере — для метрики оповещений, но может быть измененный toowork с предупреждением журнал действий.
