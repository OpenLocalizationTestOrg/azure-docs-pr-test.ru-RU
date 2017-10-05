---
title: "Архитектуры с несколькими базами данных master с использованием Azure Cosmos DB | Документация Майкрософт"
description: "Узнайте, как проектировать архитектуры приложений с локальными операциями чтения и записи в нескольких географических регионах с помощью Azure Cosmos DB."
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
ms.openlocfilehash: cf1482ae7b1070023703f5dbe861d151f5d64fd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="5156a-103">Архитектуры с несколькими глобально реплицированными базами данных master с использованием Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5156a-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="5156a-104">Azure Cosmos DB поддерживает готовую [глобальную репликацию](distribute-data-globally.md), что позволяет распространять данные в нескольких регионах и обеспечивает доступ с низкой задержкой в любом месте рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="5156a-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you to distribute data to multiple regions with low latency access anywhere in the workload.</span></span> <span data-ttu-id="5156a-105">Эта модель обычно используется для рабочих нагрузок типа "издатель и потребитель", в которых модуль записи находится в одном географическом регионе, а глобально распределенные модули чтения — в других регионах (регионах чтения).</span><span class="sxs-lookup"><span data-stu-id="5156a-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="5156a-106">Поддержку глобальной репликации Azure Cosmos DB можно также использовать для создания приложений с глобально распределенными модулями записи и чтения.</span><span class="sxs-lookup"><span data-stu-id="5156a-106">You can also use Azure Cosmos DB's global replication support to build applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="5156a-107">В этом документе рассматривается шаблон, который позволяет обеспечить локальные операции записи и чтения для распределенных модулей записи с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5156a-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="5156a-108"><a id="ExampleScenario"></a>Пример сценария публикации содержимого</span><span class="sxs-lookup"><span data-stu-id="5156a-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="5156a-109">Рассмотрим реальный сценарий, чтобы показать, как можно использовать шаблоны чтения и записи в глобально распределенных средах с несколькими регионами или несколькими базами данных master с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5156a-109">Let's look at a real world scenario to describe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="5156a-110">Рассмотрим платформу публикации содержимого, созданную на базе Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5156a-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="5156a-111">Ниже приведены некоторые требования, которым эта платформа должна соответствовать, чтобы обеспечить удобство работы пользователя как с издателями, так и с потребителями.</span><span class="sxs-lookup"><span data-stu-id="5156a-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="5156a-112">Авторы и подписчики разбросаны по всему земному шару.</span><span class="sxs-lookup"><span data-stu-id="5156a-112">Both authors and subscribers are spread over the world</span></span> 
* <span data-ttu-id="5156a-113">Авторам необходимо публиковать (записывать) статьи в своем локальном (ближайшем) регионе.</span><span class="sxs-lookup"><span data-stu-id="5156a-113">Authors must publish (write) articles to their local (closest) region</span></span>
* <span data-ttu-id="5156a-114">У авторов статей есть читатели и подписчики, разбросанные по всему миру.</span><span class="sxs-lookup"><span data-stu-id="5156a-114">Authors have readers/subscribers of their articles who are distributed across the globe.</span></span> 
* <span data-ttu-id="5156a-115">Подписчики должны получать уведомление при публикации новой статьи.</span><span class="sxs-lookup"><span data-stu-id="5156a-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="5156a-116">Подписчики должны иметь возможность читать статьи в своем локальном регионе.</span><span class="sxs-lookup"><span data-stu-id="5156a-116">Subscribers must be able to read articles from their local region.</span></span> <span data-ttu-id="5156a-117">Они также должны иметь возможность добавлять рецензентов этих статей.</span><span class="sxs-lookup"><span data-stu-id="5156a-117">They should also be able to add reviews to these articles.</span></span> 
* <span data-ttu-id="5156a-118">Кто угодно, включая автора статей, должен иметь возможность просматривать все рецензии, прилагаемые к статьям из локального региона.</span><span class="sxs-lookup"><span data-stu-id="5156a-118">Anyone including the author of the articles should be able view all the reviews attached to articles from a local region.</span></span> 

<span data-ttu-id="5156a-119">Предполагая участие миллионов потребителей и издателей и наличие миллиардов статей, очень скоро мы столкнемся с проблемами масштабирования и гарантирования локальности доступа.</span><span class="sxs-lookup"><span data-stu-id="5156a-119">Assuming millions of consumers and publishers with billions of articles, soon we have to confront the problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="5156a-120">Как с большинством проблем масштабируемости, решение заключается в качественной стратегии секционирования.</span><span class="sxs-lookup"><span data-stu-id="5156a-120">As with most scalability problems, the solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="5156a-121">Давайте рассмотрим, как смоделировать статьи, рецензии и уведомления как документы, настроить учетные записи Azure Cosmos DB и реализовать уровень доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="5156a-121">Next, let's look at how to model articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="5156a-122">Если вы хотите узнать больше о секционировании и ключах секций, ознакомьтесь со статьей [Секционирование и масштабирование в базе данных Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="5156a-122">If you would like to learn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="5156a-123"><a id="ModelingNotifications"></a>Моделирование уведомлений</span><span class="sxs-lookup"><span data-stu-id="5156a-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="5156a-124">Уведомления — это веб-каналы данных конкретного пользователя.</span><span class="sxs-lookup"><span data-stu-id="5156a-124">Notifications are data feeds specific to a user.</span></span> <span data-ttu-id="5156a-125">Следовательно, шаблоны доступа для документов уведомлений всегда находятся в контексте одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="5156a-125">Therefore, the access patterns for notifications documents are always in the context of single user.</span></span> <span data-ttu-id="5156a-126">Например, можно "отправить уведомление пользователю" или "получить все уведомления для заданного пользователя".</span><span class="sxs-lookup"><span data-stu-id="5156a-126">For example, you would "post a notification to a user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="5156a-127">Поэтому оптимальным выбором типа ключа секционирования будет `UserId`.</span><span class="sxs-lookup"><span data-stu-id="5156a-127">So, the optimal choice of partitioning key for this type would be `UserId`.</span></span>

    class Notification 
    { 
        // Unique ID for Notification. 
        public string Id { get; set; }

        // The user Id for which notification is addressed to. 
        public string UserId { get; set; }

        // The partition Key for the resource. 
        public string PartitionKey 
        { 
            get 
            { 
                return this.UserId; 
            }
        }

        // Subscription for which this notification is raised. 
        public string SubscriptionFilter { get; set; }

        // Subject of the notification. 
        public string ArticleId { get; set; } 
    }

## <span data-ttu-id="5156a-128"><a id="ModelingSubscriptions"></a>Моделирование подписок</span><span class="sxs-lookup"><span data-stu-id="5156a-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="5156a-129">Подписки могут быть созданы для различных критериев, например для определенной интересующей категории статей или определенного издателя.</span><span class="sxs-lookup"><span data-stu-id="5156a-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="5156a-130">Поэтому `SubscriptionFilter` — удачный выбор для ключа секции.</span><span class="sxs-lookup"><span data-stu-id="5156a-130">Hence the `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="5156a-131"><a id="ModelingArticles"></a>Моделирование статей</span><span class="sxs-lookup"><span data-stu-id="5156a-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="5156a-132">После определения статьи посредством уведомлений последующие запросы обычно основаны на `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="5156a-132">Once an article is identified through notifications, subsequent queries are typically based on the `Article.Id`.</span></span> <span data-ttu-id="5156a-133">Поэтому выбор `Article.Id` в качестве ключа секции обеспечивает наилучшее распределение для хранения статей в коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5156a-133">Choosing `Article.Id` as partition the key thus provides the best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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
        
        // Author of the article
        public string Author { get; set; }

        // Category/genre of the article
        public string Category { get; set; }

        // Tags associated with the article
        public string[] Tags { get; set; }

        // Title of the article
        public string Title { get; set; }
        
        //... 
    }

## <span data-ttu-id="5156a-134"><a id="ModelingReviews"></a>Моделирование рецензий</span><span class="sxs-lookup"><span data-stu-id="5156a-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="5156a-135">Как и статьи, рецензии главным образом создаются и читаются в контексте статьи.</span><span class="sxs-lookup"><span data-stu-id="5156a-135">Like articles, reviews are mostly written and read in the context of article.</span></span> <span data-ttu-id="5156a-136">Если выбрать `ArticleId` в качестве ключа секции, это обеспечит наилучшее распространение рецензий, связанных со статьей, и эффективный доступ к ним.</span><span class="sxs-lookup"><span data-stu-id="5156a-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

    class Review 
    { 
        // Unique ID for Review 
        public string Id { get; set; }

        // Article Id of the review 
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

## <span data-ttu-id="5156a-137"><a id="DataAccessMethods"></a>Методы уровня доступа к данным</span><span class="sxs-lookup"><span data-stu-id="5156a-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="5156a-138">Теперь давайте рассмотрим основные методы доступа к данных, которые нужно реализовать.</span><span class="sxs-lookup"><span data-stu-id="5156a-138">Now let's look at the main data access methods we need to implement.</span></span> <span data-ttu-id="5156a-139">Ниже приведен список методов, требуемых для `ContentPublishDatabase`.</span><span class="sxs-lookup"><span data-stu-id="5156a-139">Here's the list of methods that the `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="5156a-140"><a id="Architecture"></a>Конфигурация учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5156a-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="5156a-141">Чтобы обеспечить локальные операции чтения и записи, необходимо секционировать данные не только по ключу секции, но и с учетом шаблона географического доступа к регионам.</span><span class="sxs-lookup"><span data-stu-id="5156a-141">To guarantee local reads and writes, we must partition data not just on partition key, but also based on the geographical access pattern into regions.</span></span> <span data-ttu-id="5156a-142">Модель основана на использовании геореплицируемой учетной записи базы данных Azure Cosmos DB для каждого региона.</span><span class="sxs-lookup"><span data-stu-id="5156a-142">The model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="5156a-143">Например, ниже приведена конфигурация операций записи в несколько регионов в среде с двумя регионами.</span><span class="sxs-lookup"><span data-stu-id="5156a-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="5156a-144">Имя учетной записи</span><span class="sxs-lookup"><span data-stu-id="5156a-144">Account Name</span></span> | <span data-ttu-id="5156a-145">Регион записи</span><span class="sxs-lookup"><span data-stu-id="5156a-145">Write Region</span></span> | <span data-ttu-id="5156a-146">Регион чтения</span><span class="sxs-lookup"><span data-stu-id="5156a-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="5156a-147">На следующей схеме показано, как при такой конфигурации выполняются чтение и запись в типичном приложении.</span><span class="sxs-lookup"><span data-stu-id="5156a-147">The following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Архитектура с несколькими базами данных master на основе Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="5156a-149">Ниже приведен фрагмент кода, показывающий, как инициализировать на уровне доступа к данным клиенты, работающие в регионе `West US`.</span><span class="sxs-lookup"><span data-stu-id="5156a-149">Here is a code snippet showing how to initialize the clients in a DAL running in the `West US` region.</span></span>
    
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

<span data-ttu-id="5156a-150">В приведенной ранее конфигурации уровень доступа к данным может направлять все операции записи в локальную учетную запись в зависимости от того, где она развернута.</span><span class="sxs-lookup"><span data-stu-id="5156a-150">With the preceding setup, the data access layer can forward all writes to the local account based on where it is deployed.</span></span> <span data-ttu-id="5156a-151">При операциях чтения выполняется чтение из обеих учетных записей для получения глобального представления данных.</span><span class="sxs-lookup"><span data-stu-id="5156a-151">Reads are performed by reading from both accounts to get the global view of data.</span></span> <span data-ttu-id="5156a-152">Этот подход можно распространить на любое число регионов.</span><span class="sxs-lookup"><span data-stu-id="5156a-152">This approach can be extended to as many regions as required.</span></span> <span data-ttu-id="5156a-153">Например, ниже приведена конфигурация с тремя географическими регионами.</span><span class="sxs-lookup"><span data-stu-id="5156a-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="5156a-154">Имя учетной записи</span><span class="sxs-lookup"><span data-stu-id="5156a-154">Account Name</span></span> | <span data-ttu-id="5156a-155">Регион записи</span><span class="sxs-lookup"><span data-stu-id="5156a-155">Write Region</span></span> | <span data-ttu-id="5156a-156">Регион чтения 1</span><span class="sxs-lookup"><span data-stu-id="5156a-156">Read Region 1</span></span> | <span data-ttu-id="5156a-157">Регион чтения 2</span><span class="sxs-lookup"><span data-stu-id="5156a-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="5156a-158"><a id="DataAccessImplementation"></a>Реализация уровня доступа к данным</span><span class="sxs-lookup"><span data-stu-id="5156a-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="5156a-159">Теперь давайте рассмотрим реализацию уровня доступа к данным (DAL) для приложения с двумя регионами для записи.</span><span class="sxs-lookup"><span data-stu-id="5156a-159">Now let's look at the implementation of the data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="5156a-160">DAL должен реализовывать следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5156a-160">The DAL must implement the following steps:</span></span>

* <span data-ttu-id="5156a-161">Создание нескольких экземпляров `DocumentClient` для каждой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5156a-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="5156a-162">В конфигурации с двумя регионами у каждого экземпляра DAL имеется по одному `writeClient` и `readClient`.</span><span class="sxs-lookup"><span data-stu-id="5156a-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="5156a-163">Настройка конечных точек для `writeclient` и `readClient` на основе региона развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="5156a-163">Based on the deployed region of the application, configure the endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="5156a-164">Например, DAL, развернутый в `West US`, использует `contentpubdatabase-usa.documents.azure.com` для выполнения операций записи.</span><span class="sxs-lookup"><span data-stu-id="5156a-164">For example, the DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="5156a-165">DAL, развернутый в `NorthEurope`, для операций записи использует `contentpubdatabase-europ.documents.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="5156a-165">The DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="5156a-166">В представленной ранее конфигурации можно реализовать методы доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="5156a-166">With the preceding setup, the data access methods can be implemented.</span></span> <span data-ttu-id="5156a-167">Операции записи перенаправляют запись к соответствующему `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="5156a-167">Write operations forward the write to the corresponding `writeClient`.</span></span>

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

<span data-ttu-id="5156a-168">Для чтения уведомлений и рецензий необходимо считать данные из обоих регионов и объединить результаты, как показано в следующем фрагменте кода.</span><span class="sxs-lookup"><span data-stu-id="5156a-168">For reading notifications and reviews, you must read from both regions and union the results as shown in the following snippet:</span></span>

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

<span data-ttu-id="5156a-169">Таким образом, выбрав подходящий ключ секционирования и статическое секционирование на основе учетных записей, с помощью Azure Cosmos DB можно достичь локальности операций записи и чтения в нескольких регионах.</span><span class="sxs-lookup"><span data-stu-id="5156a-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="5156a-170"><a id="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5156a-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="5156a-171">В этой статье на примере сценария публикации содержимого показано, как с помощью Azure Cosmos DB использовать шаблоны чтения и записи в глобально распределенных средах с несколькими регионами.</span><span class="sxs-lookup"><span data-stu-id="5156a-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="5156a-172">Дополнительные сведения о поддержке глобального распределения в Azure Cosmos DB см. в [этой статье](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="5156a-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="5156a-173">Узнайте об [автоматической и ручной отработках отказа в Azure Cosmos DB](regional-failover.md).</span><span class="sxs-lookup"><span data-stu-id="5156a-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="5156a-174">Дополнительные сведения о глобальной согласованности в Azure Cosmos DB см. в [этой статье](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="5156a-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="5156a-175">Сведения о разработке с использованием нескольких регионов с помощью API DocumentDB см. в статье [Как настроить глобальное распределение Azure Cosmos DB с помощью API DocumentDB](tutorial-global-distribution-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="5156a-175">Develop with multiple regions using the [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="5156a-176">Сведения о разработке с использованием нескольких регионов с помощью API MongoDB см. в статье [Как настроить глобальное распределение Azure Cosmos DB с помощью API MongoDB](tutorial-global-distribution-MongoDB.md).</span><span class="sxs-lookup"><span data-stu-id="5156a-176">Develop with multiple regions using the [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="5156a-177">Сведения о разработке с использованием нескольких регионов с помощью API таблицы см. в статье [Как настроить глобальное распределение Azure Cosmos DB с помощью API таблицы](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="5156a-177">Develop with multiple regions using the [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
