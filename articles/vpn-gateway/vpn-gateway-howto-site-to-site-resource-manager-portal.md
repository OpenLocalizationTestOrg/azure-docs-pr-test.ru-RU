---
title: "Подключение к локальной сети tooan виртуальной сети Azure: через виртуальную Частную сеть для: портал | Документы Microsoft"
description: "Действия toocreate соединении по протоколу IPsec в локальной сети tooan виртуальной сети Azure через hello общедоступный Интернет. Эти шаги помогают создавать подключения между организациями сеть-сеть VPN-шлюза, с помощью портала hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a><span data-ttu-id="25446-104">Создайте соединение сайт-сайт в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="25446-104">Create a Site-to-Site connection in hello Azure portal</span></span>

<span data-ttu-id="25446-105">В этой статье показано, как toouse hello Azure портала toocreate через виртуальную Частную сеть для подключения шлюза из вашей локальной сети toohello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="25446-105">This article shows you how toouse hello Azure portal toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="25446-106">в этой статье инструкциям Hello применяются toohello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="25446-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="25446-107">Можно также создать этой конфигурации с помощью средства развертывания или модель развертывания, выбрав другой вариант из hello после списка.</span><span class="sxs-lookup"><span data-stu-id="25446-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="25446-108">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="25446-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="25446-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25446-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="25446-110">ИНТЕРФЕЙС КОМАНДНОЙ СТРОКИ</span><span class="sxs-lookup"><span data-stu-id="25446-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="25446-111">Портал Azure (классический)</span><span class="sxs-lookup"><span data-stu-id="25446-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

<span data-ttu-id="25446-112">Используется tooconnect — подключение через виртуальную Частную сеть для шлюза в локальной сети tooan виртуальной сети Azure через туннель VPN IPsec/IKE (IKEv1 или IKEv2).</span><span class="sxs-lookup"><span data-stu-id="25446-112">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="25446-113">Этот тип подключения требуется VPN устройства, расположенного в локальной среде, имеет внешний tooit открытый IP-адрес, назначенный.</span><span class="sxs-lookup"><span data-stu-id="25446-113">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="25446-114">Дополнительные сведения о VPN-шлюзах см. в [этой статье](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="25446-114">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Схема подключения типа "сеть — сеть" через VPN-шлюз](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a><span data-ttu-id="25446-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="25446-116">Before you begin</span></span>

<span data-ttu-id="25446-117">Убедитесь, что выполнены следующие условия перед началом настройки hello:</span><span class="sxs-lookup"><span data-stu-id="25446-117">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="25446-118">Убедитесь, что у вас есть совместимых устройств VPN и тем, кто имеет доступ tooconfigure его.</span><span class="sxs-lookup"><span data-stu-id="25446-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="25446-119">Дополнительные сведения о совместимых устройствах VPN и их настройке см. в [этой статье](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="25446-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="25446-120">Убедитесь, что у вас есть общедоступный IPv4–адрес для вашего VPN–устройства.</span><span class="sxs-lookup"><span data-stu-id="25446-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="25446-121">Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="25446-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="25446-122">Если вы не знакомы с hello диапазоны IP-адресов в вашей локальной сети, конфигурации, необходимо toocoordinate с тем, кто сможет предоставить эти сведения для вас.</span><span class="sxs-lookup"><span data-stu-id="25446-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="25446-123">При создании этой конфигурации необходимо указать что Azure будет направлять в локальное расположение tooyour диапазон префиксов hello IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="25446-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="25446-124">Ни один из подсетей hello в локальной сети можно через Знакомство с функциями с hello подсети виртуальной сети, которые будут tooconnect для.</span><span class="sxs-lookup"><span data-stu-id="25446-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span> 

### <span data-ttu-id="25446-125"><a name="values"></a>Примеры значений</span><span class="sxs-lookup"><span data-stu-id="25446-125"><a name="values"></a>Example values</span></span>

<span data-ttu-id="25446-126">Hello примерах в этой статье используется hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="25446-126">hello examples in this article use hello following values.</span></span> <span data-ttu-id="25446-127">Можно использовать эти значения toocreate тестовой среде, или ссылаться toothem toobetter понять hello примеры в этой статье.</span><span class="sxs-lookup"><span data-stu-id="25446-127">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

* <span data-ttu-id="25446-128">**Имя виртуальной сети:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="25446-128">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="25446-129">**Адресное пространство:**</span><span class="sxs-lookup"><span data-stu-id="25446-129">**Address Space:**</span></span> 
  * <span data-ttu-id="25446-130">10.11.0.0/16;</span><span class="sxs-lookup"><span data-stu-id="25446-130">10.11.0.0/16</span></span>
  * <span data-ttu-id="25446-131">10.12.0.0/16 (необязательно для этого упражнения).</span><span class="sxs-lookup"><span data-stu-id="25446-131">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="25446-132">**Подсети:**</span><span class="sxs-lookup"><span data-stu-id="25446-132">**Subnets:**</span></span>
  * <span data-ttu-id="25446-133">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="25446-133">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="25446-134">BackEnd: 10.12.0.0/24 (необязательно для этого упражнения).</span><span class="sxs-lookup"><span data-stu-id="25446-134">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
* <span data-ttu-id="25446-135">**Подсеть шлюза:** 10.11.255.0/27.</span><span class="sxs-lookup"><span data-stu-id="25446-135">**GatewaySubnet:** 10.11.255.0/27</span></span>
* <span data-ttu-id="25446-136">**Группа ресурсов:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="25446-136">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="25446-137">**Расположение:** восточная часть США.</span><span class="sxs-lookup"><span data-stu-id="25446-137">**Location:** East US</span></span>
* <span data-ttu-id="25446-138">**DNS-сервер:** (необязательно)</span><span class="sxs-lookup"><span data-stu-id="25446-138">**DNS Server:** Optional.</span></span> <span data-ttu-id="25446-139">Hello IP-адрес DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="25446-139">hello IP address of your DNS server.</span></span>
* <span data-ttu-id="25446-140">**Имя шлюза виртуальной сети:** VNet1GW.</span><span class="sxs-lookup"><span data-stu-id="25446-140">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="25446-141">**Общедоступный IP-адрес:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="25446-141">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="25446-142">**Тип VPN:** на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="25446-142">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="25446-143">**Тип подключения:** "сеть — сеть" (IPsec)</span><span class="sxs-lookup"><span data-stu-id="25446-143">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="25446-144">**Тип шлюза:** VPN.</span><span class="sxs-lookup"><span data-stu-id="25446-144">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="25446-145">**Имя шлюза локальной сети:** Site2</span><span class="sxs-lookup"><span data-stu-id="25446-145">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="25446-146">**Имя подключения:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="25446-146">**Connection Name:** VNet1toSite2</span></span>

## <span data-ttu-id="25446-147"><a name="CreatVNet"></a>1. Создать виртуальную сеть</span><span class="sxs-lookup"><span data-stu-id="25446-147"><a name="CreatVNet"></a>1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="25446-148"><a name="dns"></a>2. Выбор DNS-сервера</span><span class="sxs-lookup"><span data-stu-id="25446-148"><a name="dns"></a>2. Specify a DNS server</span></span>

<span data-ttu-id="25446-149">DNS не требуется toocreate сайта для сайта соединением.</span><span class="sxs-lookup"><span data-stu-id="25446-149">DNS is not required toocreate a Site-to-Site connection.</span></span> <span data-ttu-id="25446-150">Однако если требуется toohave разрешение имен для ресурсов, которые являются tooyour развернутой виртуальной сети, следует указать DNS-сервер.</span><span class="sxs-lookup"><span data-stu-id="25446-150">However, if you want toohave name resolution for resources that are deployed tooyour virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="25446-151">Этот параметр позволяет указать hello DNS-сервера требуется toouse для разрешения имен для этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="25446-151">This setting lets you specify hello DNS server that you want toouse for name resolution for this virtual network.</span></span> <span data-ttu-id="25446-152">Он не приводит к созданию DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="25446-152">It does not create a DNS server.</span></span> <span data-ttu-id="25446-153">См. дополнительные сведения о [разрешении имен для виртуальных машин и экземпляров ролей](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="25446-153">For more information about name resolution, see [Name Resolution for VMs and role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <span data-ttu-id="25446-154"><a name="gatewaysubnet"></a>3. Создать подсеть шлюза hello</span><span class="sxs-lookup"><span data-stu-id="25446-154"><a name="gatewaysubnet"></a>3. Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <span data-ttu-id="25446-155"><a name="VNetGateway"></a>4. Создание шлюза VPN hello</span><span class="sxs-lookup"><span data-stu-id="25446-155"><a name="VNetGateway"></a>4. Create hello VPN gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <span data-ttu-id="25446-156"><a name="LocalNetworkGateway"></a>5. Создание шлюза локальной сети hello</span><span class="sxs-lookup"><span data-stu-id="25446-156"><a name="LocalNetworkGateway"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="25446-157">шлюз локальной сети Hello обычно относится tooyour в локальном расположении.</span><span class="sxs-lookup"><span data-stu-id="25446-157">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="25446-158">Присвоить имя, на который Azure можно ссылаться tooit, а затем укажите hello IP-адрес сайта hello объекта toowhich устройство VPN локальной hello будет создавать подключение.</span><span class="sxs-lookup"><span data-stu-id="25446-158">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="25446-159">Можно также указать префиксов hello IP-адресов, которые будет проходить через устройство VPN toohello шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="25446-159">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="25446-160">префиксы адресов Hello, указываемые являются префиксы hello в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="25446-160">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="25446-161">Если изменения в локальной сети, или вы должны toochange hello общедоступный IP-адрес для VPN-устройства hello, можно легко обновить значения hello позже.</span><span class="sxs-lookup"><span data-stu-id="25446-161">If your on-premises network changes or you need toochange hello public IP address for hello VPN device, you can easily update hello values later.</span></span>

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <span data-ttu-id="25446-162"><a name="VPNDevice"></a>6. Настройка устройства VPN</span><span class="sxs-lookup"><span data-stu-id="25446-162"><a name="VPNDevice"></a>6. Configure your VPN device</span></span>

<span data-ttu-id="25446-163">Для межсайтовых подключений tooan локальной сети требуется VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="25446-163">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="25446-164">На этом этапе мы настроим VPN-устройство.</span><span class="sxs-lookup"><span data-stu-id="25446-164">In this step, you configure your VPN device.</span></span> <span data-ttu-id="25446-165">Во время настройки устройства VPN, необходимо hello следующее:</span><span class="sxs-lookup"><span data-stu-id="25446-165">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="25446-166">Общий ключ.</span><span class="sxs-lookup"><span data-stu-id="25446-166">A shared key.</span></span> <span data-ttu-id="25446-167">Это является hello того же самого общего ключа, указанного при создании через виртуальную Частную сеть для подключения.</span><span class="sxs-lookup"><span data-stu-id="25446-167">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="25446-168">В наших примерах мы используем простые общие ключи.</span><span class="sxs-lookup"><span data-stu-id="25446-168">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="25446-169">Рекомендуется создавать более сложные ключа toouse.</span><span class="sxs-lookup"><span data-stu-id="25446-169">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="25446-170">Здравствуйте, общедоступный IP-адрес шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="25446-170">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="25446-171">Hello общедоступный IP-адрес можно просмотреть с помощью hello портал Azure, PowerShell или интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="25446-171">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="25446-172">hello toofind общедоступный IP-адрес шлюза VPN с помощью портала Azure hello перейдите слишком**шлюзы виртуальной сети**, затем щелкните имя hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="25446-172">toofind hello Public IP address of your VPN gateway using hello Azure portal, navigate too**Virtual network gateways**, then click hello name of your gateway.</span></span>

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <span data-ttu-id="25446-173"><a name="CreateConnection"></a>7. Создание VPN-подключения hello</span><span class="sxs-lookup"><span data-stu-id="25446-173"><a name="CreateConnection"></a>7. Create hello VPN connection</span></span>

<span data-ttu-id="25446-174">Создайте hello сеть-сеть VPN-подключение между шлюзом виртуальной сети и локальным VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="25446-174">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span>

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <span data-ttu-id="25446-175"><a name="VerifyConnection"></a>8. Проверьте hello VPN-подключения</span><span class="sxs-lookup"><span data-stu-id="25446-175"><a name="VerifyConnection"></a>8. Verify hello VPN connection</span></span>

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="25446-176"><a name="connectVM"></a>tooconnect tooa виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="25446-176"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="25446-177"><a name="reset"></a>Как tooreset VPN-шлюза</span><span class="sxs-lookup"><span data-stu-id="25446-177"><a name="reset"></a>How tooreset a VPN gateway</span></span>

<span data-ttu-id="25446-178">Сброс настроек VPN-шлюза Azure полезен при потере распределенного VPN-подключения в одном или нескольких VPN-туннелях типа "сеть-сеть".</span><span class="sxs-lookup"><span data-stu-id="25446-178">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="25446-179">В этой ситуации локального VPN-устройств являются все работает правильно, но не удается tooestablish туннелей IPsec со шлюзами Azure VPN hello.</span><span class="sxs-lookup"><span data-stu-id="25446-179">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="25446-180">Пошаговые инструкции см. в статье [Сброс VPN-шлюза](vpn-gateway-resetgw-classic.md).</span><span class="sxs-lookup"><span data-stu-id="25446-180">For steps, see [Reset a VPN gateway](vpn-gateway-resetgw-classic.md).</span></span>

## <span data-ttu-id="25446-181"><a name="resize"></a>Как toochange шлюза SKU (изменение размера шлюза)</span><span class="sxs-lookup"><span data-stu-id="25446-181"><a name="resize"></a>How toochange a gateway SKU (resize a gateway)</span></span>

<span data-ttu-id="25446-182">Hello шаги toochange номер SKU шлюза, см. в разделе [SKU шлюза](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="25446-182">For hello steps toochange a gateway SKU, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <a name="next-steps"></a><span data-ttu-id="25446-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="25446-183">Next steps</span></span>

* <span data-ttu-id="25446-184">Сведения о BGP см. в разделе hello [Обзор BGP](vpn-gateway-bgp-overview.md) и [как tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="25446-184">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="25446-185">Сведения о принудительном туннелировании см. в статье [Настройка принудительного туннелирования с помощью классической модели развертывания](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="25446-185">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="25446-186">Сведения о высокодоступных подключениях в режиме "активный — активный" см. в статье [Настройка высокодоступных подключений: распределенных и между виртуальными сетями](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="25446-186">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
