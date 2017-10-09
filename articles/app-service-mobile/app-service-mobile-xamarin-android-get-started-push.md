---
title: "aaaAdd принудительной уведомления tooyour Xamarin.Android приложения | Документы Microsoft"
description: "Узнайте, как toouse службе приложений Azure и концентраторов уведомлений Azure toosend push-уведомления tooyour Xamarin.Android приложения"
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
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="250b6-103">Добавить приложение Xamarin.Android tooyour уведомлений push</span><span class="sxs-lookup"><span data-stu-id="250b6-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="250b6-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="250b6-104">Overview</span></span>
<span data-ttu-id="250b6-105">В этом учебнике добавить push уведомления toohello [Xamarin.Android краткого](app-service-mobile-windows-store-dotnet-get-started.md) проекта, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="250b6-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="250b6-106">Если вы не используете hello загружен проект быстрый запуск сервера, будет необходимо hello пакета расширения уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="250b6-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="250b6-107">В разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="250b6-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="250b6-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="250b6-108">Prerequisites</span></span>
<span data-ttu-id="250b6-109">Этот учебник требует hello следующее:</span><span class="sxs-lookup"><span data-stu-id="250b6-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="250b6-110">Активная учетная запись Google.</span><span class="sxs-lookup"><span data-stu-id="250b6-110">An active Google account.</span></span> <span data-ttu-id="250b6-111">Вы можете зарегистрировать учетную запись Google на сайте [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="250b6-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="250b6-112">[Компонент клиента Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="250b6-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="250b6-113"><a name="configure-hub"></a>Настройка концентратора уведомлений</span><span class="sxs-lookup"><span data-stu-id="250b6-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="250b6-114"><a id="register"></a>Включение Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="250b6-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="250b6-115">Настройка Azure toosend принудительной запросов</span><span class="sxs-lookup"><span data-stu-id="250b6-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="250b6-116"><a id="update-server"></a>Обновить hello server проекта toosend push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="250b6-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="250b6-117"><a id="configure-app"></a>Настройка проекта клиента hello push-уведомления</span><span class="sxs-lookup"><span data-stu-id="250b6-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="250b6-118"><a id="add-push"></a>Добавление кода tooyour принудительной уведомлений приложения</span><span class="sxs-lookup"><span data-stu-id="250b6-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="250b6-119"><a name="test"></a>Тестирование push-уведомлений в приложении</span><span class="sxs-lookup"><span data-stu-id="250b6-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="250b6-120">Приложение hello можно проверить с помощью виртуального устройства в эмуляторе hello.</span><span class="sxs-lookup"><span data-stu-id="250b6-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="250b6-121">Для запуска в эмуляторе необходимо выполнить дополнительную настройку.</span><span class="sxs-lookup"><span data-stu-id="250b6-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="250b6-122">Убедитесь в том, чтобы развертывание tooor отладку на виртуальное устройство с API-интерфейсы Google задать в качестве цели hello, как показано ниже в диспетчере hello виртуального устройства Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="250b6-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="250b6-123">Добавить устройство Android toohello учетной записи Google, щелкнув **приложения** > **параметры** > **добавьте учетную запись**, следуйте указаниям hello.</span><span class="sxs-lookup"><span data-stu-id="250b6-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="250b6-124">Запустите приложение hello todolist как перед и вставить новый элемент todo.</span><span class="sxs-lookup"><span data-stu-id="250b6-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="250b6-125">На этот раз значок уведомления отображается в области уведомлений hello.</span><span class="sxs-lookup"><span data-stu-id="250b6-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="250b6-126">Вы можете открыть hello уведомления лоток tooview hello полный текст hello уведомления.</span><span class="sxs-lookup"><span data-stu-id="250b6-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
