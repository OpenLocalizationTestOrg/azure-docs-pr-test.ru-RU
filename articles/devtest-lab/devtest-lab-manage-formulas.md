---
title: "Управление формулами в Azure DevTest Labs для создания виртуальных машин | Документация Майкрософт"
description: "Узнайте, как изменять и удалять формулы Azure DevTest Labs."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfdab5def50158f9b764bbb1e50c2624cc6d5fb3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="4d942-103">Управление формулами Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4d942-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="4d942-104">В этой статье показано, как создать формулу из базового образа (пользовательского образа, образа Marketplace или другой формулы) или существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4d942-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="4d942-105">В этой статье также объясняется, как управлять существующими формулами.</span><span class="sxs-lookup"><span data-stu-id="4d942-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="4d942-106">Создание формулы</span><span class="sxs-lookup"><span data-stu-id="4d942-106">Create a formula</span></span>
<span data-ttu-id="4d942-107">Любой пользователь, имеющий разрешения роли *Пользователь* DevTest Labs, может создавать виртуальные машины на основе формул.</span><span class="sxs-lookup"><span data-stu-id="4d942-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="4d942-108">Формулы можно создавать двумя способами.</span><span class="sxs-lookup"><span data-stu-id="4d942-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="4d942-109">Из базового образа — используйте этот способ, если хотите задать все характеристики формулы.</span><span class="sxs-lookup"><span data-stu-id="4d942-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="4d942-110">На основе существующей виртуальной машины — используйте этот способ, если хотите создать формулу на основе параметров существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4d942-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="4d942-111">Дополнительные сведения о добавлении пользователей и разрешений см. в статье [Добавление владельцев и пользователей в Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="4d942-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="4d942-112">Создание формулы из базового образа</span><span class="sxs-lookup"><span data-stu-id="4d942-112">Create a formula from a base</span></span>
<span data-ttu-id="4d942-113">Ниже приведены пошаговые инструкции по созданию формулы на основе пользовательского образа, образа Marketplace или другой формулы.</span><span class="sxs-lookup"><span data-stu-id="4d942-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="4d942-114">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4d942-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="4d942-115">Щелкните **Больше служб**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="4d942-115">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="4d942-116">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="4d942-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="4d942-117">В колонке лаборатории выберите **Formulas (reusable bases)**(Формулы (базовые образы, используемые повторно)).</span><span class="sxs-lookup"><span data-stu-id="4d942-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Меню формулы](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="4d942-119">В колонке **Formulas** (Формулы) выберите **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="4d942-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![Добавление формулы](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="4d942-121">В колонке **Выбор основы** выберите базовый образ (пользовательский образ, образ Marketplace или формулу), на основе которого хотите создать формулу.</span><span class="sxs-lookup"><span data-stu-id="4d942-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![Список базовых образов](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="4d942-123">В колонке **Создание формулы** укажите перечисленные ниже значения.</span><span class="sxs-lookup"><span data-stu-id="4d942-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="4d942-124">**Имя формулы** — введите имя формулы.</span><span class="sxs-lookup"><span data-stu-id="4d942-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="4d942-125">Это значение отображается в списке базовых образов при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4d942-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="4d942-126">Имя проверяется по мере ввода. Если оно недопустимо, появляется сообщение с указанием требований к именам.</span><span class="sxs-lookup"><span data-stu-id="4d942-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="4d942-127">**Описание** — введите содержательное описание формулы.</span><span class="sxs-lookup"><span data-stu-id="4d942-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="4d942-128">Это значение доступно в контекстном меню формулы при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4d942-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="4d942-129">**Имя пользователя** — введите имя пользователя, которому будут предоставлены права администратора.</span><span class="sxs-lookup"><span data-stu-id="4d942-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="4d942-130">**Пароль** — введите или выберите из раскрывающегося списка значение, связанное с секретом (паролем), которое будет применяться для указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="4d942-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="4d942-131">Дополнительные сведения о секретах см. в статье [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/) (Azure DevTest Labs: личное хранилище секретов).</span><span class="sxs-lookup"><span data-stu-id="4d942-131">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="4d942-132">**Virtual machine disk type** (Тип диска виртуальной машины) — выберите тип диска, HDD (жесткий диск) или SSD (твердотельный накопитель), чтобы указать тип диска хранилища, разрешенный для виртуальных машин, которые подготавливаются с помощью этого базового образа.</span><span class="sxs-lookup"><span data-stu-id="4d942-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="4d942-133">**Размер виртуальной машины** — выберите один из стандартных пунктов, указывающих количество ядер процессора, объем ОЗУ и размер жесткого диска для создаваемой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4d942-133">** Virtual machine size** - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="4d942-134">**Артефакты** — щелкните, чтобы открыть колонку **Add artifacts** (Добавление артефактов), где можно выбрать и настроить артефакты, которые нужно добавить в базовый образ.</span><span class="sxs-lookup"><span data-stu-id="4d942-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="4d942-135">Дополнительные сведения об артефактах см. в статье [Управление артефактами виртуальной машины в Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="4d942-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="4d942-136">**Дополнительные параметры** — щелкните, чтобы открыть колонку **Advanced** (Дополнительно), в которой можно настроить следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="4d942-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="4d942-137">**Виртуальная сеть** — укажите нужную виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="4d942-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="4d942-138">**Подсеть** — укажите нужную подсеть.</span><span class="sxs-lookup"><span data-stu-id="4d942-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="4d942-139">**Настройка IP-адреса** — укажите, какие IP-адреса необходимо использовать (общедоступные, частные или общие).</span><span class="sxs-lookup"><span data-stu-id="4d942-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="4d942-140">Дополнительные сведения см. в статье [Общие IP-адреса в Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="4d942-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="4d942-141">**Make this machine claimable** (Разрешить запрашивать эту виртуальную машину) — этот параметр означает, что при создании виртуальной машины права владения не будут назначаться.</span><span class="sxs-lookup"><span data-stu-id="4d942-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="4d942-142">Вместо этого пользователи лаборатории смогут становиться владельцами этой виртуальной машины ("запрашивать" ее) в колонке лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4d942-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="4d942-143">**Образ** — в этом поле приводится имя базового образа, выбранного в предыдущей колонке.</span><span class="sxs-lookup"><span data-stu-id="4d942-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Создание формулы](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="4d942-145">Щелкните **Создать** , чтобы создать формулу.</span><span class="sxs-lookup"><span data-stu-id="4d942-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="4d942-146">Когда формула создана, она отображается в колонке **Formulas** (Формулы).</span><span class="sxs-lookup"><span data-stu-id="4d942-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="4d942-147">Создание формулы на основе виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="4d942-147">Create a formula from a VM</span></span>
<span data-ttu-id="4d942-148">Ниже приводятся пошаговые инструкции по созданию формулы на основе существующей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4d942-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="4d942-149">Для создания формулы на основе виртуальной машины необходимо, чтобы эта виртуальная машина была создана после 30 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="4d942-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="4d942-150">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4d942-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="4d942-151">Щелкните **Больше служб**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="4d942-151">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="4d942-152">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="4d942-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="4d942-153">В колонке **Обзор** выберите виртуальную машину, на основе которой будет создана формула.</span><span class="sxs-lookup"><span data-stu-id="4d942-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![Лабораторные виртуальные машины](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="4d942-155">В колонке виртуальной машины выберите **Create formula (reusable base)**(Создать формулу (базовый образ, используемый повторно)).</span><span class="sxs-lookup"><span data-stu-id="4d942-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Создание формулы](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="4d942-157">В колонке **Создать формулу** введите **имя** и **описание** новой формулы в соответствующих полях.</span><span class="sxs-lookup"><span data-stu-id="4d942-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Колонка "Create formula" (Создание формулы)](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="4d942-159">Нажмите кнопку **ОК** , чтобы создать формулу.</span><span class="sxs-lookup"><span data-stu-id="4d942-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="4d942-160">Изменение формулы</span><span class="sxs-lookup"><span data-stu-id="4d942-160">Modify a formula</span></span>
<span data-ttu-id="4d942-161">Чтобы изменить формулу, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4d942-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="4d942-162">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4d942-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="4d942-163">Щелкните **Больше служб**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="4d942-163">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="4d942-164">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="4d942-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="4d942-165">В колонке лаборатории выберите **Formulas (reusable bases)**(Формулы (базовые образы, используемые повторно)).</span><span class="sxs-lookup"><span data-stu-id="4d942-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Меню формулы](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="4d942-167">В колонке **Lab formulas** (Формулы лаборатории) выберите формулу, которую нужно изменить.</span><span class="sxs-lookup"><span data-stu-id="4d942-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="4d942-168">В колонке **Update formula** (Обновление формулы) внесите необходимые изменения и щелкните **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="4d942-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="4d942-169">Удаление формулы</span><span class="sxs-lookup"><span data-stu-id="4d942-169">Delete a formula</span></span>
<span data-ttu-id="4d942-170">Чтобы удалить формулу, выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="4d942-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="4d942-171">Войдите на [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="4d942-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="4d942-172">Щелкните **Больше служб**, а затем выберите в списке **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="4d942-172">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="4d942-173">Из списка лабораторий выберите нужную лабораторию.</span><span class="sxs-lookup"><span data-stu-id="4d942-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="4d942-174">В колонке **Параметры** лаборатории выберите **Формулы**.</span><span class="sxs-lookup"><span data-stu-id="4d942-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Меню формулы](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="4d942-176">В колонке **Lab formulas** (Формулы лаборатории) щелкните многоточие справа от формулы, которую нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="4d942-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![Меню формулы](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="4d942-178">В контекстном меню формулы выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="4d942-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![Контекстное меню формулы](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="4d942-180">В диалоговом окне подтверждения удаления нажмите кнопку **Да** .</span><span class="sxs-lookup"><span data-stu-id="4d942-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="4d942-181">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="4d942-181">Related blog posts</span></span>
* [<span data-ttu-id="4d942-182">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="4d942-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="4d942-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d942-183">Next steps</span></span>
<span data-ttu-id="4d942-184">После создания формулы, которая служит для создания виртуальных машин, можно [добавить виртуальную машину в лабораторию](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="4d942-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

