---
title: "aaaAzure AD v2.0 Приступая к работе приложения на одной странице NodeJS AngularJS | Документы Microsoft"
description: "Как toobuild углового JS одностраничное приложение, выполняющий вход пользователей с помощью обоих личных Microsoft учетные записи и рабочих или учебных учетных записей."
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
ms.openlocfilehash: 1ab450caf08ab05fba140b94b1b8de652e99cbc1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---nodejs"></a><span data-ttu-id="e4e45-103">Добавление приложения AngularJS tooan вход на одной странице - NodeJS</span><span class="sxs-lookup"><span data-stu-id="e4e45-103">Add sign-in tooan AngularJS single page app - NodeJS</span></span>
<span data-ttu-id="e4e45-104">В этой статье мы добавим вход на платформе Microsoft учетных записей tooan AngularJS приложения с помощью конечной v2.0 hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e4e45-104">In this article we'll add sign in with Microsoft powered accounts tooan AngularJS app using hello Azure Active Directory v2.0 endpoint.</span></span> <span data-ttu-id="e4e45-105">Конечная точка v2.0 Hello позволяют tooperform интеграции единого приложения и проверять подлинность пользователей с учетными записями личных и рабочих или учебного заведения.</span><span class="sxs-lookup"><span data-stu-id="e4e45-105">hello v2.0 endpoint enable you tooperform a single integration in your app and authenticate users with both personal and work/school accounts.</span></span>

<span data-ttu-id="e4e45-106">Этот пример представляет собой простое одностраничное приложение со списком дел, которое сохраняет задачи в серверной части API REST, написанное на NodeJS и защищенное с помощью токенов носителя OAuth из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4e45-106">This sample is a simple To-Do List single page app that stores tasks in a backend REST API, written in NodeJS and secured using OAuth bearer tokens from Azure AD.</span></span>  <span data-ttu-id="e4e45-107">Hello AngularJS приложение будет использовать нашей библиотеке проверки подлинности открытым исходным кодом JavaScript [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello всей входа в систему и получить маркеры для hello вызовах API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="e4e45-107">hello AngularJS app will use our open source JavaScript authentication library [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello entire sign in process and acquire tokens for calling hello REST API.</span></span>  <span data-ttu-id="e4e45-108">Hello же шаблон может быть применен tooauthenticate tooother API REST, например hello [Microsoft Graph](https://graph.microsoft.com) или hello API диспетчера ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e4e45-108">hello same pattern can be applied tooauthenticate tooother REST APIs, like hello [Microsoft Graph](https://graph.microsoft.com) or hello Azure Resource Manager APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="e4e45-109">Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="e4e45-109">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="e4e45-110">toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="e4e45-110">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download"></a><span data-ttu-id="e4e45-111">Загрузить</span><span class="sxs-lookup"><span data-stu-id="e4e45-111">Download</span></span>
<span data-ttu-id="e4e45-112">tooget к работе, вам потребуется toodownload & установки [node.js](https://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="e4e45-112">tooget started, you'll need toodownload & install [node.js](https://nodejs.org).</span></span>  <span data-ttu-id="e4e45-113">Затем можно клонировать или [загрузить](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) скелет приложения:</span><span class="sxs-lookup"><span data-stu-id="e4e45-113">Then you can clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/skeleton.zip) a skeleton app:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS.git
```

<span data-ttu-id="e4e45-114">каркас приложение Hello включает все hello стандартный код для простого приложения AngularJS, но не удалось обнаружить все компоненты, связанные с идентификаторами hello.</span><span class="sxs-lookup"><span data-stu-id="e4e45-114">hello skeleton app includes all hello boilerplate code for a simple AngularJS app, but is missing all of hello identity-related pieces.</span></span>  <span data-ttu-id="e4e45-115">Если вы не хотите toofollow вдоль, вместо этого можно клонировать или [загрузки](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) образец hello завершена.</span><span class="sxs-lookup"><span data-stu-id="e4e45-115">If you don't want toofollow along, you can instead clone or [download](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-NodeJS/archive/complete.zip) hello completed sample.</span></span>

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-NodeJS.git
```

## <a name="register-an-app"></a><span data-ttu-id="e4e45-116">регистрация приложения;</span><span class="sxs-lookup"><span data-stu-id="e4e45-116">Register an app</span></span>
<span data-ttu-id="e4e45-117">Во-первых, создайте приложение в hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните следующие [подробные шаги](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="e4e45-117">First, create an app in hello [App Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="e4e45-118">Не забудьте:</span><span class="sxs-lookup"><span data-stu-id="e4e45-118">Make sure to:</span></span>

* <span data-ttu-id="e4e45-119">Добавить hello **Web** платформы для приложения.</span><span class="sxs-lookup"><span data-stu-id="e4e45-119">Add hello **Web** platform for your app.</span></span>
* <span data-ttu-id="e4e45-120">Введите правильный hello **URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="e4e45-120">Enter hello correct **Redirect URI**.</span></span> <span data-ttu-id="e4e45-121">по умолчанию Hello в данном примере — `http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="e4e45-121">hello default for this sample is `http://localhost:8080`.</span></span>
* <span data-ttu-id="e4e45-122">Оставьте hello **разрешить неявного потока** флажок включено.</span><span class="sxs-lookup"><span data-stu-id="e4e45-122">Leave hello **Allow Implicit Flow** checkbox enabled.</span></span> 

<span data-ttu-id="e4e45-123">Копировать вниз hello **идентификатор приложения** , назначенный tooyour приложение, потребуется скоро.</span><span class="sxs-lookup"><span data-stu-id="e4e45-123">Copy down hello **Application ID** that is assigned tooyour app, you'll need it shortly.</span></span> 

## <a name="install-adaljs"></a><span data-ttu-id="e4e45-124">Установка adal.js</span><span class="sxs-lookup"><span data-stu-id="e4e45-124">Install adal.js</span></span>
<span data-ttu-id="e4e45-125">toostart, перейдите tooproject, который вы загрузили и установить adal.js.</span><span class="sxs-lookup"><span data-stu-id="e4e45-125">toostart, navigate tooproject you downloaded and install adal.js.</span></span>  <span data-ttu-id="e4e45-126">Если у вас установлен [bower](http://bower.io/) , можно просто выполнить эту команду.</span><span class="sxs-lookup"><span data-stu-id="e4e45-126">If you have [bower](http://bower.io/) installed, you can just run this command.</span></span>  <span data-ttu-id="e4e45-127">Для любого несоответствия версий зависимостей просто выберите hello более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e4e45-127">For any dependency version mismatches, just choose hello higher version.</span></span>

```
bower install adal-angular#experimental
```

<span data-ttu-id="e4e45-128">Кроме того, можно вручную загрузить [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) и [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span><span class="sxs-lookup"><span data-stu-id="e4e45-128">Alternatively, you can manually download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) and [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).</span></span>  <span data-ttu-id="e4e45-129">Добавление обоих файлов toohello `app/lib/adal-angular-experimental/dist` каталога.</span><span class="sxs-lookup"><span data-stu-id="e4e45-129">Add both files toohello `app/lib/adal-angular-experimental/dist` directory.</span></span>

<span data-ttu-id="e4e45-130">Теперь откройте проект hello в другом текстовом редакторе и загрузить adal.js конце hello body страницы приветствия:</span><span class="sxs-lookup"><span data-stu-id="e4e45-130">Now open hello project in your favorite text editor, and load adal.js at hello end of hello page body:</span></span>

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a><span data-ttu-id="e4e45-131">Настройка hello REST API</span><span class="sxs-lookup"><span data-stu-id="e4e45-131">Set up hello REST API</span></span>
<span data-ttu-id="e4e45-132">Хотя мы устанавливаем вещей, позволяет серверной части REST API get hello работу.</span><span class="sxs-lookup"><span data-stu-id="e4e45-132">While we're setting things up, lets get hello backend REST API working.</span></span>  <span data-ttu-id="e4e45-133">В командной строке, установить все необходимые пакеты hello, запустив (Убедитесь, что вы находитесь в каталог верхнего уровня hello hello проекта):</span><span class="sxs-lookup"><span data-stu-id="e4e45-133">In a command prompt, install all hello necessary packages by running (make sure you're in hello top-level directory of hello project):</span></span>

```
npm install
```

<span data-ttu-id="e4e45-134">Теперь откройте `config.js` и замените hello `audience` значение:</span><span class="sxs-lookup"><span data-stu-id="e4e45-134">Now open `config.js` and replace hello `audience` value:</span></span>

```js
exports.creds = {

     // TODO: Replace this value with hello Application ID from hello registration portal
     audience: '<Your-application-id>',

     ...
}
```

<span data-ttu-id="e4e45-135">Hello REST API будет использовать этот токены toovalidate значением, получаемым от углового приложение hello на запросы AJAX.</span><span class="sxs-lookup"><span data-stu-id="e4e45-135">hello REST API will use this value toovalidate tokens it receives from hello Angular app on AJAX requests.</span></span>  <span data-ttu-id="e4e45-136">Обратите внимание, что это простой API-Интерфейс REST хранит данные в памяти - таким образом, каждый сервер hello toostop времени, вы потеряете все ранее созданные задачи.</span><span class="sxs-lookup"><span data-stu-id="e4e45-136">Note that this simple REST API stores data in-memory - so each time toostop hello server, you will lose all previously created tasks.</span></span>

<span data-ttu-id="e4e45-137">Вот и все время hello, мы будем toospend обсуждение, как работает hello REST API.</span><span class="sxs-lookup"><span data-stu-id="e4e45-137">That's all hello time we're going toospend discussing how hello REST API works.</span></span>  <span data-ttu-id="e4e45-138">Чувствовать себя свободного toopoke кода hello, но Дополнительные сведения о защите веб-API в Azure AD toolearn следует извлечь [в этой статье](active-directory-v2-devquickstarts-node-api.md).</span><span class="sxs-lookup"><span data-stu-id="e4e45-138">Feel free toopoke around in hello code, but if you want toolearn more about securing web APIs with Azure AD, check out [this article](active-directory-v2-devquickstarts-node-api.md).</span></span> 

## <a name="sign-users-in"></a><span data-ttu-id="e4e45-139">Вход пользователей</span><span class="sxs-lookup"><span data-stu-id="e4e45-139">Sign users in</span></span>
<span data-ttu-id="e4e45-140">Время toowrite некоторый код удостоверения.</span><span class="sxs-lookup"><span data-stu-id="e4e45-140">Time toowrite some identity code.</span></span>  <span data-ttu-id="e4e45-141">Вы уже могли заметить, что в adal.js имеется поставщик AngularJS, который хорошо работает с механизмами маршрутизации Angular.</span><span class="sxs-lookup"><span data-stu-id="e4e45-141">You might have already noticed that adal.js contains an AngularJS provider, which plays nicely with Angular routing mechanisms.</span></span>  <span data-ttu-id="e4e45-142">Начните с добавления toohello приложение hello adal модуля:</span><span class="sxs-lookup"><span data-stu-id="e4e45-142">Start by adding hello adal module toohello app:</span></span>

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

<span data-ttu-id="e4e45-143">Теперь можно инициализировать hello `adalProvider` с помощью идентификатора приложения:</span><span class="sxs-lookup"><span data-stu-id="e4e45-143">You can now initialize hello `adalProvider` with your Application ID:</span></span>

```js
// app/scripts/app.js

...

adalProvider.init({

        // Use this value for hello public instance of Azure AD
        instance: 'https://login.microsoftonline.com/', 

        // hello 'common' endpoint is used for multi-tenant applications like this one
        tenant: 'common',

        // Your application id from hello registration portal
        clientId: '<Your-application-id>',

        // If you're using IE, uncommment this line - hello default HTML5 sessionStorage does not work for localhost.
        //cacheLocation: 'localStorage',

    }, $httpProvider);
```

<span data-ttu-id="e4e45-144">Отлично, теперь adal.js есть все сведения hello ему toosecure пользователей в приложение и выполните вход.</span><span class="sxs-lookup"><span data-stu-id="e4e45-144">Great, now adal.js has all hello information it needs toosecure your app and sign users in.</span></span>  <span data-ttu-id="e4e45-145">tooforce входа для конкретного маршрута в приложение hello, всего лишь отображается только одна строка кода:</span><span class="sxs-lookup"><span data-stu-id="e4e45-145">tooforce sign in for a particular route in hello app, all it takes is one line of code:</span></span>

```js
// app/scripts/app.js

...

}).when("/TodoList", {
    controller: "todoListCtrl",
    templateUrl: "/static/views/TodoList.html",
    requireADLogin: true, // Ensures that hello user must be logged in tooaccess hello route
})

...
```

<span data-ttu-id="e4e45-146">Теперь в том случае, когда пользователь щелкает hello `TodoList` ссылку, adal.js будете автоматически перенаправлены tooAzure AD для входа в систему при необходимости.</span><span class="sxs-lookup"><span data-stu-id="e4e45-146">Now when a user clicks hello `TodoList` link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span>  <span data-ttu-id="e4e45-147">Вы можете явно отправлять запросы на выполнение входа и выхода, вызывая adal.js в контроллерах:</span><span class="sxs-lookup"><span data-stu-id="e4e45-147">You can also explicitly send sign-in and sign-out requests by invoking adal.js in your controllers:</span></span>

```js
// app/scripts/homeCtrl.js

angular.module('todoApp')
// Load adal.js hello same way for use in controllers and views   
.controller('homeCtrl', ['$scope', 'adalAuthenticationService','$location', function ($scope, adalService, $location) {
    $scope.login = function () {

        // Redirect hello user toosign in
        adalService.login();

    };
    $scope.logout = function () {

        // Redirect hello user toolog out    
        adalService.logOut();

    };
...
```

## <a name="display-user-info"></a><span data-ttu-id="e4e45-148">Отображение сведений о пользователе</span><span class="sxs-lookup"><span data-stu-id="e4e45-148">Display user info</span></span>
<span data-ttu-id="e4e45-149">Теперь, когда hello пользователь выполнил вход, возможно, потребуется данные проверки подлинности tooaccess hello выполнившего вход пользователя в приложении.</span><span class="sxs-lookup"><span data-stu-id="e4e45-149">Now that hello user is signed in, you'll probably need tooaccess hello signed-in user's authentication data in your application.</span></span>  <span data-ttu-id="e4e45-150">Adal.js предоставляет эти сведения для вас в hello `userInfo` объекта.</span><span class="sxs-lookup"><span data-stu-id="e4e45-150">Adal.js exposes this information for you in hello `userInfo` object.</span></span>  <span data-ttu-id="e4e45-151">tooaccess этот объект в представлении, сначала следует добавить корневой области adal.js toohello hello соответствующего контроллера:</span><span class="sxs-lookup"><span data-stu-id="e4e45-151">tooaccess this object in a view, first add adal.js toohello root scope of hello corresponding controller:</span></span>

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

<span data-ttu-id="e4e45-152">Затем можно непосредственно обращаться hello `userInfo` объекта в представлении:</span><span class="sxs-lookup"><span data-stu-id="e4e45-152">Then you can directly address hello `userInfo` object in your view:</span></span> 

```html
<!--app/views/UserData.html-->

...

    <!--Get hello user's profile information from hello ADAL userInfo object-->
    <tr ng-repeat="(key, value) in userInfo.profile">
        <td>{{key}}</td>
        <td>{{value}}</td>
    </tr>
...
```

<span data-ttu-id="e4e45-153">Можно также использовать hello `userInfo` объекта toodetermine, если hello пользователь выполнил вход, или нет.</span><span class="sxs-lookup"><span data-stu-id="e4e45-153">You can also use hello `userInfo` object toodetermine if hello user is signed in or not.</span></span>

```html
<!--index.html-->

...

    <!--Use hello ADAL userInfo object tooshow hello right login/logout button-->
    <ul class="nav navbar-nav navbar-right">
        <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
        <li><a class="btn btn-link" ng-hide="userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    </ul>
...
```

## <a name="call-hello-rest-api"></a><span data-ttu-id="e4e45-154">Hello вызовов REST API</span><span class="sxs-lookup"><span data-stu-id="e4e45-154">Call hello REST API</span></span>
<span data-ttu-id="e4e45-155">Наконец это время tooget некоторые маркеры и вызова hello toocreate REST API, чтение, обновление и удаление задачи.</span><span class="sxs-lookup"><span data-stu-id="e4e45-155">Finally, it's time tooget some tokens and call hello REST API toocreate, read, update, and delete tasks.</span></span>  <span data-ttu-id="e4e45-156">И знаете что?</span><span class="sxs-lookup"><span data-stu-id="e4e45-156">Well guess what?</span></span>  <span data-ttu-id="e4e45-157">Нет toodo *вещь*.</span><span class="sxs-lookup"><span data-stu-id="e4e45-157">You don't have toodo *a thing*.</span></span>  <span data-ttu-id="e4e45-158">Adal.js автоматически обеспечит получение, кэширование и обновление токенов.</span><span class="sxs-lookup"><span data-stu-id="e4e45-158">Adal.js will automatically take care of getting, caching, and refreshing tokens.</span></span>  <span data-ttu-id="e4e45-159">Он также берет на себя присоединения этих токенов toooutgoing AJAX запрашивает отправку toohello API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="e4e45-159">It will also take care of attaching those tokens toooutgoing AJAX requests that you send toohello REST API.</span></span>  

<span data-ttu-id="e4e45-160">Как именно это работает?</span><span class="sxs-lookup"><span data-stu-id="e4e45-160">How exactly does this work?</span></span> <span data-ttu-id="e4e45-161">Это все Спасибо toohello возможностей [AngularJS перехватчики](https://docs.angularjs.org/api/ng/service/$http), что позволяет adal.js tootransform исходящих и входящих сообщений http.</span><span class="sxs-lookup"><span data-stu-id="e4e45-161">It's all thanks toohello magic of [AngularJS interceptors](https://docs.angularjs.org/api/ng/service/$http), which allows adal.js tootransform outgoing and incoming http messages.</span></span>  <span data-ttu-id="e4e45-162">Кроме того, adal.js предполагается, что все запросы на отправку toohello того же домена как окно hello следует использовать токены, предназначенные для hello таким же Идентификатором приложения как hello приложения AngularJS.</span><span class="sxs-lookup"><span data-stu-id="e4e45-162">Furthermore, adal.js assumes that any requests send toohello same domain as hello window should use tokens intended for hello same Application ID as hello AngularJS app.</span></span>  <span data-ttu-id="e4e45-163">Именно поэтому мы использовали hello таким же Идентификатором приложения в обоих углового приложение hello и hello NodeJS REST API.</span><span class="sxs-lookup"><span data-stu-id="e4e45-163">This is why we used hello same Application ID in both hello Angular app and in hello NodeJS REST API.</span></span>  <span data-ttu-id="e4e45-164">Конечно можно переопределить это поведение и сообщить adal.js tooget маркеры для других API REST, при необходимости -, но для этой простой сценарий hello будет выполнять значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e4e45-164">Of course, you can override this behavior and tell adal.js tooget tokens for other REST APIs if necessary - but for this simple scenario hello defaults will do.</span></span>

<span data-ttu-id="e4e45-165">Ниже приведен фрагмент, который показывает, насколько просто toosend запросы с носителя токены из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4e45-165">Here's a snippet that shows how easy it is toosend requests with bearer tokens from Azure AD:</span></span>

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

<span data-ttu-id="e4e45-166">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="e4e45-166">Congratulations!</span></span>  <span data-ttu-id="e4e45-167">Ваше одностраничное приложение, интегрированное с Azure AD, готово.</span><span class="sxs-lookup"><span data-stu-id="e4e45-167">Your Azure AD integrated single page app is now complete.</span></span>  <span data-ttu-id="e4e45-168">Протестируйте его.</span><span class="sxs-lookup"><span data-stu-id="e4e45-168">Go ahead, take a bow.</span></span>  <span data-ttu-id="e4e45-169">Он может проверять подлинность пользователей, безопасно вызвать его серверной части REST API с помощью OpenID Connect и получить основные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="e4e45-169">It can authenticate users, securely call its backend REST API using OpenID Connect, and get basic information about hello user.</span></span>  <span data-ttu-id="e4e45-170">В стандартной hello он поддерживает любой пользователь, имеющий личную учетную запись Майкрософт или учетную запись рабочего или учебного заведения из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4e45-170">Out of hello box, it supports any user with a personal Microsoft Account or a work/school account from Azure AD.</span></span>  <span data-ttu-id="e4e45-171">Попробуйте приложение hello, выполнив:</span><span class="sxs-lookup"><span data-stu-id="e4e45-171">Give hello app a try by running:</span></span>

```
node server.js
```

<span data-ttu-id="e4e45-172">В браузере перейдите слишком`http://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="e4e45-172">In a browser navigate too`http://localhost:8080`.</span></span>  <span data-ttu-id="e4e45-173">Войдите с личной учетной записью Майкрософт либо рабочей или учебной учетной записью.</span><span class="sxs-lookup"><span data-stu-id="e4e45-173">Sign in using either a personal Microsoft account or a work/school account.</span></span>  <span data-ttu-id="e4e45-174">Добавьте список дел задачи toohello пользователя и выйдите из системы.  Попробуйте подписи с помощью hello другой тип учетной записи.</span><span class="sxs-lookup"><span data-stu-id="e4e45-174">Add tasks toohello user's to-do list, and sign out.  Try signing in with hello other type of account.</span></span> <span data-ttu-id="e4e45-175">Если требуется, чтобы пользователи Azure AD клиента toocreate рабочего или учебного заведения, [Узнайте, как один здесь tooget](active-directory-howto-tenant.md) (бесплатно).</span><span class="sxs-lookup"><span data-stu-id="e4e45-175">If you need an Azure AD tenant toocreate work/school users, [learn how tooget one here](active-directory-howto-tenant.md) (it's free).</span></span>

<span data-ttu-id="e4e45-176">обучающие материалы по hello toocontinue Здравствуйте v2.0 конечной точки, head задней tooour [руководстве разработчика v2.0](active-directory-appmodel-v2-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e4e45-176">toocontinue learning about hello hello v2.0 endpoint, head back tooour [v2.0 developer guide](active-directory-appmodel-v2-overview.md).</span></span>  <span data-ttu-id="e4e45-177">Дополнительные ресурсы:</span><span class="sxs-lookup"><span data-stu-id="e4e45-177">For additional resources, check out:</span></span>

* [<span data-ttu-id="e4e45-178">Образцы Azure на GitHub >></span><span class="sxs-lookup"><span data-stu-id="e4e45-178">Azure-Samples on GitHub >></span></span>](https://github.com/Azure-Samples)
* [<span data-ttu-id="e4e45-179">Azure AD на Stack Overflow >></span><span class="sxs-lookup"><span data-stu-id="e4e45-179">Azure AD on Stack Overflow >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* <span data-ttu-id="e4e45-180">Документация по Azure AD [на сайте Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span><span class="sxs-lookup"><span data-stu-id="e4e45-180">Azure AD documentation on [Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)</span></span>

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="e4e45-181">Получение обновлений системы безопасности для наших продуктов</span><span class="sxs-lookup"><span data-stu-id="e4e45-181">Get security updates for our products</span></span>
<span data-ttu-id="e4e45-182">Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.</span><span class="sxs-lookup"><span data-stu-id="e4e45-182">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

