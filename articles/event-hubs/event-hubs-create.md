---
title: "aaaCreate концентратор событий Azure | Документы Microsoft"
description: "Создать пространство имен концентраторов событий Azure и концентратор событий с помощью портала Azure hello"
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
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a><span data-ttu-id="2dba5-103">Создать пространство имен концентраторов событий и концентратор событий с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="2dba5-103">Create an Event Hubs namespace and an event hub using hello Azure portal</span></span>

## <a name="create-an-event-hubs-namespace"></a><span data-ttu-id="2dba5-104">Создание пространства имен концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="2dba5-104">Create an Event Hubs namespace</span></span>
1. <span data-ttu-id="2dba5-105">Войдите на toohello [портал Azure][Azure portal]и нажмите кнопку **New** на hello верхнего левого угла экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="2dba5-105">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
1. <span data-ttu-id="2dba5-106">Последовательно выберите **Интернет вещей** и **Концентраторы событий**.</span><span class="sxs-lookup"><span data-stu-id="2dba5-106">Click **Internet of Things**, and then click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. <span data-ttu-id="2dba5-107">В hello **создать пространство имен** колонки, введите имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="2dba5-107">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="2dba5-108">система Hello немедленно проверяет toosee, доступно ли имя hello.</span><span class="sxs-lookup"><span data-stu-id="2dba5-108">hello system immediately checks toosee if hello name is available.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. <span data-ttu-id="2dba5-109">После внесения убедиться, что имя пространства имен hello недоступна, выберите hello ценовой категории (Basic или Standard).</span><span class="sxs-lookup"><span data-stu-id="2dba5-109">After making sure hello namespace name is available, choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="2dba5-110">Кроме того, в какой ресурс hello toocreate выберите подписки Azure, группа ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="2dba5-110">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> 
1. <span data-ttu-id="2dba5-111">Нажмите кнопку **создать** toocreate приветствия имен.</span><span class="sxs-lookup"><span data-stu-id="2dba5-111">Click **Create** toocreate hello namespace.</span></span> <span data-ttu-id="2dba5-112">Вы можете иметь toowait hello системных toofully подготовки hello ресурсов в течение нескольких минут.</span><span class="sxs-lookup"><span data-stu-id="2dba5-112">You may have toowait a few minutes for hello system toofully provision hello resources.</span></span>
2. <span data-ttu-id="2dba5-113">В hello портала пространств имен выберите hello вновь создано и пространство имен.</span><span class="sxs-lookup"><span data-stu-id="2dba5-113">In hello portal list of namespaces, click hello newly created namespace.</span></span>
2. <span data-ttu-id="2dba5-114">В колонке **Политики общего доступа** щелкните **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="2dba5-114">Click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. <span data-ttu-id="2dba5-115">Нажмите кнопку toocopy hello копирования hello **RootManageSharedAccessKey** буфер обмена toohello строку соединения.</span><span class="sxs-lookup"><span data-stu-id="2dba5-115">Click hello copy button toocopy hello **RootManageSharedAccessKey** connection string toohello clipboard.</span></span> <span data-ttu-id="2dba5-116">Сохраните эту строку подключения во временной папке, например в блокноте, toouse более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2dba5-116">Save this connection string in a temporary location, such as Notepad, toouse later.</span></span>
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a><span data-ttu-id="2dba5-117">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="2dba5-117">Create an event hub</span></span>

1. <span data-ttu-id="2dba5-118">В списке пространство имен hello концентраторов событий выберите только что созданный hello пространства имен.</span><span class="sxs-lookup"><span data-stu-id="2dba5-118">In hello Event Hubs namespace list, click hello newly created namespace.</span></span>      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. <span data-ttu-id="2dba5-119">В колонке приветствия имен щелкните **концентраторов событий**.</span><span class="sxs-lookup"><span data-stu-id="2dba5-119">In hello namespace blade, click **Event Hubs**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. <span data-ttu-id="2dba5-120">Hello верхней части колонки hello, нажмите кнопку **добавить концентратор событий**.</span><span class="sxs-lookup"><span data-stu-id="2dba5-120">At hello top of hello blade, click **Add Event Hub**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. <span data-ttu-id="2dba5-121">Введите имя концентратора событий, а затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2dba5-121">Type a name for your event hub, then click **Create**.</span></span>
   
    ![](./media/event-hubs-create/create-event-hub5.png)

<span data-ttu-id="2dba5-122">Теперь создается концентратора событий и hello строки подключения требуется toosend и получения событий.</span><span class="sxs-lookup"><span data-stu-id="2dba5-122">Your event hub is now created, and you have hello connection strings you need toosend and receive events.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dba5-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2dba5-123">Next steps</span></span>
<span data-ttu-id="2dba5-124">toolearn Дополнительные сведения о концентраторах событий в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="2dba5-124">toolearn more about Event Hubs, visit these links:</span></span>

* [<span data-ttu-id="2dba5-125">Обзор концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="2dba5-125">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="2dba5-126">Общие сведения об API концентраторов событий</span><span class="sxs-lookup"><span data-stu-id="2dba5-126">Event Hubs API overview</span></span>](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/