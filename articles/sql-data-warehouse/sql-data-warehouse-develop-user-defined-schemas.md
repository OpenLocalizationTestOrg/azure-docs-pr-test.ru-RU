---
title: "определенные aaaUser схемы в хранилище данных SQL | Документы Microsoft"
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
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="74355-103">Определяемые пользователем схемы в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="74355-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="74355-104">Традиционных хранилищах данных часто используйте отдельные базы данных toocreate границы приложения на основе рабочей нагрузки, домена или безопасности.</span><span class="sxs-lookup"><span data-stu-id="74355-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="74355-105">Например, традиционное хранилище данных SQL Server может включать в себя промежуточную базу данных, базу данных хранилища данных и базы данных киоска данных.</span><span class="sxs-lookup"><span data-stu-id="74355-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="74355-106">В этой топологии каждая база данных работает в качестве рабочей нагрузки и границы безопасности в архитектуре hello.</span><span class="sxs-lookup"><span data-stu-id="74355-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="74355-107">В отличие от этого хранилище данных SQL выполняется hello нагрузку хранилища данных в одной базе данных.</span><span class="sxs-lookup"><span data-stu-id="74355-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="74355-108">Кроссплатформенные соединения баз данных не допускаются.</span><span class="sxs-lookup"><span data-stu-id="74355-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="74355-109">Поэтому хранилище данных SQL ожидает, что все таблицы, используемые toobe хранилища hello, хранятся в одной базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="74355-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="74355-110">Хранилище данных SQL не поддерживает какие-либо перекрестные запросы к базам данных.</span><span class="sxs-lookup"><span data-stu-id="74355-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="74355-111">В результате реализации хранилища данных, использующие этот шаблон потребуется toobe внес изменения.</span><span class="sxs-lookup"><span data-stu-id="74355-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="74355-112">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="74355-112">Recommendations</span></span>
<span data-ttu-id="74355-113">Ниже приведены рекомендации по консолидации границ рабочих нагрузок, безопасности, домена и функциональных границы с помощью определяемых пользователем схем.</span><span class="sxs-lookup"><span data-stu-id="74355-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="74355-114">Использовать один toorun базы данных хранилища данных SQL рабочей нагрузке хранилища данных</span><span class="sxs-lookup"><span data-stu-id="74355-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="74355-115">Консолидация вашей существующей среды toouse одно хранилище данных SQL базы данных хранилища данных</span><span class="sxs-lookup"><span data-stu-id="74355-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="74355-116">Использование **пользовательских схем** границ hello tooprovide ранее реализовано с помощью базы данных.</span><span class="sxs-lookup"><span data-stu-id="74355-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="74355-117">Если ранее определяемые пользователем схемы не использовалось, следует начать с нуля.</span><span class="sxs-lookup"><span data-stu-id="74355-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="74355-118">Для пользовательских схем в базе данных хранилища данных SQL hello просто используйте hello старое имя базы данных в качестве основы hello.</span><span class="sxs-lookup"><span data-stu-id="74355-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="74355-119">Если же схемы уже использовались, у вас несколько вариантов:</span><span class="sxs-lookup"><span data-stu-id="74355-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="74355-120">Удалите имена прежних версий схем hello и начать заново</span><span class="sxs-lookup"><span data-stu-id="74355-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="74355-121">Сохранить имена hello прежних версий схем по имени таблицы toohello имя прежних версий схемы предварительно ожидающие hello</span><span class="sxs-lookup"><span data-stu-id="74355-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="74355-122">Сохранить имена прежних версий схем hello путем реализации представления над таблицей hello в дополнительных схем toore-создать hello старую структуру схемы.</span><span class="sxs-lookup"><span data-stu-id="74355-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="74355-123">На первой проверки вариант 3 может показаться наиболее привлекательный параметр hello.</span><span class="sxs-lookup"><span data-stu-id="74355-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="74355-124">Однако hello devil будет подробно hello.</span><span class="sxs-lookup"><span data-stu-id="74355-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="74355-125">Представления в хранилище данных SQL доступны только для чтения.</span><span class="sxs-lookup"><span data-stu-id="74355-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="74355-126">Любые изменения данных или таблицы, должны toobe, выполняются для hello базовой таблицы.</span><span class="sxs-lookup"><span data-stu-id="74355-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="74355-127">Кроме того, вариант 3 добавляет в систему уровень представлений.</span><span class="sxs-lookup"><span data-stu-id="74355-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="74355-128">Может потребоваться toogive этого некоторые дополнительные размышления при использовании представления в архитектуре уже.</span><span class="sxs-lookup"><span data-stu-id="74355-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="74355-129">Примеры:</span><span class="sxs-lookup"><span data-stu-id="74355-129">Examples:</span></span>
<span data-ttu-id="74355-130">Реализация определяемых пользователем схем на основе имен баз данных</span><span class="sxs-lookup"><span data-stu-id="74355-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="74355-131">Сохранить прежних версий схемы назначает путем предварительно ожидающие их toohello имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="74355-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="74355-132">Используйте схемы для границ hello рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="74355-132">Use schemas for hello workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="74355-133">Сохранение прежних имен схем с помощью представлений</span><span class="sxs-lookup"><span data-stu-id="74355-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="74355-134">Любое изменение в стратегии схемы должен ознакомиться с моделью безопасности hello для hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="74355-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="74355-135">Во многих случаях может быть модель безопасности может toosimplify hello путем назначения разрешений на уровне схемы hello.</span><span class="sxs-lookup"><span data-stu-id="74355-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="74355-136">Если требуются более детализированные разрешения, можно использовать роли базы данных.</span><span class="sxs-lookup"><span data-stu-id="74355-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="74355-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="74355-137">Next steps</span></span>
<span data-ttu-id="74355-138">Дополнительные советы по разработке см. в статье [Проектные решения и методики программирования для хранилища данных SQL][development overview].</span><span class="sxs-lookup"><span data-stu-id="74355-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
