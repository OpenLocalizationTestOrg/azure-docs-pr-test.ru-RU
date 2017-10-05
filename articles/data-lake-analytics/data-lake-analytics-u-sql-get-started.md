---
title: "Начало работы с языком U-SQL | Документация Майкрософт"
description: "Основы языка U-SQL."
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
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 38c4e1b9bd24ef0b8a81f6154620f3f98d3b5ac1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="6f6ef-103">Начало работы с U-SQL</span><span class="sxs-lookup"><span data-stu-id="6f6ef-103">Get started with U-SQL</span></span>
<span data-ttu-id="6f6ef-104">U-SQL — это язык, который объединяет декларативный SQL и императивный C#, позволяя обрабатывать данные любого масштаба.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-104">U-SQL is a language that combines declarative SQL with imperative C# to let you process data at any scale.</span></span> <span data-ttu-id="6f6ef-105">Масштабируемые распределенные запросы U-SQL позволяют эффективно анализировать данные в таких реляционных хранилищах, как база данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-105">Through the scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="6f6ef-106">С помощью U-SQL вы можете обрабатывать неструктурированные данные, применяя схему к пользовательской логике чтения и вставки, а также определяемым пользователем функциям.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="6f6ef-107">Кроме того, U-SQL содержит расширения, которые помогают разработчику точно управлять способом выполнения в нужном масштабе.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how to execute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="6f6ef-108">Учебные материалы</span><span class="sxs-lookup"><span data-stu-id="6f6ef-108">Learning resources</span></span>

* <span data-ttu-id="6f6ef-109">В [учебнике по U-SQL](http://aka.ms/usqltutorial) приводятся пошаговые инструкции по выполнению большинства операций с языком U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-109">The [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of the U-SQL language.</span></span> <span data-ttu-id="6f6ef-110">Этот документ рекомендуется к ознакомлению всем разработчикам, которые хотят освоить U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-110">This document is recommended reading for all developers wanting to learn U-SQL.</span></span>
* <span data-ttu-id="6f6ef-111">Дополнительные сведения о **синтаксисе языка U-SQL** см. в [справочнике по языку U-SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="6f6ef-111">For detailed information about the **U-SQL language syntax**, see the [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="6f6ef-112">Чтобы понять **принципы разработки на U-SQL**, см. запись блога Visual Studio, посвященную [использованию языка U-SQL для простой обработки больших данных](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="6f6ef-112">To understand the **U-SQL design philosophy**, see the Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f6ef-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6f6ef-113">Prerequisites</span></span>

<span data-ttu-id="6f6ef-114">Прежде чем переходить к примерам в этом документе, ознакомьтесь с [руководством по разработке скриптов U-SQL с помощью средств Data Lake для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6f6ef-114">Before you go through the U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="6f6ef-115">Это руководство описывает механизм использования U-SQL с помощью средств Azure Data Lake для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-115">That tutorial explains the mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="6f6ef-116">Первый скрипт U-SQL</span><span class="sxs-lookup"><span data-stu-id="6f6ef-116">Your first U-SQL script</span></span>

<span data-ttu-id="6f6ef-117">Ниже приведен очень простой скрипт U-SQL, который помогает понять различные аспекты языка U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-117">The following U-SQL script is simple and lets us explore many aspects the U-SQL language.</span></span>

```
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

OUTPUT @searchlog   
    TO "/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="6f6ef-118">Этот сценарий не содержит действий преобразования.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="6f6ef-119">Он считывает данные из исходного файла `SearchLog.tsv`, схематизирует их, а затем записывает набор строк в файл с именем SearchLog-first-u-sql.csv.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-119">It reads from the source file called `SearchLog.tsv`, schematizes it, and writes the rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="6f6ef-120">Обратите внимание на вопросительный знак рядом с типом данных в поле `Duration`.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-120">Notice the question mark next to the data type in the `Duration` field.</span></span> <span data-ttu-id="6f6ef-121">Это означает, что поле `Duration` может иметь значение NULL.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-121">It means that the `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="6f6ef-122">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="6f6ef-122">Key concepts</span></span>
* <span data-ttu-id="6f6ef-123">**Переменные набора строк**: каждое выражение запроса, которое возвращает набор строк, может быть назначено переменной.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-123">**Rowset variables**: Each query expression that produces a rowset can be assigned to a variable.</span></span> <span data-ttu-id="6f6ef-124">U-SQL использует в сценарии шаблон именования переменных T-SQL (пример: `@searchlog`).</span><span class="sxs-lookup"><span data-stu-id="6f6ef-124">U-SQL follows the T-SQL variable naming pattern (`@searchlog`, for example) in the script.</span></span>
* <span data-ttu-id="6f6ef-125">Оператор **EXTRACT** считывает данные из файла и определяет схему для чтения.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-125">The **EXTRACT** keyword reads data from a file and defines the schema on read.</span></span> <span data-ttu-id="6f6ef-126">`Extractors.Tsv` — это встроенное средство извлечения U-SQL для файлов со значениями с разделением знаками табуляции.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="6f6ef-127">Можно разрабатывать пользовательские средства извлечения.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="6f6ef-128">Оператор **OUTPUT** записывает данные из набора строк в файл.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-128">The **OUTPUT** writes data from a rowset to a file.</span></span> <span data-ttu-id="6f6ef-129">`Outputters.Csv()` — это встроенное средство вывода данных U-SQL для файлов данных с разделителями-запятыми.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-129">`Outputters.Csv()` is a built-in U-SQL outputter to create a comma-separated-value file.</span></span> <span data-ttu-id="6f6ef-130">Вы можете разработать собственные средства вывода.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="6f6ef-131">Пути к файлам</span><span class="sxs-lookup"><span data-stu-id="6f6ef-131">File paths</span></span>

<span data-ttu-id="6f6ef-132">Операторы EXTRACT и OUTPUT используют пути к файлам.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-132">The EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="6f6ef-133">Пути к файлам могут быть абсолютными или относительными.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="6f6ef-134">Следующий абсолютный путь к файлу ссылается на файл `mystore` в Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="6f6ef-134">This following absolute file path refers to a file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="6f6ef-135">Следующий относительный путь к файлу начинается с `"/"`.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="6f6ef-136">Он указывает на файл в учетной записи Data Lake Store по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="6f6ef-136">It refers to a file in the default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="6f6ef-137">Использование скалярных переменных</span><span class="sxs-lookup"><span data-stu-id="6f6ef-137">Use scalar variables</span></span>

<span data-ttu-id="6f6ef-138">Скалярные переменные можно использовать также для упрощения обслуживания вашего сценария.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-138">You can use scalar variables as well to make your script maintenance easier.</span></span> <span data-ttu-id="6f6ef-139">Предыдущий скрипт U-SQL также можно записать так:</span><span class="sxs-lookup"><span data-stu-id="6f6ef-139">The previous U-SQL script can also be written as:</span></span>

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        TO @out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="6f6ef-140">Преобразования наборов строк</span><span class="sxs-lookup"><span data-stu-id="6f6ef-140">Transform rowsets</span></span>

<span data-ttu-id="6f6ef-141">Используйте **SELECT** для преобразования наборов строк:</span><span class="sxs-lookup"><span data-stu-id="6f6ef-141">Use **SELECT** to transform rowsets:</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="6f6ef-142">Предложение WHERE использует [логическое выражение C#](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f6ef-142">The WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="6f6ef-143">Для создания собственных выражений и функций можно использовать язык выражений C#.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-143">You can use the C# expression language to do your own expressions and functions.</span></span> <span data-ttu-id="6f6ef-144">Можно даже выполнить более сложную фильтрацию, сочетая их с помощью логического объединения (and) и разделения (or).</span><span class="sxs-lookup"><span data-stu-id="6f6ef-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="6f6ef-145">Следующий сценарий использует метод DateTime.Parse() и объединение.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-145">The following script uses the DateTime.Parse() method and a conjunction.</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        TO "/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="6f6ef-146">Второй запрос выполняется на основе результатов первого набора строк, объединяя таким образом два фильтра.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-146">The second query is operating on the result of the first rowset, which creates a composite of the two filters.</span></span> <span data-ttu-id="6f6ef-147">Можно также повторно использовать имя переменной. Имена объединяются лексически.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-147">You can also reuse a variable name, and the names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="6f6ef-148">Агрегированные наборы строк</span><span class="sxs-lookup"><span data-stu-id="6f6ef-148">Aggregate rowsets</span></span>
<span data-ttu-id="6f6ef-149">U-SQL поддерживает знакомые предложения ORDER BY, GROUP BY и агрегаты.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-149">U-SQL gives you the familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="6f6ef-150">Следующий запрос определяет общую длительность по регионам, а затем последовательно выводит пять результатов со значениями максимальной длительности.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-150">The following query finds the total duration per region, and then displays the top five durations in order.</span></span>

<span data-ttu-id="6f6ef-151">Наборы строк U-SQL не сохраняют свой порядок для следующего запроса.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-151">U-SQL rowsets do not preserve their order for the next query.</span></span> <span data-ttu-id="6f6ef-152">Таким образом, чтобы упорядочить выходные данные, необходимо добавить предложение ORDER BY в предложение OUTPUT.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-152">Thus, to order an output, you need to add ORDER BY to the OUTPUT statement:</span></span>

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

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

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        TO @out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        TO @out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="6f6ef-153">Предложение ORDER BY в U-SQL необходимо использовать вместе с предложением FETCH в выражении SELECT.</span><span class="sxs-lookup"><span data-stu-id="6f6ef-153">The U-SQL ORDER BY clause requires using the FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="6f6ef-154">Предложение HAVING в U-SQL можно использовать для ограничения выходных данных группами, которые удовлетворяют условиям HAVING:</span><span class="sxs-lookup"><span data-stu-id="6f6ef-154">The U-SQL HAVING clause can be used to restrict the output to groups that satisfy the HAVING condition:</span></span>

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

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        TO "/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="6f6ef-155">Сведения о расширенных сценариях агрегирования см. в справочной документации U-SQL по [статистическим, аналитическим и ссылочным функциям](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f6ef-155">For advanced aggregation scenarios, see the The U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f6ef-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6f6ef-156">Next steps</span></span>
* [<span data-ttu-id="6f6ef-157">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6f6ef-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="6f6ef-158">Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6f6ef-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
