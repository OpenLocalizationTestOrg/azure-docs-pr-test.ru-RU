---
title: "Управление API с помощью монитора Azure aaaMonitor | Документы Microsoft"
description: "Узнайте, как службы с помощью монитора Azure toomonitor API управления Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a>Наблюдение за управлением API с помощью Azure Monitor
Azure Monitor — это служба Azure, которая предоставляет единый источник данных для наблюдения за всеми ресурсами Azure. Монитор Azure можно визуализировать, запрос, маршрутизации, архивировать и выполнять действия с метриками hello и журналы, полученные из ресурсов Azure, такие как управление API. 

Здравствуйте, следуя видео показано, как toomonitor управления API, с помощью монитора Azure. Дополнительные сведения об Azure Monitor см. в статье [Приступая к работе с Azure Monitor]. 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>Метрики
Управление API в настоящее время создает пять показателей, мы планируем в будущем hello tooadd. Эти показатели создаются каждую минуту, предоставляя почти в реальном времени отслеживать в состоянии hello и работоспособности собственные интерфейсы API. Ниже приводится сводка hello метрик:
* Общее количество запросов шлюза: hello количество API запрашивает в период hello. 
* Количество успешных запросов шлюза: число hello запросы API, которые получены успешно коды ответа HTTP, включая 304, 307 и меньший, чем 301 (например, 200). 
* Количество неудачных запросов шлюза: hello число запросы API, которые получены ошибочные коды ответа HTTP, включая 400 и ничего больше 500.
* Неавторизованных запросов шлюза: номер hello запросов API, которые получены коды ответа HTTP 401, 403, а 429. 
* Других шлюза запросов: номер hello запросы API, которые получены коды ответа HTTP, не принадлежащие tooany из hello предшествующий категории (например, 418).

Вы можете получить доступ к метрикам в службе управления API или получить доступ к метрикам всех ресурсов Azure в Azure Monitor. метрики tooview в службе управления API.
1. Здравствуйте, откройте портал Azure.
2. Go tooyour службы управления API.
3. Щелкните **Метрики**.

![Колонка метрик][metrics-blade]

Дополнительные сведения о том, как toouse метрик, в разделе [Обзор метрик].

## <a name="activity-logs"></a>Журналы действий
Журналы действий глубже понять hello операций, которые были выполнены на ваши службы управления API. Ранее они назывались журналами аудита или журналами операций. Используя журналы действий, можно определить hello», кто и когда» для любой записи операций (PUT, POST, DELETE), затраченное на ваши службы управления API. 

> [!NOTE]
> Журналы действий не включать операции чтения (GET) или операций, выполняемых в hello классический портал издателя или с помощью hello исходного API-интерфейсы управления.

Вы можете получить доступ к журналам действий в службе управления API или получить доступ к журналам всех ресурсов Azure в Azure Monitor. Действие tooview регистрирует в службе управления API:
1. Здравствуйте, откройте портал Azure.
2. Go tooyour службы управления API.
3. Щелкните **Журнал действий**.

![Колонка журналов действий][activity-logs-blade]

Дополнительные сведения о том, как toouse метрик, в разделе [Общие сведения о журналах активности].

## <a name="alerts"></a>Оповещения
Можно настроить предупреждения tooreceive, основанные на журналах метрик и действия. Монитор Azure позволяет tooconfigure предупреждения toodo hello следующие при инициировании:

* Отправка уведомления по электронной почте.
* Вызов webhook.
* Вызов приложения логики Azure.

Правила оповещений можно настроить в службе управления API или в Azure Monitor. tooconfigure их в службе управления API: 
1. Здравствуйте, откройте портал Azure.
2. Go tooyour службы управления API.
3. Щелкните **Правила оповещения**.

![Колонка "Правила оповещения"][alert-rules-blade]

Дополнительные сведения об использовании оповещений см. в статье [Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure].

## <a name="diagnostic-logs"></a>Журналы диагностики
Журналы диагностики предоставляют подробные сведения об операциях и ошибках, которые важны для аудита, а также для устранения неполадок. Журналы диагностики отличаются от журналов действий. Журналы действий получить представление о hello операций, которые были выполнены на ресурсам Azure. Журналы диагностики дают представление об операциях, выполняемых самим ресурсом.

API управления в данный момент предоставляет диагностики журналы отдельных API (в пакетном режиме каждый час) запрос с каждой записи, наличие hello следующие структуры:

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

Вы можете получить доступ к журналам диагностики в службе управления API или получить доступ к журналам всех ресурсов Azure в Azure Monitor. журналы диагностики tooview в службе управления API:
1. Здравствуйте, откройте портал Azure.
2. Go tooyour службы управления API.
3. Щелкните **Журналы диагностики**.

![Колонка "Журналы диагностики"][diagnostic-logs-blade]

Дополнительные сведения о том, как toouse метрик, в разделе [Обзор журналов диагностики].

## <a name="next-step"></a>Дальнейшее действие

* [Приступая к работе с Azure Monitor]
* [Обзор метрик]
* [Общие сведения о журналах активности]
* [Обзор журналов диагностики]
* [Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure]

[Приступая к работе с Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[Обзор метрик]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[Общие сведения о журналах активности]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[Обзор журналов диагностики]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
