---
title: "Как использовать соединитель служебной шины Azure в приложениях логики | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Подключитесь к служебной шине Azure для отправки и получения сообщений. Вы можете выполнять такие действия, как отправка в очередь, отправка в раздел, получение из очереди и получение из подписки."
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
ms.openlocfilehash: 1e2ce06f5993280dbdb67121849591e67f7979e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-service-bus-connector"></a><span data-ttu-id="d7374-105">Начало работы с соединителем служебной шины Azure</span><span class="sxs-lookup"><span data-stu-id="d7374-105">Get started with the Azure Service Bus connector</span></span>
<span data-ttu-id="d7374-106">Подключитесь к служебной шине Azure для отправки и получения сообщений.</span><span class="sxs-lookup"><span data-stu-id="d7374-106">Connect to Azure Service Bus to send and receive messages.</span></span> <span data-ttu-id="d7374-107">Вы можете выполнять такие действия, как отправка в очередь, отправка в раздел, получение из очереди и получение из подписки.</span><span class="sxs-lookup"><span data-stu-id="d7374-107">You can perform actions such as send to queue, send to topic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="d7374-108">Чтобы использовать [соединитель](apis-list.md), сначала нужно создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="d7374-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="d7374-109">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d7374-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-service-bus"></a><span data-ttu-id="d7374-110">Подключение к служебной шине</span><span class="sxs-lookup"><span data-stu-id="d7374-110">Connect to Service Bus</span></span>
<span data-ttu-id="d7374-111">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать подключение к этой службе.</span><span class="sxs-lookup"><span data-stu-id="d7374-111">Before your logic app can access any service, you first need to create a connection to the service.</span></span> <span data-ttu-id="d7374-112">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="d7374-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps to create a connection to Azure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="d7374-113">Использование триггера служебной шины</span><span class="sxs-lookup"><span data-stu-id="d7374-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="d7374-114">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="d7374-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="d7374-115">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d7374-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="d7374-116">Использование действия служебной шины</span><span class="sxs-lookup"><span data-stu-id="d7374-116">Use a Service Bus action</span></span>
<span data-ttu-id="d7374-117">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="d7374-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="d7374-118">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d7374-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps to create a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="d7374-119">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="d7374-119">Connector-specific details</span></span>

<span data-ttu-id="d7374-120">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="d7374-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d7374-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7374-121">Next steps</span></span>
<span data-ttu-id="d7374-122">[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d7374-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

