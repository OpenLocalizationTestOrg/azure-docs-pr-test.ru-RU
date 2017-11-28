---
title: "Сценарий обработки исключений и ведения журнала ошибок с помощью Azure Logic Apps | Документация Майкрософт"
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
ms.openlocfilehash: 044de27c75da93c95609110d2b73336c42f746fe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="b684d-103">Сценарий обработки исключений и ведения журнала ошибок для приложений логики</span><span class="sxs-lookup"><span data-stu-id="b684d-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="b684d-104">В этом сценарии описано, как улучшить поддержку для обработки исключений в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="b684d-104">This scenario describes how you can extend a logic app to better support exception handling.</span></span> <span data-ttu-id="b684d-105">Мы использовали пример из реальной жизни, который можно считать ответом на вопрос "Поддерживает ли Azure Logic Apps обработку исключений и ошибок?".</span><span class="sxs-lookup"><span data-stu-id="b684d-105">We've used a real-life use case to answer the question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="b684d-106">В текущей схеме Azure Logic Apps предоставляется стандартный шаблон для ответов на действия.</span><span class="sxs-lookup"><span data-stu-id="b684d-106">The current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="b684d-107">В этот шаблон входят внутренние проверки и обработка сообщений об ошибках, возвращаемых из приложения API.</span><span class="sxs-lookup"><span data-stu-id="b684d-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="b684d-108">Обзор сценария и варианта использование</span><span class="sxs-lookup"><span data-stu-id="b684d-108">Scenario and use case overview</span></span>

<span data-ttu-id="b684d-109">Ниже приводится история, которая лежит в основе варианта использования для данного сценария.</span><span class="sxs-lookup"><span data-stu-id="b684d-109">Here's the story as the use case for this scenario:</span></span> 

<span data-ttu-id="b684d-110">Известная медицинская организация поручила нам разработать решение на базе Azure, которое позволит создать портал для пациентов с использованием Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="b684d-110">A well-known healthcare organization engaged us to develop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="b684d-111">Также им нужно передавать информацию о приемах между порталом пациентов на базе Dynamics CRM Online и системой Salesforce.</span><span class="sxs-lookup"><span data-stu-id="b684d-111">They needed to send appointment records between the Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="b684d-112">Для передачи информации о пациентах необходимо использовать стандарт [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) .</span><span class="sxs-lookup"><span data-stu-id="b684d-112">We were asked to use the [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="b684d-113">Проект включает два основных требования:</span><span class="sxs-lookup"><span data-stu-id="b684d-113">The project had two major requirements:</span></span>  

* <span data-ttu-id="b684d-114">метод ведения журнала записей, отправленных с онлайн-портала Dynamics CRM Online;</span><span class="sxs-lookup"><span data-stu-id="b684d-114">A method to log records sent from the Dynamics CRM Online portal</span></span>
* <span data-ttu-id="b684d-115">механизм для просмотра всех ошибок, возникающих в рамках рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="b684d-115">A way to view any errors that occurred within the workflow</span></span>

> [!TIP]
> <span data-ttu-id="b684d-116">Подробное видео об этом проекте можно посмотреть на сайте [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span><span class="sxs-lookup"><span data-stu-id="b684d-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-the-problem"></a><span data-ttu-id="b684d-117">Решение проблемы</span><span class="sxs-lookup"><span data-stu-id="b684d-117">How we solved the problem</span></span>

<span data-ttu-id="b684d-118">В качестве репозитория для записей журнала и ошибок мы выбрали [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") (Cosmos DB означает, что записями этой базы данных являются документы).</span><span class="sxs-lookup"><span data-stu-id="b684d-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for the log and error records (Cosmos DB refers to records as documents).</span></span> <span data-ttu-id="b684d-119">В Azure Logic Apps используется стандартный шаблон для всех ответов, поэтому нам не пришлось создавать настраиваемую схему.</span><span class="sxs-lookup"><span data-stu-id="b684d-119">Because Azure Logic Apps has a standard template for all responses, we would not have to create a custom schema.</span></span> <span data-ttu-id="b684d-120">Чтобы **добавлять** и **запрашивать** записи журнала и записи об ошибках, можно было создать приложение API.</span><span class="sxs-lookup"><span data-stu-id="b684d-120">We could create an API app to **Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="b684d-121">В нем мы могли определить схему выполнения каждой из этих операций.</span><span class="sxs-lookup"><span data-stu-id="b684d-121">We could also define a schema for each within the API app.</span></span>  

<span data-ttu-id="b684d-122">Но существовало еще одно требование: автоматическое удаление записей через определенное время.</span><span class="sxs-lookup"><span data-stu-id="b684d-122">Another requirement was to purge records after a certain date.</span></span> <span data-ttu-id="b684d-123">Cosmos DB поддерживает свойство [Срок жизни](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Срок жизни") (TTL), которое позволяет определить значение **Срок жизни** для каждой записи или всей коллекции.</span><span class="sxs-lookup"><span data-stu-id="b684d-123">Cosmos DB has a property called [Time to Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time to Live") (TTL), which allowed us to set a **Time to Live** value for each record or collection.</span></span> <span data-ttu-id="b684d-124">Эта возможность избавляет от необходимости вручную удалять записи из Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b684d-124">This capability eliminated the need to manually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b684d-125">Для работы с этим руководством необходимо создать базу данных Cosmos DB и две коллекции ("Ведение журнала" и "Ошибки").</span><span class="sxs-lookup"><span data-stu-id="b684d-125">To complete this tutorial, you need to create a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-the-logic-app"></a><span data-ttu-id="b684d-126">Создание приложения логики</span><span class="sxs-lookup"><span data-stu-id="b684d-126">Create the logic app</span></span>

<span data-ttu-id="b684d-127">Прежде всего необходимо создать приложение логики и открыть его в конструкторе приложений логики.</span><span class="sxs-lookup"><span data-stu-id="b684d-127">The first step is to create the logic app and open the app in Logic App Designer.</span></span> <span data-ttu-id="b684d-128">В этом примере мы используем родительское и дочерние приложения логики.</span><span class="sxs-lookup"><span data-stu-id="b684d-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="b684d-129">Предположим, мы уже создали родительское приложение, а теперь создаем одно дочернее приложение логики.</span><span class="sxs-lookup"><span data-stu-id="b684d-129">Let's assume that we have already created the parent and are going to create one child logic app.</span></span>

<span data-ttu-id="b684d-130">Так как нам нужен журнал записей, отправляемых из Dynamics CRM Online, мы начнем с верхнего уровня.</span><span class="sxs-lookup"><span data-stu-id="b684d-130">Because we are going to log the record coming out of Dynamics CRM Online, let's start at the top.</span></span> <span data-ttu-id="b684d-131">Родительское приложение логики активирует дочернее, поэтому нам нужен триггер **запроса**.</span><span class="sxs-lookup"><span data-stu-id="b684d-131">We must use a **Request** trigger because the parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="b684d-132">Триггер приложения логики</span><span class="sxs-lookup"><span data-stu-id="b684d-132">Logic app trigger</span></span>

<span data-ttu-id="b684d-133">Мы используем триггер **запроса**, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="b684d-133">We are using a **Request** trigger as shown in the following example:</span></span>

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


## <a name="steps"></a><span data-ttu-id="b684d-134">Действия</span><span class="sxs-lookup"><span data-stu-id="b684d-134">Steps</span></span>

<span data-ttu-id="b684d-135">Необходимо записать в журнал источник (запрос) записи пациента, полученный с портала Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="b684d-135">We must log the source (request) of the patient record from the Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="b684d-136">Необходимо получить новую запись о приеме с портала Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="b684d-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="b684d-137">Триггер, полученный из CRM, содержит следующие сведения: **идентификатор пациента CRM**, **тип записи**, **состояние записи — новая или обновленная** (логическое значение) и **идентификатор Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="b684d-137">The trigger coming from CRM provides us with the **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="b684d-138">Параметр **SalesforceId** (идентификатор Salesforce) может иметь значение NULL, так как он используется только для обновлений.</span><span class="sxs-lookup"><span data-stu-id="b684d-138">The **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="b684d-139">Для получения записи CRM используются параметры **PatientID** (идентификатор пациента) и **Тип записи** службы CRM.</span><span class="sxs-lookup"><span data-stu-id="b684d-139">We get the CRM record by using the CRM **PatientID** and the **Record Type**.</span></span>

2. <span data-ttu-id="b684d-140">Далее необходимо добавить операцию **InsertLogEntry** для приложения API DocumentDB, как показано ниже в конструкторе приложений логики.</span><span class="sxs-lookup"><span data-stu-id="b684d-140">Next, we need to add our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="b684d-141">**Добавление записи журнала**</span><span class="sxs-lookup"><span data-stu-id="b684d-141">**Insert log entry**</span></span>

   ![Добавление записи журнала](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="b684d-143">**Добавление записи об ошибке**</span><span class="sxs-lookup"><span data-stu-id="b684d-143">**Insert error entry**</span></span>

   ![Добавление записи журнала](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="b684d-145">**Проверка на наличие ошибки создания записи**</span><span class="sxs-lookup"><span data-stu-id="b684d-145">**Check for create record failure**</span></span>

   ![Условие](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="b684d-147">Исходный код приложения логики</span><span class="sxs-lookup"><span data-stu-id="b684d-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="b684d-148">Приведенные ниже фрагменты кода используется только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b684d-148">The following examples are samples only.</span></span> <span data-ttu-id="b684d-149">Так как в этом руководстве используется пример из реальной жизни, который уже реализован в рабочей среде, значения свойств **исходного узла**, связанные с планированием приемов, могут не отображаться.</span><span class="sxs-lookup"><span data-stu-id="b684d-149">Because this tutorial is based on an implementation now in production, the value of a **Source Node** might not display properties that are related to scheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="b684d-150">Ведение журналов</span><span class="sxs-lookup"><span data-stu-id="b684d-150">Logging</span></span>

<span data-ttu-id="b684d-151">В следующем примере кода приложения логики показано, как обрабатывать ведение журналов.</span><span class="sxs-lookup"><span data-stu-id="b684d-151">The following logic app code sample shows how to handle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="b684d-152">Запись в журнале</span><span class="sxs-lookup"><span data-stu-id="b684d-152">Log entry</span></span>

<span data-ttu-id="b684d-153">Вот исходный код приложения логики для добавления записи в журнал:</span><span class="sxs-lookup"><span data-stu-id="b684d-153">Here is the logic app source code for inserting a log entry.</span></span>

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

#### <a name="log-request"></a><span data-ttu-id="b684d-154">Запрос к журналу</span><span class="sxs-lookup"><span data-stu-id="b684d-154">Log request</span></span>

<span data-ttu-id="b684d-155">Вот сообщение с запросом к журналу, переданное в приложение API:</span><span class="sxs-lookup"><span data-stu-id="b684d-155">Here is the log request message posted to the API app.</span></span>

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


#### <a name="log-response"></a><span data-ttu-id="b684d-156">Ответ журнала</span><span class="sxs-lookup"><span data-stu-id="b684d-156">Log response</span></span>

<span data-ttu-id="b684d-157">Вот сообщение с ответом из журнала, полученное из приложения API:</span><span class="sxs-lookup"><span data-stu-id="b684d-157">Here is the log response message from the API app.</span></span>

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

<span data-ttu-id="b684d-158">Теперь давайте рассмотрим действия по обработке ошибок.</span><span class="sxs-lookup"><span data-stu-id="b684d-158">Now let's look at the error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="b684d-159">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="b684d-159">Error handling</span></span>

<span data-ttu-id="b684d-160">В следующем примере кода приложения логики показано, как можно реализовать обработку ошибок.</span><span class="sxs-lookup"><span data-stu-id="b684d-160">The following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="b684d-161">Создание записи об ошибке</span><span class="sxs-lookup"><span data-stu-id="b684d-161">Create error record</span></span>

<span data-ttu-id="b684d-162">Вот исходный код приложения логики, который используется для создания записи об ошибке:</span><span class="sxs-lookup"><span data-stu-id="b684d-162">Here is the logic app source code for creating an error record.</span></span>

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

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="b684d-163">Добавление записи об ошибке в Cosmos DB — запрос</span><span class="sxs-lookup"><span data-stu-id="b684d-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="b684d-164">Добавление записи об ошибке в Cosmos DB — ответ</span><span class="sxs-lookup"><span data-stu-id="b684d-164">Insert error into Cosmos DB--response</span></span>

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
        "body": "CRM failed to complete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
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

#### <a name="salesforce-error-response"></a><span data-ttu-id="b684d-165">Ответ на ошибку Salesforce</span><span class="sxs-lookup"><span data-stu-id="b684d-165">Salesforce error response</span></span>

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
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-the-response-back-to-parent-logic-app"></a><span data-ttu-id="b684d-166">Возвращение ответа в родительское приложение логики</span><span class="sxs-lookup"><span data-stu-id="b684d-166">Return the response back to parent logic app</span></span>

<span data-ttu-id="b684d-167">После получения ответа его можно вернуть в родительское приложение логики.</span><span class="sxs-lookup"><span data-stu-id="b684d-167">After you get the response, you can pass the response back to the parent logic app.</span></span>

#### <a name="return-success-response-to-parent-logic-app"></a><span data-ttu-id="b684d-168">Возвращение успешного ответа в родительское приложение логики</span><span class="sxs-lookup"><span data-stu-id="b684d-168">Return success response to parent logic app</span></span>

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

#### <a name="return-error-response-to-parent-logic-app"></a><span data-ttu-id="b684d-169">Возвращение ответа на ошибку в родительское приложение логики</span><span class="sxs-lookup"><span data-stu-id="b684d-169">Return error response to parent logic app</span></span>

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


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="b684d-170">Репозиторий и портал Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b684d-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="b684d-171">Благодаря использованию [Cosmos DB](https://azure.microsoft.com/services/documentdb) наше решение предоставляет больше возможностей.</span><span class="sxs-lookup"><span data-stu-id="b684d-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="b684d-172">Портал управления ошибками</span><span class="sxs-lookup"><span data-stu-id="b684d-172">Error management portal</span></span>

<span data-ttu-id="b684d-173">Чтобы просмотреть ошибки, полученные из Cosmos DB, можно создать веб-приложение MVC, в котором будут отображаться соответствующие записи об ошибках.</span><span class="sxs-lookup"><span data-stu-id="b684d-173">To view the errors, you can create an MVC web app to display the error records from Cosmos DB.</span></span> <span data-ttu-id="b684d-174">В текущую версию приложения входят операции **List**, **Details**, **Edit** и **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b684d-174">The **List**, **Details**, **Edit**, and **Delete** operations are included in the current version.</span></span>

> [!NOTE]
> <span data-ttu-id="b684d-175">Операция Edit: Cosmos DB заменяет весь документ.</span><span class="sxs-lookup"><span data-stu-id="b684d-175">Edit operation: Cosmos DB replaces the entire document.</span></span> <span data-ttu-id="b684d-176">Записи в представлении списка (**List**) и в подробном представлении (**Detail**) приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b684d-176">The records shown in the **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="b684d-177">Это не фактические записи о приемах пациентов.</span><span class="sxs-lookup"><span data-stu-id="b684d-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="b684d-178">Ниже приведены примеры сведений о приложении MVC, созданные с помощью описанного выше метода.</span><span class="sxs-lookup"><span data-stu-id="b684d-178">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="b684d-179">Список для управления ошибками</span><span class="sxs-lookup"><span data-stu-id="b684d-179">Error management list</span></span>
![Список ошибок](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="b684d-181">Просмотр подробных сведений об ошибке</span><span class="sxs-lookup"><span data-stu-id="b684d-181">Error management detail view</span></span>
![Сведения об ошибке](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="b684d-183">Портал управления журналами</span><span class="sxs-lookup"><span data-stu-id="b684d-183">Log management portal</span></span>

<span data-ttu-id="b684d-184">Для просмотра журналов мы также создали веб-приложение MVC.</span><span class="sxs-lookup"><span data-stu-id="b684d-184">To view the logs, we also created an MVC web app.</span></span> <span data-ttu-id="b684d-185">Ниже приведены примеры сведений о приложении MVC, созданные с помощью описанного выше метода.</span><span class="sxs-lookup"><span data-stu-id="b684d-185">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="b684d-186">Просмотр подробных сведений об ошибке из журнала</span><span class="sxs-lookup"><span data-stu-id="b684d-186">Sample log detail view</span></span>
![Просмотр сведений о записи журнала](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="b684d-188">Сведения о приложении API</span><span class="sxs-lookup"><span data-stu-id="b684d-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="b684d-189">API управления исключениями приложений логики</span><span class="sxs-lookup"><span data-stu-id="b684d-189">Logic Apps exception management API</span></span>

<span data-ttu-id="b684d-190">Приложение API на основе Azure Logic Apps с открытым исходным кодом, которое мы создали для управления исключениями, поддерживает следующие возможности, включая два контроллера:</span><span class="sxs-lookup"><span data-stu-id="b684d-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="b684d-191">**ErrorController** добавляет запись об ошибке (документ) в коллекцию DocumentDB;</span><span class="sxs-lookup"><span data-stu-id="b684d-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="b684d-192">**LogController** добавляет запись журнала (документ) в коллекцию DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="b684d-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="b684d-193">Оба контроллера используют операции `async Task<dynamic>`, что позволяет выполнять операции в среде выполнения, а значит, мы сможем создать схему DocumentDB в тексте операции.</span><span class="sxs-lookup"><span data-stu-id="b684d-193">Both controllers use `async Task<dynamic>` operations, allowing operations to resolve at runtime, so we can create the DocumentDB schema in the body of the operation.</span></span> 
> 

<span data-ttu-id="b684d-194">Каждому документу в DocumentDB необходимо присвоить уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="b684d-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="b684d-195">Мы используем идентификатор `PatientId` , к которому добавляем метку времени, преобразованную в значение в формате Unix (значение с двойной точностью).</span><span class="sxs-lookup"><span data-stu-id="b684d-195">We are using `PatientId` and adding a timestamp that is converted to a Unix timestamp value (double).</span></span> <span data-ttu-id="b684d-196">Чтобы удалить дробное значение, мы обрежем метку времени.</span><span class="sxs-lookup"><span data-stu-id="b684d-196">We truncate the value to remove the fractional value.</span></span>

<span data-ttu-id="b684d-197">Исходный код API контроллера ошибок доступен [в репозитории GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="b684d-197">You can view the source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="b684d-198">Для вызова API из приложения логики используется следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="b684d-198">We call the API from a logic app by using the following syntax:</span></span>

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

<span data-ttu-id="b684d-199">Выражение в примере кода выше проверяет, не имеет ли параметр *Create_NewPatientRecord* значение **Failed**.</span><span class="sxs-lookup"><span data-stu-id="b684d-199">The expression in the preceding code sample checks for the *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="b684d-200">Сводка</span><span class="sxs-lookup"><span data-stu-id="b684d-200">Summary</span></span>

* <span data-ttu-id="b684d-201">В приложении логики можно легко реализовать ведение журнала и обработку ошибок.</span><span class="sxs-lookup"><span data-stu-id="b684d-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="b684d-202">DocumentDB можно использовать в качестве репозитория для хранения записей журнала и записей об ошибках (документов).</span><span class="sxs-lookup"><span data-stu-id="b684d-202">You can use DocumentDB as the repository for log and error records (documents).</span></span>
* <span data-ttu-id="b684d-203">С помощью веб-приложения MVC можно создать портал, на котором будут отображаться записи журналов и записи об ошибках.</span><span class="sxs-lookup"><span data-stu-id="b684d-203">You can use MVC to create a portal to display log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="b684d-204">Исходный код</span><span class="sxs-lookup"><span data-stu-id="b684d-204">Source code</span></span>

<span data-ttu-id="b684d-205">Исходный код для приложения API, используемого для управления исключениями приложений логики, доступен в [репозитории GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "API управления исключениями приложений логики").</span><span class="sxs-lookup"><span data-stu-id="b684d-205">The source code for the Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="b684d-206">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b684d-206">Next steps</span></span>

* [<span data-ttu-id="b684d-207">Примеры приложений логики и распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="b684d-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="b684d-208">Мониторинг приложений логики</span><span class="sxs-lookup"><span data-stu-id="b684d-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="b684d-209">Создание шаблона развертывания приложения логики</span><span class="sxs-lookup"><span data-stu-id="b684d-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
