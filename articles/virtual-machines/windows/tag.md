---
title: "aaaHow tootag ресурс виртуальной Машины Windows в Azure | Документы Microsoft"
description: "Дополнительные сведения о виртуальной машине Windows, созданные в Azure с помощью модели развертывания диспетчера ресурсов hello тегов"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="98d37-103">Как tootag виртуальной машине в Azure</span><span class="sxs-lookup"><span data-stu-id="98d37-103">How tootag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="98d37-104">Этой статье описываются различные способы tootag виртуальной машине в Azure через hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="98d37-104">This article describes different ways tootag a Windows virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="98d37-105">Теги — это определяемые пользователем пары "ключ-значение", которые можно помещать непосредственно в ресурс или группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="98d37-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="98d37-106">В настоящее время Azure поддерживает теги too15 каждого ресурса и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="98d37-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="98d37-107">Теги можно поместить в ресурс во время создания hello или добавлены tooan существующий ресурс.</span><span class="sxs-lookup"><span data-stu-id="98d37-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="98d37-108">Обратите внимание, что теги поддерживаются для ресурсов, созданные с помощью модели развертывания диспетчера ресурсов hello только.</span><span class="sxs-lookup"><span data-stu-id="98d37-108">Please note that tags are supported for resources created via hello Resource Manager deployment model only.</span></span> <span data-ttu-id="98d37-109">Если tootag виртуальной машины Linux, см. [как tootag виртуальной машины Linux в Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="98d37-109">If you want tootag a Linux virtual machine, see [How tootag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="98d37-110">Маркировка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="98d37-110">Tagging with PowerShell</span></span>
<span data-ttu-id="98d37-111">toocreate, добавление и удаление тегов с помощью PowerShell, сначала необходимо tooset вверх к [среды PowerShell с помощью диспетчера ресурсов Azure][PowerShell environment with Azure Resource Manager].</span><span class="sxs-lookup"><span data-stu-id="98d37-111">toocreate, add, and delete tags through PowerShell, you first need tooset up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="98d37-112">После завершения установки hello теги можно разместить на вычисления, сети и хранилища ресурсов при создании или после создания ресурса hello через PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98d37-112">Once you have completed hello setup, you can place tags on Compute, Network, and Storage resources at creation or after hello resource is created via PowerShell.</span></span> <span data-ttu-id="98d37-113">Эта статья в основном посвящена просмотру и редактированию тегов виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="98d37-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="98d37-114">Во-первых, перейдите tooa виртуальной машины через hello `Get-AzureRmVM` командлета.</span><span class="sxs-lookup"><span data-stu-id="98d37-114">First, navigate tooa Virtual Machine through hello `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="98d37-115">Если виртуальная машина уже содержит теги, вы увидите все теги hello для ресурса:</span><span class="sxs-lookup"><span data-stu-id="98d37-115">If your Virtual Machine already contains tags, you will then see all hello tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="98d37-116">Если вы хотите tooadd теги с помощью PowerShell, можно использовать hello `Set-AzureRmResource` команды.</span><span class="sxs-lookup"><span data-stu-id="98d37-116">If you would like tooadd tags through PowerShell, you can use hello `Set-AzureRmResource` command.</span></span> <span data-ttu-id="98d37-117">Обратите внимание, что при изменении тегов с помощью PowerShell обновляются все теги.</span><span class="sxs-lookup"><span data-stu-id="98d37-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="98d37-118">Поэтому при добавлении один ресурс tooa тег, который уже имеет теги, необходимо будет tooinclude все теги hello, которые нужно разместить на ресурс hello toobe.</span><span class="sxs-lookup"><span data-stu-id="98d37-118">So if you are adding one tag tooa resource that already has tags, you will need tooinclude all hello tags that you want toobe placed on hello resource.</span></span> <span data-ttu-id="98d37-119">Ниже приведен пример как tooadd дополнительные теги tooa ресурса с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="98d37-119">Below is an example of how tooadd additional tags tooa resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="98d37-120">Этот первый командлет задает все теги hello разместить на *MyTestVM* toohello *$tags* переменной, используя hello `Get-AzureRmResource` и `Tags` свойства.</span><span class="sxs-lookup"><span data-stu-id="98d37-120">This first cmdlet sets all of hello tags placed on *MyTestVM* toohello *$tags* variable, using hello `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="98d37-121">Вторая команда Hello отображает hello теги для hello, заданному переменной.</span><span class="sxs-lookup"><span data-stu-id="98d37-121">hello second command displays hello tags for hello given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="98d37-122">Третья команда Hello добавляет дополнительный тег toohello *$tags* переменной.</span><span class="sxs-lookup"><span data-stu-id="98d37-122">hello third command adds an additional tag toohello *$tags* variable.</span></span> <span data-ttu-id="98d37-123">Обратите внимание на использование hello hello  **+=**  tooappend hello новый toohello пары ключ значение *$tags* списка.</span><span class="sxs-lookup"><span data-stu-id="98d37-123">Note hello use of hello **+=** tooappend hello new key/value pair toohello *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="98d37-124">Четвертая команда Hello задает все теги hello, определенные в hello *$tags* переменных toohello заданного ресурса.</span><span class="sxs-lookup"><span data-stu-id="98d37-124">hello fourth command sets all of hello tags defined in hello *$tags* variable toohello given resource.</span></span> <span data-ttu-id="98d37-125">В нашем примере это MyTestVM.</span><span class="sxs-lookup"><span data-stu-id="98d37-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="98d37-126">Hello пятая команда отображает все теги hello hello ресурса.</span><span class="sxs-lookup"><span data-stu-id="98d37-126">hello fifth command displays all of hello tags on hello resource.</span></span> <span data-ttu-id="98d37-127">Как видите, *расположение* определен как тег *MyLocation* как значение hello.</span><span class="sxs-lookup"><span data-stu-id="98d37-127">As you can see, *Location* is now defined as a tag with *MyLocation* as hello value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="98d37-128">Дополнительные сведения о toolearn тегов с помощью PowerShell извлекать hello [командлеты ресурса Azure][Azure Resource Cmdlets].</span><span class="sxs-lookup"><span data-stu-id="98d37-128">toolearn more about tagging through PowerShell, check out hello [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="98d37-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="98d37-129">Next steps</span></span>
* <span data-ttu-id="98d37-130">toolearn Дополнительные сведения о тегов ресурсам Azure в разделе [Обзор диспетчера ресурсов Azure] [ Azure Resource Manager Overview] и [tooorganize с помощью тегов ресурсов Azure] [ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="98d37-130">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="98d37-131">toosee теги помогают управлять использование ресурсов Azure разделе [основные сведения о счете Azure] [ Understanding your Azure Bill] и [анализировать потребления ресурсов Microsoft Azure] [Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="98d37-131">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
