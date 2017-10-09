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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Уведомление пациентов об изменениях в медицинских картах HL7 FHIR с помощью Logic Apps и Azure Cosmos DB

Недавно Azure Edidin Говард MVP подключился здравоохранения организации, которая нужна tooadd новые функциональные возможности tootheir пациента портала. Они нужны toopatients toosend уведомлений при их записи работоспособности была обновлена, и они нужны пациентов toobe может toosubscribe toothese обновлений. 

В этой статье рассматриваются hello изменение канала уведомлений решения, созданного для этой организации здравоохранения, с помощью Azure Cosmos DB, Logic Apps и Service Bus. 

## <a name="project-requirements"></a>Проектные требования
- Поставщики отправляют документы в формате XML, соответствующие архитектуре HL7 для консолидированных клинических документов (C-CDA). Документы C-CDA могут включать практически любые типы клинических документов, в том числе клинические (семейные истории болезни, журналы вакцинации и т. п.), административные, операционные и финансовые. 
- Документы C CDA преобразуются слишком[FHIR ресурсы HL7](http://hl7.org/fhir/2017Jan/resourcelist.html) в формате JSON.
- Преобразованные документы ресурсов FHIR отправляются по электронной почте в формате JSON.

## <a name="solution-workflow"></a>Рабочий процесс решения 

На высоком уровне hello проекту требуется hello действий рабочего процесса: 
1. Преобразуйте ресурсы tooFHIR C CDA документов.
2. Регулярный опрос триггеров для выявления измененных ресурсов FHIR. 
2. Вызов пользовательского приложения, FhirNotificationApi, tooconnect tooAzure Cosmos DB и запросов для новых или измененных документов.
3. Сохраните очереди Service Bus tootoohello hello ответов.
4. Опрос для новых сообщений в очереди Service Bus hello.
5. Отправьте по электронной почте уведомления toopatients.

## <a name="solution-architecture"></a>Архитектура решения
Это решение требует трех hello toomeet Logic Apps выше требования и рабочий процесс завершения hello решения. Ниже перечислены три логику приложения Hello
1. **Приложение HL7 FHIR сопоставления**: Получает документ HL7 C-CDA hello, преобразует их toohello FHIR ресурсов, а затем сохраняет его tooAzure Cosmos DB.
2. **Приложение EHR**: запрос hello Azure Cosmos DB FHIR репозитория и сохраняет очереди Service Bus tooa ответов hello. Это приложение логики использует [приложения API](#api-app) tooretrieve новые и измененные документы.
3. **Процесс уведомления приложения**: отправляет уведомление по электронной почте с документами ресурсов FHIR hello в тексте hello.

![Приложения Hello трех логики, используемый в этом решении здравоохранения HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Используемые в решении hello служб Azure

#### <a name="azure-cosmos-db-documentdb-api"></a>API DocumentDB в Azure Cosmos DB
Azure Cosmos DB — репозиторий hello hello FHIR ресурсов, как показано в hello следующий рисунок.

![Учетная запись Azure Cosmos DB Hello, используемая в этом учебнике здравоохранения HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Logic Apps
Приложения логики обработки hello рабочего процесса. Hello следующих снимках экрана показано hello логики приложений, созданных для этого решения. 


1. **Приложение HL7 FHIR сопоставления**: получить документ HL7 C-CDA hello и преобразовать его tooan FHIR ресурсов с использованием hello пакет интеграции Enterprise для логики приложений. Пакет интеграции Enterprise Hello обрабатывает сопоставление из hello ресурсов tooFHIR C CDA hello.

    ![Логика приложения Hello используется tooreceive HL7 FHIR медицинских записей](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **Приложение EHR**: запроса hello Azure Cosmos DB FHIR репозиторий и сохраните tooa ответа hello Service Bus в очередь. Hello для приложения hello GetNewOrModifiedFHIRDocuments приведен ниже.

    ![tooquery Hello использовать приложения логики Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **Процесс уведомления приложения**: отправить уведомление по электронной почте с документами ресурсов FHIR hello в тексте hello.

    ![Hello логики приложения, отправляющие пациента письма с ресурсом HL7 FHIR hello в тексте hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>Служебная шина
Следующий рисунок показывает hello пациентов очереди Hello. Hello значению свойства Tag используется тема сообщения hello.

![Hello очередь Service Bus, используемые в этом учебнике HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>Приложение API
Приложения API подключается tooAzure Cosmos DB и запросов для новых или измененных документов FHIR от типа ресурса. Это приложение содержит один контроллер **FhirNotificationApi** с одной операцией **GetNewOrModifiedFhirDocuments** (см. раздел об [исходном коде для приложения API](#api-app-source)).

Мы используем hello [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) класс из hello Azure Cosmos DB DocumentDB .NET API. Дополнительные сведения см. в разделе hello [изменение веб-канала статьи](change-feed.md). 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>Операция GetNewOrModifiedFhirDocuments

**Входные данные**
- DatabaseId;
- CollectionId;
- имя типа ресурса FHIR HL7;
- логическое значение Start from Beginning (Начать с начала);
- целочисленное значение количества обработанных документов.

**Outputs**
- При успешном завершении: код состояния 200; возвращается список документов (в массиве JSON).
- В случае ошибки: код состояния 404; возвращает строку "No Documents found for '*resource name'* Resource Type" (Не найдены документы с типом ресурса "имя_ресурса").

<a id="api-app-source"></a>

**Источник для приложение hello API**

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

### <a name="testing-hello-fhirnotificationapi"></a>Приветствие FhirNotificationApi тестирования 

Hello на рисунке показано, каким образом было hello используется tootootest swagger [FhirNotificationApi](#api-app-source).

![файл Swagger Hello использовать приложение API tootest hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Панель мониторинга портала Azure

Следующие изображения Hello показывает все hello служб Azure для этого решения, работающих в hello портал Azure.

![портал Azure, показывающий все службы hello, используемые в этом учебнике HL7 FHIR Hello](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>Сводка

- Вы узнали, что Azure Cosmos DB имеет собственный поддержки для получения уведомлений о новых или изменена документы и как просто можно toouse. 
- Используя приложения логики, вы можете создавать рабочие процессы даже без написания кода.
- С помощью распространения hello toohandle очереди шины обслуживания Azure для hello HL7 FHIR документов.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о базе данных Azure Cosmos см. в разделе hello [Домашняя страница Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). Подробную информацию о приложениях логики см. [здесь](https://azure.microsoft.com/services/logic-apps/).


