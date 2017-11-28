---
title: "политики лаборатории aaaManage в Azure DevTest Labs | Документы Microsoft"
description: "Дополнительные сведения о том, как размер toodefine лаборатории политики, такие как ВМ, максимальное виртуальных машин на пользователя и завершение работы службы автоматизации."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 351b3645a1fd729455884e5d177877c2986bd853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="bdd5a-103">Управление всеми политиками лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bdd5a-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="bdd5a-104">Azure DevTest Labs позволяет контролировать расходы и свести к минимуму излишние траты в лабораториях с помощью управления политиками (параметрами) для каждой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="bdd5a-105">Подробное пошаговое описание этой статье объясняется, как tooset каждой политики.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-105">This article explains in step-by-step detail how tooset each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="bdd5a-106">Настройка допустимых размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="bdd5a-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="bdd5a-107">Hello политику для hello параметр допускается лаборатории toominimize тратить, позволяя toospecify разрешенных какие размеры виртуальных Машин в лаборатории hello помогает размеры виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-107">hello policy for setting hello allowed VM sizes helps toominimize lab waste by enabling you toospecify which VM sizes are allowed in hello lab.</span></span> <span data-ttu-id="bdd5a-108">Если этот параметр активирован, только размеры виртуальных Машин из этого списка может быть используется toocreate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-108">If this policy is activated, only VM sizes from this list can be used toocreate VMs.</span></span>

1. <span data-ttu-id="bdd5a-109">В лаборатории hello **конфигурации и политиках** колонке выберите **допускается размеры виртуальных машин**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-109">On hello lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Allowed virtual machines sizes](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="bdd5a-111">Выберите **на** tooenable эту политику и **Off** toodisable его.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-111">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="bdd5a-112">Если эта политика включена, выберите один или несколько размеров виртуальных машин, которые могут быть созданы в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="bdd5a-113">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="bdd5a-114">Настройка количества виртуальных машин на пользователя</span><span class="sxs-lookup"><span data-stu-id="bdd5a-114">Set virtual machines per user</span></span>
<span data-ttu-id="bdd5a-115">Здравствуйте, политики для **виртуальных машин на пользователя** позволяет toospecify hello максимальное число виртуальных машин, которые могут быть созданы отдельными пользователями.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-115">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="bdd5a-116">Если пользователь пытается toocreate или утверждения VM достижении hello предельное число пользователей, сообщение об ошибке указывает этой виртуальной Машины нельзя создать или предъявить приветствия.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-116">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="bdd5a-117">В лаборатории hello **конфигурации и политиках** последовательно выберите пункты **виртуальных машин на пользователя**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-117">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtual machines per user](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="bdd5a-119">Выберите **Да** toolimit hello число виртуальных машин на пользователя.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-119">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="bdd5a-120">Если toolimit hello число виртуальных машин на пользователя не требуется, установите **нет**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-120">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="bdd5a-121">При выборе **Да**, введите числовое значение, указывающее максимальное количество виртуальных машин, которые могут быть созданы или пользователь утвердил hello.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-121">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="bdd5a-122">Выберите **Да** toolimit hello число виртуальных машин, которые можно использовать SSD (твердотельных дисков).</span><span class="sxs-lookup"><span data-stu-id="bdd5a-122">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="bdd5a-123">Если количество виртуальных машин, которые можно использовать SSD hello toolimit не требуется, выберите **нет**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-123">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="bdd5a-124">При выборе **Да**, введите значение, указывающее максимальное количество виртуальных машин, которые могут быть созданы с помощью SSD hello.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-124">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="bdd5a-125">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="bdd5a-126">Настройка количества виртуальных машин на лабораторию</span><span class="sxs-lookup"><span data-stu-id="bdd5a-126">Set virtual machines per lab</span></span>
<span data-ttu-id="bdd5a-127">Здравствуйте, политики для **виртуальных машин в лаборатории** позволяет toospecify hello максимальное число виртуальных машин, которые могут быть созданы для текущей лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-127">hello policy for **Virtual machines per lab** allows you toospecify hello maximum number of VMs that can be created for hello current lab.</span></span> <span data-ttu-id="bdd5a-128">Если пользователь пытается toocreate виртуальной Машины в достижении предела лаборатории hello, сообщение об ошибке указывает, hello виртуальной Машины не может быть создан.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-128">If a user attempts toocreate a VM when hello lab limit has been met, an error message indicates that hello VM cannot be created.</span></span> 

1. <span data-ttu-id="bdd5a-129">В лаборатории hello **конфигурации и политиках** последовательно выберите пункты **виртуальных машин в лаборатории**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-129">On hello lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Virtual machines per lab](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="bdd5a-131">Выберите **Да** toolimit hello количества виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-131">Select **Yes** toolimit hello number of VMs per lab.</span></span> <span data-ttu-id="bdd5a-132">Если не требуется toolimit hello количества виртуальных машин в лаборатории, установите **нет**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-132">If you do not want toolimit hello number of VMs per lab, select **No**.</span></span> <span data-ttu-id="bdd5a-133">При выборе **Да**, введите числовое значение, указывающее максимальное количество виртуальных машин, которые могут быть созданы или пользователь утвердил hello.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-133">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="bdd5a-134">Выберите **Да** toolimit hello число виртуальных машин, которые можно использовать SSD (твердотельных дисков).</span><span class="sxs-lookup"><span data-stu-id="bdd5a-134">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="bdd5a-135">Если количество виртуальных машин, которые можно использовать SSD hello toolimit не требуется, выберите **нет**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-135">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="bdd5a-136">При выборе **Да**, введите значение, указывающее максимальное количество виртуальных машин, которые могут быть созданы с помощью SSD hello.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-136">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="bdd5a-137">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="bdd5a-138">Настройка автоматического завершения работы</span><span class="sxs-lookup"><span data-stu-id="bdd5a-138">Set auto-shutdown</span></span>
<span data-ttu-id="bdd5a-139">Политика автоматического завершения работы Hello помогает лаборатории toominimize тратить, позволяя toospecify hello время выключить виртуальные машины в этой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-139">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="bdd5a-140">В лаборатории hello **конфигурации и политиках** колонке выберите **автоматическое завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-140">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Auto-shutdown](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="bdd5a-142">Выберите **на** tooenable эту политику и **Off** toodisable его.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-142">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="bdd5a-143">Если эта политика включена, укажите hello времени (и часовой пояс) tooshut работу всех виртуальных машин в лаборатории текущего hello.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-143">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="bdd5a-144">Укажите **Да** или **нет** для hello параметр toosend toohello предыдущего 15 минут уведомления указано время автоматического завершения работы.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-144">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="bdd5a-145">При указании **Да**, введите уведомление hello tooreceive веб-перехватчика URL-адрес конечной точки.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-145">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="bdd5a-146">Дополнительные сведения об объектах webhook см. в статье [Создание функции Azure объекта webhook или API](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5a-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="bdd5a-147">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-147">Select **Save**.</span></span>

    <span data-ttu-id="bdd5a-148">По умолчанию один раз включена эта политика применяется tooall ВМ в текущей лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-148">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="bdd5a-149">tooremove этот параметр из определенной виртуальной Машине откройте колонку hello ВМ и измените его **автоматическое завершение работы** параметр</span><span class="sxs-lookup"><span data-stu-id="bdd5a-149">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="bdd5a-150">Настройка автоматического запуска</span><span class="sxs-lookup"><span data-stu-id="bdd5a-150">Set auto-start</span></span>
<span data-ttu-id="bdd5a-151">политики автозапуска Hello позволяет toospecify начала hello виртуальных машин в лаборатории текущего hello.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-151">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="bdd5a-152">В лаборатории hello **конфигурации и политиках** колонке выберите **автозапуска**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-152">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Auto-start](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="bdd5a-154">Выберите **на** tooenable эту политику и **Off** toodisable его.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-154">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="bdd5a-155">Если эта политика включена, укажите hello запланированное время начала, часовой пояс и hello дни недели hello, для какой hello применяется времени.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-155">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="bdd5a-156">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-156">Select **Save**.</span></span>

    <span data-ttu-id="bdd5a-157">После включения этой политики не автоматически применяться tooany виртуальные машины в текущей лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-157">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="bdd5a-158">tooapply этот параметр tooa определенную виртуальную Машину, откройте hello ВМ колонки и изменение его **автозапуска** параметр</span><span class="sxs-lookup"><span data-stu-id="bdd5a-158">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="bdd5a-159">Задание срока действия</span><span class="sxs-lookup"><span data-stu-id="bdd5a-159">Set expiration date</span></span>
<span data-ttu-id="bdd5a-160">Можно задать срок действия Дата, когда вы [создать hello ВМ](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="bdd5a-160">You can set an expiration date when you [create hello VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="bdd5a-161">В **Дополнительные параметры**, выберите значок toospecify hello календаря, дата, на котором hello виртуальной Машины будут автоматически удалены.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-161">In **Advanced settings**, choose hello calendar icon toospecify a date on which hello VM will be automatically deleted.</span></span>  <span data-ttu-id="bdd5a-162">По умолчанию hello виртуальных Машин никогда не истекает.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-162">By default, hello VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="bdd5a-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bdd5a-163">Next steps</span></span>
<span data-ttu-id="bdd5a-164">После применения и определенные Здравствуйте различные параметры политики ВМ для лаборатории, Вот некоторые вещи tootry далее:</span><span class="sxs-lookup"><span data-stu-id="bdd5a-164">Once you've defined and applied hello various VM policy settings for your lab, here are some things tootry next:</span></span>

* <span data-ttu-id="bdd5a-165">[Понимание общего IP-адреса](devtest-lab-shared-ip.md) -объясняется, как общий IP адреса используются в DevTest Labs toominimize hello число tooyour необходимые tooconnect лаборатории виртуальных машин для открытого IP адресов.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs toominimize hello number of public IP addresses required tooconnect tooyour lab VMs.</span></span>
* <span data-ttu-id="bdd5a-166">[Настройте управление стоимостью](devtest-lab-configure-cost-management.md) -показано, как toouse hello **ежемесячные тренда Предполагаемая стоимость** диаграммы</span><span class="sxs-lookup"><span data-stu-id="bdd5a-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how toouse hello **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="bdd5a-167">tooview hello текущего месяца Оценка затрат с начала и затраты на конец месяца hello спроецировать.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-167">tooview hello current month's estimated cost-to-date and hello projected end-of-month cost.</span></span>
* <span data-ttu-id="bdd5a-168">[Создание пользовательского образа.](devtest-lab-create-template.md) При создании виртуальной машины необходимо указать базовый образ виртуальной машины, который может представлять собой пользовательский образ или образ из Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="bdd5a-169">В этой статье показано, как toocreate пользовательского образа из VHD-файл.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-169">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="bdd5a-170">[Настройка образов Marketplace.](devtest-lab-configure-marketplace-images.md) Azure DevTest Labs поддерживает создание виртуальных машин на основе образов Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="bdd5a-171">В этой статье показано, как toospecify, который, если таковые имеются, образы Azure Marketplace можно использовать при создании виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-171">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="bdd5a-172">[Создание виртуальной Машины в лабораторной среде](devtest-lab-add-vm-with-artifacts.md) -показано, как toocreate из базового образа виртуальной Машины (либо настраиваемый или Marketplace) и как toowork с артефактами в ВМ.</span><span class="sxs-lookup"><span data-stu-id="bdd5a-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

