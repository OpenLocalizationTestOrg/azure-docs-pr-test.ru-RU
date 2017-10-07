---
title: "aaaAbout требования шифрования и VPN-шлюзы Azure | Документы Microsoft"
description: "В этой статье рассматриваются требования к шифрованию и VPN-шлюзы Azure"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="ba337-103">Требования к шифрованию и VPN-шлюзы Azure</span><span class="sxs-lookup"><span data-stu-id="ba337-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="ba337-104">Здесь рассматривается настройка toosatisfy шлюзах Azure VPN требованиями шифрования для туннелей S2S VPN между организациями и подключений виртуальной сети для виртуальной сети в Azure.</span><span class="sxs-lookup"><span data-stu-id="ba337-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="ba337-105">Параметры политики IPsec и IKE для VPN-шлюзов Azure</span><span class="sxs-lookup"><span data-stu-id="ba337-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="ba337-106">Стандарт протоколов IPsec и IKE поддерживает широкий набор алгоритмов шифрования в различных сочетаниях.</span><span class="sxs-lookup"><span data-stu-id="ba337-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="ba337-107">Если клиенты не запрашивают конкретную комбинацию алгоритмов шифрования и параметров, VPN-шлюзы Azure используют набор предложений по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ba337-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="ba337-108">Задает политику по умолчанию Hello были выбраны toomaximize взаимодействия с широким спектром устройств VPN сторонних разработчиков в конфигурации по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ba337-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="ba337-109">В результате политики hello и hello количество предложений не могут охватывать все возможные сочетания доступных алгоритмов шифрования и значений длины ключа.</span><span class="sxs-lookup"><span data-stu-id="ba337-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="ba337-110">Здравствуйте, политика по умолчанию, задайте для VPN-шлюз Azure, приведен в документе hello: [сведения о VPN-устройства и параметры IPsec/IKE для подключений VPN-шлюз сайта для сайта](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="ba337-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="ba337-111">Требования к шифрованию</span><span class="sxs-lookup"><span data-stu-id="ba337-111">Cryptographic requirements</span></span>
<span data-ttu-id="ba337-112">Для обмена данными, требуют определенных алгоритмов шифрования или параметров обычно из-за требований к toocompliance или безопасности клиентов теперь можно настроить их toouse шлюзах Azure VPN настраиваемой политики IPsec/IKE с конкретными шифрования алгоритмы и ключевые преимущества, чем наборы политики hello Azure по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ba337-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="ba337-113">Например hello IKEv2 основного режима политик для VPN-шлюзы Azure использовать только алгоритм Диффи-Хелмана группа 2 (1024 бита), а клиентам может потребоваться более надежные группы toobe toospecify используется в IKE, такие как группы 14 (2048 бит), 24 группы (группа MODP 2048-разрядный) или ECP (эллиптических Кривая групп) 256 или 384 бит (Группировать 19 и 20 группы, соответственно).</span><span class="sxs-lookup"><span data-stu-id="ba337-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="ba337-114">Подобные требования применяются также tooIPsec политики быстрого режима.</span><span class="sxs-lookup"><span data-stu-id="ba337-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="ba337-115">Пользовательская политика IPsec/IKE с VPN-шлюзами Azure</span><span class="sxs-lookup"><span data-stu-id="ba337-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="ba337-116">VPN-шлюзы Azure теперь поддерживают настраиваемые политики IPsec/IKE, задаваемые для отдельных подключений.</span><span class="sxs-lookup"><span data-stu-id="ba337-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="ba337-117">Для сеть-сеть или подключение виртуальной сети для виртуальной сети можно выбрать определенное сочетание алгоритмов шифрования IPsec и IKE с hello требуемого стойкость ключа, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="ba337-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="ba337-119">Можно создать политику IPsec/IKE и применить tooa существующего или нового соединения.</span><span class="sxs-lookup"><span data-stu-id="ba337-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="ba337-120">Рабочий процесс</span><span class="sxs-lookup"><span data-stu-id="ba337-120">Workflow</span></span>

1. <span data-ttu-id="ba337-121">Создайте виртуальные сети hello, шлюзах VPN или шлюзы локальной сети для подключения к топологии, как описано в других как toodocuments</span><span class="sxs-lookup"><span data-stu-id="ba337-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="ba337-122">Создайте политику IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="ba337-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="ba337-123">При создании подключения к S2S или виртуальной сети для виртуальной сети можно применить политику hello</span><span class="sxs-lookup"><span data-stu-id="ba337-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="ba337-124">Если соединение hello уже создано, можно применить или обновить существующее соединение hello политики tooan</span><span class="sxs-lookup"><span data-stu-id="ba337-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="ba337-125">Часто задаваемые вопросы о политике IPsec/IKE</span><span class="sxs-lookup"><span data-stu-id="ba337-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="ba337-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ba337-126">Next steps</span></span>
<span data-ttu-id="ba337-127">Пошаговые инструкции по настройке пользовательской политики IPsec/IKE для подключения см. в статье о [настройке политики IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ba337-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="ba337-128">См. также [подключения нескольких устройств VPN на основе политики](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn Дополнительные сведения о hello UsePolicyBasedTrafficSelectors параметр.</span><span class="sxs-lookup"><span data-stu-id="ba337-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
