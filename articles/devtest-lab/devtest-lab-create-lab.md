---
title: "aaaCreate лаборатории в Azure DevTest Labs | Документы Microsoft"
description: "Создание лаборатории в Azure DevTest Labs для виртуальных машин"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/30/2017
ms.author: tarcher
ms.openlocfilehash: 2ec5498f10e0cc06a196a71e319e340937abb1a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="a4cf2-103">Создание лаборатории в лаборатории для разработки и тестирования Azure</span><span class="sxs-lookup"><span data-stu-id="a4cf2-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="a4cf2-104">Лаборатории в Azure DevTest Labs — hello инфраструктурой, которая содержит группы ресурсов, например виртуальных машин (ВМ), которые позволяют лучше управлять этими ресурсами, указывая, ограничения и квоты.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-104">A lab in Azure DevTest Labs is hello infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="a4cf2-105">В этой статье рассматриваются hello процесс создания лаборатории, используя hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-105">This article walks you through hello process of creating a lab using hello Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4cf2-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a4cf2-106">Prerequisites</span></span>
<span data-ttu-id="a4cf2-107">toocreate лабораторной среде, необходимо:</span><span class="sxs-lookup"><span data-stu-id="a4cf2-107">toocreate a lab, you need:</span></span>

* <span data-ttu-id="a4cf2-108">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-108">An Azure subscription.</span></span> <span data-ttu-id="a4cf2-109">toolearn о варианты приобретения Azure, в разделе [как toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) или [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a4cf2-109">toolearn about Azure purchase options, see [How toobuy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="a4cf2-110">Необходимо быть владельцем hello hello подписки toocreate hello лаборатории.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-110">You must be hello owner of hello subscription toocreate hello lab.</span></span>

## <a name="steps-toocreate-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="a4cf2-111">Действия toocreate лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a4cf2-111">Steps toocreate a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="a4cf2-112">Привет, следующие шаги показывают, как toouse hello Azure портала toocreate лаборатории в Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-112">hello following steps illustrate how toouse hello Azure portal toocreate a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="a4cf2-113">Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="a4cf2-113">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="a4cf2-114">Hello в главном меню в левой части hello, выберите **более служб** (внизу hello hello список).</span><span class="sxs-lookup"><span data-stu-id="a4cf2-114">From hello main menu on hello left side, select **More Services** (at hello bottom of hello list).</span></span>

    ![Пункт меню "Больше служб"](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="a4cf2-116">Из списка доступных служб hello **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-116">From hello list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="a4cf2-117">На hello **DevTest Labs** колонке выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-117">On hello **DevTest Labs** blade, select **Add**.</span></span>
   
    ![Добавление лаборатории](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="a4cf2-119">На hello **создание лаборатории, DevTest** колонки:</span><span class="sxs-lookup"><span data-stu-id="a4cf2-119">On hello **Create a DevTest Lab** blade:</span></span>
   
    1. <span data-ttu-id="a4cf2-120">Введите **имени лаборатории** для новой лабораторной hello.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-120">Enter a **Lab Name** for hello new lab.</span></span>
    2. <span data-ttu-id="a4cf2-121">Выберите hello **подписки** tooassociate hello лаборатории.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-121">Select hello **Subscription** tooassociate with hello lab.</span></span>
    3. <span data-ttu-id="a4cf2-122">Выберите **расположение** в какой лаборатории toostore hello.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-122">Select a **Location** in which toostore hello lab.</span></span>
    4. <span data-ttu-id="a4cf2-123">Выберите **автоматическое завершение работы** toospecify tooenable - и определения параметров hello - hello автоматическое завершение работы всех лаборатории hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-123">Select **Auto-shutdown** toospecify if you want tooenable - and define hello parameters for - hello automatic shutting down of all hello lab's VMs.</span></span> <span data-ttu-id="a4cf2-124">Hello автоматического завершения работы компонент является главным образом снизить издержки при котором можно указать, когда требуется hello ВМ tooautomatically завершить работу.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-124">hello auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want hello VM tooautomatically be shut down.</span></span> <span data-ttu-id="a4cf2-125">Параметры автоматического завершения работы можно изменить после создания лаборатории hello hello выполните действия, описанные в статье hello [управления всеми политиками для лаборатории в Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="a4cf2-125">You can change auto-shutdown settings after creating hello lab by following hello steps outlined in hello article, [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    5. <span data-ttu-id="a4cf2-126">Выберите **tooDashboard ПИН-код** Если нужно упростить hello tooappear лаборатории на панели мониторинга портала hello.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-126">Select **Pin tooDashboard** if you want a shortcut of hello lab tooappear on hello portal dashboard.</span></span>
    6. <span data-ttu-id="a4cf2-127">Выберите **возможности автоматизации** tooget шаблонов диспетчера ресурсов Azure для автоматизации настройки.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-127">Select **Automation options** tooget Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="a4cf2-128">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-128">Select **Create**.</span></span> <span data-ttu-id="a4cf2-129">После выбора **создать**, hello **DevTest Labs** отображает колонку.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-129">After selecting **Create**, hello **DevTest Labs** blade displays.</span></span> <span data-ttu-id="a4cf2-130">Можно отслеживать состояние hello процесса создания лаборатории hello посмотрите hello **уведомления** области.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-130">You can monitor hello status of hello lab creation process by watching hello **Notifications** area.</span></span> <span data-ttu-id="a4cf2-131">После завершения обновления hello страницы toosee hello новые лаборатории в списке hello лабораторий.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-131">Once completed, refresh hello page toosee hello newly created lab in hello list of labs.</span></span>  
    
    ![Колонка создания лаборатории](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="a4cf2-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a4cf2-133">Next steps</span></span>
<span data-ttu-id="a4cf2-134">После создания лаборатории, ниже приведены некоторые Далее tooconsider действия.</span><span class="sxs-lookup"><span data-stu-id="a4cf2-134">Once you've created your lab, here are some next steps tooconsider:</span></span>

* <span data-ttu-id="a4cf2-135">[Безопасный доступ tooa лаборатории](devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="a4cf2-135">[Secure access tooa lab](devtest-lab-add-devtest-user.md).</span></span>
* <span data-ttu-id="a4cf2-136">[Определение политик лаборатории](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a4cf2-136">[Set lab policies](devtest-lab-set-lab-policy.md).</span></span>
* <span data-ttu-id="a4cf2-137">[Создание шаблона лаборатории](devtest-lab-create-template.md).</span><span class="sxs-lookup"><span data-stu-id="a4cf2-137">[Create a lab template](devtest-lab-create-template.md).</span></span>
* <span data-ttu-id="a4cf2-138">[Создание пользовательских артефактов для виртуальных машин](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="a4cf2-138">[Create custom artifacts for your VMs](devtest-lab-artifact-author.md).</span></span>
* <span data-ttu-id="a4cf2-139">[Добавить виртуальную Машину с артефакты лаборатории tooa](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span><span class="sxs-lookup"><span data-stu-id="a4cf2-139">[Add a VM with artifacts tooa lab](https://azure.microsoft.com/resources/videos/how-to-create-vms-with-artifacts-in-a-devtest-lab/).</span></span>

