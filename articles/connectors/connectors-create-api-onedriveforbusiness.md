---
title: "OneDrive для бизнеса | Документация Майкрософт"
description: "Создание приложений логики с помощью службы приложений Azure. Подключитесь к OneDrive для бизнеса, чтобы управлять файлами. Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cf9484e9-7a20-4de0-93c8-0fa132221f2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 783d6a640d9626508bcabc5f991dc5b6fc22eaf4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-for-business-connector"></a><span data-ttu-id="181d0-105">Начало работы с соединителем OneDrive для бизнеса</span><span class="sxs-lookup"><span data-stu-id="181d0-105">Get started with the OneDrive for Business connector</span></span>
<span data-ttu-id="181d0-106">Подключитесь к OneDrive для бизнеса, чтобы управлять файлами.</span><span class="sxs-lookup"><span data-stu-id="181d0-106">Connect to OneDrive for Business to manage your files.</span></span> <span data-ttu-id="181d0-107">Вы можете выполнять различные действия, такие как отправка, обновление, получение и удаление файлов.</span><span class="sxs-lookup"><span data-stu-id="181d0-107">You can perform various actions such as upload, update, get, and delete on files.</span></span>

<span data-ttu-id="181d0-108">Для начала можно создать приложение логики, как описано [здесь](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="181d0-108">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-onedrive-for-business"></a><span data-ttu-id="181d0-109">Создание подключения к OneDrive для бизнеса</span><span class="sxs-lookup"><span data-stu-id="181d0-109">Create a connection to OneDrive for Business</span></span>
<span data-ttu-id="181d0-110">Для создания приложений логики с помощью OneDrive для бизнеса необходимо создать **подключение**, а затем указать данные для приведенных ниже свойств.</span><span class="sxs-lookup"><span data-stu-id="181d0-110">To create Logic apps with OneDrive for Business, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="181d0-111">Свойство</span><span class="sxs-lookup"><span data-stu-id="181d0-111">Property</span></span> | <span data-ttu-id="181d0-112">Обязательно</span><span class="sxs-lookup"><span data-stu-id="181d0-112">Required</span></span> | <span data-ttu-id="181d0-113">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="181d0-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="181d0-114">Маркер</span><span class="sxs-lookup"><span data-stu-id="181d0-114">Token</span></span> |<span data-ttu-id="181d0-115">Да</span><span class="sxs-lookup"><span data-stu-id="181d0-115">Yes</span></span> |<span data-ttu-id="181d0-116">Укажите учетные данные OneDrive для бизнеса</span><span class="sxs-lookup"><span data-stu-id="181d0-116">Provide OneDrive for Business Credentials</span></span> |

<span data-ttu-id="181d0-117">Созданное подключение можно использовать для выполнения действий и прослушивания триггеров, описанных в этой статье.</span><span class="sxs-lookup"><span data-stu-id="181d0-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to OneDrive for Business](../../includes/connectors-create-api-onedriveforbusiness.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="181d0-118">Сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="181d0-118">Connector-specific details</span></span>

<span data-ttu-id="181d0-119">Информацию о существующих ограничениях, а также о триггерах и действиях, определенных в Swagger, см. в статье со [сведениями о соединителях](/connectors/onedriveforbusinessconnector/).</span><span class="sxs-lookup"><span data-stu-id="181d0-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveforbusinessconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="181d0-120">Дополнительные сведения о соединителях</span><span class="sxs-lookup"><span data-stu-id="181d0-120">More connectors</span></span>
<span data-ttu-id="181d0-121">Вы можете вернуться к [списку интерфейсов API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="181d0-121">Go back to the [APIs list](apis-list.md).</span></span>