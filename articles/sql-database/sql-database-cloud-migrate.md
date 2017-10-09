---
title: "aaaSQL сервера базы данных миграции tooAzure базы данных SQL | Документы Microsoft"
description: "Дополнительные сведения о том, как миграции базы данных SQL Server tooAzure базы данных SQL в облаке hello. Используйте базу данных миграции средства tootest совместимости предыдущих toodatabase миграцию."
keywords: "миграция базы данных, миграция базы данных SQL Server, средства миграции базы данных, миграция базы данных, миграция базы данных SQL"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>TooSQL миграции базы данных SQL Server базы данных в облаке hello
В этой статье вы узнаете о hello два основных способа проведения миграции SQL Server 2005 или более поздней версии базы данных tooAzure базы данных SQL. Hello первый метод проще, но требуется в некоторых случаях, возможно значительное время простоя во время миграции hello. Второй метод Hello сложнее, но существенно исключает время простоя во время миграции hello.

В обоих случаях необходимо tooensure базы данных-источника, hello совместим с базой данных SQL Azure с помощью hello [данных помощник по миграции (DMA)](https://www.microsoft.com/download/details.aspx?id=53595). Приближается к базе данных SQL V12 [сходные функции](sql-database-features.md) с SQL Server, отличных от операций уровня tooserver и межбазовые связанные проблемы. Базы данных и приложения, зависящие от [частично поддерживаемые и неподдерживаемые функции](sql-database-transact-sql-information.md) требуются некоторые [перепроектирования toofix этих несовместимостей](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues) перед hello SQL Server можно выполнить миграцию базы данных.

> [!NOTE]
> базы данных SQL Server, включая Microsoft Access, Sybase, Oracle, MySQL и tooAzure DB2 база данных SQL, в разделе toomigrate [SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/).
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Метод 1: Миграция с временем простоя во время миграции hello

 Используйте этот метод, если вы можете позволить себе некоторое время простоя или выполняете тестовую миграцию рабочей базы данных для последующей полноценной миграции. Руководство см. в статье [Migrate a SQL Server database](sql-database-migrate-your-sql-server-database.md) (Миграция базы данных SQL Server).

Hello следующий список содержит hello общий рабочий процесс для миграции базы данных SQL Server с помощью этого метода.

  ![Схема переноса VSSSDT](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. Оценка hello базы данных для совместимости с помощью hello последнюю версию [данных помощник по миграции (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).
2. Подготовьте все необходимые исправления в виде скриптов Transact-SQL.
3. Сделать транзакционно согласованной копии базы данных-источника hello переносимым - и убедитесь, никаких изменений были сделаны toohello базы данных-источника (или любых подобных изменений можно вручную применить после завершения миграции hello). Существует множество методов tooquiesce базы данных, отключить toocreating подключения клиента [моментальный снимок базы данных](https://msdn.microsoft.com/library/ms175876.aspx).
4. Разверните сценарии hello Transact-SQL tooapply исправления hello toohello копию базы данных.
5. [Экспорт](sql-database-export.md) hello tooa копии базы данных. BACPAC-файл на локальный диск.
6. [Импорт](sql-database-import.md) hello. Средства, импортировать файл BACPAC в качестве новой базы данных Azure SQL, с помощью любого из нескольких BACPAC с SQLPackage.exe, средство для достижения оптимальной производительности рекомендуется hello.

### <a name="optimizing-data-transfer-performance-during-migration"></a>Оптимизация производительности передачи данных во время миграции 

После списка Hello содержит рекомендации для повышения производительности во время процесса импорта hello.

* Выберите hello наивысший уровень обслуживания и производительности уровня, что бюджет позволяет производительности передачи toomaximize hello. Можно масштабировать после завершения миграции hello toosave money. 
* Свести к минимуму hello расстояние между вашей. BACPAC файл и hello целевой центр обработки данных.
* Отключите автоматическую статистику во время миграции.
* Выполните секционирование таблиц и индексов.
* Удалите индексированные представления и заново создайте их по завершении миграции.
* Удаление базы данных tooanother редко запрашиваемые данные журнала и перенести этот исторические данные tooa отдельной базы данных Azure SQL. Затем вы сможете запросить эти данные с помощью [эластичных запросов](sql-database-elastic-query-overview.md).

### <a name="optimize-performance-after-hello-migration-completes"></a>Оптимизация производительности после завершения миграции hello

[Обновить статистику](https://msdn.microsoft.com/library/ms187348.aspx) с полную проверку после завершения миграции hello.

## <a name="method-2-use-transactional-replication"></a>Метод 2. Использование репликации транзакций

Если во время миграции hello не может допустить tooremove базу данных SQL из рабочей среды, репликация транзакций SQL Server может служить миграции решения. toouse, этот метод hello базы данных-источника необходимо соответствует hello [требования для репликации транзакций](https://msdn.microsoft.com/library/mt589530.aspx) и совместимости для базы данных SQL Azure. См. дополнительные сведения о [настройке репликации для групп доступности AlwaysOn (SQL Server)](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server).

toouse это решение настройке базы данных SQL Azure как обратиться в toomigrate экземпляр SQL Server toohello подписчика. Hello распространителя репликации транзакций синхронизирует данные из синхронизации toobe базы данных hello (hello издатель) прерывая возникают новые транзакции. 

В случае репликации транзакций все изменения tooyour данных или схемы отображаются в базе данных SQL Azure. После завершения синхронизации hello и будут готовы toomigrate изменить строку подключения hello из вашего приложения toopoint их tooyour базы данных SQL Azure. После репликации транзакций очищает все изменения влево на базы данных-источника и во всех приложениях точка tooAzure DB, можно удалить репликацию транзакций. База данных SQL Azure теперь является рабочей системой.

 ![Диаграмма SeedCloudTR](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> Также можно использовать репликацию транзакций toomigrate подмножество базы данных-источника. Hello публикации репликации tooAzure базы данных SQL может быть tooa ограниченное подмножество таблиц hello в реплицируемой базы данных hello. Для каждой таблицы реплицируются можно ограничить hello данных tooa подмножества строк hello и/или подмножество столбцов hello.
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>TooSQL миграции базы данных с помощью репликации транзакций рабочего процесса

> [!IMPORTANT]
> Используйте hello последнюю версию SQL Server Management Studio tooremain синхронизированы с tooMicrosoft обновления Azure и базы данных SQL. Более старые версии SQL Server Management Studio не позволяют настроить Базу данных SQL как подписчика. [Обновите среду SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 

1. Настройка распространения
   -  [С помощью SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1).
   -  [С помощью Transact-SQL](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2).
2. Создание публикации
   -  [С помощью SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1).
   -  [С помощью Transact-SQL](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2).
3. Создание подписки
   -  [С помощью SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0).
   -  [С помощью Transact-SQL](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1).

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>Некоторые советы и различия по переносу tooSQL базы данных

1. Использование локального распространителя 
   - Это приводит к снижению производительности на сервере hello. 
   - Влияние на производительность hello это неприемлемо, можно использовать другой сервер, но увеличения сложности управления и администрирования.
2. При выборе папки моментальных снимков, убедитесь, что hello папка находится достаточно большой toohold BCP всех таблиц нужно tooreplicate. 
3. Блокировки создания моментального снимка hello связанных таблиц до завершения, поэтому соответствующим образом запланировать моментальный снимок. 
4. В базе данных SQL Azure поддерживаются только принудительные подписки. Подписчикам можно добавить только из базы данных-источника hello.

## <a name="resolving-database-migration-compatibility-issues"></a>Устранение проблем совместимости при миграции базы данных
Существует широкий спектр проблем совместимости, которые могут возникнуть, в зависимости от обоих hello версии SQL Server в hello исходной базы данных и hello сложности hello базы данных которого выполняется миграция. В более старых версиях SQL Server имеются дополнительные проблемы совместимости. Используйте следующие ресурсы hello, кроме tooa целевые поиск в Интернете с помощью поисковой системе вариантов:

* [Функции базы данных SQL Server, которые не поддерживаются в базе данных SQL Azure](sql-database-transact-sql-information.md)
* [Неподдерживаемые функции ядра СУБД в SQL Server 2016](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [Неподдерживаемые функции ядра СУБД в SQL Server 2014](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [Неподдерживаемые функции ядра СУБД в SQL Server 2012](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [Неподдерживаемые функции ядра СУБД в SQL Server 2008 R2](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [Неподдерживаемые функции ядра СУБД в SQL Server 2005](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

Кроме toosearching hello Интернет и использование этих ресурсов используйте hello [форумы MSDN SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver) или [StackOverflow](http://stackoverflow.com/).

## <a name="next-steps"></a>Дальнейшие действия
* Использовать сценарий hello блог инженеров EMEA SQL Azure hello слишком[наблюдения за использованием базы данных tempdb во время миграции](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/).
* Использовать сценарий hello блог инженеров EMEA SQL Azure hello слишком[отслеживать hello место в журнале транзакций базы данных во время миграции](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0).
* SQL Server группа консультантов по блог о миграции с помощью BACPAC-файлов в разделе [миграции с SQL Server tooAzure базы данных SQL с помощью файлов BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Сведения о работе с временем UTC после миграции см. в разделе [Изменение часового пояса hello по умолчанию для вашего часового пояса](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/).
* Сведения об изменении языка по умолчанию hello базы данных после миграции см. в разделе [как toochange hello язык по умолчанию для базы данных SQL Azure](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/).


