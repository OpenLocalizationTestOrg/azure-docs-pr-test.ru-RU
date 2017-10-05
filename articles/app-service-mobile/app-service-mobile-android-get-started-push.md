---
title: "Добавление push-уведомлений в приложение Android с помощью мобильных приложений | Документация Майкрософт"
description: "Узнайте, как использовать мобильные приложения для отправки push-уведомлений в приложение Android."
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
ms.openlocfilehash: b89e9af55342d5d7473d848956996f846250b4b5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-android-app"></a><span data-ttu-id="70029-103">Добавление push-уведомлений в приложение Android</span><span class="sxs-lookup"><span data-stu-id="70029-103">Add push notifications to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="70029-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="70029-104">Overview</span></span>
<span data-ttu-id="70029-105">В этом учебнике мы добавим push-уведомления в [ознакомительный проект для платформы Android], чтобы при каждом добавлении новой записи на устройство отправлялось push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="70029-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="70029-106">Если вы не используете скачанный проект сервера, необходимо добавить пакет расширений для push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="70029-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="70029-107">Дополнительные сведения см. в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="70029-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70029-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="70029-108">Prerequisites</span></span>
<span data-ttu-id="70029-109">Кроме этого, вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="70029-109">You need the following:</span></span>

* <span data-ttu-id="70029-110">Интегрированная среда разработки, в зависимости от серверной части вашего проекта:</span><span class="sxs-lookup"><span data-stu-id="70029-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="70029-111">[Android Studio](https://developer.android.com/sdk/index.html) — если это приложение имеет серверную часть Node.js.</span><span class="sxs-lookup"><span data-stu-id="70029-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="70029-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) или более поздняя версия — если это приложение имеет серверную часть Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="70029-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="70029-113">Android 2.3 или более поздняя версия, репозиторий Google версии 27 или более поздняя версия и службы Google Play 9.0.2 или более поздняя версия для Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="70029-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="70029-114">Изучение [ознакомительный проект для платформы Android].</span><span class="sxs-lookup"><span data-stu-id="70029-114">Complete the [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="70029-115">Создание проекта с поддержкой Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="70029-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="70029-116">Настройка центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="70029-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="70029-117">Настройка Azure для отправки push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="70029-117">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-the-server-project"></a><span data-ttu-id="70029-118">Включение push-уведомлений для серверного проекта</span><span class="sxs-lookup"><span data-stu-id="70029-118">Enable push notifications for the server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="70029-119">Добавление push-уведомлений в приложение</span><span class="sxs-lookup"><span data-stu-id="70029-119">Add push notifications to your app</span></span>
<span data-ttu-id="70029-120">В этом разделе мы обновим клиентское приложение Android для обработки push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="70029-120">In this section, you update your client Android app to handle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="70029-121">Проверка версии пакета SDK для Android</span><span class="sxs-lookup"><span data-stu-id="70029-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="70029-122">Далее следует установить службы Google Play.</span><span class="sxs-lookup"><span data-stu-id="70029-122">Your next step is to install Google Play services.</span></span> <span data-ttu-id="70029-123">Google Cloud Messaging предъявляет некоторые требования к минимальному уровню API для разработки и тестирования, которым должно удовлетворять свойство **minSdkVersion** в манифесте.</span><span class="sxs-lookup"><span data-stu-id="70029-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span></span>

<span data-ttu-id="70029-124">Если вы тестируете приложение на более старом устройстве, обратитесь к руководству [Настройка пакета SDK служб Google Play], чтобы определить, насколько малым можно задать это значение.</span><span class="sxs-lookup"><span data-stu-id="70029-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] to determine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="70029-125">Добавление служб Google Play в проект</span><span class="sxs-lookup"><span data-stu-id="70029-125">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="70029-126">Добавление кода</span><span class="sxs-lookup"><span data-stu-id="70029-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-the-app-against-the-published-mobile-service"></a><span data-ttu-id="70029-127">Тестирование приложения с помощью опубликованной мобильной службы</span><span class="sxs-lookup"><span data-stu-id="70029-127">Test the app against the published mobile service</span></span>
<span data-ttu-id="70029-128">Приложение можно проверить, подключив телефон Android напрямую с помощью USB-кабеля или используя виртуальное устройство в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="70029-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70029-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="70029-129">Next steps</span></span>
<span data-ttu-id="70029-130">Вы изучили это руководство и теперь можете перейти к ознакомлению с одной из следующих тем.</span><span class="sxs-lookup"><span data-stu-id="70029-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="70029-131">[Добавление аутентификации в приложение Android](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="70029-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="70029-132">Узнайте, как добавить аутентификацию в проект быстрого запуска ToDoList для Android с помощью поддерживаемого поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="70029-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="70029-133">[Включение автономной синхронизации для приложения Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="70029-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="70029-134">Узнайте, как добавить в приложение поддержку автономной работы с помощью серверной части мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="70029-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="70029-135">Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением (&mdash;просматривать, добавлять или изменять данные&mdash;) даже при отсутствии подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="70029-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
<span data-ttu-id="70029-136">[ознакомительный проект для платформы Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="70029-136">[Android quick start]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="70029-137">[Настройка пакета SDK служб Google Play]:https://developers.google.com/android/guides/setup</span><span class="sxs-lookup"><span data-stu-id="70029-137">[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup</span></span>
