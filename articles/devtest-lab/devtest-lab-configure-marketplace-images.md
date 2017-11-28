---
title: "Настройка параметров образов Azure Marketplace в Azure DevTest Labs | Документация Майкрософт"
description: "Настройка образов Azure Marketplace, которые можно использовать при создании виртуальной машины в Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 804c6af2-17e9-4320-af3a-f454bd398379
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: 5f888c9d92a9164cc7d3d1aed66c29a724b365d7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="4e806-103">Настройка параметров образов Azure Marketplace в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4e806-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="4e806-104">DevTest Labs поддерживает создание виртуальных машин на основе образов Azure Marketplace в зависимости от того, как вы настроили образы Azure Marketplace для использования в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4e806-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images to be used in your lab.</span></span> <span data-ttu-id="4e806-105">В этой статье показано, как определить, какие образы Azure Marketplace (если таковые имеются) можно использовать при создании виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4e806-105">This article shows you how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="4e806-106">Благодаря этому ваша рабочая группа будет иметь доступ только к тем образам Marketplace, которые ей требуются.</span><span class="sxs-lookup"><span data-stu-id="4e806-106">This ensures that your team only has access to the Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="4e806-107">Выбор разрешенных образов Azure Marketplace при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4e806-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="4e806-108">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4e806-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="4e806-109">Щелкните **Больше служб**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="4e806-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="4e806-110">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="4e806-110">From the list of labs, select the desired lab.</span></span> 
4. <span data-ttu-id="4e806-111">В колонке лаборатории выберите **Конфигурация и политики**.</span><span class="sxs-lookup"><span data-stu-id="4e806-111">On the lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="4e806-112">В колонке **Конфигурация и политики** лаборатории в разделе **Базы виртуальных машин** выберите **Образы Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="4e806-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="4e806-113">Укажите, должны ли все соответствующие образы Azure Marketplace быть доступны для использования в качестве основы новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4e806-113">Specify whether you want all the qualified Azure Marketplace images to be available for use as a base of a new VM.</span></span> <span data-ttu-id="4e806-114">При выборе варианта **Да**в лаборатории будут разрешены все образы Azure Marketplace, соответствующие всем следующим условиям:</span><span class="sxs-lookup"><span data-stu-id="4e806-114">If you select **Yes**, then all the Azure Marketplace images that meet all the following criteria are allowed in the lab:</span></span>
   
   * <span data-ttu-id="4e806-115">образ создает одну виртуальную машину **и**</span><span class="sxs-lookup"><span data-stu-id="4e806-115">The image creates a single VM, **and**</span></span>
   * <span data-ttu-id="4e806-116">образ использует диспетчер ресурсов Azure для подготовки виртуальных машин, **а также**</span><span class="sxs-lookup"><span data-stu-id="4e806-116">The image uses Azure Resource Manager to provision VMs, **and**</span></span>
   * <span data-ttu-id="4e806-117">для образа не требуется приобретать дополнительный план лицензирования.</span><span class="sxs-lookup"><span data-stu-id="4e806-117">The image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="4e806-118">Если не требуется разрешать никакие образы или нужно указать, какие образы можно использовать, нажмите кнопку **Нет**.</span><span class="sxs-lookup"><span data-stu-id="4e806-118">If you want no images to be allowed, or you want to specify which images can be used, select **No**.</span></span>
     
     ![Параметр для разрешения использования всех образов Marketplace в качестве базовых образов для виртуальных машин](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="4e806-120">Если на предыдущем шаге вы выбрали **Нет**, то активируется флажок **Allowed images/Select all** (Разрешенные образы/выбрать все).</span><span class="sxs-lookup"><span data-stu-id="4e806-120">If you select **No** to the previous step, the **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="4e806-121">Этот параметр можно использовать вместе с полем поиска для быстрого выбора или отмены выбора всех элементов, отображаемых в списке.</span><span class="sxs-lookup"><span data-stu-id="4e806-121">You can use this option together with the search box to quickly select or deselect all the items displayed in the list.</span></span>
   * <span data-ttu-id="4e806-122">Образы Azure Marketplace, которые необходимо разрешить для создания виртуальной машины, можно выбрать по отдельности, установив соответствующий флажок для каждого образа.</span><span class="sxs-lookup"><span data-stu-id="4e806-122">Select the Azure Marketplace images you want to allow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="4e806-123">Ничего не выбирайте, если не хотите использовать образы Azure Marketplace в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4e806-123">Select nothing from the list if you don't want to allow any Azure Marketplace images to be used in the lab.</span></span>
   
    ![Можно указать, какие образы Azure Marketplace будут использоваться в качестве базовых образов для виртуальных машин.](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4e806-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4e806-125">Next steps</span></span>
<span data-ttu-id="4e806-126">После настройки разрешения образов Azure Marketplace при создании виртуальной машины необходимо [добавить виртуальную машину в лабораторию](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="4e806-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

