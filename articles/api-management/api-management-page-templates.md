---
title: "Шаблоны страниц в службе управления API Azure | Документация Майкрософт"
description: "Сведения о настройке содержимого страниц портала разработчика с использованием набора шаблонов в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7f9ef37a694bce786b6acaa428df83f0cb23c2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="d2e16-103">Шаблоны страниц в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="d2e16-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="d2e16-104">Служба управления API Azure позволяет настраивать содержимое страниц портала разработчика с помощью набора шаблонов.</span><span class="sxs-lookup"><span data-stu-id="d2e16-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="d2e16-105">С помощью синтаксиса [DotLiquid](http://dotliquidmarkup.org/), выбранного редактора, например [DotLiquid для разработчиков](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), и указанного набора локализованных [строковых ресурсов](api-management-template-resources.md#strings), [ресурсов глифов](api-management-template-resources.md#glyphs), а также [элементов управления на странице](api-management-page-controls.md) можно гибко настраивать содержимое страниц по своему усмотрению с использованием этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="d2e16-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="d2e16-106">С помощью шаблонов в этом разделе вы сможете настроить содержимое страниц входа, регистрации и страницы с ошибкой "Страница не найдена" на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="d2e16-106">The templates in this section allow you to customize the content of the sign in, sign up, and page not found pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="d2e16-107">Вход</span><span class="sxs-lookup"><span data-stu-id="d2e16-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="d2e16-108">Регистрация</span><span class="sxs-lookup"><span data-stu-id="d2e16-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="d2e16-109">Страница не найдена</span><span class="sxs-lookup"><span data-stu-id="d2e16-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="d2e16-110">Примеры шаблонов по умолчанию включены в следующую документацию, но могут в любой момент измениться, так как ведется постоянная работа по их улучшению.</span><span class="sxs-lookup"><span data-stu-id="d2e16-110">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="d2e16-111">Актуальные шаблоны по умолчанию можно просмотреть на портале разработчика, перейдя к требуемому отдельному шаблону.</span><span class="sxs-lookup"><span data-stu-id="d2e16-111">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="d2e16-112">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="d2e16-112">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="d2e16-113"><a name="SignIn"></a> Вход</span><span class="sxs-lookup"><span data-stu-id="d2e16-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="d2e16-114">Шаблон **входа** позволяет настроить страницу входа на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="d2e16-114">The **sign in** template allows you to customize the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="d2e16-115">![Страница входа](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "шаблоны страницы входа портала разработчика APIM")</span><span class="sxs-lookup"><span data-stu-id="d2e16-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d2e16-116">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d2e16-116">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="d2e16-117">Управление</span><span class="sxs-lookup"><span data-stu-id="d2e16-117">Controls</span></span>  
 <span data-ttu-id="d2e16-118">Шаблон может использовать следующие [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d2e16-118">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="d2e16-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="d2e16-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="d2e16-120">providers</span><span class="sxs-lookup"><span data-stu-id="d2e16-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="d2e16-121">Модель данных</span><span class="sxs-lookup"><span data-stu-id="d2e16-121">Data model</span></span>  
 <span data-ttu-id="d2e16-122">Сущность [входа пользователя](api-management-template-data-model-reference.md#UseSignIn).</span><span class="sxs-lookup"><span data-stu-id="d2e16-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="d2e16-123">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="d2e16-123">Sample template data</span></span>  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <span data-ttu-id="d2e16-124"><a name="SignUp"></a> Регистрация</span><span class="sxs-lookup"><span data-stu-id="d2e16-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="d2e16-125">Шаблон **регистрации** позволяет настроить страницу регистрации на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="d2e16-125">The **sign up** template allows you to customize the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="d2e16-126">![Страница регистрации](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "шаблоны страницы регистрации на портале разработчика APIM")</span><span class="sxs-lookup"><span data-stu-id="d2e16-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d2e16-127">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d2e16-127">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="d2e16-128">Управление</span><span class="sxs-lookup"><span data-stu-id="d2e16-128">Controls</span></span>  
 <span data-ttu-id="d2e16-129">Шаблон может использовать следующие [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d2e16-129">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="d2e16-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="d2e16-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="d2e16-131">Модель данных</span><span class="sxs-lookup"><span data-stu-id="d2e16-131">Data model</span></span>  
 <span data-ttu-id="d2e16-132">Сущность [регистрация пользователя](api-management-template-data-model-reference.md#UserSignUp).</span><span class="sxs-lookup"><span data-stu-id="d2e16-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="d2e16-133">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="d2e16-133">Sample template data</span></span>  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <span data-ttu-id="d2e16-134"><a name="PageNotFound"></a> Страница не найдена</span><span class="sxs-lookup"><span data-stu-id="d2e16-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="d2e16-135">Шаблон страницы с ошибкой **Страница не найдена** позволяет настроить страницу с ошибкой "Страница не найдена" на портале разработчика.</span><span class="sxs-lookup"><span data-stu-id="d2e16-135">The **page not found** template allows you to customize the page not found page in the developer portal.</span></span>  
  
 <span data-ttu-id="d2e16-136">![Страница не найдена](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "шаблон страницы с ошибкой "Страница не найдена" на портале разработчика APIM")</span><span class="sxs-lookup"><span data-stu-id="d2e16-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="d2e16-137">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d2e16-137">Default template</span></span>  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a><span data-ttu-id="d2e16-138">Управление</span><span class="sxs-lookup"><span data-stu-id="d2e16-138">Controls</span></span>  
 <span data-ttu-id="d2e16-139">Этот шаблон не может использовать [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="d2e16-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="d2e16-140">Модель данных</span><span class="sxs-lookup"><span data-stu-id="d2e16-140">Data model</span></span>  
  
|<span data-ttu-id="d2e16-141">Свойство</span><span class="sxs-lookup"><span data-stu-id="d2e16-141">Property</span></span>|<span data-ttu-id="d2e16-142">Тип</span><span class="sxs-lookup"><span data-stu-id="d2e16-142">Type</span></span>|<span data-ttu-id="d2e16-143">Описание</span><span class="sxs-lookup"><span data-stu-id="d2e16-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="d2e16-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="d2e16-144">referenceCode</span></span>|<span data-ttu-id="d2e16-145">строка</span><span class="sxs-lookup"><span data-stu-id="d2e16-145">string</span></span>|<span data-ttu-id="d2e16-146">Код формируется, если эта страница отобразилась в результате внутренней ошибки.</span><span class="sxs-lookup"><span data-stu-id="d2e16-146">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="d2e16-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="d2e16-147">errorCode</span></span>|<span data-ttu-id="d2e16-148">строка</span><span class="sxs-lookup"><span data-stu-id="d2e16-148">string</span></span>|<span data-ttu-id="d2e16-149">Код формируется, если эта страница отобразилась в результате внутренней ошибки.</span><span class="sxs-lookup"><span data-stu-id="d2e16-149">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="d2e16-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="d2e16-150">emailBody</span></span>|<span data-ttu-id="d2e16-151">строка</span><span class="sxs-lookup"><span data-stu-id="d2e16-151">string</span></span>|<span data-ttu-id="d2e16-152">Текст сообщения электронной почты формируется, если эта страница отобразилась в результате внутренней ошибки.</span><span class="sxs-lookup"><span data-stu-id="d2e16-152">Email body generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="d2e16-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="d2e16-153">requestedUrl</span></span>|<span data-ttu-id="d2e16-154">строка</span><span class="sxs-lookup"><span data-stu-id="d2e16-154">string</span></span>|<span data-ttu-id="d2e16-155">URL-адрес, запрашиваемый, если страница не найдена.</span><span class="sxs-lookup"><span data-stu-id="d2e16-155">The URL requested when the page was not found.</span></span>|  
|<span data-ttu-id="d2e16-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="d2e16-156">referrerUrl</span></span>|<span data-ttu-id="d2e16-157">строка</span><span class="sxs-lookup"><span data-stu-id="d2e16-157">string</span></span>|<span data-ttu-id="d2e16-158">URL-адрес источника ссылки для запрошенного URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d2e16-158">The referrer URL to the requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="d2e16-159">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="d2e16-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="d2e16-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2e16-160">Next steps</span></span>
<span data-ttu-id="d2e16-161">Дополнительные сведения о работе с шаблонами см. в статье [Настройка портала разработчика в службе управления API Azure с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d2e16-161">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>