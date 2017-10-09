---
title: "сценарии aaaAdvanced с многофакторной проверки Подлинности Azure и виртуальные частные сети сторонних разработчиков"
description: "Конфигурация пошаговые руководства по toointegrate многофакторной проверки Подлинности Azure с Cisco, Citrix и Juniper."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/13/2017
ms.author: kgremban
ms.openlocfilehash: e23960ca4977cc01271f99fa2bec70449e9acfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>Расширенные сценарии с использованием Многофакторной идентификации Azure и VPN-решений сторонних поставщиков
Azure Multi-factor Authentication может использоваться tooseamlessly подключиться с помощью различных решений VPN сторонних разработчиков. В этой статье описываются на устройство Cisco® ASA VPN, Citrix NetScaler SSL VPN-устройства и hello Juniper сетей безопасного доступа/Pulse Secure подключения защиты SSL VPN-устройством. Мы создали tooaddress руководства по конфигурации эти три общие устройства, но можно интегрировать многофакторную проверку подлинности сервера с большинством систем, использующих RADIUS, LDAP, IIS или проверки подлинности на основе утверждений tooAD FS. Дополнительные сведения см. в разделе [Дополнительные конфигурации сервера Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md#next-steps).

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Устройство VPN Cisco ASA и многофакторная проверка подлинности Azure
Azure Multi-factor Authentication интегрируется с вашей ASA® Cisco VPN устройства tooprovide дополнительную безопасность VPN Cisco AnyConnect® имена входа и доступа к порталу.  Это можно сделать с помощью либо hello протокол LDAP или RADIUS.  Выберите один из hello следующая конфигурация подробные пошаговые hello toodownload направляющих.

| Руководство по настройке | Описание |
| --- | --- |
| [Настройка Cisco ASA с конфигурацией Anyconnect VPN и многофакторной проверки подлинности Azure для LDAP](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | Интеграция устройства VPN Cisco ASA с Azure MFA с помощью LDAP |
| [Настройка Cisco ASA с конфигурацией Anyconnect VPN и многофакторной проверки подлинности Azure для RADIUS](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | Интеграция устройства VPN Cisco ASA с Azure MFA с помощью RADIUS |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>VPN Citrix NetScaler SSL и многофакторная проверка подлинности Azure
Azure Multi-factor Authentication интегрируется с Citrix NetScaler SSL VPN устройства tooprovide дополнительной безопасности для имен входа для Citrix NetScaler SSL VPN и доступа к порталу.  Это можно сделать с помощью либо hello протокол LDAP или RADIUS.  Выберите один из hello следующая конфигурация подробные пошаговые hello toodownload направляющих.

| Руководство по настройке | Описание |
| --- | --- |
| [Настройка VPN Citrix NetScaler SSL и многофакторной проверки подлинности Azure для LDAP](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | Интеграция устройства VPN Citrix NetScaler SSL с Azure MFA с помощью LDAP |
| [Настройка VPN Citrix NetScaler SSL и многофакторной проверки подлинности Azure для RADIUS](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | Интеграция устройства VPN Citrix NetScaler SSL с Azure MFA с помощью RADIUS |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Устройство VPN Juniper/Pulse Secure SSL и многофакторная проверка подлинности Azure
Azure Multi-factor Authentication интегрируется с Juniper/Pulse Secure SSL VPN устройства tooprovide дополнительной безопасности для имен входа Juniper/Pulse Secure SSL VPN и доступа к порталу.  Это можно сделать с помощью либо hello протокол LDAP или RADIUS.  Выберите один из hello следующая конфигурация подробные пошаговые hello toodownload направляющих.

| Руководство по настройке | Описание |
| --- | --- |
| [Настройка VPN Juniper/Pulse Secure SSL и многофакторной проверки подлинности Azure для LDAP](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | Интеграция устройства VPN Juniper/Pulse Secure SSL с Azure MFA с помощью LDAP |
| [Настройка VPN Juniper/Pulse Secure SSL и многофакторной проверки подлинности Azure для RADIUS](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | Интеграция устройства VPN Juniper/Pulse Secure SSL с Azure MFA с помощью RADIUS |

## <a name="next-steps"></a>Дальнейшие действия

- [Расширить существующую инфраструктуру проверки подлинности с hello NPS расширения для многофакторной проверки подлинности Azure](multi-factor-authentication-nps-extension.md)

- [Настройка параметров Многофакторной идентификации Azure.](multi-factor-authentication-whats-next.md)