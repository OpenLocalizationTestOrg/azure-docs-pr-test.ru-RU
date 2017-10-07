---
title: "aaaAzure tooService AD службы проверки подлинности с помощью OAuth2.0 | Документы Microsoft"
description: "В этой статье описывается, как tooimplement toouse HTTP сообщения службы tooservice проверки подлинности с помощью поток предоставления учетных данных клиента OAuth2.0 hello."
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Вызовы tooservice службы с использованием учетных данных клиента (общий секрет или сертификат)
Hello поток по разрешений учетных данных OAuth 2.0 клиента разрешает веб-службы (*конфиденциальному клиенту*) toouse свои собственные учетные данные вместо олицетворения пользователя, tooauthenticate при вызове другой веб-службы. В этом сценарии клиент hello — обычно средний уровень веб-службы, служба управляющей программы или веб-сайта. Для более высокого уровня надежности Azure AD также позволяет hello вызов службы toouse сертификат (а не общий секрет) в качестве учетных данных.

## Схема потока предоставления учетных данных клиента
Hello следующая диаграмма объясняет, как учетные данные клиента hello предоставить потока работает в Azure Active Directory (Azure AD).

![Поток предоставления учетных данных клиента OAuth2.0](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. Hello клиентское приложение выполняет проверку подлинности toohello конечная точка выдачи токена Azure AD и запрашивает маркер доступа.
2. проблемы конечной точки выдачи маркера Hello Azure AD hello маркер доступа.
3. маркер доступа Hello — используется tooauthenticate toohello защищенному ресурсу.
4. Данные из защищенных ресурсов hello возвращается toohello веб-приложения.

## Регистрация службы hello в Azure AD
Зарегистрируйте hello вызова службы и hello Получение службы в Azure Active Directory (Azure AD). Подробные инструкции см. в статье [Интеграция приложений с Azure Active Directory](active-directory-integrating-applications.md).

## Запрос маркера доступа
toorequest маркера доступа используйте конечную точку HTTP POST toohello Azure AD конкретного клиента.

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## Запрос маркера взаимного доступа между службами
Существует два варианта, в зависимости от того, является ли клиентское приложение hello выбирает toobe защищен общий секрет или сертификат.

### Первый сценарий: запрос маркера доступа с помощью общего секрета
При использовании общего секрета, запрос маркера доступа для служб содержит hello следующие параметры:

| Параметр |  | Описание |
| --- | --- | --- |
| grant_type |обязательно |Указывает запрошенный hello предоставить тип. В потоке предоставления учетных данных клиента hello значение должно быть **значение client_credentials**. |
| client_id |обязательно |Указывает идентификатор клиента Azure AD hello hello вызова веб-службы. вызов идентификатор клиента приложения, в hello hello toofind [портал Azure](https://portal.azure.com), нажмите кнопку **Active Directory**, перейдите в каталог, выберите приложение hello. Hello client_id — hello *идентификатор приложения* |
| client_secret |обязательно |Введите ключ, зарегистрированный для вызова веб-службы или управляющей программы приложения в Azure AD hello. toocreate ключ в hello портала Azure щелкните **Active Directory**перейдите в каталог, выберите приложение hello, **параметры**, нажмите кнопку **ключей**, и добавьте раздел.|
| resource |обязательно |Введите hello URI идентификатора приложения hello, получение веб-службы. hello toofind URI идентификатора приложения, в hello портала Azure щелкните **Active Directory**, перейдите в каталог, выберите служебное приложение hello и нажмите кнопку **параметры** и **свойства** |

#### Пример
Hello следующие HTTP POST запрашивает токен доступа для веб-службы https://service.contoso.com/ hello. Hello `client_id` идентифицирует hello веб-службу, которая запрашивает токен доступа hello.

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### Второй сценарий: запрос маркера доступа с помощью сертификата
Запрос маркера доступа для служб с помощью сертификата содержит hello следующие параметры:

| Параметр |  | Описание |
| --- | --- | --- |
| grant_type |обязательно |Указывает hello запрошенный тип ответа. В потоке предоставления учетных данных клиента hello значение должно быть **значение client_credentials**. |
| client_id |обязательно |Указывает идентификатор клиента Azure AD hello hello вызова веб-службы. вызов идентификатор клиента приложения, в hello hello toofind [портал Azure](https://portal.azure.com), нажмите кнопку **Active Directory**, перейдите в каталог, выберите приложение hello. Hello client_id — hello *идентификатор приложения* |
| client_assertion_type |обязательно |должно быть значение Hello`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |обязательно | Утверждение (веб-маркера JSON), необходимо toocreate и сертификата входа со слова hello зарегистрирован как учетные данные для приложения. Узнайте, как [учетные данные сертификатов](active-directory-certificate-credentials.md) toolearn как tooregister вашего сертификата и hello формата hello утверждения.|
| resource | обязательно |Введите hello URI идентификатора приложения hello, получение веб-службы. hello toofind URI идентификатора приложения, в hello портала Azure щелкните **Active Directory**, щелкните каталог hello, выберите приложение hello и нажмите кнопку **Настройка**. |

Обратите внимание, что параметры hello являются почти hello же, как в случае hello запроса hello, общий секрет, за исключением того, что параметр client_secret hello заменяется два параметра: client_assertion_type и client_assertion.

#### Пример
Привет, выполнив HTTP POST запрашивает токен доступа для веб-службы https://service.contoso.com/ hello с сертификатом. Hello `client_id` идентифицирует hello веб-службу, которая запрашивает токен доступа hello.

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### Ответ маркера взаимного доступа между службами

Успешный ответ содержит ответ JSON OAuth 2.0 с hello следующие параметры:

| Параметр | Описание |
| --- | --- |
| access_token |Hello запрашиваемый маркер доступа. Hello вызова веб-службы можно использовать этот токен tooauthenticate toohello, получение веб-службы. |
| token_type |Указывает значение типа токена hello. Здравствуйте, только тип, который поддерживает Azure AD является **носителя**. Дополнительные сведения о маркерах носителя см. в разделе hello [OAuth 2.0 Authorization Framework: использование токенов предъявителя (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt). |
| expires_in |Как долго маркер доступа hello является действительным (в секундах). |
| expires_on |Hello время истечения срока действия маркера доступа hello. Hello Дата представляется в виде hello число секунд с 1970-01-01T0:0:0Z UTC до времени истечения срока действия hello. Это значение определяет используемые toodetermine hello времени жизни кэшированных маркеров. |
| not_before |время Hello, из которого hello маркер доступа был готов к использованию. Hello Дата представляется в виде hello число секунд с 1970-01-01T0:0:0Z UTC до времени действия маркера hello.|
| resource |Здравствуйте, URI идентификатора приложения hello, получение веб-службы. |

#### Пример ответа
Hello следующем примере показан запрос tooa успех ответа tooa токена доступа веб-службы.

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## См. также
* [OAuth 2.0 в Azure AD](active-directory-protocols-oauth-code.md)
* [Пример на языке C# hello вызова tooservice службы с помощью общего секрета](https://github.com/Azure-Samples/active-directory-dotnet-daemon) и [пример на языке C# hello вызова tooservice службы с помощью сертификата](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
