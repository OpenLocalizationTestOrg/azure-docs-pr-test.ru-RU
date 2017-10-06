---
title: "журналы диагностики aaaAzure Service Bus | Документы Microsoft"
description: "Узнайте, как tooset копирование журналов диагностики для шины обслуживания в Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a>Журналы диагностики служебной шины

Для служебной шины Azure можно просмотреть журналы двух типов.
* **[Журналы действий](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Эти журналы содержат сведения об операциях, выполненных с заданием. журналы Hello всегда включен.
* **[Журналы диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. Вы можете настроить журналы диагностики, чтобы получать более подробные сведения обо всем, что происходит с заданием. Действия титульных журналы диагностики с момента создания задания hello до удаления задания hello, включая обновления и действия, которые могут возникнуть при выполнении задания hello hello.

## <a name="turn-on-diagnostic-logs"></a>Включение журналов диагностики

По умолчанию журналы диагностики отключены. tooenable журналы диагностики, выполните следующие шаги hello.

1.  В hello [портал Azure](https://portal.azure.com)в разделе **мониторинг + управления**, нажмите кнопку **журналы диагностики**.

    ![журналы toodiagnostic колонке навигации](./media/service-bus-diagnostic-logs/image1.png)

2. Щелкните ресурс hello требуется toomonitor.  

3.  Щелкните **Включить диагностику**.

    ![Включение журналов диагностики](./media/service-bus-diagnostic-logs/image2.png)

4.  Для параметра **Состояние** щелкните **Вкл**.

    ![Изменение состояния журналов диагностики](./media/service-bus-diagnostic-logs/image3.png)

5.  Набор hello архив целевой объекты; например учетная запись хранения, концентратора событий или анализа журналов Azure.

6.  Сохраните новые параметры диагностики hello.

Новые параметры вступят в силу в течение 10 минут. После этого журналы отображаются на конечном архивных hello настроен на hello **журналы диагностики** колонку.

Дополнительные сведения о настройке диагностики см. в разделе hello [Обзор Azure журналам диагностики](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-schema"></a>Схема журналов диагностики

Все журналы хранятся в формате JSON (нотация объектов JavaScript). Каждая запись содержит поля строки, используйте формат hello, описанные в следующем разделе hello.

## <a name="operational-logs-schema"></a>Схема операционных журналов

Регистрирует в hello **OperationalLogs** категории записи, что происходит при выполнении операций с Service Bus. В частности эти журналы записать hello тип операции, включая создание очереди, использование ресурсов и состояние операции hello hello.

Операционный журнал JSON строки включать элементы, перечисленные в следующей таблице hello:

Имя | Описание
------- | -------
ActivityId | Внутренний идентификатор, используемый для отслеживания
EventName | Имя операции           
resourceId | Идентификатор ресурса Azure Resource Manager
SubscriptionId | Идентификатор подписки
EventTimeString | Время операции
EventProperties | Свойства операции
Status | Состояние операции
Caller | Объект, вызвавший операцию (портал Azure или клиент управления)
category | OperationalLogs

Ниже приведен пример строки JSON операционного журнала.

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Дальнейшие действия

Посетите следующие ссылки toolearn дополнительные о Service Bus hello:

* [Введение tooService шины](service-bus-messaging-overview.md)
* [Приступая к работе со служебной шиной](service-bus-dotnet-get-started-with-queues.md)
