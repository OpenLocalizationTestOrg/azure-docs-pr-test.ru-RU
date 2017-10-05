---
title: "Подключение виртуальной сети к нескольким сайтам с помощью VPN-шлюза и PowerShell: классическая модель | Документы Майкрософт"
description: "Данная статья поможет настроить подключение нескольких локальных сайтов к виртуальной сети с использованием VPN-шлюза для классической модели развертывания."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: bb3129f70f5eeed99d5889226aa6727f675b6217
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="9a29e-103">Добавление подключения типа "сеть-сеть" к виртуальной сети с помощью существующего подключения VPN-шлюза (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="9a29e-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9a29e-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="9a29e-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="9a29e-105">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="9a29e-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="9a29e-106">В этой статье рассматривается использование PowerShell для добавления подключений типа "сеть — сеть" (S2S) к VPN-шлюзу с имеющимся подключением.</span><span class="sxs-lookup"><span data-stu-id="9a29e-106">This article walks you through using PowerShell to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="9a29e-107">Этот тип подключения часто называется "многосайтовым".</span><span class="sxs-lookup"><span data-stu-id="9a29e-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="9a29e-108">Действия из этой статьи относятся к виртуальным сетям, созданным с помощью классической модели развертывания (также называется управлением службами).</span><span class="sxs-lookup"><span data-stu-id="9a29e-108">The steps in this article apply to virtual networks created using the classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="9a29e-109">Эти действия не применяются к параллельно существующим конфигурациям подключений ExpressRoute и "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="9a29e-109">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="9a29e-110">Модели и методы развертывания</span><span class="sxs-lookup"><span data-stu-id="9a29e-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="9a29e-111">Мы обновляем эту таблицу по мере выпуска новых статей и дополнительных инструментов для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9a29e-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="9a29e-112">При появлении статьи мы указываем прямую ссылку на нее в этой таблице.</span><span class="sxs-lookup"><span data-stu-id="9a29e-112">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="9a29e-113">О подключении</span><span class="sxs-lookup"><span data-stu-id="9a29e-113">About connecting</span></span>

<span data-ttu-id="9a29e-114">Вы можете подключить несколько локальных сайтов к одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a29e-114">You can connect multiple on-premises sites to a single virtual network.</span></span> <span data-ttu-id="9a29e-115">Это особенно привлекательно для создания гибридных облачных решений.</span><span class="sxs-lookup"><span data-stu-id="9a29e-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="9a29e-116">Создание многосайтового подключения к шлюзу виртуальной сети Azure похоже на создание других подключений типа "сеть-сеть".</span><span class="sxs-lookup"><span data-stu-id="9a29e-116">Creating a multi-site connection to your Azure virtual network gateway is similar to creating other Site-to-Site connections.</span></span> <span data-ttu-id="9a29e-117">На самом деле вы можете использовать имеющийся VPN-шлюз Azure, если это шлюз с динамической маршрутизацией (на основе маршрутов).</span><span class="sxs-lookup"><span data-stu-id="9a29e-117">In fact, you can use an existing Azure VPN gateway, as long as the gateway is dynamic (route-based).</span></span>

<span data-ttu-id="9a29e-118">Если к вашей виртуальной сети уже подключен статический шлюз, вы можете изменить его тип на динамический, не перестраивая виртуальную сеть, чтобы обеспечить многосайтовое подключение.</span><span class="sxs-lookup"><span data-stu-id="9a29e-118">If you already have a static gateway connected to your virtual network, you can change the gateway type to dynamic without needing to rebuild the virtual network in order to accommodate multi-site.</span></span> <span data-ttu-id="9a29e-119">Прежде чем менять тип маршрутизации, убедитесь, что локальный VPN-шлюз поддерживает конфигурации VPN на основе маршрутов.</span><span class="sxs-lookup"><span data-stu-id="9a29e-119">Before changing the routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="9a29e-120">![Схема многосайтового подключения](./media/vpn-gateway-multi-site/multisite.png "Многосайтовое подключение")</span><span class="sxs-lookup"><span data-stu-id="9a29e-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-to-consider"></a><span data-ttu-id="9a29e-121">Что необходимо учесть</span><span class="sxs-lookup"><span data-stu-id="9a29e-121">Points to consider</span></span>

<span data-ttu-id="9a29e-122">**Для внесения изменений в эту виртуальную сеть портал не подходит.**</span><span class="sxs-lookup"><span data-stu-id="9a29e-122">**You won't be able to use the portal to make changes to this virtual network.**</span></span> <span data-ttu-id="9a29e-123">Нужно внести в файл конфигурации сети, а не использовать для этого портал.</span><span class="sxs-lookup"><span data-stu-id="9a29e-123">You need to make changes to the network configuration file instead of using the portal.</span></span> <span data-ttu-id="9a29e-124">Если внести изменения на портале, они заменят параметры ссылок на несколько сайтов для этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a29e-124">If you make changes in the portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="9a29e-125">К завершению процедуры многосайтового подключения вы научитесь уверенно использовать файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="9a29e-125">You should feel comfortable using the network configuration file by the time you've completed the multi-site procedure.</span></span> <span data-ttu-id="9a29e-126">Однако при наличии нескольких людей, работающих над конфигурацией сети, необходимо убедиться, что все знают об этом ограничении.</span><span class="sxs-lookup"><span data-stu-id="9a29e-126">However, if you have multiple people working on your network configuration, you'll need to make sure that everyone knows about this limitation.</span></span> <span data-ttu-id="9a29e-127">Это не значит, что использовать портал Azure вообще не нужно.</span><span class="sxs-lookup"><span data-stu-id="9a29e-127">This doesn't mean that you can't use the portal at all.</span></span> <span data-ttu-id="9a29e-128">Вы можете использовать его для всех действий, кроме изменения конфигурации этой конкретной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a29e-128">You can use it for everything else, except making configuration changes to this particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9a29e-129">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9a29e-129">Before you begin</span></span>

<span data-ttu-id="9a29e-130">Перед началом настройки убедитесь, что выполнены следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="9a29e-130">Before you begin configuration, verify that you have the following:</span></span>

* <span data-ttu-id="9a29e-131">Совместимое оборудование VPN для каждого местного расположения.</span><span class="sxs-lookup"><span data-stu-id="9a29e-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="9a29e-132">Ознакомьтесь со статьей [VPN-устройства для создания виртуальных сетей](vpn-gateway-about-vpn-devices.md) , чтобы проверить, является ли совместимым устройство, которое вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="9a29e-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) to verify if the device that you want to use is something that is known to be compatible.</span></span>
* <span data-ttu-id="9a29e-133">Внешний общедоступный IPv4-адрес для каждого VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="9a29e-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="9a29e-134">Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="9a29e-134">The IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="9a29e-135">Это обязательное требование.</span><span class="sxs-lookup"><span data-stu-id="9a29e-135">This is requirement.</span></span>
* <span data-ttu-id="9a29e-136">Вам потребуется установить последнюю версию командлетов Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a29e-136">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="9a29e-137">В дополнение к версии Resource Manager нужно установить версию управления службой (SM).</span><span class="sxs-lookup"><span data-stu-id="9a29e-137">Make sure you install the Service Management (SM) version in addition to the Resource Manager version.</span></span> <span data-ttu-id="9a29e-138">Дополнительные сведения см. в статье [Как установить и настроить Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9a29e-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="9a29e-139">Пользователь, имеющий опыт в настройке вашего оборудования VPN.</span><span class="sxs-lookup"><span data-stu-id="9a29e-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="9a29e-140">Вам нужно будет хорошо понимать, как настраивать VPN-устройство, или воспользоваться помощью соответствующего специалиста.</span><span class="sxs-lookup"><span data-stu-id="9a29e-140">You'll have to have a strong understanding of how to configure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="9a29e-141">Диапазоны IP-адресов, которые вы хотите использовать для виртуальной сети (если она еще не создана).</span><span class="sxs-lookup"><span data-stu-id="9a29e-141">The IP address ranges that you want to use for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="9a29e-142">Диапазоны IP-адресов для каждого сайта локальной сети, к которым вы будете подключаться.</span><span class="sxs-lookup"><span data-stu-id="9a29e-142">The IP address ranges for each of the local network sites that you'll be connecting to.</span></span> <span data-ttu-id="9a29e-143">Понадобится убедиться, что диапазоны IP-адресов сайтов локальной сети, к которым требуется подключиться, не перекрываются.</span><span class="sxs-lookup"><span data-stu-id="9a29e-143">You'll need to make sure that the IP address ranges for each of the local network sites that you want to connect to do not overlap.</span></span> <span data-ttu-id="9a29e-144">В противном случае портал или REST API отклонит передаваемую конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="9a29e-144">Otherwise, the portal or the REST API will reject the configuration being uploaded.</span></span><br><span data-ttu-id="9a29e-145">Например, если два сайта локальной сети содержат диапазон IP-адресов 10.2.3.0/24 и имеется пакет с адресом назначения 10.2.3.3, Azure не сможет определить сайт, на который требуется отправить пакет, так как диапазоны адресов перекрываются.</span><span class="sxs-lookup"><span data-stu-id="9a29e-145">For example, if you have two local network sites that both contain the IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want to send the package to because the address ranges are overlapping.</span></span> <span data-ttu-id="9a29e-146">Для предотвращения проблем с маршрутизацией Azure не позволит передать файл конфигурации с перекрывающимися диапазонами адресов.</span><span class="sxs-lookup"><span data-stu-id="9a29e-146">To prevent routing issues, Azure doesn't allow you to upload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="9a29e-147">1. Создание подключения VPN типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="9a29e-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="9a29e-148">Это отлично, если у вас уже есть подключение VPN типа "сеть — сеть" со шлюзом с динамической маршрутизацией.</span><span class="sxs-lookup"><span data-stu-id="9a29e-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="9a29e-149">Можно перейти к [экспорту параметров конфигурации виртуальной сети](#export).</span><span class="sxs-lookup"><span data-stu-id="9a29e-149">You can proceed to [Export the virtual network configuration settings](#export).</span></span> <span data-ttu-id="9a29e-150">Если нет, выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="9a29e-150">If not, do the following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="9a29e-151">Если у вас уже есть виртуальная сеть типа "сеть — сеть", но со шлюзом со статической маршрутизацией (на основе политики)</span><span class="sxs-lookup"><span data-stu-id="9a29e-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="9a29e-152">Измените тип шлюза на шлюз с динамической маршрутизацией.</span><span class="sxs-lookup"><span data-stu-id="9a29e-152">Change your gateway type to dynamic routing.</span></span> <span data-ttu-id="9a29e-153">Для многосайтового подключения VPN требуется шлюз с динамической маршрутизацией (также известный как шлюз на основе маршрутов).</span><span class="sxs-lookup"><span data-stu-id="9a29e-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="9a29e-154">Чтобы изменить тип шлюза, необходимо сначала удалить существующий шлюз, а затем создать новый.</span><span class="sxs-lookup"><span data-stu-id="9a29e-154">To change your gateway type, you'll need to first delete the existing gateway, then create a new one.</span></span> <span data-ttu-id="9a29e-155">Инструкции см. в разделе [Как изменить тип маршрутизации VPN для шлюза](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="9a29e-155">For instructions, see [How to change the VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="9a29e-156">Настройте новый шлюз и создайте VPN-туннель.</span><span class="sxs-lookup"><span data-stu-id="9a29e-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="9a29e-157">Инструкции см. в разделе [Настройка VPN-шлюза на классическом портале Azure](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="9a29e-157">For instructions, see [Configure a VPN Gateway in the Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="9a29e-158">Сначала измените тип шлюза на шлюз с динамической маршрутизацией.</span><span class="sxs-lookup"><span data-stu-id="9a29e-158">First, change your gateway type to dynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="9a29e-159">Если у вас нет виртуальной сети типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="9a29e-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="9a29e-160">Создайте виртуальную сеть типа "сеть — сеть" с помощью указаний в статье [Создание виртуальной сети с VPN-подключением типа "сеть — сеть" с помощью классического портала Azure](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="9a29e-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in the Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="9a29e-161">Настройте шлюз с динамической маршрутизацией с помощью следующей процедуры: [Настройка VPN-шлюза](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="9a29e-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="9a29e-162">Не забудьте выбрать **динамическую маршрутизацию** в качестве типа шлюза.</span><span class="sxs-lookup"><span data-stu-id="9a29e-162">Be sure to select **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="9a29e-163"><a name="export"></a>2. Экспорт файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="9a29e-163"><a name="export"></a>2. Export the network configuration file</span></span>
<span data-ttu-id="9a29e-164">Экспортируйте файл конфигурации сети Azure, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="9a29e-164">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="9a29e-165">При необходимости можно изменить расположение файла для экспорта.</span><span class="sxs-lookup"><span data-stu-id="9a29e-165">You can change the location of the file to export to a different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-the-network-configuration-file"></a><span data-ttu-id="9a29e-166">3. Открытие файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="9a29e-166">3. Open the network configuration file</span></span>
<span data-ttu-id="9a29e-167">Откройте файл конфигурации сети, скачанный на последнем шаге.</span><span class="sxs-lookup"><span data-stu-id="9a29e-167">Open the network configuration file that you downloaded in the last step.</span></span> <span data-ttu-id="9a29e-168">Используйте любой редактор XML.</span><span class="sxs-lookup"><span data-stu-id="9a29e-168">Use any xml editor that you like.</span></span> <span data-ttu-id="9a29e-169">Файл должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9a29e-169">The file should look similar to the following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="9a29e-170">4. Добавление ссылок на несколько сайтов</span><span class="sxs-lookup"><span data-stu-id="9a29e-170">4. Add multiple site references</span></span>
<span data-ttu-id="9a29e-171">При добавлении или удалении данных ссылок на сайты будут внесены изменения в элемент ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="9a29e-171">When you add or remove site reference information, you'll make configuration changes to the ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="9a29e-172">При добавлении новой ссылки на локальный сайт Azure инициирует создание нового туннеля.</span><span class="sxs-lookup"><span data-stu-id="9a29e-172">Adding a new local site reference triggers Azure to create a new tunnel.</span></span> <span data-ttu-id="9a29e-173">В следующем примере приведена конфигурации сети для подключения одного сайта.</span><span class="sxs-lookup"><span data-stu-id="9a29e-173">In the example below, the network configuration is for a single-site connection.</span></span> <span data-ttu-id="9a29e-174">Сохраните файл после внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="9a29e-174">Save the file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="9a29e-175">Чтобы добавить ссылки на сайты (создать многосайтовую конфигурацию), просто добавьте дополнительные строки "LocalNetworkSiteRef", как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="9a29e-175">To add additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in the example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-the-network-configuration-file"></a><span data-ttu-id="9a29e-176">5. Импорт файла конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="9a29e-176">5. Import the network configuration file</span></span>
<span data-ttu-id="9a29e-177">Импортируйте файл конфигурации сети.</span><span class="sxs-lookup"><span data-stu-id="9a29e-177">Import the network configuration file.</span></span> <span data-ttu-id="9a29e-178">После импорта этого файла с изменениями будут добавлены новые туннели.</span><span class="sxs-lookup"><span data-stu-id="9a29e-178">When you import this file with the changes, the new tunnels will be added.</span></span> <span data-ttu-id="9a29e-179">Туннели будут использовать динамический шлюз, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="9a29e-179">The tunnels will use the dynamic gateway that you created earlier.</span></span> <span data-ttu-id="9a29e-180">Для импорта файла можно использовать либо классический портал, либо PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a29e-180">You can either use the classic portal, or PowerShell to import the file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="9a29e-181">6. Скачивание ключей</span><span class="sxs-lookup"><span data-stu-id="9a29e-181">6. Download keys</span></span>
<span data-ttu-id="9a29e-182">После добавления новых туннелей используйте командлет PowerShell "Get-AzureVNetGatewayKey", чтобы получить общие ключи IPsec/IKE для каждого туннеля.</span><span class="sxs-lookup"><span data-stu-id="9a29e-182">Once your new tunnels have been added, use the PowerShell cmdlet 'Get-AzureVNetGatewayKey' to get the IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="9a29e-183">Например:</span><span class="sxs-lookup"><span data-stu-id="9a29e-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="9a29e-184">Кроме того, при желании можно использовать REST API *получения общего ключа шлюза виртуальной сети* для получения общих ключей.</span><span class="sxs-lookup"><span data-stu-id="9a29e-184">If you prefer, you can also use the *Get Virtual Network Gateway Shared Key* REST API to get the pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="9a29e-185">7. Проверка подключений</span><span class="sxs-lookup"><span data-stu-id="9a29e-185">7. Verify your connections</span></span>
<span data-ttu-id="9a29e-186">Проверьте состояние многосайтового туннеля.</span><span class="sxs-lookup"><span data-stu-id="9a29e-186">Check the multi-site tunnel status.</span></span> <span data-ttu-id="9a29e-187">После скачивания ключей для каждого туннеля необходимо проверить подключения.</span><span class="sxs-lookup"><span data-stu-id="9a29e-187">After downloading the keys for each tunnel, you'll want to verify connections.</span></span> <span data-ttu-id="9a29e-188">Используйте командлет "Get-AzureVnetConnection", чтобы получить список туннелей виртуальной сети, как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="9a29e-188">Use 'Get-AzureVnetConnection' to get a list of virtual network tunnels, as shown in the example below.</span></span> <span data-ttu-id="9a29e-189">VNet1 — имя виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="9a29e-189">VNet1 is the name of the VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="9a29e-190">Пример возвращаемых данных:</span><span class="sxs-lookup"><span data-stu-id="9a29e-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site1' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site2' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="9a29e-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a29e-191">Next steps</span></span>

<span data-ttu-id="9a29e-192">Чтобы больше узнать о VPN-шлюзах, см. статью [Шлюзы VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="9a29e-192">To learn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
