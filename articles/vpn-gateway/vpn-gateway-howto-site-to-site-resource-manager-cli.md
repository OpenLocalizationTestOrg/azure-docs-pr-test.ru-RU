---
title: "Соединение локальной сети с виртуальной сетью Azure с помощью VPN типа \"сеть — сеть\" и интерфейса командной строки | Документация Майкрософт"
description: "Сведения о создании подключения IPsec между локальной сетью и виртуальной сетью Azure через общедоступный Интернет. Они помогут вам создать подключение типа \"сеть — сеть\" с использованием VPN-шлюза и интерфейса командной строки."
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
ms.openlocfilehash: 019c5421dc470b18c9087417b93c241cc5730f77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="bb77b-104">Создание виртуальной сети с VPN типа "сеть — сеть" с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="bb77b-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="bb77b-105">В этой статье показано, как с помощью Azure CLI создавать подключение типа "сеть — сеть" с использованием VPN-шлюза между вашей локальной сетью к виртуальной.</span><span class="sxs-lookup"><span data-stu-id="bb77b-105">This article shows you how to use the Azure CLI to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="bb77b-106">Приведенные в этой статье инструкции относятся к модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bb77b-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="bb77b-107">Эту конфигурацию также можно создать с помощью разных средств или моделей развертывания, выбрав вариант из следующего списка:</span><span class="sxs-lookup"><span data-stu-id="bb77b-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb77b-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="bb77b-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="bb77b-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bb77b-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="bb77b-110">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="bb77b-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="bb77b-111">Портал Azure (классический)</span><span class="sxs-lookup"><span data-stu-id="bb77b-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Схема подключения типа "сеть — сеть" через VPN-шлюз](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="bb77b-113">Подключение VPN-шлюза типа "сеть — сеть" используется для подключения между локальной сетью и виртуальной сетью Azure через туннель VPN по протоколу IPsec/IKE (IKEv1 или IKEv2).</span><span class="sxs-lookup"><span data-stu-id="bb77b-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="bb77b-114">Для этого типа подключения требуется локальное VPN-устройство, которому назначен внешний общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="bb77b-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="bb77b-115">Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="bb77b-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bb77b-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="bb77b-116">Before you begin</span></span>

<span data-ttu-id="bb77b-117">Перед началом настройки убедитесь, что удовлетворены следующие требования:</span><span class="sxs-lookup"><span data-stu-id="bb77b-117">Verify that you have met the following criteria before beginning configuration:</span></span>

* <span data-ttu-id="bb77b-118">Убедитесь, что у вас есть совместимое VPN–устройство и пользователь, который может настроить его.</span><span class="sxs-lookup"><span data-stu-id="bb77b-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="bb77b-119">Дополнительные сведения о совместимых устройствах VPN и их настройке см. в [этой статье](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="bb77b-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="bb77b-120">Убедитесь, что у вас есть общедоступный IPv4–адрес для вашего VPN–устройства.</span><span class="sxs-lookup"><span data-stu-id="bb77b-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="bb77b-121">Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="bb77b-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="bb77b-122">Если вы не знаете диапазоны IP-адресов в своей конфигурации локальной сети, найдите того, кто сможет предоставить вам нужную информацию.</span><span class="sxs-lookup"><span data-stu-id="bb77b-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="bb77b-123">При создании этой конфигурации необходимо указать префиксы диапазона IP-адресов, которые Azure будет направлять к локальному расположению.</span><span class="sxs-lookup"><span data-stu-id="bb77b-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="bb77b-124">Ни одна из подсетей локальной сети не может перекрывать виртуальные подсети, к которым вы хотите подключиться.</span><span class="sxs-lookup"><span data-stu-id="bb77b-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="bb77b-125">Убедитесь, что вы установили последнюю версию команд интерфейса командной строки (2.0 или новее).</span><span class="sxs-lookup"><span data-stu-id="bb77b-125">Verify that you have installed latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="bb77b-126">Сведения об установке команд интерфейса командной строки см. в статьях [Install Azure CLI 2.0](/cli/azure/install-azure-cli) (Установка Azure CLI 2.0) и [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) (Приступая к работе с Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="bb77b-126">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="bb77b-127"><a name="example"></a>Примеры значений</span><span class="sxs-lookup"><span data-stu-id="bb77b-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="bb77b-128">Следующие значения можно использовать для создания тестовой среды или для лучшего понимания примеров в этой статье.</span><span class="sxs-lookup"><span data-stu-id="bb77b-128">You can use the following values to create a test environment, or refer to these values to better understand the examples in this article:</span></span>

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

## <span data-ttu-id="bb77b-129"><a name="Login"></a>1. Подключение к подписке</span><span class="sxs-lookup"><span data-stu-id="bb77b-129"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="bb77b-130"><a name="rg"></a>2. Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="bb77b-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="bb77b-131">В следующем примере создается группа ресурсов с именем TestRG1 в расположении eastus.</span><span class="sxs-lookup"><span data-stu-id="bb77b-131">The following example creates a resource group named 'TestRG1' in the 'eastus' location.</span></span> <span data-ttu-id="bb77b-132">Если у вас уже есть группа ресурсов в регионе, где вы хотите создать виртуальную сеть, вы можете воспользоваться ею.</span><span class="sxs-lookup"><span data-stu-id="bb77b-132">If you already have a resource group in the region that you want to create your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="bb77b-133"><a name="VNet"></a>3. Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="bb77b-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="bb77b-134">Если у вас еще нет виртуальной сети, создайте ее, используя команду [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="bb77b-134">If you don't already have a virtual network, create one using the [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="bb77b-135">При создании виртуальной сети убедитесь, что указанные адресные пространства не перекрываются ни с одним из адресных пространств, которые используются в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="bb77b-135">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="bb77b-136">В следующем примере создаются виртуальная сеть TestVNet1 и подсеть Subnet1.</span><span class="sxs-lookup"><span data-stu-id="bb77b-136">The following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="bb77b-137">4. <a name="gwsub"></a>Создание подсети шлюза</span><span class="sxs-lookup"><span data-stu-id="bb77b-137">4. <a name="gwsub"></a>Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="bb77b-138">Для этой конфигурации необходима также подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="bb77b-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="bb77b-139">Шлюз виртуальной сети использует подсеть шлюза, которая содержит IP-адреса, используемые службами VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="bb77b-139">The virtual network gateway uses a gateway subnet that contains the IP addresses that are used by the VPN gateway services.</span></span> <span data-ttu-id="bb77b-140">При создании подсеть шлюза нужно назвать GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="bb77b-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="bb77b-141">Если будет присвоено другое имя, вы создадите подсеть, но Azure не будет рассматривать ее как подсеть шлюза.</span><span class="sxs-lookup"><span data-stu-id="bb77b-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="bb77b-142">Размер указанной подсети шлюза зависит от конфигурации VPN-шлюза, которую вы хотите создать.</span><span class="sxs-lookup"><span data-stu-id="bb77b-142">The size of the gateway subnet that you specify depends on the VPN gateway configuration that you want to create.</span></span> <span data-ttu-id="bb77b-143">Хотя можно создать подсеть шлюза размером /29, рекомендуется создать подсеть большего размера, включающую несколько адресов, выбрав значение /27 или /28.</span><span class="sxs-lookup"><span data-stu-id="bb77b-143">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="bb77b-144">Использование более крупной подсети для шлюза позволяет создавать достаточное число IP-адресов с учетом возможных конфигураций в будущем.</span><span class="sxs-lookup"><span data-stu-id="bb77b-144">Using a larger gateway subnet allows for enough IP addresses to accommodate possible future configurations.</span></span>

<span data-ttu-id="bb77b-145">Используйте команду [azure network vnet subnet create](/cli/azure/network/vnet/subnet#create), чтобы создать шлюз подсети.</span><span class="sxs-lookup"><span data-stu-id="bb77b-145">Use the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command to create the gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="bb77b-146"><a name="localnet"></a>5. Создание шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="bb77b-146"><a name="localnet"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="bb77b-147">Обычно термин "шлюз локальной сети" означает локальное расположение.</span><span class="sxs-lookup"><span data-stu-id="bb77b-147">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="bb77b-148">Присвойте сайту имя, по которому Azure может обращаться к этому сайту, а затем укажите IP-адрес локального VPN-устройства, к которому вы подключитесь.</span><span class="sxs-lookup"><span data-stu-id="bb77b-148">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="bb77b-149">Вы можете также указать префиксы IP-адресов, которые будут направляться через VPN-шлюз к VPN-устройству.</span><span class="sxs-lookup"><span data-stu-id="bb77b-149">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="bb77b-150">Указываемые префиксы адресов расположены в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="bb77b-150">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="bb77b-151">При изменении локальной сети вы сможете без проблем обновить эти префиксы.</span><span class="sxs-lookup"><span data-stu-id="bb77b-151">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="bb77b-152">Используйте следующие значения:</span><span class="sxs-lookup"><span data-stu-id="bb77b-152">Use the following values:</span></span>

* <span data-ttu-id="bb77b-153">Параметр *--gateway-ip-address* — это IP-адрес локального VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="bb77b-153">The *--gateway-ip-address* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="bb77b-154">Ваше VPN-устройство не может располагаться вне преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="bb77b-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="bb77b-155">*--local-address-prefixes* — это локальные адресные пространства.</span><span class="sxs-lookup"><span data-stu-id="bb77b-155">The *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="bb77b-156">Используйте команду [az network local-gateway create](/cli/azure/network/local-gateway#create),чтобы добавить шлюз локальной сети с несколькими префиксами адресов:</span><span class="sxs-lookup"><span data-stu-id="bb77b-156">Use the [az network local-gateway create](/cli/azure/network/local-gateway#create) command to add a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="bb77b-157"><a name="PublicIP"></a>6. Запрос общедоступного IP-адреса</span><span class="sxs-lookup"><span data-stu-id="bb77b-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="bb77b-158">VPN-шлюз должен иметь общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="bb77b-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="bb77b-159">Сначала запросите ресурс IP-адреса, а затем укажите его при создании шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bb77b-159">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="bb77b-160">IP-адрес динамически назначается ресурсу при создании VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="bb77b-160">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="bb77b-161">В настоящее время VPN-шлюз поддерживает только *динамическое* выделение общедоступных IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="bb77b-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="bb77b-162">Вы не можете запросить назначение статического общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="bb77b-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="bb77b-163">Однако это не означает, что IP-адрес изменяется после назначения VPN-шлюзу.</span><span class="sxs-lookup"><span data-stu-id="bb77b-163">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="bb77b-164">Общедоступный IP-адрес изменяется только после удаления и повторного создания шлюза.</span><span class="sxs-lookup"><span data-stu-id="bb77b-164">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="bb77b-165">При изменении размера, сбросе или других внутренних операциях обслуживания или обновления IP-адрес VPN-шлюза не изменяется.</span><span class="sxs-lookup"><span data-stu-id="bb77b-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="bb77b-166">Используйте команду [az network public-ip create](/cli/azure/network/public-ip#create), чтобы запросить динамический общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="bb77b-166">Use the [az network public-ip create](/cli/azure/network/public-ip#create) command to request a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="bb77b-167"><a name="CreateGateway"></a>7. Создание VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="bb77b-167"><a name="CreateGateway"></a>7. Create the VPN gateway</span></span>

<span data-ttu-id="bb77b-168">Создайте VPN-шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bb77b-168">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="bb77b-169">Создание VPN-шлюза может занять от 45 минут и более.</span><span class="sxs-lookup"><span data-stu-id="bb77b-169">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="bb77b-170">Используйте следующие значения:</span><span class="sxs-lookup"><span data-stu-id="bb77b-170">Use the following values:</span></span>

* <span data-ttu-id="bb77b-171">Для конфигурации "сеть — сеть" задайте для параметра *--gateway-type* значение *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="bb77b-171">The *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="bb77b-172">Тип шлюза всегда зависит от реализуемой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bb77b-172">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="bb77b-173">Дополнительные сведения см. в разделе [Типы шлюзов](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="bb77b-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="bb77b-174">У параметра *--vpn-type* может быть значение *RouteBased* (в некоторых документах такой шлюз называется шлюзом с динамической маршрутизацией) или *PolicyBased* (в некоторых документах — шлюз со статической маршрутизацией).</span><span class="sxs-lookup"><span data-stu-id="bb77b-174">The *--vpn-type* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="bb77b-175">Этот параметр зависит от требований устройства, к которому вы подключаетесь.</span><span class="sxs-lookup"><span data-stu-id="bb77b-175">The setting is specific to requirements of the device that you are connecting to.</span></span> <span data-ttu-id="bb77b-176">Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="bb77b-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="bb77b-177">Выберите SKU шлюза, который нужно использовать.</span><span class="sxs-lookup"><span data-stu-id="bb77b-177">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="bb77b-178">К определенным номерам SKU применяются ограничения настройки.</span><span class="sxs-lookup"><span data-stu-id="bb77b-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="bb77b-179">Дополнительные сведения см. в разделе о [номерах SKU шлюзов](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="bb77b-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="bb77b-180">Чтобы создать VPN-шлюз, используйте команду [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create).</span><span class="sxs-lookup"><span data-stu-id="bb77b-180">Create the VPN gateway using the [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="bb77b-181">При выполнении этой команды с использованием параметра --no-wait вы не увидите ответа или выходных данных.</span><span class="sxs-lookup"><span data-stu-id="bb77b-181">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="bb77b-182">Этот параметр позволяет создать шлюз в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="bb77b-182">This parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="bb77b-183">Процесс создания шлюза занимает около 45 минут.</span><span class="sxs-lookup"><span data-stu-id="bb77b-183">It takes around 45 minutes to create a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="bb77b-184"><a name="VPNDevice"></a>8. Настройка устройства VPN</span><span class="sxs-lookup"><span data-stu-id="bb77b-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="bb77b-185">Для подключения типа "сеть — сеть" к локальной сети требуется VPN-устройство.</span><span class="sxs-lookup"><span data-stu-id="bb77b-185">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="bb77b-186">На этом этапе мы настроим VPN-устройство.</span><span class="sxs-lookup"><span data-stu-id="bb77b-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="bb77b-187">Чтобы настроить локальное VPN-устройство, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="bb77b-187">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="bb77b-188">Общий ключ.</span><span class="sxs-lookup"><span data-stu-id="bb77b-188">A shared key.</span></span> <span data-ttu-id="bb77b-189">Это тот же общий ключ, который указывается при создании VPN-подключения "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="bb77b-189">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="bb77b-190">В наших примерах мы используем простые общие ключи.</span><span class="sxs-lookup"><span data-stu-id="bb77b-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="bb77b-191">Для практического использования рекомендуется создавать более сложные ключи.</span><span class="sxs-lookup"><span data-stu-id="bb77b-191">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="bb77b-192">Общедоступный IP-адрес шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="bb77b-192">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="bb77b-193">Общедоступный IP-адрес можно просмотреть с помощью портала Azure, PowerShell или CLI.</span><span class="sxs-lookup"><span data-stu-id="bb77b-193">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="bb77b-194">Чтобы найти общедоступный IP-адрес шлюза виртуальной сети, используйте команду [az network public-ip list](/cli/azure/network/public-ip#list).</span><span class="sxs-lookup"><span data-stu-id="bb77b-194">To find the public IP address of your virtual network gateway, use the [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="bb77b-195">Для удобства чтения выходные данные форматируются для отображения списка общедоступных IP-адресов в формате таблицы.</span><span class="sxs-lookup"><span data-stu-id="bb77b-195">For easy reading, the output is formatted to display the list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="bb77b-196"><a name="CreateConnection"></a>9. Создание VPN-подключения</span><span class="sxs-lookup"><span data-stu-id="bb77b-196"><a name="CreateConnection"></a>9. Create the VPN connection</span></span>

<span data-ttu-id="bb77b-197">Создайте VPN-подключение типа "сеть — сеть" между шлюзом виртуальной сети и локальным VPN-устройством.</span><span class="sxs-lookup"><span data-stu-id="bb77b-197">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="bb77b-198">Обратите особое внимание на значение общего ключа, которое должно соответствовать значению заданного общего ключа для VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="bb77b-198">Pay particular attention to the shared key value, which must match the configured shared key value for your VPN device.</span></span>

<span data-ttu-id="bb77b-199">Создайте подключение с помощью команды [az network vpn-connection create](/cli/azure/network/vpn-connection#create).</span><span class="sxs-lookup"><span data-stu-id="bb77b-199">Create the connection using the [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="bb77b-200">Через некоторое время будет установлено подключение.</span><span class="sxs-lookup"><span data-stu-id="bb77b-200">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="bb77b-201"><a name="toverify"></a>10. Проверка VPN-подключения</span><span class="sxs-lookup"><span data-stu-id="bb77b-201"><a name="toverify"></a>10. Verify the VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="bb77b-202">Если вы хотите использовать другой метод проверки подключения, см. статью [Проверка соединения VPN-шлюза](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="bb77b-202">If you want to use another method to verify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="bb77b-203"><a name="connectVM"></a>Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="bb77b-203"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="bb77b-204"><a name="tasks"></a>Стандартные задачи</span><span class="sxs-lookup"><span data-stu-id="bb77b-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="bb77b-205">Этот раздел содержит общие команды, которые могут быть полезны при работе с конфигурациями подключения типа "сайт — сайт".</span><span class="sxs-lookup"><span data-stu-id="bb77b-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="bb77b-206">Полный список сетевых команд интерфейса командной строки см. в разделе об [управлении ресурсами сети Azure](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="bb77b-206">For the full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="bb77b-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb77b-207">Next steps</span></span>

* <span data-ttu-id="bb77b-208">Установив подключение, можно добавить виртуальные машины в виртуальные сети.</span><span class="sxs-lookup"><span data-stu-id="bb77b-208">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="bb77b-209">Дополнительные сведения о виртуальных машинах см. [здесь](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="bb77b-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="bb77b-210">Сведения о BGP см. в статьях [Обзор использования BGP с VPN-шлюзами Azure](vpn-gateway-bgp-overview.md) и [Настройка BGP на VPN-шлюзах Azure с помощью Azure Resource Manager и PowerShell](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="bb77b-210">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="bb77b-211">Сведения о принудительном туннелировании см. в статье [Настройка принудительного туннелирования с помощью классической модели развертывания](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="bb77b-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="bb77b-212">Сведения о высокодоступных подключениях в режиме "активный — активный" см. в статье [Настройка высокодоступных подключений: распределенных и между виртуальными сетями](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="bb77b-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="bb77b-213">Список сетевых команд Azure CLI см. в статье об [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="bb77b-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>