---
title: "Начало работы с одностраничными приложениями Azure AD v2.0 NodeJS AngularJS | Документация Майкрософт"
description: "Как создать одностраничное приложение AngularJS, которое поддерживает вход пользователей в систему с помощью личной учетной записи Майкрософт, а также рабочей или учебной учетной записи."
services: active-directory
documentationcenter: 
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: d286aa33-8a94-452f-beb7-ddc6c6daa5c8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 0e90171afd9c4c782fbb18375ab2d147497ef442
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-angularjs-single-page-app---nodejs"></a><span data-ttu-id="62ad1-103">Добавление функции входа в одностраничное приложение AngularJS — версия для NodeJS</span><span class="sxs-lookup"><span data-stu-id="62ad1-103">Add sign-in to an AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="62ad1-104">В этой статье мы добавим в приложение AngularJS функцию входа с учетными записями на платформе Майкрософт с помощью конечной точки Azure Active Directory версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="62ad1-104">In this article we'll add sign in with Microsoft powered accounts to an AngularJS app using the Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="62ad1-105">Конечная точка версии 2.0 обеспечивает единую интеграцию в приложении и аутентификацию пользователей с личными, рабочими или учебными учетными записями.</span><span class="sxs-lookup"><span data-stu-id="62ad1-105">the v2.0 endpoint enable you to perform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="62ad1-106">Этот пример представляет собой простое одностраничное приложение со списком дел, которое сохраняет задачи в серверной части API REST, написанное на NodeJS и защищенное с помощью токенов носителя OAuth из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62ad1-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="62ad1-107">Приложение AngularJS будет использовать нашу библиотеку проверки подлинности JavaScript с открытым исходным кодом [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) для обработки всего процесса входа в систему и получения токенов для вызова интерфейса API REST.</span><span class="sxs-lookup"><span data-stu-id="62ad1-107">The AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) to handle the entire sign in process and acquire tokens for calling the REST API.</span></span>  <span data-ttu-id="62ad1-108">Эта модель может применяться для проверки подлинности в других интерфейсах REST API, например [Microsoft Graph](https://graph.microsoft.com) или API диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="62ad1-108">The same pattern can be applied to authenticate to other REST APIs, like the [Microsoft Graph](https://graph.microsoft.com) or the Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="62ad1-109">Не все сценарии и компоненты Azure Active Directory поддерживаются конечной точкой версии 2.0.</span><span class="sxs-lookup"><span data-stu-id="62ad1-109">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="62ad1-110">Чтобы определить, следует ли вам использовать конечную точку версии 2.0, ознакомьтесь с [ограничениями версии 2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="62ad1-110">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="62ad1-111">Загрузить</span><span class="sxs-lookup"><span data-stu-id="62ad1-111">Download</span></span>
<span data-ttu-id="62ad1-112">Чтобы начать работу, необходимо скачать и установить [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="62ad1-112">To get started, you'll need to download & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="62ad1-113">Затем можно клонировать или [загрузить](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) скелет приложения:</span><span class="sxs-lookup"><span data-stu-id="62ad1-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="62ad1-114">Скелет приложения включает в себя весь код шаблона простого приложения AngularJS, но в нем отсутствуют все компоненты, связанные с удостоверениями.</span><span class="sxs-lookup"><span data-stu-id="62ad1-114">The skeleton app includes all the boilerplate code for a simple AngularJS app, but is missing all of the identity-related pieces.</span></span>  <span data-ttu-id="62ad1-115">Если не хотите следовать учебнику, вместо этого можно клонировать или [загрузить](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) готовый пример.</span><span class="sxs-lookup"><span data-stu-id="62ad1-115">If you don't want to follow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) the completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="62ad1-116">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="62ad1-116">Register an app</span></span>
<span data-ttu-id="62ad1-117">Во-первых, создайте приложение на [портале регистрации приложений](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) или выполните следующие [подробные шаги](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="62ad1-117">First, create an app in the [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="62ad1-118">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="62ad1-118">Make sure to:</span></span>

* <span data-ttu-id="62ad1-119">Добавьте **веб-платформу** для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="62ad1-119">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="62ad1-120">Введите правильный **универсальный код ресурса (URI) перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="62ad1-120">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="62ad1-121">Значение по умолчанию для этого примера: `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="62ad1-121">The default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="62ad1-122">Оставьте включенным флажок **Разрешить неявный поток** .</span><span class="sxs-lookup"><span data-stu-id="62ad1-122">Leave the **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="62ad1-123">Запишите назначенный **идентификатор приложения**. Он вскоре вам понадобится.</span><span class="sxs-lookup"><span data-stu-id="62ad1-123">Copy down the **Application ID** that is assigned to your app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="62ad1-124">Установка adal.js</span><span class="sxs-lookup"><span data-stu-id="62ad1-124">Install adal.js</span></span>
<span data-ttu-id="62ad1-125">Для запуска перейдите в загруженный проект и установите библиотеку adal.js.</span><span class="sxs-lookup"><span data-stu-id="62ad1-125">To start, navigate to project you downloaded and install adal.js.</span></span>  <span data-ttu-id="62ad1-126">Если у вас установлен [bower](http://bower.io/) , можно просто выполнить эту команду.</span><span class="sxs-lookup"><span data-stu-id="62ad1-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="62ad1-127">В случае несоответствия версий каких-либо зависимостей просто выберите наиболее актуальную версию.</span><span class="sxs-lookup"><span data-stu-id="62ad1-127">For any dependency version mismatches, just choose the higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="62ad1-128">Кроме того, можно вручную загрузить [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) и [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="62ad1-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="62ad1-129">Добавьте оба файла в каталог `app/lib/adal-angular-experimental/dist` .</span><span class="sxs-lookup"><span data-stu-id="62ad1-129">Add both files to the `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="62ad1-130">Теперь откройте проект в своем любимом текстовом редакторе и загрузите adal.js в конце тела страницы:</span><span class="sxs-lookup"><span data-stu-id="62ad1-130">Now open the project in your favorite text editor, and load adal.js at the end of the page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-the-rest-api"></a><span data-ttu-id="62ad1-131">Настройка API REST</span><span class="sxs-lookup"><span data-stu-id="62ad1-131">Set up the REST API</span></span>
<span data-ttu-id="62ad1-132">Пока мы все настраиваем, обеспечим работу серверной части API REST.</span><span class="sxs-lookup"><span data-stu-id="62ad1-132">While we're setting things up, lets get the backend REST API working.</span></span>  <span data-ttu-id="62ad1-133">В командной строке установите все необходимые пакеты, выполнив команду (убедитесь, что находитесь в каталоге верхнего уровня проекта):</span><span class="sxs-lookup"><span data-stu-id="62ad1-133">In a command prompt, install all the necessary packages by running (make sure you're in the top-level directory of the project):</span></span>

```
npm install
```

<span data-ttu-id="62ad1-134">Теперь откройте `config.js` и замените значение `audience`:</span><span class="sxs-lookup"><span data-stu-id="62ad1-134">Now open `config.js` and replace the `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with the Application ID from the registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="62ad1-135">Интерфейс API REST будет использовать это значение для проверки токенов, получаемых от приложения Angular по запросам AJAX.</span><span class="sxs-lookup"><span data-stu-id="62ad1-135">The REST API will use this value to validate tokens it receives from the Angular app on AJAX requests.</span></span>  <span data-ttu-id="62ad1-136">Обратите внимание, что этот простой API REST хранит данные в памяти — поэтому каждый раз при остановке сервера все ранее созданные задачи будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="62ad1-136">Note that this simple REST API stores data in-memory - so each time to stop the server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="62ad1-137">Вот и все время, которое мы потратим на обсуждение принципов работы API REST.</span><span class="sxs-lookup"><span data-stu-id="62ad1-137">That's all the time we're going to spend discussing how the REST API works.</span></span>  <span data-ttu-id="62ad1-138">Не стесняйтесь изучать код, но если вы хотите узнать больше о защите веб-API с помощью Azure AD, ознакомьтесь с [этой статьей](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="62ad1-138">Feel free to poke around in the code, but if you want to learn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="62ad1-139">Вход пользователей</span><span class="sxs-lookup"><span data-stu-id="62ad1-139">Sign users in</span></span>
<span data-ttu-id="62ad1-140">Настало время написать код для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="62ad1-140">Time to write some identity code.</span></span>  <span data-ttu-id="62ad1-141">Вы уже могли заметить, что в adal.js имеется поставщик AngularJS, который хорошо работает с механизмами маршрутизации Angular.</span><span class="sxs-lookup"><span data-stu-id="62ad1-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="62ad1-142">Начните с добавления в приложение модуля adal:</span><span class="sxs-lookup"><span data-stu-id="62ad1-142">Start by adding the adal module to the app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="62ad1-143">Теперь вы можете инициализировать `adalProvider` с помощью ИД приложения:</span><span class="sxs-lookup"><span data-stu-id="62ad1-143">You can now initialize the `adalProvider` with your Application ID:</span></span>

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

<span data-ttu-id="62ad1-144">Отлично, теперь у adal.js есть все сведения, необходимые для защиты приложения и входа пользователей.</span><span class="sxs-lookup"><span data-stu-id="62ad1-144">Great, now adal.js has all the information it needs to secure your app and sign users in.</span></span>  <span data-ttu-id="62ad1-145">Принудительный вход с определенным маршрутом в приложении определяется всего одной строкой кода:</span><span class="sxs-lookup"><span data-stu-id="62ad1-145">To force sign in for a particular route in the app, all it takes is one line of code:</span></span>

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

<span data-ttu-id="62ad1-146">Когда пользователь щелкает ссылку `TodoList` , библиотека adal.js при необходимости автоматически выполнит перенаправление на Azure AD для выполнения входа.</span><span class="sxs-lookup"><span data-stu-id="62ad1-146">Now when a user clicks the `TodoList` link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span>  <span data-ttu-id="62ad1-147">Вы можете явно отправлять запросы на выполнение входа и выхода, вызывая adal.js в контроллерах:</span><span class="sxs-lookup"><span data-stu-id="62ad1-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

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

## <a name="display-user-info"></a><span data-ttu-id="62ad1-148">Отображение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="62ad1-148">Display user info</span></span>
<span data-ttu-id="62ad1-149">Теперь, когда пользователь выполнил вход, вам может потребоваться доступ к данным проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="62ad1-149">Now that the user is signed in, you'll probably need to access the signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="62ad1-150">Adal.js предоставляет эти сведения в объекте `userInfo` .</span><span class="sxs-lookup"><span data-stu-id="62ad1-150">Adal.js exposes this information for you in the `userInfo` object.</span></span>  <span data-ttu-id="62ad1-151">Чтобы получить доступ к этому объекту в представлении, сначала добавьте adal.js в корневую область соответствующего контроллера:</span><span class="sxs-lookup"><span data-stu-id="62ad1-151">To access this object in a view, first add adal.js to the root scope of the corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="62ad1-152">Затем можно обращаться напрямую к объекту `userInfo` в представлении:</span><span class="sxs-lookup"><span data-stu-id="62ad1-152">Then you can directly address the `userInfo` object in your view:</span></span> 

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

<span data-ttu-id="62ad1-153">Можно также использовать объект `userInfo` , чтобы определить, выполнил пользователь вход или нет.</span><span class="sxs-lookup"><span data-stu-id="62ad1-153">You can also use the `userInfo` object to determine if the user is signed in or not.</span></span>

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

## <a name="call-the-rest-api"></a><span data-ttu-id="62ad1-154">Вызов REST API</span><span class="sxs-lookup"><span data-stu-id="62ad1-154">Call the REST API</span></span>
<span data-ttu-id="62ad1-155">Наконец пришло время получить токены и вызвать REST API для создания, чтения, обновления и удаления задач.</span><span class="sxs-lookup"><span data-stu-id="62ad1-155">Finally, it's time to get some tokens and call the REST API to create, read, update, and delete tasks.</span></span>  <span data-ttu-id="62ad1-156">И знаете что?</span><span class="sxs-lookup"><span data-stu-id="62ad1-156">Well guess what?</span></span>  <span data-ttu-id="62ad1-157">Вам не придется делать *ничего*.</span><span class="sxs-lookup"><span data-stu-id="62ad1-157">You don't have to do *a thing*.</span></span>  <span data-ttu-id="62ad1-158">Adal.js автоматически обеспечит получение, кэширование и обновление токенов.</span><span class="sxs-lookup"><span data-stu-id="62ad1-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="62ad1-159">Библиотека также позаботится о присоединении этих токенов к исходящим запросам AJAX, отправляемым в REST API.</span><span class="sxs-lookup"><span data-stu-id="62ad1-159">It will also take care of attaching those tokens to outgoing AJAX requests that you send to the REST API.</span></span>  

<span data-ttu-id="62ad1-160">Как именно это работает?</span><span class="sxs-lookup"><span data-stu-id="62ad1-160">How exactly does this work?</span></span> <span data-ttu-id="62ad1-161">Это все благодаря магии [перехватчиков AngularJS](https://docs.angularjs.org/api/ng/service/$http), которые позволяют adal.js преобразовывать входящие и исходящие http-сообщения.</span><span class="sxs-lookup"><span data-stu-id="62ad1-161">It's all thanks to the magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js to transform outgoing and incoming http messages.</span></span>  <span data-ttu-id="62ad1-162">Кроме того, adal.js предполагает, что все запросы отправляются в один домен, так как окно должно использовать токены, предназначенные для того же идентификатора приложения, что и у приложения AngularJS.</span><span class="sxs-lookup"><span data-stu-id="62ad1-162">Furthermore, adal.js assumes that any requests send to the same domain as the window should use tokens intended for the same Application ID as the AngularJS app.</span></span>  <span data-ttu-id="62ad1-163">Именно поэтому мы использовали один и тот же идентификатор приложения в приложении Angular и в REST API NodeJS.</span><span class="sxs-lookup"><span data-stu-id="62ad1-163">This is why we used the same Application ID in both the Angular app and in the NodeJS REST API.</span></span>  <span data-ttu-id="62ad1-164">Конечно, можно переопределить это поведение и сделать так, чтобы библиотека adal.js при необходимости получала токены для других интерфейсов REST API. Но в нашем упрощенном примере подойдут значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="62ad1-164">Of course, you can override this behavior and tell adal.js to get tokens for other REST APIs if necessary - but for this simple scenario the defaults will do.</span></span>

<span data-ttu-id="62ad1-165">Ниже приведен фрагмент, который показывает, насколько просто отправлять запросы с токенами носителя из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62ad1-165">Here's a snippet that shows how easy it is to send requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="62ad1-166">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="62ad1-166">Congratulations!</span></span>  <span data-ttu-id="62ad1-167">Ваше одностраничное приложение, интегрированное с Azure AD, готово.</span><span class="sxs-lookup"><span data-stu-id="62ad1-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="62ad1-168">Протестируйте его.</span><span class="sxs-lookup"><span data-stu-id="62ad1-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="62ad1-169">Приложение может проверять подлинность пользователей, безопасно обращаться к REST API серверной части с помощью OpenID Connect и получать основные сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="62ad1-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about the user.</span></span>  <span data-ttu-id="62ad1-170">По умолчанию оно поддерживает любого пользователя с личной учетной записью Майкрософт или рабочей либо школьной учетной записью из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62ad1-170">Out of the box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="62ad1-171">Попробуйте приложение, выполнив:</span><span class="sxs-lookup"><span data-stu-id="62ad1-171">Give the app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="62ad1-172">Откройте браузер и перейдите по адресу `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="62ad1-172">In a browser navigate to `http://localhost:8080`.</span></span>  <span data-ttu-id="62ad1-173">Войдите с личной учетной записью Майкрософт либо рабочей или школьной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="62ad1-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="62ad1-174">Добавьте задачи в список дел и выйдите.</span><span class="sxs-lookup"><span data-stu-id="62ad1-174">Add tasks to the user's to-do list, and sign out.</span></span>  <span data-ttu-id="62ad1-175">Попробуйте войти с учетной записью другого типа.</span><span class="sxs-lookup"><span data-stu-id="62ad1-175">Try signing in with the other type of account.</span></span> <span data-ttu-id="62ad1-176">Если вам нужен клиент Azure AD для создания рабочих или школьных учетных записей, [узнайте здесь, как его получить](active-directory-howto-tenant.md) (предоставляется бесплатно).</span><span class="sxs-lookup"><span data-stu-id="62ad1-176">If you need an Azure AD tenant to create work/school users, [learn how to get one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="62ad1-177">Чтобы продолжить изучение конечной точки версии 2.0, вернитесь к нашему [руководству разработчика для версии 2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62ad1-177">To continue learning about the the v2.0 endpoint, head back to our [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="62ad1-178">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="62ad1-178">For additional resources, check out:</span></span>

* [<span data-ttu-id="62ad1-179">Образцы Azure на GitHub >></span><span class="sxs-lookup"><span data-stu-id="62ad1-179">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="62ad1-180">Azure AD на Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="62ad1-180">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="62ad1-181">Документация по Azure AD [на сайте Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="62ad1-181">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="62ad1-182">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="62ad1-182">Get security updates for our products</span></span>
<span data-ttu-id="62ad1-183">Рекомендуем вам настроить уведомления о нарушениях безопасности. Это можно сделать, подписавшись на уведомления безопасности консультационных служб на [этой странице](https://technet.microsoft.com/security/dd252948).</span><span class="sxs-lookup"><span data-stu-id="62ad1-183">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

