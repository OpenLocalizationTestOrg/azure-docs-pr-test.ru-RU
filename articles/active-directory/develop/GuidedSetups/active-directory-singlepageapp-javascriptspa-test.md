---
title: "Интерактивная настройка Azure AD версии 2 для JS SPA. Тестирование | Документация Майкрософт"
description: "В этой статье описано, как приложения JavaScript SPA могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: c888760ab311e8ac08b1e625bb837f91047db645
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
## <a name="test-your-code"></a><span data-ttu-id="59a1b-103">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="59a1b-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="59a1b-104">Тестирование с Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59a1b-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="59a1b-105">При использовании Visual Studio нажмите клавишу `F5` для запуска проекта. Откроется браузер и переместит вас на страницу по адресу *http://localhost:{port}*. На странице отобразится кнопка *Call Microsoft Graph API* (Вызвать Microsoft Graph API).</span><span class="sxs-lookup"><span data-stu-id="59a1b-105">If you are using Visual Studio, press `F5` to run your project: the browser opens and directs you to *http://localhost:{port}* where you see the *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="59a1b-106">Тестирование с помощью Python или другого веб-сервера</span><span class="sxs-lookup"><span data-stu-id="59a1b-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="59a1b-107">Если вы не используете Visual Studio, убедитесь, что веб-сервер запущен и настроен для ожидания передачи данных с TCP-порта в папке с файлом *index.html*.</span><span class="sxs-lookup"><span data-stu-id="59a1b-107">If you are not using Visual Studio, make sure your web server is started and it is configured to listen to a TCP port based on the folder containing your *index.html* file.</span></span> <span data-ttu-id="59a1b-108">Для Python можно запустить ожидание передачи данных на порте, выполнив команду в командной строке или в окне терминала из папки приложения:</span><span class="sxs-lookup"><span data-stu-id="59a1b-108">For Python, you can start listening to the port by running the in the command prompt/ terminal, from the app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="59a1b-109">Затем откройте браузер и введите *http://localhost:8080* или *http://localhost:{port}*, где *port* соответствует порту, с которого веб-сервер ожидает передачи данных.</span><span class="sxs-lookup"><span data-stu-id="59a1b-109">Then, open the browser and type *http://localhost:8080* or *http://localhost:{port}* - where the *port* corresponds to the port that your web server is listening to.</span></span> <span data-ttu-id="59a1b-110">Появится содержимое страницы index.html с кнопкой *Call Microsoft Graph API* (Вызвать Microsoft Graph API).</span><span class="sxs-lookup"><span data-stu-id="59a1b-110">You should see the contents of your index.html page with the *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="59a1b-111">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="59a1b-111">Test your application</span></span>

<span data-ttu-id="59a1b-112">После загрузки *index.html* в браузере нажмите кнопку *Call Microsoft Graph API* (Вызвать Microsoft Graph API).</span><span class="sxs-lookup"><span data-stu-id="59a1b-112">After the browser loads your *index.html*, click the *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="59a1b-113">Если вы делаете это впервые, браузер перенаправит вас в конечную точку Microsoft Azure Active Directory v2, где вам будет предложено войти.</span><span class="sxs-lookup"><span data-stu-id="59a1b-113">If this is the first time, the browser redirects you to the Microsoft Azure Active Directory v2 endpoint, where you are  prompted to sign in.</span></span>
 
![Пример снимка экрана](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="59a1b-115">Согласие на предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="59a1b-115">Consent</span></span>
<span data-ttu-id="59a1b-116">При первом входе в приложение появится экран согласия, как показано ниже, где необходимо дать согласие:</span><span class="sxs-lookup"><span data-stu-id="59a1b-116">The very first time you sign in to your application, you are presented with a consent screen similar to the following, where you need to accept:</span></span>

 ![Экран согласия](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="59a1b-118">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="59a1b-118">Expected results</span></span>
<span data-ttu-id="59a1b-119">Сведения о профиле пользователя должны отобразиться при ответе на вызов API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="59a1b-119">You should see user profile information returned by the Microsoft Graph API call response.</span></span>
 
 ![Результаты](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="59a1b-121">Кроме того, должны отобразиться основные сведения о маркере, полученные с помощью полей *Маркер доступа* и *ID Token Claims* (Утверждения маркера идентификатора).</span><span class="sxs-lookup"><span data-stu-id="59a1b-121">You also see basic information about the token acquired in the *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="59a1b-122">Дополнительные сведения об областях и делегированных разрешениях</span><span class="sxs-lookup"><span data-stu-id="59a1b-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="59a1b-123">Для чтения профиля пользователя API Microsoft Graph требуется область `user.read`.</span><span class="sxs-lookup"><span data-stu-id="59a1b-123">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="59a1b-124">По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="59a1b-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="59a1b-125">Для некоторых других API Microsoft Graph, а также пользовательских API для вашего внутреннего сервера могут потребоваться дополнительные области.</span><span class="sxs-lookup"><span data-stu-id="59a1b-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="59a1b-126">Например, для Microsoft Graph требуется область `Calendars.Read`, чтобы отобразить список календарей пользователя.</span><span class="sxs-lookup"><span data-stu-id="59a1b-126">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="59a1b-127">Чтобы получить доступ к календарю пользователя в контексте приложения, в сведения о регистрации приложения необходимо добавить делегированное разрешение `Calendars.Read`, а затем добавить область `Calendars.Read` в вызов `acquireTokenSilent`.</span><span class="sxs-lookup"><span data-stu-id="59a1b-127">In order to access the user’s calendar in the context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="59a1b-128">При увеличении количества областей от пользователя может потребоваться дополнительное согласие.</span><span class="sxs-lookup"><span data-stu-id="59a1b-128">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<span data-ttu-id="59a1b-129">Если для API серверной части не требуется область (не рекомендуется), то вы можете использовать `clientId` в качестве области в вызове `acquireTokenSilent` и (или) вызовах `acquireTokenRedirect`.</span><span class="sxs-lookup"><span data-stu-id="59a1b-129">If a backend API does not require a scope (not recommended), you can use the `clientId` as the scope in the `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
