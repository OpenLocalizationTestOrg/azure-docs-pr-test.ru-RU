---
title: "Начало работы с языком U-SQL | Документация Майкрософт"
description: "Основы hello объекта hello языка U-SQL."
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
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="f59eb-103">Начало работы с U-SQL</span><span class="sxs-lookup"><span data-stu-id="f59eb-103">Get started with U-SQL</span></span>
<span data-ttu-id="f59eb-104">U-SQL — это язык, объединяет декларативный SQL с принудительной C# toolet обрабатывать данные любых объемов.</span><span class="sxs-lookup"><span data-stu-id="f59eb-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="f59eb-105">Через hello масштабируемого, распределенного запроса возможности U-SQL может эффективно анализировать данные в реляционных хранилищах, таких как базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f59eb-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="f59eb-106">С помощью U-SQL вы можете обрабатывать неструктурированные данные, применяя схему к пользовательской логике чтения и вставки, а также определяемым пользователем функциям.</span><span class="sxs-lookup"><span data-stu-id="f59eb-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="f59eb-107">Кроме того, U-SQL содержит расширения, который обеспечивает точное управление над тем, как tooexecute в масштабе.</span><span class="sxs-lookup"><span data-stu-id="f59eb-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="f59eb-108">Учебные материалы</span><span class="sxs-lookup"><span data-stu-id="f59eb-108">Learning resources</span></span>

* <span data-ttu-id="f59eb-109">Hello [U-SQL учебника](http://aka.ms/usqltutorial) Пошаговое руководство для большинства hello U-SQL языка.</span><span class="sxs-lookup"><span data-stu-id="f59eb-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="f59eb-110">В этом документе рекомендуется использовать считывании для всех разработчиков, желающих toolearn U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f59eb-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="f59eb-111">Дополнительные сведения о hello **синтаксиса языка U-SQL**, hello в разделе [Справочник по языку U SQL](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="f59eb-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="f59eb-112">toounderstand hello **принципы разработки U-SQL**, см. блоге Visual Studio hello [введение U-SQL — язык, который упрощает больших обработки данных](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="f59eb-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f59eb-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f59eb-113">Prerequisites</span></span>

<span data-ttu-id="f59eb-114">Перед выполнением примеров hello U-SQL в этом документе, прочтите и выполните [учебника: сценарии разработки U-SQL, с помощью средств Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f59eb-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="f59eb-115">Этот учебник объясняется hello механизм использования U-SQL с помощью средств Озера данных Azure для Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f59eb-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="f59eb-116">Первый скрипт U-SQL</span><span class="sxs-lookup"><span data-stu-id="f59eb-116">Your first U-SQL script</span></span>

<span data-ttu-id="f59eb-117">Привет, выполнив скрипт U-SQL является простым также позволяют исследовать многие аспекты hello U-SQL языка.</span><span class="sxs-lookup"><span data-stu-id="f59eb-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

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
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="f59eb-118">Этот сценарий не содержит действий преобразования.</span><span class="sxs-lookup"><span data-stu-id="f59eb-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="f59eb-119">Она считывает данные из hello исходный файл с именем `SearchLog.tsv`, schematizes его и записывает набор строк hello обратно в файл с именем SearchLog первый u sql.csv.</span><span class="sxs-lookup"><span data-stu-id="f59eb-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="f59eb-120">Обратите внимание, тип данных hello вопросительный знак Далее toohello в hello `Duration` поля.</span><span class="sxs-lookup"><span data-stu-id="f59eb-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="f59eb-121">Это означает, что hello `Duration` поле может иметь значение null.</span><span class="sxs-lookup"><span data-stu-id="f59eb-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="f59eb-122">Основные понятия</span><span class="sxs-lookup"><span data-stu-id="f59eb-122">Key concepts</span></span>
* <span data-ttu-id="f59eb-123">**Переменные строк**: tooa переменной можно назначить для каждого выражения запроса, который возвращает набор строк.</span><span class="sxs-lookup"><span data-stu-id="f59eb-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="f59eb-124">U-SQL соответствует шаблону именования переменных hello T-SQL (`@searchlog`, например) в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="f59eb-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="f59eb-125">Hello **ИЗВЛЕЧЬ** ключевое слово считывает данные из файла и определяется hello схемы для чтения.</span><span class="sxs-lookup"><span data-stu-id="f59eb-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="f59eb-126">`Extractors.Tsv` — это встроенное средство извлечения U-SQL для файлов со значениями с разделением знаками табуляции.</span><span class="sxs-lookup"><span data-stu-id="f59eb-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="f59eb-127">Можно разрабатывать пользовательские средства извлечения.</span><span class="sxs-lookup"><span data-stu-id="f59eb-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="f59eb-128">Hello **ВЫВОДА** записывает данные из файла tooa набора строк.</span><span class="sxs-lookup"><span data-stu-id="f59eb-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="f59eb-129">`Outputters.Csv()`— Это файл с разделителями запятыми для встроенных toocreate outputter U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f59eb-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="f59eb-130">Вы можете разработать собственные средства вывода.</span><span class="sxs-lookup"><span data-stu-id="f59eb-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="f59eb-131">Пути к файлам</span><span class="sxs-lookup"><span data-stu-id="f59eb-131">File paths</span></span>

<span data-ttu-id="f59eb-132">Hello ИЗВЛЕЧЕНИЯ и выходные данные инструкции используйте пути к файлам.</span><span class="sxs-lookup"><span data-stu-id="f59eb-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="f59eb-133">Пути к файлам могут быть абсолютными или относительными.</span><span class="sxs-lookup"><span data-stu-id="f59eb-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="f59eb-134">Это следующий абсолютный путь к файлу ссылается файл tooa в хранилище Озера данных с именем `mystore`:</span><span class="sxs-lookup"><span data-stu-id="f59eb-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="f59eb-135">Следующий относительный путь к файлу начинается с `"/"`.</span><span class="sxs-lookup"><span data-stu-id="f59eb-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="f59eb-136">Он ссылается файл tooa в учетной записи хранилища Озера данных по умолчанию hello:</span><span class="sxs-lookup"><span data-stu-id="f59eb-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="f59eb-137">Использование скалярных переменных</span><span class="sxs-lookup"><span data-stu-id="f59eb-137">Use scalar variables</span></span>

<span data-ttu-id="f59eb-138">Можно использовать скалярные переменные как хорошо toomake обслуживания сценарий проще.</span><span class="sxs-lookup"><span data-stu-id="f59eb-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="f59eb-139">Hello предыдущий скрипт U-SQL также может быть записан следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f59eb-139">hello previous U-SQL script can also be written as:</span></span>

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
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="f59eb-140">Преобразования наборов строк</span><span class="sxs-lookup"><span data-stu-id="f59eb-140">Transform rowsets</span></span>

<span data-ttu-id="f59eb-141">Используйте **ВЫБЕРИТЕ** tootransform наборы строк:</span><span class="sxs-lookup"><span data-stu-id="f59eb-141">Use **SELECT** tootransform rowsets:</span></span>

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
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="f59eb-142">Здравствуйте, предложение WHERE использует [C# логическое выражение](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="f59eb-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="f59eb-143">Toodo языка, hello C# выражение можно использовать собственные выражения и функции.</span><span class="sxs-lookup"><span data-stu-id="f59eb-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="f59eb-144">Можно даже выполнить более сложную фильтрацию, сочетая их с помощью логического объединения (and) и разделения (or).</span><span class="sxs-lookup"><span data-stu-id="f59eb-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="f59eb-145">Hello следующий скрипт использует метод DateTime.Parse() hello и вместе.</span><span class="sxs-lookup"><span data-stu-id="f59eb-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="f59eb-146">второй запрос Hello работает на результат hello hello первый набор строк, создающий составной hello два фильтра.</span><span class="sxs-lookup"><span data-stu-id="f59eb-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="f59eb-147">Также можно повторно использовать имя переменной, а лексически относятся имена hello.</span><span class="sxs-lookup"><span data-stu-id="f59eb-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="f59eb-148">Агрегированные наборы строк</span><span class="sxs-lookup"><span data-stu-id="f59eb-148">Aggregate rowsets</span></span>
<span data-ttu-id="f59eb-149">U-SQL предоставляет hello знакомы ORDER BY, GROUP BY и агрегаты.</span><span class="sxs-lookup"><span data-stu-id="f59eb-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="f59eb-150">Hello следующий запрос находит общая длительность hello по регионам, а затем отображает hello верхней пять длительности в порядке.</span><span class="sxs-lookup"><span data-stu-id="f59eb-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="f59eb-151">Наборы строк U-SQL не сохранять их порядок для следующего запроса hello.</span><span class="sxs-lookup"><span data-stu-id="f59eb-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="f59eb-152">Таким образом, tooorder выход, необходимо tooadd ORDER BY toohello выходных данных инструкции:</span><span class="sxs-lookup"><span data-stu-id="f59eb-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

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
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="f59eb-153">Hello U-SQL предложение ORDER BY, необходимо использовать предложения FETCH hello в выражении SELECT.</span><span class="sxs-lookup"><span data-stu-id="f59eb-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="f59eb-154">можно использовать toorestrict hello вывода toogroups, удовлетворяют условиям HAVING hello предложение U-SQL с Hello:</span><span class="sxs-lookup"><span data-stu-id="f59eb-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="f59eb-155">При использовании дополнительных статистических см hello hello U-SQL справочной документации для [статистической обработки, аналитические и ссылаться на функции](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="f59eb-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f59eb-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f59eb-156">Next steps</span></span>
* [<span data-ttu-id="f59eb-157">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="f59eb-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="f59eb-158">Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f59eb-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
