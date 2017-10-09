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
# <a name="add-push-notifications-tooyour-android-app"></a>Добавить приложение Android tooyour уведомлений push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Обзор
В этом учебнике добавить push уведомления toohello [краткое руководство по Android] проекта, чтобы каждый раз при вставке записи push-уведомление отправляется toohello устройства.

Если вы не используете hello загружен быстрый запуск сервера проекта, требуется hello пакета расширения уведомлений push. Дополнительные сведения см. в разделе [работать с сервера базы данных hello .NET SDK для мобильных приложений Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Предварительные требования
Требуется hello следующее:

* Интегрированная среда разработки, в зависимости от серверной части вашего проекта:

  * [Android Studio](https://developer.android.com/sdk/index.html) — если это приложение имеет серверную часть Node.js.
  * [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) или более поздняя версия — если это приложение имеет серверную часть Microsoft .NET.
* Android 2.3 или более поздняя версия, репозиторий Google версии 27 или более поздняя версия и службы Google Play 9.0.2 или более поздняя версия для Firebase Cloud Messaging.
* Полный hello [краткое руководство по Android].

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Создание проекта с поддержкой Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>Настройка центра уведомлений
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Настройка Azure toosend push-уведомлений
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>Включить push-уведомления для проекта сервера hello
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>Добавить приложение tooyour уведомлений push
В этом разделе обновить ваш клиент приложения Android toohandle push-уведомлений.

### <a name="verify-android-sdk-version"></a>Проверка версии пакета SDK для Android
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

Следующим шагом является tooinstall служб Google Play. Google Cloud Messaging имеет некоторые минимальные требования уровня API для разработки и тестирования, какие hello **minSdkVersion** должно соответствовать свойству в манифесте hello.

Если вы тестируете с старое устройство, обратитесь к [задайте копии Google воспроизведения пакета SDK служб] toodetermine малых это значение и настроить ее соответствующим образом.

### <a name="add-google-play-services-toohello-project"></a>Добавление проекта toohello служб Google Play
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>Добавление кода
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>Тестовое приложение hello от hello публикации мобильной службы
Вы можете протестировать приложение hello, присоединив телефоне с Android с помощью кабеля USB непосредственно или с помощью виртуального устройства в эмуляторе hello.

## <a name="next-steps"></a>Дальнейшие действия
Завершения этого учебника рекомендуется продолжить на tooone из hello следующие учебники:

* [Добавить приложение Android tooyour проверки подлинности](app-service-mobile-android-get-started-users.md).
  Узнайте, как проект quickstart todolist toohello проверки подлинности tooadd на Android с помощью поставщика удостоверений, поддерживаемых.
* [Включение автономной синхронизации для приложения Android](app-service-mobile-android-get-started-offline-data.md).
  Узнайте, как tooadd в автономном режиме поддерживают tooyour приложения с помощью серверной части мобильных приложений. Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением (&mdash;просматривать, добавлять или изменять данные&mdash;) даже при отсутствии подключения к сети.

<!-- URLs -->
[краткое руководство по Android]: app-service-mobile-android-get-started.md

[задайте копии Google воспроизведения пакета SDK служб]:https://developers.google.com/android/guides/setup
