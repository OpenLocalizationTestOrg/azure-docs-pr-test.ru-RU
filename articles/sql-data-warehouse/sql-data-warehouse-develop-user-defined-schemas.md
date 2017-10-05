---
title: "Определяемые пользователем схемы в хранилище данных SQL | Документация Майкрософт"
description: "Советы по использованию схем Transact-SQL в хранилище данных SQL Azure для разработки решений."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: dfb58956ad6637cf0f50b4c052ab98fb7c26139d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="16890-103">Определяемые пользователем схемы в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="16890-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="16890-104">В традиционных хранилищах данных часто используются отдельные базы данных, чтобы создать границы приложений на основе рабочей нагрузки, домену или безопасности.</span><span class="sxs-lookup"><span data-stu-id="16890-104">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="16890-105">Например, традиционное хранилище данных SQL Server может включать в себя промежуточную базу данных, базу данных хранилища данных и базы данных киоска данных.</span><span class="sxs-lookup"><span data-stu-id="16890-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="16890-106">В этой топологии каждая база данных работает как рабочая нагрузка и граница безопасности в архитектуре.</span><span class="sxs-lookup"><span data-stu-id="16890-106">In this topology each database operates as a workload and security boundary in the architecture.</span></span>

<span data-ttu-id="16890-107">Напротив, хранилище данных SQL выполняет всю рабочую нагрузку хранилища данных в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="16890-107">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="16890-108">Кроссплатформенные соединения баз данных не допускаются.</span><span class="sxs-lookup"><span data-stu-id="16890-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="16890-109">Поэтому хранилище данных SQL ожидает, что все таблицы, используемые в хранилище, должны храниться в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="16890-109">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span></span>

> [!NOTE]
> <span data-ttu-id="16890-110">Хранилище данных SQL не поддерживает какие-либо перекрестные запросы к базам данных.</span><span class="sxs-lookup"><span data-stu-id="16890-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="16890-111">Следовательно, реализации хранилища данных, использующих этот шаблон, будет необходимо пересмотреть.</span><span class="sxs-lookup"><span data-stu-id="16890-111">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="16890-112">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="16890-112">Recommendations</span></span>
<span data-ttu-id="16890-113">Ниже приведены рекомендации по консолидации границ рабочих нагрузок, безопасности, домена и функциональных границы с помощью определяемых пользователем схем.</span><span class="sxs-lookup"><span data-stu-id="16890-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="16890-114">Используйте одну базу данных хранилища данных SQL для выполнения рабочей нагрузки хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="16890-114">Use one SQL Data Warehouse database to run your entire data warehouse workload</span></span>
2. <span data-ttu-id="16890-115">Объедините существующую среду хранилища данных, чтобы использовать одну базу данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="16890-115">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="16890-116">Используйте **определяемые пользователем схемы** , чтобы создать границы, ранее реализуемые с помощью баз данных.</span><span class="sxs-lookup"><span data-stu-id="16890-116">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span></span>

<span data-ttu-id="16890-117">Если ранее определяемые пользователем схемы не использовалось, следует начать с нуля.</span><span class="sxs-lookup"><span data-stu-id="16890-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="16890-118">Просто используйте старое имя базы данных в определяемых пользователем схемах в базе данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="16890-118">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span></span>

<span data-ttu-id="16890-119">Если же схемы уже использовались, у вас несколько вариантов:</span><span class="sxs-lookup"><span data-stu-id="16890-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="16890-120">Удалить прежние имена схем и создать новые.</span><span class="sxs-lookup"><span data-stu-id="16890-120">Remove the legacy schema names and start fresh</span></span>
2. <span data-ttu-id="16890-121">Сохранить прежние имена схем, добавляя прежнее имя схемы в начало имени таблицы.</span><span class="sxs-lookup"><span data-stu-id="16890-121">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span></span>
3. <span data-ttu-id="16890-122">Сохранить прежние имена схем, реализовав представления таблицы в дополнительной схеме, чтобы воссоздать старую структуру схемы.</span><span class="sxs-lookup"><span data-stu-id="16890-122">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="16890-123">На первый взгляд вариант 3 может показаться наиболее привлекательным.</span><span class="sxs-lookup"><span data-stu-id="16890-123">On first inspection option 3 may seem like the most appealing option.</span></span> <span data-ttu-id="16890-124">Однако черт прячется в деталях.</span><span class="sxs-lookup"><span data-stu-id="16890-124">However, the devil is in the detail.</span></span> <span data-ttu-id="16890-125">Представления в хранилище данных SQL доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="16890-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="16890-126">Любое изменение данных или таблицы потребуется выполнять в базовой таблице.</span><span class="sxs-lookup"><span data-stu-id="16890-126">Any data or table modification would need to be performed against the base table.</span></span> <span data-ttu-id="16890-127">Кроме того, вариант 3 добавляет в систему уровень представлений.</span><span class="sxs-lookup"><span data-stu-id="16890-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="16890-128">Вы можете обдумать это, если в вашей архитектуре уже используются представления.</span><span class="sxs-lookup"><span data-stu-id="16890-128">You might want to give this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="16890-129">Примеры:</span><span class="sxs-lookup"><span data-stu-id="16890-129">Examples:</span></span>
<span data-ttu-id="16890-130">Реализация определяемых пользователем схем на основе имен баз данных</span><span class="sxs-lookup"><span data-stu-id="16890-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for the data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in the stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in the edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="16890-131">Сохраните прежние имена схем, добавляя их в начало имени таблицы.</span><span class="sxs-lookup"><span data-stu-id="16890-131">Retain legacy schema names by pre-pending them to the table name.</span></span> <span data-ttu-id="16890-132">Используйте схемы для создания границы рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="16890-132">Use schemas for the workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines the data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend the old schema name to the table and create in the staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend the old schema name to the table and create in the data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="16890-133">Сохранение прежних имен схем с помощью представлений</span><span class="sxs-lookup"><span data-stu-id="16890-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines the data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines the legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create the base staging tables in the staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create the base data warehouse tables in the data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in the legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="16890-134">Любое изменение в стратегии схем влечет за собой пересмотр модели безопасности базы данных.</span><span class="sxs-lookup"><span data-stu-id="16890-134">Any change in schema strategy needs a review of the security model for the database.</span></span> <span data-ttu-id="16890-135">Во многих случаях можно упростить модель безопасности, назначая разрешения на уровне схем.</span><span class="sxs-lookup"><span data-stu-id="16890-135">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span></span> <span data-ttu-id="16890-136">Если требуются более детализированные разрешения, можно использовать роли базы данных.</span><span class="sxs-lookup"><span data-stu-id="16890-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="16890-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16890-137">Next steps</span></span>
<span data-ttu-id="16890-138">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="16890-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
