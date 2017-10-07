---
title: "aaaData исследования и моделирования с Spark | Документы Microsoft"
description: "Демонстрирует hello возможности набора средств hello Spark MLlib на Azure моделирования и просмотра данных."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a>Исследование и моделирование данных с помощью Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

В этом пошаговом руководстве использует просмотр данных toodo HDInsight Spark и двоичной классификации и регрессии задачи моделирования образца hello NYC такси маршрута и успешного 2013 набора данных.  Он поможет выполнить шаги hello hello [процесса обработки и анализа данных](http://aka.ms/datascienceprocess), узел узел, с помощью HDInsight Spark кластера для обработки и модели данных и hello hello toostore больших двоичных объектов Azure. Hello процесс более подробно рассматривается и визуализация данных из большого двоичного объекта хранилища Azure и затем выполняется подготовка данных toobuild hello прогнозных моделей. Эти модели, с помощью hello Spark MLlib toolkit toodo двоичной классификации и регрессии моделирования задачи построения.

* Hello **двоичной классификации** задача — toopredict ли совет оплачивается поездки hello. 
* Hello **регрессии** задача представляет сумму hello toopredict hello подсказки на основе других функций подсказки. 

модели Hello, мы используем включают логистической и линейной регрессии, случайные леса и градиента повышенных деревьев:

* [Линейная регрессия с SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) модель линейной регрессии, которая использует метод вероятностный градиентный спуск (SGD) и для оптимизации и возможность масштабирования toopredict hello совет суммы оплаты. 
* [Логистическая Регрессия с LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) и регрессии «logit» представляет собой модель регрессии, который может использоваться при классификации данных категориальные toodo hello зависимой переменной. LBFGS-это алгоритм оптимизации реализация ньютон, соответствующий алгоритм Бройдена-Флетчера-Гольдфарба-Шанно (BFGS) hello ограниченный объем памяти компьютера с помощью и широко используемый в машинном обучении.
* [Случайные леса](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) — это совокупности деревьев принятия решений.  Они объединяют многих решений деревьев tooreduce hello риск переобучения. Случайные леса, используются для классификации и регрессии и может обрабатывать категориальных признаков и могут быть расширены параметр toohello мультиклассовой классификации. Они не требуется возможность масштабирования и являются может toocapture нелинейности и возможность взаимодействия. Случайные леса принадлежат hello наиболее успешных моделей машинного обучения для классификации и регрессии.
* [Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений. Решение GBTs обучение итеративного дерева toominimize функции потерь. GBTs используются для классификации и регрессии и может обрабатывать категориальных признаков не требуется возможность масштабирования и являются может toocapture нелинейности и возможностей взаимодействия. Кроме того, его можно использовать для создания модели мультиклассовой классификации.

Hello моделирования действия также содержат код, показывающий, как tootrain, оценки и сохранение каждого типа модели. Python был используется toocode hello решения и tooshow hello соответствующие графики.   

> [!NOTE]
> Хотя набор средств Spark MLlib hello спроектированный toowork с большими наборами данных, сравнительно небольшую выборку (с помощью 170 тысяч строк, 0,1% hello исходный набор данных NYC ~ 30 МБ) используется здесь для удобства. Упражнение Hello в данном разделе выполняется эффективно (в течение 10 минут) в кластере HDInsight с 2 рабочих узлов. Hello одинаковый код, с небольшими изменениями может быть используется tooprocess более крупных-наборов данных, с соответствующими изменениями для кэширования данных в памяти и изменение размера кластера hello.
> 
> 

## <a name="prerequisites"></a>Предварительные требования
Вам потребуется учетная запись Azure и Spark 1.6 (или Spark 2.0) кластер HDInsight toocomplete в данном пошаговом руководстве. В разделе hello [Обзор для обработки и анализа данных с помощью Spark на Azure HDInsight](machine-learning-data-science-spark-overview.md) инструкции о том, как toosatisfy эти требования. Этот раздел также содержит описание hello такси 2013 NYC данные, используемые здесь и инструкции о том, как код tooexecute из записной книжке Jupyter на кластере Spark hello. 

## <a name="spark-clusters-and-notebooks"></a>Кластеры и записные книжки Spark
Действия по настройке и код, указанные в этом пошаговом руководстве, применимы к использованию для HDInsight Spark 1.6. Но записные книжки Jupyter можно использовать для кластеров HDInsight Spark 1.6 и Spark 2.0. Описание toothem hello записных книжек и ссылки, представлено в hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub hello, содержащий их. Кроме того код hello здесь и в записных книжках hello связаны является универсальным и должен работать на любой кластер Spark. Если вы не используете HDInsight Spark, настройку и управление ими действия hello кластера может быть немного отличается от показанной здесь. Для удобства ниже приведены hello ссылки записные книжки Jupyter toohello для 1.6 Spark (выполняются в ядро pySpark hello hello server книжке Jupyter toobe) и 2.0 Spark (toobe запуска ядра pySpark3 hello объекта hello книжке Jupyter сервера).

### <a name="spark-16-notebooks"></a>Записные книжки для Spark 1.6

[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): содержит сведения о том, как просмотр данных tooperform, моделирование и оценка с несколько разных алгоритмов.

### <a name="spark-20-notebooks"></a>Записные книжки для Spark 2.0
Hello регрессии и классификации задачи, которые реализуются с помощью кластера Spark 2.0 находятся в отдельном записных книжек и записной книжки hello классификации используются различные наборы данных.

- [Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): этот файл содержит сведения о как tooperform Просмотр данных, моделирования и оценки в Spark 2.0 кластеры, использующие hello trip такси NYC и набор данных тариф авиакомпании, описано [здесь](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Записной книжки может быть хорошей отправной точкой для быстрого исследования кода hello, предоставленные для Spark 2.0. Для подробных записной книжки анализирует hello такси NYC данных, см. Далее записной книжки hello в этом списке. См. примечания hello ниже, сравнивающие эти портативные компьютеры. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): этот файл показывает, как tooperform данные wrangling (Spark SQL и кадр данных операции), просмотр, моделирование и оценка с помощью hello trip такси NYC и тариф авиакомпании набор данных описывается [ Здесь](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): этот файл показывает, как tooperform данные wrangling (Spark SQL и кадр данных операции), просмотр, моделирование и оценка с помощью hello хорошо известных авиакомпании на время отправления набор данных на основе 2011 г. и 2012. Мы интегрировать dataset авиакомпании hello hello аэропорта погоды данных (например, windspeed, температуры, высота над уровнем моря т. д.) предыдущих toomodeling, эти функции погоды могут быть включены в модель hello.

<!-- -->

> [!NOTE]
> набор данных авиакомпании Hello был добавлен toohello Spark 2.0 записных книжек toobetter иллюстрируют использование hello алгоритмы классификации. См. следующие ссылки на сведения о набора данных на время отправления авиакомпании и набора данных погоды hello.

>- Данные о расписании вылетов авиакомпании: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Данные о погоде в аэропортах: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
записных книжек Spark 2.0 Hello на такси NYC hello и наборы авиакомпании рейса задержка данных может занять 10 минут или более toorun (в зависимости от размера hello кластер HDI). Hello первой записной книжки в hello над списком показаны различные аспекты hello исследования данных, визуализации и машинного Обучения моделей обучения в записной книжке, занимает меньше времени toorun уменьшается NYC набора данных, в которой hello такси и тариф авиакомпании файлы были предварительно присоединены к домену: [ Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) записной книжки принимает более короткое время toofinish (2-3 минуты) и может быть это хорошая отправная точка для быстро анализ кода hello у нас есть обеспечивает Spark 2.0. 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
Hello ниже описаны связанные toousing Spark 1.6. Для версий Spark 2.0 используйте записных книжек hello описаны и ссылки выше. 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Программа установки: hello, библиотеки и расположения хранилища конфигурации Spark контекста
Spark — может tooAzure tooread и записи хранилища больших двоичных объектов (также известный как WASB). Поэтому любые существующие данные, хранящиеся в ней могут быть обработаны с помощью Spark и hello результаты хранимых в WASB.

toosave модели или файлов в WASB, hello путь должен toobe указано правильно. Hello кластера Spark toohello присоединенного контейнера по умолчанию можно обращаться, используя путь, начиная с: «wasb: / / /». Другие расположения начинаются с wasb://.

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Настройка путей каталога к месту хранения в хранилище BLOB-объектов
Hello следующий код задает hello место чтения toobe данных hello и hello hello модели хранения каталога toowhich hello модели выходных данных будет сохранен:

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a>Импорт библиотек
Для установки также требуется импорт необходимых библиотек. Задать контекст spark и импортируйте необходимые библиотеки с hello, следующий код:

    # IMPORT LIBRARIES
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

* **%% локального** указывает, что код hello в последующих строках toobe выполняются локально. В качестве кода должен быть указан корректный код Python.
* **%% sql -o <variable name>**  выполняет запрос Hive в отношении hello sqlContext. Если передается параметр -o hello, hello результат запроса hello сохраняется в hello %% локального контекста Python как Pandas кадр данных.

Для Дополнительные сведения о ядра hello записные книжки Jupyter и предопределенные hello «magics», они предоставляют, в разделе [кластеры ядер, доступных для записные книжки Jupyter с HDInsight Spark Linux в HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="data-ingestion-from-public-blob"></a>Прием данных из открытого большого двоичного объекта
Первым шагом процесса обработки и анализа данных hello Hello является tooingest hello данных toobe анализируются из источников где — находится в среде моделирования и просмотра данных. Среда Hello — Spark в этом пошаговом руководстве. Этот раздел содержит toocomplete кода hello последовательности задач:

* hello данные примера toobe моделируется приема
* чтение во входном наборе данных hello (хранятся в формате .tsv)
* Очистить hello данные и формат
* создание и кэширование объектов (устойчивых распределенных наборов данных или фреймов данных) в памяти;
* регистрация данных в качестве временной таблицы в контексте SQL.

Ниже приведен код hello для приема данных.

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
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

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 51.72 секунд

## <a name="data-exploration--visualization"></a>Исследование и визуализация данных
Hello данных была помещена в Spark, hello следующим шагом в процессе обработки и анализа данных hello после toogain глубокого понимания hello данных через Просмотр и визуализация. В этом разделе рассматриваются hello такси данные с помощью SQL-запросов построения hello целевой переменных и потенциальных возможностей для визуальной проверки. В частности мы построения hello частоту пассажира счетчиков в такси приема-передачи, частота hello совет сумм и как изменять советы по типам и сумма платежа.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Построить гистограмму для частоты счетчика пассажира в образце hello такси приема-передачи данных
Этот код и последующие фрагменты использовать образец hello magic tooquery SQL и данных локального magic tooplot hello.

* **Магическое SQL (`%%sql`)** hello ядра HDInsight PySpark поддерживает встроенные легко HiveQL запросы к hello sqlContext. Hello (-o имя_переменной) аргумент hello выходных данных запроса SQL hello сохраняется как Pandas кадр данных на сервере Jupyter hello. Это означает, что он доступен в локальном режиме hello.
* Hello  **`%%local` магическое** — использовать код toorun локально на сервере Jupyter hello, где hello головному узлу кластера HDInsight hello. Как правило, используется `%%local` magic вместе с hello `%%sql` magic с параметром -o. параметр -o Hello сохранится hello выходных данных запроса SQL hello локально и затем %% локального magic приведет к запуску hello следующего набора toorun фрагмент кода локально к выходным данным hello hello запросов SQL, в которой сохраняется локально

выходные данные Hello автоматически визуализируются после выполнения кода hello.

Этот запрос извлекает hello приема-передачи данных по количеству пассажира. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

Этот код создает локальный кадров данных из результатов запроса hello и представлены данные hello. Hello `%%local` magic создает локальный-кадра данных, `sqlResults`, который может использоваться для отображения на диаграмме с помощью matplotlib. 

> [!NOTE]
> В этом пошаговом руководстве волшебная команда PySpark используется несколько раз. При больших размерах hello объем данных следует образец toocreate кадра данных, помещающихся в локальной памяти.
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Вот hello кода tooplot hello приема-передачи с пассажира счетчиков

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**ВЫХОДНЫЕ ДАННЫЕ:**

![Частота поездок в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

Можно выбирать различные виды визуализаций (таблицы, круговая, строки, области или панели) с помощью hello **тип** кнопок меню в записной книжке hello. Здесь показана панель построения Hello.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Построение гистограммы суммы чаевых и ее зависимости от количества пассажиров и тарифа.
Используйте toosample данных запроса SQL.

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped 
    FROM taxi_train 
    WHERE passenger_count > 0 
    AND passenger_count < 7 
    AND fare_amount > 0 
    AND fare_amount < 200 
    AND payment_type in ('CSH', 'CRD') 
    AND tip_amount > 0 
    AND tip_amount < 25


Эта ячейка код использует данные о hello hello SQL запроса toocreate три графики.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


**ВЫХОДНЫЕ ДАННЫЕ:** 

![Распределение суммы чаевых](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Сумма чаевых в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Сумма чаевых в зависимости от тарифа](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Проектирование признаков, преобразование и подготовка данных к моделированию
В этом разделе описывается и предоставляет кода hello для процедур, используемых tooprepare данных для использования в модели машинного Обучения. Здесь показано, как hello toodo следующие задачи:

* Создание нового признака путем группирования часов в периоды трафика
* индексация и кодирование категориальных признаков;
* Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения
* Создание вложенных случайной выборки данных hello и разбейте его на обучающий и проверочный наборы
* масштабирование признаков;
* кэширование объектов в памяти.

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Создание нового признака путем группирования часов в периоды трафика
Этот код показывает, как toocreate новая функция путем сегментирования часов в момент трафик контейнеров, а затем как toocache hello результирующий кадр данных в памяти. Где устойчивым распределенных наборы данных (RDDs) и кадров данных используются многократно, кэширование приводит tooimproved времени выполнения. Соответственно, мы RDDs и кэш кадров данных на несколько этапов в пошаговом руководстве hello. 

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

**ВЫХОДНЫЕ ДАННЫЕ:** 

126 050.

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a>Индексация и кодирование категориальных признаков в качестве ввода для функций моделирования
В этом разделе показано, как tooindex или кодирования категориальных признаков для входных данных в моделирования функции hello. Здравствуйте моделирования и предполагаете, что функции MLlib требуют возможности с помощью toobe категориальных данных входного индексированных или кодировке предыдущих toouse. В зависимости от модели hello необходима tooindex или кодировать их по-разному:  

* **На основе дерева моделирования** требует toobe категорий, кодируются как числовые значения (например, компонент с три категории могут быть кодированы 0, 1, 2). Для этого можно использовать функцию [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) в MLlib. Эта функция кодирует строковый столбец метки столбца tooa метки индексов, упорядоченных по частот метки. Несмотря на то, что индексации с числовыми значениями для ввода и обработки данных, на основе дерева алгоритмы hello может быть указанного tootreat их соответствующим образом как категории. 
* **Модели логистической и линейной регрессии** требуют горячей один кодировки, where, например, компонент с трем категориям можно развернуть в трех столбцов компонентов, с каждой содержащее 0 или 1 в зависимости от категории hello наблюдения. Предоставляет MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) функции toodo горячей один кодировки. Этот кодировщик сопоставляет столбец метки столбца tooa индексы двоичных векторов, с максимум один значение single. Эта кодировка позволяет алгоритмы, которые ожидают числовой табличное значение функции, такие как логистической регрессии применяется toobe toocategorical функции.

Ниже приведен код tooindex hello и кодирования категориальных признаков:

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
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

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 1,28 секунд

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения
Этот раздел содержит код, который показывает, как тип данных категориальные текст tooindex как с меткой точки данных и зашифровать их, чтобы его можно было использовать tootrain и тестирования MLlib логистической регрессии и других моделей классификации. Объекты с помеченной вершиной отформатированы в устойчивые распределенные наборы данных, которые можно использовать в качестве входных для большинства алгоритмов машинного обучения в MLlib. Объект [с помеченной вершиной](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) — это разреженный или плотный локальный вектор, связанный с меткой или ответом.  

Этот раздел содержит код, который показывает, как tooindex категориальные текстовых данных как [с меткой точки](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) тип данных, а затем включите ее, чтобы его можно было использовать tootrain и тестирования MLlib логистической регрессии и других моделей классификации. Объекты с помеченной вершиной — это устойчивые распределенные наборы данных, состоящие из метки (переменной ответа или целевой переменной) и вектора признаков. Данные в таком формате используются в качестве входных для алгоритмов машинного обучения в MLlib.

Ниже приведен код tooindex hello и кодирования текста функции для двоичной классификации.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


Ниже приведен код hello tooencode и индекс категориальные текстовых признаков для анализа линейной регрессии.

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])

        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>Создание вложенных случайной выборки данных hello и разбейте его на обучающий и проверочный наборы
Этот код создает случайной выборки данных hello (здесь используется 25%). Несмотря на то, что он не является обязательным для этого примера из-за размера toohello hello набора данных, мы демонстрируют, как можно произвести выборку здесь, вы знаете, как toouse его собственные проблемы, если это требуется. Если выборки большие, этот процесс может значительно сэкономить время обучения моделей. Далее мы разбить образец hello в рамках обучения (здесь 75%) и тестирования toouse часть (25% здесь) в классификации и регрессии моделирования.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 0.24 секунд

### <a name="feature-scaling"></a>масштабирование признаков;
Масштабирование функции, также известные как нормализация данных гарантирует, что функции широко распределенные значениями не учитывая чрезмерного весить в целевой функции hello. Hello код для функции масштабирования использует hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello функции toounit дисперсию. MLlib предоставляет функцию StandardScaler для выполнения линейной регрессии с применением метода стохастического градиента. Этот алгоритм широко используется для обучения других моделей машинного обучения (например, регуляризованной регрессии или метода опорных векторов).

> [!NOTE]
> Обнаружено алгоритм toobe hello LinearRegressionWithSGD конфиденциальных toofeature масштабирования.
> 
> 

Вот переменных tooscale hello кода для использования с регуляризацией hello линейный SGD алгоритм.

    # FEATURE SCALING

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ВЫХОДНЫЕ ДАННЫЕ:**

Время, затраченное tooexecute над ячейкой: 13.17 секунд

### <a name="cache-objects-in-memory"></a>кэширование объектов в памяти.
Hello время, необходимое для обучения и проверки алгоритмов машинного Обучения может быть уменьшена путем кэширования объекты кадра hello входные данные, используемые для классификации, регрессию, и возможности масштабирования.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ВЫХОДНЫЕ ДАННЫЕ:** 

Время, затраченное tooexecute над ячейкой: 0,15 секунд

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Прогнозирование вероятности выплаты чаевых за поездку с помощью моделей бинарной классификации
В этом разделе показано, как использование трех моделей для задача двоичной классификации hello прогнозирования, независимо от того, имеется ли для обработки такси оплачивается совет. Hello модели представлены являются:

* регуляризованная логистическая регрессия; 
* модель случайного леса;
* градиентный бустинг деревьев.

Процесс создания модели состоит из следующих этапов: 

1. **Обучение модели** с использованием данных с одним набором параметров.
2. **Оценка модели** на основе набора тестовых данных с метриками.
3. **Сохранение модели** в большом двоичном объекте для последующего использования.

### <a name="classification-using-logistic-regression"></a>Классификация с применением логистической регрессии
Hello кода в этом разделе показано, как tootrain, оценки и сохранить модель логистической регрессии с [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , прогнозирует ли совет получает оплату за маршрут в наборе данных маршрута и тариф авиакомпании такси hello NYC.

**Обучение модели логистической регрессии hello, используя CV и hyperparameter свертки**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ВЫХОДНЫЕ ДАННЫЕ:** 

Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]

Intercept: -0.0111216486893

Время, затраченное tooexecute над ячейкой: 14.43 секунд

**Оценка модели двоичной классификации hello со стандартными показателями**

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**ВЫХОДНЫЕ ДАННЫЕ:** 

Area under PR = 0.985297691373

Area under ROC = 0.983714670256

Summary Stats

Precision = 0.984304060189

Recall = 0.984304060189

F1 Score = 0.984304060189

Время, затраченное tooexecute над ячейкой: 57.61 секунд

**Отобразите hello ROC кривой.**

Hello *predictionAndLabelsDF* регистрируется как таблица, *tmp_results*, в предыдущую ячейку hello. *tmp_results* можно использовать toodo запросов и выводить результаты в hello sqlResults-кадра данных для отображения на диаграмме. Ниже приведен код hello.

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Вот прогнозов toomake кода hello и построения hello ROC кривой.

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**ВЫХОДНЫЕ ДАННЫЕ:**

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a>Классификация случайного леса
Hello кода в этом разделе показано, как tootrain, оценки и сохранить модель случайного леса, которая прогнозирует, оплачивается ли подсказка для обработки в hello NYC такси маршрута и тариф авиакомпании набора данных.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ВЫХОДНЫЕ ДАННЫЕ:**

Area under ROC = 0.985297691373

Время, затраченное tooexecute над ячейкой: 31.09 секунд

### <a name="gradient-boosting-trees-classification"></a>Классификация с применением модели градиентного бустинга деревьев
Hello кода в этом разделе описывается, как tootrain, оценки и сохранить градиента подъема дерева модели, которая прогнозирует, оплачивается ли подсказка для обработки в hello NYC такси маршрута и тариф авиакомпании набора данных.

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ВЫХОДНЫЕ ДАННЫЕ:**

Area under ROC = 0.985297691373

Время, затраченное tooexecute над ячейкой: 19.76 секунд

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a>Прогнозирование суммы чаевых за поездку в такси с помощью моделей регрессии
В этом разделе показано, как использование трех моделей для hello регрессии задача прогнозирования hello Сумма оплаты trip такси, на основе других функций совет подсказки hello. Hello модели представлены являются:

* регуляризованная линейная регрессия;
* случайный лес;
* градиентный бустинг деревьев.

Эти модели был описан в введение hello. Процесс создания модели состоит из следующих этапов: 

1. **Обучение модели** с использованием данных с одним набором параметров.
2. **Оценка модели** на основе набора тестовых данных с метриками.
3. **Сохранение модели** в большом двоичном объекте для последующего использования.

### <a name="linear-regression-with-sgd"></a>Линейная регрессия с применением SGD
Hello кода в этом разделе показано, как toouse масштабировать tootrain функции линейной регрессии, который использует вероятностный градиентный спуск (SGD) для оптимизации, и как tooscore, оценки и сохранить модель hello в хранилище больших двоичных объектов Azure (WASB).

> [!TIP]
> Наш опыт показывает могут возникать проблемы с последующим согласованием hello LinearRegressionWithSGD моделей и параметры должны toobe изменен или оптимизированное тщательно для получения модели. Проблему конвергенции можно решить, выполнив масштабирование переменных. 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ВЫХОДНЫЕ ДАННЫЕ:**

Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]

Intercept: 0.853872718283

RMSE = 1.24190115863

R-sqr = 0.608017146081

Время, затраченное tooexecute над ячейкой: 58,42 секунд

### <a name="random-forest-regression"></a>Регрессия с использованием модели случайного леса
Hello кода в этом разделе показано, как tootrain, оценки и сохранить регрессии случайного леса, которая прогнозирует сумма подсказки для hello NYC такси обработки данных.

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ВЫХОДНЫЕ ДАННЫЕ:**

RMSE = 0.891209218139

R-sqr = 0.759661334921

Время, затраченное tooexecute над ячейкой: 49.21 секунд

### <a name="gradient-boosting-trees-regression"></a>Регрессия с применением градиентного бустинга деревьев
Hello кода в этом разделе описывается, как tootrain, оценки и сохранить градиента повышения деревьев модель, прогнозирующая объем подсказки для hello NYC такси обработки данных.

**Обучение и анализ**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ВЫХОДНЫЕ ДАННЫЕ:**

RMSE = 0.908473148639

R-sqr = 0.753835096681

Время, затраченное tooexecute над ячейкой: 34.52 секунд

**Графическое представления**

*tmp_results* регистрируется как таблицу Hive в предыдущую ячейку hello. Результаты из таблицы hello выводятся в hello *sqlResults* кадра данных для отображения на диаграмме. Ниже приведен код hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

Вот hello tooplot кода hello данных с помощью сервера Jupyter hello.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


**ВЫХОДНЫЕ ДАННЫЕ:**

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a>Очистка объектов из памяти
Используйте `unpersist()` toodelete объектов в кэше в памяти.

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a>Запись места хранения для потребления и оценки моделей hello
tooconsume и оценка набор независимых описано в hello [оценка и оценить построение Spark машинного обучения моделей](machine-learning-data-science-spark-model-consumption.md) разделе требуются toocopy и вставки этих файлов имена содержащего hello сохранения моделей, созданных здесь в hello Потребление книжке Jupyter. Вот tooprint кода hello hello пути toomodel файлы, необходимые существует.

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**ВЫХОДНЫЕ ДАННЫЕ**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"

## <a name="whats-next"></a>Что дальше?
Теперь после создания модели регрессии и классификации с hello Spark MlLib, готовы toolearn, как tooscore и оценивать эти модели. Расширенный просмотр данных и моделирования записной книжки Погружение глубже в том числе перекрестной проверки, hyper параметр приветствия широкими и модели оценки. 

**Модели потребления:** toolearn как tooscore и оценить hello классификационных и регрессионных моделей, созданных в этом разделе см. в разделе [оценка и оценки моделей построен Spark машинного обучения](machine-learning-data-science-spark-model-consumption.md).

**Перекрестная проверка и перебор гиперпараметров**. Сведения об обучении моделей с помощью перекрестной проверки и перебора гиперпараметров см. в статье [Расширенное исследование и моделирование данных с помощью Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md).

