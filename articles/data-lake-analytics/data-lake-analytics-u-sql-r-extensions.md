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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>Руководство. Начало работы с расширением возможностей U-SQL c R

В следующих примерах представлены основные шаги по развертыванию кода R:
* Используйте инструкцию `REFERENCE ASSEMBLY`, чтобы включить расширения R для скрипта U-SQL.
* Используйте операцию ` REDUCE` для разделения входных данных в ключе.
* Расширения R для U-SQL включают встроенное средство редукции (`Extension.R.Reducer`), которое выполняет код R в каждой назначенной ему вершине. 
* Передача данных между U-SQL и R с использованием выделенных именованных таблиц данных `inputFromUSQL` и `outputToUSQL ` соответственно. Имена идентификаторов входной и выходной таблицы данных исправлены (то есть пользователи не могут изменить эти предопределенные имена идентификаторов входной и выходной таблицы данных).

## <a name="embedding-r-code-in-the-u-sql-script"></a>Внедрение кода R в скрипт U-SQL

Код R можно встроить в скрипт U-SQL с помощью параметра команды средства `Extension.R.Reducer`. Например, можно объявить скрипт R как строковую переменную и передать его в качестве параметра в Reducer.


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

## <a name="keep-the-r-code-in-a-separate-file-and-reference-it--the-u-sql-script"></a>Сохраните код R в отдельном файле и ссылайтесь на него в скрипте U-SQL

В следующем примере демонстрируется более сложное использование. В этом случае код R развертывается как RESOURCE, который является скриптом U-SQL.

Сохраните этот код R как отдельный файл.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

Используйте скрипт U-SQL для развертывания этого скрипта R с оператором DEPLOY RESOURCE.

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

## <a name="how-r-integrates-with-u-sql"></a>Интеграция R c U-SQL

### <a name="datatypes"></a>Типы данных
* Строковые и числовые столбцы из U-SQL преобразуются без изменений между таблицей данных на R и U-SQL [поддерживаемые типы: `double`, `string`, `bool`, `integer`, `byte`].
* Тип данных `Factor` не поддерживается в U-SQL.
* Тип `byte[]` должен быть сериализован как строка `string` в кодировке Base64.
* После создания в U-SQL входной таблицы данных R или установки для параметра средства редукции `stringsAsFactors: true` значения true строки U-SQL можно преобразовать в коэффициенты кода R.

### <a name="schemas"></a>Схемы
* Наборы данных U-SQL не могут содержать повторяемые имена столбцов.
* Имена столбцов в наборах данных U-SQL должны быть строками.
* Имена столбцов в скриптах U-SQL и R должны совпадать.
* Столбцы с доступом только для чтения не могут быть частью выходной таблицы данных, так как они автоматически вставляются обратно в таблицу U-SQL (если она является частью выходной схемы определяемых пользователем объектов).

### <a name="functional-limitations"></a>Ограничения функциональных возможностей
* Ядро R нельзя создать дважды в одном процессе. 
* В настоящее время U-SQL не поддерживает определяемые пользователем операторы Combiner для прогнозирования с помощью секционированных моделей, созданных с использованием определяемых пользователем операторов Reducer. Пользователи могут объявить секционированные модели как ресурс и использовать их в своих скриптах R (см. пример кода `ExtR_PredictUsingLMRawStringReducer.usql`)

### <a name="r-versions"></a>Версии R
Поддерживается только R 3.2.2.

### <a name="standard-r-modules"></a>Стандартные модули R

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

### <a name="input-and-output-size-limitations"></a>Ограничения размера входных и выходных данных
Каждой вершине назначен ограниченный объем памяти. Так как входящие и исходящие кадры данных должны существовать в памяти кода R, общий размер входных и выходных данных должен находиться в пределах 500 ГБ.

### <a name="sample-code"></a>Пример кода
Дополнительные примеры кода доступны в вашей учетной записи Data Lake Store после установки расширений расширенной аналитики U-SQL. Путь к другим примерам кода: `<your_account_address>/usqlext/samples/R`. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>Развертывание настраиваемых модулей R с помощью U-SQL

Сначала создайте настраиваемый модуль R, заархивируйте его в ZIP-файл, а затем отправьте этот ZIP-файл с настраиваемым модулем в хранилище ADL. В этом примере файл magittr_1.5.zip будет отправлен в корень учетной записи ADLS по умолчанию для используемой учетной записи ADLA. После отправки модуля в хранилище ADL объявите его с помощью DEPLOY RESOURCE, чтобы сделать этот модуль доступным в скрипте U-SQL, затем вызовите метод `install.packages`, чтобы установить его.

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

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор аналитики озера данных Microsoft Azure](data-lake-analytics-overview.md)
* [Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Использование оконных функций U-SQL для заданий в службе аналитики озера данных Azure](data-lake-analytics-use-window-functions.md)
