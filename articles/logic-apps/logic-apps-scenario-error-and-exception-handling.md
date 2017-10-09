---
title: "aaaException обработка & сценарий ведения журнала ошибок - приложения логики Azure | Документы Microsoft"
description: "В этой статье описывается реальный вариант использования расширенной обработки исключений и ведения журнала ошибок для Azure Logic Apps."
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>Сценарий обработки исключений и ведения журнала ошибок для приложений логики

В этом сценарии описывается, как можно расширить обработку логики приложения toobetter поддержки исключений. Мы используем практическом использовании вариантов tooanswer hello вопрос: «Приложения логики Azure поддерживает обработка ошибок и исключений?»

> [!NOTE]
> Hello текущая схема приложения логики Azure предоставляет стандартный шаблон для ответов действия. В этот шаблон входят внутренние проверки и обработка сообщений об ошибках, возвращаемых из приложения API.

## <a name="scenario-and-use-case-overview"></a>Обзор сценария и варианта использование

Здесь-истории hello hello вариант использования для этого сценария: 

Хорошо известных здравоохранения организации, которая участвует нам toodevelop решения Azure, которые создают пациента портала с помощью Microsoft Dynamics CRM Online. Они нужны toosend встречи записи Dynamics CRM Online пациента портала hello и Salesforce. Спросили toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) стандарт для всех пациентов.

Hello проекте имеется два основных требования:  

* Метод toolog записей отправленных hello Dynamics CRM Online портала
* Tooview способом любые ошибки, возникшие в рамках рабочего процесса hello

> [!TIP]
> Видео высокого уровня о данном проекте см. в разделе [группы пользователей интеграции](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "группы пользователей интеграции").

## <a name="how-we-solved-hello-problem"></a>Как мы решена проблема hello

Мы выбрали [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") как хранилище hello журнала ошибок записи и (Cosmos DB ссылается toorecords как документы). Поскольку приложения логики Azure имеет стандартный шаблон для всех ответов, мы не toocreate пользовательской схемы. Можно было бы создать приложения API слишком**вставить** и **запроса** для записи ошибок и журнала. Также мы можем определить схему для каждого приложения hello API.  

Другим требованием был toopurge записей после определенной даты. Cosmos DB имеет свойство с именем [время tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "время tooLive") (TTL), который позволил нам tooset **tooLive время** значение для каждой записи или коллекции. Эта возможность устраняется hello необходимость toomanually удаления записей в базу данных, Cosmos.

> [!IMPORTANT]
> toocomplete этого учебника требуется toocreate Cosmos DB базы данных и две коллекции (Ведение журнала и ошибки).

## <a name="create-hello-logic-app"></a>Создание приложения hello логики

Hello первым шагом является toocreate hello логику приложения и приложение hello открыть в конструкторе логики приложения. В этом примере мы используем родительское и дочерние приложения логики. Предположим, что мы уже создали родительского hello и будет toocreate один дочерний логику приложения.

Так как мы будем toolog записи hello, поступающих из Dynamics CRM Online, давайте начнем вверху hello. Мы воспользуемся **запроса** триггер, так как логика приложения hello родительского триггеры этого дочернего элемента.

### <a name="logic-app-trigger"></a>Триггер приложения логики

Мы используем **запроса** триггера, как показано в следующий пример hello:

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a>Действия

Мы необходимо войти в источник hello (запрос) пациентов hello из портала Dynamics CRM Online hello.

1. Необходимо получить новую запись о приеме с портала Dynamics CRM Online.

   триггер Hello, поступающих от CRM предоставляет hello **CRM PatentId**, **тип записи**, **создать или обновить запись** (новой или обновление логическое значение), и  **SalesforceId**. Hello **SalesforceId** может иметь значение null, так как оно используется только для обновления.
   Мы получаем hello CRM записи с помощью hello CRM **PatientID** и hello **тип записи**.

2. Теперь нам нужны tooadd нашего приложения DocumentDB API **InsertLogEntry** операции, как показано здесь в конструктор логику приложения.

   **Добавление записи журнала**

   ![Добавление записи журнала](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **Добавление записи об ошибке**

   ![Добавление записи журнала](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **Проверка на наличие ошибки создания записи**

   ![Условие](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>Исходный код приложения логики

> [!NOTE]
> Следующие примеры Hello — это только примеры. Так как этот учебник основывается на реализацию теперь в рабочей среде, hello значение **исходный узел** могут отображаться свойства, связанные tooscheduling встречи. > 

### <a name="logging"></a>Ведение журналов

Следующий код логики приложения Hello образце показано, как toohandle ведения журнала.

#### <a name="log-entry"></a>Запись в журнале

Ниже приведен исходный код приложения hello логику для вставки записи журнала.

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a>Запрос к журналу

Вот hello журнала запрос сообщения toohello приложения API.

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a>Ответ журнала

Вот hello журнала ответное сообщение от приложения hello API.

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

Теперь рассмотрим шаги обработки ошибок, hello.

### <a name="error-handling"></a>Обработка ошибок

Hello следующий образец кода логики приложения показано, как можно реализовать обработку ошибок.

#### <a name="create-error-record"></a>Создание записи об ошибке

Ниже приведен исходный код приложения hello логику для создания записи об ошибке.

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a>Добавление записи об ошибке в Cosmos DB — запрос

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a>Добавление записи об ошибке в Cosmos DB — ответ

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a>Ответ на ошибку Salesforce

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a>Возвращаемый ответ назад tooparent логику приложение hello

После получения ответа hello можно передать hello ответ назад toohello родительского логику приложения.

#### <a name="return-success-response-tooparent-logic-app"></a>Возвращает успех ответа tooparent логику приложения

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-tooparent-logic-app"></a>Ошибка возврата ответа tooparent логику приложения

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a>Репозиторий и портал Cosmos DB

Благодаря использованию [Cosmos DB](https://azure.microsoft.com/services/documentdb) наше решение предоставляет больше возможностей.

### <a name="error-management-portal"></a>Портал управления ошибками

tooview hello ошибки, можно создать MVC web app toodisplay hello записи об ошибках из Cosmos DB. Hello **списка**, **сведения**, **изменить**, и **удалить** операций, включенных в текущей версии hello.

> [!NOTE]
> Изменить операцию: Cosmos DB заменяет hello весь документ. Здравствуйте, записи на hello **списка** и **сведений** представления — это только примеры. Это не фактические записи о приемах пациентов.

Ниже приведены примеры из нашего приложения MVC сведения, ранее созданными hello описанный подход.

#### <a name="error-management-list"></a>Список для управления ошибками
![Список ошибок](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>Просмотр подробных сведений об ошибке
![Сведения об ошибке](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>Портал управления журналами

журналы tooview hello, также был создан веб-приложение MVC. Ниже приведены примеры из нашего приложения MVC сведения, ранее созданными hello описанный подход.

#### <a name="sample-log-detail-view"></a>Просмотр подробных сведений об ошибке из журнала
![Просмотр сведений о записи журнала](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>Сведения о приложении API

#### <a name="logic-apps-exception-management-api"></a>API управления исключениями приложений логики

Приложение API на основе Azure Logic Apps с открытым исходным кодом, которое мы создали для управления исключениями, поддерживает следующие возможности, включая два контроллера:

* **ErrorController** добавляет запись об ошибке (документ) в коллекцию DocumentDB;
* **LogController** добавляет запись журнала (документ) в коллекцию DocumentDB.

> [!TIP]
> Использовать оба контроллера `async Task<dynamic>` операции, tooresolve операции во время выполнения, чтобы мы могли создавать hello схемы DocumentDB в тексте hello hello операции. 
> 

Каждому документу в DocumentDB необходимо присвоить уникальный идентификатор. Мы используем `PatientId` и добавление отметка времени, преобразуется в значение отметки времени Unix tooa (double). Мы усечь дробное значение tooremove значение hello hello.

Можно просмотреть исходный код hello нашей ошибка контроллера API [из GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).

Мы называем hello API из логики приложения с помощью hello, используя синтаксис:

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

Здравствуйте, выражение в hello предшествующий код примера проверяет наличие hello *Create_NewPatientRecord* состояние **сбой**.

## <a name="summary"></a>Сводка

* В приложении логики можно легко реализовать ведение журнала и обработку ошибок.
* DocumentDB можно использовать как хранилище hello записей журнала и ошибки (документов).
* Можно использовать toocreate MVC журнала портала toodisplay и ошибочные записи.

### <a name="source-code"></a>Исходный код

Hello исходный код для управления исключениями Logic Apps API приложения hello доступен в этом [репозитории GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API управления исключение логику приложения").

## <a name="next-steps"></a>Дальнейшие действия

* [Примеры приложений логики и распространенные сценарии](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Мониторинг приложений логики](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Создание шаблона развертывания приложения логики](../logic-apps/logic-apps-create-deploy-template.md)
