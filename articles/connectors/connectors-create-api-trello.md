---
title: "Соединитель Trello в Azure Logic Apps | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Trello позволяет отслеживать все ваши проекты как на работе, так и дома.  Это простое, бесплатное, гибкое и наглядное средство организации данных и управления проектами.  Подключитесь к Trello для управления досками, списками и карточками."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: fe7a4377-5c24-4f72-ab1a-6d9d23e8d895
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 526a14710f24ee4a4b61a11873aa6caa0b47dc10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-trello-connector"></a><span data-ttu-id="0aed9-106">Начало работы с соединителем Trello</span><span class="sxs-lookup"><span data-stu-id="0aed9-106">Get started with the Trello connector</span></span>
<span data-ttu-id="0aed9-107">Trello позволяет отслеживать все ваши проекты как на работе, так и дома.</span><span class="sxs-lookup"><span data-stu-id="0aed9-107">Trello gives you perspective over all your projects, at work and at home.</span></span>  <span data-ttu-id="0aed9-108">Это простое, бесплатное, гибкое и наглядное средство организации данных и управления проектами.</span><span class="sxs-lookup"><span data-stu-id="0aed9-108">It is an easy, free, flexible, and visual way to manage your projects and organize anything.</span></span>  <span data-ttu-id="0aed9-109">Подключитесь к Trello для управления досками, списками и карточками.</span><span class="sxs-lookup"><span data-stu-id="0aed9-109">Connect to Trello to manage your boards, lists and cards.</span></span>

<span data-ttu-id="0aed9-110">Для начала создайте приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0aed9-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-trello"></a><span data-ttu-id="0aed9-111">Создание подключения к Trello</span><span class="sxs-lookup"><span data-stu-id="0aed9-111">Create a connection to Trello</span></span>
<span data-ttu-id="0aed9-112">Для создания приложения логики с Trello сначала нужно создать **подключение**, а затем указать данные для следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="0aed9-112">To create Logic apps with Trello, first create a **connection**, and enter the details for the following properties:</span></span>

| <span data-ttu-id="0aed9-113">Свойство</span><span class="sxs-lookup"><span data-stu-id="0aed9-113">Property</span></span> | <span data-ttu-id="0aed9-114">Обязательно</span><span class="sxs-lookup"><span data-stu-id="0aed9-114">Required</span></span> | <span data-ttu-id="0aed9-115">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="0aed9-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0aed9-116">Маркер</span><span class="sxs-lookup"><span data-stu-id="0aed9-116">Token</span></span> |<span data-ttu-id="0aed9-117">Да</span><span class="sxs-lookup"><span data-stu-id="0aed9-117">Yes</span></span> |<span data-ttu-id="0aed9-118">Укажите учетные данные Trello</span><span class="sxs-lookup"><span data-stu-id="0aed9-118">Provide Trello Credentials</span></span> |

<span data-ttu-id="0aed9-119">Созданное подключение можно использовать для выполнения действий и прослушивания триггеров.</span><span class="sxs-lookup"><span data-stu-id="0aed9-119">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Trello](../../includes/connectors-create-api-trello.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="0aed9-120">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="0aed9-120">Connector-specific details</span></span>

<span data-ttu-id="0aed9-121">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/trello/).</span><span class="sxs-lookup"><span data-stu-id="0aed9-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/trello/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="0aed9-122">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="0aed9-122">More connectors</span></span>
<span data-ttu-id="0aed9-123">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0aed9-123">Go back to the [APIs list](apis-list.md).</span></span>