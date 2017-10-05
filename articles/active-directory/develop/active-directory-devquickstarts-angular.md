---
title: "Приступая к работе с Azure AD на AngularJS | Документация Майкрософт"
description: "Практическое руководство по созданию одностраничного приложения на AngularJS, которое выполняет вход через Azure AD и вызывает API-интерфейсы, защищенные в Azure AD, по протоколу OAuth."
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
ms.openlocfilehash: 4153910bc03f112f84c26cda6f9c78f11028b934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="help-secure-angularjs-single-page-apps-by-using-azure-ad"></a><span data-ttu-id="903eb-103">Защита одностраничных приложений AngularJS с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="903eb-103">Help secure AngularJS single-page apps by using Azure AD</span></span>

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="903eb-104">Используя Azure Active Directory (Azure AD), разработчики могут не только легко реализовать процедуры входа и выхода пользователей, но и защищать вызовы к API одностраничных приложений по протоколу OAuth.</span><span class="sxs-lookup"><span data-stu-id="903eb-104">Azure Active Directory (Azure AD) makes it simple and straightforward for you to add sign-in, sign-out, and secure OAuth API calls to your single-page apps.</span></span>  <span data-ttu-id="903eb-105">Также разработчик сможет осуществлять аутентификацию пользователей по учетным записям Active Directory Windows Server и использовать любые веб-интерфейсы API, защищенные в Azure AD, включая API Office 365 или API Azure.</span><span class="sxs-lookup"><span data-stu-id="903eb-105">It enables your apps to authenticate users with their Windows Server Active Directory accounts and consume any web API that Azure AD helps protect, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="903eb-106">Для JavaScript-приложений, выполняющихся в браузере, Azure AD предоставляет библиотеку adal.js, используемую при аутентификации в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="903eb-106">For JavaScript applications running in a browser, Azure AD provides the Active Directory Authentication Library (ADAL), or adal.js.</span></span> <span data-ttu-id="903eb-107">Adal.js выполняет единственную функцию — упрощает получение маркеров доступа.</span><span class="sxs-lookup"><span data-stu-id="903eb-107">The sole purpose of adal.js is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="903eb-108">Чтобы показать, насколько это просто, создадим приложение To Do List (список дел) на AngularJS, которое:</span><span class="sxs-lookup"><span data-stu-id="903eb-108">To demonstrate just how easy it is, here we'll build an AngularJS To Do List application that:</span></span>

* <span data-ttu-id="903eb-109">выполняет вход пользователя в приложение, используя Azure AD как поставщика удостоверений;</span><span class="sxs-lookup"><span data-stu-id="903eb-109">Signs the user in to the app by using Azure AD as the identity provider.</span></span>

* <span data-ttu-id="903eb-110">Отображает некоторые сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="903eb-110">Displays some information about the user.</span></span>
* <span data-ttu-id="903eb-111">безопасно вызывает реализованный в приложении интерфейс приложения со списком дел, используя токены носителя из Azure AD;</span><span class="sxs-lookup"><span data-stu-id="903eb-111">Securely calls the app's To Do List API by using bearer tokens from Azure AD.</span></span>
* <span data-ttu-id="903eb-112">Обеспечивает функцию выхода пользователя из приложения.</span><span class="sxs-lookup"><span data-stu-id="903eb-112">Signs the user out of the app.</span></span>

<span data-ttu-id="903eb-113">Для создания полного и действующего приложения вам потребуется следующее.</span><span class="sxs-lookup"><span data-stu-id="903eb-113">To build the complete, working application, you need to:</span></span>

1. <span data-ttu-id="903eb-114">Зарегистрировать приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="903eb-114">Register your app with Azure AD.</span></span>
2. <span data-ttu-id="903eb-115">Установить библиотеку ADAL и настроить одностраничное приложение.</span><span class="sxs-lookup"><span data-stu-id="903eb-115">Install ADAL and configure the single-page app.</span></span>
3. <span data-ttu-id="903eb-116">Применить ADAL для защиты страниц одностраничного приложения.</span><span class="sxs-lookup"><span data-stu-id="903eb-116">Use ADAL to help secure pages in the single-page app.</span></span>

<span data-ttu-id="903eb-117">Чтобы начать работу, [скачайте схему приложения](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) или [скачайте готовый пример](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="903eb-117">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="903eb-118">Вам также нужен клиент Azure AD, в котором можно создать пользователей и зарегистрировать приложение.</span><span class="sxs-lookup"><span data-stu-id="903eb-118">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="903eb-119">Если клиента нет, [узнайте, как его получить](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="903eb-119">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-register-the-directorysearcher-application"></a><span data-ttu-id="903eb-120">Шаг 1. Регистрация приложения DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="903eb-120">Step 1: Register the DirectorySearcher application</span></span>
<span data-ttu-id="903eb-121">Чтобы приложение могло осуществлять аутентификацию пользователей и получать маркеры, необходимо зарегистрировать его в клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="903eb-121">To enable your app to authenticate users and get tokens, you first need to register it in your Azure AD tenant:</span></span>

1. <span data-ttu-id="903eb-122">Выполните вход на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="903eb-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="903eb-123">Если вы вошли в несколько каталогов, убедитесь, что вы просматриваете правильный каталог.</span><span class="sxs-lookup"><span data-stu-id="903eb-123">If you are signed in to multiple directories, you may need to ensure you are viewing the correct directory.</span></span> <span data-ttu-id="903eb-124">Для этого на верхней панели щелкните свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="903eb-124">To do so, on the top bar, click your account.</span></span> <span data-ttu-id="903eb-125">В списке **Каталог** выберите клиент Azure AD для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="903eb-125">Under the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="903eb-126">В области слева щелкните **Больше служб** и выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="903eb-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="903eb-127">Щелкните **Регистрация приложений**, а затем выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="903eb-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="903eb-128">Следуйте инструкциям на экране, а затем создайте новое веб-приложение и (или) веб-API.</span><span class="sxs-lookup"><span data-stu-id="903eb-128">Follow the prompts and create a new web application and/or web API:</span></span>
  * <span data-ttu-id="903eb-129">**Имя** приложения является его описанием для пользователей.</span><span class="sxs-lookup"><span data-stu-id="903eb-129">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="903eb-130">**URI перенаправления** — расположение, в которое Azure AD будет возвращать маркеры.</span><span class="sxs-lookup"><span data-stu-id="903eb-130">**Redirect Uri** is the location to which Azure AD will return tokens.</span></span> <span data-ttu-id="903eb-131">Для нашего примера значением по умолчанию будет `https://localhost:44326/`.</span><span class="sxs-lookup"><span data-stu-id="903eb-131">The default location for this sample is `https://localhost:44326/`.</span></span>
6. <span data-ttu-id="903eb-132">Когда вы завершите регистрацию, Azure AD присвоит приложению уникальный идентификатор приложения.</span><span class="sxs-lookup"><span data-stu-id="903eb-132">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span>  <span data-ttu-id="903eb-133">Это значение вам понадобится в следующих разделах, поэтому скопируйте его с вкладки приложения.</span><span class="sxs-lookup"><span data-stu-id="903eb-133">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="903eb-134">Библиотека adal.js использует неявный поток OAuth для взаимодействия с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="903eb-134">Adal.js uses the OAuth implicit flow to communicate with Azure AD.</span></span> <span data-ttu-id="903eb-135">Подключите этот неявный поток к своему приложению, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="903eb-135">You must enable the implicit flow for your application:</span></span>
  1. <span data-ttu-id="903eb-136">Щелкните приложение и выберите **Манифест**, чтобы открыть встроенный редактор манифеста.</span><span class="sxs-lookup"><span data-stu-id="903eb-136">Click the application and select **Manifest** to open the inline manifest editor.</span></span>
  2. <span data-ttu-id="903eb-137">Найдите свойство `oauth2AllowImplicitFlow`.</span><span class="sxs-lookup"><span data-stu-id="903eb-137">Locate the `oauth2AllowImplicitFlow` property.</span></span> <span data-ttu-id="903eb-138">Задайте для него значение `true`.</span><span class="sxs-lookup"><span data-stu-id="903eb-138">Set its value to `true`.</span></span>
  3. <span data-ttu-id="903eb-139">Нажмите кнопку **Сохранить**, чтобы сохранить манифест.</span><span class="sxs-lookup"><span data-stu-id="903eb-139">Click **Save** to save the manifest.</span></span>
8. <span data-ttu-id="903eb-140">Предоставьте разрешения для приложения в клиенте.</span><span class="sxs-lookup"><span data-stu-id="903eb-140">Grant permissions across your tenant for your application.</span></span> <span data-ttu-id="903eb-141">Перейдите к разделу **Параметры** > **Свойства** > **Необходимые разрешения**, а затем нажмите кнопку **Предоставить разрешения** на панели сверху.</span><span class="sxs-lookup"><span data-stu-id="903eb-141">Go to **Settings** > **Properties** > **Required Permissions**, and click the **Grant Permissions** button on the top bar.</span></span> <span data-ttu-id="903eb-142">Нажмите кнопку **Да** для подтверждения.</span><span class="sxs-lookup"><span data-stu-id="903eb-142">Click **Yes** to confirm.</span></span>

## <a name="step-2-install-adal-and-configure-the-single-page-app"></a><span data-ttu-id="903eb-143">Шаг 2. Установка библиотеки ADAL и настройка одностраничного приложения</span><span class="sxs-lookup"><span data-stu-id="903eb-143">Step 2: Install ADAL and configure the single-page app</span></span>
<span data-ttu-id="903eb-144">Теперь, когда приложение зарегистрировано в Azure AD, можно установить библиотеку adal.js и написать код для работы с удостоверением.</span><span class="sxs-lookup"><span data-stu-id="903eb-144">Now that you have an application in Azure AD, you can install adal.js and write your identity-related code.</span></span>

### <a name="configure-the-javascript-client"></a><span data-ttu-id="903eb-145">Настройка клиента JavaScript</span><span class="sxs-lookup"><span data-stu-id="903eb-145">Configure the JavaScript client</span></span>
<span data-ttu-id="903eb-146">Добавьте adal.js в проект TodoSPA с помощью консоли диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="903eb-146">Begin by adding adal.js to the TodoSPA project by using the Package Manager Console:</span></span>
  1. <span data-ttu-id="903eb-147">Скачайте файл [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) и добавьте его в каталог проекта `App/Scripts/`.</span><span class="sxs-lookup"><span data-stu-id="903eb-147">Download [adal.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal.js) and add it to the `App/Scripts/` project directory.</span></span>
  2. <span data-ttu-id="903eb-148">Скачайте файл [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) и добавьте его в каталог проекта `App/Scripts/`.</span><span class="sxs-lookup"><span data-stu-id="903eb-148">Download [adal-angular.js](https://raw.githubusercontent.com/AzureAD/azure-activedirectory-library-for-js/master/lib/adal-angular.js) and add it to the `App/Scripts/` project directory.</span></span>
  3. <span data-ttu-id="903eb-149">До закрывающего тега `</body>` in `index.html`вставьте строки загрузки сценариев:</span><span class="sxs-lookup"><span data-stu-id="903eb-149">Load each script before the end of the `</body>` in `index.html`:</span></span>

    ```js
    ...
    <script src="App/Scripts/adal.js"></script>
    <script src="App/Scripts/adal-angular.js"></script>
    ...
    ```

### <a name="configure-the-back-end-server"></a><span data-ttu-id="903eb-150">Настройка внутреннего сервера</span><span class="sxs-lookup"><span data-stu-id="903eb-150">Configure the back end server</span></span>
<span data-ttu-id="903eb-151">Чтобы API серверной части одностраничного интерфейсного приложения со списком дел мог принимать маркеры от браузера, ему требуются сведения о параметрах регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="903eb-151">For the single-page app's back-end To Do List API to accept tokens from the browser, the back end needs configuration information about the app registration.</span></span> <span data-ttu-id="903eb-152">В проекте TodoSPA откройте файл `web.config`.</span><span class="sxs-lookup"><span data-stu-id="903eb-152">In the TodoSPA project, open `web.config`.</span></span> <span data-ttu-id="903eb-153">Замените значения элементов в разделе `<appSettings>` на значения, которые вы указали на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="903eb-153">Replace the values of the elements in the `<appSettings>` section to reflect the values that you used in the Azure portal.</span></span> <span data-ttu-id="903eb-154">Ваш код будет ссылаться на эти значения при каждом использовании ADAL.</span><span class="sxs-lookup"><span data-stu-id="903eb-154">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="903eb-155">`ida:Tenant` — это имя вашего клиента Azure AD, например contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="903eb-155">`ida:Tenant` is the domain of your Azure AD tenant--for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="903eb-156">Для `ida:Audience` укажите скопированный на портале идентификатор клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="903eb-156">`ida:Audience` is the client ID of your application that you copied from the portal.</span></span>

## <a name="step-3-use-adal-to-help-secure-pages-in-the-single-page-app"></a><span data-ttu-id="903eb-157">Шаг 3. Применение ADAL для защиты страниц одностраничного приложения</span><span class="sxs-lookup"><span data-stu-id="903eb-157">Step 3: Use ADAL to help secure pages in the single-page app</span></span>
<span data-ttu-id="903eb-158">Adal.js интегрируется с маршрутом AngularJS и поставщиками HTTP, позволяя вам защищать отдельные представления в одностраничных приложениях.</span><span class="sxs-lookup"><span data-stu-id="903eb-158">Adal.js integrates with AngularJS route and HTTP providers, so you can help secure individual views in your single-page app.</span></span>

1. <span data-ttu-id="903eb-159">В файл `App/Scripts/app.js` добавьте код для привязки модуля adal.js:</span><span class="sxs-lookup"><span data-stu-id="903eb-159">In `App/Scripts/app.js`, bring in the adal.js module:</span></span>

    ```js
    angular.module('todoApp', ['ngRoute','AdalAngular'])
    .config(['$routeProvider','$httpProvider', 'adalAuthenticationServiceProvider',
     function ($routeProvider, $httpProvider, adalProvider) {
    ...
    ```
2. <span data-ttu-id="903eb-160">В этом же файле `App/Scripts/app.js` инициализируйте `adalProvider`, используя значения конфигурации для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="903eb-160">Initialize `adalProvider` by using the configuration values of your application registration, also in `App/Scripts/app.js`:</span></span>

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
3. <span data-ttu-id="903eb-161">Защитите представление `TodoList` в приложении, добавив всего одну строку кода: `requireADLogin`.</span><span class="sxs-lookup"><span data-stu-id="903eb-161">Help secure the `TodoList` view in the app by using only one line of code: `requireADLogin`.</span></span>

    ```js
    ...
    }).when("/TodoList", {
            controller: "todoListCtrl",
            templateUrl: "/App/Views/TodoList.html",
            requireADLogin: true,
    ...
    ```

## <a name="summary"></a><span data-ttu-id="903eb-162">Сводка</span><span class="sxs-lookup"><span data-stu-id="903eb-162">Summary</span></span>
<span data-ttu-id="903eb-163">Теперь у вас есть защищенное одностраничное приложение, которое может обрабатывать вход пользователей и выполнять запросы к серверному API, защищенные с помощью токена носителя.</span><span class="sxs-lookup"><span data-stu-id="903eb-163">You now have a secure single-page app that can sign in users and issue bearer-token-protected requests to its back-end API.</span></span> <span data-ttu-id="903eb-164">Когда пользователь щелкает ссылку **TodoList**, библиотека adal.js выполняет автоматическое перенаправление к Azure AD для входа, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="903eb-164">When a user clicks the **TodoList** link, adal.js will automatically redirect to Azure AD for sign-in if necessary.</span></span> <span data-ttu-id="903eb-165">Кроме того, adal.js автоматически добавляет маркер доступа ко всем запросам AJAX, которые передаются серверной части приложения.</span><span class="sxs-lookup"><span data-stu-id="903eb-165">In addition, adal.js will automatically attach an access token to any Ajax requests that are sent to the app's back end.</span></span>  

<span data-ttu-id="903eb-166">Выше описан минимально возможный процесс создания одностраничного приложения с помощью adal.js.</span><span class="sxs-lookup"><span data-stu-id="903eb-166">The preceding steps are the bare minimum necessary to build a single-page app by using adal.js.</span></span> <span data-ttu-id="903eb-167">Но для одностраничных приложений есть еще несколько полезных функций.</span><span class="sxs-lookup"><span data-stu-id="903eb-167">But a few other features are useful in single-page app:</span></span>

* <span data-ttu-id="903eb-168">Вы можете определить в контроллерах функции, которые будут вызывать библиотеку adal.js для явной обработки запросов на вход и выход.</span><span class="sxs-lookup"><span data-stu-id="903eb-168">To explicitly issue sign-in and sign-out requests, you can define functions in your controllers that invoke adal.js.</span></span>  <span data-ttu-id="903eb-169">В `App/Scripts/homeCtrl.js` добавьте:</span><span class="sxs-lookup"><span data-stu-id="903eb-169">In `App/Scripts/homeCtrl.js`:</span></span>

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
* <span data-ttu-id="903eb-170">В интерфейсе приложения можно предоставить сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="903eb-170">You might want to present user information in the app's UI.</span></span> <span data-ttu-id="903eb-171">Служба ADAL уже добавлена к контроллеру `userDataCtrl`, поэтому в связанном представлении `App/Views/UserData.html` можно получить доступ к объекту `userInfo`:</span><span class="sxs-lookup"><span data-stu-id="903eb-171">The ADAL service has already been added to the `userDataCtrl` controller, so you can access the `userInfo` object in the associated view, `App/Views/UserData.html`:</span></span>

    ```js
    <p>{{userInfo.userName}}</p>
    <p>aud:{{userInfo.profile.aud}}</p>
    <p>iss:{{userInfo.profile.iss}}</p>
    ...
    ```

* <span data-ttu-id="903eb-172">Также во многих случаях требуется знать, зарегистрирован пользователь или нет.</span><span class="sxs-lookup"><span data-stu-id="903eb-172">There are many scenarios in which you'll want to know if the user is signed in or not.</span></span> <span data-ttu-id="903eb-173">Для сбора этой информации также можно использовать объект `userInfo` .</span><span class="sxs-lookup"><span data-stu-id="903eb-173">You can also use the `userInfo` object to gather this information.</span></span>  <span data-ttu-id="903eb-174">Например, в `index.html` можно отображать кнопку **Вход** или **Выход** в зависимости от текущего состояния аутентификации:</span><span class="sxs-lookup"><span data-stu-id="903eb-174">For instance, in `index.html`, you can show either the **Login** or **Logout** button based on authentication status:</span></span>

    ```js
    <li><a class="btn btn-link" ng-show="userInfo.isAuthenticated" ng-click="logout()">Logout</a></li>
    <li><a class="btn btn-link" ng-hide=" userInfo.isAuthenticated" ng-click="login()">Login</a></li>
    ```

<span data-ttu-id="903eb-175">Интегрированное с Azure AD одностраничное приложение может выполнять аутентификацию пользователей, безопасно обращаться к серверной части по протоколу OAuth 2.0 и получать основные сведения о пользователе.</span><span class="sxs-lookup"><span data-stu-id="903eb-175">Your Azure AD-integrated single-page app can authenticate users, securely call its back end by using OAuth 2.0, and get basic information about the user.</span></span> <span data-ttu-id="903eb-176">Если же вы этого еще не сделали, пришло время добавить в клиент нескольких пользователей.</span><span class="sxs-lookup"><span data-stu-id="903eb-176">If you haven't already, now is the time to populate your tenant with some users.</span></span> <span data-ttu-id="903eb-177">Запустите одностраничное приложение со списком дел и выполните вход от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="903eb-177">Run your To Do List single-page app, and sign in with one of those users.</span></span> <span data-ttu-id="903eb-178">Добавьте задачи в список дел этого пользователя, выйдите и войдите снова.</span><span class="sxs-lookup"><span data-stu-id="903eb-178">Add tasks to the user's to-do list, sign out, and sign back in.</span></span>

<span data-ttu-id="903eb-179">Adal.js позволяет легко добавлять в приложение основные компоненты для работы с идентификаторами.</span><span class="sxs-lookup"><span data-stu-id="903eb-179">Adal.js makes it easy to incorporate common identity features into your application.</span></span> <span data-ttu-id="903eb-180">Методы этой библиотеки выполняют всю черновую работу: управляют кэшем, поддерживают протокол OAuth, выводят для пользователя диалоговое окно входа, обновляют маркеры с истекшим сроком действия и многое другое.</span><span class="sxs-lookup"><span data-stu-id="903eb-180">It takes care of all the dirty work for you: cache management, OAuth protocol support, presenting the user with a sign-in UI, refreshing expired tokens, and more.</span></span>

<span data-ttu-id="903eb-181">Готовый пример (для которого лишь осталось задать конфигурацию) можно найти в [репозитории GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="903eb-181">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/SinglePageApp-AngularJS-DotNet/archive/complete.zip).</span></span>

## <a name="next-steps"></a><span data-ttu-id="903eb-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="903eb-182">Next steps</span></span>
<span data-ttu-id="903eb-183">Теперь можно приступить к изучению других сценариев.</span><span class="sxs-lookup"><span data-stu-id="903eb-183">You can now move on to additional scenarios.</span></span> <span data-ttu-id="903eb-184">Попробуйте осуществить [вызов веб-интерфейса API CORS из одностраничного приложения](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span><span class="sxs-lookup"><span data-stu-id="903eb-184">You might want to try: [Call a CORS web API from a single-page app](https://github.com/AzureAdSamples/SinglePageApp-WebAPI-AngularJS-DotNet).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
