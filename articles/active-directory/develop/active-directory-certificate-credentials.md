---
title: "Учетные данные сертификата в Azure AD | Документация Майкрософт"
description: "В этой статье рассматривается регистрация и использование учетных данных сертификата для аутентификации приложения."
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
ms.openlocfilehash: 08bb5140bb35bbd120aaa506afeab8ad247f81e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="946b9-103">Учетные данные сертификата для аутентификации приложения</span><span class="sxs-lookup"><span data-stu-id="946b9-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="946b9-104">Azure Active Directory позволяет приложению использовать для аутентификации свои собственные учетные данные, например, в потоке предоставления учетных данных клиента OAuth 2.0 и потоке On-Behalf-Of.</span><span class="sxs-lookup"><span data-stu-id="946b9-104">Azure Active Directory allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow and the On-Behalf-Of flow.</span></span>
<span data-ttu-id="946b9-105">Одной из форм учетных данных, которая может использоваться, является утверждение JSON Web Token (JWT), подписанное с помощью сертификата приложения.</span><span class="sxs-lookup"><span data-stu-id="946b9-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="format-of-the-assertion"></a><span data-ttu-id="946b9-106">Формат утверждения</span><span class="sxs-lookup"><span data-stu-id="946b9-106">Format of the assertion</span></span>
<span data-ttu-id="946b9-107">Чтобы сформировать утверждение, воспользуйтесь одной из многих библиотек [JSON Web Token](https://jwt.io/) на удобном для вас языке.</span><span class="sxs-lookup"><span data-stu-id="946b9-107">To compute the assertion, you probably want to use one of the many [JSON Web Token](https://jwt.io/) libraries in the language of your choice.</span></span> <span data-ttu-id="946b9-108">Маркер содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="946b9-108">The information carried by the token is:</span></span>

#### <a name="header"></a><span data-ttu-id="946b9-109">Заголовок</span><span class="sxs-lookup"><span data-stu-id="946b9-109">Header</span></span>

| <span data-ttu-id="946b9-110">Параметр</span><span class="sxs-lookup"><span data-stu-id="946b9-110">Parameter</span></span> |  <span data-ttu-id="946b9-111">Комментарий</span><span class="sxs-lookup"><span data-stu-id="946b9-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="946b9-112">Должен иметь значение **RS256**</span><span class="sxs-lookup"><span data-stu-id="946b9-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="946b9-113">Должен иметь значение **JWT**</span><span class="sxs-lookup"><span data-stu-id="946b9-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="946b9-114">Это должен быть отпечаток SHA-1 сертификата X.509</span><span class="sxs-lookup"><span data-stu-id="946b9-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="946b9-115">Утверждения (полезные данные)</span><span class="sxs-lookup"><span data-stu-id="946b9-115">Claims (Payload)</span></span>

| <span data-ttu-id="946b9-116">Параметр</span><span class="sxs-lookup"><span data-stu-id="946b9-116">Parameter</span></span> |  <span data-ttu-id="946b9-117">Комментарий</span><span class="sxs-lookup"><span data-stu-id="946b9-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="946b9-118">Аудитория: параметр должен иметь значение **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span><span class="sxs-lookup"><span data-stu-id="946b9-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="946b9-119">Срок действия: дата, когда истекает срок действия маркера.</span><span class="sxs-lookup"><span data-stu-id="946b9-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="946b9-120">Время представлено как количество секунд с 1 января 1970 года (1970-01-01T0:0:0Z) в формате UTC до истечения срока действия маркера.</span><span class="sxs-lookup"><span data-stu-id="946b9-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="946b9-121">Издатель: параметр должен иметь значение client_id (идентификатор приложения службы клиента)</span><span class="sxs-lookup"><span data-stu-id="946b9-121">Issuer: should be the client_id (Application Id of the client service)</span></span> |
| `jti` | <span data-ttu-id="946b9-122">GUID: идентификатор JWT</span><span class="sxs-lookup"><span data-stu-id="946b9-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="946b9-123">Не ранее: дата, до которой маркер не может использоваться.</span><span class="sxs-lookup"><span data-stu-id="946b9-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="946b9-124">Время представлено как количество секунд с 1 января 1970 года (1970-01-01T0:0:0Z) в формате UTC до времени выдачи маркера.</span><span class="sxs-lookup"><span data-stu-id="946b9-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="946b9-125">Субъект: параметр должен иметь значение client_id (идентификатор приложения службы клиента), как и `iss`</span><span class="sxs-lookup"><span data-stu-id="946b9-125">Subject: As for `iss`, should be the client_id (Application Id of the client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="946b9-126">Подпись</span><span class="sxs-lookup"><span data-stu-id="946b9-126">Signature</span></span>
<span data-ttu-id="946b9-127">Подпись формируется через применение сертификата, как описано в [документе RFC7519 о спецификации JSON Web Token](https://tools.ietf.org/html/rfc7519).</span><span class="sxs-lookup"><span data-stu-id="946b9-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="946b9-128">Пример декодированного утверждения JWT</span><span class="sxs-lookup"><span data-stu-id="946b9-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="946b9-129">Пример закодированного утверждения JWT</span><span class="sxs-lookup"><span data-stu-id="946b9-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="946b9-130">Ниже приводится строка, которая является примером закодированного утверждения.</span><span class="sxs-lookup"><span data-stu-id="946b9-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="946b9-131">Если внимательно ее изучить, то можно заметить, что она состоит из трех разделов, разделенных точками (.).</span><span class="sxs-lookup"><span data-stu-id="946b9-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="946b9-132">Первый раздел кодирует заголовок, второй — полезные данные, а последний является подписью, сформированной с помощью сертификатов на основе содержимого первых двух разделов.</span><span class="sxs-lookup"><span data-stu-id="946b9-132">The first section encodes the header, the second the payload, and the last is the signature computed with the certificates from the content of the first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="946b9-133">Регистрация сертификат в Azure AD</span><span class="sxs-lookup"><span data-stu-id="946b9-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="946b9-134">Чтобы связать учетные данные сертификата с клиентским приложением в Azure AD, необходимо изменить манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="946b9-134">To associate the certificate credential with the client application in Azure AD, you need to edit the application manifest.</span></span>
<span data-ttu-id="946b9-135">Получив сертификат, необходимо вычислить следующие значения:</span><span class="sxs-lookup"><span data-stu-id="946b9-135">Having hold of a certificate, you need to compute:</span></span>
- <span data-ttu-id="946b9-136">`$base64Thumbprint` — хэш сертификата в кодировке base64;</span><span class="sxs-lookup"><span data-stu-id="946b9-136">`$base64Thumbprint`, which is the base64 encoding of the certificate Hash</span></span>
- <span data-ttu-id="946b9-137">`$base64Value` — необработанные данные сертификата в кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="946b9-137">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="946b9-138">Также необходимо предоставить идентификатор GUID для определения ключа в манифесте приложения (`$keyId`).</span><span class="sxs-lookup"><span data-stu-id="946b9-138">you also need to provide a GUID to identify the key in the application manifest (`$keyId`)</span></span>

<span data-ttu-id="946b9-139">При регистрации клиентского приложения в Azure откройте манифест приложения и замените свойство *keyCredentials* данными нового сертификата, используя следующую схему:</span><span class="sxs-lookup"><span data-stu-id="946b9-139">In the Azure app registration for the client application, open the application manifest, and replace the *keyCredentials* property with your new certificate information using the following schema:</span></span>
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

<span data-ttu-id="946b9-140">Сохраните изменения в манифесте приложения и отправьте его в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="946b9-140">Save the edits to the application manifest, and upload to Azure AD.</span></span> <span data-ttu-id="946b9-141">Свойство keyCredentials является многозначным, поэтому для расширенного управления ключами можно передать несколько сертификатов.</span><span class="sxs-lookup"><span data-stu-id="946b9-141">The keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
