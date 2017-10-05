---
title: "Управление базовыми политиками лаборатории в Azure DevTest Labs | Документация Майкрософт"
description: "Узнайте, как настроить некоторые базовые политики (параметры) для лаборатории в DevTest Labs."
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
ms.openlocfilehash: ed35d081b191ec41ed9e5970515057a4715c0d59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="62853-103">Управление базовыми политиками лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="62853-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="62853-104">Azure DevTest Labs позволяет контролировать расходы и свести к минимуму излишние траты в лабораториях с помощью управления политиками (параметрами) для каждой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="62853-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="62853-105">В этой статье показано, как начать работу с политиками, настроив две наиболее важные политики — ограничение числа виртуальных машин, которые может создать или запросить один пользователь, и настройка автоматического завершения работы.</span><span class="sxs-lookup"><span data-stu-id="62853-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="62853-106">Сведения о настройке каждой политики лаборатории см. в статье [Управление всеми политиками лаборатории в Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="62853-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="62853-107">Оценка политик лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="62853-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="62853-108">Ниже приведены инструкции по настройке политик для лаборатории в Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="62853-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="62853-109">Чтобы просмотреть (и изменить) политики для лаборатории, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="62853-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="62853-110">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="62853-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="62853-111">Щелкните **Другие службы**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="62853-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="62853-112">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="62853-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="62853-113">Выберите **Configuration and policies** (Конфигурация и политики).</span><span class="sxs-lookup"><span data-stu-id="62853-113">Select **Configuration and policies**.</span></span>

    ![Колонка "Параметры политики"](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="62853-115">Колонка **Configuration and policies** (Конфигурация и политики) содержит меню параметров, которые можно задать.</span><span class="sxs-lookup"><span data-stu-id="62853-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="62853-116">В этой статье рассматриваются только параметры **Virtual machines per user** (Количество виртуальных машин на пользователя) и **Автозавершение работы**.</span><span class="sxs-lookup"><span data-stu-id="62853-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="62853-117">Сведения о настройке остальных параметров см. в статье [Управление всеми политиками лаборатории в Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="62853-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="62853-118">Настройка количества виртуальных машин на пользователя</span><span class="sxs-lookup"><span data-stu-id="62853-118">Set virtual machines per user</span></span>
<span data-ttu-id="62853-119">Политика для **Virtual machines per user** (Количество виртуальных машин на пользователя) позволяет указать максимальное число виртуальных машин, которые может создать отдельный пользователь.</span><span class="sxs-lookup"><span data-stu-id="62853-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="62853-120">Если пользователь пытается создать или запросить виртуальную машину в случае достижения ограничения для пользователя, то выводится сообщение об ошибке, информирующее о невозможности создания или запроса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="62853-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="62853-121">В меню **Configuration and policies** (Конфигурация и политики) лаборатории выберите **Virtual machines per user** (Количество виртуальных машин на пользователя).</span><span class="sxs-lookup"><span data-stu-id="62853-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtual machines per user](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="62853-123">Выберите **Да**, чтобы ограничить количество виртуальных машин на пользователя.</span><span class="sxs-lookup"><span data-stu-id="62853-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="62853-124">Если вы не хотите ограничивать это количество, то выберите **Нет**.</span><span class="sxs-lookup"><span data-stu-id="62853-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="62853-125">Если вы выбрали **Да**, то введите максимальное количество виртуальных машин, которые может создать или запросить пользователь.</span><span class="sxs-lookup"><span data-stu-id="62853-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="62853-126">Выберите **Да**, чтобы ограничить количество виртуальных машин, которые могут использовать твердотельный накопитель (SSD).</span><span class="sxs-lookup"><span data-stu-id="62853-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="62853-127">Если вы не хотите ограничивать это количество, то выберите **Нет**.</span><span class="sxs-lookup"><span data-stu-id="62853-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="62853-128">Если вы выбрали **Да**, то введите максимальное количество виртуальных машин, которые можно создать с помощью SSD.</span><span class="sxs-lookup"><span data-stu-id="62853-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="62853-129">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="62853-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="62853-130">Настройка автоматического завершения работы</span><span class="sxs-lookup"><span data-stu-id="62853-130">Set auto-shutdown</span></span>
<span data-ttu-id="62853-131">Политика автоматического завершения работы помогает сократить издержки, позволяя указывать время выключения виртуальных машин в этой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="62853-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="62853-132">В колонке **Configuration and Policies** (Конфигурация и политики) лаборатории выберите **Автозавершение работы**.</span><span class="sxs-lookup"><span data-stu-id="62853-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Auto-shutdown](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="62853-134">Щелкните **On** (Вкл.), чтобы включить эту политику, или **Off** (Выкл.), чтобы отключить ее.</span><span class="sxs-lookup"><span data-stu-id="62853-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="62853-135">Если эта политика включена, то укажите время (и часовой пояс) завершения работы всех виртуальных машин в текущей лаборатории.</span><span class="sxs-lookup"><span data-stu-id="62853-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="62853-136">Укажите значение **Да** или **Нет** для параметра отправки уведомления за 15 минут до времени автоматического завершения работы.</span><span class="sxs-lookup"><span data-stu-id="62853-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="62853-137">Если выбрано значение **Да**, то введите конечную точку URL-адреса webhook для получения уведомления.</span><span class="sxs-lookup"><span data-stu-id="62853-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="62853-138">Дополнительные сведения об объектах webhook см. в статье [Создание функции Azure объекта webhook или API](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="62853-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="62853-139">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="62853-139">Select **Save**.</span></span>

    <span data-ttu-id="62853-140">По умолчанию после включения эта политика применяется ко всем виртуальным машинам в текущей лаборатории.</span><span class="sxs-lookup"><span data-stu-id="62853-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="62853-141">Чтобы удалить этот параметр из конкретной виртуальной машины, откройте колонку виртуальной машины и измените значение параметра **Auto-shutdown** (Автоматическое завершение работы).</span><span class="sxs-lookup"><span data-stu-id="62853-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="62853-142">Настройка автоматического запуска</span><span class="sxs-lookup"><span data-stu-id="62853-142">Set auto-start</span></span>
<span data-ttu-id="62853-143">Политика автоматического запуска позволяет указать время запуска виртуальных машин в текущей среде.</span><span class="sxs-lookup"><span data-stu-id="62853-143">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="62853-144">В колонке **Configuration and Policies** (Конфигурация и политики) лаборатории выберите **Auto-start** (Автозапуск).</span><span class="sxs-lookup"><span data-stu-id="62853-144">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Auto-start](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="62853-146">Щелкните **On** (Вкл.), чтобы включить эту политику, или **Off** (Выкл.), чтобы отключить ее.</span><span class="sxs-lookup"><span data-stu-id="62853-146">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="62853-147">Если вы включили эту политику, то укажите время запланированного запуска, часовой пояс и дни недели, к которым применяется это время.</span><span class="sxs-lookup"><span data-stu-id="62853-147">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="62853-148">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="62853-148">Select **Save**.</span></span>

    <span data-ttu-id="62853-149">После включения эта политика не применяется автоматически к виртуальным машинам в текущей лаборатории.</span><span class="sxs-lookup"><span data-stu-id="62853-149">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="62853-150">Чтобы применить этот параметр к конкретной виртуальной машине, откройте колонку виртуальной машины и измените значение параметра **Auto-start** (Автоматический запуск).</span><span class="sxs-lookup"><span data-stu-id="62853-150">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="62853-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="62853-151">Next steps</span></span>

- <span data-ttu-id="62853-152">[Управление всеми политиками лаборатории в Azure DevTest Labs](devtest-lab-set-lab-policy.md): сведения об изменении других политик лаборатории.</span><span class="sxs-lookup"><span data-stu-id="62853-152">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 
