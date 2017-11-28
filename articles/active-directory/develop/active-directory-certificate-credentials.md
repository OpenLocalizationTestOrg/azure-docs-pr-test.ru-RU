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
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="f50cb-103">Учетные данные сертификата для аутентификации приложения</span><span class="sxs-lookup"><span data-stu-id="f50cb-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="f50cb-104">Azure Active Directory позволяет toouse приложения свои собственные учетные данные для проверки подлинности, например, в hello предоставления учетных данных клиента OAuth 2.0 и hello от имени представляет поток.</span><span class="sxs-lookup"><span data-stu-id="f50cb-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="f50cb-105">Одним из учетных данных, который может использоваться является утверждением JSON Web Token(JWT), подписанным сертификатом, которому принадлежит приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f50cb-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="f50cb-106">Формат утверждения hello</span><span class="sxs-lookup"><span data-stu-id="f50cb-106">Format of hello assertion</span></span>
<span data-ttu-id="f50cb-107">Утверждение hello toocompute, может понадобиться toouse один hello много [веб-маркера JSON](https://jwt.io/) библиотеки на языке hello по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="f50cb-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="f50cb-108">Hello информацию, сопровождающих hello маркера можно:</span><span class="sxs-lookup"><span data-stu-id="f50cb-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="f50cb-109">Заголовок</span><span class="sxs-lookup"><span data-stu-id="f50cb-109">Header</span></span>

| <span data-ttu-id="f50cb-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="f50cb-110">Parameter</span></span> |  <span data-ttu-id="f50cb-111">Комментарий</span><span class="sxs-lookup"><span data-stu-id="f50cb-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="f50cb-112">Должен иметь значение **RS256**</span><span class="sxs-lookup"><span data-stu-id="f50cb-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="f50cb-113">Должен иметь значение **JWT**</span><span class="sxs-lookup"><span data-stu-id="f50cb-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="f50cb-114">Должно быть hello отпечаток сертификата X.509 SHA-1</span><span class="sxs-lookup"><span data-stu-id="f50cb-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="f50cb-115">Утверждения (полезные данные)</span><span class="sxs-lookup"><span data-stu-id="f50cb-115">Claims (Payload)</span></span>

| <span data-ttu-id="f50cb-116">Параметр</span><span class="sxs-lookup"><span data-stu-id="f50cb-116">Parameter</span></span> |  <span data-ttu-id="f50cb-117">Комментарий</span><span class="sxs-lookup"><span data-stu-id="f50cb-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="f50cb-118">Аудитория: параметр должен иметь значение **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="f50cb-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="f50cb-119">Дата окончания срока действия: hello Дата истечения срока действия маркера hello.</span><span class="sxs-lookup"><span data-stu-id="f50cb-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="f50cb-120">Hello время представляется в виде hello количество секунд от 1 января 1970 г. (1970-01-01T0:0:0Z) UTC до истечения срока действия hello время hello действия маркера.</span><span class="sxs-lookup"><span data-stu-id="f50cb-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="f50cb-121">Поставщик: должно быть hello client_id (идентификатор приложения hello клиент службы)</span><span class="sxs-lookup"><span data-stu-id="f50cb-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="f50cb-122">GUID: hello JWT ID</span><span class="sxs-lookup"><span data-stu-id="f50cb-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="f50cb-123">Не было: hello даты до какие hello не может использоваться токен.</span><span class="sxs-lookup"><span data-stu-id="f50cb-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="f50cb-124">Hello время представляется в виде hello количество секунд от 1 января 1970 г. (1970-01-01T0:0:0Z) UTC до выдачи токена hello hello времени.</span><span class="sxs-lookup"><span data-stu-id="f50cb-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="f50cb-125">Тема: как для `iss`, должно быть hello client_id (идентификатор приложения hello клиент службы)</span><span class="sxs-lookup"><span data-stu-id="f50cb-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="f50cb-126">Подпись</span><span class="sxs-lookup"><span data-stu-id="f50cb-126">Signature</span></span>
<span data-ttu-id="f50cb-127">Hello подпись вычисляется применение hello сертификат, как описано в hello [спецификация JSON Web Token RFC7519](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="f50cb-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="f50cb-128">Пример декодированного утверждения JWT</span><span class="sxs-lookup"><span data-stu-id="f50cb-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="f50cb-129">Пример закодированного утверждения JWT</span><span class="sxs-lookup"><span data-stu-id="f50cb-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="f50cb-130">Следующая строка Hello приведен пример кодировке утверждения.</span><span class="sxs-lookup"><span data-stu-id="f50cb-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="f50cb-131">Если внимательно ее изучить, то можно заметить, что она состоит из трех разделов, разделенных точками (.).</span><span class="sxs-lookup"><span data-stu-id="f50cb-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="f50cb-132">Первый раздел Hello кодирует заголовок hello, hello второй полезных данных hello, и hello последним, является hello подписью, вычисленной с сертификатами hello из содержимого hello hello первых двух разделов.</span><span class="sxs-lookup"><span data-stu-id="f50cb-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="f50cb-133">Регистрация сертификат в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f50cb-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="f50cb-134">tooassociate hello учетных данных сертификата с hello клиентского приложения в Azure AD необходимо tooedit манифест приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f50cb-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="f50cb-135">Необходимо наличие удержание сертификата, toocompute:</span><span class="sxs-lookup"><span data-stu-id="f50cb-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="f50cb-136">`$base64Thumbprint`, который Здравствуйте, Кодировка base64 сертификата hello хэш</span><span class="sxs-lookup"><span data-stu-id="f50cb-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="f50cb-137">`$base64Value`, который Здравствуйте, кодирование base64 hello необработанные данные сертификата</span><span class="sxs-lookup"><span data-stu-id="f50cb-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="f50cb-138">необходимо также tooprovide ключ hello tooidentify GUID в манифесте приложения hello (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="f50cb-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="f50cb-139">Откройте манифест приложения hello в hello регистрации приложения Azure для клиентского приложения hello и замените hello *keyCredentials* свойство своими данными новый сертификат с помощью hello следующие схемы:</span><span class="sxs-lookup"><span data-stu-id="f50cb-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
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

<span data-ttu-id="f50cb-140">Сохранить манифест приложения toohello hello изменения и загрузить tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="f50cb-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="f50cb-141">Свойство keyCredentials Hello является несколькими значениями, поэтому может отправить несколько сертификатов обширные возможности управления ключами.</span><span class="sxs-lookup"><span data-stu-id="f50cb-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
