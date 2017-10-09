---
title: "aaaUse Azure DevTest Labs для разработчиков | Документы Microsoft"
description: "Узнайте, как toouse Azure DevTest Labs для сценариев разработки."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="8c3e1-103">Использование Azure DevTest Labs для разработчиков</span><span class="sxs-lookup"><span data-stu-id="8c3e1-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="8c3e1-104">Azure DevTest Labs может быть используется tooimplement множество ключевых сценариев, но одна из основных сценариев hello заключаются в использовании компьютеров разработчиков toohost DevTest Labs для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-104">Azure DevTest Labs can be used tooimplement many key scenarios, but one of hello primary scenarios involves using DevTest Labs toohost development machines for developers.</span></span> <span data-ttu-id="8c3e1-105">В этом сценарии DevTest Labs предоставляет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="8c3e1-106">разработчики могут быстро подготовить виртуальные машины разработки по требованию;</span><span class="sxs-lookup"><span data-stu-id="8c3e1-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="8c3e1-107">разработчики могут в любое время легко настроить виртуальные машины разработки;</span><span class="sxs-lookup"><span data-stu-id="8c3e1-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="8c3e1-108">администраторы могут контролировать затраты, следя за тем, чтобы:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="8c3e1-109">разработчикам не выделялось больше виртуальных машин, чем требуется для разработки;</span><span class="sxs-lookup"><span data-stu-id="8c3e1-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="8c3e1-110">виртуальные машины отключались, если они не используются.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-110">VMs are shut down when not in use.</span></span> 

![Использование DevTest Labs для обучения](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="8c3e1-112">В этой статье вы узнаете о различных компонентов Azure DevTest Labs, можно использовать toomeet требования для разработки и hello подробное описание действий, которые необходимо выполнить tooset лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-112">In this article, you learn about various Azure DevTest Labs features that can be used toomeet developer requirements and hello detailed steps that you can follow tooset up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="8c3e1-113">Реализация сред разработки при помощи Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8c3e1-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="8c3e1-114">**Создание лаборатории hello**</span><span class="sxs-lookup"><span data-stu-id="8c3e1-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="8c3e1-115">Практические работы ― это hello, начальной точкой в Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="8c3e1-116">После создания лабораторной среде можно выполнять задачи, такие как добавление лаборатории toohello пользователям (разработчикам), параметр политики toocontrol затрат, определение образов виртуальных Машин, которые можно быстро создать и многое другое.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-116">Once you create a lab, you can perform tasks such as adding users (developers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="8c3e1-117">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="8c3e1-118">Задача</span><span class="sxs-lookup"><span data-stu-id="8c3e1-118">Task</span></span> | <span data-ttu-id="8c3e1-119">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8c3e1-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="8c3e1-120">Создание лаборатории в лаборатории для разработки и тестирования Azure</span><span class="sxs-lookup"><span data-stu-id="8c3e1-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="8c3e1-121">Узнайте, как toocreate a лаборатории в Azure DevTest Labs в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="8c3e1-122">**Создание виртуальных машин за считанные минуты с помощью пользовательских образов и готовых образов из Marketplace**</span><span class="sxs-lookup"><span data-stu-id="8c3e1-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="8c3e1-123">Можно выбрать готовых образов из разнообразных изображения в hello Azure Marketplace и сделать их доступными в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="8c3e1-124">Если готовых образов hello не соответствует требованиям, можно создать пользовательский образ путем создания лаборатории виртуальной Машины, используя готовые образ из Azure Marketplace, установка всех hello необходимого программного обеспечения и сохранение hello виртуальной Машины в качестве пользовательского образа в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="8c3e1-125">При использовании пользовательских образов, рассмотрите возможность использования toocreate фабрики образа и распространение изображений.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="8c3e1-126">Фабрика образов — это решение "конфигурация как код", которое регулярно автоматически создает и распространяет настроенные образы.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="8c3e1-127">Это toomanually время, необходимое hello сохраняет настройки системы hello, после создания виртуальной Машины с hello базовая ОС.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="8c3e1-128">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="8c3e1-129">Задача</span><span class="sxs-lookup"><span data-stu-id="8c3e1-129">Task</span></span> | <span data-ttu-id="8c3e1-130">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8c3e1-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="8c3e1-131">Настройка образов Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8c3e1-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="8c3e1-132">Дополнительные сведения о белом списке образы Azure Marketplace, чтобы сделать доступными для выбора только hello изображения, предназначенные для разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello developers.</span></span>|
   | [<span data-ttu-id="8c3e1-133">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="8c3e1-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="8c3e1-134">Создайте пользовательский образ по предварительной установке hello программное обеспечение, чтобы разработчики могут быстро создавать ВМ с помощью пользовательского образа hello.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-134">Create a custom image by pre-installing hello software you need so that developers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="8c3e1-135">Дополнительные сведения о фабрике образов</span><span class="sxs-lookup"><span data-stu-id="8c3e1-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="8c3e1-136">Просмотрите видео, которое описывает способ tooset Настройка и использование фабрику изображения.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="8c3e1-137">**Создание многократно используемых шаблонов для компьютеров разработки**</span><span class="sxs-lookup"><span data-stu-id="8c3e1-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="8c3e1-138">Формулы в Azure DevTest Labs представляет собой список значений свойства по умолчанию используемых toocreate виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="8c3e1-139">Можно создать формулу в лаборатории hello, выбирая изображение, размер виртуальной Машины (сочетание ЦП и ОЗУ) и виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="8c3e1-140">Каждый разработчик может видеть hello формулы в лаборатории hello и использовать ее toocreate виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-140">Each developer can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="8c3e1-141">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="8c3e1-142">Задача</span><span class="sxs-lookup"><span data-stu-id="8c3e1-142">Task</span></span> | <span data-ttu-id="8c3e1-143">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8c3e1-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="8c3e1-144">Управление toocreate формулы DevTest Labs виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="8c3e1-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="8c3e1-145">Как создать формулу, выбрав образ, размер виртуальной машины (сочетание ЦП и ОЗУ) и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="8c3e1-146">**Создать настройку виртуальной Машины гибкие артефакты tooenable**</span><span class="sxs-lookup"><span data-stu-id="8c3e1-146">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="8c3e1-147">Артефакты, используемые toodeploy и настройки приложения после подготовки виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-147">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="8c3e1-148">Артефактами могут быть:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-148">Artifacts can be:</span></span>

   - <span data-ttu-id="8c3e1-149">Средства, которые должны tooinstall на hello виртуальной Машины — например агенты, Fiddler и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-149">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="8c3e1-150">Действия, которые должны toorun на hello виртуальной Машины — например клонированием репозитория.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-150">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="8c3e1-151">Приложения, которые должны tootest.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-151">Applications that you want tootest.</span></span>

   <span data-ttu-id="8c3e1-152">Многие артефакты уже встроены.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="8c3e1-153">Если для определенных целей вам нужны дополнительные настройки, можно создать пользовательские артефакты.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="8c3e1-154">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-154">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="8c3e1-155">Задача</span><span class="sxs-lookup"><span data-stu-id="8c3e1-155">Task</span></span> | <span data-ttu-id="8c3e1-156">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8c3e1-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="8c3e1-157">Создание пользовательских артефактов для виртуальной машины DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8c3e1-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="8c3e1-158">Создайте собственные пользовательские артефакты для hello виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-158">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="8c3e1-159">Добавление репозитория Git toostore пользовательские артефакты и шаблоны Azure Resource Manager для использования в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8c3e1-159">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="8c3e1-160">Узнайте, как toostore вашей пользовательской артефактов в собственный закрытый репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-160">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="8c3e1-161">**Контроль расходов**</span><span class="sxs-lookup"><span data-stu-id="8c3e1-161">**Control costs**</span></span>
   
    <span data-ttu-id="8c3e1-162">Azure DevTest Labs позволяет tooset политику в hello лаборатории toospecify hello максимальное число виртуальных машин, которые могут быть созданы разработчиком в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-162">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a developer in hello lab.</span></span> 
   
    <span data-ttu-id="8c3e1-163">Если команда разработчиков имеет набор график работы и вы хотите toostop все виртуальные машины hello в определенное время дня hello и автоматически перезапустить их hello следующий день, это легко сделать, политиками параметр автоматического завершения работы и автозапуска в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-163">If your developer team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="8c3e1-164">Наконец при разработке приложений можно удалить все виртуальные машины hello за один раз, выполнив один сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-164">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="8c3e1-165">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-165">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="8c3e1-166">Задача</span><span class="sxs-lookup"><span data-stu-id="8c3e1-166">Task</span></span> | <span data-ttu-id="8c3e1-167">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8c3e1-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="8c3e1-168">Определение политик лаборатории</span><span class="sxs-lookup"><span data-stu-id="8c3e1-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="8c3e1-169">Контролировать стоимость путем создания политик в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-169">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="8c3e1-170">Удалить все hello лаборатории виртуальных машин с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c3e1-170">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="8c3e1-171">Удалите все hello labs за одну операцию, после завершения разработки.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-171">Delete all hello labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="8c3e1-172">**Добавить tooa виртуальной сети виртуальной Машины**</span><span class="sxs-lookup"><span data-stu-id="8c3e1-172">**Add a virtual network tooa VM**</span></span> 
   
    <span data-ttu-id="8c3e1-173">При каждом создании лаборатории служба DevTest Labs создает новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="8c3e1-174">Если вы настроили собственную виртуальную сеть — например, с помощью ExpressRoute или через виртуальную Частную сеть для — можно добавить параметры виртуальной сети этой виртуальной сети лаборатории tooyour, чтобы оно было доступно при создании виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="8c3e1-175">Кроме того является объединение домена Azure Active Directory артефакта доступны, будет присоединить к домену tooa виртуальной Машины, при создании виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="8c3e1-176">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-176">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="8c3e1-177">Задача</span><span class="sxs-lookup"><span data-stu-id="8c3e1-177">Task</span></span> | <span data-ttu-id="8c3e1-178">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8c3e1-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="8c3e1-179">Настройка виртуальной сети в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8c3e1-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="8c3e1-180">Узнайте, как tooconfigure виртуальной сети в Azure DevTest Labs, используя hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-180">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="8c3e1-181">**Предоставить каждый разработчик hello лаборатории**</span><span class="sxs-lookup"><span data-stu-id="8c3e1-181">**Share hello lab with each developer**</span></span>
   
    <span data-ttu-id="8c3e1-182">Разработчики могут напрямую подключаться к лаборатории, используя предоставленную им ссылку.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="8c3e1-183">Даже не toohave учетная запись Azure, при условии, что они имеют [учетную запись Майкрософт](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="8c3e1-183">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="8c3e1-184">Разработчики не видят виртуальные машины, созданные другими разработчиками.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="8c3e1-185">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="8c3e1-186">Задача</span><span class="sxs-lookup"><span data-stu-id="8c3e1-186">Task</span></span> | <span data-ttu-id="8c3e1-187">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8c3e1-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="8c3e1-188">Добавьте лаборатории tooa разработчика в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8c3e1-188">Add a developer tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="8c3e1-189">Используйте hello Azure tooadd портала разработчиков tooyour лаборатории.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-189">Use hello Azure portal tooadd developers tooyour lab.</span></span>|
   | [<span data-ttu-id="8c3e1-190">Добавить лаборатории toohello разработчиков с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c3e1-190">Add developers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="8c3e1-191">С помощью добавления разработчики tooyour лаборатории tooautomate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-191">Use PowerShell tooautomate adding developers tooyour lab.</span></span> |
   | [<span data-ttu-id="8c3e1-192">Получение лабораторной toohello ссылку</span><span class="sxs-lookup"><span data-stu-id="8c3e1-192">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="8c3e1-193">Как разработчики могут напрямую подключаться к лаборатории по гиперссылке.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="8c3e1-194">**Автоматическое создание лабораторий для дополнительных команд**</span><span class="sxs-lookup"><span data-stu-id="8c3e1-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="8c3e1-195">Можно автоматизировать создание лаборатории, включая пользовательские настройки, путем создания шаблона диспетчера ресурсов и использования идентичных labs toocreate снова и снова.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="8c3e1-196">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="8c3e1-196">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="8c3e1-197">Задача</span><span class="sxs-lookup"><span data-stu-id="8c3e1-197">Task</span></span> | <span data-ttu-id="8c3e1-198">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8c3e1-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="8c3e1-199">Создание лаборатории с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8c3e1-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="8c3e1-200">Как создать лабораторию в Azure DevTest Labs с помощью шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8c3e1-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

