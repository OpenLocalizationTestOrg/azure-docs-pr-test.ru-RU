---
title: "aaaAzure AD v2 Windows Desktop Приступая к работе - тестирования | Документы Microsoft"
description: "Здесь описывается, как классические приложения для Windows .NET (XAML) могут вызвать API, требующий маркеры доступа от конечной точки Azure Active Directory версии 2."
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="8e93e-103">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="8e93e-103">Test your code</span></span>

<span data-ttu-id="8e93e-104">Чтобы tootest приложение, нажмите клавишу `F5` toorun свой проект в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8e93e-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="8e93e-105">Откроется главное окно.</span><span class="sxs-lookup"><span data-stu-id="8e93e-105">Your Main Window should appear:</span></span>

![Пример снимка экрана](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="8e93e-107">Когда будете готовы tootest щелкните *вызывать Graph API Microsoft* и использовать Microsoft Azure Active Directory (учетная запись организации) либо toosign учетную запись учетной записью Майкрософт (live.com, outlook.com) в.</span><span class="sxs-lookup"><span data-stu-id="8e93e-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="8e93e-108">Он впервые hello, появится окно с запросом пользователя toosign в:</span><span class="sxs-lookup"><span data-stu-id="8e93e-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![Вход](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="8e93e-110">Согласие на предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="8e93e-110">Consent</span></span>
<span data-ttu-id="8e93e-111">Hello при первом входе в приложение tooyour откроется с согласия экрана примерно toohello ниже, где необходимо принять tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="8e93e-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Экран согласия](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="8e93e-113">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="8e93e-113">Expected results</span></span>
<span data-ttu-id="8e93e-114">Должны появиться сведения о профиле пользователя, возвращенный вызовом Microsoft Graph API hello на экране приветствия результатов вызова API.</span><span class="sxs-lookup"><span data-stu-id="8e93e-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="8e93e-115">Вы также увидите основные сведения о hello токена, полученного через `AcquireTokenAsync` или `AcquireTokenSilentAsync` hello маркера информационной панели:</span><span class="sxs-lookup"><span data-stu-id="8e93e-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="8e93e-116">Свойство</span><span class="sxs-lookup"><span data-stu-id="8e93e-116">Property</span></span>  |<span data-ttu-id="8e93e-117">Формат</span><span class="sxs-lookup"><span data-stu-id="8e93e-117">Format</span></span>  |<span data-ttu-id="8e93e-118">Описание</span><span class="sxs-lookup"><span data-stu-id="8e93e-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="8e93e-119">Имя</span><span class="sxs-lookup"><span data-stu-id="8e93e-119">Name</span></span> | <span data-ttu-id="8e93e-120">{Полное имя пользователя}</span><span class="sxs-lookup"><span data-stu-id="8e93e-120">{User Full name}</span></span> |<span data-ttu-id="8e93e-121">пользователь Hello и фамилию имя</span><span class="sxs-lookup"><span data-stu-id="8e93e-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="8e93e-122">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="8e93e-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="8e93e-123">Hello имя пользователя, используемое tooidentify hello пользователя</span><span class="sxs-lookup"><span data-stu-id="8e93e-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="8e93e-124">Истечение срока действия маркера</span><span class="sxs-lookup"><span data-stu-id="8e93e-124">Token Expires</span></span> |<span data-ttu-id="8e93e-125">{дата и время}</span><span class="sxs-lookup"><span data-stu-id="8e93e-125">{DateTime}</span></span>         |<span data-ttu-id="8e93e-126">время Hello, на какие hello истечения срока действия маркера.</span><span class="sxs-lookup"><span data-stu-id="8e93e-126">hello time on which hello token expires.</span></span> <span data-ttu-id="8e93e-127">MSAL продлить срок действия hello можно, обновив hello токен при необходимости</span><span class="sxs-lookup"><span data-stu-id="8e93e-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="8e93e-128">Маркер доступа</span><span class="sxs-lookup"><span data-stu-id="8e93e-128">Access token</span></span> |<span data-ttu-id="8e93e-129">{Строка}</span><span class="sxs-lookup"><span data-stu-id="8e93e-129">{String}</span></span>         |<span data-ttu-id="8e93e-130">Строка токена Hello отправлено, будут отправлены tooHTTP запросы, требующие заголовок авторизации</span><span class="sxs-lookup"><span data-stu-id="8e93e-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="8e93e-131">Дополнительные сведения об областях и делегированных разрешениях</span><span class="sxs-lookup"><span data-stu-id="8e93e-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="8e93e-132">Graph API требуется hello `user.read` область tooread профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="8e93e-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="8e93e-133">По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="8e93e-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="8e93e-134">Некоторые другие API Graph, а также пользовательские API для вашего внутреннего сервера требуют дополнительные области.</span><span class="sxs-lookup"><span data-stu-id="8e93e-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="8e93e-135">Например, граф `Calendars.Read` является обязательным toolist пользовательских календарях.</span><span class="sxs-lookup"><span data-stu-id="8e93e-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="8e93e-136">В порядке tooaccess Здравствуйте календаря пользователя в контексте приложения, необходимо tooadd `Calendars.Read` делегировать сведения о регистрации приложения, а затем добавьте `Calendars.Read` toohello `AcquireTokenAsync` вызова.</span><span class="sxs-lookup"><span data-stu-id="8e93e-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="8e93e-137">Пользователя запрашивается согласие дополнительных, при увеличении числа hello областей.</span><span class="sxs-lookup"><span data-stu-id="8e93e-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



