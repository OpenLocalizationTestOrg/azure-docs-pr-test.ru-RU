---
title: "aaaHow tooconfigure Facebook и проверки подлинности для приложения службы приложений"
description: "Узнайте, как tooconfigure проверки подлинности Facebook для приложения службы приложений."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a><span data-ttu-id="28e5e-103">Как tooconfigure имени входа Facebook toouse приложения служб приложений</span><span class="sxs-lookup"><span data-stu-id="28e5e-103">How tooconfigure your App Service application toouse Facebook login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="28e5e-104">В этом разделе показано, как службы приложений Azure tooconfigure toouse Facebook в качестве поставщика проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="28e5e-104">This topic shows you how tooconfigure Azure App Service toouse Facebook as an authentication provider.</span></span>

<span data-ttu-id="28e5e-105">toocomplete hello процедуры в этом разделе, необходимо иметь учетную запись Facebook с проверенной адрес и номер мобильного телефона.</span><span class="sxs-lookup"><span data-stu-id="28e5e-105">toocomplete hello procedure in this topic, you must have a Facebook account that has a verified email address and a mobile phone number.</span></span> <span data-ttu-id="28e5e-106">toocreate новую учетную запись Facebook go слишком[facebook.com].</span><span class="sxs-lookup"><span data-stu-id="28e5e-106">toocreate a new Facebook account, go too[facebook.com].</span></span>

## <span data-ttu-id="28e5e-107"><a name="register"> </a>Регистрация приложения с помощью Facebook</span><span class="sxs-lookup"><span data-stu-id="28e5e-107"><a name="register"> </a>Register your application with Facebook</span></span>
1. <span data-ttu-id="28e5e-108">Войдите на toohello [портал Azure]и перейдите tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="28e5e-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="28e5e-109">Скопируйте свой **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="28e5e-109">Copy your **URL**.</span></span> <span data-ttu-id="28e5e-110">Вы воспользуетесь этой tooconfigure приложения Facebook.</span><span class="sxs-lookup"><span data-stu-id="28e5e-110">You will use this tooconfigure your Facebook app.</span></span>
2. <span data-ttu-id="28e5e-111">В другом окне браузера перейдите toohello [разработчиков в Facebook] веб-сайта и войдите в ваш Facebook учетные данные учетной записи.</span><span class="sxs-lookup"><span data-stu-id="28e5e-111">In another browser window, navigate toohello [Facebook Developers] website and sign-in with your Facebook account credentials.</span></span>
3. <span data-ttu-id="28e5e-112">(Необязательно) Если вы уже не зарегистрировались, щелкните **приложения** > **зарегистрировать как разработчик**, примите политику hello и выполните действия по регистрации hello.</span><span class="sxs-lookup"><span data-stu-id="28e5e-112">(Optional) If you have not already registered, click **Apps** > **Register as a Developer**, then accept hello policy and follow hello registration steps.</span></span>
4. <span data-ttu-id="28e5e-113">Щелкните **Мои приложения** > **Add a New App** (Добавить новое приложение) > **Веб-сайт** > **Skip and Create App ID** (Пропустить и создать идентификатор приложения).</span><span class="sxs-lookup"><span data-stu-id="28e5e-113">Click **My Apps** > **Add a New App** > **Website** > **Skip and Create App ID**.</span></span> 
5. <span data-ttu-id="28e5e-114">В **отображаемое имя**, введите уникальное имя для вашего приложения, тип вашей **адрес электронной почты**, выберите **категории** приложение и нажмите кнопку **создать идентификатор приложения**и выполнить проверку безопасности hello.</span><span class="sxs-lookup"><span data-stu-id="28e5e-114">In **Display Name**, type a unique name for your app, type your **Contact Email**, choose a **Category** for your app, then click **Create App ID** and complete hello security check.</span></span> <span data-ttu-id="28e5e-115">Откроется панель toohello разработчика для нового приложения Facebook.</span><span class="sxs-lookup"><span data-stu-id="28e5e-115">This takes you toohello developer dashboard for your new Facebook app.</span></span>
6. <span data-ttu-id="28e5e-116">В разделе Facebook Login (Вход в Facebook) щелкните **Get Started**(Начать).</span><span class="sxs-lookup"><span data-stu-id="28e5e-116">Under "Facebook Login," click **Get Started**.</span></span> <span data-ttu-id="28e5e-117">Добавление приложения **URI перенаправления** слишком**OAuth допустимый URI перенаправления**, нажмите кнопку **сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="28e5e-117">Add your application's **Redirect URI** too**Valid OAuth redirect URIs**, then click **Save Changes**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="28e5e-118">Ваш перенаправления URI является hello URL-адрес приложения дополненная путь hello */.auth/login/facebook/callback*.</span><span class="sxs-lookup"><span data-stu-id="28e5e-118">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/facebook/callback*.</span></span> <span data-ttu-id="28e5e-119">Например, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span><span class="sxs-lookup"><span data-stu-id="28e5e-119">For example, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`.</span></span> <span data-ttu-id="28e5e-120">Убедитесь, что вы используете hello схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="28e5e-120">Make sure that you are using hello HTTPS scheme.</span></span>
   > 
   > 
7. <span data-ttu-id="28e5e-121">В левой области навигации hello щелкните **параметры**.</span><span class="sxs-lookup"><span data-stu-id="28e5e-121">In hello left-hand navigation, click **Settings**.</span></span> <span data-ttu-id="28e5e-122">На hello **секрет приложения** щелкните **Показать**, предоставить свой пароль, если в запросе, а затем запишите значения hello **идентификатор приложения** и **секрет приложения**.</span><span class="sxs-lookup"><span data-stu-id="28e5e-122">On hello **App Secret** field, click **Show**, provide your password if requested, then make a note of hello values of **App ID** and **App Secret**.</span></span> <span data-ttu-id="28e5e-123">Использования этих более поздних tooconfigure приложения в Azure.</span><span class="sxs-lookup"><span data-stu-id="28e5e-123">You use these later tooconfigure your application in Azure.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="28e5e-124">секрет приложения Hello — важный элемент обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="28e5e-124">hello app secret is an important security credential.</span></span> <span data-ttu-id="28e5e-125">Не сообщайте этот секрет никому и не раскрывайте его в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="28e5e-125">Do not share this secret with anyone or distribute it within a client application.</span></span>
   > 
   > 
8. <span data-ttu-id="28e5e-126">Hello Facebook учетной записи, которая была используется tooregister приложения hello не является администратором приложения hello.</span><span class="sxs-lookup"><span data-stu-id="28e5e-126">hello Facebook account which was used tooregister hello application is an administrator of hello app.</span></span> <span data-ttu-id="28e5e-127">На этом этапе только администраторы могут входить в приложение.</span><span class="sxs-lookup"><span data-stu-id="28e5e-127">At this point, only administrators can sign into this application.</span></span> <span data-ttu-id="28e5e-128">tooauthenticate другие учетные записи Facebook, нажмите кнопку **проверки приложения** и включить **марка < your app-name > public** tooenable общие общего доступа с помощью проверки подлинности Facebook.</span><span class="sxs-lookup"><span data-stu-id="28e5e-128">tooauthenticate other Facebook accounts, click **App Review** and enable **Make <your-app-name> public** tooenable general public access using Facebook authentication.</span></span>

## <span data-ttu-id="28e5e-129"><a name="secrets"></a>Tooyour приложения Facebook, добавить сведения</span><span class="sxs-lookup"><span data-stu-id="28e5e-129"><a name="secrets"> </a>Add Facebook information tooyour application</span></span>
1. <span data-ttu-id="28e5e-130">Вернитесь в hello [портал Azure], перейдите tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="28e5e-130">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="28e5e-131">Щелкните **Параметры** > **Аутентификация или авторизация** и установите для параметра **Проверка подлинности службы приложений** значение **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="28e5e-131">Click **Settings** > **Authentication / Authorization**, and make sure that **App Service Authentication** is **On**.</span></span>
2. <span data-ttu-id="28e5e-132">Нажмите кнопку **Facebook**, вставьте в значениях идентификатор приложения и секрет приложения hello, что был получен, при необходимости включить любые области, необходимые для приложения, а затем нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="28e5e-132">Click **Facebook**, paste in hello App ID and App Secret values which you obtained previously, optionally enable any scopes needed by your application, then click **OK**.</span></span>
   
    ![][0]
   
    <span data-ttu-id="28e5e-133">По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="28e5e-133">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="28e5e-134">Авторизация пользователей должна быть включена в код приложения.</span><span class="sxs-lookup"><span data-stu-id="28e5e-134">You must authorize users in your app code.</span></span>
3. <span data-ttu-id="28e5e-135">(Необязательно) toorestrict доступа tooyour сайта tooonly пользователи аутентифицироваться Facebook, задать **tootake действия, если запрос не прошел проверку подлинности** слишком**Facebook**.</span><span class="sxs-lookup"><span data-stu-id="28e5e-135">(Optional) toorestrict access tooyour site tooonly users authenticated by Facebook, set **Action tootake when request is not authenticated** too**Facebook**.</span></span> <span data-ttu-id="28e5e-136">Это требует проверку подлинности всех запросов, и все запросы без проверки подлинности, перенаправленный tooFacebook для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="28e5e-136">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooFacebook for authentication.</span></span>
4. <span data-ttu-id="28e5e-137">Завершив настройку аутентификации, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="28e5e-137">When done configuring authentication, click **Save**.</span></span>

<span data-ttu-id="28e5e-138">Теперь вы находитесь готов toouse Facebook для проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="28e5e-138">You are now ready toouse Facebook for authentication in your app.</span></span>

## <span data-ttu-id="28e5e-139"><a name="related-content"> </a>Связанная информация</span><span class="sxs-lookup"><span data-stu-id="28e5e-139"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[разработчиков в Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[портал Azure]: https://portal.azure.com/
