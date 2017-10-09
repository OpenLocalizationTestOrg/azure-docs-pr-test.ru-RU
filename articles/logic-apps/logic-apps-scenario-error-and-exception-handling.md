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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="12f6c-103">Сценарий обработки исключений и ведения журнала ошибок для приложений логики</span><span class="sxs-lookup"><span data-stu-id="12f6c-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="12f6c-104">В этом сценарии описывается, как можно расширить обработку логики приложения toobetter поддержки исключений.</span><span class="sxs-lookup"><span data-stu-id="12f6c-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="12f6c-105">Мы используем практическом использовании вариантов tooanswer hello вопрос: «Приложения логики Azure поддерживает обработка ошибок и исключений?»</span><span class="sxs-lookup"><span data-stu-id="12f6c-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="12f6c-106">Hello текущая схема приложения логики Azure предоставляет стандартный шаблон для ответов действия.</span><span class="sxs-lookup"><span data-stu-id="12f6c-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="12f6c-107">В этот шаблон входят внутренние проверки и обработка сообщений об ошибках, возвращаемых из приложения API.</span><span class="sxs-lookup"><span data-stu-id="12f6c-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="12f6c-108">Обзор сценария и варианта использование</span><span class="sxs-lookup"><span data-stu-id="12f6c-108">Scenario and use case overview</span></span>

<span data-ttu-id="12f6c-109">Здесь-истории hello hello вариант использования для этого сценария:</span><span class="sxs-lookup"><span data-stu-id="12f6c-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="12f6c-110">Хорошо известных здравоохранения организации, которая участвует нам toodevelop решения Azure, которые создают пациента портала с помощью Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="12f6c-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="12f6c-111">Они нужны toosend встречи записи Dynamics CRM Online пациента портала hello и Salesforce.</span><span class="sxs-lookup"><span data-stu-id="12f6c-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="12f6c-112">Спросили toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) стандарт для всех пациентов.</span><span class="sxs-lookup"><span data-stu-id="12f6c-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="12f6c-113">Hello проекте имеется два основных требования:</span><span class="sxs-lookup"><span data-stu-id="12f6c-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="12f6c-114">Метод toolog записей отправленных hello Dynamics CRM Online портала</span><span class="sxs-lookup"><span data-stu-id="12f6c-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="12f6c-115">Tooview способом любые ошибки, возникшие в рамках рабочего процесса hello</span><span class="sxs-lookup"><span data-stu-id="12f6c-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="12f6c-116">Видео высокого уровня о данном проекте см. в разделе [группы пользователей интеграции](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "группы пользователей интеграции").</span><span class="sxs-lookup"><span data-stu-id="12f6c-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="12f6c-117">Как мы решена проблема hello</span><span class="sxs-lookup"><span data-stu-id="12f6c-117">How we solved hello problem</span></span>

<span data-ttu-id="12f6c-118">Мы выбрали [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") как хранилище hello журнала ошибок записи и (Cosmos DB ссылается toorecords как документы).</span><span class="sxs-lookup"><span data-stu-id="12f6c-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="12f6c-119">Поскольку приложения логики Azure имеет стандартный шаблон для всех ответов, мы не toocreate пользовательской схемы.</span><span class="sxs-lookup"><span data-stu-id="12f6c-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="12f6c-120">Можно было бы создать приложения API слишком**вставить** и **запроса** для записи ошибок и журнала.</span><span class="sxs-lookup"><span data-stu-id="12f6c-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="12f6c-121">Также мы можем определить схему для каждого приложения hello API.</span><span class="sxs-lookup"><span data-stu-id="12f6c-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="12f6c-122">Другим требованием был toopurge записей после определенной даты.</span><span class="sxs-lookup"><span data-stu-id="12f6c-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="12f6c-123">Cosmos DB имеет свойство с именем [время tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "время tooLive") (TTL), который позволил нам tooset **tooLive время** значение для каждой записи или коллекции.</span><span class="sxs-lookup"><span data-stu-id="12f6c-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="12f6c-124">Эта возможность устраняется hello необходимость toomanually удаления записей в базу данных, Cosmos.</span><span class="sxs-lookup"><span data-stu-id="12f6c-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12f6c-125">toocomplete этого учебника требуется toocreate Cosmos DB базы данных и две коллекции (Ведение журнала и ошибки).</span><span class="sxs-lookup"><span data-stu-id="12f6c-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="12f6c-126">Создание приложения hello логики</span><span class="sxs-lookup"><span data-stu-id="12f6c-126">Create hello logic app</span></span>

<span data-ttu-id="12f6c-127">Hello первым шагом является toocreate hello логику приложения и приложение hello открыть в конструкторе логики приложения.</span><span class="sxs-lookup"><span data-stu-id="12f6c-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="12f6c-128">В этом примере мы используем родительское и дочерние приложения логики.</span><span class="sxs-lookup"><span data-stu-id="12f6c-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="12f6c-129">Предположим, что мы уже создали родительского hello и будет toocreate один дочерний логику приложения.</span><span class="sxs-lookup"><span data-stu-id="12f6c-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="12f6c-130">Так как мы будем toolog записи hello, поступающих из Dynamics CRM Online, давайте начнем вверху hello.</span><span class="sxs-lookup"><span data-stu-id="12f6c-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="12f6c-131">Мы воспользуемся **запроса** триггер, так как логика приложения hello родительского триггеры этого дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="12f6c-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="12f6c-132">Триггер приложения логики</span><span class="sxs-lookup"><span data-stu-id="12f6c-132">Logic app trigger</span></span>

<span data-ttu-id="12f6c-133">Мы используем **запроса** триггера, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="12f6c-133">We are using a **Request** trigger as shown in hello following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="12f6c-134">Действия</span><span class="sxs-lookup"><span data-stu-id="12f6c-134">Steps</span></span>

<span data-ttu-id="12f6c-135">Мы необходимо войти в источник hello (запрос) пациентов hello из портала Dynamics CRM Online hello.</span><span class="sxs-lookup"><span data-stu-id="12f6c-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="12f6c-136">Необходимо получить новую запись о приеме с портала Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="12f6c-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="12f6c-137">триггер Hello, поступающих от CRM предоставляет hello **CRM PatentId**, **тип записи**, **создать или обновить запись** (новой или обновление логическое значение), и  **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="12f6c-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="12f6c-138">Hello **SalesforceId** может иметь значение null, так как оно используется только для обновления.</span><span class="sxs-lookup"><span data-stu-id="12f6c-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="12f6c-139">Мы получаем hello CRM записи с помощью hello CRM **PatientID** и hello **тип записи**.</span><span class="sxs-lookup"><span data-stu-id="12f6c-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="12f6c-140">Теперь нам нужны tooadd нашего приложения DocumentDB API **InsertLogEntry** операции, как показано здесь в конструктор логику приложения.</span><span class="sxs-lookup"><span data-stu-id="12f6c-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="12f6c-141">**Добавление записи журнала**</span><span class="sxs-lookup"><span data-stu-id="12f6c-141">**Insert log entry**</span></span>

   ![Добавление записи журнала](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="12f6c-143">**Добавление записи об ошибке**</span><span class="sxs-lookup"><span data-stu-id="12f6c-143">**Insert error entry**</span></span>

   ![Добавление записи журнала](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="12f6c-145">**Проверка на наличие ошибки создания записи**</span><span class="sxs-lookup"><span data-stu-id="12f6c-145">**Check for create record failure**</span></span>

   ![Условие](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="12f6c-147">Исходный код приложения логики</span><span class="sxs-lookup"><span data-stu-id="12f6c-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="12f6c-148">Следующие примеры Hello — это только примеры.</span><span class="sxs-lookup"><span data-stu-id="12f6c-148">hello following examples are samples only.</span></span> <span data-ttu-id="12f6c-149">Так как этот учебник основывается на реализацию теперь в рабочей среде, hello значение **исходный узел** могут отображаться свойства, связанные tooscheduling встречи. ></span><span class="sxs-lookup"><span data-stu-id="12f6c-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="12f6c-150">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="12f6c-150">Logging</span></span>

<span data-ttu-id="12f6c-151">Следующий код логики приложения Hello образце показано, как toohandle ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="12f6c-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="12f6c-152">Запись в журнале</span><span class="sxs-lookup"><span data-stu-id="12f6c-152">Log entry</span></span>

<span data-ttu-id="12f6c-153">Ниже приведен исходный код приложения hello логику для вставки записи журнала.</span><span class="sxs-lookup"><span data-stu-id="12f6c-153">Here is hello logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="12f6c-154">Запрос к журналу</span><span class="sxs-lookup"><span data-stu-id="12f6c-154">Log request</span></span>

<span data-ttu-id="12f6c-155">Вот hello журнала запрос сообщения toohello приложения API.</span><span class="sxs-lookup"><span data-stu-id="12f6c-155">Here is hello log request message posted toohello API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="12f6c-156">Ответ журнала</span><span class="sxs-lookup"><span data-stu-id="12f6c-156">Log response</span></span>

<span data-ttu-id="12f6c-157">Вот hello журнала ответное сообщение от приложения hello API.</span><span class="sxs-lookup"><span data-stu-id="12f6c-157">Here is hello log response message from hello API app.</span></span>

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

<span data-ttu-id="12f6c-158">Теперь рассмотрим шаги обработки ошибок, hello.</span><span class="sxs-lookup"><span data-stu-id="12f6c-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="12f6c-159">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="12f6c-159">Error handling</span></span>

<span data-ttu-id="12f6c-160">Hello следующий образец кода логики приложения показано, как можно реализовать обработку ошибок.</span><span class="sxs-lookup"><span data-stu-id="12f6c-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="12f6c-161">Создание записи об ошибке</span><span class="sxs-lookup"><span data-stu-id="12f6c-161">Create error record</span></span>

<span data-ttu-id="12f6c-162">Ниже приведен исходный код приложения hello логику для создания записи об ошибке.</span><span class="sxs-lookup"><span data-stu-id="12f6c-162">Here is hello logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="12f6c-163">Добавление записи об ошибке в Cosmos DB — запрос</span><span class="sxs-lookup"><span data-stu-id="12f6c-163">Insert error into Cosmos DB--request</span></span>

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

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="12f6c-164">Добавление записи об ошибке в Cosmos DB — ответ</span><span class="sxs-lookup"><span data-stu-id="12f6c-164">Insert error into Cosmos DB--response</span></span>

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

#### <a name="salesforce-error-response"></a><span data-ttu-id="12f6c-165">Ответ на ошибку Salesforce</span><span class="sxs-lookup"><span data-stu-id="12f6c-165">Salesforce error response</span></span>

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

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="12f6c-166">Возвращаемый ответ назад tooparent логику приложение hello</span><span class="sxs-lookup"><span data-stu-id="12f6c-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="12f6c-167">После получения ответа hello можно передать hello ответ назад toohello родительского логику приложения.</span><span class="sxs-lookup"><span data-stu-id="12f6c-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="12f6c-168">Возвращает успех ответа tooparent логику приложения</span><span class="sxs-lookup"><span data-stu-id="12f6c-168">Return success response tooparent logic app</span></span>

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

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="12f6c-169">Ошибка возврата ответа tooparent логику приложения</span><span class="sxs-lookup"><span data-stu-id="12f6c-169">Return error response tooparent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="12f6c-170">Репозиторий и портал Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="12f6c-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="12f6c-171">Благодаря использованию [Cosmos DB](https://azure.microsoft.com/services/documentdb) наше решение предоставляет больше возможностей.</span><span class="sxs-lookup"><span data-stu-id="12f6c-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="12f6c-172">Портал управления ошибками</span><span class="sxs-lookup"><span data-stu-id="12f6c-172">Error management portal</span></span>

<span data-ttu-id="12f6c-173">tooview hello ошибки, можно создать MVC web app toodisplay hello записи об ошибках из Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="12f6c-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="12f6c-174">Hello **списка**, **сведения**, **изменить**, и **удалить** операций, включенных в текущей версии hello.</span><span class="sxs-lookup"><span data-stu-id="12f6c-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="12f6c-175">Изменить операцию: Cosmos DB заменяет hello весь документ.</span><span class="sxs-lookup"><span data-stu-id="12f6c-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="12f6c-176">Здравствуйте, записи на hello **списка** и **сведений** представления — это только примеры.</span><span class="sxs-lookup"><span data-stu-id="12f6c-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="12f6c-177">Это не фактические записи о приемах пациентов.</span><span class="sxs-lookup"><span data-stu-id="12f6c-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="12f6c-178">Ниже приведены примеры из нашего приложения MVC сведения, ранее созданными hello описанный подход.</span><span class="sxs-lookup"><span data-stu-id="12f6c-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="12f6c-179">Список для управления ошибками</span><span class="sxs-lookup"><span data-stu-id="12f6c-179">Error management list</span></span>
![Список ошибок](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="12f6c-181">Просмотр подробных сведений об ошибке</span><span class="sxs-lookup"><span data-stu-id="12f6c-181">Error management detail view</span></span>
![Сведения об ошибке](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="12f6c-183">Портал управления журналами</span><span class="sxs-lookup"><span data-stu-id="12f6c-183">Log management portal</span></span>

<span data-ttu-id="12f6c-184">журналы tooview hello, также был создан веб-приложение MVC.</span><span class="sxs-lookup"><span data-stu-id="12f6c-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="12f6c-185">Ниже приведены примеры из нашего приложения MVC сведения, ранее созданными hello описанный подход.</span><span class="sxs-lookup"><span data-stu-id="12f6c-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="12f6c-186">Просмотр подробных сведений об ошибке из журнала</span><span class="sxs-lookup"><span data-stu-id="12f6c-186">Sample log detail view</span></span>
![Просмотр сведений о записи журнала](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="12f6c-188">Сведения о приложении API</span><span class="sxs-lookup"><span data-stu-id="12f6c-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="12f6c-189">API управления исключениями приложений логики</span><span class="sxs-lookup"><span data-stu-id="12f6c-189">Logic Apps exception management API</span></span>

<span data-ttu-id="12f6c-190">Приложение API на основе Azure Logic Apps с открытым исходным кодом, которое мы создали для управления исключениями, поддерживает следующие возможности, включая два контроллера:</span><span class="sxs-lookup"><span data-stu-id="12f6c-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="12f6c-191">**ErrorController** добавляет запись об ошибке (документ) в коллекцию DocumentDB;</span><span class="sxs-lookup"><span data-stu-id="12f6c-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="12f6c-192">**LogController** добавляет запись журнала (документ) в коллекцию DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="12f6c-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="12f6c-193">Использовать оба контроллера `async Task<dynamic>` операции, tooresolve операции во время выполнения, чтобы мы могли создавать hello схемы DocumentDB в тексте hello hello операции.</span><span class="sxs-lookup"><span data-stu-id="12f6c-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="12f6c-194">Каждому документу в DocumentDB необходимо присвоить уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="12f6c-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="12f6c-195">Мы используем `PatientId` и добавление отметка времени, преобразуется в значение отметки времени Unix tooa (double).</span><span class="sxs-lookup"><span data-stu-id="12f6c-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="12f6c-196">Мы усечь дробное значение tooremove значение hello hello.</span><span class="sxs-lookup"><span data-stu-id="12f6c-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="12f6c-197">Можно просмотреть исходный код hello нашей ошибка контроллера API [из GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="12f6c-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="12f6c-198">Мы называем hello API из логики приложения с помощью hello, используя синтаксис:</span><span class="sxs-lookup"><span data-stu-id="12f6c-198">We call hello API from a logic app by using hello following syntax:</span></span>

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

<span data-ttu-id="12f6c-199">Здравствуйте, выражение в hello предшествующий код примера проверяет наличие hello *Create_NewPatientRecord* состояние **сбой**.</span><span class="sxs-lookup"><span data-stu-id="12f6c-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="12f6c-200">Сводка</span><span class="sxs-lookup"><span data-stu-id="12f6c-200">Summary</span></span>

* <span data-ttu-id="12f6c-201">В приложении логики можно легко реализовать ведение журнала и обработку ошибок.</span><span class="sxs-lookup"><span data-stu-id="12f6c-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="12f6c-202">DocumentDB можно использовать как хранилище hello записей журнала и ошибки (документов).</span><span class="sxs-lookup"><span data-stu-id="12f6c-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="12f6c-203">Можно использовать toocreate MVC журнала портала toodisplay и ошибочные записи.</span><span class="sxs-lookup"><span data-stu-id="12f6c-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="12f6c-204">Исходный код</span><span class="sxs-lookup"><span data-stu-id="12f6c-204">Source code</span></span>

<span data-ttu-id="12f6c-205">Hello исходный код для управления исключениями Logic Apps API приложения hello доступен в этом [репозитории GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API управления исключение логику приложения").</span><span class="sxs-lookup"><span data-stu-id="12f6c-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="12f6c-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12f6c-206">Next steps</span></span>

* [<span data-ttu-id="12f6c-207">Примеры приложений логики и распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="12f6c-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="12f6c-208">Мониторинг приложений логики</span><span class="sxs-lookup"><span data-stu-id="12f6c-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="12f6c-209">Создание шаблона развертывания приложения логики</span><span class="sxs-lookup"><span data-stu-id="12f6c-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
