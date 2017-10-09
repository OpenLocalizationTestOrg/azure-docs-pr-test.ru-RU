---
title: "aaaAdd принудительной уведомления tooyour приложения Android с помощью мобильных приложений | Документы Microsoft"
description: "Узнайте, как мобильные приложения toosend toouse push приложения Android tooyour уведомления."
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="8a945-103">Добавить приложение Android tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="8a945-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="8a945-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="8a945-104">Overview</span></span>
<span data-ttu-id="8a945-105">В этом учебнике добавить push уведомления toohello [краткое руководство по Android] проекта, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="8a945-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="8a945-106">Если вы не используете hello загружен быстрый запуск сервера проекта, требуется hello пакета расширения уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="8a945-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="8a945-107">Дополнительные сведения см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="8a945-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a945-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8a945-108">Prerequisites</span></span>
<span data-ttu-id="8a945-109">Требуется hello следующее:</span><span class="sxs-lookup"><span data-stu-id="8a945-109">You need hello following:</span></span>

* <span data-ttu-id="8a945-110">Интегрированная среда разработки, в зависимости от серверной части вашего проекта:</span><span class="sxs-lookup"><span data-stu-id="8a945-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="8a945-111">[Android Studio](https://developer.android.com/sdk/index.html) — если это приложение имеет серверную часть Node.js.</span><span class="sxs-lookup"><span data-stu-id="8a945-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="8a945-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) или более поздняя версия — если это приложение имеет серверную часть Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="8a945-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="8a945-113">Android 2.3 или более поздняя версия, репозиторий Google версии 27 или более поздняя версия и службы Google Play 9.0.2 или более поздняя версия для Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="8a945-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="8a945-114">Полный hello [краткое руководство по Android].</span><span class="sxs-lookup"><span data-stu-id="8a945-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="8a945-115">Создание проекта с поддержкой Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="8a945-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="8a945-116">Настройка центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="8a945-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="8a945-117">Настройка Azure toosend push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="8a945-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="8a945-118">Включить push-уведомления для проекта сервера hello</span><span class="sxs-lookup"><span data-stu-id="8a945-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="8a945-119">Добавить приложение tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="8a945-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="8a945-120">В этом разделе обновить ваш клиент приложения Android toohandle push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="8a945-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="8a945-121">Проверка версии пакета SDK для Android</span><span class="sxs-lookup"><span data-stu-id="8a945-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="8a945-122">Следующим шагом является tooinstall служб Google Play.</span><span class="sxs-lookup"><span data-stu-id="8a945-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="8a945-123">Google Cloud Messaging имеет некоторые минимальные требования уровня API для разработки и тестирования, какие hello **minSdkVersion** должно соответствовать свойству в манифесте hello.</span><span class="sxs-lookup"><span data-stu-id="8a945-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="8a945-124">Если вы тестируете с старое устройство, обратитесь к [задайте копии Google воспроизведения пакета SDK служб] toodetermine малых это значение и настроить ее соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="8a945-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="8a945-125">Добавление проекта toohello служб Google Play</span><span class="sxs-lookup"><span data-stu-id="8a945-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="8a945-126">Добавление кода</span><span class="sxs-lookup"><span data-stu-id="8a945-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="8a945-127">Тестовое приложение hello от hello публикации мобильной службы</span><span class="sxs-lookup"><span data-stu-id="8a945-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="8a945-128">Вы можете протестировать приложение hello, присоединив телефоне с Android с помощью кабеля USB непосредственно или с помощью виртуального устройства в эмуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="8a945-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a945-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a945-129">Next steps</span></span>
<span data-ttu-id="8a945-130">Завершения этого учебника рекомендуется продолжить на tooone из hello следующие учебники:</span><span class="sxs-lookup"><span data-stu-id="8a945-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="8a945-131">[Добавить приложение Android tooyour проверки подлинности](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="8a945-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="8a945-132">Узнайте, как проект quickstart todolist toohello проверки подлинности tooadd на Android с помощью поставщика удостоверений, поддерживаемых.</span><span class="sxs-lookup"><span data-stu-id="8a945-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="8a945-133">[Включение автономной синхронизации для приложения Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="8a945-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="8a945-134">Узнайте, как tooadd в автономном режиме поддерживают tooyour приложения с помощью серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="8a945-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="8a945-135">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением (&mdash;просматривать, добавлять или изменять данные&mdash;) даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="8a945-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[краткое руководство по Android]: app-service-mobile-android-get-started.md

[задайте копии Google воспроизведения пакета SDK служб]:https://developers.google.com/android/guides/setup
