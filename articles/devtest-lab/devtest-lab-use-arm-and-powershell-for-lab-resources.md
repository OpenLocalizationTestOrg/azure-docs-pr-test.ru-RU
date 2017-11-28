---
title: "aaaCreate или изменить labs, автоматически, используя шаблоны Azure Resource Manager с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как шаблоны Azure Resource Manager toouse с PowerShell toocreate или изменить labs автоматически в лаборатории DevTest"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="36290-103">Автоматическое создание и изменение лабораторий помощью шаблонов Azure Resource Manager и PowerShell</span><span class="sxs-lookup"><span data-stu-id="36290-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="36290-104">DevTest Labs предоставляет множество шаблонов Azure Resource Manager и сценариев PowerShell, которые позволяют быстро и автоматически создавать новые или изменять существующие лаборатории и затем развертывать эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="36290-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="36290-105">Эта статья поможет hello процесс использования этих шаблонов и сценариев создания tooautomate hello, изменения и развертывания лабораториях.</span><span class="sxs-lookup"><span data-stu-id="36290-105">This article helps guide you through hello process of using these templates and scripts tooautomate hello creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="36290-106">В этой статье также показано, где можно найти дополнительные сведения о том, как toouse PowerShell tooperform некоторые наиболее распространенные задачи в DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="36290-106">This article also shows you where you can find more information about how toouse PowerShell tooperform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="36290-107">Шаг 1. Сбор шаблонов и сценариев</span><span class="sxs-lookup"><span data-stu-id="36290-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="36290-108">Вы можете найти готовые [шаблоны Azure Resource Manager](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) и [сценарии PowerShell](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) в нашем общедоступном [репозитории Github](https://github.com/Azure/azure-devtestlab).</span><span class="sxs-lookup"><span data-stu-id="36290-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="36290-109">Используйте их в исходном виде или настраивайте их и сохраняйте в своем [частном репозитории Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="36290-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="36290-110">Шаг 2. Изменение шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="36290-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="36290-111">Можно выполнить инструкции раздела hello [создание первого шаблона диспетчера ресурсов Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) Если не был создан шаблон до.</span><span class="sxs-lookup"><span data-stu-id="36290-111">You can follow hello steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span></span>

<span data-ttu-id="36290-112">Кроме того [советы и рекомендации по созданию шаблонов диспетчера ресурсов Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) предлагает множество toohelp указания и рекомендации, создание шаблонов диспетчера ресурсов Azure, надежное и легко toouse.</span><span class="sxs-lookup"><span data-stu-id="36290-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions toohelp you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="36290-113">Как правило используется один из подходов hello разновидность или примеры исключительно и изменить шаблон вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="36290-113">Typically, you will use a variation of one of hello approaches or examples provided and modify your template for your needs.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="36290-114">Шаг 3. Развертывание ресурсов с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="36290-114">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="36290-115">После настройки шаблонов и сценариев, выполните необходимые действия hello слишком[развертывания ресурсов с помощью шаблонов диспетчера ресурсов и Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="36290-115">After you have customized your templates and scripts, follow hello steps necessary too[deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="36290-116">Hello статья содержит общие сведения об использовании Azure PowerShell с toodeploy шаблоны Azure Resource Manager вашей tooAzure ресурсов.</span><span class="sxs-lookup"><span data-stu-id="36290-116">hello article provides general information about using Azure PowerShell with Azure Resource Manager templates toodeploy your resources tooAzure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="36290-117">Общие задачи, которые можно выполнять в DevTest Labs с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="36290-117">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="36290-118">Существует множество других распространенных задач, которые можно автоматизировать с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36290-118">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="36290-119">Hello в следующих разделах документации hello структуры tooperform необходимые шаги hello этих задач.</span><span class="sxs-lookup"><span data-stu-id="36290-119">hello following sections of hello documentation outline hello steps required tooperform these tasks.</span></span>

* [<span data-ttu-id="36290-120">Создание пользовательского образа из VHD-файла с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="36290-120">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="36290-121">Отправка VHD файл toolab учетной записи хранилища с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="36290-121">Upload VHD file toolab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="36290-122">Добавить лаборатории tooa внешнего пользователя, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="36290-122">Add an external user tooa lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="36290-123">Создание пользовательской роли лаборатории с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="36290-123">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="36290-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="36290-124">Next steps</span></span>
* <span data-ttu-id="36290-125">Узнайте, как toocreate [закрытом репозитории Git](devtest-lab-add-artifact-repo.md) для хранения настраиваемых шаблонов или сценарии.</span><span class="sxs-lookup"><span data-stu-id="36290-125">Learn how toocreate a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="36290-126">Просмотр hello [шаблоны диспетчера ресурсов Azure из коллекции шаблонов быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="36290-126">Explore hello [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
