---
title: "Использование Azure DevTest Labs для разработчиков | Документация Майкрософт"
description: "Узнайте, как использовать Azure DevTest Labs для сценариев разработки."
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
ms.openlocfilehash: c187819e9392908c8979556f80e8c94739eb14d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="aae22-103">Использование Azure DevTest Labs для разработчиков</span><span class="sxs-lookup"><span data-stu-id="aae22-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="aae22-104">Azure DevTest Labs можно использовать для реализации многих ключевых сценариев. Рассмотрим один из них, в котором DevTest Labs применяется для размещения виртуальных машин разработки.</span><span class="sxs-lookup"><span data-stu-id="aae22-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span></span> <span data-ttu-id="aae22-105">В этом сценарии DevTest Labs предоставляет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="aae22-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="aae22-106">разработчики могут быстро подготовить виртуальные машины разработки по требованию;</span><span class="sxs-lookup"><span data-stu-id="aae22-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="aae22-107">разработчики могут в любое время легко настроить виртуальные машины разработки;</span><span class="sxs-lookup"><span data-stu-id="aae22-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="aae22-108">администраторы могут контролировать затраты, следя за тем, чтобы:</span><span class="sxs-lookup"><span data-stu-id="aae22-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="aae22-109">разработчикам не выделялось больше виртуальных машин, чем требуется для разработки;</span><span class="sxs-lookup"><span data-stu-id="aae22-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="aae22-110">виртуальные машины отключались, если они не используются.</span><span class="sxs-lookup"><span data-stu-id="aae22-110">VMs are shut down when not in use.</span></span> 

![Использование DevTest Labs для обучения](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="aae22-112">Из этой статьи вы узнаете о различных функциях Azure DevTest Labs, обеспечивающих соответствие требованиям разработчиков. Также здесь приведены подробные инструкции по настройке лаборатории.</span><span class="sxs-lookup"><span data-stu-id="aae22-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="aae22-113">Реализация сред разработки при помощи Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="aae22-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="aae22-114">**Создание лаборатории**</span><span class="sxs-lookup"><span data-stu-id="aae22-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="aae22-115">Лаборатории являются отправной точкой в Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="aae22-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="aae22-116">Создав лабораторию, вы сможете добавить пользователей (разработчиков) в лабораторию, настроить политики для контроля расходов, определить образы виртуальных машин, которые можно будет быстро создавать, и др.</span><span class="sxs-lookup"><span data-stu-id="aae22-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="aae22-117">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="aae22-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="aae22-118">Задача</span><span class="sxs-lookup"><span data-stu-id="aae22-118">Task</span></span> | <span data-ttu-id="aae22-119">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="aae22-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="aae22-120">Создание лаборатории в лаборатории для разработки и тестирования Azure</span><span class="sxs-lookup"><span data-stu-id="aae22-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="aae22-121">Как создать лабораторию в Azure DevTest Labs на портале Azure</span><span class="sxs-lookup"><span data-stu-id="aae22-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="aae22-122">**Создание виртуальных машин за считанные минуты с помощью пользовательских образов и готовых образов из Marketplace**</span><span class="sxs-lookup"><span data-stu-id="aae22-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="aae22-123">Вы можете выбрать любой из множества доступных готовых образов в Azure Marketplace и добавить его в свою лабораторию.</span><span class="sxs-lookup"><span data-stu-id="aae22-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="aae22-124">Если готовые образы не подходят, вы можете создать свой собственный образ. Для этого нужно создать лабораторную виртуальную машину, используя готовый образ из Azure Marketplace, установить на нее все необходимое программное обеспечение и сохранить ее в качестве пользовательского образа в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="aae22-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="aae22-125">Если вы планируете использовать пользовательские образы, рекомендуем использовать фабрику образов, которая поможет их создавать и распространять.</span><span class="sxs-lookup"><span data-stu-id="aae22-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="aae22-126">Фабрика образов — это решение "конфигурация как код", которое регулярно автоматически создает и распространяет настроенные образы.</span><span class="sxs-lookup"><span data-stu-id="aae22-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="aae22-127">Это экономит время, которое обычно уходит на настройку системы вручную после создания виртуальной машины с базовой операционной системой.</span><span class="sxs-lookup"><span data-stu-id="aae22-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="aae22-128">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="aae22-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="aae22-129">Задача</span><span class="sxs-lookup"><span data-stu-id="aae22-129">Task</span></span> | <span data-ttu-id="aae22-130">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="aae22-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="aae22-131">Настройка образов Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="aae22-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="aae22-132">Как добавить образы из Azure Marketplace в список разрешений, сделав доступными для выбора только образы для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="aae22-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span></span>|
   | [<span data-ttu-id="aae22-133">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="aae22-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="aae22-134">Как создать пользовательский образ путем предварительной установки необходимого ПО. С помощью пользовательского образа разработчики смогут быстро создавать виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="aae22-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="aae22-135">Дополнительные сведения о фабрике образов</span><span class="sxs-lookup"><span data-stu-id="aae22-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="aae22-136">Как настроить и использовать фабрику образов (видео).</span><span class="sxs-lookup"><span data-stu-id="aae22-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="aae22-137">**Создание многократно используемых шаблонов для компьютеров разработки**</span><span class="sxs-lookup"><span data-stu-id="aae22-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="aae22-138">Формула в Azure DevTest Labs — это список значений свойств, используемых по умолчанию при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aae22-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="aae22-139">Вы можете создать формулу в лаборатории, выбрав образ, размер виртуальной машины (сочетание ЦП и ОЗУ) и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="aae22-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="aae22-140">Каждый разработчик может просмотреть формулу в лаборатории и использовать ее для создания новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aae22-140">Each developer can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="aae22-141">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="aae22-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="aae22-142">Задача</span><span class="sxs-lookup"><span data-stu-id="aae22-142">Task</span></span> | <span data-ttu-id="aae22-143">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="aae22-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="aae22-144">Управление формулами DevTest Labs для создания виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="aae22-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="aae22-145">Как создать формулу, выбрав образ, размер виртуальной машины (сочетание ЦП и ОЗУ) и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="aae22-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="aae22-146">**Создание артефактов для включения гибкой настройки виртуальной машины**</span><span class="sxs-lookup"><span data-stu-id="aae22-146">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="aae22-147">Артефакты используются для развертывания и настройки приложения после подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="aae22-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="aae22-148">Артефактами могут быть:</span><span class="sxs-lookup"><span data-stu-id="aae22-148">Artifacts can be:</span></span>

   - <span data-ttu-id="aae22-149">Средства для установки на виртуальной машине, такие как агенты, Fiddler и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aae22-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="aae22-150">Действия, которые должны выполняться на виртуальной машине, такие как клонирование репозитория.</span><span class="sxs-lookup"><span data-stu-id="aae22-150">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="aae22-151">Приложения, которые требуется протестировать.</span><span class="sxs-lookup"><span data-stu-id="aae22-151">Applications that you want to test.</span></span>

   <span data-ttu-id="aae22-152">Многие артефакты уже встроены.</span><span class="sxs-lookup"><span data-stu-id="aae22-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="aae22-153">Если для определенных целей вам нужны дополнительные настройки, можно создать пользовательские артефакты.</span><span class="sxs-lookup"><span data-stu-id="aae22-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="aae22-154">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="aae22-154">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="aae22-155">Задача</span><span class="sxs-lookup"><span data-stu-id="aae22-155">Task</span></span> | <span data-ttu-id="aae22-156">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="aae22-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="aae22-157">Создание пользовательских артефактов для виртуальной машины DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="aae22-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="aae22-158">Как создавать пользовательские артефакты для виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="aae22-158">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="aae22-159">Добавление репозитория Git для хранения пользовательских артефактов и шаблонов Azure Resource Manager в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="aae22-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="aae22-160">Как сохранять пользовательские артефакты в частном репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="aae22-160">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="aae22-161">**Контроль расходов**</span><span class="sxs-lookup"><span data-stu-id="aae22-161">**Control costs**</span></span>
   
    <span data-ttu-id="aae22-162">Azure DevTest Labs позволяет задать в лаборатории политику, указывающую максимальное число виртуальных машин, которые может создать разработчик.</span><span class="sxs-lookup"><span data-stu-id="aae22-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span></span> 
   
    <span data-ttu-id="aae22-163">Предположим, команда разработчиков установила рабочее расписание и нужно остановить все виртуальные машины в определенное время, а затем автоматически перезапустить их на следующий день. Для этого в лаборатории нужно задать политики автоматического завершения работы и запуска.</span><span class="sxs-lookup"><span data-stu-id="aae22-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="aae22-164">По завершении разработки вы сможете удалить все виртуальные машины одновременно, выполнив один сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aae22-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="aae22-165">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="aae22-165">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="aae22-166">Задача</span><span class="sxs-lookup"><span data-stu-id="aae22-166">Task</span></span> | <span data-ttu-id="aae22-167">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="aae22-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="aae22-168">Определение политик лаборатории</span><span class="sxs-lookup"><span data-stu-id="aae22-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="aae22-169">Как обеспечить контроль расходов с помощью политик в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="aae22-169">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="aae22-170">Удаление всех виртуальных машин лаборатории с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="aae22-170">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="aae22-171">Как по завершении разработки удалить все лаборатории в рамках одной операции.</span><span class="sxs-lookup"><span data-stu-id="aae22-171">Delete all the labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="aae22-172">**Добавление виртуальной сети для виртуальной машины**</span><span class="sxs-lookup"><span data-stu-id="aae22-172">**Add a virtual network to a VM**</span></span> 
   
    <span data-ttu-id="aae22-173">При каждом создании лаборатории служба DevTest Labs создает новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="aae22-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="aae22-174">Если вы настроили свою собственную виртуальную сеть (например, с помощью ExpressRoute или VPN типа "сеть — сеть"), можно добавить ее в параметрах виртуальной сети лаборатории и сделать доступной при создании виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="aae22-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="aae22-175">Кроме того, можно воспользоваться артефактом присоединения к домену Azure Active Directory, соединяющим виртуальную машину с доменом при ее создании.</span><span class="sxs-lookup"><span data-stu-id="aae22-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="aae22-176">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="aae22-176">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="aae22-177">Задача</span><span class="sxs-lookup"><span data-stu-id="aae22-177">Task</span></span> | <span data-ttu-id="aae22-178">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="aae22-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="aae22-179">Настройка виртуальной сети в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="aae22-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="aae22-180">Как настроить виртуальную сеть в Azure DevTest Labs на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="aae22-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="aae22-181">**Предоставление доступа к лаборатории для каждого разработчика**</span><span class="sxs-lookup"><span data-stu-id="aae22-181">**Share the lab with each developer**</span></span>
   
    <span data-ttu-id="aae22-182">Разработчики могут напрямую подключаться к лаборатории, используя предоставленную им ссылку.</span><span class="sxs-lookup"><span data-stu-id="aae22-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="aae22-183">Разработчикам с [учетной записью Майкрософт](devtest-lab-faq.md#what-is-a-microsoft-account) даже не требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="aae22-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="aae22-184">Разработчики не видят виртуальные машины, созданные другими разработчиками.</span><span class="sxs-lookup"><span data-stu-id="aae22-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="aae22-185">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="aae22-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="aae22-186">Задача</span><span class="sxs-lookup"><span data-stu-id="aae22-186">Task</span></span> | <span data-ttu-id="aae22-187">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="aae22-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="aae22-188">Добавление разработчика в лабораторию в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="aae22-188">Add a developer to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="aae22-189">Как добавлять разработчиков в лабораторию с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="aae22-189">Use the Azure portal to add developers to your lab.</span></span>|
   | [<span data-ttu-id="aae22-190">Добавление разработчиков в лабораторию с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="aae22-190">Add developers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="aae22-191">Как выполнять автоматическое добавление разработчиков в лабораторию с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aae22-191">Use PowerShell to automate adding developers to your lab.</span></span> |
   | [<span data-ttu-id="aae22-192">Получение ссылки на лабораторию</span><span class="sxs-lookup"><span data-stu-id="aae22-192">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="aae22-193">Как разработчики могут напрямую подключаться к лаборатории по гиперссылке.</span><span class="sxs-lookup"><span data-stu-id="aae22-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="aae22-194">**Автоматическое создание лабораторий для дополнительных команд**</span><span class="sxs-lookup"><span data-stu-id="aae22-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="aae22-195">Вы можете автоматизировать создание лаборатории вместе с пользовательскими параметрами, создав шаблон Resource Manager, который можно много раз использовать для создания идентичных лабораторий.</span><span class="sxs-lookup"><span data-stu-id="aae22-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="aae22-196">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="aae22-196">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="aae22-197">Задача</span><span class="sxs-lookup"><span data-stu-id="aae22-197">Task</span></span> | <span data-ttu-id="aae22-198">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="aae22-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="aae22-199">Создание лаборатории с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="aae22-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="aae22-200">Как создать лабораторию в Azure DevTest Labs с помощью шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="aae22-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

