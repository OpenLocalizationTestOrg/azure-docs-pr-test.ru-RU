---
title: "aaaLoad образца данных в хранилище данных SQL | Документы Microsoft"
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
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="fafb9-103">Загрузка образца данных в хранилище данных SQL</span><span class="sxs-lookup"><span data-stu-id="fafb9-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="fafb9-104">Выполните эти простые действия tooload и запрос к базе данных Adventure Works образец hello.</span><span class="sxs-lookup"><span data-stu-id="fafb9-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="fafb9-105">Сначала с помощью этих скриптов sqlcmd toorun SQL, что приведет к созданию таблиц и представлений.</span><span class="sxs-lookup"><span data-stu-id="fafb9-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="fafb9-106">После создания таблицы bcp tooload данные будут использоваться в сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="fafb9-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="fafb9-107">Если у вас еще нет sqlcmd и bcp установлена, перейдите по соответствующей ссылке слишком[установить bcp] [ install bcp] и слишком[установить sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="fafb9-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="fafb9-108">Загрузка примера данных</span><span class="sxs-lookup"><span data-stu-id="fafb9-108">Load sample data</span></span>
1. <span data-ttu-id="fafb9-109">Загрузите hello [Adventure Works примеры сценариев для хранилища данных SQL] [ Adventure Works Sample Scripts for SQL Data Warehouse] ZIP-файл.</span><span class="sxs-lookup"><span data-stu-id="fafb9-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="fafb9-110">Извлеките файлы hello из каталога tooa загруженный zip на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="fafb9-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="fafb9-111">Измените aw_create.bat hello извлечь файл и задайте следующие переменные, найденные в начале hello файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="fafb9-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="fafb9-112">Быть убедиться, что tooleave без пробелов между hello «=» и параметром hello.</span><span class="sxs-lookup"><span data-stu-id="fafb9-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="fafb9-113">Ниже приведены примеры того, как могут выглядеть такие изменения.</span><span class="sxs-lookup"><span data-stu-id="fafb9-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="fafb9-114">Запустите aw_create.bat изменить hello из командную строку Windows.</span><span class="sxs-lookup"><span data-stu-id="fafb9-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="fafb9-115">Убедитесь, что вы находитесь в каталоге hello, где был сохранен aw_create.bat вашей измененной версии.</span><span class="sxs-lookup"><span data-stu-id="fafb9-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="fafb9-116">Вот что делает этот сценарий:</span><span class="sxs-lookup"><span data-stu-id="fafb9-116">This script will...</span></span>
   
   * <span data-ttu-id="fafb9-117">удаляет все представления и таблицы Adventure Works, которые уже существуют в базе данных;</span><span class="sxs-lookup"><span data-stu-id="fafb9-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="fafb9-118">Создание hello Adventure Works таблиц и представлений</span><span class="sxs-lookup"><span data-stu-id="fafb9-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="fafb9-119">загружает каждую таблицу Adventure Works с помощью bcp;</span><span class="sxs-lookup"><span data-stu-id="fafb9-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="fafb9-120">Проверка hello количество строк для каждой таблицы Adventure Works</span><span class="sxs-lookup"><span data-stu-id="fafb9-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="fafb9-121">собирает статистику по каждому столбцу для каждой таблицы Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="fafb9-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="fafb9-122">Запрос части данных для примера</span><span class="sxs-lookup"><span data-stu-id="fafb9-122">Query sample data</span></span>
<span data-ttu-id="fafb9-123">После загрузки некоторых демонстрационных данных в хранилище данных SQL можно быстро выполнить несколько запросов.</span><span class="sxs-lookup"><span data-stu-id="fafb9-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="fafb9-124">toorun запроса, подключите tooyour вновь созданные базы данных Adventure Works в хранилища данных SQL Azure с помощью Visual Studio и SSDT, как описано в hello [запроса с помощью Visual Studio] [ query with Visual Studio] документа.</span><span class="sxs-lookup"><span data-stu-id="fafb9-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="fafb9-125">Пример простого выберите tooget инструкции все сведения о hello hello сотрудников:</span><span class="sxs-lookup"><span data-stu-id="fafb9-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="fafb9-126">Пример более сложный запрос с помощью конструкций, таких как toolook GROUP BY в hello Общая сумма всех продаж за каждый день.</span><span class="sxs-lookup"><span data-stu-id="fafb9-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="fafb9-127">Пример инструкции SELECT с toofilter предложение WHERE out заказами до определенной даты.</span><span class="sxs-lookup"><span data-stu-id="fafb9-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="fafb9-128">Хранилище данных SQL поддерживает почти все конструкции T-SQL, которые поддерживаются SQL Server.</span><span class="sxs-lookup"><span data-stu-id="fafb9-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="fafb9-129">Все различия описаны в нашей документации по [переносу кода][migrate code].</span><span class="sxs-lookup"><span data-stu-id="fafb9-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fafb9-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fafb9-130">Next steps</span></span>
<span data-ttu-id="fafb9-131">Теперь, когда вы tootry вероятность некоторых запросов с образцами данных, узнать о возможностях слишком[разработки][develop], [загрузить][load], или [ Перенос] [ migrate] tooSQL хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="fafb9-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

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
