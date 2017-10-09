---
title: "Проверка подлинности учетной записи Майкрософт tooconfigure aaaHow для приложения службы приложений"
description: "Узнайте, как проверка подлинности учетной записи Майкрософт tooconfigure для приложения службы приложений."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>Как tooconfigure имя входа учетной записи Майкрософт toouse приложения служб приложений
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

В этом разделе показано, как службы приложений Azure tooconfigure toouse учетную запись Майкрософт как поставщик проверки подлинности. 

## <a name="register-microsoft-account"> </a>Регистрация приложения с использованием учетной записи Майкрософт
1. Войдите на toohello [портал Azure]и перейдите tooyour приложения. Копировать вашей **URL-адрес**, который впоследствии используется tooconfigure приложения с учетной записью Майкрософт.
2. Перейдите toohello [Мои приложения] в hello Центр разработчиков учетной записи Майкрософт и войдите с учетной записью Майкрософт, при необходимости.
3. Щелкните **Добавить приложение**, введите имя приложения и нажмите кнопку **Создать приложение**.
4. Запишите hello **идентификатор приложения**, как он понадобится позже. 
5. В разделе "Платформы" щелкните **Добавить платформу** и выберите "Интернет".
6. Под «URI перенаправления» конечной hello питания для приложения, нажмите кнопку **Сохранить**. 
   
   > [!NOTE]
   > Ваш перенаправления URI является hello URL-адрес приложения дополненная путь hello */.auth/login/microsoftaccount/callback*. Например, `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Убедитесь, что вы используете hello схему HTTPS.
   
7. В разделе "Секреты приложения" щелкните **Создать новый пароль**. Запишите значение hello, которое появляется. Когда вы покинете страницу приветствия, он больше не будет отображаться.

    > [!IMPORTANT]
    > пароль Hello — важный элемент обеспечения безопасности. Не делитесь hello пароль с кем и не распространяйте в клиентском приложении.

## <a name="secrets"></a>Tooyour добавьте учетную запись Майкрософт сведения приложения служб приложений
1. В hello [портал Azure], перейдите в приложение tooyour, щелкните **параметры** > **проверки подлинности и авторизации**.
2. Если hello проверки подлинности и авторизации не включена, включите ее **на**.
3. Щелкните **учетную запись Майкрософт**. Вставьте в значениях идентификатора приложения и пароль hello, что был получен и при необходимости включить любые области, которые требуются приложению. Нажмите кнопку **ОК**.
   
    ![][1]
   
    По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы. Авторизация пользователей должна быть включена в код приложения.
4. (Необязательно) toorestrict доступа tooyour сайта tooonly пользователь проверку подлинности с учетной записью Майкрософт, установить **tootake действия, если запрос не прошел проверку подлинности** слишком**учетную запись Майкрософт**. Это требует проверку подлинности всех запросов, и все запросы, не прошедшие проверку подлинности, перенаправляются tooMicrosoft учетной записи для проверки подлинности.
5. Щелкните **Сохранить**.

Теперь вы находитесь готов toouse учетную запись Майкрософт для проверки подлинности в приложении.

## <a name="related-content"> </a>Связанная информация
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[Мои приложения]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[портал Azure]: https://portal.azure.com/
