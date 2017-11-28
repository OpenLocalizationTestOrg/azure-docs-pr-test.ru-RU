---
title: "aaaExtend U-SQL скрипты с языком R в аналитике Озера данных Azure | Документы Microsoft"
description: "Узнайте о том, как код toorun R в скриптах U-SQL"
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
ms.openlocfilehash: 24affd4963a08d30a7111b49af388e9c1268430e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a><span data-ttu-id="5c612-103">Руководство. Начало работы с расширением возможностей U-SQL c R</span><span class="sxs-lookup"><span data-stu-id="5c612-103">Tutorial: Get started with extending U-SQL with R</span></span>

<span data-ttu-id="5c612-104">Следующий пример Hello рассмотрены основные шаги развертывания кода R hello:</span><span class="sxs-lookup"><span data-stu-id="5c612-104">hello following example illustrates hello basic steps for deploying R code:</span></span>
* <span data-ttu-id="5c612-105">Используйте hello `REFERENCE ASSEMBLY` расширения tooenable R инструкции для hello скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5c612-105">Use hello `REFERENCE ASSEMBLY` statement tooenable R extensions for hello U-SQL Script.</span></span>
* <span data-ttu-id="5c612-106">Используйте` REDUCE` операции toopartition hello входные данные по ключу.</span><span class="sxs-lookup"><span data-stu-id="5c612-106">Use the` REDUCE` operation toopartition hello input data on a key.</span></span>
* <span data-ttu-id="5c612-107">расширения Hello R для U-SQL включают в себя встроенные редуктора (`Extension.R.Reducer`), которое будет выполняться код R на каждой вершины назначенный toohello редуктора.</span><span class="sxs-lookup"><span data-stu-id="5c612-107">hello R extensions for U-SQL include a built-in reducer (`Extension.R.Reducer`) that runs R code on each vertex assigned toohello reducer.</span></span> 
* <span data-ttu-id="5c612-108">Использование выделенного с именем кадров данных называется `inputFromUSQL` и `outputToUSQL `соответственно toopass данных между U-SQL и R. ввода и вывода исправленные имена идентификаторов кадр данных (то есть, пользователи не могут изменить эти стандартные имена входных данных и вывода кадр данных идентификаторы).</span><span class="sxs-lookup"><span data-stu-id="5c612-108">Usage of dedicated named data frames called `inputFromUSQL` and `outputToUSQL `respectively toopass data between U-SQL and R. Input and output DataFrame identifier names are fixed (that is, users cannot change these predefined names of input and output DataFrame identifiers).</span></span>

## <a name="embedding-r-code-in-hello-u-sql-script"></a><span data-ttu-id="5c612-109">Внедрение кода R в hello скрипт U-SQL</span><span class="sxs-lookup"><span data-stu-id="5c612-109">Embedding R code in hello U-SQL script</span></span>

<span data-ttu-id="5c612-110">Вы можете hello R во встроенном коде на ваш скрипт U-SQL с помощью параметра команды hello hello `Extension.R.Reducer`.</span><span class="sxs-lookup"><span data-stu-id="5c612-110">You can inline hello R code your U-SQL script by using hello command parameter of hello `Extension.R.Reducer`.</span></span> <span data-ttu-id="5c612-111">Например можно объявить hello сценария R в переменной строки и передайте его в качестве параметра toohello редуктора.</span><span class="sxs-lookup"><span data-stu-id="5c612-111">For example, you can declare hello R script as a string variable and pass it as a parameter toohello Reducer.</span></span>


    REFERENCE ASSEMBLY [ExtR];
    
    DECLARE @myRScript = @"
    inputFromUSQL$Species = as.factor(inputFromUSQL$Species)
    lm.fit=lm(unclass(Species)~.-Par, data=inputFromUSQL)
    #do not return readonly columns and make sure that hello column names are hello same in usql and r scripts,
    outputToUSQL=data.frame(summary(lm.fit)$coefficients)
    colnames(outputToUSQL) <- c(""Estimate"", ""StdError"", ""tValue"", ""Pr"")
    outputToUSQL
    ";
    
    @RScriptOutput = REDUCE … USING new Extension.R.Reducer(command:@myRScript, rReturnType:"dataframe");

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a><span data-ttu-id="5c612-112">Сохранить в отдельном файле кода hello R и ссылок на него скрипт hello U-SQL</span><span class="sxs-lookup"><span data-stu-id="5c612-112">Keep hello R code in a separate file and reference it  hello U-SQL script</span></span>

<span data-ttu-id="5c612-113">Следующий пример Hello рассмотрены более сложные использования.</span><span class="sxs-lookup"><span data-stu-id="5c612-113">hello following example illustrates a more complex usage.</span></span> <span data-ttu-id="5c612-114">В этом случае код hello R развертывается как РЕСУРС, который является hello скрипт U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5c612-114">In this case, hello R code is deployed as a RESOURCE that is hello U-SQL script.</span></span>

<span data-ttu-id="5c612-115">Сохраните этот код R как отдельный файл.</span><span class="sxs-lookup"><span data-stu-id="5c612-115">Save this R code as a separate file.</span></span>

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

<span data-ttu-id="5c612-116">Используйте этот скрипт R toodeploy скрипт U-SQL с hello инструкции РАЗВЕРТЫВАНИЯ РЕСУРСОВ.</span><span class="sxs-lookup"><span data-stu-id="5c612-116">Use a U-SQL script toodeploy that R script with hello DEPLOY RESOURCE statement.</span></span>

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
        OUTPUT @RScriptOutput too@OutputFilePredictions USING Outputters.Tsv();

## <a name="how-r-integrates-with-u-sql"></a><span data-ttu-id="5c612-117">Интеграция R c U-SQL</span><span class="sxs-lookup"><span data-stu-id="5c612-117">How R Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="5c612-118">Типы данных</span><span class="sxs-lookup"><span data-stu-id="5c612-118">Datatypes</span></span>
* <span data-ttu-id="5c612-119">Строковые и числовые столбцы из U-SQL преобразуются без изменений между таблицей данных на R и U-SQL [поддерживаемые типы: `double`, `string`, `bool`, `integer`, `byte`].</span><span class="sxs-lookup"><span data-stu-id="5c612-119">String and numeric columns from U-SQL are converted as-is between R DataFrame and U-SQL [supported types: `double`, `string`, `bool`, `integer`, `byte`].</span></span>
* <span data-ttu-id="5c612-120">Hello `Factor` тип данных не поддерживается в U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5c612-120">hello `Factor` datatype is not supported in U-SQL.</span></span>
* <span data-ttu-id="5c612-121">Тип `byte[]` должен быть сериализован как строка `string` в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="5c612-121">`byte[]` must be serialized as a base64-encoded `string`.</span></span>
* <span data-ttu-id="5c612-122">Строки U-SQL могут быть toofactors, преобразованное в коде R, один раз U-SQL создать входной кадр данных R или параметром задание hello редуктора `stringsAsFactors: true`.</span><span class="sxs-lookup"><span data-stu-id="5c612-122">U-SQL strings can be converted toofactors in R code, once U-SQL create R input dataframe or by setting hello reducer parameter `stringsAsFactors: true`.</span></span>

### <a name="schemas"></a><span data-ttu-id="5c612-123">Схемы</span><span class="sxs-lookup"><span data-stu-id="5c612-123">Schemas</span></span>
* <span data-ttu-id="5c612-124">Наборы данных U-SQL не могут содержать повторяемые имена столбцов.</span><span class="sxs-lookup"><span data-stu-id="5c612-124">U-SQL datasets cannot have duplicate column names.</span></span>
* <span data-ttu-id="5c612-125">Имена столбцов в наборах данных U-SQL должны быть строками.</span><span class="sxs-lookup"><span data-stu-id="5c612-125">U-SQL datasets column names must be strings.</span></span>
* <span data-ttu-id="5c612-126">Имена столбцов должны hello же U-SQL и R-сценариев.</span><span class="sxs-lookup"><span data-stu-id="5c612-126">Column names must be hello same in U-SQL and R scripts.</span></span>
* <span data-ttu-id="5c612-127">Только для чтения столбец не может быть частью блока hello выходных данных.</span><span class="sxs-lookup"><span data-stu-id="5c612-127">Readonly column cannot be part of hello output dataframe.</span></span> <span data-ttu-id="5c612-128">Так как столбцы только для чтения автоматически добавляются обратно в таблице hello U-SQL, если он является частью схемы вывода данных из определяемого пользователем ОПЕРАТОРА.</span><span class="sxs-lookup"><span data-stu-id="5c612-128">Because readonly columns are automatically injected back in hello U-SQL table if it is a part of output schema of UDO.</span></span>

### <a name="functional-limitations"></a><span data-ttu-id="5c612-129">Ограничения функциональных возможностей</span><span class="sxs-lookup"><span data-stu-id="5c612-129">Functional limitations</span></span>
* <span data-ttu-id="5c612-130">Hello модуль R не может быть создан в два раза hello одного процесса.</span><span class="sxs-lookup"><span data-stu-id="5c612-130">hello R Engine can't be instantiated twice in hello same process.</span></span> 
* <span data-ttu-id="5c612-131">В настоящее время U-SQL не поддерживает определяемые пользователем операторы Combiner для прогнозирования с помощью секционированных моделей, созданных с использованием определяемых пользователем операторов Reducer.</span><span class="sxs-lookup"><span data-stu-id="5c612-131">Currently, U-SQL does not support Combiner UDOs for prediction using partitioned models generated using Reducer UDOs.</span></span> <span data-ttu-id="5c612-132">Пользователи могут объявить hello секционированы моделей в качестве ресурса и использовать их в R-сценария (см. пример кода `ExtR_PredictUsingLMRawStringReducer.usql`)</span><span class="sxs-lookup"><span data-stu-id="5c612-132">Users can declare hello partitioned models as resource and use them in their R Script (see sample code `ExtR_PredictUsingLMRawStringReducer.usql`)</span></span>

### <a name="r-versions"></a><span data-ttu-id="5c612-133">Версии R</span><span class="sxs-lookup"><span data-stu-id="5c612-133">R Versions</span></span>
<span data-ttu-id="5c612-134">Поддерживается только R 3.2.2.</span><span class="sxs-lookup"><span data-stu-id="5c612-134">Only R 3.2.2 is supported.</span></span>

### <a name="standard-r-modules"></a><span data-ttu-id="5c612-135">Стандартные модули R</span><span class="sxs-lookup"><span data-stu-id="5c612-135">Standard R modules</span></span>

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

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="5c612-136">Ограничения размера входных и выходных данных</span><span class="sxs-lookup"><span data-stu-id="5c612-136">Input and Output size limitations</span></span>
<span data-ttu-id="5c612-137">Каждая вершина имеет ограниченный объем памяти, назначенный tooit.</span><span class="sxs-lookup"><span data-stu-id="5c612-137">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="5c612-138">Поскольку hello блоки входных и выходных данных должна существовать в памяти в коде hello R, hello общий размер для hello ввода и вывода не может превышать 500 МБ.</span><span class="sxs-lookup"><span data-stu-id="5c612-138">Because hello input and output DataFrames must exist in memory in hello R code, hello total size for hello input and output cannot exceed 500 MB.</span></span>

### <a name="sample-code"></a><span data-ttu-id="5c612-139">Пример кода</span><span class="sxs-lookup"><span data-stu-id="5c612-139">Sample Code</span></span>
<span data-ttu-id="5c612-140">Несколько примеров кода доступен в вашей учетной записи хранилища Озера данных после установки расширения U-SQL Advanced Analytics hello.</span><span class="sxs-lookup"><span data-stu-id="5c612-140">More sample code is available in your Data Lake Store account after you install hello U-SQL Advanced Analytics extensions.</span></span> <span data-ttu-id="5c612-141">несколько примеров кода Hello путь —: `<your_account_address>/usqlext/samples/R`.</span><span class="sxs-lookup"><span data-stu-id="5c612-141">hello path for more sample code is: `<your_account_address>/usqlext/samples/R`.</span></span> 

## <a name="deploying-custom-r-modules-with-u-sql"></a><span data-ttu-id="5c612-142">Развертывание настраиваемых модулей R с помощью U-SQL</span><span class="sxs-lookup"><span data-stu-id="5c612-142">Deploying Custom R modules with U-SQL</span></span>

<span data-ttu-id="5c612-143">Во-первых создайте настраиваемый модуль R и почтовый индекс, он, а затем отправьте ZIP-хранилище ADL tooyour файла настраиваемого модуля R hello.</span><span class="sxs-lookup"><span data-stu-id="5c612-143">First, create an R custom module and zip it and then upload hello zipped R custom module file tooyour ADL store.</span></span> <span data-ttu-id="5c612-144">В примере hello будет передать корень toohello magittr_1.5.zip hello ADLS учетная запись по умолчанию hello ADLA учетную запись, которую мы используем.</span><span class="sxs-lookup"><span data-stu-id="5c612-144">In hello example, we will upload magittr_1.5.zip toohello root of hello default ADLS account for hello ADLA account we are using.</span></span> <span data-ttu-id="5c612-145">После загрузки хранилища tooADL модуль hello объявить его как использование РЕСУРСОВ РАЗВЕРТЫВАНИЯ toomake его доступным в скрипт U-SQL и вызовите `install.packages` tooinstall его.</span><span class="sxs-lookup"><span data-stu-id="5c612-145">Once you upload hello module tooADL store, declare it as use DEPLOY RESOURCE toomake it available in your U-SQL script and call `install.packages` tooinstall it.</span></span>

    REFERENCE ASSEMBLY [ExtR];
    DEPLOY RESOURCE @"/magrittr_1.5.zip";

    DECLARE @IrisData string =  @"/usqlext/samples/R/iris.csv";
    DECLARE @OutputFileModelSummary string = @"/R/Output/CustomePackages.txt";

    // R script toorun
    DECLARE @myRScript = @"
    # install hello magrittr package,
    install.packages('magrittr_1.5.zip', repos = NULL),
    # load hello magrittr package,
    require(magrittr),
    # demonstrate use of hello magrittr package,
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

    OUTPUT @RScriptOutput too@OutputFileModelSummary USING Outputters.Tsv();

## <a name="next-steps"></a><span data-ttu-id="5c612-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c612-146">Next Steps</span></span>
* [<span data-ttu-id="5c612-147">Обзор аналитики озера данных Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="5c612-147">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="5c612-148">Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5c612-148">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="5c612-149">Использование оконных функций U-SQL для заданий в службе аналитики озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="5c612-149">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
