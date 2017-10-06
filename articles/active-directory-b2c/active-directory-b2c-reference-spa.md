---
title: "Azure Active Directory B2C. Одностраничные приложения, использующие неявный поток | Документация Майкрософт"
description: "Узнайте, как toobuild одностраничного приложения непосредственно с помощью OAuth 2.0 неявного потока с Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: a45cc74c-a37e-453f-b08b-af75855e0792
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: parakhj
ms.openlocfilehash: 5e52abc18fe545f0f6d1745cdb2ea42c5b2698cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-single-page-app-sign-in-by-using-oauth-20-implicit-flow"></a>Azure AD B2C. Вход в одностраничные приложения с помощью неявного потока OAuth 2.0

> [!NOTE]
> Эта функция предоставляется в предварительной версии.
> 

Многие современные приложения содержат интерфейсное одностраничное приложение, созданное преимущественно на языке JavaScript. Часто приложение hello записывается с помощью платформы наподобие AngularJS, Ember.js или Durandal. При аутентификации одностраничные и другие приложения JavaScript, которые запускаются в основном в браузере, сталкиваются с некоторыми дополнительными проблемами:

* Hello характеристики безопасности этих приложений, значительно отличаются от традиционных серверных веб-приложений.
* Многие серверы авторизации и поставщики удостоверений не поддерживают запросы на общий доступ к ресурсам независимо от источника (CORS).
* Перенаправления браузера полностраничном вне приложение hello может быть значительно вмешивается в работу toohello взаимодействие с пользователем.

toosupport эти приложения Azure Active Directory B2C (Azure AD B2C) использует неявного потока OAuth 2.0 hello. поток неявного предоставления авторизации OAuth 2.0 Hello описан в [статьи 4.2 спецификации OAuth 2.0 hello](http://tools.ietf.org/html/rfc6749). В неявного потока приложение hello получение маркеров непосредственно из hello конечную точку, без любого сервера на сервер exchange авторизации Azure Active Directory (Azure AD). Все логики проверки подлинности и обработки принимает сеанса поместите полностью в клиенте JavaScript hello без перенаправления дополнительных страниц.

Azure AD B2C расширяет возможности стандартных toomore неявного потока OAuth 2.0 hello чем простой проверки подлинности и авторизации. Azure AD B2C вводит hello [параметра политики](active-directory-b2c-reference-policies.md). При использовании параметра политики hello, можно использовать tooadd взаимодействие с пользователем; tooyour приложения, такие как OAuth 2.0 регистрации, вход и управление профилями пользователей. В этой статье мы покажем как toouse hello неявного потока и Azure AD tooimplement каждого этих функций в одной страницы приложения. toohelp приступить к работе, ознакомьтесь с нашей [Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi) и [Microsoft .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi) образцов.

В запросах HTTP пример hello в этой статье, мы используем наш каталог Azure AD B2C образцов, **fabrikamb2c.onmicrosoft.com**. Также используются наши примеры приложения и политик. Попробуйте hello запросы вручную с помощью этих значений или их можно заменить собственные значения.
Узнайте, каким образом слишком[собственного каталога Azure AD B2C, приложения и политики](#use-your-own-b2c-tenant).


## <a name="protocol-diagram"></a>Схема протокола

Hello неявного входа потока будет выглядеть примерно так hello следующий рисунок. Каждый шаг описан более подробно в статье hello.

![Дорожки OpenID Connect](../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## <a name="send-authentication-requests"></a>Отправка запросов проверки подлинности
Когда веб-приложения требуется tooauthenticate пользователя hello и выполнить политику, он направляет пользователя toohello hello `/authorize` конечной точки. Это интерактивный часть потока hello hello где hello пользователь выполняет действие, в зависимости от политики hello. Hello пользователь получает идентификатор маркера из конечной точки Azure AD hello.

В этом запросе hello клиент указывает в hello `scope` параметр hello разрешения, необходимость tooacquire от пользователя hello. В hello `p` параметра, он указывает tooexecute политики hello. Hello следующих трех примерах (с разбиением на строки для удобства чтения) каждого с помощью другой политики. tooget вид, как работает каждый запрос, повторите запрос вставки hello в браузере и запустив его.

### <a name="use-a-sign-in-policy"></a>Пример с политикой входа в систему
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_in
```

### <a name="use-a-sign-up-policy"></a>Пример с политикой регистрации
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_sign_up
```

### <a name="use-an-edit-profile-policy"></a>Пример с политикой изменения профиля
```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=id_token+token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&response_mode=fragment
&scope=openid%20offline_access
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&p=b2c_1_edit_profile
```

| Параметр | Обязательный? | Описание |
| --- | --- | --- |
| client_id |Обязательно |Идентификатор приложения Hello назначен tooyour приложения hello [портал Azure](https://portal.azure.com). |
| response_type |Обязательно |Должен включать `id_token` для входа в OpenID Connect. Он также может включать тип ответа hello `token`. Если вы используете `token`, приложение немедленно могут получить токен доступа от hello авторизации конечной точки, не внося второй toohello запроса конечной точки проверки подлинности.  Если вы используете hello `token` тип ответа, hello `scope` параметр должен содержать область, которая указывает, какой ресурс tooissue hello токен для. |
| redirect_uri |Рекомендуется |URI приложения, где запросы проверки подлинности можно отправленных и полученных приложения перенаправления Hello. Его должен точно соответствовать одно перенаправление hello URI, которые зарегистрированы в портале hello, за исключением того, он должен быть в кодировке URL. |
| response_mode |Рекомендуется |Указывает метод toouse toosend hello результирующий токен задней tooyour приложение hello.  Для неявных потоков используйте `fragment`. |
| scope |Обязательно |Список областей с разделителями-пробелами. Значение одной области указывает tooAzure AD обоих hello разрешений, которые запрашиваются. Hello `openid` область указывает toosign разрешение в hello пользователей и получения данных о пользователе hello в форме hello маркеров безопасности. (Мы рассмотрим это более далее в статье hello.) Hello `offline_access` область является необязательным для веб-приложений. Он показывает, что приложение требует токен обновления для tooresources долгоживущие доступа. |
| state |Рекомендуется |Значение, включенных в запрос hello, которое также возвращается в ответ на токен hello. Он может быть строка любое содержимое, которое следует toouse. Как правило, используется значение созданный случайным образом уникальный, tooprevent атак с подделкой межсайтовых запросов. Hello состояния является также используется tooencode сведения о состоянии пользователя hello в приложение hello до возникновения hello запрос проверки подлинности, как страница hello они находились на. |
| nonce |Обязательно |Значение, включенных в запрос hello (созданных в ходе приложение hello), включенный в hello полученный маркер идентификатора как утверждения. приложение Hello можно затем удостоверьтесь, что атак воспроизведения токена значение toomitigate. Как правило значение hello является случайного уникальный строкой, можно использовать tooidentify hello источник запроса hello. |
| p |Обязательно |tooexecute политики Hello. Он является hello имя политики, которая создается в клиенте Azure AD B2C. Имя политики Hello значение должна начинаться с **b2c\_1\_**. Дополнительные сведения см. в [документации по встроенным политикам Azure AD B2C](active-directory-b2c-reference-policies.md). |
| prompt |Необязательно |взаимодействие с пользователем, необходимый тип Hello. В настоящее время является единственным допустимым значением hello `login`. Это заставляет пользователя tooenter hello свои учетные данные в этот запрос. Единый вход не сработает. |

На этом этапе hello пользователя запрашивается toocomplete hello политики рабочего процесса. Это может вызвать hello пользователь вводит свое имя пользователя и пароль, вход удостоверений из социальных сетей, зарегистрировавшись для каталога hello или любое другое число шагов. Действие пользователя зависит от того, как определяется политика hello.

После завершения политики hello hello пользователя Azure AD возвращает приложении tooyour ответа hello значения, используемые для `redirect_uri`. Она использует hello метода, указанного в hello `response_mode` параметра. Hello ответа ровно hello же для каждого hello действия сценариев пользователя, независимо от политики hello, который был выполнен.

### <a name="successful-response"></a>Успешный ответ
Успешный ответ, который использует `response_mode=fragment` и `response_type=id_token+token` выглядит в разрывы строк для удобочитаемости hello следующим:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope="90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6 offline_access",
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
```

| Параметр | Описание |
| --- | --- |
| access_token |маркер доступа Hello, hello запрошенного приложения.  не следует декодировать или проверять Hello маркер доступа. Его можно рассматривать как непрозрачную строку. |
| token_type |значение типа токена Hello. Hello вводить только что поддерживает Azure AD является носителя. |
| expires_in |Hello продолжительность hello токен доступа является допустимым (в секундах). |
| scope |Hello областям hello маркер является допустимым для. Также можно использовать токены toocache областей для последующего использования. |
| id_token |Здравствуйте, маркер идентификатора, hello запрошенного приложения. Можно использовать удостоверение маркера tooverify hello hello идентификатор пользователя и начать сеанс с пользователем hello. Дополнительные сведения о маркеров безопасности и их содержимое. в разделе hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md). |
| state |Если `state` параметр включен в запрос hello hello же значение должно содержаться в ответе hello. Hello приложения следует убедиться, что hello `state` значения в hello запроса и ответа идентичны. |

### <a name="error-response"></a>Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello URI перенаправления, чтобы hello приложение может обрабатывать их соответствующим образом:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=access_denied
&error_description=the+user+canceled+the+authentication
&state=arbitrary_data_you_can_receive_in_the_response
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки используемых типов tooclassify возникающие ошибки. Код ошибки hello также можно использовать для обработки ошибок. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello. |
| state |См. полное описание hello в предшествующей таблице hello. Если `state` параметр включен в запрос hello hello же значение должно содержаться в ответе hello. Hello приложения следует убедиться, что hello `state` значения в hello запроса и ответа идентичны.|

## <a name="validate-hello-id-token"></a>Проверка токена идентификатор hello
Получает маркер идентификатора не хватает tooauthenticate hello пользователем. Проверить подпись маркер идентификатора hello и проверить hello утверждения маркера hello в соответствии с требованиями приложения. Использует Azure AD B2C [веб-маркеры JSON (JWT)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) и открытый ключ шифрования toosign маркеры и убедитесь, что они являются допустимыми.

Многие библиотеки с открытым исходным кодом, доступных для проверки маркеров JWT, в зависимости от языка hello вы предпочитаете toouse. Рекомендуется изучить доступные библиотеки с открытым исходным кодом, а не реализовывать логику проверки самостоятельно. Можно использовать информацию hello в toohelp этой статьи вы узнаете, как tooproperly использование этих библиотек.

Служба Azure AD B2C имеет конечную точку метаданных OpenID Connect. Приложение может использовать сведения о Azure AD B2C toofetch конечных точках hello во время выполнения. Эти сведения включают конечные точки, содержимое маркеров и ключи подписи маркеров. Для каждой политики в клиенте Azure AD B2C есть собственный документ метаданных JSON. Например документ метаданных hello политики b2c_1_sign_in hello в клиенте fabrikamb2c.onmicrosoft.com hello расположен по адресу:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/v2.0/.well-known/openid-configuration?p=b2c_1_sign_in`

Одно из свойств hello этого документа конфигурации — hello `jwks_uri`. значение Hello приветствия бы одной политике:

`https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/discovery/v2.0/keys?p=b2c_1_sign_in`

toodetermine, какая политика была toosign используется маркер идентификатора (и где toofetch hello метаданные из), у вас есть два варианта. Во-первых, имя политики hello включается в hello `acr` утверждения в `id_token`. Сведения о как tooparse hello утверждений от маркер идентификатора содержатся hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md). Другой вариант — tooencode политики hello в значение hello hello `state` параметра при выполнении запроса hello. Затем декодировать hello `state` toodetermine параметра политики, был использован. Каждый из этих методов является допустимым.

После приобретен hello документов метаданных из конечной точки метаданных OpenID Connect hello можно использовать hello RSA 256 toovalidate открытых ключей (находится в этой конечной точке) hello подпись токена идентификатор hello. В каждый момент времени в этой конечной точке может находиться множество ключей, каждый из которых определяется `kid`. Заголовок Hello `id_token` также содержит `kid` утверждения. Он указывает, какой из этих ключей был маркер идентификатора используется toosign hello. Дополнительные сведения, включая изучение [проверку маркеров](active-directory-b2c-reference-tokens.md#token-validation), в разделе hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md).
<!--TODO: Improve hello information on this-->

После проверки hello подпись токена идентификатор hello несколько утверждений требуется проверка. Например:

* Проверка hello `nonce` утверждения tooprevent атак с повторением токенов. Его значение должно быть указанный запрос hello вход.
* Проверка hello `aud` утверждения, hello маркер идентификатора tooensure был выпущен для приложения. Его значение должно быть Идентификатором приложения hello приложения.
* Проверка hello `iat` и `exp` утверждений tooensure, hello маркер идентификатора не истек.

Некоторые дополнительные проверки, которые необходимо выполнить подробно описывается в hello [OpenID подключения Core Spec](http://openid.net/specs/openid-connect-core-1_0.html). Можно также toovalidate дополнительные утверждения, в зависимости от вашего сценария. Ниже приведены некоторые из стандартных проверок:

* Обеспечение hello пользователю или организации зарегистрировался для приложения hello.
* Гарантирует, что hello пользователь имеет необходимые права и привилегии.
* Обеспечение определенного уровня аутентификации, например с помощью Многофакторной идентификации Azure.

Дополнительные сведения об утверждениях hello в маркер идентификатора см. в разделе hello [ссылку маркера Azure AD B2C](active-directory-b2c-reference-tokens.md).

После полной проверки маркер идентификатора hello можно начать сеанс с пользователем hello. В приложении используйте hello утверждений в hello идентификатор маркера tooobtain сведения о пользователе hello. Эти сведения можно использовать для отображения, записей, авторизации и т. д.

## <a name="get-access-tokens"></a>Получение маркеров доступа
Если hello единственное является вашей toodo потребностей приложения web выполнение политик, можно пропустить hello следующие несколько разделов. Hello сведения в следующих разделах hello, применимые только tooweb приложения, требующие проверку подлинности toomake вызовы tooa веб-API, и которой защищаются с помощью Azure AD B2C.

Теперь, когда вы вышли из пользователя hello в tooyour одностраничного приложения, можно получить токены доступа для вызова веб-API, защищенные Azure AD. Даже если вы уже получили маркер с помощью hello `token` тип ответа можно использовать этот метод tooacquire токены дополнительные ресурсы без перенаправления toosign пользователя hello в еще раз.

В потоке приложения обычно web это делается, делая toohello запроса `/token` конечной точки.  Однако hello конечные точки не не CORS запросов поддержки, так что AJAX вызывает tooget и токены обновления являются обязательными. Вместо этого можно использовать hello неявного потока в скрытый HTML iframe элемент tooget новые маркеры для других веб-API. Ниже приведен пример (разрывы строк — для удобства чтения):

```

https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6
&response_type=token
&redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
&response_mode=fragment
&state=arbitrary_data_you_can_receive_in_the_response
&nonce=12345
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
&p=b2c_1_sign_in
```

| Параметр | Обязательный? | Описание |
| --- | --- | --- |
| client_id |Обязательно |Идентификатор приложения Hello назначен tooyour приложения hello [портал Azure](https://portal.azure.com). |
| response_type |Обязательно |Должен включать `id_token` для входа в OpenID Connect.  Она также может включать тип ответа hello `token`. Если вы используете `token` здесь, приложения могут немедленно получить маркер доступа от hello авторизации конечной точки, не внося второй toohello запроса конечной точки проверки подлинности. Если вы используете hello `token` тип ответа, hello `scope` параметр должен содержать область, которая указывает, какой ресурс tooissue hello токен для. |
| redirect_uri |Рекомендуется |URI приложения, где запросы проверки подлинности можно отправленных и полученных приложения перенаправления Hello. Его должен точно соответствовать один hello перенаправления зарегистрирован в портале hello идентификаторы URI, за исключением того, он должен быть в кодировке URL. |
| scope |Обязательно |Список областей с разделителями-пробелами.  Для получения маркеров, включают все области, необходимые для hello предназначен ресурсов. |
| response_mode |Рекомендуется |Указывает метод hello, используемые toosend hello итоговое маркера задней tooyour приложение.  Возможные значения: `query`, `form_post` или `fragment`. |
| state |Рекомендуется |Значение, включенных в запрос hello, возвращаемых в ответ на токен hello.  Он может быть строка любое содержимое, которое следует toouse.  Как правило, используется значение созданный случайным образом уникальный, tooprevent атак с подделкой межсайтовых запросов.  состояние Hello также является используется tooencode сведения о состоянии пользователя hello в приложение hello, до возникновения hello запрос проверки подлинности. Например, hello страницы или представления hello пользователя была. |
| nonce |Обязательно |Значение, включенных в запрос hello, созданное приложение hello, входящую в hello полученный маркер идентификатора как утверждения.  приложение Hello можно затем удостоверьтесь, что атак воспроизведения токена значение toomitigate. Как правило значение hello — случайным образом уникальный строка, определяющая источник hello hello запроса. |
| prompt |Обязательно |использовать токены toorefresh и get в скрытого iframe, `prompt=none` tooensure, hello iframe не возникли затруднения на страницу входа hello и возвращается немедленно. |
| login_hint |Обязательно |toorefresh и get токенов в скрытого iframe, включите пользователя hello hello в это указание toodistinguish между несколько сеансов, которые hello пользователя может иметь в определенный момент времени. Имя пользователя hello можно извлечь из более ранних вход с помощью hello `preferred_username` утверждения. |
| domain_hint |Обязательно |Может иметь значение `consumers` или `organizations`.  Для обновления и получения токенов в скрытого iframe, необходимо включить hello `domain_hint` значение в запросе hello.  Извлеките hello `tid` утверждение от токен идентификатор hello ранее вход toodetermine какие toouse значение.  Если hello `tid` утверждения, значение — `9188040d-6c67-4c5b-b112-36a304b66dad`, используйте `domain_hint=consumers`.  Или используйте `domain_hint=organizations`. |

Путем установки hello `prompt=none` параметра, этот запрос либо выполняется успешно или прекращается немедленно и возвращает tooyour приложения.  Успешный ответ отправляется tooyour приложения в указанном hello перенаправление URI, с помощью метода hello, указанного в hello `response_mode` параметра.

### <a name="successful-response"></a>Успешный ответ
Успешный ответ с использованием `response_mode=fragment` выглядит следующим образом:

```
GET https://aadb2cplayground.azurewebsites.net/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=arbitrary_data_you_sent_earlier
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fapi.contoso.com%2Ftasks.read
```

| Параметр | Описание |
| --- | --- |
| access_token |токен Hello, hello запрошенного приложения. |
| token_type |Тип токена Hello всегда будет носителя. |
| state |Если `state` параметр включен в запрос hello hello же значение должно содержаться в ответе hello. Hello приложения следует убедиться, что hello `state` значения в hello запроса и ответа идентичны. |
| expires_in |Как долго маркер доступа hello является действительным (в секундах). |
| scope |Hello областям hello токен доступа является действительным для. |

### <a name="error-response"></a>Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello URI перенаправления, чтобы hello приложение может обрабатывать их соответствующим образом.  Для `prompt=none` ожидаемая ошибка выглядит следующим образом:

```
GET https://aadb2cplayground.azurewebsites.net/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Параметр | Описание |
| --- | --- |
| error |Строка кода ошибки, может быть типов используемых tooclassify возникающие ошибки. Также можно использовать tooerrors tooreact строку hello. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello. |

Если эта ошибка возникает в запросе iframe hello, hello пользователь должен интерактивно войти снова tooretrieve новый маркер. Это можно обрабатывать любым способом, который лучше всего подходит для вашего приложения.

## <a name="refresh-tokens"></a>Маркеры обновления
Срок действия маркеров идентификации и доступа достаточно короткий. Приложение должно быть готово toorefresh эти токены периодически.  toorefresh любого типа маркера, выполнять hello скрытого iframe запросе используется в предыдущем примере, с помощью hello `prompt=none` действия параметра toocontrol Azure AD.  tooreceive новый `id_token` значение, равно, что toouse `response_type=id_token` и `scope=openid`и `nonce` параметра.

## <a name="send-a-sign-out-request"></a>Отправка запроса на выход
При необходимости hello toosign выход пользователя из приложения hello перенаправление hello пользователя tooAzure AD toosign out. Если этого не сделать, hello пользователь может быть приложение может tooreauthenticate tooyour без еще раз ввести свои учетные данные. так как они будут иметь действительный сеанс единого входа с Azure AD.

Можно просто перенаправить пользователя toohello hello `end_session_endpoint` , перечисленных в hello того же документа метаданных OpenID Connect описано в [маркер идентификатора hello проверки](#validate-the-id-token). Например:

```
GET https://login.microsoftonline.com/fabrikamb2c.onmicrosoft.com/oauth2/v2.0/logout?
p=b2c_1_sign_in
&post_logout_redirect_uri=https%3A%2F%2Faadb2cplayground.azurewebsites.net%2F
```

| Параметр | Обязательный? | Описание |
| --- | --- | --- |
| p |Обязательно |Hello политики toouse toosign hello выход пользователя из приложения. |
| post_logout_redirect_uri |Рекомендуется |Hello URL-адрес этого hello пользователя должно быть перенаправленный tooafter успешного выхода. Если не указан, Azure AD B2C отображает пользователь toohello универсальное сообщение. |

> [!NOTE]
> Направление hello пользователя toohello `end_session_endpoint` очищает некоторые из одного состояния входа с Azure AD B2C hello пользователя. Тем не менее он не подписывать hello выход пользователя из сеанса поставщика удостоверений из социальных сетей hello пользователя. Если hello пользователь выбирает hello же определения поставщика при последующем входе в систему, hello пользователя выполняется повторная проверка подлинности, не вводя свои учетные данные. Если пользователю toosign приложения Azure AD B2C, оно означает, что им нужен toocompletely выхода свою учетную запись Facebook, например. Тем не менее, для локальных учетных записей пользователя hello сеанс будет завершен правильно.
> 
> 

## <a name="use-your-own-azure-ad-b2c-tenant"></a>Использование собственного клиента Azure AD B2C
Эти запросы самостоятельно, выполните tootry hello следующие три шага. Замените примеры значений hello, мы используем в этой статье собственными значениями:

1. [Создайте клиента Azure AD B2C](active-directory-b2c-get-started.md). Используйте имя hello вашего клиента в запросах hello.
2. [Создание приложения](active-directory-b2c-app-registration.md) tooobtain идентификатора приложения и `redirect_uri` значение. Включите в свое приложение веб-приложение или веб-API. При необходимости можно также создать секретный код приложения.
3. [Создание политик](active-directory-b2c-reference-policies.md) tooobtain имена ваших политики.

## <a name="samples"></a>Примеры

* [Создание одностраничного приложения с помощью Node.js](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-nodejs-webapi)
* [Создание одностраничного приложения с помощью .NET](https://github.com/Azure-Samples/active-directory-b2c-javascript-singlepageapp-dotnet-webapi)

