---
title: "Открытие портов для виртуальной машины с помощью Azure PowerShell | Документация Майкрософт"
description: "Узнайте, как открыть порт или создать конечную точку для виртуальной машины Windows, используя модель развертывания с помощью Azure Resource Manager и Azure PowerShell."
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
ms.openlocfilehash: e818e3b3c707e1471d6f580f8379a277d3575b89
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-and-endpoints-to-a-vm-in-azure-using-powershell"></a><span data-ttu-id="2ea32-103">Как открыть порты и конечные точки для виртуальной машины в Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ea32-103">How to open ports and endpoints to a VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="2ea32-104">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="2ea32-104">Quick commands</span></span>
<span data-ttu-id="2ea32-105">Для создания группы безопасности сети и правил ACL потребуется [последняя версия Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="2ea32-105">To create a Network Security Group and ACL rules you need [the latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="2ea32-106">Эти действия можно также [выполнить с помощью портала Azure](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2ea32-106">You can also [perform these steps using the Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="2ea32-107">Войдите в свою учетную запись Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea32-107">Log in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="2ea32-108">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="2ea32-108">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2ea32-109">Примеры имен параметров: *myResourceGroup*, *mystorageaccount* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="2ea32-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="2ea32-110">Создайте правило с помощью командлета [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="2ea32-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="2ea32-111">В следующем примере создается правило с именем *myNetworkSecurityGroupRule*. Это правило разрешает *TCP*-трафик через порт *80*:</span><span class="sxs-lookup"><span data-stu-id="2ea32-111">The following example creates a rule named *myNetworkSecurityGroupRule* to allow *tcp* traffic on port *80*:</span></span>

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

<span data-ttu-id="2ea32-112">Затем с помощью командлета [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) создайте группу безопасности сети и назначьте только что созданное правило HTTP, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="2ea32-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign the HTTP rule you just created as follows.</span></span> <span data-ttu-id="2ea32-113">В следующем примере создается группа безопасности сети с именем *myNetworkSecurityGroup*.</span><span class="sxs-lookup"><span data-stu-id="2ea32-113">The following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="2ea32-114">Теперь давайте назначим подсети вашу группу безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="2ea32-114">Now let's assign your Network Security Group to a subnet.</span></span> <span data-ttu-id="2ea32-115">В следующем примере с помощью [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork) переменной *$vnet* назначается существующая виртуальная сеть *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="2ea32-115">The following example assigns an existing virtual network named *myVnet* to the variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="2ea32-116">Свяжите группу безопасности сети с подсетью с помощью командлета [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="2ea32-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="2ea32-117">В следующем примере подсеть *mySubnet* связывается с группой безопасности сети:</span><span class="sxs-lookup"><span data-stu-id="2ea32-117">The following example associates the subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="2ea32-118">Наконец, с помощью командлета [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) обновите виртуальную сеть, чтобы изменения вступили в силу.</span><span class="sxs-lookup"><span data-stu-id="2ea32-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes to take effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="2ea32-119">Дополнительная информация о группах безопасности сети</span><span class="sxs-lookup"><span data-stu-id="2ea32-119">More information on Network Security Groups</span></span>
<span data-ttu-id="2ea32-120">Приведенные здесь быстрые команды позволят настроить трафик, поступающий в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="2ea32-120">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="2ea32-121">Группы безопасности сети предоставляют множество полезных функций и всевозможные настройки для управления доступом к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="2ea32-121">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="2ea32-122">[Здесь](tutorial-virtual-network.md#manage-internal-traffic)вы можете больше прочитать о создании группы безопасности сети и правил ACL.</span><span class="sxs-lookup"><span data-stu-id="2ea32-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="2ea32-123">Для веб-приложений с высокой доступностью необходимо поместить виртуальную машину за Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="2ea32-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="2ea32-124">Балансировщик нагрузки распределяет трафик между виртуальными машинами с группой безопасности сети, обеспечивающей фильтрацию трафика.</span><span class="sxs-lookup"><span data-stu-id="2ea32-124">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="2ea32-125">Подробные сведения см. в статье [Балансировка нагрузки виртуальных машин Windows в Azure для создания высокодоступного приложения](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="2ea32-125">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ea32-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2ea32-126">Next steps</span></span>
<span data-ttu-id="2ea32-127">В этом примере создано простое правило, разрешающее трафик HTTP.</span><span class="sxs-lookup"><span data-stu-id="2ea32-127">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="2ea32-128">Информацию о создании более детализированных сред можно найти в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="2ea32-128">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="2ea32-129">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2ea32-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="2ea32-130">Группа безопасности сети</span><span class="sxs-lookup"><span data-stu-id="2ea32-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="2ea32-131">Поддержка диспетчера ресурсов Azure для подсистемы балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="2ea32-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

