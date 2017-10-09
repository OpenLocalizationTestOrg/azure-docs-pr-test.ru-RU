---
title: "aaaAdding a сегментов с помощью средств эластичной базы данных | Документы Microsoft"
description: "Как задать toouse API динамического масштабирования tooadd новых сегментов tooa сегментов."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 62a349db-bebe-406f-a120-2f1986f2b286
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f44b59578376d1238b3012a3cb52339978079f0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-shard-using-elastic-database-tools"></a><span data-ttu-id="31e39-103">Добавление сегмента с использованием средств эластичных баз данных</span><span class="sxs-lookup"><span data-stu-id="31e39-103">Adding a shard using Elastic Database tools</span></span>
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a><span data-ttu-id="31e39-104">tooadd сегментов для нового диапазона или ключа</span><span class="sxs-lookup"><span data-stu-id="31e39-104">tooadd a shard for a new range or key</span></span>
<span data-ttu-id="31e39-105">Приложениям часто требуется toosimply добавить новые данные toohandle сегментов, который ожидается от новых ключей или диапазонов ключей для карты сегментов, которая уже существует.</span><span class="sxs-lookup"><span data-stu-id="31e39-105">Applications often need toosimply add new shards toohandle data that is expected from new keys or key ranges, for a shard map that already exists.</span></span> <span data-ttu-id="31e39-106">Например приложение сегментированных по ИД клиента может потребоваться tooprovision новый сегмент для нового клиента или ежемесячно сегментированных данных может потребоваться новый сегмент подготовить перед запуском hello каждого нового месяца.</span><span class="sxs-lookup"><span data-stu-id="31e39-106">For example, an application sharded by Tenant ID may need tooprovision a new shard for a new tenant, or data sharded monthly may need a new shard provisioned before hello start of each new month.</span></span> 

<span data-ttu-id="31e39-107">Если hello новый диапазон значений ключа уже не является частью существующего сопоставления, это очень простой tooadd hello новых сегментов и связывание hello новый ключ или диапазон toothat сегмент.</span><span class="sxs-lookup"><span data-stu-id="31e39-107">If hello new range of key values is not already part of an existing mapping, it is very simple tooadd hello new shard and associate hello new key or range toothat shard.</span></span> 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a><span data-ttu-id="31e39-108">Пример: Добавление сегмент и его сопоставление диапазона tooan существующих сегментов</span><span class="sxs-lookup"><span data-stu-id="31e39-108">Example:  adding a shard and its range tooan existing shard map</span></span>
<span data-ttu-id="31e39-109">В этом образце используется hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) методов и создает экземпляр hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) класса.</span><span class="sxs-lookup"><span data-stu-id="31e39-109">This sample uses hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) methods, and creates an instance of hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) class.</span></span> <span data-ttu-id="31e39-110">В образце hello ниже базы данных с именем **sample_shard_2** и все необходимые объекты внутри объекта были созданы toohold диапазона [300, 400).</span><span class="sxs-lookup"><span data-stu-id="31e39-110">In hello sample below, a database named **sample_shard_2** and all necessary schema objects inside of it have been created toohold range [300, 400).</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range being added. 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 
        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Create hello mapping and associate it with hello new shard 
    sm.CreateRangeMapping(new RangeMappingCreationInfo<long> 
                            (new Range<long>(300, 400), shard2, MappingStatus.Online)); 


<span data-ttu-id="31e39-111">В качестве альтернативы можно использовать Powershell toocreate нового диспетчера карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="31e39-111">As an alternative, you can use Powershell toocreate a new Shard Map Manager.</span></span> <span data-ttu-id="31e39-112">Пример представлен [здесь](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span><span class="sxs-lookup"><span data-stu-id="31e39-112">An example is available [here](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).</span></span>

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a><span data-ttu-id="31e39-113">tooadd сегментов для пустую часть существующего диапазона</span><span class="sxs-lookup"><span data-stu-id="31e39-113">tooadd a shard for an empty part of an existing range</span></span>
<span data-ttu-id="31e39-114">В некоторых случаях уже сопоставлено с сегментом tooa диапазона и частично заполненный его данными, но теперь хотите предстоящих данных toobe направленной tooa другой сегмент.</span><span class="sxs-lookup"><span data-stu-id="31e39-114">In some circumstances, you may have already mapped a range tooa shard and partially filled it with data, but you now want upcoming data toobe directed tooa different shard.</span></span> <span data-ttu-id="31e39-115">Например, вы сегментов по дням в диапазоне и выделен сегментов tooa 50 дней, но день 24 tooland будущие данные в другой сегмент.</span><span class="sxs-lookup"><span data-stu-id="31e39-115">For example, you shard by day range and have already allocated 50 days tooa shard, but on day 24, you want future data tooland in a different shard.</span></span> <span data-ttu-id="31e39-116">Hello эластичной базы данных [средством слияния разбиение](sql-database-elastic-scale-overview-split-and-merge.md) могут выполнять эту операцию, но если перемещение данных не является обязательной (например, данные для диапазона hello дни [25, 50), т. е., too50 включительно день 25 исчерпывающим, еще не существует) можно выполнить полностью использование hello непосредственно API-интерфейсы управления карты сегментов.</span><span class="sxs-lookup"><span data-stu-id="31e39-116">hello elastic database [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) can perform this operation, but if data movement is not necessary (for example, data for hello range of days [25, 50), i.e., day 25 inclusive too50 exclusive, does not yet exist) you can perform this entirely using hello Shard Map Management APIs directly.</span></span>

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a><span data-ttu-id="31e39-117">Пример: разбиение диапазона и назначение hello пустые часть tooa новых сегментов</span><span class="sxs-lookup"><span data-stu-id="31e39-117">Example: splitting a range and assigning hello empty portion tooa newly-added shard</span></span>
<span data-ttu-id="31e39-118">В рамках примера были созданы база данных с именем sample_shard_2 и все необходимые объекты схемы, содержащиеся в ней.</span><span class="sxs-lookup"><span data-stu-id="31e39-118">A database named “sample_shard_2” and all necessary schema objects inside of it have been created.</span></span>  

    // sm is a RangeShardMap object.
    // Add a new shard toohold hello range we will move 
    Shard shard2 = null; 

    if (!sm.TryGetShard(new ShardLocation(shardServer, "sample_shard_2"),out shard2)) 
    { 

        shard2 = sm.CreateShard(new ShardLocation(shardServer, "sample_shard_2"));  
    } 

    // Split hello Range holding Key 25 

    sm.SplitMapping(sm.GetMappingForKey(25), 25); 

    // Map new range holding [25-50) toodifferent shard: 
    // first take existing mapping offline 
    sm.MarkMappingOffline(sm.GetMappingForKey(25)); 
    // now map while offline tooa different shard and take online 
    RangeMappingUpdate upd = new RangeMappingUpdate(); 
    upd.Shard = shard2; 
    sm.MarkMappingOnline(sm.UpdateMapping(sm.GetMappingForKey(25), upd)); 

<span data-ttu-id="31e39-119">**Важные**: этот метод следует использовать только при наличии определенных, hello диапазона для hello обновить сопоставление является пустым.</span><span class="sxs-lookup"><span data-stu-id="31e39-119">**Important**:  Use this technique only if you are certain that hello range for hello updated mapping is empty.</span></span>  <span data-ttu-id="31e39-120">выше методов Hello не проверять данные для перемещения диапазона hello, поэтому лучше tooinclude проверяет в коде.</span><span class="sxs-lookup"><span data-stu-id="31e39-120">hello methods above do not check data for hello range being moved, so it is best tooinclude checks in your code.</span></span>  <span data-ttu-id="31e39-121">Если существуют строки в диапазоне hello перемещения, распространения hello фактические данные не будут соответствовать карты обновленного сегментов hello.</span><span class="sxs-lookup"><span data-stu-id="31e39-121">If rows exist in hello range being moved, hello actual data distribution will not match hello updated shard map.</span></span> <span data-ttu-id="31e39-122">Используйте hello [средством слияния разбиение](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello операции вместо этого в таких случаях.</span><span class="sxs-lookup"><span data-stu-id="31e39-122">Use hello [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello operation instead in these cases.</span></span>  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

