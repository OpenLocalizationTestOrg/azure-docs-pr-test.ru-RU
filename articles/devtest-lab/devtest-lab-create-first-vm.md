---
title: "aaaCreate первой виртуальной Машины в лабораторной среде в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как toocreate первой виртуальной машины в лабораторной среде в Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: fbc5a438-6e02-4952-b654-b8fa7322ae5f
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/24/2017
ms.author: tarcher
ms.openlocfilehash: 4c3257efca9be6fdd190eaac1db731464e07fcfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="a1a2f-103">Создание первой виртуальной машины в лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a1a2f-103">Create your first VM in a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="a1a2f-104">При первоначальном доступ к DevTest Labs toocreate первой ВМ, скорее всего этого с помощью предварительно загруженных [образа marketplace базовый](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="a1a2f-104">When you initially access DevTest Labs and want toocreate your first VM, you will likely do so using a pre-loaded [base marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="a1a2f-105">Позднее вы также будете может toochoose из [пользовательского образа и формула](devtest-lab-add-vm.md) при создании дополнительных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-105">Later on, you'll also be able toochoose from a [custom image and a formula](devtest-lab-add-vm.md) when creating more VMs.</span></span> 

<span data-ttu-id="a1a2f-106">Этот учебник знакомит с помощью hello Azure портала tooadd первый tooa лаборатории для виртуальной Машины в DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-106">This tutorial walks you through using hello Azure portal tooadd your first VM tooa lab in DevTest Labs.</span></span>

## <a name="steps-tooadd-your-first-vm-tooa-lab-in-azure-devtest-labs"></a><span data-ttu-id="a1a2f-107">Шаги tooadd первый tooa лаборатории для виртуальной Машины в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a1a2f-107">Steps tooadd your first VM tooa lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="a1a2f-108">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a1a2f-108">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="a1a2f-109">Выберите **более служб**, а затем выберите **DevTest Labs** из списка hello.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-109">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
1. <span data-ttu-id="a1a2f-110">Выберите из списка hello лабораториям hello лаборатории, в которой будет toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-110">From hello list of labs, select hello lab in which you want toocreate hello VM.</span></span>  
1. <span data-ttu-id="a1a2f-111">В лаборатории hello **Обзор** колонке выберите **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-111">On hello lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Кнопка добавления виртуальной машины](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="a1a2f-113">На hello **выберите базовый** колонке выберите образа marketplace для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-113">On hello **Choose a base** blade, select a marketplace image for hello VM.</span></span>
1. <span data-ttu-id="a1a2f-114">На hello **виртуальной машины** колонки, введите имя для новой виртуальной машины hello в hello **имя виртуальной машины** текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-114">On hello **Virtual machine** blade, enter a name for hello new virtual machine in hello **Virtual machine name** text box.</span></span>

    ![Колонка виртуальной машины лаборатории](./media/devtest-lab-add-vm/devtestlab-lab-add-first-vm.png)

1. <span data-ttu-id="a1a2f-116">Введите **имя пользователя** , которой предоставляются права администратора на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-116">Enter a **User Name** that is granted administrator privileges on hello virtual machine.</span></span>  
1. <span data-ttu-id="a1a2f-117">Введите пароль в hello текстовое поле с меткой **введите значение**.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-117">Enter a password in hello text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="a1a2f-118">Hello **тип диска виртуальной машины** определяет, какой тип диска хранилища допустим для hello виртуальных машин в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-118">hello **Virtual machine disk type** determines which storage disk type is allowed for hello virtual machines in hello lab.</span></span>
1. <span data-ttu-id="a1a2f-119">Выберите **размер виртуальной машины** и выберите один из hello предопределенные элементы, определяющие hello процессорных ядер, объем оперативной памяти и размер жесткого диска hello toocreate hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-119">Select **Virtual machine size** and select one of hello predefined items that specify hello processor cores, RAM size, and hello hard drive size of hello VM toocreate.</span></span>
1. <span data-ttu-id="a1a2f-120">Выберите **артефакты** - списке hello артефактов - выберите и настройте hello артефакты, что требуется tooadd toohello базового образа.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-120">Select **Artifacts** and - from hello list of artifacts - select and configure hello artifacts that you want tooadd toohello base image.</span></span>
    <span data-ttu-id="a1a2f-121">**Примечание:** Если вы будете новый Labs tooDevTest или настройка артефакты, см. toohello [Добавление существующих артефактов tooa ВМ](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) статьи, а затем вернитесь сюда, после завершения.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-121">**Note:** If you're new tooDevTest Labs or configuring artifacts, refer toohello [Add an existing artifact tooa VM](./devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="a1a2f-122">Выберите **создать** tooadd hello указан лаборатории toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-122">Select **Create** tooadd hello specified VM toohello lab.</span></span>

   <span data-ttu-id="a1a2f-123">Hello лаборатории колонке hello состояния создания виртуальной Машины hello - сначала отображает как **создание**, затем по мере **под управлением** после hello, виртуальная машина запущена.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-123">hello lab blade displays hello status of hello VM's creation - first as **Creating**, then as **Running** after hello VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1a2f-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a1a2f-124">Next steps</span></span>
* <span data-ttu-id="a1a2f-125">Один раз hello, виртуальная машина будет создана, можно подключиться toohello виртуальной Машины, выбрав **Connect** на колонки hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-125">Once hello VM has been created, you can connect toohello VM by selecting **Connect** on hello VM's blade.</span></span>
* <span data-ttu-id="a1a2f-126">Извлечение [добавления виртуальных Машин лаборатории tooa](devtest-lab-add-vm.md) более полные сведения о добавлении последующих виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="a1a2f-126">Check out [Add a VM tooa lab](devtest-lab-add-vm.md) for more complete info about adding subsequent VMs in your lab.</span></span>
* <span data-ttu-id="a1a2f-127">Просмотр hello [коллекции шаблонов Azure Resource Manager DevTest Labs QuickStart](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span><span class="sxs-lookup"><span data-stu-id="a1a2f-127">Explore hello [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates).</span></span>
