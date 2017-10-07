---
title: "aaaConfigure георепликация для базы данных SQL Azure с помощью Transact-SQL | Документы Microsoft"
description: "Настройка георепликации базы данных SQL Azure с помощью Transact-SQL."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Настройка активной георепликации базы данных SQL Azure с помощью Transact-SQL

В этой статье показано, как tooconfigure активной георепликации для базы данных SQL Azure с помощью Transact-SQL.

tooinitiate отработки отказа, с помощью Transact-SQL, в разделе [инициации плановой или незапланированной отработки отказа для базы данных SQL Azure с помощью Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> При использовании активной георепликации (получателей для чтения) для аварийного восстановления следует настроить группу отработки отказа для всех баз данных в приложение tooenable автоматический, так и прозрачный переход на другой ресурс. Эта функция предоставляется в предварительной версии. Дополнительные сведения см. в статье [Обзор. Группы отработки отказа и активная георепликация](sql-database-geo-replication-overview.md).
> 
> 

tooconfigure активной георепликации с помощью Transact-SQL, необходимо hello следующее:

* Подписка Azure
* Логический сервер базы данных SQL Azure <MyLocalServer> и базы данных SQL <MyDB> -hello базы данных-источника, которые должны tooreplicate
* Один или несколько логических баз данных SQL Azure серверов < MySecondaryServer(n) > - hello логических серверов, которые будут серверами-партнерами hello, в которых вы создадите баз данных-получателей
* Имя входа, которое является DBManager на основной hello
* У db_ownership hello локальной базы данных, что вы будете репликации
* Быть DBManager на серверы toowhich hello партнера вы настроите географической репликации
* Новейшая версия Hello объекта SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> Рекомендуется всегда использовать hello последнюю версию среды Management Studio tooremain синхронизированы с tooMicrosoft обновления Azure и базы данных SQL. [Обновите среду SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>Добавление базы данных-получателя
Можно использовать hello **инструкции ALTER DATABASE** toocreate инструкции географическая репликация базы данных-получателя на сервере-партнере. Эта инструкция выполняется на hello базы данных master hello server содержащего hello базы данных toobe репликации. Hello географическая репликация базы данных (hello «основной базы данных») будут иметь одинаковые имена, как hello реплицируемой базы данных и будет по умолчанию имеют hello hello базы данных-источника hello же уровне службы. Hello баз данных-получателей может быть доступной для чтения или недоступную для чтения и может быть одной базы данных или в пуле эластичных БД. Дополнительные сведения см. в статьях [ALTER DATABASE (база данных SQL Azure)](https://msdn.microsoft.com/library/mt574871.aspx) и [Уровни служб базы данных SQL для отдельных баз данных и пулов эластичных баз данных](sql-database-service-tiers.md).
После создания и заполнения базы данных-получателя hello, данных, начнут репликацию асинхронно из базы данных-источника hello. Приведенные ниже действия Hello как tooconfigure географическую репликацию данных в среде Management Studio. Действия toocreate недоступного для чтения и для чтения вторичные реплики, предоставляются как одной базы данных или в пуле эластичных БД.

> [!NOTE]
> Если база данных существует на сервере, указанный партнер hello hello точно такое же имя, как команда hello hello базы данных-источника не будет выполнена.
> 

### <a name="add-readable-secondary-single-database"></a>Добавление доступной для чтения отдельной базы данных-получателя
Используйте hello, выполнив шаги toocreate вторичной как одной базы данных.

1. В среде Management Studio подключитесь логический сервер tooyour базы данных SQL Azure.
2. Откройте папку баз данных hello, разверните узел hello **системных баз данных** папку, щелкните правой кнопкой мыши **master**и нажмите кнопку **новый запрос**.
3. Используйте следующие hello **инструкции ALTER DATABASE** toomake инструкции локальной базы данных в основной географической репликации с для чтения базы данных-получателя на сервере-получателе.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Нажмите кнопку **Execute** toorun hello запроса.

### <a name="add-readable-secondary-elastic-pool"></a>Добавление доступной для чтения базы данных-получателя (в пуле эластичных баз данных)
Используйте следующие шаги toocreate вторичной в пуле эластичных hello.

1. В среде Management Studio подключитесь логический сервер tooyour базы данных SQL Azure.
2. Откройте папку баз данных hello, разверните узел hello **системных баз данных** папку, щелкните правой кнопкой мыши **master**и нажмите кнопку **новый запрос**.
3. На следующих hello **инструкции ALTER DATABASE** toomake инструкции локальной базы данных в основной географической репликации с для чтения базы данных-получателя на сервере-получателе в пуле эластичных БД.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Нажмите кнопку **Execute** toorun hello запроса.

## <a name="remove-secondary-database"></a>Удаление базы данных-получателя
Можно использовать hello **инструкции ALTER DATABASE** toopermanently инструкции завершить hello партнерства репликации между базы данных-получателя и основным. Эта инструкция выполняется в базе данных master hello, на какие hello находится база данных-источник. После завершения связи hello hello базу данных-получатель становится обычной базой данных чтения и записи. Если база данных toosecondary подключения hello нарушена hello команда выполняется, но hello получателей станет чтения и записи, после восстановления подключения. Дополнительные сведения см. в статьях [ALTER DATABASE (база данных SQL Azure)](https://msdn.microsoft.com/library/mt574871.aspx) и [Уровни служб базы данных SQL для отдельных баз данных и пулов эластичных баз данных](sql-database-service-tiers.md).

Используйте следующую получателя георепликацией tooremove действия из географической репликации партнерства hello.

1. В среде Management Studio подключитесь логический сервер tooyour базы данных SQL Azure.
2. Откройте папку баз данных hello, разверните узел hello **системных баз данных** папку, щелкните правой кнопкой мыши **master**и нажмите кнопку **новый запрос**.
3. Используйте следующие hello **инструкции ALTER DATABASE** получателя tooremove географически реплицируются инструкции.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Нажмите кнопку **Execute** toorun hello запроса.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Мониторинг конфигурации и работоспособности активной георепликации

Задачи наблюдения включают мониторинг конфигурации георепликации hello и наблюдение за работоспособностью репликации данных.  Можно использовать hello **sys.dm_geo_replication_links** динамическое административное представление hello базы данных master tooreturn сведения все существующие связи репликации для каждой базы данных на логическом сервере hello базы данных SQL Azure. Это представление содержит по одной строке для каждого канала репликации hello между первичной и вторичной базы данных. Можно использовать hello **sys.dm_replication_link_status** динамическому административному представлению tooreturn строку для каждой базы данных SQL Azure, которая в настоящее время участвует в репликации связи репликации. Это относится как к базам данных-источникам, так и к базам данных-получателям. Если для заданной базы данных-источника существует более одной связи с непрерывной репликацией, эта таблица содержит по одной строке для каждой из связей hello. во всех базах данных, включая hello логической базе данных master создается представление Hello. Однако запрос этого представления в базе данных master логического hello возвращает пустой набор. Можно использовать hello **sys.dm_operation_status** динамическому административному представлению tooshow hello состояние всех операций, включая состояние hello hello связей репликации базы данных. Дополнительные сведения см. в статьях [sys.geo_replication_links (база данных SQL Azure)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (база данных SQL Azure)](https://msdn.microsoft.com/library/mt575504.aspx) и [sys.dm_operation_status (база данных SQL Azure)](https://msdn.microsoft.com/library/dn270022.aspx).

Используйте следующие действия toomonitor активной георепликации сотрудничество hello.

1. В среде Management Studio подключитесь логический сервер tooyour базы данных SQL Azure.
2. Откройте папку баз данных hello, разверните узел hello **системных баз данных** папку, щелкните правой кнопкой мыши **master**и нажмите кнопку **новый запрос**.
3. Используйте следующие инструкции tooshow hello всех баз данных с связи георепликации.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Нажмите кнопку **Execute** toorun hello запроса.
5. Откройте папку баз данных hello, разверните узел hello **системных баз данных** папку, щелкните правой кнопкой мыши **MyDB**, а затем нажмите кнопку **новый запрос**.
6. Hello используйте следующие инструкции tooshow hello репликации отстает и время репликации из моей базы данных-получатели MyDB последнего.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Нажмите кнопку **Execute** toorun hello запроса.
8. Используйте следующие инструкции tooshow hello последних географической репликации операций, связанных с базы данных MyDB hello.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Нажмите кнопку **Execute** toorun hello запроса.

## <a name="next-steps"></a>Дальнейшие действия
* в разделе toolearn Дополнительные сведения о группах отработки отказа и активной георепликации - [перехода на другой ресурс группы](sql-database-geo-replication-overview.md)
* Сведения об обеспечении непрерывности бизнес-процессов и возможные сценарии описаны в [обзоре непрерывности бизнес-процессов](sql-database-business-continuity.md)

