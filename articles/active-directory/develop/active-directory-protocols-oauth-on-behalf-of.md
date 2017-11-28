---
title: "aaaAzure AD службы tooservice проверки подлинности с помощью OAuth2.0 от имени представляет проект спецификации | Документы Microsoft"
description: "В этой статье описывается, как toouse HTTP сообщения tooimplement службы tooservice проверки подлинности с помощью hello от имени представляет потока OAuth2.0."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 09f6f318-e88b-4024-9ee1-e7f09fb19a82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 55b7fcfe6c0223bddedd8d8fa2defcb5769b43c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Служба tooservice вызывает использование в hello потока от имени представляет удостоверение делегированного пользователя
Hello потока behalf-of OAuth 2.0 служит hello вариант использования которой приложение вызывает службу или веб-API, которая в свою очередь должна toocall другой службы и веб-API. Идея Hello — toopropagate hello делегировать удостоверение пользователя и разрешения с помощью цепочки запросов hello. Для hello службы среднего уровня toomake проверку подлинности запросы toohello нижестоящие службы от имени пользователя hello ему toosecure маркера доступа из Azure Active Directory (Azure AD).

## Схема потока On-Behalf-Of
Предположим, что hello пользователь прошел проверку на приложения с помощью hello [поток разрешений кода авторизации OAuth 2.0](active-directory-protocols-oauth-code.md). На этом этапе приложение hello содержит маркер доступа (маркера A) с утверждения пользователя hello и согласия tooaccess hello среднего уровня веб-API (API A). Теперь API A должен toomake запрос с проверкой подлинности toohello нижестоящий веб-API (API B).

Hello описанных ниже составляют hello от имени представляет поток и описываются с помощью hello hello следующие схемы.

![Поток On-Behalf-Of в OAuth 2.0](media/active-directory-protocols-oauth-on-behalf-of/active-directory-protocols-oauth-on-behalf-of-flow.png)


1. клиентское приложение Hello делает запрос tooAPI С hello маркера A.
2. Объект API проверяет подлинность toohello конечная точка выдачи токена Azure AD и запрашивает токен tooaccess б API.
3. Конечная точка выдачи токена Azure AD Hello проверяет API A учетные данные с помощью маркера A и проблемы hello маркер доступа для API B (маркер B).
4. токен Hello B задается в заголовок authorization hello tooAPI запрос hello б.
5. Данные из hello, защищенному ресурсу, возвращенный API б.

## Регистрация приложения hello и службы в Azure AD
Регистрация клиентского приложения hello и служба среднего уровня hello в Azure AD.
### Регистрация службы среднего уровня hello
1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello, нажмите кнопку в вашей учетной записи, а также в разделе hello **каталога** выберите hello клиента Active Directory, где будут tooregister приложения.
3. Щелкните **более служб** в hello левую панель навигации и выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений** и выберите **Регистрация нового приложения**.
5. Введите понятное имя для приложения hello и выберите тип приложения hello. Зависимости от типа приложения hello набор hello входа URL-адрес или URL-адрес toohello базовый URL-адрес перенаправления. Щелкните **создать** toocreate приложения hello.
6. Оставаясь в hello портал Azure, выберите приложение и щелкнуть **параметры**. В меню "настройки" hello, выберите **ключей** и добавьте раздел - выберите длительность ключа 1 года или 2 года. При сохранить эту страницу, будет отображаться значение ключа hello, скопируйте и сохраните значение hello в безопасном месте - они потребуются этого ключа поздней tooconfigure hello параметры приложения в собственной реализации - это значение ключа не будет снова отображается, а также доступны по любому иным образом, так что произведите запись его как только он будет видимым в hello портала Azure.

### Регистрация клиентского приложения hello
1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. На верхней панели hello, нажмите кнопку в вашей учетной записи, а также в разделе hello **каталога** выберите hello клиента Active Directory, где будут tooregister приложения.
3. Щелкните **более служб** в hello левую панель навигации и выберите **Azure Active Directory**.
4. Щелкните **Регистрация приложений** и выберите **Регистрация нового приложения**.
5. Введите понятное имя для приложения hello и выберите тип приложения hello. Зависимости от типа приложения hello набор hello входа URL-адрес или URL-адрес toohello базовый URL-адрес перенаправления. Щелкните **создать** toocreate приложения hello.
6. Настройка разрешений для приложения — в меню "настройки" hello, выберите hello **разрешения, необходимые** щелкните **добавить**, затем **выберите API**и тип hello Имя службы среднего уровня hello в текстовом поле hello. Затем щелкните **Выбор разрешений** и выберите разрешение "Доступ к *имя_службы*".

### Настройка известных клиентских приложений
В этом случае служба среднего уровня hello имеет не взаимодействия tooobtain hello пользователя согласия tooaccess hello подчиненных API. Здравствуйте, таким образом, параметр toogrant доступа toohello подчиненных API должна быть представлена переднего плана в рамках шага согласия hello во время проверки подлинности.
tooachieve это, выполните hello описанные ниже шаги регистрации hello клиента tooexplicitly привязку приложения в Azure AD с регистрацией hello hello среднего уровня службы, которая объединяет предусмотренного hello клиентского и среднего уровня в одном диалоговом окне согласия hello.
1. Перейдите toohello регистрации службы среднего уровня и выберите команду **манифеста** Редактор манифестов tooopen hello.
2. В манифесте hello найдите hello `knownClientApplications` массива свойства и добавить hello идентификатор клиента приложения hello клиента как элемент.
3. Сохраните манифест hello, установив hello кнопку Сохранить.

## Запрос маркера доступа tooservice службы
toorequest маркер доступа, сделать конечную точку HTTP POST toohello конкретного клиента Azure AD с hello следующие параметры.

```
https://login.microsoftonline.com/<tenant>/oauth2/token
```
Существует два варианта, в зависимости от того, является ли клиентское приложение hello выбирает toobe защищен общий секрет или сертификат.

### Первый сценарий: запрос маркера доступа с помощью общего секрета
При использовании общего секрета, запрос маркера доступа для служб содержит hello следующие параметры:

| Параметр |  | Описание |
| --- | --- | --- |
| grant_type |обязательно | Тип запроса маркера hello Hello. Для запроса, с помощью JWT, hello значение должно быть **urn: ietf:params:oauth:grant-тип: jwt-носителя**. |
| assertion |обязательно | значение Hello hello маркера, используемого в запросе hello. |
| client_id |обязательно | Hello идентификатор приложения назначить toohello вызывающей службы во время регистрации в Azure AD. hello toofind идентификатор приложения в hello портала управления Azure щелкните **Active Directory**, щелкните каталог hello, а затем щелкните имя приложения hello. |
| client_secret |обязательно | Hello ключ зарегистрирован для вызова службы в Azure AD hello. Это значение следует отмечали во время регистрации hello. |
| resource |обязательно | Здравствуйте, URI идентификатора приложения hello, получение службы (защищенный ресурс). hello toofind URI идентификатора приложения, в hello портала управления Azure щелкните **Active Directory**, выберите каталог hello, щелкните имя приложения hello, **все параметры** и нажмите кнопку **свойства** . |
| requested_token_use |обязательно | Указывает, каким образом должны обрабатываться запрос hello. В hello потока от имени представляет hello значение должно быть **on_behalf_of**. |
| scope |обязательно | Разделенный пробелами список областей для запроса токена hello. Для OpenID Connect, hello области **openid** должен быть указан.|

#### Пример
Hello следующие HTTP POST запрашивает токен доступа для веб-https://graph.windows.net hello API. Hello `client_id` идентифицирует службу hello, который запрашивает токен доступа hello.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_secret=0Y1W%2BY3yYb3d9N8vSjvm8WrGzVZaAaHbHHcGbcgG%2BoI%3D
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

### Второй сценарий: запрос маркера доступа с помощью сертификата
Запрос маркера доступа для служб с помощью сертификата содержит hello следующие параметры:

| Параметр |  | Описание |
| --- | --- | --- |
| grant_type |обязательно | Тип запроса маркера hello Hello. Для запроса, с помощью JWT, hello значение должно быть **urn: ietf:params:oauth:grant-тип: jwt-носителя**. |
| assertion |обязательно | значение Hello hello маркера, используемого в запросе hello. |
| client_id |обязательно | Hello идентификатор приложения назначить toohello вызывающей службы во время регистрации в Azure AD. hello toofind идентификатор приложения в hello портала управления Azure щелкните **Active Directory**, щелкните каталог hello, а затем щелкните имя приложения hello. |
| client_assertion_type |обязательно |должно быть значение Hello`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |обязательно | Утверждение (веб-маркера JSON), необходимо toocreate и сертификата входа со слова hello зарегистрирован как учетные данные для приложения.  Узнайте, как [учетные данные сертификатов](active-directory-certificate-credentials.md) toolearn как tooregister вашего сертификата и hello формата hello утверждения.|
| resource |обязательно | Здравствуйте, URI идентификатора приложения hello, получение службы (защищенный ресурс). hello toofind URI идентификатора приложения, в hello портала управления Azure щелкните **Active Directory**, выберите каталог hello, щелкните имя приложения hello, **все параметры** и нажмите кнопку **свойства** . |
| requested_token_use |обязательно | Указывает, каким образом должны обрабатываться запрос hello. В hello потока от имени представляет hello значение должно быть **on_behalf_of**. |
| scope |обязательно | Разделенный пробелами список областей для запроса токена hello. Для OpenID Connect, hello области **openid** должен быть указан.|

Обратите внимание, что параметры hello являются почти hello же, как в случае hello запроса hello, общий секрет, за исключением того, что параметр client_secret hello заменяется два параметра: client_assertion_type и client_assertion.

#### Пример
Привет, выполнив HTTP POST запрашивает токен доступа для hello https://graph.windows.net web API с помощью сертификата. Hello `client_id` идентифицирует службу hello, который запрашивает токен доступа hello.

```
// line breaks for legibility only

POST /oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=urn%3Aietf%3Aparams%3Aoauth%3Agrant-type%3Ajwt-bearer
&client_id=625391af-c675-43e5-8e44-edd3e30ceb15
&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer
&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg
&resource=https%3A%2F%2Fgraph.windows.net
&assertion=eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2Rkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tLzE5MjNmODYyLWU2ZGMtNDFhMy04MWRhLTgwMmJhZTAwYWY2ZCIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzI2MDM5Y2NlLTQ4OWQtNDAwMi04MjkzLTViMGM1MTM0ZWFjYi8iLCJpYXQiOjE0OTM0MjMxNTIsIm5iZiI6MTQ5MzQyMzE1MiwiZXhwIjoxNDkzNDY2NjUyLCJhY3IiOiIxIiwiYWlvIjoiWTJaZ1lCRFF2aTlVZEc0LzM0L3dpQndqbjhYeVp4YmR1TFhmVE1QeG8yYlN2elgreHBVQSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiJiMzE1MDA3OS03YmViLTQxN2YtYTA2YS0zZmRjNzhjMzI1NDUiLCJhcHBpZGFjciI6IjAiLCJlX2V4cCI6MzAyNDAwLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzY3AiOiJ1c2VyX2ltcGVyc29uYXRpb24iLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidmVyIjoiMS4wIn0.R-Ke-XO7lK0r5uLwxB8g5CrcPAwRln5SccJCfEjU6IUqpqcjWcDzeDdNOySiVPDU_ZU5knJmzRCF8fcjFtPsaA4R7vdIEbDuOur15FXSvE8FvVSjP_49OH6hBYqoSUAslN3FMfbO6Z8YfCIY4tSOB2I6ahQ_x4ZWFWglC3w5mK-_4iX81bqi95eV4RUKefUuHhQDXtWhrSgIEC0YiluMvA4TnaJdLq_tWXIc4_Tq_KfpkvI004ONKgU7EAMEr1wZ4aDcJV2yf22gQ1sCSig6EGSTmmzDuEPsYiyd4NhidRZJP4HiiQh-hePBQsgcSgYGvz9wC6n57ufYKh2wm_Ti3Q
&requested_token_use=on_behalf_of
&scope=openid
```

## Ответ на токен доступа службы tooservice
Об успехе — ответ JSON OAuth 2.0 с hello следующие параметры.

| Параметр | Описание |
| --- | --- |
| token_type |Указывает значение типа токена hello. Здравствуйте, только тип, который поддерживает Azure AD является **носителя**. Дополнительные сведения о маркерах носителя см. в разделе hello [OAuth 2.0 Authorization Framework: использование токенов предъявителя (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| scope |область Hello права доступа, предоставляемые в маркере hello. |
| expires_in |Длина Hello токена доступа hello времени является допустимым (в секундах). |
| expires_on |Hello время истечения срока действия маркера доступа hello. Hello Дата представляется в виде hello число секунд с 1970-01-01T0:0:0Z UTC до времени истечения срока действия hello. Это значение определяет используемые toodetermine hello времени жизни кэшированных маркеров. |
| resource |Здравствуйте, URI идентификатора приложения hello, получение службы (защищенный ресурс). |
| access_token |Hello запрашиваемый маркер доступа. Hello вызова службы можно использовать эту службу принимающей маркера tooauthenticate toohello. |
| id_token |токен Hello запрошенным идентификатором. Привет, вызов службы можно использовать удостоверение пользователя tooverify hello и начать сеанс с пользователем hello. |
| refresh_token |токен обновления Hello для hello запрашиваемый маркер доступа. Привет, вызов службы можно использовать этот токен toorequest другой маркер доступа после истечения срока действия текущего маркера доступа hello. |

### Пример ответа с успешным предоставлением доступа
Hello пример успешного ответа tooa запрашивает маркер доступа для веб-https://graph.windows.net hello API.

```
{
    "token_type":"Bearer",
    "scope":"User.Read",
    "expires_in":"43482",
    "ext_expires_in":"302683",
    "expires_on":"1493466951",
    "not_before":"1493423168",
    "resource":"https://graph.windows.net",
    "access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ",
    "refresh_token":"AQABAAAAAABnfiG-mA6NTae7CdWW7QfdjKGu9-t1scy_TDEmLi4eLQMjJGt_nAoVu6A4oSu1KsRiz8XyQIPKQxSGfbf2FoSK-hm2K8TYzbJuswYusQpJaHUQnSqEvdaCeFuqXHBv84wjFhuanzF9dQZB_Ng5za9xKlUENrNtlq9XuLNVKzxEyeUM7JyxzdY7JiEphWImwgOYf6II316d0Z6-H3oYsFezf4Xsjz-MOBYEov0P64UaB5nJMvDyApV-NWpgklLASfNoSPGb67Bc02aFRZrm4kLk-xTl6eKE6hSo0XU2z2t70stFJDxvNQobnvNHrAmBaHWPAcC3FGwFnBOojpZB2tzG1gLEbmdROVDp8kHEYAwnRK947Py12fJNKExUdN0njmXrKxNZ_fEM33LHW1Tf4kMX_GvNmbWHtBnIyG0w5emb-b54ef5AwV5_tGUeivTCCysgucEc-S7G8Cz0xNJ_BOiM_4bAv9iFmrm9STkltpz0-Tftg8WKmaJiC0xXj6uTf4ZkX79mJJIuuM7XP4ARIcLpkktyg2Iym9jcZqymRkGH2Rm9sxBwC4eeZXM7M5a7TJ-5CqOdfuE3sBPq40RdEWMFLcrAzFvP0VDR8NKHIrPR1AcUruat9DETmTNJukdlJN3O41nWdZOVoJM-uKN3uz2wQ2Ld1z0Mb9_6YfMox9KTJNzRzcL52r4V_y3kB6ekaOZ9wQ3HxGBQ4zFt-2U0mSszIAA",
    "id_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC8yNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IvIiwiaWF0IjoxNDkzNDIzMTY4LCJuYmYiOjE0OTM0MjMxNjgsImV4cCI6MTQ5MzQ2Njk1MSwiYW1yIjpbInB3ZCJdLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJzdWIiOiJEVXpYbkdKMDJIUk0zRW5pbDFxdjZCakxTNUllQy0tQ2ZpbzRxS1MzNEc4IiwidGlkIjoiMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiIiwidW5pcXVlX25hbWUiOiJuYXZ5YUBkZG9iYWxpYW5vdXRsb29rLm9ubWljcm9zb2Z0LmNvbSIsInVwbiI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXRpIjoieEN3ZnpoYS1QMFdKUU9MeENHZ0tBQSIsInZlciI6IjEuMCJ9."
}
```

### Пример ответа с сообщением об ошибке
Ответ с ошибкой по конечную точку токена Azure AD при попытке tooacquire маркер доступа для hello подчиненных API, если возвращается hello подчиненных API содержит политику условного доступа, такие как многофакторная проверка подлинности установки на нем. Служба среднего уровня Hello следует контактной это ошибка toohello клиентское приложение, чтобы клиентское приложение hello могла предоставлять hello hello пользователя взаимодействия toosatisfy политики условного доступа.

```
{
    "error":"interaction_required",
    "error_description":"AADSTS50079: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must enroll in multi-factor authentication tooaccess 'bf8d80f9-9098-4972-b203-500f535113b1'.\r\nTrace ID: b72a68c3-0926-4b8e-bc35-3150069c2800\r\nCorrelation ID: 73d656cf-54b1-4eb2-b429-26d8165a52d7\r\nTimestamp: 2017-05-01 22:43:20Z",
    "error_codes":[50079],
    "timestamp":"2017-05-01 22:43:20Z",
    "trace_id":"b72a68c3-0926-4b8e-bc35-3150069c2800",
    "correlation_id":"73d656cf-54b1-4eb2-b429-26d8165a52d7",
    "claims":"{\"access_token\":{\"polids\":{\"essential\":true,\"values\":[\"9ab03e19-ed42-4168-b6b7-7001fb3e933a\"]}}}"
}
```

## Использовать hello tooaccess токена доступа hello, защищенному ресурсу
Теперь служба среднего уровня hello можно использовать toohello запросы маркера приобретенных выше toomake с проверкой подлинности hello нижестоящим веб-API, параметр маркером hello в hello `Authorization` заголовок.

### Пример
```
GET /me?api-version=2013-11-08 HTTP/1.1
Host: graph.windows.net
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCIsImtpZCI6InowMzl6ZHNGdWl6cEJmQlZLMVRuMjVRSFlPMCJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRvd3MubmV0IiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvMjYwMzljY2UtNDg5ZC00MDAyLTgyOTMtNWIwYzUxMzRlYWNiLyIsImlhdCI6MTQ5MzQyMzE2OCwibmJmIjoxNDkzNDIzMTY4LCJleHAiOjE0OTM0NjY5NTEsImFjciI6IjEiLCJhaW8iOiJBU1FBMi84REFBQUE1NnZGVmp0WlNjNWdBVWwrY1Z0VFpyM0VvV2NvZEoveWV1S2ZqcTZRdC9NPSIsImFtciI6WyJwd2QiXSwiYXBwaWQiOiI2MjUzOTFhZi1jNjc1LTQzZTUtOGU0NC1lZGQzZTMwY2ViMTUiLCJhcHBpZGFjciI6IjEiLCJlX2V4cCI6MzAyNjgzLCJmYW1pbHlfbmFtZSI6IlRlc3QiLCJnaXZlbl9uYW1lIjoiTmF2eWEiLCJpcGFkZHIiOiIxNjcuMjIwLjEuMTc3IiwibmFtZSI6Ik5hdnlhIFRlc3QiLCJvaWQiOiIxY2Q0YmNhYy1iODA4LTQyM2EtOWUyZi04MjdmYmIxYmI3MzkiLCJwbGF0ZiI6IjMiLCJwdWlkIjoiMTAwMzNGRkZBMTJFRDdGRSIsInNjcCI6IlVzZXIuUmVhZCIsInN1YiI6IjNKTUlaSWJlYTc1R2hfWHdDN2ZzX0JDc3kxa1l1ekZKLTUyVm1Zd0JuM3ciLCJ0aWQiOiIyNjAzOWNjZS00ODlkLTQwMDItODI5My01YjBjNTEzNGVhY2IiLCJ1bmlxdWVfbmFtZSI6Im5hdnlhQGRkb2JhbGlhbm91dGxvb2sub25taWNyb3NvZnQuY29tIiwidXBuIjoibmF2eWFAZGRvYmFsaWFub3V0bG9vay5vbm1pY3Jvc29mdC5jb20iLCJ1dGkiOiJ4Q3dmemhhLVAwV0pRT0x4Q0dnS0FBIiwidmVyIjoiMS4wIn0.cqmUVjfVbqWsxJLUI1Z4FRx1mNQAHP-L0F4EMN09r8FY9bIKeO-0q1eTdP11Nkj_k4BmtaZsTcK_mUygdMqEp9AfyVyA1HYvokcgGCW_Z6DMlVGqlIU4ssEkL9abgl1REHElPhpwBFFBBenOk9iHddD1GddTn6vJbKC3qAaNM5VarjSPu50bVvCrqKNvFixTb5bbdnSz-Qr6n6ACiEimiI1aNOPR2DeKUyWBPaQcU5EAK0ef5IsVJC1yaYDlAcUYIILMDLCD9ebjsy0t9pj_7lvjzUSrbMdSCCdzCqez_MSNxrk1Nu9AecugkBYp3UVUZOIyythVrj6-sVvLZKUutQ
```

## Дальнейшие действия
Дополнительные сведения о протоколах OAuth 2.0 hello и другим способом tooperform службы tooservice проверки подлинности с использованием учетных данных клиента.
* [Служба проверки подлинности tooservice с помощью предоставления учетных данных клиента OAuth 2.0 в Azure AD](active-directory-protocols-oauth-service-to-service.md)
* [OAuth 2.0 в Azure AD](active-directory-protocols-oauth-code.md)
