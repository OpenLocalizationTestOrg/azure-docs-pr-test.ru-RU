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
ms.openlocfilehash: 9472cb01eb713e297053727b1a314293574bb657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="4acc7-103">Предотвращение угроз в Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="4acc7-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="4acc7-104">Предотвращение угроз включает в себя планирование защиты от атак, нацеленных на систему и сети.</span><span class="sxs-lookup"><span data-stu-id="4acc7-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="4acc7-105">Атаки типа "отказ в обслуживании" могут сделать ресурсы недоступными для предполагаемых пользователей.</span><span class="sxs-lookup"><span data-stu-id="4acc7-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="4acc7-106">Атаки для взлома пароля приводят к несанкционированному доступу к ресурсам.</span><span class="sxs-lookup"><span data-stu-id="4acc7-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="4acc7-107">Служба Azure Active Directory B2C (Azure AD B2C) оснащена несколькими встроенными средствами защиты данных от таких угроз.</span><span class="sxs-lookup"><span data-stu-id="4acc7-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="4acc7-108">Атаки типа "отказ в обслуживании"</span><span class="sxs-lookup"><span data-stu-id="4acc7-108">Denial-of-service attacks</span></span>

<span data-ttu-id="4acc7-109">Для защиты базовых ресурсов от атак типа "отказ в обслуживании" Azure AD B2C использует методики обнаружения и уменьшения негативных последствий, такие как файлы cookie SYN, ограничение скорости и количества подключений.</span><span class="sxs-lookup"><span data-stu-id="4acc7-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="4acc7-110">Атаки для взлома пароля</span><span class="sxs-lookup"><span data-stu-id="4acc7-110">Password attacks</span></span>

<span data-ttu-id="4acc7-111">Служба Azure AD B2C также имеет методики противодействия атакам для взлома пароля.</span><span class="sxs-lookup"><span data-stu-id="4acc7-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="4acc7-112">Эти методики действуют при атаках методом подбора пароля и при словарных атаках на пароль.</span><span class="sxs-lookup"><span data-stu-id="4acc7-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="4acc7-113">Пароли, задаваемые пользователями, должны быть достаточно сложными.</span><span class="sxs-lookup"><span data-stu-id="4acc7-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="4acc7-114">Используя различные сигналы, Azure AD B2C анализирует целостность запросов.</span><span class="sxs-lookup"><span data-stu-id="4acc7-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="4acc7-115">Azure AD B2C предназначен для того, чтобы интеллектуально отличить предполагаемых пользователей от злоумышленников и ботнетов.</span><span class="sxs-lookup"><span data-stu-id="4acc7-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="4acc7-116">Служба Azure AD B2C применяет сложные стратегии для блокировки учетных записей, анализируя вводимые пароли и выявляя потенциальные атаки.</span><span class="sxs-lookup"><span data-stu-id="4acc7-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="4acc7-117">Дополнительные сведения см. в [центре управления безопасностью Майкрософт](https://www.microsoft.com/trustcenter/security/threatmanagement).</span><span class="sxs-lookup"><span data-stu-id="4acc7-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/security/threatmanagement).</span></span>
