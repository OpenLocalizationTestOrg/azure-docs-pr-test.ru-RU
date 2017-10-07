---
title: "aaaMove (классические) виртуальной Машины или облачные службы роли экземпляра tooa другой подсети - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toomove виртуальные машины (классические) и облачные службы роли экземпляров tooa другой подсети, с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: de4135c7-dc5b-4ffa-84cc-1b8364b7b427
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c8d2de56f42a91be4a665414ea9641ffd46588fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-vm-classic-or-cloud-services-role-instance-tooa-different-subnet-using-powershell"></a><span data-ttu-id="3b09d-103">Перемещение виртуальной Машины (классические) или облачные службы роли экземпляра tooa другой подсети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b09d-103">Move a VM (Classic) or Cloud Services role instance tooa different subnet using PowerShell</span></span>
<span data-ttu-id="3b09d-104">В можно использовать PowerShell toomove виртуальные машины (классические) из одной подсети tooanother hello одной виртуальной сети (VNet).</span><span class="sxs-lookup"><span data-stu-id="3b09d-104">You can use PowerShell toomove your VMs (Classic) from one subnet tooanother in hello same virtual network (VNet).</span></span> <span data-ttu-id="3b09d-105">Экземпляры роли можно перемещать путем редактирования файла CSCFG hello, а не с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b09d-105">Role instances can be moved by editing hello CSCFG file, rather than using PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="3b09d-106">В этой статье объясняется, как развернутые виртуальные машины toomove с помощью hello классической модели развертывания только.</span><span class="sxs-lookup"><span data-stu-id="3b09d-106">This article explains how toomove VMs deployed through hello classic deployment model only.</span></span>
> 
> 

<span data-ttu-id="3b09d-107">Зачем перемещать виртуальные машины подсети tooanother?</span><span class="sxs-lookup"><span data-stu-id="3b09d-107">Why move VMs tooanother subnet?</span></span> <span data-ttu-id="3b09d-108">Подсеть миграции полезно, когда старая подсеть hello слишком мал и не могут быть развернуты из-за tooexisting работающих виртуальных машин в этой подсети.</span><span class="sxs-lookup"><span data-stu-id="3b09d-108">Subnet migration is useful when hello older subnet is too small and cannot be expanded due tooexisting running VMs in that subnet.</span></span> <span data-ttu-id="3b09d-109">В этом случае можно создать новый, больший подсети и перенести hello виртуальные машины toohello новую подсеть, а затем после завершения миграции можно удалить старые пустой подсети hello.</span><span class="sxs-lookup"><span data-stu-id="3b09d-109">In that case, you can create a new, larger subnet and migrate hello VMs toohello new subnet, then after migration is complete, you can delete hello old empty subnet.</span></span>

## <a name="how-toomove-a-vm-tooanother-subnet"></a><span data-ttu-id="3b09d-110">Как toomove tooanother подсеть виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="3b09d-110">How toomove a VM tooanother subnet</span></span>
<span data-ttu-id="3b09d-111">toomove виртуальную Машину, выполните командлет PowerShell Set-AzureSubnet hello, используя в качестве шаблона пример hello ниже.</span><span class="sxs-lookup"><span data-stu-id="3b09d-111">toomove a VM, run hello Set-AzureSubnet PowerShell cmdlet, using hello example below as a template.</span></span> <span data-ttu-id="3b09d-112">В следующем примере hello, выполняется перемещение TestVM из старой подсети tooSubnet-2.</span><span class="sxs-lookup"><span data-stu-id="3b09d-112">In hello example below, we are moving TestVM from its present subnet, tooSubnet-2.</span></span> <span data-ttu-id="3b09d-113">Быть убедиться, что tooreflect пример hello tooedit вашей среде.</span><span class="sxs-lookup"><span data-stu-id="3b09d-113">Be sure tooedit hello example tooreflect your environment.</span></span> <span data-ttu-id="3b09d-114">Обратите внимание, что при каждом выполнении командлета Update-AzureVM hello в рамках процедуры, она будет перезагружать вашу ВМ в рамках процесса обновления hello.</span><span class="sxs-lookup"><span data-stu-id="3b09d-114">Note that whenever you run hello Update-AzureVM cmdlet as part of a procedure, it will restart your VM as part of hello update process.</span></span>

    Get-AzureVM –ServiceName TestVMCloud –Name TestVM `
    | Set-AzureSubnet –SubnetNames Subnet-2 `
    | Update-AzureVM

<span data-ttu-id="3b09d-115">Если указан статический внутренний частных IP-адрес для ВМ, вы получите tooclear эту настройку перед перемещением hello ВМ tooa новую подсеть.</span><span class="sxs-lookup"><span data-stu-id="3b09d-115">If you specified a static internal private IP for your VM, you'll have tooclear that setting before you can move hello VM tooa new subnet.</span></span> <span data-ttu-id="3b09d-116">В этом случае используйте hello ниже:</span><span class="sxs-lookup"><span data-stu-id="3b09d-116">In that case, use hello following:</span></span>

    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM
    Get-AzureVM -ServiceName TestVMCloud -Name TestVM `
    | Set-AzureSubnet -SubnetNames Subnet-2 `
    | Update-AzureVM

## <a name="toomove-a-role-instance-tooanother-subnet"></a><span data-ttu-id="3b09d-117">toomove подсети tooanother экземпляра роли</span><span class="sxs-lookup"><span data-stu-id="3b09d-117">toomove a role instance tooanother subnet</span></span>
<span data-ttu-id="3b09d-118">toomove экземпляра роли, измените файл CSCFG hello.</span><span class="sxs-lookup"><span data-stu-id="3b09d-118">toomove a role instance, edit hello CSCFG file.</span></span> <span data-ttu-id="3b09d-119">В следующем примере hello, выполняется перемещение «Role0» в виртуальной сети *VNETName* из старой подсети слишком*Subnet-2*.</span><span class="sxs-lookup"><span data-stu-id="3b09d-119">In hello example below, we are moving "Role0" in virtual network *VNETName* from its present subnet too*Subnet-2*.</span></span> <span data-ttu-id="3b09d-120">Поскольку экземпляр роли hello уже был развернут, достаточно изменить имя подсети hello = Subnet-2.</span><span class="sxs-lookup"><span data-stu-id="3b09d-120">Because hello role instance was already deployed, you'll just change hello Subnet name = Subnet-2.</span></span> <span data-ttu-id="3b09d-121">Быть убедиться, что tooreflect пример hello tooedit вашей среде.</span><span class="sxs-lookup"><span data-stu-id="3b09d-121">Be sure tooedit hello example tooreflect your environment.</span></span>

    <NetworkConfiguration>
        <VirtualNetworkSite name="VNETName" />
        <AddressAssignments>
           <InstanceAddress roleName="Role0">
                <Subnets><Subnet name="Subnet-2" /></Subnets>
           </InstanceAddress>
        </AddressAssignments>
    </NetworkConfiguration> 
