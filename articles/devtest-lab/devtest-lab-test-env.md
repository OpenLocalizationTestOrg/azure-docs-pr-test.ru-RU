---
title: "Использование Azure DevTest Labs для виртуальных машин и тестовых сред PaaS | Документы Майкрософт"
description: "Сведения об использовании Azure DevTest Labs для виртуальных машин и тестовых сред PaaS."
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
ms.openlocfilehash: a556cee9d7b665cd7df23c97e7e2c8c2afabbe58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="4ba82-103">Использование Azure DevTest Labs для виртуальных машин и тестовых сред PaaS</span><span class="sxs-lookup"><span data-stu-id="4ba82-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="4ba82-104">Azure DevTest Labs можно использовать для реализации многих ключевых сценариев. Основным из них является размещение виртуальных машин для тестировщиков.</span><span class="sxs-lookup"><span data-stu-id="4ba82-104">You can use Azure DevTest Labs to implement many key scenarios, but a primary scenario involves using DevTest Labs to host machines for testers.</span></span> 

<span data-ttu-id="4ba82-105">В этом сценарии DevTest Labs предоставляет следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="4ba82-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="4ba82-106">Тестировщики могут проверить последнюю версию своего приложения, быстро развернув среды Windows и Linux с применением повторно используемых шаблонов и артефактов.</span><span class="sxs-lookup"><span data-stu-id="4ba82-106">Testers can test the latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="4ba82-107">Тестировщики могут увеличить масштаб нагрузочного тестирования, развернув несколько агентов тестирования.</span><span class="sxs-lookup"><span data-stu-id="4ba82-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="4ba82-108">Администраторы могут контролировать затраты, следя за тем, чтобы:</span><span class="sxs-lookup"><span data-stu-id="4ba82-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="4ba82-109">тестировщикам не выделялось больше виртуальных машин, чем требуется для тестирования;</span><span class="sxs-lookup"><span data-stu-id="4ba82-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="4ba82-110">виртуальные машины отключались, если они не используются.</span><span class="sxs-lookup"><span data-stu-id="4ba82-110">VMs are shut down when not in use.</span></span>

![Использование DevTest Labs для обучения](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="4ba82-112">Из этой статьи вы узнаете о различных функциях Azure DevTest Labs, которые обеспечивают соответствие требованиям для тестировщиков. Здесь также приведены подробные инструкции по настройке лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4ba82-112">In this article, you learn about various Azure DevTest Labs features used to meet tester requirements and the detailed steps to follow to set up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="4ba82-113">Реализация тестовых сред с помощью Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4ba82-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="4ba82-114">**Создание лаборатории**</span><span class="sxs-lookup"><span data-stu-id="4ba82-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="4ba82-115">Лаборатории являются отправной точкой в Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="4ba82-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="4ba82-116">Создав лабораторию, вы сможете добавить пользователей (тестировщиков) в лабораторию, настроить политики для контроля расходов, определить образы виртуальных машин, которые можно будет быстро создавать, и др.</span><span class="sxs-lookup"><span data-stu-id="4ba82-116">Once you create a lab, you can perform tasks such as adding users (testers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="4ba82-117">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba82-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4ba82-118">Задача</span><span class="sxs-lookup"><span data-stu-id="4ba82-118">Task</span></span> | <span data-ttu-id="4ba82-119">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="4ba82-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4ba82-120">Создание лаборатории в лаборатории для разработки и тестирования Azure</span><span class="sxs-lookup"><span data-stu-id="4ba82-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="4ba82-121">Как создать лабораторию в Azure DevTest Labs на портале Azure</span><span class="sxs-lookup"><span data-stu-id="4ba82-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="4ba82-122">**Создание виртуальных машин за считанные минуты с помощью пользовательских образов и готовых образов из Marketplace**</span><span class="sxs-lookup"><span data-stu-id="4ba82-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="4ba82-123">Вы можете выбрать любой из множества доступных готовых образов в Azure Marketplace и добавить его в свою лабораторию.</span><span class="sxs-lookup"><span data-stu-id="4ba82-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="4ba82-124">Если готовые образы не подходят, вы можете создать свой собственный образ. Для этого нужно создать лабораторную виртуальную машину, используя готовый образ из Azure Marketplace, установить на нее все необходимое программное обеспечение и сохранить ее в качестве пользовательского образа в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4ba82-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="4ba82-125">Если вы планируете использовать пользовательские образы, рекомендуем использовать фабрику образов, которая поможет их создавать и распространять.</span><span class="sxs-lookup"><span data-stu-id="4ba82-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="4ba82-126">Фабрика образов — это решение "конфигурация как код", которое регулярно автоматически создает и распространяет настроенные образы.</span><span class="sxs-lookup"><span data-stu-id="4ba82-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="4ba82-127">Это экономит время, которое обычно уходит на настройку системы вручную после создания виртуальной машины с базовой операционной системой.</span><span class="sxs-lookup"><span data-stu-id="4ba82-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="4ba82-128">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba82-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4ba82-129">Задача</span><span class="sxs-lookup"><span data-stu-id="4ba82-129">Task</span></span> | <span data-ttu-id="4ba82-130">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="4ba82-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4ba82-131">Настройка образов Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4ba82-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="4ba82-132">Сведения о том, как добавить образы Azure Marketplace в список разрешений, а также сделать доступными необходимые образы для тестировщиков.</span><span class="sxs-lookup"><span data-stu-id="4ba82-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the testers.</span></span>|
   | [<span data-ttu-id="4ba82-133">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="4ba82-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="4ba82-134">Сведения о том, как создать пользовательский образ путем предварительной установки необходимого ПО. С помощью пользовательского образа тестеры смогут быстро создавать виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="4ba82-134">Create a custom image by pre-installing the software you need so that testers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="4ba82-135">Дополнительные сведения о фабрике образов</span><span class="sxs-lookup"><span data-stu-id="4ba82-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="4ba82-136">Как настроить и использовать фабрику образов (видео).</span><span class="sxs-lookup"><span data-stu-id="4ba82-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="4ba82-137">**Создание многократно используемых шаблонов для виртуальных машин тестировщиков**</span><span class="sxs-lookup"><span data-stu-id="4ba82-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="4ba82-138">Формула в Azure DevTest Labs — это список значений свойств, используемых по умолчанию при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4ba82-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="4ba82-139">Вы можете создать формулу в лаборатории, выбрав образ, размер виртуальной машины (сочетание ЦП и ОЗУ) и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="4ba82-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="4ba82-140">Каждый тестировщик может просмотреть формулу в лаборатории и использовать ее для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4ba82-140">Each tester can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="4ba82-141">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba82-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4ba82-142">Задача</span><span class="sxs-lookup"><span data-stu-id="4ba82-142">Task</span></span> | <span data-ttu-id="4ba82-143">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="4ba82-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4ba82-144">Управление формулами DevTest Labs для создания виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="4ba82-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="4ba82-145">Как создать формулу, выбрав образ, размер виртуальной машины (сочетание ЦП и ОЗУ) и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="4ba82-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="4ba82-146">**Создание тестовых сред с несколькими виртуальными машинами**</span><span class="sxs-lookup"><span data-stu-id="4ba82-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="4ba82-147">С помощью шаблонов Azure Resource Manager можно определить инфраструктуру и конфигурацию решения Azure и многократно развернуть несколько тестовых виртуальных машин в согласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="4ba82-147">You can use Azure Resource Manager templates to define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="4ba82-148">Ресурсы PaaS Azure можно развернуть в среде на основе шаблона Resource Manager. Эти ресурсы появятся в отслеживаемых затратах.</span><span class="sxs-lookup"><span data-stu-id="4ba82-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="4ba82-149">Однако автоматическое выключение виртуальной машины не применяется к ресурсам PaaS.</span><span class="sxs-lookup"><span data-stu-id="4ba82-149">However, VM auto shutdown does not apply to PaaS resources.</span></span>

    <span data-ttu-id="4ba82-150">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba82-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4ba82-151">Задача</span><span class="sxs-lookup"><span data-stu-id="4ba82-151">Task</span></span> | <span data-ttu-id="4ba82-152">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="4ba82-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4ba82-153">Создание сред со множеством виртуальных машин и ресурсов PaaS с помощью шаблонов Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4ba82-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="4ba82-154">Сведения о том, как развернуть несколько виртуальных машин в согласованном состоянии для тестовой среды.</span><span class="sxs-lookup"><span data-stu-id="4ba82-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="4ba82-155">**Создание артефактов для включения гибкой настройки виртуальной машины**</span><span class="sxs-lookup"><span data-stu-id="4ba82-155">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="4ba82-156">Артефакты используются для развертывания и настройки приложения после подготовки виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="4ba82-156">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="4ba82-157">Артефактами могут быть:</span><span class="sxs-lookup"><span data-stu-id="4ba82-157">Artifacts can be:</span></span>

   - <span data-ttu-id="4ba82-158">Средства для установки на виртуальной машине, такие как агенты, Fiddler и Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ba82-158">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="4ba82-159">Действия, которые должны выполняться на виртуальной машине, такие как клонирование репозитория.</span><span class="sxs-lookup"><span data-stu-id="4ba82-159">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="4ba82-160">Приложения, которые требуется протестировать.</span><span class="sxs-lookup"><span data-stu-id="4ba82-160">Applications that you want to test.</span></span>

   <span data-ttu-id="4ba82-161">Многие артефакты уже встроены.</span><span class="sxs-lookup"><span data-stu-id="4ba82-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="4ba82-162">Но если вам нужны дополнительные настройки для определенных потребностей, можно создать пользовательские артефакты.</span><span class="sxs-lookup"><span data-stu-id="4ba82-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="4ba82-163">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba82-163">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4ba82-164">Задача</span><span class="sxs-lookup"><span data-stu-id="4ba82-164">Task</span></span> | <span data-ttu-id="4ba82-165">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="4ba82-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4ba82-166">Создание пользовательских артефактов для виртуальной машины DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4ba82-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="4ba82-167">Как создавать пользовательские артефакты для виртуальных машин в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4ba82-167">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="4ba82-168">Добавление репозитория Git для хранения пользовательских артефактов и шаблонов Azure Resource Manager в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4ba82-168">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="4ba82-169">Как сохранять пользовательские артефакты в частном репозитории Git.</span><span class="sxs-lookup"><span data-stu-id="4ba82-169">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="4ba82-170">**Контроль расходов**</span><span class="sxs-lookup"><span data-stu-id="4ba82-170">**Control costs**</span></span>
   
    <span data-ttu-id="4ba82-171">Azure DevTest Labs позволяет задать политику, определяющую максимальное число виртуальных машин, которые тестировщик может создать в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4ba82-171">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a tester in the lab.</span></span> 
   
    <span data-ttu-id="4ba82-172">Предположим, команда тестирования установила рабочее расписание, и нужно остановить все виртуальные машины в определенное время, а затем автоматически перезапустить их на следующий день. Для этого в лаборатории нужно задать политики автоматического завершения работы и запуска.</span><span class="sxs-lookup"><span data-stu-id="4ba82-172">If your test team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="4ba82-173">По завершении разработки вы сможете удалить все виртуальные машины одновременно, выполнив один сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ba82-173">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="4ba82-174">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba82-174">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4ba82-175">Задача</span><span class="sxs-lookup"><span data-stu-id="4ba82-175">Task</span></span> | <span data-ttu-id="4ba82-176">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="4ba82-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4ba82-177">Определение политик лаборатории</span><span class="sxs-lookup"><span data-stu-id="4ba82-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="4ba82-178">Как обеспечить контроль расходов с помощью политик в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="4ba82-178">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="4ba82-179">Удаление всех виртуальных машин лаборатории с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ba82-179">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="4ba82-180">После завершения тестирования удалите все лаборатории в составе одной операции.</span><span class="sxs-lookup"><span data-stu-id="4ba82-180">Delete all the labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="4ba82-181">**Добавление виртуальной сети в лабораторию**</span><span class="sxs-lookup"><span data-stu-id="4ba82-181">**Add a virtual network to a Lab**</span></span> 
   
    <span data-ttu-id="4ba82-182">При каждом создании лаборатории служба DevTest Labs создает новую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="4ba82-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="4ba82-183">Если вы настроили свою собственную виртуальную сеть (например, с помощью ExpressRoute или VPN типа "сеть-сеть"), можно добавить ее в параметрах виртуальной сети лаборатории и сделать доступной при создании виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="4ba82-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="4ba82-184">Кроме того, можно воспользоваться артефактом присоединения к домену Azure Active Directory. Этот артефакт присоединяет виртуальную машину к домену при ее создании.</span><span class="sxs-lookup"><span data-stu-id="4ba82-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="4ba82-185">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba82-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4ba82-186">Задача</span><span class="sxs-lookup"><span data-stu-id="4ba82-186">Task</span></span> | <span data-ttu-id="4ba82-187">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="4ba82-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4ba82-188">Настройка виртуальной сети в Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4ba82-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="4ba82-189">Как настроить виртуальную сеть в Azure DevTest Labs на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba82-189">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="4ba82-190">**Предоставление доступа к лаборатории для каждого тестировщика**</span><span class="sxs-lookup"><span data-stu-id="4ba82-190">**Share the lab with each tester**</span></span>
   
    <span data-ttu-id="4ba82-191">Тестировщики могут получить прямой доступ к лаборатории с помощью предоставленной им ссылки.</span><span class="sxs-lookup"><span data-stu-id="4ba82-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="4ba82-192">Разработчикам с [учетной записью Майкрософт](devtest-lab-faq.md#what-is-a-microsoft-account) даже не требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba82-192">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="4ba82-193">Тестировщики не видят виртуальные машины, созданные другими тестировщиками.</span><span class="sxs-lookup"><span data-stu-id="4ba82-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="4ba82-194">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba82-194">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4ba82-195">Задача</span><span class="sxs-lookup"><span data-stu-id="4ba82-195">Task</span></span> | <span data-ttu-id="4ba82-196">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="4ba82-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4ba82-197">Добавление тестировщика в лабораторию Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="4ba82-197">Add a tester to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="4ba82-198">Добавление тестировщиков в лабораторию с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="4ba82-198">Use the Azure portal to add testers to your lab.</span></span>|
   | [<span data-ttu-id="4ba82-199">Добавление тестировщиков в лабораторию с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ba82-199">Add testers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="4ba82-200">Автоматическое добавление тестировщиков в лабораторию с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ba82-200">Use PowerShell to automate adding testers to your lab.</span></span> |
   | [<span data-ttu-id="4ba82-201">Получение ссылки на лабораторию</span><span class="sxs-lookup"><span data-stu-id="4ba82-201">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="4ba82-202">Сведения о том, как тестировщики могут напрямую подключаться к лаборатории по ссылке.</span><span class="sxs-lookup"><span data-stu-id="4ba82-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="4ba82-203">**Автоматическое создание лабораторий для дополнительных команд**</span><span class="sxs-lookup"><span data-stu-id="4ba82-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="4ba82-204">Вы можете автоматизировать создание лаборатории вместе с пользовательскими параметрами, создав шаблон Resource Manager, который можно много раз использовать для создания идентичных лабораторий.</span><span class="sxs-lookup"><span data-stu-id="4ba82-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="4ba82-205">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="4ba82-205">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="4ba82-206">Задача</span><span class="sxs-lookup"><span data-stu-id="4ba82-206">Task</span></span> | <span data-ttu-id="4ba82-207">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="4ba82-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="4ba82-208">Создание лаборатории с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4ba82-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="4ba82-209">Как создать лабораторию в Azure DevTest Labs с помощью шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4ba82-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

