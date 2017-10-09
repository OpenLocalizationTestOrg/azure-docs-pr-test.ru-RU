---
title: "Azure Active Directory B2C: регистрация приложения | Документация Майкрософт"
description: "Как tooregister приложения с Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C: регистрация приложения

Из этого краткого руководства вы узнаете, как зарегистрировать приложение в клиенте Microsoft Azure Active Directory (Azure AD) B2C за несколько минут. После завершения приложение регистрируется для использования в клиенте hello Azure B2C.

## <a name="prerequisites"></a>Предварительные требования

toobuild приложения, которое принимает потребителя регистрации и входе в систему, необходимо сначала приложения hello tooregister с клиентом Azure Active Directory B2C. Получение вашего собственного клиента с помощью hello действия, описанные в [создание клиента Azure AD B2C](active-directory-b2c-get-started.md).

Приложения, созданные из колонки hello Azure AD B2C в hello портал Azure, должна управляться из hello местоположения. При редактировании hello B2C приложений с помощью PowerShell или другого портала становятся не поддерживается и не работают с Azure AD B2C. Просмотреть сведения в hello [произошел сбой приложения](#faulted-apps) раздела. 

## <a name="navigate-toob2c-settings"></a>Параметры tooB2C перехода

Войдите в toohello [портал Azure](https://portal.azure.com/) как глобальный администратор клиента hello B2C hello. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

Выбор следующего действия в зависимости от типа приложения hello, регистрируемая:

* [регистрация веб-приложения;](#register-a-web-app)
* [регистрация веб-API;](#register-a-web-api)
* [регистрация мобильного или собственного приложения.](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>Регистрация веб-приложения

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

Если веб-приложение вызовет веб-API, защищенный Azure AD B2C, выполните следующие действия.
   1. Создать секрет приложения с переходом toohello **ключей** колонки и щелкнув hello **создать ключ** кнопки. Запишите hello **ключ приложения** значение. Значение hello используется секрет приложения hello в код приложения.
   2. Щелкните **Доступ через API**, **Добавить** и выберите свой веб-API и области (разрешения).

> [!NOTE]
> **Секрет приложения** — это важные учетные данные безопасности, которые должны быть надежно защищены.
> 

[Переход слишком**дальнейшие действия**](#next-steps)

## <a name="register-a-web-api"></a>Регистрация веб-API

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

Нажмите кнопку **публикации областей** tooadd более областей при необходимости. По умолчанию определяется областью «user_impersonation» hello. областью user_impersonation Hello дает tooaccess возможность hello других приложений этот api от имени пользователя, выполнившего вход hello. При желании можно удалить областью user_impersonation hello.

[Переход слишком**дальнейшие действия**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>Регистрация мобильного или собственного приложения

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[Переход слишком**дальнейшие действия**](#next-steps)

## <a name="limitations"></a>Ограничения

### <a name="choosing-a-web-app-or-api-reply-url"></a>Выбор URL-адреса ответа для веб-приложения или API

В настоящее время приложения, которые зарегистрированы в Azure AD B2C являются ограниченными tooa ограниченный набор значений URL-адрес ответа. Здравствуйте, URL-адрес для веб-приложений и служб должны начинаться со схемой hello ответ `https`, и всех ответов значений URL-адреса должны совместно использовать одного домена DNS. Например, невозможно зарегистрировать веб-приложение с одним из следующих URL-адресов ответа:

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Система регистрации Hello сравнивает hello всей DNS-имя hello существующего ответа URL-адрес toohello DNS-имя URL-адреса hello ответа, который добавляется. hello tooadd Hello запрос DNS-имя завершается ошибкой, если выполняется любое из следующих условий hello:

* Hello всей DNS-имя hello новый URL-адрес ответа не соответствует DNS-имя hello hello существующий URL-адреса ответа.
* всего DNS-имя Hello hello новый URL-адреса ответа не поддомен hello существующий URL-адреса ответа.

Например если hello приложение имеет этот URL-адрес ответа:

`https://login.contoso.com`

Можно добавить tooit следующим образом:

`https://login.contoso.com/new`

В этом случае hello DNS-имя соответствует точно. Или же можно сделать следующее.

`https://new.login.contoso.com`

В этом случае ссылка поддомен login.contoso.com tooa DNS. Если вы хотите toohave входа east.contoso.com и west.contoso.com входа как URL-адреса ответа приложения, необходимо добавить эти URL-адреса ответа в указанном порядке:

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Можно добавить hello последние две, поскольку они являются поддомены hello первого URL-адреса ответа, contoso.com.

### <a name="choosing-a-native-app-redirect-uri"></a>Выбор URI перенаправления для собственного приложения

При выборе URI перенаправления для мобильных и собственных приложений нужно учитывать два важных момента:

* **Уникальный**: hello схема URI перенаправления hello должно быть уникальным для каждого приложения. В нашем примере (com.onmicrosoft.contoso.appname://redirect/path) мы используем com.onmicrosoft.contoso.appname как схему hello. Рекомендуется следовать этому шаблону. Если два приложения имеют hello же схемы, hello пользователь видит диалоговое окно «Выбор приложений». Если пользователь hello вносит неправильному выбору, вход hello не выполняется.
* **Полнота**. URI перенаправления должен иметь схему и путь. Hello путь должен содержать по крайней мере одного знака косой черты после hello домена (например, //contoso/ работает и //contoso завершается с ошибкой).

Убедитесь, что никакие специальные символы, как символ подчеркивания в hello uri перенаправления.

### <a name="faulted-apps"></a>Неисправные приложения

Не следует вносить изменения в приложения B2C:

* с помощью других порталов для управления приложениями, таких как [классический портал Azure](https://manage.windowsazure.com/) и [портал регистрации приложений](https://apps.dev.microsoft.com/);
* с помощью API Graph или PowerShell.

Если изменить приложение hello B2C, как описано выше и повторите tooedit его снова в колонке функции hello Azure AD B2C на hello портал Azure, становится неисправной приложения и приложения больше не может использоваться с Azure AD B2C. Приложение hello toodelete и создайте его заново.

приложение hello toodelete, последовательно выберите toohello [портала регистрации приложения](https://apps.dev.microsoft.com/) и удалить приложение hello. Чтобы toobe приложения hello видимым понадобится toobe hello владелец приложения hello (и не только администратор клиента hello).

## <a name="next-steps"></a>Дальнейшие действия

Теперь, когда приложение зарегистрировано в Azure AD B2C, выполните одно из [нашим руководствам краткое](active-directory-b2c-overview.md#get-started) tooget запуска.

> [!div class="nextstepaction"]
> [Azure AD B2C: регистрация и вход в систему в веб-приложении ASP.NET](active-directory-b2c-devquickstarts-web-dotnet-susi.md)