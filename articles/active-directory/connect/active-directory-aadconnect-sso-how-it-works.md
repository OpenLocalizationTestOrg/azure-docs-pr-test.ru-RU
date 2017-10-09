---
title: "Azure AD Connect: простой единый вход — как это работает | Документы Майкрософт"
description: "В этой статье описано, как работает функция hello Azure Active Directory прозрачную единого входа."
services: active-directory
keywords: "что такое Azure AD Connect, установка Active Directory, необходимые компоненты для Azure AD, единый вход"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="7edd3-104">Подробное техническое руководство по простому единому входу Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7edd3-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="7edd3-105">В этой статье приводятся технические сведения в работе системы hello Azure Active Directory прозрачную единого входа (прозрачную SSO).</span><span class="sxs-lookup"><span data-stu-id="7edd3-105">This article gives you technical details into how hello Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="7edd3-106">компонент Hello прозрачную единого входа в настоящий момент в режиме предварительного просмотра.</span><span class="sxs-lookup"><span data-stu-id="7edd3-106">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="7edd3-107">Как работает простой единый вход?</span><span class="sxs-lookup"><span data-stu-id="7edd3-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="7edd3-108">Этот раздел состоит из двух частей tooit.</span><span class="sxs-lookup"><span data-stu-id="7edd3-108">This section has two parts tooit:</span></span>
1. <span data-ttu-id="7edd3-109">Настройка Hello функции hello прозрачную единого входа.</span><span class="sxs-lookup"><span data-stu-id="7edd3-109">hello setup of hello Seamless SSO feature.</span></span>
2. <span data-ttu-id="7edd3-110">Как транзакция единого входа пользователя работает с простым единым входом.</span><span class="sxs-lookup"><span data-stu-id="7edd3-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="7edd3-111">Как выполняется настройка?</span><span class="sxs-lookup"><span data-stu-id="7edd3-111">How does set up work?</span></span>

<span data-ttu-id="7edd3-112">Простой единый вход включается с помощью Azure AD Connect, как показано [здесь](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="7edd3-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="7edd3-113">При включении компонента hello, происходят hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="7edd3-113">While enabling hello feature, hello following steps occur:</span></span>
- <span data-ttu-id="7edd3-114">В локальной службе Active Directory (AD) создается учетная запись компьютера с именем `AZUREADSSOACCT` (представляет Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7edd3-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="7edd3-115">ключ расшифровки Kerberos учетная запись компьютера Hello безопасно совместно с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7edd3-115">hello computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="7edd3-116">Кроме того два Kerberos имен участников-служб (SPN) создаются toorepresent два URL-адреса, используемые при входе в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7edd3-116">In addition, two Kerberos service principal names (SPNs) are created toorepresent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="7edd3-117">в каждом лесу создаются Hello учетной записи компьютера и Kerberos приветствия имен участников-служб синхронизации tooAzure AD (с помощью Azure AD Connect) и для пользователей, для которого требуется эффективная единого входа.</span><span class="sxs-lookup"><span data-stu-id="7edd3-117">hello computer account and hello Kerberos SPNs are created in each AD forest you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="7edd3-118">Переместить hello `AZUREADSSOACCT` tooan учетной записи компьютера подразделение (OU) которых хранимые tooensure, которые управляются в другие учетные записи компьютеров hello таким же способом, а не удаляется.</span><span class="sxs-lookup"><span data-stu-id="7edd3-118">Move hello `AZUREADSSOACCT` computer account tooan Organization Unit (OU) where other computer accounts are stored tooensure that it is managed in hello same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="7edd3-119">Настоятельно рекомендуется, чтобы вы [, наведите курсор на ключ расшифровки Kerberos hello](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) из hello `AZUREADSSOACCT` учетная запись компьютера каждые 30 дней.</span><span class="sxs-lookup"><span data-stu-id="7edd3-119">We highly recommend that you [roll over hello Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of hello `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="7edd3-120">Как работает вход с функцией простого единого входа?</span><span class="sxs-lookup"><span data-stu-id="7edd3-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="7edd3-121">После завершения установки hello прозрачную SSO работает hello таким же способом, как любой другой вход, использующего встроенную проверку подлинности Windows (IWA).</span><span class="sxs-lookup"><span data-stu-id="7edd3-121">Once hello set-up is complete, Seamless SSO works hello same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="7edd3-122">Hello поток выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="7edd3-122">hello flow is as follows:</span></span>

1. <span data-ttu-id="7edd3-123">Hello пользователь пытается tooaccess приложения (например, hello Outlook Web App - https://outlook.office365.com/owa/) с корпоративной устройства в корпоративной сети, присоединенных к домену.</span><span class="sxs-lookup"><span data-stu-id="7edd3-123">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="7edd3-124">Если пользователь hello не уже выполнил вход, пользователь hello не перенаправленный toohello Azure AD на странице входа.</span><span class="sxs-lookup"><span data-stu-id="7edd3-124">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="7edd3-125">Если запрос вход hello Azure AD включает `domain_hint` (идентификации клиента - например, contoso.onmicrosoft.com) или `login_hint` (Идентификация пользователя hello - например, user@contoso.onmicrosoft.com или user@contoso.com) пропущен параметр, а затем шаг 2.</span><span class="sxs-lookup"><span data-stu-id="7edd3-125">If hello Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying hello user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="7edd3-126">пользователь вводит свои имя пользователя в hello Azure AD на странице входа Hello.</span><span class="sxs-lookup"><span data-stu-id="7edd3-126">hello user types in their user name into hello Azure AD sign-in page.</span></span>
4. <span data-ttu-id="7edd3-127">С помощью JavaScript в фоновом режиме hello, Azure AD предлагает hello браузера, через 401 несанкционированный ответа tooprovide билет Kerberos.</span><span class="sxs-lookup"><span data-stu-id="7edd3-127">Using JavaScript in hello background, Azure AD challenges hello browser, via a 401 Unauthorized response, tooprovide a Kerberos ticket.</span></span>
5. <span data-ttu-id="7edd3-128">Hello браузера, в свою очередь, запрашивает билет у Active Directory для hello `AZUREADSSOACCT` учетной записи компьютера (представляющий Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7edd3-128">hello browser, in turn, requests a ticket from Active Directory for hello `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="7edd3-129">Active Directory находит учетную запись компьютера hello и возвращается обозревателя toohello билет Kerberos, зашифрованные с помощью учетной записи компьютера hello секрет.</span><span class="sxs-lookup"><span data-stu-id="7edd3-129">Active Directory locates hello computer account and returns a Kerberos ticket toohello browser encrypted with hello computer account's secret.</span></span>
7. <span data-ttu-id="7edd3-130">hello билет Kerberos, полученную из Active Directory tooAzure AD перенаправляет браузер Hello (на одном hello [URL-адреса Azure AD, ранее добавленных настроек зоны toohello обозревателя](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="7edd3-130">hello browser forwards hello Kerberos ticket it acquired from Active Directory tooAzure AD (on one of hello [Azure AD URLs previously added toohello browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="7edd3-131">Azure AD расшифровывает hello билет Kerberos, включающий hello удостоверение пользователя hello, вход в корпоративных устройств hello, ранее с помощью hello общий ключ.</span><span class="sxs-lookup"><span data-stu-id="7edd3-131">Azure AD decrypts hello Kerberos ticket, which includes hello identity of hello user signed into hello corporate device, using hello previously shared key.</span></span>
9. <span data-ttu-id="7edd3-132">После оценки Azure AD возвращается токен задней toohello приложение или запрашивает у пользователя tooperform hello дополнительных экспериментов, например многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7edd3-132">After evaluation, Azure AD either returns a token back toohello application or asks hello user tooperform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="7edd3-133">Если вход hello пользователей прошла успешно, hello пользователь не может tooaccess приложения hello.</span><span class="sxs-lookup"><span data-stu-id="7edd3-133">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="7edd3-134">Hello следующей схеме показаны все компоненты hello и этапы hello.</span><span class="sxs-lookup"><span data-stu-id="7edd3-134">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Простой единый вход](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="7edd3-136">Эффективная SSO нежестких, что означает, что в случае неудачи hello входа в систему возвращается tooits регулярного поведение — т. е., hello пользователь должен tooenter их toosign пароль в.</span><span class="sxs-lookup"><span data-stu-id="7edd3-136">Seamless SSO is opportunistic, which means if it fails, hello sign-in experience falls back tooits regular behavior - i.e, hello user needs tooenter their password toosign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7edd3-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7edd3-137">Next steps</span></span>

- <span data-ttu-id="7edd3-138">[**Краткое руководство**](active-directory-aadconnect-sso-quick-start.md). Настройка и подготовка к работе простого единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7edd3-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="7edd3-139">[**Часто задаваемые вопросы** ](active-directory-aadconnect-sso-faq.md) -ответы на вопросы и ответы toofrequently.</span><span class="sxs-lookup"><span data-stu-id="7edd3-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="7edd3-140">[**Устранение неполадок** ](active-directory-aadconnect-troubleshoot-sso.md) -Узнайте, как tooresolve распространенные проблемы, с помощью функции hello.</span><span class="sxs-lookup"><span data-stu-id="7edd3-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="7edd3-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.</span><span class="sxs-lookup"><span data-stu-id="7edd3-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
