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
# <a name="get-started-with-hello-u-sql-catalog"></a>Приступая к работе с hello каталога U-SQL

## <a name="create-a-tvf"></a>Создание функции TVF

Hello предыдущих скрипт U-SQL, повторяющиеся hello использование tooread ИЗВЛЕЧЕНИЯ из hello же исходном файле. С U-SQL возвращающих табличные значения функции hello (TVF) можно инкапсулировать hello данных для повторного использования в будущем.  

Hello следующий скрипт создает возвращающей табличное значение функции вызывается `Searchlog()` в базе данных по умолчанию hello и схемы:

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

Привет, выполнив сценарий показывает, как toouse hello возвращающей табличное значение, которое было определено в предыдущем сценарии hello:

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

## <a name="create-views"></a>Создание представлений

Если единственное выражение запроса, вместо возвращающей табличное значение функции можно использовать tooencapsulate U-SQL-ПРЕДСТАВЛЕНИЕ этого выражения.

Hello следующий скрипт создает представление с именем `SearchlogView` в базе данных по умолчанию hello и схемы:

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

Привет, выполнив сценарий демонстрирует использование hello hello определенные представления:

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

## <a name="create-tables"></a>создание таблиц.
Как с таблицами в реляционной базе данных, с помощью U-SQL можно создать таблицу с предварительно определенной схемой или создать таблицу, которая выводит схему hello hello запроса, который заполняет таблицу hello (также известный как CREATE TABLE AS SELECT или CTAS).

Создание базы данных и две таблицы с помощью hello следующий скрипт:

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

## <a name="query-tables"></a>Запросы к таблицам
Вы можете запрашивать таблицы, созданные в предыдущих сценария hello в hello таким же образом, что выполняется запрос hello файлов данных. Вместо создания набора строк с помощью ИЗВЛЕЧЕНИЯ, теперь можно ссылаться toohello имя таблицы.

tooread из таблиц hello, измените hello преобразования скрипта, который использовался ранее.

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
 >В настоящее время невозможно запустить SELECT на таблицу в hello же скрипт как один hello которой была создана таблица hello.

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор аналитики озера данных Microsoft Azure](data-lake-analytics-overview.md)
* [Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Устранение неполадок с заданиями аналитики озера данных Azure с помощью портала Azure](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
