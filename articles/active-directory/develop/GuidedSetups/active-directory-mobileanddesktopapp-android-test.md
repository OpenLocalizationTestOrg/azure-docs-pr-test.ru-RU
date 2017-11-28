---
title: "aaaAzure AD v2 Android Приступая к работе - тестирования | Документы Microsoft"
description: "Получение маркера доступа для приложения Android и вызов API Microsoft Graph или API, которые требуют маркер доступа, из конечной точки Azure Active Directory версии 2."
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="81cda-103">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="81cda-103">Test your code</span></span>

1. <span data-ttu-id="81cda-104">Развертывание вашего кода tooyour устройстве или эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="81cda-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="81cda-105">Когда вы будете готовы tootest, используйте Microsoft Azure Active Directory (учетная запись организации) или toosign учетной записи учетную запись Майкрософт (live.com, outlook.com) в.</span><span class="sxs-lookup"><span data-stu-id="81cda-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="81cda-106">![Пример снимка экрана](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="81cda-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="81cda-107">
![Вход](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="81cda-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="81cda-108">Согласие на предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="81cda-108">Consent</span></span>
<span data-ttu-id="81cda-109">Hello при первом входе в приложение tooyour они предоставят согласия экрана примерно toohello ниже, где они должны принимать tooexplicitly:</span><span class="sxs-lookup"><span data-stu-id="81cda-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![Согласие на предоставление разрешений](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="81cda-111">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="81cda-111">Expected results</span></span>
<span data-ttu-id="81cda-112">Вы увидите результаты hello tooMicrosoft вызова Graph API «me» конечной точкой, используется профиль пользователя hello tootooobtain - https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="81cda-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="81cda-113">Список распространенных конечных точек Microsoft Graph см. в [этой статье](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="81cda-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="81cda-114">Дополнительные сведения об областях и делегированных разрешениях</span><span class="sxs-lookup"><span data-stu-id="81cda-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="81cda-115">Hello Microsoft Graph API требует hello `user.read` области профиля пользователя tooread hello.</span><span class="sxs-lookup"><span data-stu-id="81cda-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="81cda-116">По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="81cda-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="81cda-117">Для некоторых других API Microsoft Graph, а также пользовательских API для вашего внутреннего сервера могут потребоваться дополнительные области.</span><span class="sxs-lookup"><span data-stu-id="81cda-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="81cda-118">Например, для Microsoft Graph hello области `Calendars.Read` является обязательным toolist hello пользовательских календарях.</span><span class="sxs-lookup"><span data-stu-id="81cda-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="81cda-119">В порядке tooaccess hello календаря пользователя в контексте приложения, вы должны tooadd hello `Calendars.Read` делегировать разрешения toohello приложения регистрационную информацию, а затем добавьте hello `Calendars.Read` toohello область `acquireTokenSilentAsync` вызова.</span><span class="sxs-lookup"><span data-stu-id="81cda-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="81cda-120">Hello пользователей могут запрашиваться дополнительных согласие по мере увеличения количества hello областей.</span><span class="sxs-lookup"><span data-stu-id="81cda-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
