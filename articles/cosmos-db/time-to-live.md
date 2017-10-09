---
title: "aaaExpire данных в базе данных Azure Cosmos с временем toolive | Документы Microsoft"
description: "Срок ЖИЗНИ Microsoft Azure Cosmos DB обеспечивает hello возможность toohave документы автоматически удаляются из системы hello после определенного периода времени."
services: cosmos-db
documentationcenter: 
keywords: "время toolive"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="283b3-104">Срок действия данных в коллекциях Azure Cosmos DB автоматически с временем toolive</span><span class="sxs-lookup"><span data-stu-id="283b3-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="283b3-105">Приложения могут создавать и хранить большие объемы данных.</span><span class="sxs-lookup"><span data-stu-id="283b3-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="283b3-106">Некоторые из этих данных, например созданные компьютером данные о событиях, журналы и пользовательские сеансы, имеют ценность только в течение ограниченного периода времени.</span><span class="sxs-lookup"><span data-stu-id="283b3-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="283b3-107">После hello данные становятся избыточные toohello потребностями приложения hello он безопасном toopurge эти данные и уменьшить hello потребностям приложения.</span><span class="sxs-lookup"><span data-stu-id="283b3-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="283b3-108">«Время toolive» или истечения срока ЖИЗНИ Microsoft Azure Cosmos DB предоставляет hello возможность toohave документы автоматически удаляются из базы данных hello после определенного периода времени.</span><span class="sxs-lookup"><span data-stu-id="283b3-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="283b3-109">время по умолчанию Hello toolive можно задавать на уровне коллекции hello и переопределен в на уровне документа.</span><span class="sxs-lookup"><span data-stu-id="283b3-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="283b3-110">Когда свойство TTL определено (будь то время жизни по умолчанию на уровне коллекции или для конкретного документа), Cosmos DB автоматически удаляет документы, время жизни которых с момента их последнего изменения превышает заданное значение.</span><span class="sxs-lookup"><span data-stu-id="283b3-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="283b3-111">Время toolive в Cosmos DB использует смещение от последнего изменения документа hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="283b3-112">toodo этого оно использует hello `_ts` поля, которое существует в каждом документе.</span><span class="sxs-lookup"><span data-stu-id="283b3-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="283b3-113">поле _ts Hello является стиле unix эпохи timestamp представляющих hello даты и времени.</span><span class="sxs-lookup"><span data-stu-id="283b3-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="283b3-114">Hello `_ts` поле обновляется каждый раз при изменении документа.</span><span class="sxs-lookup"><span data-stu-id="283b3-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="283b3-115">Поведение TTL</span><span class="sxs-lookup"><span data-stu-id="283b3-115">TTL behavior</span></span>
<span data-ttu-id="283b3-116">функция TTL Hello управляется свойства TTL на двух уровнях — уровне коллекции hello и hello документа.</span><span class="sxs-lookup"><span data-stu-id="283b3-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="283b3-117">Hello значения задаются в секундах и обрабатываются как разностный из hello `_ts` документ hello было изменено на.</span><span class="sxs-lookup"><span data-stu-id="283b3-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="283b3-118">DefaultTTL для коллекции hello</span><span class="sxs-lookup"><span data-stu-id="283b3-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="283b3-119">Если отсутствует (или набор toonull), документы не удаляются автоматически.</span><span class="sxs-lookup"><span data-stu-id="283b3-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="283b3-120">При наличии и hello значение равно «-1» = неограниченное — документы не ограничивать срок действия по умолчанию</span><span class="sxs-lookup"><span data-stu-id="283b3-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="283b3-121">Если присутствует и hello имеет некоторое значение («n») — документов истекает «n» секунд после последнего изменения</span><span class="sxs-lookup"><span data-stu-id="283b3-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="283b3-122">Срок ЖИЗНИ для hello документов:</span><span class="sxs-lookup"><span data-stu-id="283b3-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="283b3-123">Свойство применимо только в том случае, если DefaultTTL отсутствует коллекция родительских hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="283b3-124">Переопределяет значение DefaultTTL hello для hello родительской коллекции.</span><span class="sxs-lookup"><span data-stu-id="283b3-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="283b3-125">Как только hello документа истек (`ttl`  +  `_ts` > = текущее время сервера), hello документ помечается как «устаревшая».</span><span class="sxs-lookup"><span data-stu-id="283b3-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="283b3-126">Операция не будет разрешен в этих документах после этой даты, и они будут исключены из результатов hello запросы, выполняемые.</span><span class="sxs-lookup"><span data-stu-id="283b3-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="283b3-127">документы Hello физически удаляются в системе hello и будут удалены в фоновом режиме hello возможности на более позднее время.</span><span class="sxs-lookup"><span data-stu-id="283b3-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="283b3-128">Это не использовать любой [единиц запроса (RUs)](request-units.md) из коллекции бюджета hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="283b3-129">Hello выше логику могут отображаться следующие матрицы hello:</span><span class="sxs-lookup"><span data-stu-id="283b3-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="283b3-130">DefaultTTL отсутствует или не включен hello коллекции</span><span class="sxs-lookup"><span data-stu-id="283b3-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="283b3-131">Свойство DefaultTTL на уровне коллекции имеет значение -1</span><span class="sxs-lookup"><span data-stu-id="283b3-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="283b3-132">Свойство DefaultTTL на уровне коллекции имеет значение n</span><span class="sxs-lookup"><span data-stu-id="283b3-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="283b3-133">Свойство TTL на уровне документа отсутствует</span><span class="sxs-lookup"><span data-stu-id="283b3-133">TTL Missing on document</span></span> |<span data-ttu-id="283b3-134">Ничего не toooverride на уровне документа, так как документ hello и коллекции не имеют концепции TTL.</span><span class="sxs-lookup"><span data-stu-id="283b3-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="283b3-135">Документы в этой коллекции не устаревают.</span><span class="sxs-lookup"><span data-stu-id="283b3-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="283b3-136">по истечении интервала n, истекает Hello документы в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="283b3-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="283b3-137">Свойство TTL на уровне документа имеет значение -1</span><span class="sxs-lookup"><span data-stu-id="283b3-137">TTL = -1 on document</span></span> |<span data-ttu-id="283b3-138">Ничего не toooverride на уровне документа hello, так как не определяет коллекцию hello hello DefaultTTL свойство, которое можно переопределить документа.</span><span class="sxs-lookup"><span data-stu-id="283b3-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="283b3-139">Срок ЖИЗНИ в документе без интерпретируемых системой hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="283b3-140">Документы в этой коллекции не устаревают.</span><span class="sxs-lookup"><span data-stu-id="283b3-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="283b3-141">никогда не истекал Hello документ с TTL = 1 в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="283b3-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="283b3-142">Все прочие документы устаревают по истечении n секунд.</span><span class="sxs-lookup"><span data-stu-id="283b3-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="283b3-143">Свойство TTL на уровне документа имеет значение n</span><span class="sxs-lookup"><span data-stu-id="283b3-143">TTL = n on document</span></span> |<span data-ttu-id="283b3-144">Ничего не toooverride на уровне документа hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="283b3-145">Срок ЖИЗНИ документа в ненадежных интерпретируемых системой hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="283b3-146">Hello документа с TTL = n истекает через n интервал, в секундах.</span><span class="sxs-lookup"><span data-stu-id="283b3-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="283b3-147">Другие документы наследуют значение интервала -1 и никогда не устаревают.</span><span class="sxs-lookup"><span data-stu-id="283b3-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="283b3-148">Hello документа с TTL = n истекает через n интервал, в секундах.</span><span class="sxs-lookup"><span data-stu-id="283b3-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="283b3-149">Другие документы унаследует интервал «n» из коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="283b3-150">Настройка TTL</span><span class="sxs-lookup"><span data-stu-id="283b3-150">Configuring TTL</span></span>
<span data-ttu-id="283b3-151">По умолчанию время toolive отключен по умолчанию во всех коллекциях Cosmos DB и на всех документах.</span><span class="sxs-lookup"><span data-stu-id="283b3-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="283b3-152">Активация TTL</span><span class="sxs-lookup"><span data-stu-id="283b3-152">Enabling TTL</span></span>
<span data-ttu-id="283b3-153">tooenable TTL в коллекцию или hello документы в коллекции необходимо tooset свойства DefaultTTL hello коллекции tooeither -1 или ненулевое положительное число.</span><span class="sxs-lookup"><span data-stu-id="283b3-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="283b3-154">Включение hello DefaultTTL слишком-1 означает, что по умолчанию все документы в коллекции hello будет располагаться навсегда, но hello Cosmos DB службы требуется отслеживать с помощью этой коллекции для документов, которые переопределить это поведение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="283b3-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="283b3-155">Настройка TTL по умолчанию на уровне коллекции</span><span class="sxs-lookup"><span data-stu-id="283b3-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="283b3-156">Предпринимается может tooconfigure toolive время по умолчанию на уровне коллекции.</span><span class="sxs-lookup"><span data-stu-id="283b3-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="283b3-157">tooset hello TTL с коллекцией, потребуется tooprovide ненулевое положительное число, указывающее период hello в секундах, tooexpire все документы в коллекции hello после hello последнего изменения отметок времени hello документа (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="283b3-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="283b3-158">Или можно задать hello по умолчанию слишком-1, что означает неограниченное время жизни вставлен в коллекцию toohello все документы по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="283b3-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="283b3-159">Настройка TTL на уровне документа</span><span class="sxs-lookup"><span data-stu-id="283b3-159">Setting TTL on a document</span></span>
<span data-ttu-id="283b3-160">В дополнение к этому toosetting TTL по умолчанию для коллекции можно задать срок ЖИЗНИ определенного на уровне документа.</span><span class="sxs-lookup"><span data-stu-id="283b3-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="283b3-161">Таким образом будут переопределены по умолчанию hello hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="283b3-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="283b3-162">tooset hello TTL в документе необходимо tooprovide ненулевое положительное число, которое указывает hello период, в секундах, tooexpire hello документа после hello последнего изменения отметок времени hello документа (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="283b3-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="283b3-163">Если документ не содержит TTL поля, затем hello по умолчанию hello коллекции будут применяться.</span><span class="sxs-lookup"><span data-stu-id="283b3-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="283b3-164">Если TTL отключен на уровне коллекции hello, поля TTL hello hello документе будут проигнорированы до TTL будет включена снова на коллекцию hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="283b3-165">Ниже приведен фрагмент с как tooset hello TTL истечение срока действия в документе.</span><span class="sxs-lookup"><span data-stu-id="283b3-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="283b3-166">Продление TTL для существующего документа</span><span class="sxs-lookup"><span data-stu-id="283b3-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="283b3-167">Вы можете сбросить hello TTL в документе, выполнив любая операция записи документа hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="283b3-168">Это позволит установить hello `_ts` toohello текущее время и toohello обратного отсчета hello документов окончания срока действия, задаваемое при помощи hello `ttl`, начнется снова.</span><span class="sxs-lookup"><span data-stu-id="283b3-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="283b3-169">Если вы хотите toochange hello `ttl` документа, как в случае с другим настраиваемым полям можно обновить поля hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="283b3-170">Удаление TTL из документа</span><span class="sxs-lookup"><span data-stu-id="283b3-170">Removing TTL from a document</span></span>
<span data-ttu-id="283b3-171">Если нет необходимости использовать этот документ tooexpire задал параметр TTL в документе, затем можно получить документ hello, удалите поле TTL hello и замените hello документа на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="283b3-172">Если поле TTL hello удаляется из документа hello, будет применяться по умолчанию hello hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="283b3-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="283b3-173">toostop документа истечение срока действия и наследует из коллекции hello, потребуется tooset hello TTL значение слишком-1.</span><span class="sxs-lookup"><span data-stu-id="283b3-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="283b3-174">Отключение TTL</span><span class="sxs-lookup"><span data-stu-id="283b3-174">Disabling TTL</span></span>
<span data-ttu-id="283b3-175">toodisable TTL полностью на коллекции и stop hello фоновой обработки взглянув на просроченные документы, которые следует удалить свойство DefaultTTL hello hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="283b3-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="283b3-176">При удалении этого свойства отличается от параметра он слишком-1.</span><span class="sxs-lookup"><span data-stu-id="283b3-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="283b3-177">Включение слишком-1 означает новые документы добавляются toohello коллекции будет располагаться навсегда, однако этот параметр можно переопределить на определенные документы из коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="283b3-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="283b3-178">Удаление это свойство из коллекции hello означает, что документов не истекает, даже если имеются документы, которые явно переопределены предыдущее значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="283b3-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="283b3-179">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="283b3-179">FAQ</span></span>
<span data-ttu-id="283b3-180">**Сколько стоит использование функции TTL?**</span><span class="sxs-lookup"><span data-stu-id="283b3-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="283b3-181">Нет без дополнительных затрат toosetting TTL в документе.</span><span class="sxs-lookup"><span data-stu-id="283b3-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="283b3-182">**Как долго займет toodelete документе после истечения срока ЖИЗНИ hello?**</span><span class="sxs-lookup"><span data-stu-id="283b3-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="283b3-183">документы Hello истечет сразу после приветствия TTL работает и не будут доступны через CRUD или API-интерфейсы запроса.</span><span class="sxs-lookup"><span data-stu-id="283b3-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="283b3-184">**Предусматривает ли использование функции TTL на уровне документа оплату за использование единиц запросов?**</span><span class="sxs-lookup"><span data-stu-id="283b3-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="283b3-185">Нет, удаление просроченных документов с помощью функции TTL в Cosmos DB не предусматривает оплату за использование единиц запросов.</span><span class="sxs-lookup"><span data-stu-id="283b3-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="283b3-186">**Функция TTL hello только применение tooentire документы или можно срок действия значения свойств отдельного документа.**</span><span class="sxs-lookup"><span data-stu-id="283b3-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="283b3-187">Срок ЖИЗНИ применяется toohello весь документ.</span><span class="sxs-lookup"><span data-stu-id="283b3-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="283b3-188">При желании tooexpire только часть документа, то рекомендуется извлечения из основного документа hello в отдельный документ «связанный» tooa часть hello и затем использовать TTL на извлеченный документ.</span><span class="sxs-lookup"><span data-stu-id="283b3-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="283b3-189">**Есть ли у функции hello TTL специальных требований индексирования?**</span><span class="sxs-lookup"><span data-stu-id="283b3-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="283b3-190">Да.</span><span class="sxs-lookup"><span data-stu-id="283b3-190">Yes.</span></span> <span data-ttu-id="283b3-191">Hello коллекции должно быть [индексирования набора политики](indexing-policies.md) tooeither Consistent и Lazy.</span><span class="sxs-lookup"><span data-stu-id="283b3-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="283b3-192">Попытка tooset DefaultTTL на коллекцию с индексированием tooNone набор приведет ошибку, как будет tooturn идет отключение индексирования для коллекции, которая имеет DefaultTTL уже задан.</span><span class="sxs-lookup"><span data-stu-id="283b3-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="283b3-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="283b3-193">Next steps</span></span>
<span data-ttu-id="283b3-194">toolearn Дополнительные сведения о базе данных Azure Cosmos, см. Служба toohello [ *документации* ](https://azure.microsoft.com/documentation/services/cosmos-db/) страницы.</span><span class="sxs-lookup"><span data-stu-id="283b3-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

