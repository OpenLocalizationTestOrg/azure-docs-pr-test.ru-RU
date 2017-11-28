---
title: "aaaAdd claimable лаборатории tooa ВМ в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как tooadd лаборатории tooa claimable виртуальной машины в Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: fe6385ae2e59b9636b82aec250dc3a1f8a40ba5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="8bd62-103">Добавить claimable лаборатории tooa ВМ в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8bd62-103">Add a claimable VM tooa lab in Azure DevTest Labs</span></span>
<span data-ttu-id="8bd62-104">Добавить claimable лаборатории tooa ВМ в аналогичные toohow способом вы [Стандартная виртуальная машина добавляется](devtest-lab-add-vm.md) — *базового* , либо [пользовательского образа](devtest-lab-create-template.md), [формула](devtest-lab-manage-formulas.md), или [образа Marketplace](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="8bd62-104">You add a claimable VM tooa lab in a similar manner toohow you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="8bd62-105">Этот учебник поможет выполнить с помощью hello Azure портала tooadd claimable лаборатории tooa ВМ в DevTest Labs и показывает процесс hello hello tooclaim ВМ подписан пользователь.</span><span class="sxs-lookup"><span data-stu-id="8bd62-105">This tutorial walks you through using hello Azure portal tooadd a claimable VM tooa lab in DevTest Labs, and shows hello process a user follows tooclaim hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="8bd62-106">При развертывании виртуальных машин лаборатории через [шаблоны Azure Resource Manager](devtest-lab-create-environment-from-arm.md), можно создать claimable виртуальных машин, установка hello **allowClaim** tootrue свойства в разделе "Свойства" hello.</span><span class="sxs-lookup"><span data-stu-id="8bd62-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting hello **allowClaim** property tootrue in hello properties section.</span></span>
>
>

## <a name="steps-tooadd-a-claimable-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="8bd62-107">Tooadd действия claimable лаборатории tooa ВМ в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8bd62-107">Steps tooadd a claimable VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="8bd62-108">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8bd62-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="8bd62-109">Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="8bd62-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="8bd62-110">Выберите из списка hello лабораториям hello лаборатории, необходимо toocreate hello claimable виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8bd62-110">From hello list of labs, select hello lab in which you want toocreate hello claimable VM.</span></span>  
1. <span data-ttu-id="8bd62-111">В лаборатории hello **Обзор** колонке выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="8bd62-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Кнопка добавления виртуальной машины](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="8bd62-113">На hello **выберите базовый** колонке выберите база для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8bd62-113">On hello **Choose a base** blade, select a base for hello VM.</span></span>
1. <span data-ttu-id="8bd62-114">На hello **виртуальной машины** колонки, введите имя для новой виртуальной машины hello в hello **имя виртуальной машины** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="8bd62-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Колонка виртуальной машины лаборатории](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="8bd62-116">Введите **имя пользователя** , которой предоставляются права администратора на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="8bd62-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="8bd62-117">Если вы хотите toouse пароль хранится в вашей [секретное хранилище](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store)выберите **сохраненного секрета**и укажите значение ключа, которое соответствует tooyour секрет (пароль).</span><span class="sxs-lookup"><span data-stu-id="8bd62-117">If you want toouse a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds tooyour secret (password).</span></span> <span data-ttu-id="8bd62-118">В противном случае введите пароль в hello текстовое поле с меткой **введите значение**.</span><span class="sxs-lookup"><span data-stu-id="8bd62-118">Otherwise, enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="8bd62-119">Hello **тип диска виртуальной машины** определяет, какой тип диска хранилища допустим для hello виртуальных машин в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="8bd62-119">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="8bd62-120">Выберите **размер виртуальной машины** и выберите один из hello предопределенные элементы, определяющие hello процессорных ядер, объем оперативной памяти и размер жесткого диска hello toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8bd62-120">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="8bd62-121">Выберите **артефакты** из списка hello артефактов, выберите и настройте hello артефакты, что требуется tooadd toohello базового образа.</span><span class="sxs-lookup"><span data-stu-id="8bd62-121">Select **Artifacts** and from hello list of artifacts, select and configure hello artifacts that you want tooadd toohello base image.</span></span> <span data-ttu-id="8bd62-122">Если вы будете новый Labs tooDevTest или настройка артефакты, см. toohello [Добавление существующих артефактов tooa ВМ](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) статьи, а затем вернитесь сюда, после завершения.</span><span class="sxs-lookup"><span data-stu-id="8bd62-122">If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="8bd62-123">Выберите **Дополнительные параметры** сеть виртуальной Машины hello tooconfigure параметры и срок действия параметров.</span><span class="sxs-lookup"><span data-stu-id="8bd62-123">Select **Advanced settings** tooconfigure hello VM's network options and expiration options.</span></span> <span data-ttu-id="8bd62-124">В разделе **утверждения параметры**, выберите **Да** машины hello toomake claimable.</span><span class="sxs-lookup"><span data-stu-id="8bd62-124">Under **Claim options**, choose **Yes** toomake hello machine claimable.</span></span>

  ![Выберите toomake hello claimable виртуальной Машины.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="8bd62-126">Если требуется tooview или копировать hello шаблона диспетчера ресурсов Azure, см. toohello [шаблона Azure Resource Manager, Сохранить](devtest-lab-add-vm.md#save-azure-resource-manager-template) раздела и после завершения вернитесь сюда.</span><span class="sxs-lookup"><span data-stu-id="8bd62-126">If you want tooview or copy hello Azure Resource Manager template, refer toohello [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="8bd62-127">Выберите **создать** tooadd hello указан лаборатории toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8bd62-127">Select **Create** tooadd hello specified VM toohello lab.</span></span>
1. <span data-ttu-id="8bd62-128">Hello лаборатории колонке hello состояния создания виртуальной Машины hello - сначала отображает как **создание**, затем по мере **под управлением** после hello, виртуальная машина запущена.</span><span class="sxs-lookup"><span data-stu-id="8bd62-128">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="8bd62-129">Использование запрашиваемой виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="8bd62-129">Using a claimable VM</span></span>

<span data-ttu-id="8bd62-130">Пользователь может утверждений все виртуальные Машины, из списка «Claimable виртуальные машины» hello, выполнив одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="8bd62-130">A user can claim any VM from hello list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="8bd62-131">Из списка «Claimable виртуальные машины» hello нижней части колонки Обзор лаборатории hello hello, щелкните правой кнопкой мыши на одном из hello виртуальных машин в списке hello и выберите **утверждения машины**.</span><span class="sxs-lookup"><span data-stu-id="8bd62-131">From hello list of "Claimable virtual machines" at hello bottom of hello lab's Overview blade, right-click on one of hello VMs in hello list and choose **Claim machine**.</span></span>

 ![Запрос определенной запрашиваемой виртуальной машины](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="8bd62-133">Вверху hello hello **Обзор** колонке выберите **утверждений любой**.</span><span class="sxs-lookup"><span data-stu-id="8bd62-133">At hello top of hello **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="8bd62-134">Случайное виртуальной машине назначается из списка hello claimable виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8bd62-134">A random virtual machine is assigned from hello list of claimable VMs.</span></span>

 ![Запрос любой запрашиваемой виртуальной машины](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="8bd62-136">Выбранная пользователем запрашиваемая виртуальная машина перемещается в список раздела "My virtual machines" (Мои виртуальные машины). Ее не могут повторно запрашивать другие пользователи.</span><span class="sxs-lookup"><span data-stu-id="8bd62-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bd62-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8bd62-137">Next steps</span></span>
* <span data-ttu-id="8bd62-138">Один раз hello, виртуальная машина будет создана, можно подключиться toohello виртуальной Машины, выбрав **Connect** на колонки hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8bd62-138">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="8bd62-139">Просмотр hello [DevTest Labs Azure Resource Manager QuickStart коллекции шаблонов](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="8bd62-139">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>
