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
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>Требования к шифрованию и VPN-шлюзы Azure

Здесь рассматривается настройка toosatisfy шлюзах Azure VPN требованиями шифрования для туннелей S2S VPN между организациями и подключений виртуальной сети для виртуальной сети в Azure. 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>Параметры политики IPsec и IKE для VPN-шлюзов Azure
Стандарт протоколов IPsec и IKE поддерживает широкий набор алгоритмов шифрования в различных сочетаниях. Если клиенты не запрашивают конкретную комбинацию алгоритмов шифрования и параметров, VPN-шлюзы Azure используют набор предложений по умолчанию. Задает политику по умолчанию Hello были выбраны toomaximize взаимодействия с широким спектром устройств VPN сторонних разработчиков в конфигурации по умолчанию. В результате политики hello и hello количество предложений не могут охватывать все возможные сочетания доступных алгоритмов шифрования и значений длины ключа.

Здравствуйте, политика по умолчанию, задайте для VPN-шлюз Azure, приведен в документе hello: [сведения о VPN-устройства и параметры IPsec/IKE для подключений VPN-шлюз сайта для сайта](vpn-gateway-about-vpn-devices.md).

## <a name="cryptographic-requirements"></a>Требования к шифрованию
Для обмена данными, требуют определенных алгоритмов шифрования или параметров обычно из-за требований к toocompliance или безопасности клиентов теперь можно настроить их toouse шлюзах Azure VPN настраиваемой политики IPsec/IKE с конкретными шифрования алгоритмы и ключевые преимущества, чем наборы политики hello Azure по умолчанию.

Например hello IKEv2 основного режима политик для VPN-шлюзы Azure использовать только алгоритм Диффи-Хелмана группа 2 (1024 бита), а клиентам может потребоваться более надежные группы toobe toospecify используется в IKE, такие как группы 14 (2048 бит), 24 группы (группа MODP 2048-разрядный) или ECP (эллиптических Кривая групп) 256 или 384 бит (Группировать 19 и 20 группы, соответственно). Подобные требования применяются также tooIPsec политики быстрого режима.

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>Пользовательская политика IPsec/IKE с VPN-шлюзами Azure
VPN-шлюзы Azure теперь поддерживают настраиваемые политики IPsec/IKE, задаваемые для отдельных подключений. Для сеть-сеть или подключение виртуальной сети для виртуальной сети можно выбрать определенное сочетание алгоритмов шифрования IPsec и IKE с hello требуемого стойкость ключа, как показано в следующий пример hello:

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

Можно создать политику IPsec/IKE и применить tooa существующего или нового соединения. 

### <a name="workflow"></a>Рабочий процесс

1. Создайте виртуальные сети hello, шлюзах VPN или шлюзы локальной сети для подключения к топологии, как описано в других как toodocuments
2. Создайте политику IPsec/IKE
3. При создании подключения к S2S или виртуальной сети для виртуальной сети можно применить политику hello
4. Если соединение hello уже создано, можно применить или обновить существующее соединение hello политики tooan


## <a name="ipsecike-policy-faq"></a>Часто задаваемые вопросы о политике IPsec/IKE

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>Дальнейшие действия
Пошаговые инструкции по настройке пользовательской политики IPsec/IKE для подключения см. в статье о [настройке политики IPsec/IKE](vpn-gateway-ipsecikepolicy-rm-powershell.md).

См. также [подключения нескольких устройств VPN на основе политики](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn Дополнительные сведения о hello UsePolicyBasedTrafficSelectors параметр.
