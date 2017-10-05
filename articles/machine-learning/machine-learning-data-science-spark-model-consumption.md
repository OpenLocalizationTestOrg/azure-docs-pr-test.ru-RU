---
title: "Ввод моделей машинного обучения, созданных с помощью Spark, в эксплуатацию | Документация Майкрософт"
description: "Сведения об отправке и оценке моделей обучения, сохраненных в хранилище BLOB-объектов Azure, с помощью Python."
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
ms.openlocfilehash: 00fec675bed0137473f7e3c5ddfe9c3c0e8344c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="f8c90-103">Ввод моделей машинного обучения, созданных с помощью Spark, в эксплуатацию</span><span class="sxs-lookup"><span data-stu-id="f8c90-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="f8c90-104">В этой статье показано, как ввести сохраненные модели машинного обучения в эксплуатацию с помощью Python в кластерах HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f8c90-104">This topic shows how to operationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="f8c90-105">Кроме того, здесь описывается, как загрузить модели машинного обучения, созданные с помощью Spark MLlib и сохраненные в хранилище BLOB-объектов Azure, а также как оценить их с помощью наборов данных, которые сохранены в этом же хранилище.</span><span class="sxs-lookup"><span data-stu-id="f8c90-105">It describes how to load machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how to score them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="f8c90-106">Здесь также описано, как выполнить предварительную подготовку входных данных, преобразовать признаки с помощью функций индексирования и кодирования в наборе средств MLlib и как создать объекты данных с помеченной вершиной, которые можно использовать в качестве входных данных для оценки при помощи моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="f8c90-106">It shows how to pre-process the input data, transform features using the indexing and encoding functions in the MLlib toolkit, and how to create a labeled point data object that can be used as input for scoring with the ML models.</span></span> <span data-ttu-id="f8c90-107">Для оценки будут использоваться такие модели, как линейная регрессия, логистическая регрессия, случайные леса и градиентный бустинг деревьев.</span><span class="sxs-lookup"><span data-stu-id="f8c90-107">The models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="f8c90-108">Кластеры Spark и записные книжки Jupyter</span><span class="sxs-lookup"><span data-stu-id="f8c90-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="f8c90-109">Действия по настройке и код, используемые для ввода модели машинного обучения в эксплуатацию в рамках этого руководства, можно выполнять как в кластере HDInsight Spark 1.6, так и в кластере Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="f8c90-109">Setup steps and the code to operationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="f8c90-110">В записных книжках Jupyter также содержится код для выполнения этих процедур.</span><span class="sxs-lookup"><span data-stu-id="f8c90-110">The code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="f8c90-111">Записная книжка для Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="f8c90-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="f8c90-112">Записная книжка Jupyter [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) показывает, как применять сохраненную модель в кластерах HDInsight с помощью Python.</span><span class="sxs-lookup"><span data-stu-id="f8c90-112">The [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how to operationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="f8c90-113">Записная книжка для Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="f8c90-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="f8c90-114">Чтобы изменить записную книжку Jupyter для Spark 1.6 для использования в кластере HDInsight Spark 2.0, замените файл кода Python [этим файлом](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="f8c90-114">To modify the Jupyter notebook for Spark 1.6 to use with an HDInsight Spark 2.0 cluster, replace the Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="f8c90-115">Этот код показывает, как использовать модели, созданные в Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="f8c90-115">This code shows how to consume the models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f8c90-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f8c90-116">Prerequisites</span></span>

1. <span data-ttu-id="f8c90-117">Для работы с этим пошаговым руководством требуется учетная запись Azure и кластер Spark 1.6 или Spark 2.0 HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8c90-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="f8c90-118">См. статью [Общие сведения об обработке и анализе данных с помощью платформы Spark в Azure HDInsight](machine-learning-data-science-spark-overview.md) для получения инструкций по выполнению этих требований.</span><span class="sxs-lookup"><span data-stu-id="f8c90-118">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="f8c90-119">В этой статье также содержится описание используемых здесь данных о поездках в такси по Нью-Йорку за 2013 г., и инструкции по выполнению кода из записной книжки Jupyter в кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="f8c90-119">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 
2. <span data-ttu-id="f8c90-120">Вам также необходимо создать модели машинного обучения, которые будут оцениваться. Для этого выполните действия, описанные в статье [Исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-data-exploration-modeling.md) (для кластера Spark 1.6 или записных книжек Spark 2.0).</span><span class="sxs-lookup"><span data-stu-id="f8c90-120">You must also create the machine learning models to be scored here by working through the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for the Spark 1.6 cluster or the Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="f8c90-121">Записные книжки Spark 2.0 используют для задачи классификации дополнительный набор данных — известное расписание вылетов авиакомпании за 2011 и 2012 гг.</span><span class="sxs-lookup"><span data-stu-id="f8c90-121">The Spark 2.0 notebooks use an additional data set for the classification task, the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="f8c90-122">Описание записных книжек и ссылки на них вы можете найти в файле [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub с записными книжками.</span><span class="sxs-lookup"><span data-stu-id="f8c90-122">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="f8c90-123">Более того, код здесь и в связанных записных книжках является универсальным и должен работать в любом кластере Spark.</span><span class="sxs-lookup"><span data-stu-id="f8c90-123">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="f8c90-124">Действия по настройке кластера и управлению им могут немного отличаться от приведенных здесь, если вы не используете HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f8c90-124">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="f8c90-125">Настройка места хранения, библиотек и предустановленного контекста Spark</span><span class="sxs-lookup"><span data-stu-id="f8c90-125">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="f8c90-126">Spark может использовать хранилище BLOB-объектов Azure (WASB) для считывания и записи данных.</span><span class="sxs-lookup"><span data-stu-id="f8c90-126">Spark is able to read and write to an Azure Storage Blob (WASB).</span></span> <span data-ttu-id="f8c90-127">Таким образом, данные из хранилища можно обрабатывать с помощью Spark и сохранять полученные данные в этом же хранилище.</span><span class="sxs-lookup"><span data-stu-id="f8c90-127">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="f8c90-128">Чтобы сохранить модели или файлы в хранилище BLOB-объектов, необходимо указать путь соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="f8c90-128">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="f8c90-129">Контейнер по умолчанию, присоединенный к кластеру Spark, можно указать с помощью пути, который начинается с *"wasb//"*.</span><span class="sxs-lookup"><span data-stu-id="f8c90-129">The default container attached to the Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="f8c90-130">В следующем примере кода задается расположение данных, которые необходимо считать, и путь для каталога хранилища модели, где сохраняются выходные данные модели:</span><span class="sxs-lookup"><span data-stu-id="f8c90-130">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="f8c90-131">Настройка путей каталога к месту хранения в хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="f8c90-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="f8c90-132">Модели сохраняются в следующем расположении: wasb:///user/remoteuser/NYCTaxi/Models.</span><span class="sxs-lookup"><span data-stu-id="f8c90-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="f8c90-133">Если этот путь задан неправильно, загрузить модели для оценки не удастся.</span><span class="sxs-lookup"><span data-stu-id="f8c90-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="f8c90-134">Результаты оценки сохраняются в следующем расположении: wasb:///user/remoteuser/NYCTaxi/ScoredResults.</span><span class="sxs-lookup"><span data-stu-id="f8c90-134">The scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="f8c90-135">Если путь задан неправильно, сохранить результаты в эту папку не удастся.</span><span class="sxs-lookup"><span data-stu-id="f8c90-135">If the path to folder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="f8c90-136">Путь к расположению файлов можно скопировать из выходных данных, полученных после выполнения последнего фрагмента кода записной книжки **machine-learning-data-science-spark-data-exploration-modeling.ipynb** , и вставить в заполнители в этом коде.</span><span class="sxs-lookup"><span data-stu-id="f8c90-136">The file path locations can be copied and pasted into the placeholders in this code from the output of the last cell of the **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="f8c90-137">Ниже приведен код для настройки путей к каталогам:</span><span class="sxs-lookup"><span data-stu-id="f8c90-137">Here is the code to set directory paths:</span></span> 

    # LOCATION OF DATA TO BE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR THE MODELS TO BE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="f8c90-138">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="f8c90-138">**OUTPUT:**</span></span>

<span data-ttu-id="f8c90-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="f8c90-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="f8c90-140">Импорт библиотек</span><span class="sxs-lookup"><span data-stu-id="f8c90-140">Import libraries</span></span>
<span data-ttu-id="f8c90-141">Чтобы импортировать библиотеки и настроить контекст Spark, используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="f8c90-141">Set spark context and import necessary libraries with the following code</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="f8c90-142">Предустановленный контекст Spark и волшебные команды PySpark</span><span class="sxs-lookup"><span data-stu-id="f8c90-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="f8c90-143">Ядра PySpark, входящие в состав записных книжек Jupyter, имеют предустановленный контекст.</span><span class="sxs-lookup"><span data-stu-id="f8c90-143">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="f8c90-144">Поэтому перед началом работы с разрабатываемым приложением вам не нужно явно задавать контексты Spark или Hive.</span><span class="sxs-lookup"><span data-stu-id="f8c90-144">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="f8c90-145">Эти контексты доступны вам по умолчанию,</span><span class="sxs-lookup"><span data-stu-id="f8c90-145">These are available for you by default.</span></span> <span data-ttu-id="f8c90-146">а именно:</span><span class="sxs-lookup"><span data-stu-id="f8c90-146">These contexts are:</span></span>

* <span data-ttu-id="f8c90-147">sc для Spark;</span><span class="sxs-lookup"><span data-stu-id="f8c90-147">sc - for Spark</span></span> 
* <span data-ttu-id="f8c90-148">sqlContext для Hive.</span><span class="sxs-lookup"><span data-stu-id="f8c90-148">sqlContext - for Hive</span></span>

<span data-ttu-id="f8c90-149">Ядро PySpark предоставляет несколько "волшебных команд". Это специальные команды, которые можно вызывать с %%.</span><span class="sxs-lookup"><span data-stu-id="f8c90-149">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="f8c90-150">В этих примерах кода используются две подобные команды.</span><span class="sxs-lookup"><span data-stu-id="f8c90-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="f8c90-151">**%%local** Указывает, что код в последующих строках будет выполнен локально.</span><span class="sxs-lookup"><span data-stu-id="f8c90-151">**%%local** Specified that the code in subsequent lines is executed locally.</span></span> <span data-ttu-id="f8c90-152">В качестве кода должен быть указан корректный код Python.</span><span class="sxs-lookup"><span data-stu-id="f8c90-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="f8c90-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="f8c90-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="f8c90-154">Выполняет запрос Hive к sqlContext.</span><span class="sxs-lookup"><span data-stu-id="f8c90-154">Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="f8c90-155">Если передан параметр -o, результат запроса сохраняется в контексте %%local Python в качестве таблицы данных Pandas.</span><span class="sxs-lookup"><span data-stu-id="f8c90-155">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="f8c90-156">Дополнительные сведения о ядрах для записных книжек Jupyter и предустановленных "волшебных командах", которые они предоставляют, см. в статье [Ядра, доступные для использования записными книжками Jupyter с кластерами Apache Spark в HDInsight на платформе Linux](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="f8c90-156">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="f8c90-157">Прием данных и создание очищенного фрейма данных</span><span class="sxs-lookup"><span data-stu-id="f8c90-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="f8c90-158">В этом разделе содержится код, предназначенный для выполнения задач приема данных, которые нужно смоделировать.</span><span class="sxs-lookup"><span data-stu-id="f8c90-158">This section contains the code for a series of tasks required to ingest the data to be scored.</span></span> <span data-ttu-id="f8c90-159">С помощью этого кода можно считать файлы в формате TCV (выборку с примерно 0,1 % исходного набора данных о поездках в такси по Нью-Йорку и тарифами), форматировать данные, а затем создавать очищенные фреймы данных.</span><span class="sxs-lookup"><span data-stu-id="f8c90-159">Read in a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file), format the data, and then creates a clean data frame.</span></span>

<span data-ttu-id="f8c90-160">Файлы с данными о поездках в такси по Нью-Йорку и тарифах были объединены с помощью процедуры, описанной в статье [Процесс обработки и анализа данных группы на практике: использование кластеров HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) .</span><span class="sxs-lookup"><span data-stu-id="f8c90-160">The taxi trip and fare files were joined based on the procedure provided in the: [The Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF THE FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="f8c90-161">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="f8c90-161">**OUTPUT:**</span></span>

<span data-ttu-id="f8c90-162">Время на выполнение кода выше: 46,37 с.</span><span class="sxs-lookup"><span data-stu-id="f8c90-162">Time taken to execute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="f8c90-163">Подготовка данных для оценки в Spark</span><span class="sxs-lookup"><span data-stu-id="f8c90-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="f8c90-164">В этом разделе описано, как индексировать, кодировать и масштабировать категориальные признаки, чтобы подготовить их для использования в контролируемых алгоритмах обучения MLlib для моделей классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="f8c90-164">This section shows how to index, encode, and scale categorical features to prepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="f8c90-165">Преобразование признаков. Индексирование и кодирование категориальных признаков для получения входных данных для оцениваемых моделей</span><span class="sxs-lookup"><span data-stu-id="f8c90-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="f8c90-166">В этом разделе описано, как проиндексировать категориальные данные с помощью `StringIndexer` и закодировать признаки с помощью `OneHotEncoder`, чтобы получить входные данные для моделей.</span><span class="sxs-lookup"><span data-stu-id="f8c90-166">This section shows how to index categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into the models.</span></span>

<span data-ttu-id="f8c90-167">С помощью функции [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) столбец меток строкового типа кодируется как столбец с индексами меток.</span><span class="sxs-lookup"><span data-stu-id="f8c90-167">The [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels to a column of label indices.</span></span> <span data-ttu-id="f8c90-168">При этом индексы упорядочиваются по частоте меток.</span><span class="sxs-lookup"><span data-stu-id="f8c90-168">The indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="f8c90-169">[OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) сопоставляет столбец с индексами меток со столбцом двоичных векторов как минимум с одним отдельным значением.</span><span class="sxs-lookup"><span data-stu-id="f8c90-169">The [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="f8c90-170">Благодаря этой кодировке алгоритмы, для которых требуются признаки со значениями (например, логистическая регрессия), можно применять к категориальным признакам.</span><span class="sxs-lookup"><span data-stu-id="f8c90-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, to be applied to categorical features.</span></span>

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
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is the cleaned one from above
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="f8c90-171">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="f8c90-171">**OUTPUT:**</span></span>

<span data-ttu-id="f8c90-172">Время на выполнение кода выше: 5,37 с.</span><span class="sxs-lookup"><span data-stu-id="f8c90-172">Time taken to execute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="f8c90-173">Создание объектов устойчивого распределенного набора данных с массивами признаков для получения входных данных для моделей</span><span class="sxs-lookup"><span data-stu-id="f8c90-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="f8c90-174">С помощью кода в этом разделе можно индексировать категориальные текстовые данные в объекты устойчивого распределенного набора данных, а затем выполнить их прямое кодирование. После этого данные можно использовать для обучения и проверки модели логистической регрессии MLlib и моделей с применением дерева.</span><span class="sxs-lookup"><span data-stu-id="f8c90-174">This section contains code that shows how to index categorical text data as an RDD object and one-hot encode it so it can be used to train and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="f8c90-175">Проиндексированные данные хранятся в объектах [устойчивого распределенного набора данных](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html).</span><span class="sxs-lookup"><span data-stu-id="f8c90-175">The indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="f8c90-176">Это базовая абстракция Spark.</span><span class="sxs-lookup"><span data-stu-id="f8c90-176">These are the basic abstraction in Spark.</span></span> <span data-ttu-id="f8c90-177">Объект устойчивого распределенного набора данных — это неизменяемая, секционированная коллекция элементов, которыми можно одновременно управлять с помощью Spark.</span><span class="sxs-lookup"><span data-stu-id="f8c90-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="f8c90-178">Здесь также содержится код, в котором показано, как масштабировать данные с помощью функции MLlib `StandardScalar` для использования в моделях линейной регрессии с применением метода стохастического градиента. Этот алгоритм широко используется для обучения других моделей машинного обучения.</span><span class="sxs-lookup"><span data-stu-id="f8c90-178">It also contains code that shows how to scale data with the `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="f8c90-179">[StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) используется для масштабирования признаков до единичной дисперсии.</span><span class="sxs-lookup"><span data-stu-id="f8c90-179">The [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used to scale the features to unit variance.</span></span> <span data-ttu-id="f8c90-180">Масштабирование признаков (или нормализация данных) гарантирует, что для признаков с широко распределенными значениями не задано высокое значение веса в целевой функции.</span><span class="sxs-lookup"><span data-stu-id="f8c90-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> 

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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="f8c90-181">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="f8c90-181">**OUTPUT:**</span></span>

<span data-ttu-id="f8c90-182">Время на выполнение кода выше: 11,72 с.</span><span class="sxs-lookup"><span data-stu-id="f8c90-182">Time taken to execute above cell: 11.72 seconds</span></span>

## <a name="score-with-the-logistic-regression-model-and-save-output-to-blob"></a><span data-ttu-id="f8c90-183">Оценка с использованием модели логистической регрессии и сохранение выходных данных в хранилище BLOB-объектов</span><span class="sxs-lookup"><span data-stu-id="f8c90-183">Score with the Logistic Regression Model and save output to blob</span></span>
<span data-ttu-id="f8c90-184">С помощью кода, описанного в этом разделе, можно выполнить следующие задачи: загрузить модель логистической регрессии, сохраненную в хранилище BLOB-объектов Azure, использовать ее, чтобы спрогнозировать, будут ли оставлены чаевые за поездку в такси, оценить ее с помощью стандартных показателей классификации, а затем сохранить полученные результаты в это хранилище и отобразить их.</span><span class="sxs-lookup"><span data-stu-id="f8c90-184">The code in this section shows how to load a Logistic Regression Model that has been saved in Azure blob storage and use it to predict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot the results to blob storage.</span></span> <span data-ttu-id="f8c90-185">Результаты оценки будут сохранены в объектах устойчивого распределенного набора данных.</span><span class="sxs-lookup"><span data-stu-id="f8c90-185">The scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) TO BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="f8c90-186">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="f8c90-186">**OUTPUT:**</span></span>

<span data-ttu-id="f8c90-187">Время на выполнение кода выше: 19,22 с.</span><span class="sxs-lookup"><span data-stu-id="f8c90-187">Time taken to execute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="f8c90-188">Оценка модели линейной регрессии</span><span class="sxs-lookup"><span data-stu-id="f8c90-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="f8c90-189">Чтобы спрогнозировать сумму чаевых, мы с помощью функции [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) обучили модель линейной регрессии, в которой для оптимизации применяется метод стохастического градиента.</span><span class="sxs-lookup"><span data-stu-id="f8c90-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) to train a linear regression model using Stochastic Gradient Descent (SGD) for optimization to predict the amount of tip paid.</span></span> 

<span data-ttu-id="f8c90-190">С помощью кода, описанного в этом разделе, можно загрузить модель линейной регрессии из хранилища BLOB-объектов Azure, оценить ее с помощью масштабированных переменных, а затем сохранить результаты в большом двоичном объекте.</span><span class="sxs-lookup"><span data-stu-id="f8c90-190">The code in this section shows how to load a Linear Regression Model from Azure blob storage, score using scaled variables, and then save the results back to the blob.</span></span>

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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="f8c90-191">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="f8c90-191">**OUTPUT:**</span></span>

<span data-ttu-id="f8c90-192">Время на выполнение кода выше: 16,63 с.</span><span class="sxs-lookup"><span data-stu-id="f8c90-192">Time taken to execute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="f8c90-193">Оценка моделей классификации и регрессии с применением алгоритма случайного леса</span><span class="sxs-lookup"><span data-stu-id="f8c90-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="f8c90-194">С помощью кода, описанного в этом разделе, можно загрузить сохраненные в хранилище BLOB-объектов Azure модели классификации и регрессии с применением алгоритма случайного леса, оценить их эффективность с помощью стандартных показателей классификации и регрессии, а затем сохранить результаты в том же хранилище.</span><span class="sxs-lookup"><span data-stu-id="f8c90-194">The code in this section shows how to load the saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span>

<span data-ttu-id="f8c90-195">[Случайные леса](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="f8c90-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="f8c90-196">Такие совокупности минимизируют необходимость в переобучении.</span><span class="sxs-lookup"><span data-stu-id="f8c90-196">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="f8c90-197">С помощью этого алгоритма можно обрабатывать категориальные признаки, расширять модель для выполнения задач мультиклассовой классификации, а также определять нелинейные зависимости и взаимодействия признаков. Этот метод не требуют масштабирования признаков.</span><span class="sxs-lookup"><span data-stu-id="f8c90-197">Random forests can handle categorical features, extend to the multiclass classification setting, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="f8c90-198">Случайные леса — одна из самых эффективных моделей машинного обучения для задач классификации и регрессии.</span><span class="sxs-lookup"><span data-stu-id="f8c90-198">Random forests are one of the most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="f8c90-199">[spark.mllib](http://spark.apache.org/mllib/) предусматривает использование метода случайного леса в моделях двоичной, мультиклассовой классификации и регрессии с применением как непрерывных, так и категориальных признаков.</span><span class="sxs-lookup"><span data-stu-id="f8c90-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="f8c90-200">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="f8c90-200">**OUTPUT:**</span></span>

<span data-ttu-id="f8c90-201">Время на выполнение кода выше: 31,07 с.</span><span class="sxs-lookup"><span data-stu-id="f8c90-201">Time taken to execute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="f8c90-202">Оценка моделей классификации и регрессии с применением метода градиентного бустинга деревьев</span><span class="sxs-lookup"><span data-stu-id="f8c90-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="f8c90-203">С помощью кода, описанного в этом разделе, можно загрузить сохраненные в хранилище BLOB-объектов Azure модели классификации и регрессии с применением метода градиентного бустинга деревьев, оценить их эффективность с помощью стандартных показателей классификации и регрессии, а затем сохранить результаты в том же хранилище.</span><span class="sxs-lookup"><span data-stu-id="f8c90-203">The code in this section shows how to load classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span> 

<span data-ttu-id="f8c90-204">**spark.mllib** предусматривает использование метода деревьев с градиентным бустингом (GBT) в моделях двоичной классификации и регрессии с применением как непрерывных, так и категориальных признаков.</span><span class="sxs-lookup"><span data-stu-id="f8c90-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="f8c90-205">[Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений.</span><span class="sxs-lookup"><span data-stu-id="f8c90-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="f8c90-206">Этот метод предусматривает итеративное обучение деревьев принятия решений, что позволяет свести потери к минимуму.</span><span class="sxs-lookup"><span data-stu-id="f8c90-206">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="f8c90-207">С его помощью можно обрабатывать категориальные признаки, а также определять нелинейные зависимости и взаимодействия признаков. Этот метод не требует масштабирования признаков.</span><span class="sxs-lookup"><span data-stu-id="f8c90-207">GBTs can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="f8c90-208">Кроме того, его можно использовать для создания модели мультиклассовой классификации.</span><span class="sxs-lookup"><span data-stu-id="f8c90-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    #LOAD AND SCORE THE MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="f8c90-209">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="f8c90-209">**OUTPUT:**</span></span>

<span data-ttu-id="f8c90-210">Время на выполнение кода выше: 14,6 с.</span><span class="sxs-lookup"><span data-stu-id="f8c90-210">Time taken to execute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="f8c90-211">Очистка объектов из памяти и вывод расположений оцененных файлов</span><span class="sxs-lookup"><span data-stu-id="f8c90-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH TO SCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="f8c90-212">**ВЫХОДНЫЕ ДАННЫЕ:**</span><span class="sxs-lookup"><span data-stu-id="f8c90-212">**OUTPUT:**</span></span>

<span data-ttu-id="f8c90-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="f8c90-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="f8c90-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="f8c90-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="f8c90-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="f8c90-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="f8c90-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="f8c90-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="f8c90-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="f8c90-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="f8c90-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="f8c90-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="f8c90-219">Использование моделей Spark через веб-интерфейс</span><span class="sxs-lookup"><span data-stu-id="f8c90-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="f8c90-220">В кластере Spark реализован механизм, который позволяет отправлять пакетные задания или интерактивные запросы удаленно через интерфейс REST с помощью компонента Livy.</span><span class="sxs-lookup"><span data-stu-id="f8c90-220">Spark provides a mechanism to remotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="f8c90-221">Livy включен по умолчанию в кластере Spark в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f8c90-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="f8c90-222">Дополнительные сведения о Livy см. в статье [Удаленная отправка заданий Spark в кластер Apache Spark в HDInsight с помощью Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="f8c90-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="f8c90-223">Вы можете использовать Livy, чтобы удаленно отправить запрос на выполнение пакетного задания оценки файла, сохраненного в большом двоичном объекте Azure, а затем записать результаты в другой большой двоичный объект.</span><span class="sxs-lookup"><span data-stu-id="f8c90-223">You can use Livy to remotely submit a job that batch scores a file that is stored in an Azure blob and then writes the results to another blob.</span></span> <span data-ttu-id="f8c90-224">Чтобы сделать это, необходимо загрузить сценарий Python из </span><span class="sxs-lookup"><span data-stu-id="f8c90-224">To do this, you upload the Python script from</span></span>  
<span data-ttu-id="f8c90-225">репозитория [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) в большой двоичный объект кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="f8c90-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) to the blob of the Spark cluster.</span></span> <span data-ttu-id="f8c90-226">Используйте **Microsoft Azure Storage Explorer** или **AzCopy**, чтобы скопировать сценарий в большой двоичный объект кластера.</span><span class="sxs-lookup"><span data-stu-id="f8c90-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** to copy the script to the cluster blob.</span></span> <span data-ttu-id="f8c90-227">В нашем случае мы загрузили скрипт в ***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="f8c90-227">In our case we uploaded the script to ***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="f8c90-228">Необходимые ключи доступа можно найти на портале для учетной записи хранения, связанной с кластером Spark.</span><span class="sxs-lookup"><span data-stu-id="f8c90-228">The access keys that you need can be found on the portal for the storage account associated with the Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="f8c90-229">После загрузки скрипт будет выполнен в кластере Spark в распределенном контексте.</span><span class="sxs-lookup"><span data-stu-id="f8c90-229">Once uploaded to this location, this script runs within the Spark cluster in a distributed context.</span></span> <span data-ttu-id="f8c90-230">Он загрузит модель и запустит прогнозирование на основе входных файлов в зависимости от модели.</span><span class="sxs-lookup"><span data-stu-id="f8c90-230">It loads the model and runs predictions on input files based on the model.</span></span>  

<span data-ttu-id="f8c90-231">Этот скрипт можно вызвать удаленно, выполнив простой запрос HTTPS или REST в Livy.</span><span class="sxs-lookup"><span data-stu-id="f8c90-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="f8c90-232">Ниже приведен пример команды Curl, с помощью которой можно создать запрос HTTP для удаленного вызова скрипта Python.</span><span class="sxs-lookup"><span data-stu-id="f8c90-232">Here is a curl command to construct the HTTP request to invoke the Python script remotely.</span></span> <span data-ttu-id="f8c90-233">Параметры CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME следует заменить соответствующими значениями для используемого кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="f8c90-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with the appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND TO INVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="f8c90-234">Чтобы вызвать задание Spark через Livy, необходимо выполнить простой вызов HTTP с обычной проверкой подлинности. В удаленной системе для этого можно использовать любой язык.</span><span class="sxs-lookup"><span data-stu-id="f8c90-234">You can use any language on the remote system to invoke the Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="f8c90-235">При выполнении вызова HTTP удобнее использовать библиотеку запросов для Python, но она не установлена по умолчанию в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="f8c90-235">It would be convenient to use the Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="f8c90-236">Поэтому вместо нее используются старые библиотеки HTTP.</span><span class="sxs-lookup"><span data-stu-id="f8c90-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="f8c90-237">Ниже приведен пример кода Python для вызова HTTP.</span><span class="sxs-lookup"><span data-stu-id="f8c90-237">Here is the Python code for the HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF THE REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY THE PYTHON SCRIPT TO RUN ON THE SPARK CLUSTER
    # IN THE FILE PARAMETER OF THE JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="f8c90-238">Чтобы отправить запрос на выполнение задания Spark для оценки большого двоичного объекта на основе событий (например, активации, создания или обновления большого двоичного объекта), можно добавить этот код Python в [Функции Azure](https://azure.microsoft.com/documentation/services/functions/).</span><span class="sxs-lookup"><span data-stu-id="f8c90-238">You can also add this Python code to [Azure Functions](https://azure.microsoft.com/documentation/services/functions/) to trigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="f8c90-239">Если вы не хотите работать с кодом, используйте [приложения логики Azure](https://azure.microsoft.com/documentation/services/app-service/logic/), чтобы вызвать пакетную оценку Spark. Для этого определите действие HTTP в **конструкторе приложений логики** и настройте соответствующие параметры.</span><span class="sxs-lookup"><span data-stu-id="f8c90-239">If you prefer a code free client experience, use the [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) to invoke the Spark batch scoring by defining an HTTP action on the **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="f8c90-240">На портале Azure создайте приложение логики, выбрав **+Создать** -> **Интернет+мобильные устройства** -> **Приложение логики**.</span><span class="sxs-lookup"><span data-stu-id="f8c90-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="f8c90-241">Введите имя приложения логики и план служб приложений, чтобы открыть **конструктор приложений логики**.</span><span class="sxs-lookup"><span data-stu-id="f8c90-241">To bring up the **Logic Apps Designer**, enter the name of the Logic App and App Service Plan.</span></span>
* <span data-ttu-id="f8c90-242">Выберите действие HTTP и введите параметры, показанные на рисунке ниже.</span><span class="sxs-lookup"><span data-stu-id="f8c90-242">Select an HTTP action and enter the parameters shown in the following figure:</span></span>

![Конструктор Logic Apps](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="f8c90-244">Что дальше?</span><span class="sxs-lookup"><span data-stu-id="f8c90-244">What's next?</span></span>
<span data-ttu-id="f8c90-245">**Перекрестная проверка и перебор гиперпараметров**. Сведения об обучении моделей с помощью перекрестной проверки и перебора гиперпараметров см. в статье [Расширенное исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md).</span><span class="sxs-lookup"><span data-stu-id="f8c90-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

