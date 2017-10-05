---
title: "Создание хранилища данных SQL с помощью TSQL | Документация Майкрософт"
description: "Сведения о создании хранилища данных SQL Azure с помощью TSQL"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 10d8aa2b3ab8d7d8a9b91e95ffccf03faa89d237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="46f20-103">Создание базы данных хранилища данных SQL с помощью Transact-SQL (TSQL)</span><span class="sxs-lookup"><span data-stu-id="46f20-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="46f20-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="46f20-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="46f20-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="46f20-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="46f20-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="46f20-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="46f20-107">В этой статье объясняется, как создать хранилище данных SQL с помощью T-SQL.</span><span class="sxs-lookup"><span data-stu-id="46f20-107">This article shows you how to create a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46f20-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="46f20-108">Prerequisites</span></span>
<span data-ttu-id="46f20-109">Для начала работы необходимы перечисленные ниже компоненты и данные.</span><span class="sxs-lookup"><span data-stu-id="46f20-109">To get started, you need:</span></span>

* <span data-ttu-id="46f20-110">**Учетная запись Azure.** Чтобы создать учетную запись, перейдите на страницу [бесплатной пробной версии Azure][Azure Free Trial] или [денег на счете в Azure][MSDN Azure Credits] MSDN.</span><span class="sxs-lookup"><span data-stu-id="46f20-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="46f20-111">**Сервер SQL Azure**: см. раздел [создание логического сервера базы данных SQL Azure с помощью портала Azure] [создание логического сервера базы данных SQL Azure с помощью портала Azure] или [создание логического сервера базы данных SQL Azure с помощью PowerShell] [создание логического сервера базы данных SQL Azure с помощью PowerShell] для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="46f20-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with the Azure Portal][Create an Azure SQL Database logical server with the Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="46f20-112">**Группа ресурсов.** Используйте ту же группу ресурсов, что и для Azure SQL Server, или [создайте группу ресурсов][how to create a resource group].</span><span class="sxs-lookup"><span data-stu-id="46f20-112">**Resource group**: Either use the same resource group as your Azure SQL server or see [how to create a resource group][how to create a resource group].</span></span>
* <span data-ttu-id="46f20-113">**Среда выполнения T-SQL.** Для выполнения T-SQL можно использовать [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd] или [SSMS][SSMS].</span><span class="sxs-lookup"><span data-stu-id="46f20-113">**Environment to execute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] to execute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="46f20-114">Создание хранилища данных SQL может привести к дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="46f20-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="46f20-115">Дополнительные сведения о ценах на хранилище данных SQL см. на [этой странице][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="46f20-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="46f20-116">Создание базы данных с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="46f20-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="46f20-117">Если вы не знакомы с Visual Studio, см. статью [Запросы к хранилищу данных SQL Azure (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="46f20-117">If you are new to Visual Studio, see the article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="46f20-118">Сначала откройте обозреватель объектов SQL Server в Visual Studio и подключитесь к серверу, на котором будет размещена база данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="46f20-118">To start, open SQL Server Object Explorer in Visual Studio and connect to the server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="46f20-119">После подключения можно создать хранилище данных SQL. Для этого выполните следующую команду для базы данных **master**.</span><span class="sxs-lookup"><span data-stu-id="46f20-119">Once connected, you can create a SQL Data Warehouse by running the following SQL command against the **master** database.</span></span>  <span data-ttu-id="46f20-120">Эта команда создаст базу данных MySqlDwDb с целевой службой DW400 и позволит ей достичь максимального размера 10 ТБ.</span><span class="sxs-lookup"><span data-stu-id="46f20-120">This command creates the database MySqlDwDb with a Service Objective of DW400 and allow the database to grow to a maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="46f20-121">Создание базы данных с помощью служебной программы sqlcmd</span><span class="sxs-lookup"><span data-stu-id="46f20-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="46f20-122">Также можно запустить ту же команду с помощью sqlcmd, выполнив следующую команду в командной строке.</span><span class="sxs-lookup"><span data-stu-id="46f20-122">Alternatively, you can run the same command with sqlcmd by running the following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="46f20-123">Если параметры сортировки не указаны, по умолчанию используется COLLATE SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="46f20-123">The default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="46f20-124">Значение параметра `MAXSIZE` может составлять от 250 ГБ до 240 ТБ.</span><span class="sxs-lookup"><span data-stu-id="46f20-124">The `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="46f20-125">Значение параметра `SERVICE_OBJECTIVE` задается в диапазоне от DW100 до DW2000 единиц [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="46f20-125">The `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="46f20-126">Список всех допустимых значений см. в документации MSDN об инструкции [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="46f20-126">For a list of all valid values, see the MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="46f20-127">Параметры MAXSIZE и SERVICE_OBJECTIVE можно изменить с помощью команды T-SQL [ALTER DATABASE][ALTER DATABASE].</span><span class="sxs-lookup"><span data-stu-id="46f20-127">Both the MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="46f20-128">Параметры сортировки базы данных нельзя изменить после создания.</span><span class="sxs-lookup"><span data-stu-id="46f20-128">The collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="46f20-129">При изменении параметра SERVICE_OBJECTIVE следует соблюдать осторожность, так как изменение DWU приводит к перезапуску служб, который отменяет все текущие запросы.</span><span class="sxs-lookup"><span data-stu-id="46f20-129">Caution should be used when changing the SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="46f20-130">При изменении параметра MAXSIZE службы не перезапускаются, так как это всего лишь простая операция с метаданными.</span><span class="sxs-lookup"><span data-stu-id="46f20-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46f20-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="46f20-131">Next steps</span></span>
<span data-ttu-id="46f20-132">После завершения подготовки хранилища данных SQL вы можете [загрузить демонстрационные данные][load sample data] или ознакомиться с возможностями [разработки][develop], [загрузки][load] или [переноса][migrate].</span><span class="sxs-lookup"><span data-stu-id="46f20-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how to [develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how to create a SQL Data Warehouse from the Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with the Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how to create a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
