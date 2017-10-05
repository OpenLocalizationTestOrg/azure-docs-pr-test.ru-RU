---
title: "Приступая к работе с Azure AD версии 2 для iOS. Тестирование | Документация Майкрософт"
description: "В этой статье описано, как приложения iOS (Swift) могут вызывать API, которому необходимы маркеры доступа, с помощью конечной точки Azure Active Directory версии 2."
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 4a88096d2b0a23708acdbc1798eac528599b4f71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
## <a name="test-querying-the-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="0bd3e-103">Отправка тестового запроса к API Microsoft Graph из приложения iOS</span><span class="sxs-lookup"><span data-stu-id="0bd3e-103">Test querying the Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="0bd3e-104">Нажмите `Command` + `R` для запуска кода в симуляторе.</span><span class="sxs-lookup"><span data-stu-id="0bd3e-104">Press `Command` + `R` to run the code in the simulator.</span></span>

![Пример снимка экрана](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="0bd3e-106">Когда вы будете готовы к проверке, нажмите кнопку *Вызвать API Microsoft Graph*, и вам будет предложено ввести имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="0bd3e-106">When you're ready to test, tap *‘Call Microsoft Graph API’* and you will be prompted to type your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="0bd3e-107">Согласие на предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="0bd3e-107">Consent</span></span>
<span data-ttu-id="0bd3e-108">При первом входе в приложение появится экран согласия, как показано ниже, где необходимо явно дать согласие:</span><span class="sxs-lookup"><span data-stu-id="0bd3e-108">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Экран согласия](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="0bd3e-110">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="0bd3e-110">Expected results</span></span>
<span data-ttu-id="0bd3e-111">Сведения о профиле пользователя, полученные в результате вызова API Microsoft Graph, отображаются в разделе *Ведение журнала*.</span><span class="sxs-lookup"><span data-stu-id="0bd3e-111">You should see user profile information returned by the Microsoft Graph API call in the *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="0bd3e-112">Дополнительные сведения об областях и делегированных разрешениях</span><span class="sxs-lookup"><span data-stu-id="0bd3e-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="0bd3e-113">Для чтения профиля пользователя API Microsoft Graph требуется область `user.read`.</span><span class="sxs-lookup"><span data-stu-id="0bd3e-113">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="0bd3e-114">По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="0bd3e-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="0bd3e-115">Для некоторых других API Microsoft Graph, а также пользовательских API для вашего внутреннего сервера могут потребоваться дополнительные области.</span><span class="sxs-lookup"><span data-stu-id="0bd3e-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="0bd3e-116">Например, для Microsoft Graph требуется область `Calendars.Read`, чтобы отобразить список календарей пользователя.</span><span class="sxs-lookup"><span data-stu-id="0bd3e-116">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="0bd3e-117">Чтобы получить доступ к календарю пользователя в контексте приложения, в сведения о регистрации приложения необходимо добавить делегированное разрешение `Calendars.Read`, а затем добавить область `Calendars.Read` в вызов `acquireTokenSilent`.</span><span class="sxs-lookup"><span data-stu-id="0bd3e-117">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilent` call.</span></span> <span data-ttu-id="0bd3e-118">При увеличении количества областей от пользователя может потребоваться дополнительное согласие.</span><span class="sxs-lookup"><span data-stu-id="0bd3e-118">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



