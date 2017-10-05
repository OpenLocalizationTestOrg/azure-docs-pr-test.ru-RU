---
title: "Добавление проверки подлинности в Android с помощью мобильных приложений | Документация Майкрософт"
description: "Узнайте, как использовать функцию мобильных приложений службы приложений Azure для аутентификации пользователей приложения Android с помощью разнообразных поставщиков удостоверений, включая Google, Facebook, Twitter и корпорацию Майкрософт."
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 1fc8e7c1-6c3c-40f4-9967-9cf5e21fc4e1
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 81331142aa6110d4e29e6fb30a90ce6e3a853439
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-android-app"></a><span data-ttu-id="d6a01-103">Добавление проверки подлинности в приложение Android</span><span class="sxs-lookup"><span data-stu-id="d6a01-103">Add authentication to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="d6a01-104">Сводка</span><span class="sxs-lookup"><span data-stu-id="d6a01-104">Summary</span></span>
<span data-ttu-id="d6a01-105">В этом руководстве вы добавите аутентификацию в проект быстрого запуска ToDoList для Android с помощью поддерживаемого поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="d6a01-105">In this tutorial, you add authentication to the todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="d6a01-106">Этот учебник создан на основе учебника [Начало работы с мобильными службами] , который необходимо изучить в первую очередь.</span><span class="sxs-lookup"><span data-stu-id="d6a01-106">This tutorial is based on the [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="d6a01-107"><a name="register"></a>Регистрация приложения для аутентификации и настройка службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="d6a01-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="d6a01-108"><a name="redirecturl"></a>Добавление приложения в список разрешенных URL-адресов внешнего перенаправления</span><span class="sxs-lookup"><span data-stu-id="d6a01-108"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="d6a01-109">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a01-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="d6a01-110">Это позволяет системе аутентификации выполнять перенаправление обратно в приложение после завершения процесса аутентификации.</span><span class="sxs-lookup"><span data-stu-id="d6a01-110">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="d6a01-111">В этом руководстве мы повсеместно используем схему URL-адресов _appname_.</span><span class="sxs-lookup"><span data-stu-id="d6a01-111">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="d6a01-112">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="d6a01-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="d6a01-113">Она должна быть уникальной для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a01-113">It should be unique to your mobile application.</span></span> <span data-ttu-id="d6a01-114">Вот как можно включить перенаправление на стороне сервера.</span><span class="sxs-lookup"><span data-stu-id="d6a01-114">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="d6a01-115">На портале Azure выберите свою службу приложений.</span><span class="sxs-lookup"><span data-stu-id="d6a01-115">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="d6a01-116">Выберите пункт меню **Аутентификация или авторизация**.</span><span class="sxs-lookup"><span data-stu-id="d6a01-116">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="d6a01-117">В поле **Разрешенные URL-адреса внешнего перенаправления** введите `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="d6a01-117">In the **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="d6a01-118">_appname_ в этой строке — это схема URL-адресов для вашего мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a01-118">The _appname_ in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="d6a01-119">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="d6a01-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="d6a01-120">Необходимо записать выбранную строку, так как потребуется в нескольких местах настроить код мобильного приложения с использованием схемы URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="d6a01-120">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="d6a01-121">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d6a01-121">Click **OK**.</span></span>

5. <span data-ttu-id="d6a01-122">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d6a01-122">Click **Save**.</span></span>

## <span data-ttu-id="d6a01-123"><a name="permissions"></a>Предоставление разрешений только пользователям, прошедшим проверку подлинности</span><span class="sxs-lookup"><span data-stu-id="d6a01-123"><a name="permissions"></a>Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="d6a01-124">В Android Studio откройте проект, при выполнении заданий руководства [Начало работы с мобильными службами].</span><span class="sxs-lookup"><span data-stu-id="d6a01-124">In Android Studio, open the project you completed with the tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="d6a01-125">В меню **Run** (Запуск) щелкните **Run app** (Запустить приложение). Убедитесь, что после запуска приложения возникает необработанное исключение с кодом состояния "401 (Не авторизовано)".</span><span class="sxs-lookup"><span data-stu-id="d6a01-125">From the **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span>

     <span data-ttu-id="d6a01-126">Это происходит, потому что приложение пытается получить доступ к серверной части как неаутентифицированный пользователь, а таблица *TodoItem* теперь требует проходить аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="d6a01-126">This exception happens because the app attempts to access the back end as an unauthenticated user, but the *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="d6a01-127">Далее мы изменим приложение таким образом, что оно станет аутентифицировать пользователей, прежде чем запрашивать ресурсы из серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="d6a01-127">Next, you update the app to authenticate users before requesting resources from the Mobile Apps back end.</span></span> 

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="d6a01-128">Добавление проверки подлинности в приложение</span><span class="sxs-lookup"><span data-stu-id="d6a01-128">Add authentication to the app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="d6a01-129"><a name="cache-tokens"></a>Кэширование маркеров проверки подлинности на клиенте</span><span class="sxs-lookup"><span data-stu-id="d6a01-129"><a name="cache-tokens"></a>Cache authentication tokens on the client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="d6a01-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6a01-130">Next steps</span></span>
<span data-ttu-id="d6a01-131">Вы прошли этот учебник по обычной проверке подлинности и теперь можете перейти к одному из следующих учебников:</span><span class="sxs-lookup"><span data-stu-id="d6a01-131">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="d6a01-132">[Добавление push-уведомлений в приложение Android](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="d6a01-132">[Add push notifications to your Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="d6a01-133">Узнайте, как добавить поддержку push-уведомлений в мобильное приложение и настроить в его серверной части использование центров уведомлений Azure для отправки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="d6a01-133">Learn how to configure your Mobile Apps back end to use Azure notification hubs to send push notifications.</span></span>
* <span data-ttu-id="d6a01-134">[Включение автономной синхронизации для приложения Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="d6a01-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="d6a01-135">Узнайте, как добавить в приложение поддержку автономной работы с помощью серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="d6a01-135">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="d6a01-136">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением (&mdash;просматривать, добавлять или изменять данные&mdash;) даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="d6a01-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions to authenticated users]: #permissions
[Add authentication to the app]: #add-authentication
[Store authentication tokens on the client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
<span data-ttu-id="d6a01-137">[Начало работы с мобильными службами]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="d6a01-137">[Get started with Mobile Apps]: app-service-mobile-android-get-started.md</span></span>
