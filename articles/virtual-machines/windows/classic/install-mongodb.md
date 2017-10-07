---
title: "aaaInstall MongoDB на виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall MongoDB на Виртуальной машине Azure создан с hello классической модели развертывания под управлением Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a><span data-ttu-id="7e58b-103">Установите MongoDB на виртуальную машину Windows в Azure</span><span class="sxs-lookup"><span data-stu-id="7e58b-103">Install MongoDB on a Windows VM in Azure</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7e58b-104">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7e58b-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7e58b-105">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="7e58b-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="7e58b-106">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7e58b-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="7e58b-107">tooinstall и настроить с помощью модели развертывания диспетчера ресурсов hello MongoDB см. в разделе [в этой статье](../install-mongodb.md).</span><span class="sxs-lookup"><span data-stu-id="7e58b-107">tooinstall and configure MongoDB using hello Resource Manager deployment model, see [this article](../install-mongodb.md).</span></span>

<span data-ttu-id="7e58b-108">[MongoDB][MongoDB] — это популярная высокопроизводительная база данных NoSQL с открытым кодом.</span><span class="sxs-lookup"><span data-stu-id="7e58b-108">[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="7e58b-109">В этой статье руководство по созданию Windows Server виртуальной машины (VM) с помощью hello [портал Azure][AzurePortal].</span><span class="sxs-lookup"><span data-stu-id="7e58b-109">This article guides you through creating a Windows Server virtual machine (VM) using hello [Azure portal][AzurePortal].</span></span> <span data-ttu-id="7e58b-110">Затем создайте и присоединить toohello диска данных виртуальной Машины перед установкой и настройкой MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7e58b-110">You then create and attach a data disk toohello VM before installing and configuring MongoDB.</span></span> <span data-ttu-id="7e58b-111">При наличии существующей виртуальной Машины в Azure, желательно toouse перехода непосредственно слишком[Установка и настройка MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="7e58b-111">If you have an existing VM in Azure that you would like toouse, you can jump straight too[installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).</span></span>

## <a name="create-a-virtual-machine-running-windows-server"></a><span data-ttu-id="7e58b-112">Создание виртуальной машины под управлением Windows Server</span><span class="sxs-lookup"><span data-stu-id="7e58b-112">Create a virtual machine running Windows Server</span></span>
<span data-ttu-id="7e58b-113">Выполните эти инструкции toocreate виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7e58b-113">Follow these instructions toocreate a virtual machine.</span></span>

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> <span data-ttu-id="7e58b-114">Добавить конечную точку для MongoDB при создании виртуальной машины hello и настроить его следующим образом: имя его как **Mongo**, используйте **TCP** как hello протокола и set обеих hello общие и частные порты слишком**27017**.</span><span class="sxs-lookup"><span data-stu-id="7e58b-114">You can add an endpoint for MongoDB while creating hello virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as hello protocol, and set both hello public and private ports too**27017**.</span></span>
>
>

## <a name="attach-a-data-disk"></a><span data-ttu-id="7e58b-115">Присоединение диска данных</span><span class="sxs-lookup"><span data-stu-id="7e58b-115">Attach a data disk</span></span>
<span data-ttu-id="7e58b-116">tooprovide хранилище для hello виртуальной машины, подключить диск данных и затем инициализируйте его, чтобы Windows могла использовать его.</span><span class="sxs-lookup"><span data-stu-id="7e58b-116">tooprovide storage for hello virtual machine, attach a data disk and then initialize it so that Windows can use it.</span></span> <span data-ttu-id="7e58b-117">Можно подключить существующий диск или пустой диск.</span><span class="sxs-lookup"><span data-stu-id="7e58b-117">If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.</span></span>

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

<span data-ttu-id="7e58b-118">Инициализация диска hello инструкции см. в разделе «как: инициализация нового диска с данными в Windows Server» в [как tooattach данных на диске виртуальной машины Windows tooa](attach-disk.md).</span><span class="sxs-lookup"><span data-stu-id="7e58b-118">For instructions on initializing hello disk, see "How to: Initialize a new data disk in Windows Server" in [How tooattach a data disk tooa Windows virtual machine](attach-disk.md).</span></span>

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a><span data-ttu-id="7e58b-119">Установить и запустить на виртуальной машине hello MongoDB</span><span class="sxs-lookup"><span data-stu-id="7e58b-119">Install and run MongoDB on hello virtual machine</span></span>
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a><span data-ttu-id="7e58b-120">Сводка</span><span class="sxs-lookup"><span data-stu-id="7e58b-120">Summary</span></span>
<span data-ttu-id="7e58b-121">В этом учебнике вы узнали, как toocreate виртуальной машины под управлением Windows Server удаленно подключиться tooit и присоединить диск данных.</span><span class="sxs-lookup"><span data-stu-id="7e58b-121">In this tutorial, you learned how toocreate a virtual machine running Windows Server, remotely connect tooit, and attach a data disk.</span></span>  <span data-ttu-id="7e58b-122">Вы также узнали, каким образом tooinstall и настройте MongoDB на основе Windows hello виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="7e58b-122">You also learned how tooinstall and configure MongoDB on hello Windows-based virtual machine.</span></span> <span data-ttu-id="7e58b-123">Теперь вы можете просматривать MongoDB на hello на основе Windows виртуальной машины с следующие дополнительные разделы в hello hello [документацию MongoDB][MongoDocs].</span><span class="sxs-lookup"><span data-stu-id="7e58b-123">You can now access MongoDB on hello Windows-based virtual machine, by following hello advanced topics in hello [MongoDB documentation][MongoDocs].</span></span>

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

