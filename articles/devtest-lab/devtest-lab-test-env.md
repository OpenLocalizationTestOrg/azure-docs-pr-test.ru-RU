---
title: "aaaUse Azure DevTest Labs для виртуальных Машин и PaaS тестовую среду | Документы Microsoft"
description: "Узнайте, как toouse Azure DevTest Labs для виртуальных Машин и PaaS тестирования среды."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="33c77-103">Использование Azure DevTest Labs для виртуальных машин и тестовых сред PaaS</span><span class="sxs-lookup"><span data-stu-id="33c77-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="33c77-104">Tooimplement Azure DevTest Labs можно использовать многие основные сценарии, но основной сценарий предполагает использование машины toohost DevTest Labs для тест-инженеров.</span><span class="sxs-lookup"><span data-stu-id="33c77-104">You can use Azure DevTest Labs tooimplement many key scenarios, but a primary scenario involves using DevTest Labs toohost machines for testers.</span></span> 

<span data-ttu-id="33c77-105">В этом сценарии DevTest Labs предоставляет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="33c77-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="33c77-106">Тест-инженеры можно проверить последнюю версию своего приложения hello, быстро подготовки средах Windows и Linux, с помощью шаблонов для повторного использования и артефакты.</span><span class="sxs-lookup"><span data-stu-id="33c77-106">Testers can test hello latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="33c77-107">Тестировщики могут увеличить масштаб нагрузочного тестирования, развернув несколько агентов тестирования.</span><span class="sxs-lookup"><span data-stu-id="33c77-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="33c77-108">Администраторы могут контролировать затраты, следя за тем, чтобы:</span><span class="sxs-lookup"><span data-stu-id="33c77-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="33c77-109">тестировщикам не выделялось больше виртуальных машин, чем требуется для тестирования;</span><span class="sxs-lookup"><span data-stu-id="33c77-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="33c77-110">виртуальные машины отключались, если они не используются.</span><span class="sxs-lookup"><span data-stu-id="33c77-110">VMs are shut down when not in use.</span></span>

![Использование DevTest Labs для обучения](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="33c77-112">В этой статье различные требования тест-инженер Azure DevTest Labs используемых функций toomeet и hello tooset toofollow подробное описание действий лаборатории.</span><span class="sxs-lookup"><span data-stu-id="33c77-112">In this article, you learn about various Azure DevTest Labs features used toomeet tester requirements and hello detailed steps toofollow tooset up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="33c77-113">Реализация тестовых сред с помощью Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="33c77-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="33c77-114">**Создание лаборатории hello**</span><span class="sxs-lookup"><span data-stu-id="33c77-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="33c77-115">Практические работы ― это hello, начальной точкой в Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="33c77-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="33c77-116">После создания лабораторной среде можно выполнять задачи, например добавление пользователей (тест-инженерами) toohello лаборатории, параметр политики toocontrol затрат, определение образов виртуальных Машин, которые можно быстро создать и многое другое.</span><span class="sxs-lookup"><span data-stu-id="33c77-116">Once you create a lab, you can perform tasks such as adding users (testers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="33c77-117">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="33c77-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="33c77-118">Задача</span><span class="sxs-lookup"><span data-stu-id="33c77-118">Task</span></span> | <span data-ttu-id="33c77-119">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="33c77-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="33c77-120">Создание лаборатории в лаборатории для разработки и тестирования Azure</span><span class="sxs-lookup"><span data-stu-id="33c77-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="33c77-121">Узнайте, как toocreate a лаборатории в Azure DevTest Labs в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="33c77-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="33c77-122">**Создание виртуальных машин за считанные минуты с помощью пользовательских образов и готовых образов из Marketplace**</span><span class="sxs-lookup"><span data-stu-id="33c77-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="33c77-123">Можно выбрать готовых образов из разнообразных изображения в hello Azure Marketplace и сделать их доступными в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="33c77-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="33c77-124">Если готовых образов hello не соответствует требованиям, можно создать пользовательский образ путем создания лаборатории виртуальной Машины, используя готовые образ из Azure Marketplace, установка всех hello необходимого программного обеспечения и сохранение hello виртуальной Машины в качестве пользовательского образа в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="33c77-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="33c77-125">При использовании пользовательских образов, рассмотрите возможность использования toocreate фабрики образа и распространение изображений.</span><span class="sxs-lookup"><span data-stu-id="33c77-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="33c77-126">Фабрика образов — это решение "конфигурация как код", которое регулярно автоматически создает и распространяет настроенные образы.</span><span class="sxs-lookup"><span data-stu-id="33c77-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="33c77-127">Это toomanually время, необходимое hello сохраняет настройки системы hello, после создания виртуальной Машины с hello базовая ОС.</span><span class="sxs-lookup"><span data-stu-id="33c77-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="33c77-128">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="33c77-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="33c77-129">Задача</span><span class="sxs-lookup"><span data-stu-id="33c77-129">Task</span></span> | <span data-ttu-id="33c77-130">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="33c77-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="33c77-131">Настройка образов Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="33c77-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="33c77-132">Дополнительные сведения о белом списке образы Azure Marketplace, чтобы сделать доступными для выбора только образы hello нужный для инженеров-испытателей hello.</span><span class="sxs-lookup"><span data-stu-id="33c77-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello testers.</span></span>|
   | [<span data-ttu-id="33c77-133">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="33c77-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="33c77-134">Создайте пользовательский образ по предварительной установке hello программное обеспечение, чтобы тест-инженерам быстро создать ВМ с помощью пользовательского образа hello.</span><span class="sxs-lookup"><span data-stu-id="33c77-134">Create a custom image by pre-installing hello software you need so that testers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="33c77-135">Дополнительные сведения о фабрике образов</span><span class="sxs-lookup"><span data-stu-id="33c77-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="33c77-136">Просмотрите видео, которое описывает способ tooset Настройка и использование фабрику изображения.</span><span class="sxs-lookup"><span data-stu-id="33c77-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="33c77-137">**Создание многократно используемых шаблонов для виртуальных машин тестировщиков**</span><span class="sxs-lookup"><span data-stu-id="33c77-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="33c77-138">Формулы в Azure DevTest Labs представляет собой список значений свойства по умолчанию используемых toocreate виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="33c77-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="33c77-139">Можно создать формулу в лаборатории hello, выбирая изображение, размер виртуальной Машины (сочетание ЦП и ОЗУ) и виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="33c77-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="33c77-140">Каждый тестировщик может видеть hello формулы в лаборатории hello и использовать ее toocreate виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="33c77-140">Each tester can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="33c77-141">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="33c77-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="33c77-142">Задача</span><span class="sxs-lookup"><span data-stu-id="33c77-142">Task</span></span> | <span data-ttu-id="33c77-143">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="33c77-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="33c77-144">Управление toocreate формулы DevTest Labs виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="33c77-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="33c77-145">Как создать формулу, выбрав образ, размер виртуальной машины (сочетание ЦП и ОЗУ) и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="33c77-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="33c77-146">**Создание тестовых сред с несколькими виртуальными машинами**</span><span class="sxs-lookup"><span data-stu-id="33c77-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="33c77-147">Можно использовать диспетчер ресурсов Azure шаблоны toodefine hello инфраструктурой и настройкой решение Azure и постоянно развертывать несколько тестовых виртуальных машин в согласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="33c77-147">You can use Azure Resource Manager templates toodefine hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="33c77-148">Ресурсы PaaS Azure можно развернуть в среде на основе шаблона Resource Manager. Эти ресурсы появятся в отслеживаемых затратах.</span><span class="sxs-lookup"><span data-stu-id="33c77-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="33c77-149">Завершение работы виртуальной Машины автоматически не применяется tooPaaS ресурсов.</span><span class="sxs-lookup"><span data-stu-id="33c77-149">However, VM auto shutdown does not apply tooPaaS resources.</span></span>

    <span data-ttu-id="33c77-150">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="33c77-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="33c77-151">Задача</span><span class="sxs-lookup"><span data-stu-id="33c77-151">Task</span></span> | <span data-ttu-id="33c77-152">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="33c77-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="33c77-153">Создание сред со множеством виртуальных машин и ресурсов PaaS с помощью шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="33c77-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="33c77-154">Сведения о том, как развернуть несколько виртуальных машин в согласованном состоянии для тестовой среды.</span><span class="sxs-lookup"><span data-stu-id="33c77-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="33c77-155">**Создать настройку виртуальной Машины гибкие артефакты tooenable**</span><span class="sxs-lookup"><span data-stu-id="33c77-155">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="33c77-156">Артефакты, используемые toodeploy и настройки приложения после подготовки виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="33c77-156">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="33c77-157">Артефактами могут быть:</span><span class="sxs-lookup"><span data-stu-id="33c77-157">Artifacts can be:</span></span>

   - <span data-ttu-id="33c77-158">Средства, которые должны tooinstall на hello виртуальной Машины — например агенты, Fiddler и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33c77-158">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="33c77-159">Действия, которые должны toorun на hello виртуальной Машины — например клонированием репозитория.</span><span class="sxs-lookup"><span data-stu-id="33c77-159">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="33c77-160">Приложения, которые должны tootest.</span><span class="sxs-lookup"><span data-stu-id="33c77-160">Applications that you want tootest.</span></span>

   <span data-ttu-id="33c77-161">Многие артефакты уже встроены.</span><span class="sxs-lookup"><span data-stu-id="33c77-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="33c77-162">Но если вам нужны дополнительные настройки для определенных потребностей, можно создать пользовательские артефакты.</span><span class="sxs-lookup"><span data-stu-id="33c77-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="33c77-163">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="33c77-163">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="33c77-164">Задача</span><span class="sxs-lookup"><span data-stu-id="33c77-164">Task</span></span> | <span data-ttu-id="33c77-165">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="33c77-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="33c77-166">Создание пользовательских артефактов для виртуальной машины DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="33c77-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="33c77-167">Создайте собственные пользовательские артефакты для hello виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="33c77-167">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="33c77-168">Добавление репозитория Git toostore пользовательские артефакты и шаблоны Azure Resource Manager для использования в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="33c77-168">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="33c77-169">Узнайте, как toostore вашей пользовательской артефактов в собственный закрытый репозиторий Git.</span><span class="sxs-lookup"><span data-stu-id="33c77-169">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="33c77-170">**Контроль расходов**</span><span class="sxs-lookup"><span data-stu-id="33c77-170">**Control costs**</span></span>
   
    <span data-ttu-id="33c77-171">Azure DevTest Labs позволяет tooset политику в hello лаборатории toospecify hello максимальное число виртуальных машин, которые могут быть созданы в лаборатории hello тест-инженером.</span><span class="sxs-lookup"><span data-stu-id="33c77-171">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a tester in hello lab.</span></span> 
   
    <span data-ttu-id="33c77-172">Если команда тестирования имеет набор график работы и вы хотите toostop все виртуальные машины hello в определенное время дня hello и автоматически перезапустить их hello следующий день, это легко сделать, политиками параметр автоматического завершения работы и автозапуска в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="33c77-172">If your test team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="33c77-173">Наконец при разработке приложений можно удалить все виртуальные машины hello за один раз, выполнив один сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33c77-173">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="33c77-174">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="33c77-174">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="33c77-175">Задача</span><span class="sxs-lookup"><span data-stu-id="33c77-175">Task</span></span> | <span data-ttu-id="33c77-176">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="33c77-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="33c77-177">Определение политик лаборатории</span><span class="sxs-lookup"><span data-stu-id="33c77-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="33c77-178">Контролировать стоимость путем создания политик в лаборатории hello.</span><span class="sxs-lookup"><span data-stu-id="33c77-178">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="33c77-179">Удалить все hello лаборатории виртуальных машин с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="33c77-179">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="33c77-180">Удалите все hello labs за одну операцию, после завершения тестирования.</span><span class="sxs-lookup"><span data-stu-id="33c77-180">Delete all hello labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="33c77-181">**Добавление виртуальной сети tooa лаборатории**</span><span class="sxs-lookup"><span data-stu-id="33c77-181">**Add a virtual network tooa Lab**</span></span> 
   
    <span data-ttu-id="33c77-182">При каждом создании лаборатории служба DevTest Labs создает новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="33c77-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="33c77-183">Если вы настроили собственную виртуальную сеть — например, с помощью ExpressRoute или через виртуальную Частную сеть для — можно добавить параметры виртуальной сети этой виртуальной сети лаборатории tooyour, чтобы оно было доступно при создании виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="33c77-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="33c77-184">Кроме того нет Azure Active Directory домена соединения артефакт доступен, при создании hello ВМ, присоединенных к домену tooa виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="33c77-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="33c77-185">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="33c77-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="33c77-186">Задача</span><span class="sxs-lookup"><span data-stu-id="33c77-186">Task</span></span> | <span data-ttu-id="33c77-187">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="33c77-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="33c77-188">Настройка виртуальной сети в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="33c77-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="33c77-189">Узнайте, как tooconfigure виртуальной сети в Azure DevTest Labs, используя hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="33c77-189">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="33c77-190">**Предоставить каждого инженера-испытателя hello лаборатории**</span><span class="sxs-lookup"><span data-stu-id="33c77-190">**Share hello lab with each tester**</span></span>
   
    <span data-ttu-id="33c77-191">Тестировщики могут получить прямой доступ к лаборатории с помощью предоставленной им ссылки.</span><span class="sxs-lookup"><span data-stu-id="33c77-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="33c77-192">Даже не toohave учетная запись Azure, при условии, что они имеют [учетную запись Майкрософт](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="33c77-192">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="33c77-193">Тестировщики не видят виртуальные машины, созданные другими тестировщиками.</span><span class="sxs-lookup"><span data-stu-id="33c77-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="33c77-194">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="33c77-194">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="33c77-195">Задача</span><span class="sxs-lookup"><span data-stu-id="33c77-195">Task</span></span> | <span data-ttu-id="33c77-196">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="33c77-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="33c77-197">Добавить тест-инженер tooa лаборатории в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="33c77-197">Add a tester tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="33c77-198">Используйте hello Azure tooadd портала тест-инженеры tooyour лаборатории.</span><span class="sxs-lookup"><span data-stu-id="33c77-198">Use hello Azure portal tooadd testers tooyour lab.</span></span>|
   | [<span data-ttu-id="33c77-199">Добавить тест-инженеры toohello лаборатории с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="33c77-199">Add testers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="33c77-200">Используйте Добавление тест-инженеры tooyour лаборатории tooautomate PowerShell.</span><span class="sxs-lookup"><span data-stu-id="33c77-200">Use PowerShell tooautomate adding testers tooyour lab.</span></span> |
   | [<span data-ttu-id="33c77-201">Получение лабораторной toohello ссылку</span><span class="sxs-lookup"><span data-stu-id="33c77-201">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="33c77-202">Сведения о том, как тестировщики могут напрямую подключаться к лаборатории по ссылке.</span><span class="sxs-lookup"><span data-stu-id="33c77-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="33c77-203">**Автоматическое создание лабораторий для дополнительных команд**</span><span class="sxs-lookup"><span data-stu-id="33c77-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="33c77-204">Можно автоматизировать создание лаборатории, включая пользовательские настройки, путем создания шаблона диспетчера ресурсов и использования идентичных labs toocreate снова и снова.</span><span class="sxs-lookup"><span data-stu-id="33c77-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="33c77-205">Дополнительные сведения, щелкнув ссылки hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="33c77-205">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="33c77-206">Задача</span><span class="sxs-lookup"><span data-stu-id="33c77-206">Task</span></span> | <span data-ttu-id="33c77-207">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="33c77-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="33c77-208">Создание лаборатории с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="33c77-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="33c77-209">Как создать лабораторию в Azure DevTest Labs с помощью шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="33c77-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

