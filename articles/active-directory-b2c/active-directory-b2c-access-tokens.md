---
title: "Azure Active Directory B2C: запрос маркеров доступа | Документация Майкрософт"
description: "В этой статье будет показано, как toosetup клиентского приложения и получить маркер доступа."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C: запрос маркеров доступа

Маркер доступа (обозначается как **доступа\_маркера** в ответах hello из Azure AD B2C) представляет собой форму маркера безопасности, который клиент может использовать ресурсы tooaccess, защищенные [сервер авторизации](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), например веб-API. Маркеры доступа представлены в виде [JWT](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) и содержит информацию о hello предполагаемого ресурсов сервера и сервера toohello разрешения, предоставленные hello. При вызове hello ресурсов сервера hello токена доступа должен присутствовать в hello HTTP-запроса.

В этой статье описывается, как tooconfigure клиентского приложения и веб-API в порядок tooobtain **доступа\_маркера**.

> [!NOTE]
> **Цепочки веб-API ("от имени") не поддерживаются в Azure AD B2C.**
>
> Многие архитектуры включают веб-API, который должен toocall другой нисходящий веб-API, оба защищен Azure AD B2C. Этот сценарий характерен в собственных клиентов, имеющих серверной части веб-API, который в свою очередь вызывает интерактивным службам Майкрософт, например hello API Azure AD Graph.
>
> Этот сценарий цепочек веб-API может поддерживаться с помощью hello grant OAuth 2.0 JWT носителя, учетных данных, в противном случае называется hello от имени представляет потока. Однако hello от имени представляет поток еще не реализован в Azure AD B2C.

## <a name="register-a-web-api-and-publish-permissions"></a>Регистрация веб-API и публикация разрешений

Прежде чем запросить маркер доступа, сначала необходимо tooregister веб-API и опубликуйте разрешений (областей), которые могут быть предоставлены toohello клиентское приложение.

### <a name="register-a-web-api"></a>Регистрация веб-API

1. В колонке функции hello B2C на hello портал Azure, щелкните **приложений**.
1. Нажмите кнопку **+ добавить** hello верхней части колонки hello.
1. Введите **имя** для приложения hello, где описан tooconsumers вашего приложения. Например, введите Contoso API.
1. Переключить hello **включают веб-приложения или веб-API** переключения слишком**Да**.
1. Введите произвольное значение для hello **URL-адреса ответа**. Например, введите `https://localhost:44316/`. значение Hello не имеет значения, так как API должен не получать токен hello непосредственно из Azure AD B2C.
1. Введите **URI идентификатора приложения**. Это идентификатор hello, используемый для веб-API. Например введите «примечания» в поле hello. Hello **URI идентификатора приложения** будут `https://{tenantName}.onmicrosoft.com/notes`.
1. Нажмите кнопку **создать** tooregister приложения.
1. Выберите приложение hello, которое вы только что создали и копировать hello глобальный уникальный **идентификатор клиента приложения** , который будет использоваться в коде.

### <a name="publishing-permissions"></a>Публикация разрешений

Области, которые являются аналогом toopermissions, необходимы в том случае, если приложение вызывает API-Интерфейс. Примеры областей — области чтения или записи. Предположим, что требуется веб-приложения или собственное приложение слишком «чтение» из API. Приложение будет вызывать Azure AD B2C и запрос, маркер доступа, который предоставляет область toohello доступа «чтение». Для Azure AD B2C tooemit такой маркер доступа, приложение hello должен toobe предоставлено разрешение слишком «чтение» из конкретного API hello. toodo, область действия «чтение» hello toopublish сначала нужен API.

1. В Azure AD B2C hello **приложений** колонке Привет открыть веб-API («API Contoso»).
1. Щелкните **Опубликованные области**. Это поле определяется hello разрешений (областей), которые могут быть предоставлены tooother приложений.
1. При необходимости добавьте **значения области** (например, read). По умолчанию будут определены области «user_impersonation» hello. Их можно игнорировать. Введите описание области hello hello **имя области** столбца.
1. Щелкните **Сохранить**.

> [!IMPORTANT]
> Hello **имя области** — описание hello hello **значение области**. При использовании области hello, убедитесь, что hello toouse **значение области**.

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a>Предоставление собственного или веб-приложения разрешения tooa веб-API

После API настроенных toopublish областей, hello клиентскому приложению требуется toobe предоставлены через портал Azure hello этих областей.

1. Перейдите toohello **приложений** меню в колонке функции hello B2C.
1. Зарегистрируйте клиентское приложение ([веб-приложение](active-directory-b2c-app-registration.md#register-a-web-app) или [собственный клиент](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)), если у вас еще его нет. Если вы следуете в этом руководстве в качестве отправной точки, вам потребуется tooregister клиентское приложение.
1. Щелкните **Доступ через API**.
1. Щелкните **Добавить**.
1. Выберите свои web API и hello области хотелось бы toogrant (разрешения).
1. Нажмите кнопку **ОК**.

> [!NOTE]
> Для Azure AD B2C не нужно предоставлять согласие пользователей клиентского приложения. Вместо этого все разрешения предоставляются Здравствуйте, администратор, на основе разрешений hello между приложения hello, описанных выше. При запрете разрешений, предоставленных для приложения всех пользователей, которые были ранее может tooacquire этого разрешения перестанет быть toodo может поэтому.

## <a name="requesting-a-token"></a>Запрос маркера

При запросе маркера доступа, клиентское приложение hello требуются разрешения hello требуемого toospecify в hello **область** параметр hello. Например, hello toospecify **значение области** «чтение» для интерфейса API с hello hello **URI идентификатора приложения** из `https://contoso.onmicrosoft.com/notes`, hello области будет `https://contoso.onmicrosoft.com/notes/read`. Ниже приведен пример toohello запрос кода авторизации `/authorize` конечной точки.

> [!NOTE]
> Сейчас пользовательские домены и маркеры доступа не поддерживаются. Необходимо использовать домен tenantName.onmicrosoft.com в URL-адрес запроса hello.

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

tooacquire нескольких разрешений в hello же запрос, можно добавить несколько записей в одном hello **область** параметров, разделенных пробелами. Например:

Декодированный URL-адрес:

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

Закодированный URL-адрес:

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

Для ресурса можно запросить больше областей или разрешений, чем предоставлено для клиентского приложения. В этом случае hello hello вызов будет успешным, если хотя бы одно разрешение. Полученный Hello **доступа\_маркера** будет иметь его утверждение «scp» заполненный только hello разрешения, которые были успешно предоставлены.

> [!NOTE] 
> Мы не поддерживаем запроса разрешений для двух разных web ресурсов hello того же запроса. Такой запрос завершится ошибкой.

### <a name="special-cases"></a>Особые случаи

OpenID Connect Стандартная Hello указывает несколько значений специальные «scope». Здравствуйте, слишком следующие специальные области представляют Привет разрешение «доступ к профилю пользователя hello»:

* **openid** — запрашивает маркер идентификатора;
* **offline\_access** — запрашивает маркер обновления (с помощью [потоков кода аутентификации](active-directory-b2c-reference-oauth-code.md)).

Если hello `response_type` параметр в `/authorize` запрос включает `token`, hello `scope` параметр должен содержать хотя бы один ресурс область (отличного от `openid` и `offline_access`), будут предоставлены. В противном случае hello `/authorize` запрос будет завершена с ошибкой.

## <a name="hello-returned-token"></a>Hello вернул токен

В успешно созданный **доступа\_маркера** (из либо hello `/authorize` или `/token` конечной точки), hello следующих утверждений будет присутствовать:

| Имя | Утверждение | Описание |
| --- | --- | --- |
|Аудитория |`aud` |Hello **идентификатор приложения** hello одного ресурса, hello маркер предоставляет доступ к. |
|Область |`scp` |Hello разрешения toohello ресурсов. Несколько предоставленных разрешений разделяются пробелами. |
|Авторизованная сторона |`azp` |Hello **идентификатор приложения** hello клиентского приложения, инициировавшего запрос hello. |

При получении hello в API **доступа\_маркера**, он должен [проверка токена hello](active-directory-b2c-reference-tokens.md) tooprove, hello маркера подлинность и имеет правильные утверждений hello.

Мы всегда являются предложения и откройте toofeedback! Если возникли проблемы с этим разделом, опубликуйте о переполнении стека с помощью тега hello в [«azure ad b2c»](https://stackoverflow.com/questions/tagged/azure-ad-b2c). Для запросов, компонент, добавьте их слишком[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

## <a name="next-steps"></a>Дальнейшие действия

* Создайте веб-API с помощью [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi).
* Создайте веб-API с помощью [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi).
