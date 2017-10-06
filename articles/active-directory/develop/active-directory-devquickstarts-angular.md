---
title: "Приступая к работе AD AngularJS aaaAzure | Документы Microsoft"
description: "Как toobuild одностраничного приложения AngularJS, интегрируется с Azure AD для входа в систему и вызывает Azure API, защищенные AD с помощью OAuth."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: f2991054-8146-4718-a5f7-59b892230ad7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: eca5e1c9662186dfae4f96ca3041f9350583cf79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a>Защита одностраничных приложений AngularJS с помощью Azure AD

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure Active Directory (Azure AD) упрощает простыми и понятными для вас tooadd входа, выхода и безопасные API OAuth вызывает tooyour одностраничного приложения.  Он предоставляет пользователям tooauthenticate приложений с их учетными записями Windows Server Active Directory и использовать любой веб-API, который Azure AD позволяет защитить, например hello API Office 365 или hello Azure API.

Для приложений JavaScript в браузере, Azure AD предоставляет hello библиотеку проверки подлинности Active Directory (ADAL) или adal.js. Цель Hello adal.js — toomake легко и маркеры доступа tooget вашего приложения. toodemonstrate, насколько просто здесь мы выполним сборку AngularJS tooDo список приложений:

* Подписывает hello пользователя в приложении toohello с помощью Azure AD как поставщика удостоверений hello.

* Некоторые сведения о пользователе hello.
* Безопасно вызовы hello приложения tooDo список API с помощью маркеров носителя из Azure AD.
* Подписывает hello выход пользователя из приложения hello.

toobuild hello завершения рабочее приложение, необходимо:

1. Зарегистрировать приложения в Azure AD.
2. Установка ADAL и настройте одностраничного приложения hello.
3. Используйте ADAL toohelp защищенным страницам в одностраничного приложения hello.

tooget к работе, [загрузить каркас приложения hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip). Вам также нужен клиент Azure AD, в котором можно создать пользователей и зарегистрировать приложение. Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).

## <a name="step-1-register-hello-directorysearcher-application"></a>Шаг 1: Регистрация приложения hello DirectorySearcher
tooenable пользователи tooauthenticate приложения и маркеры get, необходимо сначала tooregister его в Azure AD клиента:

1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Если вы вошли в каталогах toomultiple, может потребоваться tooensure вы просматриваете hello правильный каталог. toodo таким образом, на верхней панели hello, выберите свою учетную запись. В разделе hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.
3. Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений**, а затем выберите **Добавить**.
5. Следуйте инструкциям hello и создайте новое веб-приложение или веб-API:
  * **Имя** описывает toousers вашего приложения.
  * **Uri перенаправления** — toowhich расположение hello Azure AD будет возвращать маркеры. расположение по умолчанию Hello в этом примере `https://localhost:44326/`.
6. После завершения регистрации Azure AD присваивает значение приложении tooyour приложения уникальный идентификатор.  Это значение необходимо в следующих разделах hello, поэтому скопируйте его с вкладка "приложение" hello.
7. Adal.js использует toocommunicate неявного потока OAuth hello в Azure AD. Необходимо включить hello неявного потока для приложения:
  1. Щелкните приложение hello и выберите **манифеста** tooopen hello встроенного редактора манифеста.
  2. Найдите hello `oauth2AllowImplicitFlow` свойство. Присвойте ему значение слишком`true`.
  3. Нажмите кнопку **Сохранить** toosave hello манифест.
8. Предоставьте разрешения для приложения в клиенте. Go слишком**параметры** > **свойства** > **требуемые разрешения**и нажмите кнопку hello **GRANT, предоставление разрешений**кнопку на верхней панели hello. Нажмите кнопку **Да** tooconfirm.

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a>Шаг 2: Установка ADAL и настройте одностраничного приложения hello
Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку adal.js и написать код для работы с удостоверением.

### <a name="configure-hello-javascript-client"></a>Настройка клиента JavaScript hello
Сначала добавьте adal.js toohello TodoSPA проекта с помощью консоли диспетчера пакетов hello:
  1. Загрузить [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) и добавьте его toohello `App/Scripts/` каталога проекта.
  2. Загрузить [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) и добавьте его toohello `App/Scripts/` каталога проекта.
  3. Загрузить каждый скрипт до конца hello hello `</body>` в `index.html`:

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a>Настройка сервера hello серверной части
Для одностраничного приложения hello tooDo внутреннего интерфейса List API tooaccept маркеров из браузера hello hello серверной части требуется конфигурации сведения о регистрации приложения hello. В проекте TodoSPA hello откройте `web.config`. Замените значения hello элементов hello в hello `<appSettings>` раздел tooreflect hello значения, используемые в hello портал Azure. Ваш код будет ссылаться на эти значения при каждом использовании ADAL.
  * `ida:Tenant`Представляет домен hello вашего клиента Azure AD — например, contoso.onmicrosoft.com.
  * `ida:Audience`— Идентификатор клиента приложения, скопированный из портала hello hello.

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a>Шаг 3: Используйте ADAL toohelp безопасного страницы одностраничного приложения hello
Adal.js интегрируется с маршрутом AngularJS и поставщиками HTTP, позволяя вам защищать отдельные представления в одностраничных приложениях.

1. В `App/Scripts/app.js`, переведите в модуле adal.js hello:

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. Инициализация `adalProvider` с помощью значений конфигурации hello регистрации вашего приложения, также в `App/Scripts/app.js`:

    ```js
    adalProvider.init(
      {
          instance: 'https://login.microsoftonline.com/',
          tenant: 'Enter your tenant name here e.g. contoso.onmicrosoft.com',
          clientId: 'Enter your client ID here e.g. e9a5a8b6-8af7-4719-9821-0deef255f68e',
          extraQueryParameter: 'nux=1',
          //cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
      },
      $httpProvider
    );
    ```
3. Справка безопасный hello `TodoList` представление в приложение hello с использованием только одной строки кода: `requireADLogin`.

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a>Сводка
Теперь у вас есть безопасного одностраничного приложения, может регистрация пользователей и отправить API внутреннего сервера tooits носителя токен защищенные запросы. Когда пользователь щелкает hello **TodoList** ссылку, adal.js будете автоматически перенаправлены tooAzure AD для входа в систему при необходимости. Кроме того adal.js автоматически подключает к ней доступ маркера tooany Ajax запросов, отправленных toohello приложения серверной части.  

Hello описанные выше шаги являются hello bare минимальные необходимые toobuild одностраничного приложения с помощью adal.js. Но для одностраничных приложений есть еще несколько полезных функций.

* tooexplicitly выдавать запросы входа и выхода из системы, можно определить функции в контроллерах, которые вызывают adal.js.  В `App/Scripts/homeCtrl.js` добавьте:

    ```js
    ...
    $scope.login = function () {
        adalService.login();
    };
    $scope.logout = function () {
        adalService.logOut();
    };
    ...
    ```
* Может потребоваться toopresent учетных данных пользователей в пользовательском Интерфейсе приложения hello. Hello ADAL службы уже был добавлен toohello `userDataCtrl` контроллер, чтобы вы могли использовать hello `userInfo` представление, связанных объектов в hello `App/Views/UserData.html`:

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* Существует множество сценариев, в которых требуется tooknow Если hello пользователь выполнил вход, или нет. Можно также использовать hello `userInfo` объекта toogather эти сведения.  Например, в `index.html`, можно отобразить либо hello **входа** или **выхода** кнопки в зависимости от состояния проверки подлинности:

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

Приложения Azure AD-интегрированные одностраничной может проверять подлинность пользователей, безопасно вызывать его серверной части с помощью OAuth 2.0 и получить основные сведения о пользователе hello. Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям. Запуск приложения списка одностраничной tooDo и войти по одной из этих пользователей. Добавьте список дел задачи toohello пользователя, выйдите из системы и снова выполнить вход.

Adal.js позволяет легко tooincorporate общие функции управления удостоверениями в приложения. Он отвечает за всю работу dirty hello для вас: Управление кэшем, поддержка протокола OAuth, представивший hello пользователя входа в пользовательский Интерфейс, обновление маркеры с истекшим сроком действия и многое другое.

Для ссылки, пример hello завершена (без настройки) доступен в [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).

## <a name="next-steps"></a>Дальнейшие действия
Теперь можно переходить на tooadditional сценариев. Может потребоваться tootry: [вызывать веб-API CORS из одной страницы приложения](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
