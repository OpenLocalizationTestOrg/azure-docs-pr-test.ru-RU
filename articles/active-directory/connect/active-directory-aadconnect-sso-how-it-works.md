---
title: "Azure AD Connect: простой единый вход — как это работает | Документы Майкрософт"
description: "В этой статье описывается принцип работы функции простого единого входа в Azure Active Directory."
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
ms.openlocfilehash: f0bcbdb03fbb70ff91ac3a56974a88eb1b26c245
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="19e68-104">Подробное техническое руководство по простому единому входу Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="19e68-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="19e68-105">В этой статье приводятся технические сведения о работе функции простого единого входа Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="19e68-105">This article gives you technical details into how the Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="19e68-106">Функция простого единого входа находится на этапе предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="19e68-106">The Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="19e68-107">Как работает простой единый вход?</span><span class="sxs-lookup"><span data-stu-id="19e68-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="19e68-108">Этот раздел состоит из двух частей.</span><span class="sxs-lookup"><span data-stu-id="19e68-108">This section has two parts to it:</span></span>
1. <span data-ttu-id="19e68-109">Настройка функции простого единого входа.</span><span class="sxs-lookup"><span data-stu-id="19e68-109">The setup of the Seamless SSO feature.</span></span>
2. <span data-ttu-id="19e68-110">Как транзакция единого входа пользователя работает с простым единым входом.</span><span class="sxs-lookup"><span data-stu-id="19e68-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="19e68-111">Как выполняется настройка?</span><span class="sxs-lookup"><span data-stu-id="19e68-111">How does set up work?</span></span>

<span data-ttu-id="19e68-112">Простой единый вход включается с помощью Azure AD Connect, как показано [здесь](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="19e68-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="19e68-113">При включении функции выполняются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="19e68-113">While enabling the feature, the following steps occur:</span></span>
- <span data-ttu-id="19e68-114">В локальной службе Active Directory (AD) создается учетная запись компьютера с именем `AZUREADSSOACCT` (представляет Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19e68-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="19e68-115">С помощью Azure AD безопасным образом предоставляется ключ расшифровки Kerberos учетной записи компьютера.</span><span class="sxs-lookup"><span data-stu-id="19e68-115">The computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="19e68-116">Кроме того, создаются два имени субъектов-служб (SPN) Kerberos, представляющие URL-адреса, используемые при входе в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19e68-116">In addition, two Kerberos service principal names (SPNs) are created to represent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="19e68-117">Учетная запись компьютера и имена участников-служб Kerberos создаются в каждом лесу AD, который синхронизируется с Azure AD (с помощью Azure AD Connect) и для пользователей которого должен иметься простой единый вход.</span><span class="sxs-lookup"><span data-stu-id="19e68-117">The computer account and the Kerberos SPNs are created in each AD forest you synchronize to Azure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="19e68-118">Переместите учетную запись `AZUREADSSOACCT` компьютера в подразделение (OU), где хранятся другие учетные записи компьютеров, чтобы управлять им таким же образом и избежать удаления.</span><span class="sxs-lookup"><span data-stu-id="19e68-118">Move the `AZUREADSSOACCT` computer account to an Organization Unit (OU) where other computer accounts are stored to ensure that it is managed in the same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="19e68-119">Настоятельно рекомендуется, чтобы вы [меняли ключ расшифровки Kerberos](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) для учетной записи компьютера `AZUREADSSOACCT` хотя бы раз в 30 дней.</span><span class="sxs-lookup"><span data-stu-id="19e68-119">We highly recommend that you [roll over the Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of the `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="19e68-120">Как работает вход с функцией простого единого входа?</span><span class="sxs-lookup"><span data-stu-id="19e68-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="19e68-121">После завершения настройки функция простого входа в Azure AD работает так же, как любая другая функция входа, использующая встроенную проверку подлинности Windows (IWA).</span><span class="sxs-lookup"><span data-stu-id="19e68-121">Once the set-up is complete, Seamless SSO works the same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="19e68-122">Процесс выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="19e68-122">The flow is as follows:</span></span>

1. <span data-ttu-id="19e68-123">Пользователь пытается получить доступ к приложению (например, Outlook Web App - https://outlook.office365.com/owa/) с корпоративного устройства, присоединенного к домену, в корпоративной сети.</span><span class="sxs-lookup"><span data-stu-id="19e68-123">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="19e68-124">Если пользователь еще не выполнил вход, он перенаправляется на страницу входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19e68-124">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="19e68-125">Если запрос на вход в Azure AD содержит параметр `domain_hint` (идентифицирует клиент, например contoso.onmicrosoft.com) или `login_hint` (определяет пользователя, например user@contoso.onmicrosoft.com или user@contoso.com), то шаг 2 пропускается.</span><span class="sxs-lookup"><span data-stu-id="19e68-125">If the Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying the user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="19e68-126">Пользователь вводит свое имя на странице входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19e68-126">The user types in their user name into the Azure AD sign-in page.</span></span>
4. <span data-ttu-id="19e68-127">С помощью JavaScript, выполняемого в фоновом режиме, Azure AD запрашивает у браузера билет Kerberos (возвращается ответ 401 — не авторизовано).</span><span class="sxs-lookup"><span data-stu-id="19e68-127">Using JavaScript in the background, Azure AD challenges the browser, via a 401 Unauthorized response, to provide a Kerberos ticket.</span></span>
5. <span data-ttu-id="19e68-128">В свою очередь браузер запрашивает в Active Directory билет для учетной записи компьютера `AZUREADSSOACCT` (которая представляет Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19e68-128">The browser, in turn, requests a ticket from Active Directory for the `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="19e68-129">Active Directory находит учетную запись компьютера и возвращает браузеру билет Kerberos, зашифрованный с использованием секрета этой учетной записи компьютера.</span><span class="sxs-lookup"><span data-stu-id="19e68-129">Active Directory locates the computer account and returns a Kerberos ticket to the browser encrypted with the computer account's secret.</span></span>
7. <span data-ttu-id="19e68-130">Браузер отправляет билет Kerberos, полученный из Active Directory, в Azure AD (по одному из [URL-адресов Azure AD, предварительно добавленных в настройки зоны интрасети браузера](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="19e68-130">The browser forwards the Kerberos ticket it acquired from Active Directory to Azure AD (on one of the [Azure AD URLs previously added to the browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="19e68-131">Azure AD расшифровывает билет Kerberos, который содержит удостоверение пользователя, выполнившего вход в корпоративное устройство, с помощью полученного ранее общего ключа.</span><span class="sxs-lookup"><span data-stu-id="19e68-131">Azure AD decrypts the Kerberos ticket, which includes the identity of the user signed into the corporate device, using the previously shared key.</span></span>
9. <span data-ttu-id="19e68-132">После анализа Azure AD либо возвращает маркер приложению, либо предлагает пользователю выполнить дополнительную проверку, например Многофакторную идентификацию.</span><span class="sxs-lookup"><span data-stu-id="19e68-132">After evaluation, Azure AD either returns a token back to the application or asks the user to perform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="19e68-133">При успешном входе в систему пользователь может получить доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="19e68-133">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="19e68-134">На схеме ниже показаны все соответствующие компоненты и шаги.</span><span class="sxs-lookup"><span data-stu-id="19e68-134">The following diagram illustrates all the components and the steps involved.</span></span>

![Простой единый вход](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="19e68-136">Простой единый вход — ситуативно-обусловленная функция. Это означает, что если в ней происходит сбой, процедура входа выполняется стандартно, то есть пользователь, как и прежде, должен просто ввести пароль для входа.</span><span class="sxs-lookup"><span data-stu-id="19e68-136">Seamless SSO is opportunistic, which means if it fails, the sign-in experience falls back to its regular behavior - i.e, the user needs to enter their password to sign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19e68-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="19e68-137">Next steps</span></span>

- <span data-ttu-id="19e68-138">[**Краткое руководство**](active-directory-aadconnect-sso-quick-start.md). Настройка и подготовка к работе простого единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19e68-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="19e68-139">[**Часто задаваемые вопросы**](active-directory-aadconnect-sso-faq.md). Ответы на часто задаваемые вопросы.</span><span class="sxs-lookup"><span data-stu-id="19e68-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="19e68-140">[**Устранение неполадок**](active-directory-aadconnect-troubleshoot-sso.md). Узнайте, как устранить самые распространенные проблемы с этой функцией.</span><span class="sxs-lookup"><span data-stu-id="19e68-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="19e68-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect). Отправка запросов новых функций.</span><span class="sxs-lookup"><span data-stu-id="19e68-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
