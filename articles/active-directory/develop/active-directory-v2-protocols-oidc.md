---
title: "Active Directory версии 2.0 и hello OpenID Connect протокола aaaAzure | Документы Microsoft"
description: "Построение веб-приложений с использованием протокола проверки подлинности OpenID Connect hello реализации v2.0 hello Azure AD."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a4875997-3aac-4e4c-b7fe-2b4b829151ce
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 277bb406dbb24ccefb09e4e4c928f0421755cf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Azure Active Directory версии 2.0 и hello OpenID Connect протокола
OpenID Connect — это протокол проверки подлинности, построенные на OAuth 2.0, можно использовать toosecurely входа в веб-приложении tooa пользователя. При использовании конечной точки v2.0 hello реализацию OpenID Connect, можно добавить вход и API-Интерфейс доступа tooyour веб-приложений. В этой статье мы покажем, как toodo этом независимо от языка. Описано, как toosend и получать сообщения HTTP без использования все библиотеки Microsoft открытым исходным кодом.

> [!NOTE]
> Конечная точка v2.0 Hello не поддерживает все сценарии Azure Active Directory и возможности. toodetermine необходимость использования конечной точки v2.0 hello, узнайте, как [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html) расширяет hello OAuth 2.0 *авторизации* toouse протокола как *проверки подлинности* протокола, чтобы можно было выполнить один вход с использованием OAuth. OpenID Connect введена концепция hello объекта *маркер идентификатора*, являющееся маркера безопасности, который позволяет клиентским hello tooverify hello удостоверение пользователя hello. маркер идентификатора Hello также возвращает базовый профиль сведения о пользователе hello. Поскольку OpenID Connect расширяет возможности OAuth 2.0, приложения можно безопасно получить *маркеры доступа*, который может быть используется tooaccess ресурсы, которые защищены с помощью [сервер авторизации](active-directory-v2-protocols.md#the-basics). Мы рекомендуем использовать OpenID Connect для [веб-приложений](active-directory-v2-flows.md#web-apps), которые размещаются на сервере и доступны через браузер.

## Схема протокола: вход в систему
Hello основной поток имеет hello шаги, представленные в следующей схеме hello. Каждый этап подробно описан далее в этой статье.

![Протокол OpenID Connect: вход в систему](../../media/active-directory-v2-flows/convergence_scenarios_webapp.png)

## Получить документ метаданных OpenID Connect hello
OpenID Connect описывает документ метаданных, содержащая большую часть hello сведения, необходимые для приложения tooperform входа. Сюда входят сведения, например toouse hello URL-адреса и расположение hello открытые ключи подписи hello службы. Для конечной точки v2.0 hello это hello OpenID Connect метаданных документ, который следует использовать:

```
https://login.microsoftonline.com/{tenant}/v2.0/.well-known/openid-configuration
```

Hello `{tenant}` может принимать одно из четырех значений:

| Значение | Описание |
| --- | --- |
| `common` |Пользователи с личную учетную запись Майкрософт и рабочую или учебную учетную запись из Azure Active Directory (Azure AD) могут входить в приложение toohello. |
| `organizations` |Только пользователи с рабочих или учебных учетных записей из Azure AD можно войти в приложение toohello. |
| `consumers` |Только пользователи с личной учетной записи Microsoft могут войти в приложение toohello. |
| `8eaef023-2b34-4da1-9baa-8bc8c9d6a490` или `contoso.onmicrosoft.com` |Только пользователи с рабочей или учебной учетной записи из Azure AD для конкретного клиента можно войти в приложения toohello. Здравствуйте, hello понятное доменное имя клиента Azure AD, либо можно использовать идентификатор GUID клиента hello. |

Hello метаданные — это простой документ нотации объектов JavaScript (JSON). См. следующий фрагмент кода для пример hello. Hello содержимое фрагмента кода полностью описаны в hello [спецификация OpenID Connect](https://openid.net).

```
{
  "authorization_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/authorize",
  "token_endpoint": "https:\/\/login.microsoftonline.com\/common\/oauth2\/v2.0\/token",
  "token_endpoint_auth_methods_supported": [
    "client_secret_post",
    "private_key_jwt"
  ],
  "jwks_uri": "https:\/\/login.microsoftonline.com\/common\/discovery\/v2.0\/keys",

  ...

}
```

Как правило используется этот документ метаданных tooconfigure библиотеку OpenID Connect или SDK; Библиотека Hello использовать hello метаданных toodo свою работу. Тем не менее если вы не используете OpenID Connect до построения библиотеки, можно выполнить действия hello в hello оставшейся части этой статьи tooperform входа в веб-приложения с использованием конечной точки v2.0 hello.

## Отправить запрос hello вход
Когда веб-приложение должно tooauthenticate пользователя hello и мог направлять пользователя toohello hello `/authorize` конечной точки. Этот запрос создан как первый участок toohello из hello [потока кода авторизации OAuth 2.0](active-directory-v2-protocols-oauth-code.md), с помощью этих важные различия:

* Hello запрос должен включать hello `openid` область в hello `scope` параметра.
* Hello `response_type` необходимо включить параметр `id_token`.
* Hello запрос должен включать hello `nonce` параметра.

Например:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=form_post
&scope=openid
&state=12345
&nonce=678910
```

> [!TIP]
> Щелкните следующие ссылки tooexecute hello этого запроса. После входа в браузере будет перенаправленный toohttps://localhost/myapp/, с помощью идентификатора токена в адресную строку hello. Обратите внимание, что в этом запросе используется `response_mode=query` (исключительно в демонстрационных целях). Мы рекомендуем использовать `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid&response_mode=query&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Параметр | Условие | Описание |
| --- | --- | --- |
| tenant |Обязательно |Можно использовать hello `{tenant}` значение пути toocontrol hello запроса, которые можно выполнять вход в приложение toohello hello. Hello допустимые значения: `common`, `organizations`, `consumers`и идентификаторы клиентов. Чтобы узнать больше, ознакомьтесь с [основами протокола](active-directory-v2-protocols.md#endpoints). |
| client_id |Обязательно |Приложение Hello идентификатор этого hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) назначенный tooyour приложения. |
| response_type |Обязательно |Должен включать `id_token` для входа в OpenID Connect. Кроме того, может включать другие значения `response_types`, например `code`. |
| redirect_uri |Рекомендуется |URI приложения, где запросы проверки подлинности можно отправленных и полученных приложения перенаправления Hello. Он должен точно соответствовать одной кодировке идентификаторы URI, зарегистрированные в портале hello, за исключением того, что он должен быть URL-адрес перенаправления hello. |
| scope |Обязательно |Список областей с разделителями-пробелами. OpenID Connect, он должен содержать область hello `openid`, что означает разрешение «Вход» toohello пользовательского интерфейса согласия hello. Для предоставления согласия этот запрос может также включать в себя другие области. |
| nonce |Обязательно |Значение, включенных в запрос hello, созданное приложение hello, который будет включаться в результирующее значение id_token hello как утверждения. проверить приложение Hello атак воспроизведения токена значение toomitigate. значение Hello обычно является случайного уникальный строкой, можно использовать tooidentify hello источник запроса hello. |
| response_mode |Рекомендуется |Указывает метод hello, которые должны быть задней tooyour используется toosend hello полученный авторизации кода приложения. Может иметь значение `query`, `form_post` или `fragment`. Для веб-приложений, мы рекомендуем использовать `response_mode=form_post`, tooensure hello наиболее безопасной передачи маркеров tooyour приложения. |
| state |Рекомендуется |Значение, включенных в запрос hello, также будут возвращены в ответ на токен hello. Это может быть строка любого содержания. Случайный уникальное значение обычно используется слишком[предотвращения атак с подделкой межсайтовых запросов](http://tools.ietf.org/html/rfc6749#section-10.12). состояние Hello также является используется tooencode сведения о состоянии пользователя hello в приложение hello до возникновения hello запрос проверки подлинности, таких как hello страницы или представления hello пользователя была. |
| prompt |Необязательно |Указывает тип hello это требует взаимодействия с пользователем. Hello только допустимые значения в данный момент: `login`, `none`, и `consent`. Hello `prompt=login` утверждения принудительно hello пользователя tooenter свои учетные данные на этот запрос, инвертирует единого входа. Hello `prompt=none` утверждения — hello противоположным. Это утверждение гарантирует, что этот пользователь hello не предоставляется все запросы на экран ни при каких обстоятельствах. Если hello запрос выполнить не удалось автоматически через единый вход, конечная точка v2.0 hello возвращает ошибку. Hello `prompt=consent` утверждения триггеры hello диалоговое окно согласия OAuth после входа пользователя hello. диалоговое окно приветствия запрашивает приложение hello пользователя toogrant разрешения toohello. |
| login_hint |Необязательно |Можно использовать этот параметр toopre заполнения hello имя пользователя и адрес электронной почты поля адреса hello-на страницу входа для пользователя hello, если известно имя пользователя hello заранее. Часто приложения используют этот параметр во время повторной проверки подлинности, после уже извлечения имени пользователя hello из более ранних вход с помощью hello `preferred_username` утверждения. |
| domain_hint |Необязательно |Возможные значения — `consumers` или `organizations`. Если включен, он пропускает hello процесса обнаружения на основе электронной почты этого пользователя hello проходит через на hello v2.0 страницы входа, немного упрощает взаимодействие с пользователем. Часто приложения используют этот параметр во время повторной проверки подлинности путем извлечения hello `tid` утверждения из токена идентификатор hello. Если hello `tid` утверждения, значение — `9188040d-6c67-4c5b-b112-36a304b66dad`, используйте `domain_hint=consumers`. Или используйте `domain_hint=organizations`. |

На этом этапе пользователь hello является запросом tooenter своих учетных данных и завершения hello. Hello v2.0 конечной точки проверяет, что hello пользователь согласился toohello разрешениями, перечисленными в hello `scope` параметр запроса. Если пользователь hello не согласился tooany таких разрешений, конечная точка v2.0 hello предлагает hello пользователя tooconsent toohello необходимые разрешения. Вы можете узнать больше о [разрешениях, согласии и мультитенантных приложениях](active-directory-v2-scopes.md).

После hello пользователь проходит аутентификацию и дает свое согласие, URI перенаправления hello v2.0 конечная точка возвращает tooyour ответа приложения hello указано с помощью метода hello, указанного в hello `response_mode` параметра.

### Успешный ответ
Успешный ответ при использовании `response_mode=form_post` выглядит следующим образом.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&state=12345
```

| Параметр | Описание |
| --- | --- |
| id_token |Здравствуйте, маркер идентификатора, hello запрошенного приложения. Можно использовать hello `id_token` tooverify параметр hello удостоверение пользователя и начать сеанс с пользователем hello. Дополнительные сведения о маркеров безопасности и их содержимое. в разделе hello [конечной точки v2.0 маркеры ссылка](active-directory-v2-tokens.md). |
| state |Если `state` параметр включен в запрос hello hello же значение должно содержаться в ответе hello. приложение Hello следует Проверьте идентичность значений состояния hello hello запроса и ответа. |

### Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello URI перенаправления, чтобы hello приложение может обрабатывать их. Сообщение об ошибке выглядит следующим образом.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки, который можно использовать типы tooclassify возникающие ошибки и tooreact tooerrors. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello. |

### Коды ошибок конечной точки авторизации
Hello следующей таблице описаны коды ошибок, которые могут быть возвращены в hello `error` параметр hello сообщение об ошибке:

| Код ошибки | Описание | Действие клиента |
| --- | --- | --- |
| invalid_request |Ошибка протокола, например отсутствует обязательный параметр. |Исправить и повторно отправьте запрос hello. Это ошибка разработки, которая, как правило, обнаруживается во время первоначального тестирования. |
| unauthorized_client |клиентское приложение Hello не может запросить код авторизации. |Обычно это происходит, когда клиентское приложение hello не зарегистрирован в Azure AD или toohello пользователей клиента Azure AD не добавляется. приложение Hello можно запрашивать hello пользователя с приложением hello tooinstall инструкции и добавить его tooAzure AD. |
| access_denied |владелец ресурса Hello не дал согласие. |Hello клиентское приложение может уведомить пользователя hello, он не может продолжена без согласия пользователя hello. |
| unsupported_response_type |сервер авторизации Hello не поддерживает тип ответа hello в запросе hello. |Исправить и повторно отправьте запрос hello. Это ошибка разработки, которая, как правило, обнаруживается во время первоначального тестирования. |
| server_error |Произошла непредвиденная ошибка сервера Hello. |Повторите запрос hello. Эти ошибки могут возникать в связи с временными условиями. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временной ошибки tooa. |
| temporarily_unavailable |Hello server временно — слишком занят, toohandle hello запрос. |Повторите запрос hello. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временного состояния ошибки tooa. |
| invalid_resource |Hello целевой ресурс является недопустимым, так как он не существует, Azure AD не удается найти или настроена неправильно. |Это означает, что ресурс hello, если он существует, не был настроен в клиенте hello. приложение Hello можно предлагать hello с инструкциями по установке приложения hello и его добавления tooAzure AD. |

## Проверка токена идентификатор hello
Получает маркер идентификатора не достаточно tooauthenticate hello пользователем. Необходимо также проверить подпись маркер идентификатора hello и проверить hello утверждения маркера hello в соответствии с требованиями приложения. Конечная точка v2.0 Hello использует [веб-маркеры JSON (JWT)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) и открытый ключ шифрования toosign маркеры и убедитесь, что они являются допустимыми.

Вы можете маркер идентификатора toovalidate hello в клиентском коде, но принято toosend hello идентификатор маркера tooa серверных и выполнять проверки hello существует. После проверки предоставленных hello подпись токена идентификатор hello потребуется tooverify несколько утверждений. Дополнительные сведения, включая несколько о [проверку маркеров](active-directory-v2-tokens.md#validating-tokens) и [важные сведения о смене ключей подписывания](active-directory-v2-tokens.md#validating-tokens), разделе hello [v2.0 маркеры ссылка](active-directory-v2-tokens.md). Мы рекомендуем использовать tooparse библиотеки и проверки токенов. Для большинства языков и платформ доступна по крайней мере одна такая библиотека.
<!--TODO: Improve hello information on this-->

Вы также можете toovalidate дополнительные утверждения, в зависимости от вашего сценария. Ниже приведены некоторые из стандартных проверок:

* Убедитесь, что hello пользователя или организации зарегистрировался для приложения hello.
* Убедитесь, что этот пользователь hello необходимые права или авторизации.
* Обеспечение определенной строгости аутентификации, например Многофакторной идентификации.

Дополнительные сведения об утверждениях hello в маркер идентификатора см. в разделе hello [конечной точки v2.0 маркеры ссылка](active-directory-v2-tokens.md).

После полной проверки маркер идентификатора hello можно начать сеанс с пользователем hello. Используйте утверждения hello в hello идентификатор маркера tooget сведения о hello пользователя в приложении. Эти сведения можно использовать для отображения, записей, авторизации и т. д.

## Отправка запроса на выход
При необходимости toosign выход hello пользователя из приложения, он не достаточно tooclear файлов cookie вашего приложения или в противном случае завершение сеанса пользователя hello. Также необходимо перенаправить toosign hello пользователя toohello v2.0 конечной точки ожидания. Если этого не сделать, hello пользователя повторно проверяет подлинность tooyour приложения без ввода учетных данных, так как они будут иметь допустимый единого входа в сеанс с конечной точкой v2.0 hello.

Вы можете перенаправлять пользователя toohello hello `end_session_endpoint` указаны в документе метаданных OpenID Connect hello:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/logout?
post_logout_redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
```

| Параметр | Условие | Описание |
| ----------------------- | ------------------------------- | ------------ |
| post_logout_redirect_uri | Рекомендуется | URL-адрес Hello hello пользователя является перенаправленный tooafter успешно выполняется выход. Если hello не указан, hello пользователь увидит универсальное сообщение, которое создается hello v2.0 конечной точкой. Этот URL-адрес должен соответствовать одному из перенаправления hello зарегистрировано URIs для приложения на портал регистрации приложения hello.  |

## Единый выход
При перенаправлении hello пользователя toohello `end_session_endpoint`, конечная точка v2.0 hello очищает сеанса hello пользователя из браузера hello. Тем не менее пользователь hello может находиться в системе tooother приложений, использующих учетные записи Майкрософт для проверки подлинности. tooenable этих приложений toosign hello пользователя одновременно, конечная точка v2.0 hello отправляет HTTP-GET запроса toohello зарегистрированные `LogoutUrl` всех приложений hello hello пользователя подключен к сети для. Приложения должен вернуть запрос toothis сняв сеансов идентифицирует пользователя hello и возвращая `200` ответа.  При желании единого входа toosupport помещает в приложении, необходимо реализовать такие `LogoutUrl` в код приложения.  Можно задать hello `LogoutUrl` из портала регистрации приложения hello.

## Схема протокола: получение маркера
Многие веб-приложения должны toonot только войти hello пользователь в, но tooaccess веб-службы, от имени пользователя hello с помощью OAuth. Этот сценарий объединяет OpenID Connect для проверки подлинности пользователя при получении авторизации одновременно маркеры, которые можно использовать tooget доступа кода при использовании потока кода авторизации OAuth hello.

Здравствуйте полного OpenID Connect вход и получения маркера потока выглядит примерно toohello на следующей диаграмме. Чтобы описать каждый шаг подробно в последующих разделах статьи hello hello.

![Протокол OpenID Connect: получение маркера](../../media/active-directory-v2-flows/convergence_scenarios_webapp_webapi.png)

## Получение маркеров доступа
tooacquire маркеры доступа, измените запрос hello вход:

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e        // Your registered Application ID
&response_type=id_token%20code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F       // Your registered redirect URI, URL encoded
&response_mode=form_post                              // 'query', 'form_post', or 'fragment'
&scope=openid%20                                      // Include both 'openid' and scopes that your app needs  
offline_access%20                                         
https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345                                          // Any value, provided by your app
&nonce=678910                                         // Any value, provided by your app
```

> [!TIP]
> Щелкните следующие ссылки tooexecute hello этого запроса. После входа в браузере — перенаправленный toohttps://localhost/myapp/, маркер идентификатора и кода в адресную строку hello. Обратите внимание, что в этом запросе используется `response_mode=query` (исключительно в демонстрационных целях). Мы рекомендуем использовать `response_mode=form_post`.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token%20code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

Включив области разрешений в запросе hello и с помощью `response_type=id_token code`, конечная точка v2.0 hello гарантирует, что hello пользователь согласился toohello разрешениями, перечисленными в hello `scope` параметр запроса. Он возвращает tooyour приложения авторизации кода tooexchange маркера доступа.

### Успешный ответ
Успешный ответ с использованием `response_mode=form_post` выглядит следующим образом.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNB...&code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...&state=12345
```

| Параметр | Описание |
| --- | --- |
| id_token |Здравствуйте, маркер идентификатора, hello запрошенного приложения. Можно использовать удостоверение маркера tooverify hello hello идентификатор пользователя и начать сеанс с пользователем hello. Вы найдете дополнительные сведения о маркеров безопасности и их содержимое в hello [конечной точки v2.0 маркеры ссылка](active-directory-v2-tokens.md). |
| Код |Здравствуйте, приложение hello запрошенный код авторизации. приложение Hello можно использовать toorequest код авторизации hello маркер доступа для hello целевого ресурса. Код авторизации имеет очень небольшой срок действия. Как правило, он действует в течение 10 минут. |
| state |Если параметр состояния включается в запрос hello, hello одинаковое значение должно отображаться в ответ hello. приложение Hello следует Проверьте идентичность значений состояния hello hello запроса и ответа. |

### Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello URI перенаправления, чтобы hello приложение может обрабатывать их соответствующим образом. Сообщение об ошибке выглядит следующим образом.

```
POST /myapp/ HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded

error=access_denied&error_description=the+user+canceled+the+authentication
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки, который можно использовать типы tooclassify возникающие ошибки и tooreact tooerrors. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello. |

Описание возможных кодов ошибок и рекомендуемые ответы клиента см. в разделе [Коды ошибок конечной точки авторизации](#error-codes-for-authorization-endpoint-errors).

При наличии кода авторизации и маркер идентификатора, можно войти пользователя hello и получить токены доступа от их имени. пользователь toosign hello в, необходимо проверить маркер идентификатора hello [точно так, как описано](#validate-the-id-token). tooget маркеры доступа, следуйте hello действия, описанные в нашем [документации по протоколу OAuth](active-directory-v2-protocols-oauth-code.md#request-an-access-token).
