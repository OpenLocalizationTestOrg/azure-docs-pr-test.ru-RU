---
title: "aaaData обработки и анализа с помощью Scala и Spark на Azure | Документы Microsoft"
description: "Как toouse Scala для защищенных машинного обучения задач с помощью hello Spark масштабируемой MLlib Spark ML пакеты и на кластере Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a>Обработка и анализ данных с использованием Scala и Spark в Azure
В этой статье показано, как пакеты toouse Scala для задач защищенных машинного обучения с hello масштабируемой MLlib Spark и Spark ML на кластере Azure HDInsight Spark. Он поможет выполнить задачи hello, составляющих hello [процесса обработки и анализа данных](http://aka.ms/datascienceprocess): приема данных и просмотра, визуализации, конструируются, моделирования и модели использования. модели Hello в статье hello включают логистической и линейной регрессии, случайные леса и градиент повышенных деревьев (GBTs), кроме общих tootwo защищено задач машинного обучения:

* Проблемы регрессии: прогноз суммы совет hello ($) для обработки такси
* двоичная классификация: прогнозирование вероятности оплаты чаевых (1 или 0) за поездку в такси.

процесс моделирования Hello требует обучения и оценки проверочного набора данных и показатели точности применимо. В этой статье рассказывается, как toostore этих моделей в хранилище больших двоичных объектов Azure и как tooscore и оценить их прогнозирования производительности. В этой статье также описывается hello дополнительные разделы, как toooptimize модели с помощью свертки перекрестной проверки и hyper параметра. Hello данные, используемые приводится образец hello 2013 NYC такси маршрута и тариф авиакомпании набора данных на сайте GitHub.

[Scala](http://www.scala-lang.org/), язык, основанный на виртуальной машине Java hello интегрирует концепции объектно ориентированного и функциональный язык. Это масштабируемая язык, хорошо подходит toodistributed обработки в облаке hello и выполняется в кластерах Azure Spark.

[Spark](http://spark.apache.org/) платформу параллельной обработки открытым исходным кодом, поддерживающий в памяти обрабатывает tooboost hello производительность больших данных аналитики приложений. Подсистема обработки Spark Hello, созданную для скорости, простоте использования и сложные analytics. Возможности распределенного вычисления в памяти Spark отлично подходят для итеративных алгоритмов в машинном обучении и графовых вычислениях. Hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) пакет предоставляет единый набор API высокого уровня, построена на базе данных кадры, которые помогут вам создать и настроить практические машинного обучения конвейеров. [MLlib](http://spark.apache.org/mllib/) — библиотека Spark в масштабируемой машинного обучения, который переводит возможностей моделирования toothis распределенной среде.

[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) — предложение размещенной в Azure hello Spark с открытым исходным кодом. Она также включает поддержку записные книжки Jupyter Scala на кластере Spark hello и может выполнения интерактивных запросов tootransform Spark SQL, фильтрации и отображения данных, хранящихся в хранилище больших двоичных объектов Azure. Hello Scala фрагменты кода в этой статье, предоставляющие решения hello и отображения графики соответствующие hello toovisualize hello данных выполняются в записные книжки Jupyter установлен в кластерах Spark hello. шаги моделирования Hello в этих разделах имеется код, показано, как tootrain, вычисления, сохранения и использовать каждый вводе модели.

шаги настройки Hello и кода в этой статье предназначены для Azure HDInsight 3.4 Spark 1.6. Однако hello кода в этой статье и в hello [книжке Jupyter Scala](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) , являются универсальными и должен работать на любой кластер Spark. Здравствуйте, настройка кластера и управления действия может быть немного отличается от элементы, отображаемые в этой статье, если вы не используете HDInsight Spark.

> [!NOTE]
> Разделе показано, как Python, а не Scala toocomplete toouse задач для начала до конца процесса обработки и анализа данных. в разделе [обработки и анализа данных с помощью Spark на Azure HDInsight](machine-learning-data-science-spark-overview.md).
> 
> 

## <a name="prerequisites"></a>Предварительные требования
* У вас должна быть подписка Azure. Если у вас ее нет, [получите бесплатную пробную версию Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Вы должны hello toocomplete кластера Azure HDInsight 3.4 Spark 1.6 следующих процедур. toocreate кластера, см. инструкции hello в [приступить к работе: создание Apache Spark на Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Задайте тип кластера hello и версии в hello **Выбор типа кластера** меню.

![Настройка типа кластера HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

Описание hello NYC такси обработки данных и инструкции о том, как код tooexecute из записной книжке Jupyter на кластере Spark hello, см. соответствующие разделы hello в [Обзор для обработки и анализа данных с помощью Spark на Azure HDInsight](machine-learning-data-science-spark-overview.md).  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Выполнение кода Scala записной книжке Jupyter на кластере Spark hello
Вы можете запустить записной книжке Jupyter из hello портал Azure. Найдите кластер Spark приветствия на информационной панели, затем щелкните страницу управления hello tooenter для кластера. Далее щелкните **панели мониторинга кластера**и нажмите кнопку **книжке Jupyter** tooopen hello ноутбук, связанные с кластера Spark hello.

![Панель мониторинга кластера и записные книжки Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

Записные книжки Jupyter также можно просмотреть по адресу https://&lt;clustername&gt;.azurehdinsight.net/jupyter. Замените *clustername* с hello имя кластера. Вам необходим пароль hello вашего администратора учетной записи tooaccess hello Jupyter портативных компьютеров.

![Go tooJupyter портативные компьютеры с помощью имени кластера hello](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

Выберите **Scala** toosee каталога, который содержит несколько примеров предварительно пакетированных записных книжек, используйте hello PySpark API. Здравствуйте моделирования исследования и счет с помощью Scala.ipynb ноутбук, содержащий hello образцы кода для этого набора разделов Spark доступен на [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).

Можно передать записной книжки hello непосредственно из GitHub toohello книжке Jupyter сервера на кластере Spark. На домашней странице Jupyter, нажмите кнопку hello **отправить** кнопки. В проводнике hello, вставьте URL-адрес GitHub (необработанное содержимое) hello портативного компьютера Scala hello и нажмите кнопку **откройте**. ноутбук Scala Hello доступна на hello URL-адреса:

[Exploration-Modeling-and-Scoring-using-Scala.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a>Настройка: предустановленные контексты Spark и Hive, а также магические команды и библиотеки Spark
### <a name="preset-spark-and-hive-contexts"></a>Предустановленные контексты Spark и Hive
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


Hello Spark ядер, предоставляемых с записные книжки Jupyter имеют предустановленных контекстов. Не нужно tooexplicitly набор hello Spark или куст контекстов перед началом работы с приложением hello, которое вы разрабатываете. Hello предустановленную контексты — это:

* `sc` — для контекста Spark;
* `sqlContext` — для контекста Hive.

### <a name="spark-magics"></a>Волшебные команды Spark
Hello ядра Spark предоставляет некоторые предопределенные «magics», которые являются специальные команды, которые можно вызвать с `%%`. Два из этих команд используются следующие примеры кода hello.

* `%%local`Указывает, что кода hello в последующих строках выполняется локально. Hello код должен быть допустимым кодом Scala.
* `%%sql -o <variable name>` выполняет запрос Hive к `sqlContext`. Если hello `-o` передается параметр, результат hello hello запроса сохраняется в hello `%%local` Scala контекста в виде блока данных Spark.

Для Дополнительные сведения о ядрах hello записные книжки Jupyter и их стандартных «magics», можно вызвать с `%%` (например, `%%local`), в разделе [кластеров ядер, доступных для записные книжки Jupyter с HDInsight Spark Linux HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

### <a name="import-libraries"></a>Импорт библиотек
Импорт hello Spark, MLlib и другие библиотеки вам с помощью hello, следующий код.

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a>Прием данных
Первым этапом Hello hello процесса обработки и анализа данных является tooingest hello данных, что tooanalyze. Переносе hello данных из внешних источников или системами его местоположение в среде моделирования и просмотра данных. В этой статье вы приема данных hello, соединенных 0,1% пример hello такси маршрута и тариф авиакомпании (хранятся в формате .tsv). среда моделирования и просмотра данных Hello — Spark. Этот раздел содержит hello toocomplete кода hello, следующая последовательность задач:

1. Установка пути к каталогам для хранения данных и моделей.
2. Чтение в hello (хранятся в формате .tsv) входного набора данных.
3. Определение схемы для hello и очистить hello данными.
4. Создание очищенного кадра данных и его кэширование в памяти.
5. Зарегистрируйте hello данных как временные таблицы в SQLContext.
6. Запросы к таблице hello и Импорт результатов hello в кадре данных.

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a>Настройка путей каталога к местам хранения в хранилище BLOB-объектов Azure
Spark может считывать и записывать tooAzure хранилища больших двоичных объектов. Используйте Spark tooprocess любой из существующих данных и сохраните результаты hello снова в хранилище больших двоичных объектов.

toosave модели или файлов в хранилище больших двоичных объектов, необходимо tooproperly укажите путь hello. Контейнер по умолчанию hello ссылку присоединенного кластера Spark toohello, используя путь, который начинается с `wasb:///`. Другие расположения указываются с помощью `wasb://`.

Hello следующий код задает hello место чтения toobe входных данных hello и hello путь tooBlob хранилища, кластер Spark вложенного toohello сохранения модели hello.

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a>Импорт данных, создать RDD определить toohello схемы в соответствии с кадра данных.
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Выходные данные:**

Время toorun hello ячейки: 8 секунд.

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a>Запросы к таблице hello и Импорт результатов в кадре данных.
Далее таблица hello запроса тариф авиакомпании, пассажира и подсказки данных. Фильтрация данных поврежден и малые; и напечатайте несколько строк.

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

**Выходные данные:**

| fare_amount | passenger_count | tip_amount | tipped |
| --- | --- | --- | --- |
|        13,5 |1.0 |2,9 |1.0 |
|        16,0 |2,0 |3.4 |1.0 |
|        10,5 |2,0 |1.0 |1.0 |

## <a name="data-exploration-and-visualization"></a>Исследование и визуализация данных
После переноса данных hello в Spark, следующим шагом hello в hello процесса обработки и анализа данных является toogain более глубокое представление о данных hello через Просмотр и визуализация. В этом разделе вы проверяете hello такси данных с помощью SQL-запросов. Затем результаты импорта hello в кадр данных tooplot hello целевыми переменными и потенциального функций для визуальной проверки с помощью функции автоматического визуализации hello Jupyter.

### <a name="use-local-and-sql-magic-tooplot-data"></a>Использование локальных и magic tooplot данных SQL
По умолчанию выходные данные hello фрагмента кода, запускаемого из записной книжке Jupyter доступна в контексте hello hello сеанса, в которой сохраняется на hello рабочих узлов. Если требуется toosave trip toohello рабочих узлов для каждого вычисления, и если все hello данных, необходимых для вашей вычисление доступен локально на узел сервера Jupyter hello (который hello головного узла), можно использовать hello `%%local` магическая toorun кода hello фрагмент кода на сервере Jupyter hello.

* **Волшебная команда SQL** (`%%sql`). Hello ядра HDInsight Spark поддерживает запросы HiveQL легко встроенного к SQLContext. Hello (`-o VARIABLE_NAME`) аргумент hello выходных данных запроса SQL hello сохраняется как Pandas кадр данных на сервере Jupyter hello. Это означает, что она доступна в локальном режиме hello.
* `%%local` **Волшебная команда**. Hello `%%local` magic работает кода hello локально на сервере Jupyter hello, где hello головного узла кластера HDInsight hello. Как правило, используется `%%local` magic вместе с hello `%%sql` magic с hello `-o` параметра. Hello `-o` параметр сохранится hello выходных данных запроса SQL hello локально, а затем `%%local` magic приведет к запуску hello следующего набора toorun фрагмент кода локально к выходным данным hello hello запросов SQL, в которой сохраняется локально.

### <a name="query-hello-data-by-using-sql"></a>Запрос hello данных с помощью SQL
Этот запрос извлекает hello такси приема-передачи, сумма тариф авиакомпании, пассажира количество и сумма подсказки.

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

В следующих кода hello, hello `%%local` magic создает кадр локальных данных sqlResults. Можно использовать sqlResults tooplot с помощью matplotlib.

> [!TIP]
> В этой статье магическая команда local используется несколько раз. Если набор данных имеет большой размер, проверьте образец toocreate кадра данных, помещающихся в локальной памяти.
> 
> 

### <a name="plot-hello-data"></a>Отобразить данные hello
Вы можете отобразить с помощью кода Python в локальном контексте виде блока данных Pandas после hello кадра данных.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 Hello Spark ядра автоматически визуализирует hello вывод запросов SQL (HiveQL) после выполнения кода hello. Вы можете выбрать тип визуализации среди нескольких типов:

* Таблица
* круговая диаграмма;
* график;
* Область
* линейчатая диаграмма.

Вот tooplot hello hello код данных:

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


**Выходные данные:**

![Гистограмма суммы чаевых](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Сумма чаевых в зависимости от количества пассажиров](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Сумма чаевых в зависимости от тарифа](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a>Создание и преобразование признаков, а также последующая подготовка данных для ввода в функции моделирования
Для функций на основе дерева моделирования из Spark ML и MLlib имеется целевой tooprepare и компонентов с помощью различных методов, таких как группирование, индексирование, горячей один кодировки и векторизации. Ниже приведены процедуры toofollow hello в этом разделе.

1. Создание нового признака путем **группирования** часов в периоды трафика.
2. Применить **индексирования и один горячей кодировки** toocategorical функции.
3. **Выборка и разбиение hello набора данных** в обучающий и проверочный дробей.
4. **Указание переменной обучения и признаков**, а затем создание индексированных или прямо закодированных обучающих и проверочных устойчивых распределенных наборов данных (RDD) или входящих кадров данных с помеченной вершиной.
5. Автоматически **классификации и Векторизация функций и целевые объекты** toouse в качестве входных данных для моделей машинного обучения.

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Создание нового признака путем группирования часов в периоды трафика
Этот код показывает, как toocreate новая функция путем сегментирования часов в момент трафик контейнеров и как toocache hello результирующий кадр данных в памяти. При повторном использовании кадры RDDs и данные кэширование приводит tooimproved времени выполнения. Соответственно будет кэшировать кадры RDDs и данные на нескольких этапах hello следующих процедур.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a>Индексирование и прямое кодирование категориальных признаков
Здравствуйте моделирования и предполагаете, что функции MLlib требуют возможности с помощью toobe категориальных данных входного индексированных или кодировке предыдущих toouse. В этом разделе показано, как tooindex или кодирования категориальных признаков для входных данных в моделирования функции hello.

Необходима tooindex или кодирования модели по-разному в зависимости от модели hello. Например, для моделей логистической и линейной регрессии требуется прямое кодирование. Скажем, признак с тремя категориями можно представить в виде трех столбцов признаков. Каждый столбец будет содержать 0 или 1 в зависимости от категории hello наблюдения. MLlib предоставляет hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) функция горячей один кодирования. Этот кодировщик сопоставляет столбец метки столбца tooa индексы двоичных векторов с не более одного значение single. С этой кодировкой алгоритмы, которые ожидают числовой табличное значение функции, такие как логистической регрессии может быть применен toocategorical функции.

Здесь можно преобразовать только четыре переменных tooshow примеры, которые являются символьные строки. Вы также можете индексировать другие переменные, такие как день недели, представленные числовыми значениями, в качестве категориальных переменных.

Для индексирования используйте функцию `StringIndexer()`, а для прямого кодирования — `OneHotEncoder()` из MLlib. Ниже приведен код tooindex hello и кодирования категориальных признаков:

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Выходные данные:**

Время toorun hello ячейки: 4 секунды.

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a>Выборка и разбиение hello набора данных на обучающие и проверочные дроби
Этот код создает случайной выборки данных hello (25%, в этом примере). Несмотря на то, что выборка не является обязательным для этого примера из-за toohello размер набора данных hello, hello статье показано, как можно произвести выборку, чтобы знать, как toouse его для собственных задач, если это требуется. Если выборки большие, этот процесс может значительно сэкономить время обучения моделей. Затем разделить образец hello в рамках обучения (75%, в этом примере) и проверочные часть toouse (25%, в этом примере) в классификации и регрессии моделирования.

Добавьте строку tooeach случайное число (от 0 до 1) (в столбце «rand»), может быть используется tooselect свертки перекрестной проверки во время обучения.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Выходные данные:**

Время toorun hello ячейки: 2 секунды.

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a>Указание переменной обучения и признаков, а также последующее создание индексированных или прямо закодированных обучающих и проверочных RDD или входящих кадров данных с помеченной вершиной
Этот раздел содержит код, который будет показано, как tooindex категориальные текстовых данных, помеченных как выберите тип данных, а его кодирования, поэтому можно использовать алгоритм логистической регрессии MLlib tootrain и тестирования и другие модели классификации. Объекты с помеченной вершиной отформатированы в RDD, которые можно использовать в качестве входных данных для большинства алгоритмов машинного обучения в MLlib. Объект [с помеченной вершиной](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) — это разреженный или плотный локальный вектор, связанный с меткой или ответом.

В этом коде hello целевой (зависимого) переменной и указываются моделей tootrain toouse функции hello. Затем вы создаете индексированные или прямо закодированные обучающие и проверочные RDD или входящие кадры данных с помеченной вершиной.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Выходные данные:**

Время toorun hello ячейки: 4 секунды.

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a>Автоматически классификации и Векторизация toouse функции и целевых объектов в качестве входных данных для моделей машинного обучения
Используйте Spark ML toocategorize hello целевой объект и компоненты toouse функций на основе дерева моделирования. Код Hello выполняет две задачи:

* Создает двоичный целевым объектом для классификации, присвоив значение 0 или 1 tooeach точки данных, от 0 до 1 с помощью пороговое значение 0,5.
* Автоматически категоризирует признаки. Если количество различных числовых значений для любого компонента, hello меньше 32, категория эту функцию.

Ниже приведен код hello для этих двух задач.

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a>Модель двоичной классификации: прогнозирование вероятности выплаты чаевых за поездку
В этом разделе создайте три типа ли должно быть уделено совет toopredict модели двоичной классификации:

* Объект **модель логистической регрессии** с помощью hello Spark ML `LogisticRegression()` функции
* Объект **модель классификации случайного леса** с помощью hello Spark ML `RandomForestClassifier()` функции
* Объект **градиента подъема дерева модели классификации** с помощью hello MLlib `GradientBoostedTrees()` функции

### <a name="create-a-logistic-regression-model"></a>Создание модели логистической регрессии
Создайте модель логистической регрессии с помощью hello Spark ML `LogisticRegression()` функции. Здесь создается модель hello, построение кода в последовательность шагов:

1. **Обучение модели hello** данных с одним набором параметров.
2. **Рассмотрение модели hello** на проверочного набора данных с метриками.
3. **Сохранить модель hello** в хранилище больших двоичных объектов для последующей обработки.
4. **Модель оценки hello** для тестовых данных.
5. **Отобразить результаты hello** с получателем операционной кривых характеристика (ROC).

Ниже приведен код hello для этих процедур.

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

Загрузки, оценки и сохранить результаты hello.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


**Выходные данные:**

ROC для тестовых данных — 0,9827381497557599.

На локальном кривой ROC hello tooplot Pandas данных кадров с помощью Python.

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
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


**Выходные данные:**

![Кривая ROC вероятности выплаты чаевых](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a>Создание модели классификации случайного леса
Создайте модель классификации случайного леса с помощью hello Spark ML `RandomForestClassifier()` функции, а затем проверять hello модели к тестовым данным.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


**Выходные данные:**

ROC для тестовых данных — 0,9847103571552683.

### <a name="create-a-gbt-classification-model"></a>Создание модели классификации по методу деревьев с градиентным повышением
Создайте модель классификации GBT с помощью элемента MLlib `GradientBoostedTrees()` функции, а затем проверять hello модели к тестовым данным.

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


**Выходные данные:**

площадь под ROC — 0,9846895479241554.

## <a name="regression-model-predict-tip-amount"></a>Модель регрессии: прогнозирование суммы чаевых
В этом разделе создайте два вида сумму чаевых hello toopredict моделей регрессии:

* Объект **модели линейной регрессии, регуляризованной** с помощью hello Spark ML `LinearRegression()` функции. Можно сохранить модель hello и рассмотрение hello модели к тестовым данным.
* Объект **повышение приоритета градиента модель дерева регрессии** с помощью hello Spark ML `GBTRegressor()` функции.

### <a name="create-a-regularized-linear-regression-model"></a>Создание регуляризованной линейной регрессии
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Выходные данные:**

Время toorun hello ячейки: 13 секунд.

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


**Выходные данные:**

R-sqr для тестовых данных — 0,5960320470835743.

Далее запрос hello результатов тестов как кадра данных и AutoVizWidget и matplotlib toovisualize его.

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

Код Hello создается фрейм локальных данных из результатов запроса hello и представлены данные hello. Hello `%%local` magic создает кадр локальных данных `sqlResults`, который можно использовать с matplotlib tooplot.

> [!NOTE]
> В этой статье данная магическая команда Spark используется несколько раз. При больших размерах hello объем данных следует образец toocreate кадра данных, помещающихся в локальной памяти.
> 
> 

Создайте график с помощью "matplotlib" Python.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

**Выходные данные:**

![Сумма чаевых: соотношение фактической и прогнозируемой суммы](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a>Создание модели регрессии GBT
Создать модель регрессии GBT с помощью hello Spark ML `GBTRegressor()` функции, а затем проверять hello модели к тестовым данным.

[Деревья с градиентным бустингом](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) — это совокупности деревьев принятия решений. Решение GBTs обучение итеративного дерева toominimize функции потерь. Деревья с градиентным повышением можно использовать для моделей регрессии и классификации. С их помощью можно обрабатывать категориальные признаки, а также определять нелинейные зависимости и взаимодействия признаков. Этот метод не требует масштабирования признаков. Кроме того, их можно использовать для создания модели мультиклассовой классификации.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


**Выходные данные:**

Test R-sqr — 0,7655383534596654.

## <a name="advanced-modeling-utilities-for-optimization"></a>Служебные программы расширенного моделирования для оптимизации
В этом разделе используются служебные программы машинного обучения, которые часто применяют для оптимизации моделей. В частности, есть три разных способа оптимизации моделей машинного обучения с использованием перебора параметров и перекрестной проверки.

* Разбиение данных hello на обучение и проверка наборов, оптимизация hello модели с помощью свертки hyper параметров на основе набора и вычисления в проверочном наборе (Линейная регрессия)
* Оптимизация hello модели с помощью перекрестной проверки и hyper-очистки параметров с помощью функции CrossValidator Spark ML (двоичная классификация)
* Оптимизация hello модели с помощью пользовательского кода перекрестной проверки и выполнить очистку параметров toouse любой машинного обучения набор функций и параметров (Линейная регрессия)

**Перекрестная проверка** — это метод, который оценивает, насколько хорошо модель, обученную на известный набор данных будет generalize функции hello toopredict наборов данных, на которых он еще не прошла обучение. Hello общие идея этот способ является обучения модели на основе набора данных, известных данных, которое затем hello точности прогнозов его проверяется на основе независимый набор данных. Типичная реализация — toodivide набора данных в *k*-свертывает, а затем обучения модели hello в циклического перебора всех, кроме одного сверток hello.

**Hyper параметр оптимизации** проблема hello выбрать набор параметров hyper-для алгоритма обучения, обычно с целью hello оптимизация показателем производительности hello алгоритм на независимый набор данных. Hyper параметр является значением, которое необходимо указать вне процедуры обучения модели hello. Предположения о значениях hyper параметров может повлиять на hello гибкость и точность модели hello. Деревья принятия решений имеют hyper параметры, например, такие как hello требуемого глубины и количества листьев в дереве hello. Для метода опорных векторов (SVM) необходимо задать условие штрафа за неправильную классификацию.

Обычно hyper параметр для оптимизации tooperform способом является toouse поиска сетки, также называемый **очистки параметров**. В поиске сетки тщательный поиск выполняется по значениям hello определенному подмножеству hello пространства hyper параметр для алгоритма обучения. Перекрестная проверка может предоставить toosort метрики производительности out hello оптимальные результаты, найденные с помощью алгоритма поиска hello сетки. При использовании свертки перекрестной проверки hyper параметров, может помочь предел подобных лжевзаимосвязей tootraining модели данных. В этом случае модель hello сохраняет hello емкость tooapply toohello общий набор данных, из которой hello обучающие данные были извлечены.

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a>Оптимизация модели линейной регрессии с помощью перебора гиперпараметров
Затем разбиение данных на обучение и проверка наборов, используйте hyper-очистки параметров в обучении модели hello toooptimize задано и оценки в проверочном наборе (Линейная регрессия).

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


**Выходные данные:**

Test R-sqr — 0,6226484708501209

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a>Оптимизировать hello модель двоичной классификации с помощью свертки перекрестной проверки и hyper параметр
В этом разделе показано, как моделировать toooptimize двоичной классификации с использованием свертки перекрестной проверки и hyper параметр. В этом случае используется hello Spark ML `CrossValidator` функции.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Выходные данные:**

Время toorun hello ячейки: 33 секунды.

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a>Оптимизация модели линейной регрессии hello с помощью пользовательского кода перекрестной проверки и выполнить очистку параметров
Затем оптимизация hello модели с помощью пользовательского кода и определить hello оптимальных параметров модели с помощью hello критерию высокой степени точности. Затем создайте окончательной модели hello, оценивать hello модели к тестовым данным и сохранить модель hello в хранилище больших двоичных объектов. Наконец загрузить модель hello оценки тестовые данные и оценить точность.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


**Выходные данные:**

Время toorun hello ячейки: 61 секунд.

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a>Автоматическое использование моделей машинного обучения на основе Spark с кодом Scala
Обзор разделы с пошаговыми руководствами hello задачами, которые составляют hello процесса обработки и анализа данных в Azure см. в разделе [процесс обработки и анализа данных для команды](http://aka.ms/datascienceprocess).

[Пошаговые руководства по процессу для обработки и анализа данных командного](data-science-process-walkthroughs.md) описывает другие руководства начала до конца, демонстрирующие hello шагов в hello командного процесса обработки и анализа данных для конкретных сценариев. Пошаговые руководства Hello также показывают, как облачные toocombine и локальных средств и служб в рабочий процесс или конвейера toocreate интеллектуальной приложения.

[Оценка построения Spark машинного обучения моделей](machine-learning-data-science-spark-model-consumption.md) показано, как код tooautomatically toouse Scala загрузки и оценки новых наборов данных с помощью машинного обучения моделей встроенные Spark и в хранилище больших двоичных объектов Azure. Следуйте приведенным инструкциям hello наличие и просто заменить hello кода Python Scala кода в этой статье для автоматических потребления.

