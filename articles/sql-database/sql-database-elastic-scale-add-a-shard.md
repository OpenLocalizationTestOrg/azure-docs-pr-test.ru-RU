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
# <a name="adding-a-shard-using-elastic-database-tools"></a>Добавление сегмента с использованием средств эластичных баз данных
## <a name="tooadd-a-shard-for-a-new-range-or-key"></a>tooadd сегментов для нового диапазона или ключа
Приложениям часто требуется toosimply добавить новые данные toohandle сегментов, который ожидается от новых ключей или диапазонов ключей для карты сегментов, которая уже существует. Например приложение сегментированных по ИД клиента может потребоваться tooprovision новый сегмент для нового клиента или ежемесячно сегментированных данных может потребоваться новый сегмент подготовить перед запуском hello каждого нового месяца. 

Если hello новый диапазон значений ключа уже не является частью существующего сопоставления, это очень простой tooadd hello новых сегментов и связывание hello новый ключ или диапазон toothat сегмент. 

### <a name="example--adding-a-shard-and-its-range-tooan-existing-shard-map"></a>Пример: Добавление сегмент и его сопоставление диапазона tooan существующих сегментов
В этом образце используется hello [TryGetShard](https://msdn.microsoft.com/library/azure/dn823929.aspx) hello [CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx), [CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn807221.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeShardMap`1.CreateRangeMapping\(Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.RangeMappingCreationInfo{`0}\)) методов и создает экземпляр hello [ShardLocation](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardlocation.shardlocation.aspx#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardLocation.) класса. В образце hello ниже базы данных с именем **sample_shard_2** и все необходимые объекты внутри объекта были созданы toohold диапазона [300, 400).  

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


В качестве альтернативы можно использовать Powershell toocreate нового диспетчера карты сегментов. Пример представлен [здесь](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="tooadd-a-shard-for-an-empty-part-of-an-existing-range"></a>tooadd сегментов для пустую часть существующего диапазона
В некоторых случаях уже сопоставлено с сегментом tooa диапазона и частично заполненный его данными, но теперь хотите предстоящих данных toobe направленной tooa другой сегмент. Например, вы сегментов по дням в диапазоне и выделен сегментов tooa 50 дней, но день 24 tooland будущие данные в другой сегмент. Hello эластичной базы данных [средством слияния разбиение](sql-database-elastic-scale-overview-split-and-merge.md) могут выполнять эту операцию, но если перемещение данных не является обязательной (например, данные для диапазона hello дни [25, 50), т. е., too50 включительно день 25 исчерпывающим, еще не существует) можно выполнить полностью использование hello непосредственно API-интерфейсы управления карты сегментов.

### <a name="example-splitting-a-range-and-assigning-hello-empty-portion-tooa-newly-added-shard"></a>Пример: разбиение диапазона и назначение hello пустые часть tooa новых сегментов
В рамках примера были созданы база данных с именем sample_shard_2 и все необходимые объекты схемы, содержащиеся в ней.  

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

**Важные**: этот метод следует использовать только при наличии определенных, hello диапазона для hello обновить сопоставление является пустым.  выше методов Hello не проверять данные для перемещения диапазона hello, поэтому лучше tooinclude проверяет в коде.  Если существуют строки в диапазоне hello перемещения, распространения hello фактические данные не будут соответствовать карты обновленного сегментов hello. Используйте hello [средством слияния разбиение](sql-database-elastic-scale-overview-split-and-merge.md) tooperform hello операции вместо этого в таких случаях.  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

