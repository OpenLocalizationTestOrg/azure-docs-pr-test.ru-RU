---
title: "Веб-канал изменений для ресурсов HL7 FHIR в Azure Cosmos DB | Документация Майкрософт"
description: "Сведения о настройке уведомлений об изменениях в медицинских картах пациентов в системе HL7 FHIR с помощью Azure Logic Apps, Azure Cosmos DB и служебной шины."
keywords: HL7 FHIR
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2b50c0b6864af41fb9cfa051721c432772b228d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="b953b-104">Уведомление пациентов об изменениях в медицинских картах HL7 FHIR с помощью Logic Apps и Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b953b-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="b953b-105">Недавно специалист MVP по Azure Ховард Эдидин (Howard Edidin) получил запрос от медицинской организации, которая решила добавить новые функциональные возможности на свой портал для пациентов.</span><span class="sxs-lookup"><span data-stu-id="b953b-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="b953b-106">Ей нужно было отправлять пациентам уведомления об изменениях в медицинских картах, а также предоставить пациентам возможность подписаться на такие уведомления.</span><span class="sxs-lookup"><span data-stu-id="b953b-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="b953b-107">Эта статья содержит пошаговое описание процесса, позволившего создать для этой организации веб-канал изменений с помощью Azure Cosmos DB, Logic Apps и служебной шины.</span><span class="sxs-lookup"><span data-stu-id="b953b-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="b953b-108">Проектные требования</span><span class="sxs-lookup"><span data-stu-id="b953b-108">Project requirements</span></span>
- <span data-ttu-id="b953b-109">Поставщики отправляют документы в формате XML, соответствующие архитектуре HL7 для консолидированных клинических документов (C-CDA).</span><span class="sxs-lookup"><span data-stu-id="b953b-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="b953b-110">Документы C-CDA могут включать практически любые типы клинических документов, в том числе клинические (семейные истории болезни, журналы вакцинации и т. п.), административные, операционные и финансовые.</span><span class="sxs-lookup"><span data-stu-id="b953b-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="b953b-111">Документы C-CDA преобразуются в [ресурсы HL7 FHIR](http://hl7.org/fhir/2017Jan/resourcelist.html) в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b953b-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="b953b-112">Преобразованные документы ресурсов FHIR отправляются по электронной почте в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="b953b-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="b953b-113">Рабочий процесс решения</span><span class="sxs-lookup"><span data-stu-id="b953b-113">Solution workflow</span></span> 

<span data-ttu-id="b953b-114">На высоком уровне этот проект включал следующие этапы рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="b953b-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="b953b-115">Преобразование документов C-CDA в ресурсы FHIR.</span><span class="sxs-lookup"><span data-stu-id="b953b-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="b953b-116">Регулярный опрос триггеров для выявления измененных ресурсов FHIR.</span><span class="sxs-lookup"><span data-stu-id="b953b-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="b953b-117">Вызов пользовательского приложения FhirNotificationApi для подключения к Azure Cosmos DB и получения новых и измененных документов.</span><span class="sxs-lookup"><span data-stu-id="b953b-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="b953b-118">Сохранение ответа в очереди служебной шины.</span><span class="sxs-lookup"><span data-stu-id="b953b-118">Save the response to to the Service Bus queue.</span></span>
4. <span data-ttu-id="b953b-119">Опрос очереди служебной шины для отслеживания новых сообщений.</span><span class="sxs-lookup"><span data-stu-id="b953b-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="b953b-120">Отправка пациентам уведомлений по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="b953b-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="b953b-121">Архитектура решения</span><span class="sxs-lookup"><span data-stu-id="b953b-121">Solution architecture</span></span>
<span data-ttu-id="b953b-122">Для выполнения перечисленных выше требований и создания полного рабочего процесса в это решение потребовалось включить три приложения логики,</span><span class="sxs-lookup"><span data-stu-id="b953b-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="b953b-123">перечисленные ниже.</span><span class="sxs-lookup"><span data-stu-id="b953b-123">The three logic apps are:</span></span>
1. <span data-ttu-id="b953b-124">**Приложение HL7-FHIR-Mapping** получает документ HL7 C-CDA, преобразует его в ресурс FHIR, а затем сохраняет в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b953b-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="b953b-125">**Приложение EHR** запрашивает репозиторий FHIR в Azure Cosmos DB и сохраняет ответ в очередь служебной шины.</span><span class="sxs-lookup"><span data-stu-id="b953b-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="b953b-126">Это приложение логики использует [приложение API](#api-app) для получения новых и измененных документов.</span><span class="sxs-lookup"><span data-stu-id="b953b-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="b953b-127">**Приложение для обработки уведомлений** отправляет по электронной почте уведомление, в текст которого включает документы ресурсов FHIR.</span><span class="sxs-lookup"><span data-stu-id="b953b-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![Три приложения логики, используемые в этом решении HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="b953b-129">Службы Azure, используемые в решении</span><span class="sxs-lookup"><span data-stu-id="b953b-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="b953b-130">API DocumentDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b953b-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="b953b-131">Azure Cosmos DB выполняет роль репозитория для ресурсов FHIR, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="b953b-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![Учетная запись Azure Cosmos DB, используемая в этом руководстве по HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="b953b-133">Приложения логики</span><span class="sxs-lookup"><span data-stu-id="b953b-133">Logic Apps</span></span>
<span data-ttu-id="b953b-134">Приложения логики обрабатывают рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="b953b-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="b953b-135">На следующих снимках экрана показаны приложения логики, созданные для этого решения.</span><span class="sxs-lookup"><span data-stu-id="b953b-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="b953b-136">**Приложение HL7-FHIR-Mapping** получает документ HL7 C-CDA и преобразует его в ресурс FHIR с помощью пакета интеграции Enterprise для Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b953b-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="b953b-137">Пакет интеграции Enterprise обрабатывает сопоставление C-CDA с ресурсами FHIR.</span><span class="sxs-lookup"><span data-stu-id="b953b-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![Приложение логики для получения медицинских карт HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="b953b-139">**Приложение EHR** отправляет запросы в репозиторий FHIR в Azure Cosmos DB и сохраняет ответ в очередь служебной шины.</span><span class="sxs-lookup"><span data-stu-id="b953b-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="b953b-140">Ниже приводится код приложения GetNewOrModifiedFHIRDocuments.</span><span class="sxs-lookup"><span data-stu-id="b953b-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Приложение логики, используемое для запросов к Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="b953b-142">**Приложение для обработки уведомлений** отправляет по электронной почте уведомление, в текст которого включает документы ресурсов FHIR.</span><span class="sxs-lookup"><span data-stu-id="b953b-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![Приложение логики, отправляющее пациенту сообщение электронной почты, текст которого содержит ресурсы HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="b953b-144">Service Bus</span><span class="sxs-lookup"><span data-stu-id="b953b-144">Service Bus</span></span>
<span data-ttu-id="b953b-145">На следующем рисунке показана очередь пациентов.</span><span class="sxs-lookup"><span data-stu-id="b953b-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="b953b-146">Значение свойства Tag используется для создания темы сообщения электронной почты.</span><span class="sxs-lookup"><span data-stu-id="b953b-146">The Tag property value is used for the email subject.</span></span>

![Очередь служебной шины, используемая в этом руководстве по HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="b953b-148">Приложение API</span><span class="sxs-lookup"><span data-stu-id="b953b-148">API app</span></span>
<span data-ttu-id="b953b-149">Приложение API подключается к Azure Cosmos DB и запрашивает наличие новых или измененных документов FHIR по типу ресурса.</span><span class="sxs-lookup"><span data-stu-id="b953b-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="b953b-150">Это приложение содержит один контроллер **FhirNotificationApi** с одной операцией **GetNewOrModifiedFhirDocuments** (см. раздел об [исходном коде для приложения API](#api-app-source)).</span><span class="sxs-lookup"><span data-stu-id="b953b-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="b953b-151">Мы используем класс [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) из API-интерфейса .NET для DocumentDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b953b-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="b953b-152">Дополнительные сведения см. в статье [Работа с поддержкой веб-канала изменений в Azure DocumentDB](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="b953b-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="b953b-153">Операция GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="b953b-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="b953b-154">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="b953b-154">**Inputs**</span></span>
- <span data-ttu-id="b953b-155">DatabaseId;</span><span class="sxs-lookup"><span data-stu-id="b953b-155">DatabaseId</span></span>
- <span data-ttu-id="b953b-156">CollectionId;</span><span class="sxs-lookup"><span data-stu-id="b953b-156">CollectionId</span></span>
- <span data-ttu-id="b953b-157">имя типа ресурса FHIR HL7;</span><span class="sxs-lookup"><span data-stu-id="b953b-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="b953b-158">логическое значение Start from Beginning (Начать с начала);</span><span class="sxs-lookup"><span data-stu-id="b953b-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="b953b-159">целочисленное значение количества обработанных документов.</span><span class="sxs-lookup"><span data-stu-id="b953b-159">Int: Number of documents returned</span></span>

<span data-ttu-id="b953b-160">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="b953b-160">**Outputs**</span></span>
- <span data-ttu-id="b953b-161">При успешном завершении: код состояния 200; возвращается список документов (в массиве JSON).</span><span class="sxs-lookup"><span data-stu-id="b953b-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="b953b-162">В случае ошибки: код состояния 404; возвращает строку "No Documents found for '*resource name'* Resource Type" (Не найдены документы с типом ресурса "имя_ресурса").</span><span class="sxs-lookup"><span data-stu-id="b953b-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="b953b-163">**Исходный код приложения API**</span><span class="sxs-lookup"><span data-stu-id="b953b-163">**Source for the API app**</span></span>

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="b953b-164">Тестирование FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="b953b-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="b953b-165">На следующем рисунке показано, как использовалось приложение Swagger для тестирования [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="b953b-165">The following image demonstrates how swagger was used to to test the [FhirNotificationApi](#api-app-source).</span></span>

![Файл Swagger, используемый для тестирования приложения API](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="b953b-167">Панель мониторинга портала Azure</span><span class="sxs-lookup"><span data-stu-id="b953b-167">Azure portal dashboard</span></span>

<span data-ttu-id="b953b-168">На следующем рисунке показаны все службы Azure, используемые в этом решении, которые работают на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b953b-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![Портал Azure с информацией обо всех службах, используемых в этом руководстве по HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="b953b-170">Сводка</span><span class="sxs-lookup"><span data-stu-id="b953b-170">Summary</span></span>

- <span data-ttu-id="b953b-171">Вы узнали, что в Azure Cosmos DB есть встроенная поддержка уведомлений о новых или измененных документах, и научились легко ее применять.</span><span class="sxs-lookup"><span data-stu-id="b953b-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="b953b-172">Используя приложения логики, вы можете создавать рабочие процессы даже без написания кода.</span><span class="sxs-lookup"><span data-stu-id="b953b-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="b953b-173">Также вы узнали, как использовать очереди служебной шины Azure для обработки распространения документов HL7 FHIR.</span><span class="sxs-lookup"><span data-stu-id="b953b-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b953b-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b953b-174">Next steps</span></span>
<span data-ttu-id="b953b-175">Дополнительные сведения о базе данных Azure Cosmos DB см. на [ее главной странице](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="b953b-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="b953b-176">Подробную информацию о приложениях логики см. [здесь](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="b953b-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


