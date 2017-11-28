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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="095dc-104">Управление вычислительными ресурсами в хранилище данных SQL (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="095dc-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="095dc-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="095dc-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="095dc-106">Портал</span><span class="sxs-lookup"><span data-stu-id="095dc-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="095dc-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="095dc-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="095dc-108">REST</span><span class="sxs-lookup"><span data-stu-id="095dc-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="095dc-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="095dc-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="095dc-110">для просмотра текущих параметров DWU;</span><span class="sxs-lookup"><span data-stu-id="095dc-110">View current DWU settings</span></span>
<span data-ttu-id="095dc-111">tooview hello текущие DWU параметры для баз данных:</span><span class="sxs-lookup"><span data-stu-id="095dc-111">tooview hello current DWU settings for your databases:</span></span>

1. <span data-ttu-id="095dc-112">Откройте обозреватель объектов SQL Server в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="095dc-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="095dc-113">Подключение базы данных master toohello, связанные с сервером базы данных SQL логические hello.</span><span class="sxs-lookup"><span data-stu-id="095dc-113">Connect toohello master database associated with hello logical SQL Database server.</span></span>
3. <span data-ttu-id="095dc-114">Выберите из динамического административного представления sys.database_service_objectives hello.</span><span class="sxs-lookup"><span data-stu-id="095dc-114">Select from hello sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="095dc-115">Пример:</span><span class="sxs-lookup"><span data-stu-id="095dc-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="095dc-116">Масштабирование вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="095dc-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="095dc-117">hello toochange Dwu:</span><span class="sxs-lookup"><span data-stu-id="095dc-117">toochange hello DWUs:</span></span>

1. <span data-ttu-id="095dc-118">Подключение базы данных master toohello, связанный с логической базы данных SQL server.</span><span class="sxs-lookup"><span data-stu-id="095dc-118">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="095dc-119">Используйте hello [инструкции ALTER DATABASE] [ ALTER DATABASE] инструкции t-SQL.</span><span class="sxs-lookup"><span data-stu-id="095dc-119">Use hello [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="095dc-120">Hello следующий пример устанавливает hello службы уровня цели tooDW1000 для базы данных hello MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="095dc-120">hello following example sets hello service level objective tooDW1000 for hello database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="095dc-121">Проверка состояния базы данных и хода выполнения операции</span><span class="sxs-lookup"><span data-stu-id="095dc-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="095dc-122">Подключение базы данных master toohello, связанный с логической базы данных SQL server.</span><span class="sxs-lookup"><span data-stu-id="095dc-122">Connect toohello master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="095dc-123">Отправить запрос о состоянии toocheck базы данных</span><span class="sxs-lookup"><span data-stu-id="095dc-123">Submit query toocheck database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="095dc-124">Отправить запрос toocheck состояние операции</span><span class="sxs-lookup"><span data-stu-id="095dc-124">Submit query toocheck status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="095dc-125">Это динамическое административное Представление возвращает сведения о различных операций управления на хранилище данных SQL как hello операции и hello состояние операции hello, который будет IN_PROGRESS или ЗАВЕРШЕНА.</span><span class="sxs-lookup"><span data-stu-id="095dc-125">This DMV will return information about various management operations on your SQL Data Warehouse such as hello operation and hello state of hello operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="095dc-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="095dc-126">Next steps</span></span>
<span data-ttu-id="095dc-127">Сведения о других задачах управления см. в статье [Управление базами данных в хранилище данных SQL Azure][Management overview].</span><span class="sxs-lookup"><span data-stu-id="095dc-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
