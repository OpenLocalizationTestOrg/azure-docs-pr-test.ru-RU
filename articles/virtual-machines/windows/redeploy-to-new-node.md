---
title: "aaaRedeploy виртуальных машинах в Azure | Документы Microsoft"
description: "Как проблемы tooredeploy виртуальных машинах в Azure toomitigate RDP-подключение."
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
ms.openlocfilehash: 903d9d5bf241075931ee4b746690c553d808a58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-windows-virtual-machine-toonew-azure-node"></a><span data-ttu-id="509bb-103">Повторное развертывание Windows виртуальной машины toonew узла Azure</span><span class="sxs-lookup"><span data-stu-id="509bb-103">Redeploy Windows virtual machine toonew Azure node</span></span>
<span data-ttu-id="509bb-104">Если направлена трудностей Устранение неполадок удаленного рабочего стола (RDP) подключения или приложения доступ к tooWindows Azure виртуальной машины (VM), повторное развертывание виртуальной Машины может помочь приветствия.</span><span class="sxs-lookup"><span data-stu-id="509bb-104">If you have been facing difficulties troubleshooting Remote Desktop (RDP) connection or application access tooWindows-based Azure virtual machine (VM), redeploying hello VM may help.</span></span> <span data-ttu-id="509bb-105">При повторном развертывании виртуальной Машины, он перемещает новый узел hello ВМ tooa внутри hello инфраструктуры Azure и лежащих в основе обратно на, сохраняя все параметры конфигурации и связанных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="509bb-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on, retaining all your configuration options and associated resources.</span></span> <span data-ttu-id="509bb-106">В этой статье показано, как tooredeploy в виртуальную Машину с помощью Azure PowerShell или портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="509bb-106">This article shows you how tooredeploy a VM using Azure PowerShell or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="509bb-107">После повторного развертывания виртуальной Машины, теряется временный диск hello и обновляются динамические IP-адреса, связанные с виртуального сетевого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="509bb-107">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 


## <a name="using-azure-powershell"></a><span data-ttu-id="509bb-108">Использование Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="509bb-108">Using Azure PowerShell</span></span>
<span data-ttu-id="509bb-109">Убедитесь, что у hello последнюю версию Azure PowerShell 1.x, установлены на компьютере.</span><span class="sxs-lookup"><span data-stu-id="509bb-109">Make sure you have hello latest Azure PowerShell 1.x installed on your machine.</span></span> <span data-ttu-id="509bb-110">Дополнительные сведения см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="509bb-110">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="509bb-111">Hello следующий пример выполняет развертывание виртуальной Машины с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="509bb-111">hello following example deploys hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Set-AzureRmVM -Redeploy -ResourceGroupName "myResourceGroup" -Name "myVM"
```


[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="509bb-112">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="509bb-112">Next steps</span></span>
<span data-ttu-id="509bb-113">Если возникли проблемы с подключением tooyour виртуальной Машины, можно найти справку на [Устранение неполадок подключений по протоколу RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) или [подробные шаги по устранению неполадок протокола удаленного рабочего СТОЛА](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="509bb-113">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting RDP connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [detailed RDP troubleshooting steps](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="509bb-114">При проблемах с доступом к приложению, выполняющемуся в виртуальной машине, ознакомьтесь со статьей [Устранение неполадок доступа к приложению, выполняющемуся в виртуальной машине Azure](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="509bb-114">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

