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
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="63dd0-103">Как tooconfigure BGP на шлюзах VPN Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="63dd0-103">How tooconfigure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="63dd0-104">В этой статье описывается tooenable действия hello BGP на-сайтами (S2S) VPN-подключения между организациями и подключение к виртуальной сети для виртуальной сети, с помощью модели развертывания диспетчера ресурсов hello и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63dd0-104">This article walks you through hello steps tooenable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="63dd0-105">О протоколе BGP</span><span class="sxs-lookup"><span data-stu-id="63dd0-105">About BGP</span></span>
<span data-ttu-id="63dd0-106">BGP — hello протокол маршрутизации обычно используется в hello информации через Интернет tooexchange маршрутизации и возможности доступа между двумя или более сетями.</span><span class="sxs-lookup"><span data-stu-id="63dd0-106">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="63dd0-107">BGP обеспечивает VPN-шлюзы Azure hello и VPN-устройства локальной называется узлов BGP или соседей, tooexchange «маршруты» сообщит обоих шлюзов на доступность hello и возможности доступа для тех префиксов toogo через hello шлюзы или маршрутизаторы участвующих.</span><span class="sxs-lookup"><span data-stu-id="63dd0-107">BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="63dd0-108">BGP можно также включить транзитной маршрутизацией среди нескольких сетей, распространение маршрутов BGP шлюз узнает из одного tooall однорангового узла BGP других узлов BGP.</span><span class="sxs-lookup"><span data-stu-id="63dd0-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span>

<span data-ttu-id="63dd0-109">В разделе [Обзор BGP со шлюзами VPN Azure](vpn-gateway-bgp-overview.md) дополнительную информацию о преимуществах BGP и toounderstand hello технических требований и рекомендаций, связанных с помощью BGP.</span><span class="sxs-lookup"><span data-stu-id="63dd0-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and toounderstand hello technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="63dd0-110">Приступая к работе с BGP на VPN-шлюзах Azure</span><span class="sxs-lookup"><span data-stu-id="63dd0-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="63dd0-111">В этой статье рассматриваются hello действия toodo hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="63dd0-111">This article walks you through hello steps toodo hello following tasks:</span></span>

* [<span data-ttu-id="63dd0-112">Часть 1 — активация BGP на VPN-шлюзе Azure</span><span class="sxs-lookup"><span data-stu-id="63dd0-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="63dd0-113">Часть 2 — создание подключения между локальными сетями с использованием BGP</span><span class="sxs-lookup"><span data-stu-id="63dd0-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="63dd0-114">Часть 3 — создание подключения между виртуальными сетями с использованием BGP</span><span class="sxs-lookup"><span data-stu-id="63dd0-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="63dd0-115">Каждая часть инструкции hello forms это основной стандартный блок для включения BGP в сетевое подключение.</span><span class="sxs-lookup"><span data-stu-id="63dd0-115">Each part of hello instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="63dd0-116">Если вы прошли все три части, как показано в hello, следующая схема сборки hello топологии:</span><span class="sxs-lookup"><span data-stu-id="63dd0-116">If you complete all three parts, you build hello topology as shown in hello following diagram:</span></span>

![Топология BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="63dd0-118">Можно объединять части вместе toobuild более сложных, мульти-прыжка транзитной сети, соответствующий вашим потребностям.</span><span class="sxs-lookup"><span data-stu-id="63dd0-118">You can combine parts together toobuild a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="63dd0-119"><a name ="enablebgp"></a>Часть 1 — Настройка BGP на hello Azure VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="63dd0-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on hello Azure VPN Gateway</span></span>
<span data-ttu-id="63dd0-120">действия по настройке Hello настроить hello параметров BGP hello шлюза Azure VPN как показано в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="63dd0-120">hello configuration steps set up hello BGP parameters of hello Azure VPN gateway as shown in hello following diagram:</span></span>

![Шлюз BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="63dd0-122">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="63dd0-122">Before you begin</span></span>
* <span data-ttu-id="63dd0-123">Убедитесь в том, что у вас уже есть подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="63dd0-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="63dd0-124">Если у вас нет подписки Azure, вы можете [активировать преимущества для подписчиков MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) или [зарегистрировать бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63dd0-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="63dd0-125">Установите командлеты PowerShell диспетчера ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="63dd0-125">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="63dd0-126">Дополнительные сведения об установке hello командлеты PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="63dd0-126">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="63dd0-127">Шаг 1. Создание и настройка VNet1</span><span class="sxs-lookup"><span data-stu-id="63dd0-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="63dd0-128">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="63dd0-128">1. Declare your variables</span></span>
<span data-ttu-id="63dd0-129">В этом упражнении мы начнем с объявления переменных.</span><span class="sxs-lookup"><span data-stu-id="63dd0-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="63dd0-130">Hello следующий пример hello переменных объявляются с помощью hello значения для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="63dd0-130">hello following example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="63dd0-131">Быть убедиться, что значения hello tooreplace собственными при настройке для рабочей среды.</span><span class="sxs-lookup"><span data-stu-id="63dd0-131">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="63dd0-132">Эти переменные можно использовать при выполнении через toobecome действия hello знакомы с этим типом конфигурации.</span><span class="sxs-lookup"><span data-stu-id="63dd0-132">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="63dd0-133">Изменение переменных hello, а затем скопируйте и вставьте в консоль PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63dd0-133">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="63dd0-134">2. Подключить tooyour подписки и создать новую группу ресурсов</span><span class="sxs-lookup"><span data-stu-id="63dd0-134">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="63dd0-135">hello toouse командлеты диспетчера ресурсов убедитесь в том, что режима tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="63dd0-135">toouse hello Resource Manager cmdlets, Make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="63dd0-136">Дополнительные сведения см. в статье [Использование Azure PowerShell с диспетчером ресурсов Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="63dd0-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="63dd0-137">Откройте консоль PowerShell и подключить tooyour учетную запись.</span><span class="sxs-lookup"><span data-stu-id="63dd0-137">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="63dd0-138">Используйте следующий пример toohelp подключении hello.</span><span class="sxs-lookup"><span data-stu-id="63dd0-138">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="63dd0-139">3. Создание TestVNet1</span><span class="sxs-lookup"><span data-stu-id="63dd0-139">3. Create TestVNet1</span></span>
<span data-ttu-id="63dd0-140">Hello следующий пример создает виртуальную сеть с именем TestVNet1 и три подсети, один именем GatewaySubnet, одной вызываемой переднего плана и один внутренний вызван.</span><span class="sxs-lookup"><span data-stu-id="63dd0-140">hello following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="63dd0-141">При замене значений важно, чтобы вы назвали подсеть шлюза именем GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="63dd0-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="63dd0-142">Если вы используете другое имя, создание шлюза завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="63dd0-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="63dd0-143">Шаг 2 — Создание hello VPN-шлюза для TestVNet1 с параметрами BGP</span><span class="sxs-lookup"><span data-stu-id="63dd0-143">Step 2 - Create hello VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-hello-ip-and-subnet-configurations"></a><span data-ttu-id="63dd0-144">1. Создайте hello конфигурации IP-адресов и подсети</span><span class="sxs-lookup"><span data-stu-id="63dd0-144">1. Create hello IP and subnet configurations</span></span>
<span data-ttu-id="63dd0-145">Запрос открытый IP-адрес toobe toohello выделенный шлюз, создаваемых для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="63dd0-145">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="63dd0-146">Также мы определим hello требуется подсеть и IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="63dd0-146">You'll also define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a><span data-ttu-id="63dd0-147">2. Создайте шлюз VPN hello hello как число</span><span class="sxs-lookup"><span data-stu-id="63dd0-147">2. Create hello VPN gateway with hello AS number</span></span>
<span data-ttu-id="63dd0-148">Создание шлюза виртуальной сети hello для TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="63dd0-148">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="63dd0-149">BGP требуется TestVNet1 типа на основе маршрутов VPN-шлюза, а также hello сложения параметр - Asn, tooset hello ASN (номер AS).</span><span class="sxs-lookup"><span data-stu-id="63dd0-149">BGP requires a Route-Based VPN gateway, and also hello addition parameter, -Asn, tooset hello ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="63dd0-150">Если не задан параметр ASN hello, назначается ASN 65515.</span><span class="sxs-lookup"><span data-stu-id="63dd0-150">If you do not set hello ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="63dd0-151">Создание шлюза может занять некоторое время (30 минут или более toocomplete).</span><span class="sxs-lookup"><span data-stu-id="63dd0-151">Creating a gateway can take a while (30 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a><span data-ttu-id="63dd0-152">3. Получить hello Azure BGP однорангового узла, IP-адрес</span><span class="sxs-lookup"><span data-stu-id="63dd0-152">3. Obtain hello Azure BGP Peer IP address</span></span>
<span data-ttu-id="63dd0-153">После создания шлюза hello требуется tooobtain hello IP-однорангового узла BGP адрес на hello шлюза VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="63dd0-153">Once hello gateway is created, you need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="63dd0-154">Этот адрес будет hello необходимые tooconfigure VPN-шлюз Azure как узла BGP для VPN-устройства в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="63dd0-154">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="63dd0-155">Последняя команда Hello показывает hello соответствующей конфигурации BGP hello VPN-шлюз Azure; Например:</span><span class="sxs-lookup"><span data-stu-id="63dd0-155">hello last command shows hello corresponding BGP configurations on hello Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="63dd0-156">После создания шлюза hello с протоколом BGP можно использовать этот шлюз tooestablish между организациями подключение или подключение виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="63dd0-156">Once hello gateway is created, you can use this gateway tooestablish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="63dd0-157">Hello следующие разделы содержат пошаговые инструкции hello действия toocomplete hello упражнении.</span><span class="sxs-lookup"><span data-stu-id="63dd0-157">hello following sections walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="63dd0-158"><a name ="crossprembbgp"></a>Часть 2 — создание подключения между локальными сетями с использованием BGP</span><span class="sxs-lookup"><span data-stu-id="63dd0-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="63dd0-159">tooestablish подключения между организациями необходимо toocreate toorepresent шлюза локальной сети VPN-устройства в локальной среде и hello VPN-подключения tooconnect шлюза с hello шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="63dd0-159">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="63dd0-160">Хотя статей, которые помогают выполнить эти действия, в этой статье содержатся параметры конфигурации BGP hello необходимые toospecify hello дополнительные свойства.</span><span class="sxs-lookup"><span data-stu-id="63dd0-160">While there are articles that walk you through these steps, this article contains hello additional properties required toospecify hello BGP configuration parameters.</span></span>

![BGP между локальными сетями](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="63dd0-162">Прежде чем продолжить, убедитесь, что вы выполнили инструкции из [первой части](#enablebgp) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="63dd0-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="63dd0-163">Шаг 1. Создание и настройка шлюза локальной сети hello</span><span class="sxs-lookup"><span data-stu-id="63dd0-163">Step 1 - Create and configure hello local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="63dd0-164">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="63dd0-164">1. Declare your variables</span></span>

<span data-ttu-id="63dd0-165">В этом упражнении продолжается конфигурации hello toobuild иллюстрации hello.</span><span class="sxs-lookup"><span data-stu-id="63dd0-165">This exercise continues toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="63dd0-166">Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="63dd0-166">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="63dd0-167">Несколько вещей toonote относительно hello параметры шлюза локальной сети:</span><span class="sxs-lookup"><span data-stu-id="63dd0-167">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="63dd0-168">Hello шлюза локальной сети может быть в hello таким же или другое расположение и ресурсов группы как hello шлюза VPN.</span><span class="sxs-lookup"><span data-stu-id="63dd0-168">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="63dd0-169">В нашем примере они располагаются в разных группах ресурсов и расположениях.</span><span class="sxs-lookup"><span data-stu-id="63dd0-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="63dd0-170">адрес узла hello ваш адрес BGP одноранговых IP на VPN-устройства используется префикс минимальное Hello, требуется toodeclare hello шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="63dd0-170">hello minimum prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="63dd0-171">В нашем примере это префикс /32 для адреса 10.52.255.254/32.</span><span class="sxs-lookup"><span data-stu-id="63dd0-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="63dd0-172">Не забывайте, что для локальных сетей и виртуальной сети Azure должны быть указаны разные номера ASN BGP.</span><span class="sxs-lookup"><span data-stu-id="63dd0-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="63dd0-173">Если они являются одинаковыми hello, необходимо toochange вашей виртуальной сети ASN Если VPN-устройства локальной уже использует hello ASN toopeer с соседним узлам BGP.</span><span class="sxs-lookup"><span data-stu-id="63dd0-173">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

<span data-ttu-id="63dd0-174">Прежде чем продолжить, убедитесь, что будут по-прежнему подключенных tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="63dd0-174">Before you continue, make sure you are still connected tooSubscription 1.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="63dd0-175">2. Создание шлюза локальной сети hello для Site5</span><span class="sxs-lookup"><span data-stu-id="63dd0-175">2. Create hello local network gateway for Site5</span></span>

<span data-ttu-id="63dd0-176">Убедиться, что группа ресурсов hello toocreate быть в том случае, если она не была создана, прежде чем создать шлюз локальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="63dd0-176">Be sure toocreate hello resource group if it is not created, before you create hello local network gateway.</span></span> <span data-ttu-id="63dd0-177">Обратите внимание, hello два дополнительных параметров для шлюза локальной сети hello: BgpPeerAddress и Asn.</span><span class="sxs-lookup"><span data-stu-id="63dd0-177">Notice hello two additional parameters for hello local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="63dd0-178">Шаг 2 - подключения шлюза виртуальной сети hello и шлюз локальной сети</span><span class="sxs-lookup"><span data-stu-id="63dd0-178">Step 2 - Connect hello VNet gateway and local network gateway</span></span>

#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="63dd0-179">1. Получить hello двумя шлюзами</span><span class="sxs-lookup"><span data-stu-id="63dd0-179">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="63dd0-180">2. Создание подключения tooSite5 TestVNet1 hello</span><span class="sxs-lookup"><span data-stu-id="63dd0-180">2. Create hello TestVNet1 tooSite5 connection</span></span>

<span data-ttu-id="63dd0-181">На этом этапе можно создать подключение hello TestVNet1 tooSite5.</span><span class="sxs-lookup"><span data-stu-id="63dd0-181">In this step, you create hello connection from TestVNet1 tooSite5.</span></span> <span data-ttu-id="63dd0-182">Необходимо указать «-EnableBGP $True» tooenable BGP для этого подключения.</span><span class="sxs-lookup"><span data-stu-id="63dd0-182">You must specify "-EnableBGP $True" tooenable BGP for this connection.</span></span> <span data-ttu-id="63dd0-183">Как было сказано ранее, это возможных toohave BGP и не BGP подключения hello же шлюза VPN Azure.</span><span class="sxs-lookup"><span data-stu-id="63dd0-183">As discussed earlier, it is possible toohave both BGP and non-BGP connections for hello same Azure VPN Gateway.</span></span> <span data-ttu-id="63dd0-184">Если включен протокол BGP в свойстве соединения hello, Azure не включит BGP для этого подключения несмотря на то, что параметры BGP уже настроены для обоих шлюзов.</span><span class="sxs-lookup"><span data-stu-id="63dd0-184">Unless BGP is enabled in hello connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="63dd0-185">Hello следующий пример формирует список параметров Привет вводимых вами в hello BGP раздел конфигурации для локального VPN-устройства для этого упражнения.</span><span class="sxs-lookup"><span data-stu-id="63dd0-185">hello following example lists hello parameters you enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="63dd0-186">Hello подключение выполняется через несколько минут и запускает сеанс пиринга BGP hello после установления соединения IPsec hello.</span><span class="sxs-lookup"><span data-stu-id="63dd0-186">hello connection is established after a few minutes, and hello BGP peering session starts once hello IPsec connection is established.</span></span>

## <span data-ttu-id="63dd0-187"><a name ="v2vbgp"></a>Часть 3 — создание подключения между виртуальными сетями с использованием BGP</span><span class="sxs-lookup"><span data-stu-id="63dd0-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="63dd0-188">В этом разделе добавит подключение виртуальной сети для виртуальной сети с протоколом BGP, как показано на hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="63dd0-188">This section adds a VNet-to-VNet connection with BGP, as shown in hello following diagram:</span></span>

![BGP между виртуальными сетями](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="63dd0-190">Привет, следуя инструкциям по-прежнему hello предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="63dd0-190">hello following instructions continue from hello previous steps.</span></span> <span data-ttu-id="63dd0-191">Необходимо выполнить [части I](#enablebgp) toocreate hello VPN-шлюз с BGP и настроите TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="63dd0-191">You must complete [Part I](#enablebgp) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="63dd0-192">Шаг 1 — Создание TestVNet2 и hello VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="63dd0-192">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>

<span data-ttu-id="63dd0-193">Это важные toomake в том, что пространство IP-адресов hello hello новой виртуальной сети, TestVNet2, не перекрываются с диапазонов виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="63dd0-193">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="63dd0-194">В этом примере hello виртуальные сети относятся toohello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="63dd0-194">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="63dd0-195">Вы можете создавать подключения между виртуальным сетями из разных подписок.</span><span class="sxs-lookup"><span data-stu-id="63dd0-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="63dd0-196">Дополнительные сведения см. в статье [Настройка подключения VPN-шлюза между виртуальными сетями с помощью PowerShell](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="63dd0-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="63dd0-197">Убедитесь, что добавить hello»-EnableBgp $True» при создании hello tooenable подключений BGP.</span><span class="sxs-lookup"><span data-stu-id="63dd0-197">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="63dd0-198">1. Объявление переменных</span><span class="sxs-lookup"><span data-stu-id="63dd0-198">1. Declare your variables</span></span>

<span data-ttu-id="63dd0-199">Быть убедиться, что tooreplace hello значениями hello из них требуется toouse для вашей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="63dd0-199">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="63dd0-200">2. Создание TestVNet2 в новую группу ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="63dd0-200">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="63dd0-201">3. Создание VPN-шлюз hello для TestVNet2 с параметрами BGP</span><span class="sxs-lookup"><span data-stu-id="63dd0-201">3. Create hello VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="63dd0-202">Запрос открытый IP-адрес toobe выделенный toohello шлюза вы создадите для виртуальной сети и определите необходимые hello подсети и IP-конфигурации.</span><span class="sxs-lookup"><span data-stu-id="63dd0-202">Request a public IP address toobe allocated toohello gateway you will create for your VNet and define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="63dd0-203">Создайте шлюз VPN hello hello как число.</span><span class="sxs-lookup"><span data-stu-id="63dd0-203">Create hello VPN gateway with hello AS number.</span></span> <span data-ttu-id="63dd0-204">По умолчанию hello ASN необходимо переопределить на шлюзах Azure VPN.</span><span class="sxs-lookup"><span data-stu-id="63dd0-204">You must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="63dd0-205">Hello ASN для hello подключенных виртуальных сетей должны быть разные tooenable BGP и транзитной маршрутизацией.</span><span class="sxs-lookup"><span data-stu-id="63dd0-205">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="63dd0-206">Шаг 2 — подключить hello TestVNet1 и TestVNet2 шлюзов</span><span class="sxs-lookup"><span data-stu-id="63dd0-206">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="63dd0-207">В этом примере обоих шлюзов находятся в hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="63dd0-207">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="63dd0-208">На этом шаге hello можно завершить сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63dd0-208">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="63dd0-209">1. Получение обоих шлюзов</span><span class="sxs-lookup"><span data-stu-id="63dd0-209">1. Get both gateways</span></span>

<span data-ttu-id="63dd0-210">Убедитесь, что вход и подключиться tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="63dd0-210">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="63dd0-211">2. Создание двух подключений</span><span class="sxs-lookup"><span data-stu-id="63dd0-211">2. Create both connections</span></span>

<span data-ttu-id="63dd0-212">На этом этапе можно создать hello из TestVNet1 tooTestVNet2 и hello соединению с TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="63dd0-212">In this step, you create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="63dd0-213">Быть убедиться, что tooenable BGP для ОБОИХ подключений.</span><span class="sxs-lookup"><span data-stu-id="63dd0-213">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="63dd0-214">После выполнения этих действий, hello подключение выполняется через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="63dd0-214">After completing these steps, hello connection is established after a few minutes.</span></span> <span data-ttu-id="63dd0-215">сеанс пиринга BGP Hello работает после завершения hello подключения VNet-VNet.</span><span class="sxs-lookup"><span data-stu-id="63dd0-215">hello BGP peering session is up once hello VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="63dd0-216">Если вы выполнили все три части этого упражнения, вы установили hello следующие топологии сети:</span><span class="sxs-lookup"><span data-stu-id="63dd0-216">If you completed all three parts of this exercise, you have established hello following network topology:</span></span>

![BGP между виртуальными сетями](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="63dd0-218">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63dd0-218">Next steps</span></span>

<span data-ttu-id="63dd0-219">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="63dd0-219">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="63dd0-220">Инструкции см. в статье о [создании виртуальной машины](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="63dd0-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
