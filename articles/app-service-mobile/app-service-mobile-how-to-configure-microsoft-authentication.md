---
title: "Проверка подлинности учетной записи Майкрософт tooconfigure aaaHow для приложения службы приложений"
description: "Узнайте, как проверка подлинности учетной записи Майкрософт tooconfigure для приложения службы приложений."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a><span data-ttu-id="2f5ad-103">Как tooconfigure имя входа учетной записи Майкрософт toouse приложения служб приложений</span><span class="sxs-lookup"><span data-stu-id="2f5ad-103">How tooconfigure your App Service application toouse Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="2f5ad-104">В этом разделе показано, как службы приложений Azure tooconfigure toouse учетную запись Майкрософт как поставщик проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-104">This topic shows you how tooconfigure Azure App Service toouse Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="2f5ad-105"><a name="register-microsoft-account"> </a>Регистрация приложения с использованием учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="2f5ad-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="2f5ad-106">Войдите на toohello [портал Azure]и перейдите tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-106">Log on toohello [Azure portal], and navigate tooyour application.</span></span> <span data-ttu-id="2f5ad-107">Копировать вашей **URL-адрес**, который впоследствии используется tooconfigure приложения с учетной записью Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-107">Copy your **URL**, which later you use tooconfigure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="2f5ad-108">Перейдите toohello [Мои приложения] в hello Центр разработчиков учетной записи Майкрософт и войдите с учетной записью Майкрософт, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-108">Navigate toohello [My Applications] page in hello Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="2f5ad-109">Щелкните **Добавить приложение**, введите имя приложения и нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="2f5ad-110">Запишите hello **идентификатор приложения**, как он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-110">Make a note of hello **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="2f5ad-111">В разделе "Платформы" щелкните **Добавить платформу** и выберите "Интернет".</span><span class="sxs-lookup"><span data-stu-id="2f5ad-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="2f5ad-112">Под «URI перенаправления» конечной hello питания для приложения, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-112">Under "Redirect URIs" supply hello endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="2f5ad-113">Ваш перенаправления URI является hello URL-адрес приложения дополненная путь hello */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-113">Your redirect URI is hello URL of your application appended with hello path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="2f5ad-114">Например, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="2f5ad-115">Убедитесь, что вы используете hello схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-115">Make sure that you are using hello HTTPS scheme.</span></span>
   
7. <span data-ttu-id="2f5ad-116">В разделе "Секреты приложения" щелкните **Создать новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="2f5ad-117">Запишите значение hello, которое появляется.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-117">Make note of hello value that appears.</span></span> <span data-ttu-id="2f5ad-118">Когда вы покинете страницу приветствия, он больше не будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-118">Once you leave hello page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2f5ad-119">пароль Hello — важный элемент обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-119">hello password is an important security credential.</span></span> <span data-ttu-id="2f5ad-120">Не делитесь hello пароль с кем и не распространяйте в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-120">Do not share hello password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="2f5ad-121"><a name="secrets"></a>Tooyour добавьте учетную запись Майкрософт сведения приложения служб приложений</span><span class="sxs-lookup"><span data-stu-id="2f5ad-121"><a name="secrets"> </a>Add Microsoft Account information tooyour App Service application</span></span>
1. <span data-ttu-id="2f5ad-122">В hello [портал Azure], перейдите в приложение tooyour, щелкните **параметры** > **проверки подлинности и авторизации**.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-122">Back in hello [Azure portal], navigate tooyour application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="2f5ad-123">Если hello проверки подлинности и авторизации не включена, включите ее **на**.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-123">If hello Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="2f5ad-124">Щелкните **учетную запись Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="2f5ad-125">Вставьте в значениях идентификатора приложения и пароль hello, что был получен и при необходимости включить любые области, которые требуются приложению.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-125">Paste in hello Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="2f5ad-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="2f5ad-127">По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-127">By default, App Service provides authentication but does not restrict authorized access tooyour site content and APIs.</span></span> <span data-ttu-id="2f5ad-128">Авторизация пользователей должна быть включена в код приложения.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="2f5ad-129">(Необязательно) toorestrict доступа tooyour сайта tooonly пользователь проверку подлинности с учетной записью Майкрософт, установить **tootake действия, если запрос не прошел проверку подлинности** слишком**учетную запись Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-129">(Optional) toorestrict access tooyour site tooonly users authenticated by Microsoft account, set **Action tootake when request is not authenticated** too**Microsoft Account**.</span></span> <span data-ttu-id="2f5ad-130">Это требует проверку подлинности всех запросов, и все запросы, не прошедшие проверку подлинности, перенаправляются tooMicrosoft учетной записи для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected tooMicrosoft account for authentication.</span></span>
5. <span data-ttu-id="2f5ad-131">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-131">Click **Save**.</span></span>

<span data-ttu-id="2f5ad-132">Теперь вы находитесь готов toouse учетную запись Майкрософт для проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="2f5ad-132">You are now ready toouse Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="2f5ad-133"><a name="related-content"> </a>Связанная информация</span><span class="sxs-lookup"><span data-stu-id="2f5ad-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[Мои приложения]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[портал Azure]: https://portal.azure.com/
