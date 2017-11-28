---
title: "aaaCreate Azure DevTest Labs образ из VHD-файл | Документы Microsoft"
description: "Узнайте, как toocreate из файла виртуального жесткого диска с помощью настраиваемого изображения в Azure DevTest Labs hello портал Azure"
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
ms.openlocfilehash: 80af8ea1cb72380f868df0a76c4a0dcd92e63cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="86b25-103">Создание пользовательского образа из VHD-файла</span><span class="sxs-lookup"><span data-stu-id="86b25-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="86b25-104">Пошаговые инструкции</span><span class="sxs-lookup"><span data-stu-id="86b25-104">Step-by-step instructions</span></span>

<span data-ttu-id="86b25-105">Hello следующие шаги содержат пошаговые инструкции по созданию настраиваемого образа из VHD-файла с помощью портала Azure hello:</span><span class="sxs-lookup"><span data-stu-id="86b25-105">hello following steps walk you through creating a custom image from a VHD file using hello Azure portal:</span></span>

1. <span data-ttu-id="86b25-106">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="86b25-106">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="86b25-107">Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="86b25-107">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="86b25-108">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="86b25-108">From hello list of labs, select hello desired lab.</span></span>  

1. <span data-ttu-id="86b25-109">В колонке hello лаборатории выберите **конфигурации**.</span><span class="sxs-lookup"><span data-stu-id="86b25-109">On hello lab's blade, select **Configuration**.</span></span> 

1. <span data-ttu-id="86b25-110">В лаборатории hello **конфигурации** колонке выберите **пользовательских изображений (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="86b25-110">On hello lab **Configuration** blade, select **Custom images (VHDs)**.</span></span>

1. <span data-ttu-id="86b25-111">На hello **пользовательских образов** колонке выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="86b25-111">On hello **Custom images** blade, select **+Add**.</span></span>

    ![Добавить пользовательский образ](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="86b25-113">Введите имя пользовательского образа hello hello.</span><span class="sxs-lookup"><span data-stu-id="86b25-113">Enter hello name of hello custom image.</span></span> <span data-ttu-id="86b25-114">Это имя отображается в списке hello базовые образы, при создании виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="86b25-114">This name is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="86b25-115">Введите описание hello hello пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="86b25-115">Enter hello description of hello custom image.</span></span> <span data-ttu-id="86b25-116">Это описание отображается в списке hello базовые образы, при создании виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="86b25-116">This description is displayed in hello list of base images when creating a VM.</span></span>

1. <span data-ttu-id="86b25-117">Выберите **VHD**.</span><span class="sxs-lookup"><span data-stu-id="86b25-117">Select **VHD**.</span></span>

1. <span data-ttu-id="86b25-118">Из hello **VHD** колонки, выберите hello требуемого файла виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="86b25-118">From hello **VHD** blade, select hello desired VHD file.</span></span>

1. <span data-ttu-id="86b25-119">Выберите **ОК** tooclose hello **VHD** колонку.</span><span class="sxs-lookup"><span data-stu-id="86b25-119">Select **OK** tooclose hello **VHD** blade.</span></span>

1. <span data-ttu-id="86b25-120">Щелкните **Конфигурация ОС**.</span><span class="sxs-lookup"><span data-stu-id="86b25-120">Select **OS configuration**.</span></span>

1. <span data-ttu-id="86b25-121">На hello **конфигурация ОС** выберите либо **Windows** или **Linux**.</span><span class="sxs-lookup"><span data-stu-id="86b25-121">On hello **OS configuration** tab, select either **Windows** or **Linux**.</span></span>

1. <span data-ttu-id="86b25-122">Если **Windows** — флажок установлен, укажите через флажок hello ли *Sysprep* была запущена на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="86b25-122">If **Windows** is selected, specify via hello checkbox whether *Sysprep* has been run on hello machine.</span></span> 

1. <span data-ttu-id="86b25-123">Выберите **ОК** tooclose hello **конфигурация ОС** колонку.</span><span class="sxs-lookup"><span data-stu-id="86b25-123">Select **OK** tooclose hello **OS configuration** blade.</span></span>

1. <span data-ttu-id="86b25-124">Выберите **ОК** toocreate hello пользовательского образа.</span><span class="sxs-lookup"><span data-stu-id="86b25-124">Select **OK** toocreate hello custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="86b25-125">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="86b25-125">Related blog posts</span></span>

- [<span data-ttu-id="86b25-126">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="86b25-126">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="86b25-127">Copying Custom Images between Azure DevTest Labs (Копирование пользовательских образов между лабораториями для разработки и тестирования Azure)</span><span class="sxs-lookup"><span data-stu-id="86b25-127">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="86b25-128">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="86b25-128">Next steps</span></span>

- [<span data-ttu-id="86b25-129">Добавление виртуальных Машин лаборатории tooyour</span><span class="sxs-lookup"><span data-stu-id="86b25-129">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
