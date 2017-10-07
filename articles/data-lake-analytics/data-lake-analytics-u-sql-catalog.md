---
title: "Начало работы с каталогом hello U-SQL | Документы Microsoft"
description: "Узнайте, как toouse hello U-SQL каталога tooshare кода и данных."
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
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a><span data-ttu-id="b22cb-103">Приступая к работе с hello каталога U-SQL</span><span class="sxs-lookup"><span data-stu-id="b22cb-103">Get started with hello U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="b22cb-104">Создание функции TVF</span><span class="sxs-lookup"><span data-stu-id="b22cb-104">Create a TVF</span></span>

<span data-ttu-id="b22cb-105">Hello предыдущих скрипт U-SQL, повторяющиеся hello использование tooread ИЗВЛЕЧЕНИЯ из hello же исходном файле.</span><span class="sxs-lookup"><span data-stu-id="b22cb-105">In hello previous U-SQL script, you repeated hello use of EXTRACT tooread from hello same source file.</span></span> <span data-ttu-id="b22cb-106">С U-SQL возвращающих табличные значения функции hello (TVF) можно инкапсулировать hello данных для повторного использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="b22cb-106">With hello U-SQL table-valued function (TVF), you can encapsulate hello data for future reuse.</span></span>  

<span data-ttu-id="b22cb-107">Hello следующий скрипт создает возвращающей табличное значение функции вызывается `Searchlog()` в базе данных по умолчанию hello и схемы:</span><span class="sxs-lookup"><span data-stu-id="b22cb-107">hello following script creates a TVF called `Searchlog()` in hello default database and schema:</span></span>

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

<span data-ttu-id="b22cb-108">Привет, выполнив сценарий показывает, как toouse hello возвращающей табличное значение, которое было определено в предыдущем сценарии hello:</span><span class="sxs-lookup"><span data-stu-id="b22cb-108">hello following script shows you how toouse hello TVF that was defined in hello previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="b22cb-109">Создание представлений</span><span class="sxs-lookup"><span data-stu-id="b22cb-109">Create views</span></span>

<span data-ttu-id="b22cb-110">Если единственное выражение запроса, вместо возвращающей табличное значение функции можно использовать tooencapsulate U-SQL-ПРЕДСТАВЛЕНИЕ этого выражения.</span><span class="sxs-lookup"><span data-stu-id="b22cb-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW tooencapsulate that expression.</span></span>

<span data-ttu-id="b22cb-111">Hello следующий скрипт создает представление с именем `SearchlogView` в базе данных по умолчанию hello и схемы:</span><span class="sxs-lookup"><span data-stu-id="b22cb-111">hello following script creates a view called `SearchlogView` in hello default database and schema:</span></span>

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

<span data-ttu-id="b22cb-112">Привет, выполнив сценарий демонстрирует использование hello hello определенные представления:</span><span class="sxs-lookup"><span data-stu-id="b22cb-112">hello following script demonstrates hello use of hello defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="b22cb-113">создание таблиц.</span><span class="sxs-lookup"><span data-stu-id="b22cb-113">Create tables</span></span>
<span data-ttu-id="b22cb-114">Как с таблицами в реляционной базе данных, с помощью U-SQL можно создать таблицу с предварительно определенной схемой или создать таблицу, которая выводит схему hello hello запроса, который заполняет таблицу hello (также известный как CREATE TABLE AS SELECT или CTAS).</span><span class="sxs-lookup"><span data-stu-id="b22cb-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers hello schema from hello query that populates hello table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="b22cb-115">Создание базы данных и две таблицы с помощью hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="b22cb-115">Create a database and two tables by using hello following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="b22cb-116">Запросы к таблицам</span><span class="sxs-lookup"><span data-stu-id="b22cb-116">Query tables</span></span>
<span data-ttu-id="b22cb-117">Вы можете запрашивать таблицы, созданные в предыдущих сценария hello в hello таким же образом, что выполняется запрос hello файлов данных.</span><span class="sxs-lookup"><span data-stu-id="b22cb-117">You can query tables, such as those created in hello previous script, in hello same way that you query hello data files.</span></span> <span data-ttu-id="b22cb-118">Вместо создания набора строк с помощью ИЗВЛЕЧЕНИЯ, теперь можно ссылаться toohello имя таблицы.</span><span class="sxs-lookup"><span data-stu-id="b22cb-118">Instead of creating a rowset by using EXTRACT, you now can refer toohello table name.</span></span>

<span data-ttu-id="b22cb-119">tooread из таблиц hello, измените hello преобразования скрипта, который использовался ранее.</span><span class="sxs-lookup"><span data-stu-id="b22cb-119">tooread from hello tables, modify hello transform script that you used previously:</span></span>

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
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="b22cb-120">В настоящее время невозможно запустить SELECT на таблицу в hello же скрипт как один hello которой была создана таблица hello.</span><span class="sxs-lookup"><span data-stu-id="b22cb-120">Currently, you cannot run a SELECT on a table in hello same script as hello one where you created hello table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b22cb-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b22cb-121">Next Steps</span></span>
* [<span data-ttu-id="b22cb-122">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b22cb-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="b22cb-123">Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b22cb-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="b22cb-124">Устранение неполадок с заданиями аналитики озера данных Azure с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="b22cb-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
