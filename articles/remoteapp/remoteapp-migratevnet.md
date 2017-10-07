---
title: "toomigrate aaaHow из виртуальной сети RemoteApp tooan виртуальной сети Azure | Документы Microsoft"
description: "Узнайте, как toomigrate из виртуальной сети RemoteApp tooan виртуальной сети Azure"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a><span data-ttu-id="2971c-103">Как toomigrate гибридной коллекции из виртуальной сети RemoteApp tooan виртуальной сети Azure</span><span class="sxs-lookup"><span data-stu-id="2971c-103">How toomigrate a hybrid collection from a RemoteApp VNET tooan Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2971c-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="2971c-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="2971c-105">Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="2971c-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="2971c-106">Отличная новость!</span><span class="sxs-lookup"><span data-stu-id="2971c-106">Good news!</span></span> <span data-ttu-id="2971c-107">Мы включили коллекции RemoteApp гибридного toodeploy непосредственно в вашей существующей Azure виртуальных сетей (Vnet) вместо создания виртуальных сетей RemoteApp определенного.</span><span class="sxs-lookup"><span data-stu-id="2971c-107">We have enabled you toodeploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="2971c-108">Это позволяет воспользоваться преимуществами hello новейших функций виртуальной сети (например, ExpressRoute) и предоставьте вашей гибридной коллекции прямого сетевого доступа tooother служб Azure и развернуть виртуальные машины toothat виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2971c-108">This lets you take advantage of hello latest VNET features (like ExpressRoute) and give your hybrid collections direct network access tooother Azure services and virtual machines deployed toothat VNET.</span></span>  <span data-ttu-id="2971c-109">(Это повышает эффективность и производительность, а также упрощает настройку в сравнении с конфигурациями VNET/VNET.)</span><span class="sxs-lookup"><span data-stu-id="2971c-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="2971c-110">Предположим, у вас уже есть гибридная коллекция RemoteApp под названием *OriginalCollection* с VNET-сетью RemoteApp, которая называется *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="2971c-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="2971c-111">Ниже приведены шаги toomigrate hello его новой виртуальной сети Azure вызывается tooa *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="2971c-111">Here are hello steps toomigrate it tooa new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="2971c-112">На hello **сетей** на вкладке hello [портала управления](http://manage.windowsazure.com/), создание виртуальной сети называется *AzureVNET*, с использованием hello местоположения, конфигурацию DNS и адресного пространства (хотя бы для одного из hello *AzureVNET* подсетей) как вы использовали для *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="2971c-112">On hello **Networks** tab in hello [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using hello same location, DNS configuration, and address space (for at least one of hello *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="2971c-113">Настройка *AzureVNET* tooeither размещения или развертывания Active Directory toohello подключения к сети, *OriginalCollection* присоединен к домену.</span><span class="sxs-lookup"><span data-stu-id="2971c-113">Configure *AzureVNET* tooeither host or have network connectivity toohello Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="2971c-114">На hello **удаленными приложениями** создайте новую коллекцию RemoteApp с названием *новую коллекцию*.</span><span class="sxs-lookup"><span data-stu-id="2971c-114">On hello **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="2971c-115">(Используйте hello **Создание виртуальной сети** вариант не **быстрое создание**.)</span><span class="sxs-lookup"><span data-stu-id="2971c-115">(Use hello **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="2971c-116">Настройка *NewCollection* toobe развернут в подсети tooa *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="2971c-116">Configure *NewCollection* toobe deployed tooa subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="2971c-117">Настройка *NewCollection* toouse hello того же образа и сведений о присоединении домена, как вы использовали для *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="2971c-117">Configure *NewCollection* toouse hello same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="2971c-118">Через несколько часов коллекция *NewCollection* появится в списке коллекции в активном состоянии.</span><span class="sxs-lookup"><span data-stu-id="2971c-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="2971c-119">Теперь если не требуется toomigrate сведений о пользователе из hello исходной коллекции toohello новой коллекции, выполните указанные ниже действия далее:</span><span class="sxs-lookup"><span data-stu-id="2971c-119">Now, if you DON’T need toomigrate any user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="2971c-120">Удалите исходную коллекцию *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="2971c-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="2971c-121">Удалите виртуальную сеть *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="2971c-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="2971c-122">Готово!</span><span class="sxs-lookup"><span data-stu-id="2971c-122">And, you’re done!</span></span>

<span data-ttu-id="2971c-123">Кроме того Если требуется toomigrate сведений о пользователе из hello исходной коллекции toohello новой коллекции, выполните указанные ниже действия далее:</span><span class="sxs-lookup"><span data-stu-id="2971c-123">Alternately, if you DO need toomigrate user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="2971c-124">Отправить сообщение электронной почты слишком[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) своим Идентификатором подписки Azure hello имя исходной коллекции, а имя новой коллекции hello и попросите его toomigrate свои учетные данные.</span><span class="sxs-lookup"><span data-stu-id="2971c-124">Send an email too[remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, hello name of your original collection, and hello name of your new collection, and ask them toomigrate your user information.</span></span>
2. <span data-ttu-id="2971c-125">В течение 2 рабочих дней команды RemoteApp hello будет перемещать hello список доступа пользователей и все документы пользователя и параметров пользователя из hello исходной коллекции toohello новой коллекции.</span><span class="sxs-lookup"><span data-stu-id="2971c-125">Within 2 business days hello RemoteApp team will move hello user access list and all user documents and user settings from hello original collection toohello new collection.</span></span>
3. <span data-ttu-id="2971c-126">Удалите исходную коллекцию *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="2971c-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="2971c-127">Удалите виртуальную сеть *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="2971c-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="2971c-128">Готово!</span><span class="sxs-lookup"><span data-stu-id="2971c-128">And now, you’re done!</span></span>

<span data-ttu-id="2971c-129">Если у вас есть какие-либо вопросы или вам необходима дополнительная помощь, напишите по адресу [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="2971c-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

