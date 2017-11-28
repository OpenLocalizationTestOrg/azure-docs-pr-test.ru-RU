---
title: "aaaAzure AD v2 JS SPA Интерактивная установка - тестирования | Документы Microsoft"
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
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="a8c75-103">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="a8c75-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="a8c75-104">Тестирование с Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a8c75-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="a8c75-105">Если вы используете Visual Studio, нажмите клавишу `F5` toorun проекта: hello браузер откроется, а также указаны слишком*http://localhost: {port}* показывающий hello *вызывать Graph API Microsoft* кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8c75-105">If you are using Visual Studio, press `F5` toorun your project: hello browser opens and directs you too*http://localhost:{port}* where you see hello *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="a8c75-106">Тестирование с помощью Python или другого веб-сервера</span><span class="sxs-lookup"><span data-stu-id="a8c75-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="a8c75-107">Если вы не используете Visual Studio, убедитесь, что веб-сервера запущена, и он настроен на папку, содержащую hello основе toolisten tooa TCP-порт вашей *index.html* файла.</span><span class="sxs-lookup"><span data-stu-id="a8c75-107">If you are not using Visual Studio, make sure your web server is started and it is configured toolisten tooa TCP port based on hello folder containing your *index.html* file.</span></span> <span data-ttu-id="a8c75-108">Для Python, можно начать прослушивание порта toohello, выполнив hello в hello команда prompt / терминалов, из папки приложения hello:</span><span class="sxs-lookup"><span data-stu-id="a8c75-108">For Python, you can start listening toohello port by running hello in hello command prompt/ terminal, from hello app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="a8c75-109">Откройте браузер hello и введите *http://localhost: 8080* или *http://localhost: {port}* — там, где hello *порт* соответствует toohello порт, на веб-сервере прослушивание.</span><span class="sxs-lookup"><span data-stu-id="a8c75-109">Then, open hello browser and type *http://localhost:8080* or *http://localhost:{port}* - where hello *port* corresponds toohello port that your web server is listening to.</span></span> <span data-ttu-id="a8c75-110">Вы увидите содержимое hello index.html страницы с hello *вызова API Graph Microsoft* кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8c75-110">You should see hello contents of your index.html page with hello *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="a8c75-111">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="a8c75-111">Test your application</span></span>

<span data-ttu-id="a8c75-112">После hello браузер загружает вашей *index.html*, щелкните hello *вызова API Graph Microsoft* кнопки.</span><span class="sxs-lookup"><span data-stu-id="a8c75-112">After hello browser loads your *index.html*, click hello *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="a8c75-113">Если это первый раз hello перенаправления браузера hello вы toohello v2 Microsoft Azure Active Directory конечной точки, где вы находитесь запрос toosign в.</span><span class="sxs-lookup"><span data-stu-id="a8c75-113">If this is hello first time, hello browser redirects you toohello Microsoft Azure Active Directory v2 endpoint, where you are  prompted toosign in.</span></span>
 
![Пример снимка экрана](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="a8c75-115">Согласие на предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="a8c75-115">Consent</span></span>
<span data-ttu-id="a8c75-116">Hello первый раз при входе в приложение tooyour решаемой согласия экрана примерно toohello следующую команду, где должны tooaccept:</span><span class="sxs-lookup"><span data-stu-id="a8c75-116">hello very first time you sign in tooyour application, you are presented with a consent screen similar toohello following, where you need tooaccept:</span></span>

 ![Экран согласия](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="a8c75-118">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="a8c75-118">Expected results</span></span>
<span data-ttu-id="a8c75-119">Должны появиться сведения о профиле пользователя, возвращенный hello в ответ на вызов Microsoft Graph API.</span><span class="sxs-lookup"><span data-stu-id="a8c75-119">You should see user profile information returned by hello Microsoft Graph API call response.</span></span>
 
 ![Результаты](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="a8c75-121">Также отображаются основные сведения о hello токена, полученного в hello *токена доступа* и *идентификатор токена утверждений* поля.</span><span class="sxs-lookup"><span data-stu-id="a8c75-121">You also see basic information about hello token acquired in hello *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="a8c75-122">Дополнительные сведения об областях и делегированных разрешениях</span><span class="sxs-lookup"><span data-stu-id="a8c75-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="a8c75-123">Hello Microsoft Graph API требует hello `user.read` области профиля пользователя tooread hello.</span><span class="sxs-lookup"><span data-stu-id="a8c75-123">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="a8c75-124">По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="a8c75-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="a8c75-125">Для некоторых других API Microsoft Graph, а также пользовательских API для вашего внутреннего сервера могут потребоваться дополнительные области.</span><span class="sxs-lookup"><span data-stu-id="a8c75-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="a8c75-126">Например, для Microsoft Graph hello области `Calendars.Read` является обязательным toolist hello пользовательских календарях.</span><span class="sxs-lookup"><span data-stu-id="a8c75-126">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="a8c75-127">В порядке tooaccess hello календаря пользователя в контексте приложения hello, вы должны tooadd hello `Calendars.Read` делегировать разрешения toohello приложения регистрационную информацию, а затем добавьте hello `Calendars.Read` toohello область `acquireTokenSilent` вызова.</span><span class="sxs-lookup"><span data-stu-id="a8c75-127">In order tooaccess hello user’s calendar in hello context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="a8c75-128">Hello пользователей могут запрашиваться дополнительных согласие по мере увеличения количества hello областей.</span><span class="sxs-lookup"><span data-stu-id="a8c75-128">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<span data-ttu-id="a8c75-129">Если API внутреннего сервера не требуется область (не рекомендуется), можно использовать hello `clientId` как область hello в hello `acquireTokenSilent` и/или `acquireTokenRedirect` вызовов.</span><span class="sxs-lookup"><span data-stu-id="a8c75-129">If a backend API does not require a scope (not recommended), you can use hello `clientId` as hello scope in hello `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
