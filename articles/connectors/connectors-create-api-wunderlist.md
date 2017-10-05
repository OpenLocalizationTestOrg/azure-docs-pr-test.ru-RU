---
title: "Соединитель Wunderlist в Azure Logic Apps | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как создать подключение к Wunderlist и с его помощью создавать рабочие процессы в приложениях логики."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e4773ecf-3ad3-44b4-a1b5-ee5f58baeadd
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 899110992cc52ca5edf1706320fd5570473de784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-wunderlist-connector"></a><span data-ttu-id="faa6e-103">Начало работы с соединителем Wunderlist</span><span class="sxs-lookup"><span data-stu-id="faa6e-103">Get started with the Wunderlist connector</span></span>
<span data-ttu-id="faa6e-104">Wunderlist — это приложение для ведения списка дел и управления задачами, помогающее справляться с делами.</span><span class="sxs-lookup"><span data-stu-id="faa6e-104">Wunderlist provide a todo list and task manager to help people get their stuff done.</span></span>  <span data-ttu-id="faa6e-105">Wunderlist позволяет легко составлять и вести списки дел, а также предоставлять к ним доступ, будь то отправка списка покупок, работа над проектом или планирование отпуска.</span><span class="sxs-lookup"><span data-stu-id="faa6e-105">Whether you’re sharing a grocery list with a loved one, working on a project, or planning a vacation, Wunderlist makes it easy to capture, share, and complete your to¬dos.</span></span> <span data-ttu-id="faa6e-106">Wunderlist мгновенно синхронизируется между телефоном, планшетом и компьютером, обеспечивая доступ к задачам из любой точки мира.</span><span class="sxs-lookup"><span data-stu-id="faa6e-106">Wunderlist instantly syncs between your phone, tablet and computer, so you can access all your tasks from anywhere.</span></span>

<span data-ttu-id="faa6e-107">Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="faa6e-107">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-wunderlist"></a><span data-ttu-id="faa6e-108">Создание подключения к Wunderlist</span><span class="sxs-lookup"><span data-stu-id="faa6e-108">Create a connection to Wunderlist</span></span>
<span data-ttu-id="faa6e-109">Для создания приложений логики с помощью Wunderlist необходимо создать **подключение**, а затем указать данные для приведенных ниже свойств.</span><span class="sxs-lookup"><span data-stu-id="faa6e-109">To create Logic apps with Wunderlist, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="faa6e-110">Свойство</span><span class="sxs-lookup"><span data-stu-id="faa6e-110">Property</span></span> | <span data-ttu-id="faa6e-111">Обязательно</span><span class="sxs-lookup"><span data-stu-id="faa6e-111">Required</span></span> | <span data-ttu-id="faa6e-112">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="faa6e-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="faa6e-113">Маркер</span><span class="sxs-lookup"><span data-stu-id="faa6e-113">Token</span></span> |<span data-ttu-id="faa6e-114">Да</span><span class="sxs-lookup"><span data-stu-id="faa6e-114">Yes</span></span> |<span data-ttu-id="faa6e-115">Учетные данные Wunderlist</span><span class="sxs-lookup"><span data-stu-id="faa6e-115">Provide Wunderlist Credentials</span></span> |

<span data-ttu-id="faa6e-116">Созданное подключение можно использовать для выполнения действий и прослушивания триггеров.</span><span class="sxs-lookup"><span data-stu-id="faa6e-116">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Wunderlist](../../includes/connectors-create-api-wunderlist.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="faa6e-117">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="faa6e-117">Connector-specific details</span></span>

<span data-ttu-id="faa6e-118">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/wunderlist/).</span><span class="sxs-lookup"><span data-stu-id="faa6e-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/wunderlist/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="faa6e-119">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="faa6e-119">More connectors</span></span>
<span data-ttu-id="faa6e-120">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="faa6e-120">Go back to the [APIs list](apis-list.md).</span></span>