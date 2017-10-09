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
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="e5447-103">Предотвращение угроз в Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="e5447-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="e5447-104">Предотвращение угроз включает в себя планирование защиты от атак, нацеленных на систему и сети.</span><span class="sxs-lookup"><span data-stu-id="e5447-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="e5447-105">Атаки типа "отказ в обслуживании" может стать недоступным toointended пользователей ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e5447-105">Denial-of-service attacks might make resources unavailable toointended users.</span></span> <span data-ttu-id="e5447-106">Tooresources доступа toounauthorized интереса атак пароль.</span><span class="sxs-lookup"><span data-stu-id="e5447-106">Password attacks lead toounauthorized access tooresources.</span></span> <span data-ttu-id="e5447-107">Служба Azure Active Directory B2C (Azure AD B2C) оснащена несколькими встроенными средствами защиты данных от таких угроз.</span><span class="sxs-lookup"><span data-stu-id="e5447-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="e5447-108">Атаки типа "отказ в обслуживании"</span><span class="sxs-lookup"><span data-stu-id="e5447-108">Denial-of-service attacks</span></span>

<span data-ttu-id="e5447-109">Azure AD B2C использует методы обнаружения и устранения рисков как файлы cookie SYN и скорость и подключение tooprotect ограничения базового ресурсы от атак типа "отказ в обслуживании".</span><span class="sxs-lookup"><span data-stu-id="e5447-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits tooprotect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="e5447-110">Атаки для взлома пароля</span><span class="sxs-lookup"><span data-stu-id="e5447-110">Password attacks</span></span>

<span data-ttu-id="e5447-111">Служба Azure AD B2C также имеет методики противодействия атакам для взлома пароля.</span><span class="sxs-lookup"><span data-stu-id="e5447-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="e5447-112">Эти методики действуют при атаках методом подбора пароля и при словарных атаках на пароль.</span><span class="sxs-lookup"><span data-stu-id="e5447-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="e5447-113">Пароли, которые установлены пользователями, требуется toobe достаточно сложными.</span><span class="sxs-lookup"><span data-stu-id="e5447-113">Passwords that are set by users are required toobe reasonably complex.</span></span> <span data-ttu-id="e5447-114">С помощью различных сигналов, Azure AD B2C анализирует целостности hello запросов.</span><span class="sxs-lookup"><span data-stu-id="e5447-114">By using various signals, Azure AD B2C analyzes hello integrity of requests.</span></span> <span data-ttu-id="e5447-115">Azure AD B2C предназначен toointelligently предполагаемым пользователям отличить от хакеров и ботнетов.</span><span class="sxs-lookup"><span data-stu-id="e5447-115">Azure AD B2C is designed toointelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="e5447-116">Azure AD B2C предоставляет toolock сложные стратегии учетных записей с учетом hello пароли, введенные в hello вероятность атаки.</span><span class="sxs-lookup"><span data-stu-id="e5447-116">Azure AD B2C provides a sophisticated strategy toolock accounts based on hello passwords entered, in hello likelihood of an attack.</span></span>

<span data-ttu-id="e5447-117">Для получения дополнительной информации посетите hello [Центр управления безопасностью Microsoft](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="e5447-117">For more information, visit hello [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
