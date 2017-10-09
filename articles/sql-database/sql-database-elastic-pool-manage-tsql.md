---
title: "T-SQL: управление пулом эластичных баз данных SQL Azure | Документация Майкрософт"
description: "С помощью T-SQL toomanage пул эластичных баз данных SQL Azure."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>Мониторинг пула эластичных баз данных и управление им с помощью Transact-SQL
В этом разделе показано, как масштабируемой toomanage [эластичные пулы](sql-database-elastic-pool.md) с помощью Transact-SQL.  Можно также создать и управлять hello Azure эластичного пула [портал Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API или [C#](sql-database-elastic-pool-manage-csharp.md). Вы также можете использовать [Transact-SQL](sql-database-elastic-pool-manage-tsql.md), чтобы создавать новые базы данных в эластичных пулах и перемещать базы данных в пулы и обратно.


Используйте hello [Create Database (база данных SQL Azure)](https://msdn.microsoft.com/library/dn268335.aspx) и [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) команды toocreate и перемещения баз данных в действие и из эластичные пулы. Hello эластичного пула должен существовать, прежде чем использовать эти команды. Эти команды влияют только на базы данных. Создание новых групп и приветствия свойств пула (например, min и max Edtu) нельзя изменить с помощью команды T-SQL.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Создание базы данных внутри эластичного пула
Команда CREATE DATABASE hello с hello SERVICE_OBJECTIVE параметр.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Все базы данных в пуле эластичных наследуют уровень обслуживания hello hello эластичного пула (Basic, Standard, Premium). 

## <a name="move-a-database-between-elastic-pools"></a>Перемещение базы данных между пулами эластичных БД
Используйте команду ALTER DATABASE hello с hello изменить и настроить службу\_цели параметр как ГИБКОМУ\_ПУЛА. Задайте имя toohello имя hello hello целевого пула.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Перемещение базы данных в пул эластичных БД
Используйте команду ALTER DATABASE hello с hello изменить и настроить службу\_цели параметр как ELASTIC_POOL. Задайте имя toohello имя hello hello целевого пула.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Перемещение базы данных из пула эластичных БД
Используйте команду ALTER DATABASE hello и установите tooone SERVICE_OBJECTIVE hello hello уровней производительности (например S0 или S1).

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Получение списка баз данных в пуле эластичных БД
Используйте hello [sys.database\_службы \_целей представление](https://msdn.microsoft.com/library/mt712619) toolist все hello баз данных в пуле эластичных БД. Войдите в базе данных master toohello представление hello tooquery базы данных.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Получение данных об использовании ресурсов в эластичном пуле
Используйте hello [sys.elastic\_пула \_ресурсов \_представление stats](https://msdn.microsoft.com/library/mt280062.aspx) tooexamine hello Статистика использования ресурсов для эластичного пула на логическом сервере. Войдите в базе данных master toohello представление hello tooquery базы данных.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Получение данных об использовании ресурсов в базе данных, которая находится в пуле
Используйте hello [sys.dm\_ db\_ ресурсов\_stats представление](https://msdn.microsoft.com/library/dn800981.aspx) или [sys.resource \_представление stats](https://msdn.microsoft.com/library/dn269979.aspx) Статистика использования ресурсов tooexamine hello объекта База данных в пуле эластичных БД. Этот процесс является аналогичные использования tooquerying ресурсов для одной базы данных.

## <a name="next-steps"></a>Дальнейшие действия
После создания эластичного пула, можно управлять путем создания эластичной заданий эластичных баз данных в пуле hello. Эластичный заданий облегчают выполнение скриптов T-SQL для любого количества баз данных в пуле hello. Дополнительные сведения можно узнать в статье [Обзор службы заданий эластичной базы данных](sql-database-elastic-jobs-overview.md). 

В разделе [горизонтального масштабирования с базой данных SQL Azure](sql-database-elastic-scale-introduction.md): использовать эластичной базы данных средства tooscale out, перемещение данных, запроса или создания транзакции.

