---
title: "Управление политиками лаборатории в Azure DevTest Labs | Документация Майкрософт"
description: "Узнайте, как определить политики лаборатории, такие как размеры виртуальных машин, максимальное количество виртуальных машин для каждого пользователя и автоматизация завершения работы."
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
ms.openlocfilehash: 328a4d893637d7150807855e118b485a2c3bbfc5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="4af05-103">Управление всеми политиками лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4af05-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="4af05-104">Azure DevTest Labs позволяет контролировать расходы и свести к минимуму излишние траты в лабораториях с помощью управления политиками (параметрами) для каждой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="4af05-105">В этой статье описываются пошаговые действия по настройке каждой политики.</span><span class="sxs-lookup"><span data-stu-id="4af05-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="4af05-106">Настройка допустимых размеров виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4af05-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="4af05-107">Политика для настройки допустимых размеров виртуальных машин помогает сократить издержки, позволяя указывать, какие размеры виртуальных машин допускаются в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="4af05-108">Если эта политика включена, для создания виртуальных машин можно использовать размеры виртуальных машин только из этого списка.</span><span class="sxs-lookup"><span data-stu-id="4af05-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="4af05-109">В колонке **Configuration and policies** (Конфигурация и политики) лаборатории выберите **Allowed virtual machines sizes** (Допустимые размеры виртуальных машин).</span><span class="sxs-lookup"><span data-stu-id="4af05-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Allowed virtual machines sizes](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="4af05-111">Щелкните **On** (Вкл.), чтобы включить эту политику, или **Off** (Выкл.), чтобы отключить ее.</span><span class="sxs-lookup"><span data-stu-id="4af05-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="4af05-112">Если эта политика включена, выберите один или несколько размеров виртуальных машин, которые могут быть созданы в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="4af05-113">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4af05-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="4af05-114">Настройка количества виртуальных машин на пользователя</span><span class="sxs-lookup"><span data-stu-id="4af05-114">Set virtual machines per user</span></span>
<span data-ttu-id="4af05-115">Политика для **Virtual machines per user** (Количество виртуальных машин на пользователя) позволяет указать максимальное число виртуальных машин, которые может создать отдельный пользователь.</span><span class="sxs-lookup"><span data-stu-id="4af05-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="4af05-116">Если пользователь пытается создать или запросить виртуальную машину в случае достижения ограничения для пользователя, то выводится сообщение об ошибке, информирующее о невозможности создания или запроса виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4af05-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="4af05-117">В меню **Configuration and policies** (Конфигурация и политики) лаборатории выберите **Virtual machines per user** (Количество виртуальных машин на пользователя).</span><span class="sxs-lookup"><span data-stu-id="4af05-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtual machines per user](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="4af05-119">Выберите **Да**, чтобы ограничить количество виртуальных машин на пользователя.</span><span class="sxs-lookup"><span data-stu-id="4af05-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="4af05-120">Если вы не хотите ограничивать это количество, то выберите **Нет**.</span><span class="sxs-lookup"><span data-stu-id="4af05-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="4af05-121">Если вы выбрали **Да**, то введите максимальное количество виртуальных машин, которые может создать или запросить пользователь.</span><span class="sxs-lookup"><span data-stu-id="4af05-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="4af05-122">Выберите **Да**, чтобы ограничить количество виртуальных машин, которые могут использовать твердотельный накопитель (SSD).</span><span class="sxs-lookup"><span data-stu-id="4af05-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="4af05-123">Если вы не хотите ограничивать это количество, то выберите **Нет**.</span><span class="sxs-lookup"><span data-stu-id="4af05-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="4af05-124">Если вы выбрали **Да**, то введите максимальное количество виртуальных машин, которые можно создать с помощью SSD.</span><span class="sxs-lookup"><span data-stu-id="4af05-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="4af05-125">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4af05-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="4af05-126">Настройка количества виртуальных машин на лабораторию</span><span class="sxs-lookup"><span data-stu-id="4af05-126">Set virtual machines per lab</span></span>
<span data-ttu-id="4af05-127">Политика для **Virtual machines per lab** (Количество виртуальных машин на лабораторию) позволяет указать максимальное число виртуальных машин, которые можно создать для текущей лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="4af05-128">Если пользователь пытается создать виртуальную машину в случае достижения ограничения для лаборатории, то выводится сообщение об ошибке, информирующее о невозможности создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4af05-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="4af05-129">В меню **Configuration and policies** (Конфигурация и политики) лаборатории выберите **Virtual machines per lab** (Количество виртуальных машин на лабораторию).</span><span class="sxs-lookup"><span data-stu-id="4af05-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Virtual machines per lab](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="4af05-131">Выберите **Да**, чтобы ограничить количество виртуальных машин на лабораторию.</span><span class="sxs-lookup"><span data-stu-id="4af05-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="4af05-132">Если вы не хотите ограничивать это количество, то выберите **Нет**.</span><span class="sxs-lookup"><span data-stu-id="4af05-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="4af05-133">Если вы выбрали **Да**, то введите максимальное количество виртуальных машин, которые может создать или запросить пользователь.</span><span class="sxs-lookup"><span data-stu-id="4af05-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="4af05-134">Выберите **Да**, чтобы ограничить количество виртуальных машин, которые могут использовать твердотельный накопитель (SSD).</span><span class="sxs-lookup"><span data-stu-id="4af05-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="4af05-135">Если вы не хотите ограничивать это количество, то выберите **Нет**.</span><span class="sxs-lookup"><span data-stu-id="4af05-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="4af05-136">Если вы выбрали **Да**, то введите максимальное количество виртуальных машин, которые можно создать с помощью SSD.</span><span class="sxs-lookup"><span data-stu-id="4af05-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="4af05-137">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4af05-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="4af05-138">Настройка автоматического завершения работы</span><span class="sxs-lookup"><span data-stu-id="4af05-138">Set auto-shutdown</span></span>
<span data-ttu-id="4af05-139">Политика автоматического завершения работы помогает сократить издержки, позволяя указывать время выключения виртуальных машин в этой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="4af05-140">В колонке **Configuration and Policies** (Конфигурация и политики) лаборатории выберите **Автозавершение работы**.</span><span class="sxs-lookup"><span data-stu-id="4af05-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Auto-shutdown](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="4af05-142">Щелкните **On** (Вкл.), чтобы включить эту политику, или **Off** (Выкл.), чтобы отключить ее.</span><span class="sxs-lookup"><span data-stu-id="4af05-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="4af05-143">Если эта политика включена, то укажите время (и часовой пояс) завершения работы всех виртуальных машин в текущей лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="4af05-144">Укажите значение **Да** или **Нет** для параметра отправки уведомления за 15 минут до времени автоматического завершения работы.</span><span class="sxs-lookup"><span data-stu-id="4af05-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="4af05-145">Если выбрано значение **Да**, то введите конечную точку URL-адреса webhook для получения уведомления.</span><span class="sxs-lookup"><span data-stu-id="4af05-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="4af05-146">Дополнительные сведения об объектах webhook см. в статье [Создание функции Azure объекта webhook или API](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="4af05-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="4af05-147">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4af05-147">Select **Save**.</span></span>

    <span data-ttu-id="4af05-148">По умолчанию после включения эта политика применяется ко всем виртуальным машинам в текущей лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="4af05-149">Чтобы удалить этот параметр из конкретной виртуальной машины, откройте колонку виртуальной машины и измените значение параметра **Auto-shutdown** (Автоматическое завершение работы).</span><span class="sxs-lookup"><span data-stu-id="4af05-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="4af05-150">Настройка автоматического запуска</span><span class="sxs-lookup"><span data-stu-id="4af05-150">Set auto-start</span></span>
<span data-ttu-id="4af05-151">Политика автоматического запуска позволяет указать время запуска виртуальных машин в текущей среде.</span><span class="sxs-lookup"><span data-stu-id="4af05-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="4af05-152">В колонке **Configuration and Policies** (Конфигурация и политики) лаборатории выберите **Auto-start** (Автозапуск).</span><span class="sxs-lookup"><span data-stu-id="4af05-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Auto-start](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="4af05-154">Щелкните **On** (Вкл.), чтобы включить эту политику, или **Off** (Выкл.), чтобы отключить ее.</span><span class="sxs-lookup"><span data-stu-id="4af05-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="4af05-155">Если вы включили эту политику, то укажите время запланированного запуска, часовой пояс и дни недели, к которым применяется это время.</span><span class="sxs-lookup"><span data-stu-id="4af05-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="4af05-156">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="4af05-156">Select **Save**.</span></span>

    <span data-ttu-id="4af05-157">После включения эта политика не применяется автоматически к виртуальным машинам в текущей лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="4af05-158">Чтобы применить этот параметр к конкретной виртуальной машине, откройте колонку виртуальной машины и измените значение параметра **Auto-start** (Автоматический запуск).</span><span class="sxs-lookup"><span data-stu-id="4af05-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="4af05-159">Задание срока действия</span><span class="sxs-lookup"><span data-stu-id="4af05-159">Set expiration date</span></span>
<span data-ttu-id="4af05-160">Вы можете задать дату истечения срока действия при [создании виртуальной машины](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="4af05-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="4af05-161">В **дополнительных параметрах** щелкните значок календаря и укажите дату, в которую виртуальная машина будет автоматически удалена.</span><span class="sxs-lookup"><span data-stu-id="4af05-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="4af05-162">По умолчанию виртуальная машина является бессрочной.</span><span class="sxs-lookup"><span data-stu-id="4af05-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="4af05-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4af05-163">Next steps</span></span>
<span data-ttu-id="4af05-164">После определения и применения различных параметров политики виртуальных машин для лаборатории можно выполнить следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="4af05-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="4af05-165">[Общие IP-адреса в Azure DevTest Labs](devtest-lab-shared-ip.md). Объясняется, как с помощью общих IP-адресов в DevTest Labs минимизировать количество общедоступных IP-адресов, необходимых для подключения к виртуальным машинам лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="4af05-166">[Настройка управления затратами.](devtest-lab-configure-cost-management.md) Показано, как использовать диаграмму **Monthly Estimated Cost Trend** (Помесячная тенденция изменения оценочной стоимости),</span><span class="sxs-lookup"><span data-stu-id="4af05-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="4af05-167">чтобы просматривать стоимость на данный момент в текущем календарном месяце и прогнозируемую стоимость на конец месяца.</span><span class="sxs-lookup"><span data-stu-id="4af05-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="4af05-168">[Создание пользовательского образа.](devtest-lab-create-template.md) При создании виртуальной машины необходимо указать базовый образ виртуальной машины, который может представлять собой пользовательский образ или образ из Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4af05-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="4af05-169">В этой статье показано, как создать настраиваемый образ из VHD-файла.</span><span class="sxs-lookup"><span data-stu-id="4af05-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="4af05-170">[Настройка образов Marketplace.](devtest-lab-configure-marketplace-images.md) Azure DevTest Labs поддерживает создание виртуальных машин на основе образов Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4af05-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="4af05-171">В этой статье показано, как определить, какие образы Azure Marketplace (если таковые имеются) можно использовать при создании виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4af05-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="4af05-172">[Добавление виртуальной машины с артефактами в лабораторию.](devtest-lab-add-vm-with-artifacts.md) В этой статье рассказывается, как создать виртуальную машину из базового образа (пользовательского или из Marketplace) и работать с артефактами виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4af05-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

