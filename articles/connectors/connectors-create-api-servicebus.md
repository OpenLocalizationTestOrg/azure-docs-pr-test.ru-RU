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
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="f6df1-105">Приступая к работе с Azure Service Bus соединителя hello</span><span class="sxs-lookup"><span data-stu-id="f6df1-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="f6df1-106">Подключения шины обслуживания toosend tooAzure и получать сообщения.</span><span class="sxs-lookup"><span data-stu-id="f6df1-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="f6df1-107">Можно выполнять действия, такие как tooqueue отправки, отправить tootopic, получать из очереди и получения из подписки.</span><span class="sxs-lookup"><span data-stu-id="f6df1-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="f6df1-108">toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики.</span><span class="sxs-lookup"><span data-stu-id="f6df1-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="f6df1-109">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f6df1-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="f6df1-110">Подключения шины tooService</span><span class="sxs-lookup"><span data-stu-id="f6df1-110">Connect tooService Bus</span></span>
<span data-ttu-id="f6df1-111">Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate toohello подключения службы.</span><span class="sxs-lookup"><span data-stu-id="f6df1-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="f6df1-112">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="f6df1-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="f6df1-113">Использование триггера служебной шины</span><span class="sxs-lookup"><span data-stu-id="f6df1-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="f6df1-114">Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="f6df1-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="f6df1-115">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f6df1-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="f6df1-116">Использование действия служебной шины</span><span class="sxs-lookup"><span data-stu-id="f6df1-116">Use a Service Bus action</span></span>
<span data-ttu-id="f6df1-117">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="f6df1-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="f6df1-118">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f6df1-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="f6df1-119">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="f6df1-119">Connector-specific details</span></span>

<span data-ttu-id="f6df1-120">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="f6df1-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f6df1-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6df1-121">Next steps</span></span>
<span data-ttu-id="f6df1-122">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f6df1-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

