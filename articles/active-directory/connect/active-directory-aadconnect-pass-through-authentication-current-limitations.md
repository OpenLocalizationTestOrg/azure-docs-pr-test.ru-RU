---
title: "Текущие ограничения сквозной проверки подлинности Azure AD Connect | Документация Майкрософт"
description: "В этой статье описываются hello текущего ограничения сквозная проверка подлинности Azure Active Directory (Azure AD)."
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
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="8b6cd-104">Текущие ограничения сквозной проверки подлинности Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b6cd-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="8b6cd-105">Сквозная проверка подлинности Azure AD доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-105">Azure AD Pass-through Authentication is currently in preview.</span></span> <span data-ttu-id="8b6cd-106">Это бесплатная функция, и любые платных выпусков toouse Azure AD не нужно его.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-106">It is a free feature, and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="8b6cd-107">Сквозная проверка подлинности доступна только в hello world wide экземпляра Azure AD, а не в [Германия Microsoft Cloud](http://www.microsoft.de/cloud-deutschland) и [государственных облако Microsoft Azure](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="8b6cd-107">Pass-through Authentication is only available in hello world-wide instance of Azure AD, and not on [Microsoft Cloud Germany](http://www.microsoft.de/cloud-deutschland) and [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="8b6cd-108">Поддерживаемые сценарии использования.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-108">Supported scenarios</span></span>

<span data-ttu-id="8b6cd-109">следующие сценарии Hello, полностью поддерживаются во время предварительного просмотра:</span><span class="sxs-lookup"><span data-stu-id="8b6cd-109">hello following scenarios are fully supported during preview:</span></span>

- <span data-ttu-id="8b6cd-110">Вход пользователей во все браузерные приложения.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-110">User sign-ins into all web browser-based applications.</span></span>
- <span data-ttu-id="8b6cd-111">Вход пользователей в клиентские приложения Office 365, поддерживающие [современную проверку подлинности](https://aka.ms/modernauthga).</span><span class="sxs-lookup"><span data-stu-id="8b6cd-111">User sign-ins into Office 365 client applications that support [modern authentication](https://aka.ms/modernauthga).</span></span>
- <span data-ttu-id="8b6cd-112">Присоединение устройств Windows 10 к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-112">Azure AD Join for Windows 10 devices.</span></span>
- <span data-ttu-id="8b6cd-113">Поддержка Exchange ActiveSync.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-113">Exchange ActiveSync support.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="8b6cd-114">Неподдерживаемые сценарии</span><span class="sxs-lookup"><span data-stu-id="8b6cd-114">Unsupported scenarios</span></span>

<span data-ttu-id="8b6cd-115">Hello ниже сценарии являются _не_ поддерживается во время предварительного просмотра:</span><span class="sxs-lookup"><span data-stu-id="8b6cd-115">hello following scenarios are _not_ supported during preview:</span></span>

- <span data-ttu-id="8b6cd-116">Вход пользователей в устаревшие клиентские приложения Office (Office 2013 или более ранних версий).</span><span class="sxs-lookup"><span data-stu-id="8b6cd-116">User sign-ins into legacy Office client applications (Office 2013 or earlier).</span></span> <span data-ttu-id="8b6cd-117">Организаций, рекомендуется tooswitch toomodern проверки подлинности, если это возможно.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-117">Organizations are encouraged tooswitch toomodern authentication, if possible.</span></span> <span data-ttu-id="8b6cd-118">Современная аутентификация обеспечивает поддержку сквозной аутентификации, а также помогает защитить учетные записи пользователей с помощью таких функций [условного доступа](../active-directory-conditional-access.md), как Многофакторная идентификация (MFA).</span><span class="sxs-lookup"><span data-stu-id="8b6cd-118">Modern authentication allows for Pass-through Authentication support but also helps you secure your user accounts using [conditional access](../active-directory-conditional-access.md) features such as Multi-Factor Authentication (MFA).</span></span>
- <span data-ttu-id="8b6cd-119">Вход пользователей в клиентские приложения Skype для бизнеса, включая Skype для бизнеса 2016.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-119">User sign-ins into Skype for Business client applications, including Skype for Business 2016.</span></span>
- <span data-ttu-id="8b6cd-120">Вход пользователей в PowerShell версии 1.0.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-120">User sign-ins into PowerShell v1.0.</span></span> <span data-ttu-id="8b6cd-121">Вместо этого рекомендуется использовать PowerShell версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-121">It is recommended that you use PowerShell v2.0 instead.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8b6cd-122">В качестве решения для неподдерживаемых сценариях Включение синхронизация хэшей паролей hello [дополнительных компонентов](active-directory-aadconnect-get-started-custom.md#optional-features) страница в мастере hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-122">As a workaround for unsupported scenarios, enable Password Hash Synchronization on hello [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in hello Azure AD Connect wizard.</span></span> <span data-ttu-id="8b6cd-123">Синхронизация хэшей паролей действует как переход на резервный ресурс hello предшествующий сценарии _только_ (и _не_ как универсальный резервной tooPass сквозной проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="8b6cd-123">Password Hash Synchronization acts as a fallback for hello preceding scenarios _only_ (and _not_ as a generic fallback tooPass-through Authentication).</span></span> <span data-ttu-id="8b6cd-124">Если эти сценарии не требуются, отключите синхронизацию хэша паролей.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-124">If you don't need these scenarios, turn off Password Hash Synchronization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b6cd-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b6cd-125">Next steps</span></span>
- <span data-ttu-id="8b6cd-126">[**Краткое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-quick-start.md). Настройка и подготовка к работе сквозной проверки подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="8b6cd-127">[**Техническое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-how-it-works.md). Сведения о том, как работает эта функция.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-127">[**Technical Deep Dive**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="8b6cd-128">[**Часто задаваемые вопросы** ](active-directory-aadconnect-pass-through-authentication-faq.md) -ответы на вопросы и ответы toofrequently.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-128">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="8b6cd-129">[**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-129">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="8b6cd-130">[**Простой единый вход Azure Active Directory**](active-directory-aadconnect-sso.md). Дополнительные сведения об этой дополнительной функции.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-130">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="8b6cd-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.</span><span class="sxs-lookup"><span data-stu-id="8b6cd-131">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
