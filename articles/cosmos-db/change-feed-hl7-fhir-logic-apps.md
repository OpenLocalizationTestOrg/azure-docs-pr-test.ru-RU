---
title: "веб-канал для ресурсов HL7 FHIR - Azure Cosmos DB aaaChange | Документы Microsoft"
description: "Узнайте, как tooset копирование изменить уведомления для HL7 FHIR здравоохранения пациентов с помощью приложения логики Azure Azure Cosmos DB и Service Bus."
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
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="14378-104">Уведомление пациентов об изменениях в медицинских картах HL7 FHIR с помощью Logic Apps и Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="14378-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="14378-105">Недавно Azure Edidin Говард MVP подключился здравоохранения организации, которая нужна tooadd новые функциональные возможности tootheir пациента портала.</span><span class="sxs-lookup"><span data-stu-id="14378-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="14378-106">Они нужны toopatients toosend уведомлений при их записи работоспособности была обновлена, и они нужны пациентов toobe может toosubscribe toothese обновлений.</span><span class="sxs-lookup"><span data-stu-id="14378-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="14378-107">В этой статье рассматриваются hello изменение канала уведомлений решения, созданного для этой организации здравоохранения, с помощью Azure Cosmos DB, Logic Apps и Service Bus.</span><span class="sxs-lookup"><span data-stu-id="14378-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="14378-108">Проектные требования</span><span class="sxs-lookup"><span data-stu-id="14378-108">Project requirements</span></span>
- <span data-ttu-id="14378-109">Поставщики отправляют документы в формате XML, соответствующие архитектуре HL7 для консолидированных клинических документов (C-CDA).</span><span class="sxs-lookup"><span data-stu-id="14378-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="14378-110">Документы C-CDA могут включать практически любые типы клинических документов, в том числе клинические (семейные истории болезни, журналы вакцинации и т. п.), административные, операционные и финансовые.</span><span class="sxs-lookup"><span data-stu-id="14378-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="14378-111">Документы C CDA преобразуются слишком[FHIR ресурсы HL7](http://hl7.org/fhir/2017Jan/resourcelist.html) в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="14378-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="14378-112">Преобразованные документы ресурсов FHIR отправляются по электронной почте в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="14378-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="14378-113">Рабочий процесс решения</span><span class="sxs-lookup"><span data-stu-id="14378-113">Solution workflow</span></span> 

<span data-ttu-id="14378-114">На высоком уровне hello проекту требуется hello действий рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="14378-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="14378-115">Преобразуйте ресурсы tooFHIR C CDA документов.</span><span class="sxs-lookup"><span data-stu-id="14378-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="14378-116">Регулярный опрос триггеров для выявления измененных ресурсов FHIR.</span><span class="sxs-lookup"><span data-stu-id="14378-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="14378-117">Вызов пользовательского приложения, FhirNotificationApi, tooconnect tooAzure Cosmos DB и запросов для новых или измененных документов.</span><span class="sxs-lookup"><span data-stu-id="14378-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="14378-118">Сохраните очереди Service Bus tootoohello hello ответов.</span><span class="sxs-lookup"><span data-stu-id="14378-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="14378-119">Опрос для новых сообщений в очереди Service Bus hello.</span><span class="sxs-lookup"><span data-stu-id="14378-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="14378-120">Отправьте по электронной почте уведомления toopatients.</span><span class="sxs-lookup"><span data-stu-id="14378-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="14378-121">Архитектура решения</span><span class="sxs-lookup"><span data-stu-id="14378-121">Solution architecture</span></span>
<span data-ttu-id="14378-122">Это решение требует трех hello toomeet Logic Apps выше требования и рабочий процесс завершения hello решения.</span><span class="sxs-lookup"><span data-stu-id="14378-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="14378-123">Ниже перечислены три логику приложения Hello</span><span class="sxs-lookup"><span data-stu-id="14378-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="14378-124">**Приложение HL7 FHIR сопоставления**: Получает документ HL7 C-CDA hello, преобразует их toohello FHIR ресурсов, а затем сохраняет его tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="14378-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="14378-125">**Приложение EHR**: запрос hello Azure Cosmos DB FHIR репозитория и сохраняет очереди Service Bus tooa ответов hello.</span><span class="sxs-lookup"><span data-stu-id="14378-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="14378-126">Это приложение логики использует [приложения API](#api-app) tooretrieve новые и измененные документы.</span><span class="sxs-lookup"><span data-stu-id="14378-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="14378-127">**Процесс уведомления приложения**: отправляет уведомление по электронной почте с документами ресурсов FHIR hello в тексте hello.</span><span class="sxs-lookup"><span data-stu-id="14378-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![Приложения Hello трех логики, используемый в этом решении здравоохранения HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="14378-129">Используемые в решении hello служб Azure</span><span class="sxs-lookup"><span data-stu-id="14378-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="14378-130">API DocumentDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="14378-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="14378-131">Azure Cosmos DB — репозиторий hello hello FHIR ресурсов, как показано в hello следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="14378-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![Учетная запись Azure Cosmos DB Hello, используемая в этом учебнике здравоохранения HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="14378-133">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="14378-133">Logic Apps</span></span>
<span data-ttu-id="14378-134">Приложения логики обработки hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="14378-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="14378-135">Hello следующих снимках экрана показано hello логики приложений, созданных для этого решения.</span><span class="sxs-lookup"><span data-stu-id="14378-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="14378-136">**Приложение HL7 FHIR сопоставления**: получить документ HL7 C-CDA hello и преобразовать его tooan FHIR ресурсов с использованием hello пакет интеграции Enterprise для логики приложений.</span><span class="sxs-lookup"><span data-stu-id="14378-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="14378-137">Пакет интеграции Enterprise Hello обрабатывает сопоставление из hello ресурсов tooFHIR C CDA hello.</span><span class="sxs-lookup"><span data-stu-id="14378-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![Логика приложения Hello используется tooreceive HL7 FHIR медицинских записей](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="14378-139">**Приложение EHR**: запроса hello Azure Cosmos DB FHIR репозиторий и сохраните tooa ответа hello Service Bus в очередь.</span><span class="sxs-lookup"><span data-stu-id="14378-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="14378-140">Hello для приложения hello GetNewOrModifiedFHIRDocuments приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="14378-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![tooquery Hello использовать приложения логики Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="14378-142">**Процесс уведомления приложения**: отправить уведомление по электронной почте с документами ресурсов FHIR hello в тексте hello.</span><span class="sxs-lookup"><span data-stu-id="14378-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![Hello логики приложения, отправляющие пациента письма с ресурсом HL7 FHIR hello в тексте hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="14378-144">Служебная шина</span><span class="sxs-lookup"><span data-stu-id="14378-144">Service Bus</span></span>
<span data-ttu-id="14378-145">Следующий рисунок показывает hello пациентов очереди Hello.</span><span class="sxs-lookup"><span data-stu-id="14378-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="14378-146">Hello значению свойства Tag используется тема сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="14378-146">hello Tag property value is used for hello email subject.</span></span>

![Hello очередь Service Bus, используемые в этом учебнике HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="14378-148">Приложение API</span><span class="sxs-lookup"><span data-stu-id="14378-148">API app</span></span>
<span data-ttu-id="14378-149">Приложения API подключается tooAzure Cosmos DB и запросов для новых или измененных документов FHIR от типа ресурса.</span><span class="sxs-lookup"><span data-stu-id="14378-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="14378-150">Это приложение содержит один контроллер **FhirNotificationApi** с одной операцией **GetNewOrModifiedFhirDocuments** (см. раздел об [исходном коде для приложения API](#api-app-source)).</span><span class="sxs-lookup"><span data-stu-id="14378-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="14378-151">Мы используем hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) класс из hello Azure Cosmos DB DocumentDB .NET API.</span><span class="sxs-lookup"><span data-stu-id="14378-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="14378-152">Дополнительные сведения см. в разделе hello [изменение веб-канала статьи](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="14378-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="14378-153">Операция GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="14378-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="14378-154">**Входные данные**</span><span class="sxs-lookup"><span data-stu-id="14378-154">**Inputs**</span></span>
- <span data-ttu-id="14378-155">DatabaseId;</span><span class="sxs-lookup"><span data-stu-id="14378-155">DatabaseId</span></span>
- <span data-ttu-id="14378-156">CollectionId;</span><span class="sxs-lookup"><span data-stu-id="14378-156">CollectionId</span></span>
- <span data-ttu-id="14378-157">имя типа ресурса FHIR HL7;</span><span class="sxs-lookup"><span data-stu-id="14378-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="14378-158">логическое значение Start from Beginning (Начать с начала);</span><span class="sxs-lookup"><span data-stu-id="14378-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="14378-159">целочисленное значение количества обработанных документов.</span><span class="sxs-lookup"><span data-stu-id="14378-159">Int: Number of documents returned</span></span>

<span data-ttu-id="14378-160">**Outputs**</span><span class="sxs-lookup"><span data-stu-id="14378-160">**Outputs**</span></span>
- <span data-ttu-id="14378-161">При успешном завершении: код состояния 200; возвращается список документов (в массиве JSON).</span><span class="sxs-lookup"><span data-stu-id="14378-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="14378-162">В случае ошибки: код состояния 404; возвращает строку "No Documents found for '*resource name'* Resource Type" (Не найдены документы с типом ресурса "имя_ресурса").</span><span class="sxs-lookup"><span data-stu-id="14378-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="14378-163">**Источник для приложение hello API**</span><span class="sxs-lookup"><span data-stu-id="14378-163">**Source for hello API app**</span></span>

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
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
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

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="14378-164">Приветствие FhirNotificationApi тестирования</span><span class="sxs-lookup"><span data-stu-id="14378-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="14378-165">Hello на рисунке показано, каким образом было hello используется tootootest swagger [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="14378-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![файл Swagger Hello использовать приложение API tootest hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="14378-167">Панель мониторинга портала Azure</span><span class="sxs-lookup"><span data-stu-id="14378-167">Azure portal dashboard</span></span>

<span data-ttu-id="14378-168">Следующие изображения Hello показывает все hello служб Azure для этого решения, работающих в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="14378-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![портал Azure, показывающий все службы hello, используемые в этом учебнике HL7 FHIR Hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="14378-170">Сводка</span><span class="sxs-lookup"><span data-stu-id="14378-170">Summary</span></span>

- <span data-ttu-id="14378-171">Вы узнали, что Azure Cosmos DB имеет собственный поддержки для получения уведомлений о новых или изменена документы и как просто можно toouse.</span><span class="sxs-lookup"><span data-stu-id="14378-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="14378-172">Используя приложения логики, вы можете создавать рабочие процессы даже без написания кода.</span><span class="sxs-lookup"><span data-stu-id="14378-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="14378-173">С помощью распространения hello toohandle очереди шины обслуживания Azure для hello HL7 FHIR документов.</span><span class="sxs-lookup"><span data-stu-id="14378-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14378-174">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="14378-174">Next steps</span></span>
<span data-ttu-id="14378-175">Дополнительные сведения о базе данных Azure Cosmos см. в разделе hello [Домашняя страница Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="14378-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="14378-176">Подробную информацию о приложениях логики см. [здесь](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="14378-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


