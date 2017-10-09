---
title: "Исходящая проверка подлинности aaaScheduler"
description: "Исходящая проверка подлинности планировщика"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 6707f82b-7e32-401b-a960-02aae7bb59cc
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2016
ms.author: deli
ms.openlocfilehash: ef713f4770b48d0a9176415e87c1042a823582e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-outbound-authentication"></a><span data-ttu-id="de182-103">Исходящая проверка подлинности планировщика</span><span class="sxs-lookup"><span data-stu-id="de182-103">Scheduler Outbound Authentication</span></span>
<span data-ttu-id="de182-104">Задания планировщика могут потребовать toocall out tooservices, который требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="de182-104">Scheduler jobs may need toocall out tooservices that require authentication.</span></span> <span data-ttu-id="de182-105">В этом случае вызванная служба способна определить, если задание планировщика hello доступ к ее ресурсам.</span><span class="sxs-lookup"><span data-stu-id="de182-105">This way, a called service can determine if hello Scheduler job can access its resources.</span></span> <span data-ttu-id="de182-106">В число таких служб входят другие службы Azure, Salesforce.com, Facebook и защищенные пользовательские веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="de182-106">Some of these services include other Azure services, Salesforce.com, Facebook, and secure custom websites.</span></span>

## <a name="adding-and-removing-authentication"></a><span data-ttu-id="de182-107">Добавление и удаление проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="de182-107">Adding and Removing Authentication</span></span>
<span data-ttu-id="de182-108">Добавление проверки подлинности tooa планировщик заданий выполняется просто — добавьте дочерний элемент JSON `authentication` toohello `request` элемент при создании или обновлении задания.</span><span class="sxs-lookup"><span data-stu-id="de182-108">Adding authentication tooa Scheduler job is simple – add a JSON child element `authentication` toohello `request` element when creating or updating a job.</span></span> <span data-ttu-id="de182-109">Секретные данные передаются toohello служба планировщика в запросе PUT, POST или PATCH — как часть hello `authentication` объекта — никогда не возвращаются в ответах.</span><span class="sxs-lookup"><span data-stu-id="de182-109">Secrets passed toohello Scheduler service in a PUT, PATCH, or POST request – as part of hello `authentication` object – are never returned in responses.</span></span> <span data-ttu-id="de182-110">В ответах секретная информация имеет toonull или может иметь открытый маркер, который представляет сущность hello с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="de182-110">In responses, secret information is set toonull or may have a public token that represents hello authenticated entity.</span></span>

<span data-ttu-id="de182-111">tooremove проверки подлинности, PUT или PATCH задания hello явным образом, параметр hello `authentication` объекта toonull.</span><span class="sxs-lookup"><span data-stu-id="de182-111">tooremove authentication, PUT or PATCH hello job explicitly, setting hello `authentication` object toonull.</span></span> <span data-ttu-id="de182-112">Никакие свойства проверки подлинности в ответе показаны не будут.</span><span class="sxs-lookup"><span data-stu-id="de182-112">You will not see any authentication properties back in response.</span></span>

<span data-ttu-id="de182-113">В настоящее время типы hello поддерживается только проверка подлинности: hello `ClientCertificate` модели (для использования сертификатов клиентов hello SSL/TLS), hello `Basic` модели (для обычной проверки подлинности) и hello `ActiveDirectoryOAuth` модели (для Active Directory OAuth Проверка подлинности.)</span><span class="sxs-lookup"><span data-stu-id="de182-113">Currently, hello only supported authentication types are hello `ClientCertificate` model (for using hello SSL/TLS client certificates), hello `Basic` model (for Basic authentication), and hello `ActiveDirectoryOAuth` model (for Active Directory OAuth authentication.)</span></span>

## <a name="request-body-for-clientcertificate-authentication"></a><span data-ttu-id="de182-114">Текст запроса для проверки подлинности ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="de182-114">Request Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="de182-115">При добавлении проверки подлинности с использованием hello `ClientCertificate` модель, указать следующие дополнительные элементы в тексте запроса hello hello.</span><span class="sxs-lookup"><span data-stu-id="de182-115">When adding authentication using hello `ClientCertificate` model, specify hello following additional elements in hello request body.</span></span>  

| <span data-ttu-id="de182-116">Элемент</span><span class="sxs-lookup"><span data-stu-id="de182-116">Element</span></span> | <span data-ttu-id="de182-117">Описание</span><span class="sxs-lookup"><span data-stu-id="de182-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="de182-118">*authentication (родительский элемент)*</span><span class="sxs-lookup"><span data-stu-id="de182-118">*authentication (parent element)*</span></span> |<span data-ttu-id="de182-119">Объект проверки подлинности для использования клиентского SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="de182-119">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="de182-120">*type*</span><span class="sxs-lookup"><span data-stu-id="de182-120">*type*</span></span> |<span data-ttu-id="de182-121">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="de182-121">Required.</span></span> <span data-ttu-id="de182-122">Тип проверки подлинности. Для SSL-сертификатов клиента, hello значение должно быть `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="de182-122">Type of authentication.For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="de182-123">*pfx*</span><span class="sxs-lookup"><span data-stu-id="de182-123">*pfx*</span></span> |<span data-ttu-id="de182-124">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="de182-124">Required.</span></span> <span data-ttu-id="de182-125">Содержимое base64-кодированном hello PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="de182-125">Base64-encoded contents of hello PFX file.</span></span> |
| <span data-ttu-id="de182-126">*password*</span><span class="sxs-lookup"><span data-stu-id="de182-126">*password*</span></span> |<span data-ttu-id="de182-127">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="de182-127">Required.</span></span> <span data-ttu-id="de182-128">Пароль tooaccess hello PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="de182-128">Password tooaccess hello PFX file.</span></span> |

## <a name="response-body-for-clientcertificate-authentication"></a><span data-ttu-id="de182-129">Текст ответа при проверке подлинности ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="de182-129">Response Body for ClientCertificate Authentication</span></span>
<span data-ttu-id="de182-130">При отправке запроса с данными проверки подлинности, hello ответ содержит следующие элементы, связанные с проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="de182-130">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="de182-131">Элемент</span><span class="sxs-lookup"><span data-stu-id="de182-131">Element</span></span> | <span data-ttu-id="de182-132">Описание</span><span class="sxs-lookup"><span data-stu-id="de182-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="de182-133">*authentication (родительский элемент)*</span><span class="sxs-lookup"><span data-stu-id="de182-133">*authentication (parent element)*</span></span> |<span data-ttu-id="de182-134">Объект проверки подлинности для использования клиентского SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="de182-134">Authentication object for using an SSL client certificate.</span></span> |
| <span data-ttu-id="de182-135">*type*</span><span class="sxs-lookup"><span data-stu-id="de182-135">*type*</span></span> |<span data-ttu-id="de182-136">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="de182-136">Type of authentication.</span></span> <span data-ttu-id="de182-137">Для SSL-сертификатов клиента, значение hello — `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="de182-137">For SSL client certificates, hello value is `ClientCertificate`.</span></span> |
| <span data-ttu-id="de182-138">*certificateThumbprint*</span><span class="sxs-lookup"><span data-stu-id="de182-138">*certificateThumbprint*</span></span> |<span data-ttu-id="de182-139">отпечаток сертификата hello Hello.</span><span class="sxs-lookup"><span data-stu-id="de182-139">hello thumbprint of hello certificate.</span></span> |
| <span data-ttu-id="de182-140">*certificateSubjectName*</span><span class="sxs-lookup"><span data-stu-id="de182-140">*certificateSubjectName*</span></span> |<span data-ttu-id="de182-141">Hello различающееся имя субъекта сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="de182-141">hello subject distinguished name of hello certificate.</span></span> |
| <span data-ttu-id="de182-142">*certificateExpiration*</span><span class="sxs-lookup"><span data-stu-id="de182-142">*certificateExpiration*</span></span> |<span data-ttu-id="de182-143">Hello срок сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="de182-143">hello expiration date of hello certificate.</span></span> |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a><span data-ttu-id="de182-144">Пример запроса REST для аутентификации ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="de182-144">Sample REST Request for ClientCertificate Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "clientcertificate",
          "password": "password",
          "pfx": "pfx key"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-clientcertificate-authentication"></a><span data-ttu-id="de182-145">Пример ответа REST для аутентификации ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="de182-145">Sample REST Response for ClientCertificate Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 858
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 56c7b40e-721a-437e-88e6-f68562a73aa8
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 1075219e-e879-4030-bc81-094e54fbabce
x-ms-routing-request-id: WESTUS:20160316T190424Z:1075219e-e879-4030-bc81-094e54fbabce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:04:23 GMT

{
  "id": "/subscriptions/1fe0abdf-581e-4dfe-9ec7-e5cb8e7b205e/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
  "type": "Microsoft.Scheduler/jobCollections/jobs",
  "name": "southeastasiajc/httpjob",
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "certificateThumbprint": "88105CG9DF9ADE75B835711D899296CB217D7055",
          "certificateExpiration": "2021-01-01T07:00:00Z",
          "certificateSubjectName": "CN=Scheduler Mgmt",
          "type": "ClientCertificate"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
    "status": {
      "nextExecutionTime": "2016-03-16T19:05:00Z",
      "executionCount": 0,
      "failureCount": 0,
      "faultedCount": 0
    }
  }
}
```

## <a name="request-body-for-basic-authentication"></a><span data-ttu-id="de182-146">Текст запроса для обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="de182-146">Request Body for Basic Authentication</span></span>
<span data-ttu-id="de182-147">При добавлении проверки подлинности с использованием hello `Basic` модель, указать следующие дополнительные элементы в тексте запроса hello hello.</span><span class="sxs-lookup"><span data-stu-id="de182-147">When adding authentication using hello `Basic` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="de182-148">Элемент</span><span class="sxs-lookup"><span data-stu-id="de182-148">Element</span></span> | <span data-ttu-id="de182-149">Описание</span><span class="sxs-lookup"><span data-stu-id="de182-149">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="de182-150">*authentication (родительский элемент)*</span><span class="sxs-lookup"><span data-stu-id="de182-150">*authentication (parent element)*</span></span> |<span data-ttu-id="de182-151">Объект проверки подлинности для использования обычной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="de182-151">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="de182-152">*type*</span><span class="sxs-lookup"><span data-stu-id="de182-152">*type*</span></span> |<span data-ttu-id="de182-153">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="de182-153">Required.</span></span> <span data-ttu-id="de182-154">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="de182-154">Type of authentication.</span></span> <span data-ttu-id="de182-155">Для обычной проверки подлинности должно быть значение hello `Basic`.</span><span class="sxs-lookup"><span data-stu-id="de182-155">For Basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="de182-156">*username*</span><span class="sxs-lookup"><span data-stu-id="de182-156">*username*</span></span> |<span data-ttu-id="de182-157">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="de182-157">Required.</span></span> <span data-ttu-id="de182-158">Tooauthenticate имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="de182-158">Username tooauthenticate.</span></span> |
| <span data-ttu-id="de182-159">*password*</span><span class="sxs-lookup"><span data-stu-id="de182-159">*password*</span></span> |<span data-ttu-id="de182-160">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="de182-160">Required.</span></span> <span data-ttu-id="de182-161">Tooauthenticate пароль.</span><span class="sxs-lookup"><span data-stu-id="de182-161">Password tooauthenticate.</span></span> |

## <a name="response-body-for-basic-authentication"></a><span data-ttu-id="de182-162">Текст ответа при обычной проверке подлинности</span><span class="sxs-lookup"><span data-stu-id="de182-162">Response Body for Basic Authentication</span></span>
<span data-ttu-id="de182-163">При отправке запроса с данными проверки подлинности, hello ответ содержит следующие элементы, связанные с проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="de182-163">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="de182-164">Элемент</span><span class="sxs-lookup"><span data-stu-id="de182-164">Element</span></span> | <span data-ttu-id="de182-165">Описание</span><span class="sxs-lookup"><span data-stu-id="de182-165">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="de182-166">*authentication (родительский элемент)*</span><span class="sxs-lookup"><span data-stu-id="de182-166">*authentication (parent element)*</span></span> |<span data-ttu-id="de182-167">Объект проверки подлинности для использования обычной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="de182-167">Authentication object for using Basic authentication.</span></span> |
| <span data-ttu-id="de182-168">*type*</span><span class="sxs-lookup"><span data-stu-id="de182-168">*type*</span></span> |<span data-ttu-id="de182-169">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="de182-169">Type of authentication.</span></span> <span data-ttu-id="de182-170">Для обычной проверки подлинности значение hello — `Basic`.</span><span class="sxs-lookup"><span data-stu-id="de182-170">For Basic authentication, hello value is `Basic`.</span></span> |
| <span data-ttu-id="de182-171">*username*</span><span class="sxs-lookup"><span data-stu-id="de182-171">*username*</span></span> |<span data-ttu-id="de182-172">Hello проверку подлинности имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="de182-172">hello authenticated username.</span></span> |

## <a name="sample-rest-request-for-basic-authentication"></a><span data-ttu-id="de182-173">Пример запроса REST для обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="de182-173">Sample REST Request for Basic Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 562
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "type": "basic",
          "username": "user",
          "password": "password"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-basic-authentication"></a><span data-ttu-id="de182-174">Пример ответа REST для обычной проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="de182-174">Sample REST Response for Basic Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 701
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: a2dcb9cd-1aea-4887-8893-d81273a8cf04
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 7816f222-6ea7-468d-b919-e6ddebbd7e95
x-ms-routing-request-id: WESTUS:20160316T190506Z:7816f222-6ea7-468d-b919-e6ddebbd7e95
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:05:06 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "username":"user1",
               "type":"Basic"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "nextExecutionTime":"2016-03-16T19:06:00Z",
         "executionCount":0,
         "failureCount":0,
         "faultedCount":0
      }
   }
}
```

## <a name="request-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="de182-175">Текст запроса для проверки подлинности ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="de182-175">Request Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="de182-176">При добавлении проверки подлинности с использованием hello `ActiveDirectoryOAuth` модель, указать следующие дополнительные элементы в тексте запроса hello hello.</span><span class="sxs-lookup"><span data-stu-id="de182-176">When adding authentication using hello `ActiveDirectoryOAuth` model, specify hello following additional elements in hello request body.</span></span>

| <span data-ttu-id="de182-177">Элемент</span><span class="sxs-lookup"><span data-stu-id="de182-177">Element</span></span> | <span data-ttu-id="de182-178">Описание</span><span class="sxs-lookup"><span data-stu-id="de182-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="de182-179">*authentication (родительский элемент)*</span><span class="sxs-lookup"><span data-stu-id="de182-179">*authentication (parent element)*</span></span> |<span data-ttu-id="de182-180">Объект проверки подлинности для использования проверки подлинности ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="de182-180">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="de182-181">*type*</span><span class="sxs-lookup"><span data-stu-id="de182-181">*type*</span></span> |<span data-ttu-id="de182-182">обязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="de182-182">Required.</span></span> <span data-ttu-id="de182-183">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="de182-183">Type of authentication.</span></span> <span data-ttu-id="de182-184">Для проверки подлинности ActiveDirectoryOAuth hello значение должно быть `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="de182-184">For ActiveDirectoryOAuth authentication, hello value must be `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="de182-185">*tenant*</span><span class="sxs-lookup"><span data-stu-id="de182-185">*tenant*</span></span> |<span data-ttu-id="de182-186">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="de182-186">Required.</span></span> <span data-ttu-id="de182-187">Здравствуйте, идентификатор клиента для клиента hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de182-187">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="de182-188">*audience*</span><span class="sxs-lookup"><span data-stu-id="de182-188">*audience*</span></span> |<span data-ttu-id="de182-189">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="de182-189">Required.</span></span> <span data-ttu-id="de182-190">Этот параметр задается toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="de182-190">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="de182-191">*clientId*</span><span class="sxs-lookup"><span data-stu-id="de182-191">*clientId*</span></span> |<span data-ttu-id="de182-192">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="de182-192">Required.</span></span> <span data-ttu-id="de182-193">Укажите идентификатор клиента hello для hello приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de182-193">Provide hello client identifier for hello Azure AD application.</span></span> |
| <span data-ttu-id="de182-194">*secret*</span><span class="sxs-lookup"><span data-stu-id="de182-194">*secret*</span></span> |<span data-ttu-id="de182-195">Обязательный элемент.</span><span class="sxs-lookup"><span data-stu-id="de182-195">Required.</span></span> <span data-ttu-id="de182-196">Секрет клиента hello, который запрашивает токен hello.</span><span class="sxs-lookup"><span data-stu-id="de182-196">Secret of hello client that is requesting hello token.</span></span> |

### <a name="determining-your-tenant-identifier"></a><span data-ttu-id="de182-197">Определение идентификатора клиента</span><span class="sxs-lookup"><span data-stu-id="de182-197">Determining your Tenant Identifier</span></span>
<span data-ttu-id="de182-198">Hello идентификатор клиента для клиента hello Azure AD можно получить, выполнив `Get-AzureAccount` в Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de182-198">You can find hello tenant identifier for hello Azure AD tenant by running `Get-AzureAccount` in Azure PowerShell.</span></span>

## <a name="response-body-for-activedirectoryoauth-authentication"></a><span data-ttu-id="de182-199">Текст ответа при проверке подлинности ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="de182-199">Response Body for ActiveDirectoryOAuth Authentication</span></span>
<span data-ttu-id="de182-200">При отправке запроса с данными проверки подлинности, hello ответ содержит следующие элементы, связанные с проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="de182-200">When a request is sent with authentication info, hello response contains hello following authentication-related elements.</span></span>

| <span data-ttu-id="de182-201">Элемент</span><span class="sxs-lookup"><span data-stu-id="de182-201">Element</span></span> | <span data-ttu-id="de182-202">Описание</span><span class="sxs-lookup"><span data-stu-id="de182-202">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="de182-203">*authentication (родительский элемент)*</span><span class="sxs-lookup"><span data-stu-id="de182-203">*authentication (parent element)*</span></span> |<span data-ttu-id="de182-204">Объект проверки подлинности для использования проверки подлинности ActiveDirectoryOAuth.</span><span class="sxs-lookup"><span data-stu-id="de182-204">Authentication object for using ActiveDirectoryOAuth authentication.</span></span> |
| <span data-ttu-id="de182-205">*type*</span><span class="sxs-lookup"><span data-stu-id="de182-205">*type*</span></span> |<span data-ttu-id="de182-206">Тип проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="de182-206">Type of authentication.</span></span> <span data-ttu-id="de182-207">Для проверки подлинности activedirectoryoauth используется значение hello — `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="de182-207">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |
| <span data-ttu-id="de182-208">*tenant*</span><span class="sxs-lookup"><span data-stu-id="de182-208">*tenant*</span></span> |<span data-ttu-id="de182-209">Здравствуйте, идентификатор клиента для клиента hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de182-209">hello tenant identifier for hello Azure AD tenant.</span></span> |
| <span data-ttu-id="de182-210">*audience*</span><span class="sxs-lookup"><span data-stu-id="de182-210">*audience*</span></span> |<span data-ttu-id="de182-211">Этот параметр задается toohttps://management.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="de182-211">This is set toohttps://management.core.windows.net/.</span></span> |
| <span data-ttu-id="de182-212">*clientId*</span><span class="sxs-lookup"><span data-stu-id="de182-212">*clientId*</span></span> |<span data-ttu-id="de182-213">Здравствуйте, идентификатор клиента приложения hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="de182-213">hello client identifier for hello Azure AD application.</span></span> |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a><span data-ttu-id="de182-214">Пример запроса REST для аутентификации ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="de182-214">Sample REST Request for ActiveDirectoryOAuth Authentication</span></span>
```
PUT https://management.azure.com/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobcollections/southeastasiajc/jobs/httpjob?api-version=2016-01-01 HTTP/1.1
User-Agent: Fiddler
Host: management.azure.com
Authorization: Bearer sometoken
Content-Length: 757
Content-Type: application/json; charset=utf-8

{
  "properties": {
    "startTime": "2015-05-14T14:10:00Z",
    "action": {
      "request": {
        "uri": "https://mywebserviceendpoint.com",
        "method": "GET",
        "headers": {
          "x-ms-version": "2013-03-01"
        },
        "authentication": {
          "tenant":"microsoft.onmicrosoft.com",
          "audience":"https://management.core.windows.net/",
          "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
          "secret": "G6u071r8Gjw4V4KSibnb+VK4+tX399hkHaj7LOyHuj5=",
          "type":"ActiveDirectoryOAuth"
        }
      },
      "type": "http"
    },
    "recurrence": {
      "frequency": "minute",
      "endTime": "2016-04-10T08:00:00Z",
      "interval": 1
    },
    "state": "enabled",
  }
}
```

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a><span data-ttu-id="de182-215">Пример ответа REST для аутентификации ActiveDirectoryOAuth</span><span class="sxs-lookup"><span data-stu-id="de182-215">Sample REST Response for ActiveDirectoryOAuth Authentication</span></span>
```
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 885
Content-Type: application/json; charset=utf-8
Expires: -1
x-ms-request-id: 86d8e9fd-ac0d-4bed-9420-9baba1af3251
Server: Microsoft-IIS/8.5
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
x-ms-ratelimit-remaining-subscription-resource-requests: 599
x-ms-correlation-request-id: 5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
x-ms-routing-request-id: WESTUS:20160316T191003Z:5183bbf4-9fa1-44bb-98c6-6872e3f2e7ce
Strict-Transport-Security: max-age=31536000; includeSubDomains
Date: Wed, 16 Mar 2016 19:10:02 GMT

{  
   "id":"/subscriptions/1d908808-e491-4fe5-b97e-29886e18efd4/resourceGroups/CS-SoutheastAsia-scheduler/providers/Microsoft.Scheduler/jobCollections/southeastasiajc/jobs/httpjob",
   "type":"Microsoft.Scheduler/jobCollections/jobs",
   "name":"southeastasiajc/httpjob",
   "properties":{  
      "startTime":"2015-05-14T14:10:00Z",
      "action":{  
         "request":{  
            "uri":"https://mywebserviceendpoint.com",
            "method":"GET",
            "headers":{  
               "x-ms-version":"2013-03-01"
            },
            "authentication":{  
               "tenant":"microsoft.onmicrosoft.com",
               "audience":"https://management.core.windows.net/",
               "clientId":"dc23e764-9be6-4a33-9b9a-c46e36f0c137",
               "type":"ActiveDirectoryOAuth"
            }
         },
         "type":"http"
      },
      "recurrence":{  
         "frequency":"minute",
         "endTime":"2016-04-10T08:00:00Z",
         "interval":1
      },
      "state":"enabled",
      "status":{  
         "lastExecutionTime":"2016-03-16T19:10:00.3762123Z",
         "nextExecutionTime":"2016-03-16T19:11:00Z",
         "executionCount":5,
         "failureCount":5,
         "faultedCount":1
      }
   }
}
```

## <a name="see-also"></a><span data-ttu-id="de182-216">См. также</span><span class="sxs-lookup"><span data-stu-id="de182-216">See Also</span></span>
 [<span data-ttu-id="de182-217">Что такое планировщик?</span><span class="sxs-lookup"><span data-stu-id="de182-217">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="de182-218">Основные понятия, терминология и иерархия сущностей планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de182-218">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="de182-219">Начало работы с планировщиком в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="de182-219">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="de182-220">Планы и выставление счетов в планировщике Azure</span><span class="sxs-lookup"><span data-stu-id="de182-220">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="de182-221">Справочник по API REST планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de182-221">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="de182-222">Справочник по командлетам PowerShell планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de182-222">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="de182-223">Высокая доступность и надежность планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de182-223">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="de182-224">Ограничения, значения по умолчанию и коды ошибок планировщика Azure</span><span class="sxs-lookup"><span data-stu-id="de182-224">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

