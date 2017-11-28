---
title: "Добавление push-уведомлений в приложение Xamarin.Android | Документация Майкрософт"
description: "Узнайте, как использовать службу приложений и центры уведомлений Azure для отправки push-уведомлений в приложение Xamarin.Android."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c3757d56fb1792092710740dc5ffbd64f18730cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="2e7fa-103">Добавление push-уведомлений в приложение Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="2e7fa-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="2e7fa-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="2e7fa-104">Overview</span></span>
<span data-ttu-id="2e7fa-105">В этом руководстве мы добавим push-уведомления в [проект быстрого запуска Xamarin.Android](app-service-mobile-windows-store-dotnet-get-started.md), чтобы при каждом добавлении новой записи на устройство отправлялось push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="2e7fa-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="2e7fa-106">Если вы не используете скачанный проект сервера, необходимо добавить пакет расширений для push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="2e7fa-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="2e7fa-107">Дополнительные сведения о пакетах расширений для сервера см. в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="2e7fa-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e7fa-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2e7fa-108">Prerequisites</span></span>
<span data-ttu-id="2e7fa-109">Для работы с данным учебником требуется следующее:</span><span class="sxs-lookup"><span data-stu-id="2e7fa-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="2e7fa-110">Активная учетная запись Google.</span><span class="sxs-lookup"><span data-stu-id="2e7fa-110">An active Google account.</span></span> <span data-ttu-id="2e7fa-111">Вы можете зарегистрировать учетную запись Google на сайте [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="2e7fa-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="2e7fa-112">[Компонент клиента Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="2e7fa-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="2e7fa-113"><a name="configure-hub"></a>Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="2e7fa-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="2e7fa-114"><a id="register"></a>Включение Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="2e7fa-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="2e7fa-115">Настройка Azure для отправки push-запросов</span><span class="sxs-lookup"><span data-stu-id="2e7fa-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="2e7fa-116"><a id="update-server"></a>Обновление серверного проекта для отправки push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="2e7fa-116"><a id="update-server"></a>Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="2e7fa-117"><a id="configure-app"></a>Настройка клиентского проекта для использования push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="2e7fa-117"><a id="configure-app"></a>Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="2e7fa-118"><a id="add-push"></a>Добавление кода push-уведомлений в приложение</span><span class="sxs-lookup"><span data-stu-id="2e7fa-118"><a id="add-push"></a>Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="2e7fa-119"><a name="test"></a>Тестирование push-уведомлений в приложении</span><span class="sxs-lookup"><span data-stu-id="2e7fa-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="2e7fa-120">Приложение можно проверить, используя виртуальное устройство в эмуляторе.</span><span class="sxs-lookup"><span data-stu-id="2e7fa-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="2e7fa-121">Для запуска в эмуляторе необходимо выполнить дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="2e7fa-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="2e7fa-122">Убедитесь, что для развертывания или отладки используется виртуальное устройство, на котором в качестве назначения заданы интерфейсы Google API, как показано ниже в диспетчере виртуальных устройств Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="2e7fa-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="2e7fa-123">Добавить учетную запись Google на устройстве Android, поочередно щелкнув **Apps** (Приложения) > **Settings** (Параметры) > **Add account** (Добавить учетную запись). Затем следуйте указаниям на экране.</span><span class="sxs-lookup"><span data-stu-id="2e7fa-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="2e7fa-124">Запустите приложение todolist, как ранее, и вставьте новый элемент списка дел.</span><span class="sxs-lookup"><span data-stu-id="2e7fa-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="2e7fa-125">На этот раз в области уведомлений отображается значок уведомления.</span><span class="sxs-lookup"><span data-stu-id="2e7fa-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="2e7fa-126">Вы можете открыть панель уведомлений, чтобы просмотреть полный текст уведомления.</span><span class="sxs-lookup"><span data-stu-id="2e7fa-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
