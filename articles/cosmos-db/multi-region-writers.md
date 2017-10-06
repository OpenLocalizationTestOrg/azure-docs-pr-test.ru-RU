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
# <a name="multi-master-globally-replicated-database-architectures-with-azure-cosmos-db"></a><span data-ttu-id="0f3ca-103">Архитектуры с несколькими глобально реплицированными базами данных master с использованием Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0f3ca-103">Multi-master globally replicated database architectures with Azure Cosmos DB</span></span>
<span data-ttu-id="0f3ca-104">Azure Cosmos DB поддерживает под ключ [глобального репликации](distribute-data-globally.md), что позволяет toodistribute области toomultiple данных с низкой задержкой доступ в любом месте рабочей нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-104">Azure Cosmos DB supports turnkey [global replication](distribute-data-globally.md), which allows you toodistribute data toomultiple regions with low latency access anywhere in hello workload.</span></span> <span data-ttu-id="0f3ca-105">Эта модель обычно используется для рабочих нагрузок типа "издатель и потребитель", в которых модуль записи находится в одном географическом регионе, а глобально распределенные модули чтения — в других регионах (регионах чтения).</span><span class="sxs-lookup"><span data-stu-id="0f3ca-105">This model is commonly used for publisher/consumer workloads where there is a writer in a single geographic region and globally distributed readers in other (read) regions.</span></span> 

<span data-ttu-id="0f3ca-106">Также можно использовать Azure Cosmos DB репликации глобальных поддержки toobuild приложений в которых объекты записи и чтения глобально распределяются.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-106">You can also use Azure Cosmos DB's global replication support toobuild applications in which writers and readers are globally distributed.</span></span> <span data-ttu-id="0f3ca-107">В этом документе рассматривается шаблон, который позволяет обеспечить локальные операции записи и чтения для распределенных модулей записи с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-107">This document outlines a pattern that enables achieving local write and local read access for distributed writers using Azure Cosmos DB.</span></span>

## <span data-ttu-id="0f3ca-108"><a id="ExampleScenario"></a>Пример сценария публикации содержимого</span><span class="sxs-lookup"><span data-stu-id="0f3ca-108"><a id="ExampleScenario"></a>Content Publishing - an example scenario</span></span>
<span data-ttu-id="0f3ca-109">Давайте взглянем на toodescribe реальные сценарии и использование шаблонов распределенной несколькими region и несколькими главный чтение и запись с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-109">Let's look at a real world scenario toodescribe how you can use globally distributed multi-region/multi-master read write patterns with Azure Cosmos DB.</span></span> <span data-ttu-id="0f3ca-110">Рассмотрим платформу публикации содержимого, созданную на базе Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-110">Consider a content publishing platform built on Azure Cosmos DB.</span></span> <span data-ttu-id="0f3ca-111">Ниже приведены некоторые требования, которым эта платформа должна соответствовать, чтобы обеспечить удобство работы пользователя как с издателями, так и с потребителями.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-111">Here are some requirements that this platform must meet for a great user experience for both publishers and consumers.</span></span>

* <span data-ttu-id="0f3ca-112">Авторы и подписчики отделениями Здравствуй, мир!</span><span class="sxs-lookup"><span data-stu-id="0f3ca-112">Both authors and subscribers are spread over hello world</span></span> 
* <span data-ttu-id="0f3ca-113">Авторы необходимо опубликовать (запись) статьи tootheir локального (ближайший) области</span><span class="sxs-lookup"><span data-stu-id="0f3ca-113">Authors must publish (write) articles tootheir local (closest) region</span></span>
* <span data-ttu-id="0f3ca-114">Читатели/подписчиков их статей распределяются по всему миру hello, включающих авторов.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-114">Authors have readers/subscribers of their articles who are distributed across hello globe.</span></span> 
* <span data-ttu-id="0f3ca-115">Подписчики должны получать уведомление при публикации новой статьи.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-115">Subscribers should get a notification when new articles are published.</span></span>
* <span data-ttu-id="0f3ca-116">Подписчики должны быть статей может tooread из своей локальной области.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-116">Subscribers must be able tooread articles from their local region.</span></span> <span data-ttu-id="0f3ca-117">Они также должны быть может tooadd проверки toothese статей.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-117">They should also be able tooadd reviews toothese articles.</span></span> 
* <span data-ttu-id="0f3ca-118">Любой пользователь, включая автора hello hello статей должен быть сможет просматривать, что все hello проверками вложенного tooarticles из локальной области.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-118">Anyone including hello author of hello articles should be able view all hello reviews attached tooarticles from a local region.</span></span> 

<span data-ttu-id="0f3ca-119">Миллионы клиентам и издателям миллиардов статей, при условии, что вскоре у нас есть tooconfront hello проблемы масштабирования и обеспечения доступа к расположению.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-119">Assuming millions of consumers and publishers with billions of articles, soon we have tooconfront hello problems of scale along with guaranteeing locality of access.</span></span> <span data-ttu-id="0f3ca-120">Как и большинство проблем масштабируемость hello решение заключается в хорошие стратегии секционирования.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-120">As with most scalability problems, hello solution lies in a good partitioning strategy.</span></span> <span data-ttu-id="0f3ca-121">Теперь рассмотрим как toomodel статей, просмотра и уведомления в виде документов, Настройка учетных записей Azure Cosmos DB и реализации уровня доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-121">Next, let's look at how toomodel articles, review, and notifications as documents, configure Azure Cosmos DB accounts, and implement a data access layer.</span></span> 

<span data-ttu-id="0f3ca-122">Если вы хотите toolearn Дополнительные сведения о создании разделов и разделов, в разделе [секционирование и масштабирование в базе данных Azure Cosmos](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="0f3ca-122">If you would like toolearn more about partitioning and partition keys, see [Partitioning and Scaling in Azure Cosmos DB](partition-data.md).</span></span>

## <span data-ttu-id="0f3ca-123"><a id="ModelingNotifications"></a>Моделирование уведомлений</span><span class="sxs-lookup"><span data-stu-id="0f3ca-123"><a id="ModelingNotifications"></a>Modeling notifications</span></span>
<span data-ttu-id="0f3ca-124">Уведомления — это пользователь tooa конкретного веб-каналов данных.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-124">Notifications are data feeds specific tooa user.</span></span> <span data-ttu-id="0f3ca-125">Таким образом шаблоны доступа к hello для документов уведомления всегда находятся в контексте hello одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-125">Therefore, hello access patterns for notifications documents are always in hello context of single user.</span></span> <span data-ttu-id="0f3ca-126">Например вы «post tooa уведомления пользователя» или «извлечь все уведомления для данного пользователя».</span><span class="sxs-lookup"><span data-stu-id="0f3ca-126">For example, you would "post a notification tooa user" or "fetch all notifications for a given user".</span></span> <span data-ttu-id="0f3ca-127">Таким образом, hello оптимальным выбором секционирования ключ для этого типа будет `UserId`.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-127">So, hello optimal choice of partitioning key for this type would be `UserId`.</span></span>

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

## <span data-ttu-id="0f3ca-128"><a id="ModelingSubscriptions"></a>Моделирование подписок</span><span class="sxs-lookup"><span data-stu-id="0f3ca-128"><a id="ModelingSubscriptions"></a>Modeling subscriptions</span></span>
<span data-ttu-id="0f3ca-129">Подписки могут быть созданы для различных критериев, например для определенной интересующей категории статей или определенного издателя.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-129">Subscriptions can be created for various criteria like a specific category of articles of interest, or a specific publisher.</span></span> <span data-ttu-id="0f3ca-130">Здравствуйте, поэтому `SubscriptionFilter` лучше всего подойдет для ключа раздела.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-130">Hence hello `SubscriptionFilter` is a good choice for partition key.</span></span>

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

## <span data-ttu-id="0f3ca-131"><a id="ModelingArticles"></a>Моделирование статей</span><span class="sxs-lookup"><span data-stu-id="0f3ca-131"><a id="ModelingArticles"></a>Modeling articles</span></span>
<span data-ttu-id="0f3ca-132">После определения статьи по уведомлениям в последующих запросах обычно основаны на hello `Article.Id`.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-132">Once an article is identified through notifications, subsequent queries are typically based on hello `Article.Id`.</span></span> <span data-ttu-id="0f3ca-133">Выбор `Article.Id` как раздел ключ hello тем самым предоставляя hello наиболее распространения для хранения статьи в базе данных Azure Cosmos коллекции.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-133">Choosing `Article.Id` as partition hello key thus provides hello best distribution for storing articles inside an Azure Cosmos DB collection.</span></span> 

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

## <span data-ttu-id="0f3ca-134"><a id="ModelingReviews"></a>Моделирование рецензий</span><span class="sxs-lookup"><span data-stu-id="0f3ca-134"><a id="ModelingReviews"></a>Modeling reviews</span></span>
<span data-ttu-id="0f3ca-135">Как статьи обзоры главным образом записи и чтения в контексте hello статьи.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-135">Like articles, reviews are mostly written and read in hello context of article.</span></span> <span data-ttu-id="0f3ca-136">Если выбрать `ArticleId` в качестве ключа секции, это обеспечит наилучшее распространение рецензий, связанных со статьей, и эффективный доступ к ним.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-136">Choosing `ArticleId` as a partition key provides best distribution and efficient access of reviews associated with article.</span></span> 

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

## <span data-ttu-id="0f3ca-137"><a id="DataAccessMethods"></a>Методы уровня доступа к данным</span><span class="sxs-lookup"><span data-stu-id="0f3ca-137"><a id="DataAccessMethods"></a>Data access layer methods</span></span>
<span data-ttu-id="0f3ca-138">Теперь давайте рассмотрим hello основных данных мы должны tooimplement методов доступа.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-138">Now let's look at hello main data access methods we need tooimplement.</span></span> <span data-ttu-id="0f3ca-139">Ниже приведен список методов, которые hello hello `ContentPublishDatabase` должен:</span><span class="sxs-lookup"><span data-stu-id="0f3ca-139">Here's hello list of methods that hello `ContentPublishDatabase` needs:</span></span>

    class ContentPublishDatabase 
    { 
        public async Task CreateSubscriptionAsync(string userId, string category);
    
        public async Task<IEnumerable<Notification>> ReadNotificationFeedAsync(string userId);
    
        public async Task<Article> ReadArticleAsync(string articleId);
    
        public async Task WriteReviewAsync(string articleId, string userId, string reviewText, int rating);
    
        public async Task<IEnumerable<Review>> ReadReviewsAsync(string articleId); 
    }

## <span data-ttu-id="0f3ca-140"><a id="Architecture"></a>Конфигурация учетной записи Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0f3ca-140"><a id="Architecture"></a>Azure Cosmos DB account configuration</span></span>
<span data-ttu-id="0f3ca-141">tooguarantee локального считывает и записывает данные, должны секционировать данные не только на ключ секционирования, но также основана на шаблон географических доступа hello в области.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-141">tooguarantee local reads and writes, we must partition data not just on partition key, but also based on hello geographical access pattern into regions.</span></span> <span data-ttu-id="0f3ca-142">Hello модели зависит от необходимости георепликацией Azure Cosmos DB учетной записи базы данных для каждого региона.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-142">hello model relies on having a geo-replicated Azure Cosmos DB database account for each region.</span></span> <span data-ttu-id="0f3ca-143">Например, ниже приведена конфигурация операций записи в несколько регионов в среде с двумя регионами.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-143">For example, with two regions, here's a setup for multi-region writes:</span></span>

| <span data-ttu-id="0f3ca-144">Имя учетной записи</span><span class="sxs-lookup"><span data-stu-id="0f3ca-144">Account Name</span></span> | <span data-ttu-id="0f3ca-145">Регион записи</span><span class="sxs-lookup"><span data-stu-id="0f3ca-145">Write Region</span></span> | <span data-ttu-id="0f3ca-146">Регион чтения</span><span class="sxs-lookup"><span data-stu-id="0f3ca-146">Read Region</span></span> |
| --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |

<span data-ttu-id="0f3ca-147">Hello следующей схеме показано, как выполнять операции чтения и записи в типичном приложении с помощью этой программы:</span><span class="sxs-lookup"><span data-stu-id="0f3ca-147">hello following diagram shows how reads and writes are performed in a typical application with this setup:</span></span>

![Архитектура с несколькими базами данных master на основе Azure Cosmos DB](./media/multi-region-writers/multi-master.png)

<span data-ttu-id="0f3ca-149">Ниже приведен фрагмент кода, показывающий, как tooinitialize hello клиентов в DAL, работающих в hello `West US` области.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-149">Here is a code snippet showing how tooinitialize hello clients in a DAL running in hello `West US` region.</span></span>
    
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

<span data-ttu-id="0f3ca-150">Hello предшествующей установки уровень доступа к данным hello пересылает все записи toohello локальной учетной записи на основе которых она развернута.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-150">With hello preceding setup, hello data access layer can forward all writes toohello local account based on where it is deployed.</span></span> <span data-ttu-id="0f3ca-151">Операции чтения выполняются путем чтения из обеих учетных записей tooget hello глобальное представление данных.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-151">Reads are performed by reading from both accounts tooget hello global view of data.</span></span> <span data-ttu-id="0f3ca-152">Этот подход может быть расширенных tooas многих регионах при необходимости.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-152">This approach can be extended tooas many regions as required.</span></span> <span data-ttu-id="0f3ca-153">Например, ниже приведена конфигурация с тремя географическими регионами.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-153">For example, here's a setup with three geographic regions:</span></span>

| <span data-ttu-id="0f3ca-154">Имя учетной записи</span><span class="sxs-lookup"><span data-stu-id="0f3ca-154">Account Name</span></span> | <span data-ttu-id="0f3ca-155">Регион записи</span><span class="sxs-lookup"><span data-stu-id="0f3ca-155">Write Region</span></span> | <span data-ttu-id="0f3ca-156">Регион чтения 1</span><span class="sxs-lookup"><span data-stu-id="0f3ca-156">Read Region 1</span></span> | <span data-ttu-id="0f3ca-157">Регион чтения 2</span><span class="sxs-lookup"><span data-stu-id="0f3ca-157">Read Region 2</span></span> |
| --- | --- | --- | --- |
| `contentpubdatabase-usa.documents.azure.com` | `West US` |`North Europe` |`Southeast Asia` |
| `contentpubdatabase-europe.documents.azure.com` | `North Europe` |`West US` |`Southeast Asia` |
| `contentpubdatabase-asia.documents.azure.com` | `Southeast Asia` |`North Europe` |`West US` |

## <span data-ttu-id="0f3ca-158"><a id="DataAccessImplementation"></a>Реализация уровня доступа к данным</span><span class="sxs-lookup"><span data-stu-id="0f3ca-158"><a id="DataAccessImplementation"></a>Data access layer implementation</span></span>
<span data-ttu-id="0f3ca-159">Теперь давайте рассмотрим реализацию hello hello доступа к данным (DAL) для приложения с двумя областями для записи.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-159">Now let's look at hello implementation of hello data access layer (DAL) for an application with two writable regions.</span></span> <span data-ttu-id="0f3ca-160">Hello DAL, должны реализовывать hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="0f3ca-160">hello DAL must implement hello following steps:</span></span>

* <span data-ttu-id="0f3ca-161">Создание нескольких экземпляров `DocumentClient` для каждой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-161">Create multiple instances of `DocumentClient` for each account.</span></span> <span data-ttu-id="0f3ca-162">В конфигурации с двумя регионами у каждого экземпляра DAL имеется по одному `writeClient` и `readClient`.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-162">With two regions, each DAL instance has one `writeClient` and one `readClient`.</span></span> 
* <span data-ttu-id="0f3ca-163">На основе hello развернут области приложения hello, настройте hello конечных точек для `writeclient` и `readClient`.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-163">Based on hello deployed region of hello application, configure hello endpoints for `writeclient` and `readClient`.</span></span> <span data-ttu-id="0f3ca-164">Например, hello DAL развертываются в `West US` использует `contentpubdatabase-usa.documents.azure.com` для выполнения операций записи.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-164">For example, hello DAL deployed in `West US` uses `contentpubdatabase-usa.documents.azure.com` for performing writes.</span></span> <span data-ttu-id="0f3ca-165">Hello DAL развернутых в `NorthEurope` использует `contentpubdatabase-europ.documents.azure.com` для операций записи.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-165">hello DAL deployed in `NorthEurope` uses `contentpubdatabase-europ.documents.azure.com` for writes.</span></span>

<span data-ttu-id="0f3ca-166">С hello предшествующей установки можно реализовать hello методов доступа к данным.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-166">With hello preceding setup, hello data access methods can be implemented.</span></span> <span data-ttu-id="0f3ca-167">Записи операций пересылать hello записи toohello соответствующий `writeClient`.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-167">Write operations forward hello write toohello corresponding `writeClient`.</span></span>

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

<span data-ttu-id="0f3ca-168">Для чтения, уведомления и проверки, необходимо прочитать из области и результатов union hello как показано в следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="0f3ca-168">For reading notifications and reviews, you must read from both regions and union hello results as shown in hello following snippet:</span></span>

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

<span data-ttu-id="0f3ca-169">Таким образом, выбрав подходящий ключ секционирования и статическое секционирование на основе учетных записей, с помощью Azure Cosmos DB можно достичь локальности операций записи и чтения в нескольких регионах.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-169">Thus, by choosing a good partitioning key and static account-based partitioning, you can achieve multi-region local writes and reads using Azure Cosmos DB.</span></span>

## <span data-ttu-id="0f3ca-170"><a id="NextSteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f3ca-170"><a id="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="0f3ca-171">В этой статье на примере сценария публикации содержимого показано, как с помощью Azure Cosmos DB использовать шаблоны чтения и записи в глобально распределенных средах с несколькими регионами.</span><span class="sxs-lookup"><span data-stu-id="0f3ca-171">In this article, we described how you can use globally distributed multi-region read write patterns with Azure Cosmos DB using content publishing as a sample scenario.</span></span>

* <span data-ttu-id="0f3ca-172">Дополнительные сведения о поддержке глобального распределения в Azure Cosmos DB см. в [этой статье](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="0f3ca-172">Learn about how Azure Cosmos DB supports [global distribution](distribute-data-globally.md)</span></span>
* <span data-ttu-id="0f3ca-173">Узнайте об [автоматической и ручной отработках отказа в Azure Cosmos DB](regional-failover.md).</span><span class="sxs-lookup"><span data-stu-id="0f3ca-173">Learn about [automatic and manual failovers in Azure Cosmos DB](regional-failover.md)</span></span>
* <span data-ttu-id="0f3ca-174">Дополнительные сведения о глобальной согласованности в Cosmos DB см. в [этой статье](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="0f3ca-174">Learn about [global consistency with Azure Cosmos DB](consistency-levels.md)</span></span>
* <span data-ttu-id="0f3ca-175">Разработка с несколькими областями с помощью hello [Cosmos Azure база данных — DocumentDB API](tutorial-global-distribution-documentdb.md)</span><span class="sxs-lookup"><span data-stu-id="0f3ca-175">Develop with multiple regions using hello [Azure Cosmos DB - DocumentDB API](tutorial-global-distribution-documentdb.md)</span></span>
* <span data-ttu-id="0f3ca-176">Разработка с несколькими областями с помощью hello [Cosmos Azure база данных — MongoDB API](tutorial-global-distribution-MongoDB.md)</span><span class="sxs-lookup"><span data-stu-id="0f3ca-176">Develop with multiple regions using hello [Azure Cosmos DB - MongoDB API](tutorial-global-distribution-MongoDB.md)</span></span>
* <span data-ttu-id="0f3ca-177">Разработка с несколькими областями с помощью hello [Cosmos Azure база данных — таблицу API](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="0f3ca-177">Develop with multiple regions using hello [Azure Cosmos DB - Table API](tutorial-global-distribution-table.md)</span></span>
