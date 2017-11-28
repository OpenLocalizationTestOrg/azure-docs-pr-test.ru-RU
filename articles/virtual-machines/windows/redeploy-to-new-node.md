---
title: "Повторное развертывание виртуальных машин Windows в Azure | Документация Майкрософт"
description: "Повторное развертывание виртуальных машин Windows в Azure для устранения проблем с подключением к удаленному рабочему столу."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: genlin
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: 0ee456ee-4595-4a14-8916-72c9110fc8bd
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: a607d0747f64ee6b224d300113905f54e003aef0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-windows-virtual-machine-to-new-azure-node"></a><span data-ttu-id="2dabb-103">Повторное развертывание виртуальной машины Windows на новом узле Azure</span><span class="sxs-lookup"><span data-stu-id="2dabb-103">Redeploy Windows virtual machine to new Azure node</span></span>
<span data-ttu-id="2dabb-104">Если вам не удается подключиться к удаленному рабочему столу или получить доступ к приложению на виртуальной машине Windows Azure, можно попробовать повторно развернуть виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="2dabb-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access to Windows-based Azure virtual machine (VM), redeploying the VM may help.</span></span> <span data-ttu-id="2dabb-105">При повторном развертывании виртуальная машина перемещается на новый узел в рамках инфраструктуры Azure. Там она снова включается с сохранением всех параметров конфигурации и связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2dabb-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="2dabb-106">В этой статье показано, как повторно развернуть виртуальную машину с помощью Azure PowerShell или портала Azure.</span><span class="sxs-lookup"><span data-stu-id="2dabb-106">This article shows you how to redeploy a VM using Azure PowerShell or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="2dabb-107">После развертывания временный диск будет удален, а связанные с виртуальным сетевым интерфейсом динамические IP-адреса будут обновлены.</span><span class="sxs-lookup"><span data-stu-id="2dabb-107">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="2dabb-108">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dabb-108">Using Azure PowerShell</span></span>
<span data-ttu-id="2dabb-109">Убедитесь, что на компьютере установлена последняя версия Azure PowerShell 1.x.</span><span class="sxs-lookup"><span data-stu-id="2dabb-109">Make sure you have the latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="2dabb-110">Дополнительные сведения см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2dabb-110">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="2dabb-111">В следующем примере развертывается виртуальная машина `myVM` в группе ресурсов `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="2dabb-111">The following example deploys the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="2dabb-112">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2dabb-112">Next steps</span></span>
<span data-ttu-id="2dabb-113">При проблемах с подключением к виртуальной машине ознакомьтесь со статьями [Устранение неполадок с подключением к удаленному рабочему столу на виртуальной машине Azure под управлением Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [Подробная диагностика подключений к удаленному рабочему столу виртуальной машины Azure под управлением Windows](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2dabb-113">If you are having issues connecting to your VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="2dabb-114">При проблемах с доступом к приложению, выполняющемуся на виртуальной машине, ознакомьтесь со статьей [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2dabb-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

