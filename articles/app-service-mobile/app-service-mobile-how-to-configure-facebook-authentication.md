---
title: "aaaHow tooconfigure Facebook и проверки подлинности для приложения службы приложений"
description: "Узнайте, как tooconfigure проверки подлинности Facebook для приложения службы приложений."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>Как tooconfigure имени входа Facebook toouse приложения служб приложений
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

В этом разделе показано, как службы приложений Azure tooconfigure toouse Facebook в качестве поставщика проверки подлинности.

toocomplete hello процедуры в этом разделе, необходимо иметь учетную запись Facebook с проверенной адрес и номер мобильного телефона. toocreate новую учетную запись Facebook go слишком[facebook.com].

## <a name="register"> </a>Регистрация приложения с помощью Facebook
1. Войдите на toohello [портал Azure]и перейдите tooyour приложения. Скопируйте свой **URL-адрес**. Вы воспользуетесь этой tooconfigure приложения Facebook.
2. В другом окне браузера перейдите toohello [разработчиков в Facebook] веб-сайта и войдите в ваш Facebook учетные данные учетной записи.
3. (Необязательно) Если вы уже не зарегистрировались, щелкните **приложения** > **зарегистрировать как разработчик**, примите политику hello и выполните действия по регистрации hello.
4. Щелкните **Мои приложения** > **Add a New App** (Добавить новое приложение) > **Веб-сайт** > **Skip and Create App ID** (Пропустить и создать идентификатор приложения). 
5. В **отображаемое имя**, введите уникальное имя для вашего приложения, тип вашей **адрес электронной почты**, выберите **категории** приложение и нажмите кнопку **создать идентификатор приложения**и выполнить проверку безопасности hello. Откроется панель toohello разработчика для нового приложения Facebook.
6. В разделе Facebook Login (Вход в Facebook) щелкните **Get Started**(Начать). Добавление приложения **URI перенаправления** слишком**OAuth допустимый URI перенаправления**, нажмите кнопку **сохранить изменения**. 
   
   > [!NOTE]
   > Ваш перенаправления URI является hello URL-адрес приложения дополненная путь hello */.auth/login/facebook/callback*. Например, `https://contoso.azurewebsites.net/.auth/login/facebook/callback`. Убедитесь, что вы используете hello схему HTTPS.
   > 
   > 
7. В левой области навигации hello щелкните **параметры**. На hello **секрет приложения** щелкните **Показать**, предоставить свой пароль, если в запросе, а затем запишите значения hello **идентификатор приложения** и **секрет приложения**. Использования этих более поздних tooconfigure приложения в Azure.
   
   > [!IMPORTANT]
   > секрет приложения Hello — важный элемент обеспечения безопасности. Не сообщайте этот секрет никому и не раскрывайте его в клиентском приложении.
   > 
   > 
8. Hello Facebook учетной записи, которая была используется tooregister приложения hello не является администратором приложения hello. На этом этапе только администраторы могут входить в приложение. tooauthenticate другие учетные записи Facebook, нажмите кнопку **проверки приложения** и включить **марка < your app-name > public** tooenable общие общего доступа с помощью проверки подлинности Facebook.

## <a name="secrets"></a>Tooyour приложения Facebook, добавить сведения
1. Вернитесь в hello [портал Azure], перейдите tooyour приложения. Щелкните **Параметры** > **Аутентификация или авторизация** и установите для параметра **Проверка подлинности службы приложений** значение **Вкл**.
2. Нажмите кнопку **Facebook**, вставьте в значениях идентификатор приложения и секрет приложения hello, что был получен, при необходимости включить любые области, необходимые для приложения, а затем нажмите кнопку **ОК**.
   
    ![][0]
   
    По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы. Авторизация пользователей должна быть включена в код приложения.
3. (Необязательно) toorestrict доступа tooyour сайта tooonly пользователи аутентифицироваться Facebook, задать **tootake действия, если запрос не прошел проверку подлинности** слишком**Facebook**. Это требует проверку подлинности всех запросов, и все запросы без проверки подлинности, перенаправленный tooFacebook для проверки подлинности.
4. Завершив настройку аутентификации, нажмите кнопку **Сохранить**.

Теперь вы находитесь готов toouse Facebook для проверки подлинности в приложении.

## <a name="related-content"> </a>Связанная информация
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[разработчиков в Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[портал Azure]: https://portal.azure.com/
