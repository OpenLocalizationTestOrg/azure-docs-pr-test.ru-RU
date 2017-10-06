---
title: "приложение, в котором тип toouse при добавлении приложения toochoose aaaHow | Документы Microsoft"
description: "Понимать типы hello поддерживается приложений можно интегрировать с Azure AD и их соответствующие параметры настройки"
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
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a><span data-ttu-id="57439-103">Как toochoose приложение, в котором тип toouse при добавлении приложения</span><span class="sxs-lookup"><span data-stu-id="57439-103">How toochoose which application type toouse when adding an application</span></span>

<span data-ttu-id="57439-104">В этой статье, чтобы toounderstand hello четыре основных типа приложений, которые можно интегрировать с Azure AD:</span><span class="sxs-lookup"><span data-stu-id="57439-104">This article help you toounderstand hello four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="57439-105">что они поддерживают;</span><span class="sxs-lookup"><span data-stu-id="57439-105">What is supported by each of them</span></span>
* <span data-ttu-id="57439-106">какой тип приложения следует выбирать;</span><span class="sxs-lookup"><span data-stu-id="57439-106">Why you might choose which application</span></span>
* <span data-ttu-id="57439-107">Tooconfigure основные свойства этих приложений, как пользователи знакомы **подготовить**, или что **единого входа** toouse технологии.</span><span class="sxs-lookup"><span data-stu-id="57439-107">How tooconfigure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology toouse.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="57439-108">Поддерживаемые типы приложений в Azure AD</span><span class="sxs-lookup"><span data-stu-id="57439-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="57439-109">Здравствуйте, Azure AD поддерживает четыре основных типах приложений, которые можно добавить с помощью **добавить** вложенной функции **корпоративных приложений**.</span><span class="sxs-lookup"><span data-stu-id="57439-109">Azure AD supports four main application types that you can add using hello **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="57439-110">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="57439-110">These include:</span></span>

-   <span data-ttu-id="57439-111">**Приложения из коллекции Azure AD** — это предварительно интегрированные приложения для единого входа через Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57439-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="57439-112">**Прокси-сервер приложений-приложения** — приложения, работающего в локальной среде, которые должны tooprovide безопасный единый вход в tooexternally.</span><span class="sxs-lookup"><span data-stu-id="57439-112">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

-   <span data-ttu-id="57439-113">**Сторонних разрабатываемых приложений** — приложение, ваша организация хочет toodevelop на hello платформы разработки приложений Azure AD, но который еще не существует.</span><span class="sxs-lookup"><span data-stu-id="57439-113">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="57439-114">**Приложения не из коллекции** — собственные приложения.</span><span class="sxs-lookup"><span data-stu-id="57439-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="57439-115">Любой веб-ссылка нужные или любого приложения, в которой отображается поле имени пользователя и пароля, поддерживает протокол SAML или OpenID Connect или поддерживает SCIM, который вы хотите toointegrate для единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57439-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a><span data-ttu-id="57439-116">Функции и возможности, поддерживаемые все hello выше типы приложений</span><span class="sxs-lookup"><span data-stu-id="57439-116">Features and capabilities supported by all hello above application types</span></span>

<span data-ttu-id="57439-117">Hello поддерживаются следующие функции по любому hello выше 4 типа приложения в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="57439-117">hello following features are supported by any of hello above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="57439-118">**Быстрый запуск.** Быстро приступите к работе с приложением, выполнив [простые шаги по развертыванию](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started).</span><span class="sxs-lookup"><span data-stu-id="57439-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="57439-119">**Общие свойства управления** — получить [прямой прямой ссылки](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) приложения tooan [Настройка фирменной символики hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) приложения, или [отключить приложение hello](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="57439-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan application, [customize hello branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable hello application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="57439-120">**Управление пользователями и группами** — [назначить](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) или [удалить](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) tooan приложения пользователям и группам и при необходимости назначить hello определенные роли приложения эти пользователи и группы имеют доступ к</span><span class="sxs-lookup"><span data-stu-id="57439-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups tooan application, and optionally assign hello specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="57439-121">**Доступ к приложению самообслуживания** — включить вашей toorequest пользователей [доступа к приложению самообслуживания](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) панелями tooan приложения из их доступа к приложениям, либо путем добавления приложения непосредственно или [ присоединение группы включена самообслуживания](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), при необходимости требования бизнеса утверждения вдоль hello способом</span><span class="sxs-lookup"><span data-stu-id="57439-121">**Self-service application access** – enable your users toorequest [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along hello way</span></span>

-   <span data-ttu-id="57439-122">**Журналы вход** — в разделе [все hello приложения tooan входа в систему](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), или во всех приложениях</span><span class="sxs-lookup"><span data-stu-id="57439-122">**Sign-in logs** – see [all hello sign-ins tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="57439-123">**Журналы аудита** — в разделе [подробные журналы аудита о приложении tooan изменения](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), или tooall приложений</span><span class="sxs-lookup"><span data-stu-id="57439-123">**Audit logs** – see [detailed audit logs about modifications tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or tooall your applications</span></span>

-   <span data-ttu-id="57439-124">**Основе риска и условного доступа** — мощный задайте [правила доступа на основе условий](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) , применяются при обращении пользователей toosign в конкретном приложении tooa</span><span class="sxs-lookup"><span data-stu-id="57439-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt toosign in tooa specific application</span></span>

-   <span data-ttu-id="57439-125">**Просмотр разрешений** — просматривать любые hello [разрешения OAuth2](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) приложение имеет доступ tooin каталог из одного места</span><span class="sxs-lookup"><span data-stu-id="57439-125">**Permissions view** – view any of hello [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access tooin your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="57439-126">Режимы единого входа и подготовки, поддерживаемые конкретными типами приложений</span><span class="sxs-lookup"><span data-stu-id="57439-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="57439-127">в следующей таблице Hello описывает hello различных единого входа и подготовки режимов, поддерживаемых каждым hello выше типов приложений.</span><span class="sxs-lookup"><span data-stu-id="57439-127">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="57439-128">Можно использовать этот toohelp таблицы toounderstand приложение, в котором требуется tooadd toosupport определенную задачу.</span><span class="sxs-lookup"><span data-stu-id="57439-128">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![Таблица типов приложений](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="57439-130">Как toochoose режима единого входа</span><span class="sxs-lookup"><span data-stu-id="57439-130">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="57439-131">Hello поддерживается **единого входа** режимы для приложения Azure AD, перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="57439-131">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="57439-132">**Azure AD единый вход отключен** — выберите Azure AD единый вход отключен **режим-** Если вы еще не готова toointegrate это приложение с единым входом в Azure AD, или производится проверка только его</span><span class="sxs-lookup"><span data-stu-id="57439-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="57439-133">**Связанные входа** — выберите hello [входа на связанный](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **режим-** при наличии приложения, который уже связан с существующего единого входа для решения, или если необходимо просто toopublish простой ссылки для пользователей в их [панели доступа приложения](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) или [запуска приложений Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="57439-133">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="57439-134">**Пароль входа на основе** — выберите hello [входа на базе пароля](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **режим-** Если приложение отображает HTML-поле имени пользователя и пароля и toostore, имя пользователя и пароль безопасно toobe в дополнительной воспроизведены toohello приложения позже</span><span class="sxs-lookup"><span data-stu-id="57439-134">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="57439-135">**На основе SAML единого входа** — выберите hello [входа на базе SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) на основе ролей приложения toospecific единый вход в режим, если приложение поддерживает протокол SAML или OpenID Connect hello, или пользователи могут toomap toobe на правилах, определенных в вашей SAML утверждений *</span><span class="sxs-lookup"><span data-stu-id="57439-135">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="57439-136">Этот параметр недоступен при настройке прокси-сервера приложения hello для приложения.</span><span class="sxs-lookup"><span data-stu-id="57439-136">This option is not available when hello application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="57439-137">**Заголовок входа на основе** — выберите этот параметр, [входа на базе заголовок](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) единого входа режим при наличии приложения с помощью PingAccess, которая поддерживает заголовок HTTP на основе проверки подлинности, на котором необходимо tooperform единого входа на слишком</span><span class="sxs-lookup"><span data-stu-id="57439-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="57439-138">Этот параметр доступен только при настройке прокси-сервера приложения hello и PingAccess для приложения.</span><span class="sxs-lookup"><span data-stu-id="57439-138">This option is only available when hello application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="57439-139">**Встроенная проверка подлинности Windows** — выберите hello [встроенная проверка подлинности Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) единый вход в режим при предоставлении WIA приложения локально, на котором необходимо tooperform единого входа на слишком</span><span class="sxs-lookup"><span data-stu-id="57439-139">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="57439-140">Этот параметр доступен только при настройке прокси-сервера приложения hello для приложения.</span><span class="sxs-lookup"><span data-stu-id="57439-140">This option is only available when hello application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="57439-141">Режимы единого входа для специально разработанных приложений</span><span class="sxs-lookup"><span data-stu-id="57439-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="57439-142">Приложения имеют пользовательский при hello [приложения, разработанного](#_Custom-Developed_Applications) качества также поддерживают дополнительных единого входа режима не перечисленные выше.</span><span class="sxs-lookup"><span data-stu-id="57439-142">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="57439-143">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="57439-143">These include:</span></span>

-   <span data-ttu-id="57439-144">единый вход на основе [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code);</span><span class="sxs-lookup"><span data-stu-id="57439-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="57439-145">единый вход на основе [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code);</span><span class="sxs-lookup"><span data-stu-id="57439-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="57439-146">единый вход на основе [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html);</span><span class="sxs-lookup"><span data-stu-id="57439-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="57439-147">единый вход на основе [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span><span class="sxs-lookup"><span data-stu-id="57439-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="57439-148">Чтение hello [руководство разработчика Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn Дополнительные сведения о как toocreate, разработанного приложения, который поддерживает эти единого входа режимов.</span><span class="sxs-lookup"><span data-stu-id="57439-148">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="57439-149">Как tooset приложения одного режима входа</span><span class="sxs-lookup"><span data-stu-id="57439-149">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="57439-150">tooset приложения **единого входа** режим, выполните приведенные ниже инструкции hello:</span><span class="sxs-lookup"><span data-stu-id="57439-150">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="57439-151">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="57439-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="57439-152">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="57439-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="57439-153">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="57439-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="57439-154">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="57439-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="57439-155">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="57439-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="57439-156">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="57439-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="57439-157">Выберите приложение hello, для которого требуется tooconfigure единого входа.</span><span class="sxs-lookup"><span data-stu-id="57439-157">Select hello application for which you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="57439-158">После загрузки приложения hello щелкните **единого входа** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="57439-158">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="how-toochoose-a-provisioning-mode"></a><span data-ttu-id="57439-159">Как toochoose режим подготовки</span><span class="sxs-lookup"><span data-stu-id="57439-159">How toochoose a provisioning mode</span></span>

-   <span data-ttu-id="57439-160">**Идет подготовка вручную** — выберите hello [вручную](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) режима подготовки, если имеются существующие учетные записи, или если нужна toomanage учетных записей для этого приложения за пределами Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57439-160">**Manual Provisioning** – choose hello [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish toomanage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="57439-161">**Автоматическая подготовка** — выберите hello [автоматического](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **режим подготовки** Если tooenable инициализации автоматического на основе API и/или отменить подготовку учетных записей пользователей toothis приложения</span><span class="sxs-lookup"><span data-stu-id="57439-161">**Automatic Provisioning** – choose hello [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want tooenable automatic API-based provisioning and/or de-provisioning of user accounts toothis application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="57439-162">Этот параметр доступен только для приложений в пределах hello **избранные** категории hello [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="57439-162">This option is available only for applications within hello **featured** category of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="57439-163">**На основе SCIM автоматическую подготовку** — использовать [на основе SCIM автоматическую подготовку](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) Если приложение поддерживает протокол SCIM hello обнаружения изменений toousers и групп, которые создаются автоматически для изменения tooany приложения, интегрированного с Azure AD</span><span class="sxs-lookup"><span data-stu-id="57439-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports hello SCIM protocol for detecting changes toousers and groups, which are automatically emitted for changes tooany application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="57439-164">Этот параметр не является определенным режимом подготовки, но он включен по умолчанию для всех приложений, интегрированных с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57439-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a><span data-ttu-id="57439-165">Способ подготовки режим tooset приложения</span><span class="sxs-lookup"><span data-stu-id="57439-165">How tooset an application’s provisioning mode</span></span>

<span data-ttu-id="57439-166">tooset приложения **Подготовка** режиме, выполните приведенные ниже инструкции hello:</span><span class="sxs-lookup"><span data-stu-id="57439-166">tooset an application’s **provisioning** mode, follow hello instructions below:</span></span>

<span data-ttu-id="57439-167">tooset приложения **единого входа** режим, выполните приведенные ниже инструкции hello:</span><span class="sxs-lookup"><span data-stu-id="57439-167">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="57439-168">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора** или **Co-администратору.**</span><span class="sxs-lookup"><span data-stu-id="57439-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="57439-169">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="57439-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="57439-170">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="57439-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="57439-171">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="57439-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="57439-172">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="57439-172">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="57439-173">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="57439-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="57439-174">Выберите приложение hello, для которого требуется tooconfigure подготовки.</span><span class="sxs-lookup"><span data-stu-id="57439-174">Select hello application for which you want tooconfigure provisioning.</span></span>

7.  <span data-ttu-id="57439-175">После загрузки приложения hello щелкните **Provisioning** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="57439-175">Once hello application loads, click **Provisioning** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57439-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57439-176">Next steps</span></span>
[<span data-ttu-id="57439-177">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="57439-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
