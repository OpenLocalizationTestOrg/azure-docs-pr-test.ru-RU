---
title: "aaaPause, возобновить, масштабирования с помощью T-SQL в хранилище данных SQL Azure | Документы Microsoft"
description: "Transact-SQL (T-SQL) задачи tooscale производительности путем настройки Dwu. Сокращение затрат путем свертывания ресурсов в периоды низкой загрузки."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: 84c6868acb673221d8853319ac9a05bb98b2b7c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a>Управление вычислительными ресурсами в хранилище данных SQL (T-SQL)
> [!div class="op_single_selector"]
> * [Обзор](sql-data-warehouse-manage-compute-overview.md)
> * [Портал](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a>для просмотра текущих параметров DWU;
tooview hello текущие DWU параметры для баз данных:

1. Откройте обозреватель объектов SQL Server в Visual Studio.
2. Подключение базы данных master toohello, связанные с сервером базы данных SQL логические hello.
3. Выберите из динамического административного представления sys.database_service_objectives hello. Пример: 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Масштабирование вычислительных ресурсов
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

hello toochange Dwu:

1. Подключение базы данных master toohello, связанный с логической базы данных SQL server.
2. Используйте hello [инструкции ALTER DATABASE] [ ALTER DATABASE] инструкции t-SQL. Hello следующий пример устанавливает hello службы уровня цели tooDW1000 для базы данных hello MySQLDW. 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a>Проверка состояния базы данных и хода выполнения операции

1. Подключение базы данных master toohello, связанный с логической базы данных SQL server.
2. Отправить запрос о состоянии toocheck базы данных

```sql
SELECT *
FROM
sys.databases
```

3. Отправить запрос toocheck состояние операции

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

Это динамическое административное Представление возвращает сведения о различных операций управления на хранилище данных SQL как hello операции и hello состояние операции hello, который будет IN_PROGRESS или ЗАВЕРШЕНА.



<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Дальнейшие действия
Сведения о других задачах управления см. в статье [Управление базами данных в хранилище данных SQL Azure][Management overview].

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
