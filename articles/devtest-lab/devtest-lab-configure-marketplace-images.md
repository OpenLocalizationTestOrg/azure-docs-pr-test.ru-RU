---
title: "Параметры изображения aaaConfigure Azure Marketplace в Azure DevTest Labs | Документы Microsoft"
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
ms.openlocfilehash: bb4b7f1c0cbe967bee724f7ee20f64f8c4ea58ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-marketplace-image-settings-in-azure-devtest-labs"></a><span data-ttu-id="fb919-103">Настройка параметров образов Azure Marketplace в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fb919-103">Configure Azure Marketplace image settings in Azure DevTest Labs</span></span>
<span data-ttu-id="fb919-104">DevTest Labs поддерживает создание виртуальных машин на основе образов Azure Marketplace в зависимости от того, как вы настроили Azure Marketplace toobe изображений, используемых в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="fb919-104">DevTest Labs supports creating VMs based on Azure Marketplace images depending on how you have configured Azure Marketplace images toobe used in your lab.</span></span> <span data-ttu-id="fb919-105">В этой статье показано, как toospecify, который, если таковые имеются, образы Azure Marketplace можно использовать при создании виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="fb919-105">This article shows you how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span> <span data-ttu-id="fb919-106">Это гарантирует, что у команды есть только доступ toohello Marketplace образов, которые они должны.</span><span class="sxs-lookup"><span data-stu-id="fb919-106">This ensures that your team only has access toohello Marketplace images they need.</span></span> 

## <a name="select-which-azure-marketplace-images-are-allowed-when-creating-a-vm"></a><span data-ttu-id="fb919-107">Выбор разрешенных образов Azure Marketplace при создании виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="fb919-107">Select which Azure Marketplace images are allowed when creating a VM</span></span>
1. <span data-ttu-id="fb919-108">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fb919-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="fb919-109">Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="fb919-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="fb919-110">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="fb919-110">From hello list of labs, select hello desired lab.</span></span> 
4. <span data-ttu-id="fb919-111">В колонке hello лаборатории выберите **конфигурации и политиках**.</span><span class="sxs-lookup"><span data-stu-id="fb919-111">On hello lab's blade, select **Configuration and policies**.</span></span>
5. <span data-ttu-id="fb919-112">В колонке **Конфигурация и политики** лаборатории в разделе **Базы виртуальных машин** выберите **Образы Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="fb919-112">On lab's **Configuration and policies** blade under **Virtual Machine Bases**, select **Marketplace images**.</span></span>
6. <span data-ttu-id="fb919-113">Укажите, следует ли все hello полное toobe образы Azure Marketplace, доступных для использования в качестве основы новой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="fb919-113">Specify whether you want all hello qualified Azure Marketplace images toobe available for use as a base of a new VM.</span></span> <span data-ttu-id="fb919-114">При выборе **Да**, затем все образы Azure Marketplace hello в лаборатории hello допускается, удовлетворяющих hello все следующие условия:</span><span class="sxs-lookup"><span data-stu-id="fb919-114">If you select **Yes**, then all hello Azure Marketplace images that meet all hello following criteria are allowed in hello lab:</span></span>
   
   * <span data-ttu-id="fb919-115">изображение Hello создает одной виртуальной Машины **и**</span><span class="sxs-lookup"><span data-stu-id="fb919-115">hello image creates a single VM, **and**</span></span>
   * <span data-ttu-id="fb919-116">образ Hello использует ВМ tooprovision диспетчера ресурсов Azure, **и**</span><span class="sxs-lookup"><span data-stu-id="fb919-116">hello image uses Azure Resource Manager tooprovision VMs, **and**</span></span>
   * <span data-ttu-id="fb919-117">изображение Hello не требует приобретения дополнительного лицензирования план</span><span class="sxs-lookup"><span data-stu-id="fb919-117">hello image doesn't require purchasing an extra licensing plan</span></span>
     
    <span data-ttu-id="fb919-118">Если нужно, toobe изображений не допускается, или вы хотите toospecify изображения, можно использовать, выберите **нет**.</span><span class="sxs-lookup"><span data-stu-id="fb919-118">If you want no images toobe allowed, or you want toospecify which images can be used, select **No**.</span></span>
     
     ![Параметр tooallow все toobe Marketplace образов используется в качестве базовые образы для виртуальных машин](./media/devtest-lab-configure-marketplace-images/allow-all-marketplace-images.png)
7. <span data-ttu-id="fb919-120">При выборе **нет** toohello предыдущего шага hello **разрешено изображения или выбирать все** установлен флажок.</span><span class="sxs-lookup"><span data-stu-id="fb919-120">If you select **No** toohello previous step, hello **Allowed images/Select all** checkbox is enabled.</span></span> 
   <span data-ttu-id="fb919-121">Можно использовать этот параметр вместе с tooquickly hello поиска выберите или отмените выбор всех hello элементов, отображаемых в списке hello.</span><span class="sxs-lookup"><span data-stu-id="fb919-121">You can use this option together with hello search box tooquickly select or deselect all hello items displayed in hello list.</span></span>
   * <span data-ttu-id="fb919-122">Выберите образы Azure Marketplace hello требуется tooallow для создания виртуальной Машины по отдельности, установив соответствующий флажок для каждого изображения.</span><span class="sxs-lookup"><span data-stu-id="fb919-122">Select hello Azure Marketplace images you want tooallow for VM creation individually by checking each image's corresponding checkbox.</span></span>
   * <span data-ttu-id="fb919-123">Если вы не хотите tooallow любой toobe образы Azure Marketplace, используемых в лаборатории hello, выбор пуст из списка hello.</span><span class="sxs-lookup"><span data-stu-id="fb919-123">Select nothing from hello list if you don't want tooallow any Azure Marketplace images toobe used in hello lab.</span></span>
   
    ![Можно указать, какие образы Azure Marketplace будут использоваться в качестве базовых образов для виртуальных машин.](./media/devtest-lab-configure-marketplace-images/select-marketplace-images.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="fb919-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb919-125">Next steps</span></span>
<span data-ttu-id="fb919-126">После настройки как образы Azure Marketplace могут при создании виртуальной Машины hello следующим шагом является слишком[добавления виртуальных Машин лаборатории tooyour](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="fb919-126">Once you have configured how Azure Marketplace images are allowed when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

