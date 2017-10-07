---
title: "aaaScale ожидания базы данных Azure SQL | Документы Microsoft"
description: "Как toouse hello ShardMapManager клиентской библиотеке эластичной базы данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: 0e9d647a-9ba9-4875-aa22-662d01283439
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 4cf670d42ad7ded98fb8d6f0830154587dd2c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-out-databases-with-hello-shard-map-manager"></a>Горизонтальное масштабирование баз данных с использованием диспетчера карты сегментов hello
tooeasily горизонтальное масштабирование баз данных в SQL Azure, используйте диспетчера карты сегментов. диспетчера карты сегментов Hello является специальная база данных, которое поддерживает глобального сопоставления информацию о всем сегментам (базы данных) в наборе сегментов. Hello метаданных позволяет tooconnect toohello правильный базы данных приложения на основе значения hello hello **ключа сегментирования**. Кроме того, каждый сегмент в наборе hello содержит maps, отслеживающие hello локального сегментов данных (известный как **Подсегменты**). 

![Управление размещением сегментов](./media/sql-database-elastic-scale-shard-map-management/glossary.png)

Понимание того, как создавать эти карты, управления essential tooshard карты. Это делается с помощью hello [класса ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)в hello [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md) toomanage сегмент соответствует.  

## <a name="shard-maps-and-shard-mappings"></a>Карты сегментов и сопоставление сегментов
Для каждого сегмента необходимо выбрать тип hello toocreate карты сегментов. Выбор Hello зависит от архитектуры hello базы данных. 

1. По одному клиенту для каждой базы данных.  
2. Несколько клиентов на одну базу данных (два типа):
   1. Сопоставление по спискам
   2. Сопоставление по диапазонам

Для модели с одним клиентом создайте карту сегментов с **сопоставлением по списку** . модель одного клиента Hello назначает одной базы данных на клиенте. Эта модель подходит для разработчиков SaaS, так как она упрощает управление.

![Сопоставление по спискам][1]

Hello мультитенантной модели назначает несколько клиентов tooa одной базы данных (и групп клиентов можно распределить по нескольким базам данных). Эту модель можно используйте, когда предполагается, что данные, toohave небольшой каждого клиента. В этой модели мы назначает диапазон клиентов tooa базы данных с помощью **сопоставления диапазона**. 

![Сопоставление по диапазонам][2]

Или можно применить модель базы данных нескольких клиентов с помощью *сопоставление списка* tooassign несколько клиентов tooa одной базы данных. Например используется toostore сведения об ИД клиента 1 и 5 — DB1 и DB2 хранит данные для клиента 7 и 10 клиента. 

![Несколько клиентов для одной базы данных][3] 

### <a name="supported-net-types-for-sharding-keys"></a>Поддерживаемые типы .net для ключей сегментирования
Эластичный hello поддержки масштабирования, следующие .net Framework типы как ключи сегментирования:

* целое число
* длинное целое число
* guid
* byte[]  
* datetime;
* интервал времени
* datetimeoffset;

### <a name="list-and-range-shard-maps"></a>Списочные и диапазонные карты сегментов
Карты сегментов могут быть созданы с использованием **списков индивидуальных величин сегментных ключей** или с использованием **диапазонов величин сегментных ключей**. 

### <a name="list-shard-maps"></a>Списочные карты сегментов
**Сегменты** содержат **Подсегменты** и hello сопоставление подсегментов tooshards обеспечивается карты сегментов. Объект **карта сегментов список** — это связь между hello отдельные значения ключей, идентифицирующих Подсегменты hello и hello баз данных, которые служат в качестве сегментов.  **Список сопоставлений** явные и различные значения ключа может быть сопоставленных toohello одной базе данных. Например раздел 1 сопоставляет tooDatabase A и B. база данных ссылаются на значения ключей, 3 и 6

| Ключ | Расположение сегмента |
| --- | --- |
| 1 |БазаДанных_А |
| 3 |БазаДанных_Б |
| 4. |БазаДанных_В |
| 6 |БазаДанных_Б |
| ... |... |

### <a name="range-shard-maps"></a>Диапазонные карты сегментов
В **карта сегментов диапазон**, диапазона ключей hello описан с помощью пары **[высокой стоимости, большое значение)** где hello *высокой стоимости* — минимальный ключ hello в диапазоне hello и hello *Высокое значение* является hello первое значение выше диапазона hello. 

Например **[0, 100)** включает все целые числа, которые больше или равны 0 и меньше 100. Обратите внимание, что поддерживаются несколько toohello точка может диапазоны же базы данных и несвязанных диапазонов (например, [100,200) и [400,600) обоих точки tooDatabase C в приведенном ниже примере hello.)

| Ключ | Расположение сегмента |
| --- | --- |
| [1,50) |БазаДанных_А |
| [50,100) |БазаДанных_Б |
| [100,200) |БазаДанных_В |
| [400,600) |БазаДанных_В |
| ... |... |

Каждый из вышеуказанных таблиц hello является пример **ShardMap** объекта. Каждая строка является упрощенным примером индивидуального **PointMapping** (для карты сегментов hello списка) или **RangeMapping** (для карты сегментов hello диапазона) объекта.

## <a name="shard-map-manager"></a>Диспетчер карты сегментов
В клиентской библиотеке hello hello диспетчера карты сегментов — это совокупность карт сегментов. Здравствуйте, данные, которыми управляет **ShardMapManager** экземпляр сохраняется в трех местах: 

1. **Глобальные карты сегментов (GSM)**: укажите tooserve базы данных в качестве hello репозиторий для всех карт сегментов и сопоставления. Специальные таблицы и хранимые процедуры создаются автоматически toomanage hello сведения. Это обычно небольшая база данных и в незначительной степени доступ и не должны использоваться для других нужд приложения hello. Hello таблицы расположены в специальной схеме с именем **__ShardManagement**. 
2. **Локальный карты сегментов (LSM)**: каждой базы данных, укажите toobe сегмент — изменить toocontain несколько небольших таблиц и специальные хранимые процедуры, которые содержат и управляют сведения о конкретных toothat сегментов карты сегментов. Эти сведения являются избыточными сведениями hello в hello GSM и сведений о карте сегментов в кэше toovalidate приложения hello позволяет без помещения любая нагрузка на hello GSM; приложение Hello использует hello LSM toodetermine, если кэшированные сопоставления по-прежнему действителен. Hello таблиц соответствующего toohello LSM на каждый сегмент также находятся в схеме hello **__ShardManagement**.
3. **Кэш приложения**: каждый экземпляр приложения, у которого есть доступ к объекту **ShardMapManager**, поддерживает локальный кэш своих сопоставлений в памяти. Хранятся использованные за последнее время сведения о маршрутизации. 

## <a name="constructing-a-shardmapmanager"></a>Создание объекта ShardMapManager
Объект **ShardMapManager** создается с помощью шаблона [фабрики](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx) . Hello  **[ShardMapManagerFactory.GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**  метод принимает учетные данные (включая имя сервера hello и имя базы данных, содержащий hello GSM) в форме hello  **ConnectionString** и возвращает экземпляр класса **ShardMapManager**.  

**Имейте в виду:** hello **ShardMapManager** должен создаваться только один раз на домен приложения, в код инициализации hello для приложения. Создание дополнительных экземпляров ShardMapManager в hello того же домена приложения, приведет к увеличение памяти и ЦП приложения hello. **ShardMapManager** может содержать любое число карт сегментов. Многим приложениям достаточно одной карты сегментов, но в некоторых случаях применяются разные наборы баз данных, которые используются в разных схемах или имеют уникальное назначение. В таком случае желательно использовать несколько карт сегментов. 

В этом коде приложение попытается tooopen существующий **ShardMapManager** с hello [TryGetSqlShardMapManager метод](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx).  Если объекты, представляющие Global **ShardMapManager** (GSM) еще не существует в базе данных hello, hello клиентская библиотека создает их наличие с помощью hello [CreateSqlShardMapManager метод](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx).

    // Try tooget a reference toohello Shard Map Manager 
     // via hello Shard Map Manager database.  
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
        // Create hello Shard Map Manager. 
        ShardMapManagerFactory.CreateSqlShardMapManager(connectionString);
        Console.WriteLine("Created SqlShardMapManager"); 

        shardMapManager = ShardMapManagerFactory.GetSqlShardMapManager(
            connectionString, 
            ShardMapManagerLoadPolicy.Lazy);

        // hello connectionString contains server name, database name, and admin credentials 
        // for privileges on both hello GSM and hello shards themselves.
    } 

В качестве альтернативы можно использовать Powershell toocreate нового диспетчера карты сегментов. Пример представлен [здесь](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

## <a name="get-a-rangeshardmap-or-listshardmap"></a>Получение RangeShardMap или ListShardMap
После создания диспетчера карты сегментов, можно получить hello [RangeShardMap](https://msdn.microsoft.com/library/azure/dn807318.aspx) или [ListShardMap](https://msdn.microsoft.com/library/azure/dn807370.aspx) с помощью hello [TryGetRangeShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), hello [ TryGetListShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), или hello [GetShardMap](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) метод.

    /// <summary>
    /// Creates a new Range Shard Map with hello specified name, or gets hello Range Shard Map if it already exists.
    /// </summary>
    public static RangeShardMap<T> CreateOrGetRangeShardMap<T>(ShardMapManager shardMapManager, string shardMapName)
    {
        // Try tooget a reference toohello Shard Map.
        RangeShardMap<T> shardMap;
        bool shardMapExists = shardMapManager.TryGetRangeShardMap(shardMapName, out shardMap);

        if (shardMapExists)
        {
            ConsoleUtils.WriteInfo("Shard Map {0} already exists", shardMap.Name);
        }
        else
        {
            // hello Shard Map does not exist, so create it
            shardMap = shardMapManager.CreateRangeShardMap<T>(shardMapName);
            ConsoleUtils.WriteInfo("Created Shard Map {0}", shardMap.Name);
        }

        return shardMap;
    } 

### <a name="shard-map-administration-credentials"></a>Учетные данные для администрирования карты сегментов
Приложения, администрирования и управления ими карт сегментов, отличаются от привязок, использующих подключения tooroute карты сегментов hello. 

Сопоставляет tooadminister сегментов (Добавление или изменение сегментов, карт сегментов, сопоставления сегментов, т. д.) необходимо создать экземпляр hello **ShardMapManager** с помощью **учетные данные, имеющие права на обе базы данных GSM hello и на каждом чтение и запись базы данных, которая служит в качестве сегментом**. Hello учетные данные необходимо разрешить для записи в таблицах hello в обоих hello GSM и LSM как вводится или изменяется, также как и для создания таблиц LSM на новые сегменты сведений о карте сегментов.  

В разделе [учетные данные, используемые tooaccess hello эластичной базы данных клиентской библиотеки](sql-database-elastic-scale-manage-credentials.md).

### <a name="only-metadata-affected"></a>Воздействует только на метаданные
Методы, используемые для заполнения или изменение hello **ShardMapManager** данных не меняйте hello пользователем данные, хранящиеся в сегменты hello сами. Например, методы, такие как **CreateShard**, **DeleteShard**, **UpdateMapping**, т. д. влияют на hello сегментов карты только метаданные. Не удаляйте, добавления или изменения пользовательских данных, содержащихся в сегментах hello. Вместо этого эти методы являются спроектированный toobe используется в сочетании с отдельные операции можно выполнять toocreate и удаления действительных баз данных или переместить строки из одного сегмента tooanother toorebalance сегментированных среды.  (hello **разделения слияния** средства, включенная в средства эластичной базы данных использует эти API-интерфейсы, а также управляя операциями перемещения фактических данных между сегментами.) В разделе [масштабирования с помощью средства hello разделения эластичной базы данных-слияния](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="populating-a-shard-map-example"></a>Пример заполнения сопоставления сегментов
Ниже приведен пример последовательности операций toopopulate карты конкретных сегментов. Hello код выполняет следующие действия. 

1. При помощи диспетчера сопоставления сегментов создается новое сопоставление сегментов. 
2. карта сегментов toohello добавляются метаданные Hello для двух различных сегментах. 
3. Добавляются различные сопоставления диапазона ключей и hello общее сопоставление сегментов hello отображения. 

Hello код, чтобы метод hello можно перезапустить, если произошла ошибка. Каждый запрос проверяет, является ли тот или иной сегмент или сопоставление уже существует, прежде чем toocreate его. Hello коде предполагается, что базы данных с именем **sample_shard_0**, **sample_shard_1** и **sample_shard_2** уже были созданы в hello server ссылается строка **shardServer**. 

    public void CreatePopulatedRangeMap(ShardMapManager smm, string mapName) 
        {            
            RangeShardMap<long> sm = null; 

            // check if shardmap exists and if not, create it 
            if (!smm.TryGetRangeShardMap(mapName, out sm)) 
            { 
                sm = smm.CreateRangeShardMap<long>(mapName); 
            } 

            Shard shard0 = null, shard1=null; 
            // Check if shard exists and if not, 
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetShard(new ShardLocation(
                                     shardServer, 
                                     "sample_shard_0"), 
                                     out shard0)) 
            { 
                Shard0 = sm.CreateShard(new ShardLocation(
                                            shardServer, 
                                            "sample_shard_0")); 
            } 

            if (!sm.TryGetShard(new ShardLocation(
                                    shardServer, 
                                    "sample_shard_1"), 
                                    out shard1)) 
            { 
                Shard1 = sm.CreateShard(new ShardLocation(
                                             shardServer, 
                                            "sample_shard_1"));  
            } 

            RangeMapping<long> rmpg=null; 

            // Check if mapping exists and if not,
            // create it (Idempotent / tolerant of re-execute) 
            if (!sm.TryGetMappingForKey(0, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                          new RangeMappingCreationInfo<long>
                          (new Range<long>(0, 50), 
                          shard0, 
                          MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(50, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(50, 100), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(100, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long>
                         (new Range<long>(100, 150), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(150, out rmpg)) 
            { 
                sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(150, 200), 
                         shard1, 
                         MappingStatus.Online)); 
            } 

            if (!sm.TryGetMappingForKey(200, out rmpg)) 
            { 
               sm.CreateRangeMapping(
                         new RangeMappingCreationInfo<long> 
                         (new Range<long>(200, 300), 
                         shard0, 
                         MappingStatus.Online)); 
            } 

            // List hello shards and mappings 
            foreach (Shard s in sm.GetShards()
                         .OrderBy(s => s.Location.DataSource)
                         .ThenBy(s => s.Location.Database))
            { 
               Console.WriteLine("shard: "+ s.Location); 
            } 

            foreach (RangeMapping<long> rm in sm.GetMappings()) 
            { 
                Console.WriteLine("range: [" + rm.Value.Low.ToString() + ":" 
                        + rm.Value.High.ToString()+ ")  ==>" +rm.Shard.Location); 
            } 
        } 

Как можно использовать PowerShell вместо сценариев tooachieve hello же результат. Некоторые примеры PowerShell образец hello доступны [здесь](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).     

После заполнения карт сегментов приложений доступа к данным могут быть созданы или адаптировать toowork с картами hello. Заполнение и управления данными карты hello не должен появиться пока **макета карты** должен toochange.  

## <a name="data-dependent-routing"></a>Маршрутизация, зависящая от данных
диспетчера карты сегментов Hello наиболее будет использоваться в приложениях, требующих операций данных конкретного приложения hello tooperform подключения базы данных. Эти соединения должна быть связана с hello нужную базу данных. Это называется **маршрутизацией, зависимой от данных**. Для этих приложений создание экземпляра объекта диспетчера карты сегментов из фабрики hello, используя учетные данные, иметь доступ только для чтения данных GSM hello. Отдельные запросы для подключения к более поздней версии предоставить учетные данные, необходимые для соединения базы данных toohello соответствующий сегмент.

Обратите внимание, что эти приложения (с помощью **ShardMapManager** открывается с учетными данными только для чтения) не может вносить в них изменения toohello сопоставления или сопоставления. Для этого создайте специальные административные приложения или сценарии PowerShell, которые будут передавать учетные данные с более высокими правами доступа, как об этом говорилось ранее. В разделе [учетные данные, используемые tooaccess hello эластичной базы данных клиентской библиотеки](sql-database-elastic-scale-manage-credentials.md).

Дополнительные сведения см. в статье [Маршрутизация, зависящая от данных](sql-database-elastic-scale-data-dependent-routing.md). 

## <a name="modifying-a-shard-map"></a>Изменение карты сегментов
Карту сегментов можно изменять различными способами. Все следующие методы hello изменить hello метаданные, описывающие hello сегментов и их сопоставлений, но физически не изменяют данные в сегменты hello или сделать их создания или удаления hello действительных баз данных.  Некоторые операции hello на карте сегментов hello, описанных ниже может понадобиться toobe, координируемых с административные действия, физически переместить данные или, добавлять и удалять базы данных, которые выступают в качестве сегментов.

Эти методы работают вместе как hello стандартные блоки, доступные для изменения hello общее распределение данных в вашей среде сегментированной базы данных.  

* tooadd или удаления сегментов: использовать  **[CreateShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.createshard.aspx)**  и  **[DeleteShard](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.deleteshard.aspx)**  из hello [Shardmap класса](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.aspx). 
  
    Hello сервера и базы данных, представляющий целевой сегментов hello должен существовать для tooexecute этих операций. Эти методы никак не повлияли на hello самих базах данных, только на метаданные в карте сегментов hello.
* toocreate или удаление точек или диапазоны, которые сопоставляются toohello сегментов: использовать  **[CreateRangeMapping](https://msdn.microsoft.com/library/azure/dn841993.aspx)**,  **[DeleteMapping](https://msdn.microsoft.com/library/azure/dn824200.aspx)**  из hello [Класса RangeShardMapping](https://msdn.microsoft.com/library/azure/dn807318.aspx), и  **[CreatePointMapping](https://msdn.microsoft.com/library/azure/dn807218.aspx)**  из hello [ListShardMap](https://msdn.microsoft.com/library/azure/dn842123.aspx)
  
    Много разных точек или диапазоны могут быть сопоставленных toohello же сегментов. Эти методы изменяют только метаданные, но не изменяют данные, хранящиеся в сегментах. Если данные должны удаляются из базы данных hello в порядке toobe согласуется с toobe **DeleteMapping** операций, необходимо будет tooperform этих операций отдельно, но вместе с помощью этих методов.  
* существующий диапазон toosplit в две или слияния соседних диапазонах в один: использовать  **[SplitMapping](https://msdn.microsoft.com/library/azure/dn824205.aspx)**  и  **[MergeMappings](https://msdn.microsoft.com/library/azure/dn824201.aspx)**.  
  
    Обратите внимание, что разбиение и объединение операций **не изменяйте hello сегментов toowhich ключ значения сопоставляются**. Разбиения прерывается существующего диапазона на две части, но оставляет и как сопоставленные toohello же сегментов. Слияние работает в двух соседних диапазонах, которые уже сопоставленных toohello же сегменту, объединение их в один диапазон.  Hello перемещения точек или сами диапазоны между сегментами должен toobe, координируемых с помощью **UpdateMapping** в сочетании с перемещением фактические данные.  Можно использовать hello **разделения или слияния** toocoordinate изменения карты сегментов с перемещением данных службы, который является частью эластичной базы данных в средствах при необходимости перемещения. 
* toore карты (или переместите) отдельные точки или диапазоны toodifferent сегменты: использовать  **[UpdateMapping](https://msdn.microsoft.com/library/azure/dn824207.aspx)**.  
  
    Так как данные могут требовать перемещать из одного сегмента tooanother в порядке toobe согласуется с toobe **UpdateMapping** операций, необходимо будет tooperform изменения отдельно, но вместе с помощью этих методов.
* tootake сопоставления сети и вне сети: использовать  **[MarkMappingOffline](https://msdn.microsoft.com/library/azure/dn824202.aspx)**  и  **[MarkMappingOnline](https://msdn.microsoft.com/library/azure/dn807225.aspx)**  toocontrol hello состояния сети сопоставление. 
  
    Определенные операции для сопоставлений сегментов, включая **UpdateMapping** и **DeleteMapping**, могут выполняться только в автономном режиме. Если сопоставление находится в автономном режиме, то запрос данных с ключом, указывающим на это сопоставление, возвратит ошибку. Кроме того Если диапазон сначала переводится в автономный режим, сегментов toohello затронуты все подключения автоматически будут уничтожены в порядке tooprevent неправильные или неполные результаты запросов направлена диапазоны изменяемое. 

Сопоставления являются неизменяемыми объектами в .net.  Все hello методы выше, измените сопоставления также недействительными toothem все ссылки в коде. toomake ИТ проще tooperform последовательности операций, изменяющих состояние сопоставления, все методы hello, измените сопоставление возвращают новый сопоставление ссылку, поэтому операции могут быть соединены. Например при toodelete существующее сопоставление в sm shardmap, который содержит ключ hello 25, можно выполнить следующие hello: 

        sm.DeleteMapping(sm.MarkMappingOffline(sm.GetMappingForKey(25)));

## <a name="adding-a-shard"></a>Добавление сегмента
Приложениям часто требуется toosimply добавить новые данные toohandle сегментов, который ожидается от новых ключей или диапазонов ключей для карты сегментов, которая уже существует. Например приложение сегментированных по ИД клиента может потребоваться tooprovision новый сегмент для нового клиента или ежемесячно сегментированных данных может потребоваться новый сегмент подготовить перед запуском hello каждого нового месяца. 

При hello новый диапазон значений ключа еще не частью существующее сопоставление и перемещение данных отсутствует, это очень простой tooadd hello новый сегмент, связать новый ключ hello или диапазон toothat сегментов. Дополнительные сведения о добавлении новых сегментов см. в статье [Добавление сегмента с использованием средств эластичных баз данных](sql-database-elastic-scale-add-a-shard.md).

Тем не менее, в сценариях, требующих перемещения данных, средство разделения слияния hello происходит перемещение данных hello необходимые tooorchestrate между сегментами в сочетании с обновления сопоставлений hello необходимые сегментов. Сведения об использовании hello yool разделения слияния, см. в разделе [Обзор разделения слияния](sql-database-elastic-scale-overview-split-and-merge.md) 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-shard-map-management/listmapping.png
[2]: ./media/sql-database-elastic-scale-shard-map-management/rangemapping.png
[3]: ./media/sql-database-elastic-scale-shard-map-management/multipleonsingledb.png
