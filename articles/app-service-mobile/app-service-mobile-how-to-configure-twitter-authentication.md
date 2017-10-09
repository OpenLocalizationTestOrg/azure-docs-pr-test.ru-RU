---
title: "Проверка подлинности Twitter tooconfigure aaaHow для приложения службы приложений"
description: "Узнайте, как проверка подлинности Twitter tooconfigure для приложения службы приложений."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: c6dc91d7-30f6-448c-9f2d-8e91104cde73
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 0d16ac44d7b54e3567b793a904059d31ab1d8911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-twitter-login"></a>Как tooconfigure имя входа Twitter toouse приложения служб приложений
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

В этом разделе показано, как службы приложений Azure tooconfigure toouse Twitter, как поставщик проверки подлинности.

toocomplete hello процедуры в этом разделе, необходимо иметь учетную запись Twitter, имеющую проверенных электронной почты адрес и номер телефона. toocreate новую учетную запись Twitter, переход слишком<a href="http://go.microsoft.com/fwlink/p/?LinkID=268287" target="_blank">twitter.com</a>.

## <a name="register"> </a>Регистрация приложения в Twitter
1. Войдите на toohello [портал Azure]и перейдите tooyour приложения. Скопируйте свой **URL-адрес**. Вы воспользуетесь этой tooconfigure приложения Twitter.
2. Перейдите toohello [Twitter разработчики] веб-сайта, войдите, используя учетные данные учетной записи Twitter и нажмите кнопку **создать новое приложение**.
3. Тип в hello **имя** и **описание** для нового приложения. Вставить в вашем приложении **URL-адрес** для hello **веб-сайт** значение. Затем для hello **URL-адрес обратного вызова**, вставьте hello **URL-адрес обратного вызова** скопированное ранее. Это шлюз мобильного приложения, дополненная путь hello */.auth/login/twitter/callback*. Например, `https://contoso.azurewebsites.net/.auth/login/twitter/callback`. Убедитесь, что вы используете hello схему HTTPS.
4. На странице приветствия нижней hello прочтите и примите условия hello. Затем щелкните **Создать приложение Twitter**. Это приложение hello регистры отображает подробные сведения о приложении hello.
5. Нажмите кнопку hello **параметры** установите флажок **разрешить toosign toobe использовать это приложение с использованием Twitter**, нажмите кнопку **параметры обновления**.
6. Выберите hello **ключей и маркеры доступа** вкладки. Запомните значения hello **потребителя ключом (API)** и **секрет пользователя (секрет API)**.
   
   > [!NOTE]
   > секрет получателя Hello — важный элемент обеспечения безопасности. Не сообщайте никому этого секрета и не распространяйте его вместе с вашим приложением.
   > 
   > 

## <a name="secrets"></a>Добавить Twitter приложения tooyour сведения
1. Вернитесь в hello [портал Azure], перейдите tooyour приложения. Щелкните **Параметры**, а затем — **Проверка подлинности или авторизация**.
2. Если hello проверки подлинности и авторизации не включена, включать hello слишком**на**.
3. Щелкните **Twitter**. Значения, которые ранее полученный вставьте hello идентификатор приложения и секрет приложения. Нажмите кнопку **ОК**.
   
   ![][1]
   
   По умолчанию приложение службы обеспечивает проверку подлинности, но не ограничивает содержимого узла tooyour авторизованный доступ и API-интерфейсы. Авторизация пользователей должна быть включена в код приложения.
4. (Необязательно) toorestrict доступа tooyour сайта tooonly пользователь проверку подлинности Twitter, установить **tootake действия, если запрос не прошел проверку подлинности** слишком**Twitter**. Это требует проверку подлинности всех запросов, и все запросы без проверки подлинности, перенаправленный tooTwitter для проверки подлинности.
5. Щелкните **Сохранить**.

Теперь вы находитесь готов toouse Twitter для проверки подлинности в приложении.

## <a name="related-content"> </a>Связанная информация
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-twitter-authentication/app-service-twitter-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-twitter-authentication/mobile-app-twitter-settings.png

<!-- URLs. -->

[Twitter разработчики]: http://go.microsoft.com/fwlink/p/?LinkId=268300
[портал Azure]: https://portal.azure.com/
[xamarin]: ../app-services-mobile-app-xamarin-ios-get-started-users.md
