---
title: "aaaSecure приложений на одной странице с помощью неявного потока v2.0 hello Azure AD | Документы Microsoft"
description: "Построение веб-приложения, используя реализацию v2.0 Azure AD hello неявного потока для приложений на одной странице."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 3605931f-dc24-4910-bb50-5375defec6a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 2cdce4eee88be4af54966d15204b79fa4992a58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Протоколы — с помощью неявного потока hello SPAs v2.0
С конечной точкой v2.0 hello пользователи могут входить в одну страницу приложения при помощи личных и рабочих или учебного заведения учетных записей Microsoft.  Одну страницу и другие приложения JavaScript, работающих в основном в браузер гарнитуру несколько интересных решить проблемы при его поступает tooauthentication:

* Hello характеристики безопасности этих приложений, значительно отличаются от традиционных серверные веб-приложений.
* Многие серверы авторизации и поставщики удостоверений не поддерживают запросы CORS.
* Перенаправления браузера по страницам от приложение hello становятся особенно вмешивается в работу toohello взаимодействие с пользователем.

Для этих приложений (подумать: AngularJS, Ember.js, React.js, и т. д) Azure AD поддерживает потока hello неявного предоставления OAuth 2.0.  Описывается Hello неявного потока в hello [спецификации OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.2).  Его основное преимущество является то, что маркеры tooget приложения hello из Azure AD без выполнения внутреннего сервера учетных данных exchange.  Таким образом, toosign приложения hello в пользователя hello, поддержания сеанса и получить токены tooother web API-интерфейсы в течение hello клиентский код JavaScript.  Существуют несколько tootake вопросы безопасности в учетную запись, при использовании неявного потока hello - специально около [клиента](http://tools.ietf.org/html/rfc6749#section-10.3) и [олицетворения пользователя](http://tools.ietf.org/html/rfc6749#section-10.3).

Если требуется неявного потока toouse hello и приложения Azure AD tooadd проверки подлинности tooyour JavaScript, рекомендуется использовать нашей библиотеке открытым исходным кодом JavaScript, [adal.js](https://github.com/AzureAD/azure-activedirectory-library-for-js).  Есть несколько учебников AngularJS [здесь](active-directory-appmodel-v2-overview.md#getting-started) toohelp приступить к работе.  

Однако если вы бы предпочли бы toouse библиотеки в одностраничное приложение и отправки сообщений протокола самостоятельно, выполните действия ниже hello.

> [!NOTE]
> Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.  toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

## Схема протокола
Hello всей неявного входа потока выглядит примерно так - каждое из действий hello подробно рассмотрены ниже.

![Дорожки OpenID Connect](../../media/active-directory-v2-flows/convergence_scenarios_implicit.png)

## Отправить запрос hello вход
tooinitially входа hello пользователя в веб-приложения, можно отправить [OpenID Connect](active-directory-v2-protocols-oidc.md) авторизации запроса и get `id_token` из конечной точки v2.0 hello:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=id_token+token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&response_mode=fragment
&state=12345
&nonce=678910
```

> [!TIP]
> Щелкните ссылку hello под tooexecute этого запроса. После входа в браузере должны быть перенаправлены слишком`https://localhost/myapp/` с `id_token` в адресную строку hello.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=id_token+token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=openid%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Параметр |  | Описание |
| --- | --- | --- |
| tenant |обязательно |Hello `{tenant}` значение в путь hello hello запроса может быть используется toocontrol, которые можно выполнять вход в приложение hello.  Hello допустимые значения: `common`, `organizations`, `consumers`и идентификаторы клиентов.  Дополнительные сведения см. в [описании протоколов](active-directory-v2-protocols.md#endpoints). |
| client_id |обязательно |Идентификатор приложения этот портал регистрации hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) назначенный приложения. |
| response_type |обязательно |Должен включать `id_token` для входа в OpenID Connect.  Он также может включать hello response_type `token`. С помощью `token` здесь позволит вашей tooreceive приложения токен доступа непосредственно из hello конечной точки проверки подлинности без необходимости toomake авторизовать второй toohello запроса конечной точки.  Если вы используете hello `token` response_type, hello `scope` параметр должен содержать, указывающее, какой ресурс tooissue hello токен для области. |
| redirect_uri |рекомендуется |Hello redirect_uri приложения, где запросы проверки подлинности можно отправленных и полученных приложения.  Он должен точно соответствовать одной redirect_uris hello, зарегистрированное в портале hello, за исключением того, он должен быть в кодировке URL-адрес. |
| scope |обязательно |Список областей с разделителями-пробелами.  OpenID Connect, он должен содержать область hello `openid`, что означает разрешение «Вход» toohello пользовательского интерфейса согласия hello.  При необходимости можно также tooinclude hello `email` или `profile` [областей](active-directory-v2-scopes.md) для получения доступа к данным пользователя tooadditional.  Может также включать другие области в запросе согласия toovarious ресурсов этого запроса. |
| response_mode |рекомендуется |Задает метод должен быть используется toosend hello итоговое маркера задней tooyour приложение hello.  Должно быть `fragment` для неявного потока hello. |
| state |рекомендуется |Значение, включенных в запрос hello, также будет возвращаться в ответ на токен hello.  Это может быть строка любого контента.  Как правило, для [предотвращения подделки межсайтовых запросов](http://tools.ietf.org/html/rfc6749#section-10.12)используется генерируемое случайным образом уникальное значение.  Hello вариант, также используется tooencode сведения о состоянии пользователя hello в приложение hello до возникновения hello запрос проверки подлинности, такие как страница hello и представление, в котором они находились на. |
| nonce |обязательно |Значение, включенных в запрос hello, создаваемые приложения hello, которое будут включены в результирующий id_token hello качестве утверждения.  приложение Hello можно затем удостоверьтесь, что атак воспроизведения токена значение toomitigate.  значение Hello обычно является случайным образом уникальный строкой, можно использовать tooidentify hello источник запроса hello. |
| prompt |необязательный |Указывает тип hello это требует взаимодействия с пользователем.  Здравствуйте только допустимые значения в настоящее время: «вход», «нет» и «разрешения».  `prompt=login`будет принудительно hello пользователя tooenter свои учетные данные на этот запрос, Инверсия единого входа на.  `prompt=none`— hello противоположной — он будет убедитесь, что этот пользователь hello не предоставляется все запросы на экран ни при каких обстоятельствах.  Если hello запрос выполнить не удалось автоматически через единый вход, конечная точка v2.0 hello будет возвращена ошибка.  `prompt=consent`будет триггер hello OAuth consent диалоговое окно после hello пользователь выполняет вход, подтверждения приложение hello пользователя toogrant разрешения toohello. |
| login_hint |необязательный |Может быть hello заполнением нулями toopre используется имя пользователя и электронной почты поля адреса hello страница входа для пользователя hello, если вы знаете свое имя пользователя, заранее.  Часто приложения будут использовать этот параметр во время повторной проверки подлинности, уже извлеченных hello имя пользователя из предыдущих вход с помощью hello `preferred_username` утверждения. |
| domain_hint |необязательный |Может использоваться значение `consumers` или `organizations`.  Если включен, он пропускает hello процесса обнаружения на основе электронной почты, пользователь не пройдет на странице входа v2.0 hello начальные tooa немного более упрощенную взаимодействие с пользователем.  Часто приложения будут использовать этот параметр во время повторной проверки подлинности, путем извлечения hello `tid` утверждение от hello id_token.  Если hello `tid` утверждения, значение — `9188040d-6c67-4c5b-b112-36a304b66dad`, следует использовать `domain_hint=consumers`.  Или используйте `domain_hint=organizations`. |

На этом этапе пользователь hello будет задаваемые tooenter своих учетных данных и завершения hello.  Hello конечной точки v2.0 гарантирует, что hello пользователь согласился toohello разрешениями, перечисленными в hello `scope` параметр запроса.  Если пользователь hello не согласился tooany таких разрешений, он запросит hello пользователя tooconsent toohello необходимые разрешения.  Подробные сведения о [разрешениях, согласии на предоставление и мультитенантных приложениях можно найти здесь](active-directory-v2-scopes.md).

Hello пользователь проходит аутентификацию и дает свое согласие, конечная точка v2.0 hello будет выполнен возврат к приложению tooyour ответ в указанном hello `redirect_uri`, с помощью метода hello, указанного в hello `response_mode` параметра.

#### Успешный ответ
Успешный ответ с помощью `response_mode=fragment` и `response_type=id_token+token` выглядит в разрывы строк для удобочитаемости hello следующим:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&token_type=Bearer
&expires_in=3599
&scope=https%3a%2f%2fgraph.microsoft.com%2fmail.read 
&id_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
```

| Параметр | Описание |
| --- | --- |
| access_token |Указывается, если параметр `response_type` содержит значение `token`. маркер доступа Hello, hello запросе приложения в этом случае для hello Microsoft Graph.  маркер доступа Hello не следует декодировать или проверять, его можно рассматривать как непрозрачная строка. |
| token_type |Указывается, если параметр `response_type` содержит значение `token`.  Всегда используется значение `Bearer`. |
| expires_in |Указывается, если параметр `response_type` содержит значение `token`.  Указывает номер hello hello токен действителен, для кэширования в секундах. |
| scope |Указывается, если параметр `response_type` содержит значение `token`.  Указывает, для какой hello access_token допустимы следующие области hello. |
| id_token |id_token Hello, hello запрошенного приложения. Можно использовать hello id_token tooverify hello удостоверение пользователя и начать сеанс с пользователем hello.  Дополнительные сведения о id_tokens и их содержимое включается в hello [v2.0 ссылки на конечную точку token](active-directory-v2-tokens.md). |
| state |Если параметр состояния включается в запрос hello, hello одинаковое значение должно отображаться в ответ hello. приложение Hello следует Проверьте идентичность значений состояния hello hello запроса и ответа. |

#### Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello `redirect_uri` , приложение hello можно обрабатывать их соответствующим образом:

```
GET https://localhost/myapp/#
error=access_denied
&error_description=the+user+canceled+the+authentication
```

| Параметр | Описание |
| --- | --- |
| error |Ошибка строка кода, который может быть используется tooclassify типы ошибок, которые возникают и может быть tooerrors используется tooreact. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |

## Проверка hello id_token
Только получение id_token не достаточно tooauthenticate hello пользователем; необходимо проверить подпись hello id_token и hello утверждения маркера hello в соответствии с требованиями приложения.  Конечная точка v2.0 Hello использует [веб-маркеры JSON (JWT)](http://self-issued.info/docs/draft-ietf-oauth-json-web-token.html) и открытый ключ шифрования toosign маркеры и убедитесь, что они являются допустимыми.

Вы можете toovalidate hello `id_token` в клиентском коде, но распространенной практикой является toosend hello `id_token` tooa внутреннего сервера и выполняет проверку hello существует.  После проверки предоставленных hello подпись hello id_token доступны несколько утверждений будет обязательным tooverify.  Hello в разделе [v2.0 ссылку на маркер](active-directory-v2-tokens.md) Дополнительные сведения, включая [токены проверки](active-directory-v2-tokens.md#validating-tokens) и [важные сведения о подписи смене ключей](active-directory-v2-tokens.md#validating-tokens).  Советуем использовать библиотеку для синтаксического анализа и проверки токенов. Для большинства языков и платформ доступна по крайней мере одна такая библиотека.
<!--TODO: Improve hello information on this-->

Вы также можете toovalidate дополнительные утверждения в зависимости от вашего сценария.  Ниже приведены некоторые из стандартных проверок:

* Обеспечение hello пользователя или организации зарегистрировался для приложения hello.
* Обеспечение hello пользователь имеет правильную авторизации и права доступа
* Обеспечение определенного уровня проверки подлинности, например Многофакторной Идентификации.

Дополнительные сведения об утверждениях hello в id_token см. в разделе hello [v2.0 ссылки на конечную точку token](active-directory-v2-tokens.md).

После полной проверки hello id_token, можно начать сеанс с пользователем hello и применять утверждения hello в hello id_token tooobtain сведения о пользователе hello в вашем приложении.  Эти сведения можно использовать для отображения, записей, авторизации и т. д.

## Получение маркеров доступа
Теперь, когда вы вышли из пользователя hello в приложения на одной странице, можно получить токены доступа для вызова веб-API, защищенные Azure AD, например hello [Microsoft Graph](https://graph.microsoft.io).  Даже если вы уже получили маркер с использованием hello `token` response_type, этот метод tooacquire маркеры tooadditional ресурсы используются без необходимости toosign пользователя tooredirect hello еще раз.

В обычном потоке OpenID Connect и OAuth hello, это делается, делая v2.0 toohello запроса `/token` конечной точки.  Однако hello v2.0 конечные точки не не CORS запросов поддержки, так что AJAX вызывает tooget и токенов обновления выходит за пределы вопрос hello.  Вместо этого можно использовать hello неявного потока в новых маркеров с tooget скрытого iframe для других веб-API: 

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=token
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment
&state=12345&nonce=678910
&prompt=none
&domain_hint=organizations
&login_hint=myuser@mycompany.com
```

> [!TIP]
> Повторите Вставка hello ниже запроса на вкладке браузера & Копировать! (Не забудьте tooreplace hello `domain_hint` и hello `login_hint` значениями hello исправьте значения для пользователя)
> 
> 

```
https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=token&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&response_mode=fragment&state=12345&nonce=678910&prompt=none&domain_hint={{consumers-or-organizations}}&login_hint={{your-username}}
```

| Параметр |  | Описание |
| --- | --- | --- |
| tenant |обязательно |Hello `{tenant}` значение в путь hello hello запроса может быть используется toocontrol, которые можно выполнять вход в приложение hello.  Hello допустимые значения: `common`, `organizations`, `consumers`и идентификаторы клиентов.  Дополнительные сведения см. в [описании протоколов](active-directory-v2-protocols.md#endpoints). |
| client_id |обязательно |Идентификатор приложения этот портал регистрации hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) назначенный приложения. |
| response_type |обязательно |Должен включать `id_token` для входа в OpenID Connect.  Параметр также может содержать другие типы response_types, например `code`. |
| redirect_uri |рекомендуется |Hello redirect_uri приложения, где запросы проверки подлинности можно отправленных и полученных приложения.  Он должен точно соответствовать одной redirect_uris hello, зарегистрированное в портале hello, за исключением того, он должен быть в кодировке URL-адрес. |
| scope |обязательно |Список областей с разделителями-пробелами.  Для получения маркеров, включают все [областей](active-directory-v2-scopes.md) требуется для ресурса hello интерес. |
| response_mode |рекомендуется |Задает метод должен быть используется toosend hello итоговое маркера задней tooyour приложение hello.  Может иметь значение `query`, `form_post` или `fragment`. |
| state |рекомендуется |Значение, включенных в запрос hello, также будет возвращаться в ответ на токен hello.  Это может быть строка любого контента.  Как правило, с целью предотвращения подделки межсайтовых запросов используется генерируемое случайным образом уникальное значение.  Hello вариант, также используется tooencode сведения о состоянии пользователя hello в приложение hello до возникновения hello запрос проверки подлинности, такие как страница hello и представление, в котором они находились на. |
| nonce |обязательно |Значение, включенных в запрос hello, создаваемые приложения hello, которое будут включены в результирующий id_token hello качестве утверждения.  приложение Hello можно затем удостоверьтесь, что атак воспроизведения токена значение toomitigate.  значение Hello обычно является случайным образом уникальный строкой, можно использовать tooidentify hello источник запроса hello. |
| prompt |обязательно |Для обновления & получение маркеров в скрытого iframe, следует использовать `prompt=none` tooensure, hello iframe завис на страницу входа v2.0 hello и возвращается немедленно. |
| login_hint |обязательно |Обновление и получение маркеров в скрытого iframe, необходимо включить пользователя hello hello в это указание в порядке toodistinguish между несколько сеансов пользователя hello возможно, в определенный момент времени. Hello username можно извлечь из предыдущих вход с помощью hello `preferred_username` утверждения. |
| domain_hint |обязательно |Может использоваться значение `consumers` или `organizations`.  Обновление и получение маркеров в скрытого iframe, необходимо включить в запрос hello hello domain_hint.  Следует извлечь hello `tid` утверждение от id_token hello из предыдущих toodetermine входа в какие toouse значение.  Если hello `tid` утверждения, значение — `9188040d-6c67-4c5b-b112-36a304b66dad`, следует использовать `domain_hint=consumers`.  Или используйте `domain_hint=organizations`. |

Благодарим вас toohello `prompt=none` , этот запрос будет либо успешно или моментально завершаются ошибкой и возврата tooyour приложения.  Успешный ответ будет отправляться tooyour приложения в указанном hello `redirect_uri`, с помощью метода hello, указанного в hello `response_mode` параметра.

#### Успешный ответ
Успешный ответ с использованием метода `response_mode=fragment` выглядит следующим образом:

```
GET https://localhost/myapp/#
access_token=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
&state=12345
&token_type=Bearer
&expires_in=3599
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read
```

| Параметр | Описание |
| --- | --- |
| access_token |токен Hello, hello запрошенного приложения. |
| token_type |Всегда будет использоваться значение `Bearer`. |
| state |Если параметр состояния включается в запрос hello, hello одинаковое значение должно отображаться в ответ hello. приложение Hello следует Проверьте идентичность значений состояния hello hello запроса и ответа. |
| expires_in |Как долго маркер доступа hello является действительным (в секундах). |
| scope |Hello областям hello токен доступа является действительным для. |

#### Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello `redirect_uri` , приложение hello можно обрабатывать их соответствующим образом.  В случае hello `prompt=none`, будет ожидаемой ошибкой:

```
GET https://localhost/myapp/#
error=user_authentication_required
&error_description=the+request+could+not+be+completed+silently
```

| Параметр | Описание |
| --- | --- |
| error |Ошибка строка кода, который может быть используется tooclassify типы ошибок, которые возникают и может быть tooerrors используется tooreact. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |

Если эта ошибка возникает в запросе iframe hello, hello пользователь должен интерактивно войти снова tooretrieve новый маркер.  Можно выбрать этот вариант toohandle в так, как лучше всего подходит для вашего приложения.

## Обновление маркеров
Оба `id_token`s и `access_token`s будут действительны в течение короткого промежутка времени, поэтому приложение должно быть готово toorefresh эти токены периодически.  toorefresh тип маркера, можно выполнить hello скрытого iframe запросе выше с помощью hello `prompt=none` параметр поведение toocontrol Azure AD.  Если требуется, чтобы tooreceive новый `id_token`, быть toouse убедиться, что `response_type=id_token` и `scope=openid`, а также `nonce` параметр.

## Отправка запроса на выход
Hello OpenIdConnect `end_session_endpoint` позволяет вашего приложения toosend запроса toohello v2.0 конечной точки tooend сеанса и очистить файлы cookie пользователя задать hello v2.0 конечной точкой.  toofully входа пользователя из веб-приложения, приложение должно завершить собственный сеанс с пользователем hello (обычно по очистке кэша маркера или удаления файлов cookie) и последующего перенаправления hello браузер, чтобы:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/logout?post_logout_redirect_uri=https://localhost/myapp/
```

| Параметр |  | Описание |
| --- | --- | --- |
| tenant |обязательно |Hello `{tenant}` значение в путь hello hello запроса может быть используется toocontrol, которые можно выполнять вход в приложение hello.  Hello допустимые значения: `common`, `organizations`, `consumers`и идентификаторы клиентов.  Дополнительные сведения см. в [описании протоколов](active-directory-v2-protocols.md#endpoints). |
| post_logout_redirect_uri | рекомендуется | URL-адрес Hello hello пользователя должно быть возвращено, что завершения tooafter выхода. Это значение должно соответствовать одному из перенаправления hello зарегистрировано URIs для приложения hello. Если не включен, пользователь hello отображается универсальное сообщение hello v2.0 конечной точкой. |
