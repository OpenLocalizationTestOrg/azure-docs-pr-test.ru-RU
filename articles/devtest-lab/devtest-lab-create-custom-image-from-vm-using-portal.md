---
title: "Создание пользовательского образа Azure DevTest Labs из виртуальной машины | Документация Майкрософт"
description: "Сведения о создании пользовательского образа в Azure DevTest Labs из подготовленной виртуальной машины с использованием портала Azure"
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
ms.openlocfilehash: 9d2dcf7164985508d691e8a0c123efaf3b8aa19a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="7be1e-103">Создание пользовательского образа из виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7be1e-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="7be1e-104">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="7be1e-104">Step-by-step instructions</span></span>

<span data-ttu-id="7be1e-105">Вы можете создать пользовательский образ из подготовленной виртуальной машины, а затем использовать его для создания идентичных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="7be1e-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="7be1e-106">Ниже описано, как создать пользовательский образ на основе виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7be1e-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="7be1e-107">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="7be1e-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="7be1e-108">Щелкните **Другие службы**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="7be1e-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="7be1e-109">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="7be1e-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="7be1e-110">В колонке лаборатории выберите **My virtual machines**(Мои виртуальные машины).</span><span class="sxs-lookup"><span data-stu-id="7be1e-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="7be1e-111">В колонке **My virtual machines** (Мои виртуальные машины) выберите виртуальную машину, на основе которой будет создан пользовательский образ.</span><span class="sxs-lookup"><span data-stu-id="7be1e-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="7be1e-112">В колонке виртуальной машины выберите **Create custom image (VHD)**(Создать пользовательский образ (VHD)).</span><span class="sxs-lookup"><span data-stu-id="7be1e-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Пункт меню "Создание пользовательского образа"](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="7be1e-114">В колонке **Create image** (Создание образа) введите имя и описание нового пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="7be1e-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="7be1e-115">Эти данные отображаются в списке базовых образов при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7be1e-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![Колонка "Создание пользовательского образа"](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="7be1e-117">Укажите, была ли выполнена на виртуальной машине программа sysprep.</span><span class="sxs-lookup"><span data-stu-id="7be1e-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="7be1e-118">Если программа sysprep не была запущена на виртуальной машине, укажите, нужно ли ее запускать при создании виртуальной машины из этого пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="7be1e-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="7be1e-119">Нажмите кнопку **ОК** , чтобы создать пользовательский образ.</span><span class="sxs-lookup"><span data-stu-id="7be1e-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="7be1e-120">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="7be1e-120">Related blog posts</span></span>

- [<span data-ttu-id="7be1e-121">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="7be1e-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="7be1e-122">Copying Custom Images between Azure DevTest Labs (Копирование пользовательских образов между лабораториями для разработки и тестирования Azure)</span><span class="sxs-lookup"><span data-stu-id="7be1e-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="7be1e-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7be1e-123">Next steps</span></span>

- [<span data-ttu-id="7be1e-124">Добавление виртуальной машины с артефактами в лабораторию в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="7be1e-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
