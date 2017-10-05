---
title: "Настройка нового мультитенантного приложения | Документы Майкрософт"
description: "В этой статье описано, как настроить единый вход для пользовательского приложения, которое вы разрабатываете, и зарегистрировать это приложение в Azure AD."
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
ms.openlocfilehash: 0fdc58d82d9cd2e7edac33cc5af4b98d2fd06c56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="1ad6d-103">Настройка нового мультитенантного приложения</span><span class="sxs-lookup"><span data-stu-id="1ad6d-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="1ad6d-104">При настройке федерации с помощью Azure AD для OpenID Connect, SAML 2.0 или WS-Fed федеративный единый вход для вашего приложения включается автоматически.</span><span class="sxs-lookup"><span data-stu-id="1ad6d-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="1ad6d-105">Если конечным пользователям приходится снова входить в систему несмотря на то, что сеанс Azure AD уже существует, возможно, приложение настроено неправильно.</span><span class="sxs-lookup"><span data-stu-id="1ad6d-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="1ad6d-106">Если вы используете ADAL и MSAL, убедитесь, что параметр **PromptBehavior** имеет значение **Auto**, а не **Always**.</span><span class="sxs-lookup"><span data-stu-id="1ad6d-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="1ad6d-107">При создании мобильного приложения для включения единого входа с использованием или без использования брокера может потребоваться дополнительная настройка.</span><span class="sxs-lookup"><span data-stu-id="1ad6d-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="1ad6d-108">Для Android см. раздел [Включение единого входа для нескольких приложений в Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="1ad6d-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="1ad6d-109">Для iOS см. раздел [Включение единого входа для нескольких приложений в iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="1ad6d-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ad6d-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ad6d-110">Next steps</span></span>

[<span data-ttu-id="1ad6d-111">Единый вход в Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad6d-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="1ad6d-112">Включение единого входа для нескольких приложений в Android</span><span class="sxs-lookup"><span data-stu-id="1ad6d-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="1ad6d-113">Включение единого входа для нескольких приложений в iOS</span><span class="sxs-lookup"><span data-stu-id="1ad6d-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="1ad6d-114">Интеграция приложений с Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad6d-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="1ad6d-115">Согласие и разрешения для конвергированных приложений в Azure AD версии 2.0</span><span class="sxs-lookup"><span data-stu-id="1ad6d-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="1ad6d-116">StackOverflow в AzureAD</span><span class="sxs-lookup"><span data-stu-id="1ad6d-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
