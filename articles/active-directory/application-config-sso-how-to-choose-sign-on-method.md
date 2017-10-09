---
title: "aaaHow toodetermine какие единого входа на метод toouse | Документы Microsoft"
description: "Понимать hello единого входа режимы, поддерживаемые Azure AD и как toopick приложения hello какие один toochoose для вас интересуют."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a><span data-ttu-id="fb789-103">Как toodetermine какие единого входа на метод toouse</span><span class="sxs-lookup"><span data-stu-id="fb789-103">How toodetermine what single-sign on method toouse</span></span>

<span data-ttu-id="fb789-104">В этой статье помогут toounderstand hello единого входа режимы, поддерживаемые Azure AD и как toopick приложения hello какие один toochoose для вас интересуют.</span><span class="sxs-lookup"><span data-stu-id="fb789-104">This article help you toounderstand hello single sign-on modes supported by Azure AD and how toopick which one toochoose for hello application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="fb789-105">Режимы единого входа и подготовки, поддерживаемые конкретными типами приложений</span><span class="sxs-lookup"><span data-stu-id="fb789-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="fb789-106">в следующей таблице Hello описывает hello различных единого входа и подготовки режимов, поддерживаемых каждым hello выше типов приложений.</span><span class="sxs-lookup"><span data-stu-id="fb789-106">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="fb789-107">Можно использовать этот toohelp таблицы toounderstand приложение, в котором требуется tooadd toosupport определенную задачу.</span><span class="sxs-lookup"><span data-stu-id="fb789-107">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![Таблица типов приложений](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="fb789-109">Как toochoose режима единого входа</span><span class="sxs-lookup"><span data-stu-id="fb789-109">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="fb789-110">Hello поддерживается **единого входа** режимы для приложения Azure AD, перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="fb789-110">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="fb789-111">**Azure AD единый вход отключен** — выберите Azure AD единый вход отключен **режим-** Если вы еще не готова toointegrate это приложение с единым входом в Azure AD, или производится проверка только его</span><span class="sxs-lookup"><span data-stu-id="fb789-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="fb789-112">**Связанные входа** — выберите hello [входа на связанный](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **режим-** при наличии приложения, который уже связан с существующего единого входа для решения, или если необходимо просто toopublish простой ссылки для пользователей в их [панели доступа приложения](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) или [запуска приложений Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="fb789-112">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="fb789-113">**Пароль входа на основе** — выберите hello [входа на базе пароля](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **режим-** Если приложение отображает HTML-поле имени пользователя и пароля и toostore, имя пользователя и пароль безопасно toobe в дополнительной воспроизведены toohello приложения позже</span><span class="sxs-lookup"><span data-stu-id="fb789-113">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="fb789-114">**На основе SAML единого входа** — выберите hello [входа на базе SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) на основе ролей приложения toospecific единый вход в режим, если приложение поддерживает протокол SAML или OpenID Connect hello, или пользователи могут toomap toobe на правилах, определенных в вашей SAML утверждений *(**Примечание:** этот параметр недоступен при настройке прокси-сервера приложения hello для приложения) *</span><span class="sxs-lookup"><span data-stu-id="fb789-114">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *(**Note:** this option is not available when hello application proxy is configured for an application)*</span></span>

-   <span data-ttu-id="fb789-115">**Заголовок входа на основе** — выберите этот параметр, [входа на базе заголовок](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) единого входа режим при наличии приложения с помощью PingAccess, которая поддерживает заголовок HTTP на основе проверки подлинности, на котором необходимо tooperform единого входа на слишком *(**Примечание:** этот параметр доступен только при настройке прокси-сервера приложения hello и PingAccess для приложения) *</span><span class="sxs-lookup"><span data-stu-id="fb789-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too*(**Note:** this option is only available when hello application proxy and PingAccess is configured for an application)*</span></span>

-   <span data-ttu-id="fb789-116">**Встроенная проверка подлинности Windows** — выберите hello [встроенная проверка подлинности Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) единый вход в режим при предоставлении WIA приложения локально, на котором необходимо tooperform единого входа на слишком*()*  *Примечание:** этот параметр доступен только при настройке прокси-сервера приложения hello для приложения) *</span><span class="sxs-lookup"><span data-stu-id="fb789-116">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too*(**Note:** this option is only available when hello application proxy is configured for an application)*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="fb789-117">Режимы единого входа для специально разработанных приложений</span><span class="sxs-lookup"><span data-stu-id="fb789-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="fb789-118">Приложения имеют пользовательский при hello [приложения, разработанного](#_Custom-Developed_Applications) качества также поддерживают дополнительных единого входа режима не перечисленные выше.</span><span class="sxs-lookup"><span data-stu-id="fb789-118">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="fb789-119">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="fb789-119">These include:</span></span>

-   <span data-ttu-id="fb789-120">единый вход на основе [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code);</span><span class="sxs-lookup"><span data-stu-id="fb789-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="fb789-121">единый вход на основе [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code);</span><span class="sxs-lookup"><span data-stu-id="fb789-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="fb789-122">единый вход на основе [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html);</span><span class="sxs-lookup"><span data-stu-id="fb789-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="fb789-123">единый вход на основе [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span><span class="sxs-lookup"><span data-stu-id="fb789-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="fb789-124">Чтение hello [руководство разработчика Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn Дополнительные сведения о как toocreate, разработанного приложения, который поддерживает эти единого входа режимов.</span><span class="sxs-lookup"><span data-stu-id="fb789-124">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="fb789-125">Как tooset приложения одного режима входа</span><span class="sxs-lookup"><span data-stu-id="fb789-125">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="fb789-126">tooset приложения **единого входа** режим, выполните приведенные ниже инструкции hello:</span><span class="sxs-lookup"><span data-stu-id="fb789-126">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="fb789-127">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="fb789-127">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="fb789-128">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="fb789-128">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="fb789-129">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="fb789-129">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="fb789-130">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="fb789-130">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="fb789-131">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="fb789-131">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="fb789-132">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="fb789-132">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="fb789-133">Выберите hello приложение tooconfigure единого входа</span><span class="sxs-lookup"><span data-stu-id="fb789-133">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="fb789-134">После загрузки приложения hello щелкните **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="fb789-134">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb789-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fb789-135">Next steps</span></span>
[<span data-ttu-id="fb789-136">Создавайте приложения tooyour, прокси-сервера приложений</span><span class="sxs-lookup"><span data-stu-id="fb789-136">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

