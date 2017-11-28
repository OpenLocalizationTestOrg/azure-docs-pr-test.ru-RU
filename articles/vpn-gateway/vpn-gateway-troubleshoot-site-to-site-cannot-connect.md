---
title: "aaaTroubleshoot Azure VPN-подключение с сайт сайт, который не может подключиться | Документы Microsoft"
description: "Узнайте, как tootroubleshoot сеть сеть VPN-подключения, внезапно перестает работать и будет невозможно."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="4c459-103">Устранение проблемы подключения VPN типа "сеть — сеть" Azure</span><span class="sxs-lookup"><span data-stu-id="4c459-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="4c459-104">После настройки VPN-подключения сеть сеть между локальной сетью и виртуальной сети Azure hello VPN-подключение неожиданно перестанет работать и будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="4c459-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="4c459-105">В этой статье приведены по устранению неполадок toohelp действия при решении этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="4c459-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="4c459-106">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="4c459-106">Troubleshooting steps</span></span>

<span data-ttu-id="4c459-107">tooresolve hello проблему, сначала воспользуйтесь слишком[сброса hello VPN-шлюз Azure](vpn-gateway-resetgw-classic.md) и сбросить hello туннеля VPN-устройство локальной hello.</span><span class="sxs-lookup"><span data-stu-id="4c459-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="4c459-108">При повторном возникновении проблемы hello, выполните эти шаги tooidentify hello причины проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="4c459-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="4c459-109">Предварительные действия</span><span class="sxs-lookup"><span data-stu-id="4c459-109">Prerequisite step</span></span>

<span data-ttu-id="4c459-110">Проверка типа hello hello шлюза Azure VPN.</span><span class="sxs-lookup"><span data-stu-id="4c459-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="4c459-111">Go toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4c459-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4c459-112">Проверьте hello **Обзор** страницы приветствия VPN-шлюза hello сведений о типе.</span><span class="sxs-lookup"><span data-stu-id="4c459-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Общие сведения о шлюзе hello](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="4c459-114">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="4c459-114">Step 1.</span></span> <span data-ttu-id="4c459-115">Проверьте, выполняется ли проверка hello локального VPN-устройства</span><span class="sxs-lookup"><span data-stu-id="4c459-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="4c459-116">Узнайте, используете ли вы [проверенную версию VPN-устройства и операционной системы](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="4c459-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="4c459-117">Если устройство hello не проверенные устройства VPN, toosee изготовителя устройства hello toocontact может потребоваться при наличии проблемы совместимости.</span><span class="sxs-lookup"><span data-stu-id="4c459-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="4c459-118">Убедитесь в том, что это устройство VPN hello настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="4c459-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="4c459-119">Дополнительные сведения см. на странице об [изменении примеров конфигурации устройств](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="4c459-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="4c459-120">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="4c459-120">Step 2.</span></span> <span data-ttu-id="4c459-121">Проверка общего ключа hello</span><span class="sxs-lookup"><span data-stu-id="4c459-121">Verify hello shared key</span></span>

<span data-ttu-id="4c459-122">Сравните hello общий ключ для hello локального VPN устройства toohello виртуальной сети VPN Azure toomake убедиться, что hello ключи совпадают.</span><span class="sxs-lookup"><span data-stu-id="4c459-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="4c459-123">tooview hello общий ключ для hello Azure VPN-подключения, используйте один из следующих методов hello:</span><span class="sxs-lookup"><span data-stu-id="4c459-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="4c459-124">**Портал Azure**</span><span class="sxs-lookup"><span data-stu-id="4c459-124">**Azure portal**</span></span>

1. <span data-ttu-id="4c459-125">Go toohello шлюза сеть сеть через VPN, созданный.</span><span class="sxs-lookup"><span data-stu-id="4c459-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="4c459-126">В hello **параметры** щелкните **общий ключ**.</span><span class="sxs-lookup"><span data-stu-id="4c459-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![Общий ключ](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="4c459-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="4c459-128">**Azure PowerShell**</span></span>

<span data-ttu-id="4c459-129">Для модели развертывания диспетчера ресурсов Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4c459-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="4c459-130">Для hello классической модели развертывания:</span><span class="sxs-lookup"><span data-stu-id="4c459-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="4c459-131">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="4c459-131">Step 3.</span></span> <span data-ttu-id="4c459-132">Проверьте одноранговых VPN hello IP-адресов</span><span class="sxs-lookup"><span data-stu-id="4c459-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="4c459-133">Здравствуйте, определение IP в hello **шлюза локальной сети** объекта в Azure должны совпадать IP-адрес устройства в локальной среде hello.</span><span class="sxs-lookup"><span data-stu-id="4c459-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="4c459-134">Hello определения IP шлюз Azure, установленного на hello локального устройства должен совпадать IP-адреса hello Azure шлюза.</span><span class="sxs-lookup"><span data-stu-id="4c459-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="4c459-135">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="4c459-135">Step 4.</span></span> <span data-ttu-id="4c459-136">Проверьте UDR и Nsg из подсети шлюза hello</span><span class="sxs-lookup"><span data-stu-id="4c459-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="4c459-137">Поиск и удаление определяемых пользователем маршрутизации (UDR) или группы безопасности сети (Nsg) в подсети шлюза hello затем hello результат теста.</span><span class="sxs-lookup"><span data-stu-id="4c459-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="4c459-138">Если hello проблема не будет устранена, проверьте параметры hello, примененные UDR или NSG.</span><span class="sxs-lookup"><span data-stu-id="4c459-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="4c459-139">Шаг 5.</span><span class="sxs-lookup"><span data-stu-id="4c459-139">Step 5.</span></span> <span data-ttu-id="4c459-140">Проверка hello локальный адрес внешнего интерфейса VPN-устройства</span><span class="sxs-lookup"><span data-stu-id="4c459-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="4c459-141">Если hello из Интернета IP-адрес устройства VPN hello включается в hello **локальной сети** определение в Azure, могут возникать нерегулярные отключения.</span><span class="sxs-lookup"><span data-stu-id="4c459-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="4c459-142">Hello внешнего интерфейса устройства должны находиться непосредственно в Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="4c459-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="4c459-143">Должна существовать без преобразования сетевых адресов или брандмауэра между hello Интернета и устройством hello.</span><span class="sxs-lookup"><span data-stu-id="4c459-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="4c459-144">tooconfigure брандмауэра кластеризации toohave виртуального IP-адреса, необходимо разорвать кластера hello и предоставлять hello VPN-устройством напрямую tooa открытый интерфейс, hello шлюза может взаимодействовать с.</span><span class="sxs-lookup"><span data-stu-id="4c459-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="4c459-145">Шаг 6.</span><span class="sxs-lookup"><span data-stu-id="4c459-145">Step 6.</span></span> <span data-ttu-id="4c459-146">Убедитесь, что подсети hello точно соответствуют (шлюзы Azure на основе политики)</span><span class="sxs-lookup"><span data-stu-id="4c459-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="4c459-147">Проверьте соответствие подсети hello точно между hello виртуальной сети Azure и локальной определения для hello виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="4c459-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="4c459-148">Проверьте соответствие подсети hello точно между hello **шлюза локальной сети** и локальными определения для hello в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="4c459-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="4c459-149">Шаг 7.</span><span class="sxs-lookup"><span data-stu-id="4c459-149">Step 7.</span></span> <span data-ttu-id="4c459-150">Проверьте проверки работоспособности hello шлюз Azure</span><span class="sxs-lookup"><span data-stu-id="4c459-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="4c459-151">Go toohello [проверки работоспособности](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="4c459-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="4c459-152">Пролистайте hello предупреждение сертификата.</span><span class="sxs-lookup"><span data-stu-id="4c459-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="4c459-153">Если ответ получен, считается исправной hello VPN-шлюз.</span><span class="sxs-lookup"><span data-stu-id="4c459-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="4c459-154">Если ответ не получен, hello шлюза не может быть работоспособное или NSG из подсети шлюза hello является причиной hello.</span><span class="sxs-lookup"><span data-stu-id="4c459-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="4c459-155">После текста Hello приведен образец ответа:</span><span class="sxs-lookup"><span data-stu-id="4c459-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="4c459-156">&lt;?xml version="1.0"?> <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Основной экземпляр: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span><span class="sxs-lookup"><span data-stu-id="4c459-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="4c459-157">Шаг 8.</span><span class="sxs-lookup"><span data-stu-id="4c459-157">Step 8.</span></span> <span data-ttu-id="4c459-158">Проверьте ли hello из локального VPN-устройства включена hello безопасной пересылки</span><span class="sxs-lookup"><span data-stu-id="4c459-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="4c459-159">функция безопасной пересылки Hello может вызвать проблемы разрыва соединения.</span><span class="sxs-lookup"><span data-stu-id="4c459-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="4c459-160">Если VPN-устройства hello безопасной пересылки включен, отключите функцию hello.</span><span class="sxs-lookup"><span data-stu-id="4c459-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="4c459-161">Затем обновите политику IPsec шлюза VPN hello.</span><span class="sxs-lookup"><span data-stu-id="4c459-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c459-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c459-162">Next steps</span></span>

-   [<span data-ttu-id="4c459-163">Настройка виртуальной сети tooa подключения сеть сеть</span><span class="sxs-lookup"><span data-stu-id="4c459-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="4c459-164">Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"</span><span class="sxs-lookup"><span data-stu-id="4c459-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
