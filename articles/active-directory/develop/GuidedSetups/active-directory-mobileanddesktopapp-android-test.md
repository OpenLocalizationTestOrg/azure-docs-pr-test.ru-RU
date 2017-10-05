---
title: "Приступая к работе с Azure AD версии 2 для Android. Тестирование | Документация Майкрософт"
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
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="97f69-103">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="97f69-103">Test your code</span></span>

1. <span data-ttu-id="97f69-104">Разверните код на своем устройстве или эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="97f69-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="97f69-105">Когда вы будете готовы к тестированию, используйте Microsoft Azure Active Directory (учетная запись организации) или учетную запись Майкрософт (live.com, outlook.com) для входа.</span><span class="sxs-lookup"><span data-stu-id="97f69-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="97f69-106">![Пример снимка экрана](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="97f69-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="97f69-107">
![Вход](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="97f69-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="97f69-108">Согласие на предоставление разрешений</span><span class="sxs-lookup"><span data-stu-id="97f69-108">Consent</span></span>
<span data-ttu-id="97f69-109">При первом входе пользователя в приложение появится экран согласия, как показано ниже, где необходимо явно дать согласие:</span><span class="sxs-lookup"><span data-stu-id="97f69-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![Согласие на предоставление разрешений](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="97f69-111">Ожидаемые результаты</span><span class="sxs-lookup"><span data-stu-id="97f69-111">Expected results</span></span>
<span data-ttu-id="97f69-112">Вы увидите результаты вызова конечной точки "me" API Microsoft Graph, используемой для получения профиля пользователя — https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="97f69-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="97f69-113">Список распространенных конечных точек Microsoft Graph см. в [этой статье](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="97f69-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="97f69-114">Дополнительные сведения об областях и делегированных разрешениях</span><span class="sxs-lookup"><span data-stu-id="97f69-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="97f69-115">Для чтения профиля пользователя API Microsoft Graph требуется область `user.read`.</span><span class="sxs-lookup"><span data-stu-id="97f69-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="97f69-116">По умолчанию эта область автоматически добавляется в каждое приложение, регистрируемое на портале регистрации.</span><span class="sxs-lookup"><span data-stu-id="97f69-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="97f69-117">Для некоторых других API Microsoft Graph, а также пользовательских API для вашего внутреннего сервера могут потребоваться дополнительные области.</span><span class="sxs-lookup"><span data-stu-id="97f69-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="97f69-118">Например, для Microsoft Graph требуется область `Calendars.Read`, чтобы отобразить список календарей пользователя.</span><span class="sxs-lookup"><span data-stu-id="97f69-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="97f69-119">Чтобы получить доступ к календарю пользователя в контексте приложения, в сведения о регистрации приложения необходимо добавить делегированное разрешение `Calendars.Read`, а затем добавить область `Calendars.Read` в вызов `acquireTokenSilentAsync`.</span><span class="sxs-lookup"><span data-stu-id="97f69-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="97f69-120">При увеличении количества областей от пользователя может потребоваться дополнительное согласие.</span><span class="sxs-lookup"><span data-stu-id="97f69-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
