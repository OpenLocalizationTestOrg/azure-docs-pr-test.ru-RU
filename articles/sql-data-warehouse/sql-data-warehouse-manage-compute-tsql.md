---
title: "Приостановка, возобновление и масштабирование ресурсов в хранилище данных SQL Azure с помощью T-SQL | Документация Майкрософт"
description: "Задачи Transact-SQL (T-SQL) для масштабирования производительности путем изменения числа единиц DWU. Сокращение затрат путем свертывания ресурсов в периоды низкой загрузки."
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
ms.openlocfilehash: 9221d72ecf8ab2ba8b04e4bc97eeef7157817cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="2208f-104">Управление вычислительными ресурсами в хранилище данных SQL (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="2208f-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2208f-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="2208f-105">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="2208f-106">Портал</span><span class="sxs-lookup"><span data-stu-id="2208f-106">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="2208f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2208f-107">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="2208f-108">REST</span><span class="sxs-lookup"><span data-stu-id="2208f-108">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="2208f-109">TSQL</span><span class="sxs-lookup"><span data-stu-id="2208f-109">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="2208f-110">для просмотра текущих параметров DWU;</span><span class="sxs-lookup"><span data-stu-id="2208f-110">View current DWU settings</span></span>
<span data-ttu-id="2208f-111">Для просмотра текущих параметров DWU для своих баз данных:</span><span class="sxs-lookup"><span data-stu-id="2208f-111">To view the current DWU settings for your databases:</span></span>

1. <span data-ttu-id="2208f-112">Откройте обозреватель объектов SQL Server в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2208f-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="2208f-113">Подключитесь к базе данных master, связанной с логическим сервером базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="2208f-113">Connect to the master database associated with the logical SQL Database server.</span></span>
3. <span data-ttu-id="2208f-114">Выберите в sys.database_service_objectives динамическое административное представление.</span><span class="sxs-lookup"><span data-stu-id="2208f-114">Select from the sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="2208f-115">Пример:</span><span class="sxs-lookup"><span data-stu-id="2208f-115">Here is an example:</span></span> 

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

## <a name="scale-compute"></a><span data-ttu-id="2208f-116">Масштабирование вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="2208f-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="2208f-117">Изменение DWU:</span><span class="sxs-lookup"><span data-stu-id="2208f-117">To change the DWUs:</span></span>

1. <span data-ttu-id="2208f-118">Подключитесь к базе данных master, связанной с логическим сервером базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="2208f-118">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="2208f-119">Используйте оператор TSQL [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="2208f-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="2208f-120">В приведенном ниже примере для базы данных MySQLDW устанавливается цель уровня обслуживания DW1000.</span><span class="sxs-lookup"><span data-stu-id="2208f-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="2208f-121">Проверка состояния базы данных и хода выполнения операции</span><span class="sxs-lookup"><span data-stu-id="2208f-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="2208f-122">Подключитесь к базе данных master, связанной с логическим сервером базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="2208f-122">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="2208f-123">Отправьте запрос для проверки состояния базы данных.</span><span class="sxs-lookup"><span data-stu-id="2208f-123">Submit query to check database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="2208f-124">Отправьте запрос для проверки состояния операции.</span><span class="sxs-lookup"><span data-stu-id="2208f-124">Submit query to check status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="2208f-125">Это динамическое административное представление возвращает сведения о различных операциях управления хранилищем данных SQL, такие как операция и ее состояние, которое будет иметь значение IN_PROGRESS или COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="2208f-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="2208f-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2208f-126">Next steps</span></span>
<span data-ttu-id="2208f-127">Сведения о других задачах управления см. в статье [Управление базами данных в хранилище данных SQL Azure][Management overview].</span><span class="sxs-lookup"><span data-stu-id="2208f-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
