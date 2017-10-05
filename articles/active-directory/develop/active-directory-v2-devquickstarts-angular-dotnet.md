---
title: "Начало работы с одностраничными приложениями Azure AD v2.0 .NET AngularJS | Документация Майкрософт"
description: "Как создать одностраничное приложение AngularJS, которое поддерживает вход пользователей в систему с помощью личной учетной записи Майкрософт, а также рабочей или учебной учетной записи."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 6a341781-278f-461b-92ca-7572a06e6852
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c68180c0ecabf5c0732f0db77ef1f3cc93be965b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---net"></a><span data-ttu-id="ae657-103">Добавление функции входа в одностраничное приложение AngularJS — версия для .NET</span><span class="sxs-lookup"><span data-stu-id="ae657-103">Add sign-in to an AngularJS single page app - .NET</span></span>
<span data-ttu-id="ae657-104">В этой статье мы добавим в приложение AngularJS функцию входа с учетными записями на платформе Майкрософт с помощью конечной точки Azure Active Directory версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="ae657-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span>  <span data-ttu-id="ae657-105">Конечная точка версии 2.0 обеспечивает единую интеграцию в приложении и аутентификацию пользователей как с личными, так и с рабочими или учебными учетными записями.</span><span class="sxs-lookup"><span data-stu-id="ae657-105">The v2.0 endpoint enables you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="ae657-106">Наш пример — это простое одностраничное приложение со списком дел, которое сохраняет задачи в серверной части REST API. Оно написано на платформе MVC .NET 4.5 и защищено с помощью токенов носителя OAuth из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae657-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written using the .NET 4.5 MVC framework and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="ae657-107">Приложение AngularJS будет использовать нашу библиотеку проверки подлинности JavaScript с открытым исходным кодом [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) для обработки всего процесса входа в систему и получения токенов для вызова интерфейса API REST.</span><span class="sxs-lookup"><span data-stu-id="ae657-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="ae657-108">Эта модель может применяться для аутентификации в других интерфейсах REST API, например [Microsoft Graph](https://graph.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ae657-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com).</span></span>

> [!NOTE]
> <span data-ttu-id="ae657-109">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="ae657-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="ae657-110">Чтобы определить, следует ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="ae657-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="ae657-111">Загрузить</span><span class="sxs-lookup"><span data-stu-id="ae657-111">Download</span></span>
<span data-ttu-id="ae657-112">Чтобы начать работу, необходимо загрузить и установить Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae657-112">To get started, you'll need to download & install Visual Studio.</span></span>  <span data-ttu-id="ae657-113">Затем можно клонировать или [загрузить](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) скелет приложения:</span><span class="sxs-lookup"><span data-stu-id="ae657-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

<span data-ttu-id="ae657-114">Скелет приложения включает в себя весь код шаблона простого приложения AngularJS, но в нем отсутствуют все компоненты, связанные с удостоверениями.</span><span class="sxs-lookup"><span data-stu-id="ae657-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="ae657-115">Если не хотите следовать учебнику, вместо этого можно клонировать или [загрузить](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) готовый пример.</span><span class="sxs-lookup"><span data-stu-id="ae657-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a><span data-ttu-id="ae657-116">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="ae657-116">Register an app</span></span>
<span data-ttu-id="ae657-117">Во-первых, создайте приложение на [портале регистрации приложений](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните следующие [подробные шаги](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ae657-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="ae657-118">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="ae657-118">Make sure to:</span></span>

* <span data-ttu-id="ae657-119">Добавьте **веб-платформу** для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="ae657-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="ae657-120">Введите правильный **универсальный код ресурса (URI) перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="ae657-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="ae657-121">Значение по умолчанию для этого примера: `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="ae657-121">The default for this sample is `https://localhost:44326/`.</span></span>
* <span data-ttu-id="ae657-122">Оставьте включенным флажок **Разрешить неявный поток** .</span><span class="sxs-lookup"><span data-stu-id="ae657-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="ae657-123">Запишите назначенный **идентификатор приложения**. Он вскоре вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="ae657-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="ae657-124">Установка adal.js</span><span class="sxs-lookup"><span data-stu-id="ae657-124">Install adal.js</span></span>
<span data-ttu-id="ae657-125">Для запуска перейдите в загруженный проект и установите библиотеку adal.js.</span><span class="sxs-lookup"><span data-stu-id="ae657-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="ae657-126">Если у вас установлен [bower](http://bower.io/) , можно просто выполнить эту команду.</span><span class="sxs-lookup"><span data-stu-id="ae657-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="ae657-127">В случае несоответствия версий каких-либо зависимостей просто выберите наиболее актуальную версию.</span><span class="sxs-lookup"><span data-stu-id="ae657-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="ae657-128">Кроме того, можно вручную загрузить [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) и [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="ae657-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="ae657-129">Добавьте оба файла в каталог `app/lib/adal-angular-experimental/dist` проекта `TodoSPA`.</span><span class="sxs-lookup"><span data-stu-id="ae657-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory of the `TodoSPA` project.</span></span>

<span data-ttu-id="ae657-130">Теперь откройте проект в Visual Studio и в конце главной страницы добавьте код adal.js:</span><span class="sxs-lookup"><span data-stu-id="ae657-130">Now open the project in Visual Studio, and load adal.js at the end of the main page's body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="ae657-131">Настройка REST API</span><span class="sxs-lookup"><span data-stu-id="ae657-131">Set up the REST API</span></span>
<span data-ttu-id="ae657-132">Пока мы все настраиваем, давайте обеспечим работу серверной части REST API.</span><span class="sxs-lookup"><span data-stu-id="ae657-132">While we're setting things up, let's get the backend REST API working.</span></span>  <span data-ttu-id="ae657-133">В корневой папке проекта откройте `web.config` и замените значение `audience`.</span><span class="sxs-lookup"><span data-stu-id="ae657-133">In the root of the project, open `web.config` and replace the `audience` value.</span></span>  <span data-ttu-id="ae657-134">Интерфейс REST API будет использовать это значение для проверки токенов, получаемых от приложения Angular по запросам AJAX.</span><span class="sxs-lookup"><span data-stu-id="ae657-134">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

<span data-ttu-id="ae657-135">На этом мы остановимся и не будем углубляться в обсуждение принципов работы REST API.</span><span class="sxs-lookup"><span data-stu-id="ae657-135">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="ae657-136">Не стесняйтесь изучать код, но если вы хотите узнать больше о защите веб-API с помощью Azure AD, ознакомьтесь с [этой статьей](active-directory-v2-devquickstarts-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="ae657-136">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-dotnet-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="ae657-137">Вход пользователей</span><span class="sxs-lookup"><span data-stu-id="ae657-137">Sign users in</span></span>
<span data-ttu-id="ae657-138">Настало время написать код для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ae657-138">Time to write some identity code.</span></span>  <span data-ttu-id="ae657-139">Вы уже могли заметить, что в adal.js имеется поставщик AngularJS, который хорошо работает с механизмами маршрутизации Angular.</span><span class="sxs-lookup"><span data-stu-id="ae657-139">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="ae657-140">Начните с добавления в приложение модуля adal:</span><span class="sxs-lookup"><span data-stu-id="ae657-140">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="ae657-141">Теперь вы можете инициализировать `adalProvider` с помощью ИД приложения:</span><span class="sxs-lookup"><span data-stu-id="ae657-141">You can now initialize the `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for the public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // The 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from the registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - the default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="ae657-142">Отлично, теперь у adal.js есть все сведения, необходимые для защиты приложения и входа пользователей.</span><span class="sxs-lookup"><span data-stu-id="ae657-142">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="ae657-143">Принудительный вход с определенным маршрутом в приложении определяется всего одной строкой кода:</span><span class="sxs-lookup"><span data-stu-id="ae657-143">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that the user must be logged in to access the route
})

...
```

<span data-ttu-id="ae657-144">Когда пользователь щелкает ссылку `TodoList` , библиотека adal.js при необходимости автоматически выполнит перенаправление на Azure AD для выполнения входа.</span><span class="sxs-lookup"><span data-stu-id="ae657-144">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="ae657-145">Вы можете явно отправлять запросы на выполнение входа и выхода, вызывая adal.js в контроллерах:</span><span class="sxs-lookup"><span data-stu-id="ae657-145">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js the same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect the user to sign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect the user to log out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="ae657-146">Отображение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="ae657-146">Display user info</span></span>
<span data-ttu-id="ae657-147">Теперь, когда пользователь выполнил вход, вам может потребоваться доступ к данным проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="ae657-147">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="ae657-148">Adal.js предоставляет эти сведения в объекте `userInfo` .</span><span class="sxs-lookup"><span data-stu-id="ae657-148">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="ae657-149">Чтобы получить доступ к этому объекту в представлении, сначала добавьте adal.js в корневую область соответствующего контроллера:</span><span class="sxs-lookup"><span data-stu-id="ae657-149">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="ae657-150">Затем можно обращаться напрямую к объекту `userInfo` в представлении:</span><span class="sxs-lookup"><span data-stu-id="ae657-150">Then you can directly address the `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get the user's profile information from the ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="ae657-151">Можно также использовать объект `userInfo` , чтобы определить, выполнил пользователь вход или нет.</span><span class="sxs-lookup"><span data-stu-id="ae657-151">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use the ADAL userInfo object to show the right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-the-rest-api"></a><span data-ttu-id="ae657-152">Вызов REST API</span><span class="sxs-lookup"><span data-stu-id="ae657-152">Call the REST API</span></span>
<span data-ttu-id="ae657-153">Наконец пришло время получить токены и вызвать REST API для создания, чтения, обновления и удаления задач.</span><span class="sxs-lookup"><span data-stu-id="ae657-153">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="ae657-154">И знаете что?</span><span class="sxs-lookup"><span data-stu-id="ae657-154">Well guess what?</span></span>  <span data-ttu-id="ae657-155">Вам не придется делать *ничего*.</span><span class="sxs-lookup"><span data-stu-id="ae657-155">You don't have to do *a thing*.</span></span>  <span data-ttu-id="ae657-156">Adal.js автоматически обеспечит получение, кэширование и обновление токенов.</span><span class="sxs-lookup"><span data-stu-id="ae657-156">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="ae657-157">Библиотека также позаботится о присоединении этих токенов к исходящим запросам AJAX, отправляемым в REST API.</span><span class="sxs-lookup"><span data-stu-id="ae657-157">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="ae657-158">Как именно это работает?</span><span class="sxs-lookup"><span data-stu-id="ae657-158">How exactly does this work?</span></span> <span data-ttu-id="ae657-159">Это все благодаря магии [перехватчиков AngularJS](https://docs.angularjs.org/api/ng/service/$http), которые позволяют adal.js преобразовывать входящие и исходящие http-сообщения.</span><span class="sxs-lookup"><span data-stu-id="ae657-159">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="ae657-160">Кроме того, adal.js предполагает, что все запросы отправляются в один домен, так как окно должно использовать токены, предназначенные для того же идентификатора приложения, что и у приложения AngularJS.</span><span class="sxs-lookup"><span data-stu-id="ae657-160">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="ae657-161">Именно поэтому мы использовали один и тот же идентификатор приложения в приложении Angular и в REST API NodeJS.</span><span class="sxs-lookup"><span data-stu-id="ae657-161">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="ae657-162">Конечно, можно переопределить это поведение и сделать так, чтобы библиотека adal.js при необходимости получала токены для других интерфейсов REST API. Но в нашем упрощенном примере подойдут значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ae657-162">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="ae657-163">Ниже приведен фрагмент, который показывает, насколько просто отправлять запросы с токенами носителя из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae657-163">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="ae657-164">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="ae657-164">Congratulations!</span></span>  <span data-ttu-id="ae657-165">Ваше одностраничное приложение, интегрированное с Azure AD, готово.</span><span class="sxs-lookup"><span data-stu-id="ae657-165">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="ae657-166">Протестируйте его.</span><span class="sxs-lookup"><span data-stu-id="ae657-166">Go ahead, take a bow.</span></span>  <span data-ttu-id="ae657-167">Приложение может проверять подлинность пользователей, безопасно обращаться к REST API серверной части с помощью OpenID Connect и получать основные сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="ae657-167">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="ae657-168">По умолчанию оно поддерживает всех пользователей с учетной записью Майкрософт или рабочей либо учебной учетной записью в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae657-168">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="ae657-169">Запустите приложение и в адресной строке браузера введите `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="ae657-169">Run the app, and in a browser navigate to `https://localhost:44326/`.</span></span>  <span data-ttu-id="ae657-170">Войдите с личной учетной записью Майкрософт либо рабочей или учебной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="ae657-170">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="ae657-171">Добавьте задачи в список дел и выйдите.</span><span class="sxs-lookup"><span data-stu-id="ae657-171">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="ae657-172">Попробуйте войти с учетной записью другого типа.</span><span class="sxs-lookup"><span data-stu-id="ae657-172">Try signing in with the other type of account.</span></span> <span data-ttu-id="ae657-173">Если вам нужен клиент Azure AD для создания рабочих или школьных учетных записей, [узнайте здесь, как его получить](active-directory-howto-tenant.md) (предоставляется бесплатно).</span><span class="sxs-lookup"><span data-stu-id="ae657-173">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="ae657-174">Чтобы продолжить изучение конечной точки версии 2.0, вернитесь к нашему [руководству разработчика для версии 2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae657-174">To continue learning about the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="ae657-175">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="ae657-175">For additional resources, check out:</span></span>

* [<span data-ttu-id="ae657-176">Образцы Azure на GitHub >></span><span class="sxs-lookup"><span data-stu-id="ae657-176">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="ae657-177">Azure AD на Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="ae657-177">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="ae657-178">Документация по Azure AD [на сайте Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="ae657-178">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="ae657-179">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="ae657-179">Get security updates for our products</span></span>
<span data-ttu-id="ae657-180">Рекомендуем вам настроить уведомления о нарушениях безопасности. Это можно сделать, подписавшись на уведомления безопасности консультационных служб на [этой странице](https://technet.microsoft.com/security/dd252948).</span><span class="sxs-lookup"><span data-stu-id="ae657-180">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

