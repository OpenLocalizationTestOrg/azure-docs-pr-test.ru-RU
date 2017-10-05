---
title: "Начало работы с каталогом U-SQL | Документация Майкрософт"
description: "Сведения об использовании каталога U-SQL для совместного использования кода и данных."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="bc1f4-103">Начало работы с каталогом U-SQL</span><span class="sxs-lookup"><span data-stu-id="bc1f4-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="bc1f4-104">Создание функции TVF</span><span class="sxs-lookup"><span data-stu-id="bc1f4-104">Create a TVF</span></span>

<span data-ttu-id="bc1f4-105">В предыдущем скрипте U-SQL мы повторно использовали EXTRACT для чтения из одного и того же исходного файла.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="bc1f4-106">В U-SQL функция с табличным значением (TVF) позволяет инкапсулировать данные для повторного использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="bc1f4-107">Следующий скрипт создает возвращающую табличное значение функцию с именем `Searchlog()` в базе данных и схеме по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="bc1f4-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

<span data-ttu-id="bc1f4-108">Следующий скрипт демонстрирует, как использовать функцию TVF, определенную в предыдущем скрипте:</span><span class="sxs-lookup"><span data-stu-id="bc1f4-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="bc1f4-109">Создание представлений</span><span class="sxs-lookup"><span data-stu-id="bc1f4-109">Create views</span></span>

<span data-ttu-id="bc1f4-110">Если у вас есть одно выражение запроса вместо возвращающей табличное значение функции, можно использовать представление U-SQL для инкапсуляции этого выражения.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="bc1f4-111">Следующий скрипт создает представление с именем `SearchlogView` в базе данных и схеме по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="bc1f4-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

<span data-ttu-id="bc1f4-112">Следующий скрипт демонстрирует, как использовать определенное представление.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="bc1f4-113">создание таблиц.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-113">Create tables</span></span>
<span data-ttu-id="bc1f4-114">Как и в случае с таблицами реляционной базы данных, U-SQL позволяет создать таблицу с предварительно определенной схемой или же создать таблицу и определить схему из запроса, который заполняет таблицу (CREATE TABLE AS SELECT или CTAS).</span><span class="sxs-lookup"><span data-stu-id="bc1f4-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="bc1f4-115">Следующий скрипт создает базу данных и две таблицы:</span><span class="sxs-lookup"><span data-stu-id="bc1f4-115">Create a database and two tables by using the following script:</span></span>

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a><span data-ttu-id="bc1f4-116">Запросы к таблицам</span><span class="sxs-lookup"><span data-stu-id="bc1f4-116">Query tables</span></span>
<span data-ttu-id="bc1f4-117">Вы можете отправлять запросы к таблицам (созданным с помощью предыдущего скрипта) так же, как вы отправляете запросы к файлам данных.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="bc1f4-118">Чтобы не создавать набор строк с помощью EXTRACT, теперь можно просто ссылаться на имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="bc1f4-119">Для чтения из таблиц нужно изменить скрипт преобразования, который использовался ранее:</span><span class="sxs-lookup"><span data-stu-id="bc1f4-119">To read from the tables, modify the transform script that you used previously:</span></span>

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="bc1f4-120">Сейчас выполнять SELECT для таблицы в том же скрипте, где создается таблица, нельзя.</span><span class="sxs-lookup"><span data-stu-id="bc1f4-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc1f4-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc1f4-121">Next Steps</span></span>
* [<span data-ttu-id="bc1f4-122">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bc1f4-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="bc1f4-123">Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc1f4-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="bc1f4-124">Устранение неполадок с заданиями аналитики озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="bc1f4-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
