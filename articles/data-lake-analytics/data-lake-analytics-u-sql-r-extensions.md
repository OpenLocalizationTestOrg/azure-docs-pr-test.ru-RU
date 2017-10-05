---
title: "Расширение возможностей скриптов U-SQL c R в Azure Data Lake Analytics | Документация Майкрософт"
description: "Узнайте о том, как выполнять код R в скриптах U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: d479af515566f497d9611e75426f6acb8f8276d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="918ff-103">Руководство. Начало работы с расширением возможностей U-SQL c R</span><span class="sxs-lookup"><span data-stu-id="918ff-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="918ff-104">В следующих примерах представлены основные шаги по развертыванию кода R:</span><span class="sxs-lookup"><span data-stu-id="918ff-104">The following example illustrates the basic steps for deploying R code:</span></span>
* <span data-ttu-id="918ff-105">Используйте инструкцию `REFERENCE ASSEMBLY`, чтобы включить расширения R для скрипта U-SQL.</span><span class="sxs-lookup"><span data-stu-id="918ff-105">Use the `REFERENCE ASSEMBLY` statement to enable R extensions for the U-SQL Script.</span></span>
* <span data-ttu-id="918ff-106">Используйте операцию ` REDUCE` для разделения входных данных в ключе.</span><span class="sxs-lookup"><span data-stu-id="918ff-106">Use the` REDUCE` operation to partition the input data on a key.</span></span>
* <span data-ttu-id="918ff-107">Расширения R для U-SQL включают встроенное средство редукции (`Extension.R.Reducer`), которое выполняет код R в каждой назначенной ему вершине.</span><span class="sxs-lookup"><span data-stu-id="918ff-107">The R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned to the reducer.</span></span> 
* <span data-ttu-id="918ff-108">Передача данных между U-SQL и R с использованием выделенных именованных таблиц данных `inputFromUSQL` и `outputToUSQL ` соответственно. Имена идентификаторов входной и выходной таблицы данных исправлены (то есть пользователи не могут изменить эти предопределенные имена идентификаторов входной и выходной таблицы данных).</span><span class="sxs-lookup"><span data-stu-id="918ff-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively to pass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-the-u-sql-script"></a><span data-ttu-id="918ff-109">Внедрение кода R в скрипт U-SQL</span><span class="sxs-lookup"><span data-stu-id="918ff-109">Embedding R code in the U-SQL script</span></span>

<span data-ttu-id="918ff-110">Код R можно встроить в скрипт U-SQL с помощью параметра команды средства `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="918ff-110">You can inline the R code your U-SQL script by using the command parameter of the `Extension.R.Reducer`.</span></span> <span data-ttu-id="918ff-111">Например, можно объявить скрипт R как строковую переменную и передать его в качестве параметра в Reducer.</span><span class="sxs-lookup"><span data-stu-id="918ff-111">For example, you can declare the R script as a string variable and pass it as a parameter to the Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that the column names are the same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a><span data-ttu-id="918ff-112">Сохраните код R в отдельном файле и ссылайтесь на него в скрипте U-SQL</span><span class="sxs-lookup"><span data-stu-id="918ff-112">Keep the R code in a separate file and reference it  the U-SQL script</span></span>

<span data-ttu-id="918ff-113">В следующем примере демонстрируется более сложное использование.</span><span class="sxs-lookup"><span data-stu-id="918ff-113">The following example illustrates a more complex usage.</span></span> <span data-ttu-id="918ff-114">В этом случае код R развертывается как RESOURCE, который является скриптом U-SQL.</span><span class="sxs-lookup"><span data-stu-id="918ff-114">In this case, the R code is deployed as a RESOURCE that is the U-SQL script.</span></span>

<span data-ttu-id="918ff-115">Сохраните этот код R как отдельный файл.</span><span class="sxs-lookup"><span data-stu-id="918ff-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="918ff-116">Используйте скрипт U-SQL для развертывания этого скрипта R с оператором DEPLOY RESOURCE.</span><span class="sxs-lookup"><span data-stu-id="918ff-116">Use a U-SQL script to deploy that R script with the DEPLOY RESOURCE statement.</span></span>

    REFERENCE ASSEMBLY [ExtR];

    DEPLOY RESOURCE @"/usqlext/samples/R/RinUSQL_PredictUsingLinearModelasDF.R";
    DEPLOY RESOURCE @"/usqlext/samples/R/my_model_LM_Iris.rda";
    DECLARE @IrisData string = @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFilePredictions string = @"/my/R/Output/LMPredictionsIris.txt";
    DECLARE @PartitionCount int = 10;

    @InputData =
        EXTRACT 
            SepalLength double,
            SepalWidth double,
            PetalLength double,
            PetalWidth double,
            Species string
        FROM @IrisData
        USING Extractors.Csv();

    @ExtendedData =
        SELECT 
            Extension.R.RandomNumberGenerator.GetRandomNumber(@PartitionCount) AS Par,
            SepalLength,
            SepalWidth,
            PetalLength,
            PetalWidth
        FROM @InputData;

    // Predict Species

    @RScriptOutput = REDUCE @ExtendedData ON Par
        PRODUCE Par, fit double, lwr double, upr double
        READONLY Par
        USING new Extension.R.Reducer(scriptFile:"RinUSQL_PredictUsingLinearModelasDF.R", rReturnType:"dataframe", stringsAsFactors:false);
        OUTPUT @RScriptOutput TO @OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="918ff-117">Интеграция R c U-SQL</span><span class="sxs-lookup"><span data-stu-id="918ff-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="918ff-118">Типы данных</span><span class="sxs-lookup"><span data-stu-id="918ff-118">Datatypes</span></span>
* <span data-ttu-id="918ff-119">Строковые и числовые столбцы из U-SQL преобразуются без изменений между таблицей данных на R и U-SQL [поддерживаемые типы: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="918ff-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="918ff-120">Тип данных `Factor` не поддерживается в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="918ff-120">The `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="918ff-121">Тип `byte[]` должен быть сериализован как строка `string` в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="918ff-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="918ff-122">После создания в U-SQL входной таблицы данных R или установки для параметра средства редукции `stringsAsFactors: true` значения true строки U-SQL можно преобразовать в коэффициенты кода R.</span><span class="sxs-lookup"><span data-stu-id="918ff-122">U-SQL strings can be converted to factors in R code, once U-SQL create R input dataframe or by setting the reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="918ff-123">Схемы</span><span class="sxs-lookup"><span data-stu-id="918ff-123">Schemas</span></span>
* <span data-ttu-id="918ff-124">Наборы данных U-SQL не могут содержать повторяемые имена столбцов.</span><span class="sxs-lookup"><span data-stu-id="918ff-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="918ff-125">Имена столбцов в наборах данных U-SQL должны быть строками.</span><span class="sxs-lookup"><span data-stu-id="918ff-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="918ff-126">Имена столбцов в скриптах U-SQL и R должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="918ff-126">Column names must be the same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="918ff-127">Столбцы с доступом только для чтения не могут быть частью выходной таблицы данных,</span><span class="sxs-lookup"><span data-stu-id="918ff-127">Readonly column cannot be part of the output dataframe.</span></span> <span data-ttu-id="918ff-128">так как они автоматически вставляются обратно в таблицу U-SQL (если она является частью выходной схемы определяемых пользователем объектов).</span><span class="sxs-lookup"><span data-stu-id="918ff-128">Because readonly columns are automatically injected back in the U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="918ff-129">Ограничения функциональных возможностей</span><span class="sxs-lookup"><span data-stu-id="918ff-129">Functional limitations</span></span>
* <span data-ttu-id="918ff-130">Ядро R нельзя создать дважды в одном процессе.</span><span class="sxs-lookup"><span data-stu-id="918ff-130">The R Engine can't be instantiated twice in the same process.</span></span> 
* <span data-ttu-id="918ff-131">В настоящее время U-SQL не поддерживает определяемые пользователем операторы Combiner для прогнозирования с помощью секционированных моделей, созданных с использованием определяемых пользователем операторов Reducer.</span><span class="sxs-lookup"><span data-stu-id="918ff-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="918ff-132">Пользователи могут объявить секционированные модели как ресурс и использовать их в своих скриптах R (см. пример кода `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="918ff-132">Users can declare the partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="918ff-133">Версии R</span><span class="sxs-lookup"><span data-stu-id="918ff-133">R Versions</span></span>
<span data-ttu-id="918ff-134">Поддерживается только R 3.2.2.</span><span class="sxs-lookup"><span data-stu-id="918ff-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="918ff-135">Стандартные модули R</span><span class="sxs-lookup"><span data-stu-id="918ff-135">Standard R modules</span></span>

    base
    boot
    Class
    Cluster
    codetools
    compiler
    datasets
    doParallel
    doRSR
    foreach
    foreign
    Graphics
    grDevices
    grid
    iterators
    KernSmooth
    lattice
    MASS
    Matrix
    Methods
    mgcv
    nlme
    Nnet
    Parallel
    pkgXMLBuilder
    RevoIOQ
    revoIpe
    RevoMods
    RevoPemaR
    RevoRpeConnector
    RevoRsrConnector
    RevoScaleR
    RevoTreeView
    RevoUtils
    RevoUtilsMath
    Rpart
    RUnit
    spatial
    splines
    Stats
    stats4
    survival
    Tcltk
    Tools
    translations
    utils
    XML

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="918ff-136">Ограничения размера входных и выходных данных</span><span class="sxs-lookup"><span data-stu-id="918ff-136">Input and Output size limitations</span></span>
<span data-ttu-id="918ff-137">Каждой вершине назначен ограниченный объем памяти.</span><span class="sxs-lookup"><span data-stu-id="918ff-137">Every vertex has a limited amount of memory assigned to it.</span></span> <span data-ttu-id="918ff-138">Так как входящие и исходящие кадры данных должны существовать в памяти кода R, общий размер входных и выходных данных должен находиться в пределах 500 ГБ.</span><span class="sxs-lookup"><span data-stu-id="918ff-138">Because the input and output DataFrames must exist in memory in the R code, the total size for the input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="918ff-139">Пример кода</span><span class="sxs-lookup"><span data-stu-id="918ff-139">Sample Code</span></span>
<span data-ttu-id="918ff-140">Дополнительные примеры кода доступны в вашей учетной записи Data Lake Store после установки расширений расширенной аналитики U-SQL.</span><span class="sxs-lookup"><span data-stu-id="918ff-140">More sample code is available in your Data Lake Store account after you install the U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="918ff-141">Путь к другим примерам кода: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="918ff-141">The path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="918ff-142">Развертывание настраиваемых модулей R с помощью U-SQL</span><span class="sxs-lookup"><span data-stu-id="918ff-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="918ff-143">Сначала создайте настраиваемый модуль R, заархивируйте его в ZIP-файл, а затем отправьте этот ZIP-файл с настраиваемым модулем в хранилище ADL.</span><span class="sxs-lookup"><span data-stu-id="918ff-143">First, create an R custom module and zip it and then upload the zipped R custom module file to your ADL store.</span></span> <span data-ttu-id="918ff-144">В этом примере файл magittr_1.5.zip будет отправлен в корень учетной записи ADLS по умолчанию для используемой учетной записи ADLA.</span><span class="sxs-lookup"><span data-stu-id="918ff-144">In the example, we will upload magittr_1.5.zip to the root of the default ADLS account for the ADLA account we are using.</span></span> <span data-ttu-id="918ff-145">После отправки модуля в хранилище ADL объявите его с помощью DEPLOY RESOURCE, чтобы сделать этот модуль доступным в скрипте U-SQL, затем вызовите метод `install.packages`, чтобы установить его.</span><span class="sxs-lookup"><span data-stu-id="918ff-145">Once you upload the module to ADL store, declare it as use DEPLOY RESOURCE to make it available in your U-SQL script and call `install.packages` to install it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script to run
    DECLARE @myRScript = @"
    # install the magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load the magrittr package,
    require(magrittr),
    # demonstrate use of the magrittr package,
    2 %>% sqrt
    ";

    @InputData =
    EXTRACT SepalLength double,
    SepalWidth double,
    PetalLength double,
    PetalWidth double,
    Species string
    FROM @IrisData
    USING Extractors.Csv();

    @ExtendedData =
    SELECT 0 AS Par,
    *
    FROM @InputData;

    @RScriptOutput = REDUCE @ExtendedData ON Par
    PRODUCE Par, RowId int, ROutput string
    READONLY Par
    USING new Extension.R.Reducer(command:@myRScript, rReturnType:"charactermatrix");

    OUTPUT @RScriptOutput TO @OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="918ff-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="918ff-146">Next Steps</span></span>
* [<span data-ttu-id="918ff-147">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="918ff-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="918ff-148">Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="918ff-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="918ff-149">Использование оконных функций U-SQL для заданий в службе аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="918ff-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
