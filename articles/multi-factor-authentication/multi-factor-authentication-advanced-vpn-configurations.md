---
title: "Расширенные сценарии с использованием Azure MFA и VPN сторонних поставщиков"
description: "Пошаговые руководства по настройке Azure MFA для интеграции с устройствами Cisco, Citrix и Juniper."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: richagi
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: joflore
ms.openlocfilehash: 62caebb6dec5b3603bf7618fdaf183e9a98d992e
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/11/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>Расширенные сценарии с использованием Многофакторной идентификации Azure и VPN-решений сторонних поставщиков
Многофакторную идентификацию Azure можно использовать для быстрого подключения к широкому спектру VPN-решений сторонних поставщиков. Эта статья посвящена применению устройств VPN Cisco® ASA, Citrix NetScaler SSL, а также Juniper Networks Secure Access/Pulse Secure Connect Secure SSL. Мы разработали руководства по настройке для этих трех распространенных устройств. Сервер Многофакторной идентификации также можно интегрировать с большинством других систем, которые используют для доступа в AD FS технологии RADIUS, LDAP, IIS или проверку подлинности на основе утверждений. Дополнительные сведения см. в разделе [Дополнительные конфигурации сервера Azure Multi-Factor Authentication](multi-factor-authentication-get-started-server.md#next-steps).

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Устройство VPN Cisco ASA и Многофакторная идентификация Azure
Многофакторная идентификация Azure интегрируется с устройством VPN Cisco® ASA, обеспечивая дополнительную защиту учетных данных VPN Cisco AnyConnect® и доступа к порталу.  Вы можете использовать протокол LDAP или RADIUS.  Щелкните одну из следующих ссылок и загрузите подробную пошаговую инструкцию по настройке.

| Руководство по настройке | ОПИСАНИЕ |
| --- | --- |
| [Настройка Cisco ASA с конфигурацией Anyconnect VPN и многофакторной проверки подлинности Azure для LDAP](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | Интеграция устройства VPN Cisco ASA с Azure MFA с помощью LDAP |
| [Настройка Cisco ASA с конфигурацией Anyconnect VPN и многофакторной проверки подлинности Azure для RADIUS](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | Интеграция устройства VPN Cisco ASA с Azure MFA с помощью RADIUS |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>VPN Citrix NetScaler SSL и Многофакторная идентификация Azure
Многофакторная идентификация Azure интегрируется с устройством VPN Citrix NetScaler SSL, обеспечивая дополнительную защиту учетных данных VPN Citrix NetScaler SSL и доступа к порталу.  Вы можете использовать протокол LDAP или RADIUS.  Щелкните одну из следующих ссылок и загрузите подробную пошаговую инструкцию по настройке.

| Руководство по настройке | ОПИСАНИЕ |
| --- | --- |
| [Настройка VPN Citrix NetScaler SSL и многофакторной проверки подлинности Azure для LDAP](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | Интеграция устройства VPN Citrix NetScaler SSL с Azure MFA с помощью LDAP |
| [Настройка VPN Citrix NetScaler SSL и многофакторной проверки подлинности Azure для RADIUS](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | Интеграция устройства VPN Citrix NetScaler SSL с Azure MFA с помощью RADIUS |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Устройство VPN Juniper/Pulse Secure SSL и Многофакторная идентификация Azure
Служба Многофакторной идентификации Azure интегрируется с устройством VPN Juniper/Pulse Secure SSL, обеспечивая дополнительную защиту учетных данных VPN Juniper/Pulse Secure SSL и доступа к порталу.  Вы можете использовать протокол LDAP или RADIUS.  Щелкните одну из следующих ссылок и загрузите подробную пошаговую инструкцию по настройке.

| Руководство по настройке | ОПИСАНИЕ |
| --- | --- |
| [Настройка VPN Juniper/Pulse Secure SSL и многофакторной проверки подлинности Azure для LDAP](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | Интеграция устройства VPN Juniper/Pulse Secure SSL с Azure MFA с помощью LDAP |
| [Настройка VPN Juniper/Pulse Secure SSL и многофакторной проверки подлинности Azure для RADIUS](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | Интеграция устройства VPN Juniper/Pulse Secure SSL с Azure MFA с помощью RADIUS |

## <a name="next-steps"></a>Дальнейшие действия

- [Внедрение расширения NPS для Многофакторной идентификации Azure в существующую инфраструктуру проверки подлинности.](multi-factor-authentication-nps-extension.md)

- [Настройка параметров Многофакторной идентификации Azure](multi-factor-authentication-whats-next.md)