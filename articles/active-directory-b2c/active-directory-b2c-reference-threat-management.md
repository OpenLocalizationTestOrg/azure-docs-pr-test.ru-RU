---
title: "Предотвращение угроз в Azure Active Directory B2C | Документация Майкрософт"
description: "Дополнительные сведения о методиках обнаружения и устранения рисков атак типа \"отказ в обслуживании\" и атак для взлома пароля в Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: vigunase
manager: Ajith Alexander
editor: 
ms.assetid: 6df79878-65cb-4dfc-98bb-2b328055bc2e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2016
ms.author: 
ms.openlocfilehash: 60bc0cc392b332cc4e9741ddb97dfa58e68ed420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a>Предотвращение угроз в Azure Active Directory B2C

Предотвращение угроз включает в себя планирование защиты от атак, нацеленных на систему и сети. Атаки типа "отказ в обслуживании" может стать недоступным toointended пользователей ресурсы. Tooresources доступа toounauthorized интереса атак пароль. Служба Azure Active Directory B2C (Azure AD B2C) оснащена несколькими встроенными средствами защиты данных от таких угроз.

## <a name="denial-of-service-attacks"></a>Атаки типа "отказ в обслуживании"

Azure AD B2C использует методы обнаружения и устранения рисков как файлы cookie SYN и скорость и подключение tooprotect ограничения базового ресурсы от атак типа "отказ в обслуживании".

## <a name="password-attacks"></a>Атаки для взлома пароля

Служба Azure AD B2C также имеет методики противодействия атакам для взлома пароля. Эти методики действуют при атаках методом подбора пароля и при словарных атаках на пароль. Пароли, которые установлены пользователями, требуется toobe достаточно сложными. С помощью различных сигналов, Azure AD B2C анализирует целостности hello запросов. Azure AD B2C предназначен toointelligently предполагаемым пользователям отличить от хакеров и ботнетов. Azure AD B2C предоставляет toolock сложные стратегии учетных записей с учетом hello пароли, введенные в hello вероятность атаки.

Для получения дополнительной информации посетите hello [Центр управления безопасностью Microsoft](https://www.microsoft.com/trustcenter/security/threatmanagement).
