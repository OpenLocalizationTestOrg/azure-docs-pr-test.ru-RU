---
title: "Настройка проверки подлинности Google для приложения служб приложений"
description: "Настройка проверки подлинности Google для приложения служб приложений."
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
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a><span data-ttu-id="7b297-103">Как настроить приложение службы приложений для использования имени для входа Google</span><span class="sxs-lookup"><span data-stu-id="7b297-103">How to configure your App Service application to use Google login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="7b297-104">В этом разделе показано, как настроить службу приложений Azure для использования Google в качестве поставщика проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7b297-104">This topic shows you how to configure Azure App Service to use Google as an authentication provider.</span></span>

<span data-ttu-id="7b297-105">Чтобы выполнить процедуру, описанную в этом разделе, необходимо иметь учетную запись Google с проверенным адресом электронной почты.</span><span class="sxs-lookup"><span data-stu-id="7b297-105">To complete the procedure in this topic, you must have a Google account that has a verified email address.</span></span> <span data-ttu-id="7b297-106">Чтобы создать новую учетную запись Google, перейдите по ссылке [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="7b297-106">To create a new Google account, go to [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>

## <span data-ttu-id="7b297-107"><a name="register"> </a>Регистрация приложения с помощью Google</span><span class="sxs-lookup"><span data-stu-id="7b297-107"><a name="register"> </a>Register your application with Google</span></span>
1. <span data-ttu-id="7b297-108">Войдите на [портал Azure]и перейдите к своему приложению.</span><span class="sxs-lookup"><span data-stu-id="7b297-108">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="7b297-109">Скопируйте **URL-адрес**, который вы будете использовать позже для настройки приложения Google.</span><span class="sxs-lookup"><span data-stu-id="7b297-109">Copy your **URL**, which you use later to configure your Google app.</span></span>
2. <span data-ttu-id="7b297-110">Перейдите на веб-сайт [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303), войдите с помощью учетных данных Google, выберите команду **Создать проект**, укажите имя проекта в поле **Название проекта**, а затем нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7b297-110">Navigate to the [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303) website, sign in with your Google account credentials, click **Create Project**, provide a **Project name**, then click **Create**.</span></span>
3. <span data-ttu-id="7b297-111">В разделе **Social APIs** (Интерфейсы API для соцсетей) щелкните **Google + API**, а затем — **Включить**.</span><span class="sxs-lookup"><span data-stu-id="7b297-111">Under **Social APIs** click **Google+ API** and then **Enable**.</span></span>
4. <span data-ttu-id="7b297-112">В области навигации слева выберите **Учетные данные** > **OAuth consent screen** (Экран согласия OAuth), выберите свой **адрес электронной почты**, введите **имя продукта** и щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7b297-112">In the left navigation, **Credentials** > **OAuth consent screen**, then select your **Email address**,  enter a **Product Name**, and click **Save**.</span></span>
5. <span data-ttu-id="7b297-113">На вкладке **Учетные данные** щелкните **Create credentials** (Создать учетные данные) > **Идентификатор клиента OAuth**, а затем выберите **Веб-приложение**.</span><span class="sxs-lookup"><span data-stu-id="7b297-113">In the **Credentials** tab, click **Create credentials** > **OAuth client ID**, then select **Web application**.</span></span>
6. <span data-ttu-id="7b297-114">Вставьте скопированный ранее **URL-адрес** службы приложений в поле **Authorized JavaScript Origins** (Разрешенные источники JavaScript) и вставьте универсальный код ресурса (URI) перенаправления в поле **Authorized Redirect URI** (Разрешенный код URI перенаправления).</span><span class="sxs-lookup"><span data-stu-id="7b297-114">Paste the App Service **URL** you copied earlier into **Authorized JavaScript Origins**, then paste your redirect URI into **Authorized Redirect URI**.</span></span> <span data-ttu-id="7b297-115">Универсальный код ресурса (URI) перенаправления — это URL-адрес приложения, дополненный путем */.auth/login/google/callback*.</span><span class="sxs-lookup"><span data-stu-id="7b297-115">The redirect URI is the URL of your application appended with the path, */.auth/login/google/callback*.</span></span> <span data-ttu-id="7b297-116">Например, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span><span class="sxs-lookup"><span data-stu-id="7b297-116">For example, `https://contoso.azurewebsites.net/.auth/login/google/callback`.</span></span> <span data-ttu-id="7b297-117">Убедитесь, что используете схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7b297-117">Make sure that you are using the HTTPS scheme.</span></span> <span data-ttu-id="7b297-118">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7b297-118">Then click **Create**.</span></span>
7. <span data-ttu-id="7b297-119">На следующем экране запишите идентификатор клиента и секрет клиента.</span><span class="sxs-lookup"><span data-stu-id="7b297-119">On the next screen, make a note of the values of the client ID and client secret.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7b297-120">Секрет клиента — это важные учетные данные безопасности.</span><span class="sxs-lookup"><span data-stu-id="7b297-120">The client secret is an important security credential.</span></span> <span data-ttu-id="7b297-121">Не сообщайте этот секрет никому и не раскрывайте его в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="7b297-121">Do not share this secret with anyone or distribute it within a client application.</span></span>


## <span data-ttu-id="7b297-122"><a name="secrets"> </a>Добавление данных Google в приложение</span><span class="sxs-lookup"><span data-stu-id="7b297-122"><a name="secrets"> </a>Add Google information to your application</span></span>
1. <span data-ttu-id="7b297-123">Снова вернитесь на [портал Azure]и перейдите к своему приложению.</span><span class="sxs-lookup"><span data-stu-id="7b297-123">Back in the [Azure portal], navigate to your application.</span></span> <span data-ttu-id="7b297-124">Щелкните **Параметры**, а затем — **Проверка подлинности или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="7b297-124">Click **Settings**, and then **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="7b297-125">Если функция аутентификации или авторизации не включена, установите переключатель в положение **Вкл**.</span><span class="sxs-lookup"><span data-stu-id="7b297-125">If the Authentication / Authorization feature is not enabled, turn the switch to **On**.</span></span>
3. <span data-ttu-id="7b297-126">Щелкните **Google**.</span><span class="sxs-lookup"><span data-stu-id="7b297-126">Click **Google**.</span></span> <span data-ttu-id="7b297-127">Вставьте значения идентификатора и секретного кода приложения, полученные ранее, и, при необходимости, включите любые области, которые требуются приложению.</span><span class="sxs-lookup"><span data-stu-id="7b297-127">Paste in the App ID and App Secret values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="7b297-128">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7b297-128">Then click **OK**.</span></span>
   
   ![][1]
   
   <span data-ttu-id="7b297-129">По умолчанию служба приложений обеспечивает проверку подлинности, но не ограничивает авторизованный доступ к содержимому сайта и API.</span><span class="sxs-lookup"><span data-stu-id="7b297-129">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="7b297-130">Авторизация пользователей должна быть включена в код приложения.</span><span class="sxs-lookup"><span data-stu-id="7b297-130">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="7b297-131">(Необязательно.) Чтобы предоставить доступ к сайту только пользователям, прошедшим проверку подлинности в Google, установите для параметра **Предпринимаемое действие, если проверка подлинности для запроса не выполнена** значение **Google**.</span><span class="sxs-lookup"><span data-stu-id="7b297-131">(Optional) To restrict access to your site to only users authenticated by Google, set **Action to take when request is not authenticated** to **Google**.</span></span> <span data-ttu-id="7b297-132">В этом случае все запросы, не прошедшие проверку подлинности, направляются для проверки подлинности с помощью Google.</span><span class="sxs-lookup"><span data-stu-id="7b297-132">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Google for authentication.</span></span>
5. <span data-ttu-id="7b297-133">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7b297-133">Click **Save**.</span></span>

<span data-ttu-id="7b297-134">Теперь вы готовы использовать Google для проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="7b297-134">You are now ready to use Google for authentication in your app.</span></span>

## <span data-ttu-id="7b297-135"><a name="related-content"> </a>Связанная информация</span><span class="sxs-lookup"><span data-stu-id="7b297-135"><a name="related-content"> </a>Related Content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[портал Azure]: https://portal.azure.com/

