---
title: "Доступ к виртуальным машинам Azure из обозревателя сервера | Документация Майкрософт"
description: "Общие сведения о просмотре и создании виртуальных машин Azure, а также об управлении ими в обозревателе сервера в Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fcbb00cc2f00691e25ea84333e8c418b08210a67
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a><span data-ttu-id="513a5-103">Доступ к виртуальным машинам Azure из обозревателя сервера</span><span class="sxs-lookup"><span data-stu-id="513a5-103">Accessing Azure Virtual Machines from Server Explorer</span></span>
<span data-ttu-id="513a5-104">С помощью обозревателя сервера в Visual Studio можно отображать сведения о виртуальных машинах, размещенных в Azure.</span><span class="sxs-lookup"><span data-stu-id="513a5-104">By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.</span></span>

## <a name="accessing-virtual-machines-in-server-explorer"></a><span data-ttu-id="513a5-105">Доступ к виртуальным машинам из обозревателя сервера</span><span class="sxs-lookup"><span data-stu-id="513a5-105">Accessing virtual machines in Server Explorer</span></span>
<span data-ttu-id="513a5-106">Виртуальные машины, размещенные в Azure, можно открыть в обозревателе сервера.</span><span class="sxs-lookup"><span data-stu-id="513a5-106">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span></span> <span data-ttu-id="513a5-107">Чтобы просмотреть мобильные службы, войдите в свою подписку Azure.</span><span class="sxs-lookup"><span data-stu-id="513a5-107">You must first sign in to your Azure subscription to view your mobile services.</span></span> <span data-ttu-id="513a5-108">Для этого откройте контекстное меню узла Azure в обозревателе сервера и выберите пункт **Подключиться к Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="513a5-108">To sign in, open the shortcut menu for the Azure node in Server Explorer, and choose **Connect to Microsoft Azure**.</span></span>

### <a name="to-get-information-about-your-virtual-machines"></a><span data-ttu-id="513a5-109">Получение сведений о виртуальных машинах</span><span class="sxs-lookup"><span data-stu-id="513a5-109">To get information about your virtual machines</span></span>
1. <span data-ttu-id="513a5-110">В обозревателе сервера выберите виртуальную машину и нажмите клавишу F4, чтобы открыть окно с ее свойствами.</span><span class="sxs-lookup"><span data-stu-id="513a5-110">In Server Explorer, choose a virtual machine, and then choose the F4 key to show its properties window.</span></span>
   
    <span data-ttu-id="513a5-111">В следующей таблице показаны доступные свойства. Обратите внимание, что все они доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="513a5-111">The following table shows what properties are available, but they are all read-only.</span></span> <span data-ttu-id="513a5-112">Чтобы изменить их, используйте [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="513a5-112">To change them, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
   
   | <span data-ttu-id="513a5-113">Свойство</span><span class="sxs-lookup"><span data-stu-id="513a5-113">Property</span></span> | <span data-ttu-id="513a5-114">Описание</span><span class="sxs-lookup"><span data-stu-id="513a5-114">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="513a5-115">DNS-имя</span><span class="sxs-lookup"><span data-stu-id="513a5-115">DNS Name</span></span> |<span data-ttu-id="513a5-116">URL-адрес виртуальной машины в Интернете.</span><span class="sxs-lookup"><span data-stu-id="513a5-116">The URL with the Internet address of the virtual machine.</span></span> |
   | <span data-ttu-id="513a5-117">Среда</span><span class="sxs-lookup"><span data-stu-id="513a5-117">Environment</span></span> |<span data-ttu-id="513a5-118">У виртуальной машины значение этого свойства всегда равно "Производство".</span><span class="sxs-lookup"><span data-stu-id="513a5-118">For a virtual machine, the value of this property is always Production.</span></span> |
   | <span data-ttu-id="513a5-119">Имя</span><span class="sxs-lookup"><span data-stu-id="513a5-119">Name</span></span> |<span data-ttu-id="513a5-120">Имя виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="513a5-120">The name of the virtual machine.</span></span> |
   | <span data-ttu-id="513a5-121">Размер</span><span class="sxs-lookup"><span data-stu-id="513a5-121">Size</span></span> |<span data-ttu-id="513a5-122">Размер виртуальной машины, который отражает объем памяти и доступного дискового пространства.</span><span class="sxs-lookup"><span data-stu-id="513a5-122">The size of the virtual machine, which reflects the amount of memory and disk space that’s available.</span></span> <span data-ttu-id="513a5-123">Дополнительные сведения см. в статье "Практическое руководство по настройке размеров виртуальных машин".</span><span class="sxs-lookup"><span data-stu-id="513a5-123">For more information, see How To: Configure Virtual Machine Sizes.</span></span> |
   | <span data-ttu-id="513a5-124">Состояние</span><span class="sxs-lookup"><span data-stu-id="513a5-124">Status</span></span> |<span data-ttu-id="513a5-125">Возможные значения: "Запуск", "Запущено", "Остановка", "Остановлено" и "Получение состояния".</span><span class="sxs-lookup"><span data-stu-id="513a5-125">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span></span> <span data-ttu-id="513a5-126">Если отображается значение "Получение состояния", текущее состояние неизвестно.</span><span class="sxs-lookup"><span data-stu-id="513a5-126">If Retrieving Status appears, the current status is unknown.</span></span> <span data-ttu-id="513a5-127">Значения этого свойства отличаются от значений, используемых на [классическом портале Azure](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="513a5-127">The values for this property differ from the values that are used on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> |
   | <span data-ttu-id="513a5-128">SubscriptionID</span><span class="sxs-lookup"><span data-stu-id="513a5-128">SubscriptionID</span></span> |<span data-ttu-id="513a5-129">Идентификатор подписки вашей учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="513a5-129">The subscription ID for your Azure account.</span></span> <span data-ttu-id="513a5-130">Эти сведения можно узнать на [классическом портале Azure](http://go.microsoft.com/fwlink/?LinkID=213885) , просмотрев свойства подписки.</span><span class="sxs-lookup"><span data-stu-id="513a5-130">You can show this information on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing the properties for a subscription.</span></span> |
2. <span data-ttu-id="513a5-131">Выберите узел конечной точки, а затем просмотрите окно **Свойства** .</span><span class="sxs-lookup"><span data-stu-id="513a5-131">Choose an endpoint node, and then view the **Properties** window.</span></span>
3. <span data-ttu-id="513a5-132">В следующей таблице описаны доступные свойства конечных точек, но они доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="513a5-132">The following table describes the available properties of endpoints, but they are read-only.</span></span> <span data-ttu-id="513a5-133">Чтобы добавить или изменить конечные точки для виртуальной машины, используйте [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="513a5-133">To add or edit the endpoints for a virtual machine, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> 
   
   | <span data-ttu-id="513a5-134">Свойство</span><span class="sxs-lookup"><span data-stu-id="513a5-134">Property</span></span> | <span data-ttu-id="513a5-135">Описание</span><span class="sxs-lookup"><span data-stu-id="513a5-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="513a5-136">Имя</span><span class="sxs-lookup"><span data-stu-id="513a5-136">Name</span></span> |<span data-ttu-id="513a5-137">Идентификатор конечной точки.</span><span class="sxs-lookup"><span data-stu-id="513a5-137">An identifier for the endpoint.</span></span> |
   | <span data-ttu-id="513a5-138">Закрытый порт</span><span class="sxs-lookup"><span data-stu-id="513a5-138">Private Port</span></span> |<span data-ttu-id="513a5-139">Порт для доступа к сети, являющийся внутренним для приложения.</span><span class="sxs-lookup"><span data-stu-id="513a5-139">The port for network access internal to your application.</span></span> |
   | <span data-ttu-id="513a5-140">Протокол</span><span class="sxs-lookup"><span data-stu-id="513a5-140">Protocol</span></span> |<span data-ttu-id="513a5-141">Протокол, используемый на транспортном уровне для этой конечной точки (TCP или UDP).</span><span class="sxs-lookup"><span data-stu-id="513a5-141">The protocol that the transport layer for this endpoint uses, either TCP or UDP.</span></span> |
   | <span data-ttu-id="513a5-142">Общий порт</span><span class="sxs-lookup"><span data-stu-id="513a5-142">Public Port</span></span> |<span data-ttu-id="513a5-143">Порт, используемый для общего доступа к приложению.</span><span class="sxs-lookup"><span data-stu-id="513a5-143">The port that’s used for public access to your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="513a5-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="513a5-144">Next steps</span></span>
<span data-ttu-id="513a5-145">Дополнительные сведения об использовании ролей Azure в Visual Studio см. в статье [Использование удаленного рабочего стола с ролями Azure](vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="513a5-145">To learn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).</span></span>

