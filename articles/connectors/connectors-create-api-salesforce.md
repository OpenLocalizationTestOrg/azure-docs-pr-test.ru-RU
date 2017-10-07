---
title: "aaaLearn toouse hello соединителю Salesforce в свои приложения логики | Документы Microsoft"
description: "Создание приложений логики с помощью службы приложений Azure. Hello соединителю Salesforce предоставляет API toowork с объектами Salesforce."
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
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="07416-104">Приступая к работе с соединителю Salesforce hello</span><span class="sxs-lookup"><span data-stu-id="07416-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="07416-105">Hello соединителю Salesforce предоставляет API toowork с объектами Salesforce.</span><span class="sxs-lookup"><span data-stu-id="07416-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="07416-106">toouse [всех соединителей](apis-list.md), необходимо сначала toocreate приложения логики.</span><span class="sxs-lookup"><span data-stu-id="07416-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="07416-107">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="07416-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="07416-108">Подключение tooSalesforce соединителя</span><span class="sxs-lookup"><span data-stu-id="07416-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="07416-109">Логика приложения можно получить доступ к любой службы, необходимо сначала toocreate *подключения* toohello службы.</span><span class="sxs-lookup"><span data-stu-id="07416-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="07416-110">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="07416-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="07416-111">Создание соединителя tooSalesforce подключения</span><span class="sxs-lookup"><span data-stu-id="07416-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="07416-112">Использование триггера соединителя Salesforce</span><span class="sxs-lookup"><span data-stu-id="07416-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="07416-113">Триггер — это событие, которое может быть рабочий процесс используется toostart hello, определенной в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="07416-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="07416-114">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="07416-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="07416-115">Добавить условие</span><span class="sxs-lookup"><span data-stu-id="07416-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="07416-116">Использование действия соединителя Salesforce</span><span class="sxs-lookup"><span data-stu-id="07416-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="07416-117">Действие — операции, выполняемые hello рабочего процесса, определенного в приложении логику.</span><span class="sxs-lookup"><span data-stu-id="07416-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="07416-118">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="07416-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="07416-119">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="07416-119">Connector-specific details</span></span>

<span data-ttu-id="07416-120">Просмотреть все триггеры и действия, определенные в hello swagger и любые пределы в hello см. также [сведений о соединителе](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="07416-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="07416-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="07416-121">Next steps</span></span>
[<span data-ttu-id="07416-122">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="07416-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

