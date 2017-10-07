---
title: "Подключение к локальной сети tooan виртуальной сети Azure: через виртуальную Частную сеть для: CLI | Документы Microsoft"
description: "Действия toocreate соединении по протоколу IPsec в локальной сети tooan виртуальной сети Azure через hello общедоступный Интернет. Они помогут вам создать подключение типа \"сеть — сеть\" с использованием VPN-шлюза и интерфейса командной строки."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="c141a-104">Создание виртуальной сети с VPN типа "сеть — сеть" с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="c141a-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="c141a-105">В этой статье показано, как toouse hello Azure CLI toocreate через виртуальную Частную сеть для подключения шлюза из вашей локальной сети toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c141a-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="c141a-106">в этой статье инструкциям Hello применяются toohello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c141a-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="c141a-107">Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.</span><span class="sxs-lookup"><span data-stu-id="c141a-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c141a-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="c141a-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c141a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c141a-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="c141a-110">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="c141a-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="c141a-111">Портал Azure (классический)</span><span class="sxs-lookup"><span data-stu-id="c141a-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Схема подключения типа "сеть — сеть" через VPN-шлюз](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="c141a-113">Используется tooconnect — подключение через виртуальную Частную сеть для шлюза в локальной сети tooan виртуальной сети Azure через туннель VPN IPsec/IKE (IKEv1 или IKEv2).</span><span class="sxs-lookup"><span data-stu-id="c141a-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="c141a-114">Этот тип подключения требуется VPN устройства, расположенного в локальной среде, имеет внешний tooit открытый IP-адрес, назначенный.</span><span class="sxs-lookup"><span data-stu-id="c141a-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="c141a-115">Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="c141a-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c141a-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="c141a-116">Before you begin</span></span>

<span data-ttu-id="c141a-117">Убедитесь, что выполнены следующие условия перед началом настройки hello:</span><span class="sxs-lookup"><span data-stu-id="c141a-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="c141a-118">Убедитесь, что у вас есть совместимых устройств VPN и тем, кто имеет доступ tooconfigure его.</span><span class="sxs-lookup"><span data-stu-id="c141a-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="c141a-119">Дополнительные сведения о совместимых устройствах VPN и их настройке см. в [этой статье](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="c141a-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="c141a-120">Убедитесь, что у вас есть общедоступный IPv4–адрес для вашего VPN–устройства.</span><span class="sxs-lookup"><span data-stu-id="c141a-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="c141a-121">Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="c141a-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c141a-122">Если вы не знакомы с hello диапазоны IP-адресов в вашей локальной сети, конфигурации, необходимо toocoordinate с тем, кто сможет предоставить эти сведения для вас.</span><span class="sxs-lookup"><span data-stu-id="c141a-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="c141a-123">При создании этой конфигурации необходимо указать что Azure будет направлять в локальное расположение tooyour диапазон префиксов hello IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c141a-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="c141a-124">Ни один из подсетей hello в локальной сети можно через Знакомство с функциями с hello подсети виртуальной сети, которые будут tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="c141a-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="c141a-125">Убедитесь, что установки последней версии hello команды CLI (2.0 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="c141a-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="c141a-126">Сведения об установке hello командах CLI см. в разделе [установить CLI Azure 2.0](/cli/azure/install-azure-cli) и [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c141a-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="c141a-127"><a name="example"></a>Примеры значений</span><span class="sxs-lookup"><span data-stu-id="c141a-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="c141a-128">Можно использовать следующие значения toocreate тестовой среде hello, или ссылаться toothese значения toobetter понять hello примеры в этой статье:</span><span class="sxs-lookup"><span data-stu-id="c141a-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="c141a-129"><a name="Login"></a>1. Подключение tooyour подписки</span><span class="sxs-lookup"><span data-stu-id="c141a-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="c141a-130"><a name="rg"></a>2. Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="c141a-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="c141a-131">Hello пример создает группу ресурсов с именем «TestRG1» в расположении «eastus» hello.</span><span class="sxs-lookup"><span data-stu-id="c141a-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="c141a-132">При наличии группы ресурсов в регионе hello требуется toocreate виртуальной сети, что один можно использовать вместо этого.</span><span class="sxs-lookup"><span data-stu-id="c141a-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="c141a-133"><a name="VNet"></a>3. Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="c141a-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="c141a-134">Если у вас еще нет виртуальной сети, создайте его с помощью hello [создания az сети vnet](/cli/azure/network/vnet#create) команды.</span><span class="sxs-lookup"><span data-stu-id="c141a-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="c141a-135">При создании виртуальной сети, убедитесь, что hello адресные пространства, указываемые не перекрываются hello адресных пространств, в которых в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c141a-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="c141a-136">Hello следующий пример создает виртуальную сеть с именем «TestVNet1» и подсеть, «Подсети1».</span><span class="sxs-lookup"><span data-stu-id="c141a-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="c141a-137">4. <a name="gwsub"></a>Создать подсеть шлюза hello</span><span class="sxs-lookup"><span data-stu-id="c141a-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="c141a-138">Для этой конфигурации необходима также подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="c141a-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="c141a-139">шлюз виртуальной сети Hello использует подсеть шлюза, содержащий hello IP-адреса, используемые службами шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="c141a-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="c141a-140">При создании подсеть шлюза нужно назвать GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="c141a-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="c141a-141">Если будет присвоено другое имя, вы создадите подсеть, но Azure не будет рассматривать ее как подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="c141a-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="c141a-142">размер Hello подсеть шлюза hello зависит от настройки шлюза VPN hello, которые должны toocreate.</span><span class="sxs-lookup"><span data-stu-id="c141a-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="c141a-143">Хотя возможных toocreate как /29 подсеть шлюза, рекомендуется создать подсеть большего размера, включающий несколько адресов, выбрав /27 или /28.</span><span class="sxs-lookup"><span data-stu-id="c141a-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="c141a-144">Использование большего подсеть шлюза позволяет недостаточно IP-адреса tooaccommodate возможных будущих конфигураций.</span><span class="sxs-lookup"><span data-stu-id="c141a-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="c141a-145">Используйте hello [создать подсеть виртуальной сети сети az](/cli/azure/network/vnet/subnet#create) подсеть шлюза hello toocreate команды.</span><span class="sxs-lookup"><span data-stu-id="c141a-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="c141a-146"><a name="localnet"></a>5. Создание шлюза локальной сети hello</span><span class="sxs-lookup"><span data-stu-id="c141a-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="c141a-147">шлюз локальной сети Hello обычно относится tooyour в локальном расположении.</span><span class="sxs-lookup"><span data-stu-id="c141a-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="c141a-148">Присвоить имя, на который Azure можно ссылаться tooit, а затем укажите hello IP-адрес сайта hello объекта toowhich устройство VPN локальной hello будет создавать подключение.</span><span class="sxs-lookup"><span data-stu-id="c141a-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="c141a-149">Можно также указать префиксов hello IP-адресов, которые будет проходить через устройство VPN toohello шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="c141a-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="c141a-150">префиксы адресов Hello, указываемые являются префиксы hello в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="c141a-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="c141a-151">Если изменяется в локальной сети, можно легко обновлять префиксы hello.</span><span class="sxs-lookup"><span data-stu-id="c141a-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="c141a-152">Используйте hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="c141a-152">Use hello following values:</span></span>

* <span data-ttu-id="c141a-153">Hello *— IP-адрес шлюза* hello IP-адрес локального VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="c141a-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="c141a-154">Ваше VPN-устройство не может располагаться вне преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="c141a-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="c141a-155">Hello *--префиксы для адресов локального* являются локальными адресных пространств.</span><span class="sxs-lookup"><span data-stu-id="c141a-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="c141a-156">Используйте hello [Создание локальной сети az-шлюз](/cli/azure/network/local-gateway#create) tooadd команда шлюза локальной сети с помощью нескольких префиксов адреса:</span><span class="sxs-lookup"><span data-stu-id="c141a-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="c141a-157"><a name="PublicIP"></a>6. Запрос общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="c141a-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="c141a-158">VPN-шлюз должен иметь общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c141a-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="c141a-159">Запросить ресурс IP-адреса hello и затем ссылаться tooit при создании шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c141a-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="c141a-160">Hello IP-адрес назначается динамически toohello ресурсов при создании шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="c141a-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="c141a-161">В настоящее время VPN-шлюз поддерживает только *динамическое* выделение общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="c141a-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="c141a-162">Вы не можете запросить назначение статического общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="c141a-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="c141a-163">Однако это не означает, что hello IP-адрес изменяется после назначения tooyour VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="c141a-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="c141a-164">только один раз Hello изменения адреса hello общедоступный IP-адрес когда hello шлюза будет удалена и создана заново.</span><span class="sxs-lookup"><span data-stu-id="c141a-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="c141a-165">При изменении размера, сбросе или других внутренних операциях обслуживания или обновления IP-адрес VPN-шлюза не изменяется.</span><span class="sxs-lookup"><span data-stu-id="c141a-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="c141a-166">Используйте hello [создания сети az public-ip](/cli/azure/network/public-ip#create) toorequest команда динамического общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="c141a-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="c141a-167"><a name="CreateGateway"></a>7. Создание шлюза VPN hello</span><span class="sxs-lookup"><span data-stu-id="c141a-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="c141a-168">Создание шлюза VPN hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c141a-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="c141a-169">Создание VPN-шлюза может занять too45 минут или более toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c141a-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="c141a-170">Используйте hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="c141a-170">Use hello following values:</span></span>

* <span data-ttu-id="c141a-171">Hello *--тип шлюза* для сайта для сайта конфигурации — *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="c141a-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="c141a-172">Тип шлюза Hello распространяется всегда конкретных toohello реализации.</span><span class="sxs-lookup"><span data-stu-id="c141a-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="c141a-173">Дополнительные сведения см. в разделе [Типы шлюзов](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="c141a-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="c141a-174">Hello *тип vpn —* может быть *routebased* (называется tooas шлюза с динамической некоторые документы), или *PolicyBased* (называется tooas статический шлюз в некоторых документация).</span><span class="sxs-lookup"><span data-stu-id="c141a-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="c141a-175">приветствия равен конкретных toorequirements hello устройство, которое вы подключаетесь.</span><span class="sxs-lookup"><span data-stu-id="c141a-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="c141a-176">Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="c141a-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="c141a-177">Выберите номер SKU шлюза, которые должны toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c141a-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="c141a-178">К определенным номерам SKU применяются ограничения настройки.</span><span class="sxs-lookup"><span data-stu-id="c141a-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="c141a-179">Дополнительные сведения см. в разделе о [номерах SKU шлюзов](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="c141a-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="c141a-180">Создание шлюза VPN hello, с помощью hello [Создание виртуальной сети — шлюз сети az](/cli/azure/network/vnet-gateway#create) команды.</span><span class="sxs-lookup"><span data-stu-id="c141a-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="c141a-181">При выполнении этой команды, с помощью hello параметр «--no - wait», вы не видите любой отзыв или выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c141a-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="c141a-182">Этот параметр позволяет toocreate шлюза hello в фоновом режиме hello.</span><span class="sxs-lookup"><span data-stu-id="c141a-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="c141a-183">Занимает около 45 минут toocreate шлюз.</span><span class="sxs-lookup"><span data-stu-id="c141a-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="c141a-184"><a name="VPNDevice"></a>8. Настройка устройства VPN</span><span class="sxs-lookup"><span data-stu-id="c141a-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="c141a-185">Для межсайтовых подключений tooan локальной сети требуется VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="c141a-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="c141a-186">На этом этапе мы настроим VPN-устройство.</span><span class="sxs-lookup"><span data-stu-id="c141a-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="c141a-187">Во время настройки устройства VPN, необходимо hello следующее:</span><span class="sxs-lookup"><span data-stu-id="c141a-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="c141a-188">Общий ключ.</span><span class="sxs-lookup"><span data-stu-id="c141a-188">A shared key.</span></span> <span data-ttu-id="c141a-189">Это является hello того же самого общего ключа, указанного при создании через виртуальную Частную сеть для подключения.</span><span class="sxs-lookup"><span data-stu-id="c141a-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="c141a-190">В наших примерах мы используем простые общие ключи.</span><span class="sxs-lookup"><span data-stu-id="c141a-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="c141a-191">Рекомендуется создавать более сложные ключа toouse.</span><span class="sxs-lookup"><span data-stu-id="c141a-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="c141a-192">Здравствуйте, общедоступный IP-адрес шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="c141a-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="c141a-193">Hello общедоступный IP-адрес можно просмотреть с помощью hello портал Azure, PowerShell или интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="c141a-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="c141a-194">toofind hello общедоступный IP-адрес шлюза виртуальной сети, используйте hello [список открытый ip-сетей az](/cli/azure/network/public-ip#list) команды.</span><span class="sxs-lookup"><span data-stu-id="c141a-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="c141a-195">Для облегчения процесса чтения hello выводится форматированный toodisplay hello список общедоступных IP-адресов в формате таблицы.</span><span class="sxs-lookup"><span data-stu-id="c141a-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="c141a-196"><a name="CreateConnection"></a>9. Создание VPN-подключения hello</span><span class="sxs-lookup"><span data-stu-id="c141a-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="c141a-197">Создайте hello сеть-сеть VPN-подключение между шлюзом виртуальной сети и локальным VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="c141a-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="c141a-198">Оплата особое внимание toohello общего ключа значение, которое должно соответствовать hello настроен общий значение ключа для VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="c141a-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="c141a-199">Hello-подключение с помощью hello [создать az сети vpn подключения](/cli/azure/network/vpn-connection#create) команды.</span><span class="sxs-lookup"><span data-stu-id="c141a-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="c141a-200">Через некоторое время hello будет установлено подключение.</span><span class="sxs-lookup"><span data-stu-id="c141a-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="c141a-201"><a name="toverify"></a>10. Проверьте hello VPN-подключения</span><span class="sxs-lookup"><span data-stu-id="c141a-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="c141a-202">Если требуется другой метод tooverify toouse подключения, в разделе [Проверка подключения к VPN-шлюз](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c141a-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="c141a-203"><a name="connectVM"></a>tooconnect tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="c141a-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="c141a-204"><a name="tasks"></a>Стандартные задачи</span><span class="sxs-lookup"><span data-stu-id="c141a-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="c141a-205">Этот раздел содержит общие команды, которые могут быть полезны при работе с конфигурациями подключения типа "сайт — сайт".</span><span class="sxs-lookup"><span data-stu-id="c141a-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="c141a-206">Hello полный список сетевые команды CLI см. в разделе [Azure CLI - сети](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="c141a-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c141a-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c141a-207">Next steps</span></span>

* <span data-ttu-id="c141a-208">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="c141a-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="c141a-209">Дополнительные сведения о виртуальных машинах см. [здесь](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="c141a-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="c141a-210">Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c141a-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="c141a-211">Сведения о принудительном туннелировании см. в статье [Настройка принудительного туннелирования с помощью классической модели развертывания](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="c141a-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="c141a-212">Сведения о высокодоступных подключениях в режиме "активный — активный" см. в статье [Настройка высокодоступных подключений: распределенных и между виртуальными сетями](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="c141a-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="c141a-213">Список сетевых команд Azure CLI см. в статье об [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="c141a-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>