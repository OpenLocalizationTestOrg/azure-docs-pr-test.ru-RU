---
title: "aaaSecure API-интерфейсов с помощью проверки подлинности сертификата клиента в службе управления API - интерфейса API управления Azure | Документы Microsoft"
description: "Узнайте, как toosecure доступ к tooAPIs, с помощью сертификатов клиентов"
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
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="4830c-103">Toosecure API-интерфейсы, с помощью клиентского сертификата проверки подлинности в службе управления API</span><span class="sxs-lookup"><span data-stu-id="4830c-103">How toosecure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="4830c-104">Управление API предоставляет hello возможность toosecure доступа tooAPIs (т. е. клиент tooAPI управления) с помощью сертификатов клиента.</span><span class="sxs-lookup"><span data-stu-id="4830c-104">API Management provides hello capability toosecure access tooAPIs (i.e., client tooAPI Management) using client certificates.</span></span> <span data-ttu-id="4830c-105">В настоящее время вы можете проверить hello отпечаток сертификата клиента для требуемого значения.</span><span class="sxs-lookup"><span data-stu-id="4830c-105">Currently, you can check hello thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="4830c-106">Можно также проверить, что отпечаток hello с существующие сертификаты отправлен tooAPI управления.</span><span class="sxs-lookup"><span data-stu-id="4830c-106">You can also check hello thumbprint against existing certificates uploaded tooAPI Management.</span></span>  

<span data-ttu-id="4830c-107">Сведения о защите доступа toohello внутренней службой API-интерфейса с помощью клиентских сертификатов (т. е. API управления tooback-end) см. в разделе [как toosecure серверными службами с помощью клиента сертификат проверки подлинности](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="4830c-107">For information about securing access toohello back-end service of an API using client certificates (i.e., API Management tooback-end), see [How toosecure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-hello-expiration-date"></a><span data-ttu-id="4830c-108">Дата окончания срока действия проверки hello</span><span class="sxs-lookup"><span data-stu-id="4830c-108">Checking hello expiration date</span></span>

<span data-ttu-id="4830c-109">Ниже политик может быть настроенный toocheck, если истек срок действия сертификата hello:</span><span class="sxs-lookup"><span data-stu-id="4830c-109">Below policies can be configured toocheck if hello certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a><span data-ttu-id="4830c-110">Проверка издателя hello и темы</span><span class="sxs-lookup"><span data-stu-id="4830c-110">Checking hello issuer and subject</span></span>

<span data-ttu-id="4830c-111">Ниже политик может быть настроенный toocheck hello издатель и субъект сертификата клиента:</span><span class="sxs-lookup"><span data-stu-id="4830c-111">Below policies can be configured toocheck hello issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a><span data-ttu-id="4830c-112">Проверка отпечаток hello</span><span class="sxs-lookup"><span data-stu-id="4830c-112">Checking hello thumbprint</span></span>

<span data-ttu-id="4830c-113">Ниже политик может быть настроенный toocheck hello отпечаток сертификата клиента:</span><span class="sxs-lookup"><span data-stu-id="4830c-113">Below policies can be configured toocheck hello thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a><span data-ttu-id="4830c-114">Проверка отпечаток от сертификатов отправлен tooAPI управления</span><span class="sxs-lookup"><span data-stu-id="4830c-114">Checking a thumbprint against certificates uploaded tooAPI Management</span></span>

<span data-ttu-id="4830c-115">Hello следующем примере показано, как toocheck hello отпечаток сертификата клиента от сертификатов отправлен tooAPI управления:</span><span class="sxs-lookup"><span data-stu-id="4830c-115">hello following example shows how toocheck hello thumbprint of a client certificate against certificates uploaded tooAPI Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="4830c-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4830c-116">Next step</span></span>

*  [<span data-ttu-id="4830c-117">Как toosecure серверными службами с помощью клиента сертификат проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="4830c-117">How toosecure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="4830c-118">Как сертификаты tooupload</span><span class="sxs-lookup"><span data-stu-id="4830c-118">How tooupload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

