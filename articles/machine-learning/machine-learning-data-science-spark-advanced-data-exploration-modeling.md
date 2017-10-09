---
title: "Просмотр данных aaaAdvanced и моделирования с Spark | Документы Microsoft"
description: "С помощью просмотра данных toodo HDInsight Spark и обучения двоичных моделей классификации и регрессии с помощью перекрестной проверки и hyperparameter оптимизации."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a>Расширенное исследование и моделирование данных с помощью Spark
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

В этом пошаговом руководстве используется HDInsight Spark toodo данных обучения и просмотра двоичной классификации и перекрестной проверки моделей регрессии и оптимизации hyperparameter образца hello NYC такси маршрута и успешного 2013 набора данных. Он поможет выполнить шаги hello hello [процесса обработки и анализа данных](http://aka.ms/datascienceprocess), узел узел, с помощью HDInsight Spark кластера для обработки и модели данных и hello hello toostore больших двоичных объектов Azure. Hello процесс более подробно рассматривается и визуализация данных из большого двоичного объекта хранилища Azure и затем выполняется подготовка данных toobuild hello прогнозных моделей. Python был используется toocode hello решения и tooshow hello соответствующие графики. Эти модели, с помощью hello Spark MLlib toolkit toodo двоичной классификации и регрессии моделирования задачи построения. 

* Hello **двоичной классификации** задача — toopredict ли совет оплачивается поездки hello. 
* Hello **регрессии** задача представляет сумму hello toopredict hello подсказки на основе других функций подсказки. 

Hello моделирования действия также содержат код, показывающий, как tootrain, оценки и сохранение каждого типа модели. Hello разделе освещаются некоторые hello основание таким же, как hello [данных и моделирование с Spark](machine-learning-data-science-spark-data-exploration-modeling.md) раздела. Однако он является более «Дополнительно», так как он использует перекрестной проверки с hyperparameter широкими tootrain оптимально точные классификационных и регрессионных моделей. 

**Перекрестная проверка (CV)** — это метод, который оценивает, насколько хорошо модель, обученную на известный набор данных обобщает возможности hello toopredicting наборов данных, на котором он еще не прошла обучение.  Здесь используется общая реализация является набор данных на свертки K toodivide и затем обучения модели hello в циклического перебора всех, кроме одного сверток hello. оценивается возможность Hello hello модели tooprediction точно в том случае, когда протестирован hello независимый набор данных в этой модели hello tootrain свертки не используется.

**Оптимизация Hyperparameter** проблема hello по выбору набор гиперпараметров для алгоритма обучения, обычно с целью hello оптимизация показателем производительности hello алгоритм на независимый набор данных. **Гиперпараметров** — это значения, которые должны быть указаны вне процедуры обучения модели hello. Предположения о этих значений может повлиять на гибкость hello и точности моделей hello. Деревья принятия решений имеют гиперпараметров, к примеру, такие как hello требуемого глубины и количества листьев в дереве hello. Для методов опорных векторов (SVM) необходимо задать условие штрафа за неправильную классификацию. 

Обычно способом tooperform hyperparameter для оптимизации используются здесь является поиска в сетке или **очистки параметров**. Сюда входят выполняет тщательный поиск по значениям hello определенному подмножеству hello hyperparameter пространства для алгоритма обучения. Перекрестной проверки можно указать toosort метрики производительности out hello оптимальные результаты, найденные с помощью алгоритма поиска hello сетки. Используется с широкими подобных ограничение помогает лжевзаимосвязей tootraining модели данных, чтобы hello модель сохраняет hello емкость tooapply toohello общий набор данных, из которой hello обучающие данные были извлечены hyperparameter CV.

модели Hello, мы используем включают логистической и линейной регрессии, случайные леса и градиента повышенных деревьев:

* [Линейная регрессия с SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) модель линейной регрессии, которая использует метод вероятностный градиентный спуск (SGD) и для оптимизации и возможность масштабирования toopredict hello совет суммы оплаты. 
* [Логистическая Регрессия с LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) и регрессии «logit» представляет собой модель регрессии, который может использоваться при классификации данных категориальные toodo hello зависимой переменной. LBFGS-это алгоритм оптимизации реализация ньютон, соответствующий алгоритм Бройдена-Флетчера-Гольдфарба-Шанно (BFGS) hello ограниченный объем памяти компьютера с помощью и широко используемый в машинном обучении.
* [Случайные леса](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) — это совокупности деревьев принятия решений.  Они объединяют многих решений деревьев tooreduce hello риск переобучения. Случайные леса, используются для классификации и регрессии и может обрабатывать категориальных признаков и могут быть расширены параметр toohello мультиклассовой классификации. Они не требуется возможность масштабирования и являются может toocapture нелинейности и возможность взаимодействия. Случайные леса принадлежат hello наиболее успешных моделей машинного обучения для классификации и регрессии.
* [Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений. Решение GBTs обучение итеративного дерева toominimize функции потерь. GBTs используются для классификации и регрессии и может обрабатывать категориальных признаков не требуется возможность масштабирования и являются может toocapture нелинейности и возможностей взаимодействия. Кроме того, его можно использовать для создания модели мультиклассовой классификации.

Примеры использования CV и Hyperparameter моделирования Очистка отображаются для проблемы бинарной классификации hello. Более простые примеры (без параметра переходов) перечислены в разделе Основные hello по задачам регрессии. Однако в приложение hello также предоставляются проверку с помощью эластичных net для линейной регрессии и CV с параметром с помощью очистки для регрессии случайного леса. Hello **гибкому net** — метод регуляризованной регрессии линейно подгонки линейной регрессии моделей, объединяющее показателей L1 и L2 hello ответственность за hello [лассо](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) и [ребра](https://en.wikipedia.org/wiki/Tikhonov_regularization) методы.   

> [!NOTE]
> Хотя набор средств Spark MLlib hello спроектированный toowork с большими наборами данных, сравнительно небольшую выборку (с помощью 170 тысяч строк, 0,1% hello исходный набор данных NYC ~ 30 МБ) используется здесь для удобства. Упражнение Hello в данном разделе выполняется эффективно (в течение 10 минут) в кластере HDInsight с 2 рабочих узлов. Hello одинаковый код, с небольшими изменениями может быть используется tooprocess более крупных-наборов данных, с соответствующими изменениями для кэширования данных в памяти и изменение размера кластера hello.
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a>Настройка: кластеры и записные книжки Spark
Действия по настройке и код, указанные в этом пошаговом руководстве, применимы к использованию для HDInsight Spark 1.6. Но записные книжки Jupyter можно использовать для кластеров HDInsight Spark 1.6 и Spark 2.0. Описание toothem hello записных книжек и ссылки, представлено в hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) для репозитория GitHub hello, содержащий их. Кроме того код hello здесь и в записных книжках hello связаны является универсальным и должен работать на любой кластер Spark. Если вы не используете HDInsight Spark, настройку и управление ими действия hello кластера может быть немного отличается от показанной здесь. Для удобства ниже приведены hello записные книжки Jupyter ссылки toohello Spark 1.6 и toobe 2.0, выполняются в ядро pyspark hello hello server книжке Jupyter.

### <a name="spark-16-notebooks"></a>Записные книжки для Spark 1.6

[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb). Содержит разделы в записной книжке №1 и варианты моделей с использованием настройки гиперпараметров и перекрестной проверки.

### <a name="spark-20-notebooks"></a>Записные книжки для Spark 2.0

[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): этот файл содержит сведения о как tooperform Просмотр данных, моделирования и оценки в Spark 2.0 кластеров.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

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
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

**ВЫХОДНЫЕ ДАННЫЕ**

datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)

### <a name="import-libraries"></a>Импорт библиотек
Импортируйте необходимые библиотеки с hello, следующий код:

    # LOAD PYSPARK LIBRARIES
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

## <a name="data-ingestion-from-public-blob"></a>Прием данных из открытого большого двоичного объекта:
Hello первым шагом в процессе обработки и анализа данных hello является tooingest hello данных toobe анализируются из источников, где она находится в среде моделирования и просмотра данных. В нашем пошаговом руководстве — это среда Spark. Этот раздел содержит toocomplete кода hello последовательности задач:

* hello данные примера toobe моделируется приема
* чтение во входном наборе данных hello (хранятся в формате .tsv)
* Очистить hello данные и формат
* создание и кэширование объектов (устойчивых распределенных наборов данных или фреймов данных) в памяти;
* регистрация данных в качестве временной таблицы в контексте SQL.

Ниже приведен код hello для приема данных.

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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ВЫХОДНЫЕ ДАННЫЕ**

Время, затраченное tooexecute над ячейкой: 276.62 секунд

## <a name="data-exploration--visualization"></a>Исследование и визуализация данных
Hello данных была помещена в Spark, hello следующим шагом в процессе обработки и анализа данных hello после toogain глубокого понимания hello данных через Просмотр и визуализация. В этом разделе рассматриваются hello такси данные с помощью SQL-запросов построения hello целевой переменных и потенциальных возможностей для визуальной проверки. В частности мы построения hello частоту пассажира счетчиков в такси приема-передачи, частота hello совет сумм и как изменять советы по типам и сумма платежа.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Построить гистограмму для частоты счетчика пассажира в образце hello такси приема-передачи данных
Этот код и последующие фрагменты использовать образец hello magic tooquery SQL и данных локального magic tooplot hello.

* **Магическое SQL (`%%sql`)** hello ядра HDInsight PySpark поддерживает встроенные легко HiveQL запросы к hello sqlContext. Hello (-o имя_переменной) аргумент hello выходных данных запроса SQL hello сохраняется как Pandas кадр данных на сервере Jupyter hello. Это означает, что он доступен в локальном режиме hello.
* Hello  **`%%local` магическое** — использовать код toorun локально на сервере Jupyter hello, где hello головному узлу кластера HDInsight hello. Как правило, используется `%%local` magic после hello `%%sql -o` magic — используется toorun запроса. параметр -o Hello сохранится hello выходных данных запроса SQL hello локально. Здравствуйте, затем `%%local` magic триггеры hello следующего набора toorun фрагменты кода локально к выходным данным hello hello запросов SQL, в которой сохраняется в локальном компьютере. выходные данные Hello автоматически визуализируются после выполнения кода hello.

Этот запрос извлекает hello приема-передачи данных по количеству пассажира. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


Этот код создает локальный кадров данных из результатов запроса hello и представлены данные hello. Hello `%%local` magic создает локальный-кадра данных, `sqlResults`, который может использоваться для отображения на диаграмме с помощью matplotlib. 

> [!NOTE]
> В этом пошаговом руководстве волшебная команда PySpark используется несколько раз. При больших размерах hello объем данных следует образец toocreate кадра данных, помещающихся в локальной памяти.
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Вот hello кода tooplot hello приема-передачи с пассажира счетчиков

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**ВЫХОДНЫЕ ДАННЫЕ**

![Частота поездок в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

Можно выбирать различные виды визуализаций (таблицы, круговая, строки, области или панели) с помощью hello **тип** кнопок меню в записной книжке hello. Здесь показана панель построения Hello.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Построение гистограммы суммы чаевых и ее зависимости от количества пассажиров и тарифа.
Использовать toosample данных запроса SQL...

    # SQL SQUERY
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

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


**ВЫХОДНЫЕ ДАННЫЕ:** 

![Распределение суммы чаевых](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Сумма чаевых в зависимости от количества пассажиров](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Сумма чаевых в зависимости от тарифа](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Проектирование признаков, преобразование и подготовка данных к моделированию
В этом разделе описывается и предоставляет кода hello для процедур, используемых tooprepare данных для использования в модели машинного Обучения. Здесь показано, как hello toodo следующие задачи:

* Создание нового признака путем секционирования часов в ячейки трафика.
* Индексация и прямое кодирование категориальных признаков
* Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения
* Создание вложенных случайной выборки данных hello и разбейте его на обучающий и проверочный наборы
* масштабирование признаков;
* кэширование объектов в памяти.

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a>Создание нового признака путем секционирования часов трафика в ячейки.
Этот код показывает, как toocreate новую функцию с помощью секционирования трафика времени в ячейки, а затем как toocache hello результирующий кадр данных в памяти. Кэширование приводит tooimproved времени выполнения, где устойчивым распределенных наборы данных (RDDs) и кадров данных используются несколько раз. В этом пошаговом руководстве процесс кэширования существующих данных выполняется в несколько этапов.

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

**ВЫХОДНЫЕ ДАННЫЕ**

126 050.

### <a name="index-and-one-hot-encode-categorical-features"></a>Индексация и прямое кодирование категориальных признаков
В этом разделе показано, как tooindex или кодирования категориальных признаков для входных данных в моделирования функции hello. Здравствуйте, моделирования и прогнозирования функции MLlib требуют возможности с помощью категориальных данных входного быть проиндексированы или кодировке предыдущих toouse. 

В зависимости от модели hello необходима tooindex или кодировать их по-разному. Например, модели логистической и линейной регрессии требуют горячей один кодировки, где, например, в трех столбцов компонентов, с каждой содержащее 0 или 1 в зависимости от категории hello наблюдения можно развернуть компонент с три категории. Предоставляет MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) функции toodo горячей один кодировки. Этот кодировщик сопоставляет столбец метки столбца tooa индексы двоичных векторов, с максимум один значение single. Эта кодировка позволяет алгоритмы, которые ожидают числовой табличное значение функции, такие как логистической регрессии применяется toobe toocategorical функции.

Ниже приведен код tooindex hello и кодирования категориальных признаков:

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

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


**ВЫХОДНЫЕ ДАННЫЕ**

Время, затраченное tooexecute над ячейкой: 3.14 секунд

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>Создание объектов с помеченной вершиной в качестве ввода для функций машинного обучения
Этот раздел содержит код, который показывает, как тип данных категориальные text tooindex как с меткой точки данных и как tooencode его. Это подготавливает toobe используется tootrain и тестирования MLlib логистической регрессии и другие модели классификации. Объекты с помеченной вершиной отформатированы в устойчивые распределенные наборы данных, которые можно использовать в качестве входных для большинства алгоритмов машинного обучения в MLlib. Объект [с помеченной вершиной](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) — это разреженный или плотный локальный вектор, связанный с меткой или ответом.

Ниже приведен код tooindex hello и кодирования текста функции для двоичной классификации.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
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
Этот код создает случайной выборки данных hello (здесь используется 25%). Несмотря на то, что он не является обязательным для этого примера из-за размера toohello hello набора данных, мы демонстрируют, как можно произвести выборку данных hello здесь. Затем вы знаете, как toouse его собственные проблемы, при необходимости. Если выборки большие, этот процесс может значительно сэкономить время обучения моделей. Далее мы разбить образец hello в рамках обучения (здесь 75%) и тестирования toouse часть (25% здесь) в классификации и регрессии моделирования.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

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

**ВЫХОДНЫЕ ДАННЫЕ**

Время, затраченное tooexecute над ячейкой: 0.31 секунд

### <a name="feature-scaling"></a>масштабирование признаков;
Масштабирование функции, также известные как нормализация данных гарантирует, что функции широко распределенные значениями не учитывая чрезмерного весить в целевой функции hello. Hello код для функции масштабирования использует hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello функции toounit дисперсию. MLlib предоставляет функцию StandardScaler для выполнения линейной регрессии с применением метода стохастического градиента (SGD). Алгоритм SGD широко используется для обучения других моделей машинного обучения (например, регуляризованной регрессии или метода опорных векторов).   

> [!TIP]
> Обнаружено алгоритм toobe hello LinearRegressionWithSGD конфиденциальных toofeature масштабирования.   
> 
> 

Вот переменных tooscale hello кода для использования с регуляризацией hello линейный SGD алгоритм.

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

**ВЫХОДНЫЕ ДАННЫЕ**

Время, затраченное tooexecute над ячейкой: 11.67 секунд

### <a name="cache-objects-in-memory"></a>кэширование объектов в памяти.
Hello время, необходимое для обучения и проверки алгоритмов машинного Обучения можно уменьшить путем кэширования hello входные данные кадра объекты используются для классификации, регрессию и возможности масштабирования.

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

**ВЫХОДНЫЕ ДАННЫЕ** 

Время, затраченное tooexecute над ячейкой: 0,13 секунд

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Прогнозирование вероятности выплаты чаевых за поездку с помощью моделей бинарной классификации
В этом разделе показано, как использование трех моделей для задача двоичной классификации hello прогнозирования, независимо от того, имеется ли для обработки такси оплачивается совет. Hello модели представлены являются:

* Логистическая регрессия 
* Случайный лес
* Градиентный бустинг деревьев

Процесс создания модели состоит из следующих этапов: 

1. **Обучение модели** с использованием данных с одним набором параметров.
2. **Оценка модели** на основе набора тестовых данных с метриками.
3. **Сохранение модели** в большом двоичном объекте для последующего использования.

Далее показано, как toodo перекрестной проверки (CV) с параметром широкими двумя способами:

1. С помощью **универсального** задает пользовательский код, который может быть применен tooany алгоритма в параметре MLlib и tooany в алгоритме. 
2. С помощью hello **pySpark CrossValidator конвейера функция**. Обратите внимание, что CrossValidator имеет несколько ограничений для Spark 1.5.0. 
   
   * Модели конвейера не могут быть сохранены для последующей обработки.
   * Не может использоваться для каждого параметра в модели.
   * Не может использоваться для каждого алгоритма MLlib.

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a>Универсальный перекрестной проверки и hyperparameter свертки, используемые с алгоритмом логистической регрессии hello для двоичной классификации
Hello кода в этом разделе показано, как tootrain, оценки и сохранить модель логистической регрессии с [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , прогнозирует ли совет получает оплату за маршрут в наборе данных маршрута и тариф авиакомпании такси hello NYC. Hello модель обучается перекрестной проверки (CV) и свертки hyperparameter реализуется с помощью пользовательского кода, который может быть применен tooany обучающие алгоритмы в MLlib hello.   

> [!NOTE]
> Этот пользовательский код CV Hello выполнение может занять несколько минут.
> 
> 

**Обучение модели логистической регрессии hello, используя CV и hyperparameter свертки**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ВЫХОДНЫЕ ДАННЫЕ**

Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]

Intercept: -0.0111216486893

Время, затраченное tooexecute над ячейкой: 14.43 секунд

**Оценка модели двоичной классификации hello со стандартными показателями**

Hello кода в этом разделе показано, как tooevaluate логистической регрессии модели с проверочных данных, включая рисунка hello ROC кривой.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

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

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ВЫХОДНЫЕ ДАННЫЕ**

Area under PR = 0.985336538462

Area under ROC = 0.983383274312

Summary Stats

Precision = 0.984174341679

Recall = 0.984174341679

F1 Score = 0.984174341679

Время, затраченное tooexecute над ячейкой: 2,67 секунд

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

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
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


**ВЫХОДНЫЕ ДАННЫЕ**

![Кривая ROC логистической регрессии для универсального подхода](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

**Сохранение модели в большом двоичном объекте для последующего использования**

Hello кода в этом разделе показано, как модели логистической регрессии hello toosave для потребления.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


**ВЫХОДНЫЕ ДАННЫЕ**

Время, затраченное tooexecute над ячейкой: 34.57 секунд

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a>Использование функции конвейера MLlib CrossValidator с моделью LogisticRegression (эластичная регрессия)
Hello кода в этом разделе показано, как tootrain, оценки и сохранить модель логистической регрессии с [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , прогнозирует ли совет получает оплату за маршрут в наборе данных маршрута и тариф авиакомпании такси hello NYC. Hello модель обучается перекрестной проверки (CV) и hyperparameter свертки реализованы с hello функция MLlib CrossValidator конвейера для CV с очистку параметров.   

> [!NOTE]
> Hello выполнение этого кода MLlib CV может занять несколько минут.
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**ВЫХОДНЫЕ ДАННЫЕ**

Время, затраченное tooexecute над ячейкой: 107.98 секунд

**Отобразите hello ROC кривой.**

Hello *predictionAndLabelsDF* регистрируется как таблица, *tmp_results*, в предыдущую ячейку hello. *tmp_results* можно использовать toodo запросов и выводить результаты в hello sqlResults-кадра данных для отображения на диаграмме. Ниже приведен код hello.

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

Вот hello кода tooplot hello ROC кривой.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
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


**ВЫХОДНЫЕ ДАННЫЕ**

![Кривая ROC логистической регрессии с использованием MLlib CrossValidator](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a>Классификация случайного леса
Hello кода в этом разделе показано, как tootrain, оценки и сохранить регрессии случайного леса, которая прогнозирует, оплачивается ли подсказка для обработки в hello NYC такси маршрута и тариф авиакомпании набора данных.

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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


**ВЫХОДНЫЕ ДАННЫЕ**

Area under ROC = 0.985336538462

Время, затраченное tooexecute над ячейкой: 26.72 секунд

### <a name="gradient-boosting-trees-classification"></a>Классификация с применением модели градиентного бустинга деревьев
Hello кода в этом разделе описывается, как tootrain, оценки и сохранить градиента подъема дерева модели, которая прогнозирует, оплачивается ли подсказка для обработки в hello NYC такси маршрута и тариф авиакомпании набора данных.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
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

**ВЫХОДНЫЕ ДАННЫЕ**

Area under ROC = 0.985336538462

Время, затраченное tooexecute над ячейкой: 28.13 секунд

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a>Прогнозирование суммы чаевых с помощью моделей регрессии (без использования перекрестной проверки)
В этом разделе показано, как использование трех моделей для регрессии задачу hello: прогнозирования hello совет оплаты такси поездки, на основе других функций подсказки. Hello модели представлены являются:

* регуляризованная линейная регрессия;
* случайный лес;
* градиентный бустинг деревьев.

Эти модели был описан в введение hello. Процесс создания модели состоит из следующих этапов: 

1. **Обучение модели** с использованием данных с одним набором параметров.
2. **Оценка модели** на основе набора тестовых данных с метриками.
3. **Сохранение модели** в большом двоичном объекте для последующего использования.   

> AZURE Примечание: Перекрестная проверка не используется с hello три модели регрессии в этом разделе, так как это было показано в подробные данные для модели логистической регрессии hello. Пример, показывающий, как toouse CV со эластичной Net для линейной регрессии предоставляется в hello приложение этого раздела.
> 
> AZURE Примечание: Наш опыт показывает, могут возникать проблемы с последующим согласованием LinearRegressionWithSGD моделей и параметры должны toobe изменен или оптимизированное тщательно для получения модели. Проблему конвергенции можно решить, выполнив масштабирование переменных. Эластичный net регрессии, как показано в разделе toothis приложение hello, можно также использовать вместо LinearRegressionWithSGD.
> 
> 

### <a name="linear-regression-with-sgd"></a>Линейная регрессия с применением SGD
Hello кода в этом разделе показано, как toouse масштабировать tootrain функции линейной регрессии, который использует вероятностный градиентный спуск (SGD) для оптимизации, и как tooscore, оценки и сохранить модель hello в хранилище больших двоичных объектов Azure (WASB).

> [!TIP]
> Наш опыт показывает могут возникать проблемы с последующим согласованием hello LinearRegressionWithSGD моделей и параметры должны toobe изменен или оптимизированное тщательно для получения модели. Проблему конвергенции можно решить, выполнив масштабирование переменных.
> 
> 

    # LINEAR REGRESSION WITH SGD 

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

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ВЫХОДНЫЕ ДАННЫЕ**

Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]

Intercept: 0.854507624459

RMSE = 1.23485131376

R-sqr = 0.597963951127

Время, затраченное tooexecute над ячейкой: 38.62 секунд

### <a name="random-forest-regression"></a>Регрессия с использованием модели случайного леса
Hello кода в этом разделе показано, как tootrain, оценки и сохранить случайного леса модель, прогнозирующая объем подсказки для hello NYC такси обработки данных.   

> [!NOTE]
> В приложение hello предоставляется перекрестной проверки с параметром широкими с использованием пользовательского кода.
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

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

**ВЫХОДНЫЕ ДАННЫЕ**

RMSE = 0.931981967875

R-sqr = 0.733445485802

Время, затраченное tooexecute над ячейкой: 25.98 секунд

### <a name="gradient-boosting-trees-regression"></a>Регрессия с применением градиентного бустинга деревьев
Hello кода в этом разделе описывается, как tootrain, оценки и сохранить градиента повышения деревьев модель, прогнозирующая объем подсказки для hello NYC такси обработки данных.

**Обучение и анализ**

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ВЫХОДНЫЕ ДАННЫЕ**

RMSE = 0.928172197114

R-sqr = 0.732680354389

Время, затраченное tooexecute над ячейкой: 20.9 секунд

**Графическое представления**

*tmp_results* регистрируется как таблицу Hive в предыдущую ячейку hello. Результаты из таблицы hello выводятся в hello *sqlResults* кадра данных для отображения на диаграмме. Ниже приведен код hello

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Вот hello tooplot кода hello данных с помощью сервера Jupyter hello.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a>Приложение. Дополнительные задачи регрессии с использованием перекрестной проверки с перебором параметров
Это приложение содержит код отображение как CV toodo с помощью эластичных net для линейной регрессии и как CV toodo с параметром Очистка регрессии случайного леса с помощью пользовательского кода.

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a>Перекрестная проверка с использованием эластичной сети для линейной регрессии
Hello кода в этом разделе показано, как toodo перекрестная проверка, с помощью net гибкому для линейной регрессии и как tooevaluate hello модели с тестовыми данными.

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ВЫХОДНЫЕ ДАННЫЕ**

Время, затраченное tooexecute над ячейкой: 161.21 секунд

**Оценка с помощью метрики R SQR**

*tmp_results* регистрируется как таблицу Hive в предыдущую ячейку hello. Результаты из таблицы hello выводятся в hello *sqlResults* кадра данных для отображения на диаграмме. Ниже приведен код hello

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


Ниже приведен код hello toocalculate R sqr.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


**ВЫХОДНЫЕ ДАННЫЕ**

R-sqr = 0.619184907088

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a>Перекрестная проверка с перебором параметров с использованием пользовательского кода для регрессии случайного леса
Hello кода в этом разделе показано, как toodo перекрестная проверка с помощью очистки параметров с помощью пользовательского кода для регрессии случайного леса и как tooevaluate hello модели с тестовыми данными.

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ВЫХОДНЫЕ ДАННЫЕ**

RMSE = 0.906972198262

R-sqr = 0.740751197012

Время, затраченное tooexecute над ячейкой: 69.17 секунд

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a>Очистка объектов из памяти и вывод расположений моделей
Используйте `unpersist()` toodelete объектов в кэше в памяти.

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

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


**ВЫХОДНЫЕ ДАННЫЕ**

PythonRDD[122] at RDD at PythonRDD.scala: 43

** Распечатки путь toomodel файлов toobe используется в записной книжке потребления hello. ** tooconsume и оценка независимой-набор данных, нужно toocopy и вставьте эти имена файлов в hello «Потребления ноутбук».

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**ВЫХОДНЫЕ ДАННЫЕ**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"

## <a name="whats-next"></a>Что дальше?
Теперь после создания модели регрессии и классификации с hello Spark MlLib, готовы toolearn, как tooscore и оценивать эти модели.

**Модели потребления:** toolearn как tooscore и оценить hello классификационных и регрессионных моделей, созданных в этом разделе см. в разделе [оценка и оценки моделей построен Spark машинного обучения](machine-learning-data-science-spark-model-consumption.md).

