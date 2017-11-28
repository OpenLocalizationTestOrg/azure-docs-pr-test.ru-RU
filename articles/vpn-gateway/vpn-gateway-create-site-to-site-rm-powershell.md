---
title: "Подключение к локальной сети tooan виртуальной сети Azure: через виртуальную Частную сеть для: PowerShell | Документы Microsoft"
description: "Действия toocreate соединении по протоколу IPsec в локальной сети tooan виртуальной сети Azure через hello общедоступный Интернет. Они помогут вам создать подключение типа \"сеть — сеть\" с использованием VPN-шлюза и PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="646a3-104">Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="646a3-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="646a3-105">В этой статье показано, как toouse toocreate сайта для сайта PowerShell VPN-подключения шлюза в локальной сети toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="646a3-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="646a3-106">в этой статье инструкциям Hello применяются toohello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="646a3-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="646a3-107">Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.</span><span class="sxs-lookup"><span data-stu-id="646a3-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="646a3-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="646a3-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="646a3-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="646a3-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="646a3-110">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="646a3-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="646a3-111">Портал Azure (классический)</span><span class="sxs-lookup"><span data-stu-id="646a3-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="646a3-112">Классический портал (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="646a3-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="646a3-113">Используется tooconnect — подключение через виртуальную Частную сеть для шлюза в локальной сети tooan виртуальной сети Azure через туннель VPN IPsec/IKE (IKEv1 или IKEv2).</span><span class="sxs-lookup"><span data-stu-id="646a3-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="646a3-114">Этот тип подключения требуется VPN устройства, расположенного в локальной среде, имеет внешний tooit открытый IP-адрес, назначенный.</span><span class="sxs-lookup"><span data-stu-id="646a3-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="646a3-115">Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="646a3-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Схема подключения типа "сеть — сеть" через VPN-шлюз](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="646a3-117"><a name="before"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="646a3-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="646a3-118">Убедитесь, что выполнены следующие условия перед началом настройки hello:</span><span class="sxs-lookup"><span data-stu-id="646a3-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="646a3-119">Убедитесь, что у вас есть совместимых устройств VPN и тем, кто имеет доступ tooconfigure его.</span><span class="sxs-lookup"><span data-stu-id="646a3-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="646a3-120">Дополнительные сведения о совместимых устройствах VPN и их настройке см. в [этой статье](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="646a3-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="646a3-121">Убедитесь, что у вас есть общедоступный IPv4–адрес для вашего VPN–устройства.</span><span class="sxs-lookup"><span data-stu-id="646a3-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="646a3-122">Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="646a3-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="646a3-123">Если вы не знакомы с hello диапазоны IP-адресов в вашей локальной сети, конфигурации, необходимо toocoordinate с тем, кто сможет предоставить эти сведения для вас.</span><span class="sxs-lookup"><span data-stu-id="646a3-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="646a3-124">При создании этой конфигурации необходимо указать что Azure будет направлять в локальное расположение tooyour диапазон префиксов hello IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="646a3-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="646a3-125">Ни один из подсетей hello в локальной сети можно через Знакомство с функциями с hello подсети виртуальной сети, которые будут tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="646a3-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="646a3-126">Установите последнюю версию hello hello командлеты PowerShell диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="646a3-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="646a3-127">Командлеты PowerShell часто обновляются, и обычно требуется tooupdate PowerShell командлеты tooget hello последние функции функциональные возможности по работе.</span><span class="sxs-lookup"><span data-stu-id="646a3-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="646a3-128">Если не обновлять ваш командлеты PowerShell, hello значений, заданных может завершиться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="646a3-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="646a3-129">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) Дополнительные сведения о загрузке и установке командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="646a3-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="646a3-130"><a name="example"></a>Примеры значений</span><span class="sxs-lookup"><span data-stu-id="646a3-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="646a3-131">Hello примерах в этой статье используется hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="646a3-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="646a3-132">Можно использовать эти значения toocreate тестовой среде, или ссылаться toothem toobetter понять hello примеры в этой статье.</span><span class="sxs-lookup"><span data-stu-id="646a3-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="646a3-133"><a name="Login"></a>1. Подключение tooyour подписки</span><span class="sxs-lookup"><span data-stu-id="646a3-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="646a3-134"><a name="VNet"></a>2. Создание виртуальной сети и подсети шлюза</span><span class="sxs-lookup"><span data-stu-id="646a3-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="646a3-135">Если у вас нет виртуальной сети, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="646a3-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="646a3-136">При создании виртуальной сети, убедитесь, что hello адресные пространства, указываемые не перекрываются hello адресных пространств, в которых в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="646a3-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="646a3-137"><a name="vnet"></a>toocreate виртуальную сеть и подсеть шлюза</span><span class="sxs-lookup"><span data-stu-id="646a3-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="646a3-138">В этом примере создается виртуальная сеть и подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="646a3-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="646a3-139">При наличии виртуальной сети, которая требуется подсеть шлюза, чтобы увидеть tooadd [tooadd шлюз подсети tooa виртуальная сеть уже создан](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="646a3-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="646a3-140">Создайте группу ресурсов:</span><span class="sxs-lookup"><span data-stu-id="646a3-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="646a3-141">Создайте свою виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="646a3-141">Create your virtual network.</span></span>

1. <span data-ttu-id="646a3-142">Установка переменных hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="646a3-143">Создайте hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="646a3-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="646a3-144"><a name="gatewaysubnet"></a>tooadd tooa шлюз подсети виртуальной сети уже создан</span><span class="sxs-lookup"><span data-stu-id="646a3-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="646a3-145">Установка переменных hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="646a3-146">Создайте подсеть шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="646a3-147">Задание конфигурации hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="646a3-148">3. <a name="localnet"></a>Создание шлюза локальной сети hello</span><span class="sxs-lookup"><span data-stu-id="646a3-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="646a3-149">шлюз локальной сети Hello обычно относится tooyour в локальном расположении.</span><span class="sxs-lookup"><span data-stu-id="646a3-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="646a3-150">Присвоить имя, на который Azure можно ссылаться tooit, а затем укажите hello IP-адрес сайта hello объекта toowhich устройство VPN локальной hello будет создавать подключение.</span><span class="sxs-lookup"><span data-stu-id="646a3-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="646a3-151">Можно также указать префиксов hello IP-адресов, которые будет проходить через устройство VPN toohello шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="646a3-152">префиксы адресов Hello, указываемые являются префиксы hello в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="646a3-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="646a3-153">Если изменяется в локальной сети, можно легко обновлять префиксы hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="646a3-154">Используйте hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="646a3-154">Use hello following values:</span></span>

* <span data-ttu-id="646a3-155">Hello *GatewayIPAddress* — hello IP-адрес локального VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="646a3-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="646a3-156">Ваше VPN-устройство не может располагаться вне преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="646a3-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="646a3-157">Hello *AddressPrefix* это в локальной памяти.</span><span class="sxs-lookup"><span data-stu-id="646a3-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="646a3-158">tooadd шлюз локальной сети с префиксом один адрес:</span><span class="sxs-lookup"><span data-stu-id="646a3-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="646a3-159">tooadd шлюза локальной сети с помощью нескольких префиксов адреса:</span><span class="sxs-lookup"><span data-stu-id="646a3-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="646a3-160">toomodify префиксов IP-адресов для шлюза локальной сети:</span><span class="sxs-lookup"><span data-stu-id="646a3-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="646a3-161">Иногда префиксы адресов шлюза локальной сети могут изменяться.</span><span class="sxs-lookup"><span data-stu-id="646a3-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="646a3-162">Hello действия можно предпринять toomodify IP-адреса, от которых зависят префиксы создали шлюза VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="646a3-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="646a3-163">В разделе hello [префиксов изменение IP-адресов для шлюза локальной сети](#modify) этой статьи.</span><span class="sxs-lookup"><span data-stu-id="646a3-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="646a3-164"><a name="PublicIP"></a>4. Запрос общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="646a3-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="646a3-165">VPN-шлюз должен иметь общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="646a3-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="646a3-166">Запросить ресурс IP-адреса hello и затем ссылаться tooit при создании шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="646a3-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="646a3-167">Hello IP-адрес назначается динамически toohello ресурсов при создании шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="646a3-168">В настоящее время VPN-шлюз поддерживает только *динамическое* выделение общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="646a3-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="646a3-169">Вы не можете запросить назначение статического общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="646a3-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="646a3-170">Однако это не означает, что hello IP-адрес изменяется после назначения tooyour VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="646a3-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="646a3-171">только один раз Hello изменения адреса hello общедоступный IP-адрес когда hello шлюза будет удалена и создана заново.</span><span class="sxs-lookup"><span data-stu-id="646a3-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="646a3-172">При изменении размера, сбросе или других внутренних операциях обслуживания или обновления IP-адрес VPN-шлюза не изменяется.</span><span class="sxs-lookup"><span data-stu-id="646a3-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="646a3-173">Запрос общедоступный IP-адрес, который будет назначен tooyour виртуальной сети шлюза VPN.</span><span class="sxs-lookup"><span data-stu-id="646a3-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="646a3-174"><a name="GatewayIPConfig"></a>5. Создайте адресации конфигурации IP-адрес шлюза hello</span><span class="sxs-lookup"><span data-stu-id="646a3-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="646a3-175">Конфигурация шлюза Hello определяет подсеть hello и hello открытый IP адрес toouse.</span><span class="sxs-lookup"><span data-stu-id="646a3-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="646a3-176">Используйте следующий пример toocreate hello конфигурацию шлюза.</span><span class="sxs-lookup"><span data-stu-id="646a3-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="646a3-177"><a name="CreateGateway"></a>6. Создание шлюза VPN hello</span><span class="sxs-lookup"><span data-stu-id="646a3-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="646a3-178">Создание шлюза VPN hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="646a3-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="646a3-179">Создание VPN-шлюза может занять too45 минут или более toocomplete.</span><span class="sxs-lookup"><span data-stu-id="646a3-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="646a3-180">Используйте hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="646a3-180">Use hello following values:</span></span>

* <span data-ttu-id="646a3-181">Hello *- тип шлюза* для сайта для сайта конфигурации — *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="646a3-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="646a3-182">Тип шлюза Hello распространяется всегда конкретных toohello реализации.</span><span class="sxs-lookup"><span data-stu-id="646a3-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="646a3-183">Например, для других конфигураций шлюза может потребоваться тип шлюза ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="646a3-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="646a3-184">Hello *- VpnType* может быть *routebased* (называется tooas шлюза с динамической некоторые документы), или *PolicyBased* (называется tooas статический шлюз некоторые документы ).</span><span class="sxs-lookup"><span data-stu-id="646a3-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="646a3-185">Дополнительные сведения о типах VPN-шлюзов см. в статье [Основные сведения о VPN-шлюзах Azure](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="646a3-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="646a3-186">Выберите номер SKU шлюза, которые должны toouse hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="646a3-187">К определенным номерам SKU применяются ограничения настройки.</span><span class="sxs-lookup"><span data-stu-id="646a3-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="646a3-188">Дополнительные сведения см. в разделе о [номерах SKU шлюзов](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="646a3-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="646a3-189">Если возникает ошибка при создании шлюза VPN hello относительно hello - GatewaySku, проверьте, установить последнюю версию hello hello командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="646a3-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="646a3-190"><a name="ConfigureVPNDevice"></a>7. Настройка устройства VPN</span><span class="sxs-lookup"><span data-stu-id="646a3-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="646a3-191">Для межсайтовых подключений tooan локальной сети требуется VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="646a3-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="646a3-192">На этом этапе мы настроим VPN-устройство.</span><span class="sxs-lookup"><span data-stu-id="646a3-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="646a3-193">Во время настройки устройства VPN, необходимо hello следующее:</span><span class="sxs-lookup"><span data-stu-id="646a3-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="646a3-194">Общий ключ.</span><span class="sxs-lookup"><span data-stu-id="646a3-194">A shared key.</span></span> <span data-ttu-id="646a3-195">Это является hello того же самого общего ключа, указанного при создании через виртуальную Частную сеть для подключения.</span><span class="sxs-lookup"><span data-stu-id="646a3-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="646a3-196">В наших примерах мы используем простые общие ключи.</span><span class="sxs-lookup"><span data-stu-id="646a3-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="646a3-197">Рекомендуется создавать более сложные ключа toouse.</span><span class="sxs-lookup"><span data-stu-id="646a3-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="646a3-198">Здравствуйте, общедоступный IP-адрес шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="646a3-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="646a3-199">Hello общедоступный IP-адрес можно просмотреть с помощью hello портал Azure, PowerShell или интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="646a3-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="646a3-200">hello toofind общедоступный IP-адрес шлюза виртуальной сети с помощью PowerShell, hello используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="646a3-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="646a3-201"><a name="CreateConnection"></a>8. Создание VPN-подключения hello</span><span class="sxs-lookup"><span data-stu-id="646a3-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="646a3-202">Создайте подключение через виртуальную Частную сеть для hello между шлюз виртуальной сети и VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="646a3-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="646a3-203">Быть убедиться, что значениями hello tooreplace собственными.</span><span class="sxs-lookup"><span data-stu-id="646a3-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="646a3-204">Hello общий ключ должен соответствовать hello значение, которое используется для конфигурации устройства VPN.</span><span class="sxs-lookup"><span data-stu-id="646a3-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="646a3-205">Обратите внимание, что hello "-тип подключения" сеть-сеть является *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="646a3-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="646a3-206">Установка переменных hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="646a3-207">Создание подключения hello.</span><span class="sxs-lookup"><span data-stu-id="646a3-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="646a3-208">Через некоторое время hello будет установлено подключение.</span><span class="sxs-lookup"><span data-stu-id="646a3-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="646a3-209"><a name="toverify"></a>9. Проверьте hello VPN-подключения</span><span class="sxs-lookup"><span data-stu-id="646a3-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="646a3-210">Существует несколько способов tooverify VPN-подключение.</span><span class="sxs-lookup"><span data-stu-id="646a3-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="646a3-211"><a name="connectVM"></a>tooconnect tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="646a3-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="646a3-212"><a name="modify"></a>Изменение префиксов IP-адресов для шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="646a3-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="646a3-213">Если изменить префиксов hello IP-адресов, которые должны направляться в локальное расположение tooyour, можно изменить hello шлюза локальной сети.</span><span class="sxs-lookup"><span data-stu-id="646a3-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="646a3-214">Мы приводим два набора инструкций.</span><span class="sxs-lookup"><span data-stu-id="646a3-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="646a3-215">инструкции Hello выбранного зависят от того, уже создали подключения шлюза.</span><span class="sxs-lookup"><span data-stu-id="646a3-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="646a3-216"><a name="modifygwipaddress"></a>Изменить IP-адрес шлюза hello шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="646a3-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="646a3-217">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="646a3-217">Next steps</span></span>

*  <span data-ttu-id="646a3-218">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="646a3-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="646a3-219">Дополнительные сведения о виртуальных машинах см. [здесь](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="646a3-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="646a3-220">Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="646a3-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
