---
title: "aaaOperationalize Spark построенных моделей машинного обучения | Документы Microsoft"
description: "Tooload оценка обучения моделей хранением и в хранилище больших двоичных объектов Azure (WASB) с Python."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="c699a-103">Ввод моделей машинного обучения, созданных с помощью Spark, в эксплуатацию</span><span class="sxs-lookup"><span data-stu-id="c699a-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="c699a-104">В этом разделе показано, как toooperationalize сохраненного модели машинного обучения (ML) с помощью Python на HDInsight Spark кластеров.</span><span class="sxs-lookup"><span data-stu-id="c699a-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="c699a-105">Здесь описываются процедуры tooload машинного обучения моделей, построенных с использованием Spark MLlib и хранятся в хранилище больших двоичных объектов Azure (WASB) и tooscore их с наборами данных, также сохраненные в WASB.</span><span class="sxs-lookup"><span data-stu-id="c699a-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="c699a-106">Он показывает процессами toopre hello входных данных, компонентов преобразования с использованием hello индексирования и кодировка функции в набор средств MLlib hello и как toocreate объекта с меткой точки данных, который можно использовать в качестве входных данных для оценки с моделями hello машинного Обучения.</span><span class="sxs-lookup"><span data-stu-id="c699a-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="c699a-107">Hello модели, используемые для оценки включают линейной регрессии, логистической регрессии, моделей случайные леса и градиента повышение приоритета моделей дерева.</span><span class="sxs-lookup"><span data-stu-id="c699a-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="c699a-108">Кластеры Spark и записные книжки Jupyter</span><span class="sxs-lookup"><span data-stu-id="c699a-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="c699a-109">Шаги настройки и toooperationalize кода hello модель машинного Обучения предоставляются в этом пошаговом руководстве по использованию кластер HDInsight Spark 1.6, а также кластер Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="c699a-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="c699a-110">Hello код для этих процедур также предоставляется в записные книжки Jupyter.</span><span class="sxs-lookup"><span data-stu-id="c699a-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="c699a-111">Записная книжка для Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="c699a-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="c699a-112">Hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) книжке Jupyter показано, как toooperationalize сохраненную модель с помощью Python в HDInsight кластеров.</span><span class="sxs-lookup"><span data-stu-id="c699a-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="c699a-113">Записная книжка для Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="c699a-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="c699a-114">книжке Jupyter hello toomodify для toouse Spark 1.6 с кластером HDInsight Spark 2.0 заменить файл кода hello Python с [этот файл](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="c699a-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="c699a-115">Этот код показывает способ создания модели tooconsume hello в Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="c699a-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c699a-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c699a-116">Prerequisites</span></span>

1. <span data-ttu-id="c699a-117">Вам потребуется учетная запись Azure и Spark 1.6 (или Spark 2.0) кластер HDInsight toocomplete в данном пошаговом руководстве.</span><span class="sxs-lookup"><span data-stu-id="c699a-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="c699a-118">В разделе hello [Обзор для обработки и анализа данных с помощью Spark на Azure HDInsight](machine-learning-data-science-spark-overview.md) инструкции о том, как toosatisfy эти требования.</span><span class="sxs-lookup"><span data-stu-id="c699a-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="c699a-119">Этот раздел также содержит описание hello такси 2013 NYC данные, используемые здесь и инструкции о том, как код tooexecute из записной книжке Jupyter на кластере Spark hello.</span><span class="sxs-lookup"><span data-stu-id="c699a-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="c699a-120">Необходимо также создать hello моделей машинного обучения toobe здесь рассчитаны с одновременной ликвидации hello [данных и моделирование с Spark](machine-learning-data-science-spark-data-exploration-modeling.md) раздел для кластера Spark 1.6 hello или ноутбуки hello Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="c699a-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="c699a-121">портативные компьютеры Hello Spark 2.0 использовать дополнительный набор данных для задачи классификации hello, hello хорошо известных авиакомпании на время отправления набор данных на основе 2011 г. и 2012.</span><span class="sxs-lookup"><span data-stu-id="c699a-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="c699a-122">Описание toothem hello записных книжек и ссылки, представлено в hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub hello, содержащий их.</span><span class="sxs-lookup"><span data-stu-id="c699a-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="c699a-123">Кроме того код hello здесь и в записных книжках hello связаны является универсальным и должен работать на любой кластер Spark.</span><span class="sxs-lookup"><span data-stu-id="c699a-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="c699a-124">Если вы не используете HDInsight Spark, настройку и управление ими действия hello кластера может быть немного отличается от показанной здесь.</span><span class="sxs-lookup"><span data-stu-id="c699a-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="c699a-125">Программа установки: hello, библиотеки и расположения хранилища конфигурации Spark контекста</span><span class="sxs-lookup"><span data-stu-id="c699a-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="c699a-126">Spark — может tooan tooread и записи больших двоичных объектов хранилища Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="c699a-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="c699a-127">Поэтому любые существующие данные, хранящиеся в ней могут быть обработаны с помощью Spark и hello результаты хранимых в WASB.</span><span class="sxs-lookup"><span data-stu-id="c699a-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="c699a-128">toosave модели или файлов в WASB, hello путь должен toobe указано правильно.</span><span class="sxs-lookup"><span data-stu-id="c699a-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="c699a-129">Hello кластера Spark toohello присоединенного контейнера по умолчанию можно обращаться, используя путь, начиная с: *«wasb / /»*.</span><span class="sxs-lookup"><span data-stu-id="c699a-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="c699a-130">Hello следующий код задает расположение hello чтения toobe данных hello и hello hello модели хранения каталога toowhich hello модели выходных данных будет сохранен.</span><span class="sxs-lookup"><span data-stu-id="c699a-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="c699a-131">Настройка путей каталога к месту хранения в хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="c699a-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="c699a-132">Модели сохраняются в следующем расположении: wasb:///user/remoteuser/NYCTaxi/Models.</span><span class="sxs-lookup"><span data-stu-id="c699a-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="c699a-133">Если этот путь задан неправильно, загрузить модели для оценки не удастся.</span><span class="sxs-lookup"><span data-stu-id="c699a-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="c699a-134">Hello оцененные результаты были сохранены в: «wasb: / / / пользователя/remoteuser/NYCTaxi/ScoredResults».</span><span class="sxs-lookup"><span data-stu-id="c699a-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="c699a-135">Если путь toofolder hello является неверной, результаты не сохраняются в этой папке.</span><span class="sxs-lookup"><span data-stu-id="c699a-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="c699a-136">пути к расположению файла Hello можно скопировать и вставить в заполнители hello в этом коде из вывода hello hello последнюю ячейку hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** ноутбука.</span><span class="sxs-lookup"><span data-stu-id="c699a-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="c699a-137">Вот путей к каталогам tooset кода hello.</span><span class="sxs-lookup"><span data-stu-id="c699a-137">Here is hello code tooset directory paths:</span></span> 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="c699a-138">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="c699a-138">**OUTPUT:**</span></span>

<span data-ttu-id="c699a-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="c699a-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="c699a-140">Импорт библиотек</span><span class="sxs-lookup"><span data-stu-id="c699a-140">Import libraries</span></span>
<span data-ttu-id="c699a-141">Spark в контексте, а затем импортируйте необходимые библиотеки после кода hello</span><span class="sxs-lookup"><span data-stu-id="c699a-141">Set spark context and import necessary libraries with hello following code</span></span>

    #IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="c699a-142">Предустановленный контекст Spark и волшебные команды PySpark</span><span class="sxs-lookup"><span data-stu-id="c699a-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="c699a-143">Hello PySpark ядер, предоставляемых с записные книжки Jupyter имеют предустановленных контекста.</span><span class="sxs-lookup"><span data-stu-id="c699a-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="c699a-144">Поэтому необязательно tooset hello Spark или куст контекстов явно перед началом работы с приложением hello, которое вы разрабатываете.</span><span class="sxs-lookup"><span data-stu-id="c699a-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="c699a-145">Эти контексты доступны вам по умолчанию,</span><span class="sxs-lookup"><span data-stu-id="c699a-145">These are available for you by default.</span></span> <span data-ttu-id="c699a-146">а именно:</span><span class="sxs-lookup"><span data-stu-id="c699a-146">These contexts are:</span></span>

* <span data-ttu-id="c699a-147">sc для Spark;</span><span class="sxs-lookup"><span data-stu-id="c699a-147">sc - for Spark</span></span> 
* <span data-ttu-id="c699a-148">sqlContext для Hive.</span><span class="sxs-lookup"><span data-stu-id="c699a-148">sqlContext - for Hive</span></span>

<span data-ttu-id="c699a-149">Hello ядра PySpark предоставляет некоторые предопределенные «magics», которые являются специальные команды, которые можно вызвать с %%.</span><span class="sxs-lookup"><span data-stu-id="c699a-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="c699a-150">В этих примерах кода используются две подобные команды.</span><span class="sxs-lookup"><span data-stu-id="c699a-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="c699a-151">**%% локального** указанного кода hello в последующих строках выполняется локально.</span><span class="sxs-lookup"><span data-stu-id="c699a-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="c699a-152">В качестве кода должен быть указан корректный код Python.</span><span class="sxs-lookup"><span data-stu-id="c699a-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="c699a-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="c699a-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="c699a-154">Выполняет запрос Hive в отношении hello sqlContext.</span><span class="sxs-lookup"><span data-stu-id="c699a-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="c699a-155">Если передается параметр -o hello, hello результат запроса hello сохраняется в hello %% локального контекста Python как Pandas кадр данных.</span><span class="sxs-lookup"><span data-stu-id="c699a-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="c699a-156">Для Дополнительные сведения о ядра hello записные книжки Jupyter и предопределенные hello «magics», они предоставляют, в разделе [кластеры ядер, доступных для записные книжки Jupyter с HDInsight Spark Linux в HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="c699a-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="c699a-157">Прием данных и создание очищенного фрейма данных</span><span class="sxs-lookup"><span data-stu-id="c699a-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="c699a-158">В этом разделе содержится код hello для ряда задач требуется tooingest hello данных toobe оцененных.</span><span class="sxs-lookup"><span data-stu-id="c699a-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="c699a-159">Чтения в соединяемых 0,1% образец hello такси маршрута и тариф авиакомпании файла (хранятся в формате .tsv) hello формат данных, а затем создает кадр очистки данных.</span><span class="sxs-lookup"><span data-stu-id="c699a-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="c699a-160">Hello такси маршрута и тариф авиакомпании файлы были соединены на основе на процедуру hello в: [hello командного процесса обработки и анализа данных в действие: с использованием кластеров HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="c699a-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_test_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="c699a-161">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="c699a-161">**OUTPUT:**</span></span>

<span data-ttu-id="c699a-162">Время, затраченное tooexecute над ячейкой: 46.37 секунд</span><span class="sxs-lookup"><span data-stu-id="c699a-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="c699a-163">Подготовка данных для оценки в Spark</span><span class="sxs-lookup"><span data-stu-id="c699a-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="c699a-164">В этом разделе описывается, как tooindex, кодирования и масштабировать категориальных признаков tooprepare их для использования в алгоритмах обучения MLlib защищено для классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="c699a-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="c699a-165">Преобразование признаков. Индексирование и кодирование категориальных признаков для получения входных данных для оцениваемых моделей</span><span class="sxs-lookup"><span data-stu-id="c699a-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="c699a-166">В этом разделе показано, как tooindex категориальные данные с помощью `StringIndexer` и кодирование функций с `OneHotEncoder` ввода в модели hello.</span><span class="sxs-lookup"><span data-stu-id="c699a-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="c699a-167">Hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) кодирует строковый столбец метки столбца tooa метки индексов.</span><span class="sxs-lookup"><span data-stu-id="c699a-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="c699a-168">индексы Hello упорядочиваются по частот метки.</span><span class="sxs-lookup"><span data-stu-id="c699a-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="c699a-169">Hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) сопоставляет столбец метки столбца tooa индексы двоичных векторов, с максимум один значение single.</span><span class="sxs-lookup"><span data-stu-id="c699a-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="c699a-170">Эта кодировка позволяет алгоритмы, которые ожидают непрерывного табличное значение функции, такие как логистическая Регрессия toobe применения toocategorical функции.</span><span class="sxs-lookup"><span data-stu-id="c699a-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="c699a-171">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="c699a-171">**OUTPUT:**</span></span>

<span data-ttu-id="c699a-172">Время, затраченное tooexecute над ячейкой: 5.37 секунд</span><span class="sxs-lookup"><span data-stu-id="c699a-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="c699a-173">Создание объектов устойчивого распределенного набора данных с массивами признаков для получения входных данных для моделей</span><span class="sxs-lookup"><span data-stu-id="c699a-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="c699a-174">Этот раздел содержит код, который показывает, как категориальные текстовые данные tooindex как RDD объекта и горячей один зашифровать их, поэтому ее можно использовать tootrain и тестирования MLlib логистической регрессии и модели на основе дерева.</span><span class="sxs-lookup"><span data-stu-id="c699a-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="c699a-175">Hello индексированных данных хранится в [устойчивым распределенного набора данных (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) объектов.</span><span class="sxs-lookup"><span data-stu-id="c699a-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="c699a-176">Это базовая абстракция hello в Spark.</span><span class="sxs-lookup"><span data-stu-id="c699a-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="c699a-177">Объект устойчивого распределенного набора данных — это неизменяемая, секционированная коллекция элементов, которыми можно одновременно управлять с помощью Spark.</span><span class="sxs-lookup"><span data-stu-id="c699a-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="c699a-178">Он также содержит код, который показывает, как hello tooscale данных с помощью `StandardScalar` MLlib, предоставляемые для использования в линейной регрессии с вероятностный градиентный спуск (SGD), популярный алгоритм для обучения широкий спектр моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="c699a-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="c699a-179">Hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) — разница toounit функции hello используется tooscale.</span><span class="sxs-lookup"><span data-stu-id="c699a-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="c699a-180">Масштабирование функции, также известные как нормализация данных гарантирует, что функции широко распределенные значениями не учитывая чрезмерного весить в целевой функции hello.</span><span class="sxs-lookup"><span data-stu-id="c699a-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="c699a-181">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="c699a-181">**OUTPUT:**</span></span>

<span data-ttu-id="c699a-182">Время, затраченное tooexecute над ячейкой: 11.72 секунд</span><span class="sxs-lookup"><span data-stu-id="c699a-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="c699a-183">Hello модели логистической регрессии для создания рейтингов и сохранить tooblob выходных данных</span><span class="sxs-lookup"><span data-stu-id="c699a-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="c699a-184">Hello кода в этом разделе показано, как tooload модели логистической регрессии, сохраненного в Azure хранилище больших двоичных объектов и использовать toopredict, оплачивается ли подсказка в такси обработки, оценка его с метриками стандартные классификации, а затем сохраните и tooblob hello результатов построения хранилище.</span><span class="sxs-lookup"><span data-stu-id="c699a-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="c699a-185">Привет, оцененные результаты хранятся в объектах RDD.</span><span class="sxs-lookup"><span data-stu-id="c699a-185">hello scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="c699a-186">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="c699a-186">**OUTPUT:**</span></span>

<span data-ttu-id="c699a-187">Время, затраченное tooexecute над ячейкой: 19.22 секунд</span><span class="sxs-lookup"><span data-stu-id="c699a-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="c699a-188">Оценка модели линейной регрессии</span><span class="sxs-lookup"><span data-stu-id="c699a-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="c699a-189">Мы использовали [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain модель линейной регрессии, используя вероятностный градиентный спуск (SGD) для оптимизации toopredict hello объем совет платная.</span><span class="sxs-lookup"><span data-stu-id="c699a-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="c699a-190">Hello кода в этом разделе показано, как оценка с помощью переменных масштабированный tooload модель линейной регрессии из хранилища BLOB-объектов Azure, а затем сохраните hello результаты назад toohello blob.</span><span class="sxs-lookup"><span data-stu-id="c699a-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="c699a-191">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="c699a-191">**OUTPUT:**</span></span>

<span data-ttu-id="c699a-192">Время, затраченное tooexecute над ячейкой: 16.63 секунд</span><span class="sxs-lookup"><span data-stu-id="c699a-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="c699a-193">Оценка моделей классификации и регрессии с применением алгоритма случайного леса</span><span class="sxs-lookup"><span data-stu-id="c699a-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="c699a-194">кода Hello в этом разделе показано, как tooload hello сохраняет классификации и случайного леса модели регрессии в хранилище BLOB-объектов Azure оценки их производительности с помощью стандартных классификатора и регрессии меры, а затем сохраните hello результаты назад tooblob хранилища.</span><span class="sxs-lookup"><span data-stu-id="c699a-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="c699a-195">[Случайные леса](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="c699a-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="c699a-196">Они объединяют многих решений деревьев tooreduce hello риск переобучения.</span><span class="sxs-lookup"><span data-stu-id="c699a-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="c699a-197">Случайные леса могут обрабатывать категориальных признаков расширения toohello мультиклассовой классификации параметр, не требуется возможность масштабирования и являются может toocapture нелинейности и возможностей взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="c699a-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="c699a-198">Случайные леса принадлежат hello наиболее успешных моделей машинного обучения для классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="c699a-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="c699a-199">[spark.mllib](http://spark.apache.org/mllib/) предусматривает использование метода случайного леса в моделях двоичной, мультиклассовой классификации и регрессии с применением как непрерывных, так и категориальных признаков.</span><span class="sxs-lookup"><span data-stu-id="c699a-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="c699a-200">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="c699a-200">**OUTPUT:**</span></span>

<span data-ttu-id="c699a-201">Время, затраченное tooexecute над ячейкой: 31.07 секунд</span><span class="sxs-lookup"><span data-stu-id="c699a-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="c699a-202">Оценка моделей классификации и регрессии с применением метода градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="c699a-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="c699a-203">Hello кода в этом разделе описывается, как tooload классификации и регрессии градиента моделей дерева повышение приоритета из хранилища BLOB-объектов Azure, оценки их производительности с помощью стандартных классификатора и меры регрессии и сохраните hello результаты назад tooblob хранилища.</span><span class="sxs-lookup"><span data-stu-id="c699a-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="c699a-204">**spark.mllib** предусматривает использование метода деревьев с градиентным бустингом (GBT) в моделях двоичной классификации и регрессии с применением как непрерывных, так и категориальных признаков.</span><span class="sxs-lookup"><span data-stu-id="c699a-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="c699a-205">[Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="c699a-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="c699a-206">Решение GBTs обучение итеративного дерева toominimize функции потерь.</span><span class="sxs-lookup"><span data-stu-id="c699a-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="c699a-207">GBTs может обрабатывать категориальных признаков не требуется возможность масштабирования и являются может toocapture нелинейности и возможностей взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="c699a-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="c699a-208">Кроме того, его можно использовать для создания модели мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="c699a-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="c699a-209">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="c699a-209">**OUTPUT:**</span></span>

<span data-ttu-id="c699a-210">Время, затраченное tooexecute над ячейкой: 14.6 секунд</span><span class="sxs-lookup"><span data-stu-id="c699a-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="c699a-211">Очистка объектов из памяти и вывод расположений оцененных файлов</span><span class="sxs-lookup"><span data-stu-id="c699a-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="c699a-212">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="c699a-212">**OUTPUT:**</span></span>

<span data-ttu-id="c699a-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="c699a-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="c699a-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="c699a-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="c699a-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="c699a-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="c699a-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="c699a-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="c699a-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="c699a-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="c699a-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="c699a-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="c699a-219">Использование моделей Spark через веб-интерфейс</span><span class="sxs-lookup"><span data-stu-id="c699a-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="c699a-220">Spark обеспечивает механизм tooremotely отправки пакетных заданий или интерактивной обработки запросов через REST взаимодействовать с компонентом, называется Livy.</span><span class="sxs-lookup"><span data-stu-id="c699a-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="c699a-221">Livy включен по умолчанию в кластере Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c699a-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="c699a-222">Дополнительные сведения о Livy см. в статье [Удаленная отправка заданий Spark в кластер Apache Spark в HDInsight с помощью Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="c699a-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="c699a-223">Можно использовать Livy tooremotely отправить задание по пакетной оценок файл, который хранится в BLOB-объекта Azure, а затем записывает большой двоичный объект tooanother результаты hello.</span><span class="sxs-lookup"><span data-stu-id="c699a-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="c699a-224">toodo, отправьте hello сценарий Python из</span><span class="sxs-lookup"><span data-stu-id="c699a-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="c699a-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello большого двоичного объекта из кластера Spark hello.</span><span class="sxs-lookup"><span data-stu-id="c699a-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="c699a-226">Можно использовать средства, подобного **обозреватель хранилищ Microsoft Azure** или **AzCopy** toocopy hello сценария toohello кластера blob.</span><span class="sxs-lookup"><span data-stu-id="c699a-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="c699a-227">В нашем случае мы загружен скрипт hello слишком***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="c699a-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="c699a-228">Здравствуйте, клавиши доступа, вы должны можно найти на портале hello для учетной записи хранения hello, связанные с кластера Spark hello.</span><span class="sxs-lookup"><span data-stu-id="c699a-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="c699a-229">После отправки toothis расположение внутри кластера Spark hello в контексте распределенных запуска этого сценария.</span><span class="sxs-lookup"><span data-stu-id="c699a-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="c699a-230">Он загружает модель hello и запускает прогнозы на входные файлы на основе модели hello.</span><span class="sxs-lookup"><span data-stu-id="c699a-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="c699a-231">Этот скрипт можно вызвать удаленно, выполнив простой запрос HTTPS или REST в Livy.</span><span class="sxs-lookup"><span data-stu-id="c699a-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="c699a-232">Вот перелистывание команда tooconstruct hello HTTP запроса tooinvoke hello сценарий Python удаленно.</span><span class="sxs-lookup"><span data-stu-id="c699a-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="c699a-233">Замените CLUSTERLOGIN, CLUSTERPASSWORD, ИМЯ_КЛАСТЕРА hello соответствующие значения для кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="c699a-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="c699a-234">Можно использовать любой язык на задание hello удаленной системе tooinvoke hello Spark через Livy путем вызова простой HTTPS с обычной проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="c699a-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="c699a-235">Было бы библиотеки Python запросы hello удобный toouse при выполнении данного вызова HTTP, но сейчас не установлена по умолчанию в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="c699a-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="c699a-236">Поэтому вместо нее используются старые библиотеки HTTP.</span><span class="sxs-lookup"><span data-stu-id="c699a-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="c699a-237">Ниже приведен код Python hello для вызова hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="c699a-237">Here is hello Python code for hello HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="c699a-238">Можно также добавить этот код Python слишком[функции Azure](https://azure.microsoft.com/documentation/services/functions/) tootrigger отправки задания Spark, которая оценивает большого двоичного объекта на основе различных событий как таймер, создания или обновления большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="c699a-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="c699a-239">Взаимодействие с произвольным клиентом кода, используйте hello [приложения логики Azure](https://azure.microsoft.com/documentation/services/app-service/logic/) оценки за счет определения действия HTTP для hello пакета Spark hello tooinvoke **логику приложения конструктор** и задание его параметров.</span><span class="sxs-lookup"><span data-stu-id="c699a-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="c699a-240">На портале Azure создайте приложение логики, выбрав **+Создать** -> **Интернет+мобильные устройства** -> **Приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="c699a-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="c699a-241">toobring копирование hello **логику приложения конструктор**, введите имя hello hello логику приложения и план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="c699a-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="c699a-242">Выберите действие HTTP и введите hello параметров, приведенных в следующий рисунок hello:</span><span class="sxs-lookup"><span data-stu-id="c699a-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![Конструктор Logic Apps](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="c699a-244">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="c699a-244">What's next?</span></span>
<span data-ttu-id="c699a-245">**Перекрестная проверка и перебор гиперпараметров**. Сведения об обучении моделей с помощью перекрестной проверки и перебора гиперпараметров см. в статье [Расширенное исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md).</span><span class="sxs-lookup"><span data-stu-id="c699a-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

