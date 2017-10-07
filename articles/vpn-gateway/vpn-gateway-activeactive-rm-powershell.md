---
title: "Настройка VPN-подключений типа \"сеть — сеть\" в режиме \"активный — активный\" для VPN-шлюзов: Azure Resource Manager и PowerShell | Документы Майкрософт"
description: "В этой статье описана поэтапная настройка подключений в режиме \"активный — активный\" для VPN-шлюзов Azure с помощью Azure Resource Manager и PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="50387-103">Настройка VPN-подключений типа "сеть — сеть" в режиме "активный — активный" для VPN-шлюзов Azure</span><span class="sxs-lookup"><span data-stu-id="50387-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="50387-104">В этой статье рассматриваются hello действия toocreate активных между организациями и подключений виртуальной сети для виртуальной сети, с помощью модели развертывания диспетчера ресурсов hello и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50387-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="50387-105">Высокодоступное подключение между локальными сетями</span><span class="sxs-lookup"><span data-stu-id="50387-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="50387-106">высокий уровень доступности tooachieve между организациями и подключения к виртуальной сети для виртуальной сети, следует развернуть несколько шлюзов виртуальной частной сети и установить несколько параллельных соединений между сетями и Azure.</span><span class="sxs-lookup"><span data-stu-id="50387-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="50387-107">Сведения о вариантах подключения и топологии подключений см. в статье [Настройка высокодоступных подключений: распределенных и между виртуальными сетями](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="50387-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="50387-108">В этой статье содержатся инструкции hello tooset копирование активный / активный между организациями VPN-подключения, а также активных соединений между двумя виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="50387-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="50387-109">Часть 1. Создание и настройка VPN-шлюза Azure в режиме "активный — активный"</span><span class="sxs-lookup"><span data-stu-id="50387-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="50387-110">Часть 2. Создание подключения между локальными сетями в режиме "активный — активный"</span><span class="sxs-lookup"><span data-stu-id="50387-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="50387-111">Часть 3. Создание подключения между виртуальными сетями в режиме "активный — активный"</span><span class="sxs-lookup"><span data-stu-id="50387-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="50387-112">Часть 4. Обновление имеющегося шлюза между режимами "активный — активный" и "активный — резервный"</span><span class="sxs-lookup"><span data-stu-id="50387-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="50387-113">Можно объединять эти вместе toobuild топологии сети более сложных, высокой надежности, соответствующий вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="50387-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50387-114">Обратите внимание, что hello активный / активный режим используется только hello после номера SKU:</span><span class="sxs-lookup"><span data-stu-id="50387-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="50387-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="50387-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="50387-116">HighPerformance (для устаревших номеров SKU)</span><span class="sxs-lookup"><span data-stu-id="50387-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="50387-117"><a name ="aagateway"></a>Часть 1. Создание и настройка VPN-шлюзов в режиме "активный — активный"</span><span class="sxs-lookup"><span data-stu-id="50387-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="50387-118">в режимах активных Hello, выполнив действия настроит шлюза Azure VPN.</span><span class="sxs-lookup"><span data-stu-id="50387-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="50387-119">Hello основные различия между шлюзами активный / активный "и" активный резервный hello.</span><span class="sxs-lookup"><span data-stu-id="50387-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="50387-120">Требуются две конфигурации IP-адреса шлюза toocreate с общедоступных IP-адресов</span><span class="sxs-lookup"><span data-stu-id="50387-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="50387-121">Вы должны установить флаг EnableActiveActiveFeature hello</span><span class="sxs-lookup"><span data-stu-id="50387-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="50387-122">номер SKU шлюза Hello необходимо VpnGw1, VpnGw2, VpnGw3 или высокопроизводительные (Конфигурация прежних версий).</span><span class="sxs-lookup"><span data-stu-id="50387-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="50387-123">Hello другие свойства являются hello такой же, как шлюзы активный активный hello.</span><span class="sxs-lookup"><span data-stu-id="50387-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="50387-124">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="50387-124">Before you begin</span></span>
* <span data-ttu-id="50387-125">Убедитесь в том, что у вас уже есть подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="50387-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="50387-126">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50387-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="50387-127">Вам потребуется командлеты PowerShell диспетчера ресурсов Azure tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="50387-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="50387-128">В разделе [Обзор Azure PowerShell](/powershell/azure/overview) Дополнительные сведения об установке командлетов PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="50387-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="50387-129">Шаг 1. Создание и настройка VNet1</span><span class="sxs-lookup"><span data-stu-id="50387-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="50387-130">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="50387-130">1. Declare your variables</span></span>
<span data-ttu-id="50387-131">В этом упражнении мы начнем с объявления переменных.</span><span class="sxs-lookup"><span data-stu-id="50387-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="50387-132">пример Hello hello переменных объявляются с помощью hello значения для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="50387-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="50387-133">Быть убедиться, что значения hello tooreplace собственными при настройке для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="50387-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="50387-134">Эти переменные можно использовать при выполнении через toobecome действия hello знакомы с этим типом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="50387-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="50387-135">Изменение переменных hello, а затем скопируйте и вставьте в консоль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50387-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="50387-136">2. Подключить tooyour подписки и создать новую группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="50387-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="50387-137">Убедитесь, что переключение tooPowerShell режим toouse hello командлеты диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="50387-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="50387-138">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="50387-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="50387-139">Откройте консоль PowerShell и подключить tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="50387-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="50387-140">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="50387-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="50387-141">3. Создание TestVNet1</span><span class="sxs-lookup"><span data-stu-id="50387-141">3. Create TestVNet1</span></span>
<span data-ttu-id="50387-142">Образец Hello ниже создает виртуальную сеть с именем TestVNet1 и три подсети, один именем GatewaySubnet, одной вызываемой переднего плана и один внутренний вызван.</span><span class="sxs-lookup"><span data-stu-id="50387-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="50387-143">При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="50387-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="50387-144">Если вы используете другое имя, шлюз не будет создан.</span><span class="sxs-lookup"><span data-stu-id="50387-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="50387-145">Шаг 2 — Создание hello VPN-шлюза для TestVNet1 активный / активный режим</span><span class="sxs-lookup"><span data-stu-id="50387-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="50387-146">1. Создание общих IP-адресов hello и шлюз IP-конфигурации</span><span class="sxs-lookup"><span data-stu-id="50387-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="50387-147">Запрос двух открытый IP-адреса toobe выделенный toohello шлюз, создаваемых для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="50387-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="50387-148">Также мы определим hello подсети и IP-конфигурации требуется.</span><span class="sxs-lookup"><span data-stu-id="50387-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="50387-149">2. Создание шлюза VPN hello в конфигурации активный активный</span><span class="sxs-lookup"><span data-stu-id="50387-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="50387-150">Создание шлюза виртуальной сети hello для TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="50387-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="50387-151">Обратите внимание, что имеется две записи GatewayIpConfig hello EnableActiveActiveFeature флаг имеет значение.</span><span class="sxs-lookup"><span data-stu-id="50387-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="50387-152">Создание шлюза может занять некоторое время (45 минут или более toocomplete).</span><span class="sxs-lookup"><span data-stu-id="50387-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="50387-153">3. Получить hello шлюза общих IP-адресов и адрес IP однорангового узла BGP hello</span><span class="sxs-lookup"><span data-stu-id="50387-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="50387-154">После создания шлюза hello требуется адрес IP однорангового узла BGP hello tooobtain на hello шлюза VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="50387-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="50387-155">Этот адрес будет hello необходимые tooconfigure VPN-шлюз Azure как узла BGP для VPN-устройства в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="50387-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="50387-156">Используйте следующие командлеты tooshow hello два общедоступных IP-адресов выделенные для шлюза VPN и их соответствующие адреса IP однорангового узла BGP для каждого экземпляра шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="50387-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

<span data-ttu-id="50387-157">порядок Hello hello общих IP-адресов для экземпляров шлюза hello и соответствующего адреса Пиринг BGP приветствия hello таким же.</span><span class="sxs-lookup"><span data-stu-id="50387-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="50387-158">В этом примере hello шлюза виртуальной Машины с помощью открытого IP-адреса 40.112.190.5 будет использовать 10.12.255.4 в качестве его адрес Пиринг BGP и hello шлюз с 138.91.156.129 будет использовать 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="50387-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="50387-159">Эти сведения необходимы при настройке локальную подключение toohello активных шлюза VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="50387-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="50387-160">шлюз Hello показано hello показан на следующем рисунке адреса всех:</span><span class="sxs-lookup"><span data-stu-id="50387-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![Шлюз в режиме "активный — активный"](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="50387-162">После создания шлюза hello, можно использовать этот шлюз tooestablish активных между организациями или подключения VNet-VNet.</span><span class="sxs-lookup"><span data-stu-id="50387-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="50387-163">Hello в следующих разделах приведены шаги упражнения hello toocomplete действия hello.</span><span class="sxs-lookup"><span data-stu-id="50387-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="50387-164"><a name ="aacrossprem"></a>Часть 2. Создание подключения между локальными сетями в режиме "активный — активный"</span><span class="sxs-lookup"><span data-stu-id="50387-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="50387-165">tooestablish подключения между организациями необходимо toocreate toorepresent шлюза локальной сети VPN-устройства в локальной среде и шлюза Azure VPN hello tooconnect соединения с hello шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="50387-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="50387-166">В этом примере hello VPN-шлюз Azure находится в режиме активных.</span><span class="sxs-lookup"><span data-stu-id="50387-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="50387-167">В результате несмотря на то, что имеется только один локальный VPN-устройством (шлюз локальной сети) и одно подключение ресурса, оба экземпляра шлюза Azure VPN установит туннелей S2S VPN с локального устройства hello.</span><span class="sxs-lookup"><span data-stu-id="50387-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="50387-168">Прежде чем продолжить, убедитесь, что вы выполнили инструкции из [первой части](#aagateway) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="50387-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="50387-169">Шаг 1. Создание и настройка шлюза локальной сети hello</span><span class="sxs-lookup"><span data-stu-id="50387-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="50387-170">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="50387-170">1. Declare your variables</span></span>
<span data-ttu-id="50387-171">В этом упражнении будет toobuild hello конфигурации, представленной схеме hello.</span><span class="sxs-lookup"><span data-stu-id="50387-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="50387-172">Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="50387-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="50387-173">Несколько вещей toonote относительно hello параметры шлюза локальной сети:</span><span class="sxs-lookup"><span data-stu-id="50387-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="50387-174">Hello шлюза локальной сети может быть в hello таким же или другое расположение и ресурсов группы как hello шлюза VPN.</span><span class="sxs-lookup"><span data-stu-id="50387-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="50387-175">В этом примере показано их в разные группы ресурсов, но в hello Azure местоположения.</span><span class="sxs-lookup"><span data-stu-id="50387-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="50387-176">Если имеется только одно устройство VPN в локальной среде, как показано выше, hello активных соединений может работать с или без протокола BGP.</span><span class="sxs-lookup"><span data-stu-id="50387-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="50387-177">Этот пример использует протокол BGP для подключения между организациями hello.</span><span class="sxs-lookup"><span data-stu-id="50387-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="50387-178">Если включен протокол BGP, префикс hello toodeclare потребность hello шлюза локальной сети — адрес узла hello ваш адрес BGP одноранговых IP на VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="50387-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="50387-179">В нашем примере это префикс /32 для адреса 10.52.255.253/32.</span><span class="sxs-lookup"><span data-stu-id="50387-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="50387-180">Не забывайте, что для локальных сетей и виртуальной сети Azure должны быть указаны разные номера ASN BGP.</span><span class="sxs-lookup"><span data-stu-id="50387-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="50387-181">Если они являются одинаковыми hello, необходимо toochange вашей виртуальной сети ASN Если VPN-устройства локальной уже использует hello ASN toopeer с соседним узлам BGP.</span><span class="sxs-lookup"><span data-stu-id="50387-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="50387-182">2. Создание шлюза локальной сети hello для Site5</span><span class="sxs-lookup"><span data-stu-id="50387-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="50387-183">Прежде чем продолжить, убедитесь в том, что по-прежнему подключенных tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="50387-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="50387-184">Создайте группу ресурсов hello, если он еще не создан.</span><span class="sxs-lookup"><span data-stu-id="50387-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="50387-185">Шаг 2 - подключения шлюза виртуальной сети hello и шлюз локальной сети</span><span class="sxs-lookup"><span data-stu-id="50387-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="50387-186">1. Получить hello двумя шлюзами</span><span class="sxs-lookup"><span data-stu-id="50387-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="50387-187">2. Создание подключения tooSite5 TestVNet1 hello</span><span class="sxs-lookup"><span data-stu-id="50387-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="50387-188">На этом шаге вы создадите hello подключения из TestVNet1 tooSite5_1 с «EnableBGP» задайте слишком $True.</span><span class="sxs-lookup"><span data-stu-id="50387-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="50387-189">3. Параметры VPN и BGP для локального VPN-устройства</span><span class="sxs-lookup"><span data-stu-id="50387-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="50387-190">пример Hello ниже перечислены параметры hello, будет вводимых вами в hello BGP раздел конфигурации для локального VPN-устройства для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="50387-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="50387-191">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="50387-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="50387-192">Site5 BGP IP         : 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="50387-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="50387-193">Префиксы tooannounce: (например) 10.51.0.0/16 и 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="50387-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="50387-194">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="50387-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="50387-195">Azure виртуальная сеть BGP IP-адрес 1: 10.12.255.4 для too40.112.190.5 туннель</span><span class="sxs-lookup"><span data-stu-id="50387-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="50387-196">Azure виртуальная сеть BGP IP-адрес 2: 10.12.255.5 для too138.91.156.129 туннель</span><span class="sxs-lookup"><span data-stu-id="50387-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="50387-197">Статические маршруты: 10.12.255.4/32 назначения, следующего hello VPN туннельный интерфейс too40.112.190.5 назначения 10.12.255.5/32, следующего hello VPN туннельный интерфейс too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="50387-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="50387-198">eBGP мульти-прыжка: Убедитесь, вариант «мульти-прыжка» hello eBGP включен на вашем устройстве, при необходимости</span><span class="sxs-lookup"><span data-stu-id="50387-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="50387-199">Hello подключение должно быть установлено, после того как несколько минут и сеанс пиринга BGP hello будет запущена после установки соединения IPsec hello.</span><span class="sxs-lookup"><span data-stu-id="50387-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="50387-200">В этом примере к текущему моменту настроил только одно устройство VPN локальной, приведет к диаграмме hello, показано ниже:</span><span class="sxs-lookup"><span data-stu-id="50387-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![Подключение между локальными сетями в режиме "активный — активный"](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="50387-202">Шаг 3 — подключить два шлюза VPN активных toohello локальной VPN устройства</span><span class="sxs-lookup"><span data-stu-id="50387-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="50387-203">При наличии двух VPN-устройства на hello же локальной сети, можно добиться двумя избыточности, подключающегося hello Azure устройство шлюза VPN toohello второй VPN.</span><span class="sxs-lookup"><span data-stu-id="50387-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="50387-204">1. Создание hello второго шлюза локальной сети для Site5</span><span class="sxs-lookup"><span data-stu-id="50387-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="50387-205">Обратите внимание, что IP-адрес шлюза hello, префикс адреса и адрес пиринг BGP для hello второго шлюза локальной сети не должны перекрываться hello предыдущих шлюза локальной сети для hello же локальной сети.</span><span class="sxs-lookup"><span data-stu-id="50387-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="50387-206">2. Подключения шлюза виртуальной сети hello и hello второго шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="50387-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="50387-207">Создание соединения hello с TestVNet1 tooSite5_2 с «EnableBGP» задайте слишком $True</span><span class="sxs-lookup"><span data-stu-id="50387-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="50387-208">3. Параметры VPN и BGP для второго локального VPN-устройства</span><span class="sxs-lookup"><span data-stu-id="50387-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="50387-209">Аналогичным образом ниже перечислены параметры hello будет ввести в hello второе устройство VPN:</span><span class="sxs-lookup"><span data-stu-id="50387-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="50387-210">После установления соединения hello (туннели) будет иметь два избыточных VPN-устройства и туннели подключения вашей локальной сетью и Azure:</span><span class="sxs-lookup"><span data-stu-id="50387-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![Подключение между локальными сетями с двойной избыточностью](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="50387-212"><a name ="aav2v"></a>Часть 3. Создание подключения между виртуальными сетями в режиме "активный — активный"</span><span class="sxs-lookup"><span data-stu-id="50387-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="50387-213">В этом разделе описано, как создать подключение между виртуальными сетями в режиме "активный — активный" с использованием BGP.</span><span class="sxs-lookup"><span data-stu-id="50387-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="50387-214">Приведенные ниже инструкции Hello по-прежнему hello предыдущих шагах, перечисленных выше.</span><span class="sxs-lookup"><span data-stu-id="50387-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="50387-215">Необходимо выполнить [часть 1](#aagateway) toocreate hello VPN-шлюз с BGP и настроите TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="50387-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="50387-216">Шаг 1 — Создание TestVNet2 и hello VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="50387-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="50387-217">Это важные toomake в том, что пространство IP-адресов hello hello новой виртуальной сети, TestVNet2, не перекрываются с диапазонов виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="50387-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="50387-218">В этом примере hello виртуальные сети относятся toohello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="50387-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="50387-219">Можно настроить виртуальную сеть — сеть соединений между разными подписками; см. слишком[Настройка подключения VNet-VNet](vpn-gateway-vnet-vnet-rm-ps.md) toolearn более подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="50387-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="50387-220">Убедитесь, что добавить hello»-EnableBgp $True» при создании hello tooenable подключений BGP.</span><span class="sxs-lookup"><span data-stu-id="50387-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="50387-221">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="50387-221">1. Declare your variables</span></span>
<span data-ttu-id="50387-222">Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="50387-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="50387-223">2. Создание TestVNet2 в новую группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="50387-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="50387-224">3. Создание VPN-шлюз hello активных для TestVNet2</span><span class="sxs-lookup"><span data-stu-id="50387-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="50387-225">Запрос двух открытый IP-адреса toobe выделенный toohello шлюз, создаваемых для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="50387-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="50387-226">Также мы определим hello подсети и IP-конфигурации требуется.</span><span class="sxs-lookup"><span data-stu-id="50387-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="50387-227">Создайте шлюз VPN hello hello как номер и hello флаг «EnableActiveActiveFeature».</span><span class="sxs-lookup"><span data-stu-id="50387-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="50387-228">Обратите внимание, что по умолчанию hello ASN необходимо переопределить на шлюзах Azure VPN.</span><span class="sxs-lookup"><span data-stu-id="50387-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="50387-229">Hello ASN для hello подключенных виртуальных сетей должны быть разные tooenable BGP и транзитной маршрутизацией.</span><span class="sxs-lookup"><span data-stu-id="50387-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="50387-230">Шаг 2 — подключить hello TestVNet1 и TestVNet2 шлюзов</span><span class="sxs-lookup"><span data-stu-id="50387-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="50387-231">В этом примере обоих шлюзов находятся в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="50387-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="50387-232">На этом шаге hello можно завершить сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="50387-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="50387-233">1. Получение обоих шлюзов</span><span class="sxs-lookup"><span data-stu-id="50387-233">1. Get both gateways</span></span>
<span data-ttu-id="50387-234">Убедитесь, что вход и подключиться tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="50387-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="50387-235">2. Создание двух подключений</span><span class="sxs-lookup"><span data-stu-id="50387-235">2. Create both connections</span></span>
<span data-ttu-id="50387-236">На этом шаге вы создадите hello из TestVNet1 tooTestVNet2 и hello соединению из TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="50387-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="50387-237">Быть убедиться, что tooenable BGP для ОБОИХ подключений.</span><span class="sxs-lookup"><span data-stu-id="50387-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="50387-238">После выполнения этих действий, подключение hello наладят через несколько минут, и сеанс пиринга BGP hello будет копии после завершения подключения hello виртуальной сети для виртуальной сети с двумя избыточности:</span><span class="sxs-lookup"><span data-stu-id="50387-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![Подключение между виртуальными сетями в режиме "активный — активный"](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="50387-240"><a name ="aaupdate"></a>Часть 4. Обновление имеющегося шлюза между режимами "активный — активный" и "активный — резервный"</span><span class="sxs-lookup"><span data-stu-id="50387-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="50387-241">Последний раздел Hello описывается способ настройки существующего шлюза Azure VPN из активный резервный tooactive активный режим, или наоборот.</span><span class="sxs-lookup"><span data-stu-id="50387-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="50387-242">Этот раздел содержит tooresize hello действия прежних версий SKU (старый SKU) уже созданные VPN-шлюза, из стандартных tooHighPerformance.</span><span class="sxs-lookup"><span data-stu-id="50387-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="50387-243">Эти действия не обновлять старые прежних версий tooone SKU для hello новых SKU.</span><span class="sxs-lookup"><span data-stu-id="50387-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="50387-244">Настройте шлюз активный tooactive активный резервный шлюза</span><span class="sxs-lookup"><span data-stu-id="50387-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="50387-245">1. Параметры шлюза</span><span class="sxs-lookup"><span data-stu-id="50387-245">1. Gateway parameters</span></span>
<span data-ttu-id="50387-246">Следующий пример Hello преобразует шлюз активный резервный в активных шлюза.</span><span class="sxs-lookup"><span data-stu-id="50387-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="50387-247">Требуется toocreate другой общедоступный IP-адрес, а затем добавить второй конфигурацию IP-адрес шлюза.</span><span class="sxs-lookup"><span data-stu-id="50387-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="50387-248">Ниже показан hello использовать параметры:</span><span class="sxs-lookup"><span data-stu-id="50387-248">Below shows hello parameters used:</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="50387-249">2. Создать hello общедоступный IP-адрес, а затем добавьте hello второй шлюз IP-конфигурации</span><span class="sxs-lookup"><span data-stu-id="50387-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="50387-250">3. Включить шлюз hello активный / активный режим и обновление</span><span class="sxs-lookup"><span data-stu-id="50387-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="50387-251">Необходимо задать hello объекта шлюза в PowerShell tootrigger hello фактического обновления.</span><span class="sxs-lookup"><span data-stu-id="50387-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="50387-252">также необходимо изменить (размер) tooHighPerformance Hello SKU шлюза виртуальной сети hello, так как он был создан ранее, от стандартных.</span><span class="sxs-lookup"><span data-stu-id="50387-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="50387-253">Это обновление может занять 30 минут too45.</span><span class="sxs-lookup"><span data-stu-id="50387-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="50387-254">Настройте шлюз tooactive standby активных шлюза</span><span class="sxs-lookup"><span data-stu-id="50387-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="50387-255">1. Параметры шлюза</span><span class="sxs-lookup"><span data-stu-id="50387-255">1. Gateway parameters</span></span>
<span data-ttu-id="50387-256">Используйте hello же параметры, как описано выше, получить имя hello hello IP-конфигурации требуется tooremove.</span><span class="sxs-lookup"><span data-stu-id="50387-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="50387-257">2. Удалите IP-конфигурации шлюза hello и отключить hello активный / активный режим</span><span class="sxs-lookup"><span data-stu-id="50387-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="50387-258">Аналогичным образом необходимо задать hello объекта шлюза в PowerShell tootrigger hello фактического обновления.</span><span class="sxs-lookup"><span data-stu-id="50387-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="50387-259">Это обновление может занять too30 слишком 45 минут.</span><span class="sxs-lookup"><span data-stu-id="50387-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50387-260">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50387-260">Next steps</span></span>
<span data-ttu-id="50387-261">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="50387-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="50387-262">Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50387-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
