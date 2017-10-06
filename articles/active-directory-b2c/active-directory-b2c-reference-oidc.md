---
title: "Azure AD B2C: вход в веб-приложения с помощью OpenID Connect | Документация Майкрософт"
description: "Построение веб-приложений с использованием реализации протокола проверки подлинности OpenID Connect hello hello Azure Active Directory"
services: active-directory-b2c
documentationcenter: 
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: 21d420c8-3c10-4319-b681-adf2e89e7ede
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/16/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: 89e9cfa28e4e5c34304aea355cca2dd0c4b42abc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-web-sign-in-with-openid-connect"></a>Azure Active Directory B2C: вход в веб-приложения с помощью OpenID Connect
OpenID Connect — это протокол проверки подлинности, построена на базе OAuth 2.0, может быть вход пользователей используется toosecurely tooweb приложений. С помощью реализации hello Azure Active Directory B2C OpenID Connect (Azure AD B2C), можно передать регистрации, вход и задач по управлению другими удостоверениями в вашей tooAzure приложения web Active Directory (Azure AD). В этом руководстве показано, как toodo так, в зависимости от языка. Описывает способ toosend и получать сообщения HTTP без использования нашей библиотек с открытым исходным кодом.

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) расширяет hello OAuth 2.0 *авторизации* протокола для использования в качестве *проверки подлинности* протокола. Это позволяет вам tooperform единого входа с помощью OAuth. Представляет концепцию hello *маркер идентификатора*, который является маркер безопасности, позволяющий tooverify клиента hello hello удостоверение пользователя hello и получить профиль основные сведения о пользователе hello.

Поскольку он расширяет OAuth 2.0, также позволяет приложениям получить toosecurely *маркеры доступа*. Можно использовать access_tokens tooaccess ресурсы, которые защищены с помощью [сервер авторизации](active-directory-b2c-reference-protocols.md#the-basics). Мы рекомендуем использовать OpenID Connect для веб-приложений, которые размещаются на сервере и доступны через веб-браузер. Если требуется tooadd identity management tooyour мобильных или настольных приложений с помощью Azure AD B2C, следует использовать [OAuth 2.0](active-directory-b2c-reference-oauth-code.md) вместо OpenID Connect.

Azure AD B2C расширяет toodo протокола Стандартная OpenID Connect hello больше, чем простой проверки подлинности и авторизации. Представляет hello [параметра политики](active-directory-b2c-reference-policies.md), обеспечивающий toouse OpenID Connect tooadd взаимодействий с пользователем, таких как регистрация, вход и управление профилями--tooyour приложения. Здесь мы покажем, как toouse OpenID Connect и политики tooimplement, каждый из них возникает в веб-приложений. Мы также покажем, как tooget токены доступа для доступа к веб-API.

запросы HTTP пример Hello в следующем разделе hello использования каталог B2C образца, fabrikamb2c.onmicrosoft.com, а также пример приложения, https://aadb2cplayground.azurewebsites.net и политик. Вы можете tootry out hello запрашивает самостоятельно, используя эти значения, или их можно заменить на собственный.
Узнайте, каким образом слишком[получить клиента B2C, приложения и политики](#use-your-own-b2c-directory).

## <a name="send-authentication-requests"></a>Отправка запросов проверки подлинности
Если веб-приложения требуется tooauthenticate hello пользователя и выполнения политики, мог направлять пользователя toohello hello `/authorize` конечной точки. Это интерактивный часть потока hello hello где hello пользователь выполняет действие, в зависимости от политики hello.

В этом запросе hello клиент указывает hello разрешения, необходимость tooacquire от пользователя hello в hello `scope` tooexecute политику параметров и hello в hello `p` параметра. Три примера приведены в следующих разделах (с разбиением на строки для удобства чтения), hello каждого с помощью другой политики. tooget вид, как работает каждый запрос, повторите запрос вставки hello в браузере и запустив его.

#### <a name="use-a-sign-in-policy"></a>Пример с политикой входа в систему
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

#### <a name="use-a-sign-up-policy"></a>Пример с политикой регистрации
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

#### <a name="use-an-edit-profile-policy"></a>Пример с политикой изменения профиля
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=code+id_token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=form_post
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Параметр | Обязательный? | Описание |
| --- | --- | --- |
| client_id |Обязательно |Hello приложение с кодом, hello [портал Azure](https://portal.azure.com/) назначенный tooyour приложения. |
| response_type |Обязательно |Тип ответа Hello, которое должно включать маркер идентификатора для OpenID Connect. Если веб-приложению также потребуются токены для вызова веб-API, можете использовать `code+id_token`, как и в наших примерах. |
| redirect_uri |Рекомендуется |Hello `redirect_uri` параметр приложения, где запросы проверки подлинности можно отправленных и полученных приложения. Он должен точно соответствовать одному из hello `redirect_uri` параметров, зарегистрированных в портале hello, за исключением того, он должен быть в кодировке URL-адрес. |
| scope |Обязательно |Список областей с разделителями-пробелами. Значение одной области указывает tooAzure AD оба разрешения, которые были запрошены. Hello `openid` область указывает toosign разрешение в hello пользователей и получить данные о пользователе hello в форме hello маркеров безопасности (Дополнительные toocome об этом hello статьи). Hello `offline_access` область является необязательным для веб-приложений. Указывает, что вашему приложению потребуется *токен обновления* для tooresources долгоживущие доступа. |
| response_mode |Рекомендуется |метод Hello, которые должны быть задней tooyour используется toosend hello полученный авторизации кода приложения. Это может быть `query`, `form_post` или `fragment`.  Hello `form_post` для обеспечения лучшей защиты рекомендуется режим ответа. |
| state |Рекомендуется |Значение, включенных в запрос hello, также возвращается в ответ на токен hello. Это может быть строка любого контента. Как правило, с целью предотвращения подделки межсайтовых запросов используется генерируемое случайным образом уникальное значение. Hello вариант, также используется tooencode сведения о состоянии пользователя hello в приложение hello до возникновения hello запрос проверки подлинности, например страницы hello, в котором они находились на. |
| nonce |Обязательно |Значение, включенных в запрос hello (созданных в ходе приложение hello), будут включены в результирующий маркер идентификатор hello как утверждения. приложение Hello можно затем удостоверьтесь, что атак воспроизведения токена значение toomitigate. Hello значение обычно равно случайного уникальную строку, которая может быть используется tooidentify hello источник запроса hello. |
| p |Обязательно |политика Hello, который будет выполняться. Это имя политики, созданные в клиенте B2C hello. Имя политики Hello значение должна начинаться с `b2c\_1\_`. Дополнительные сведения о политиках и hello [расширяемая инфраструктура политик](active-directory-b2c-reference-policies.md). |
| prompt |Необязательно |Тип Hello это требует взаимодействия с пользователем. Hello единственным допустимым значением в данный момент является `login`, который принудительно hello пользователя tooenter свои учетные данные для этого запроса. Единый вход не сработает. |

На этом этапе hello пользователя запрашивается toocomplete hello политики рабочего процесса. Это может вызвать hello пользователь вводит свое имя пользователя и пароль, вход удостоверений из социальных сетей, регистрирующихся для каталога hello или любое другое число шагов в зависимости от способа определения политики hello.

После завершения политики hello hello пользователя Azure AD возвращает приложении tooyour ответ в указанном hello `redirect_uri` параметра с помощью метода hello, которая указана в hello `response_mode` параметра. для каждого из предыдущих случаев, независимо от политики hello, который выполняется hello hello же Hello ответа.

Успешный ответ с использованием метода `response_mode=fragment` выглядит следующим образом:

```
GET https://aadb2cplayground.azurewebsites.net/#
id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=arbitrary_data_you_can_receive_in_the_response
```

| Параметр | Описание |
| --- | --- |
| id_token |Здравствуйте, маркер идентификатора, hello запрошенного приложения. Можно использовать удостоверение маркера tooverify hello hello идентификатор пользователя и начать сеанс с пользователем hello. Дополнительные сведения о маркеров безопасности и их содержимое включаются в hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| Код |Hello код авторизации, приложение hello запрошена, если вы использовали `response_type=code+id_token`. приложение Hello можно использовать toorequest код авторизации hello маркер доступа для целевого ресурса. Срок действия кодов авторизации крайне мал. и обычно истекает по прошествии порядка 10 минут. |
| state |Если `state` параметр включен в запрос hello hello же значение должно содержаться в ответе hello. Hello приложения следует убедиться, что hello `state` значения в hello запроса и ответа идентичны. |

Сообщения об ошибках могут отправляться также toohello `redirect_uri` параметра, так что приложение hello можно обрабатывать их соответствующим образом:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки, может быть используется tooclassify типы ошибок, происходящих и это может стать tooerrors tooreact используется. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |
| state |См. полное описание hello в первой таблице hello в этом разделе. Если `state` параметр включен в запрос hello hello же значение должно содержаться в ответе hello. Hello приложения следует убедиться, что hello `state` значения в hello запроса и ответа идентичны. |

## <a name="validate-hello-id-token"></a>Проверка токена идентификатор hello
Просто получает маркер идентификатора не хватает tooauthenticate hello пользователем. Необходимо проверить подпись маркер идентификатора hello и hello утверждения маркера hello в соответствии с требованиями приложения. Использует Azure AD B2C [веб-маркеры JSON (JWT)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) и открытый ключ шифрования toosign маркеры и убедитесь, что они являются допустимыми.

Для проверки JWT доступны многие библиотеки с открытым исходным кодом в зависимости от выбранного языка программирования. Мы рекомендуем изучить различные библиотеки, а не реализовывать логику проверки самостоятельно. здесь сведения Hello будет полезно понять, как tooproperly использование этих библиотек.

Azure AD B2C имеет OpenID Connect конечную точку метаданных, что позволяет toofetch приложение сведения о Azure AD B2C во время выполнения. Эти сведения включают конечные точки, содержимое маркеров и ключи подписи маркеров. Для каждой политики в клиенте B2C есть собственный документ метаданных JSON. Например, документ hello метаданных для hello `b2c_1_sign_in` политики в `fabrikamb2c.onmicrosoft.com` находится в:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Одно из свойств hello этого документа конфигурации является `jwks_uri`, значение которого для hello бы одной политике:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`.

toodetermine политики, был использован в подписи маркер идентификатора (и, из которой toofetch hello метаданных), у вас есть два варианта. Во-первых, имя политики hello включается в hello `acr` утверждения в маркер идентификатора hello. Сведения о как tooparse hello утверждений от маркер идентификатора разделе hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md). Другой вариант — tooencode политики hello в значение hello hello `state` параметра при выдать запрос hello и расшифровать его toodetermine использовался какую политику. Каждый из этих методов является допустимым.

После приобретен hello документов метаданных из конечной точки метаданных OpenID Connect hello открытые ключи RSA 256 hello (которые находятся в данной конечной точке) можно использовать подпись hello toovalidate hello идентификатор токена. В каждый момент времени в этой конечной точке может находиться множество ключей, каждый из которых определяется утверждением `kid`. Hello заголовок маркер идентификатора hello также содержит `kid` утверждения, которое указывает, какой из этих ключей был маркер идентификатора используется toosign hello. Дополнительные сведения см. в разделе hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md) (hello раздел на [проверку маркеров](active-directory-b2c-reference-tokens.md#token-validation), в частности).
<!--TODO: Improve hello information on this-->

Существует несколько утверждений, необходимо tooverify после проверки предоставленных hello подпись токена идентификатор hello. например

* Следует проверить hello `nonce` утверждения tooprevent атак с повторением токенов. Его значение должно быть указанный запрос hello вход.
* Следует проверить hello `aud` утверждения, hello маркер идентификатора tooensure был выпущен для приложения. Его значение должно быть Идентификатором приложения hello приложения.
* Следует проверить hello `iat` и `exp` утверждений tooensure, hello маркер идентификатора не истек.

Также существуют некоторые дополнительные проверки, которые необходимо выполнить. Они описаны подробно hello [OpenID подключения Core Spec](http://openid.net/specs/openid-connect-core-1_0.html).  Можно также toovalidate дополнительные утверждения, в зависимости от вашего сценария. Ниже приведены некоторые из стандартных проверок:

* Убедитесь, что Здравствуйте, пользователя или организации, зарегистрировался для приложения hello.
* Обеспечение авторизации и права, необходимые этому пользователю hello.
* Обеспечение определенного уровня проверки подлинности, например многофакторной проверки подлинности.

Дополнительные сведения о hello утверждения в маркер идентификатора см. в разделе hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md).

После проверки маркер идентификатора hello можно начать сеанс с пользователем hello. Можно использовать утверждения hello в hello идентификатор маркера tooobtain сведения о пользователе hello в вашем приложении. Эти сведения используются для отображения, получения записей и проверки подлинности.

## <a name="get-a-token"></a>Получение маркера
При необходимости вашей tooonly web app выполнение политик, можно пропустить hello следующие несколько разделов. Эти разделы — это применимо только tooweb приложения, которым требуется проверка подлинности toomake вызовы tooa веб-API и также защищен Azure AD B2C.

Можно использовать код авторизации hello, который вы приобрели (с помощью `response_type=code+id_token`) для токена toohello требуемого ресурса, отправляя `POST` запроса toohello `/token` конечной точки. В настоящее время hello только ресурсов, можно запросить маркер является серверной части приложения собственных веб-API. соглашение о Hello для запроса маркера tooyourself — это идентификатор клиента приложения hello областью toouse:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=authorization_code&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>

```

| Параметр | Обязательный? | Описание |
| --- | --- | --- |
| p |Обязательно |Здравствуйте, политики, которая была используется tooacquire hello авторизации кода. Другую политику в этом запросе использовать нельзя. Примечание При добавлении этого параметра строки запроса toohello, не toohello `POST` текста. |
| client_id |Обязательно |Hello приложение с кодом, hello [портал Azure](https://portal.azure.com/) назначенный tooyour приложения. |
| grant_type |Обязательно |Здравствуйте, тип используемого предоставления прав, который должен быть `authorization_code` для потока кода авторизации hello. |
| scope |Рекомендуется |Список областей с разделителями-пробелами. Значение одной области указывает tooAzure AD оба разрешения, которые были запрошены. Hello `openid` область указывает toosign разрешение в hello пользователей и получения данных о пользователе hello в виде hello id_token параметров. Это может быть используется tooget маркеры tooyour приложении серверной части веб-API, который представляется hello таким же Идентификатором приложения hello клиентом. Hello `offline_access` область показывает, что вашему приложению потребуется токен обновления для tooresources долгоживущие доступа. |
| Код |Обязательно |Код авторизации Hello, полученному в первый участок потока hello hello. |
| redirect_uri |Обязательно |Hello `redirect_uri` параметр приложения hello, которого вы получили код авторизации hello. |
| client_secret |Обязательно |секрет приложения Hello, созданный hello [портал Azure](https://portal.azure.com/). Это важный артефакт безопасности, и он должен безопасно храниться на сервере. Также следует периодически изменять секрет клиента. |

Успешный ответ маркера выглядит следующим образом:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Параметр | Описание |
| --- | --- |
| not_before |время Hello, на какие hello считается действительным, во время эпохи маркер. |
| token_type |значение типа токена Hello. Здравствуйте, только тип, который поддерживает Azure AD является `Bearer`. |
| access_token |Hello подписан маркер JWT по запросу. |
| scope |для какой hello маркер действителен в областях Hello. Их можно использовать для кэширования маркеров для последующего использования. |
| expires_in |Hello продолжительность hello токен доступа является допустимым (в секундах). |
| refresh_token |Маркер обновления OAuth 2.0. приложение Hello можно использовать этот токен tooacquire дополнительные маркеры, после истечения срока действия текущего маркера hello. Обновить токены долгоживущие и может быть tooresources доступа используется tooretain на длительное время. Дополнительные сведения см. в разделе toohello [ссылку на маркер B2C](active-directory-b2c-reference-tokens.md). Обратите внимание, вы должны использовали hello области `offline_access` в hello авторизации и маркер запросов в порядке tooreceive токен обновления. |

Сообщения об ошибках выглядят следующим образом:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки, может быть используется tooclassify типы ошибок, происходящих и это может стать tooerrors tooreact используется. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |

## <a name="use-hello-token"></a>Использование маркера hello
Теперь, когда вы успешно получили маркер доступа, можно использовать токен hello в запросы tooyour серверной части веб-API, включив его в hello `Authorization` заголовка:

```
GET /tasks
Host: https://mytaskwebapi.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## <a name="refresh-hello-token"></a>Обновление маркера hello
Срок действия маркеров идентификации крайне мал. Их необходимо обновить, после истечения срока их действия, ресурсы могут tooaccess toocontinue. Это можно сделать путем отправки другой `POST` запроса toohello `/token` конечной точки. На этот раз укажите hello `refresh_token` параметра вместо hello `code` параметр:

```
POST fabrikamb2c.onmicrosoft.com/oauth2/v2.0/token?p=b2c_1_sign_in HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=refresh_token&client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6&scope=openid offline_access&refresh_token=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&redirect_uri=urn:ietf:wg:oauth:2.0:oob&client_secret=<your-application-secret>
```

| Параметр | Обязательно | Описание |
| --- | --- | --- |
| p |Обязательно |политика Hello, исходный токен обновления используется tooacquire hello. Другую политику в этом запросе использовать нельзя. Обратите внимание, добавить этот параметр строки запроса toohello, toohello тело POST. |
| client_id |Обязательно |Hello приложение с кодом, hello [портал Azure](https://portal.azure.com/) назначенный tooyour приложения. |
| grant_type |Обязательно |Тип инструкции grant, который должен быть токен обновления для этого участка поток authorization code hello Hello. |
| scope |Рекомендуется |Список областей с разделителями-пробелами. Значение одной области указывает tooAzure AD оба разрешения, которые были запрошены. Hello `openid` область указывает toosign разрешение в hello пользователей и получения данных о пользователе hello в форме hello маркеров безопасности. Это может быть используется tooget маркеры tooyour приложении серверной части веб-API, который представляется hello таким же Идентификатором приложения hello клиентом. Hello `offline_access` область показывает, что вашему приложению потребуется токен обновления для tooresources долгоживущие доступа. |
| redirect_uri |Рекомендуется |Hello `redirect_uri` параметр приложения hello, которого вы получили код авторизации hello. |
| refresh_token |Обязательно |Hello исходный токен обновления, полученному в hello второго участка hello потока. Обратите внимание, вы должны использовали hello области `offline_access` в hello авторизации и маркер запросов в порядке tooreceive токен обновления. |
| client_secret |Обязательно |секрет приложения Hello, созданный hello [портал Azure](https://portal.azure.com/). Это важный артефакт безопасности, и он должен безопасно храниться на сервере. Также следует периодически изменять секрет клиента. |

Успешный ответ маркера выглядит следующим образом:

```
{
    "not_before": "1442340812",
    "token_type": "Bearer",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "scope": "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
    "expires_in": "3600",
    "refresh_token": "AAQfQmvuDy8WtUv-sd0TBwWVQs1rC-Lfxa_NDkLqpg50Cxp5Dxj0VPF1mx2Z...",
}
```
| Параметр | Описание |
| --- | --- |
| not_before |время Hello, на какие hello считается действительным, во время эпохи маркер. |
| token_type |значение типа токена Hello. Здравствуйте, только тип, который поддерживает Azure AD является `Bearer`. |
| access_token |Hello подписан маркер JWT по запросу. |
| scope |область Hello, hello токена является допустимым для, который может использоваться для кэширования токенов для последующего использования. |
| expires_in |Hello продолжительность hello токен доступа является допустимым (в секундах). |
| refresh_token |Маркер обновления OAuth 2.0. приложение Hello можно использовать этот токен tooacquire дополнительные маркеры, после истечения срока действия текущего маркера hello.  Обновить токены долгоживущие и может быть tooresources доступа используется tooretain на длительное время. Дополнительные сведения см. в разделе toohello [ссылку на маркер B2C](active-directory-b2c-reference-tokens.md). |

Сообщения об ошибках выглядят следующим образом:

```
{
    "error": "access_denied",
    "error_description": "hello user revoked access toohello app.",
}
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки, может быть используется tooclassify типы ошибок, происходящих и это может стать tooerrors tooreact используется. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |

## <a name="send-a-sign-out-request"></a>Отправка запроса на выход
При необходимости hello toosign выход пользователя из приложения hello, оно не хватает tooclear файлов cookie вашего приложения или в противном случае завершения сеанса hello с пользователем hello. Также необходимо перенаправить hello пользователя tooAzure AD toosign out. Если не toodo таким образом, пользователь hello может быть приложение может tooreauthenticate tooyour без еще раз ввести свои учетные данные. так как они будут иметь действительный сеанс единого входа с Azure AD.

Можно просто перенаправить пользователя toohello hello `end_session` конечной точки, указанный в документе метаданных OpenID Connect hello описано ранее в hello раздел «Проверка маркер идентификатора hello»:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Параметр | Обязательный? | Описание |
| --- | --- | --- |
| p |Обязательно |политика Hello требуется toouse toosign hello пользователя приложения. |
| post_logout_redirect_uri |Рекомендуется |Hello URL-адрес этого hello пользователя должно быть перенаправленный tooafter успешного выхода. Если не указан, Azure AD B2C показан пользователь hello универсальное сообщение. |

> [!NOTE]
> Несмотря на то, что направление hello пользователя toohello `end_session` некоторые из одного состояния входа с Azure AD B2C hello пользователя приведет к очистке конечной точки, hello выход пользователя из сеанса поставщика Удостоверений удостоверений из социальных сетей подпись не будет. При выборе пользователем hello Здравствуйте того же поставщика Удостоверений, при последующем входе в систему, они будут пройти повторную проверку подлинности, не вводя свои учетные данные. Если пользователю toosign B2C приложения, оно означает, что им нужен toosign за пределы свою учетную запись Facebook. Однако в случае hello локальных учетных записей пользователя hello сеанс будет завершен правильно.
> 
> 

## <a name="use-your-own-b2c-tenant"></a>Использование собственного клиента B2C
Если требуется tootry эти запросы самостоятельно, необходимо сначала выполнить следующие три шага и замените примеры значений hello описано выше на собственный:

1. [Создание клиента B2C](active-directory-b2c-get-started.md)и использовать в запросах hello hello имя вашего клиента.
2. [Создание приложения](active-directory-b2c-app-registration.md) tooobtain идентификатор приложения. Включите в свое приложение веб-приложение или веб-API. При необходимости создайте секрет приложения.
3. [Создание политик](active-directory-b2c-reference-policies.md) tooobtain имена ваших политики.

