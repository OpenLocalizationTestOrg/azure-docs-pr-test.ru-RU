---
title: "aaaHow tooconfigure Google и проверки подлинности для приложения службы приложений"
description: "Узнайте, как проверка подлинности Google tooconfigure для приложения службы приложений."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: 2b2f9abf-9120-4aac-ac5b-4a268d9b6e2b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 9175c40b78c859e9e191504c41cd0bb9a3380ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-google-login"></a>Как tooconfigure вход Google toouse приложения служб приложений
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

В этом разделе показано, как служба приложений Azure tooconfigure toouse Google в качестве поставщика проверки подлинности.

toocomplete hello процедуры в этом разделе, необходимо иметь учетную запись Google, имеющую проверенных адрес. toocreate новой учетной записи Google go слишком[accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"> </a>Регистрация приложения с помощью Google
1. Войдите на toohello [портал Azure]и перейдите tooyour приложения. Копировать вашей **URL-адрес**, который использовать более поздней версии tooconfigure приложение Google.
2. Перейдите toohello [Google API-интерфейсы](http://go.microsoft.com/fwlink/p/?LinkId=268303) веб-сайта, выполните вход с помощью учетных данных учетной записи Google, нажмите кнопку **Создание проекта**, предоставляют **имя проекта**, нажмите кнопку  **Создание**.
3. В разделе **Social APIs** (Интерфейсы API для соцсетей) щелкните **Google + API**, а затем — **Включить**.
4. В области навигации слева hello **учетные данные** > **экран согласия OAuth**, а затем выберите ваш **адрес электронной почты**, введите **название продукта**и нажмите кнопку **Сохранить**.
5. В hello **учетные данные** щелкните **создать учетные данные** > **идентификатор клиента OAuth**, а затем выберите **веб-приложение**.
6. Вставить hello службы приложений **URL-адрес** вы ранее копируется **Authorized JavaScript Origins**, вставьте вашей перенаправления URI в **авторизации URI перенаправления**. Здравствуйте перенаправления URI является hello URL-адрес приложения дополненная путь hello */.auth/login/google/callback*. Например, `https://contoso.azurewebsites.net/.auth/login/google/callback`. Убедитесь, что вы используете hello схему HTTPS. Затем щелкните **Создать**.
7. На следующем экране приветствия запишите значения hello клиента hello идентификатор и секрет клиента.

    > [!IMPORTANT]
    > Hello секрет клиента — важный элемент обеспечения безопасности. Не сообщайте этот секрет никому и не раскрывайте его в клиентском приложении.


## <a name="secrets"></a>Google, добавить сведения tooyour приложения
1. Вернитесь в hello [портал Azure], перейдите tooyour приложения. Щелкните **Параметры**, а затем — **Проверка подлинности или авторизация**.
2. Если hello проверки подлинности и авторизации не включена, включать hello слишком**на**.
3. Щелкните **Google**. Вставьте в значениях идентификатор приложения и секрет приложения hello, что был получен и при необходимости включить любые области, которые требуются приложению. Нажмите кнопку **ОК**.
   
   ![][1]
   
   По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы. Авторизация пользователей должна быть включена в код приложения.
4. (Необязательно) toorestrict доступа tooyour сайта tooonly пользователь проверку подлинности Google, установить **tootake действия, если запрос не прошел проверку подлинности** слишком**Google**. Это требует проверку подлинности всех запросов, и все запросы без проверки подлинности, перенаправленный tooGoogle для проверки подлинности.
5. Щелкните **Сохранить**.

Теперь вы находитесь готов toouse Google для проверки подлинности в приложении.

## <a name="related-content"> </a>Связанная информация
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[портал Azure]: https://portal.azure.com/

