---
title: "политики основные лаборатории aaaManage в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tooset некоторые основные политик hello (параметры) для лаборатории в DevTest Labs"
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
ms.date: 06/29/2017
ms.author: tarcher
ms.openlocfilehash: 792c0d19cfe73964be9c03d3de7751a868fd86e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="51971-103">Управление базовыми политиками лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="51971-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="51971-104">Azure DevTest Labs позволяет toocontrol затрат и снижения убытков в лабораториях, управление политиками (параметры) для каждого занятия.</span><span class="sxs-lookup"><span data-stu-id="51971-104">Azure DevTest Labs enables you toocontrol cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="51971-105">В этой статье, начало работы с политиками обучения как tooset два наиболее важных политики hello - ограничение Здравствуйте, количество виртуальных машин (VM), которые могут быть созданы или заявленным одного пользователя и настройка автоматического завершения работы.</span><span class="sxs-lookup"><span data-stu-id="51971-105">In this article, you get started with policies by learning how tooset two of hello most critical policies - limiting hello number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="51971-106">tooview как tooset каждую политику лаборатории см. в статье hello [определять политики лаборатории в Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="51971-106">tooview how tooset every lab policy, see hello article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="51971-107">Оценка политик лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="51971-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="51971-108">Hello следующие инструкции по настройке политик для лаборатории в Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="51971-108">hello following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="51971-109">tooview (изменение) hello политики и для лаборатории выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="51971-109">tooview (and change) hello policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="51971-110">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="51971-110">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="51971-111">Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="51971-111">Select **More services**, and then select **DevTest Labs** from hello list.</span></span>

1. <span data-ttu-id="51971-112">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="51971-112">From hello list of labs, select hello desired lab.</span></span>   

1. <span data-ttu-id="51971-113">Выберите **Configuration and policies** (Конфигурация и политики).</span><span class="sxs-lookup"><span data-stu-id="51971-113">Select **Configuration and policies**.</span></span>

    ![Колонка "Параметры политики"](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="51971-115">Hello **конфигурации и политиках** колонка содержит меню параметров, которые можно указать.</span><span class="sxs-lookup"><span data-stu-id="51971-115">hello **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="51971-116">В этой статье рассматриваются только параметры hello для **виртуальных машин на пользователя** и **автоматическое завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="51971-116">This article covers only hello settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="51971-117">toolearn о hello оставшиеся параметры, в разделе [управления всеми политиками для лаборатории в Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="51971-117">toolearn about hello remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="51971-118">Настройка количества виртуальных машин на пользователя</span><span class="sxs-lookup"><span data-stu-id="51971-118">Set virtual machines per user</span></span>
<span data-ttu-id="51971-119">Здравствуйте, политики для **виртуальных машин на пользователя** позволяет toospecify hello максимальное число виртуальных машин, которые могут быть созданы отдельными пользователями.</span><span class="sxs-lookup"><span data-stu-id="51971-119">hello policy for **Virtual machines per user** allows you toospecify hello maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="51971-120">Если пользователь пытается toocreate или утверждения VM достижении hello предельное число пользователей, сообщение об ошибке указывает этой виртуальной Машины нельзя создать или предъявить приветствия.</span><span class="sxs-lookup"><span data-stu-id="51971-120">If a user attempts toocreate or claim a VM when hello user limit has been met, an error message indicates that hello VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="51971-121">В лаборатории hello **конфигурации и политиках** последовательно выберите пункты **виртуальных машин на пользователя**.</span><span class="sxs-lookup"><span data-stu-id="51971-121">On hello lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtual machines per user](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="51971-123">Выберите **Да** toolimit hello число виртуальных машин на пользователя.</span><span class="sxs-lookup"><span data-stu-id="51971-123">Select **Yes** toolimit hello number of VMs per user.</span></span> <span data-ttu-id="51971-124">Если toolimit hello число виртуальных машин на пользователя не требуется, установите **нет**.</span><span class="sxs-lookup"><span data-stu-id="51971-124">If you do not want toolimit hello number of VMs per user, select **No**.</span></span> <span data-ttu-id="51971-125">При выборе **Да**, введите числовое значение, указывающее максимальное количество виртуальных машин, которые могут быть созданы или пользователь утвердил hello.</span><span class="sxs-lookup"><span data-stu-id="51971-125">If you select **Yes**, enter a numeric value indicating hello maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="51971-126">Выберите **Да** toolimit hello число виртуальных машин, которые можно использовать SSD (твердотельных дисков).</span><span class="sxs-lookup"><span data-stu-id="51971-126">Select **Yes** toolimit hello number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="51971-127">Если количество виртуальных машин, которые можно использовать SSD hello toolimit не требуется, выберите **нет**.</span><span class="sxs-lookup"><span data-stu-id="51971-127">If you do not want toolimit hello number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="51971-128">При выборе **Да**, введите значение, указывающее максимальное количество виртуальных машин, которые могут быть созданы с помощью SSD hello.</span><span class="sxs-lookup"><span data-stu-id="51971-128">If you select **Yes**, enter a value indicating hello maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="51971-129">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="51971-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="51971-130">Настройка автоматического завершения работы</span><span class="sxs-lookup"><span data-stu-id="51971-130">Set auto-shutdown</span></span>
<span data-ttu-id="51971-131">Политика автоматического завершения работы Hello помогает лаборатории toominimize тратить, позволяя toospecify hello время выключить виртуальные машины в этой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="51971-131">hello auto-shutdown policy helps toominimize lab waste by allowing you toospecify hello time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="51971-132">В лаборатории hello **конфигурации и политиках** колонке выберите **автоматическое завершение работы**.</span><span class="sxs-lookup"><span data-stu-id="51971-132">On hello lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Auto-shutdown](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="51971-134">Выберите **на** tooenable эту политику и **Off** toodisable его.</span><span class="sxs-lookup"><span data-stu-id="51971-134">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

1. <span data-ttu-id="51971-135">Если эта политика включена, укажите hello времени (и часовой пояс) tooshut работу всех виртуальных машин в лаборатории текущего hello.</span><span class="sxs-lookup"><span data-stu-id="51971-135">If you enable this policy, specify hello time (and time zone) tooshut down all VMs in hello current lab.</span></span>

1. <span data-ttu-id="51971-136">Укажите **Да** или **нет** для hello параметр toosend toohello предыдущего 15 минут уведомления указано время автоматического завершения работы.</span><span class="sxs-lookup"><span data-stu-id="51971-136">Specify **Yes** or **No** for hello option toosend a notification 15 minutes prior toohello specified auto-shutdown time.</span></span> <span data-ttu-id="51971-137">При указании **Да**, введите уведомление hello tooreceive веб-перехватчика URL-адрес конечной точки.</span><span class="sxs-lookup"><span data-stu-id="51971-137">If you specify **Yes**, enter a webhook URL endpoint tooreceive hello notification.</span></span> <span data-ttu-id="51971-138">Дополнительные сведения об объектах webhook см. в статье [Создание функции Azure объекта webhook или API](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="51971-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="51971-139">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="51971-139">Select **Save**.</span></span>

    <span data-ttu-id="51971-140">По умолчанию один раз включена эта политика применяется tooall ВМ в текущей лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="51971-140">By default, once enabled, this policy applies tooall VMs in hello current lab.</span></span> <span data-ttu-id="51971-141">tooremove этот параметр из определенной виртуальной Машине откройте колонку hello ВМ и измените его **автоматическое завершение работы** параметр</span><span class="sxs-lookup"><span data-stu-id="51971-141">tooremove this setting from a specific VM, open hello VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="51971-142">Настройка автоматического запуска</span><span class="sxs-lookup"><span data-stu-id="51971-142">Set auto-start</span></span>
<span data-ttu-id="51971-143">политики автозапуска Hello позволяет toospecify начала hello виртуальных машин в лаборатории текущего hello.</span><span class="sxs-lookup"><span data-stu-id="51971-143">hello auto-start policy allows you toospecify when hello VMs in hello current lab should be started.</span></span>  

1. <span data-ttu-id="51971-144">В лаборатории hello **конфигурации и политиках** колонке выберите **автозапуска**.</span><span class="sxs-lookup"><span data-stu-id="51971-144">On hello lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Auto-start](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="51971-146">Выберите **на** tooenable эту политику и **Off** toodisable его.</span><span class="sxs-lookup"><span data-stu-id="51971-146">Select **On** tooenable this policy, and **Off** toodisable it.</span></span>

3. <span data-ttu-id="51971-147">Если эта политика включена, укажите hello запланированное время начала, часовой пояс и hello дни недели hello, для какой hello применяется времени.</span><span class="sxs-lookup"><span data-stu-id="51971-147">If you enable this policy, specify hello scheduled start time, time zone, and hello days of hello week for which hello time applies.</span></span> 

4. <span data-ttu-id="51971-148">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="51971-148">Select **Save**.</span></span>

    <span data-ttu-id="51971-149">После включения этой политики не автоматически применяться tooany виртуальные машины в текущей лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="51971-149">Once enabled, this policy is not automatically applied tooany VMs in hello current lab.</span></span> <span data-ttu-id="51971-150">tooapply этот параметр tooa определенную виртуальную Машину, откройте hello ВМ колонки и изменение его **автозапуска** параметр</span><span class="sxs-lookup"><span data-stu-id="51971-150">tooapply this setting tooa specific VM, open hello VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="51971-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="51971-151">Next steps</span></span>

- <span data-ttu-id="51971-152">[Определить политики лаборатории в Azure DevTest Labs](devtest-lab-set-lab-policy.md) -Узнайте, как toomodify другими политиками лаборатории</span><span class="sxs-lookup"><span data-stu-id="51971-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how toomodify other lab policies</span></span> 
