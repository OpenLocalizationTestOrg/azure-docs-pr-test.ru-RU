---
title: "aaaDownload hello шаблона виртуальной машины Azure | Документы Microsoft"
description: "Загрузите hello процессадля toohelp виртуальной Машины с помощью автоматизации развертываний в модели развертывания диспетчера ресурсов hello"
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
ms.openlocfilehash: 86fd05f67409019b5e5c9023881745047860eee1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="download-hello-template-for-a-vm"></a><span data-ttu-id="c5238-103">Загрузите шаблон hello для виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="c5238-103">Download hello template for a VM</span></span>
<span data-ttu-id="c5238-104">При создании виртуальной Машины в Azure с помощью портала hello или PowerShell диспетчера ресурсов шаблона создается автоматически для вас.</span><span class="sxs-lookup"><span data-stu-id="c5238-104">When you create a VM in Azure using hello portal or PowerShell, a Resource Manager template is automatically created for you.</span></span> <span data-ttu-id="c5238-105">Можно использовать этот шаблон tooquickly дубликат развертывания.</span><span class="sxs-lookup"><span data-stu-id="c5238-105">You can use this template tooquickly duplicate a deployment.</span></span> <span data-ttu-id="c5238-106">шаблон Hello содержит сведения обо всех hello ресурсов в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5238-106">hello template contains information about all of hello resources in a resource group.</span></span> <span data-ttu-id="c5238-107">Для виртуальной машины это означает, что шаблон hello содержит все элементы, созданные для поддержки hello виртуальной Машины в этой группе ресурсов, включая hello сетевых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c5238-107">For a virtual machine, this means hello template contains everything that is created in support of hello VM in that resource group, including hello networking resources.</span></span>

## <a name="download-hello-template-using-hello-portal"></a><span data-ttu-id="c5238-108">Загрузите шаблон hello, с помощью портала hello</span><span class="sxs-lookup"><span data-stu-id="c5238-108">Download hello template using hello portal</span></span>
1. <span data-ttu-id="c5238-109">Войдите в toohello [портал Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c5238-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c5238-110">Один hello концентратора последовательно выберите пункты **виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="c5238-110">One hello hub menu, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="c5238-111">Выберите виртуальную машину hello из списка hello.</span><span class="sxs-lookup"><span data-stu-id="c5238-111">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="c5238-112">Выберите элемент **Сценарий автоматизации**.</span><span class="sxs-lookup"><span data-stu-id="c5238-112">Select **Automation script**.</span></span>
5. <span data-ttu-id="c5238-113">Выберите **загрузки** и сохранить на локальном компьютере файл .zip tooyour hello.</span><span class="sxs-lookup"><span data-stu-id="c5238-113">Select **Download** and save hello .zip file tooyour local computer.</span></span>
6. <span data-ttu-id="c5238-114">Откройте hello ZIP-файл и извлеките папки tooa файлов hello.</span><span class="sxs-lookup"><span data-stu-id="c5238-114">Open hello .zip file and extract hello files tooa folder.</span></span> <span data-ttu-id="c5238-115">Hello ZIP-файл будет содержать:</span><span class="sxs-lookup"><span data-stu-id="c5238-115">hello .zip file will contain:</span></span>
   
   * <span data-ttu-id="c5238-116">deploy.ps1;</span><span class="sxs-lookup"><span data-stu-id="c5238-116">deploy.ps1</span></span>
   * <span data-ttu-id="c5238-117">deploy.sh;</span><span class="sxs-lookup"><span data-stu-id="c5238-117">deploy.sh</span></span> 
   * <span data-ttu-id="c5238-118">deployer.rb;</span><span class="sxs-lookup"><span data-stu-id="c5238-118">deployer.rb</span></span>
   * <span data-ttu-id="c5238-119">DeploymentHelper.cs;</span><span class="sxs-lookup"><span data-stu-id="c5238-119">DeploymentHelper.cs</span></span>
   * <span data-ttu-id="c5238-120">parameters.json;</span><span class="sxs-lookup"><span data-stu-id="c5238-120">parameters.json</span></span>
   * <span data-ttu-id="c5238-121">template.json.</span><span class="sxs-lookup"><span data-stu-id="c5238-121">template.json</span></span>

<span data-ttu-id="c5238-122">файл template.json Hello — шаблон hello.</span><span class="sxs-lookup"><span data-stu-id="c5238-122">hello template.json file is hello template.</span></span>

## <a name="download-hello-template-using-powershell"></a><span data-ttu-id="c5238-123">Загрузите шаблон hello, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5238-123">Download hello template using PowerShell</span></span>
<span data-ttu-id="c5238-124">Можно также загрузить файл шаблона .json hello, с помощью hello [AzureRMResourceGroup экспорта](https://msdn.microsoft.com/library/mt715427.aspx) командлета.</span><span class="sxs-lookup"><span data-stu-id="c5238-124">You can also download hello .json template file using hello [Export-AzureRMResourceGroup](https://msdn.microsoft.com/library/mt715427.aspx) cmdlet.</span></span> <span data-ttu-id="c5238-125">Можно использовать hello `-path` параметр tooprovide hello, имя файла и путь для hello JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="c5238-125">You can use hello `-path` parameter tooprovide hello filename and path for hello .json file.</span></span> <span data-ttu-id="c5238-126">В этом примере показано, как с именем шаблона hello toodownload для группы ресурсов hello **myResourceGroup** toohello **C:\users\public\downloads** папку на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c5238-126">This example shows how toodownload hello template for hello resource group named **myResourceGroup** toohello **C:\users\public\downloads** folder on your local computer.</span></span>

```powershell
    Export-AzureRmResourceGroup -ResourceGroupName "myResourceGroup" -Path "C:\users\public\downloads"
```

## <a name="next-steps"></a><span data-ttu-id="c5238-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c5238-127">Next steps</span></span>
<span data-ttu-id="c5238-128">toolearn Дополнительные сведения о развертывании ресурсов с помощью шаблонов, в разделе [Пошаговое руководство диспетчера ресурсов шаблона](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="c5238-128">toolearn more about deploying resources using templates, see [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

