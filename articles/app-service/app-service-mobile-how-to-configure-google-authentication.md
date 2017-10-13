---
title: "Настройка проверки подлинности Google для приложения служб приложений"
description: "Настройка проверки подлинности Google для приложения служб приложений."
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
ms.openlocfilehash: d6c1707f67d986487e5a45e76ffc9a02ddf16eb1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-your-app-service-application-to-use-google-login"></a>Как настроить приложение службы приложений для использования имени для входа Google
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

В этом разделе показано, как настроить службу приложений Azure для использования Google в качестве поставщика проверки подлинности.

Чтобы выполнить процедуру, описанную в этом разделе, необходимо иметь учетную запись Google с проверенным адресом электронной почты. Чтобы создать новую учетную запись Google, перейдите по ссылке [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).

## <a name="register"> </a>Регистрация приложения с помощью Google
1. Войдите на [портал Azure]и перейдите к своему приложению. Скопируйте **URL-адрес**, который вы будете использовать позже для настройки приложения Google.
2. Перейдите на веб-сайт [Google apis](http://go.microsoft.com/fwlink/p/?LinkId=268303), войдите с помощью учетных данных Google, выберите команду **Создать проект**, укажите имя проекта в поле **Название проекта**, а затем нажмите кнопку **Создать**.
3. В разделе **Social APIs** (Интерфейсы API для соцсетей) щелкните **Google + API**, а затем — **Включить**.
4. В области навигации слева выберите **Учетные данные** > **OAuth consent screen** (Экран согласия OAuth), выберите свой **адрес электронной почты**, введите **имя продукта** и щелкните **Сохранить**.
5. На вкладке **Учетные данные** щелкните **Create credentials** (Создать учетные данные) > **Идентификатор клиента OAuth**, а затем выберите **Веб-приложение**.
6. Вставьте скопированный ранее **URL-адрес** службы приложений в поле **Authorized JavaScript Origins** (Разрешенные источники JavaScript) и вставьте универсальный код ресурса (URI) перенаправления в поле **Authorized Redirect URI** (Разрешенный код URI перенаправления). Универсальный код ресурса (URI) перенаправления — это URL-адрес приложения, дополненный путем */.auth/login/google/callback*. Например, `https://contoso.azurewebsites.net/.auth/login/google/callback`. Убедитесь, что используете схему HTTPS. Затем щелкните **Создать**.
7. На следующем экране запишите идентификатор клиента и секрет клиента.

    > [!IMPORTANT]
    > Секрет клиента — это важные учетные данные безопасности. Не сообщайте этот секрет никому и не раскрывайте его в клиентском приложении.


## <a name="secrets"> </a>Добавление данных Google в приложение
1. Снова вернитесь на [портал Azure]и перейдите к своему приложению. Щелкните **Параметры**, а затем — **Проверка подлинности или авторизация**.
2. Если функция аутентификации или авторизации не включена, установите переключатель в положение **Вкл**.
3. Щелкните **Google**. Вставьте значения идентификатора и секретного кода приложения, полученные ранее, и, при необходимости, включите любые области, которые требуются приложению. Нажмите кнопку **ОК**.
   
   ![][1]
   
   По умолчанию служба приложений обеспечивает проверку подлинности, но не ограничивает авторизованный доступ к содержимому сайта и API. Авторизация пользователей должна быть включена в код приложения.
4. (Необязательно.) Чтобы предоставить доступ к сайту только пользователям, прошедшим проверку подлинности в Google, установите для параметра **Предпринимаемое действие, если проверка подлинности для запроса не выполнена** значение **Google**. В этом случае все запросы, не прошедшие проверку подлинности, направляются для проверки подлинности с помощью Google.
5. Щелкните **Сохранить**.

Теперь вы готовы использовать Google для проверки подлинности в приложении.

## <a name="related-content"> </a>Связанная информация
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Anchors. -->

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-google-authentication/mobile-app-google-settings.png

<!-- URLs. -->

[Google apis]: http://go.microsoft.com/fwlink/p/?LinkId=268303

[портал Azure]: https://portal.azure.com/

