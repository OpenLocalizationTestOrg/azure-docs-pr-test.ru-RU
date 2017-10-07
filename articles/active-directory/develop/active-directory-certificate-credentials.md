---
title: "учетные данные aaaCertificate в Azure AD | Документы Microsoft"
description: "В этой статье рассматриваются hello регистрации и использования учетных данных сертификата для проверки подлинности приложения"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a>Учетные данные сертификата для аутентификации приложения

Azure Active Directory позволяет toouse приложения свои собственные учетные данные для проверки подлинности, например, в hello предоставления учетных данных клиента OAuth 2.0 и hello от имени представляет поток.
Одним из учетных данных, который может использоваться является утверждением JSON Web Token(JWT), подписанным сертификатом, которому принадлежит приложения hello.

## <a name="format-of-hello-assertion"></a>Формат утверждения hello
Утверждение hello toocompute, может понадобиться toouse один hello много [веб-маркера JSON](https://jwt.io/) библиотеки на языке hello по своему усмотрению. Hello информацию, сопровождающих hello маркера можно:

#### <a name="header"></a>Заголовок

| Параметр |  Комментарий |
| --- | --- | --- |
| `alg` | Должен иметь значение **RS256** |
| `typ` | Должен иметь значение **JWT** |
| `x5t` | Должно быть hello отпечаток сертификата X.509 SHA-1 |

#### <a name="claims-payload"></a>Утверждения (полезные данные)

| Параметр |  Комментарий |
| --- | --- | --- |
| `aud` | Аудитория: параметр должен иметь значение **https://login.microsoftonline.com/*tenant_Id*/oauth2/token** |
| `exp` | Дата окончания срока действия: hello Дата истечения срока действия маркера hello. Hello время представляется в виде hello количество секунд от 1 января 1970 г. (1970-01-01T0:0:0Z) UTC до истечения срока действия hello время hello действия маркера.|
| `iss` | Поставщик: должно быть hello client_id (идентификатор приложения hello клиент службы) |
| `jti` | GUID: hello JWT ID |
| `nbf` | Не было: hello даты до какие hello не может использоваться токен. Hello время представляется в виде hello количество секунд от 1 января 1970 г. (1970-01-01T0:0:0Z) UTC до выдачи токена hello hello времени. |
| `sub` | Тема: как для `iss`, должно быть hello client_id (идентификатор приложения hello клиент службы) |

#### <a name="signature"></a>Подпись
Hello подпись вычисляется применение hello сертификат, как описано в hello [спецификация JSON Web Token RFC7519](https://tools.ietf.org/html/rfc7519)

### <a name="example-of-a-decoded-jwt-assertion"></a>Пример декодированного утверждения JWT
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a>Пример закодированного утверждения JWT
Следующая строка Hello приведен пример кодировке утверждения. Если внимательно ее изучить, то можно заметить, что она состоит из трех разделов, разделенных точками (.).
Первый раздел Hello кодирует заголовок hello, hello второй полезных данных hello, и hello последним, является hello подписью, вычисленной с сертификатами hello из содержимого hello hello первых двух разделов.
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a>Регистрация сертификат в Azure AD
tooassociate hello учетных данных сертификата с hello клиентского приложения в Azure AD необходимо tooedit манифест приложения hello.
Необходимо наличие удержание сертификата, toocompute:
- `$base64Thumbprint`, который Здравствуйте, Кодировка base64 сертификата hello хэш
- `$base64Value`, который Здравствуйте, кодирование base64 hello необработанные данные сертификата

необходимо также tooprovide ключ hello tooidentify GUID в манифесте приложения hello (`$keyId`)

Откройте манифест приложения hello в hello регистрации приложения Azure для клиентского приложения hello и замените hello *keyCredentials* свойство своими данными новый сертификат с помощью hello следующие схемы:
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

Сохранить манифест приложения toohello hello изменения и загрузить tooAzure AD. Свойство keyCredentials Hello является несколькими значениями, поэтому может отправить несколько сертификатов обширные возможности управления ключами.
