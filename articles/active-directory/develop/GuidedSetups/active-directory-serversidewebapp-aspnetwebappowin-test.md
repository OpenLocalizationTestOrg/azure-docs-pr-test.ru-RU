---
title: "Приступая к работе с Azure AD версии 2 для веб-сервера ASP.NET. Проверка | Документация Майкрософт"
description: "Реализация входа Майкрософт в решении ASP.NET с традиционным браузерным приложением с использованием стандарта OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="eadb3-103">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="eadb3-103">Test your code</span></span>

<span data-ttu-id="eadb3-104">Щелкните `F5`, чтобы запустить проект в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eadb3-104">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="eadb3-105">Откроется браузер, и вы будете перенаправлены на страницу *http://localhost:{порт}*, где вы увидите кнопку *Вход с учетной записью Майкрософт*.</span><span class="sxs-lookup"><span data-stu-id="eadb3-105">The browser will open and direct you to *http://localhost:{port}* where you’ll see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="eadb3-106">Щелкните ее, чтобы выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="eadb3-106">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="eadb3-107">Когда вы будете готовы выполнить проверку, используйте рабочую или учебную учетную запись (Azure Active Directory) либо личную учетную запись (live.com, outlook.com), чтобы выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="eadb3-107">When you're ready to test, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account to sign in.</span></span> 

![Окно браузера для входа с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Окно браузера для входа с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="eadb3-110">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="eadb3-110">Expected results</span></span>
<span data-ttu-id="eadb3-111">После входа в систему пользователь перенаправляется на домашнюю страницу веб-сайта, URL-адрес для протокола HTTPS которой указан в сведениях о регистрации приложения на портале регистрации приложений Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="eadb3-111">After sign-in, the user is redirected to the home page of your web site which is the HTTPS URL specified in your application registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="eadb3-112">Теперь на этой странице отображается *приветствие*, ссылка, чтобы выйти из приложения, и ссылка, чтобы увидеть утверждения пользователя. Она является ссылкой на ранее созданный контроллер авторизации.</span><span class="sxs-lookup"><span data-stu-id="eadb3-112">This page now shows *Hello {User}* and a link to sign-out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="eadb3-113">Просмотр утверждений пользователя</span><span class="sxs-lookup"><span data-stu-id="eadb3-113">See user's claims</span></span>
<span data-ttu-id="eadb3-114">Выберите гиперссылку, чтобы просмотреть утверждения пользователя.</span><span class="sxs-lookup"><span data-stu-id="eadb3-114">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="eadb3-115">Вы перейдете к контроллеру и представлению, которое доступно только для пользователей, прошедших проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="eadb3-115">This leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="eadb3-116">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="eadb3-116">Expected results</span></span>
 <span data-ttu-id="eadb3-117">Вы должны увидеть таблицу, содержащую основные свойства пользователя, выполнившего вход.</span><span class="sxs-lookup"><span data-stu-id="eadb3-117">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="eadb3-118">Свойство</span><span class="sxs-lookup"><span data-stu-id="eadb3-118">Property</span></span> | <span data-ttu-id="eadb3-119">Значение</span><span class="sxs-lookup"><span data-stu-id="eadb3-119">Value</span></span> | <span data-ttu-id="eadb3-120">Описание</span><span class="sxs-lookup"><span data-stu-id="eadb3-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="eadb3-121">Имя</span><span class="sxs-lookup"><span data-stu-id="eadb3-121">Name</span></span> | <span data-ttu-id="eadb3-122">{Полное имя пользователя}</span><span class="sxs-lookup"><span data-stu-id="eadb3-122">{User Full Name}</span></span> | <span data-ttu-id="eadb3-123">Имя и фамилия пользователя</span><span class="sxs-lookup"><span data-stu-id="eadb3-123">The user’s first and last name</span></span>
|<span data-ttu-id="eadb3-124">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="eadb3-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="eadb3-125">Имя пользователя, используемое для его идентификации</span><span class="sxs-lookup"><span data-stu-id="eadb3-125">The username used to identify the logged user</span></span>
| <span data-ttu-id="eadb3-126">Субъект</span><span class="sxs-lookup"><span data-stu-id="eadb3-126">Subject</span></span>| <span data-ttu-id="eadb3-127">{Тема}</span><span class="sxs-lookup"><span data-stu-id="eadb3-127">{Subject}</span></span>|<span data-ttu-id="eadb3-128">Строка для уникальной идентификации входа пользователя в Интернете</span><span class="sxs-lookup"><span data-stu-id="eadb3-128">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="eadb3-129">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="eadb3-129">Tenant ID</span></span>| <span data-ttu-id="eadb3-130">Guid</span><span class="sxs-lookup"><span data-stu-id="eadb3-130">{Guid}</span></span>| <span data-ttu-id="eadb3-131">Значение *guid* используется для однозначного представления организации пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eadb3-131">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="eadb3-132">Кроме того, вы увидите таблицу со всеми утверждениями пользователя, включенными в запрос проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="eadb3-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="eadb3-133">Список всех утверждений в маркере идентификатора и их описание см. в этой [статье](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Список утверждений в маркере идентификатора").</span><span class="sxs-lookup"><span data-stu-id="eadb3-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="eadb3-134">Проверка доступа к методу, включающему атрибут *[Authorize]* (необязательно)</span><span class="sxs-lookup"><span data-stu-id="eadb3-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="eadb3-135">На этом шаге вы проверите доступ к аутентифицированному контроллеру как анонимный пользователь.</span><span class="sxs-lookup"><span data-stu-id="eadb3-135">In this step, you will test accessing the Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="eadb3-136">Выберите ссылку для выхода пользователя и завершения процесса выхода.</span><span class="sxs-lookup"><span data-stu-id="eadb3-136">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="eadb3-137">Теперь в окне браузера введите http://localhost:{порт}/authenticated, чтобы получить доступ к контроллеру, защищенному атрибутом `[Authorize]`.</span><span class="sxs-lookup"><span data-stu-id="eadb3-137">Now in your browser, type http://localhost:{port}/authenticated to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="eadb3-138">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="eadb3-138">Expected results</span></span>
<span data-ttu-id="eadb3-139">Вы должны получить запрос на выполнение проверки подлинности, чтобы открылось представление.</span><span class="sxs-lookup"><span data-stu-id="eadb3-139">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="eadb3-140">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="eadb3-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="eadb3-141">Защита всего веб-сайта</span><span class="sxs-lookup"><span data-stu-id="eadb3-141">Protect your entire web site</span></span>
<span data-ttu-id="eadb3-142">Для защиты всего веб-сайта добавьте `AuthorizeAttribute` для `GlobalFilters` в метод `Global.asax` `Application_Start`:</span><span class="sxs-lookup"><span data-stu-id="eadb3-142">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="eadb3-143">**Как разрешить вход в приложение только пользователям одной организации**</span><span class="sxs-lookup"><span data-stu-id="eadb3-143">**How to restrict users from only one organization to sign in to your application**</span></span>

> <span data-ttu-id="eadb3-144">По умолчанию в приложение можно выполнить вход с помощью личных учетных записей (включая outlook.com, live.com и другие), а также рабочих и учебных учетных записей из любой компании или организации, которая использует Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eadb3-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in to your application.</span></span> 

> <span data-ttu-id="eadb3-145">Если вы хотите, чтобы вход в приложение был настроен только для пользователей из одной организации Azure Active Directory, замените параметр `Tenant` в файле *web.config* с `Common` на имя клиента организации, например *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="eadb3-145">If you want your application to accept sign-ins from only one Azure Active Directory organization, replace the `Tenant` parameter in *web.config* from `Common` to the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="eadb3-146">После этого измените аргумент `ValidateIssuer` в *классе запуска OWIN*, задав ему значение `true`.</span><span class="sxs-lookup"><span data-stu-id="eadb3-146">After that, change the `ValidateIssuer` argument in your *OWIN Startup class* to `true`.</span></span>

> <span data-ttu-id="eadb3-147">Чтобы разрешить вход для пользователей из списка определенных организаций, задайте параметру `ValidateIssuer` значение true и используйте параметр `ValidIssuers`, чтобы указать список организаций.</span><span class="sxs-lookup"><span data-stu-id="eadb3-147">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

> <span data-ttu-id="eadb3-148">Другой вариант — реализовать пользовательский метод для проверки издателей с помощью параметра IssuerValidator.</span><span class="sxs-lookup"><span data-stu-id="eadb3-148">Another option is to implement a custom method to validate the issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="eadb3-149">Дополнительные сведения о `TokenValidationParameters` см. в этой [статье](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "Статья о классе TokenValidationParameters на сайте MSDN") на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="eadb3-149">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

