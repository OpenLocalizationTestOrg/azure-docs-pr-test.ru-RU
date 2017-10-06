---
title: "базы данных aaaMulti master архитектуры с помощью Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, как toodesign архитектур приложений с локальным считывают и записывают в нескольких географических регионов с Azure Cosmos DB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 706ced74-ea67-45dd-a7de-666c3c893687
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3269c8405afe16f75db69b42e576fe76e00a8e16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a>Архитектуры с несколькими глобально реплицированными базами данных master с использованием Azure Cosmos DB
Azure Cosmos DB поддерживает под ключ [глобального репликации](distribute-data-globally.md), что позволяет toodistribute области toomultiple данных с низкой задержкой доступ в любом месте рабочей нагрузки hello. Эта модель обычно используется для рабочих нагрузок типа "издатель и потребитель", в которых модуль записи находится в одном географическом регионе, а глобально распределенные модули чтения — в других регионах (регионах чтения). 

Также можно использовать Azure Cosmos DB репликации глобальных поддержки toobuild приложений в которых объекты записи и чтения глобально распределяются. В этом документе рассматривается шаблон, который позволяет обеспечить локальные операции записи и чтения для распределенных модулей записи с помощью Azure Cosmos DB.

## <a id="ExampleScenario"></a>Пример сценария публикации содержимого
Давайте взглянем на toodescribe реальные сценарии и использование шаблонов распределенной несколькими region и несколькими главный чтение и запись с Azure Cosmos DB. Рассмотрим платформу публикации содержимого, созданную на базе Azure Cosmos DB. Ниже приведены некоторые требования, которым эта платформа должна соответствовать, чтобы обеспечить удобство работы пользователя как с издателями, так и с потребителями.

* Авторы и подписчики отделениями Здравствуй, мир! 
* Авторы необходимо опубликовать (запись) статьи tootheir локального (ближайший) области
* Читатели/подписчиков их статей распределяются по всему миру hello, включающих авторов. 
* Подписчики должны получать уведомление при публикации новой статьи.
* Подписчики должны быть статей может tooread из своей локальной области. Они также должны быть может tooadd проверки toothese статей. 
* Любой пользователь, включая автора hello hello статей должен быть сможет просматривать, что все hello проверками вложенного tooarticles из локальной области. 

Миллионы клиентам и издателям миллиардов статей, при условии, что вскоре у нас есть tooconfront hello проблемы масштабирования и обеспечения доступа к расположению. Как и большинство проблем масштабируемость hello решение заключается в хорошие стратегии секционирования. Теперь рассмотрим как toomodel статей, просмотра и уведомления в виде документов, Настройка учетных записей Azure Cosmos DB и реализации уровня доступа к данным. 

Если вы хотите toolearn Дополнительные сведения о создании разделов и разделов, в разделе [секционирование и масштабирование в базе данных Azure Cosmos](partition-data.md).

## <a id="ModelingNotifications"></a>Моделирование уведомлений
Уведомления — это пользователь tooa конкретного веб-каналов данных. Таким образом шаблоны доступа к hello для документов уведомления всегда находятся в контексте hello одного пользователя. Например вы «post tooa уведомления пользователя» или «извлечь все уведомления для данного пользователя». Таким образом, hello оптимальным выбором секционирования ключ для этого типа будет `UserId`.

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // hello user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // hello partition Key for hello resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of hello notification. 
        public string ArticleId { get; set; } 
    }

## <a id="ModelingSubscriptions"></a>Моделирование подписок
Подписки могут быть созданы для различных критериев, например для определенной интересующей категории статей или определенного издателя. Здравствуйте, поэтому `SubscriptionFilter` лучше всего подойдет для ключа раздела.

    class Subscriptions 
    { 
        // Unique ID for Subscription 
        public string Id { get; set; }

        // Subscription source. Could be Author | Category etc. 
        public string SubscriptionFilter { get; set; }

        // subscribing User. 
        public string UserId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.SubscriptionFilter; 
            } 
        } 
    }

## <a id="ModelingArticles"></a>Моделирование статей
После определения статьи по уведомлениям в последующих запросах обычно основаны на hello `Article.Id`. Выбор `Article.Id` как раздел ключ hello тем самым предоставляя hello наиболее распространения для хранения статьи в базе данных Azure Cosmos коллекции. 

    class Article 
    { 
        // Unique ID for Article 
        public string Id { get; set; }
        
        public string PartitionKey 
        { 
            get 
            { 
                return this.Id; 
            } 
        }
        
        // Author of hello article
        public string Author { get; set; }

        // Category/genre of hello article
        public string Category { get; set; }

        // Tags associated with hello article
        public string[] Tags { get; set; }

        // Title of hello article
        public string Title { get; set; }
        
        //... 
    }

## <a id="ModelingReviews"></a>Моделирование рецензий
Как статьи обзоры главным образом записи и чтения в контексте hello статьи. Если выбрать `ArticleId` в качестве ключа секции, это обеспечит наилучшее распространение рецензий, связанных со статьей, и эффективный доступ к ним. 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of hello review 
        public string ArticleId { get; set; }

        public string PartitionKey 
        { 
            get 
            { 
                return this.ArticleId; 
            } 
        }
        
        //Reviewer Id 
        public string UserId { get; set; }
        public string ReviewText { get; set; }
        
        public int Rating { get; set; } }
    }

## <a id="DataAccessMethods"></a>Методы уровня доступа к данным
Теперь давайте рассмотрим hello основных данных мы должны tooimplement методов доступа. Ниже приведен список методов, которые hello hello `ContentPublishDatabase` должен:

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <a id="Architecture"></a>Конфигурация учетной записи Azure Cosmos DB
tooguarantee локального считывает и записывает данные, должны секционировать данные не только на ключ секционирования, но также основана на шаблон географических доступа hello в области. Hello модели зависит от необходимости георепликацией Azure Cosmos DB учетной записи базы данных для каждого региона. Например, ниже приведена конфигурация операций записи в несколько регионов в среде с двумя регионами.

| Имя учетной записи | Регион записи | Регион чтения |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

Hello следующей схеме показано, как выполнять операции чтения и записи в типичном приложении с помощью этой программы:

![Архитектура с несколькими базами данных master на основе Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

Ниже приведен фрагмент кода, показывающий, как tooinitialize hello клиентов в DAL, работающих в hello `West US` области.
    
    ConnectionPolicy writeClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    writeClientPolicy.PreferredLocations.Add(LocationNames.WestUS);
    writeClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);

    DocumentClient writeClient = new DocumentClient(
        new Uri("https://contentpubdatabase-usa.documents.azure.com"), 
        writeRegionAuthKey,
        writeClientPolicy);

    ConnectionPolicy readClientPolicy = new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp };
    readClientPolicy.PreferredLocations.Add(LocationNames.NorthEurope);
    readClientPolicy.PreferredLocations.Add(LocationNames.WestUS);

    DocumentClient readClient = new DocumentClient(
        new Uri("https://contentpubdatabase-europe.documents.azure.com"),
        readRegionAuthKey,
        readClientPolicy);

Hello предшествующей установки уровень доступа к данным hello пересылает все записи toohello локальной учетной записи на основе которых она развернута. Операции чтения выполняются путем чтения из обеих учетных записей tooget hello глобальное представление данных. Этот подход может быть расширенных tooas многих регионах при необходимости. Например, ниже приведена конфигурация с тремя географическими регионами.

| Имя учетной записи | Регион записи | Регион чтения 1 | Регион чтения 2 |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <a id="DataAccessImplementation"></a>Реализация уровня доступа к данным
Теперь давайте рассмотрим реализацию hello hello доступа к данным (DAL) для приложения с двумя областями для записи. Hello DAL, должны реализовывать hello следующие шаги:

* Создание нескольких экземпляров `DocumentClient` для каждой учетной записи. В конфигурации с двумя регионами у каждого экземпляра DAL имеется по одному `writeClient` и `readClient`. 
* На основе hello развернут области приложения hello, настройте hello конечных точек для `writeclient` и `readClient`. Например, hello DAL развертываются в `West US` использует `contentpubdatabase-usa.documents.azure.com` для выполнения операций записи. Hello DAL развернутых в `NorthEurope` использует `contentpubdatabase-europ.documents.azure.com` для операций записи.

С hello предшествующей установки можно реализовать hello методов доступа к данным. Записи операций пересылать hello записи toohello соответствующий `writeClient`.

    public async Task CreateSubscriptionAsync(string userId, string category)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Subscriptions
        {
            UserId = userId,
            SubscriptionFilter = category
        });
    }

    public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating)
    {
        await this.writeClient.CreateDocumentAsync(this.contentCollection, new Review
        {
            UserId = userId,
            ArticleId = articleId,
            ReviewText = reviewText,
            Rating = rating
        });
    }

Для чтения, уведомления и проверки, необходимо прочитать из области и результатов union hello как показано в следующий фрагмент кода hello:

    public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId)
    {
        IDocumentQuery<Notification> writeAccountNotification = (
            from notification in this.writeClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();
        
        IDocumentQuery<Notification> readAccountNotification = (
            from notification in this.readClient.CreateDocumentQuery<Notification>(this.contentCollection) 
            where notification.UserId == userId 
            select notification).AsDocumentQuery();

        List<Notification> notifications = new List<Notification>();

        while (writeAccountNotification.HasMoreResults || readAccountNotification.HasMoreResults)
        {
            IList<Task<FeedResponse<Notification>>> results = new List<Task<FeedResponse<Notification>>>();

            if (writeAccountNotification.HasMoreResults)
            {
                results.Add(writeAccountNotification.ExecuteNextAsync<Notification>());
            }

            if (readAccountNotification.HasMoreResults)
            {
                results.Add(readAccountNotification.ExecuteNextAsync<Notification>());
            }

            IList<FeedResponse<Notification>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Notification> feed in notificationFeedResult)
            {
                notifications.AddRange(feed);
            }
        }
        return notifications;
    }

    public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId)
    {
        IDocumentQuery<Review> writeAccountReviews = (
            from review in this.writeClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();
        
        IDocumentQuery<Review> readAccountReviews = (
            from review in this.readClient.CreateDocumentQuery<Review>(this.contentCollection) 
            where review.ArticleId == articleId 
            select review).AsDocumentQuery();

        List<Review> reviews = new List<Review>();
        
        while (writeAccountReviews.HasMoreResults || readAccountReviews.HasMoreResults)
        {
            IList<Task<FeedResponse<Review>>> results = new List<Task<FeedResponse<Review>>>();

            if (writeAccountReviews.HasMoreResults)
            {
                results.Add(writeAccountReviews.ExecuteNextAsync<Review>());
            }

            if (readAccountReviews.HasMoreResults)
            {
                results.Add(readAccountReviews.ExecuteNextAsync<Review>());
            }

            IList<FeedResponse<Review>> notificationFeedResult = await Task.WhenAll(results);

            foreach (FeedResponse<Review> feed in notificationFeedResult)
            {
                reviews.AddRange(feed);
            }
        }

        return reviews;
    }

Таким образом, выбрав подходящий ключ секционирования и статическое секционирование на основе учетных записей, с помощью Azure Cosmos DB можно достичь локальности операций записи и чтения в нескольких регионах.

## <a id="NextSteps"></a>Дальнейшие действия
В этой статье на примере сценария публикации содержимого показано, как с помощью Azure Cosmos DB использовать шаблоны чтения и записи в глобально распределенных средах с несколькими регионами.

* Дополнительные сведения о поддержке глобального распределения в Azure Cosmos DB см. в [этой статье](distribute-data-globally.md).
* Узнайте об [автоматической и ручной отработках отказа в Azure Cosmos DB](regional-failover.md).
* Дополнительные сведения о глобальной согласованности в Cosmos DB см. в [этой статье](consistency-levels.md).
* Разработка с несколькими областями с помощью hello [Cosmos Azure база данных — DocumentDB API](tutorial-global-distribution-documentdb.md)
* Разработка с несколькими областями с помощью hello [Cosmos Azure база данных — MongoDB API](tutorial-global-distribution-MongoDB.md)
* Разработка с несколькими областями с помощью hello [Cosmos Azure база данных — таблицу API](tutorial-global-distribution-table.md)
