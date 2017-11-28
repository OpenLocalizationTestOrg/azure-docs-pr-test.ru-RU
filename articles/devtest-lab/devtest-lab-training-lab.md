---
title: "Использование Azure DevTest Labs для обучения | Документация Майкрософт"
description: "Узнайте, как использовать Azure DevTest Labs для сценариев обучения."
services: devtest-lab,virtual-machines
documentationcenter: na
author: steved0x
manager: douge
editor: 
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/12/2016
ms.author: sdanie
ms.openlocfilehash: a85999b7963e9a07d3f91ec47f298f91439c0808
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-training"></a><span data-ttu-id="1156b-103">Использование Azure DevTest Labs для обучения</span><span class="sxs-lookup"><span data-stu-id="1156b-103">Use Azure DevTest Labs for training</span></span>
<span data-ttu-id="1156b-104">Помимо разработки и тестирования, Azure DevTest Labs можно использовать для реализации множества основных сценариев.</span><span class="sxs-lookup"><span data-stu-id="1156b-104">Azure DevTest Labs can be used to implement many key scenarios in addition to dev/test.</span></span> <span data-ttu-id="1156b-105">Один из таких сценариев — настройка лаборатории для обучения.</span><span class="sxs-lookup"><span data-stu-id="1156b-105">One of those scenarios is to set up a lab for training.</span></span> <span data-ttu-id="1156b-106">Azure DevTest Labs позволяет создать лабораторию, куда можно добавить пользовательские шаблоны. Каждый обучаемый может использовать их для создания идентичных изолированных сред для обучения.</span><span class="sxs-lookup"><span data-stu-id="1156b-106">Azure DevTest Labs allows you to create a lab where you can provide custom templates that each trainee can use to create identical and isolated environments for training.</span></span> <span data-ttu-id="1156b-107">Путем применения политик можно настроить лабораторию таким образом, чтобы каждый обучаемый мог использовать среды обучения только при необходимости и при достаточном количестве ресурсов, например виртуальных машин, требуемых для обучения.</span><span class="sxs-lookup"><span data-stu-id="1156b-107">You can apply policies to ensure that training environments are available to each trainee only when they need them and contain enough resources - such as virtual machines - required for the training.</span></span> <span data-ttu-id="1156b-108">Теперь вы можете с легкостью предоставить обучаемым доступ к лаборатории, которую они могут открыть одним щелчком.</span><span class="sxs-lookup"><span data-stu-id="1156b-108">Finally, you can easily share the lab with trainees, which they can access in one click.</span></span>

![Использование DevTest Labs для обучения](./media/devtest-lab-training-lab/devtest-lab-training.png)

<span data-ttu-id="1156b-110">Azure DevTest Labs соответствует следующим требованиям, установленным для проведения обучения в любой виртуальной среде:</span><span class="sxs-lookup"><span data-stu-id="1156b-110">Azure DevTest Labs meets the following requirements that are required to conduct training in any virtual environment:</span></span> 

* <span data-ttu-id="1156b-111">Обучаемые не видят виртуальные машины, созданные другими обучаемыми.</span><span class="sxs-lookup"><span data-stu-id="1156b-111">Trainees cannot see VMs created by other trainees</span></span>
* <span data-ttu-id="1156b-112">Все машины для обучения должны быть идентичными.</span><span class="sxs-lookup"><span data-stu-id="1156b-112">Every training machine should be identical</span></span>
* <span data-ttu-id="1156b-113">Обучаемые могут быстро подготовить среды для обучения.</span><span class="sxs-lookup"><span data-stu-id="1156b-113">Trainees can quickly provision their training environments</span></span>
* <span data-ttu-id="1156b-114">Обучаемые не могут получить больше виртуальных машин, чем требуется для обучения, и завершают работу виртуальных машин, которые не используются, что гарантирует контроль расходования ресурсов.</span><span class="sxs-lookup"><span data-stu-id="1156b-114">Control cost by ensuring that trainees cannot get more VMs than they need for the training and also shutdown VMs when they are not using them</span></span>
* <span data-ttu-id="1156b-115">Каждому обучаемому можно предоставить доступ к учебной лаборатории.</span><span class="sxs-lookup"><span data-stu-id="1156b-115">Easily share the training lab with each trainee</span></span>
* <span data-ttu-id="1156b-116">При необходимости учебные лаборатории можно использовать повторно.</span><span class="sxs-lookup"><span data-stu-id="1156b-116">Reuse the training lab again and again</span></span>

<span data-ttu-id="1156b-117">В этой статье вы узнаете о различных функциях Azure DevTest Labs, позволяющих обеспечить соответствие указанным выше требованиям, а также приведены подробные инструкции по настройке лаборатории для обучения.</span><span class="sxs-lookup"><span data-stu-id="1156b-117">In this article, you learn about various Azure DevTest Labs features that can be used to meet the previously described training requirements and detailed steps that you can follow to set up a lab for training.</span></span>  

## <a name="implementing-training-with-azure-devtest-labs"></a><span data-ttu-id="1156b-118">Реализация обучения с помощью Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1156b-118">Implementing training with Azure DevTest Labs</span></span>
1. <span data-ttu-id="1156b-119">**Создание лаборатории**</span><span class="sxs-lookup"><span data-stu-id="1156b-119">**Create the lab**</span></span> 
   
    <span data-ttu-id="1156b-120">Лаборатории являются отправной точкой в Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="1156b-120">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="1156b-121">После создания лаборатории можно приступить к выполнению задач, например добавлению пользователей (обучаемых) в лабораторию, настройке политик для контроля расходов, определению образов виртуальных машин, которые можно быстро создать, и др.</span><span class="sxs-lookup"><span data-stu-id="1156b-121">Once you create a lab, you can perform tasks such as add users (trainees) to the lab, set policies to control costs, define VM images that can create quickly, and more.</span></span>   
   
    <span data-ttu-id="1156b-122">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1156b-122">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1156b-123">Задача</span><span class="sxs-lookup"><span data-stu-id="1156b-123">Task</span></span> | <span data-ttu-id="1156b-124">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="1156b-124">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1156b-125">Создание лаборатории в лаборатории для разработки и тестирования Azure</span><span class="sxs-lookup"><span data-stu-id="1156b-125">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="1156b-126">Как создать лабораторию в Azure DevTest Labs на портале Azure</span><span class="sxs-lookup"><span data-stu-id="1156b-126">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="1156b-127">**Создание обучающих виртуальных машин за считаные минуты с помощью готовых образов Marketplace и пользовательских образов**</span><span class="sxs-lookup"><span data-stu-id="1156b-127">**Create training VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="1156b-128">Вы можете выбрать любые из множества готовых образов, доступных в Azure Marketplace, и сделать их доступными для обучаемых в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="1156b-128">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available for the trainees in the lab.</span></span> <span data-ttu-id="1156b-129">Если готовые образы не соответствуют требованиям, вы можете создать пользовательский образ. Для этого нужно создать виртуальную машину лаборатории, используя готовый образ из Azure Marketplace, установить на нее все необходимое программное обеспечение для обучения и сохранить ее в качестве пользовательского образа в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="1156b-129">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need for the training, and saving the VM as custom image in the lab.</span></span> 
   
    <span data-ttu-id="1156b-130">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1156b-130">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1156b-131">Задача</span><span class="sxs-lookup"><span data-stu-id="1156b-131">Task</span></span> | <span data-ttu-id="1156b-132">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="1156b-132">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1156b-133">Настройка образов Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="1156b-133">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="1156b-134">Как добавить образы Azure Marketplace в список разрешений, а также сделать доступными для выбора необходимые образы для обучения.</span><span class="sxs-lookup"><span data-stu-id="1156b-134">Learn how you can whitelist Azure Marketplace images; making available for selection only the images you want for the training.</span></span> |
   | [<span data-ttu-id="1156b-135">Создание пользовательского образа</span><span class="sxs-lookup"><span data-stu-id="1156b-135">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="1156b-136">Как создать пользовательский образ путем предварительной установки необходимого ПО для обучения, чтобы обучаемые могли быстро создать виртуальную машину с его помощью.</span><span class="sxs-lookup"><span data-stu-id="1156b-136">Create a custom image by pre-installing the software you need for the training so that trainees can quickly create a VM using the custom image.</span></span> |
3. <span data-ttu-id="1156b-137">**Создание многократно используемых шаблонов для обучающих машин**</span><span class="sxs-lookup"><span data-stu-id="1156b-137">**Create reusable templates for training machines**</span></span> 
   
    <span data-ttu-id="1156b-138">Формула в Azure DevTest Labs — это список значений свойств, используемых по умолчанию при создании виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1156b-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="1156b-139">Вы можете создать формулу в лаборатории, выбрав образ, размер виртуальной машины (сочетание ЦП и ОЗУ) и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="1156b-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="1156b-140">Каждый обучаемый может просмотреть формулу в лаборатории и использовать ее для создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="1156b-140">Each trainee can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="1156b-141">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1156b-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1156b-142">Задача</span><span class="sxs-lookup"><span data-stu-id="1156b-142">Task</span></span> | <span data-ttu-id="1156b-143">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="1156b-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1156b-144">Управление формулами DevTest Labs для создания виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="1156b-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="1156b-145">Как создать формулу, выбрав образ, размер виртуальной машины (сочетание ЦП и ОЗУ) и виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="1156b-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span> |
4. <span data-ttu-id="1156b-146">**Контроль расходов**</span><span class="sxs-lookup"><span data-stu-id="1156b-146">**Control costs**</span></span>
   
    <span data-ttu-id="1156b-147">Azure DevTest Labs позволяет задать в лаборатории политику, чтобы указать максимальное число виртуальных машин, которые может создать обучаемый.</span><span class="sxs-lookup"><span data-stu-id="1156b-147">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a trainee in the lab.</span></span> 
   
    <span data-ttu-id="1156b-148">Если обучение проводится в течение нескольких дней и нужно остановить все виртуальные машины в определенное время, а затем автоматически перезапустить их на следующий день, для этого в лаборатории нужно задать политики автоматического завершения работы и запуска.</span><span class="sxs-lookup"><span data-stu-id="1156b-148">If you are conducting multi-day training and want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="1156b-149">После завершения обучения вы можете удалить все виртуальные машины одновременно, выполнив один сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1156b-149">Finally, when training is complete you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="1156b-150">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1156b-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1156b-151">Задача</span><span class="sxs-lookup"><span data-stu-id="1156b-151">Task</span></span> | <span data-ttu-id="1156b-152">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="1156b-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1156b-153">Определение политик лаборатории</span><span class="sxs-lookup"><span data-stu-id="1156b-153">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="1156b-154">Как обеспечить контроль расходов с помощью политик в лаборатории.</span><span class="sxs-lookup"><span data-stu-id="1156b-154">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="1156b-155">Удаление всех виртуальных машин лаборатории с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="1156b-155">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="1156b-156">Как удалить все лаборатории в рамках одной операции после завершения обучения.</span><span class="sxs-lookup"><span data-stu-id="1156b-156">Delete all the labs in one operation when the training is complete.</span></span> |
5. <span data-ttu-id="1156b-157">**Предоставление доступа к лаборатории для каждого обучаемого**</span><span class="sxs-lookup"><span data-stu-id="1156b-157">**Share the lab with each trainee**</span></span>
   
    <span data-ttu-id="1156b-158">Обучаемые могут получить прямой доступ к лаборатории с помощью предоставленной им ссылки.</span><span class="sxs-lookup"><span data-stu-id="1156b-158">Labs can be directly accessed using a link that you share with your trainees.</span></span> <span data-ttu-id="1156b-159">Обучаемым с [учетной записью Майкрософт](devtest-lab-faq.md#what-is-a-microsoft-account)даже не требуется учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="1156b-159">Your trainees don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="1156b-160">Обучаемые не видят виртуальные машины, созданные другими обучаемыми.</span><span class="sxs-lookup"><span data-stu-id="1156b-160">Trainees cannot see VMs created by other trainees.</span></span>  
   
    <span data-ttu-id="1156b-161">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1156b-161">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1156b-162">Задача</span><span class="sxs-lookup"><span data-stu-id="1156b-162">Task</span></span> | <span data-ttu-id="1156b-163">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="1156b-163">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1156b-164">Добавление обучаемого в лабораторию Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1156b-164">Add a trainee to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="1156b-165">Как добавить обучаемых в учебную лабораторию с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="1156b-165">Use the Azure portal to add trainees to your training lab.</span></span> |
   | [<span data-ttu-id="1156b-166">Добавление обучаемых в лабораторию с помощью сценария PowerShell</span><span class="sxs-lookup"><span data-stu-id="1156b-166">Add trainees to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="1156b-167">Как выполнять автоматическое добавление обучаемых в учебную лабораторию с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1156b-167">Use PowerShell to automate adding trainees to your training lab.</span></span> |
   | [<span data-ttu-id="1156b-168">Получение ссылки на лабораторию</span><span class="sxs-lookup"><span data-stu-id="1156b-168">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="1156b-169">Как получить прямой доступ к лаборатории через гиперссылку.</span><span class="sxs-lookup"><span data-stu-id="1156b-169">Learn how a lab can be directly accessed via a hyperlink.</span></span> |
6. <span data-ttu-id="1156b-170">**Повторное использование учебной лаборатории**</span><span class="sxs-lookup"><span data-stu-id="1156b-170">**Reuse the lab again and again**</span></span> 
   
    <span data-ttu-id="1156b-171">Вы можете автоматизировать создание лаборатории вместе с пользовательскими параметрами, создав шаблон Resource Manager, который можно много раз использовать для создания идентичных лабораторий.</span><span class="sxs-lookup"><span data-stu-id="1156b-171">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="1156b-172">Дополнительные сведения см. по ссылкам в таблице ниже.</span><span class="sxs-lookup"><span data-stu-id="1156b-172">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1156b-173">Задача</span><span class="sxs-lookup"><span data-stu-id="1156b-173">Task</span></span> | <span data-ttu-id="1156b-174">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="1156b-174">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1156b-175">Создание лаборатории с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1156b-175">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="1156b-176">Как создать лабораторию в Azure DevTest Labs с помощью шаблона Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1156b-176">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

