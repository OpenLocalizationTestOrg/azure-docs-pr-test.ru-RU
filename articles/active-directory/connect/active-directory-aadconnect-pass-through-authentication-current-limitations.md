---
title: "Текущие ограничения сквозной проверки подлинности Azure AD Connect | Документация Майкрософт"
description: "Эта статья содержит сведения о текущих ограничениях сквозной проверки подлинности Azure Active Directory (Azure AD)."
services: active-directory
keywords: "сквозная проверка подлинности azure ad connect, установка active directory, необходимые компоненты для azure ad, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 37c0ea094d02208f2516a4a040f75894e046c670
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="a6ed2-104">Текущие ограничения сквозной проверки подлинности Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a6ed2-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="a6ed2-105">Сквозная проверка подлинности Azure AD доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="a6ed2-106">Это бесплатная функция, и для ее использования не требуются платные выпуски Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-106">It is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="a6ed2-107">Сквозная проверка подлинности доступна только в общедоступном экземпляре Azure AD, а не в [Microsoft Cloud для Германии](http://www.microsoft.de/cloud-deutschland) и [облаке Microsoft Azure для государственных организаций](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="a6ed2-107">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="a6ed2-108">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-108">Supported scenarios</span></span>

<span data-ttu-id="a6ed2-109">На этапе предварительной версии полностью поддерживаются следующие сценарии.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-109">The following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="a6ed2-110">Вход пользователей во все браузерные приложения.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="a6ed2-111">Вход пользователей в клиентские приложения Office 365, поддерживающие [современную проверку подлинности](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="a6ed2-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="a6ed2-112">Присоединение устройств Windows 10 к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="a6ed2-113">Поддержка Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="a6ed2-114">Неподдерживаемые сценарии</span><span class="sxs-lookup"><span data-stu-id="a6ed2-114">Unsupported scenarios</span></span>

<span data-ttu-id="a6ed2-115">На этапе предварительной версии _не_ поддерживаются следующие сценарии.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-115">The following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="a6ed2-116">Вход пользователей в устаревшие клиентские приложения Office (Office 2013 или более ранних версий).</span><span class="sxs-lookup"><span data-stu-id="a6ed2-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="a6ed2-117">Организациям рекомендуется перейти на современные способы аутентификации, если это возможно.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-117">Organizations are encouraged to switch to modern authentication, if possible.</span></span> <span data-ttu-id="a6ed2-118">Современная аутентификация обеспечивает поддержку сквозной аутентификации, а также помогает защитить учетные записи пользователей с помощью таких функций [условного доступа](../active-directory-conditional-access.md), как Многофакторная идентификация (MFA).</span><span class="sxs-lookup"><span data-stu-id="a6ed2-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="a6ed2-119">Вход пользователей в клиентские приложения Skype для бизнеса, включая Skype для бизнеса 2016.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="a6ed2-120">Вход пользователей в PowerShell версии 1.0.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="a6ed2-121">Вместо этого рекомендуется использовать PowerShell версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="a6ed2-122">В качестве временного решения для неподдерживаемых сценариев включите синхронизацию хэша паролей на странице [Дополнительные возможности](active-directory-aadconnect-get-started-custom.md#optional-features) в мастере Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span> <span data-ttu-id="a6ed2-123">Синхронизация хэша паролей используется в качестве запасного варианта _только_ для предыдущих сценариев (а _не_ в качестве универсального варианта для сквозной проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="a6ed2-123">Password Hash Synchronization acts as a fallback for the preceding scenarios _only_ (and _not_ as a generic fallback to Pass-through Authentication).</span></span> <span data-ttu-id="a6ed2-124">Если эти сценарии не требуются, отключите синхронизацию хэша паролей.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6ed2-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6ed2-125">Next steps</span></span>
- <span data-ttu-id="a6ed2-126">[**Краткое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-quick-start.md). Настройка и подготовка к работе сквозной проверки подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="a6ed2-127">[**Azure Active Directory Pass-through Authentication: Technical deep dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) (Техническое руководство по сквозной проверке подлинности Azure Active Directory). Сведения о том, как работает эта функция.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="a6ed2-128">[**Часто задаваемые вопросы**](active-directory-aadconnect-pass-through-authentication-faq.md). Ответы на часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="a6ed2-129">[**Устранение неполадок**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md). Узнайте, как устранить самые распространенные проблемы с этой функцией.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="a6ed2-130">[**Простой единый вход Azure Active Directory**](active-directory-aadconnect-sso.md). Дополнительные сведения об этой дополнительной функции.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="a6ed2-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.</span><span class="sxs-lookup"><span data-stu-id="a6ed2-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
