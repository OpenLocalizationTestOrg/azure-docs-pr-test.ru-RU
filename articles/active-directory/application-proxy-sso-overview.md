---
title: "aaaManage единого входа для прокси приложения Azure AD | Документы Microsoft"
description: "Дополнительные сведения об основах hello из единого входа с помощью прокси приложения"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="70ea3-103">Как прокси приложения Azure AD предоставляет единый вход?</span><span class="sxs-lookup"><span data-stu-id="70ea3-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="70ea3-104">Единый вход — это ключевой элемент прокси приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70ea3-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="70ea3-105">Он обеспечивает hello оптимального взаимодействия с пользователем, так как пользователи имеют только toosign в tooAzure Active Directory в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="70ea3-105">It provides hello best user experience because your users only have toosign in tooAzure Active Directory in hello cloud.</span></span> <span data-ttu-id="70ea3-106">После проверки подлинности tooAzure Active Directory, соединитель прокси приложения hello обрабатывает hello проверки подлинности toohello локального приложения.</span><span class="sxs-lookup"><span data-stu-id="70ea3-106">Once they authenticate tooAzure Active Directory, hello Application Proxy connector handles hello authentication toohello on-premises application.</span></span> <span data-ttu-id="70ea3-107">внутреннее приложение Hello не может определить hello различие между удаленным пользователям вход через прокси-сервер приложения и обычного использования на устройстве, присоединенных к домену.</span><span class="sxs-lookup"><span data-stu-id="70ea3-107">hello backend application can't tell hello difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="70ea3-108">для приложений,-tooyour toouse Azure Active Directory необходимо tooselect **Azure Active Directory** как hello метод предварительной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="70ea3-108">toouse Azure Active Directory for single sign-on tooyour applications, you need tooselect **Azure Active Directory** as hello pre-authentication method.</span></span> <span data-ttu-id="70ea3-109">При выборе **Passthrough** пользователей не аутентификации tooAzure Active Directory, но направленной прямой toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="70ea3-109">If you select **Passthrough** then your users don't authenticate tooAzure Active Directory at all, but are directed straight toohello application.</span></span> <span data-ttu-id="70ea3-110">Этот параметр можно настроить при первой публикации приложения, или перейдите tooyour приложение hello портал Azure и изменить параметры прокси-сервера приложения hello.</span><span class="sxs-lookup"><span data-stu-id="70ea3-110">You can configure this setting when you first publish an application, or navigate tooyour application in hello Azure portal and edit hello Application Proxy settings.</span></span> 

<span data-ttu-id="70ea3-111">toosee единого входа параметры, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="70ea3-111">toosee your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="70ea3-112">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="70ea3-112">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="70ea3-113">Перейдите в слишком**Azure Active Directory** > **корпоративных приложений** > **все приложения**.</span><span class="sxs-lookup"><span data-stu-id="70ea3-113">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="70ea3-114">Приложение SELECT hello, параметры которого единого входа вы хотите toomanage.</span><span class="sxs-lookup"><span data-stu-id="70ea3-114">Select hello app whose single sign-on options you want toomanage.</span></span>
4. <span data-ttu-id="70ea3-115">Щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="70ea3-115">Select **Single sign-on**.</span></span>

   ![Раскрывающееся меню "Единый вход"](./media/application-proxy-sso-overview/single-sign-on-mode.png)

<span data-ttu-id="70ea3-117">Раскрывающееся меню Hello показывает пять вариантов-tooyour приложения:</span><span class="sxs-lookup"><span data-stu-id="70ea3-117">hello dropdown menu shows five options for single sign-on tooyour application:</span></span>

* <span data-ttu-id="70ea3-118">Единый вход Azure AD отключен</span><span class="sxs-lookup"><span data-stu-id="70ea3-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="70ea3-119">Единый вход по паролю</span><span class="sxs-lookup"><span data-stu-id="70ea3-119">Password-based sign-on</span></span>
* <span data-ttu-id="70ea3-120">Связанный единый вход</span><span class="sxs-lookup"><span data-stu-id="70ea3-120">Linked sign-on</span></span>
* <span data-ttu-id="70ea3-121">Встроенная проверка подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="70ea3-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="70ea3-122">Единый входа на основе заголовка</span><span class="sxs-lookup"><span data-stu-id="70ea3-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="70ea3-123">Единый вход Azure AD отключен</span><span class="sxs-lookup"><span data-stu-id="70ea3-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="70ea3-124">Если вы не хотите toouse интеграции Azure Active Directory для-tooyour приложения, выберите **Azure AD единый вход отключен**.</span><span class="sxs-lookup"><span data-stu-id="70ea3-124">If you don't want toouse Azure Active Directory integration for single sign-on tooyour application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="70ea3-125">Если этот параметр выбран, пользователи могут дважды проходить аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="70ea3-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="70ea3-126">Во-первых они проверки подлинности tooAzure Active Directory, а затем войдите в самом приложении toohello.</span><span class="sxs-lookup"><span data-stu-id="70ea3-126">First, they authenticate tooAzure Active Directory and then sign in toohello application itself.</span></span> 

<span data-ttu-id="70ea3-127">Этот параметр является хорошим выбором, если локальные приложения не требует tooauthenticate пользователей, но желательно tooadd Azure Active Directory как уровень безопасности для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="70ea3-127">This option is a good choice if your on-premises application doesn't require users tooauthenticate, but you want tooadd Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="70ea3-128">Единый вход по паролю</span><span class="sxs-lookup"><span data-stu-id="70ea3-128">Password-based sign-on</span></span>

<span data-ttu-id="70ea3-129">Если требуется toouse Azure Active Directory как хранилище паролей для локальных приложений, щелкните **пароль входа на основе**.</span><span class="sxs-lookup"><span data-stu-id="70ea3-129">If you want toouse Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="70ea3-130">Этот параметр удобно использовать, если для аутентификации приложение использует сочетание имени пользователя и пароля, а не маркеры доступа или заголовки.</span><span class="sxs-lookup"><span data-stu-id="70ea3-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="70ea3-131">С использованием пароля входа пользователи должны toosign в toohello приложения hello первом доступе к нему.</span><span class="sxs-lookup"><span data-stu-id="70ea3-131">With password-based sign-on, your users need toosign in toohello application hello first time they access it.</span></span> <span data-ttu-id="70ea3-132">После этого Azure Active Directory предоставляет hello имя пользователя и пароль от имени пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="70ea3-132">After that, Azure Active Directory supplies hello username and password on behalf of hello user.</span></span> 

<span data-ttu-id="70ea3-133">Сведения о настройке входа по паролю см. в разделе [Хранение паролей для единого входа с помощью прокси приложения](application-proxy-sso-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="70ea3-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-sso-azure-portal.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="70ea3-134">Связанный единый вход</span><span class="sxs-lookup"><span data-stu-id="70ea3-134">Linked sign-on</span></span>

<span data-ttu-id="70ea3-135">Если вы уже настроили решение единого входа для своих локальных удостоверений, выберите **Вход по ссылке**.</span><span class="sxs-lookup"><span data-stu-id="70ea3-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="70ea3-136">Этот параметр позволяет Azure Active Directory tooleverage существующими решениями единого входа, но по-прежнему предоставляет пользователям toohello приложение удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="70ea3-136">This option enables Azure Active Directory tooleverage existing SSO solutions, but still gives your users remote access toohello application.</span></span> 

<span data-ttu-id="70ea3-137">Дополнительные сведения о функции связанного входа (существующей функции единого входа) см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="70ea3-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="70ea3-138">Встроенная проверка подлинности Windows</span><span class="sxs-lookup"><span data-stu-id="70ea3-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="70ea3-139">Если локальные приложения используют Authentication(IWA) интеграции Windows, или если требуется toouse ограниченное делегирование Kerberos (KCD) для единого входа, выберите **встроенная проверка подлинности Windows**.</span><span class="sxs-lookup"><span data-stu-id="70ea3-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want toouse Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="70ea3-140">Этот параметр пользователи достаточно tooauthenticate tooAzure Active Directory, и затем соединитель прокси приложения hello олицетворяет пользователя hello tooget маркер Kerberos и входа в приложение toohello.</span><span class="sxs-lookup"><span data-stu-id="70ea3-140">With this option, your users only need tooauthenticate tooAzure Active Directory, and then hello Application Proxy connector impersonates hello user tooget a Kerberos token and sign in toohello application.</span></span> 

<span data-ttu-id="70ea3-141">Сведения о настройке встроенной проверки подлинности Windows см. в разделе [Реализация единого входа в приложения с помощью прокси приложения](active-directory-application-proxy-sso-using-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="70ea3-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="70ea3-142">Единый входа на основе заголовка</span><span class="sxs-lookup"><span data-stu-id="70ea3-142">Header-based sign-on</span></span> 

<span data-ttu-id="70ea3-143">Если приложения используют заголовки для аутентификации, выберите **Вход на основе заголовков**.</span><span class="sxs-lookup"><span data-stu-id="70ea3-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="70ea3-144">Этот параметр пользователи должны только tooauthentication hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70ea3-144">With this option, your users only need tooauthentication hello Azure Active Directory.</span></span> <span data-ttu-id="70ea3-145">Партнеры корпорации Майкрософт с помощью службы проверки подлинности сторонних вызывается PingAccess, который преобразуется в формат заголовка для приложения hello hello маркер доступа Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70ea3-145">Microsoft partners with a third-party authentication service called PingAccess, which translated hello Azure Active Directory access token into a header format for hello application.</span></span> 

<span data-ttu-id="70ea3-146">Сведения о настройке аутентификации на основе заголовка см. в разделе [Публикация приложений с поддержкой аутентификации на основе заголовков с использованием прокси приложения Azure AD и PingAccess](application-proxy-ping-access.md).</span><span class="sxs-lookup"><span data-stu-id="70ea3-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="70ea3-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70ea3-147">Next steps</span></span>

- [<span data-ttu-id="70ea3-148">Хранение паролей для единого входа с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="70ea3-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-sso-azure-portal.md)
- [<span data-ttu-id="70ea3-149">Реализация единого входа в приложения с помощью прокси приложения</span><span class="sxs-lookup"><span data-stu-id="70ea3-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="70ea3-150">Публикация приложений с поддержкой аутентификации на основе заголовков с использованием прокси приложения Azure AD и PingAccess</span><span class="sxs-lookup"><span data-stu-id="70ea3-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-ping-access.md) 
