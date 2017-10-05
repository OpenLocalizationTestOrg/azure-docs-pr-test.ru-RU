---
title: "Завершение срока действия данных в Azure Cosmos DB с использованием срока жизни | Документация Майкрософт"
description: "Функция TTL в Microsoft Azure Cosmos DB позволяет автоматически удалять документы из системы по прошествии определенного периода времени."
services: cosmos-db
documentationcenter: 
keywords: "Срок жизни"
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
ms.openlocfilehash: 6f1c43ca0113dc7579b0fc3743d3314c16ce78a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-to-live"></a><span data-ttu-id="8dd5d-104">Автоматическое завершение срока действия данных в коллекциях Azure Cosmos DB с использованием срока жизни</span><span class="sxs-lookup"><span data-stu-id="8dd5d-104">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>
<span data-ttu-id="8dd5d-105">Приложения могут создавать и хранить большие объемы данных.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="8dd5d-106">Некоторые из этих данных, например созданные компьютером данные о событиях, журналы и пользовательские сеансы, имеют ценность только в течение ограниченного периода времени.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="8dd5d-107">Когда данных становится больше, чем нужно приложению, их можно безопасно удалять, чтобы снизить потребности приложения в ресурсах хранения.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="8dd5d-108">Свойство TTL (время жизни) в Microsoft Azure Cosmos DB позволяет автоматически удалять документы из базы данных по прошествии определенного периода времени.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="8dd5d-109">Время жизни можно указать на уровне коллекции, и тогда оно будет использоваться по умолчанию, либо отдельно переопределить для каждого документа.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="8dd5d-110">Когда свойство TTL определено (будь то время жизни по умолчанию на уровне коллекции или для конкретного документа), Cosmos DB автоматически удаляет документы, время жизни которых с момента их последнего изменения превышает заданное значение.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="8dd5d-111">Срок жизни в Cosmos DB отсчитывается в секундах от последнего изменения документа.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-111">Time to live in Cosmos DB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="8dd5d-112">Для этого используется поле `_ts`, которое существует в каждом документе.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-112">To do this it uses the `_ts` field which exists on every document.</span></span> <span data-ttu-id="8dd5d-113">В поле _ts отмечается дата и время в формате UNIX-времени.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="8dd5d-114">Поле `_ts` обновляется при каждом изменении документа.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="8dd5d-115">Поведение TTL</span><span class="sxs-lookup"><span data-stu-id="8dd5d-115">TTL behavior</span></span>
<span data-ttu-id="8dd5d-116">Функция TTL управляется свойствами TTL на двух уровнях — коллекции и документа.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="8dd5d-117">Значения задаются в секундах и отсчитываются от значения `_ts`, то есть от момента последнего изменения документа.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="8dd5d-118">DefaultTTL (TTL по умолчанию) на уровне коллекции:</span><span class="sxs-lookup"><span data-stu-id="8dd5d-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="8dd5d-119">Если свойство отсутствует (или имеет значение NULL), документы не удаляются автоматически.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="8dd5d-120">Если свойство присутствует и имеет значение –1, документы по умолчанию имеют неограниченный срок жизни.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-120">If present and the value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="8dd5d-121">Если свойство присутствует и его значением является некоторое число (n), документы удаляются по истечении n секунд после последнего изменения.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="8dd5d-122">TTL на уровне документов:</span><span class="sxs-lookup"><span data-stu-id="8dd5d-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="8dd5d-123">Свойство применяется только в том случае, если для родительской коллекции установлено значение DefaultTTL.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="8dd5d-124">Переопределяет значение DefaultTTL, установленное для родительской коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="8dd5d-125">Когда срок жизни документа истекает (`ttl` + `_ts` >= текущее время сервера), документ отмечается как устаревший.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span></span> <span data-ttu-id="8dd5d-126">После этого не допускаются никакие действия с этим документом, и он исключается из результатов любых запросов.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="8dd5d-127">Позднее документ физически удаляется из системы в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="8dd5d-128">Это действие не использует [единицы запроса](request-units.md) из бюджета коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span></span>

<span data-ttu-id="8dd5d-129">Описанную выше логику можно представить в виде следующей таблицы.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="8dd5d-130">Свойство DefaultTTL на уровне коллекции отсутствует или не определено</span><span class="sxs-lookup"><span data-stu-id="8dd5d-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="8dd5d-131">Свойство DefaultTTL на уровне коллекции имеет значение -1</span><span class="sxs-lookup"><span data-stu-id="8dd5d-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="8dd5d-132">Свойство DefaultTTL на уровне коллекции имеет значение n</span><span class="sxs-lookup"><span data-stu-id="8dd5d-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="8dd5d-133">Свойство TTL на уровне документа отсутствует</span><span class="sxs-lookup"><span data-stu-id="8dd5d-133">TTL Missing on document</span></span> |<span data-ttu-id="8dd5d-134">Переопределение на уровне документа не происходит, так как свойство TTL не применяется ни для коллекции, ни для документа.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="8dd5d-135">Документы в этой коллекции не устаревают.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="8dd5d-136">Документы в этой коллекции устаревают по истечении n секунд.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-136">The documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="8dd5d-137">Свойство TTL на уровне документа имеет значение -1</span><span class="sxs-lookup"><span data-stu-id="8dd5d-137">TTL = -1 on document</span></span> |<span data-ttu-id="8dd5d-138">Переопределение на уровне документа не происходит, так как для коллекции не определено свойство DefaultTTL.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="8dd5d-139">Система не учитывает свойство TTL, определенное для документа.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-139">TTL on a document is un-interpreted by the system.</span></span> |<span data-ttu-id="8dd5d-140">Документы в этой коллекции не устаревают.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="8dd5d-141">Документ с TTL=-1 в этой коллекции никогда не устаревает.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="8dd5d-142">Все прочие документы устаревают по истечении n секунд.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="8dd5d-143">Свойство TTL на уровне документа имеет значение n</span><span class="sxs-lookup"><span data-stu-id="8dd5d-143">TTL = n on document</span></span> |<span data-ttu-id="8dd5d-144">Переопределение на уровне документа не происходит.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-144">Nothing to override at the document level.</span></span> <span data-ttu-id="8dd5d-145">Система не учитывает свойство TTL, определенное для документа.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-145">TTL on a document in un-interpreted by the system.</span></span> |<span data-ttu-id="8dd5d-146">Документ с TTL=n устаревает через n секунд.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="8dd5d-147">Другие документы наследуют значение интервала -1 и никогда не устаревают.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="8dd5d-148">Документ с TTL=n устаревает через n секунд.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="8dd5d-149">Другие документы наследуют интервал n из коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-149">Other documents will inherit "n" interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="8dd5d-150">Настройка TTL</span><span class="sxs-lookup"><span data-stu-id="8dd5d-150">Configuring TTL</span></span>
<span data-ttu-id="8dd5d-151">По умолчанию срок жизни отключен для всех коллекций Cosmos DB и для всех документов.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="8dd5d-152">Активация TTL</span><span class="sxs-lookup"><span data-stu-id="8dd5d-152">Enabling TTL</span></span>
<span data-ttu-id="8dd5d-153">Чтобы включить TTL на уровне коллекции или документов, необходимо определить для коллекции свойство DefaultTTL и задать в качестве его значения ненулевое положительное число или -1.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="8dd5d-154">Значение DefaultTTL, равное –1, означает, что по умолчанию все документы будут сохраняться в коллекции в течение неограниченного времени, но служба Cosmos DB будет отслеживать наличие в этой коллекции документов, для которых значение по умолчанию переопределено.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="8dd5d-155">Настройка TTL по умолчанию на уровне коллекции</span><span class="sxs-lookup"><span data-stu-id="8dd5d-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="8dd5d-156">Вы можете настроить срок жизни по умолчанию для коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-156">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="8dd5d-157">Для этого необходимо ввести ненулевое положительное число, которое будет означать время в секундах, по истечении которого с момента последнего изменения документа (отметка времени `_ts`) любой документ в этой коллекции будет считаться устаревшим.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="8dd5d-158">Также можно задать значение по умолчанию -1, что будет означать неограниченное время жизни по умолчанию для всех документов в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="8dd5d-159">Настройка TTL на уровне документа</span><span class="sxs-lookup"><span data-stu-id="8dd5d-159">Setting TTL on a document</span></span>
<span data-ttu-id="8dd5d-160">Помимо значения TTL по умолчанию для коллекции, вы можете задать значение TTL на уровне документа.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="8dd5d-161">Это значение переопределит значение по умолчанию, установленное для коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-161">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="8dd5d-162">Чтобы задать TTL для коллекции, необходимо ввести ненулевое положительное число, которое будет означать время в секундах, по истечении которого с момента последнего изменения документа (отметка времени `_ts`) этот документ будет считаться устаревшим.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="8dd5d-163">Если в документе нет поля TTL, для коллекции будет применяться значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-163">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="8dd5d-164">Если свойство TTL отключено на уровне коллекции, поле TTL в документе будет игнорироваться, пока свойство TTL не будет включено для этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="8dd5d-165">Во фрагменте кода ниже показано, как задать срок жизни в документе.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-165">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

    // Include a property that serializes to "ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used to set expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set the value to the expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="8dd5d-166">Продление TTL для существующего документа</span><span class="sxs-lookup"><span data-stu-id="8dd5d-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="8dd5d-167">Отсчет периода TTL для документа можно сбросить, выполнив для него любую операцию записи.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-167">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="8dd5d-168">При этом в поле `_ts` будет записано текущее время, и отсчет устаревания документа, определенный свойством `ttl`, начнется заново.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="8dd5d-169">Если вы хотите изменить срок жизни (`ttl`) на уровне документа, вы можете обновить поле TTL, как и любое другое редактируемое поле.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="8dd5d-170">Удаление TTL из документа</span><span class="sxs-lookup"><span data-stu-id="8dd5d-170">Removing TTL from a document</span></span>
<span data-ttu-id="8dd5d-171">Если для документа определено свойство TTL, но необходимость в устаревании документа отпала, вы можете извлечь этот документ, удалить поле TTL и сохранить документ на сервере.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="8dd5d-172">Когда поле TTL удаляется из документа, для него применяется значение по умолчанию, установленное для коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-172">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="8dd5d-173">Чтобы документ не устаревал и к нему не применялось значение TTL для коллекции, следует установить значение TTL, равное -1.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="8dd5d-174">Отключение TTL</span><span class="sxs-lookup"><span data-stu-id="8dd5d-174">Disabling TTL</span></span>
<span data-ttu-id="8dd5d-175">Чтобы полностью отключить функцию TTL для коллекции и остановить фоновый поиск устаревших документов, следует удалить свойство DefaultTTL из коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="8dd5d-176">Удаление этого свойства и выбор значения -1 имеют разный эффект.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-176">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="8dd5d-177">Выбор значения -1 означает, что новые документы, добавляемые в коллекцию, будут сохраняться в течение неограниченного времени, но это поведение можно переопределить для конкретных документов в коллекции.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="8dd5d-178">Удаление свойства из коллекции означает, что документы не будут устаревать, даже если для них значение по умолчанию было ранее переопределено.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="8dd5d-179">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="8dd5d-179">FAQ</span></span>
<span data-ttu-id="8dd5d-180">**Сколько стоит использование функции TTL?**</span><span class="sxs-lookup"><span data-stu-id="8dd5d-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="8dd5d-181">Использование TTL на уровне документа не влечет никаких дополнительных затрат.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-181">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="8dd5d-182">**Сколько времени займет удаление документа после истечения срока жизни?**</span><span class="sxs-lookup"><span data-stu-id="8dd5d-182">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="8dd5d-183">Срок действия документов истекает сразу после истечения срока жизни (TTL); они будут недоступны для операций CRUD или интерфейсов API запросов.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="8dd5d-184">**Предусматривает ли использование функции TTL на уровне документа оплату за использование единиц запросов?**</span><span class="sxs-lookup"><span data-stu-id="8dd5d-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="8dd5d-185">Нет, удаление просроченных документов с помощью функции TTL в Cosmos DB не предусматривает оплату за использование единиц запросов.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="8dd5d-186">**Функция TTL применяется только к всему документу, или я могу установить срок жизни для отдельных свойств документа?**</span><span class="sxs-lookup"><span data-stu-id="8dd5d-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="8dd5d-187">TTL применяется ко всему документу.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-187">TTL applies to the entire document.</span></span> <span data-ttu-id="8dd5d-188">Если вы хотите, чтобы устаревала только часть документа, мы рекомендуем извлекать эту часть из основного документа в отдельный связанный документ, для которого и применять TTL.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="8dd5d-189">**Есть ли особые требования к индексированию при использовании функции TTL?**</span><span class="sxs-lookup"><span data-stu-id="8dd5d-189">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="8dd5d-190">Да.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-190">Yes.</span></span> <span data-ttu-id="8dd5d-191">Для коллекции должна быть [задана политика индексирования](indexing-policies.md) — Consistent (Согласованная) или Lazy (Асинхронная).</span><span class="sxs-lookup"><span data-stu-id="8dd5d-191">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="8dd5d-192">Попытка определить DefaultTTL на уровне коллекции с политикой индексирования None приведет к ошибке. Также ошибкой завершится попытка отключить индексирование коллекции, для которой уже задано свойство DefaultTTL.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dd5d-193">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8dd5d-193">Next steps</span></span>
<span data-ttu-id="8dd5d-194">Дополнительные сведения об Azure Cosmos DB см. на странице [*документации*](https://azure.microsoft.com/documentation/services/cosmos-db/) по этой службе.</span><span class="sxs-lookup"><span data-stu-id="8dd5d-194">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

