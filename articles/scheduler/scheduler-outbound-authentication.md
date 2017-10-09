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
# <a name="scheduler-outbound-authentication"></a>Исходящая проверка подлинности планировщика
Задания планировщика могут потребовать toocall out tooservices, который требует проверки подлинности. В этом случае вызванная служба способна определить, если задание планировщика hello доступ к ее ресурсам. В число таких служб входят другие службы Azure, Salesforce.com, Facebook и защищенные пользовательские веб-сайты.

## <a name="adding-and-removing-authentication"></a>Добавление и удаление проверки подлинности
Добавление проверки подлинности tooa планировщик заданий выполняется просто — добавьте дочерний элемент JSON `authentication` toohello `request` элемент при создании или обновлении задания. Секретные данные передаются toohello служба планировщика в запросе PUT, POST или PATCH — как часть hello `authentication` объекта — никогда не возвращаются в ответах. В ответах секретная информация имеет toonull или может иметь открытый маркер, который представляет сущность hello с проверкой подлинности.

tooremove проверки подлинности, PUT или PATCH задания hello явным образом, параметр hello `authentication` объекта toonull. Никакие свойства проверки подлинности в ответе показаны не будут.

В настоящее время типы hello поддерживается только проверка подлинности: hello `ClientCertificate` модели (для использования сертификатов клиентов hello SSL/TLS), hello `Basic` модели (для обычной проверки подлинности) и hello `ActiveDirectoryOAuth` модели (для Active Directory OAuth Проверка подлинности.)

## <a name="request-body-for-clientcertificate-authentication"></a>Текст запроса для проверки подлинности ClientCertificate
При добавлении проверки подлинности с использованием hello `ClientCertificate` модель, указать следующие дополнительные элементы в тексте запроса hello hello.  

| Элемент | Описание |
|:--- |:--- |
| *authentication (родительский элемент)* |Объект проверки подлинности для использования клиентского SSL-сертификата. |
| *type* |Обязательный элемент. Тип проверки подлинности. Для SSL-сертификатов клиента, hello значение должно быть `ClientCertificate`. |
| *pfx* |Обязательный элемент. Содержимое base64-кодированном hello PFX-файла. |
| *password* |Обязательный элемент. Пароль tooaccess hello PFX-файла. |

## <a name="response-body-for-clientcertificate-authentication"></a>Текст ответа при проверке подлинности ClientCertificate
При отправке запроса с данными проверки подлинности, hello ответ содержит следующие элементы, связанные с проверки подлинности hello.

| Элемент | Описание |
|:--- |:--- |
| *authentication (родительский элемент)* |Объект проверки подлинности для использования клиентского SSL-сертификата. |
| *type* |Тип проверки подлинности. Для SSL-сертификатов клиента, значение hello — `ClientCertificate`. |
| *certificateThumbprint* |отпечаток сертификата hello Hello. |
| *certificateSubjectName* |Hello различающееся имя субъекта сертификата hello. |
| *certificateExpiration* |Hello срок сертификата hello. |

## <a name="sample-rest-request-for-clientcertificate-authentication"></a>Пример запроса REST для аутентификации ClientCertificate
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

## <a name="sample-rest-response-for-clientcertificate-authentication"></a>Пример ответа REST для аутентификации ClientCertificate
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

## <a name="request-body-for-basic-authentication"></a>Текст запроса для обычной проверки подлинности
При добавлении проверки подлинности с использованием hello `Basic` модель, указать следующие дополнительные элементы в тексте запроса hello hello.

| Элемент | Описание |
|:--- |:--- |
| *authentication (родительский элемент)* |Объект проверки подлинности для использования обычной проверки подлинности. |
| *type* |обязательный параметр. Тип проверки подлинности. Для обычной проверки подлинности должно быть значение hello `Basic`. |
| *username* |Обязательный элемент. Tooauthenticate имя пользователя. |
| *password* |Обязательный элемент. Tooauthenticate пароль. |

## <a name="response-body-for-basic-authentication"></a>Текст ответа при обычной проверке подлинности
При отправке запроса с данными проверки подлинности, hello ответ содержит следующие элементы, связанные с проверки подлинности hello.

| Элемент | Описание |
|:--- |:--- |
| *authentication (родительский элемент)* |Объект проверки подлинности для использования обычной проверки подлинности. |
| *type* |Тип проверки подлинности. Для обычной проверки подлинности значение hello — `Basic`. |
| *username* |Hello проверку подлинности имени пользователя. |

## <a name="sample-rest-request-for-basic-authentication"></a>Пример запроса REST для обычной проверки подлинности
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

## <a name="sample-rest-response-for-basic-authentication"></a>Пример ответа REST для обычной проверки подлинности
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

## <a name="request-body-for-activedirectoryoauth-authentication"></a>Текст запроса для проверки подлинности ActiveDirectoryOAuth
При добавлении проверки подлинности с использованием hello `ActiveDirectoryOAuth` модель, указать следующие дополнительные элементы в тексте запроса hello hello.

| Элемент | Описание |
|:--- |:--- |
| *authentication (родительский элемент)* |Объект проверки подлинности для использования проверки подлинности ActiveDirectoryOAuth. |
| *type* |обязательный параметр. Тип проверки подлинности. Для проверки подлинности ActiveDirectoryOAuth hello значение должно быть `ActiveDirectoryOAuth`. |
| *tenant* |Обязательный элемент. Здравствуйте, идентификатор клиента для клиента hello Azure AD. |
| *audience* |Обязательный элемент. Этот параметр задается toohttps://management.core.windows.net/. |
| *clientId* |Обязательный элемент. Укажите идентификатор клиента hello для hello приложения Azure AD. |
| *secret* |Обязательный элемент. Секрет клиента hello, который запрашивает токен hello. |

### <a name="determining-your-tenant-identifier"></a>Определение идентификатора клиента
Hello идентификатор клиента для клиента hello Azure AD можно получить, выполнив `Get-AzureAccount` в Azure PowerShell.

## <a name="response-body-for-activedirectoryoauth-authentication"></a>Текст ответа при проверке подлинности ActiveDirectoryOAuth
При отправке запроса с данными проверки подлинности, hello ответ содержит следующие элементы, связанные с проверки подлинности hello.

| Элемент | Описание |
|:--- |:--- |
| *authentication (родительский элемент)* |Объект проверки подлинности для использования проверки подлинности ActiveDirectoryOAuth. |
| *type* |Тип проверки подлинности. Для проверки подлинности activedirectoryoauth используется значение hello — `ActiveDirectoryOAuth`. |
| *tenant* |Здравствуйте, идентификатор клиента для клиента hello Azure AD. |
| *audience* |Этот параметр задается toohttps://management.core.windows.net/. |
| *clientId* |Здравствуйте, идентификатор клиента приложения hello Azure AD. |

## <a name="sample-rest-request-for-activedirectoryoauth-authentication"></a>Пример запроса REST для аутентификации ActiveDirectoryOAuth
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

## <a name="sample-rest-response-for-activedirectoryoauth-authentication"></a>Пример ответа REST для аутентификации ActiveDirectoryOAuth
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

## <a name="see-also"></a>См. также
 [Что такое планировщик?](scheduler-intro.md)

 [Основные понятия, терминология и иерархия сущностей планировщика Azure](scheduler-concepts-terms.md)

 [Начало работы с планировщиком в hello портал Azure](scheduler-get-started-portal.md)

 [Планы и выставление счетов в планировщике Azure](scheduler-plans-billing.md)

 [Справочник по API REST планировщика Azure](https://msdn.microsoft.com/library/mt629143)

 [Справочник по командлетам PowerShell планировщика Azure](scheduler-powershell-reference.md)

 [Высокая доступность и надежность планировщика Azure](scheduler-high-availability-reliability.md)

 [Ограничения, значения по умолчанию и коды ошибок планировщика Azure](scheduler-limits-defaults-errors.md)

