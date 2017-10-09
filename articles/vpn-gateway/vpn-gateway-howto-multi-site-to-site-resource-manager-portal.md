---
title: "Добавление нескольких VPN шлюзом для межсайтовых подключений tooa виртуальной сети: портала Azure: диспетчер ресурсов | Документы Microsoft"
description: "Добавление нескольких сайтов S2S подключений tooa VPN-шлюз, имеется существующее подключение"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="69f99-103">Добавить tooa подключения сайта для сайта виртуальной сети с помощью существующего VPN-подключения шлюза</span><span class="sxs-lookup"><span data-stu-id="69f99-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="69f99-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="69f99-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="69f99-105">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="69f99-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="69f99-106">В этой статье описывается использование hello Azure портала tooadd-сайтами (S2S) подключений tooa VPN-шлюз, имеется существующее подключение.</span><span class="sxs-lookup"><span data-stu-id="69f99-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="69f99-107">Этот тип подключения чаще всего ссылка tooas конфигурации «нескольких сайтов».</span><span class="sxs-lookup"><span data-stu-id="69f99-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="69f99-108">Вы можете добавить tooa подключения S2S виртуальной сети, который уже S2S подключение, подключение точка-сеть или подключение виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="69f99-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="69f99-109">При добавлении подключения есть некоторые ограничения.</span><span class="sxs-lookup"><span data-stu-id="69f99-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="69f99-110">Проверьте hello [перед началом](#before) раздела в этой статье tooverify, прежде чем начать настройку.</span><span class="sxs-lookup"><span data-stu-id="69f99-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="69f99-111">Эта статья относится tooVNets, созданных с помощью модели развертывания диспетчера ресурсов hello, шлюз VPN routebased..</span><span class="sxs-lookup"><span data-stu-id="69f99-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="69f99-112">Эти действия не относятся существующих конфигураций подключений tooExpressRoute/сайт-сайт.</span><span class="sxs-lookup"><span data-stu-id="69f99-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="69f99-113">Сведения о параллельно существующих подключениях см. в разделе [Параллельно существующие подключения ExpressRoute и "сеть — сеть"](../expressroute/expressroute-howto-coexist-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="69f99-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="69f99-114">Модели и методы развертывания</span><span class="sxs-lookup"><span data-stu-id="69f99-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="69f99-115">Мы обновляем эту таблицу по мере выпуска новых статей и дополнительных инструментов для этой конфигурации.</span><span class="sxs-lookup"><span data-stu-id="69f99-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="69f99-116">Если статья доступен, непосредственно свяжем tooit из этой таблицы.</span><span class="sxs-lookup"><span data-stu-id="69f99-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="69f99-117"><a name="before"></a>Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="69f99-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="69f99-118">Проверьте hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="69f99-118">Verify hello following items:</span></span>

* <span data-ttu-id="69f99-119">Убедитесь, что не создаете параллельно действующие подключения ExpressRoute и "сеть — сеть".</span><span class="sxs-lookup"><span data-stu-id="69f99-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="69f99-120">У вас есть виртуальная сеть, созданную с помощью модели развертывания диспетчера ресурсов hello использовать существующее подключение.</span><span class="sxs-lookup"><span data-stu-id="69f99-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="69f99-121">Hello шлюз виртуальной сети для виртуальной сети — routebased..</span><span class="sxs-lookup"><span data-stu-id="69f99-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="69f99-122">При наличии шлюза PolicyBased VPN, необходимо удалить шлюз виртуальной сети hello и создать новый шлюз VPN как routebased..</span><span class="sxs-lookup"><span data-stu-id="69f99-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="69f99-123">Ни один из диапазонов адресов hello перекрываться для любого hello виртуальных сетей, которая подключается к этой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="69f99-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="69f99-124">У вас есть совместимых устройств VPN и тем, кто имеет доступ tooconfigure его.</span><span class="sxs-lookup"><span data-stu-id="69f99-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="69f99-125">См. статью о [VPN-устройствах](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="69f99-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="69f99-126">Если вы не знакомы с конфигурацией своего устройства VPN или не знакомы с hello диапазоны IP-адресов в конфигурации локальной сети, необходимо toocoordinate с тем, кто сможет предоставить эти сведения для вас.</span><span class="sxs-lookup"><span data-stu-id="69f99-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="69f99-127">Имеется внешний общедоступный IP-адрес для VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="69f99-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="69f99-128">Этот IP-адрес не может располагаться вне преобразования сетевых адресов (NAT).</span><span class="sxs-lookup"><span data-stu-id="69f99-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="69f99-129"><a name="part1"></a>Часть 1. Настройка подключения</span><span class="sxs-lookup"><span data-stu-id="69f99-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="69f99-130">В браузере перейдите toohello [портал Azure](http://portal.azure.com) и, при необходимости, выполнить вход с учетной записью Azure.</span><span class="sxs-lookup"><span data-stu-id="69f99-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="69f99-131">Нажмите кнопку **все ресурсы** и найдите вашей **шлюз виртуальной сети** из списка ресурсов hello и щелкните его.</span><span class="sxs-lookup"><span data-stu-id="69f99-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="69f99-132">На hello **шлюз виртуальной сети** колонка, щелкните **подключения**.</span><span class="sxs-lookup"><span data-stu-id="69f99-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="69f99-133">![Колонка подключений](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Колонка подключений")</span><span class="sxs-lookup"><span data-stu-id="69f99-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="69f99-134">На hello **подключений** колонка, щелкните **+ добавить**.</span><span class="sxs-lookup"><span data-stu-id="69f99-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="69f99-135">![Добавить кнопки подключения](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "кнопку Добавить соединения")</span><span class="sxs-lookup"><span data-stu-id="69f99-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="69f99-136">На hello **добавить подключение** колонки, заполните следующие поля hello:</span><span class="sxs-lookup"><span data-stu-id="69f99-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="69f99-137">**Имя:** hello имя узла toohello toogive вы создаете подключение hello.</span><span class="sxs-lookup"><span data-stu-id="69f99-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="69f99-138">**Тип подключения.** Выберите **Сеть — сеть (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="69f99-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="69f99-139">![Добавить подключение колонке](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "добавить подключение колонку")</span><span class="sxs-lookup"><span data-stu-id="69f99-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="69f99-140"><a name="part2"></a>Часть 2. Добавление шлюза локальной сети</span><span class="sxs-lookup"><span data-stu-id="69f99-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="69f99-141">Щелкните **Шлюз локальной сети**, а затем ***Выберите шлюз локальной сети***.</span><span class="sxs-lookup"><span data-stu-id="69f99-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="69f99-142">После этого откроется hello **Выбор шлюза локальной сети** колонку.</span><span class="sxs-lookup"><span data-stu-id="69f99-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="69f99-143">![Выбор шлюза локальной сети](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Выбор шлюза локальной сети")</span><span class="sxs-lookup"><span data-stu-id="69f99-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="69f99-144">Нажмите кнопку **создать новый** tooopen hello **создать шлюз локальной сети** колонку.</span><span class="sxs-lookup"><span data-stu-id="69f99-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="69f99-145">![Создание локальной сети шлюза колонке](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "создать шлюз локальной сети")</span><span class="sxs-lookup"><span data-stu-id="69f99-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="69f99-146">На hello **создать шлюз локальной сети** колонки, заполните следующие поля hello:</span><span class="sxs-lookup"><span data-stu-id="69f99-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="69f99-147">**Имя:** hello имя ресурса шлюза локальной сети toohello toogive.</span><span class="sxs-lookup"><span data-stu-id="69f99-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="69f99-148">**IP-адрес:** hello hello VPN-устройства на узел hello tooconnect на общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="69f99-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="69f99-149">**Адресное пространство:** hello адресное пространство, которое следует toobe направлено toohello новый сайт локальной сети.</span><span class="sxs-lookup"><span data-stu-id="69f99-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="69f99-150">Нажмите кнопку **ОК** на hello **создать шлюз локальной сети** колонке toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="69f99-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="69f99-151"><a name="part3"></a>Часть 3 — добавить общий ключ hello и создания подключения hello</span><span class="sxs-lookup"><span data-stu-id="69f99-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="69f99-152">На hello **добавить подключение** колонке добавить hello общий ключ должен toouse toocreate подключения к.</span><span class="sxs-lookup"><span data-stu-id="69f99-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="69f99-153">Можно получить общий ключ hello из устройства VPN или сделать здесь и затем настройте ваш hello toouse устройство VPN же общим ключом.</span><span class="sxs-lookup"><span data-stu-id="69f99-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="69f99-154">важный, что это ключи hello абсолютно Hello hello таким же.</span><span class="sxs-lookup"><span data-stu-id="69f99-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="69f99-155">![Общий ключ](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Общий ключ")</span><span class="sxs-lookup"><span data-stu-id="69f99-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="69f99-156">Hello нижней части колонки hello, нажмите кнопку **ОК** toocreate hello соединения.</span><span class="sxs-lookup"><span data-stu-id="69f99-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="69f99-157"><a name="part4"></a>Часть 4 - Проверка hello VPN-подключения</span><span class="sxs-lookup"><span data-stu-id="69f99-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="69f99-158">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69f99-158">Next steps</span></span>

<span data-ttu-id="69f99-159">После завершения подключения можно добавить виртуальные машины tooyour виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="69f99-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="69f99-160">Hello виртуальные машины в разделе [обучения](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="69f99-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
