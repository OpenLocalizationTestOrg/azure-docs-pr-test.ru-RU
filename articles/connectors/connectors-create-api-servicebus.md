---
title: "Соединитель Azure Service Bus aaaLearn toouse hello в приложениях для логики | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Подключения шины обслуживания toosend tooAzure и получать сообщения. Можно выполнять действия, такие как tooqueue отправки, отправить tootopic, получать из очереди и получения из подписки."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a>Приступая к работе с Azure Service Bus соединителя hello
Подключения шины обслуживания toosend tooAzure и получать сообщения. Можно выполнять действия, такие как tooqueue отправки, отправить tootopic, получать из очереди и получения из подписки.

toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики. Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooservice-bus"></a>Подключения шины tooService
Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate toohello подключения службы. Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a>Использование триггера служебной шины
Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики. [Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a>Использование действия служебной шины
Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику. [Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a>Сведения о соединителях

Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/servicebus/). 

## <a name="next-steps"></a>Дальнейшие действия
[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).

