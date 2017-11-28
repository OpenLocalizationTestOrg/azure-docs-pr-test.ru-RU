---
title: "Настройка BGP на VPN-шлюзах Azure с помощью Resource Manager и PowerShell | Документы Майкрософт"
description: "В этой статье описана поэтапная настройка протокола BGP для VPN-шлюзов Azure с помощью Azure Resource Manager и PowerShell."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: b00a3fe7ba4b12c2e9c486188c292cd6fafb60a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="feb34-103">Настройка BGP на VPN-шлюзах Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="feb34-103">How to configure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="feb34-104">В этой статье содержится пошаговое описание процесса, который позволит с помощью модели развертывания Resource Manager и PowerShell включить BGP для VPN-подключения типа "сеть — сеть" (S2S), настроенного между локальными сетями, или для подключения между виртуальными сетями.</span><span class="sxs-lookup"><span data-stu-id="feb34-104">This article walks you through the steps to enable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="feb34-105">О протоколе BGP</span><span class="sxs-lookup"><span data-stu-id="feb34-105">About BGP</span></span>
<span data-ttu-id="feb34-106">Стандартный протокол маршрутизации BGP обычно используется в Интернете для обмена данными о маршрутизации и доступности между двумя или несколькими сетями.</span><span class="sxs-lookup"><span data-stu-id="feb34-106">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="feb34-107">Протокол BGP используется VPN-шлюзами Azure и локальными VPN-устройствами (так называемые узлы BGP) для обмена данными о маршрутах. Это позволяет информировать участников обмена о доступности и возможности передавать трафик для определенных сетей через шлюзы или маршрутизаторы.</span><span class="sxs-lookup"><span data-stu-id="feb34-107">BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="feb34-108">Также BGP позволяет передавать трафик транзитом через несколько сетей. Для этого шлюз BGP распространяет на все известные ему узлы BGP информацию о маршрутах, полученную от остальных узлов BGP.</span><span class="sxs-lookup"><span data-stu-id="feb34-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span>

<span data-ttu-id="feb34-109">В статье [Обзор использования BGP с VPN-шлюзами Azure](vpn-gateway-bgp-overview.md) приведены дополнительные сведения о преимуществах BGP, о технических требованиях и важных аспектах использования BGP.</span><span class="sxs-lookup"><span data-stu-id="feb34-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and to understand the technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="feb34-110">Приступая к работе с BGP на VPN-шлюзах Azure</span><span class="sxs-lookup"><span data-stu-id="feb34-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="feb34-111">В этой статье описано выполнение следующих действий:</span><span class="sxs-lookup"><span data-stu-id="feb34-111">This article walks you through the steps to do the following tasks:</span></span>

* [<span data-ttu-id="feb34-112">Часть 1 — активация BGP на VPN-шлюзе Azure</span><span class="sxs-lookup"><span data-stu-id="feb34-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="feb34-113">Часть 2 — создание подключения между локальными сетями с использованием BGP</span><span class="sxs-lookup"><span data-stu-id="feb34-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="feb34-114">Часть 3 — создание подключения между виртуальными сетями с использованием BGP</span><span class="sxs-lookup"><span data-stu-id="feb34-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="feb34-115">Каждая часть этой инструкции является базовым блоком для использования BGP в вашей сети.</span><span class="sxs-lookup"><span data-stu-id="feb34-115">Each part of the instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="feb34-116">Выполнив инструкции, приведенные в трех частях, вы создадите топологию, которая представлена на следующей схеме:</span><span class="sxs-lookup"><span data-stu-id="feb34-116">If you complete all three parts, you build the topology as shown in the following diagram:</span></span>

![Топология BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="feb34-118">Вы можете объединять блоки для создания более сложных, многоскачковых и транзитных сетей, в соответствии со своими задачами.</span><span class="sxs-lookup"><span data-stu-id="feb34-118">You can combine parts together to build a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="feb34-119"><a name ="enablebgp"></a>Часть 1 — настройка BGP для VPN-шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="feb34-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on the Azure VPN Gateway</span></span>
<span data-ttu-id="feb34-120">Описанные ниже действия позволят настроить параметры BGP для VPN-шлюза Azure в соответствии со следующей схемой:</span><span class="sxs-lookup"><span data-stu-id="feb34-120">The configuration steps set up the BGP parameters of the Azure VPN gateway as shown in the following diagram:</span></span>

![Шлюз BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="feb34-122">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="feb34-122">Before you begin</span></span>
* <span data-ttu-id="feb34-123">Убедитесь в том, что у вас уже есть подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="feb34-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="feb34-124">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="feb34-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="feb34-125">Установите командлеты PowerShell для Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="feb34-125">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="feb34-126">См. дополнительные сведения об [установке и настройке командлетов Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="feb34-126">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="feb34-127">Шаг 1. Создание и настройка VNet1</span><span class="sxs-lookup"><span data-stu-id="feb34-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="feb34-128">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="feb34-128">1. Declare your variables</span></span>
<span data-ttu-id="feb34-129">В этом упражнении мы начнем с объявления переменных.</span><span class="sxs-lookup"><span data-stu-id="feb34-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="feb34-130">В примере ниже объявлены переменные со значениями для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="feb34-130">The following example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="feb34-131">Обязательно замените значения своими при настройке для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="feb34-131">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="feb34-132">Эти переменные можно использовать для ознакомления с этим типом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="feb34-132">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="feb34-133">Измените переменные, а затем скопируйте и вставьте код в консоль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="feb34-133">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="feb34-134">2) Подключение к подписке Azure и создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="feb34-134">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="feb34-135">Для работы с командлетами Resource Manager необходимо переключиться в режим PowerShell.</span><span class="sxs-lookup"><span data-stu-id="feb34-135">To use the Resource Manager cmdlets, Make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="feb34-136">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="feb34-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="feb34-137">Откройте консоль PowerShell и подключитесь к своей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="feb34-137">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="feb34-138">Для подключения используйте следующий пример.</span><span class="sxs-lookup"><span data-stu-id="feb34-138">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="feb34-139">3. Создание TestVNet1</span><span class="sxs-lookup"><span data-stu-id="feb34-139">3. Create TestVNet1</span></span>
<span data-ttu-id="feb34-140">В примере ниже создается виртуальная сеть с именем TestVNet1 и три подсети: GatewaySubnet, FrontEnd и Backend.</span><span class="sxs-lookup"><span data-stu-id="feb34-140">The following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="feb34-141">При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="feb34-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="feb34-142">Если вы используете другое имя, создание шлюза завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="feb34-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="feb34-143">Шаг 2. Создание VPN-шлюза для TestVNet1 с параметрами BGP</span><span class="sxs-lookup"><span data-stu-id="feb34-143">Step 2 - Create the VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-the-ip-and-subnet-configurations"></a><span data-ttu-id="feb34-144">1. Настройка IP-адресов и подсети</span><span class="sxs-lookup"><span data-stu-id="feb34-144">1. Create the IP and subnet configurations</span></span>
<span data-ttu-id="feb34-145">Запросите выделение общедоступного IP-адреса для шлюза, который будет создан для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="feb34-145">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="feb34-146">Также следует определить необходимые конфигурации подсети и IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="feb34-146">You'll also define the required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a><span data-ttu-id="feb34-147">2. Создание VPN-шлюза с номером AS</span><span class="sxs-lookup"><span data-stu-id="feb34-147">2. Create the VPN gateway with the AS number</span></span>
<span data-ttu-id="feb34-148">Создайте шлюз для виртуальной сети TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="feb34-148">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="feb34-149">Для использования BGP обязательно нужен VPN-шлюз на основе маршрутов, а также дополнительный параметр -Asn, который задает номер ASN для TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="feb34-149">BGP requires a Route-Based VPN gateway, and also the addition parameter, -Asn, to set the ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="feb34-150">Если параметр ASN не указан, будет назначено значение ASN 65515.</span><span class="sxs-lookup"><span data-stu-id="feb34-150">If you do not set the ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="feb34-151">Создание шлюза может занять некоторое время (30 минут или более).</span><span class="sxs-lookup"><span data-stu-id="feb34-151">Creating a gateway can take a while (30 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a><span data-ttu-id="feb34-152">3. Получение IP-адреса для узла Azure BGP</span><span class="sxs-lookup"><span data-stu-id="feb34-152">3. Obtain the Azure BGP Peer IP address</span></span>
<span data-ttu-id="feb34-153">После создания шлюза необходимо получить IP-адрес для узла BGP на VPN-шлюзе Azure.</span><span class="sxs-lookup"><span data-stu-id="feb34-153">Once the gateway is created, you need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="feb34-154">Этот адрес нужен, чтобы VPN-шлюз Azure мог выполнять роль узла BGP для локальных VPN-устройств.</span><span class="sxs-lookup"><span data-stu-id="feb34-154">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="feb34-155">Последняя команда выводит соответствующую конфигурацию BGP для VPN-шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="feb34-155">The last command shows the corresponding BGP configurations on the Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="feb34-156">С помощью созданного шлюза можно установить подключение между локальными или виртуальными сетями с использованием BGP.</span><span class="sxs-lookup"><span data-stu-id="feb34-156">Once the gateway is created, you can use this gateway to establish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="feb34-157">В следующих разделах описано, как это сделать.</span><span class="sxs-lookup"><span data-stu-id="feb34-157">The following sections walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="feb34-158"><a name ="crossprembbgp"></a>Часть 2 — создание подключения между локальными сетями с использованием BGP</span><span class="sxs-lookup"><span data-stu-id="feb34-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="feb34-159">Чтобы установить подключение между локальными сетями, нужно создать локальный сетевой шлюз, который будет представлять локальное VPN-устройство, а также подключение между VPN-шлюзом и шлюзом локальной сети.</span><span class="sxs-lookup"><span data-stu-id="feb34-159">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the VPN gateway with the local network gateway.</span></span> <span data-ttu-id="feb34-160">Несмотря на то что эти действия подробно описаны в других статьях, в этой статье указаны дополнительные свойства, необходимые для параметров конфигурации BGP.</span><span class="sxs-lookup"><span data-stu-id="feb34-160">While there are articles that walk you through these steps, this article contains the additional properties required to specify the BGP configuration parameters.</span></span>

![BGP между локальными сетями](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="feb34-162">Прежде чем продолжить, убедитесь, что вы выполнили инструкции из [первой части](#enablebgp) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="feb34-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="feb34-163">Шаг 1. Создание и настройка локального сетевого шлюза</span><span class="sxs-lookup"><span data-stu-id="feb34-163">Step 1 - Create and configure the local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="feb34-164">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="feb34-164">1. Declare your variables</span></span>

<span data-ttu-id="feb34-165">В этом подразделе мы продолжим создание конфигурации, которая представлена на схеме.</span><span class="sxs-lookup"><span data-stu-id="feb34-165">This exercise continues to build the configuration shown in the diagram.</span></span> <span data-ttu-id="feb34-166">Не забудьте заменить значения теми, которые вы хотите использовать для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="feb34-166">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="feb34-167">Несколько важных замечаний о параметрах локального сетевого шлюза.</span><span class="sxs-lookup"><span data-stu-id="feb34-167">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="feb34-168">Локальный сетевой шлюз может находиться в том же расположении, что и VPN-шлюз, или в любом другом. Это же справедливо в отношении групп ресурсов.</span><span class="sxs-lookup"><span data-stu-id="feb34-168">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="feb34-169">В нашем примере они располагаются в разных группах ресурсов и расположениях.</span><span class="sxs-lookup"><span data-stu-id="feb34-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="feb34-170">Минимальный префикс, который необходимо объявить для локального сетевого шлюза — это IP-адрес узла BGP на вашем VPN-устройстве.</span><span class="sxs-lookup"><span data-stu-id="feb34-170">The minimum prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="feb34-171">В нашем примере это префикс /32 для адреса 10.52.255.254/32.</span><span class="sxs-lookup"><span data-stu-id="feb34-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="feb34-172">Не забывайте, что для локальных сетей и виртуальной сети Azure должны быть указаны разные номера ASN BGP.</span><span class="sxs-lookup"><span data-stu-id="feb34-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="feb34-173">Если они совпадают, а локальное VPN-устройство уже использует свой ASN для связи с другими соседями BGP, необходимо изменить ASN вашей виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="feb34-173">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

<span data-ttu-id="feb34-174">Прежде чем продолжить, убедитесь, что вы все еще подключены к подписке 1.</span><span class="sxs-lookup"><span data-stu-id="feb34-174">Before you continue, make sure you are still connected to Subscription 1.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="feb34-175">2. Создание локального сетевого шлюза для сети Site5</span><span class="sxs-lookup"><span data-stu-id="feb34-175">2. Create the local network gateway for Site5</span></span>

<span data-ttu-id="feb34-176">Прежде чем создавать локальный сетевой шлюз, не забудьте создать группу ресурсов, если она не была создана ранее.</span><span class="sxs-lookup"><span data-stu-id="feb34-176">Be sure to create the resource group if it is not created, before you create the local network gateway.</span></span> <span data-ttu-id="feb34-177">Обратите внимание на два дополнительных параметра локального сетевого шлюза: Asn и BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="feb34-177">Notice the two additional parameters for the local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="feb34-178">Шаг 2. Подключение шлюза виртуальной сети к локальному сетевому шлюзу</span><span class="sxs-lookup"><span data-stu-id="feb34-178">Step 2 - Connect the VNet gateway and local network gateway</span></span>

#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="feb34-179">1. Получение обоих шлюзов</span><span class="sxs-lookup"><span data-stu-id="feb34-179">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="feb34-180">2) Создание подключения между TestVNet1 и Site5</span><span class="sxs-lookup"><span data-stu-id="feb34-180">2. Create the TestVNet1 to Site5 connection</span></span>

<span data-ttu-id="feb34-181">На этом шаге вы создадите подключение между TestVNet1 и Site5.</span><span class="sxs-lookup"><span data-stu-id="feb34-181">In this step, you create the connection from TestVNet1 to Site5.</span></span> <span data-ttu-id="feb34-182">Чтобы активировать BGP для этого подключения, укажите параметр -EnableBGP True.</span><span class="sxs-lookup"><span data-stu-id="feb34-182">You must specify "-EnableBGP $True" to enable BGP for this connection.</span></span> <span data-ttu-id="feb34-183">Как обсуждалось ранее, на одном VPN-шлюзе можно одновременно создавать подключения с использованием BGP и без него.</span><span class="sxs-lookup"><span data-stu-id="feb34-183">As discussed earlier, it is possible to have both BGP and non-BGP connections for the same Azure VPN Gateway.</span></span> <span data-ttu-id="feb34-184">Если BGP не указано в свойствах подключения явным образом, Azure не будет использовать BGP для этого подключения, даже если параметры BGP настроены для обоих шлюзов.</span><span class="sxs-lookup"><span data-stu-id="feb34-184">Unless BGP is enabled in the connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="feb34-185">В следующем примере перечислены параметры, которые следует ввести в разделе конфигурации BGP на локальном VPN-устройстве для нашего упражнения.</span><span class="sxs-lookup"><span data-stu-id="feb34-185">The following example lists the parameters you enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="feb34-186">Подключение установится через несколько минут. Сразу после создания подключения IPsec начнется сеанс пиринга BGP.</span><span class="sxs-lookup"><span data-stu-id="feb34-186">The connection is established after a few minutes, and the BGP peering session starts once the IPsec connection is established.</span></span>

## <span data-ttu-id="feb34-187"><a name ="v2vbgp"></a>Часть 3 — создание подключения между виртуальными сетями с использованием BGP</span><span class="sxs-lookup"><span data-stu-id="feb34-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="feb34-188">В этом разделе мы добавим подключение между виртуальными сетями с использованием BGP, как показано на следующей схеме:</span><span class="sxs-lookup"><span data-stu-id="feb34-188">This section adds a VNet-to-VNet connection with BGP, as shown in the following diagram:</span></span>

![BGP между виртуальными сетями](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="feb34-190">Приведенные ниже инструкции продолжают действия, описанные выше.</span><span class="sxs-lookup"><span data-stu-id="feb34-190">The following instructions continue from the previous steps.</span></span> <span data-ttu-id="feb34-191">Чтобы создать и настроить сеть TestVNet1 и VPN-шлюз с использованием BGP, сначала следует выполнить инструкции из [первой части](#enablebgp) .</span><span class="sxs-lookup"><span data-stu-id="feb34-191">You must complete [Part I](#enablebgp) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="feb34-192">Шаг 1. Создание TestVNet2 и VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="feb34-192">Step 1 - Create TestVNet2 and the VPN gateway</span></span>

<span data-ttu-id="feb34-193">Важно убедиться в том, что пространство IP-адресов для новой виртуальной сети TestVNet2 не пересекается с диапазонами любой из ваших виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="feb34-193">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="feb34-194">В этом примере виртуальные сети относятся к одной подписке.</span><span class="sxs-lookup"><span data-stu-id="feb34-194">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="feb34-195">Вы можете создавать подключения между виртуальным сетями из разных подписок.</span><span class="sxs-lookup"><span data-stu-id="feb34-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="feb34-196">Дополнительные сведения см. в статье [Настройка подключения VPN-шлюза между виртуальными сетями с помощью PowerShell](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="feb34-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="feb34-197">Чтобы использовать для подключения протокол BGP, обязательно укажите параметр -EnableBgp True при создании подключения.</span><span class="sxs-lookup"><span data-stu-id="feb34-197">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="feb34-198">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="feb34-198">1. Declare your variables</span></span>

<span data-ttu-id="feb34-199">Не забудьте заменить значения теми, которые вы хотите использовать для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="feb34-199">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="feb34-200">2) Создание сети TestVNet2 в новой группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="feb34-200">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="feb34-201">3. Создание VPN-шлюза для TestVNet2 с параметрами BGP</span><span class="sxs-lookup"><span data-stu-id="feb34-201">3. Create the VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="feb34-202">Запросите выделение общедоступного IP-адреса для шлюза, который будет создан для виртуальной сети, и определите необходимые конфигурации подсети и IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="feb34-202">Request a public IP address to be allocated to the gateway you will create for your VNet and define the required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="feb34-203">Создайте VPN-шлюз с номером AS.</span><span class="sxs-lookup"><span data-stu-id="feb34-203">Create the VPN gateway with the AS number.</span></span> <span data-ttu-id="feb34-204">Номер ASN по умолчанию необходимо переопределить для ваших VPN-шлюзов Azure.</span><span class="sxs-lookup"><span data-stu-id="feb34-204">You must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="feb34-205">Номера ASN для подключенных виртуальных сетей должны быть разными, чтобы работал протокол BGP и транзитная маршрутизация.</span><span class="sxs-lookup"><span data-stu-id="feb34-205">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="feb34-206">Шаг 2. Подключение шлюзов TestVNet1 и TestVNet2</span><span class="sxs-lookup"><span data-stu-id="feb34-206">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="feb34-207">В этом примере оба шлюза находятся в одной подписке.</span><span class="sxs-lookup"><span data-stu-id="feb34-207">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="feb34-208">Этот шаг можно выполнить в одном сеансе PowerShell.</span><span class="sxs-lookup"><span data-stu-id="feb34-208">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="feb34-209">1. Получение обоих шлюзов</span><span class="sxs-lookup"><span data-stu-id="feb34-209">1. Get both gateways</span></span>

<span data-ttu-id="feb34-210">Обязательно войдите и подключитесь к подписке 1.</span><span class="sxs-lookup"><span data-stu-id="feb34-210">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="feb34-211">2) Создание двух подключений</span><span class="sxs-lookup"><span data-stu-id="feb34-211">2. Create both connections</span></span>

<span data-ttu-id="feb34-212">На этом шаге вы создадите подключение из TestVNet1 к TestVNet2, а также подключение из TestVNet2 к TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="feb34-212">In this step, you create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="feb34-213">Не забудьте включить BGP для ОБОИХ подключений.</span><span class="sxs-lookup"><span data-stu-id="feb34-213">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="feb34-214">Подключение будет установлено через несколько минут после выполнения этих действий.</span><span class="sxs-lookup"><span data-stu-id="feb34-214">After completing these steps, the connection is established after a few minutes.</span></span> <span data-ttu-id="feb34-215">Сразу после создания подключения между виртуальными сетями начнется сеанс пиринга BGP.</span><span class="sxs-lookup"><span data-stu-id="feb34-215">The BGP peering session is up once the VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="feb34-216">Если вы выполнили все три части этого упражнения, ваша сеть будет иметь примерно такую топологию:</span><span class="sxs-lookup"><span data-stu-id="feb34-216">If you completed all three parts of this exercise, you have established the following network topology:</span></span>

![BGP между виртуальными сетями](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="feb34-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="feb34-218">Next steps</span></span>

<span data-ttu-id="feb34-219">Установив подключение, можно добавить виртуальные машины в виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="feb34-219">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="feb34-220">Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="feb34-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>