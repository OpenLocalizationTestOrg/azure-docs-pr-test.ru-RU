---
title: "Удаление шлюза виртуальной сети с помощью PowerShell (Azure Resource Manager) | Документация Майкрософт"
description: "Удаление шлюза виртуальной сети посредством PowerShell в модели развертывания с помощью Resource Manager."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="61b64-103">Удаление шлюза виртуальной сети с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="61b64-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="61b64-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="61b64-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="61b64-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="61b64-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="61b64-106">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="61b64-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="61b64-107">Существует несколько разных подходов, которые можно применить, когда требуется удалить шлюз виртуальной сети для настройки VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="61b64-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="61b64-108">Если вы хотите все удалить и начать заново, как в случае с тестовой средой, то можете удалить группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="61b64-109">При удалении группы ресурсов удаляются все ресурсы в этой группе.</span><span class="sxs-lookup"><span data-stu-id="61b64-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="61b64-110">Этот метод рекомендуется, только если вы не хотите оставить какие-либо ресурсы из группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="61b64-111">При таком подходе невозможно выборочно удалить только некоторые из ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="61b64-112">Если вы хотите сохранить некоторые ресурсы в группе ресурсов, то удаление шлюза виртуальной сети немного усложняется.</span><span class="sxs-lookup"><span data-stu-id="61b64-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="61b64-113">Прежде чем удалить шлюз виртуальной сети, необходимо удалить все ресурсы, зависящие от него.</span><span class="sxs-lookup"><span data-stu-id="61b64-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="61b64-114">Выполняемые действия зависят от типа подключений, которые были созданы, и зависимых ресурсов для каждого подключения.</span><span class="sxs-lookup"><span data-stu-id="61b64-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="61b64-115">Подготовка</span><span class="sxs-lookup"><span data-stu-id="61b64-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="61b64-116">1. Скачайте последнюю версию командлетов PowerShell для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61b64-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="61b64-117">Скачайте и установите последнюю версию командлетов PowerShell для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61b64-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="61b64-118">Дополнительные сведения о скачивании и установке командлетов PowerShell см. в статье [Get started with Azure PowerShell cmdlets](/powershell/azure/overview) (Приступая к работе с командлетами Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="61b64-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="61b64-119">2. Подключитесь к своей учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="61b64-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="61b64-120">Откройте консоль PowerShell и подключитесь к своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="61b64-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="61b64-121">Для подключения используйте следующий пример кода:</span><span class="sxs-lookup"><span data-stu-id="61b64-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="61b64-122">Просмотрите подписки учетной записи.</span><span class="sxs-lookup"><span data-stu-id="61b64-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="61b64-123">При наличии нескольких подписок укажите подписку, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="61b64-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="61b64-124"><a name="S2S"></a>Удаление VPN-шлюза типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="61b64-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="61b64-125">Чтобы удалить шлюз виртуальной сети для конфигурации "сеть — сеть", необходимо сначала удалить каждый ресурс, относящийся к этому шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="61b64-126">Ресурсы должны быть удалены в определенном порядке из-за зависимостей.</span><span class="sxs-lookup"><span data-stu-id="61b64-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="61b64-127">При работе с приведенными ниже примерами некоторые значения необходимо указывать, тогда как другие значения находятся в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="61b64-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="61b64-128">В примерах для демонстрационных целей мы используем следующие конкретные значения.</span><span class="sxs-lookup"><span data-stu-id="61b64-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="61b64-129">Имя виртуальной сети: VNet1.</span><span class="sxs-lookup"><span data-stu-id="61b64-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="61b64-130">Имя группы ресурсов: RG1.</span><span class="sxs-lookup"><span data-stu-id="61b64-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="61b64-131">Имя шлюза виртуальной сети: GW1.</span><span class="sxs-lookup"><span data-stu-id="61b64-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="61b64-132">Приведенные ниже инструкции относятся к модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61b64-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="61b64-133">1. Получите шлюз виртуальной сети, который нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="61b64-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="61b64-134">2. Проверьте наличие подключений к шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="61b64-135">3. Удалите все подключения.</span><span class="sxs-lookup"><span data-stu-id="61b64-135">3. Delete all connections.</span></span>

<span data-ttu-id="61b64-136">Может потребоваться подтвердить удаление каждого подключения.</span><span class="sxs-lookup"><span data-stu-id="61b64-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="61b64-137">4. Удалите шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="61b64-138">Может потребоваться подтвердить его удаление.</span><span class="sxs-lookup"><span data-stu-id="61b64-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="61b64-139">Если кроме конфигурации типа "сеть — сеть" в этой виртуальной сети есть конфигурация типа "точка — сеть", то удаление шлюза виртуальной сети приведет к автоматическому отключению всех клиентов P2S без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="61b64-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="61b64-140">На этом этапе шлюз виртуальной сети будет удален.</span><span class="sxs-lookup"><span data-stu-id="61b64-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="61b64-141">Вы можете выполнить следующие шаги, чтобы удалить любые неиспользуемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="61b64-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="61b64-142">5. Удалите шлюзы локальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="61b64-143">Получите список соответствующих шлюзов локальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="61b64-144">Удалите шлюзы локальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-144">Delete the local network gateways.</span></span> <span data-ttu-id="61b64-145">Может потребоваться подтвердить удаление каждого из них.</span><span class="sxs-lookup"><span data-stu-id="61b64-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="61b64-146">6. Удалите ресурсы с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="61b64-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="61b64-147">Получите конфигурации IP шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="61b64-148">Получите список ресурсов с общедоступным IP-адресом, используемых для этого шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="61b64-149">Если шлюз виртуальной сети работал в режиме "активный — активный", вы увидите два общедоступных IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="61b64-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="61b64-150">Удалите ресурсы с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="61b64-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="61b64-151">7. Удалите подсеть шлюза и настройте конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="61b64-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="61b64-152"><a name="v2v"></a>Удаление VPN-шлюза типа "виртуальная сеть — виртуальная сеть"</span><span class="sxs-lookup"><span data-stu-id="61b64-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="61b64-153">Чтобы удалить шлюз виртуальной сети для конфигурации "виртуальная сеть — виртуальная сеть", необходимо сначала удалить каждый ресурс, относящийся к этому шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="61b64-154">Ресурсы должны быть удалены в определенном порядке из-за зависимостей.</span><span class="sxs-lookup"><span data-stu-id="61b64-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="61b64-155">При работе с приведенными ниже примерами некоторые значения необходимо указывать, тогда как другие значения находятся в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="61b64-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="61b64-156">В примерах для демонстрационных целей мы используем следующие конкретные значения.</span><span class="sxs-lookup"><span data-stu-id="61b64-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="61b64-157">Имя виртуальной сети: VNet1.</span><span class="sxs-lookup"><span data-stu-id="61b64-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="61b64-158">Имя группы ресурсов: RG1.</span><span class="sxs-lookup"><span data-stu-id="61b64-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="61b64-159">Имя шлюза виртуальной сети: GW1.</span><span class="sxs-lookup"><span data-stu-id="61b64-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="61b64-160">Приведенные ниже инструкции относятся к модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61b64-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="61b64-161">1. Получите шлюз виртуальной сети, который нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="61b64-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="61b64-162">2. Проверьте наличие подключений к шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="61b64-163">Могут существовать другие подключения к шлюзу виртуальной сети, входящие в другую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="61b64-164">Проверьте наличие дополнительных подключений в каждой дополнительной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="61b64-165">В этом примере выполняется проверка на наличие подключений из RG2.</span><span class="sxs-lookup"><span data-stu-id="61b64-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="61b64-166">Выполните его для каждой имеющейся группы ресурсов, которая может быть подключена к шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="61b64-167">3. Получите список соединений в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="61b64-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="61b64-168">Так как это конфигурация "виртуальная сеть — виртуальная сеть", необходим список подключений в обоих направлениях.</span><span class="sxs-lookup"><span data-stu-id="61b64-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="61b64-169">В этом примере выполняется проверка на наличие подключений из RG2.</span><span class="sxs-lookup"><span data-stu-id="61b64-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="61b64-170">Выполните его для каждой имеющейся группы ресурсов, которая может быть подключена к шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="61b64-171">4. Удалите все подключения.</span><span class="sxs-lookup"><span data-stu-id="61b64-171">4. Delete all connections.</span></span>

<span data-ttu-id="61b64-172">Может потребоваться подтвердить удаление каждого подключения.</span><span class="sxs-lookup"><span data-stu-id="61b64-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="61b64-173">5. Удалите шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="61b64-174">Может потребоваться подтвердить его удаление.</span><span class="sxs-lookup"><span data-stu-id="61b64-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="61b64-175">Если кроме конфигурации типа "виртуальная сеть — виртуальная сеть" в ваших виртуальных сетях есть конфигурация типа "точка — сеть", то удаление шлюзов виртуальных сетей приведет к автоматическому отключению всех клиентов P2S без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="61b64-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="61b64-176">На этом этапе шлюз виртуальной сети будет удален.</span><span class="sxs-lookup"><span data-stu-id="61b64-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="61b64-177">Вы можете выполнить следующие шаги, чтобы удалить любые неиспользуемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="61b64-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="61b64-178">6. Удалите ресурсы с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="61b64-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="61b64-179">Получите конфигурации IP шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="61b64-180">Получите список ресурсов с общедоступным IP-адресом, используемых для этого шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="61b64-181">Если шлюз виртуальной сети работал в режиме "активный — активный", вы увидите два общедоступных IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="61b64-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="61b64-182">Удалите ресурсы с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="61b64-182">Delete the Public IP resources.</span></span> <span data-ttu-id="61b64-183">Может потребоваться подтвердить их удаление.</span><span class="sxs-lookup"><span data-stu-id="61b64-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="61b64-184">7. Удалите подсеть шлюза и настройте конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="61b64-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="61b64-185"><a name="deletep2s"></a>Удаление VPN-шлюза типа "точка — сеть"</span><span class="sxs-lookup"><span data-stu-id="61b64-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="61b64-186">Чтобы удалить шлюз виртуальной сети для конфигурации "точка — сеть", необходимо сначала удалить каждый ресурс, относящийся к этому шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="61b64-187">Ресурсы должны быть удалены в определенном порядке из-за зависимостей.</span><span class="sxs-lookup"><span data-stu-id="61b64-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="61b64-188">При работе с приведенными ниже примерами некоторые значения необходимо указывать, тогда как другие значения находятся в выходных данных.</span><span class="sxs-lookup"><span data-stu-id="61b64-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="61b64-189">В примерах для демонстрационных целей мы используем следующие конкретные значения.</span><span class="sxs-lookup"><span data-stu-id="61b64-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="61b64-190">Имя виртуальной сети: VNet1.</span><span class="sxs-lookup"><span data-stu-id="61b64-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="61b64-191">Имя группы ресурсов: RG1.</span><span class="sxs-lookup"><span data-stu-id="61b64-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="61b64-192">Имя шлюза виртуальной сети: GW1.</span><span class="sxs-lookup"><span data-stu-id="61b64-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="61b64-193">Приведенные ниже инструкции относятся к модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61b64-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="61b64-194">При удалении VPN-шлюза все подключенные клиенты будут отключены от виртуальной сети без предупреждения.</span><span class="sxs-lookup"><span data-stu-id="61b64-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="61b64-195">1. Получите шлюз виртуальной сети, который нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="61b64-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="61b64-196">2. Удалите шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="61b64-197">Может потребоваться подтвердить его удаление.</span><span class="sxs-lookup"><span data-stu-id="61b64-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="61b64-198">На этом этапе шлюз виртуальной сети будет удален.</span><span class="sxs-lookup"><span data-stu-id="61b64-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="61b64-199">Вы можете выполнить следующие шаги, чтобы удалить любые неиспользуемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="61b64-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="61b64-200">3. Удалите ресурсы с общедоступным IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="61b64-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="61b64-201">Получите конфигурации IP шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="61b64-202">Получите список общедоступных IP-адресов, используемых для этого шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="61b64-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="61b64-203">Если шлюз виртуальной сети работал в режиме "активный — активный", вы увидите два общедоступных IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="61b64-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="61b64-204">Удалите эти общедоступные IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="61b64-204">Delete the Public IPs.</span></span> <span data-ttu-id="61b64-205">Может потребоваться подтвердить их удаление.</span><span class="sxs-lookup"><span data-stu-id="61b64-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="61b64-206">4. Удалите подсеть шлюза и настройте конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="61b64-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="61b64-207"><a name="delete"></a>Удаление VPN-шлюза путем удаления группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="61b64-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="61b64-208">Если не требуется сохранить какие-либо ресурсы из группы ресурсов и вы просто хотите начать все заново, то вы можете удалить всю группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="61b64-209">Это быстрый способ удалить все сразу.</span><span class="sxs-lookup"><span data-stu-id="61b64-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="61b64-210">Приведенные ниже инструкции относятся только к модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="61b64-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="61b64-211">1. Получите список всех групп ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="61b64-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="61b64-212">2. Найдите группу ресурсов, которую нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="61b64-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="61b64-213">Найдите группу ресурсов, которую нужно удалить, и просмотрите список содержащихся в ней ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="61b64-214">В этом примере группа ресурсов называется RG1.</span><span class="sxs-lookup"><span data-stu-id="61b64-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="61b64-215">Измените пример, чтобы получить список всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="61b64-216">3. Проверьте ресурсы в списке.</span><span class="sxs-lookup"><span data-stu-id="61b64-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="61b64-217">Получив список ресурсов, просмотрите его, чтобы удостовериться, что вы хотите удалить все ресурсы в группе ресурсов, а также саму группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="61b64-218">Если вы хотите сохранить какие-либо ресурсы из группы ресурсов, следуйте инструкциям в предыдущих разделах данной статьи, чтобы удалить шлюз.</span><span class="sxs-lookup"><span data-stu-id="61b64-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="61b64-219">4. Удалите группу ресурсов и ее содержимое.</span><span class="sxs-lookup"><span data-stu-id="61b64-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="61b64-220">Чтобы удалить группу ресурсов и ее ресурсы, измените приведенный пример и выполните его.</span><span class="sxs-lookup"><span data-stu-id="61b64-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="61b64-221">5. Проверьте состояние.</span><span class="sxs-lookup"><span data-stu-id="61b64-221">5. Check the status.</span></span>

<span data-ttu-id="61b64-222">Для удаления всех ресурсов платформе Azure потребуется некоторое время.</span><span class="sxs-lookup"><span data-stu-id="61b64-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="61b64-223">С помощью приведенного ниже командлета можно проверить состояние группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="61b64-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="61b64-224">По завершении отобразится результат "Успешно".</span><span class="sxs-lookup"><span data-stu-id="61b64-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```