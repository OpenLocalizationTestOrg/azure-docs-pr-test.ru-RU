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
# <a name="operationalize-spark-built-machine-learning-models"></a>Ввод моделей машинного обучения, созданных с помощью Spark, в эксплуатацию
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

В этом разделе показано, как toooperationalize сохраненного модели машинного обучения (ML) с помощью Python на HDInsight Spark кластеров. Здесь описываются процедуры tooload машинного обучения моделей, построенных с использованием Spark MLlib и хранятся в хранилище больших двоичных объектов Azure (WASB) и tooscore их с наборами данных, также сохраненные в WASB. Он показывает процессами toopre hello входных данных, компонентов преобразования с использованием hello индексирования и кодировка функции в набор средств MLlib hello и как toocreate объекта с меткой точки данных, который можно использовать в качестве входных данных для оценки с моделями hello машинного Обучения. Hello модели, используемые для оценки включают линейной регрессии, логистической регрессии, моделей случайные леса и градиента повышение приоритета моделей дерева.

## <a name="spark-clusters-and-jupyter-notebooks"></a>Кластеры Spark и записные книжки Jupyter
Шаги настройки и toooperationalize кода hello модель машинного Обучения предоставляются в этом пошаговом руководстве по использованию кластер HDInsight Spark 1.6, а также кластер Spark 2.0. Hello код для этих процедур также предоставляется в записные книжки Jupyter.

### <a name="notebook-for-spark-16"></a>Записная книжка для Spark 1.6
Hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) книжке Jupyter показано, как toooperationalize сохраненную модель с помощью Python в HDInsight кластеров. 

### <a name="notebook-for-spark-20"></a>Записная книжка для Spark 2.0
книжке Jupyter hello toomodify для toouse Spark 1.6 с кластером HDInsight Spark 2.0 заменить файл кода hello Python с [этот файл](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py). Этот код показывает способ создания модели tooconsume hello в Spark 2.0.


## <a name="prerequisites"></a>Предварительные требования

1. Вам потребуется учетная запись Azure и Spark 1.6 (или Spark 2.0) кластер HDInsight toocomplete в данном пошаговом руководстве. В разделе hello [Обзор для обработки и анализа данных с помощью Spark на Azure HDInsight](machine-learning-data-science-spark-overview.md) инструкции о том, как toosatisfy эти требования. Этот раздел также содержит описание hello такси 2013 NYC данные, используемые здесь и инструкции о том, как код tooexecute из записной книжке Jupyter на кластере Spark hello. 
2. Необходимо также создать hello моделей машинного обучения toobe здесь рассчитаны с одновременной ликвидации hello [данных и моделирование с Spark](machine-learning-data-science-spark-data-exploration-modeling.md) раздел для кластера Spark 1.6 hello или ноутбуки hello Spark 2.0. 
3. портативные компьютеры Hello Spark 2.0 использовать дополнительный набор данных для задачи классификации hello, hello хорошо известных авиакомпании на время отправления набор данных на основе 2011 г. и 2012. Описание toothem hello записных книжек и ссылки, представлено в hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub hello, содержащий их. Кроме того код hello здесь и в записных книжках hello связаны является универсальным и должен работать на любой кластер Spark. Если вы не используете HDInsight Spark, настройку и управление ими действия hello кластера может быть немного отличается от показанной здесь. 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Программа установки: hello, библиотеки и расположения хранилища конфигурации Spark контекста
Spark — может tooan tooread и записи больших двоичных объектов хранилища Azure (WASB). Поэтому любые существующие данные, хранящиеся в ней могут быть обработаны с помощью Spark и hello результаты хранимых в WASB.

toosave модели или файлов в WASB, hello путь должен toobe указано правильно. Hello кластера Spark toohello присоединенного контейнера по умолчанию можно обращаться, используя путь, начиная с: *«wasb / /»*. Hello следующий код задает расположение hello чтения toobe данных hello и hello hello модели хранения каталога toowhich hello модели выходных данных будет сохранен. 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Настройка путей каталога к месту хранения в хранилище BLOB-объектов
Модели сохраняются в следующем расположении: wasb:///user/remoteuser/NYCTaxi/Models. Если этот путь задан неправильно, загрузить модели для оценки не удастся.

Hello оцененные результаты были сохранены в: «wasb: / / / пользователя/remoteuser/NYCTaxi/ScoredResults». Если путь toofolder hello является неверной, результаты не сохраняются в этой папке.   

> [!NOTE]
> пути к расположению файла Hello можно скопировать и вставить в заполнители hello в этом коде из вывода hello hello последнюю ячейку hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** ноутбука.   
> 
> 

Вот путей к каталогам tooset кода hello. 

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

**ВЫХОДНЫЕ ДАННЫЕ:**

datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)

### <a name="import-libraries"></a>Импорт библиотек
Spark в контексте, а затем импортируйте необходимые библиотеки после кода hello

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


### <a name="preset-spark-context-and-pyspark-magics"></a>Предустановленный контекст Spark и волшебные команды PySpark
Hello PySpark ядер, предоставляемых с записные книжки Jupyter имеют предустановленных контекста. Поэтому необязательно tooset hello Spark или куст контекстов явно перед началом работы с приложением hello, которое вы разрабатываете. Эти контексты доступны вам по умолчанию, а именно:

* sc для Spark; 
* sqlContext для Hive.

Hello ядра PySpark предоставляет некоторые предопределенные «magics», которые являются специальные команды, которые можно вызвать с %%. В этих примерах кода используются две подобные команды.

* **%% локального** указанного кода hello в последующих строках выполняется локально. В качестве кода должен быть указан корректный код Python.
* **%%sql -o <variable name>** 
* Выполняет запрос Hive в отношении hello sqlContext. Если передается параметр -o hello, hello результат запроса hello сохраняется в hello %% локального контекста Python как Pandas кадр данных.

Для Дополнительные сведения о ядра hello записные книжки Jupyter и предопределенные hello «magics», они предоставляют, в разделе [кластеры ядер, доступных для записные книжки Jupyter с HDInsight Spark Linux в HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a>Прием данных и создание очищенного фрейма данных
В этом разделе содержится код hello для ряда задач требуется tooingest hello данных toobe оцененных. Чтения в соединяемых 0,1% образец hello такси маршрута и тариф авиакомпании файла (хранятся в формате .tsv) hello формат данных, а затем создает кадр очистки данных.

Hello такси маршрута и тариф авиакомпании файлы были соединены на основе на процедуру hello в: [hello командного процесса обработки и анализа данных в действие: с использованием кластеров HDInsight Hadoop](machine-learning-data-science-process-hive-walkthrough.md) раздела.

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

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 46.37 секунд

## <a name="prepare-data-for-scoring-in-spark"></a>Подготовка данных для оценки в Spark
В этом разделе описывается, как tooindex, кодирования и масштабировать категориальных признаков tooprepare их для использования в алгоритмах обучения MLlib защищено для классификации и регрессии.

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a>Преобразование признаков. Индексирование и кодирование категориальных признаков для получения входных данных для оцениваемых моделей
В этом разделе показано, как tooindex категориальные данные с помощью `StringIndexer` и кодирование функций с `OneHotEncoder` ввода в модели hello.

Hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) кодирует строковый столбец метки столбца tooa метки индексов. индексы Hello упорядочиваются по частот метки. 

Hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) сопоставляет столбец метки столбца tooa индексы двоичных векторов, с максимум один значение single. Эта кодировка позволяет алгоритмы, которые ожидают непрерывного табличное значение функции, такие как логистическая Регрессия toobe применения toocategorical функции.

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

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 5.37 секунд

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a>Создание объектов устойчивого распределенного набора данных с массивами признаков для получения входных данных для моделей
Этот раздел содержит код, который показывает, как категориальные текстовые данные tooindex как RDD объекта и горячей один зашифровать их, поэтому ее можно использовать tootrain и тестирования MLlib логистической регрессии и модели на основе дерева. Hello индексированных данных хранится в [устойчивым распределенного набора данных (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) объектов. Это базовая абстракция hello в Spark. Объект устойчивого распределенного набора данных — это неизменяемая, секционированная коллекция элементов, которыми можно одновременно управлять с помощью Spark.

Он также содержит код, который показывает, как hello tooscale данных с помощью `StandardScalar` MLlib, предоставляемые для использования в линейной регрессии с вероятностный градиентный спуск (SGD), популярный алгоритм для обучения широкий спектр моделей машинного обучения. Hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) — разница toounit функции hello используется tooscale. Масштабирование функции, также известные как нормализация данных гарантирует, что функции широко распределенные значениями не учитывая чрезмерного весить в целевой функции hello. 

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

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 11.72 секунд

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a>Hello модели логистической регрессии для создания рейтингов и сохранить tooblob выходных данных
Hello кода в этом разделе показано, как tooload модели логистической регрессии, сохраненного в Azure хранилище больших двоичных объектов и использовать toopredict, оплачивается ли подсказка в такси обработки, оценка его с метриками стандартные классификации, а затем сохраните и tooblob hello результатов построения хранилище. Привет, оцененные результаты хранятся в объектах RDD. 

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

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 19.22 секунд

## <a name="score-a-linear-regression-model"></a>Оценка модели линейной регрессии
Мы использовали [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain модель линейной регрессии, используя вероятностный градиентный спуск (SGD) для оптимизации toopredict hello объем совет платная. 

Hello кода в этом разделе показано, как оценка с помощью переменных масштабированный tooload модель линейной регрессии из хранилища BLOB-объектов Azure, а затем сохраните hello результаты назад toohello blob.

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


**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 16.63 секунд

## <a name="score-classification-and-regression-random-forest-models"></a>Оценка моделей классификации и регрессии с применением алгоритма случайного леса
кода Hello в этом разделе показано, как tooload hello сохраняет классификации и случайного леса модели регрессии в хранилище BLOB-объектов Azure оценки их производительности с помощью стандартных классификатора и регрессии меры, а затем сохраните hello результаты назад tooblob хранилища.

[Случайные леса](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) — это совокупности деревьев принятия решений.  Они объединяют многих решений деревьев tooreduce hello риск переобучения. Случайные леса могут обрабатывать категориальных признаков расширения toohello мультиклассовой классификации параметр, не требуется возможность масштабирования и являются может toocapture нелинейности и возможностей взаимодействия. Случайные леса принадлежат hello наиболее успешных моделей машинного обучения для классификации и регрессии.

[spark.mllib](http://spark.apache.org/mllib/) предусматривает использование метода случайного леса в моделях двоичной, мультиклассовой классификации и регрессии с применением как непрерывных, так и категориальных признаков. 

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

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 31.07 секунд

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a>Оценка моделей классификации и регрессии с применением метода градиентного бустинга деревьев
Hello кода в этом разделе описывается, как tooload классификации и регрессии градиента моделей дерева повышение приоритета из хранилища BLOB-объектов Azure, оценки их производительности с помощью стандартных классификатора и меры регрессии и сохраните hello результаты назад tooblob хранилища. 

**spark.mllib** предусматривает использование метода деревьев с градиентным бустингом (GBT) в моделях двоичной классификации и регрессии с применением как непрерывных, так и категориальных признаков. 

[Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений. Решение GBTs обучение итеративного дерева toominimize функции потерь. GBTs может обрабатывать категориальных признаков не требуется возможность масштабирования и являются может toocapture нелинейности и возможностей взаимодействия. Кроме того, его можно использовать для создания модели мультиклассовой классификации.

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

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 14.6 секунд

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a>Очистка объектов из памяти и вывод расположений оцененных файлов
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


**ВЫХОДНЫЕ ДАННЫЕ:**

logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt

linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949

randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt

randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt

BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt

BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt

## <a name="consume-spark-models-through-a-web-interface"></a>Использование моделей Spark через веб-интерфейс
Spark обеспечивает механизм tooremotely отправки пакетных заданий или интерактивной обработки запросов через REST взаимодействовать с компонентом, называется Livy. Livy включен по умолчанию в кластере Spark в HDInsight. Дополнительные сведения о Livy см. в статье [Удаленная отправка заданий Spark в кластер Apache Spark в HDInsight с помощью Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md). 

Можно использовать Livy tooremotely отправить задание по пакетной оценок файл, который хранится в BLOB-объекта Azure, а затем записывает большой двоичный объект tooanother результаты hello. toodo, отправьте hello сценарий Python из  
[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello большого двоичного объекта из кластера Spark hello. Можно использовать средства, подобного **обозреватель хранилищ Microsoft Azure** или **AzCopy** toocopy hello сценария toohello кластера blob. В нашем случае мы загружен скрипт hello слишком***wasb:///example/python/ConsumeGBNYCReg.py***.   

> [!NOTE]
> Здравствуйте, клавиши доступа, вы должны можно найти на портале hello для учетной записи хранения hello, связанные с кластера Spark hello. 
> 
> 

После отправки toothis расположение внутри кластера Spark hello в контексте распределенных запуска этого сценария. Он загружает модель hello и запускает прогнозы на входные файлы на основе модели hello.  

Этот скрипт можно вызвать удаленно, выполнив простой запрос HTTPS или REST в Livy.  Вот перелистывание команда tooconstruct hello HTTP запроса tooinvoke hello сценарий Python удаленно. Замените CLUSTERLOGIN, CLUSTERPASSWORD, ИМЯ_КЛАСТЕРА hello соответствующие значения для кластера Spark.

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

Можно использовать любой язык на задание hello удаленной системе tooinvoke hello Spark через Livy путем вызова простой HTTPS с обычной проверкой подлинности.   

> [!NOTE]
> Было бы библиотеки Python запросы hello удобный toouse при выполнении данного вызова HTTP, но сейчас не установлена по умолчанию в функциях Azure. Поэтому вместо нее используются старые библиотеки HTTP.   
> 
> 

Ниже приведен код Python hello для вызова hello HTTP.

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


Можно также добавить этот код Python слишком[функции Azure](https://azure.microsoft.com/documentation/services/functions/) tootrigger отправки задания Spark, которая оценивает большого двоичного объекта на основе различных событий как таймер, создания или обновления большого двоичного объекта. 

Взаимодействие с произвольным клиентом кода, используйте hello [приложения логики Azure](https://azure.microsoft.com/documentation/services/app-service/logic/) оценки за счет определения действия HTTP для hello пакета Spark hello tooinvoke **логику приложения конструктор** и задание его параметров. 

* На портале Azure создайте приложение логики, выбрав **+Создать** -> **Интернет+мобильные устройства** -> **Приложение логики**. 
* toobring копирование hello **логику приложения конструктор**, введите имя hello hello логику приложения и план служб приложений.
* Выберите действие HTTP и введите hello параметров, приведенных в следующий рисунок hello:

![Конструктор Logic Apps](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a>Что дальше?
**Перекрестная проверка и перебор гиперпараметров**. Сведения об обучении моделей с помощью перекрестной проверки и перебора гиперпараметров см. в статье [Расширенное исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md).

