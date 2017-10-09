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
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>Срок действия данных в коллекциях Azure Cosmos DB автоматически с временем toolive
Приложения могут создавать и хранить большие объемы данных. Некоторые из этих данных, например созданные компьютером данные о событиях, журналы и пользовательские сеансы, имеют ценность только в течение ограниченного периода времени. После hello данные становятся избыточные toohello потребностями приложения hello он безопасном toopurge эти данные и уменьшить hello потребностям приложения.

«Время toolive» или истечения срока ЖИЗНИ Microsoft Azure Cosmos DB предоставляет hello возможность toohave документы автоматически удаляются из базы данных hello после определенного периода времени. время по умолчанию Hello toolive можно задавать на уровне коллекции hello и переопределен в на уровне документа. Когда свойство TTL определено (будь то время жизни по умолчанию на уровне коллекции или для конкретного документа), Cosmos DB автоматически удаляет документы, время жизни которых с момента их последнего изменения превышает заданное значение.

Время toolive в Cosmos DB использует смещение от последнего изменения документа hello. toodo этого оно использует hello `_ts` поля, которое существует в каждом документе. поле _ts Hello является стиле unix эпохи timestamp представляющих hello даты и времени. Hello `_ts` поле обновляется каждый раз при изменении документа. 

## <a name="ttl-behavior"></a>Поведение TTL
функция TTL Hello управляется свойства TTL на двух уровнях — уровне коллекции hello и hello документа. Hello значения задаются в секундах и обрабатываются как разностный из hello `_ts` документ hello было изменено на.

1. DefaultTTL для коллекции hello
   
   * Если отсутствует (или набор toonull), документы не удаляются автоматически.
   * При наличии и hello значение равно «-1» = неограниченное — документы не ограничивать срок действия по умолчанию
   * Если присутствует и hello имеет некоторое значение («n») — документов истекает «n» секунд после последнего изменения
2. Срок ЖИЗНИ для hello документов: 
   
   * Свойство применимо только в том случае, если DefaultTTL отсутствует коллекция родительских hello.
   * Переопределяет значение DefaultTTL hello для hello родительской коллекции.

Как только hello документа истек (`ttl`  +  `_ts` > = текущее время сервера), hello документ помечается как «устаревшая». Операция не будет разрешен в этих документах после этой даты, и они будут исключены из результатов hello запросы, выполняемые. документы Hello физически удаляются в системе hello и будут удалены в фоновом режиме hello возможности на более позднее время. Это не использовать любой [единиц запроса (RUs)](request-units.md) из коллекции бюджета hello.

Hello выше логику могут отображаться следующие матрицы hello:

|  | DefaultTTL отсутствует или не включен hello коллекции | Свойство DefaultTTL на уровне коллекции имеет значение -1 | Свойство DefaultTTL на уровне коллекции имеет значение n |
| --- |:--- |:--- |:--- |
| Свойство TTL на уровне документа отсутствует |Ничего не toooverride на уровне документа, так как документ hello и коллекции не имеют концепции TTL. |Документы в этой коллекции не устаревают. |по истечении интервала n, истекает Hello документы в этой коллекции. |
| Свойство TTL на уровне документа имеет значение -1 |Ничего не toooverride на уровне документа hello, так как не определяет коллекцию hello hello DefaultTTL свойство, которое можно переопределить документа. Срок ЖИЗНИ в документе без интерпретируемых системой hello. |Документы в этой коллекции не устаревают. |никогда не истекал Hello документ с TTL = 1 в этой коллекции. Все прочие документы устаревают по истечении n секунд. |
| Свойство TTL на уровне документа имеет значение n |Ничего не toooverride на уровне документа hello. Срок ЖИЗНИ документа в ненадежных интерпретируемых системой hello. |Hello документа с TTL = n истекает через n интервал, в секундах. Другие документы наследуют значение интервала -1 и никогда не устаревают. |Hello документа с TTL = n истекает через n интервал, в секундах. Другие документы унаследует интервал «n» из коллекции hello. |

## <a name="configuring-ttl"></a>Настройка TTL
По умолчанию время toolive отключен по умолчанию во всех коллекциях Cosmos DB и на всех документах.

## <a name="enabling-ttl"></a>Активация TTL
tooenable TTL в коллекцию или hello документы в коллекции необходимо tooset свойства DefaultTTL hello коллекции tooeither -1 или ненулевое положительное число. Включение hello DefaultTTL слишком-1 означает, что по умолчанию все документы в коллекции hello будет располагаться навсегда, но hello Cosmos DB службы требуется отслеживать с помощью этой коллекции для документов, которые переопределить это поведение по умолчанию.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>Настройка TTL по умолчанию на уровне коллекции
Предпринимается может tooconfigure toolive время по умолчанию на уровне коллекции. tooset hello TTL с коллекцией, потребуется tooprovide ненулевое положительное число, указывающее период hello в секундах, tooexpire все документы в коллекции hello после hello последнего изменения отметок времени hello документа (`_ts`). Или можно задать hello по умолчанию слишком-1, что означает неограниченное время жизни вставлен в коллекцию toohello все документы по умолчанию.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>Настройка TTL на уровне документа
В дополнение к этому toosetting TTL по умолчанию для коллекции можно задать срок ЖИЗНИ определенного на уровне документа. Таким образом будут переопределены по умолчанию hello hello коллекции.

* tooset hello TTL в документе необходимо tooprovide ненулевое положительное число, которое указывает hello период, в секундах, tooexpire hello документа после hello последнего изменения отметок времени hello документа (`_ts`).
* Если документ не содержит TTL поля, затем hello по умолчанию hello коллекции будут применяться.
* Если TTL отключен на уровне коллекции hello, поля TTL hello hello документе будут проигнорированы до TTL будет включена снова на коллекцию hello.

Ниже приведен фрагмент с как tooset hello TTL истечение срока действия в документе.

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


## <a name="extending-ttl-on-an-existing-document"></a>Продление TTL для существующего документа
Вы можете сбросить hello TTL в документе, выполнив любая операция записи документа hello. Это позволит установить hello `_ts` toohello текущее время и toohello обратного отсчета hello документов окончания срока действия, задаваемое при помощи hello `ttl`, начнется снова. Если вы хотите toochange hello `ttl` документа, как в случае с другим настраиваемым полям можно обновить поля hello.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>Удаление TTL из документа
Если нет необходимости использовать этот документ tooexpire задал параметр TTL в документе, затем можно получить документ hello, удалите поле TTL hello и замените hello документа на сервере hello. Если поле TTL hello удаляется из документа hello, будет применяться по умолчанию hello hello коллекции. toostop документа истечение срока действия и наследует из коллекции hello, потребуется tooset hello TTL значение слишком-1.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>Отключение TTL
toodisable TTL полностью на коллекции и stop hello фоновой обработки взглянув на просроченные документы, которые следует удалить свойство DefaultTTL hello hello коллекции. При удалении этого свойства отличается от параметра он слишком-1. Включение слишком-1 означает новые документы добавляются toohello коллекции будет располагаться навсегда, однако этот параметр можно переопределить на определенные документы из коллекции hello. Удаление это свойство из коллекции hello означает, что документов не истекает, даже если имеются документы, которые явно переопределены предыдущее значение по умолчанию.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>Часто задаваемые вопросы
**Сколько стоит использование функции TTL?**

Нет без дополнительных затрат toosetting TTL в документе.

**Как долго займет toodelete документе после истечения срока ЖИЗНИ hello?**

документы Hello истечет сразу после приветствия TTL работает и не будут доступны через CRUD или API-интерфейсы запроса. 

**Предусматривает ли использование функции TTL на уровне документа оплату за использование единиц запросов?**

Нет, удаление просроченных документов с помощью функции TTL в Cosmos DB не предусматривает оплату за использование единиц запросов.

**Функция TTL hello только применение tooentire документы или можно срок действия значения свойств отдельного документа.**

Срок ЖИЗНИ применяется toohello весь документ. При желании tooexpire только часть документа, то рекомендуется извлечения из основного документа hello в отдельный документ «связанный» tooa часть hello и затем использовать TTL на извлеченный документ.

**Есть ли у функции hello TTL специальных требований индексирования?**

Да. Hello коллекции должно быть [индексирования набора политики](indexing-policies.md) tooeither Consistent и Lazy. Попытка tooset DefaultTTL на коллекцию с индексированием tooNone набор приведет ошибку, как будет tooturn идет отключение индексирования для коллекции, которая имеет DefaultTTL уже задан.

## <a name="next-steps"></a>Дальнейшие действия
toolearn Дополнительные сведения о базе данных Azure Cosmos, см. Служба toohello [ *документации* ](https://azure.microsoft.com/documentation/services/cosmos-db/) страницы.

