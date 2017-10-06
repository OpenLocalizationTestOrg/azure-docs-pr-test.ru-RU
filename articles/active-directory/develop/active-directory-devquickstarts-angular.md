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
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="a3d1d-103">Защита одностраничных приложений AngularJS с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="a3d1d-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="a3d1d-104">Azure Active Directory (Azure AD) упрощает простыми и понятными для вас tooadd входа, выхода и безопасные API OAuth вызывает tooyour одностраничного приложения.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you tooadd sign-in, sign-out, and secure OAuth API calls tooyour single-page apps.</span></span>  <span data-ttu-id="a3d1d-105">Он предоставляет пользователям tooauthenticate приложений с их учетными записями Windows Server Active Directory и использовать любой веб-API, который Azure AD позволяет защитить, например hello API Office 365 или hello Azure API.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-105">It enables your apps tooauthenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="a3d1d-106">Для приложений JavaScript в браузере, Azure AD предоставляет hello библиотеку проверки подлинности Active Directory (ADAL) или adal.js.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-106">For JavaScript applications running in a browser, Azure AD provides hello Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="a3d1d-107">Цель Hello adal.js — toomake легко и маркеры доступа tooget вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-107">hello sole purpose of adal.js is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="a3d1d-108">toodemonstrate, насколько просто здесь мы выполним сборку AngularJS tooDo список приложений:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-108">toodemonstrate just how easy it is, here we'll build an AngularJS tooDo List application that:</span></span>

* <span data-ttu-id="a3d1d-109">Подписывает hello пользователя в приложении toohello с помощью Azure AD как поставщика удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-109">Signs hello user in toohello app by using Azure AD as hello identity provider.</span></span>

* <span data-ttu-id="a3d1d-110">Некоторые сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-110">Displays some information about hello user.</span></span>
* <span data-ttu-id="a3d1d-111">Безопасно вызовы hello приложения tooDo список API с помощью маркеров носителя из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-111">Securely calls hello app's tooDo List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="a3d1d-112">Подписывает hello выход пользователя из приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-112">Signs hello user out of hello app.</span></span>

<span data-ttu-id="a3d1d-113">toobuild hello завершения рабочее приложение, необходимо:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-113">toobuild hello complete, working application, you need to:</span></span>

1. <span data-ttu-id="a3d1d-114">Зарегистрировать приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="a3d1d-115">Установка ADAL и настройте одностраничного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-115">Install ADAL and configure hello single-page app.</span></span>
3. <span data-ttu-id="a3d1d-116">Используйте ADAL toohelp защищенным страницам в одностраничного приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-116">Use ADAL toohelp secure pages in hello single-page app.</span></span>

<span data-ttu-id="a3d1d-117">tooget к работе, [загрузить каркас приложения hello](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) или [загрузить образец hello завершения](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a3d1d-117">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="a3d1d-118">Вам также нужен клиент Azure AD, в котором можно создать пользователей и зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="a3d1d-119">Если у вас еще нет клиента, [Узнайте, как один tooget](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="a3d1d-119">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-hello-directorysearcher-application"></a><span data-ttu-id="a3d1d-120">Шаг 1: Регистрация приложения hello DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="a3d1d-120">Step 1: Register hello DirectorySearcher application</span></span>
<span data-ttu-id="a3d1d-121">tooenable пользователи tooauthenticate приложения и маркеры get, необходимо сначала tooregister его в Azure AD клиента:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-121">tooenable your app tooauthenticate users and get tokens, you first need tooregister it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="a3d1d-122">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3d1d-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a3d1d-123">Если вы вошли в каталогах toomultiple, может потребоваться tooensure вы просматриваете hello правильный каталог.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-123">If you are signed in toomultiple directories, you may need tooensure you are viewing hello correct directory.</span></span> <span data-ttu-id="a3d1d-124">toodo таким образом, на верхней панели hello, выберите свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-124">toodo so, on hello top bar, click your account.</span></span> <span data-ttu-id="a3d1d-125">В разделе hello **каталога** выберите клиента hello Azure AD, где требуется tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-125">Under hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="a3d1d-126">Нажмите кнопку **более служб** в hello левой панели, а затем выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="a3d1d-127">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="a3d1d-128">Следуйте инструкциям hello и создайте новое веб-приложение или веб-API:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-128">Follow hello prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="a3d1d-129">**Имя** описывает toousers вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-129">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="a3d1d-130">**Uri перенаправления** — toowhich расположение hello Azure AD будет возвращать маркеры.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-130">**Redirect Uri** is hello location toowhich Azure AD will return tokens.</span></span> <span data-ttu-id="a3d1d-131">расположение по умолчанию Hello в этом примере `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-131">hello default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="a3d1d-132">После завершения регистрации Azure AD присваивает значение приложении tooyour приложения уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-132">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span>  <span data-ttu-id="a3d1d-133">Это значение необходимо в следующих разделах hello, поэтому скопируйте его с вкладка "приложение" hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-133">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="a3d1d-134">Adal.js использует toocommunicate неявного потока OAuth hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-134">Adal.js uses hello OAuth implicit flow toocommunicate with Azure AD.</span></span> <span data-ttu-id="a3d1d-135">Необходимо включить hello неявного потока для приложения:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-135">You must enable hello implicit flow for your application:</span></span>
  1. <span data-ttu-id="a3d1d-136">Щелкните приложение hello и выберите **манифеста** tooopen hello встроенного редактора манифеста.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-136">Click hello application and select **Manifest** tooopen hello inline manifest editor.</span></span>
  2. <span data-ttu-id="a3d1d-137">Найдите hello `oauth2AllowImplicitFlow` свойство.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-137">Locate hello `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="a3d1d-138">Присвойте ему значение слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-138">Set its value too`true`.</span></span>
  3. <span data-ttu-id="a3d1d-139">Нажмите кнопку **Сохранить** toosave hello манифест.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-139">Click **Save** toosave hello manifest.</span></span>
8. <span data-ttu-id="a3d1d-140">Предоставьте разрешения для приложения в клиенте.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="a3d1d-141">Go слишком**параметры** > **свойства** > **требуемые разрешения**и нажмите кнопку hello **GRANT, предоставление разрешений**кнопку на верхней панели hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-141">Go too**Settings** > **Properties** > **Required Permissions**, and click hello **Grant Permissions** button on hello top bar.</span></span> <span data-ttu-id="a3d1d-142">Нажмите кнопку **Да** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-142">Click **Yes** tooconfirm.</span></span>

## <a name="step-2-install-adal-and-configure-hello-single-page-app"></a><span data-ttu-id="a3d1d-143">Шаг 2: Установка ADAL и настройте одностраничного приложения hello</span><span class="sxs-lookup"><span data-stu-id="a3d1d-143">Step 2: Install ADAL and configure hello single-page app</span></span>
<span data-ttu-id="a3d1d-144">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку adal.js и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-hello-javascript-client"></a><span data-ttu-id="a3d1d-145">Настройка клиента JavaScript hello</span><span class="sxs-lookup"><span data-stu-id="a3d1d-145">Configure hello JavaScript client</span></span>
<span data-ttu-id="a3d1d-146">Сначала добавьте adal.js toohello TodoSPA проекта с помощью консоли диспетчера пакетов hello:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-146">Begin by adding adal.js toohello TodoSPA project by using hello Package Manager Console:</span></span>
  1. <span data-ttu-id="a3d1d-147">Загрузить [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) и добавьте его toohello `App/Scripts/` каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it toohello `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="a3d1d-148">Загрузить [adal angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) и добавьте его toohello `App/Scripts/` каталога проекта.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it toohello `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="a3d1d-149">Загрузить каждый скрипт до конца hello hello `</body>` в `index.html`:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-149">Load each script before hello end of hello `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-hello-back-end-server"></a><span data-ttu-id="a3d1d-150">Настройка сервера hello серверной части</span><span class="sxs-lookup"><span data-stu-id="a3d1d-150">Configure hello back end server</span></span>
<span data-ttu-id="a3d1d-151">Для одностраничного приложения hello tooDo внутреннего интерфейса List API tooaccept маркеров из браузера hello hello серверной части требуется конфигурации сведения о регистрации приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-151">For hello single-page app's back-end tooDo List API tooaccept tokens from hello browser, hello back end needs configuration information about hello app registration.</span></span> <span data-ttu-id="a3d1d-152">В проекте TodoSPA hello откройте `web.config`.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-152">In hello TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="a3d1d-153">Замените значения hello элементов hello в hello `<appSettings>` раздел tooreflect hello значения, используемые в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-153">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="a3d1d-154">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="a3d1d-155">`ida:Tenant`Представляет домен hello вашего клиента Azure AD — например, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-155">`ida:Tenant` is hello domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="a3d1d-156">`ida:Audience`— Идентификатор клиента приложения, скопированный из портала hello hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-156">`ida:Audience` is hello client ID of your application that you copied from hello portal.</span></span>

## <a name="step-3-use-adal-toohelp-secure-pages-in-hello-single-page-app"></a><span data-ttu-id="a3d1d-157">Шаг 3: Используйте ADAL toohelp безопасного страницы одностраничного приложения hello</span><span class="sxs-lookup"><span data-stu-id="a3d1d-157">Step 3: Use ADAL toohelp secure pages in hello single-page app</span></span>
<span data-ttu-id="a3d1d-158">Adal.js интегрируется с маршрутом AngularJS и поставщиками HTTP, позволяя вам защищать отдельные представления в одностраничных приложениях.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="a3d1d-159">В `App/Scripts/app.js`, переведите в модуле adal.js hello:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-159">In `App/Scripts/app.js`, bring in hello adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="a3d1d-160">Инициализация `adalProvider` с помощью значений конфигурации hello регистрации вашего приложения, также в `App/Scripts/app.js`:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-160">Initialize `adalProvider` by using hello configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="a3d1d-161">Справка безопасный hello `TodoList` представление в приложение hello с использованием только одной строки кода: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-161">Help secure hello `TodoList` view in hello app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="a3d1d-162">Сводка</span><span class="sxs-lookup"><span data-stu-id="a3d1d-162">Summary</span></span>
<span data-ttu-id="a3d1d-163">Теперь у вас есть безопасного одностраничного приложения, может регистрация пользователей и отправить API внутреннего сервера tooits носителя токен защищенные запросы.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests tooits back-end API.</span></span> <span data-ttu-id="a3d1d-164">Когда пользователь щелкает hello **TodoList** ссылку, adal.js будете автоматически перенаправлены tooAzure AD для входа в систему при необходимости.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-164">When a user clicks hello **TodoList** link, adal.js will automatically redirect tooAzure AD for sign-in if necessary.</span></span> <span data-ttu-id="a3d1d-165">Кроме того adal.js автоматически подключает к ней доступ маркера tooany Ajax запросов, отправленных toohello приложения серверной части.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-165">In addition, adal.js will automatically attach an access token tooany Ajax requests that are sent toohello app's back end.</span></span>  

<span data-ttu-id="a3d1d-166">Hello описанные выше шаги являются hello bare минимальные необходимые toobuild одностраничного приложения с помощью adal.js.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-166">hello preceding steps are hello bare minimum necessary toobuild a single-page app by using adal.js.</span></span> <span data-ttu-id="a3d1d-167">Но для одностраничных приложений есть еще несколько полезных функций.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="a3d1d-168">tooexplicitly выдавать запросы входа и выхода из системы, можно определить функции в контроллерах, которые вызывают adal.js.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-168">tooexplicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="a3d1d-169">В `App/Scripts/homeCtrl.js` добавьте:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="a3d1d-170">Может потребоваться toopresent учетных данных пользователей в пользовательском Интерфейсе приложения hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-170">You might want toopresent user information in hello app's UI.</span></span> <span data-ttu-id="a3d1d-171">Hello ADAL службы уже был добавлен toohello `userDataCtrl` контроллер, чтобы вы могли использовать hello `userInfo` представление, связанных объектов в hello `App/Views/UserData.html`:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-171">hello ADAL service has already been added toohello `userDataCtrl` controller, so you can access hello `userInfo` object in hello associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="a3d1d-172">Существует множество сценариев, в которых требуется tooknow Если hello пользователь выполнил вход, или нет.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-172">There are many scenarios in which you'll want tooknow if hello user is signed in or not.</span></span> <span data-ttu-id="a3d1d-173">Можно также использовать hello `userInfo` объекта toogather эти сведения.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-173">You can also use hello `userInfo` object toogather this information.</span></span>  <span data-ttu-id="a3d1d-174">Например, в `index.html`, можно отобразить либо hello **входа** или **выхода** кнопки в зависимости от состояния проверки подлинности:</span><span class="sxs-lookup"><span data-stu-id="a3d1d-174">For instance, in `index.html`, you can show either hello **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="a3d1d-175">Приложения Azure AD-интегрированные одностраничной может проверять подлинность пользователей, безопасно вызывать его серверной части с помощью OAuth 2.0 и получить основные сведения о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about hello user.</span></span> <span data-ttu-id="a3d1d-176">Если это еще не сделано, пришло время toopopulate hello вашего клиента с некоторым пользователям.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-176">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span> <span data-ttu-id="a3d1d-177">Запуск приложения списка одностраничной tooDo и войти по одной из этих пользователей.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-177">Run your tooDo List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="a3d1d-178">Добавьте список дел задачи toohello пользователя, выйдите из системы и снова выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-178">Add tasks toohello user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="a3d1d-179">Adal.js позволяет легко tooincorporate общие функции управления удостоверениями в приложения.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-179">Adal.js makes it easy tooincorporate common identity features into your application.</span></span> <span data-ttu-id="a3d1d-180">Он отвечает за всю работу dirty hello для вас: Управление кэшем, поддержка протокола OAuth, представивший hello пользователя входа в пользовательский Интерфейс, обновление маркеры с истекшим сроком действия и многое другое.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-180">It takes care of all hello dirty work for you: cache management, OAuth protocol support, presenting hello user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="a3d1d-181">Для ссылки, пример hello завершена (без настройки) доступен в [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="a3d1d-181">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3d1d-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3d1d-182">Next steps</span></span>
<span data-ttu-id="a3d1d-183">Теперь можно переходить на tooadditional сценариев.</span><span class="sxs-lookup"><span data-stu-id="a3d1d-183">You can now move on tooadditional scenarios.</span></span> <span data-ttu-id="a3d1d-184">Может потребоваться tootry: [вызывать веб-API CORS из одной страницы приложения](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="a3d1d-184">You might want tootry: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
