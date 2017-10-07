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
# <a name="tutorial-get-started-with-extending-u-sql-with-r"></a>Руководство. Начало работы с расширением возможностей U-SQL c R

Следующий пример Hello рассмотрены основные шаги развертывания кода R hello:
* Используйте hello `REFERENCE ASSEMBLY` расширения tooenable R инструкции для hello скрипт U-SQL.
* Используйте` REDUCE` операции toopartition hello входные данные по ключу.
* расширения Hello R для U-SQL включают в себя встроенные редуктора (`Extension.R.Reducer`), которое будет выполняться код R на каждой вершины назначенный toohello редуктора. 
* Использование выделенного с именем кадров данных называется `inputFromUSQL` и `outputToUSQL `соответственно toopass данных между U-SQL и R. ввода и вывода исправленные имена идентификаторов кадр данных (то есть, пользователи не могут изменить эти стандартные имена входных данных и вывода кадр данных идентификаторы).

## <a name="embedding-r-code-in-hello-u-sql-script"></a>Внедрение кода R в hello скрипт U-SQL

Вы можете hello R во встроенном коде на ваш скрипт U-SQL с помощью параметра команды hello hello `Extension.R.Reducer`. Например можно объявить hello сценария R в переменной строки и передайте его в качестве параметра toohello редуктора.


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

## <a name="keep-hello-r-code-in-a-separate-file-and-reference-it--hello-u-sql-script"></a>Сохранить в отдельном файле кода hello R и ссылок на него скрипт hello U-SQL

Следующий пример Hello рассмотрены более сложные использования. В этом случае код hello R развертывается как РЕСУРС, который является hello скрипт U-SQL.

Сохраните этот код R как отдельный файл.

    load("my_model_LM_Iris.rda")
    outputToUSQL=data.frame(predict(lm.fit, inputFromUSQL, interval="confidence")) 

Используйте этот скрипт R toodeploy скрипт U-SQL с hello инструкции РАЗВЕРТЫВАНИЯ РЕСУРСОВ.

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

## <a name="how-r-integrates-with-u-sql"></a>Интеграция R c U-SQL

### <a name="datatypes"></a>Типы данных
* Строковые и числовые столбцы из U-SQL преобразуются без изменений между таблицей данных на R и U-SQL [поддерживаемые типы: `double`, `string`, `bool`, `integer`, `byte`].
* Hello `Factor` тип данных не поддерживается в U-SQL.
* Тип `byte[]` должен быть сериализован как строка `string` в кодировке Base64.
* Строки U-SQL могут быть toofactors, преобразованное в коде R, один раз U-SQL создать входной кадр данных R или параметром задание hello редуктора `stringsAsFactors: true`.

### <a name="schemas"></a>Схемы
* Наборы данных U-SQL не могут содержать повторяемые имена столбцов.
* Имена столбцов в наборах данных U-SQL должны быть строками.
* Имена столбцов должны hello же U-SQL и R-сценариев.
* Только для чтения столбец не может быть частью блока hello выходных данных. Так как столбцы только для чтения автоматически добавляются обратно в таблице hello U-SQL, если он является частью схемы вывода данных из определяемого пользователем ОПЕРАТОРА.

### <a name="functional-limitations"></a>Ограничения функциональных возможностей
* Hello модуль R не может быть создан в два раза hello одного процесса. 
* В настоящее время U-SQL не поддерживает определяемые пользователем операторы Combiner для прогнозирования с помощью секционированных моделей, созданных с использованием определяемых пользователем операторов Reducer. Пользователи могут объявить hello секционированы моделей в качестве ресурса и использовать их в R-сценария (см. пример кода `ExtR_PredictUsingLMRawStringReducer.usql`)

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
Каждая вершина имеет ограниченный объем памяти, назначенный tooit. Поскольку hello блоки входных и выходных данных должна существовать в памяти в коде hello R, hello общий размер для hello ввода и вывода не может превышать 500 МБ.

### <a name="sample-code"></a>Пример кода
Несколько примеров кода доступен в вашей учетной записи хранилища Озера данных после установки расширения U-SQL Advanced Analytics hello. несколько примеров кода Hello путь —: `<your_account_address>/usqlext/samples/R`. 

## <a name="deploying-custom-r-modules-with-u-sql"></a>Развертывание настраиваемых модулей R с помощью U-SQL

Во-первых создайте настраиваемый модуль R и почтовый индекс, он, а затем отправьте ZIP-хранилище ADL tooyour файла настраиваемого модуля R hello. В примере hello будет передать корень toohello magittr_1.5.zip hello ADLS учетная запись по умолчанию hello ADLA учетную запись, которую мы используем. После загрузки хранилища tooADL модуль hello объявить его как использование РЕСУРСОВ РАЗВЕРТЫВАНИЯ toomake его доступным в скрипт U-SQL и вызовите `install.packages` tooinstall его.

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

## <a name="next-steps"></a>Дальнейшие действия
* [Обзор аналитики озера данных Microsoft Azure](data-lake-analytics-overview.md)
* [Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Использование оконных функций U-SQL для заданий в службе аналитики озера данных Azure](data-lake-analytics-use-window-functions.md)
