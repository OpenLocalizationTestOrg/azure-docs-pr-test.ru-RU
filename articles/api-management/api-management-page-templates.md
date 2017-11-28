---
title: "шаблоны aaaPage в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toocustomize hello содержимое страницы портала разработчиков с помощью набора шаблонов в Azure API Management."
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
ms.openlocfilehash: 84bd971ad4bcacfdd36c2ebbe05b16063f2a547b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="84497-103">Шаблоны страниц в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="84497-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="84497-104">Управления API Azure предоставляет hello возможность toocustomize hello содержимое страницы портала разработчиков с помощью набора шаблонов, которые настраивают их содержимого.</span><span class="sxs-lookup"><span data-stu-id="84497-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="84497-105">С помощью [DotLiquid](http://dotliquidmarkup.org/) синтаксис и hello редактора, таких как [DotLiquid для конструкторов](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), предоставленным набором локализации и [строковые ресурсы](api-management-template-resources.md#strings), [ Ресурсы глиф](api-management-template-resources.md#glyphs), и [страницы элементов управления](api-management-page-controls.md), у вас есть гибкость tooconfigure hello содержимого hello страниц по своему усмотрению, с помощью этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="84497-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="84497-106">шаблоны Hello в этом разделе позволяют toocustomize содержимое hello hello вход вход, копирование и страница не найдена страницы на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="84497-106">hello templates in this section allow you toocustomize hello content of hello sign in, sign up, and page not found pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="84497-107">Вход</span><span class="sxs-lookup"><span data-stu-id="84497-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="84497-108">Регистрация</span><span class="sxs-lookup"><span data-stu-id="84497-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="84497-109">Страница не найдена</span><span class="sxs-lookup"><span data-stu-id="84497-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="84497-110">Примеры шаблонов по умолчанию включены в следующие документации hello, но являются toochange субъекта из-за toocontinuous улучшения.</span><span class="sxs-lookup"><span data-stu-id="84497-110">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="84497-111">Можно просмотреть шаблоны динамической по умолчанию hello в портал разработчиков hello, перейдя по toohello требуемого отдельных шаблонов.</span><span class="sxs-lookup"><span data-stu-id="84497-111">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="84497-112">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="84497-112">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="84497-113"><a name="SignIn"></a> Вход</span><span class="sxs-lookup"><span data-stu-id="84497-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="84497-114">Hello **входа** шаблон позволяет toocustomize входа hello в портале разработчика hello.</span><span class="sxs-lookup"><span data-stu-id="84497-114">hello **sign in** template allows you toocustomize hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="84497-115">![Страница входа](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "шаблоны страницы входа портала разработчика APIM")</span><span class="sxs-lookup"><span data-stu-id="84497-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="84497-116">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="84497-116">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="84497-117">Управление</span><span class="sxs-lookup"><span data-stu-id="84497-117">Controls</span></span>  
 <span data-ttu-id="84497-118">Этот шаблон может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="84497-118">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="84497-119">basic-signin</span><span class="sxs-lookup"><span data-stu-id="84497-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="84497-120">providers</span><span class="sxs-lookup"><span data-stu-id="84497-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="84497-121">Модель данных</span><span class="sxs-lookup"><span data-stu-id="84497-121">Data model</span></span>  
 <span data-ttu-id="84497-122">Сущность [входа пользователя](api-management-template-data-model-reference.md#UseSignIn).</span><span class="sxs-lookup"><span data-stu-id="84497-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="84497-123">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="84497-123">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="84497-124"><a name="SignUp"></a> Регистрация</span><span class="sxs-lookup"><span data-stu-id="84497-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="84497-125">Hello **зарегистрироваться** шаблон позволяет toocustomize hello страницу регистрации на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="84497-125">hello **sign up** template allows you toocustomize hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="84497-126">![Страница регистрации](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "шаблоны страницы регистрации на портале разработчика APIM")</span><span class="sxs-lookup"><span data-stu-id="84497-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="84497-127">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="84497-127">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="84497-128">Управление</span><span class="sxs-lookup"><span data-stu-id="84497-128">Controls</span></span>  
 <span data-ttu-id="84497-129">Этот шаблон может использовать следующие hello [страницы элементов управления](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="84497-129">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="84497-130">sign-up</span><span class="sxs-lookup"><span data-stu-id="84497-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="84497-131">Модель данных</span><span class="sxs-lookup"><span data-stu-id="84497-131">Data model</span></span>  
 <span data-ttu-id="84497-132">Сущность [регистрация пользователя](api-management-template-data-model-reference.md#UserSignUp).</span><span class="sxs-lookup"><span data-stu-id="84497-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="84497-133">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="84497-133">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="84497-134"><a name="PageNotFound"></a> Страница не найдена</span><span class="sxs-lookup"><span data-stu-id="84497-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="84497-135">Hello **страница не найдена** шаблон позволяет вам toocustomize hello страница не найдена страница на портале разработчиков hello.</span><span class="sxs-lookup"><span data-stu-id="84497-135">hello **page not found** template allows you toocustomize hello page not found page in hello developer portal.</span></span>  
  
 <span data-ttu-id="84497-136">![Страница не найдена](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "шаблон страницы с ошибкой "Страница не найдена" на портале разработчика APIM")</span><span class="sxs-lookup"><span data-stu-id="84497-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="84497-137">Шаблон по умолчанию</span><span class="sxs-lookup"><span data-stu-id="84497-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="84497-138">Управление</span><span class="sxs-lookup"><span data-stu-id="84497-138">Controls</span></span>  
 <span data-ttu-id="84497-139">Этот шаблон не может использовать [элементы управления страницы](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="84497-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="84497-140">Модель данных</span><span class="sxs-lookup"><span data-stu-id="84497-140">Data model</span></span>  
  
|<span data-ttu-id="84497-141">Свойство</span><span class="sxs-lookup"><span data-stu-id="84497-141">Property</span></span>|<span data-ttu-id="84497-142">Тип</span><span class="sxs-lookup"><span data-stu-id="84497-142">Type</span></span>|<span data-ttu-id="84497-143">Описание</span><span class="sxs-lookup"><span data-stu-id="84497-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="84497-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="84497-144">referenceCode</span></span>|<span data-ttu-id="84497-145">string</span><span class="sxs-lookup"><span data-stu-id="84497-145">string</span></span>|<span data-ttu-id="84497-146">Код, созданный, если эта страница отображается как результат hello внутренней ошибки.</span><span class="sxs-lookup"><span data-stu-id="84497-146">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="84497-147">errorCode</span><span class="sxs-lookup"><span data-stu-id="84497-147">errorCode</span></span>|<span data-ttu-id="84497-148">string</span><span class="sxs-lookup"><span data-stu-id="84497-148">string</span></span>|<span data-ttu-id="84497-149">Код, созданный, если эта страница отображается как результат hello внутренней ошибки.</span><span class="sxs-lookup"><span data-stu-id="84497-149">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="84497-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="84497-150">emailBody</span></span>|<span data-ttu-id="84497-151">string</span><span class="sxs-lookup"><span data-stu-id="84497-151">string</span></span>|<span data-ttu-id="84497-152">Текст, если отображается эта страница hello результате внутренней ошибки сообщения.</span><span class="sxs-lookup"><span data-stu-id="84497-152">Email body generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="84497-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="84497-153">requestedUrl</span></span>|<span data-ttu-id="84497-154">string</span><span class="sxs-lookup"><span data-stu-id="84497-154">string</span></span>|<span data-ttu-id="84497-155">Когда страница hello не найдена Hello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="84497-155">hello URL requested when hello page was not found.</span></span>|  
|<span data-ttu-id="84497-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="84497-156">referrerUrl</span></span>|<span data-ttu-id="84497-157">string</span><span class="sxs-lookup"><span data-stu-id="84497-157">string</span></span>|<span data-ttu-id="84497-158">toohello URL-адрес источника ссылки Hello запрошенный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="84497-158">hello referrer URL toohello requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="84497-159">Пример данных шаблона</span><span class="sxs-lookup"><span data-stu-id="84497-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="84497-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84497-160">Next steps</span></span>
<span data-ttu-id="84497-161">Дополнительные сведения о работе с шаблонами см. в разделе [как toocustomize hello портал разработчика управления API, с помощью шаблонов](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="84497-161">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
