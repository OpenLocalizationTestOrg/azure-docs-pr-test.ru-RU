---
title: "aaaCreate Azure DevTest Labs пользовательского образа из виртуальной Машины | Документы Microsoft"
description: "Узнайте, как toocreate из подготовленных виртуальной Машины с помощью настраиваемого изображения в Azure DevTest Labs hello портал Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 7dccb79d3db4aae676c7bd2f6b800301210491e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="e3440-103">Создание пользовательского образа из виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e3440-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="e3440-104">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="e3440-104">Step-by-step instructions</span></span>

<span data-ttu-id="e3440-105">Создать образ из подготовленных виртуальной Машины и впоследствии использовать toocreate этого пользовательского образа идентичные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e3440-105">You can create a custom image from a provisioned VM, and afterwards use that custom image toocreate identical VMs.</span></span> <span data-ttu-id="e3440-106">Привет, следующие шаги показывают, как toocreate пользовательского образа из виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="e3440-106">hello following steps illustrate how toocreate a custom image from a VM:</span></span>

1. <span data-ttu-id="e3440-107">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="e3440-107">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="e3440-108">Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="e3440-108">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="e3440-109">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="e3440-109">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="e3440-110">В колонке hello лаборатории выберите **моих виртуальных машин**.</span><span class="sxs-lookup"><span data-stu-id="e3440-110">On hello lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="e3440-111">На hello **моих виртуальных машин** колонки, из которого нужно toocreate hello пользовательского образа виртуальной Машины выберите hello.</span><span class="sxs-lookup"><span data-stu-id="e3440-111">On hello **My virtual machines** blade, select hello VM from which you want toocreate hello custom image.</span></span>

1. <span data-ttu-id="e3440-112">В колонке hello виртуальной Машины выберите **создать пользовательский образ (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="e3440-112">On hello VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Пункт меню "Создание пользовательского образа"](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="e3440-114">На hello **создать изображение** колонки, введите имя и описание для настраиваемого образа.</span><span class="sxs-lookup"><span data-stu-id="e3440-114">On hello **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="e3440-115">Эта информация отображается в списке базовых классов hello при создании виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e3440-115">This information is displayed in hello list of bases when you create a VM.</span></span>

    ![Колонка "Создание пользовательского образа"](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="e3440-117">Выберите, будут ли на hello виртуальной Машины было запущено средство sysprep.</span><span class="sxs-lookup"><span data-stu-id="e3440-117">Select whether sysprep was run on hello VM.</span></span> <span data-ttu-id="e3440-118">Если hello sysprep не была запущена на hello виртуальной Машины, укажите, следует ли запускать, когда виртуальная машина создается из этого пользовательского образа sysprep.</span><span class="sxs-lookup"><span data-stu-id="e3440-118">If hello sysprep was not run on hello VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="e3440-119">Выберите **ОК** при завершении toocreate hello пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="e3440-119">Select **OK** when finished toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="e3440-120">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="e3440-120">Related blog posts</span></span>

- [<span data-ttu-id="e3440-121">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="e3440-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="e3440-122">Copying Custom Images between Azure DevTest Labs (Копирование пользовательских образов между лабораториями для разработки и тестирования Azure)</span><span class="sxs-lookup"><span data-stu-id="e3440-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="e3440-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e3440-123">Next steps</span></span>

- [<span data-ttu-id="e3440-124">Добавление виртуальных Машин лаборатории tooyour</span><span class="sxs-lookup"><span data-stu-id="e3440-124">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
