---
title: "версия 2.0 aaaAzure AD потока кода авторизации OAuth | Документы Microsoft"
description: "Построение веб-приложений с помощью Azure AD реализации протокола проверки подлинности hello OAuth 2.0."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: ae1d7d86-7098-468c-aa32-20df0a10ee3d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: dee58f2f5c627fef35cae279349728c3c7bf9421
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Протоколы версии 2.0 — поток кода авторизации OAuth 2.0
предоставления кода авторизации Hello OAuth 2.0 может использоваться в приложениях, установленных на устройстве toogain доступа tooprotected ресурсы, такие как веб-API.  С помощью реализации hello приложения модель v2.0 OAuth 2.0, можно добавить вход и tooyour мобильных и настольных приложений, доступ к API.  В этом руководстве не зависит от языка и описывается способ toosend и получать сообщения HTTP без использования нашей библиотек с открытым исходным кодом.

> [!NOTE]
> Не все сценарии Azure Active Directory и возможности поддерживаются hello v2.0 конечной точкой.  toodetermine, если необходимо использовать конечную точку v2.0 hello, прочтите сведения о [ограничения v2.0](active-directory-v2-limitations.md).
> 
> 

Hello потока кода авторизации OAuth 2.0 в описан в разделе [раздел 4.1 спецификации OAuth 2.0 hello](http://tools.ietf.org/html/rfc6749).  Это используется tooperform проверки подлинности и авторизации в hello большую часть типов приложений, включая [веб-приложений](active-directory-v2-flows.md#web-apps) и [изначально установленные приложения](active-directory-v2-flows.md#mobile-and-native-apps).  Позволяет приложениям toosecurely получить access_tokens, который может быть tooaccess используемые ресурсы, которые защищаются с использованием конечной точки v2.0 hello.  

## Схема протокола
На высоком уровне hello потока вся проверка подлинности для приложения собственный или мобильный немного выглядит следующим образом:

![Поток кода проверки подлинности OAuth](../../media/active-directory-v2-flows/convergence_scenarios_native.png)

## Запрос кода авторизации
поток authorization code Hello начинается с клиента hello направления hello пользователя toohello `/authorize` конечной точки.  В данном запросе клиента hello указывает hello разрешениях tooacquire hello пользователя:

```
// Line breaks for legibility only

https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&response_type=code
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&response_mode=query
&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&state=12345
```

> [!TIP]
> Щелкните ссылку hello под tooexecute этого запроса. После входа в браузере должны быть перенаправлены слишком`https://localhost/myapp/` с `code` в адресную строку hello.
> <a href="https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&response_type=code&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F&response_mode=query&scope=openid%20offline_access%20https%3A%2F%2Fgraph.microsoft.com%2Fmail.read&state=12345" target="_blank">https://login.microsoftonline.com/common/oauth2/v2.0/authorize...</a>
> 
> 

| Параметр |  | Описание |
| --- | --- | --- |
| tenant |обязательно |Hello `{tenant}` значение в путь hello hello запроса может быть используется toocontrol, которые можно выполнять вход в приложение hello.  Hello допустимые значения: `common`, `organizations`, `consumers`и идентификаторы клиентов.  Дополнительные сведения см. в [описании протоколов](active-directory-v2-protocols.md#endpoints). |
| client_id |обязательно |Идентификатор приложения этот портал регистрации hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) назначенный приложения. |
| response_type |обязательно |Необходимо включить `code` для потока кода авторизации hello. |
| redirect_uri |рекомендуется |Hello redirect_uri приложения, где запросы проверки подлинности можно отправленных и полученных приложения.  Он должен точно соответствовать одной redirect_uris hello, зарегистрированное в портале hello, за исключением того, он должен быть в кодировке URL-адрес.  Для собственного и мобильных приложений, следует использовать значение по умолчанию hello `https://login.microsoftonline.com/common/oauth2/nativeclient`. |
| scope |обязательно |Разделенный пробелами список [областей](active-directory-v2-scopes.md) нужных hello tooconsent пользователя для. |
| response_mode |рекомендуется |Задает метод должен быть используется toosend hello итоговое маркера задней tooyour приложение hello.  Может иметь значение `query` или `form_post`. |
| state |рекомендуется |Значение, включенных в запрос hello, также будет возвращаться в ответ на токен hello.  Это может быть строка любого контента.  Как правило, для [предотвращения подделки межсайтовых запросов](http://tools.ietf.org/html/rfc6749#section-10.12)используется генерируемое случайным образом уникальное значение.  Hello вариант, также используется tooencode сведения о состоянии пользователя hello в приложение hello до возникновения hello запрос проверки подлинности, такие как страница hello и представление, в котором они находились на. |
| prompt |необязательный |Указывает тип hello это требует взаимодействия с пользователем.  Здравствуйте только допустимые значения в настоящее время: «вход», «нет» и «разрешения».  `prompt=login`будет принудительно hello пользователя tooenter свои учетные данные на этот запрос, Инверсия единого входа на.  `prompt=none`— hello противоположной — он будет убедитесь, что этот пользователь hello не предоставляется все запросы на экран ни при каких обстоятельствах.  Если hello запрос выполнить не удалось автоматически через единый вход, конечная точка v2.0 hello будет возвращена ошибка.  `prompt=consent`будет триггер hello OAuth consent диалоговое окно после hello пользователь выполняет вход, подтверждения приложение hello пользователя toogrant разрешения toohello. |
| login_hint |необязательный |Может быть hello заполнением нулями toopre используется имя пользователя и электронной почты поля адреса hello страница входа для пользователя hello, если вы знаете свое имя пользователя, заранее.  Часто приложения будут использовать этот параметр во время повторной проверки подлинности, уже извлеченных hello имя пользователя из предыдущих вход с помощью hello `preferred_username` утверждения. |
| domain_hint |необязательный |Может использоваться значение `consumers` или `organizations`.  Если включен, он пропускает hello процесса обнаружения на основе электронной почты, пользователь не пройдет на странице входа v2.0 hello начальные tooa немного более упрощенную взаимодействие с пользователем.  Часто приложения будут использовать этот параметр во время повторной проверки подлинности, путем извлечения hello `tid` из предыдущего вход.  Если hello `tid` утверждения, значение — `9188040d-6c67-4c5b-b112-36a304b66dad`, следует использовать `domain_hint=consumers`.  Или используйте `domain_hint=organizations`. |

На этом этапе пользователь hello будет задаваемые tooenter своих учетных данных и завершения hello.  Hello конечной точки v2.0 гарантирует, что hello пользователь согласился toohello разрешениями, перечисленными в hello `scope` параметр запроса.  Если пользователь hello не согласился tooany таких разрешений, он запросит hello пользователя tooconsent toohello необходимые разрешения.  Подробные сведения о [разрешениях, согласии на предоставление и мультитенантных приложениях можно найти здесь](active-directory-v2-scopes.md).

Hello пользователь проходит аутентификацию и дает свое согласие, конечная точка v2.0 hello будет выполнен возврат к приложению tooyour ответ в указанном hello `redirect_uri`, с помощью метода hello, указанного в hello `response_mode` параметра.

#### Успешный ответ
Успешный ответ с использованием метода `response_mode=query` выглядит следующим образом:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
code=AwABAAAAvPM1KaPlrEqdFSBzjqfTGBCmLdgfSTLEMPGYuNHSUYBrq...
&state=12345
```

| Параметр | Описание |
| --- | --- |
| Код |значение authorization_code Hello hello запрошенного приложения. приложение Hello можно использовать toorequest код авторизации hello маркер доступа для hello целевого ресурса.  Срок действия кодов авторизации крайне мал и обычно истекает по прошествии порядка 10 минут. |
| state |Если параметр состояния включается в запрос hello, hello одинаковое значение должно отображаться в ответ hello. приложение Hello следует Проверьте идентичность значений состояния hello hello запроса и ответа. |

#### Сообщение об ошибке
Сообщения об ошибках могут отправляться также toohello `redirect_uri` , приложение hello можно обрабатывать их соответствующим образом:

```
GET https://login.microsoftonline.com/common/oauth2/nativeclient?
error=access_denied
&error_description=the+user+canceled+the+authentication
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
| server_error |Произошла непредвиденная ошибка сервера Hello. |Повторите запрос hello. Эти ошибки могут возникать в связи с временными условиями. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временной ошибки. |
| temporarily_unavailable |Hello server временно — слишком занят, toohandle hello запрос. |Повторите запрос hello. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временного условия. |
| invalid_resource |Hello целевой ресурс является недопустимым, так как он не существует, Azure AD не удается найти или настроена неправильно. |Это означает, что hello ресурс, если он существует, не был настроен в клиенте hello. приложение Hello может предложить пользователю инструкцию для установки приложения hello и добавив tooAzure AD hello. |

## Запрос маркера доступа
Теперь, когда вы получили значение authorization_code и имеют разрешения пользователем hello, можно активировать hello `code` для `access_token` toohello требуемого ресурса, отправляя `POST` запроса toohello `/token` конечной точки:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&code=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq3n8b2JRLk4OxVXr...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=authorization_code
&client_secret=JqQX2PNo9bpM0uEihUPzyrh    // NOTE: Only required for web apps
```

> [!TIP]
> Попытайтесь выполнить этот запрос в Postman. (Не забудьте tooreplace hello `code`) [ ![в почтальон](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Параметр |  | Описание |
| --- | --- | --- |
| tenant |обязательно |Hello `{tenant}` значение в путь hello hello запроса может быть используется toocontrol, которые можно выполнять вход в приложение hello.  Hello допустимые значения: `common`, `organizations`, `consumers`и идентификаторы клиентов.  Дополнительные сведения см. в [описании протоколов](active-directory-v2-protocols.md#endpoints). |
| client_id |обязательно |Идентификатор приложения этот портал регистрации hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) назначенный приложения. |
| grant_type |обязательно |Должно быть `authorization_code` для потока кода авторизации hello. |
| scope |обязательно |Список областей с разделителями-пробелами.  в этом участок должен tooor эквивалентное подмножество областей hello запросить в первый участок hello по запросу Hello областей.  Если указаны в этом запросе области hello охватывает несколько серверов ресурсов, конечная точка v2.0 hello возвращает токен для hello ресурс, указанный в первой области hello.  Более подробное описание областей, см. в разделе слишком[разрешений, согласия и областей](active-directory-v2-scopes.md). |
| Код |обязательно |значение authorization_code Hello, полученному в первый участок потока hello hello. |
| redirect_uri |обязательно |Здравствуйте же redirect_uri значение, которое было значение authorization_code используется tooacquire hello. |
| client_secret |необходим для веб-приложений |секрет приложения Hello, созданный на портале регистрации приложения hello для вашего приложения.  Его не следует использовать в собственном приложении, поскольку невозможно обеспечить полную безопасность секретов клиентов при их хранении на устройствах.  Это необходимо для веб-приложений и веб-API, которые безопасно иметь hello возможность toostore hello client_secret на стороне сервера hello. |

#### Успешный ответ
Успешный ответ токена выглядит следующим образом:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Параметр | Описание |
| --- | --- |
| access_token |Hello запрашиваемый маркер доступа. приложение Hello можно использовать этот токен tooauthenticate toohello, защищенному ресурсу, например веб-API. |
| token_type |Указывает значение типа токена hello. Hello только тип, который поддерживает Azure AD — носителя |
| expires_in |Как долго маркер доступа hello является действительным (в секундах). |
| scope |Hello областям hello access_token допустим. |
| refresh_token |Маркер обновления OAuth 2.0. Hello приложения можно с помощью этого токена получить дополнительные маркеры доступа после истечения срока действия текущего маркера доступа hello.  Refresh_tokens долгоживущие и может быть tooresources доступа используется tooretain на длительное время.  Дополнительные сведения см. в разделе toohello [ссылку на маркер v2.0](active-directory-v2-tokens.md). |
| id_token |Неподписанный веб-маркер JSON (JWT). base64Url может приложения Hello декодировать hello сегменты токена toorequest информация о hello пользователю, вошедшему в систему. приложение Hello может кэшировать значения hello и отобразить их, но его не следует полагаться на их для авторизации и границы безопасности.  Дополнительные сведения о id_tokens разделе hello [v2.0 ссылки на конечную точку token](active-directory-v2-tokens.md). |

#### Сообщение об ошибке
Сообщения об ошибках выглядят следующим образом:

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Параметр | Описание |
| --- | --- |
| error |Ошибка строка кода, который может быть используется tooclassify типы ошибок, которые возникают и может быть tooerrors используется tooreact. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |
| error_codes |Список кодов ошибок, характерных для службы маркеров безопасности, которые могут помочь при диагностике. |
| Timestamp |Hello время возникновения ошибки hello. |
| trace_id |Уникальный идентификатор для запроса hello, которые могут помочь в диагностике. |
| correlation_id |Уникальный идентификатор для запроса hello, которые могут помочь в диагностике во всех компонентах. |

#### Коды ошибок конечных точек токенов
| Код ошибки | Описание | Действие клиента |
| --- | --- | --- |
| invalid_request |Ошибка протокола, например отсутствует обязательный параметр. |Исправить и повторно отправьте запрос hello |
| invalid_grant |Код авторизации Hello является недопустимым, или истек срок действия. |Повторите новый toohello запроса `/authorize` конечной точки |
| unauthorized_client |Hello прошедшего проверку подлинности клиент не авторизован toouse тип предоставления этой авторизации. |Обычно это происходит, когда клиентское приложение hello не зарегистрирован в Azure AD или toohello пользователей клиента Azure AD не добавляется. приложение Hello может предложить пользователю инструкцию для установки приложения hello и добавив tooAzure AD hello. |
| invalid_client |Сбой проверки подлинности клиента. |учетные данные клиента Hello не допускаются. toofix, Здравствуйте, администратор приложения обновляет учетные данные hello. |
| unsupported_grant_type |сервер авторизации Hello не поддерживает тип предоставления авторизации hello. |Изменение hello предоставить тип в запросе hello. Ошибка этого типа должна происходить только во время разработки, и ее должны обнаружить при первоначальном тестировании. |
| invalid_resource |Hello целевой ресурс является недопустимым, так как он не существует, Azure AD не удается найти или настроена неправильно. |Это означает, что hello ресурс, если он существует, не был настроен в клиенте hello. приложение Hello может предложить пользователю инструкцию для установки приложения hello и добавив tooAzure AD hello. |
| interaction_required |Hello запрос требует взаимодействия с пользователем. К примеру, требуется дополнительный шаг проверки подлинности. |Повторите запрос hello с hello того же ресурса. |
| temporarily_unavailable |Hello server временно — слишком занят, toohandle hello запрос. |Повторите запрос hello. Hello клиентское приложение может объяснить toohello пользователя, его ответ задерживается из-за временного условия. |

## Использование маркера доступа hello
Теперь, когда вы получили успешно `access_token`, можно использовать токен hello в tooWeb запросы API-интерфейсы, включив его в hello `Authorization` заголовка:

> [!TIP]
> Выполните этот запрос в Postman. (Замените hello `Authorization` заголовок первого) [ ![в почтальон](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

## Обновление маркера доступа hello
Access_tokens невелики жили и их необходимо обновить, после истечения срока их действия toocontinue, доступ к ресурсам.  Это можно сделать путем отправки другой `POST` запроса toohello `/token` конечной точки, в настоящее время, предоставляя hello `refresh_token` вместо hello `code`:

```
// Line breaks for legibility only

POST /{tenant}/oauth2/v2.0/token HTTP/1.1
Host: https://login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&scope=https%3A%2F%2Fgraph.microsoft.com%2Fmail.read
&refresh_token=OAAABAAAAiL9Kn2Z27UubvWFPbm0gLWQJVzCTE9UkP3pSx1aXxUjq...
&redirect_uri=http%3A%2F%2Flocalhost%2Fmyapp%2F
&grant_type=refresh_token
&client_secret=JqQX2PNo9bpM0uEihUPzyrh      // NOTE: Only required for web apps
```

> [!TIP]
> Попытайтесь выполнить этот запрос в Postman. (Не забудьте tooreplace hello `refresh_token`) [ ![в почтальон](./media/active-directory-v2-protocols-oauth-code/runInPostman.png)](https://app.getpostman.com/run-collection/8f5715ec514865a07e6a)
> 
> 

| Параметр |  | Описание |
| --- | --- | --- |
| tenant |обязательно |Hello `{tenant}` значение в путь hello hello запроса может быть используется toocontrol, которые можно выполнять вход в приложение hello.  Hello допустимые значения: `common`, `organizations`, `consumers`и идентификаторы клиентов.  Дополнительные сведения см. в [описании протоколов](active-directory-v2-protocols.md#endpoints). |
| client_id |обязательно |Идентификатор приложения этот портал регистрации hello Hello ([apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)) назначенный приложения. |
| grant_type |обязательно |Должно быть `refresh_token` для этого участка поток authorization code hello. |
| scope |обязательно |Список областей с разделителями-пробелами.  в этом участок должен tooor эквивалентное подмножество областей hello запросить в hello исходное значение authorization_code запросе по запросу Hello областей.  Если указаны в этом запросе области hello охватывает несколько серверов ресурсов, конечная точка v2.0 hello возвращает токен для hello ресурс, указанный в первой области hello.  Более подробное описание областей, см. в разделе слишком[разрешений, согласия и областей](active-directory-v2-scopes.md). |
| refresh_token |обязательно |Здравствуйте, refresh_token, который вы приобрели в hello второго участка hello потока. |
| redirect_uri |обязательно |Здравствуйте же redirect_uri значение, которое было значение authorization_code используется tooacquire hello. |
| client_secret |необходим для веб-приложений |секрет приложения Hello, созданный на портале регистрации приложения hello для вашего приложения.  Его не следует использовать в собственном приложении, поскольку невозможно обеспечить полную безопасность секретов клиентов при их хранении на устройствах.  Это необходимо для веб-приложений и веб-API, которые безопасно иметь hello возможность toostore hello client_secret на стороне сервера hello. |

#### Успешный ответ
Успешный ответ токена выглядит следующим образом:

```
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...",
    "token_type": "Bearer",
    "expires_in": 3599,
    "scope": "https%3A%2F%2Fgraph.microsoft.com%2Fmail.read",
    "refresh_token": "AwABAAAAvPM1KaPlrEqdFSBzjqfTGAMxZGUTdM0t4B4...",
    "id_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiIyZDRkMTFhMi1mODE0LTQ2YTctOD...",
}
```
| Параметр | Описание |
| --- | --- |
| access_token |Hello запрашиваемый маркер доступа. приложение Hello можно использовать этот токен tooauthenticate toohello, защищенному ресурсу, например веб-API. |
| token_type |Указывает значение типа токена hello. Hello только тип, который поддерживает Azure AD — носителя |
| expires_in |Как долго маркер доступа hello является действительным (в секундах). |
| scope |Hello областям hello access_token допустим. |
| refresh_token |Новый токен обновления OAuth 2.0. Следует заменить старый обновления hello токена с этого маркера tooensure новых обновления токенов обновления будут оставаться действительными то же время. |
| id_token |Неподписанный веб-маркер JSON (JWT). base64Url может приложения Hello декодировать hello сегменты токена toorequest информация о hello пользователю, вошедшему в систему. приложение Hello может кэшировать значения hello и отобразить их, но его не следует полагаться на их для авторизации и границы безопасности.  Дополнительные сведения о id_tokens разделе hello [v2.0 ссылки на конечную точку token](active-directory-v2-tokens.md). |

#### Сообщение об ошибке
```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/mail.read is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
  "error_codes": [
    70011
  ],
  "timestamp": "2016-01-09 02:02:12Z",
  "trace_id": "255d1aef-8c98-452f-ac51-23d051240864",
  "correlation_id": "fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7"
}
```

| Параметр | Описание |
| --- | --- |
| error |Ошибка строка кода, который может быть используется tooclassify типы ошибок, которые возникают и может быть tooerrors используется tooreact. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello разработчик. |
| error_codes |Список кодов ошибок, характерных для службы маркеров безопасности, которые могут помочь при диагностике. |
| Timestamp |Hello время возникновения ошибки hello. |
| trace_id |Уникальный идентификатор для запроса hello, которые могут помочь в диагностике. |
| correlation_id |Уникальный идентификатор для запроса hello, которые могут помочь в диагностике во всех компонентах. |

Описание кодов ошибок hello и hello Рекомендуемое действие клиента, см. в разделе [коды для ошибок, конечная точка маркера](#error-codes-for-token-endpoint-errors).

