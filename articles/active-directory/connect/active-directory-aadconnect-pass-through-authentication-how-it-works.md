---
title: "Сквозная аутентификация в Azure AD Connect — как это работает? | Документация Майкрософт"
description: "В этой статье описывается процедура сквозной аутентификации Azure Active Directory."
services: active-directory
keywords: "сквозная аутентификация azure ad connect, установка active directory, необходимые компоненты для azure ad, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="9d3e6-105">Сквозная аутентификация Azure Active Directory — подробное техническое руководство</span><span class="sxs-lookup"><span data-stu-id="9d3e6-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="9d3e6-106">Сквозная проверка подлинности Azure AD доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="9d3e6-107">Как работает сквозная аутентификация Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d3e6-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="9d3e6-108">Когда пользователь пытается toosign в приложении, защищенном Azure Active Directory (Azure AD) и если сквозная проверка подлинности включена на клиенте hello hello выполняются следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="9d3e6-109">Hello пользователь пытается tooaccess приложения (например, hello Outlook Web App - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="9d3e6-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="9d3e6-110">Если пользователь hello не уже выполнил вход, пользователь hello не перенаправленный toohello Azure AD на странице входа.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="9d3e6-111">Hello пользователь вводит свое имя пользователя и пароль в hello Azure AD на странице входа и нажимает кнопку «Вход» hello.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="9d3e6-112">Azure AD, получив запрос вход hello, помещает hello имя пользователя и пароль (зашифрованный с помощью открытого ключа) в очередь.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="9d3e6-113">Агента сквозной проверки подлинности в локальной делает очередь toohello исходящего вызова и получает имя пользователя hello и зашифрованный пароль.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="9d3e6-114">агент Hello расшифровывает пароль hello, используя свой закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="9d3e6-115">агент Hello затем проверяет hello имя пользователя и пароль в Active Directory с использованием стандартных API Windows (аналогично toowhat механизм используется служб федерации Active Directory).</span><span class="sxs-lookup"><span data-stu-id="9d3e6-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="9d3e6-116">Hello имя пользователя может быть либо имя пользователя по умолчанию hello в локальной среде (обычно `userPrincipalName`) или другой атрибут, настроенные в Azure AD Connect (известный как `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="9d3e6-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="9d3e6-117">локальный контроллер домена Active Directory (DC) Hello то оценивает hello запрос и возвращает hello соответствующий ответ (успех, отказ, срок действия пароля истек, или пользователь заблокирован) toohello агента.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="9d3e6-118">агент Hello, в свою очередь, возвращает этот ответ назад tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="9d3e6-119">Azure AD оценивает ответа hello и отвечает пользователь toohello соответствующим образом — например, он сразу же входе пользователя hello или запросы для многофакторной проверки подлинности (MFA).</span><span class="sxs-lookup"><span data-stu-id="9d3e6-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="9d3e6-120">Если вход hello пользователей прошла успешно, hello пользователь не может tooaccess приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="9d3e6-121">Hello следующей схеме показаны все компоненты hello и этапы hello.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Сквозная проверка подлинности](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="9d3e6-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9d3e6-123">Next steps</span></span>
- <span data-ttu-id="9d3e6-124">[**Текущие ограничения**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) — эта функция в настоящее время находится на стадии предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="9d3e6-125">Узнайте, какие сценарии поддерживаются, а какие нет.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="9d3e6-126">[**Краткое руководство по сквозной проверке подлинности Azure Active Directory**](active-directory-aadconnect-pass-through-authentication-quick-start.md). Настройка и подготовка к работе сквозной проверки подлинности Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="9d3e6-127">[**Часто задаваемые вопросы** ](active-directory-aadconnect-pass-through-authentication-faq.md) -ответы на вопросы и ответы toofrequently.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="9d3e6-128">[**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="9d3e6-129">[**Простой единый вход Azure Active Directory**](active-directory-aadconnect-sso.md). Дополнительные сведения об этой дополнительной функции.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="9d3e6-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.</span><span class="sxs-lookup"><span data-stu-id="9d3e6-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
