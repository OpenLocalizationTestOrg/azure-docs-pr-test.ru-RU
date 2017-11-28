---
title: "aaaAzure AD v2 ASP.NET Web Server Приступая к работе - тестирования | Документы Microsoft"
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
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="6a9e6-103">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="6a9e6-103">Test your code</span></span>

<span data-ttu-id="6a9e6-104">Нажмите клавишу `F5` toorun свой проект в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-104">Press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="6a9e6-105">Hello обозреватель и дать вам слишком*http://localhost: {port}* чего вы увидите hello *вход с Microsoft* кнопки.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-105">hello browser will open and direct you too*http://localhost:{port}* where you’ll see hello *Sign in with Microsoft* button.</span></span> <span data-ttu-id="6a9e6-106">Продолжим и щелкните его toosign в.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-106">Go ahead and click it toosign in.</span></span>

<span data-ttu-id="6a9e6-107">Когда вы будете готовы tootest, используйте рабочую или учебную (Azure Active Directory) или личного (live.com, outlook.com) учетной записи toosign в.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-107">When you're ready tootest, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account toosign in.</span></span> 

![Окно браузера для входа с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Окно браузера для входа с учетной записью Майкрософт](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="6a9e6-110">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="6a9e6-110">Expected results</span></span>
<span data-ttu-id="6a9e6-111">После входа в систему пользователя hello является домашней страницей перенаправленный toohello вашего веб-сайта, являющегося hello HTTPS-адрес, указанный в данных приложения в hello портала регистрации приложения Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-111">After sign-in, hello user is redirected toohello home page of your web site which is hello HTTPS URL specified in your application registration information in hello Microsoft Application Registration Portal.</span></span> <span data-ttu-id="6a9e6-112">Эта страница будет выглядеть *Hello {User}* и ссылка toosign исходящий и утверждения пользователей toosee ссылку hello — которых является контроллером авторизовать toohello ссылку, созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-112">This page now shows *Hello {User}* and a link toosign-out, and a link toosee hello user’s claims – which is a link toohello Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="6a9e6-113">Просмотр утверждений пользователя</span><span class="sxs-lookup"><span data-stu-id="6a9e6-113">See user's claims</span></span>
<span data-ttu-id="6a9e6-114">Выберите hello гиперссылки toosee hello утверждения пользователя.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-114">Select hello hyperlink toosee hello user's claims.</span></span> <span data-ttu-id="6a9e6-115">Заставляет toohello контроллер и представление, которое можно только доступные toousers, проходят проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-115">This leads you toohello controller and view that is only available toousers that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="6a9e6-116">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="6a9e6-116">Expected results</span></span>
 <span data-ttu-id="6a9e6-117">Появится таблица, содержащая основные свойства hello hello вход пользователя:</span><span class="sxs-lookup"><span data-stu-id="6a9e6-117">You should see a table containing hello basic properties of hello logged user:</span></span>

| <span data-ttu-id="6a9e6-118">Свойство</span><span class="sxs-lookup"><span data-stu-id="6a9e6-118">Property</span></span> | <span data-ttu-id="6a9e6-119">Значение</span><span class="sxs-lookup"><span data-stu-id="6a9e6-119">Value</span></span> | <span data-ttu-id="6a9e6-120">Описание</span><span class="sxs-lookup"><span data-stu-id="6a9e6-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="6a9e6-121">Имя</span><span class="sxs-lookup"><span data-stu-id="6a9e6-121">Name</span></span> | <span data-ttu-id="6a9e6-122">{Полное имя пользователя}</span><span class="sxs-lookup"><span data-stu-id="6a9e6-122">{User Full Name}</span></span> | <span data-ttu-id="6a9e6-123">пользователь Hello и фамилию имя</span><span class="sxs-lookup"><span data-stu-id="6a9e6-123">hello user’s first and last name</span></span>
|<span data-ttu-id="6a9e6-124">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="6a9e6-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="6a9e6-125">Hello имя пользователя, используемое tooidentify hello вход пользователя</span><span class="sxs-lookup"><span data-stu-id="6a9e6-125">hello username used tooidentify hello logged user</span></span>
| <span data-ttu-id="6a9e6-126">Субъект</span><span class="sxs-lookup"><span data-stu-id="6a9e6-126">Subject</span></span>| <span data-ttu-id="6a9e6-127">{Тема}</span><span class="sxs-lookup"><span data-stu-id="6a9e6-127">{Subject}</span></span>|<span data-ttu-id="6a9e6-128">Toouniquely строка идентификации hello входа пользователя в систему по hello web</span><span class="sxs-lookup"><span data-stu-id="6a9e6-128">A string toouniquely identify hello user logon across hello web</span></span>|
| <span data-ttu-id="6a9e6-129">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="6a9e6-129">Tenant ID</span></span>| <span data-ttu-id="6a9e6-130">Guid</span><span class="sxs-lookup"><span data-stu-id="6a9e6-130">{Guid}</span></span>| <span data-ttu-id="6a9e6-131">Объект *guid* toouniquely представляют Привет пользователя Azure Active Directory организации.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-131">A *guid* toouniquely represent hello user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="6a9e6-132">Кроме того, вы увидите таблицу со всеми утверждениями пользователя, включенными в запрос проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="6a9e6-133">Список всех утверждений в маркере идентификатора и их описание см. в этой [статье](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "Список утверждений в маркере идентификатора").</span><span class="sxs-lookup"><span data-stu-id="6a9e6-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="6a9e6-134">Проверка доступа к методу, включающему атрибут *[Authorize]* (необязательно)</span><span class="sxs-lookup"><span data-stu-id="6a9e6-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="6a9e6-135">На этом шаге вы будет доступ к hello проверкой подлинности контроллер тестирования как анонимный пользователь:</span><span class="sxs-lookup"><span data-stu-id="6a9e6-135">In this step, you will test accessing hello Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="6a9e6-136">Выберите пользователя toosign out hello ссылку hello и выхода процесса завершения hello.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-136">Select hello link toosign-out hello user and complete hello sign-out process.</span></span><br/>
<span data-ttu-id="6a9e6-137">Теперь в окне браузера введите http://localhost: {port} / tooaccess проверку подлинности, контроллер, защищенного hello `[Authorize]` атрибута</span><span class="sxs-lookup"><span data-stu-id="6a9e6-137">Now in your browser, type http://localhost:{port}/authenticated tooaccess your controller that is protected with hello `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="6a9e6-138">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="6a9e6-138">Expected results</span></span>
<span data-ttu-id="6a9e6-139">Должно быть отображено сообщение hello, требуя tooauthenticate toosee hello представления.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-139">You should receive hello prompt requiring you tooauthenticate toosee hello view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="6a9e6-140">Дополнительная информация</span><span class="sxs-lookup"><span data-stu-id="6a9e6-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="6a9e6-141">Защита всего веб-сайта</span><span class="sxs-lookup"><span data-stu-id="6a9e6-141">Protect your entire web site</span></span>
<span data-ttu-id="6a9e6-142">tooprotect все веб-сайте, добавить hello `AuthorizeAttribute` слишком`GlobalFilters` в `Global.asax` `Application_Start` метод:</span><span class="sxs-lookup"><span data-stu-id="6a9e6-142">tooprotect your entire web site, add hello `AuthorizeAttribute` too`GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="6a9e6-143">**Как пользователям toorestrict toosign только в одной организации в приложении tooyour**</span><span class="sxs-lookup"><span data-stu-id="6a9e6-143">**How toorestrict users from only one organization toosign in tooyour application**</span></span>

> <span data-ttu-id="6a9e6-144">По умолчанию личные учетные записи (включая outlook.com, live.com и другие), а также работу и учебную учетные записи из любого компании или организации, интегрированное с Azure Active Directory можно входить в приложение tooyour.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in tooyour application.</span></span> 

> <span data-ttu-id="6a9e6-145">Вашего приложения tooaccept входа в систему из только одной организации Azure Active Directory следует заменить hello `Tenant` параметр в *web.config* из `Common` имя клиента toohello hello организации — примере *contoso.onmicrosoft.com*. После этого изменить hello `ValidateIssuer` аргумента в вашей *класс запуска OWIN* слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-145">If you want your application tooaccept sign-ins from only one Azure Active Directory organization, replace hello `Tenant` parameter in *web.config* from `Common` toohello tenant name of hello organization – example, *contoso.onmicrosoft.com*. After that, change hello `ValidateIssuer` argument in your *OWIN Startup class* too`true`.</span></span>

> <span data-ttu-id="6a9e6-146">задать tooallow пользователей из списка конкретных организаций `ValidateIssuer` tootrue и использование hello `ValidIssuers` toospecify параметр список организаций.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-146">tooallow users from only a list of specific organizations, set `ValidateIssuer` tootrue and use hello `ValidIssuers` parameter toospecify a list of organizations.</span></span>

> <span data-ttu-id="6a9e6-147">Другой вариант — toovalidate hello издателей, с помощью параметра IssuerValidator tooimplement пользовательский метод.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-147">Another option is tooimplement a custom method toovalidate hello issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="6a9e6-148">Дополнительные сведения о `TokenValidationParameters` см. в этой [статье](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "Статья о классе TokenValidationParameters на сайте MSDN") на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="6a9e6-148">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

