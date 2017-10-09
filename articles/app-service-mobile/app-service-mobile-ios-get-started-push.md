---
title: "aaaAdd tooiOS Push-уведомлений приложения с помощью мобильных приложений Azure"
description: "Узнайте, как toosend toouse мобильных приложений Azure push-уведомлений приложения iOS tooyour."
services: app-service\mobile
documentationcenter: ios
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: glenga
ms.openlocfilehash: 11588c56bc8987a71257dbad4fcdebf1b3209b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="9b2f9-103">Добавление приложения iOS tooyour Push-уведомления</span><span class="sxs-lookup"><span data-stu-id="9b2f9-103">Add Push Notifications tooyour iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="9b2f9-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9b2f9-104">Overview</span></span>
<span data-ttu-id="9b2f9-105">В этом учебнике добавить push уведомления toohello [iOS быстрый запуск] проекта, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.</span><span class="sxs-lookup"><span data-stu-id="9b2f9-105">In this tutorial, you add push notifications toohello [iOS quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="9b2f9-106">Если вы не используете hello загружен проект быстрый запуск сервера, будет необходимо hello пакета расширения уведомлений push.</span><span class="sxs-lookup"><span data-stu-id="9b2f9-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="9b2f9-107">В разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="9b2f9-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="9b2f9-108">Hello [симулятор iOS не поддерживает push-уведомления](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="9b2f9-108">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="9b2f9-109">Требуется физическое устройство iOS и [участие в программе для разработчиков на платформе Apple](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="9b2f9-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="9b2f9-110"><a name="configure-hub"></a>Настройка центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="9b2f9-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="9b2f9-111"><a id="register"></a>Регистрация приложения для работы с push-уведомлениями</span><span class="sxs-lookup"><span data-stu-id="9b2f9-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="9b2f9-112">Настройка Azure toosend push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="9b2f9-112">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="9b2f9-113"><a id="update-server"></a>Обновление серверной части toosend push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="9b2f9-113"><a id="update-server"></a>Update backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="9b2f9-114"><a id="add-push"></a>Добавление push tooapp уведомления</span><span class="sxs-lookup"><span data-stu-id="9b2f9-114"><a id="add-push"></a>Add push notifications tooapp</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="9b2f9-115"><a id="test"></a>Тестирование push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="9b2f9-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="9b2f9-116"><a id="more"></a>Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="9b2f9-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="9b2f9-117">Шаблоны обеспечивают гибкость toosend кросс платформенных Push-уведомлений, а также локализованные Push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="9b2f9-117">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="9b2f9-118">[Как tooUse iOS клиентскую библиотеку для мобильных приложений Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) показано, как шаблоны tooregister.</span><span class="sxs-lookup"><span data-stu-id="9b2f9-118">[How tooUse iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how tooregister templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS быстрый запуск]: app-service-mobile-ios-get-started.md
