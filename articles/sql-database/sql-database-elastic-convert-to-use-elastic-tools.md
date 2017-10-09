---
title: "aaaMigrate существующих баз данных вне tooscale | Документы Microsoft"
description: "Преобразование Сервис эластичной базы данных toouse сегментированных баз данных путем создания диспетчера карты сегментов"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 8c851d8e-8fd5-4327-89c1-9178b20ddd69
ms.service: sql-database
ms.custom: scale out apps
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: fa2c9e3699f30667cf547d1faadf4504609199be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-existing-databases-tooscale-out"></a>Миграция существующих баз данных tooscale масштабированием
Легко управлять существующих масштабируемых сегментированных баз данных с помощью базы данных SQL Azure инструменты для баз данных (таких как hello [клиентской библиотеке эластичной базы данных](sql-database-elastic-database-client-library.md)). Необходимо сначала преобразовать существующий набор баз данных toouse hello [диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md). 

## <a name="overview"></a>Обзор
toomigrate сегментированной базы данных: 

1. Подготовка hello [базы данных диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md).
2. Создание карты сегментов hello.
3. Подготовьте hello отдельные сегменты.  
4. Добавление карты сегментов toohello сопоставления.

Эти методы можно реализовать с помощью либо hello [клиентская библиотека .NET Framework](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/), или скрипты PowerShell hello, обнаруженным в [база данных SQL Azure — скриптов средств эластичной базы данных](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db). Приведенные здесь примеры Hello использовать скрипты PowerShell hello.

Дополнительные сведения о hello ShardMapManager см. в разделе [управления карты сегментов](sql-database-elastic-scale-shard-map-management.md). Обзор средств hello эластичной базы данных см. в разделе [Общие сведения о возможностях эластичной базы данных](sql-database-elastic-scale-introduction.md).

## <a name="prepare-hello-shard-map-manager-database"></a>Подготовка базы данных диспетчера карты сегментов hello
диспетчера карты сегментов Hello является специальная база данных, содержащей данные toomanage hello масштабируемых-базы данных. Можно использовать существующую базу данных или создать новую. Обратите внимание, что база данных выступает в роли диспетчера карты сегментов не должно быть hello же базы данных, как тот или иной сегмент. Также Обратите внимание, что скрипт PowerShell hello не создаются hello базы данных. 

## <a name="step-1-create-a-shard-map-manager"></a>Шаг 1. Создание диспетчера сопоставления сегментов
    # Create a shard map manager. 
    New-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 
    #<server_name> and <smm_db_name> are hello server name and database name 
    # for hello new or existing database that should be used for storing 
    # tenant-database mapping information.

### <a name="tooretrieve-hello-shard-map-manager"></a>диспетчера карты сегментов tooretrieve hello
После создания можно извлечь hello диспетчера карты сегментов с этим командлетом. Этот шаг требуется каждый раз, когда необходимо toouse hello ShardMapManager объекта.

    # Try tooget a reference toohello Shard Map Manager  
    $ShardMapManager = Get-ShardMapManager -UserName '<user_name>' 
    -Password '<password>' 
    -SqlServerName '<server_name>' 
    -SqlDatabaseName '<smm_db_name>' 


## <a name="step-2-create-hello-shard-map"></a>Шаг 2: Создание карты сегментов hello
Необходимо выбрать тип hello toocreate карты сегментов. Выбор Hello зависит от архитектуры hello базы данных. 

1. Для каждой базы данных одного клиента (условия, в разделе hello [Глоссарий](sql-database-elastic-scale-glossary.md).) 
2. Несколько клиентов на одну базу данных (два типа):
   1. Сопоставление по спискам
   2. Сопоставление по диапазонам

Для модели с одним клиентом создайте карту сегментов с **сопоставлением по списку** . модель одного клиента Hello назначает одной базы данных на клиенте. Эта модель подходит для разработчиков SaaS, так как она упрощает управление.

![Сопоставление по спискам][1]

Hello мультитенантной модели назначает несколько клиентов tooa одной базы данных (и групп клиентов можно распределить по нескольким базам данных). Эту модель можно используйте, когда предполагается, что данные, toohave небольшой каждого клиента. В этой модели мы назначает диапазон клиентов tooa базы данных с помощью **сопоставления диапазона**. 

![Сопоставление по диапазонам][2]

Или можно применить модель базы данных нескольких клиентов с помощью *сопоставление списка* tooassign несколько клиентов tooa одной базы данных. Например используется toostore сведения об ИД клиента 1 и 5 — DB1 и DB2 хранит данные для клиента 7 и 10 клиента. 

![Несколько клиентов для одной базы данных][3] 

**Выберите один из вариантов, соответствующий вашему выбору.**

### <a name="option-1-create-a-shard-map-for-a-list-mapping"></a>Вариант 1. Создание карты сегментов для сопоставления по списку
Создайте карту сегментов, с помощью объекта ShardMapManager hello. 

    # $ShardMapManager is hello shard map manager object. 
    $ShardMap = New-ListShardMap -KeyType $([int]) 
    -ListShardMapName 'ListShardMap' 
    -ShardMapManager $ShardMapManager 


### <a name="option-2-create-a-shard-map-for-a-range-mapping"></a>Вариант 2. Создание карты сегментов для сопоставления по диапазонам
Обратите внимание, что tooutilize этот шаблон для сопоставления, значения идентификатора клиента должен toobe непрерывного диапазона, и он является приемлемым toohave разрыв в диапазонах hello пропустив просто hello диапазона при создании баз данных hello.

    # $ShardMapManager is hello shard map manager object 
    # 'RangeShardMap' is hello unique identifier for hello range shard map.  
    $ShardMap = New-RangeShardMap 
    -KeyType $([int]) 
    -RangeShardMapName 'RangeShardMap' 
    -ShardMapManager $ShardMapManager 

### <a name="option-3-list-mappings-on-a-single-database"></a>Вариант 3. Сопоставление по списку для одной базы данных
Для настройки этого шаблона также требуется создать карту списков, как показано в разделе "Шаг 2, вариант 1".

## <a name="step-3-prepare-individual-shards"></a>Шаг 3. Подготовка отдельных сегментов
Добавьте каждый диспетчера карты сегментов toohello сегментов (база данных). Это подготавливает hello отдельных баз данных для хранения сведений о сопоставлении. Подготовьте так каждый сегмент.

    Add-Shard 
    -ShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>'
    # hello $ShardMap is hello shard map created in step 2.


## <a name="step-4-add-mappings"></a>Шаг 4. Добавление сопоставлений
Добавление Hello сопоставлений зависит от вида hello карта сегментов, созданный. Если создана карта списков, нужно добавить сопоставления по спискам. Если создана карта диапазонов, нужно добавить сопоставления по диапазонам.

### <a name="option-1-map-hello-data-for-a-list-mapping"></a>Вариант 1: данные hello карты для отображения списка
Сопоставление данных hello, добавив сопоставление списка для каждого клиента.  

    # Create hello mappings and associate it with hello new shards 
    Add-ListMapping 
    -KeyType $([int]) 
    -ListPoint '<tenant_id>' 
    -ListShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 

### <a name="option-2-map-hello-data-for-a-range-mapping"></a>Вариант 2: данные hello карты для сопоставления диапазона
Добавьте hello диапазон сопоставления для всех диапазон идентификаторов клиента hello - связи баз данных:

    # Create hello mappings and associate it with hello new shards 
    Add-RangeMapping 
    -KeyType $([int]) 
    -RangeHigh '5' 
    -RangeLow '1' 
    -RangeShardMap $ShardMap 
    -SqlServerName '<shard_server_name>' 
    -SqlDatabaseName '<shard_database_name>' 


### <a name="step-4-option-3-map-hello-data-for-multiple-tenants-on-a-single-database"></a>Вариант 3. шаг 4: сопоставление hello данных для нескольких клиентов в одной базе данных
Для каждого клиента, запустите hello добавить ListMapping (параметр 1, выше). 

## <a name="checking-hello-mappings"></a>Проверка сопоставления hello
Сведения о существующих сегментов hello и сопоставления hello, связанные с ними можно запросить с помощью следующих команд:  

    # List hello shards and mappings 
    Get-Shards -ShardMap $ShardMap 
    Get-Mappings -ShardMap $ShardMap 

## <a name="summary"></a>Сводка
После завершения установки hello, можно начать toouse hello эластичной базы данных клиентской библиотеки. Кроме того, можно воспользоваться [маршрутизацией, зависящей от данных](sql-database-elastic-scale-data-dependent-routing.md), и [формированием многосегментных запросов](sql-database-elastic-scale-multishard-querying.md).

## <a name="next-steps"></a>Дальнейшие действия
Получение скриптов PowerShell hello из [базы данных эластичных БД SQL Azure средств sripts](https://gallery.technet.microsoft.com/scriptcenter/Azure-SQL-DB-Elastic-731883db).

Hello средства доступны на сайте GitHub: [Azure/гибкому db-tools](https://github.com/Azure/elastic-db-tools).

Используйте tooor hello средство слияния разбиение toomove данных из одного клиента модели tooa мультитенантной модели. Ознакомьтесь со статьей о [средстве разбиения и объединения](sql-database-elastic-scale-get-started.md).

## <a name="additional-resources"></a>Дополнительные ресурсы
Сведения о распространенных шаблонах архитектуры данных для мультитенантных приложений базы данных SaaS см. в статье [Шаблоны разработки для мультитенантных приложений SaaS с использованием базы данных Azure SQL](sql-database-design-patterns-multi-tenancy-saas-applications.md).

## <a name="questions-and-feature-requests"></a>Вопросы и запросы на функции
Ответить на вопросы, пожалуйста направляться на hello toous [форум базы данных SQL](http://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted) и для запросов, компонент, добавьте их toohello [форуме обратной связи в базе данных SQL](https://feedback.azure.com/forums/217321-sql-database/).

<!--Image references-->
[1]: ./media/sql-database-elastic-convert-to-use-elastic-tools/listmapping.png
[2]: ./media/sql-database-elastic-convert-to-use-elastic-tools/rangemapping.png
[3]: ./media/sql-database-elastic-convert-to-use-elastic-tools/multipleonsingledb.png

