---
title: "Хранилище данных SQL с TSQL aaaCreate | Документы Microsoft"
description: "Узнайте, как toocreate Azure хранилище данных SQL с помощью TSQL"
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
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a><span data-ttu-id="4a716-103">Создание базы данных хранилища данных SQL с помощью Transact-SQL (TSQL)</span><span class="sxs-lookup"><span data-stu-id="4a716-103">Create a SQL Data Warehouse database by using Transact-SQL (TSQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a716-104">портале Azure</span><span class="sxs-lookup"><span data-stu-id="4a716-104">Azure Portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="4a716-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="4a716-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="4a716-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a716-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="4a716-107">В этой статье показано, как toocreate SQL в хранилище данных с помощью T-SQL.</span><span class="sxs-lookup"><span data-stu-id="4a716-107">This article shows you how toocreate a SQL Data Warehouse using T-SQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4a716-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4a716-108">Prerequisites</span></span>
<span data-ttu-id="4a716-109">tooget работы, необходимо:</span><span class="sxs-lookup"><span data-stu-id="4a716-109">tooget started, you need:</span></span>

* <span data-ttu-id="4a716-110">**Учетная запись Azure**: посетите [бесплатная пробная версия] [ Azure Free Trial] или [кредиты Azure MSDN] [ MSDN Azure Credits] toocreate учетную запись.</span><span class="sxs-lookup"><span data-stu-id="4a716-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="4a716-111">**Сервер SQL Azure**: см. раздел [создание логического сервера базы данных SQL Azure с портала Azure hello] [создание логического сервера базы данных SQL Azure с портала Azure hello] или [создание логического сервера базы данных SQL Azure с помощью PowerShell] [создание Azure SQL Логический сервер базы данных с помощью PowerShell] для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="4a716-111">**Azure SQL server**:  See [Create an Azure SQL Database logical server with hello Azure Portal][Create an Azure SQL Database logical server with hello Azure Portal] or [Create an Azure SQL Database logical server with PowerShell][Create an Azure SQL Database logical server with PowerShell] for more details.</span></span>
* <span data-ttu-id="4a716-112">**Группа ресурсов**: используйте hello того же ресурса группу, что сервер Azure SQL или в разделе [как toocreate группу ресурсов][how toocreate a resource group].</span><span class="sxs-lookup"><span data-stu-id="4a716-112">**Resource group**: Either use hello same resource group as your Azure SQL server or see [how toocreate a resource group][how toocreate a resource group].</span></span>
* <span data-ttu-id="4a716-113">**Среда tooexecute T-SQL**: можно использовать [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], или [SSMS] [ SSMS] tooexecute T-SQL.</span><span class="sxs-lookup"><span data-stu-id="4a716-113">**Environment tooexecute T-SQL**: You can use [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], or [SSMS][SSMS] tooexecute T-SQL.</span></span>

> [!NOTE]
> <span data-ttu-id="4a716-114">Создание хранилища данных SQL может привести к дополнительным расходам.</span><span class="sxs-lookup"><span data-stu-id="4a716-114">Creating a SQL Data Warehouse may result in a new billable service.</span></span>  <span data-ttu-id="4a716-115">Дополнительные сведения о ценах на хранилище данных SQL см. на [этой странице][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="4a716-115">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details on pricing.</span></span>
>
>

## <a name="create-a-database-with-visual-studio"></a><span data-ttu-id="4a716-116">Создание базы данных с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4a716-116">Create a database with Visual Studio</span></span>
<span data-ttu-id="4a716-117">Если новый tooVisual Studio, см. в статье hello [запросов хранилища данных SQL Azure (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span><span class="sxs-lookup"><span data-stu-id="4a716-117">If you are new tooVisual Studio, see hello article [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].</span></span>  <span data-ttu-id="4a716-118">toostart, откройте обозреватель объектов SQL Server в Visual Studio и подключитесь toohello сервера, на котором размещена в базе данных хранилища данных SQL.</span><span class="sxs-lookup"><span data-stu-id="4a716-118">toostart, open SQL Server Object Explorer in Visual Studio and connect toohello server that will host your SQL Data Warehouse database.</span></span>  <span data-ttu-id="4a716-119">После подключения хранилища данных SQL можно создать, запустив следующую команду SQL для hello hello **master** базы данных.</span><span class="sxs-lookup"><span data-stu-id="4a716-119">Once connected, you can create a SQL Data Warehouse by running hello following SQL command against hello **master** database.</span></span>  <span data-ttu-id="4a716-120">Эта команда создает базу данных hello MySqlDwDb с целью службы DW400 и разрешить hello toogrow tooa максимальному размеру базы данных составляет 10 ТБ.</span><span class="sxs-lookup"><span data-stu-id="4a716-120">This command creates hello database MySqlDwDb with a Service Objective of DW400 and allow hello database toogrow tooa maximum size of 10 TB.</span></span>

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a><span data-ttu-id="4a716-121">Создание базы данных с помощью служебной программы sqlcmd</span><span class="sxs-lookup"><span data-stu-id="4a716-121">Create a database with sqlcmd</span></span>
<span data-ttu-id="4a716-122">Кроме того можно запустить hello в одной команде с помощью sqlcmd, запустив hello, выполнив в командной строке.</span><span class="sxs-lookup"><span data-stu-id="4a716-122">Alternatively, you can run hello same command with sqlcmd by running hello following at a command prompt.</span></span>

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

<span data-ttu-id="4a716-123">параметры сортировки по умолчанию Hello при его отсутствии — COLLATE SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="4a716-123">hello default collation when not specified is COLLATE SQL_Latin1_General_CP1_CI_AS.</span></span>  <span data-ttu-id="4a716-124">Hello `MAXSIZE` может находиться в диапазоне от 250 ГБ и ТБ 240.</span><span class="sxs-lookup"><span data-stu-id="4a716-124">hello `MAXSIZE` can be between 250 GB and 240 TB.</span></span>  <span data-ttu-id="4a716-125">Hello `SERVICE_OBJECTIVE` может находиться в диапазоне от DW100 и DW2000 [DWU][DWU].</span><span class="sxs-lookup"><span data-stu-id="4a716-125">hello `SERVICE_OBJECTIVE` can be between DW100 and DW2000 [DWU][DWU].</span></span>  <span data-ttu-id="4a716-126">Список всех допустимых значений см. в разделе документации MSDN hello [CREATE DATABASE][CREATE DATABASE].</span><span class="sxs-lookup"><span data-stu-id="4a716-126">For a list of all valid values, see hello MSDN documentation for [CREATE DATABASE][CREATE DATABASE].</span></span>  <span data-ttu-id="4a716-127">Hello MAXSIZE и SERVICE_OBJECTIVE можно изменить с помощью [инструкции ALTER DATABASE] [ ALTER DATABASE] команды T-SQL.</span><span class="sxs-lookup"><span data-stu-id="4a716-127">Both hello MAXSIZE and SERVICE_OBJECTIVE can be changed with an [ALTER DATABASE][ALTER DATABASE] T-SQL command.</span></span>  <span data-ttu-id="4a716-128">Hello параметры сортировки базы данных нельзя изменить после создания.</span><span class="sxs-lookup"><span data-stu-id="4a716-128">hello collation of a database cannot be changed after creation.</span></span>   <span data-ttu-id="4a716-129">Следует соблюдать осторожность, когда изменение hello SERVICE_OBJECTIVE как изменение DWU приводит перезапустить службы, которая отменяет все запросы в процессе передачи.</span><span class="sxs-lookup"><span data-stu-id="4a716-129">Caution should be used when changing hello SERVICE_OBJECTIVE as changing DWU causes a restart of services, which cancels all queries in flight.</span></span>  <span data-ttu-id="4a716-130">При изменении параметра MAXSIZE службы не перезапускаются, так как это всего лишь простая операция с метаданными.</span><span class="sxs-lookup"><span data-stu-id="4a716-130">Changing MAXSIZE does not restart services as it is just a simple metadata operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a716-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a716-131">Next steps</span></span>
<span data-ttu-id="4a716-132">После завершения подготовки, вы можете хранилище данных SQL [загрузить образцы данных] [ load sample data] или узнать о возможностях слишком[разработки][develop], [загрузки][load], или [перенести][migrate].</span><span class="sxs-lookup"><span data-stu-id="4a716-132">After your SQL Data Warehouse has finished provisioning you can [load sample data][load sample data] or check out how too[develop][develop], [load][load], or [migrate][migrate].</span></span>

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
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
