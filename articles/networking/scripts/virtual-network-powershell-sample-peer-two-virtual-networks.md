---
title: "Пример скрипта Azure PowerShell. Пиринг между двумя виртуальными сетями | Документация Майкрософт"
description: "Пример скрипта Azure PowerShell для пиринга между двумя виртуальными сетями."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 51c0b98727e148671cfd7ab2b31ffd1c705d8a4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="c0c55-103">Пиринг между двумя виртуальными сетями</span><span class="sxs-lookup"><span data-stu-id="c0c55-103">Peer two virtual networks</span></span>

<span data-ttu-id="c0c55-104">Этот скрипт создает и соединяет две виртуальные сети в одном регионе через сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="c0c55-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="c0c55-105">В результате выполнения скрипта будет создан пиринг между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="c0c55-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="c0c55-106">При необходимости установите Azure PowerShell с помощью инструкции, приведенной в [руководстве Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем выполните команду `Login-AzureRmAccount`, чтобы создать подключение к Azure.</span><span class="sxs-lookup"><span data-stu-id="c0c55-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c0c55-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="c0c55-107">Sample script</span></span>

<span data-ttu-id="c0c55-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Пиринг между двумя виртуальными сетями")]</span><span class="sxs-lookup"><span data-stu-id="c0c55-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c0c55-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="c0c55-109">Clean up deployment</span></span> 

<span data-ttu-id="c0c55-110">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c0c55-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c0c55-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="c0c55-111">Script explanation</span></span>

<span data-ttu-id="c0c55-112">Для создания группы ресурсов, виртуальной машины и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="c0c55-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="c0c55-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="c0c55-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c0c55-114">Команда</span><span class="sxs-lookup"><span data-stu-id="c0c55-114">Command</span></span> | <span data-ttu-id="c0c55-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="c0c55-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c0c55-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c0c55-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c0c55-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c0c55-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="c0c55-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="c0c55-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="c0c55-119">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="c0c55-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="c0c55-120">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="c0c55-120">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="c0c55-121">Создает пиринг между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="c0c55-121">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="c0c55-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c0c55-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c0c55-123">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="c0c55-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c0c55-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0c55-124">Next steps</span></span>

<span data-ttu-id="c0c55-125">Дополнительные сведения о Azure PowerShell см. в [документации по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c0c55-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="c0c55-126">Дополнительные примеры скриптов PowerShell для сетей см. в [обзорной документации по сетям Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c0c55-126">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>