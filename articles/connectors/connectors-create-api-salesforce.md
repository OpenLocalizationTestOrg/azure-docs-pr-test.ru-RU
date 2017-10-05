---
title: "Как использовать соединитель Salesforce в приложениях логики | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Соединитель Salesforce предоставляет API для работы с объектами Salesforce."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="5130c-104">Начало работы с соединителем Salesforce</span><span class="sxs-lookup"><span data-stu-id="5130c-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="5130c-105">Соединитель Salesforce предоставляет API для работы с объектами Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5130c-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="5130c-106">Чтобы использовать [соединитель](apis-list.md), сначала нужно создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="5130c-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="5130c-107">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5130c-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="5130c-108">Подключение к соединителю Salesforce</span><span class="sxs-lookup"><span data-stu-id="5130c-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="5130c-109">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="5130c-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="5130c-110">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="5130c-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="5130c-111">Создание подключения к соединителю Salesforce</span><span class="sxs-lookup"><span data-stu-id="5130c-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="5130c-112">Использование триггера соединителя Salesforce</span><span class="sxs-lookup"><span data-stu-id="5130c-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="5130c-113">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="5130c-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="5130c-114">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="5130c-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="5130c-115">Добавить условие</span><span class="sxs-lookup"><span data-stu-id="5130c-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="5130c-116">Использование действия соединителя Salesforce</span><span class="sxs-lookup"><span data-stu-id="5130c-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="5130c-117">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="5130c-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="5130c-118">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="5130c-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="5130c-119">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="5130c-119">Connector-specific details</span></span>

<span data-ttu-id="5130c-120">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="5130c-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5130c-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5130c-121">Next steps</span></span>
[<span data-ttu-id="5130c-122">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="5130c-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

