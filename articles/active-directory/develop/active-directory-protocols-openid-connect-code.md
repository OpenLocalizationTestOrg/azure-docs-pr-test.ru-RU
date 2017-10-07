---
title: "hello aaaUnderstand OpenID Connect потока кода проверки подлинности в Azure AD | Документы Microsoft"
description: "В этой статье описывается, как доступ к toouse HTTP сообщения tooauthorize tooweb приложений и веб-API в клиенте с помощью Azure Active Directory и OpenID Connect."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 29142f7e-d862-4076-9a1a-ecae5bcd9d9b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: fafd8ab906ee576c584fec2ef1e9de83ddb1f6e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Авторизация доступа tooweb приложений с использованием OpenID Connect и Azure Active Directory
[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) является уровень простой идентификации, построена на базе протокола hello OAuth 2.0. OAuth 2.0 определяет механизмы tooobtain и используйте **маркеры доступа** tooaccess защищенные ресурсы, но они не определяют стандартные методы tooprovide идентификационных данных. OpenID Connect реализует проверку подлинности как расширение toohello процесс авторизации OAuth 2.0. Предоставляет сведения о hello конечного пользователя в форме hello `id_token` , проверяет удостоверение пользователя, hello hello и предоставляет базовый профиль сведения о пользователе hello.

Мы рекомендуем использовать OpenID Connect для веб-приложений, которые размещаются на сервере и доступны через веб-браузер.


[!INCLUDE [active-directory-protocols-getting-started](../../../includes/active-directory-protocols-getting-started.md)] 

## Поток проверки подлинности при использовании OpenID Connect
Здравствуйте, самый простой поток вход содержит следующие шаги hello - каждого из них подробно описан ниже.

![Поток проверки подлинности OpenID Connect](media/active-directory-protocols-openid-connect-code/active-directory-oauth-code-flow-web-app.png)

## Документ метаданных OpenID Connect

OpenID Connect описывает документ метаданных, содержащая большую часть hello сведения, необходимые для приложения tooperform входа. Сюда входят сведения, например toouse hello URL-адреса и расположение hello открытые ключи подписи hello службы. документ метаданных OpenID Connect Hello можно найти по адресу:

```
https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration
```
Hello метаданные — это простой документ нотации объектов JavaScript (JSON). См. следующий фрагмент кода для пример hello. Hello содержимое фрагмента кода полностью описаны в hello [спецификация OpenID Connect](https://openid.net).

```
{
    "authorization_endpoint": "https://login.microsoftonline.com/common/oauth2/authorize",
    "token_endpoint": "https://login.microsoftonline.com/common/oauth2/token",
    "token_endpoint_auth_methods_supported":
    [
        "client_secret_post",
        "private_key_jwt"
    ],
    "jwks_uri": "https://login.microsoftonline.com/common/discovery/keys"
    
    ...
}
```

## Отправить запрос hello вход
Когда веб-приложение должно tooauthenticate пользователя hello и он должен направлять пользователя toohello hello `/authorize` конечной точки. Этот запрос создан как первый участок toohello из hello [потока кода авторизации OAuth 2.0](active-directory-protocols-oauth-code.md), с помощью нескольких важные различия:

* Hello запрос должен включать область hello `openid` в hello `scope` параметра.
* Hello `response_type` необходимо включить параметр `id_token`.
* Hello запрос должен включать hello `nonce` параметра.

Запрос в целом будет выглядеть примерно так.

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=7362CAEA-9CA5-4B43-9BA3-34D7C303EBA7
```

| Параметр |  | Описание |
| --- | --- | --- |
| tenant |обязательно |Hello `{tenant}` значение в путь hello hello запроса может быть используется toocontrol, которые можно выполнять вход в приложение hello.  Hello допустимые значения: идентификаторы клиента, например, `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` или `contoso.onmicrosoft.com` или `common` для маркеров, зависящие от клиента |
| client_id |обязательно |Идентификатор приложения назначенного tooyour приложение Hello при регистрации в Azure AD. Его можно найти в hello портала Azure. Нажмите кнопку **Azure Active Directory**, нажмите кнопку **регистрации приложения**, выберите приложение hello и найдите hello идентификатор приложения на странице приложения hello. |
| response_type |обязательно |Должен включать `id_token` для входа в OpenID Connect.  Параметр также может содержать другие типы response_types, например `code`. |
| scope |обязательно |Список областей с разделителями-пробелами.  OpenID Connect, он должен содержать область hello `openid`, что означает разрешение «Вход» toohello пользовательского интерфейса согласия hello.  Для предоставления разрешений этот запрос может также включать другие области. |
| nonce |обязательно |Значение, включенное в запрос hello, созданное приложение hello, входящую в возникающие hello `id_token` качестве утверждения.  приложение Hello можно затем удостоверьтесь, что атак воспроизведения токена значение toomitigate.  Hello значение обычно равно случайного уникальная строка или идентификатор GUID, который может быть используется tooidentify hello источник запроса hello. |
| redirect_uri |рекомендуется |Hello redirect_uri приложения, где запросы проверки подлинности можно отправленных и полученных приложения.  Он должен точно соответствовать одной redirect_uris hello, зарегистрированное в портале hello, за исключением того, он должен быть в кодировке URL-адрес. |
| response_mode |рекомендуется |Задает метод должен быть используется toosend hello итоговое значение authorization_code задней tooyour приложение hello.  Поддерживаются значения `form_post` для *формы HTTP POST* или `fragment` для *фрагмента URL-адреса*.  Для веб-приложений, мы рекомендуем использовать `response_mode=form_post` tooensure hello наиболее безопасной передачи маркеров tooyour приложения. |
| state |рекомендуется |Значение, включенных в запрос hello, возвращаемых в ответ на токен hello.  Это может быть строка любого контента.  Как правило, для [предотвращения подделки межсайтовых запросов](http://tools.ietf.org/html/rfc6749#section-10.12)используется генерируемое случайным образом уникальное значение.  Hello вариант, также используется tooencode сведения о состоянии пользователя hello в приложение hello до возникновения hello запрос проверки подлинности, такие как страница hello и представление, в котором они находились на. |
| prompt |необязательный |Указывает тип hello это требует взаимодействия с пользователем.  В настоящее время hello только допустимые значения: «вход», «нет» и «разрешения».  `prompt=login`заставляет пользователя tooenter hello свои учетные данные в этот запрос Инверсия единого входа.  `prompt=none`Здравствуйте, противоположной: она гарантирует, что этот пользователь hello не предоставляется любого интерактивного запроса никакой.  Если hello запрос выполнить не удалось автоматически через единый вход, конечная точка hello возвращает ошибку.  `prompt=consent`запускает hello OAuth согласия диалоговое окно после hello пользователь выполняет вход, подтверждения приложение hello пользователя toogrant разрешения toohello. |
| login_hint |необязательный |Может быть hello заполнением нулями toopre используется имя пользователя и электронной почты поля адреса hello-на страницу входа для пользователя hello, если вы знаете свое имя пользователя, заранее.  Часто приложения используют этот параметр при повторной проверке подлинности, уже извлеченных hello имя пользователя из предыдущих вход с помощью hello `preferred_username` утверждения. |

На этом этапе является пользователь hello задаваемые tooenter своих учетных данных и завершения hello.

### Пример ответа
Образец ответа после проверки подлинности пользователя hello может выглядеть следующим образом:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Параметр | Описание |
| --- | --- |
| id_token |Hello `id_token` запросил приложение hello. Можно использовать hello `id_token` tooverify hello удостоверение пользователя и начать сеанс с пользователем hello. |
| state |Значение, включенных в запрос hello, также возвращается в ответ на токен hello. Как правило, для [предотвращения подделки межсайтовых запросов](http://tools.ietf.org/html/rfc6749#section-10.12)используется генерируемое случайным образом уникальное значение.  Hello вариант, также используется tooencode сведения о состоянии пользователя hello в приложение hello до возникновения hello запрос проверки подлинности, такие как страница hello и представление, в котором они находились на. |

### Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello `redirect_uri` , приложение hello можно обрабатывать их соответствующим образом:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Параметр | Описание |
| --- | --- |
| error |Ошибка строка кода, который может быть используется tooclassify типы ошибок, которые возникают и может быть tooerrors используется tooreact. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |

#### Коды ошибок конечной точки авторизации
Hello следующей таблице описаны hello различные коды ошибок, которые могут быть возвращены в hello `error` параметр hello сообщение об ошибке.

| Код ошибки | Описание | Действие клиента |
| --- | --- | --- |
| invalid_request |Ошибка протокола, например отсутствует обязательный параметр. |Исправить и повторно отправьте запрос hello. Это ошибка разработки, которая, как правило, обнаруживается во время первоначального тестирования. |
| unauthorized_client |Hello клиентское приложение не допускается toorequest код авторизации. |Обычно это происходит, когда клиентское приложение hello не зарегистрирован в Azure AD или toohello пользователей клиента Azure AD не добавляется. приложение Hello может предложить пользователю инструкцию для установки приложения hello и добавив tooAzure AD hello. |
| access_denied |Владелец ресурса отказал в использовании |Hello клиентское приложение может уведомить пользователя hello, он не может продолжена без согласия пользователя hello. |
| unsupported_response_type |сервер авторизации Hello не поддерживает тип ответа hello в запросе hello. |Исправить и повторно отправьте запрос hello. Это ошибка разработки, которая, как правило, обнаруживается во время первоначального тестирования. |
| server_error |Произошла непредвиденная ошибка сервера Hello. |Повторите запрос hello. Эти ошибки могут возникать в связи с временными условиями. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временной ошибки tooa. |
| temporarily_unavailable |Hello server временно — слишком занят, toohandle hello запрос. |Повторите запрос hello. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временного состояния ошибки tooa. |
| invalid_resource |Hello целевой ресурс является недопустимым, так как он не существует, Azure AD не удается найти или настроена неправильно. |Это означает, что hello ресурс, если он существует, не был настроен в клиенте hello. приложение Hello может предложить пользователю инструкцию для установки приложения hello и добавив tooAzure AD hello. |

## Проверка hello id_token
Только получение `id_token` не достаточно пользователем hello tooauthenticate; необходимо проверить подпись hello и утверждения hello в hello `id_token` в соответствии с требованиями приложения. Конечная точка Hello Azure AD использует веб-маркеры JSON (JWT) и криптографии с открытым ключом toosign маркеров и убедитесь, что они являются допустимыми.

Вы можете toovalidate hello `id_token` в клиентском коде, но распространенной практикой является toosend hello `id_token` tooa внутреннего сервера и выполняет проверку hello существует. После проверки подписи hello hello `id_token`, существует несколько утверждений, необходимых tooverify.

Вы также можете toovalidate дополнительные утверждения в зависимости от вашего сценария. Ниже приведены некоторые из стандартных проверок:

* Обеспечение hello пользователя или организации зарегистрировался для приложения hello.
* Обеспечение hello пользователь имеет правильную авторизации и права доступа
* Обеспечение определенного уровня проверки подлинности, например Многофакторной Идентификации.

После проверки hello `id_token`, можно начать сеанс с пользователем hello и использовать утверждения hello в hello `id_token` tooobtain сведения о пользователе hello в вашем приложении. Эти сведения можно использовать для отображения, записей, авторизации и т. д. Дополнительные сведения о hello типы маркеров и утверждения [типы поддерживаемых токенов и утверждений](active-directory-token-and-claims.md).

## Отправка запроса на выход
При желании hello toosign выход пользователя из приложения hello, оно недостаточно tooclear файлов cookie вашего приложения или в противном случае завершения сеанса hello с пользователем hello.  Также необходимо перенаправить пользователя toohello hello `end_session_endpoint` для выхода.  Если toodo не так, hello пользователь получит приложение может tooreauthenticate tooyour без ввода учетных данных, так как они будут иметь допустимый единого входа сеанс с конечной точки Azure AD hello.

Можно просто перенаправить пользователя toohello hello `end_session_endpoint` указаны в документе метаданных OpenID Connect hello:

```
GET https://login.microsoftonline.com/common/oauth2/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F

```

| Параметр |  | Описание |
| --- | --- | --- |
| post_logout_redirect_uri |рекомендуется |URL-адрес Hello hello пользователя должно быть перенаправленный tooafter успешного выхода.  Если не включен, пользователь hello отображается универсальное сообщение. |

## Единый выход
При перенаправлении hello пользователя toohello `end_session_endpoint`, Azure AD очищает сеанса hello пользователя из браузера hello. Тем не менее пользователь hello может находиться в системе tooother приложений, которые используют Azure AD для проверки подлинности. tooenable toosign эти приложения hello пользователя одновременно, Azure AD отправляет HTTP GET запроса toohello зарегистрированные `LogoutUrl` всех приложений hello hello пользователя подключен к сети для. Приложения должен вернуть запрос toothis сняв сеансов идентифицирует пользователя hello и возвращая `200` ответа.  При желании единого входа toosupport помещает в приложении, необходимо реализовать такие `LogoutUrl` в код приложения.  Можно задать hello `LogoutUrl` из hello портала Azure:

1. Перейдите toohello [портала Azure](https://portal.azure.com).
2. Выберите в Active Directory, щелкнув в вашей учетной записи в верхнем правом углу hello страницы приветствия.
3. На панели навигации слева hello, выберите **Azure Active Directory**, выберите **регистрации приложения** и выберите приложение.
4. Щелкните **свойства** и найти hello **URL-адрес выхода** текстовое поле. 

## Получение токена
Многие веб-приложения необходим только пользователь hello входа toonot в, но также получить доступ к веб-службы, от имени этого пользователя с помощью OAuth. Этот сценарий объединяет OpenID Connect для проверки подлинности пользователя при получении одновременно `authorization_code` , можно использовать tooget `access_tokens` с помощью hello потока кода авторизации OAuth.

## Получение токенов доступа
tooacquire маркеры доступа, необходимые toomodify hello запрос вход выше.

```
// Line breaks for legibility only

GET https://login.microsoftonline.com/{tenant}/oauth2/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application Id
&response_type=id_token+code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered Redirect Uri, url encoded
&response_mode=form_post                              // form_post', or 'fragment'
&scope=openid
&resource=https%3A%2F%2Fservice.contoso.com%2F                                     
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

Включая области разрешений в запросе hello и используя `response_type=code+id_token`, hello `authorize` конечной точки гарантирует, что hello пользователь согласился toohello разрешениями, перечисленными в hello `scope` параметр запроса и возвращать код авторизации для приложения tooexchange маркера доступа.

### Успешный ответ
Успешный ответ с использованием метода `response_mode=form_post` выглядит следующим образом:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Параметр | Описание |
| --- | --- |
| id_token |Hello `id_token` запросил приложение hello. Можно использовать hello `id_token` tooverify hello удостоверение пользователя и начать сеанс с пользователем hello. |
| Код |значение authorization_code Hello hello запрошенного приложения. приложение Hello можно использовать toorequest код авторизации hello маркер доступа для hello целевого ресурса. Срок действия кодов авторизации мал и обычно истекает по прошествии порядка 10 минут. |
| state |Если параметр состояния включается в запрос hello, hello одинаковое значение должно отображаться в ответ hello. приложение Hello следует Проверьте идентичность значений состояния hello hello запроса и ответа. |

### Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello `redirect_uri` , приложение hello можно обрабатывать их соответствующим образом:

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Параметр | Описание |
| --- | --- |
| error |Ошибка строка кода, который может быть используется tooclassify типы ошибок, которые возникают и может быть tooerrors используется tooreact. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |

Описание hello возможные коды ошибок и их действие рекомендуемые клиента см. в разделе [коды ошибки для ошибки конечной точки авторизации](#error-codes-for-authorization-endpoint-errors).

После авторизации `code` и `id_token`, может войти пользователя hello и получения маркера доступа от их имени.  пользователь toosign hello в, необходимо проверить hello `id_token` точно так, как описано выше. tooget маркеры доступа, следуйте hello действия, описанные в разделе «Использовать toorequest код авторизации hello маркер доступа» hello объекта нашей [документации по протоколу OAuth](active-directory-protocols-oauth-code.md).
