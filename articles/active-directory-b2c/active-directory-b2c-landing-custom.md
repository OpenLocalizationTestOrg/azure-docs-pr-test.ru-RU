---
title: "Azure Active Directory B2C. Целевая страница пользовательских политик | Документация Майкрософт"
description: "Разработка потребительских приложений с Azure Active Directory B2C с помощью пользовательских политик."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f2079f53-a637-4f2d-b3a0-61a9647ad433
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 5/06/2017
ms.author: parakhj
ms.openlocfilehash: 28a39f282488b81fc9e2ab7841b5f2cb4cd58715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-up-and-sign-in-consumers-in-your-applications-using-custom-policies"></a><span data-ttu-id="e6386-103">Azure Active Directory B2C. Регистрация и вход пользователей в приложения с помощью пользовательских политик</span><span class="sxs-lookup"><span data-stu-id="e6386-103">Azure Active Directory B2C: Sign up and sign in consumers in your applications using custom policies</span></span>
<span data-ttu-id="e6386-104">Настраиваемые политики, файлы конфигурации, которые определяют поведение hello вашего клиента Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="e6386-104">Custom policies are configuration files that define hello behavior of your Azure AD B2C tenant.</span></span> <span data-ttu-id="e6386-105">Их можно полностью изменить с помощью удостоверения разработчика toocomplete практически неограниченное количество задач.</span><span class="sxs-lookup"><span data-stu-id="e6386-105">They can be fully edited by an identity developer toocomplete a near unlimited number of tasks.</span></span>

## <a name="how-tooarticles"></a><span data-ttu-id="e6386-106">Как tooarticles</span><span class="sxs-lookup"><span data-stu-id="e6386-106">How-tooarticles</span></span>
<span data-ttu-id="e6386-107">Узнайте, как отдельные функции Azure Active Directory B2C toouse:</span><span class="sxs-lookup"><span data-stu-id="e6386-107">Learn how toouse specific Azure Active Directory B2C features:</span></span>

* [<span data-ttu-id="e6386-108">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="e6386-108">Get Started</span></span>](active-directory-b2c-overview-custom.md)
* <span data-ttu-id="e6386-109">Настройка поставщиков OIDC, например [Azure AD](active-directory-b2c-setup-aad-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6386-109">Configure OIDC Providers such as [Azure AD](active-directory-b2c-setup-aad-custom.md).</span></span>
* <span data-ttu-id="e6386-110">Настройка поставщиков SAML, например [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6386-110">Configure SAML Providers such as [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span></span>
* <span data-ttu-id="e6386-111">Интеграции API-интерфейсов RESTful:</span><span class="sxs-lookup"><span data-stu-id="e6386-111">Integrate RESTful APIs:</span></span>
    * <span data-ttu-id="e6386-112">[Пошаговое руководство по интеграции обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как этапа оркестрации](active-directory-b2c-rest-api-step-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6386-112">[Obtain additional claims](active-directory-b2c-rest-api-step-custom.md).</span></span>
    * <span data-ttu-id="e6386-113">[Пошаговое руководство по интеграции обмена утверждениями REST API в путях взаимодействия пользователей Azure AD B2C как метода проверки входных данных](active-directory-b2c-rest-api-validation-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6386-113">[Validate user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>
* <span data-ttu-id="e6386-114">Настройка имени для входа:</span><span class="sxs-lookup"><span data-stu-id="e6386-114">Customize Login:</span></span>
    * <span data-ttu-id="e6386-115">[Настройка пользовательского ввода](active-directory-b2c-configure-signup-self-asserted-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6386-115">[Configure User Input](active-directory-b2c-configure-signup-self-asserted-custom.md)</span></span>
    * <span data-ttu-id="e6386-116">[Настройка пользовательского интерфейса](active-directory-b2c-ui-customization-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6386-116">[Customize UI](active-directory-b2c-ui-customization-custom.md)</span></span>
    * <span data-ttu-id="e6386-117">[Настройка токена](active-directory-b2c-reference-manage-sso-and-token-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="e6386-117">[Customize Token](active-directory-b2c-reference-manage-sso-and-token-configuration.md)</span></span>
* <span data-ttu-id="e6386-118">Устранение неполадок за счет [сбора журналов с помощью Application Insights](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="e6386-118">Troubleshoot by [collecting logs using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="whats-new"></a><span data-ttu-id="e6386-119">Новые возможности</span><span class="sxs-lookup"><span data-stu-id="e6386-119">What's new</span></span>
<span data-ttu-id="e6386-120">Обратитесь к этому списку часто toolearn о будущих изменений toohello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="e6386-120">Check back here often toolearn about future changes toohello Azure Active Directory B2C.</span></span> <span data-ttu-id="e6386-121">Кроме того, мы будем сообщать о нововведениях в Twitter под именем @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="e6386-121">We'll also tweet about any updates by using @AzureAD.</span></span>



