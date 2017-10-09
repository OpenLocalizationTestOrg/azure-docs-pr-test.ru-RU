---
title: "aaaTroubleshoot VPN Azure сайт-сайт периодически отключает | Документы Microsoft"
description: "Узнайте, как tootroubleshoot hello проблемы соединений через виртуальную Частную сеть для hello регулярно отключен."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="a2d05-103">Устранение проблемы периодических разрывов подключений VPN типа "сеть — сеть" Azure</span><span class="sxs-lookup"><span data-stu-id="a2d05-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="a2d05-104">Могут возникнуть проблемы hello может быть нестабильным или отключает регулярно нового или существующего подключения VPN Microsoft Azure точка-сеть.</span><span class="sxs-lookup"><span data-stu-id="a2d05-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="a2d05-105">В этой статье приведены Устранение toohelp действия обнаруживать и устранять hello причины проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="a2d05-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="a2d05-106">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="a2d05-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="a2d05-107">Предварительные действия</span><span class="sxs-lookup"><span data-stu-id="a2d05-107">Prerequisite step</span></span>

<span data-ttu-id="a2d05-108">Проверьте тип hello шлюза виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="a2d05-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="a2d05-109">Go слишком[портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a2d05-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a2d05-110">Проверьте hello **Обзор** страница hello шлюз виртуальной сети для сведений о типе hello.</span><span class="sxs-lookup"><span data-stu-id="a2d05-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![Общие сведения о Hello hello шлюза](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="a2d05-112">Шаг 1 Проверьте ли hello локальной проверенных VPN-устройства</span><span class="sxs-lookup"><span data-stu-id="a2d05-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="a2d05-113">Узнайте, используете ли вы [проверенную версию VPN-устройства и операционной системы](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="a2d05-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="a2d05-114">Если VPN-устройства hello не проверяется, имеется toosee изготовителя устройства hello toocontact при наличии любые проблемы совместимости.</span><span class="sxs-lookup"><span data-stu-id="a2d05-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="a2d05-115">Убедитесь в том, что это устройство VPN hello настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="a2d05-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="a2d05-116">Дополнительные сведения см. на странице об [изменении примеров конфигурации устройств](vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="a2d05-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="a2d05-117">Шаг 2 Проверьте hello параметры сопоставления безопасности (для шлюзов виртуальной сети Azure на основе политики)</span><span class="sxs-lookup"><span data-stu-id="a2d05-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="a2d05-118">Убедитесь, что hello виртуальной сети, подсети и диапазоны в hello **шлюз локальной сети** определение в Microsoft Azure, соответствуют конфигурации hello на hello локального VPN-устройства.</span><span class="sxs-lookup"><span data-stu-id="a2d05-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="a2d05-119">Проверьте, соответствующие параметры hello сопоставления безопасности.</span><span class="sxs-lookup"><span data-stu-id="a2d05-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="a2d05-120">Шаг 3. Проверьте определяемые пользователем маршруты или группы безопасности сети в подсети шлюза</span><span class="sxs-lookup"><span data-stu-id="a2d05-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="a2d05-121">Пользовательские маршрут hello подсеть шлюза может ограничения часть трафика и разрешения других трафика.</span><span class="sxs-lookup"><span data-stu-id="a2d05-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="a2d05-122">Оказывается, что hello VPN-подключения является достоверным для некоторых трафика и хорошо подходит для других.</span><span class="sxs-lookup"><span data-stu-id="a2d05-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="a2d05-123">Шаг 4. Проверка Здравствуйте «один туннель VPN каждой подсети пары» (для шлюзов виртуальной сети на основе политик)</span><span class="sxs-lookup"><span data-stu-id="a2d05-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="a2d05-124">Убедитесь в том, что hello локального VPN-устройство имеет значение toohave **один туннель VPN каждой пары подсети** для шлюзов виртуальных сетей на основе политик.</span><span class="sxs-lookup"><span data-stu-id="a2d05-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="a2d05-125">Шаг 5. Проверьте ограничения сопоставления безопасности (для шлюзов виртуальной сети на основе политик)</span><span class="sxs-lookup"><span data-stu-id="a2d05-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="a2d05-126">шлюз виртуальной сети на основе политик Hello ограничен 200 пар подсети сопоставления безопасности.</span><span class="sxs-lookup"><span data-stu-id="a2d05-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="a2d05-127">Если количество hello подсетей виртуальной сети Azure, умноженное на время, hello число локальных подсетях больше 200, появиться случайные подсетей отключение.</span><span class="sxs-lookup"><span data-stu-id="a2d05-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="a2d05-128">Шаг 6. Проверьте внешний адрес интерфейса для локального VPN-устройства</span><span class="sxs-lookup"><span data-stu-id="a2d05-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="a2d05-129">Если hello IP-адрес устройства VPN hello в Интернете включается в hello **шлюз локальной сети** определение в Azure, могут возникать нерегулярные отключения.</span><span class="sxs-lookup"><span data-stu-id="a2d05-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="a2d05-130">Hello внешнего интерфейса устройства должны находиться непосредственно в Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="a2d05-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="a2d05-131">Должно быть не сетевых адресов (NAT) или брандмауэр между hello Интернета и устройством hello.</span><span class="sxs-lookup"><span data-stu-id="a2d05-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="a2d05-132">При настройке брандмауэра кластеризации toohave виртуального IP-адреса, необходимо разорвать кластера hello и предоставлять hello VPN-устройством напрямую tooa открытый интерфейс, который hello шлюза может взаимодействовать с.</span><span class="sxs-lookup"><span data-stu-id="a2d05-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="a2d05-133">Шаг 7 Проверка ли hello из локального VPN-устройство имеет точной пересылки (PFS) включена</span><span class="sxs-lookup"><span data-stu-id="a2d05-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="a2d05-134">Hello **точной пересылки (PFS)** функции может привести к проблемам отключения hello.</span><span class="sxs-lookup"><span data-stu-id="a2d05-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="a2d05-135">Если VPN-устройства hello **точную пересылку (PFS)** включен, отключить функцию hello.</span><span class="sxs-lookup"><span data-stu-id="a2d05-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="a2d05-136">Затем [обновление политики IPsec шлюза виртуальной сети hello](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span><span class="sxs-lookup"><span data-stu-id="a2d05-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a2d05-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2d05-137">Next steps</span></span>

- [<span data-ttu-id="a2d05-138">Настройка виртуальной сети tooa подключения сеть-сеть</span><span class="sxs-lookup"><span data-stu-id="a2d05-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="a2d05-139">Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"</span><span class="sxs-lookup"><span data-stu-id="a2d05-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

