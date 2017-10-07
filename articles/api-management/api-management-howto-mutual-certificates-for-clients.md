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
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a>Toosecure API-интерфейсы, с помощью клиентского сертификата проверки подлинности в службе управления API

Управление API предоставляет hello возможность toosecure доступа tooAPIs (т. е. клиент tooAPI управления) с помощью сертификатов клиента. В настоящее время вы можете проверить hello отпечаток сертификата клиента для требуемого значения. Можно также проверить, что отпечаток hello с существующие сертификаты отправлен tooAPI управления.  

Сведения о защите доступа toohello внутренней службой API-интерфейса с помощью клиентских сертификатов (т. е. API управления tooback-end) см. в разделе [как toosecure серверными службами с помощью клиента сертификат проверки подлинности](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)

## <a name="checking-hello-expiration-date"></a>Дата окончания срока действия проверки hello

Ниже политик может быть настроенный toocheck, если истек срок действия сертификата hello:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a>Проверка издателя hello и темы

Ниже политик может быть настроенный toocheck hello издатель и субъект сертификата клиента:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a>Проверка отпечаток hello

Ниже политик может быть настроенный toocheck hello отпечаток сертификата клиента:

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a>Проверка отпечаток от сертификатов отправлен tooAPI управления

Hello следующем примере показано, как toocheck hello отпечаток сертификата клиента от сертификатов отправлен tooAPI управления: 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a>Дальнейшие действия

*  [Как toosecure серверными службами с помощью клиента сертификат проверки подлинности](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [Как сертификаты tooupload](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

