---
title: "Конфигурация aaaSample - устройств Cisco ASA подключение VPN-шлюзов tooAzure | Документы Microsoft"
description: "Эта статья содержит пример конфигурации для устройств Cisco ASA подключение tooAzure VPN-шлюзов."
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
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="b9e03-103">Пример конфигурации. Устройство Cisco ASA (IKEv2/без BGP)</span><span class="sxs-lookup"><span data-stu-id="b9e03-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="b9e03-104">Эта статья содержит пример конфигурации для устройств Cisco ASA подключение tooAzure VPN-шлюзов.</span><span class="sxs-lookup"><span data-stu-id="b9e03-104">This article provides sample configurations for Cisco ASA devices connecting tooAzure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="b9e03-105">Краткий обзор устройства</span><span class="sxs-lookup"><span data-stu-id="b9e03-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="b9e03-106">Поставщик устройства</span><span class="sxs-lookup"><span data-stu-id="b9e03-106">Device vendor</span></span>          | <span data-ttu-id="b9e03-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="b9e03-107">Cisco</span></span>                             |
| <span data-ttu-id="b9e03-108">Модель устройства</span><span class="sxs-lookup"><span data-stu-id="b9e03-108">Device model</span></span>           | <span data-ttu-id="b9e03-109">ASA (устройство адаптивной безопасности)</span><span class="sxs-lookup"><span data-stu-id="b9e03-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="b9e03-110">Целевая версия</span><span class="sxs-lookup"><span data-stu-id="b9e03-110">Target version</span></span>         | <span data-ttu-id="b9e03-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="b9e03-111">8.4+</span></span>                              |
| <span data-ttu-id="b9e03-112">Проверенная модель</span><span class="sxs-lookup"><span data-stu-id="b9e03-112">Tested model</span></span>           | <span data-ttu-id="b9e03-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="b9e03-113">ASA 5505</span></span>                          |
| <span data-ttu-id="b9e03-114">Проверенные версии</span><span class="sxs-lookup"><span data-stu-id="b9e03-114">Tested version</span></span>         | <span data-ttu-id="b9e03-115">9.2</span><span class="sxs-lookup"><span data-stu-id="b9e03-115">9.2</span></span>                               |
| <span data-ttu-id="b9e03-116">Версия IKE</span><span class="sxs-lookup"><span data-stu-id="b9e03-116">IKE version</span></span>            | <span data-ttu-id="b9e03-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="b9e03-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="b9e03-118">BGP</span><span class="sxs-lookup"><span data-stu-id="b9e03-118">BGP</span></span>                    | <span data-ttu-id="b9e03-119">**Нет**</span><span class="sxs-lookup"><span data-stu-id="b9e03-119">**No**</span></span>                            |
| <span data-ttu-id="b9e03-120">Тип VPN-шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="b9e03-120">Azure VPN gateway type</span></span> | <span data-ttu-id="b9e03-121">Пример VPN-шлюза **на основе маршрута**</span><span class="sxs-lookup"><span data-stu-id="b9e03-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="b9e03-122">приведенными ниже параметрами Hello подключается tooan устройств Cisco ASA Azure **на основе маршрутов** шлюза VPN с помощью настраиваемой политики IPsec/IKE с параметром «UserPolicyBasedTrafficSelectors», как описано в [в этой статье](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b9e03-122">hello configuration below connects a Cisco ASA device tooan Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="b9e03-123">Требуется ASA устройств toouse **IKEv2** доступа список на основе конфигурации, не VTI под управлением.</span><span class="sxs-lookup"><span data-stu-id="b9e03-123">It requires ASA devices toouse **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="b9e03-124">Обратитесь к спецификации поставщиков устройств VPN политики tooensure hello поддерживается на устройствах VPN локальной.</span><span class="sxs-lookup"><span data-stu-id="b9e03-124">Please consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="b9e03-125">Требования к VPN-устройствам</span><span class="sxs-lookup"><span data-stu-id="b9e03-125">VPN device requirements</span></span>
<span data-ttu-id="b9e03-126">Azure VPN-шлюзов с помощью стандартных IPsec/IKE туннелей S2S VPN tooestablish протокола наборов.</span><span class="sxs-lookup"><span data-stu-id="b9e03-126">Azure VPN gateways use standard IPsec/IKE protocol suites tooestablish S2S VPN tunnels.</span></span> <span data-ttu-id="b9e03-127">См. слишком[сведения о VPN-устройства](vpn-gateway-about-vpn-devices.md) hello подробную параметров протокола IPsec/IKE и алгоритмов шифрования по умолчанию для VPN-шлюзы Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e03-127">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="b9e03-128">Можно дополнительно указать hello точное сочетание алгоритмов шифрования и значений длины ключа для конкретного подключения, как описано в [о требованиях к шифрования](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="b9e03-128">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="b9e03-129">При выборе конкретного сочетания алгоритмов шифрования и значений длины ключа убедитесь в том, что использовать соответствующие спецификации hello на устройствах VPN.</span><span class="sxs-lookup"><span data-stu-id="b9e03-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use hello corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="b9e03-130">Одиночный VPN-туннель</span><span class="sxs-lookup"><span data-stu-id="b9e03-130">Single VPN tunnel</span></span>
<span data-ttu-id="b9e03-131">Эта топология состоит из одного VPN-туннеля S2S между VPN-шлюзом Azure и локальным устройством VPN.</span><span class="sxs-lookup"><span data-stu-id="b9e03-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="b9e03-132">При необходимости можно настроить BGP через туннель VPN hello.</span><span class="sxs-lookup"><span data-stu-id="b9e03-132">You can optionally configure BGP across hello VPN tunnel.</span></span>

![Одиночный туннель](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="b9e03-134">См. слишком[одного туннеля установки](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) подробные пошаговые инструкции toobuild hello Azure конфигураций.</span><span class="sxs-lookup"><span data-stu-id="b9e03-134">Refer too[Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions toobuild hello Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="b9e03-135">Сведения о сети и VPN-шлюзе</span><span class="sxs-lookup"><span data-stu-id="b9e03-135">Network and VPN gateway information</span></span>
<span data-ttu-id="b9e03-136">В этом разделе перечислены параметры hello hello в этом примере.</span><span class="sxs-lookup"><span data-stu-id="b9e03-136">This section list hello parameters for hello this sample.</span></span>

| <span data-ttu-id="b9e03-137">**Параметр**</span><span class="sxs-lookup"><span data-stu-id="b9e03-137">**Parameter**</span></span>                | <span data-ttu-id="b9e03-138">**Значение**</span><span class="sxs-lookup"><span data-stu-id="b9e03-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="b9e03-139">Префиксы адресов виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b9e03-139">VNet address prefixes</span></span>        | <span data-ttu-id="b9e03-140">10.11.0.0/16;</span><span class="sxs-lookup"><span data-stu-id="b9e03-140">10.11.0.0/16</span></span><br><span data-ttu-id="b9e03-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b9e03-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="b9e03-142">IP-адрес VPN-шлюза Azure</span><span class="sxs-lookup"><span data-stu-id="b9e03-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="b9e03-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="b9e03-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="b9e03-144">Префиксы адресов в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b9e03-144">On-premises address prefixes</span></span> | <span data-ttu-id="b9e03-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b9e03-145">10.51.0.0/16</span></span><br><span data-ttu-id="b9e03-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b9e03-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="b9e03-147">IP-адрес VPN-устройства в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b9e03-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="b9e03-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="b9e03-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="b9e03-149">*ASN для BGP виртуальной сети</span><span class="sxs-lookup"><span data-stu-id="b9e03-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="b9e03-150">65010</span><span class="sxs-lookup"><span data-stu-id="b9e03-150">65010</span></span>                        |
| <span data-ttu-id="b9e03-151">*IP-адрес узла BGP Azure</span><span class="sxs-lookup"><span data-stu-id="b9e03-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="b9e03-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="b9e03-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="b9e03-153">*ASN BGP в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b9e03-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="b9e03-154">65050</span><span class="sxs-lookup"><span data-stu-id="b9e03-154">65050</span></span>                        |
| <span data-ttu-id="b9e03-155">*IP-адрес узла BGP в локальной среде</span><span class="sxs-lookup"><span data-stu-id="b9e03-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="b9e03-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="b9e03-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="b9e03-157">(*) Необязательные параметры только для BGP.</span><span class="sxs-lookup"><span data-stu-id="b9e03-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="b9e03-158">Политика и параметры IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="b9e03-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="b9e03-159">Hello перечислены hello IPsec/IKE алгоритмы и параметры, используемые в образце hello.</span><span class="sxs-lookup"><span data-stu-id="b9e03-159">hello table below lists hello IPsec/IKE algorithms and parameters used in hello sample.</span></span> <span data-ttu-id="b9e03-160">Обратитесь к спецификации VPN устройства, toomake убедиться, что все алгоритмы, перечисленных выше поддерживаются в вашей модели устройств VPN и версии встроенного по.</span><span class="sxs-lookup"><span data-stu-id="b9e03-160">Please consult your VPN device specifications toomake sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="b9e03-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="b9e03-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="b9e03-162">**Значение**</span><span class="sxs-lookup"><span data-stu-id="b9e03-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="b9e03-163">Шифрование IKEv2</span><span class="sxs-lookup"><span data-stu-id="b9e03-163">IKEv2 Encryption</span></span> | <span data-ttu-id="b9e03-164">AES256</span><span class="sxs-lookup"><span data-stu-id="b9e03-164">AES256</span></span>                               |
| <span data-ttu-id="b9e03-165">Проверка целостности IKEv2</span><span class="sxs-lookup"><span data-stu-id="b9e03-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="b9e03-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="b9e03-166">SHA384</span></span>                               |
| <span data-ttu-id="b9e03-167">Группа DH</span><span class="sxs-lookup"><span data-stu-id="b9e03-167">DH Group</span></span>         | <span data-ttu-id="b9e03-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="b9e03-168">DHGroup24</span></span>                            |
| <span data-ttu-id="b9e03-169">Шифрование IPsec</span><span class="sxs-lookup"><span data-stu-id="b9e03-169">IPsec Encryption</span></span> | <span data-ttu-id="b9e03-170">AES256</span><span class="sxs-lookup"><span data-stu-id="b9e03-170">AES256</span></span>                               |
| <span data-ttu-id="b9e03-171">Целостность IPsec</span><span class="sxs-lookup"><span data-stu-id="b9e03-171">IPsec Integrity</span></span>  | <span data-ttu-id="b9e03-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="b9e03-172">SHA1</span></span>                                 |
| <span data-ttu-id="b9e03-173">Группа PFS</span><span class="sxs-lookup"><span data-stu-id="b9e03-173">PFS Group</span></span>        | <span data-ttu-id="b9e03-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="b9e03-174">PFS24</span></span>                                |
| <span data-ttu-id="b9e03-175">Время существования QM SA</span><span class="sxs-lookup"><span data-stu-id="b9e03-175">QM SA Lifetime</span></span>   | <span data-ttu-id="b9e03-176">7200 секунд</span><span class="sxs-lookup"><span data-stu-id="b9e03-176">7200 seconds</span></span>                         |
| <span data-ttu-id="b9e03-177">Селектор трафика</span><span class="sxs-lookup"><span data-stu-id="b9e03-177">Traffic Selector</span></span> | <span data-ttu-id="b9e03-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="b9e03-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="b9e03-179">Общий ключ</span><span class="sxs-lookup"><span data-stu-id="b9e03-179">Pre-Shared Key</span></span>   | <span data-ttu-id="b9e03-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="b9e03-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="b9e03-181">(*) Если GCM-AES используется как алгоритм шифрования IPsec, целостность IPsec на некоторых устройствах должна быть равна NULL.</span><span class="sxs-lookup"><span data-stu-id="b9e03-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="b9e03-182">Заметки об устройстве</span><span class="sxs-lookup"><span data-stu-id="b9e03-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="b9e03-183">Для поддержки IKEv2 необходима ASA версии 8.4 и выше.</span><span class="sxs-lookup"><span data-stu-id="b9e03-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="b9e03-184">Установите ASA версии 9.x для более высокого уровня поддержки групп DH и PFS (за пределами группы 5).</span><span class="sxs-lookup"><span data-stu-id="b9e03-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="b9e03-185">Для шифрования IPsec с целостностью AES-GCM и IPsec с поддержкой SHA-256, SHA-384, SHA-512 необходимо устройство ASA версии 9.x на новом оборудовании ASA. ASA 5505, 5510, 5520, 5540, 5550 и 5580 **не** поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="b9e03-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="b9e03-186">(Проверьте спецификации tooconfirm hello поставщика).</span><span class="sxs-lookup"><span data-stu-id="b9e03-186">(Please check hello vendor specifications tooconfirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="b9e03-187">Примеры конфигурации устройств</span><span class="sxs-lookup"><span data-stu-id="b9e03-187">Sample device configurations</span></span>
<span data-ttu-id="b9e03-188">Приведенный ниже сценарий Hello предоставляет образец конфигурации на основе топологии hello и параметры, приведенные выше.</span><span class="sxs-lookup"><span data-stu-id="b9e03-188">hello script below provides a sample configuration based on hello topology and parameters listed above.</span></span> <span data-ttu-id="b9e03-189">настройка туннеля S2S VPN Hello состоит из следующих частей hello:</span><span class="sxs-lookup"><span data-stu-id="b9e03-189">hello S2S VPN tunnel configuration consists of hello following parts:</span></span>

1. <span data-ttu-id="b9e03-190">Интерфейсы и маршруты.</span><span class="sxs-lookup"><span data-stu-id="b9e03-190">Interfaces & routes</span></span>
2. <span data-ttu-id="b9e03-191">Списки доступа.</span><span class="sxs-lookup"><span data-stu-id="b9e03-191">Access lists</span></span>
3. <span data-ttu-id="b9e03-192">Политика и параметры IKE (фаза 1 или основной режим).</span><span class="sxs-lookup"><span data-stu-id="b9e03-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="b9e03-193">Политика и параметры IKE (фаза 2 или быстрый режим).</span><span class="sxs-lookup"><span data-stu-id="b9e03-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="b9e03-194">Другие параметры (фиксация TCP MSS и т. д.).</span><span class="sxs-lookup"><span data-stu-id="b9e03-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="b9e03-195">Убедитесь, что завершения hello дополнительной настройки, перечисленные ниже и замените заполнители hello hello фактические значения:</span><span class="sxs-lookup"><span data-stu-id="b9e03-195">Please make sure you complete hello additional configuration listed below and replace hello placeholders with hello actual values:</span></span>
> 
> - <span data-ttu-id="b9e03-196">Конфигурация для внутренних и внешних интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="b9e03-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="b9e03-197">Маршруты для внутренних (частных), внешних (общедоступных) сетей.</span><span class="sxs-lookup"><span data-stu-id="b9e03-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="b9e03-198">Убедитесь, все имена и номера политики должны быть уникальными в устройстве hello</span><span class="sxs-lookup"><span data-stu-id="b9e03-198">Ensure all names and policy numbers are unique on hello device</span></span>
> - <span data-ttu-id="b9e03-199">Убедитесь, что на вашем устройстве поддерживаются алгоритмы шифрования hello</span><span class="sxs-lookup"><span data-stu-id="b9e03-199">Ensure hello cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="b9e03-200">Замените следующие заполнителями фактическими значениями hello hello</span><span class="sxs-lookup"><span data-stu-id="b9e03-200">Replace hello following place holders with hello actual values</span></span>
>   - <span data-ttu-id="b9e03-201">Имя внешнего интерфейса: outside;</span><span class="sxs-lookup"><span data-stu-id="b9e03-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="b9e03-202">Azure_Gateway_Public_IP;</span><span class="sxs-lookup"><span data-stu-id="b9e03-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="b9e03-203">OnPrem_Device_Public_IP;</span><span class="sxs-lookup"><span data-stu-id="b9e03-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="b9e03-204">IKE Pre_Shared_Key;</span><span class="sxs-lookup"><span data-stu-id="b9e03-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="b9e03-205">Имена виртуальной сети и шлюза локальной сети (VNetName, LNGName).</span><span class="sxs-lookup"><span data-stu-id="b9e03-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="b9e03-206">Префиксы адресов виртуальной сети и локальной сети.</span><span class="sxs-lookup"><span data-stu-id="b9e03-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="b9e03-207">Правильные маски сети.</span><span class="sxs-lookup"><span data-stu-id="b9e03-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="b9e03-208">Пример конфигурации</span><span class="sxs-lookup"><span data-stu-id="b9e03-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
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
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
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
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
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
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
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
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="b9e03-209">Простые команды отладки</span><span class="sxs-lookup"><span data-stu-id="b9e03-209">Simple debugging commands</span></span>

<span data-ttu-id="b9e03-210">Ниже приведены некоторые команды ASA для отладки.</span><span class="sxs-lookup"><span data-stu-id="b9e03-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="b9e03-211">Показать hello IPsec и IKE SA</span><span class="sxs-lookup"><span data-stu-id="b9e03-211">Show hello IPsec and IKE SA's</span></span>
    - <span data-ttu-id="b9e03-212">show crypto ipsec sa;</span><span class="sxs-lookup"><span data-stu-id="b9e03-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="b9e03-213">show crypto ikev2 sa.</span><span class="sxs-lookup"><span data-stu-id="b9e03-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="b9e03-214">Ввод режима отладки — это позволяет получить очень шумный на консоли hello</span><span class="sxs-lookup"><span data-stu-id="b9e03-214">Entering debug mode - this can get very noisy on hello console</span></span>
    - <span data-ttu-id="b9e03-215">debug crypto ikev2 platform <level>;</span><span class="sxs-lookup"><span data-stu-id="b9e03-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="b9e03-216">debug crypto ikev2 protocol <level>.</span><span class="sxs-lookup"><span data-stu-id="b9e03-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="b9e03-217">Вывод текущих конфигураций.</span><span class="sxs-lookup"><span data-stu-id="b9e03-217">List current configurations</span></span>
    - <span data-ttu-id="b9e03-218">«Показать выполнения» — отображает hello текущих конфигураций на устройстве hello; можно использовать различные подкоманды toolist определенные части конфигурации hello hello.</span><span class="sxs-lookup"><span data-stu-id="b9e03-218">"show run" - shows hello current configurations on hello device; you can use hello various sub-commands toolist specific parts of hello configuration.</span></span> <span data-ttu-id="b9e03-219">Например, show run crypto, show run access-list, show run tunnel-group и т. д.</span><span class="sxs-lookup"><span data-stu-id="b9e03-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b9e03-220">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b9e03-220">Next steps</span></span>
<span data-ttu-id="b9e03-221">В разделе [настройка активных VPN-шлюзов для подключений виртуальной сети для виртуальной сети и между организациями](vpn-gateway-activeactive-rm-powershell.md) действия перекрестные tooconfigure активных и подключения к виртуальной сети для виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="b9e03-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

