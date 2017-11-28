---
title: "aaaDetach диск данных от виртуальной Машины Linux - Azure | Документы Microsoft"
description: "Узнайте, toodetach диск данных от виртуальной машины в Azure с помощью CLI 2.0 или hello портал Azure."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: azurecli
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 1c6145fc97f13179457225e93e0fb7adc261a65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetach-a-data-disk-from-a-linux-virtual-machine"></a><span data-ttu-id="e4dcb-103">Toodetach данных места на диске из виртуальной машины Linux</span><span class="sxs-lookup"><span data-stu-id="e4dcb-103">How toodetach a data disk from a Linux virtual machine</span></span>

<span data-ttu-id="e4dcb-104">Если диск данных, вложенные tooa виртуальной машины больше не нужен, можно легко отключить ее.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-104">When you no longer need a data disk that's attached tooa virtual machine, you can easily detach it.</span></span> <span data-ttu-id="e4dcb-105">Удаляет диск hello из hello виртуальной машины, но не удаляет его из хранилища.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-105">This removes hello disk from hello virtual machine, but doesn't remove it from storage.</span></span> 

> [!WARNING]
> <span data-ttu-id="e4dcb-106">Если отключить диск, он не удаляется автоматически.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-106">If you detach a disk it is not automatically deleted.</span></span> <span data-ttu-id="e4dcb-107">Если вы подписаны tooPremium хранилища, снова tooincur плата хранения для диска hello.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-107">If you have subscribed tooPremium storage, you will continue tooincur storage charges for hello disk.</span></span> <span data-ttu-id="e4dcb-108">Дополнительные сведения см. в разделе слишком[цены и выставление счетов при использовании хранилища Premium](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="e4dcb-108">For more information refer too[Pricing and Billing when using Premium Storage](../../storage/common/storage-premium-storage.md#pricing-and-billing).</span></span> 
> 
> 

<span data-ttu-id="e4dcb-109">Если требуется toouse hello существующие данные на диске hello, вам может быть повторно присоединена toohello одной виртуальной машине, так и любой другой.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-109">If you want toouse hello existing data on hello disk again, you can reattach it toohello same virtual machine, or another one.</span></span>  

## <a name="detach-a-data-disk-using-cli-20"></a><span data-ttu-id="e4dcb-110">Отключение диска данных с помощью CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e4dcb-110">Detach a data disk using CLI 2.0</span></span>

```azurecli
az vm disk detach -g myResourceGroup --vm-name myVm -n myDataDisk
```

<span data-ttu-id="e4dcb-111">Hello диск остается в хранилище, но больше не tooa подключенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-111">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>


## <a name="detach-a-data-disk-using-hello-portal"></a><span data-ttu-id="e4dcb-112">Отсоединить диск данных с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="e4dcb-112">Detach a data disk using hello portal</span></span>
1. <span data-ttu-id="e4dcb-113">В концентраторе hello портала выберите **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-113">In hello portal hub, select **Virtual Machines**.</span></span>
2. <span data-ttu-id="e4dcb-114">Выберите hello виртуальную машину с диска данных hello toodetach и щелкните **остановить** toodeallocate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-114">Select hello virtual machine that has hello data disk you want toodetach and click **Stop** toodeallocate hello VM.</span></span>
3. <span data-ttu-id="e4dcb-115">В колонке hello виртуальной машины, выберите **дисков**.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-115">In hello virtual machine blade, select **Disks**.</span></span>
4. <span data-ttu-id="e4dcb-116">Вверху hello hello **дисков** колонке выберите **изменить**.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-116">At hello top of hello **Disks** blade, select **Edit**.</span></span>
5. <span data-ttu-id="e4dcb-117">В hello **дисков** колонке toohello правому краю hello диск данных, что хотелось бы toodetach, щелкните hello ![изображение кнопки отсоединения](./media/detach-disk/detach.png) «отсоединить».</span><span class="sxs-lookup"><span data-stu-id="e4dcb-117">In hello **Disks** blade, toohello far right of hello data disk that you would like toodetach, click hello ![Detach button image](./media/detach-disk/detach.png) detach button.</span></span>
5. <span data-ttu-id="e4dcb-118">После удаления диска hello щелкните Сохранить hello верхней части колонки hello.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-118">After hello disk has been removed, click Save on hello top of hello blade.</span></span>
6. <span data-ttu-id="e4dcb-119">В колонке hello виртуальную машину, щелкните **Обзор** и нажмите кнопку hello **запустить** кнопку вверху hello hello toorestart hello колонке виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-119">In hello virtual machine blade, click **Overview** and then click hello **Start** button at hello top of hello blade toorestart hello VM.</span></span>

<span data-ttu-id="e4dcb-120">Hello диск остается в хранилище, но больше не tooa подключенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e4dcb-120">hello disk remains in storage but is no longer attached tooa virtual machine.</span></span>








## <a name="next-steps"></a><span data-ttu-id="e4dcb-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e4dcb-121">Next steps</span></span>
<span data-ttu-id="e4dcb-122">Если требуется диск данных tooreuse hello, только что [присоединить ее tooanother ВМ](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e4dcb-122">If you want tooreuse hello data disk, you can just [attach it tooanother VM](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

