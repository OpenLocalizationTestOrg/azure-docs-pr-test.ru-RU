---
title: "Приступая к работе с Azure AD версии 2 для классического приложения для Windows. Тестирование | Документация Майкрософт"
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
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="e9663-103">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="e9663-103">Test your code</span></span>

<span data-ttu-id="e9663-104">Чтобы протестировать приложение, нажмите клавишу `F5` для запуска проекта в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e9663-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="e9663-105">Откроется главное окно.</span><span class="sxs-lookup"><span data-stu-id="e9663-105">Your Main Window should appear:</span></span>

![Пример снимка экрана](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="e9663-107">Когда вы будете готовы к тестированию, щелкните *Call Microsoft Graph API* (Вызвать API Microsoft Graph) и используйте Microsoft Azure Active Directory (учетная запись организации) или учетную запись Майкрософт (live.com, outlook.com) для входа.</span><span class="sxs-lookup"><span data-stu-id="e9663-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="e9663-108">Если вход выполняется впервые, появится окно, предлагающее пользователю войти в систему:</span><span class="sxs-lookup"><span data-stu-id="e9663-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![Вход](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="e9663-110">Согласие на предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="e9663-110">Consent</span></span>
<span data-ttu-id="e9663-111">При первом входе в приложение появится экран согласия, как показано ниже, где необходимо явно дать согласие:</span><span class="sxs-lookup"><span data-stu-id="e9663-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Экран согласия](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="e9663-113">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="e9663-113">Expected results</span></span>
<span data-ttu-id="e9663-114">На экране результатов вызова API должны отобразиться сведения о профиле пользователя, возвращенные вызовом API Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="e9663-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="e9663-115">Вы также должны увидеть основные сведения о маркере, полученные с помощью `AcquireTokenAsync` или `AcquireTokenSilentAsync`, в соответствующем окне:</span><span class="sxs-lookup"><span data-stu-id="e9663-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="e9663-116">Свойство</span><span class="sxs-lookup"><span data-stu-id="e9663-116">Property</span></span>  |<span data-ttu-id="e9663-117">Формат</span><span class="sxs-lookup"><span data-stu-id="e9663-117">Format</span></span>  |<span data-ttu-id="e9663-118">Описание</span><span class="sxs-lookup"><span data-stu-id="e9663-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="e9663-119">Имя</span><span class="sxs-lookup"><span data-stu-id="e9663-119">Name</span></span> | <span data-ttu-id="e9663-120">{Полное имя пользователя}</span><span class="sxs-lookup"><span data-stu-id="e9663-120">{User Full name}</span></span> |<span data-ttu-id="e9663-121">Имя и фамилия пользователя</span><span class="sxs-lookup"><span data-stu-id="e9663-121">The user’s first and last name</span></span>|
|<span data-ttu-id="e9663-122">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="e9663-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="e9663-123">Имя пользователя, используемое для его идентификации</span><span class="sxs-lookup"><span data-stu-id="e9663-123">The username used to identify the user</span></span>|
|<span data-ttu-id="e9663-124">Истечение срока действия маркера</span><span class="sxs-lookup"><span data-stu-id="e9663-124">Token Expires</span></span> |<span data-ttu-id="e9663-125">{дата и время}</span><span class="sxs-lookup"><span data-stu-id="e9663-125">{DateTime}</span></span>         |<span data-ttu-id="e9663-126">Время окончания срока действия маркера.</span><span class="sxs-lookup"><span data-stu-id="e9663-126">The time on which the token expires.</span></span> <span data-ttu-id="e9663-127">MSAL продлит срок действия, обновив маркер при необходимости</span><span class="sxs-lookup"><span data-stu-id="e9663-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="e9663-128">Маркер доступа</span><span class="sxs-lookup"><span data-stu-id="e9663-128">Access token</span></span> |<span data-ttu-id="e9663-129">{Строка}</span><span class="sxs-lookup"><span data-stu-id="e9663-129">{String}</span></span>         |<span data-ttu-id="e9663-130">Строка маркера, которая будет отправлена HTTP-запросам, требующим заголовка авторизации</span><span class="sxs-lookup"><span data-stu-id="e9663-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="e9663-131">Дополнительные сведения об областях и делегированных разрешениях</span><span class="sxs-lookup"><span data-stu-id="e9663-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="e9663-132">API Graph требуется область `user.read` для чтения профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9663-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="e9663-133">По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="e9663-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="e9663-134">Некоторые другие API Graph, а также пользовательские API для вашего внутреннего сервера требуют дополнительные области.</span><span class="sxs-lookup"><span data-stu-id="e9663-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="e9663-135">Например, для Graph требуется `Calendars.Read`, чтобы отобразить список календарей пользователя.</span><span class="sxs-lookup"><span data-stu-id="e9663-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="e9663-136">Чтобы получить доступ к календарю пользователя в контексте приложения, необходимо добавить сведения о регистрации делегированного приложения `Calendars.Read`, а затем добавить `Calendars.Read` в вызов `AcquireTokenAsync`.</span><span class="sxs-lookup"><span data-stu-id="e9663-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="e9663-137">При увеличении количества областей от пользователя могут потребоваться дополнительные согласия.</span><span class="sxs-lookup"><span data-stu-id="e9663-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



