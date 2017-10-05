---
title: "Защита API-интерфейсов с помощью аутентификации на основе сертификата клиента в службе управления API Azure | Документация Майкрософт"
description: "Узнайте, как обеспечить безопасный доступ к API-интерфейсам с помощью сертификатов клиентов"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="fd60e-103">Защита API-интерфейсов с помощью аутентификации на основе сертификата клиента в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="fd60e-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="fd60e-104">Служба управления API помогает защитить доступ к API-интерфейсам (например, осуществляемый клиентом к службе управления API) с помощью сертификатов клиента.</span><span class="sxs-lookup"><span data-stu-id="fd60e-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="fd60e-105">Сейчас можно проверить отпечаток сертификата клиента для сопоставления с требуемым значением.</span><span class="sxs-lookup"><span data-stu-id="fd60e-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="fd60e-106">Можно также сопоставить отпечаток с существующими сертификатами, отправленными в службу управления API.</span><span class="sxs-lookup"><span data-stu-id="fd60e-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="fd60e-107">Сведения о защите серверных служб API с помощью сертификата клиента (например, управления API для серверной части) см. в статье [Защита фоновых служб посредством проверки подлинности с помощью сертификата клиента в службе Azure API Management](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates).</span><span class="sxs-lookup"><span data-stu-id="fd60e-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="fd60e-108">Проверка даты окончания срока действия</span><span class="sxs-lookup"><span data-stu-id="fd60e-108">Checking the expiration date</span></span>

<span data-ttu-id="fd60e-109">Следующие политики можно настроить для проверки даты окончания срока действия сертификата:</span><span class="sxs-lookup"><span data-stu-id="fd60e-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="fd60e-110">Проверка издателя и субъекта</span><span class="sxs-lookup"><span data-stu-id="fd60e-110">Checking the issuer and subject</span></span>

<span data-ttu-id="fd60e-111">Следующие политики можно настроить для проверки издателя и субъекта сертификата клиента:</span><span class="sxs-lookup"><span data-stu-id="fd60e-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="fd60e-112">Проверка отпечатка</span><span class="sxs-lookup"><span data-stu-id="fd60e-112">Checking the thumbprint</span></span>

<span data-ttu-id="fd60e-113">Следующие политики можно настроить для проверки отпечатка сертификата клиента:</span><span class="sxs-lookup"><span data-stu-id="fd60e-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="fd60e-114">Проверка отпечатка на соответствие сертификатам, переданным в службу управления API</span><span class="sxs-lookup"><span data-stu-id="fd60e-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="fd60e-115">В примере ниже показано, как проверить отпечаток сертификата клиента на соответствие сертификатам, переданным в службу управления API.</span><span class="sxs-lookup"><span data-stu-id="fd60e-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="fd60e-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd60e-116">Next step</span></span>

*  [<span data-ttu-id="fd60e-117">Как защитить серверные службы с помощью аутентификации на основе сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="fd60e-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="fd60e-118">Как передавать сертификаты</span><span class="sxs-lookup"><span data-stu-id="fd60e-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

