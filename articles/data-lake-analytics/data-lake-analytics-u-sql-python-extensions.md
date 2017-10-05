---
title: "Расширение возможностей сценариев U-SQL c Python в Azure Data Lake Analytics | Документы Microsoft"
description: "Узнайте о том, как выполнять код Python в сценариях U-SQL"
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
ms.openlocfilehash: d18ef1f747aee2fa01cef9891432d0461031ee4c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="098ff-103">Руководство. Начало работы с расширением возможностей U-SQL c Python</span><span class="sxs-lookup"><span data-stu-id="098ff-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="098ff-104">Расширения Python для U-SQL позволяют разработчикам выполнять код Python с массовым параллелизмом.</span><span class="sxs-lookup"><span data-stu-id="098ff-104">Python Extensions for U-SQL enable developers to perform massively parallel execution of Python code.</span></span> <span data-ttu-id="098ff-105">В следующих примерах представлены основные шаги:</span><span class="sxs-lookup"><span data-stu-id="098ff-105">The following example illustrates the basic steps:</span></span>

* <span data-ttu-id="098ff-106">Используйте инструкцию `REFERENCE ASSEMBLY`, чтобы включить расширения Python для сценария U-SQL</span><span class="sxs-lookup"><span data-stu-id="098ff-106">Use the `REFERENCE ASSEMBLY` statement to enable Python extensions for the U-SQL Script</span></span>
* <span data-ttu-id="098ff-107">Использование операции `REDUCE` для разделения входных данных в разделе</span><span class="sxs-lookup"><span data-stu-id="098ff-107">Using the `REDUCE` operation to partition the input data on a key</span></span>
* <span data-ttu-id="098ff-108">Расширения Python для U-SQL включают встроенный инструмент редукции (`Extension.Python.Reducer`), который выполняет код Python в каждой вершине, назначенный инструменту редукции.</span><span class="sxs-lookup"><span data-stu-id="098ff-108">The Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned to the reducer</span></span>
* <span data-ttu-id="098ff-109">Сценарий U-SQL содержит встроенный код Python с функцией `usqlml_main`, которая принимает кадр данных Pandas в качестве входных данных и возвращает его в качестве выходных данных.</span><span class="sxs-lookup"><span data-stu-id="098ff-109">The U-SQL script contains the embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

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
        TO "/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="098ff-110">Интеграция Python c U-SQL</span><span class="sxs-lookup"><span data-stu-id="098ff-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="098ff-111">Типы данных</span><span class="sxs-lookup"><span data-stu-id="098ff-111">Datatypes</span></span>

* <span data-ttu-id="098ff-112">Строковые и числовые столбцы из U-SQL преобразовываются без изменений между Pandas и U-SQL.</span><span class="sxs-lookup"><span data-stu-id="098ff-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="098ff-113">Пустые значения U-SQL преобразовываются в значения Pandas `NA` и из них.</span><span class="sxs-lookup"><span data-stu-id="098ff-113">U-SQL Nulls are converted to and from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="098ff-114">Схемы</span><span class="sxs-lookup"><span data-stu-id="098ff-114">Schemas</span></span>

* <span data-ttu-id="098ff-115">Векторы индексов в Pandas не поддерживаются в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="098ff-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="098ff-116">Все входные кадры данных в функции Python будут всегда содержать 64-разрядный числовой индекс от 0 до соответствующего количества строк минус 1.</span><span class="sxs-lookup"><span data-stu-id="098ff-116">All input data frames in the Python function always have a 64-bit numerical index from 0 through the number of rows minus 1.</span></span> 
* <span data-ttu-id="098ff-117">Наборы данных U-SQL не могут содержать повторяемые имена столбцов.</span><span class="sxs-lookup"><span data-stu-id="098ff-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="098ff-118">Имена столбцов в наборах данных не являются строками.</span><span class="sxs-lookup"><span data-stu-id="098ff-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="098ff-119">Версии Python</span><span class="sxs-lookup"><span data-stu-id="098ff-119">Python Versions</span></span>
<span data-ttu-id="098ff-120">Поддерживается только версия Python 3.5.1 (скомпилированная для Windows).</span><span class="sxs-lookup"><span data-stu-id="098ff-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="098ff-121">Стандартные модули Python</span><span class="sxs-lookup"><span data-stu-id="098ff-121">Standard Python modules</span></span>
<span data-ttu-id="098ff-122">Включены все стандартные модули Python.</span><span class="sxs-lookup"><span data-stu-id="098ff-122">All the standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="098ff-123">Дополнительные модули Python</span><span class="sxs-lookup"><span data-stu-id="098ff-123">Additional Python modules</span></span>
<span data-ttu-id="098ff-124">Кроме стандартных библиотек Python, включены несколько часто используемых библиотек Python:</span><span class="sxs-lookup"><span data-stu-id="098ff-124">Besides the standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="098ff-125">Сообщения об исключении</span><span class="sxs-lookup"><span data-stu-id="098ff-125">Exception Messages</span></span>
<span data-ttu-id="098ff-126">В настоящее время исключение в коде Python отображается в качестве общего сбоя вершины.</span><span class="sxs-lookup"><span data-stu-id="098ff-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="098ff-127">В будущем в сообщениях об ошибках заданий U-SQL будут отображаться сообщения об исключении Python.</span><span class="sxs-lookup"><span data-stu-id="098ff-127">In the future, the U-SQL Job error messages will display the Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="098ff-128">Ограничения размера входных и выходных данных</span><span class="sxs-lookup"><span data-stu-id="098ff-128">Input and Output size limitations</span></span>
<span data-ttu-id="098ff-129">Каждой вершине назначен ограниченный объем памяти.</span><span class="sxs-lookup"><span data-stu-id="098ff-129">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="098ff-130">В настоящее время он составляет 6 ГБ на единицу аналитики.</span><span class="sxs-lookup"><span data-stu-id="098ff-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="098ff-131">Так как входящие и исходящие кадры данных должны существовать в памяти кода Python, общий размер входных и выходных данных должен находиться в пределах 6 ГБ.</span><span class="sxs-lookup"><span data-stu-id="098ff-131">Because the input and output DataFrames must exist in memory in the Python code, the total size for the input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="098ff-132">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="098ff-132">See also</span></span>
* [<span data-ttu-id="098ff-133">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="098ff-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="098ff-134">Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="098ff-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="098ff-135">Использование оконных функций U-SQL для заданий в службе аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="098ff-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

