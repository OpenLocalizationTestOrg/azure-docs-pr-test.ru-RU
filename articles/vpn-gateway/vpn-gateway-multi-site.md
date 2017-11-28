---
title: "Подключение сайтов toomultiple виртуальной сети, с помощью VPN-шлюза и PowerShell: классический | Документы Microsoft"
description: "В этой статье описывается подключение нескольких локальных сайтов tooa виртуальной сети с помощью VPN-шлюза для hello классической модели развертывания."
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
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="29713-103">Добавить tooa подключения сайта для сайта виртуальной сети с помощью существующего VPN-шлюза подключения (классические)</span><span class="sxs-lookup"><span data-stu-id="29713-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="29713-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="29713-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="29713-105">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="29713-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="29713-106">В этой статье описывается с помощью PowerShell tooadd-сайтами (S2S) подключений tooa VPN-шлюз, имеется существующее подключение.</span><span class="sxs-lookup"><span data-stu-id="29713-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="29713-107">Этот тип подключения чаще всего ссылка tooas конфигурации «нескольких сайтов».</span><span class="sxs-lookup"><span data-stu-id="29713-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="29713-108">Hello действия в этой статье, относятся toovirtual сетей, созданных с помощью hello классической модели развертывания (также известные как службы управления).</span><span class="sxs-lookup"><span data-stu-id="29713-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="29713-109">Эти действия не относятся существующих конфигураций подключений tooExpressRoute/сайт-сайт.</span><span class="sxs-lookup"><span data-stu-id="29713-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="29713-110">Модели и методы развертывания</span><span class="sxs-lookup"><span data-stu-id="29713-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="29713-111">Мы обновляем эту таблицу по мере выпуска новых статей и дополнительных инструментов для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="29713-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="29713-112">Если статья доступен, непосредственно свяжем tooit из этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="29713-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="29713-113">О подключении</span><span class="sxs-lookup"><span data-stu-id="29713-113">About connecting</span></span>

<span data-ttu-id="29713-114">Можно подключить несколько локальных сайтов tooa одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="29713-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="29713-115">Это особенно привлекательно для создания гибридных облачных решений.</span><span class="sxs-lookup"><span data-stu-id="29713-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="29713-116">Создание шлюза виртуальной сети Azure подключение нескольких сайтов tooyour составляет примерно toocreating других подключений сайт-сайт.</span><span class="sxs-lookup"><span data-stu-id="29713-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="29713-117">На самом деле можно использовать существующий шлюз Azure VPN, при условии, что шлюз hello является динамическим (на основе маршрутов).</span><span class="sxs-lookup"><span data-stu-id="29713-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="29713-118">При наличии подключенных tooyour статический шлюз виртуальной сети можно изменить toodynamic типа hello шлюза, не перестраивая toorebuild hello виртуальной сети в порядке tooaccommodate несколькими сайтами.</span><span class="sxs-lookup"><span data-stu-id="29713-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="29713-119">Перед изменением типа маршрутизации hello, убедитесь, что шлюза VPN локальной поддерживает конфигурации VPN на основе маршрута.</span><span class="sxs-lookup"><span data-stu-id="29713-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="29713-120">![Схема многосайтового подключения](./media/vpn-gateway-multi-site/multisite.png "Многосайтовое подключение")</span><span class="sxs-lookup"><span data-stu-id="29713-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="29713-121">Tooconsider точек</span><span class="sxs-lookup"><span data-stu-id="29713-121">Points tooconsider</span></span>

<span data-ttu-id="29713-122">**Его нельзя будет toouse hello портала toomake изменения toothis виртуальной сети.**</span><span class="sxs-lookup"><span data-stu-id="29713-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="29713-123">Требуется файл конфигурации сети toohello изменения toomake вместо использования портала hello.</span><span class="sxs-lookup"><span data-stu-id="29713-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="29713-124">При внесении изменений в портале hello они заменят параметры несколькими сайтами ссылку для этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="29713-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="29713-125">Вы уверены, что справитесь с помощью файла конфигурации сети hello, hello времени после завершения процедуры hello несколькими сайтами.</span><span class="sxs-lookup"><span data-stu-id="29713-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="29713-126">Тем не менее при наличии нескольких работающим по конфигурации сети, необходимо убедиться, что все знает об этом ограничении toomake.</span><span class="sxs-lookup"><span data-stu-id="29713-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="29713-127">Это не значит, что нельзя использовать портал hello во всех.</span><span class="sxs-lookup"><span data-stu-id="29713-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="29713-128">Можно использовать для всех остальных объектов, за исключением того, делая конфигурации изменения toothis конкретной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="29713-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="29713-129">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="29713-129">Before you begin</span></span>

<span data-ttu-id="29713-130">Перед началом настройки убедитесь, что hello следующее:</span><span class="sxs-lookup"><span data-stu-id="29713-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="29713-131">Совместимое оборудование VPN для каждого местного расположения.</span><span class="sxs-lookup"><span data-stu-id="29713-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="29713-132">Проверьте [сведения об устройствах VPN для подключения к виртуальной сети](vpn-gateway-about-vpn-devices.md) tooverify Если hello устройства, которые должны toouse, известный toobe совместимы.</span><span class="sxs-lookup"><span data-stu-id="29713-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="29713-133">Внешний общедоступный IPv4-адрес для каждого VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="29713-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="29713-134">Hello IP-адрес не может располагаться за устройством NAT.</span><span class="sxs-lookup"><span data-stu-id="29713-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="29713-135">Это обязательное требование.</span><span class="sxs-lookup"><span data-stu-id="29713-135">This is requirement.</span></span>
* <span data-ttu-id="29713-136">Вам потребуется tooinstall hello последняя версия командлетов Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="29713-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="29713-137">Убедитесь, что установки службы управления (SM) версии hello в версии диспетчера ресурсов toohello сложения.</span><span class="sxs-lookup"><span data-stu-id="29713-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="29713-138">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="29713-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="29713-139">Пользователь, имеющий опыт в настройке вашего оборудования VPN.</span><span class="sxs-lookup"><span data-stu-id="29713-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="29713-140">Вы получите toohave хорошо понимать процесс tooconfigure VPN-устройство или работают с специалистом.</span><span class="sxs-lookup"><span data-stu-id="29713-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="29713-141">диапазоны IP-адресов Hello требуется toouse для виртуальной сети (Если вы еще не созданы).</span><span class="sxs-lookup"><span data-stu-id="29713-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="29713-142">Hello диапазоны IP-адресов для каждого из сайтов локальной сети hello, которые вы будете подключаться.</span><span class="sxs-lookup"><span data-stu-id="29713-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="29713-143">Необходимо убедиться, что диапазоны hello IP-адресов для каждого из сайтов локальной сети hello, что требуется tooconnect toodo не перекрываются toomake.</span><span class="sxs-lookup"><span data-stu-id="29713-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="29713-144">В противном случае hello портала или hello REST API отклонит загружаемую конфигурацию hello.</span><span class="sxs-lookup"><span data-stu-id="29713-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="29713-145">Например если у вас есть два сайта локальной сети, что оба содержат 10.2.3.0/24 диапазон адресов IP hello и у вас есть пакет с адресом назначения 10.2.3.3, Azure не сможет определить сайт, который требуется toosend hello пакета toobecause hello диапазоны адресов — перекрывающиеся.</span><span class="sxs-lookup"><span data-stu-id="29713-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="29713-146">tooprevent проблем с маршрутизацией, Azure не позволяет tooupload файл конфигурации, который имеет пересекающиеся диапазоны адресов.</span><span class="sxs-lookup"><span data-stu-id="29713-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="29713-147">1. Создание подключения VPN типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="29713-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="29713-148">Это отлично, если у вас уже есть подключение VPN типа "сеть — сеть" со шлюзом с динамической маршрутизацией.</span><span class="sxs-lookup"><span data-stu-id="29713-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="29713-149">Можно продолжить слишком[экспорт параметров конфигурации виртуальной сети hello](#export).</span><span class="sxs-lookup"><span data-stu-id="29713-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="29713-150">В противном случае hello следующие:</span><span class="sxs-lookup"><span data-stu-id="29713-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="29713-151">Если у вас уже есть виртуальная сеть типа "сеть — сеть", но со шлюзом со статической маршрутизацией (на основе политики)</span><span class="sxs-lookup"><span data-stu-id="29713-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="29713-152">Изменение маршрута toodynamic тип шлюза.</span><span class="sxs-lookup"><span data-stu-id="29713-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="29713-153">Для многосайтового подключения VPN требуется шлюз с динамической маршрутизацией (также известный как шлюз на основе маршрутов).</span><span class="sxs-lookup"><span data-stu-id="29713-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="29713-154">Введите toochange шлюз, вы добавите требуется toofirst delete hello существующий шлюз, а затем создайте новую.</span><span class="sxs-lookup"><span data-stu-id="29713-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="29713-155">Инструкции см. в разделе [как toochange hello VPN тип маршрутизации шлюза](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="29713-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="29713-156">Настройте новый шлюз и создайте VPN-туннель.</span><span class="sxs-lookup"><span data-stu-id="29713-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="29713-157">Инструкции см. в разделе [настроить VPN-шлюза в классический портал Azure hello](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="29713-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="29713-158">Во-первых измените маршрут toodynamic тип шлюза.</span><span class="sxs-lookup"><span data-stu-id="29713-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="29713-159">Если у вас нет виртуальной сети типа "сеть — сеть"</span><span class="sxs-lookup"><span data-stu-id="29713-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="29713-160">Создание виртуальной сети сайт-сайт с помощью следующей процедуры: [создайте виртуальную сеть с VPN-подключения сеть-сеть в классический портал Azure hello](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="29713-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="29713-161">Настройте шлюз с динамической маршрутизацией с помощью следующей процедуры: [Настройка VPN-шлюза](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="29713-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="29713-162">Быть убедиться, что tooselect **динамической маршрутизации** применительно к типу шлюза.</span><span class="sxs-lookup"><span data-stu-id="29713-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="29713-163"><a name="export"></a>2. Экспортируйте файл конфигурации сети hello</span><span class="sxs-lookup"><span data-stu-id="29713-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="29713-164">Экспортируйте файл конфигурации сети Azure, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="29713-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="29713-165">Можно изменить расположение hello hello tooexport tooa различные расположения файла при необходимости.</span><span class="sxs-lookup"><span data-stu-id="29713-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="29713-166">3. Привет открыть файл конфигурации сети</span><span class="sxs-lookup"><span data-stu-id="29713-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="29713-167">Откройте файл конфигурации сети hello, загруженный на последнем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="29713-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="29713-168">Используйте любой редактор XML.</span><span class="sxs-lookup"><span data-stu-id="29713-168">Use any xml editor that you like.</span></span> <span data-ttu-id="29713-169">файл Hello должен выглядеть примерно toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="29713-169">hello file should look similar toohello following:</span></span>

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

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="29713-170">4. Добавление ссылок на несколько сайтов</span><span class="sxs-lookup"><span data-stu-id="29713-170">4. Add multiple site references</span></span>
<span data-ttu-id="29713-171">При добавлении или удалении будет вносить изменения toohello элемент ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="29713-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="29713-172">Добавление новой ссылки на локальный сайт Azure toocreate запускает новый туннель.</span><span class="sxs-lookup"><span data-stu-id="29713-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="29713-173">В следующем примере hello hello сеть настроена для подключения одного сайта.</span><span class="sxs-lookup"><span data-stu-id="29713-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="29713-174">Сохраните файл hello, после внесения изменений.</span><span class="sxs-lookup"><span data-stu-id="29713-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="29713-175">tooadd дополнительных ссылок на сайты (создать конфигурации нескольких сайтов), достаточно добавить строки дополнительных «LocalNetworkSiteRef», как показано в приведенном ниже примере hello.</span><span class="sxs-lookup"><span data-stu-id="29713-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="29713-176">5. Импорт файла конфигурации сети hello</span><span class="sxs-lookup"><span data-stu-id="29713-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="29713-177">Импорт файла конфигурации сети hello.</span><span class="sxs-lookup"><span data-stu-id="29713-177">Import hello network configuration file.</span></span> <span data-ttu-id="29713-178">При импорте этого файла с изменениями hello, будут добавлены новые туннели hello.</span><span class="sxs-lookup"><span data-stu-id="29713-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="29713-179">Привет туннели будут использовать шлюз с динамической hello, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="29713-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="29713-180">Можно использовать либо hello классического портала или файл hello tooimport PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29713-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="29713-181">6. Скачивание ключей</span><span class="sxs-lookup"><span data-stu-id="29713-181">6. Download keys</span></span>
<span data-ttu-id="29713-182">После добавления новых туннелей используйте hello PowerShell командлет «Get-AzureVNetGatewayKey» tooget hello IPsec/IKE предварительные общие ключи для каждого туннеля.</span><span class="sxs-lookup"><span data-stu-id="29713-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="29713-183">Например:</span><span class="sxs-lookup"><span data-stu-id="29713-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="29713-184">При желании можно также использовать hello *получения шлюза общего ключа виртуальной сети* tooget API-интерфейса REST hello предварительные общие ключи.</span><span class="sxs-lookup"><span data-stu-id="29713-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="29713-185">7. Проверка подключений</span><span class="sxs-lookup"><span data-stu-id="29713-185">7. Verify your connections</span></span>
<span data-ttu-id="29713-186">Проверьте состояние многосайтового туннеля hello.</span><span class="sxs-lookup"><span data-stu-id="29713-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="29713-187">После загрузки hello ключей для каждого туннеля, будет необходимо tooverify подключений.</span><span class="sxs-lookup"><span data-stu-id="29713-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="29713-188">Используйте «Get-AzureVnetConnection» tooget туннели список виртуальных сетей, как показано в приведенном ниже примере hello.</span><span class="sxs-lookup"><span data-stu-id="29713-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="29713-189">VNet1 — имя hello hello виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="29713-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="29713-190">Пример возвращаемых данных:</span><span class="sxs-lookup"><span data-stu-id="29713-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
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
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="29713-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29713-191">Next steps</span></span>

<span data-ttu-id="29713-192">toolearn Дополнительные сведения о шлюзах VPN в разделе [о шлюзах VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="29713-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
