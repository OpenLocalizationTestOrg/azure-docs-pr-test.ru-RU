---
title: "Добавление push-уведомлений в приложение iOS с помощью мобильных приложений Azure"
description: "Узнайте, как использовать мобильные приложения Azure для отправки push-уведомлений в приложение iOS."
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
ms.openlocfilehash: 08a8c35b89386bd0dbe7bba406a6985a5a0d7eb8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="0408b-103">Добавление push-уведомлений в приложение iOS</span><span class="sxs-lookup"><span data-stu-id="0408b-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="0408b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="0408b-104">Overview</span></span>
<span data-ttu-id="0408b-105">В этом руководстве мы добавим push-уведомления в проект [быстрому запуску iOS], чтобы при каждом добавлении новой записи на устройство отправлялось push-уведомление.</span><span class="sxs-lookup"><span data-stu-id="0408b-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="0408b-106">Если вы не используете скачанный проект сервера, вам потребуется добавить пакет расширений для push-уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0408b-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="0408b-107">Дополнительные сведения о пакетах расширений для сервера см. в статье [Работа с пакетом SDK для внутреннего сервера .NET для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="0408b-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="0408b-108">[Симулятор iOS не поддерживает push-уведомления](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="0408b-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="0408b-109">Требуется физическое устройство iOS и [участие в программе для разработчиков на платформе Apple](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="0408b-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="0408b-110"><a name="configure-hub"></a>Настройка центра уведомлений</span><span class="sxs-lookup"><span data-stu-id="0408b-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="0408b-111"><a id="register"></a>Регистрация приложения для работы с push-уведомлениями</span><span class="sxs-lookup"><span data-stu-id="0408b-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="0408b-112">Настройка Azure для отправки push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="0408b-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="0408b-113"><a id="update-server"></a>Обновление серверной части для отправки push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="0408b-113"><a id="update-server"></a>Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="0408b-114"><a id="add-push"></a>Добавление push-уведомлений в приложение</span><span class="sxs-lookup"><span data-stu-id="0408b-114"><a id="add-push"></a>Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="0408b-115"><a id="test"></a>Тестирование push-уведомлений</span><span class="sxs-lookup"><span data-stu-id="0408b-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="0408b-116"><a id="more"></a>Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="0408b-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="0408b-117">Шаблоны обеспечивают гибкость при отправке push-уведомлений локально и между различными платформами.</span><span class="sxs-lookup"><span data-stu-id="0408b-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="0408b-118">[Использование клиентской библиотеки iOS для мобильных приложений Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) описано, как регистрировать шаблоны.</span><span class="sxs-lookup"><span data-stu-id="0408b-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="0408b-119">[быстрому запуску iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="0408b-119">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>
