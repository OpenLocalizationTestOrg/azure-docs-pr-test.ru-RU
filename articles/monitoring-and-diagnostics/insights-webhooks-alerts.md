---
title: "веб-перехватчиков aaaConfigure на оповещения Azure метрики | Документы Microsoft"
description: "Переадресация систем не Azure tooother оповещения Azure."
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Настройка объектов webhook для оповещений на основе метрик Azure
Веб-Перехватчики позволяют tooroute Azure предупреждения системы tooother уведомления для выполнения завершающей обработки или пользовательских действий. Можно использовать веб-перехватчика предупреждения tooroute его tooservices, отправляющие SMS, журнал ошибок, уведомление команды через чат и обмена сообщениями службы либо не любое количество других действий. В этой статье описывается как tooset веб-перехватчика на оповещение Azure метрики и какие полезные данные hello веб-перехватчика tooa HTTP POST hello выглядит следующим образом. Сведения по установке hello и схемы для оповещения (предупреждение о событиях), журнал действий Azure [видите эту страницу вместо](insights-auditlog-to-webhook-email.md).

Содержание оповещения hello HTTP POST в формате JSON оповещения Azure схема определена ниже веб-перехватчика tooa URI, указываемое при создании предупреждения hello. Этот URI должен быть допустимой конечной точкой HTTP или HTTPS. При активации оповещений Azure размещает одну запись для каждого запроса.

## <a name="configuring-webhooks-via-hello-portal"></a>Настройка веб-перехватчиков через портал hello
Можно добавить или обновить веб-перехватчика hello URI hello экране оповещения для создания или обновления в hello [портала](https://portal.azure.com/).

![Добавить правило оповещения](./media/insights-webhooks-alerts/Alertwebhook.png)

Можно также настроить перехватчик tooa предупреждения toopost URI с помощью hello [командлеты PowerShell Azure](insights-powershell-samples.md#create-metric-alerts), [CLI кросс-платформенных](insights-cli-samples.md#work-with-alerts), или [API REST Azure монитор](https://msdn.microsoft.com/library/azure/dn933805.aspx).

## <a name="authenticating-hello-webhook"></a>Проверка подлинности веб-перехватчика hello
веб-перехватчика Hello могут проходить проверку подлинности с помощью авторизации на основе маркеров. веб-перехватчика Hello URI сохраняется маркера идентификатором, например. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>Схема полезных данных
Hello операции POST содержит следующие полезные данные JSON и схемы для всех метрики оповещений hello.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| Поле | Обязательно | Фиксированный набор значений | Примечания |
|:--- |:--- |:--- |:--- |
| status |Да |Activated, Resolved |Состояние для hello оповещения на основе этих условий hello установки. |
| context |Да | |контекст предупреждения Hello. |
| Timestamp |Да | |время Hello, на какие hello оповещение вызвано. |
| id |Да | |Каждое правило оповещения имеет уникальный идентификатор. |
| name |Да | |Имя предупреждения Hello. |
| Описание |Да | |Описание предупреждения hello. |
| conditionType |Да |Metric, Event |Поддерживаются два типа оповещений: Один на метрики условиях и hello другие на основе события в журнал действий hello. Используйте toocheck это значение, если hello оповещения на основе метрики или событий. |
| condition |Да | |Hello toocheck определенных полей для на основании hello тип условия. |
| metricName |Для оповещений на основе метрик | |отслеживает Hello имя метрики hello, которое определяет правила какие hello. |
| metricUnit |Для оповещений на основе метрик |Bytes, BytesPerSecond, Count, CountPerSecond, Percent, Seconds |Единица Hello в метрика hello. [здесь](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |Для оповещений на основе метрик | |Hello фактическое значение показателя hello, вызвавшего предупреждение hello. |
| threshold |Для оповещений на основе метрик | |Пороговое значение Hello, на какие hello активации оповещения. |
| windowSize |Для оповещений на основе метрик | |период времени, это действие используется toomonitor предупреждения, на основе порогового значения hello Hello. Это должен быть период от 5 минут до 1 дня. Формат длительности — ISO 8601. |
| timeAggregation |Для оповещений на основе метрик |Average, Last, Maximum, Minimum, None, Total |Способ объединения собираемых данных hello со временем. значение по умолчанию Hello — среднее значение. [здесь](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| operator |Для оповещений на основе метрик | |Hello оператор, используемый toocompare hello текущего данные метрик toohello заданное пороговое значение. |
| subscriptionId |Да | |Идентификатор подписки Azure. |
| имя_группы_ресурсов |Да | |Имя группы ресурсов hello hello влияния ресурсов. |
| resourceName |Да | |Имя ресурса hello влияния ресурсов. |
| тип_ресурса |Да | |Тип ресурса hello влияния ресурсов. |
| resourceId |Да | |Идентификатор ресурса hello влияния ресурсов. |
| resourceRegion |Да | |Регион или расположение hello повлияет на ресурс. |
| portalLink |Да | |Прямая связь toohello портала ресурсов страница «Сводка». |
| properties |Нет |Необязательно |Набор `<Key, Value>` пары (т. е. `Dictionary<String, String>`), содержит сведения о событии hello. поле свойств Hello является необязательным. В пользовательских пользовательского интерфейса или логику на основе приложения рабочего процесса для ввода ключа и значения, которые могут быть переданы через hello полезных данных. веб-перехватчика Hello альтернативный способ toopass пользовательские свойства задней toohello можно с помощью uri hello веб-перехватчика себя (как параметры запроса) |

> [!NOTE]
> Hello свойства поля можно задать только с помощью hello [API REST Azure монитор](https://msdn.microsoft.com/library/azure/dn933805.aspx).
>
>

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о оповещения Azure и веб-привязок в видео hello [интегрировать Azure предупреждения с PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Выполнение скриптов службы автоматизации Azure (Runbooks) на основе оповещений Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Используйте логику приложения toosend SMS через Twilio из Azure оповещения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [Использование приложения логики toosend резерв сообщения из Azure оповещения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [Используйте логику приложения toosend tooan сообщения очереди Azure из Azure оповещения](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
