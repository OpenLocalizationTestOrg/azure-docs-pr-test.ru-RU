---
title: "Как использовать соединитель SharePoint Online в приложениях логики | Документация Майкрософт"
description: "Создание приложений логики с соединителем SharePoint Online для управления списками на сайте SharePoint."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e0ec3149-507a-409d-8e7b-d5fbded006ce
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 96fc1347604c0c6cc2c2463a5dbd83b560183a16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-online-connector"></a><span data-ttu-id="4275d-103">Приступая к работе с соединителем SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4275d-103">Get started with the SharePoint Online connector</span></span>
<span data-ttu-id="4275d-104">Соединитель SharePoint Online можно использовать для управления списками SharePoint.</span><span class="sxs-lookup"><span data-stu-id="4275d-104">Use the SharePoint Online connector to manage SharePoint lists.</span></span>  

<span data-ttu-id="4275d-105">Чтобы использовать [соединитель](apis-list.md), сначала нужно создать приложение логики.</span><span class="sxs-lookup"><span data-stu-id="4275d-105">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="4275d-106">Вы можете начать с [создания приложения логики](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4275d-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sharepoint-online"></a><span data-ttu-id="4275d-107">Подключение к SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4275d-107">Connect to SharePoint Online</span></span>
<span data-ttu-id="4275d-108">Чтобы обеспечить доступ приложения логики к какой-либо службе, сначала необходимо создать *подключение* к этой службе.</span><span class="sxs-lookup"><span data-stu-id="4275d-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="4275d-109">Таким образом вы установите [соединение](connectors-overview.md) между приложением логики и другой службой.</span><span class="sxs-lookup"><span data-stu-id="4275d-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sharepoint-online"></a><span data-ttu-id="4275d-110">Создание подключения к SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4275d-110">Create a connection to SharePoint Online</span></span>
> [!INCLUDE [Steps to create a connection to SharePoint](../../includes/connectors-create-api-sharepointonline.md)]


## <a name="use-a-sharepoint-online-trigger"></a><span data-ttu-id="4275d-111">Использование триггера SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4275d-111">Use a SharePoint Online trigger</span></span>
<span data-ttu-id="4275d-112">Триггер — это событие, которое можно использовать для запуска рабочего процесса, определенного в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="4275d-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="4275d-113">[Дополнительные сведения о триггерах](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4275d-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online trigger](../../includes/connectors-create-api-sharepointonline-trigger.md)]


## <a name="use-a-sharepoint-online-action"></a><span data-ttu-id="4275d-114">Использование действия SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="4275d-114">Use a SharePoint Online action</span></span>
<span data-ttu-id="4275d-115">Действие — это операция, выполняемая рабочим процессом, определенным в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="4275d-115">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="4275d-116">[Дополнительные сведения о действиях](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4275d-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online action](../../includes/connectors-create-api-sharepointonline-action.md)]


## <a name="connector-specific-details"></a><span data-ttu-id="4275d-117">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="4275d-117">Connector-specific details</span></span>

<span data-ttu-id="4275d-118">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="4275d-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4275d-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4275d-119">Next Steps</span></span>
[<span data-ttu-id="4275d-120">Создайте приложение логики</span><span class="sxs-lookup"><span data-stu-id="4275d-120">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

