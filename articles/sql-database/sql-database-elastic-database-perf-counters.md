---
title: "счетчики aaaPerformance для диспетчера карты сегментов"
description: "Класс ShardMapManager и счетчики производительности для маршрутизации, зависящей от данных"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: b090aba0-2e30-454c-96b3-dffa281f539a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: ddove
ms.openlocfilehash: d24198563d9fa88d12e6c464dbe89bc300e72ca0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="performance-counters-for-shard-map-manager"></a>Счетчики производительности для диспетчера карты сегментов
Можно записать hello производительность [диспетчера карты сегментов](sql-database-elastic-scale-shard-map-management.md), особенно при использовании [управляемой данными маршрутизацией](sql-database-elastic-scale-data-dependent-routing.md). Счетчики создаются с помощью методов класса Microsoft.Azure.SqlDatabase.ElasticScale.Client hello.  

Счетчики, используемые tootrack hello производительность [управляемой данными маршрутизацией](sql-database-elastic-scale-data-dependent-routing.md) операций. Эти счетчики доступны в hello системного монитора в категории «Эластичной базы данных: управления сегментами» hello.

**Для последней версии hello:** Go слишком[Microsoft.Azure.SqlDatabase.ElasticScale.Client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). См. также [обновление приложения toouse hello последнюю эластичной базы данных клиентской библиотеки](sql-database-elastic-scale-upgrade-client-library.md).

## <a name="prerequisites"></a>Предварительные требования
* Здравствуйте, категорию производительности toocreate hello и счетчики, пользователь должен быть частью локальной hello **Администраторы** на компьютере hello, где размещается приложение hello.  
* toocreate производительности, счетчик экземпляра и обновить счетчики hello, hello пользователь должен быть членом либо hello **Администраторы** или **пользователи системного монитора** группы. 

## <a name="create-performance-category-and-counters"></a>Создание счетчиков и категорий производительности
счетчики toocreate hello, вызовите метод CreatePeformanceCategoryAndCounters hello hello [ShardMapManagmentFactory класса](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.aspx). Только администратор может выполнить метод hello: 

    ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()  

Можно также использовать [это](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) метод hello tooexecute сценария PowerShell. метод Hello создает hello следующие счетчики производительности:  

* **Кэшированные сопоставления**: число сопоставлений hello карта сегментов в кэше.
* **Операции DDR/сек**: скорость зависимых операций маршрутизации данных для сопоставления сегментов hello. Этот счетчик обновляется в том случае, когда вызов слишком[OpenConnectionForKey()](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx) результатов в сегменте назначения toohello успешного подключения. 
* **Сопоставление попаданий в кэш уточняющего запроса в секунду**: скорость операций уточняющего запроса успешно кэша для сопоставления в карте сегментов hello. 
* **Сопоставление подстановки промахов кэша/с**: скорость неудачных кэша операции поиска для сопоставления в карте сегментов hello.
* **Сопоставления добавлены или обновлены в кэш в секунду**: скорость, с какой сопоставления добавляются или обновленных в кэш для карты сегментов hello. 
* **Сопоставления, удаляются из кэша в секунду**: скорость, с которой сопоставления удаляются из кэша для карты сегментов hello. 

Счетчики производительности создаются для каждой кэшированной карты сегментов каждого процесса.  

## <a name="notes"></a>Примечания
Hello следующие события запустить создание hello hello счетчиков производительности:  

* Инициализация hello [ShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx) с [упреждающую](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy.aspx), если hello ShardMapManager содержит все карты сегментов. К ним относятся hello [GetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx?f=255&MSPPError=-2147217396#M:Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerFactory.GetSqlShardMapManager%28System.String,Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.ShardMapManagerLoadPolicy%29) и hello [TryGetSqlShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx) методы.
* Успешный поиск карты сегментов (с помощью [GetShardMap()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap()](https://msdn.microsoft.com/library/azure/dn824212.aspx) или [GetRangeShardMap()](https://msdn.microsoft.com/library/azure/dn824173.aspx)). 
* Успешное создание карты сегментов с помощью CreateShardMap().

счетчики производительности Hello обновляется все операции кэша, выполняемые на карте сегментов hello и сопоставления. Успешное удаление hello карта сегментов, с помощью reults DeleteShardMap () в удаление экземпляра счетчиков производительности hello.  

## <a name="best-practices"></a>Рекомендации
* Создать категорию производительности hello и счетчики должно выполняться только один раз перед созданием hello объекта ShardMapManager. Каждый выполнение команды hello CreatePerformanceCategoryAndCounters() очищает предыдущие счетчики hello (потери данных, о которых сообщили все экземпляры) и создавать новые.  
* Экземпляры счетчиков производительности создаются для каждого процесса. Любой сбоя приложения или удаление карты сегментов из кэша hello приведет к удалению экземпляров счетчиков производительности hello.  

### <a name="see-also"></a>См. также
[Общие сведения о возможностях эластичных баз данных](sql-database-elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->

