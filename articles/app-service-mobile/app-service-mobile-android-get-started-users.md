---
title: "проверки подлинности aaaAdd в Android с помощью мобильных приложений | Документы Microsoft"
description: "Узнайте, как toouse hello компонент мобильные приложения службы приложений Azure tooauthenticate пользователей приложения Android с помощью различных поставщиков удостоверений, включая Google, Facebook, Twitter и Майкрософт."
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
ms.openlocfilehash: 01f608f996c931c643790ed2778df11cf590c903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-android-app"></a><span data-ttu-id="a2e2c-103">Добавить приложение Android tooyour проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="a2e2c-103">Add authentication tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a><span data-ttu-id="a2e2c-104">Сводка</span><span class="sxs-lookup"><span data-stu-id="a2e2c-104">Summary</span></span>
<span data-ttu-id="a2e2c-105">В этом учебнике добавлении проверки подлинности toohello todolist быстрый запуск проекта в Android с помощью поставщика удостоверений, поддерживаемых.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-105">In this tutorial, you add authentication toohello todolist quickstart project on Android by using a supported identity provider.</span></span> <span data-ttu-id="a2e2c-106">Этот учебник основывается на hello [начало работы с мобильным приложениям] руководство, в котором необходимо выполнять первой.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-106">This tutorial is based on hello [Get started with Mobile Apps] tutorial, which you must complete first.</span></span>

## <span data-ttu-id="a2e2c-107"><a name="register"></a>Регистрация приложения для аутентификации и настройка службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="a2e2c-107"><a name="register"></a>Register your app for authentication and configure Azure App Service</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="a2e2c-108"><a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений</span><span class="sxs-lookup"><span data-stu-id="a2e2c-108"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="a2e2c-109">Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-109">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="a2e2c-110">Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-110">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="a2e2c-111">В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-111">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="a2e2c-112">Тем не менее можно использовать любую схему URL-адресов на свой выбор.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-112">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="a2e2c-113">Он должен быть уникальным tooyour мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-113">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="a2e2c-114">tooenable hello перенаправления на стороне сервера hello:</span><span class="sxs-lookup"><span data-stu-id="a2e2c-114">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="a2e2c-115">В hello [Azure портал] выберите приложение службы.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-115">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="a2e2c-116">Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-116">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="a2e2c-117">В hello **допускается внешний URL-адреса перенаправления**, введите `appname://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-117">In hello **Allowed External Redirect URLs**, enter `appname://easyauth.callback`.</span></span>  <span data-ttu-id="a2e2c-118">Hello _appname_ в данной строке — hello схема URL-адресов для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-118">hello _appname_ in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="a2e2c-119">Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).</span><span class="sxs-lookup"><span data-stu-id="a2e2c-119">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="a2e2c-120">Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-120">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="a2e2c-121">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-121">Click **OK**.</span></span>

5. <span data-ttu-id="a2e2c-122">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-122">Click **Save**.</span></span>

## <span data-ttu-id="a2e2c-123"><a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="a2e2c-123"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* <span data-ttu-id="a2e2c-124">В Android Studio откройте проект hello, вы выполнили учебнику hello [начало работы с мобильным приложениям].</span><span class="sxs-lookup"><span data-stu-id="a2e2c-124">In Android Studio, open hello project you completed with hello tutorial [Get started with Mobile Apps].</span></span> <span data-ttu-id="a2e2c-125">Из hello **запуска** меню, нажмите кнопку **запуск приложения**и убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-125">From hello **Run** menu, click **Run app**, and verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span>

     <span data-ttu-id="a2e2c-126">Это исключение возникает из-за попытки приложения hello tooaccess hello обратно закончить без проверки подлинности пользователя, но hello *TodoItem* таблица теперь требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-126">This exception happens because hello app attempts tooaccess hello back end as an unauthenticated user, but hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="a2e2c-127">Затем пользователи tooauthenticate приложения hello обновить перед запросом ресурсы из приветствия завершить обратно мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-127">Next, you update hello app tooauthenticate users before requesting resources from hello Mobile Apps back end.</span></span> 

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="a2e2c-128">Добавить приложение toohello проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="a2e2c-128">Add authentication toohello app</span></span>
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <span data-ttu-id="a2e2c-129"><a name="cache-tokens"></a>Кэшировать маркеры проверки подлинности на приветствия клиента</span><span class="sxs-lookup"><span data-stu-id="a2e2c-129"><a name="cache-tokens"></a>Cache authentication tokens on hello client</span></span>
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a><span data-ttu-id="a2e2c-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a2e2c-130">Next steps</span></span>
<span data-ttu-id="a2e2c-131">Завершения этого учебника обычной проверки подлинности, рассмотрите возможность продолжить на tooone из hello следующие учебники:</span><span class="sxs-lookup"><span data-stu-id="a2e2c-131">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="a2e2c-132">[Добавить приложение Android tooyour уведомлений push](app-service-mobile-android-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="a2e2c-132">[Add push notifications tooyour Android app](app-service-mobile-android-get-started-push.md).</span></span>
  <span data-ttu-id="a2e2c-133">Узнайте, tooconfigure обратно на мобильные приложения конечного toouse уведомление Azure концентраторов toosend push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-133">Learn how tooconfigure your Mobile Apps back end toouse Azure notification hubs toosend push notifications.</span></span>
* <span data-ttu-id="a2e2c-134">[Включение автономной синхронизации для приложения Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="a2e2c-134">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="a2e2c-135">Узнайте, как tooadd в автономном режиме поддерживают tooyour приложения с помощью серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-135">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="a2e2c-136">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением (&mdash;просматривать, добавлять или изменять данные&mdash;) даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="a2e2c-136">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[начало работы с мобильным приложениям]: app-service-mobile-android-get-started.md
