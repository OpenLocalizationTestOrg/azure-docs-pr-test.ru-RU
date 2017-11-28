---
title: "aaaManage формулы в toocreate Azure DevTest Labs виртуальные машины | Документы Microsoft"
description: "Узнайте, как tooupdate и удаление формулы Azure DevTest Labs"
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
ms.openlocfilehash: 855debe46f3b70cc45ea5d55869663b64e225124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="8deab-103">Управление формулами Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8deab-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="8deab-104">В этой статье показано, как toocreate формулы из базового (пользовательского образа, образа Marketplace или другие формулы) или существующей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8deab-104">This article illustrates how toocreate a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="8deab-105">В этой статье также объясняется, как управлять существующими формулами.</span><span class="sxs-lookup"><span data-stu-id="8deab-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="8deab-106">Создание формулы</span><span class="sxs-lookup"><span data-stu-id="8deab-106">Create a formula</span></span>
<span data-ttu-id="8deab-107">Любой пользователь с DevTest Labs *пользователей* разрешений является могут toocreate виртуальные машины с помощью формулы в качестве базы.</span><span class="sxs-lookup"><span data-stu-id="8deab-107">Anyone with DevTest Labs *Users* permissions is able toocreate VMs using a formula as a base.</span></span> <span data-ttu-id="8deab-108">Существует два способа toocreate формулы:</span><span class="sxs-lookup"><span data-stu-id="8deab-108">There are two ways toocreate formulas:</span></span> 

* <span data-ttu-id="8deab-109">У базового - используйте toodefine все характеристики hello hello формулы.</span><span class="sxs-lookup"><span data-stu-id="8deab-109">From a base - Use when you want toodefine all hello characteristics of hello formula.</span></span>
* <span data-ttu-id="8deab-110">Из существующего лаборатории виртуальной Машины — используйте оператор toocreate формулы, основанные на параметрах hello существующей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8deab-110">From an existing lab VM - Use when you want toocreate a formula based on hello settings of an existing VM.</span></span>

<span data-ttu-id="8deab-111">Дополнительные сведения о добавлении пользователей и разрешений см. в статье [Добавление владельцев и пользователей в Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="8deab-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="8deab-112">Создание формулы из базового образа</span><span class="sxs-lookup"><span data-stu-id="8deab-112">Create a formula from a base</span></span>
<span data-ttu-id="8deab-113">Hello следующие шаги описывают hello процесс создания формулы из образа, образа Marketplace или другие формулы.</span><span class="sxs-lookup"><span data-stu-id="8deab-113">hello following steps guide you through hello process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="8deab-114">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8deab-114">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="8deab-115">Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="8deab-115">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>

3. <span data-ttu-id="8deab-116">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8deab-116">From hello list of labs, select hello desired lab.</span></span>  

4. <span data-ttu-id="8deab-117">В колонке hello лаборатории выберите **формулы (многократно используемых базовых классов)**.</span><span class="sxs-lookup"><span data-stu-id="8deab-117">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Меню формулы](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="8deab-119">На hello **формулы** колонке выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="8deab-119">On hello **Formulas** blade, select **+ Add**.</span></span>
   
    ![Добавление формулы](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="8deab-121">На hello **выберите базовый** колонке базы выберите hello (пользовательского образа, образа Marketplace или формулу) из которого нужно toocreate hello формулы.</span><span class="sxs-lookup"><span data-stu-id="8deab-121">On hello **Choose a base** blade, select hello base (custom image, Marketplace image, or formula) from which you want toocreate hello formula.</span></span>
   
    ![Список базовых образов](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="8deab-123">На hello **создать формулу** колонке укажите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="8deab-123">On hello **Create formula** blade, specify hello following values:</span></span>
   
    * <span data-ttu-id="8deab-124">**Имя формулы** — введите имя формулы.</span><span class="sxs-lookup"><span data-stu-id="8deab-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="8deab-125">Это значение отображается в списке hello базовые образы при создании виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8deab-125">This value is displayed in hello list of base images when you create a VM.</span></span> <span data-ttu-id="8deab-126">Имя Hello проверку введите его, и если не является допустимым, сообщение указывает hello требования к именам.</span><span class="sxs-lookup"><span data-stu-id="8deab-126">hello name is validated as you type it, and if not valid, a message indicates hello requirements for a valid name.</span></span>
    * <span data-ttu-id="8deab-127">**Описание** — введите содержательное описание формулы.</span><span class="sxs-lookup"><span data-stu-id="8deab-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="8deab-128">Это значение доступно из контекстного меню hello формулу, при создании виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8deab-128">This value is available from hello formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="8deab-129">**Имя пользователя** — введите имя пользователя, которому будут предоставлены права администратора.</span><span class="sxs-lookup"><span data-stu-id="8deab-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="8deab-130">**Пароль** : Введите - или выберите из раскрывающегося списка hello - значение, связанный с hello секрет (пароль), чтобы получить toouse hello указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="8deab-130">**Password** - Enter - or select from hello dropdown - a value that is associated with hello secret (password) that you want toouse for hello specified user.</span></span> <span data-ttu-id="8deab-131">Дополнительные сведения о секреты hello. в разделе [Azure DevTest Labs: личное хранилище секретный](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="8deab-131">For more information about hello secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="8deab-132">**Тип диска виртуальной машины** — укажите либо жесткого диска (жестком диске) или в хранилище на диске тип tooindicate SSD (твердотельного накопителя) допустим для hello виртуальных машин, подготовленных с помощью этого базового образа.</span><span class="sxs-lookup"><span data-stu-id="8deab-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) tooindicate which storage disk type is allowed for hello virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="8deab-133">** Виртуальной машины размера ** — выберите один из элементов hello предопределенные hello процессорных ядер, объем оперативной памяти и размер жесткого диска hello toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8deab-133">** Virtual machine size** - Select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span> 
    * <span data-ttu-id="8deab-134">**Артефакты** -hello выберите tooopen **добавить артефакты** колонки, выберите и настройте hello артефакты, что требуется tooadd toohello базового образа.</span><span class="sxs-lookup"><span data-stu-id="8deab-134">**Artifacts** - Select tooopen hello **Add artifacts** blade, in which you select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="8deab-135">Дополнительные сведения об артефактах см. в статье [Управление артефактами виртуальной машины в Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="8deab-135">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="8deab-136">**Дополнительные параметры** -hello выберите tooopen **Дополнительно** колонки, в которой выполняется настройка hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="8deab-136">**Advanced settings** - Select tooopen hello **Advanced** blade where you configure hello following settings:</span></span>
        * <span data-ttu-id="8deab-137">**Виртуальная сеть** -указать hello нужно виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="8deab-137">**Virtual network** - Specify hello desired virtual network.</span></span>
        * <span data-ttu-id="8deab-138">**Подсети** -указать подсеть требуемого hello.</span><span class="sxs-lookup"><span data-stu-id="8deab-138">**Subnet** - Specify hello desired subnet.</span></span>    
        * <span data-ttu-id="8deab-139">**Конфигурация IP-адреса** -указать, следует hello Public, Private или общим IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="8deab-139">**IP address configuration** - Specify if you want hello Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="8deab-140">Дополнительные сведения см. в статье [Общие IP-адреса в Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="8deab-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="8deab-141">**Сделать эту машину claimable** -внесения «claimable» на машине означает, что он не будет назначено владения во время создания hello.</span><span class="sxs-lookup"><span data-stu-id="8deab-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at hello time of creation.</span></span> <span data-ttu-id="8deab-142">Вместо этого пользователи лаборатории будет машины hello может tootake владения («утверждения») в колонке hello лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8deab-142">Instead lab users will be able tootake ownership ("claim") hello machine in hello lab's blade.</span></span>     
    * <span data-ttu-id="8deab-143">**Изображение** -это поле отображает имя hello базового образа, выбранного на предыдущей колонке hello.</span><span class="sxs-lookup"><span data-stu-id="8deab-143">**Image** - This field displays name of hello base image you selected on hello previous blade.</span></span> 
     
       ![Создание формулы](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="8deab-145">Выберите **создать** toocreate hello формулы.</span><span class="sxs-lookup"><span data-stu-id="8deab-145">Select **Create** toocreate hello formula.</span></span>

9. <span data-ttu-id="8deab-146">При создании формулы hello отображается в списке hello на hello **формулы** колонку.</span><span class="sxs-lookup"><span data-stu-id="8deab-146">When hello formula has been created, it displays in hello list on hello **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="8deab-147">Создание формулы на основе виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8deab-147">Create a formula from a VM</span></span>
<span data-ttu-id="8deab-148">Hello следующие шаги описывают hello процесс создания формула, основанная на существующей виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8deab-148">hello following steps guide you through hello process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="8deab-149">toocreate формулы из виртуальной Машины hello виртуальная машина должна быть создана после 30 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="8deab-149">toocreate a formula from a VM, hello VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="8deab-150">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8deab-150">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="8deab-151">Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="8deab-151">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="8deab-152">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8deab-152">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="8deab-153">В лаборатории hello **Обзор** колонке виртуальной Машины выберите hello, с которой вы будете toocreate hello формулы.</span><span class="sxs-lookup"><span data-stu-id="8deab-153">On hello lab's **Overview** blade, select hello VM from which you wish toocreate hello formula.</span></span>
   
    ![Лабораторные виртуальные машины](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="8deab-155">В колонке hello виртуальной Машины выберите **Создание формулы (многократно используемых base)**.</span><span class="sxs-lookup"><span data-stu-id="8deab-155">On hello VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Создание формулы](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="8deab-157">На hello **создать формулу** колонке введите **имя** и **описание** для вашей новую формулу.</span><span class="sxs-lookup"><span data-stu-id="8deab-157">On hello **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Колонка "Create formula" (Создание формулы)](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="8deab-159">Выберите **ОК** toocreate hello формулы.</span><span class="sxs-lookup"><span data-stu-id="8deab-159">Select **OK** toocreate hello formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="8deab-160">Изменение формулы</span><span class="sxs-lookup"><span data-stu-id="8deab-160">Modify a formula</span></span>
<span data-ttu-id="8deab-161">toomodify формулу, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8deab-161">toomodify a formula, follow these steps:</span></span>

1. <span data-ttu-id="8deab-162">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8deab-162">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="8deab-163">Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="8deab-163">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="8deab-164">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8deab-164">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="8deab-165">В колонке hello лаборатории выберите **формулы (многократно используемых базовых классов)**.</span><span class="sxs-lookup"><span data-stu-id="8deab-165">On hello lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Меню формулы](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="8deab-167">На hello **формулы лаборатории** колонку, вы хотите toomodify формулы выберите hello.</span><span class="sxs-lookup"><span data-stu-id="8deab-167">On hello **Lab formulas** blade, select hello formula you wish toomodify.</span></span>
6. <span data-ttu-id="8deab-168">На hello **обновить формулу** , отредактируйте требуемого hello и, при необходимости выберите **обновление**.</span><span class="sxs-lookup"><span data-stu-id="8deab-168">On hello **Update formula** blade, make hello desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="8deab-169">Удаление формулы</span><span class="sxs-lookup"><span data-stu-id="8deab-169">Delete a formula</span></span>
<span data-ttu-id="8deab-170">toodelete формулу, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8deab-170">toodelete a formula, follow these steps:</span></span>

1. <span data-ttu-id="8deab-171">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8deab-171">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="8deab-172">Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="8deab-172">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="8deab-173">Выберите из списка hello лабораториям hello требуемой лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8deab-173">From hello list of labs, select hello desired lab.</span></span>  
4. <span data-ttu-id="8deab-174">В лаборатории hello **параметры** колонке выберите **формулы**.</span><span class="sxs-lookup"><span data-stu-id="8deab-174">On hello lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Меню формулы](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="8deab-176">На hello **формулы лаборатории** колонки, toohello hello выберите кнопку с многоточием справа от формулы hello нужно toodelete.</span><span class="sxs-lookup"><span data-stu-id="8deab-176">On hello **Lab formulas** blade, select hello ellipsis toohello right of hello formula you wish toodelete.</span></span>
   
    ![Меню формулы](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="8deab-178">Формула hello контекстном меню выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="8deab-178">On hello formula's context menu, select **Delete**.</span></span>
   
    ![Контекстное меню формулы](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="8deab-180">Выберите **Да** toohello диалоговое окно подтверждения удаления.</span><span class="sxs-lookup"><span data-stu-id="8deab-180">Select **Yes** toohello deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="8deab-181">Связанные записи в блогах</span><span class="sxs-lookup"><span data-stu-id="8deab-181">Related blog posts</span></span>
* [<span data-ttu-id="8deab-182">Custom images or formulas? (Пользовательские изображения или формулы?)</span><span class="sxs-lookup"><span data-stu-id="8deab-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="8deab-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8deab-183">Next steps</span></span>
<span data-ttu-id="8deab-184">После создания формулы, используемой при создании виртуальной Машины, hello следующим шагом является слишком[добавления виртуальных Машин лаборатории tooyour](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="8deab-184">Once you have created a formula for use when creating a VM, hello next step is too[add a VM tooyour lab](devtest-lab-add-vm-with-artifacts.md).</span></span>

