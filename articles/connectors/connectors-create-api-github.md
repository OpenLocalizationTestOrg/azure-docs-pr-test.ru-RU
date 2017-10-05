---
title: "Соединитель GitHub в Azure Logic Apps | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. GitHub — это веб-служба размещения репозиториев Git. Она предоставляет все возможности распределенного управления редакциями и исходным кодом (SCM) Git, а также собственные функции."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="943d8-105">Начало работы с соединителем GitHub</span><span class="sxs-lookup"><span data-stu-id="943d8-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="943d8-106">GitHub — это веб-служба размещения репозиториев Git.</span><span class="sxs-lookup"><span data-stu-id="943d8-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="943d8-107">Она предоставляет все возможности распределенного управления редакциями и исходным кодом (SCM) Git, а также собственные функции.</span><span class="sxs-lookup"><span data-stu-id="943d8-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="943d8-108">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="943d8-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="943d8-109">Создание подключения к GitHub</span><span class="sxs-lookup"><span data-stu-id="943d8-109">Create a connection to GitHub</span></span>
<span data-ttu-id="943d8-110">Для создания приложений логики с помощью GitHub необходимо создать **подключение**, а затем указать данные для следующих свойств.</span><span class="sxs-lookup"><span data-stu-id="943d8-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="943d8-111">Свойство</span><span class="sxs-lookup"><span data-stu-id="943d8-111">Property</span></span> | <span data-ttu-id="943d8-112">Обязательно</span><span class="sxs-lookup"><span data-stu-id="943d8-112">Required</span></span> | <span data-ttu-id="943d8-113">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="943d8-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="943d8-114">Маркер</span><span class="sxs-lookup"><span data-stu-id="943d8-114">Token</span></span> |<span data-ttu-id="943d8-115">Да</span><span class="sxs-lookup"><span data-stu-id="943d8-115">Yes</span></span> |<span data-ttu-id="943d8-116">Укажите учетные данные GitHub</span><span class="sxs-lookup"><span data-stu-id="943d8-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="943d8-117">Созданное подключение можно использовать для выполнения действий и прослушивания триггеров, описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="943d8-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="943d8-118">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="943d8-118">Connector-specific details</span></span>

<span data-ttu-id="943d8-119">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/github/).</span><span class="sxs-lookup"><span data-stu-id="943d8-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="943d8-120">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="943d8-120">More connectors</span></span>
<span data-ttu-id="943d8-121">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="943d8-121">Go back to the [APIs list](apis-list.md).</span></span>