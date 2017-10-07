---
title: "aaaAzure AD приложения на одной странице v2.0 .NET AngularJS Приступая к работе | Документы Microsoft"
description: "Как toobuild углового JS одностраничное приложение, выполняющий вход пользователей с помощью обоих личных Microsoft учетные записи и рабочих или учебных учетных записей."
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
ms.openlocfilehash: bd3fc8dce91eb0bedcbfed47a9b3ef52c5568c6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-angularjs-single-page-app---net"></a>Добавление приложения AngularJS tooan вход на одной странице - .NET
В этой статье мы добавим вход на платформе Microsoft учетных записей tooan AngularJS приложения с помощью конечной v2.0 hello Azure Active Directory.  Конечная точка v2.0 Hello позволяет tooperform интеграции единого приложения и проверять подлинность пользователей с учетными записями личных и рабочих или учебного заведения.

Этот образец представляет собой простой список дел одностраничное приложение сохраняет задачи в серверной части REST API, написанные с использованием платформы .NET 4.5 MVC hello и защищено с помощью маркеров носителя OAuth из Azure AD.  Hello AngularJS приложение будет использовать нашей библиотеке проверки подлинности открытым исходным кодом JavaScript [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js) toohandle hello всей входа в систему и получить маркеры для hello вызовах API-интерфейса REST.  Hello же шаблон может быть применен tooauthenticate tooother API REST, например hello [Microsoft Graph](https://graph.microsoft.com).

> [!NOTE]
> Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.  toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download"></a>Загрузить
tooget к работе, будет необходимо toodownload & установки Visual Studio.  Затем можно клонировать или [загрузить](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) скелет приложения:

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet.git
```

каркас приложение Hello включает все hello стандартный код для простого приложения AngularJS, но не удалось обнаружить все компоненты, связанные с идентификаторами hello.  Если вы не хотите toofollow вдоль, вместо этого можно клонировать или [загрузки](https://github.com/AzureADQuickStarts/AppModelv2-SinglePageApp-AngularJS-DotNet/archive/complete.zip) образец hello завершена.

```
git clone https://github.com/AzureADSamples/SinglePageApp-AngularJS-DotNet.git
```

## <a name="register-an-app"></a>регистрация приложения;
Во-первых, создайте приложение в hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или выполните следующие [подробные шаги](active-directory-v2-app-registration.md).  Не забудьте:

* Добавить hello **Web** платформы для приложения.
* Введите правильный hello **URI перенаправления**. по умолчанию Hello в данном примере — `https://localhost:44326/`.
* Оставьте hello **разрешить неявного потока** флажок включено. 

Копировать вниз hello **идентификатор приложения** , назначенный tooyour приложение, потребуется скоро. 

## <a name="install-adaljs"></a>Установка adal.js
toostart, перейдите tooproject, который вы загрузили и установить adal.js.  Если у вас установлен [bower](http://bower.io/) , можно просто выполнить эту команду.  Для любого несоответствия версий зависимостей просто выберите hello более поздней версии.

```
bower install adal-angular#experimental
```

Кроме того, можно вручную загрузить [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal.min.js) и [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/experimental/dist/adal-angular.min.js).  Добавление обоих файлов toohello `app/lib/adal-angular-experimental/dist` каталог hello `TodoSPA` проекта.

Теперь откройте hello проект в Visual Studio и загрузить adal.js конце hello текст hello Главная страница:

```html
<!--index.html-->

...

<script src="App/bower_components/dist/adal.min.js"></script>
<script src="App/bower_components/dist/adal-angular.min.js"></script>

...
```

## <a name="set-up-hello-rest-api"></a>Настройка hello REST API
Хотя мы устанавливаем вещей, давайте hello серверной части REST API рабочий.  В корневой hello hello проекта, откройте `web.config` и замените hello `audience` значение.  Hello REST API будет использовать этот токены toovalidate значением, получаемым от углового приложение hello на запросы AJAX.

```xml
<!--web.config-->

...

    <appSettings>
        <add key="ida:Audience" value="[Your-application-id]" />
    </appSettings>

...
```

Вот и все время hello, мы будем toospend обсуждение, как работает hello REST API.  Чувствовать себя свободного toopoke кода hello, но Дополнительные сведения о защите веб-API в Azure AD toolearn следует извлечь [в этой статье](active-directory-v2-devquickstarts-dotnet-api.md). 

## <a name="sign-users-in"></a>Вход пользователей
Время toowrite некоторый код удостоверения.  Вы уже могли заметить, что в adal.js имеется поставщик AngularJS, который хорошо работает с механизмами маршрутизации Angular.  Начните с добавления toohello приложение hello adal модуля:

```js
// app/scripts/app.js

angular.module('todoApp', ['ngRoute','AdalAngular'])
.config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
 function ($routeProvider, $httpProvider, adalProvider) {

...
```

Теперь можно инициализировать hello `adalProvider` с помощью идентификатора приложения:

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

Отлично, теперь adal.js есть все сведения hello ему toosecure пользователей в приложение и выполните вход.  tooforce входа для конкретного маршрута в приложение hello, всего лишь отображается только одна строка кода:

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

Теперь в том случае, когда пользователь щелкает hello `TodoList` ссылку, adal.js будете автоматически перенаправлены tooAzure AD для входа в систему при необходимости.  Вы можете явно отправлять запросы на выполнение входа и выхода, вызывая adal.js в контроллерах:

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

## <a name="display-user-info"></a>Отображение сведений о пользователе
Теперь, когда hello пользователь выполнил вход, возможно, потребуется данные проверки подлинности tooaccess hello выполнившего вход пользователя в приложении.  Adal.js предоставляет эти сведения для вас в hello `userInfo` объекта.  tooaccess этот объект в представлении, сначала следует добавить корневой области adal.js toohello hello соответствующего контроллера:

```js
// app/scripts/userDataCtrl.js

angular.module('todoApp')
// Load ADAL for use in view
.controller('userDataCtrl', ['$scope', 'adalAuthenticationService', function ($scope, adalService) {}]);
```

Затем можно непосредственно обращаться hello `userInfo` объекта в представлении: 

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

Можно также использовать hello `userInfo` объекта toodetermine, если hello пользователь выполнил вход, или нет.

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

## <a name="call-hello-rest-api"></a>Hello вызовов REST API
Наконец это время tooget некоторые маркеры и вызова hello toocreate REST API, чтение, обновление и удаление задачи.  И знаете что?  Нет toodo *вещь*.  Adal.js автоматически обеспечит получение, кэширование и обновление токенов.  Он также берет на себя присоединения этих токенов toooutgoing AJAX запрашивает отправку toohello API-интерфейса REST.  

Как именно это работает? Это все Спасибо toohello возможностей [AngularJS перехватчики](https://docs.angularjs.org/api/ng/service/$http), что позволяет adal.js tootransform исходящих и входящих сообщений http.  Кроме того, adal.js предполагается, что все запросы на отправку toohello того же домена как окно hello следует использовать токены, предназначенные для hello таким же Идентификатором приложения как hello приложения AngularJS.  Именно поэтому мы использовали hello таким же Идентификатором приложения в обоих углового приложение hello и hello NodeJS REST API.  Конечно можно переопределить это поведение и сообщить adal.js tooget маркеры для других API REST, при необходимости -, но для этой простой сценарий hello будет выполнять значения по умолчанию.

Ниже приведен фрагмент, который показывает, насколько просто toosend запросы с носителя токены из Azure AD.

```js
// app/scripts/todoListSvc.js

...
return $http.get('/api/tasks');
...
```

Поздравляем!  Ваше одностраничное приложение, интегрированное с Azure AD, готово.  Протестируйте его.  Он может проверять подлинность пользователей, безопасно вызвать его серверной части REST API с помощью OpenID Connect и получить основные сведения о пользователе hello.  В стандартной hello он поддерживает любой пользователь, имеющий личную учетную запись Майкрософт или учетную запись рабочего или учебного заведения из Azure AD.  Выполните приложение hello и в браузере перейдите слишком`https://localhost:44326/`.  Войдите с личной учетной записью Майкрософт либо рабочей или учебной учетной записью.  Добавьте список дел задачи toohello пользователя и выйдите из системы.  Попробуйте подписи с помощью hello другой тип учетной записи. Если требуется, чтобы пользователи Azure AD клиента toocreate рабочего или учебного заведения, [Узнайте, как один здесь tooget](active-directory-howto-tenant.md) (бесплатно).

обучающие материалы по v2.0 hello конечной точки, головной назад tooour toocontinue [руководстве разработчика v2.0](active-directory-appmodel-v2-overview.md).  Дополнительные ресурсы:

* [Образцы Azure на GitHub >>](https://github.com/Azure-Samples)
* [Azure AD на Stack Overflow >>](http://stackoverflow.com/questions/tagged/azure-active-directory)
* Документация по Azure AD [на сайте Azure.com >>](https://azure.microsoft.com/documentation/services/active-directory/)

## <a name="get-security-updates-for-our-products"></a>Получение обновлений системы безопасности для наших продуктов
Мы рекомендуем вам уведомления при возникновении события безопасности, посетив tooget [эту страницу](https://technet.microsoft.com/security/dd252948) и подписка tooSecurity рекомендация предупреждения.

