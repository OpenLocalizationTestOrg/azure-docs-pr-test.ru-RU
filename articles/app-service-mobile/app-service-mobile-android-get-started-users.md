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
# <a name="add-authentication-tooyour-android-app"></a>Добавить приложение Android tooyour проверки подлинности
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Сводка
В этом учебнике добавлении проверки подлинности toohello todolist быстрый запуск проекта в Android с помощью поставщика удостоверений, поддерживаемых. Этот учебник основывается на hello [начало работы с мобильным приложениям] руководство, в котором необходимо выполнять первой.

## <a name="register"></a>Регистрация приложения для аутентификации и настройка службы приложений Azure
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Добавить ваш URL-адреса внешнего перенаправления разрешено toohello для приложений

Для безопасной аутентификации требуется определить новую схему URL-адресов для своего приложения. Это позволяет приложение hello проверки подлинности системы tooredirect задней tooyour после завершения процесса проверки подлинности hello. В этом учебнике мы используем схема URL-адресов hello _appname_ на протяжении. Тем не менее можно использовать любую схему URL-адресов на свой выбор. Он должен быть уникальным tooyour мобильного приложения. tooenable hello перенаправления на стороне сервера hello:

1. В hello [Azure портал] выберите приложение службы.

2. Нажмите кнопку hello **проверки подлинности и авторизации** пункт меню.

3. В hello **допускается внешний URL-адреса перенаправления**, введите `appname://easyauth.callback`.  Hello _appname_ в данной строке — hello схема URL-адресов для мобильного приложения.  Она должна соответствовать обычной спецификации URL-адресов для протокола (можно использовать буквы и цифры, и адрес должен начинаться с буквы).  Необходимо записать строку hello, выбранный как он потребуется tooadjust кода приложений для мобильных устройств с hello схема URL-адресов в нескольких местах.

4. Нажмите кнопку **ОК**.

5. Щелкните **Сохранить**.

## <a name="permissions"></a>Ограничить разрешения пользователей tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

* В Android Studio откройте проект hello, вы выполнили учебнику hello [начало работы с мобильным приложениям]. Из hello **запуска** меню, нажмите кнопку **запуск приложения**и убедитесь, что возникает необработанное исключение с кодом состояния 401 (не санкционировано) после запуска приложение hello.

     Это исключение возникает из-за попытки приложения hello tooaccess hello обратно закончить без проверки подлинности пользователя, но hello *TodoItem* таблица теперь требует проверки подлинности.

Затем пользователи tooauthenticate приложения hello обновить перед запросом ресурсы из приветствия завершить обратно мобильные приложения. 

## <a name="add-authentication-toohello-app"></a>Добавить приложение toohello проверки подлинности
[!INCLUDE [mobile-android-authenticate-app](../../includes/mobile-android-authenticate-app.md)]



## <a name="cache-tokens"></a>Кэшировать маркеры проверки подлинности на приветствия клиента
[!INCLUDE [mobile-android-authenticate-app-with-token](../../includes/mobile-android-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Дальнейшие действия
Завершения этого учебника обычной проверки подлинности, рассмотрите возможность продолжить на tooone из hello следующие учебники:

* [Добавить приложение Android tooyour уведомлений push](app-service-mobile-android-get-started-push.md).
  Узнайте, tooconfigure обратно на мобильные приложения конечного toouse уведомление Azure концентраторов toosend push-уведомлений.
* [Включение автономной синхронизации для приложения Android](app-service-mobile-android-get-started-offline-data.md).
  Узнайте, как tooadd в автономном режиме поддерживают tooyour приложения с помощью серверной части мобильных приложений. Автономная синхронизация позволяет пользователям взаимодействовать с мобильным приложением (&mdash;просматривать, добавлять или изменять данные&mdash;) даже при отсутствии подключения к сети.

<!-- Anchors. -->
[Register your app for authentication and configure Mobile Services]: #register
[Restrict table permissions tooauthenticated users]: #permissions
[Add authentication toohello app]: #add-authentication
[Store authentication tokens on hello client]: #cache-tokens
[Refresh expired tokens]: #refresh-tokens
[Next Steps]:#next-steps


<!-- URLs. -->
[начало работы с мобильным приложениям]: app-service-mobile-android-get-started.md
