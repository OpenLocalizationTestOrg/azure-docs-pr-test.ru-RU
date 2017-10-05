---
title: "Загрузка образца данных в хранилище данных SQL | Документация Майкрософт"
description: "Загрузка образца данных в хранилище данных SQL"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1e0df958a2f18fe1e988168918e5cfd293f84e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="727e5-103">Загрузка образца данных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="727e5-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="727e5-104">Выполните эти простые действия для загрузки примера базы данных Adventure Works и выполнения запроса к ней.</span><span class="sxs-lookup"><span data-stu-id="727e5-104">Follow these simple steps to load and query the Adventure Works Sample database.</span></span> <span data-ttu-id="727e5-105">Эти сценарии сначала используют sqlcmd для выполнения инструкций SQL, что приведет к созданию таблиц и представлений.</span><span class="sxs-lookup"><span data-stu-id="727e5-105">These scripts first use sqlcmd to run SQL which will create tables and views.</span></span> <span data-ttu-id="727e5-106">После создания таблицы сценарии используют bcp для загрузки данных.</span><span class="sxs-lookup"><span data-stu-id="727e5-106">Once tables have been created, the scripts will use bcp to load data.</span></span>  <span data-ttu-id="727e5-107">Если вы еще не установили sqlcmd и bcp, воспользуйтесь следующими ссылками для [установки bcp][install bcp] и [sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="727e5-107">If you don't already have sqlcmd and bcp installed, follow these links to [install bcp][install bcp] and to [install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="727e5-108">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="727e5-108">Load sample data</span></span>
1. <span data-ttu-id="727e5-109">Скачайте ZIP-файл с [примерами сценариев Adventure Works для хранилища данных SQL][Adventure Works Sample Scripts for SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="727e5-109">Download the [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="727e5-110">Извлеките файлы из скачанного ZIP-файла в каталог на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="727e5-110">Extract the files from downloaded zip to a directory on your local machine.</span></span>
3. <span data-ttu-id="727e5-111">Измените извлеченный файл aw_create.bat и задайте следующие переменные в верхней его части:</span><span class="sxs-lookup"><span data-stu-id="727e5-111">Edit the extracted file aw_create.bat and set the following variables found at the top of the file.</span></span>  <span data-ttu-id="727e5-112">Не забудьте, что между знаком = и параметром не должно быть пробелов.</span><span class="sxs-lookup"><span data-stu-id="727e5-112">Be sure to leave no whitespace between the "=" and the parameter.</span></span>  <span data-ttu-id="727e5-113">Ниже приведены примеры того, как могут выглядеть такие изменения.</span><span class="sxs-lookup"><span data-stu-id="727e5-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="727e5-114">Запустите измененный файл aw_create.bat из командной строки Windows.</span><span class="sxs-lookup"><span data-stu-id="727e5-114">From a Windows cmd prompt, run the edited aw_create.bat.</span></span>  <span data-ttu-id="727e5-115">Убедитесь, что вы находитесь в том каталоге, куда была сохранена измененная версия aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="727e5-115">Be sure you are in the directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="727e5-116">Вот что делает этот сценарий:</span><span class="sxs-lookup"><span data-stu-id="727e5-116">This script will...</span></span>
   
   * <span data-ttu-id="727e5-117">удаляет все представления и таблицы Adventure Works, которые уже существуют в базе данных;</span><span class="sxs-lookup"><span data-stu-id="727e5-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="727e5-118">создает представления и таблицы Adventure Works;</span><span class="sxs-lookup"><span data-stu-id="727e5-118">Create the Adventure Works tables and views</span></span>
   * <span data-ttu-id="727e5-119">загружает каждую таблицу Adventure Works с помощью bcp;</span><span class="sxs-lookup"><span data-stu-id="727e5-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="727e5-120">проверяет количество строк для каждой таблицы Adventure Works;</span><span class="sxs-lookup"><span data-stu-id="727e5-120">Validate the row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="727e5-121">собирает статистику по каждому столбцу для каждой таблицы Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="727e5-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="727e5-122">Запрос части данных для примера</span><span class="sxs-lookup"><span data-stu-id="727e5-122">Query sample data</span></span>
<span data-ttu-id="727e5-123">После загрузки некоторых демонстрационных данных в хранилище данных SQL можно быстро выполнить несколько запросов.</span><span class="sxs-lookup"><span data-stu-id="727e5-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="727e5-124">Для выполнения запроса подключитесь к недавно созданной базе данных Adventure Works в хранилище данных SQL Azure с помощью Visual Studio и SSDT, как описано в документе о [выполнении запроса с помощью Visual Studio][query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="727e5-124">To run a query, connect to your newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in the [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="727e5-125">Пример простого оператора select для получения всех сведений о сотрудниках:</span><span class="sxs-lookup"><span data-stu-id="727e5-125">Example of simple select statement to get all the info of the employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="727e5-126">Пример более сложного запроса с использованием таких конструкций, как GROUP BY, для просмотра общей суммы всех продаж за каждый день:</span><span class="sxs-lookup"><span data-stu-id="727e5-126">Example of a more complex query using constructs such as GROUP BY to look at the total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="727e5-127">Пример оператора SELECT с выражением WHERE для фильтрации заказов, размещенных до определенной даты:</span><span class="sxs-lookup"><span data-stu-id="727e5-127">Example of a SELECT with a WHERE clause to filter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="727e5-128">Хранилище данных SQL поддерживает почти все конструкции T-SQL, которые поддерживаются SQL Server.</span><span class="sxs-lookup"><span data-stu-id="727e5-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="727e5-129">Все различия описаны в нашей документации по [переносу кода][migrate code].</span><span class="sxs-lookup"><span data-stu-id="727e5-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="727e5-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="727e5-130">Next steps</span></span>
<span data-ttu-id="727e5-131">Теперь, когда имеется возможность выполнить некоторые запросы с демонстрационными данными, попробуйте осуществлять [разработку][develop], [загрузку][load] или [перенос][migrate] в хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="727e5-131">Now that you've had a chance to try some queries with sample data, check out how to [develop][develop], [load][load], or [migrate][migrate] to SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
