---
title: "Как выбрать нужный тип приложения при добавлении приложения | Документация Майкрософт"
description: "Сведения о поддерживаемых типах приложений, которые можно интегрировать с Azure AD, и о вариантах их настройки"
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
ms.openlocfilehash: e0d41d1933531c2c633613bcbc1bbcbf075d6a69
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-choose-which-application-type-to-use-when-adding-an-application"></a><span data-ttu-id="c27e1-103">Как выбрать нужный тип приложения при добавлении приложения</span><span class="sxs-lookup"><span data-stu-id="c27e1-103">How to choose which application type to use when adding an application</span></span>

<span data-ttu-id="c27e1-104">Из этой статьи вы узнаете о четырех основных типах приложений, которые можно интегрировать с Azure AD, а также:</span><span class="sxs-lookup"><span data-stu-id="c27e1-104">This article help you to understand the four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="c27e1-105">что они поддерживают;</span><span class="sxs-lookup"><span data-stu-id="c27e1-105">What is supported by each of them</span></span>
* <span data-ttu-id="c27e1-106">какой тип приложения следует выбирать;</span><span class="sxs-lookup"><span data-stu-id="c27e1-106">Why you might choose which application</span></span>
* <span data-ttu-id="c27e1-107">как настроить основные свойства этих приложений, например **метод подготовки** пользователей или используемую технологию **единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-107">How to configure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology to use.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="c27e1-108">Поддерживаемые типы приложений в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c27e1-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="c27e1-109">Azure AD поддерживает четыре основных типа приложений, которые можно добавить с помощью команды **Добавить** в разделе **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-109">Azure AD supports four main application types that you can add using the **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="c27e1-110">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="c27e1-110">These include:</span></span>

-   <span data-ttu-id="c27e1-111">**Приложения из коллекции Azure AD** — это предварительно интегрированные приложения для единого входа через Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27e1-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="c27e1-112">**Приложения прокси приложения** — приложения, работающее в локальной среде, которым необходимо предоставить безопасный единый вход извне.</span><span class="sxs-lookup"><span data-stu-id="c27e1-112">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

-   <span data-ttu-id="c27e1-113">**Специально разработанные приложения** — приложения, которые ваша организация намерена разработать на платформе разработки приложений Azure AD, но, возможно, они еще находятся на стадии обсуждения.</span><span class="sxs-lookup"><span data-stu-id="c27e1-113">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="c27e1-114">**Приложения не из коллекции** — собственные приложения.</span><span class="sxs-lookup"><span data-stu-id="c27e1-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="c27e1-115">Сюда относится любая нужная веб-ссылка или любое приложение, отображающее поле имени пользователя и пароля и поддерживающее протоколы SAML, OpenID Connect или систему SCIM, которое нужно интегрировать для единого входа через Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27e1-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-the-above-application-types"></a><span data-ttu-id="c27e1-116">Функции и возможности, поддерживаемые приведенными выше типами приложений</span><span class="sxs-lookup"><span data-stu-id="c27e1-116">Features and capabilities supported by all the above application types</span></span>

<span data-ttu-id="c27e1-117">Следующие функции поддерживают приложения всех четырех типов в Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c27e1-117">The following features are supported by any of the above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="c27e1-118">**Быстрый запуск.** Быстро приступите к работе с приложением, выполнив [простые шаги по развертыванию](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started).</span><span class="sxs-lookup"><span data-stu-id="c27e1-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="c27e1-119">**Управление общими свойствами.** Получите [прямую ссылку](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) на приложение, [настройте фирменную символику](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) приложения или [отключите приложение](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) для всех пользователей.</span><span class="sxs-lookup"><span data-stu-id="c27e1-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) to an application, [customize the branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable the application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="c27e1-120">**Управление пользователями и группами.** [Назначьте](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) или [удалите](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) пользователей и группы в приложении и при необходимости назначьте им конкретные роли, к которым они будут иметь доступ.</span><span class="sxs-lookup"><span data-stu-id="c27e1-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups to an application, and optionally assign the specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="c27e1-121">**Самостоятельный доступ к приложениям.** Разрешите пользователям запрашивать [самостоятельный доступ к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) с помощью панели доступа к приложениям. Для этого добавьте приложение напрямую или [присоедините группу с самостоятельным доступом](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), при необходимости настроив бизнес-утверждение.</span><span class="sxs-lookup"><span data-stu-id="c27e1-121">**Self-service application access** – enable your users to request [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) to an application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along the way</span></span>

-   <span data-ttu-id="c27e1-122">**Журналы входа**. Просмотрите [все операции входа в приложение](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) или приложения.</span><span class="sxs-lookup"><span data-stu-id="c27e1-122">**Sign-in logs** – see [all the sign-ins to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="c27e1-123">**Журналы аудита.** Просмотрите [подробные журналы аудита изменений в приложении](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) или приложениях.</span><span class="sxs-lookup"><span data-stu-id="c27e1-123">**Audit logs** – see [detailed audit logs about modifications to an application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or to all your applications</span></span>

-   <span data-ttu-id="c27e1-124">**Условный доступ и доступ на основе рисков.** Задайте эффективные [правила доступа на основе условия](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access), применяющиеся при попытке входа пользователей в конкретное приложение.</span><span class="sxs-lookup"><span data-stu-id="c27e1-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt to sign in to a specific application</span></span>

-   <span data-ttu-id="c27e1-125">**Представление разрешений.** Просмотрите все [разрешения OAuth2](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent), к которым приложение имеет доступ в вашем каталоге, из одного расположения.</span><span class="sxs-lookup"><span data-stu-id="c27e1-125">**Permissions view** – view any of the [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access to in your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="c27e1-126">Режимы единого входа и подготовки, поддерживаемые конкретными типами приложений</span><span class="sxs-lookup"><span data-stu-id="c27e1-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="c27e1-127">В следующей таблице описываются различные режимы единого входа и подготовки, поддерживаемые каждым из приведенных выше типов приложений.</span><span class="sxs-lookup"><span data-stu-id="c27e1-127">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="c27e1-128">С ее помощью вы можете определить, какое приложение необходимо добавить для достижения конкретной цели.</span><span class="sxs-lookup"><span data-stu-id="c27e1-128">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![Таблица типов приложений](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="c27e1-130">Как выбрать режим единого входа</span><span class="sxs-lookup"><span data-stu-id="c27e1-130">How to choose a single sign-on mode</span></span>

<span data-ttu-id="c27e1-131">Ниже приведены поддерживаемые режимы **единого входа** для приложений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27e1-131">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="c27e1-132">**Единый вход Azure AD отключен.** Выберите **режим** "Единый вход Azure AD отключен", если вы еще не готовы к интеграции этого приложения с единым входом в Azure AD или просто его тестируете.</span><span class="sxs-lookup"><span data-stu-id="c27e1-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="c27e1-133">**Вход по ссылке**. Выберите **режим** [Вход по ссылке](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) при наличии приложения, уже подключенного с использованием решения единого входа, или если требуется опубликовать простую ссылку для пользователей на [панели доступа к приложениям](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) или в [средстве запуска приложений Office 365](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none).</span><span class="sxs-lookup"><span data-stu-id="c27e1-133">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="c27e1-134">**Вход по паролю**. Выберите **режим единого входа** [Вход по паролю](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work), если приложение отображает HTML-поле имени пользователя и пароля, а также если необходимо безопасно сохранить имя пользователя и пароль для их повторного использования в приложении.</span><span class="sxs-lookup"><span data-stu-id="c27e1-134">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="c27e1-135">**Вход на основе SAML**. Выберите режим единого входа [Вход на основе SAML](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work), если приложение поддерживает протоколы SAML или OpenID Connect или если вам нужно сопоставить пользователей с конкретными ролями приложений на основе правил, определенных в утверждениях SAML*.</span><span class="sxs-lookup"><span data-stu-id="c27e1-135">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="c27e1-136">Этот параметр недоступен, если для приложения настроен прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="c27e1-136">This option is not available when the application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="c27e1-137">**Вход на основе заголовков**. Выберите режим единого входа [Вход на основе заголовков](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad), если вам необходимо выполнить единый вход для приложения, использующего решение PingAccess с поддержкой проверки подлинности на основе HTTP-заголовка.</span><span class="sxs-lookup"><span data-stu-id="c27e1-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="c27e1-138">Этот параметр доступен только, если для приложения настроен прокси приложения и PingAccess.</span><span class="sxs-lookup"><span data-stu-id="c27e1-138">This option is only available when the application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="c27e1-139">**Интегрированная проверка подлинности Windows**. Выберите режим единого входа [Интегрированная проверка подлинности Windows](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) при использовании локального приложения WIA, для которого необходимо выполнить единый вход.</span><span class="sxs-lookup"><span data-stu-id="c27e1-139">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to</span></span> 

   >[!NOTE]
   ><span data-ttu-id="c27e1-140">Этот параметр доступен, только если для приложения настроен прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="c27e1-140">This option is only available when the application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="c27e1-141">Режимы единого входа для специально разработанных приложений</span><span class="sxs-lookup"><span data-stu-id="c27e1-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="c27e1-142">[Специально разработанные приложения](#_Custom-Developed_Applications) также поддерживают дополнительные режимы единого входа, не указанные в списке выше.</span><span class="sxs-lookup"><span data-stu-id="c27e1-142">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="c27e1-143">В частности, описаны такие возможности:</span><span class="sxs-lookup"><span data-stu-id="c27e1-143">These include:</span></span>

-   <span data-ttu-id="c27e1-144">единый вход на основе [OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code);</span><span class="sxs-lookup"><span data-stu-id="c27e1-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="c27e1-145">единый вход на основе [OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code);</span><span class="sxs-lookup"><span data-stu-id="c27e1-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="c27e1-146">единый вход на основе [WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html);</span><span class="sxs-lookup"><span data-stu-id="c27e1-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="c27e1-147">единый вход на основе [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span><span class="sxs-lookup"><span data-stu-id="c27e1-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="c27e1-148">Ознакомьтесь с [руководством разработчика по Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide), чтобы узнать больше о создании специально разработанного приложения, поддерживающего данные режимы единого входа.</span><span class="sxs-lookup"><span data-stu-id="c27e1-148">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="c27e1-149">Настройка режима единого входа для приложения</span><span class="sxs-lookup"><span data-stu-id="c27e1-149">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="c27e1-150">Чтобы настроить режим **единого входа** для приложения, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c27e1-150">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="c27e1-151">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-151">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c27e1-152">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c27e1-152">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c27e1-153">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-153">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c27e1-154">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-154">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c27e1-155">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="c27e1-155">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="c27e1-156">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-156">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c27e1-157">Выберите приложение, для которого необходимо настроить единый вход.</span><span class="sxs-lookup"><span data-stu-id="c27e1-157">Select the application for which you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="c27e1-158">После загрузки приложения выберите для этого приложения пункт **Единый вход** в меню навигации слева.</span><span class="sxs-lookup"><span data-stu-id="c27e1-158">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="how-to-choose-a-provisioning-mode"></a><span data-ttu-id="c27e1-159">Как выбрать режим подготовки</span><span class="sxs-lookup"><span data-stu-id="c27e1-159">How to choose a provisioning mode</span></span>

-   <span data-ttu-id="c27e1-160">**Ручная подготовка.** Выберите режим подготовки [Вручную](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes), если у вас есть учетные записи или необходимо управлять учетными записями приложения за пределами Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27e1-160">**Manual Provisioning** – choose the [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish to manage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="c27e1-161">**Автоматическая подготовка.** Выберите **режим подготовки** [Автоматически](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning), если необходимо включить автоматическую подготовку на основе API или отмену подготовки учетных записей пользователей для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="c27e1-161">**Automatic Provisioning** – choose the [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want to enable automatic API-based provisioning and/or de-provisioning of user accounts to this application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="c27e1-162">Этот параметр доступен только для приложений, находящихся в категории **избранных** [коллекции приложений Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="c27e1-162">This option is available only for applications within the **featured** category of the [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="c27e1-163">**Автоматическая подготовка на основе SCIM.** Выберите этот [режим подготовки](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning), если приложение поддерживает протокол SCIM для обнаружения изменений пользователей и групп, которые добавляются автоматически в любое приложение, интегрированное с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27e1-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports the SCIM protocol for detecting changes to users and groups, which are automatically emitted for changes to any application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="c27e1-164">Этот параметр не является определенным режимом подготовки, но он включен по умолчанию для всех приложений, интегрированных с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c27e1-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-to-set-an-applications-provisioning-mode"></a><span data-ttu-id="c27e1-165">Как настроить режим подготовки для приложения</span><span class="sxs-lookup"><span data-stu-id="c27e1-165">How to set an application’s provisioning mode</span></span>

<span data-ttu-id="c27e1-166">Чтобы настроить режим **подготовки** для приложения,</span><span class="sxs-lookup"><span data-stu-id="c27e1-166">To set an application’s **provisioning** mode, follow the instructions below:</span></span>

<span data-ttu-id="c27e1-167">сделайте **следующее**:</span><span class="sxs-lookup"><span data-stu-id="c27e1-167">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="c27e1-168">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор** или **соадминистратор**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="c27e1-169">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="c27e1-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="c27e1-170">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="c27e1-171">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="c27e1-172">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="c27e1-172">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="c27e1-173">Если нужное приложение отсутствует в списке, воспользуйтесь элементом управления **Фильтр** в верхней части списка **Все приложения**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c27e1-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="c27e1-174">Выберите приложение, для которого необходимо настроить подготовку.</span><span class="sxs-lookup"><span data-stu-id="c27e1-174">Select the application for which you want to configure provisioning.</span></span>

7.  <span data-ttu-id="c27e1-175">После загрузки приложения щелкните **Подготовка** в меню навигации слева.</span><span class="sxs-lookup"><span data-stu-id="c27e1-175">Once the application loads, click **Provisioning** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c27e1-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c27e1-176">Next steps</span></span>
[<span data-ttu-id="c27e1-177">Управление приложениями с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c27e1-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
