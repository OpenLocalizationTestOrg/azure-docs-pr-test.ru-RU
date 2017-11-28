---
title: "Создание концентратора событий Azure | Документация Майкрософт"
description: "Узнайте, как создать пространство имен концентраторов событий Azure и концентратор событий с помощью портала Azure."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 816bf1426704d3391550e80c0700f1b011683a94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-the-azure-portal"></a><span data-ttu-id="f05ce-103">Создание пространства имен концентраторов событий и концентратора событий с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="f05ce-103">Create an Event Hubs namespace and an event hub using the Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="f05ce-104">Создание пространства имен концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="f05ce-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="f05ce-105">Войдите на [портал Azure][Azure portal] и щелкните **Создать** в левой верхней части экрана.</span><span class="sxs-lookup"><span data-stu-id="f05ce-105">Log on to the [Azure portal][Azure portal], and click **New** at the top left of the screen.</span></span>
1. <span data-ttu-id="f05ce-106">Последовательно выберите **Интернет вещей** и **Концентраторы событий**.</span><span class="sxs-lookup"><span data-stu-id="f05ce-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="f05ce-107">В колонке **Создание пространства имен** укажите имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="f05ce-107">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="f05ce-108">Система немедленно проверяет, доступно ли оно.</span><span class="sxs-lookup"><span data-stu-id="f05ce-108">The system immediately checks to see if the name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="f05ce-109">Убедившись, что пространство имен доступно, выберите ценовую категорию: "Базовый" или "Стандартный".</span><span class="sxs-lookup"><span data-stu-id="f05ce-109">After making sure the namespace name is available, choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="f05ce-110">Также выберите подписку Azure, группу ресурсов и расположение для создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="f05ce-110">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> 
1. <span data-ttu-id="f05ce-111">Щелкните **Создать** , чтобы создать пространство имен.</span><span class="sxs-lookup"><span data-stu-id="f05ce-111">Click **Create** to create the namespace.</span></span> <span data-ttu-id="f05ce-112">Полная подготовка ресурсов для системы может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="f05ce-112">You may have to wait a few minutes for the system to fully provision the resources.</span></span>
2. <span data-ttu-id="f05ce-113">На портале в списке пространств имен щелкните имя только что созданного пространства имен.</span><span class="sxs-lookup"><span data-stu-id="f05ce-113">In the portal list of namespaces, click the newly created namespace.</span></span>
2. <span data-ttu-id="f05ce-114">В колонке **Политики общего доступа** щелкните **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="f05ce-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="f05ce-115">Нажмите кнопку копирования, чтобы скопировать строку подключения **RootManageSharedAccessKey** в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="f05ce-115">Click the copy button to copy the **RootManageSharedAccessKey** connection string to the clipboard.</span></span> <span data-ttu-id="f05ce-116">Сохраните эту строку подключения во временном расположении папке, например в Блокноте, для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="f05ce-116">Save this connection string in a temporary location, such as Notepad, to use later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="f05ce-117">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="f05ce-117">Create an event hub</span></span>

1. <span data-ttu-id="f05ce-118">В списке пространств имен концентраторов событий щелкните созданное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="f05ce-118">In the Event Hubs namespace list, click the newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="f05ce-119">В колонке пространства имен щелкните **Концентраторы событий**.</span><span class="sxs-lookup"><span data-stu-id="f05ce-119">In the namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="f05ce-120">Щелкните **Добавить концентратор событий**в верхней части колонки.</span><span class="sxs-lookup"><span data-stu-id="f05ce-120">At the top of the blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="f05ce-121">Введите имя концентратора событий, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f05ce-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="f05ce-122">Теперь концентратор событий создан, и у вас есть строки подключения, необходимые для отправки и приема событий.</span><span class="sxs-lookup"><span data-stu-id="f05ce-122">Your event hub is now created, and you have the connection strings you need to send and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f05ce-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f05ce-123">Next steps</span></span>
<span data-ttu-id="f05ce-124">Дополнительные сведения о концентраторах событий см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="f05ce-124">To learn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="f05ce-125">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="f05ce-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="f05ce-126">Общие сведения об API концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="f05ce-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/