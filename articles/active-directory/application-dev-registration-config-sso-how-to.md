---
title: "aaaHow tooconfigure новый многопользовательского приложения | Документы Microsoft"
description: "Как tooconfigure единого входа для пользовательского приложения разработки и регистрации в Azure AD."
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
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="6c12a-103">Как tooconfigure новый многопользовательского приложения</span><span class="sxs-lookup"><span data-stu-id="6c12a-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="6c12a-104">При настройке федерации с помощью Azure AD для OpenID Connect, SAML 2.0 или WS-Fed федеративный единый вход для вашего приложения включается автоматически.</span><span class="sxs-lookup"><span data-stu-id="6c12a-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="6c12a-105">Если конечные пользователи возникают toosign вне зависимости от уже существующего сеанса в Azure AD, весьма вероятно, неправильно приложения.</span><span class="sxs-lookup"><span data-stu-id="6c12a-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="6c12a-106">Если вы используете ADAL/MSAL, убедитесь, что у вас есть **PromptBehavior** значение слишком**автоматически** вместо **всегда**.</span><span class="sxs-lookup"><span data-stu-id="6c12a-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="6c12a-107">При создании мобильного приложения, может потребоваться дополнительные настройки tooenable через посредника или не посредника единого входа.</span><span class="sxs-lookup"><span data-stu-id="6c12a-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="6c12a-108">Для Android см. раздел [Включение единого входа для нескольких приложений в Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="6c12a-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="6c12a-109">Для iOS см. раздел [Включение единого входа для нескольких приложений в iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="6c12a-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c12a-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c12a-110">Next steps</span></span>

[<span data-ttu-id="6c12a-111">Единый вход в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c12a-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="6c12a-112">Включение единого входа для нескольких приложений в Android</span><span class="sxs-lookup"><span data-stu-id="6c12a-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="6c12a-113">Включение единого входа для нескольких приложений в iOS</span><span class="sxs-lookup"><span data-stu-id="6c12a-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="6c12a-114">Интеграция приложений tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="6c12a-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="6c12a-115">Согласие и разрешения для конвергированных приложений в Azure AD версии 2.0</span><span class="sxs-lookup"><span data-stu-id="6c12a-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="6c12a-116">StackOverflow в AzureAD</span><span class="sxs-lookup"><span data-stu-id="6c12a-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
