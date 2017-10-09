---
title: "Проверка подлинности Twitter tooconfigure aaaHow для приложения службы приложений"
description: "Узнайте, как проверка подлинности Twitter tooconfigure для приложения службы приложений."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a><span data-ttu-id="8dc16-103">Как tooconfigure имя входа Twitter toouse приложения служб приложений</span><span class="sxs-lookup"><span data-stu-id="8dc16-103">How tooconfigure your App Service application toouse Twitter login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="8dc16-104">В этом разделе показано, как службы приложений Azure tooconfigure toouse Twitter, как поставщик проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8dc16-104">This topic shows you how tooconfigure Azure App Service toouse Twitter as an authentication provider.</span></span>

<span data-ttu-id="8dc16-105">toocomplete hello процедуры в этом разделе, необходимо иметь учетную запись Twitter, имеющую проверенных электронной почты адрес и номер телефона.</span><span class="sxs-lookup"><span data-stu-id="8dc16-105">toocomplete hello procedure in this topic, you must have a Twitter account that has a verified email address and phone number.</span></span> <span data-ttu-id="8dc16-106">toocreate новую учетную запись Twitter, переход слишком<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span><span class="sxs-lookup"><span data-stu-id="8dc16-106">toocreate a new Twitter account, go too<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.</span></span>

## <span data-ttu-id="8dc16-107"><a name="register"> </a>Регистрация приложения в Twitter</span><span class="sxs-lookup"><span data-stu-id="8dc16-107"><a name="register"> </a>Register your application with Twitter</span></span>
1. <span data-ttu-id="8dc16-108">Войдите на toohello [портал Azure]и перейдите tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="8dc16-108">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="8dc16-109">Скопируйте свой **URL-адрес**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-109">Copy your **URL**.</span></span> <span data-ttu-id="8dc16-110">Вы воспользуетесь этой tooconfigure приложения Twitter.</span><span class="sxs-lookup"><span data-stu-id="8dc16-110">You will use this tooconfigure your Twitter app.</span></span>
2. <span data-ttu-id="8dc16-111">Перейдите toohello [Twitter разработчики] веб-сайта, войдите, используя учетные данные учетной записи Twitter и нажмите кнопку **создать новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-111">Navigate toohello [Twitter Developers] website, sign in with your Twitter account credentials, and click **Create New App**.</span></span>
3. <span data-ttu-id="8dc16-112">Тип в hello **имя** и **описание** для нового приложения.</span><span class="sxs-lookup"><span data-stu-id="8dc16-112">Type in hello **Name** and a **Description** for your new app.</span></span> <span data-ttu-id="8dc16-113">Вставить в вашем приложении **URL-адрес** для hello **веб-сайт** значение.</span><span class="sxs-lookup"><span data-stu-id="8dc16-113">Paste in your application's **URL** for hello **Website** value.</span></span> <span data-ttu-id="8dc16-114">Затем для hello **URL-адрес обратного вызова**, вставьте hello **URL-адрес обратного вызова** скопированное ранее.</span><span class="sxs-lookup"><span data-stu-id="8dc16-114">Then, for hello **Callback URL**, paste hello **Callback URL** you copied earlier.</span></span> <span data-ttu-id="8dc16-115">Это шлюз мобильного приложения, дополненная путь hello */.auth/login/twitter/callback*.</span><span class="sxs-lookup"><span data-stu-id="8dc16-115">This is your Mobile App gateway appended with hello path, */.auth/login/twitter/callback*.</span></span> <span data-ttu-id="8dc16-116">Например, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="8dc16-116">For example, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`.</span></span> <span data-ttu-id="8dc16-117">Убедитесь, что вы используете hello схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8dc16-117">Make sure that you are using hello HTTPS scheme.</span></span>
4. <span data-ttu-id="8dc16-118">На странице приветствия нижней hello прочтите и примите условия hello.</span><span class="sxs-lookup"><span data-stu-id="8dc16-118">At hello bottom hello page, read and accept hello terms.</span></span> <span data-ttu-id="8dc16-119">Затем щелкните **Создать приложение Twitter**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-119">Then click **Create your Twitter application**.</span></span> <span data-ttu-id="8dc16-120">Это приложение hello регистры отображает подробные сведения о приложении hello.</span><span class="sxs-lookup"><span data-stu-id="8dc16-120">This registers hello app displays hello application details.</span></span>
5. <span data-ttu-id="8dc16-121">Нажмите кнопку hello **параметры** установите флажок **разрешить toosign toobe использовать это приложение с использованием Twitter**, нажмите кнопку **параметры обновления**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-121">Click hello **Settings** tab, check **Allow this application toobe used toosign in with Twitter**, then click **Update Settings**.</span></span>
6. <span data-ttu-id="8dc16-122">Выберите hello **ключей и маркеры доступа** вкладки. Запомните значения hello **потребителя ключом (API)** и **секрет пользователя (секрет API)**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-122">Select hello **Keys and Access Tokens** tab. Make a note of hello values of **Consumer Key (API Key)** and **Consumer secret (API Secret)**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8dc16-123">секрет получателя Hello — важный элемент обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="8dc16-123">hello consumer secret is an important security credential.</span></span> <span data-ttu-id="8dc16-124">Не сообщайте никому этого секрета и не распространяйте его вместе с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="8dc16-124">Do not share this secret with anyone or distribute it with your app.</span></span>
   > 
   > 

## <span data-ttu-id="8dc16-125"><a name="secrets"></a>Добавить Twitter приложения tooyour сведения</span><span class="sxs-lookup"><span data-stu-id="8dc16-125"><a name="secrets"> </a>Add Twitter information tooyour application</span></span>
1. <span data-ttu-id="8dc16-126">Вернитесь в hello [портал Azure], перейдите tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="8dc16-126">Back in hello [Azure portal], navigate tooyour application.</span></span> <span data-ttu-id="8dc16-127">Щелкните **Параметры**, а затем — **Проверка подлинности или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-127">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="8dc16-128">Если hello проверки подлинности и авторизации не включена, включать hello слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-128">If hello Authentication / Authorization feature is not enabled, turn hello switch too**On**.</span></span>
3. <span data-ttu-id="8dc16-129">Щелкните **Twitter**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-129">Click **Twitter**.</span></span> <span data-ttu-id="8dc16-130">Значения, которые ранее полученный вставьте hello идентификатор приложения и секрет приложения.</span><span class="sxs-lookup"><span data-stu-id="8dc16-130">Paste in hello App ID and App Secret values which you obtained previously.</span></span> <span data-ttu-id="8dc16-131">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-131">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="8dc16-132">По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="8dc16-132">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="8dc16-133">Авторизация пользователей должна быть включена в код приложения.</span><span class="sxs-lookup"><span data-stu-id="8dc16-133">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="8dc16-134">(Необязательно) toorestrict доступа tooyour сайта tooonly пользователь проверку подлинности Twitter, установить **tootake действия, если запрос не прошел проверку подлинности** слишком**Twitter**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-134">(Optional) toorestrict access tooyour site tooonly users authenticated by Twitter, set **Action tootake when request is not authenticated** too**Twitter**.</span></span> <span data-ttu-id="8dc16-135">Это требует проверку подлинности всех запросов, и все запросы без проверки подлинности, перенаправленный tooTwitter для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8dc16-135">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooTwitter for authentication.</span></span>
5. <span data-ttu-id="8dc16-136">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8dc16-136">Click **Save**.</span></span>

<span data-ttu-id="8dc16-137">Теперь вы находитесь готов toouse Twitter для проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="8dc16-137">You are now ready toouse Twitter for authentication in your app.</span></span>

## <span data-ttu-id="8dc16-138"><a name="related-content"> </a>Связанная информация</span><span class="sxs-lookup"><span data-stu-id="8dc16-138"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter разработчики]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[портал Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
