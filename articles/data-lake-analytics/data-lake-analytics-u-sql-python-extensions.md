---
title: "сценарии aaaExtend U-SQL для Python в аналитике Озера данных Azure | Документы Microsoft"
description: "Узнайте о том, как код toorun Python в скриптах U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="3e8e5-103">Руководство. Начало работы с расширением возможностей U-SQL c Python</span><span class="sxs-lookup"><span data-stu-id="3e8e5-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="3e8e5-104">Расширения Python для U-SQL позволяют разработчикам tooperform массово-параллельные выполнения кода Python.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="3e8e5-105">Привет, следующий пример иллюстрирует hello основные шаги:</span><span class="sxs-lookup"><span data-stu-id="3e8e5-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="3e8e5-106">Используйте hello `REFERENCE ASSEMBLY` инструкции tooenable Python расширения для hello скрипт U-SQL</span><span class="sxs-lookup"><span data-stu-id="3e8e5-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="3e8e5-107">С помощью hello `REDUCE` операции toopartition hello входные данные по ключу</span><span class="sxs-lookup"><span data-stu-id="3e8e5-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="3e8e5-108">Hello Python расширения для U-SQL включают в себя встроенные редуктора (`Extension.Python.Reducer`) работают на каждый редуктора toohello вершин назначенный код Python</span><span class="sxs-lookup"><span data-stu-id="3e8e5-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="3e8e5-109">Hello скрипт U-SQL содержит код Python внедренных hello, который содержит функцию с именем `usqlml_main` , pandas кадр данных в качестве входных данных принимает и возвращает pandas кадр данных в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="3e8e5-110">Интеграция Python c U-SQL</span><span class="sxs-lookup"><span data-stu-id="3e8e5-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="3e8e5-111">Типы данных</span><span class="sxs-lookup"><span data-stu-id="3e8e5-111">Datatypes</span></span>

* <span data-ttu-id="3e8e5-112">Строковые и числовые столбцы из U-SQL преобразовываются без изменений между Pandas и U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="3e8e5-113">Значения NULL U-SQL, преобразованный tooand из Pandas `NA` значения</span><span class="sxs-lookup"><span data-stu-id="3e8e5-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="3e8e5-114">Схемы</span><span class="sxs-lookup"><span data-stu-id="3e8e5-114">Schemas</span></span>

* <span data-ttu-id="3e8e5-115">Векторы индексов в Pandas не поддерживаются в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="3e8e5-116">Все кадры входных данных в функции hello Python всегда имеют 64-разрядных числовой индекс от 0 до hello количества строк минус 1.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="3e8e5-117">Наборы данных U-SQL не могут содержать повторяемые имена столбцов.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="3e8e5-118">Имена столбцов в наборах данных не являются строками.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="3e8e5-119">Версии Python</span><span class="sxs-lookup"><span data-stu-id="3e8e5-119">Python Versions</span></span>
<span data-ttu-id="3e8e5-120">Поддерживается только версия Python 3.5.1 (скомпилированная для Windows).</span><span class="sxs-lookup"><span data-stu-id="3e8e5-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="3e8e5-121">Стандартные модули Python</span><span class="sxs-lookup"><span data-stu-id="3e8e5-121">Standard Python modules</span></span>
<span data-ttu-id="3e8e5-122">Включены все hello модули Python.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="3e8e5-123">Дополнительные модули Python</span><span class="sxs-lookup"><span data-stu-id="3e8e5-123">Additional Python modules</span></span>
<span data-ttu-id="3e8e5-124">Помимо hello стандартные библиотеки Python, включены несколько библиотек часто используемые python.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="3e8e5-125">Сообщения об исключении</span><span class="sxs-lookup"><span data-stu-id="3e8e5-125">Exception Messages</span></span>
<span data-ttu-id="3e8e5-126">В настоящее время исключение в коде Python отображается в качестве общего сбоя вершины.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="3e8e5-127">В будущем hello hello задания U-SQL, сообщения об ошибках будут отображаться сообщение об исключении hello Python.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="3e8e5-128">Ограничения размера входных и выходных данных</span><span class="sxs-lookup"><span data-stu-id="3e8e5-128">Input and Output size limitations</span></span>
<span data-ttu-id="3e8e5-129">Каждая вершина имеет ограниченный объем памяти, назначенный tooit.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="3e8e5-130">В настоящее время он составляет 6 ГБ на единицу аналитики.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="3e8e5-131">Поскольку hello блоки входных и выходных данных должна существовать в памяти в коде Python hello, hello общий размер для hello ввода и вывода не может превышать 6 ГБ.</span><span class="sxs-lookup"><span data-stu-id="3e8e5-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="3e8e5-132">См. также</span><span class="sxs-lookup"><span data-stu-id="3e8e5-132">See also</span></span>
* [<span data-ttu-id="3e8e5-133">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="3e8e5-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="3e8e5-134">Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3e8e5-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="3e8e5-135">Использование оконных функций U-SQL для заданий в службе аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="3e8e5-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

