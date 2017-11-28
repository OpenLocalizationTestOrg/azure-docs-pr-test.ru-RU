---
title: "Настройка проверки подлинности учетной записи Майкрософт для приложения служб приложений"
description: "Настройка проверки подлинности учетной записи Майкрософт для приложения служб приложений."
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
ms.openlocfilehash: 67386b03ae4cc683fe00e11e8dad19d1442eff09
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-microsoft-account-login"></a><span data-ttu-id="e99fe-103">Настройка приложения службы приложений для использования входа по учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="e99fe-103">How to configure your App Service application to use Microsoft Account login</span></span>
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

<span data-ttu-id="e99fe-104">В этом разделе показано, как настроить службу приложений Azure для использования учетной записи Майкрософт в качестве поставщика проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e99fe-104">This topic shows you how to configure Azure App Service to use Microsoft Account as an authentication provider.</span></span> 

## <span data-ttu-id="e99fe-105"><a name="register-microsoft-account"> </a>Регистрация приложения с использованием учетной записи Майкрософт</span><span class="sxs-lookup"><span data-stu-id="e99fe-105"><a name="register-microsoft-account"> </a>Register your app with Microsoft Account</span></span>
1. <span data-ttu-id="e99fe-106">Перейдите на [портале Azure]и перейдите к своему приложению.</span><span class="sxs-lookup"><span data-stu-id="e99fe-106">Log on to the [Azure portal], and navigate to your application.</span></span> <span data-ttu-id="e99fe-107">Скопируйте **URL-адрес**, который позже понадобится для настройки приложения с помощью учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e99fe-107">Copy your **URL**, which later you use to configure your app with Microsoft Account.</span></span>
2. <span data-ttu-id="e99fe-108">Перейдите на страницу [Мои приложения] в центре разработки для учетной записи Майкрософт и войдите по учетной записи Майкрософт, если это требуется.</span><span class="sxs-lookup"><span data-stu-id="e99fe-108">Navigate to the [My Applications] page in the Microsoft Account Developer Center, and log on with your Microsoft account, if required.</span></span>
3. <span data-ttu-id="e99fe-109">Щелкните **Добавить приложение**, введите имя приложения и нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e99fe-109">Click **Add an app**, then type an application name, and click **Create application**.</span></span>
4. <span data-ttu-id="e99fe-110">Запишите **идентификатор приложения**, так как он понадобится позже.</span><span class="sxs-lookup"><span data-stu-id="e99fe-110">Make a note of the **Application ID**, as you will need it later.</span></span> 
5. <span data-ttu-id="e99fe-111">В разделе "Платформы" щелкните **Добавить платформу** и выберите "Интернет".</span><span class="sxs-lookup"><span data-stu-id="e99fe-111">Under "Platforms," click **Add Platform** and select "Web".</span></span>
6. <span data-ttu-id="e99fe-112">В разделе "URI перенаправления" укажите конечную точку для вашего приложения, а затем щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e99fe-112">Under "Redirect URIs" supply the endpoint for your application, then click **Save**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="e99fe-113">Ваш универсальный код ресурса (URI) перенаправления — это URL-адрес приложения, дополненный путем */.auth/login/microsoftaccount/callback*.</span><span class="sxs-lookup"><span data-stu-id="e99fe-113">Your redirect URI is the URL of your application appended with the path, */.auth/login/microsoftaccount/callback*.</span></span> <span data-ttu-id="e99fe-114">Например, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span><span class="sxs-lookup"><span data-stu-id="e99fe-114">For example, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.</span></span>   
   > <span data-ttu-id="e99fe-115">Убедитесь, что используете схему HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e99fe-115">Make sure that you are using the HTTPS scheme.</span></span>
   
7. <span data-ttu-id="e99fe-116">В разделе "Секреты приложения" щелкните **Создать новый пароль**.</span><span class="sxs-lookup"><span data-stu-id="e99fe-116">Under "Application Secrets," click **Generate New Password**.</span></span> <span data-ttu-id="e99fe-117">Запишите отображенное значение.</span><span class="sxs-lookup"><span data-stu-id="e99fe-117">Make note of the value that appears.</span></span> <span data-ttu-id="e99fe-118">Если страница закроется, оно больше не отобразится.</span><span class="sxs-lookup"><span data-stu-id="e99fe-118">Once you leave the page, it will not be displayed again.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e99fe-119">Пароль — это важный элемент обеспечения безопасности.</span><span class="sxs-lookup"><span data-stu-id="e99fe-119">The password is an important security credential.</span></span> <span data-ttu-id="e99fe-120">Не сообщайте пароль никому и не раскрывайте его в клиентском приложении.</span><span class="sxs-lookup"><span data-stu-id="e99fe-120">Do not share the password with anyone or distribute it within a client application.</span></span>

## <span data-ttu-id="e99fe-121"><a name="secrets"> </a>Добавление данных учетной записи Майкрософт в приложение службы приложений</span><span class="sxs-lookup"><span data-stu-id="e99fe-121"><a name="secrets"> </a>Add Microsoft Account information to your App Service application</span></span>
1. <span data-ttu-id="e99fe-122">На [портале Azure] перейдите к своему приложению, а затем щелкните **Параметры** > **Проверка подлинности и авторизация**.</span><span class="sxs-lookup"><span data-stu-id="e99fe-122">Back in the [Azure portal], navigate to your application, click **Settings** > **Authentication / Authorization**.</span></span>
2. <span data-ttu-id="e99fe-123">Если функция проверки подлинности и авторизации не включена, установите переключатель в положение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="e99fe-123">If the Authentication / Authorization feature is not enabled, switch it **On**.</span></span>
3. <span data-ttu-id="e99fe-124">Щелкните **учетную запись Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="e99fe-124">Click **Microsoft Account**.</span></span> <span data-ttu-id="e99fe-125">Вставьте значения идентификатора приложения и пароля, полученные ранее, и при необходимости включите любые области, которые требуются приложению.</span><span class="sxs-lookup"><span data-stu-id="e99fe-125">Paste in the Application ID and Password values which you obtained previously, and optionally enable any scopes your application requires.</span></span> <span data-ttu-id="e99fe-126">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e99fe-126">Then click **OK**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="e99fe-127">По умолчанию служба приложений обеспечивает проверку подлинности, но не ограничивает авторизованный доступ к содержимому сайта и API.</span><span class="sxs-lookup"><span data-stu-id="e99fe-127">By default, App Service provides authentication but does not restrict authorized access to your site content and APIs.</span></span> <span data-ttu-id="e99fe-128">Авторизация пользователей должна быть включена в код приложения.</span><span class="sxs-lookup"><span data-stu-id="e99fe-128">You must authorize users in your app code.</span></span>
4. <span data-ttu-id="e99fe-129">(Необязательно.) Чтобы предоставить доступ к сайту только пользователям, прошедшим проверку подлинности по учетной записи Майкрософт, установите для параметра **Предпринимаемое действие, если проверка подлинности для запроса не выполнена** значение **Учетная запись Майкрософт**.</span><span class="sxs-lookup"><span data-stu-id="e99fe-129">(Optional) To restrict access to your site to only users authenticated by Microsoft account, set **Action to take when request is not authenticated** to **Microsoft Account**.</span></span> <span data-ttu-id="e99fe-130">В этом случае все запросы, не прошедшие проверку подлинности, направляются для проверки подлинности по учетной записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="e99fe-130">This requires that all requests be authenticated, and all unauthenticated requests are redirected to Microsoft account for authentication.</span></span>
5. <span data-ttu-id="e99fe-131">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e99fe-131">Click **Save**.</span></span>

<span data-ttu-id="e99fe-132">Теперь вы можете использовать учетную запись Майкрософт для проверки подлинности в приложении.</span><span class="sxs-lookup"><span data-stu-id="e99fe-132">You are now ready to use Microsoft Account for authentication in your app.</span></span>

## <span data-ttu-id="e99fe-133"><a name="related-content"> </a>Связанная информация</span><span class="sxs-lookup"><span data-stu-id="e99fe-133"><a name="related-content"> </a>Related content</span></span>
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[Мои приложения]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[портале Azure]: https://portal.azure.com/
