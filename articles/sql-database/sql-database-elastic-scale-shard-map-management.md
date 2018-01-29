---
title: "Развертывание базы данных SQL Azure | Документация Майкрософт"
description: "Использование ShardMapManager, клиентской библиотеки гибких базы данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: On Demand
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2017
ms.author: ddove
ms.openlocfilehash: fe4c8b7b2a9d199c85faf11fcd35382d586fc009
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/08/2017
---
# <a name="scale-out-databases-with-the-shard-map-manager"></a>Развертывание баз данных с использованием диспетчера карты сегментов
Используйте диспетчер карты сегментов, чтобы легко развертывать базы данных в SQL Azure. Диспетчер карты сегментов — это специальная база данных, которая хранит глобальную информацию о сопоставлении всех сегментов (баз данных), входящих в набор сегментов. Метаданные позволяют приложению подключаться к нужной базе данных, которая определяется по значению **ключа сегментирования**. Кроме того, каждый сегмент в наборе содержит карты, отслеживающие локальные сегменты данных ( **шардлеты**). 

![Управление размещением сегментов](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Для управления картами сегментов важно понимать их структуру. Для этого используется класс ShardMapManager ([Java](https://docs.microsoft.com/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)), входящий в [клиентскую библиотеку эластичной базы данных](sql-database-elastic-database-client-library.md). Он позволяет управлять картами сегментов.  

## <a name="shard-maps-and-shard-mappings"></a>Карты сегментов и сопоставление сегментов
Для каждого сегмента следует выбрать тип создаваемой карты сегментов. Этот выбор зависит от архитектуры базы данных. 

1. По одному клиенту для каждой базы данных.  
2. Несколько клиентов на одну базу данных (два типа):
   1. Сопоставление по спискам
   2. Сопоставление по диапазонам

Для модели с одним клиентом создайте карту сегментов с **сопоставлением по списку** . В модели с одним клиентом каждому клиенту назначается по одной базе данных. Эта модель подходит для разработчиков SaaS, так как она упрощает управление.

![Сопоставление по спискам][1]

В модели базы данных с несколькими клиентами для одной базы данных назначается несколько клиентов (а группы клиентов можно распределять по нескольким базам данных). Эту модель можно использовать, когда у каждого отдельного клиента низкие потребности в обработке данных. В этой модели клиенты соотносятся с базой данных с использованием **сопоставления по диапазонам**. 

![Сопоставление по диапазонам][2]

Вы можете также реализовать модель с несколькими клиентами с помощью *сопоставления по списку* , в котором одной базе данных соответствует несколько клиентов. Например, база данных DB1 используется для хранения информации о клиенте 1 и 5, а DB2 хранит данные о клиенте 7 и 10. 

![Несколько клиентов для отдельной базы данных][3] 

### <a name="supported-types-for-sharding-keys"></a>Поддерживаемые типы для ключей сегментирования
Эластичное масштабирование поддерживает такие типы ключей сегментирования:

| .NET | Java |
| --- | --- |
| целое число |целое число |
| длинное целое число |длинное целое число |
| GUID |uuid |
| byte[]  |byte[] |
| Datetime | timestamp |
| Интервал времени | длительность|
| datetimeoffset; |offsetdatetime |

### <a name="list-and-range-shard-maps"></a>Списочные и диапазонные карты сегментов
Карты сегментов могут быть созданы с использованием **списков индивидуальных величин сегментных ключей** или с использованием **диапазонов величин сегментных ключей**. 

### <a name="list-shard-maps"></a>Списочные карты сегментов
**Сегменты** содержат **шардлеты**, и сопоставление шардлетов сегментам производится с помощью карты сегментов. **Списочная карта сегментов** представляет ассоциацию между отдельными значениями ключа, определяющими шардлеты, и базами данных, обслуживающими сегменты.  **Сопоставления по списку** — это явные и разные значения ключей, которые могут сопоставляться с одной базой данных. Например, ключ 1 соответствует базе данных A, а значения ключей 3 и 6 ссылаются на базу данных B.

| Ключ | Расположение сегмента |
| --- | --- |
| 1 |БазаДанных_А |
| 3 |БазаДанных_Б |
| 4. |БазаДанных_В |
| 6 |БазаДанных_Б |
| ... |... |

### <a name="range-shard-maps"></a>Диапазонные карты сегментов
В **картах сегментов по диапазонам** диапазон ключей описывается парой **[нижнее значение, верхнее значение)**, где *нижнее значение* — минимальный ключ в диапазоне, а *верхнее значение* — первое значение, превышающее диапазон. 

Например **[0, 100)** включает все целые числа, которые больше или равны 0 и меньше 100. Обратите внимание, что несколько диапазонов могут указывать на одну и ту же базу данных, а также поддерживаются перекрытия диапазонов (например, в текущем примере оба диапазона [100,200) и [400,600) указывают на базы данных C).

| Ключ | Расположение сегмента |
| --- | --- |
| [1,50) |БазаДанных_А |
| [50,100) |БазаДанных_Б |
| [100,200) |БазаДанных_В |
| [400,600) |БазаДанных_В |
| ... |... |

Каждая из приведенных выше таблиц является концептуальным примером объекта **ShardMap** . Каждая строка представляет упрощенный пример отдельного **PointMapping** (для карты списка сегментов) или **RangeMapping** (для карты диапазона сегментов) объекта.

## <a name="shard-map-manager"></a>Диспетчер карты сегментов
В клиентской библиотеке диспетчер карты сегментов — это набор карт сегментов. Данные, контролируемые объектом **ShardMapManager** , хранятся в трех местах. 

1. **Глобальная карта сегментов (GSM)**: вы указываете базу данных для хранения всех карт сегментов и сопоставлений. Для управления этой информацией автоматически создаются специальные таблицы и хранимые процедуры. Обычно это база данных небольшая и с простым доступом, и её не рекомендуется использовать для других прикладных задач. Таблицы расположены в специальной схеме с именем **__ShardManagement**. 
2. **Локальная карта сегментов (LSM)**: в каждую указанную вами в качестве сегмента базу данных будут добавлены несколько небольших таблиц и специальных хранимых процедур, которые содержат информацию о карте сегментов, относящуюся к этому сегменту, и управляют этой информацией. Эта информация является избыточной для информации, размещенной в глобальной карте сегментов, и позволяет приложению проверять кэшированные данные карты сегментов без нагрузки на глобальную карту сегментов; при помощи локальной карты сегментов приложение проверяет правильность кэшированного сопоставления. Таблицы, соответствующие локальной карте сегментов в каждом сегменте, также находятся в схеме **__ShardManagement**.
3. **Кэш приложения**: каждый экземпляр приложения, у которого есть доступ к объекту **ShardMapManager**, поддерживает локальный кэш своих сопоставлений в памяти. Хранятся использованные за последнее время сведения о маршрутизации. 

## <a name="constructing-a-shardmapmanager"></a>Создание объекта ShardMapManager
Объект **ShardMapManager** создается с помощью шаблона фабрики ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager_factory), [.NET](/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory)). Метод **ShardMapManagerFactory.GetSqlShardMapManager** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager_factory.getsqlshardmapmanager), [.NET](/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager)) принимает учетные данные (включая имя сервера и имя базы данных, содержащей глобальную карту сегментов) в формате **ConnectionString** и возвращает экземпляр объекта **ShardMapManager**.  

**Обратите внимание:** экземпляр **ShardMapManager** должен создаваться только один раз для каждого домена приложения в коде инициализации приложения. Создание дополнительных экземпляров ShardMapManager в том же домене приложения приводит к повышенному потреблению ресурсов памяти и ЦП приложением. **ShardMapManager** может содержать любое число карт сегментов. Многим приложениям достаточно одной карты сегментов, но в некоторых случаях применяются разные наборы баз данных, которые используются в разных схемах или имеют уникальное назначение. В таком случае желательно использовать несколько карт сегментов. 

В этом коде приложение пытается открыть существующий экземпляр **ShardMapManager** с помощью метода TryGetSqlShardMapManager ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager_factory.trygetsqlshardmapmanager), [.NET](/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)).  Если объекты, представляющие экземпляр **ShardMapManager** (GSM), еще не существуют в базе данных, клиентская библиотека создаст их с помощью метода CreateSqlShardMapManager ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager_factory.createsqlshardmapmanager), [.NET](/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager)).

```Java
// Try to get a reference to the Shard Map Manager in the shardMapManager database.
// If it doesn't already exist, then create it.
ShardMapManager shardMapManager = null;
boolean shardMapManagerExists = ShardMapManagerFactory.tryGetSqlShardMapManager(shardMapManagerConnectionString,ShardMapManagerLoadPolicy.Lazy, refShardMapManager);
shardMapManager = refShardMapManager.argValue;

if (shardMapManagerExists) {
    ConsoleUtils.writeInfo("Shard Map %s already exists", shardMapManager);
}
else {
    // The Shard Map Manager does not exist, so create it
    shardMapManager = ShardMapManagerFactory.createSqlShardMapManager(shardMapManagerConnectionString);
    ConsoleUtils.writeInfo("Created Shard Map %s", shardMapManager);
}
```

```csharp
// Try to get a reference to the Shard Map Manager via the Shard Map Manager database.  
// If it doesn't already exist, then create it. 
ShardMapManager shardMapManager; 
bool shardMapManagerExists = ShardMapManagerFactory.TryGetSqlShardMapManager(
                                        connectionString, 
                                        ShardMapManagerLoadPolicy.Lazy, 
                                        out shardMapManager); 

if (shardMapManagerExists) 
{ 
    Console.WriteLine("Shard Map Manager already exists");
} 
else
{
    // Create the Shard Map Manager. 
    ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
    Console.WriteLine("Created SqlShardMapManager"); 

    shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

// The connectionString contains server name, database name, and admin credentials for privileges on both the GSM and the shards themselves.
} 
```

Для версии .NET можно использовать PowerShell, чтобы создать диспетчер карты сегментов. Пример представлен [здесь](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>Получение RangeShardMap или ListShardMap
Создав диспетчер карты сегментов, вы можете получить объекты RangeShardMap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn807318.aspx)) или ListShardMap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._list_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn807370.aspx)) с помощью методов TryGetRangeShardMap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.trygetrangeshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx)), TryGetListShardMap ([Java](https://docs.microsoft.com/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.trygetlistshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx)) или GetShardMap ([Java](https://docs.microsoft.com/java/api/com.microsoft.azure.elasticdb.shard.mapmanager._shard_map_manager.getshardmap), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx)).

```Java
// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
static <T> RangeShardMap<T> createOrGetRangeShardMap(ShardMapManager shardMapManager,
            String shardMapName,
            ShardKeyType keyType) {
    // Try to get a reference to the Shard Map.
    ReferenceObjectHelper<RangeShardMap<T>> refRangeShardMap = new ReferenceObjectHelper<>(null);
    boolean isGetSuccess = shardMapManager.tryGetRangeShardMap(shardMapName, keyType, refRangeShardMap);
    RangeShardMap<T> shardMap = refRangeShardMap.argValue;

    if (isGetSuccess && shardMap != null) {
        ConsoleUtils.writeInfo("Shard Map %1$s already exists", shardMap.getName());
    }
    else {
        // The Shard Map does not exist, so create it
        try {
            shardMap = shardMapManager.createRangeShardMap(shardMapName, keyType);
        }
        catch (Exception e) {
            e.printStackTrace();
        }
        ConsoleUtils.writeInfo("Created Shard Map %1$s", shardMap.getName());
    }

    return shardMap;
}
```

```csharp
// Creates a new Range Shard Map with the specified name, or gets the Range Shard Map if it already exists.
public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
{
    // Try to get a reference to the Shard Map.
    RangeShardMap<T> shardMap;
    bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

    if (shardMapExists)
    {
        ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
    }
    else
    {
        // The Shard Map does not exist, so create it
        shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
        ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
    }

    return shardMap;
} 
```

### <a name="shard-map-administration-credentials"></a>Учетные данные для администрирования карты сегментов
Приложения для администрирования и обработки карт сегментов отличаются от приложений, использующих карты сегментов для маршрутизации подключений. 

Для администрирования карт сегментов (добавления или изменения сегментов, карт сегментов, сопоставлений сегментов и т. д.) необходимо создать экземпляр **ShardMapManager** с использованием **учетных данных, для которых предусмотрены права на чтение и запись в базе GSM и в каждой базе данных, выступающей в качестве сегмента**. Учетные данные должны давать право записи в таблицы в GSM и LSM при вводе или изменения информации карт сегментов, а также право создавать таблицы LSM в новых сегментах.  

См. статью [Учетные данные для доступа к клиентской библиотеке эластичной базы данных](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Воздействует только на метаданные
Методы, используемые для заполнения и изменения данных **ShardMapManager** , не воздействуют на данные пользователя, хранящиеся в самих сегментах. Например, такие методы, как **CreateShard**, **DeleteShard**, **UpdateMapping** и другие, влияют только на метаданные карты сегментов. Они не удаляют, не добавляют и не изменяют пользовательские данные, содержащиеся в сегментах. На самом деле, эти методы предназначены для использования с отдельными операциями, с помощью которых вы создаете и удаляете фактические базы данных, либо перемещаете строки между сегментами для выравнивания сегментированной среды.  (Инструмент **разбиения и объединения**, входящий в состав инструментов эластичных баз данных, использует эти API-интерфейсы и управляет фактическим перемещением данных между сегментами.) (См. статью [Перемещение данных между масштабируемыми облачными базами данных](sql-database-elastic-scale-overview-split-and-merge.md).)

## <a name="data-dependent-routing"></a>Маршрутизация, зависящая от данных
Диспетчер карт сегментов используется приложениями, которым требуются подключения к базам данных для выполнения операций с данными конкретного приложения. Эти подключения необходимо связать с нужной базой данных. Это называется **маршрутизацией, зависимой от данных**. Для таких приложений необходимо объявить объект диспетчера карт сегментов в фабричном режиме, пользуясь учетными данными с доступом к базе данных GSM только для чтения. Учетные данные для подключения к нужной базе данных сегментов впоследствии будут передаваться в отдельных запросах подключения.

Обратите внимание, что эти приложения (использующие **ShardMapManager** в режиме только для чтения) не могут вносить изменения в карты и сопоставления. Для этого создайте специальные административные приложения или сценарии PowerShell, которые будут передавать учетные данные с более высокими правами доступа, как об этом говорилось ранее. См. статью [Учетные данные для доступа к клиентской библиотеке эластичной базы данных](sql-database-elastic-scale-manage-credentials.md).

Дополнительные сведения см. в статье [Маршрутизация, зависящая от данных](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Изменение карты сегментов
Карту сегментов можно изменять различными способами. Любым из приведенных способов можно изменить метаданные сегментов и сопоставления сегментов, но нельзя изменить данные самих сегментов, создать или удалить базу данных.  Некоторые из описанных ниже операций над сопоставлениями сегментов необходимо выполнять согласованно с административными действиями для физического перемещения данных, добавления и удаления баз данных, выступающих в качестве сегментов.

Эти методы работают совместно, как строительные блоки, доступные для изменения общего распределения данных в среде сегментированной базы данных.  

* Для добавления или удаления сегментов используйте **CreateShard** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._shard_map.createshard), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)) и **DeleteShard** ([Java](https://docs.microsoft.com/java/api/com.microsoft.azure.elasticdb.shard.map._shard_map.deleteshard), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)) из класса Shardmap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._shard_map), [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx)). 
  
    Для успешного выполнения этих операций необходимо указать существующие сервер и базу данных, которая играет роль целевого сегмента. Эти методы не изменяют сами базы данных, они изменяют только метаданные в сопоставлении сегментов.
* Для создания или удаления точек или диапазонов, сопоставленных с сегментами, используйте **CreateRangeMapping** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.createrangemapping), [.NET](https://msdn.microsoft.com/library/azure/dn841993.aspx)), **DeleteMapping** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.deletemapping), [.NET](https://msdn.microsoft.com/library/azure/dn824200.aspx)) из класса RangeShardMapping ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn807318.aspx)) и **CreatePointMapping** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._list_shard_map.createpointmapping), [.NET](https://msdn.microsoft.com/library/azure/dn807218.aspx)) из класса ListShardMap ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._list_shard_map), [.NET](https://msdn.microsoft.com/library/azure/dn842123.aspx)).
  
    Один сегмент может быть сопоставлен со множеством разных точек или диапазонов. Эти методы изменяют только метаданные, но не изменяют данные, хранящиеся в сегментах. Если для обеспечения согласованности с операциями **DeleteMapping** требуется удалить данные из базы данных, необходимо выполнить операции удаления отдельно, но с использованием этих методов.  
* Чтобы разбить существующие диапазоны на два или объединить смежные диапазоны в один, используйте методы **SplitMapping** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.splitmapping), [.NET](https://msdn.microsoft.com/library/azure/dn824205.aspx)) и **MergeMappings** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.mergemappings), [.NET](https://msdn.microsoft.com/library/azure/dn824201.aspx)).  
  
    Обратите внимание, что операции разбиения и слияния **не изменяют сегмент, с которым сопоставляются ключевые значения**. Функция разбиения разделяет существующий диапазон на две части, но оставляет их обе привязанными к одному сегменту. Функция объединения соединяет два соседних диапазона, привязанных к одному сегменту, в один целый диапазон.  Перемещение точек или самих диапазонов между сегментами необходимо координировать с помощью **UpdateMapping** в сочетании с фактическим перемещением данных.  Для координации изменений в карте сегментов с перемещением данных можно использовать службу **разбиения и слияния** , входящую в состав средств для работы с эластичными базами данных. 
* Для повторного сопоставления (или перемещения) отдельных точек или диапазонов в другие сегменты используйте метод **UpdateMapping** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.updatemapping), [.NET](https://msdn.microsoft.com/library/azure/dn824207.aspx)).  
  
    Так как данные придется перемещать из одного сегмента в другой для согласования с операциями **UpdateMapping**, перемещение необходимо выполнить отдельно, но с использованием этих методов.
* Для перевода сопоставлений в сетевой и автономный режим используйте методы **MarkMappingOffline** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.markmappingoffline), [.NET](https://msdn.microsoft.com/library/azure/dn824202.aspx)) и **MarkMappingOnline** ([Java](/java/api/com.microsoft.azure.elasticdb.shard.map._range_shard_map.markmappingonline), [.NET](https://msdn.microsoft.com/library/azure/dn807225.aspx)). Последний метод также используется для управления сетевым состоянием сопоставления. 
  
    Определенные операции для сопоставлений сегментов, включая **UpdateMapping** и **DeleteMapping**, могут выполняться только в автономном режиме. Если сопоставление находится в автономном режиме, то запрос данных с ключом, указывающим на это сопоставление, вернется с ошибкой. Кроме того, при первом переходе диапазона в автономный режим все соединения с соответствующим сегментом автоматически разрываются с целью предотвращения сбоев и обрыва результатов запросов, направленных на изменяемые диапазоны. 

Сопоставления являются неизменяемыми объектами в .net.  Все описанные выше методы, изменяющие сопоставление, также проверяют все ссылки на них в коде. Для облегчения выполнения последовательности операций, изменяющих состояние сопоставления, все методы, изменяющие сопоставление, возвращают новую ссылку сопоставления, так что операции могут быть объединены в цепочку. Например, для удаления существующего сопоставления в sm shardmap, содержащего ключ 25, можно выполнить следующее: 

```
    sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));
```

## <a name="adding-a-shard"></a>Добавление сегмента
Часто необходимо, чтобы приложение добавило в существующую карту сегментов новые сегменты для обработки данных, поступление которых ожидается из новых ключей и диапазонов ключей. Например, приложение с сегментированием по идентификатору клиента должно подготовить новый сегмент для нового клиента или при обработке данных с сегментированием по месяцам требуется создание нового сегмента перед началом следующего месяца. 

Если новый диапазон ключей не входит в существующую карту и нет необходимости перемещения данных, добавление сегментов и привязка к нему нового ключа или диапазона становится простой задачей. Дополнительные сведения о добавлении новых сегментов см. в статье [Добавление сегмента с использованием средств эластичных баз данных](sql-database-elastic-scale-add-a-shard.md).

Однако для случая, когда требуется перемещение данных, необходимо использовать инструмент разбиения и объединения для выполнения перемещения данных между сегментами в сочетании с необходимым обновлением карты сегментов. Сведения об использовании средств разбиения и слияния см. в статье [Перемещение данных между масштабируемыми облачными базами данных](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
