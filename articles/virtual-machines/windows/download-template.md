---
title: "Скачивание шаблона для виртуальной машины Azure | Документация Майкрософт"
description: "Автоматизация развертываний в модели развертывания с помощью Resource Manager с использованием скачанного шаблона для виртуальной машины."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 51ef4f51-0942-4249-afea-4a3f87ce1ff8
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 9e4c0c3cf0e233447369a24b1d5fe27495abd1cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="download-the-template-for-a-vm"></a><span data-ttu-id="464e4-103">Скачивание шаблона для виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="464e4-103">Download the template for a VM</span></span>
<span data-ttu-id="464e4-104">При создании виртуальной машины в Azure с помощью портала или PowerShell автоматически создается шаблон Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="464e4-104">When you create a VM in Azure using the portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="464e4-105">Этот шаблон можно использовать для быстрого дублирования развертывания.</span><span class="sxs-lookup"><span data-stu-id="464e4-105">You can use this template to quickly duplicate a deployment.</span></span> <span data-ttu-id="464e4-106">Шаблон содержит сведения обо всех ресурсах в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="464e4-106">The template contains information about all of the resources in a resource group.</span></span> <span data-ttu-id="464e4-107">Для виртуальной машины это означает, что шаблон содержит все, что создается для поддержки виртуальных машин в этой группе ресурсов, включая сетевые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="464e4-107">For a virtual machine, this means the template contains everything that is created in support of the VM in that resource group, including the networking resources.</span></span>

## <a name="download-the-template-using-the-portal"></a><span data-ttu-id="464e4-108">Скачивание шаблона с помощью портала</span><span class="sxs-lookup"><span data-stu-id="464e4-108">Download the template using the portal</span></span>
1. <span data-ttu-id="464e4-109">Войдите на [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="464e4-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="464e4-110">В главном меню выберите **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="464e4-110">One the hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="464e4-111">Затем выберите виртуальную машину из списка.</span><span class="sxs-lookup"><span data-stu-id="464e4-111">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="464e4-112">Выберите элемент **Сценарий автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="464e4-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="464e4-113">Выберите **Скачать** и сохраните ZIP-файл на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="464e4-113">Select **Download** and save the .zip file to your local computer.</span></span>
6. <span data-ttu-id="464e4-114">Откройте ZIP-файл и извлеките файлы в папку.</span><span class="sxs-lookup"><span data-stu-id="464e4-114">Open the .zip file and extract the files to a folder.</span></span> <span data-ttu-id="464e4-115">ZIP-файл будет содержать такие файлы:</span><span class="sxs-lookup"><span data-stu-id="464e4-115">The .zip file will contain:</span></span>
   
   * <span data-ttu-id="464e4-116">deploy.ps1;</span><span class="sxs-lookup"><span data-stu-id="464e4-116">deploy.ps1</span></span>
   * <span data-ttu-id="464e4-117">deploy.sh;</span><span class="sxs-lookup"><span data-stu-id="464e4-117">deploy.sh</span></span> 
   * <span data-ttu-id="464e4-118">deployer.rb;</span><span class="sxs-lookup"><span data-stu-id="464e4-118">deployer.rb</span></span>
   * <span data-ttu-id="464e4-119">DeploymentHelper.cs;</span><span class="sxs-lookup"><span data-stu-id="464e4-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="464e4-120">parameters.json;</span><span class="sxs-lookup"><span data-stu-id="464e4-120">parameters.json</span></span>
   * <span data-ttu-id="464e4-121">template.json.</span><span class="sxs-lookup"><span data-stu-id="464e4-121">template.json</span></span>

<span data-ttu-id="464e4-122">Файл template.json является шаблоном.</span><span class="sxs-lookup"><span data-stu-id="464e4-122">The template.json file is the template.</span></span>

## <a name="download-the-template-using-powershell"></a><span data-ttu-id="464e4-123">Скачивание шаблона с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="464e4-123">Download the template using PowerShell</span></span>
<span data-ttu-id="464e4-124">JSON-файл шаблона можно также скачать с помощью командлета [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx).</span><span class="sxs-lookup"><span data-stu-id="464e4-124">You can also download the .json template file using the [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="464e4-125">Имя файла и путь к JSON-файлу можно указать с помощью параметра `-path`.</span><span class="sxs-lookup"><span data-stu-id="464e4-125">You can use the `-path` parameter to provide the filename and path for the .json file.</span></span> <span data-ttu-id="464e4-126">В этом примере показано, как скачать шаблон для группы ресурсов с именем **myResourceGroup** в папку **C:\users\public\downloads** на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="464e4-126">This example shows how to download the template for the resource group named **myResourceGroup** to the **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="464e4-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="464e4-127">Next steps</span></span>
<span data-ttu-id="464e4-128">Дополнительные сведения о развертывании ресурсов с помощью шаблонов см. в статье [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md) (Пошаговое руководство по шаблону Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="464e4-128">To learn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

