---
title: "Azure AD aaaUse v2.0 tooaccess защиты ресурсов без вмешательства пользователя | Документы Microsoft"
description: "Построение веб-приложений с использованием протокола проверки подлинности OAuth 2.0 hello реализации hello Azure AD."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9b7cfbd7-f89f-4e33-aff2-414edd584b07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 0003ec836d633a5466c48033adedac1108f27203
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Поток Azure Active Directory версии 2.0 и hello OAuth 2.0 учетные данные клиента
Можно использовать hello [предоставления учетных данных клиента OAuth 2.0](http://tools.ietf.org/html/rfc6749#section-4.4), иногда называемые *двусторонних OAuth*, tooaccess ресурсы на веб сервере с использованием идентификатора hello приложения. Этот тип предоставления часто используется для взаимодействия сервера на сервер, которые необходимо выполнить в фоновом режиме hello, без интерпретации взаимодействия с пользователем. Такие приложения часто являются ссылка tooas *управляющие программы* или *учетные записи служб*.

> [!NOTE]
> Конечная точка v2.0 Hello не поддерживает все сценарии Azure Active Directory и возможности. toodetermine необходимость использования конечной точки v2.0 hello, узнайте, как [ограничения v2.0](active-directory-v2-limitations.md).
>
>

В типичной hello *трехсторонних OAuth*, клиентское приложение представляет разрешения, предоставленные tooaccess ресурс от имени определенного пользователя. разрешение Hello делегируется приложение toohello пользователя hello, обычно во время hello [согласия](active-directory-v2-scopes.md) процесса. Однако в hello поток клиентских учетных данных, разрешения предоставляются непосредственно самим приложением toohello. Предъявляемый ресурсов маркера tooa приложение hello hello ресурсов обеспечивает само приложение hello имеет авторизации tooperform действие, которое не hello пользователь не авторизации.

## Схема протокола
поток учетных данных всю клиентскую Hello выглядит примерно toohello на следующей диаграмме. Чтобы описать каждое из действий hello далее в этой статье.

![Поток учетных данных клиента](../../media/active-directory-v2-flows/convergence_scenarios_client_creds.png)

## Получение прямой авторизации
Приложения, как правило, получает tooaccess прямой авторизации ресурса двумя способами: через список управления доступом (ACL) в ресурсе hello, или назначения разрешений приложения в Azure Active Directory (Azure AD). Эти два метода являются наиболее часто встречается в Azure AD hello и рекомендуется для клиентов и ресурсов, выполняющих hello поток клиентских учетных данных. Ресурс можно выбрать tooauthorize своих клиентов другими способами, однако. Каждый сервер ресурсов можно выбрать метод hello, hello больше смысла для приложения.

### Доступ к спискам управления
Поставщик ресурсов может принудительно применять проверку авторизации на основе списка известных идентификаторов приложений, а также предоставлять определенный уровень доступа на основе этих идентификаторов. Когда hello ресурсов Получает токен от конечной точки v2.0 hello, можно декодировать токен hello и извлечь идентификатор приложения hello клиента из hello `appid` и `iss` утверждений. Затем он сравнивает приложения hello от ACL, которую он обслуживает. Здравствуйте, список управления Доступом для детализации и метод могут существенно различаться между ресурсами.

Распространенным вариантом применения является toouse проверяет toorun ACL для веб-приложения или веб-API. Hello веб-API может предоставить только подмножество полных разрешений tooa конкретного клиента. тесты конца в конец toorun на hello API, создайте тестовый клиент, которая получает токены из конечной точки v2.0 hello и отправляет их toohello API. Hello API, а затем проверяет hello ACL для hello проверить идентификатор приложения клиента для полного доступа всю функциональность toohello API-интерфейса. При использовании такого рода ACL, нужно убедиться, что toovalidate не только hello вызывающего `appid` значение. Также для проверки этой hello `iss` значение токена hello является доверенным.

Этот тип авторизации распространено управляющие программы и учетных записей службы, которые должны tooaccess данных, владельцем потребителя пользователи, имеющие личные учетные записи Майкрософт. Для данных, принадлежащих организации корпорация Майкрософт рекомендует, чтобы получить необходимую авторизацию hello через разрешения для приложения.

### Разрешения приложения
Вместо использования списки управления доступом, можно использовать API-интерфейсы tooexpose набор разрешений приложения. Организации администратор предоставил разрешение приложения tooan приложений и данных используется только tooaccess принадлежат этой организации и ее сотрудникам. Например Microsoft Graph предоставляет несколько приложения разрешения toodo hello следующее:

* чтение почты во всех почтовых ящиках;
* чтение и запись почты во всех почтовых ящиках;
* отправка почты любым пользователем;
* Прочитать данные каталога

Дополнительные сведения о разрешениях приложения перейдите слишком[Microsoft Graph](https://graph.microsoft.io).

разрешения приложения toouse в вашем приложении hello шагов, которые рассматриваются в следующих разделах hello.

#### Запрос разрешений hello в портал регистрации приложения hello
1. Go tooyour приложение hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), или [создать приложение](active-directory-v2-app-registration.md), если это еще не сделано. Вам потребуется toouse по крайней мере один секрет приложения при создании приложения.
2. Найдите hello **прямых разрешений приложения** статьи, а затем добавьте hello разрешения, необходимые для приложения.
3. **Сохранить** hello регистрации приложения.

#### Рекомендуется: Hello пользователя входа в приложении tooyour
Как правило при построении приложения, использующего разрешения приложения hello приложению требуется страницы или представления, на какие hello admin утверждает разрешений приложение hello. Эта страница может быть частью приложение hello входа потока параметрах приложение hello или может быть выделенный поток «подключиться». Во многих случаях имеет смысл для tooshow приложения hello это «подключиться» представление, только после того, что пользователь выполнил вход с рабочей или учебной учетной записи Майкрософт.

При входе пользователя hello в приложении tooyour можно определить hello организации toowhich hello пользователь перед tooapprove пользователя hello разрешения приложения hello. Хотя это не обязательно, таким образом можно сделать пользовательский интерфейс более интуитивно понятным. пользователь toosign hello в выполните наши [учебники протокола v2.0](active-directory-v2-protocols.md).

#### Запросить hello разрешения от администратора каталога
Когда вы будете готовы toorequest разрешения от администратора организации hello, вы можете перенаправлять hello пользователя toohello v2.0 *конечной точки согласия администратора*.

```
// Line breaks are for legibility only.

GET https://login.microsoftonline.com/{tenant}/adminconsent?
client_id=6731de76-14a6-49ae-97bc-6eba6914391e
&state=12345
&redirect_uri=http://localhost/myapp/permissions
```

```
// Pro tip: Try pasting hello following request in a browser!
```

```
https://login.microsoftonline.com/common/adminconsent?client_id=6731de76-14a6-49ae-97bc-6eba6914391e&state=12345&redirect_uri=http://localhost/myapp/permissions
```

| Параметр | Условие | Описание |
| --- | --- | --- |
| tenant |Обязательно |Клиент каталога Hello, требуется разрешение toorequest из. Его можно указать в виде GUID или понятного имени. Если вы не знаете, какой клиент hello принадлежит пользователь tooand требуется toolet их вход с любого клиента, используйте `common`. |
| client_id |Обязательно |Приложение Hello идентификатор этого hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) назначенный tooyour приложения. |
| redirect_uri |Обязательно |URI, место отправки для вашего приложения toohandle toobe ответа hello перенаправления Hello. Оно должно точно соответствовать одно перенаправление hello URI, которые зарегистрированы в портале hello, за исключением того, он должен быть в кодировке URL-адрес, и может иметь дополнительные сегменты пути. |
| state |Рекомендуется |Значение, которое включается в запрос hello, также возвращается в ответ на токен hello. Это может быть строка любого контента. состояние Hello — используется tooencode сведения о состоянии пользователя hello в приложение hello, до возникновения hello запрос проверки подлинности, такие как страница hello и представление, в котором они находились на. |

В этот момент Azure AD обеспечивает только администратор клиента может выполнить вход в toocomplete hello запроса. Здравствуйте, администратор будет выведено tooapprove все hello Непосредственное применение разрешения, которые запросили приложения на портале регистрации приложения hello.

##### Успешный ответ
Если Здравствуйте, администратор подтверждает hello разрешения для приложения, hello успешный ответ выглядит следующим образом:

```
GET http://localhost/myapp/permissions?tenant=a8990e1f-ff32-408a-9f8e-78d3b9139b95&state=state=12345&admin_consent=True
```

| Параметр | Описание |
| --- | --- | --- |
| tenant |Hello клиента каталога, которому предоставляется разрешение приложения hello, она запрошена, в формате GUID. |
| state |Значение, которое включается в запрос hello, также возвращается в ответ на токен hello. Это может быть строка любого контента. состояние Hello — используется tooencode сведения о состоянии пользователя hello в приложение hello, до возникновения hello запрос проверки подлинности, такие как страница hello и представление, в котором они находились на. |
| admin_consent |Значение слишком**true**. |

##### Сообщение об ошибке
Здравствуйте, администратор не одобрения hello разрешения для приложения, hello сбой ответа выглядит следующим образом:

```
GET http://localhost/myapp/permissions?error=permission_denied&error_description=The+admin+canceled+the+request
```

| Параметр | Описание |
| --- | --- | --- |
| error |Строка кода ошибки, которые можно использовать tooclassify типы ошибок, и который можно использовать tooreact tooerrors. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки hello. |

После получения успешного ответа от конечной подготовки приложения hello приложение получило hello прямого применения разрешений, которые она запрошена. Теперь вы можете запросить маркер для ресурса hello.

## Получение маркера
После приобретен hello необходимые авторизации для приложения, перейдите к получения токенов доступа для API-интерфейсов. tooget токен с помощью hello предоставления учетных данных клиента, отправить запрос POST toohello `/token` v2.0 конечной точки:

### Первый сценарий: запрос маркера доступа с помощью общего секрета

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials
```

```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'client_id=535fb089-9ff3-47b6-9bfb-4f1264799865&scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_secret=qWgdYAmab0YSkuL1qKv5bPX&grant_type=client_credentials' 'https://login.microsoftonline.com/common/oauth2/v2.0/token'
```

| Параметр | Условие | Описание |
| --- | --- | --- |
| client_id |Обязательно |Приложение Hello идентификатор этого hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) назначенный tooyour приложения. |
| scope |Обязательно |передано значение Hello hello `scope` параметр в запросе должен быть hello идентификатор ресурса (URI ИД приложения) hello ресурса требуется добавляется hello `.default` суффикс. Например hello Microsoft Graph hello значение — `https://graph.microsoft.com/.default`. Это значение сообщает конечной точки v2.0 hello, что все hello прямого применения разрешений, которые вы настроили для своего приложения, он должен выдавать токен для hello связанных с hello ресурс, нужно toouse. |
| client_secret |Обязательно |Здравствуйте, секрет приложения, созданный для приложения на портале регистрации приложения hello. |
| grant_type |Обязательно |Этот параметр должен содержать значение `client_credentials`. |

### Второй сценарий: запрос маркера доступа с помощью сертификата

```
POST /common/oauth2/v2.0/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

scope=https%3A%2F%2Fgraph.microsoft.com%2F.default&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

| Параметр | Условие | Описание |
| --- | --- | --- |
| client_id |Обязательно |Приложение Hello идентификатор этого hello [портала регистрации приложения](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) назначенный tooyour приложения. |
| scope |Обязательно |передано значение Hello hello `scope` параметр в запросе должен быть hello идентификатор ресурса (URI ИД приложения) hello ресурса требуется добавляется hello `.default` суффикс. Например hello Microsoft Graph hello значение — `https://graph.microsoft.com/.default`. Это значение сообщает конечной точки v2.0 hello, что все hello прямого применения разрешений, которые вы настроили для своего приложения, он должен выдавать токен для hello связанных с hello ресурс, нужно toouse. |
| client_assertion_type |обязательно |должно быть значение Hello`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |обязательно | Утверждение (веб-маркера JSON), необходимо toocreate и сертификата входа со слова hello зарегистрирован как учетные данные для приложения. Узнайте, как [учетные данные сертификатов](active-directory-certificate-credentials.md) toolearn как tooregister вашего сертификата и hello формата hello утверждения.|
| grant_type |Обязательно |Этот параметр должен содержать значение `client_credentials`. |

Обратите внимание, что параметры hello являются почти hello же, как в случае hello запроса hello, общий секрет, за исключением того, что параметр client_secret hello заменяется два параметра: client_assertion_type и client_assertion.

### Успешный ответ
Успешный ответ выглядит следующим образом.

```
{
  "token_type": "Bearer",
  "expires_in": 3599,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBP..."
}
```

| Параметр | Описание |
| --- | --- |
| access_token |Hello запрашиваемый маркер доступа. приложение Hello можно использовать этот токен tooauthenticate toohello, защищенному ресурсу, например tooa веб-API. |
| token_type |Указывает значение типа токена hello. Здравствуйте, только тип, который поддерживает Azure AD является `bearer`. |
| expires_in |Как долго маркер доступа hello является действительным (в секундах). |

### Сообщение об ошибке
Сообщение об ошибке выглядит следующим образом.

```
{
  "error": "invalid_scope",
  "error_description": "AADSTS70011: hello provided value for hello input parameter 'scope' is not valid. hello scope https://foo.microsoft.com/.default is not valid.\r\nTrace ID: 255d1aef-8c98-452f-ac51-23d051240864\r\nCorrelation ID: fb3d2015-bc17-4bb9-bb85-30c5cf1aaaa7\r\nTimestamp: 2016-01-09 02:02:12Z",
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
| error |Строка кода ошибки, который можно использовать типы tooclassify возникающие ошибки и tooreact tooerrors. |
| error_description |Сообщение об ошибке, которые могут помочь определить причину ошибки проверки подлинности hello. |
| error_codes |Список кодов ошибок, характерных для службы маркеров безопасности, которые могут помочь при диагностике. |
| Timestamp |Hello время возникновения ошибки hello. |
| trace_id |Уникальный идентификатор для запроса hello, которые могут помочь с диагностикой. |
| correlation_id |Уникальный идентификатор для запроса hello, которые могут помочь с диагностикой во всех компонентах. |

## Использование маркера
Теперь, когда вы получили маркер, используйте hello маркера toomake запросов toohello ресурс. После истечения срока действия токена hello, повторите запрос toohello hello `/token` tooacquire конечной точки в маркере доступа новую.

```
GET /v1.0/me/messages
Host: https://graph.microsoft.com
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q...
```

```
// Pro tip: Try hello following command! (Replace hello token with your own.)
```

```
curl -X GET -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik5HVEZ2ZEstZnl0aEV1Q" 'https://graph.microsoft.com/v1.0/me/messages'
```

## Пример кода
см. пример приложения hello, реализует предоставления учетных данных клиента с использованием конечной точки согласия администратора hello, toosee наших [образец кода v2.0 управляющей программы](https://github.com/Azure-Samples/active-directory-dotnet-daemon-v2).
