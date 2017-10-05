---
title: "Создание пользовательского образа Azure DevTest Labs из VHD-файла | Документация Майкрософт"
description: "Сведения о создании пользовательского образа в Azure DevTest Labs из VHD-файла с использованием портала Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 9983ea9b847f44ed18a6169a4bdb224b63626a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="c1949-103">Создание пользовательского образа из VHD-файла</span><span class="sxs-lookup"><span data-stu-id="c1949-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="c1949-104">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="c1949-104">Step-by-step instructions</span></span>

<span data-ttu-id="c1949-105">Ниже приведены инструкции по созданию пользовательского образа из VHD-файла с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="c1949-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="c1949-106">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="c1949-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="c1949-107">Щелкните **Другие службы**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="c1949-107">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="c1949-108">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="c1949-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="c1949-109">В колонке лаборатории выберите **Конфигурация**.</span><span class="sxs-lookup"><span data-stu-id="c1949-109">On the lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="c1949-110">В колонке **Конфигурация** лаборатории выберите **Custom images (VHDs)** (Пользовательские образы (VHD)).</span><span class="sxs-lookup"><span data-stu-id="c1949-110">On the lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="c1949-111">В колонке **Custom images** (Пользовательские образы) выберите **+Add** (+ Добавить).</span><span class="sxs-lookup"><span data-stu-id="c1949-111">On the **Custom images** blade, select **+Add**.</span></span>

    ![Добавить пользовательский образ](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="c1949-113">Введите имя пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="c1949-113">Enter the name of the custom image.</span></span> <span data-ttu-id="c1949-114">Это имя отображается в списке базовых образов при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c1949-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="c1949-115">Введите описание пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="c1949-115">Enter the description of the custom image.</span></span> <span data-ttu-id="c1949-116">Это описание отображается в списке базовых образов при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="c1949-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="c1949-117">Выберите **VHD**.</span><span class="sxs-lookup"><span data-stu-id="c1949-117">Select **VHD**.</span></span>

1. <span data-ttu-id="c1949-118">В колонке **VHD** выберите нужный VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="c1949-118">From the **VHD** blade, select the desired VHD file.</span></span>

1. <span data-ttu-id="c1949-119">Нажмите кнопку **ОК**, чтобы закрыть колонку **VHD**.</span><span class="sxs-lookup"><span data-stu-id="c1949-119">Select **OK** to close the **VHD** blade.</span></span>

1. <span data-ttu-id="c1949-120">Щелкните **Конфигурация ОС**.</span><span class="sxs-lookup"><span data-stu-id="c1949-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="c1949-121">На вкладке **Конфигурация ОС** выберите **Windows** или **Linux**.</span><span class="sxs-lookup"><span data-stu-id="c1949-121">On the **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="c1949-122">Если выбран вариант **Windows** , то с помощью флажка укажите, была ли запущена программа *Sysprep* .</span><span class="sxs-lookup"><span data-stu-id="c1949-122">If **Windows** is selected, specify via the checkbox whether *Sysprep* has been run on the machine.</span></span> 

1. <span data-ttu-id="c1949-123">Нажмите кнопку **ОК**, чтобы закрыть колонку **Конфигурация ОС**.</span><span class="sxs-lookup"><span data-stu-id="c1949-123">Select **OK** to close the **OS configuration** blade.</span></span>

1. <span data-ttu-id="c1949-124">Нажмите кнопку **ОК** , чтобы создать пользовательский образ.</span><span class="sxs-lookup"><span data-stu-id="c1949-124">Select **OK** to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="c1949-125">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="c1949-125">Related blog posts</span></span>

- [<span data-ttu-id="c1949-126">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="c1949-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="c1949-127">Copying Custom Images between Azure DevTest Labs (Копирование пользовательских образов между лабораториями для разработки и тестирования Azure)</span><span class="sxs-lookup"><span data-stu-id="c1949-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="c1949-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c1949-128">Next steps</span></span>

- [<span data-ttu-id="c1949-129">Добавление виртуальной машины с артефактами в лабораторию в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c1949-129">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
