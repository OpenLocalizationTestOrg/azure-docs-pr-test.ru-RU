---
title: "iOS v2 aaaAzure AD Приступая к работе - тестирования | Документы Microsoft"
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
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="c777d-103">Тестирование запросов hello Microsoft Graph API из приложения iOS</span><span class="sxs-lookup"><span data-stu-id="c777d-103">Test querying hello Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="c777d-104">Нажмите клавишу `Command`  +  `R` toorun кода hello в симуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="c777d-104">Press `Command` + `R` toorun hello code in hello simulator.</span></span>

![Пример снимка экрана](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="c777d-106">Когда вы будете готовы tootest, коснитесь *«Вызвать API Microsoft Graph»* и будет tootype запрос имени пользователя и пароля.</span><span class="sxs-lookup"><span data-stu-id="c777d-106">When you're ready tootest, tap *‘Call Microsoft Graph API’* and you will be prompted tootype your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="c777d-107">Согласие на предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="c777d-107">Consent</span></span>
<span data-ttu-id="c777d-108">Hello при первом входе в приложение tooyour откроется с согласия экрана примерно toohello ниже, где необходимо принять tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="c777d-108">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Экран согласия](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="c777d-110">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="c777d-110">Expected results</span></span>
<span data-ttu-id="c777d-111">Вы увидите сведения о профиле пользователя, возвращаемый в результате вызова Microsoft Graph API hello в hello *входа* раздела.</span><span class="sxs-lookup"><span data-stu-id="c777d-111">You should see user profile information returned by hello Microsoft Graph API call in hello *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="c777d-112">Дополнительные сведения об областях и делегированных разрешениях</span><span class="sxs-lookup"><span data-stu-id="c777d-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="c777d-113">Hello Microsoft Graph API требует hello `user.read` области профиля пользователя tooread hello.</span><span class="sxs-lookup"><span data-stu-id="c777d-113">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="c777d-114">По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="c777d-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="c777d-115">Для некоторых других API Microsoft Graph, а также пользовательских API для вашего внутреннего сервера могут потребоваться дополнительные области.</span><span class="sxs-lookup"><span data-stu-id="c777d-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="c777d-116">Например, для Microsoft Graph hello области `Calendars.Read` является обязательным toolist hello пользовательских календарях.</span><span class="sxs-lookup"><span data-stu-id="c777d-116">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="c777d-117">В порядке tooaccess hello календаря пользователя в контексте приложения, вы должны tooadd hello `Calendars.Read` делегировать разрешения toohello приложения регистрационную информацию, а затем добавьте hello `Calendars.Read` toohello область `acquireTokenSilent` вызова.</span><span class="sxs-lookup"><span data-stu-id="c777d-117">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="c777d-118">Hello пользователей могут запрашиваться дополнительных согласие по мере увеличения количества hello областей.</span><span class="sxs-lookup"><span data-stu-id="c777d-118">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



