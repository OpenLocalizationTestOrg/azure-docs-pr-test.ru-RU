---
title: "Пример сценария PowerShell - aaaAzure одноранговых две виртуальные сети | Документы Microsoft"
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
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="f0ffa-103">Пиринг между двумя виртуальными сетями</span><span class="sxs-lookup"><span data-stu-id="f0ffa-103">Peer two virtual networks</span></span>

<span data-ttu-id="f0ffa-104">Этот скрипт создается и выполняется подключение двух виртуальных сетей в hello hello trhough того же региона сети Azure.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="f0ffa-105">После выполнения сценария hello, вы создадите пиринг между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="f0ffa-106">При необходимости установите Azure PowerShell с помощью инструкции hello, найденные в hello hello [руководство по Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), а затем запустите `Login-AzureRmAccount` toocreate соединения с Azure.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f0ffa-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="f0ffa-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f0ffa-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="f0ffa-108">Clean up deployment</span></span> 

<span data-ttu-id="f0ffa-109">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f0ffa-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="f0ffa-110">Script explanation</span></span>

<span data-ttu-id="f0ffa-111">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="f0ffa-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f0ffa-113">Команда</span><span class="sxs-lookup"><span data-stu-id="f0ffa-113">Command</span></span> | <span data-ttu-id="f0ffa-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="f0ffa-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f0ffa-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f0ffa-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f0ffa-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="f0ffa-117">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f0ffa-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="f0ffa-118">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="f0ffa-119">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="f0ffa-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="f0ffa-120">Создает пиринг между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="f0ffa-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f0ffa-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f0ffa-122">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="f0ffa-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0ffa-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f0ffa-123">Next steps</span></span>

<span data-ttu-id="f0ffa-124">Дополнительные сведения о hello Azure PowerShell см. в разделе [документация по Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0ffa-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="f0ffa-125">Дополнительные сетевые образцы сценариев PowerShell можно найти в hello [документации Azure Общие сведения о сети](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0ffa-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
