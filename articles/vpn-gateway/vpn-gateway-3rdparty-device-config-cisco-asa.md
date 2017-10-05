---
title: "Пример конфигурации. Подключение устройства Cisco ASA к VPN-шлюзам Azure | Документация Майкрософт"
description: "В этой статье приведен пример конфигурации для подключения устройства Cisco ASA к VPN-шлюзам Azure."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 10466b8928e2cd687f7961a2956b6d60823b82be
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="66a0d-103">Пример конфигурации. Устройство Cisco ASA (IKEv2/без BGP)</span><span class="sxs-lookup"><span data-stu-id="66a0d-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="66a0d-104">В этой статье приведен пример конфигурации для подключения устройств Cisco ASA к VPN-шлюзам Azure.</span><span class="sxs-lookup"><span data-stu-id="66a0d-104">This article provides sample configurations for Cisco ASA devices connecting to Azure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="66a0d-105">Краткий обзор устройства</span><span class="sxs-lookup"><span data-stu-id="66a0d-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="66a0d-106">Поставщик устройства</span><span class="sxs-lookup"><span data-stu-id="66a0d-106">Device vendor</span></span>          | <span data-ttu-id="66a0d-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="66a0d-107">Cisco</span></span>                             |
| <span data-ttu-id="66a0d-108">Модель устройства</span><span class="sxs-lookup"><span data-stu-id="66a0d-108">Device model</span></span>           | <span data-ttu-id="66a0d-109">ASA (устройство адаптивной безопасности)</span><span class="sxs-lookup"><span data-stu-id="66a0d-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="66a0d-110">Целевая версия</span><span class="sxs-lookup"><span data-stu-id="66a0d-110">Target version</span></span>         | <span data-ttu-id="66a0d-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="66a0d-111">8.4+</span></span>                              |
| <span data-ttu-id="66a0d-112">Проверенная модель</span><span class="sxs-lookup"><span data-stu-id="66a0d-112">Tested model</span></span>           | <span data-ttu-id="66a0d-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="66a0d-113">ASA 5505</span></span>                          |
| <span data-ttu-id="66a0d-114">Проверенные версии</span><span class="sxs-lookup"><span data-stu-id="66a0d-114">Tested version</span></span>         | <span data-ttu-id="66a0d-115">9.2</span><span class="sxs-lookup"><span data-stu-id="66a0d-115">9.2</span></span>                               |
| <span data-ttu-id="66a0d-116">Версия IKE</span><span class="sxs-lookup"><span data-stu-id="66a0d-116">IKE version</span></span>            | <span data-ttu-id="66a0d-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="66a0d-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="66a0d-118">BGP</span><span class="sxs-lookup"><span data-stu-id="66a0d-118">BGP</span></span>                    | <span data-ttu-id="66a0d-119">**Нет**</span><span class="sxs-lookup"><span data-stu-id="66a0d-119">**No**</span></span>                            |
| <span data-ttu-id="66a0d-120">Тип VPN-шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="66a0d-120">Azure VPN gateway type</span></span> | <span data-ttu-id="66a0d-121">Пример VPN-шлюза **на основе маршрута**</span><span class="sxs-lookup"><span data-stu-id="66a0d-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="66a0d-122">В примере конфигурации ниже устройство Cisco ASA подключается к VPN-шлюзу Azure **на основе маршрута**, используя пользовательскую политику IPsec/IKE с параметром UserPolicyBasedTrafficSelectors, как описано в [этой статье](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="66a0d-122">The configuration below connects a Cisco ASA device to an Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="66a0d-123">Для этого требуется, чтобы устройства ASA использовали **IKEv2** с конфигурацией на основе списка доступа, а не на основе VTI.</span><span class="sxs-lookup"><span data-stu-id="66a0d-123">It requires ASA devices to use **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="66a0d-124">Мы рекомендуем ознакомиться со спецификациями поставщиков устройств VPN, чтобы убедиться, что политика поддерживается локальными устройствами VPN.</span><span class="sxs-lookup"><span data-stu-id="66a0d-124">Please consult with your VPN device vendor specifications to ensure the policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="66a0d-125">Требования к VPN-устройствам</span><span class="sxs-lookup"><span data-stu-id="66a0d-125">VPN device requirements</span></span>
<span data-ttu-id="66a0d-126">В VPN-шлюзах Azure используются стандартные наборы протоколов IPsec/IKE для установки VPN-туннелей S2S.</span><span class="sxs-lookup"><span data-stu-id="66a0d-126">Azure VPN gateways use standard IPsec/IKE protocol suites to establish S2S VPN tunnels.</span></span> <span data-ttu-id="66a0d-127">Подробные параметры протокола IPsec/IKE и алгоритмы шифрования по умолчанию для VPN-шлюзов Azure см. в статье [VPN-устройства и параметры IPsec/IKE для подключений типа "сеть — сеть" через VPN-шлюз](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="66a0d-127">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="66a0d-128">Дополнительно можно указать точную комбинацию алгоритмов шифрования и уровней стойкости ключа для определенного подключения, как описано в статье [Требования к шифрованию и VPN-шлюзы Azure](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="66a0d-128">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="66a0d-129">В случае выбора конкретного сочетания алгоритмов шифрования и уровней стойкости ключей, убедитесь, что используется соответствующая спецификация на VPN-устройствах.</span><span class="sxs-lookup"><span data-stu-id="66a0d-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use the corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="66a0d-130">Одиночный VPN-туннель</span><span class="sxs-lookup"><span data-stu-id="66a0d-130">Single VPN tunnel</span></span>
<span data-ttu-id="66a0d-131">Эта топология состоит из одного VPN-туннеля S2S между VPN-шлюзом Azure и локальным устройством VPN.</span><span class="sxs-lookup"><span data-stu-id="66a0d-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="66a0d-132">При необходимости можно также настроить BGP поверх VPN-туннеля.</span><span class="sxs-lookup"><span data-stu-id="66a0d-132">You can optionally configure BGP across the VPN tunnel.</span></span>

![одиночный туннель](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="66a0d-134">Детальные пошаговые инструкции для создания конфигурации Azure см. в разделе [Одиночный VPN-туннель](vpn-gateway-3rdparty-device-config-overview.md#singletunnel).</span><span class="sxs-lookup"><span data-stu-id="66a0d-134">Refer to [Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions to build the Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="66a0d-135">Сведения о сети и VPN-шлюзе</span><span class="sxs-lookup"><span data-stu-id="66a0d-135">Network and VPN gateway information</span></span>
<span data-ttu-id="66a0d-136">В этом разделе перечислены параметры для этого примера.</span><span class="sxs-lookup"><span data-stu-id="66a0d-136">This section list the parameters for the this sample.</span></span>

| <span data-ttu-id="66a0d-137">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="66a0d-137">**Parameter**</span></span>                | <span data-ttu-id="66a0d-138">**Значение**</span><span class="sxs-lookup"><span data-stu-id="66a0d-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="66a0d-139">Префиксы адресов виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="66a0d-139">VNet address prefixes</span></span>        | <span data-ttu-id="66a0d-140">10.11.0.0/16;</span><span class="sxs-lookup"><span data-stu-id="66a0d-140">10.11.0.0/16</span></span><br><span data-ttu-id="66a0d-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="66a0d-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="66a0d-142">IP-адрес VPN-шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="66a0d-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="66a0d-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="66a0d-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="66a0d-144">Префиксы адресов в локальной среде</span><span class="sxs-lookup"><span data-stu-id="66a0d-144">On-premises address prefixes</span></span> | <span data-ttu-id="66a0d-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="66a0d-145">10.51.0.0/16</span></span><br><span data-ttu-id="66a0d-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="66a0d-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="66a0d-147">IP-адрес VPN-устройства в локальной среде</span><span class="sxs-lookup"><span data-stu-id="66a0d-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="66a0d-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="66a0d-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="66a0d-149">*ASN для BGP виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="66a0d-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="66a0d-150">65010</span><span class="sxs-lookup"><span data-stu-id="66a0d-150">65010</span></span>                        |
| <span data-ttu-id="66a0d-151">*IP-адрес узла BGP Azure</span><span class="sxs-lookup"><span data-stu-id="66a0d-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="66a0d-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="66a0d-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="66a0d-153">*ASN BGP в локальной среде</span><span class="sxs-lookup"><span data-stu-id="66a0d-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="66a0d-154">65050</span><span class="sxs-lookup"><span data-stu-id="66a0d-154">65050</span></span>                        |
| <span data-ttu-id="66a0d-155">*IP-адрес узла BGP в локальной среде</span><span class="sxs-lookup"><span data-stu-id="66a0d-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="66a0d-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="66a0d-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="66a0d-157">(*) Необязательные параметры только для BGP.</span><span class="sxs-lookup"><span data-stu-id="66a0d-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="66a0d-158">Политика и параметры IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="66a0d-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="66a0d-159">Указанная ниже таблица содержит список алгоритмов и параметров IPsec/IKE, используемых в этом примере.</span><span class="sxs-lookup"><span data-stu-id="66a0d-159">The table below lists the IPsec/IKE algorithms and parameters used in the sample.</span></span> <span data-ttu-id="66a0d-160">Проверьте спецификацию VPN-устройства, чтобы убедиться, что все перечисленные выше алгоритмы поддерживаются моделями VPN-устройства и версиями встроенного ПО.</span><span class="sxs-lookup"><span data-stu-id="66a0d-160">Please consult your VPN device specifications to make sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="66a0d-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="66a0d-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="66a0d-162">**Значение**</span><span class="sxs-lookup"><span data-stu-id="66a0d-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="66a0d-163">Шифрование IKEv2</span><span class="sxs-lookup"><span data-stu-id="66a0d-163">IKEv2 Encryption</span></span> | <span data-ttu-id="66a0d-164">AES256</span><span class="sxs-lookup"><span data-stu-id="66a0d-164">AES256</span></span>                               |
| <span data-ttu-id="66a0d-165">Проверка целостности IKEv2</span><span class="sxs-lookup"><span data-stu-id="66a0d-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="66a0d-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="66a0d-166">SHA384</span></span>                               |
| <span data-ttu-id="66a0d-167">Группа DH</span><span class="sxs-lookup"><span data-stu-id="66a0d-167">DH Group</span></span>         | <span data-ttu-id="66a0d-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="66a0d-168">DHGroup24</span></span>                            |
| <span data-ttu-id="66a0d-169">Шифрование IPsec</span><span class="sxs-lookup"><span data-stu-id="66a0d-169">IPsec Encryption</span></span> | <span data-ttu-id="66a0d-170">AES256</span><span class="sxs-lookup"><span data-stu-id="66a0d-170">AES256</span></span>                               |
| <span data-ttu-id="66a0d-171">Целостность IPsec</span><span class="sxs-lookup"><span data-stu-id="66a0d-171">IPsec Integrity</span></span>  | <span data-ttu-id="66a0d-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="66a0d-172">SHA1</span></span>                                 |
| <span data-ttu-id="66a0d-173">Группа PFS</span><span class="sxs-lookup"><span data-stu-id="66a0d-173">PFS Group</span></span>        | <span data-ttu-id="66a0d-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="66a0d-174">PFS24</span></span>                                |
| <span data-ttu-id="66a0d-175">Время существования QM SA</span><span class="sxs-lookup"><span data-stu-id="66a0d-175">QM SA Lifetime</span></span>   | <span data-ttu-id="66a0d-176">7200 секунд</span><span class="sxs-lookup"><span data-stu-id="66a0d-176">7200 seconds</span></span>                         |
| <span data-ttu-id="66a0d-177">Селектор трафика</span><span class="sxs-lookup"><span data-stu-id="66a0d-177">Traffic Selector</span></span> | <span data-ttu-id="66a0d-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="66a0d-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="66a0d-179">Общий ключ</span><span class="sxs-lookup"><span data-stu-id="66a0d-179">Pre-Shared Key</span></span>   | <span data-ttu-id="66a0d-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="66a0d-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="66a0d-181">(*) Если GCM-AES используется как алгоритм шифрования IPsec, целостность IPsec на некоторых устройствах должна быть равна NULL.</span><span class="sxs-lookup"><span data-stu-id="66a0d-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="66a0d-182">Заметки об устройстве</span><span class="sxs-lookup"><span data-stu-id="66a0d-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="66a0d-183">Для поддержки IKEv2 необходима ASA версии 8.4 и выше.</span><span class="sxs-lookup"><span data-stu-id="66a0d-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="66a0d-184">Установите ASA версии 9.x для более высокого уровня поддержки групп DH и PFS (за пределами группы 5).</span><span class="sxs-lookup"><span data-stu-id="66a0d-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="66a0d-185">Для шифрования IPsec с целостностью AES-GCM и IPsec с поддержкой SHA-256, SHA-384, SHA-512 необходимо устройство ASA версии 9.x на новом оборудовании ASA. ASA 5505, 5510, 5520, 5540, 5550 и 5580 **не** поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="66a0d-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="66a0d-186">(Для подтверждения проверьте спецификацию поставщика.)</span><span class="sxs-lookup"><span data-stu-id="66a0d-186">(Please check the vendor specifications to confirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="66a0d-187">Примеры конфигурации устройств</span><span class="sxs-lookup"><span data-stu-id="66a0d-187">Sample device configurations</span></span>
<span data-ttu-id="66a0d-188">Приведенный ниже скрипт предоставляет пример конфигурации на основе топологии и параметров выше.</span><span class="sxs-lookup"><span data-stu-id="66a0d-188">The script below provides a sample configuration based on the topology and parameters listed above.</span></span> <span data-ttu-id="66a0d-189">Конфигурация туннеля VPN типа "сеть — сеть" состоит из следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="66a0d-189">The S2S VPN tunnel configuration consists of the following parts:</span></span>

1. <span data-ttu-id="66a0d-190">Интерфейсы и маршруты.</span><span class="sxs-lookup"><span data-stu-id="66a0d-190">Interfaces & routes</span></span>
2. <span data-ttu-id="66a0d-191">Списки доступа.</span><span class="sxs-lookup"><span data-stu-id="66a0d-191">Access lists</span></span>
3. <span data-ttu-id="66a0d-192">Политика и параметры IKE (фаза 1 или основной режим).</span><span class="sxs-lookup"><span data-stu-id="66a0d-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="66a0d-193">Политика и параметры IKE (фаза 2 или быстрый режим).</span><span class="sxs-lookup"><span data-stu-id="66a0d-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="66a0d-194">Другие параметры (фиксация TCP MSS и т. д.).</span><span class="sxs-lookup"><span data-stu-id="66a0d-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="66a0d-195">Выполните дополнительную указанную ниже конфигурацию и замените заполнители фактическими значениями.</span><span class="sxs-lookup"><span data-stu-id="66a0d-195">Please make sure you complete the additional configuration listed below and replace the placeholders with the actual values:</span></span>
> 
> - <span data-ttu-id="66a0d-196">Конфигурация для внутренних и внешних интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="66a0d-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="66a0d-197">Маршруты для внутренних (частных), внешних (общедоступных) сетей.</span><span class="sxs-lookup"><span data-stu-id="66a0d-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="66a0d-198">Обеспечьте уникальность имен и номеров политики устройства.</span><span class="sxs-lookup"><span data-stu-id="66a0d-198">Ensure all names and policy numbers are unique on the device</span></span>
> - <span data-ttu-id="66a0d-199">Убедитесь, что на устройстве поддерживаются алгоритмы шифрования.</span><span class="sxs-lookup"><span data-stu-id="66a0d-199">Ensure the cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="66a0d-200">Замените следующие заполнители фактическими значениями:</span><span class="sxs-lookup"><span data-stu-id="66a0d-200">Replace the following place holders with the actual values</span></span>
>   - <span data-ttu-id="66a0d-201">Имя внешнего интерфейса: outside;</span><span class="sxs-lookup"><span data-stu-id="66a0d-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="66a0d-202">Azure_Gateway_Public_IP;</span><span class="sxs-lookup"><span data-stu-id="66a0d-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="66a0d-203">OnPrem_Device_Public_IP;</span><span class="sxs-lookup"><span data-stu-id="66a0d-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="66a0d-204">IKE Pre_Shared_Key;</span><span class="sxs-lookup"><span data-stu-id="66a0d-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="66a0d-205">Имена виртуальной сети и шлюза локальной сети (VNetName, LNGName).</span><span class="sxs-lookup"><span data-stu-id="66a0d-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="66a0d-206">Префиксы адресов виртуальной сети и локальной сети.</span><span class="sxs-lookup"><span data-stu-id="66a0d-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="66a0d-207">Правильные маски сети.</span><span class="sxs-lookup"><span data-stu-id="66a0d-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="66a0d-208">Пример конфигурации</span><span class="sxs-lookup"><span data-stu-id="66a0d-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting to Azure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace the following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - the Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with the actual nexthop IP address
!
! (*) Must be unique names in the device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on the outside interface or vlan
!     > <PrivateIPAddress> on the inside interface or vlan; e.g., 10.51.0.1/24
!     > Route to connect to <Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between the ASA and the Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding to the <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines the on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify the access-list between the Azure VNet and your on-premises network.
!       This access list defines the IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between the on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure the policy number is not used
!       - integrity and prf must be the same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as the crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned to your outside interface, you must use
!         the same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses the access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses the proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS to 1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="66a0d-209">Простые команды отладки</span><span class="sxs-lookup"><span data-stu-id="66a0d-209">Simple debugging commands</span></span>

<span data-ttu-id="66a0d-210">Ниже приведены некоторые команды ASA для отладки.</span><span class="sxs-lookup"><span data-stu-id="66a0d-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="66a0d-211">Отображение сопоставления безопасности IPsec и IKE.</span><span class="sxs-lookup"><span data-stu-id="66a0d-211">Show the IPsec and IKE SA's</span></span>
    - <span data-ttu-id="66a0d-212">show crypto ipsec sa;</span><span class="sxs-lookup"><span data-stu-id="66a0d-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="66a0d-213">show crypto ikev2 sa.</span><span class="sxs-lookup"><span data-stu-id="66a0d-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="66a0d-214">Ввод режима отладки. Это может привести к искаженной работе консоли.</span><span class="sxs-lookup"><span data-stu-id="66a0d-214">Entering debug mode - this can get very noisy on the console</span></span>
    - <span data-ttu-id="66a0d-215">debug crypto ikev2 platform <level>;</span><span class="sxs-lookup"><span data-stu-id="66a0d-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="66a0d-216">debug crypto ikev2 protocol <level>.</span><span class="sxs-lookup"><span data-stu-id="66a0d-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="66a0d-217">Вывод текущих конфигураций.</span><span class="sxs-lookup"><span data-stu-id="66a0d-217">List current configurations</span></span>
    - <span data-ttu-id="66a0d-218">show run — отображает текущие конфигурации на устройстве. Вы можете использовать различные вложенные команды, чтобы отобразить конкретные части конфигурации.</span><span class="sxs-lookup"><span data-stu-id="66a0d-218">"show run" - shows the current configurations on the device; you can use the various sub-commands to list specific parts of the configuration.</span></span> <span data-ttu-id="66a0d-219">Например, show run crypto, show run access-list, show run tunnel-group и т. д.</span><span class="sxs-lookup"><span data-stu-id="66a0d-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="66a0d-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="66a0d-220">Next steps</span></span>
<span data-ttu-id="66a0d-221">Инструкции по настройке распределенных подключений (локальных и между виртуальными сетями) с конфигурацией "активный — активный" см. в статье [Настройка VPN-подключений типа "сеть — сеть" в режиме "активный — активный" для VPN-шлюзов Azure с помощью Azure Resource Manager и PowerShell](vpn-gateway-activeactive-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="66a0d-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

