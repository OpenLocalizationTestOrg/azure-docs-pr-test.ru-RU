---
title: "Устранение проблемы подключения VPN типа \"сеть — сеть\" Azure | Документация Майкрософт"
description: "Узнайте, как устранить проблемы подключения VPN типа \"сеть — сеть\", которое внезапно завершается сбоем и его невозможно восстановить."
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
ms.openlocfilehash: e7a3da64895f0307e5d6c3563672205a2f93a7d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="da8ea-103">Устранение проблемы подключения VPN типа "сеть — сеть" Azure</span><span class="sxs-lookup"><span data-stu-id="da8ea-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="da8ea-104">После настройки подключения VPN типа "сеть — сеть" между локальной сетью и виртуальной сетью Azure VPN-подключение внезапно завершается сбоем и его невозможно восстановить.</span><span class="sxs-lookup"><span data-stu-id="da8ea-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, the VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="da8ea-105">В этой статье приведены действия по устранению этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="da8ea-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="da8ea-106">Действия по устранению неполадок</span><span class="sxs-lookup"><span data-stu-id="da8ea-106">Troubleshooting steps</span></span>

<span data-ttu-id="da8ea-107">Чтобы устранить эту проблему, попробуйте сначала [сбросить VPN-шлюз Azure](vpn-gateway-resetgw-classic.md), а также сбросить туннель в локальном VPN-устройстве.</span><span class="sxs-lookup"><span data-stu-id="da8ea-107">To resolve the problem, first try to [reset the Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset the tunnel from the on-premises VPN device.</span></span> <span data-ttu-id="da8ea-108">Если проблему устранить не удалось, выполните действия ниже, чтобы определить причину проблемы.</span><span class="sxs-lookup"><span data-stu-id="da8ea-108">If the problem persists, follow these steps to identify the cause of the problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="da8ea-109">Предварительные действия</span><span class="sxs-lookup"><span data-stu-id="da8ea-109">Prerequisite step</span></span>

<span data-ttu-id="da8ea-110">Проверьте тип VPN-шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="da8ea-110">Check the type of the Azure VPN gateway.</span></span>

1. <span data-ttu-id="da8ea-111">Перейдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="da8ea-111">Go to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="da8ea-112">Просмотрите тип шлюза на странице **обзора** VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="da8ea-112">Check the **Overview** page of the VPN gateway for the type information.</span></span>
    
    ![Обзор шлюза](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="da8ea-114">Шаг 1.</span><span class="sxs-lookup"><span data-stu-id="da8ea-114">Step 1.</span></span> <span data-ttu-id="da8ea-115">Проверка того, проверено ли локальное устройство VPN</span><span class="sxs-lookup"><span data-stu-id="da8ea-115">Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="da8ea-116">Узнайте, используете ли вы [проверенную версию VPN-устройства и операционной системы](vpn-gateway-about-vpn-devices.md#devicetable).</span><span class="sxs-lookup"><span data-stu-id="da8ea-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="da8ea-117">Если устройство является непроверенным VPN-устройством, может потребоваться обратиться к изготовителю устройства, чтобы узнать о возможных проблемах совместимости.</span><span class="sxs-lookup"><span data-stu-id="da8ea-117">If the device is not a validated VPN device, you might have to contact the device manufacturer to see if there is a compatibility issue.</span></span>

2. <span data-ttu-id="da8ea-118">Убедитесь, что VPN-устройство настроено правильно.</span><span class="sxs-lookup"><span data-stu-id="da8ea-118">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="da8ea-119">Дополнительные сведения см. на странице об [изменении примеров конфигурации устройств](/vpn-gateway-about-vpn-devices.md#editing).</span><span class="sxs-lookup"><span data-stu-id="da8ea-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-the-shared-key"></a><span data-ttu-id="da8ea-120">Шаг 2.</span><span class="sxs-lookup"><span data-stu-id="da8ea-120">Step 2.</span></span> <span data-ttu-id="da8ea-121">Проверка общего ключа</span><span class="sxs-lookup"><span data-stu-id="da8ea-121">Verify the shared key</span></span>

<span data-ttu-id="da8ea-122">Сравните общий ключ от локального VPN-устройства и VPN виртуальной сети Azure, чтобы убедиться, что они совпадают.</span><span class="sxs-lookup"><span data-stu-id="da8ea-122">Compare the shared key for the on-premises VPN device to the Azure Virtual Network VPN to make sure that the keys match.</span></span> 

<span data-ttu-id="da8ea-123">Чтобы просмотреть общий ключ для подключения VPN Azure, используйте один из методов ниже.</span><span class="sxs-lookup"><span data-stu-id="da8ea-123">To view the shared key for the Azure VPN connection, use one of the following methods:</span></span>

<span data-ttu-id="da8ea-124">**Портал Azure**</span><span class="sxs-lookup"><span data-stu-id="da8ea-124">**Azure portal**</span></span>

1. <span data-ttu-id="da8ea-125">Перейдите к созданному вами подключению типа "сеть — сеть" через VPN-шлюз Azure.</span><span class="sxs-lookup"><span data-stu-id="da8ea-125">Go to the VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="da8ea-126">В разделе **Параметры** щелкните **Общий ключ**.</span><span class="sxs-lookup"><span data-stu-id="da8ea-126">In the **Settings** section, click **Shared key**.</span></span>
    
    ![Общий ключ](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="da8ea-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="da8ea-128">**Azure PowerShell**</span></span>

<span data-ttu-id="da8ea-129">Для модели развертывания с помощью Azure Resource Manager выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="da8ea-129">For the Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="da8ea-130">Выполните следующую команду для классической модели развертывания:</span><span class="sxs-lookup"><span data-stu-id="da8ea-130">For the classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-the-vpn-peer-ips"></a><span data-ttu-id="da8ea-131">Шаг 3.</span><span class="sxs-lookup"><span data-stu-id="da8ea-131">Step 3.</span></span> <span data-ttu-id="da8ea-132">Проверка IP-адресов VPN-узла</span><span class="sxs-lookup"><span data-stu-id="da8ea-132">Verify the VPN peer IPs</span></span>

-   <span data-ttu-id="da8ea-133">Определение IP-адреса в объекте **шлюза локальной сети** в Azure должно совпадать с IP-адресом локального устройства.</span><span class="sxs-lookup"><span data-stu-id="da8ea-133">The IP definition in the **Local Network Gateway** object in Azure should match the on-premises device IP.</span></span>
-   <span data-ttu-id="da8ea-134">Определение IP-адреса шлюза Azure, установленное в локальном устройстве, должно совпадать с IP-адресом шлюза Azure.</span><span class="sxs-lookup"><span data-stu-id="da8ea-134">The Azure gateway IP definition that is set on the on-premises device should match the Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-the-gateway-subnet"></a><span data-ttu-id="da8ea-135">Шаг 4.</span><span class="sxs-lookup"><span data-stu-id="da8ea-135">Step 4.</span></span> <span data-ttu-id="da8ea-136">Проверка определяемого пользователем маршрута и групп безопасности сети в подсети шлюза</span><span class="sxs-lookup"><span data-stu-id="da8ea-136">Check UDR and NSGs on the gateway subnet</span></span>

<span data-ttu-id="da8ea-137">Проверьте, есть ли в подсети шлюза определяемые пользователем маршруты (UDR) или группы безопасности сети (NSG) и удалите их, если они имеются. Затем проверьте, успешно ли выполнена операция удаления.</span><span class="sxs-lookup"><span data-stu-id="da8ea-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on the gateway subnet, and then test the result.</span></span> <span data-ttu-id="da8ea-138">Если проблему удалось устранить, проверьте, соответствующим ли образом настроены параметры для NSG и UDR.</span><span class="sxs-lookup"><span data-stu-id="da8ea-138">If the problem is resolved, validate the settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-the-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="da8ea-139">Шаг 5.</span><span class="sxs-lookup"><span data-stu-id="da8ea-139">Step 5.</span></span> <span data-ttu-id="da8ea-140">Проверка внешнего адреса интерфейса для локального VPN-устройства</span><span class="sxs-lookup"><span data-stu-id="da8ea-140">Check the on-premises VPN device external interface address</span></span>

- <span data-ttu-id="da8ea-141">Если IP-адрес для Интернета VPN-устройства включен в определение **локальной сети** в Azure, вы можете столкнуться с нерегулярными отключениями.</span><span class="sxs-lookup"><span data-stu-id="da8ea-141">If the Internet-facing IP address of the VPN device is included in the **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="da8ea-142">К внешнему интерфейсу устройства должен быть прямой доступ через Интернет.</span><span class="sxs-lookup"><span data-stu-id="da8ea-142">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="da8ea-143">Между Интернетом и устройством не должно использоваться преобразование адресов сети или брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="da8ea-143">There should be no network address translation or firewall between the Internet and the device.</span></span>
- <span data-ttu-id="da8ea-144">Чтобы настроить виртуальный IP-адрес для кластеризации брандмауэра, вы должны отключить кластер и предоставить устройство VPN непосредственно общедоступному интерфейсу, с которым может взаимодействовать шлюз.</span><span class="sxs-lookup"><span data-stu-id="da8ea-144">To configure firewall clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-6-verify-that-the-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="da8ea-145">Шаг 6.</span><span class="sxs-lookup"><span data-stu-id="da8ea-145">Step 6.</span></span> <span data-ttu-id="da8ea-146">Проверка полного соответствия подсетей (шлюзов на основе политик Azure)</span><span class="sxs-lookup"><span data-stu-id="da8ea-146">Verify that the subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="da8ea-147">Для виртуальной сети Azure подсети между виртуальной сетью Azure и локальными определениями должны полностью совпадать.</span><span class="sxs-lookup"><span data-stu-id="da8ea-147">Verify that the subnets match exactly between the Azure virtual network and on-premises definitions for the Azure virtual network.</span></span>
-   <span data-ttu-id="da8ea-148">Подсети между **шлюзом локальной сети** и локальными определениями должны полностью совпадать для локальной сети.</span><span class="sxs-lookup"><span data-stu-id="da8ea-148">Verify that the subnets match exactly between the **Local Network Gateway** and on-premises definitions for the on-premises network.</span></span>

### <a name="step-7-verify-the-azure-gateway-health-probe"></a><span data-ttu-id="da8ea-149">Шаг 7.</span><span class="sxs-lookup"><span data-stu-id="da8ea-149">Step 7.</span></span> <span data-ttu-id="da8ea-150">Проверка работоспособности шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="da8ea-150">Verify the Azure gateway health probe</span></span>

1. <span data-ttu-id="da8ea-151">Перейдите к [пробе работоспособности](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span><span class="sxs-lookup"><span data-stu-id="da8ea-151">Go to the [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="da8ea-152">Просмотрите предупреждение о сертификате.</span><span class="sxs-lookup"><span data-stu-id="da8ea-152">Click through the certificate warning.</span></span>
3. <span data-ttu-id="da8ea-153">Если вы получите ответ, шлюз VPN считается работоспособным.</span><span class="sxs-lookup"><span data-stu-id="da8ea-153">If you receive a response, the VPN gateway is considered healthy.</span></span> <span data-ttu-id="da8ea-154">Если вы не получите ответ, шлюз может быть неработоспособным, или проблема может быть вызвана наличием группы безопасности сети (NSG) в подсети шлюза.</span><span class="sxs-lookup"><span data-stu-id="da8ea-154">If you don't receive a response, the gateway might not be healthy or an NSG on the gateway subnet is causing the problem.</span></span> <span data-ttu-id="da8ea-155">Пример ответа приведен ниже:</span><span class="sxs-lookup"><span data-stu-id="da8ea-155">The following text is a sample response:</span></span>

    <span data-ttu-id="da8ea-156">&lt;?xml version="1.0"?> <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Основной экземпляр: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span><span class="sxs-lookup"><span data-stu-id="da8ea-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-the-on-premises-vpn-device-has-the-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="da8ea-157">Шаг 8.</span><span class="sxs-lookup"><span data-stu-id="da8ea-157">Step 8.</span></span> <span data-ttu-id="da8ea-158">Проверка, включена ли для локального VPN-устройства функция полной безопасности пересылки</span><span class="sxs-lookup"><span data-stu-id="da8ea-158">Check whether the on-premises VPN device has the perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="da8ea-159">Функция полной безопасности пересылки может вызвать проблемы отключения.</span><span class="sxs-lookup"><span data-stu-id="da8ea-159">The perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="da8ea-160">Если для VPN-устройства включена функция полной безопасности пересылки, отключите эту функцию.</span><span class="sxs-lookup"><span data-stu-id="da8ea-160">If the VPN device has perfect forward secrecy enabled, disable the feature.</span></span> <span data-ttu-id="da8ea-161">Затем обновите политику IPsec VPN-шлюза.</span><span class="sxs-lookup"><span data-stu-id="da8ea-161">Then update the VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da8ea-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="da8ea-162">Next steps</span></span>

-   [<span data-ttu-id="da8ea-163">Создание подключения типа "сеть — сеть" на портале Azure</span><span class="sxs-lookup"><span data-stu-id="da8ea-163">Configure a site-to-site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="da8ea-164">Настройка политики IPsec/IKE для VPN-подключений типа "сеть — сеть" или "виртуальная сеть — виртуальная сеть"</span><span class="sxs-lookup"><span data-stu-id="da8ea-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
