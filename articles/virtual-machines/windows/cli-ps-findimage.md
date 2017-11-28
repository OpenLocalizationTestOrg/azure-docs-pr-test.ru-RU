---
title: "образы aaaSelect виртуальной Машины Windows в Azure | Документы Microsoft"
description: "Узнайте, как Azure PowerSHell toodetermine toouse hello издателя, предложение, SKU и версия для образов виртуальных Машин Marketplace."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 188b8974-fabd-4cd3-b7dc-559cbb86b98a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 752edcd0935f5141832e49503ae800ea0145e219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-windows-vm-images-in-hello-azure-marketplace-with-azure-powershell"></a><span data-ttu-id="9fcea-103">Как образы toofind виртуальной Машины Windows в Azure Marketplace с помощью Azure PowerShell hello</span><span class="sxs-lookup"><span data-stu-id="9fcea-103">How toofind Windows VM images in hello Azure Marketplace with Azure PowerShell</span></span>

<span data-ttu-id="9fcea-104">В этом разделе описывается, как образы Azure PowerShell toouse toofind виртуальной Машины в Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="9fcea-104">This topic describes how toouse Azure PowerShell toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="9fcea-105">Используйте этот сведения toospecify образа Marketplace при создании виртуальной Машины Windows.</span><span class="sxs-lookup"><span data-stu-id="9fcea-105">Use this information toospecify a Marketplace image when you create a Windows VM.</span></span>

<span data-ttu-id="9fcea-106">Убедитесь, что установлен и настроен hello последней [модуля Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="9fcea-106">Make sure that you installed and configured hello latest [Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>



## <a name="table-of-commonly-used-windows-images"></a><span data-ttu-id="9fcea-107">Таблица часто используемых образов Windows</span><span class="sxs-lookup"><span data-stu-id="9fcea-107">Table of commonly used Windows images</span></span>
| <span data-ttu-id="9fcea-108">PublisherName</span><span class="sxs-lookup"><span data-stu-id="9fcea-108">PublisherName</span></span> | <span data-ttu-id="9fcea-109">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="9fcea-109">Offer</span></span> | <span data-ttu-id="9fcea-110">Sku</span><span class="sxs-lookup"><span data-stu-id="9fcea-110">Sku</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="9fcea-111">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-111">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9fcea-112">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-112">WindowsServer</span></span> |<span data-ttu-id="9fcea-113">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="9fcea-113">2016-Datacenter</span></span> |
| <span data-ttu-id="9fcea-114">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-114">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9fcea-115">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-115">WindowsServer</span></span> |<span data-ttu-id="9fcea-116">2016-Datacenter-Server-Core</span><span class="sxs-lookup"><span data-stu-id="9fcea-116">2016-Datacenter-Server-Core</span></span> |
| <span data-ttu-id="9fcea-117">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-117">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9fcea-118">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-118">WindowsServer</span></span> |<span data-ttu-id="9fcea-119">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="9fcea-119">2016-Datacenter-with-Containers</span></span> |
| <span data-ttu-id="9fcea-120">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-120">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9fcea-121">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-121">WindowsServer</span></span> |<span data-ttu-id="9fcea-122">2016-Nano-Server</span><span class="sxs-lookup"><span data-stu-id="9fcea-122">2016-Nano-Server</span></span> |
| <span data-ttu-id="9fcea-123">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-123">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9fcea-124">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-124">WindowsServer</span></span> |<span data-ttu-id="9fcea-125">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="9fcea-125">2012-R2-Datacenter</span></span> |
| <span data-ttu-id="9fcea-126">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-126">MicrosoftWindowsServer</span></span> |<span data-ttu-id="9fcea-127">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-127">WindowsServer</span></span> |<span data-ttu-id="9fcea-128">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="9fcea-128">2008-R2-SP1</span></span> |
| <span data-ttu-id="9fcea-129">MicrosoftDynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="9fcea-129">MicrosoftDynamicsNAV</span></span> |<span data-ttu-id="9fcea-130">DynamicsNAV</span><span class="sxs-lookup"><span data-stu-id="9fcea-130">DynamicsNAV</span></span> |<span data-ttu-id="9fcea-131">2017</span><span class="sxs-lookup"><span data-stu-id="9fcea-131">2017</span></span> |
| <span data-ttu-id="9fcea-132">MicrosoftSharePoint</span><span class="sxs-lookup"><span data-stu-id="9fcea-132">MicrosoftSharePoint</span></span> |<span data-ttu-id="9fcea-133">MicrosoftSharePointServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-133">MicrosoftSharePointServer</span></span> |<span data-ttu-id="9fcea-134">2016</span><span class="sxs-lookup"><span data-stu-id="9fcea-134">2016</span></span> |
| <span data-ttu-id="9fcea-135">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-135">MicrosoftSQLServer</span></span> |<span data-ttu-id="9fcea-136">SQL2016-WS2016</span><span class="sxs-lookup"><span data-stu-id="9fcea-136">SQL2016-WS2016</span></span> |<span data-ttu-id="9fcea-137">Enterprise</span><span class="sxs-lookup"><span data-stu-id="9fcea-137">Enterprise</span></span> |
| <span data-ttu-id="9fcea-138">MicrosoftSQLServer</span><span class="sxs-lookup"><span data-stu-id="9fcea-138">MicrosoftSQLServer</span></span> |<span data-ttu-id="9fcea-139">SQL2014SP2-WS2012R2</span><span class="sxs-lookup"><span data-stu-id="9fcea-139">SQL2014SP2-WS2012R2</span></span> |<span data-ttu-id="9fcea-140">Enterprise</span><span class="sxs-lookup"><span data-stu-id="9fcea-140">Enterprise</span></span> |
| <span data-ttu-id="9fcea-141">MicrosoftWindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="9fcea-141">MicrosoftWindowsServerHPCPack</span></span> |<span data-ttu-id="9fcea-142">WindowsServerHPCPack</span><span class="sxs-lookup"><span data-stu-id="9fcea-142">WindowsServerHPCPack</span></span> |<span data-ttu-id="9fcea-143">2012R2</span><span class="sxs-lookup"><span data-stu-id="9fcea-143">2012R2</span></span> |
| <span data-ttu-id="9fcea-144">MicrosoftWindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="9fcea-144">MicrosoftWindowsServerEssentials</span></span> |<span data-ttu-id="9fcea-145">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="9fcea-145">WindowsServerEssentials</span></span> |<span data-ttu-id="9fcea-146">WindowsServerEssentials</span><span class="sxs-lookup"><span data-stu-id="9fcea-146">WindowsServerEssentials</span></span> |

## <a name="find-specific-images"></a><span data-ttu-id="9fcea-147">Поиск определенных образов</span><span class="sxs-lookup"><span data-stu-id="9fcea-147">Find specific images</span></span>


<span data-ttu-id="9fcea-148">При создании новой виртуальной машины с помощью диспетчера ресурсов Azure, в некоторых случаях требуется toospecify изображения с сочетанием hello hello следующие свойства изображения:</span><span class="sxs-lookup"><span data-stu-id="9fcea-148">When creating a new virtual machine with Azure Resource Manager, in some cases you need toospecify an image with hello combination of hello following image properties:</span></span>

* <span data-ttu-id="9fcea-149">Издатель</span><span class="sxs-lookup"><span data-stu-id="9fcea-149">Publisher</span></span>
* <span data-ttu-id="9fcea-150">ПРЕДЛОЖЕНИЕ</span><span class="sxs-lookup"><span data-stu-id="9fcea-150">Offer</span></span>
* <span data-ttu-id="9fcea-151">SKU</span><span class="sxs-lookup"><span data-stu-id="9fcea-151">SKU</span></span>

<span data-ttu-id="9fcea-152">Например, использовать эти значения с hello [AzureRMVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage) командлета PowerShell или с помощью шаблона группы ресурсов, в котором необходимо указать тип hello toobe виртуальная машина создана.</span><span class="sxs-lookup"><span data-stu-id="9fcea-152">For example, use these values with hello [Set-AzureRMVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) PowerShell cmdlet, or with a resource group template in which you must specify hello type of VM toobe created.</span></span>

<span data-ttu-id="9fcea-153">Если вам требуется toodetermine эти значения, можно запустить hello [Get AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), и [Get AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) командлетов toonavigate hello изображения.</span><span class="sxs-lookup"><span data-stu-id="9fcea-153">If you need toodetermine these values, you can run hello [Get-AzureRMVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher), [Get-AzureRMVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer), and [Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) cmdlets toonavigate hello images.</span></span> <span data-ttu-id="9fcea-154">Определите эти значения:</span><span class="sxs-lookup"><span data-stu-id="9fcea-154">You determine these values:</span></span>

1. <span data-ttu-id="9fcea-155">Список hello изображения издателей.</span><span class="sxs-lookup"><span data-stu-id="9fcea-155">List hello image publishers.</span></span>
2. <span data-ttu-id="9fcea-156">Получить список предложений нужного издателя.</span><span class="sxs-lookup"><span data-stu-id="9fcea-156">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="9fcea-157">Получить список номеров SKU для требуемого предложения.</span><span class="sxs-lookup"><span data-stu-id="9fcea-157">For a given offer, list their SKUs.</span></span>

<span data-ttu-id="9fcea-158">Во-первых список издателей hello с hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="9fcea-158">First, list hello publishers with hello following commands:</span></span>

```powershell
$locName="<Azure location, such as West US>"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName
```

<span data-ttu-id="9fcea-159">Введите свое имя выбранного издателя и выполните hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="9fcea-159">Fill in your chosen publisher name and run hello following commands:</span></span>

```powershell
$pubName="<publisher>"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="9fcea-160">Введите свое имя выбранного предложения и выполните следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="9fcea-160">Fill in your chosen offer name and run hello following commands:</span></span>

```powershell
$offerName="<offer>"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="9fcea-161">Из вывода hello hello `Get-AzureRMVMImageSku` команды, у вас есть все hello сведения toospecify hello изображения для новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9fcea-161">From hello output of hello `Get-AzureRMVMImageSku` command, you have all hello information you need toospecify hello image for a new virtual machine.</span></span>

<span data-ttu-id="9fcea-162">Hello ниже приведен полный пример:</span><span class="sxs-lookup"><span data-stu-id="9fcea-162">hello following shows a full example:</span></span>

```powershell
$locName="West US"
Get-AzureRMVMImagePublisher -Location $locName | Select PublisherName

```

<span data-ttu-id="9fcea-163">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9fcea-163">Output:</span></span>

```
PublisherName
-------------
a10networks
aiscaler-cache-control-ddos-and-url-rewriting-
alertlogic
AlertLogic.Extension
Barracuda.Azure.ConnectivityAgent
barracudanetworks
basho
boxless
bssw
Canonical
...
```

<span data-ttu-id="9fcea-164">Для издателя «MicrosoftWindowsServer» hello:</span><span class="sxs-lookup"><span data-stu-id="9fcea-164">For hello "MicrosoftWindowsServer" publisher:</span></span>

```powershell
$pubName="MicrosoftWindowsServer"
Get-AzureRMVMImageOffer -Location $locName -Publisher $pubName | Select Offer
```

<span data-ttu-id="9fcea-165">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9fcea-165">Output:</span></span>

```
Offer
-----
Windows-HUB
WindowsServer
WindowsServer-HUB
```

<span data-ttu-id="9fcea-166">Для предложения «WindowsServer» hello:</span><span class="sxs-lookup"><span data-stu-id="9fcea-166">For hello "WindowsServer" offer:</span></span>

```powershell
$offerName="WindowsServer"
Get-AzureRMVMImageSku -Location $locName -Publisher $pubName -Offer $offerName | Select Skus
```

<span data-ttu-id="9fcea-167">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9fcea-167">Output:</span></span>

```
Skus
----
2008-R2-SP1
2008-R2-SP1-smalldisk
2012-Datacenter
2012-Datacenter-smalldisk
2012-R2-Datacenter
2012-R2-Datacenter-smalldisk
2016-Datacenter
2016-Datacenter-Server-Core
2016-Datacenter-Server-Core-smalldisk
2016-Datacenter-smalldisk
2016-Datacenter-with-Containers
2016-Nano-Server
```

<span data-ttu-id="9fcea-168">Из этого списка, скопируйте hello выбранный номер SKU, и у вас есть все сведения о hello для hello `Set-AzureRMVMSourceImage` командлета PowerShell или для шаблона группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9fcea-168">From this list, copy hello chosen SKU name, and you have all hello information for hello `Set-AzureRMVMSourceImage` PowerShell cmdlet or for a resource group template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fcea-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fcea-169">Next steps</span></span>
<span data-ttu-id="9fcea-170">Теперь вы можете точно hello образа необходимо toouse.</span><span class="sxs-lookup"><span data-stu-id="9fcea-170">Now you can choose precisely hello image you want toouse.</span></span> <span data-ttu-id="9fcea-171">. в разделе виртуальной машины быстро с помощью информации об изображении hello, который только что найден toocreate [Создание виртуальной машины Windows с помощью PowerShell](quick-create-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9fcea-171">toocreate a virtual machine quickly by using hello image information, which you just found, see [Create a Windows virtual machine with PowerShell](quick-create-powershell.md).</span></span>
