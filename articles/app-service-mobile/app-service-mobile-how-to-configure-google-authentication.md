---
title: "aaaHow tooconfigure Google и проверки подлинности для приложения службы приложений"
description: "Узнайте, как проверка подлинности Google tooconfigure для приложения службы приложений."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a><span data-ttu-id="ca6c7-103">Как tooconfigure вход Google toouse приложения служб приложений</span><span class="sxs-lookup"><span data-stu-id="ca6c7-103">How tooconfigure your App Service application toouse Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="ca6c7-104">В этом разделе показано, как служба приложений Azure tooconfigure toouse Google в качестве поставщика проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-104">This topic shows you how tooconfigure Azure App Service toouse Google as an authentication provider.</span></span>

<span data-ttu-id="ca6c7-105">toocomplete hello процедуры в этом разделе, необходимо иметь учетную запись Google, имеющую проверенных адрес.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-105">toocomplete hello procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="ca6c7-106">toocreate новой учетной записи Google go слишком[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="ca6c7-106">toocreate a new Google account, go too[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="ca6c7-107"><a name="register"> </a>Регистрация приложения с помощью Google</span><span class="sxs-lookup"><span data-stu-id="ca6c7-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="ca6c7-108">Войдите на toohello [портал Azure]и перейдите tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="ca6c7-109">Копировать вашей **URL-адрес**, который использовать более поздней версии tooconfigure приложение Google.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-109">Copy your **URL**, which you use later tooconfigure your Google app.</span></span>
2. <span data-ttu-id="ca6c7-110">Перейдите toohello [Google API-интерфейсы](http://go.microsoft.com/fwlink/p/?LinkId=268303) веб-сайта, выполните вход с помощью учетных данных учетной записи Google, нажмите кнопку **Создание проекта**, предоставляют **имя проекта**, нажмите кнопку  **Создание**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-110">Navigate toohello [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="ca6c7-111">В разделе **Social APIs** (Интерфейсы API для соцсетей) щелкните **Google + API**, а затем — **Включить**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="ca6c7-112">В области навигации слева hello **учетные данные** > **экран согласия OAuth**, а затем выберите ваш **адрес электронной почты**, введите **название продукта**и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-112">In hello left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="ca6c7-113">В hello **учетные данные** щелкните **создать учетные данные** > **идентификатор клиента OAuth**, а затем выберите **веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-113">In hello **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="ca6c7-114">Вставить hello службы приложений **URL-адрес** вы ранее копируется **Authorized JavaScript Origins**, вставьте вашей перенаправления URI в **авторизации URI перенаправления**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-114">Paste hello App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="ca6c7-115">Здравствуйте перенаправления URI является hello URL-адрес приложения дополненная путь hello */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-115">hello redirect URI is hello URL of your application appended with hello path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="ca6c7-116">Например, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="ca6c7-117">Убедитесь, что вы используете hello схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-117">Make sure that you are using hello HTTPS scheme.</span></span> <span data-ttu-id="ca6c7-118">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-118">Then click **Create**.</span></span>
7. <span data-ttu-id="ca6c7-119">На следующем экране приветствия запишите значения hello клиента hello идентификатор и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-119">On hello next screen, make a note of hello values of hello client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ca6c7-120">Hello секрет клиента — важный элемент обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-120">hello client secret is an important security credential.</span></span> <span data-ttu-id="ca6c7-121">Не сообщайте этот секрет никому и не раскрывайте его в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="ca6c7-122"><a name="secrets"></a>Google, добавить сведения tooyour приложения</span><span class="sxs-lookup"><span data-stu-id="ca6c7-122"><a name="secrets"> </a>Add Google information tooyour application</span></span>
1. <span data-ttu-id="ca6c7-123">Вернитесь в hello [портал Azure], перейдите tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-123">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="ca6c7-124">Щелкните **Параметры**, а затем — **Проверка подлинности или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="ca6c7-125">Если hello проверки подлинности и авторизации не включена, включать hello слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-125">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="ca6c7-126">Щелкните **Google**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-126">Click **Google**.</span></span> <span data-ttu-id="ca6c7-127">Вставьте в значениях идентификатор приложения и секрет приложения hello, что был получен и при необходимости включить любые области, которые требуются приложению.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-127">Paste in hello App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="ca6c7-128">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="ca6c7-129">По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-129">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="ca6c7-130">Авторизация пользователей должна быть включена в код приложения.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="ca6c7-131">(Необязательно) toorestrict доступа tooyour сайта tooonly пользователь проверку подлинности Google, установить **tootake действия, если запрос не прошел проверку подлинности** слишком**Google**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-131">(Optional) toorestrict access tooyour site tooonly users authenticated by Google, set **Action tootake when request is not authenticated** too**Google**.</span></span> <span data-ttu-id="ca6c7-132">Это требует проверку подлинности всех запросов, и все запросы без проверки подлинности, перенаправленный tooGoogle для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooGoogle for authentication.</span></span>
5. <span data-ttu-id="ca6c7-133">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-133">Click **Save**.</span></span>

<span data-ttu-id="ca6c7-134">Теперь вы находитесь готов toouse Google для проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="ca6c7-134">You are now ready toouse Google for authentication in your app.</span></span>

## <span data-ttu-id="ca6c7-135"><a name="related-content"> </a>Связанная информация</span><span class="sxs-lookup"><span data-stu-id="ca6c7-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[портал Azure]: https://portal.azure.com/

