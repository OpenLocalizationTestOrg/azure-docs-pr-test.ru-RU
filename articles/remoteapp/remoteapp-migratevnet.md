---
title: "Переход с платформы RemoteApp VNET на платформу Azure VNET | Документация Майкрософт"
description: "Сведения о переходе с платформы RemoteApp VNET на платформу Azure VNET"
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
ms.openlocfilehash: 10b5f4844a38fe97852dee8634e8cf54f1a23a1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-migrate-a-hybrid-collection-from-a-remoteapp-vnet-to-an-azure-vnet"></a><span data-ttu-id="34665-103">Перенос гибридной коллекции с платформы RemoteApp VNET в среду Azure VNET</span><span class="sxs-lookup"><span data-stu-id="34665-103">How to migrate a hybrid collection from a RemoteApp VNET to an Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="34665-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="34665-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="34665-105">Дополнительные сведения см. в [объявлении](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="34665-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="34665-106">Отличная новость!</span><span class="sxs-lookup"><span data-stu-id="34665-106">Good news!</span></span> <span data-ttu-id="34665-107">Теперь вы можете развертывать гибридные коллекции RemoteApp непосредственно в существующих виртуальных сетях Azure (VNET-сетях) вместо создания специальных VNET-сетей для службы RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="34665-107">We have enabled you to deploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="34665-108">Благодаря этому вам становятся доступны новейшие функции и преимущества VNET (такие как ExpressRoute), а также возможность предоставить своим гибридным коллекциям непосредственный сетевой доступ к другим службам и виртуальным машинам Azure, развернутым для этой VNET-сети.</span><span class="sxs-lookup"><span data-stu-id="34665-108">This lets you take advantage of the latest VNET features (like ExpressRoute) and give your hybrid collections direct network access to other Azure services and virtual machines deployed to that VNET.</span></span>  <span data-ttu-id="34665-109">(Это повышает эффективность и производительность, а также упрощает настройку в сравнении с конфигурациями VNET/VNET.)</span><span class="sxs-lookup"><span data-stu-id="34665-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="34665-110">Предположим, у вас уже есть гибридная коллекция RemoteApp под названием *OriginalCollection* с VNET-сетью RemoteApp, которая называется *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="34665-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="34665-111">Рассмотрим действия, которые необходимо выполнить для ее переноса в новую VNET-сеть Azure под названием *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="34665-111">Here are the steps to migrate it to a new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="34665-112">На вкладке **Сети** [портала управления](http://manage.windowsazure.com/) создайте VNET-сеть под названием *AzureVNET* с тем же расположением, конфигурацией DNS и адресным пространством (как минимум для одной из подсетей *AzureVNET*), что и у виртуальной сети *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="34665-112">On the **Networks** tab in the [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using the same location, DNS configuration, and address space (for at least one of the *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="34665-113">Настройте сеть *AzureVNET* таким образом, чтобы в ней размещалось развертывание Active Directory, в которое входит домен *OriginalCollection*, или между ними был организован сетевой доступ.</span><span class="sxs-lookup"><span data-stu-id="34665-113">Configure *AzureVNET* to either host or have network connectivity to the Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="34665-114">На вкладке **RemoteApps** создайте новую коллекцию RemoteApp под названием *NewCollection*.</span><span class="sxs-lookup"><span data-stu-id="34665-114">On the **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="34665-115">(Используйте вариант **Создать с помощью VNet**, а не **Быстрое создание**.)</span><span class="sxs-lookup"><span data-stu-id="34665-115">(Use the **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="34665-116">Разверните коллекцию *NewCollection* в подсети виртуальной сети *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="34665-116">Configure *NewCollection* to be deployed to a subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="34665-117">Задайте для *NewCollection* те же параметры образа и присоединения к домену, что и для коллекции *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="34665-117">Configure *NewCollection* to use the same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="34665-118">Через несколько часов коллекция *NewCollection* появится в списке коллекции в активном состоянии.</span><span class="sxs-lookup"><span data-stu-id="34665-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="34665-119">Теперь, если вам НЕ НУЖНО переносить данные пользователей из исходной коллекции в новую, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="34665-119">Now, if you DON’T need to migrate any user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="34665-120">Удалите исходную коллекцию *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="34665-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="34665-121">Удалите виртуальную сеть *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="34665-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="34665-122">Готово!</span><span class="sxs-lookup"><span data-stu-id="34665-122">And, you’re done!</span></span>

<span data-ttu-id="34665-123">Если вам все же НУЖНО перенести данные пользователей из исходной коллекции в новую, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="34665-123">Alternately, if you DO need to migrate user information from the original collection to the new collection, do these steps next:</span></span>

1. <span data-ttu-id="34665-124">Отправьте на адрес [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) электронное сообщение с идентификатором подписки Azure, именами исходной и новой коллекций и просьбой перенести данные пользователей.</span><span class="sxs-lookup"><span data-stu-id="34665-124">Send an email to [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, the name of your original collection, and the name of your new collection, and ask them to migrate your user information.</span></span>
2. <span data-ttu-id="34665-125">В течение двух рабочих дней специалисты RemoteApp перенесут список доступа пользователей, а также все их документы и параметры из исходной коллекции в новую.</span><span class="sxs-lookup"><span data-stu-id="34665-125">Within 2 business days the RemoteApp team will move the user access list and all user documents and user settings from the original collection to the new collection.</span></span>
3. <span data-ttu-id="34665-126">Удалите исходную коллекцию *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="34665-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="34665-127">Удалите виртуальную сеть *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="34665-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="34665-128">Готово!</span><span class="sxs-lookup"><span data-stu-id="34665-128">And now, you’re done!</span></span>

<span data-ttu-id="34665-129">Если у вас есть какие-либо вопросы или вам необходима дополнительная помощь, напишите по адресу [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="34665-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>

