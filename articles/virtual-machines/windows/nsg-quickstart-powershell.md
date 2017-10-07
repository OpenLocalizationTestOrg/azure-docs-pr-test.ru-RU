---
title: "aaaOpen порты tooa виртуальную Машину с помощью Azure PowerShell | Документы Microsoft"
description: "Узнайте, как tooopen порт / create tooyour конечной точки виртуальной Машины Windows с помощью режима развертывания диспетчера ресурсов Azure hello и Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="13f24-103">Как tooopen портов и конечные точки tooa ВМ в Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="13f24-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="13f24-104">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="13f24-104">Quick commands</span></span>
<span data-ttu-id="13f24-105">Группы безопасности сети toocreate и правила ACL необходимо [hello последнюю версию Azure PowerShell установлена](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="13f24-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="13f24-106">Вы также можете [выполните следующие действия с помощью портала Azure hello](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="13f24-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="13f24-107">Вход tooyour учетная запись Azure:</span><span class="sxs-lookup"><span data-stu-id="13f24-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="13f24-108">В hello следующих примерах замените примеры имен параметров собственные значения.</span><span class="sxs-lookup"><span data-stu-id="13f24-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="13f24-109">Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="13f24-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="13f24-110">Создайте правило с помощью командлета [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="13f24-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="13f24-111">Hello следующий код создает правило с именем *myNetworkSecurityGroupRule* tooallow *tcp* трафик через порт *80*:</span><span class="sxs-lookup"><span data-stu-id="13f24-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="13f24-112">Создайте группу безопасности сети [New AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) и назначить правило hello HTTP, только что созданный следующим образом.</span><span class="sxs-lookup"><span data-stu-id="13f24-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="13f24-113">Hello следующий пример создает группу безопасности сети с именем *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="13f24-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="13f24-114">Теперь давайте назначить подсети tooa группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="13f24-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="13f24-115">Hello следующий пример назначает существующую виртуальную сеть с именем *myVnet* переменной toohello *$vnet* с [Get AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="13f24-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="13f24-116">Свяжите группу безопасности сети с подсетью с помощью командлета [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="13f24-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="13f24-117">Hello следующий пример связывает hello подсеть с именем *mySubnet* с вашей сетевой группы безопасности:</span><span class="sxs-lookup"><span data-stu-id="13f24-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="13f24-118">Наконец, обновления виртуальной сети с [AzureRmVirtualNetwork набора](/powershell/module/azurerm.network/set-azurermvirtualnetwork) в порядке для изменения эффекта tootake:</span><span class="sxs-lookup"><span data-stu-id="13f24-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="13f24-119">Дополнительная информация о группах безопасности сети</span><span class="sxs-lookup"><span data-stu-id="13f24-119">More information on Network Security Groups</span></span>
<span data-ttu-id="13f24-120">Hello здесь Быстрые команды позволяют tooget вверх и работает с tooyour передачу трафика виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="13f24-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="13f24-121">Сетевые группы безопасности предоставляют много замечательных функций и гранулярности для управления доступа к ресурсам tooyour.</span><span class="sxs-lookup"><span data-stu-id="13f24-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="13f24-122">[Здесь](tutorial-virtual-network.md#manage-internal-traffic)вы можете больше прочитать о создании группы безопасности сети и правил ACL.</span><span class="sxs-lookup"><span data-stu-id="13f24-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="13f24-123">Для веб-приложений с высокой доступностью необходимо поместить виртуальную машину за Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="13f24-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="13f24-124">Подсистема балансировки нагрузки Hello распределяет трафик tooVMs, с группой безопасности сети, которая обеспечивает фильтрацию трафика.</span><span class="sxs-lookup"><span data-stu-id="13f24-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="13f24-125">Дополнительные сведения см. в разделе [как баланс tooload Linux виртуальных машин в Azure toocreate приложение с высокой доступностью](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="13f24-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13f24-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="13f24-126">Next steps</span></span>
<span data-ttu-id="13f24-127">В этом примере вы создали трафика tooallow HTTP простое правило.</span><span class="sxs-lookup"><span data-stu-id="13f24-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="13f24-128">Можно найти сведения о создании более подробные сред в hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="13f24-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="13f24-129">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="13f24-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="13f24-130">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="13f24-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="13f24-131">Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="13f24-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

