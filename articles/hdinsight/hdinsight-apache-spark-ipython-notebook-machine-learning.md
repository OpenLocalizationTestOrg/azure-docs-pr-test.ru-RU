---
title: "aaaBuild Apache Spark машинного самообучения, приложений на Azure HDInsight | Документы Microsoft"
description: "Пошаговые инструкции по как toobuild Apache Spark машинного самообучения, приложения на HDInsight Spark кластеры, использующие книжке Jupyter"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>Создание приложений машинного обучения Apache Spark в Azure HDInsight

Узнайте, как toobuild приложения Apache Spark машины обучения с помощью Spark кластера на HDInsight. В этой статье описывается, как toouse hello книжке Jupyter, доступные с toobuild кластера hello и проверки приложения. Hello приложение использует данные HVAC.csv образец hello, которая доступна во всех кластерах по умолчанию.

**Предварительные требования:**

Необходимо иметь следующие hello.

* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="data"></a>Понимать hello набора данных
Прежде чем начать создание приложения hello, сообщите нам понять структуру hello hello данных, для которого строится приложение hello и hello тип анализа, который мы выполним hello данных. 

В этой статье мы используем образец hello **HVAC.csv** файла данных, доступные в учетной записи хранилища Azure, связанных с кластером HDInsight hello hello. В учетной записи хранилища hello, находится в файле hello **\HdiSamples\HdiSamples\SensorSampleData\hvac**. Загрузите и откройте tooget файл CSV hello hello данные моментального снимка.  

![Моментальный снимок данных, используемых для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Моментальный снимок данных, используемых для примера машинного обучения Spark")

Hello данных показаны температуры целевой hello и hello фактическое температуры здания, имеющий Кондиционирования систем. Предположим, что hello **системы** столбец представляет системный идентификатор hello и hello **SystemAge** столбец представляет hello число лет, система Кондиционирования hello находилось в месте на построение hello.

Мы используем этот toopredict данных здания будут ли еще важнее или colder основываться на целевой температура hello, заданного системой идентификатор и возраст системы.

## <a name="app"></a>Создание приложения машинного обучения Spark с помощью Spark MLlib
В этом приложении мы используем tooperform конвейера Spark ML классификация документов. Конвейера hello мы разбивается на слова hello документа, преобразовать в числовой компонент вектор слова hello и наконец создать модель прогнозирования hello векторов признаков и меток. Выполните следующие шаги toocreate hello приложения hello.

1. Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели). Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.   
2. Из колонки кластера Spark hello, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **книжке Jupyter**. При появлении запроса введите учетные данные администратора hello hello кластера.
   
   > [!NOTE]
   > Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. Создайте новую записную книжку. Щелкните **Создать**, а затем выберите **PySpark**.
   
    ![Создание записной книжки Jupyter для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Создание записной книжки Jupyter для примера машинного обучения Spark")
4. Создается и открывается с именем hello Untitled.pynb новый блокнот. Щелкните имя записной книжки hello вверху hello и введите понятное имя.
   
    ![Указание имени записной книжки для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Указание имени записной книжки для примера машинного обучения Spark")
5. Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом. контексты Spark и Hive Hello автоматически создается автоматически при выполнении первой ячейке кода hello. Можно запустить, импортировав hello типы, необходимые для этого сценария. Вставьте следующий фрагмент кода в пустой ячейке hello и нажмите клавишу **SHIFT + ВВОД**. 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. Теперь необходимо загрузить данные hello (hvac.csv), проанализировать его и использовать его tootrain hello модели. Для этого определите функцию, которая проверяет, больше ли фактическое температуры hello построения hello температуры целевой hello. Если больше фактического температуры hello, построение hello активна, обозначаемому значением hello по **1.0**. Если меньше фактического температуры hello, построение hello холода, обозначаемому значением hello по **0,0**. 
   
    Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. Настройка конвейера hello Spark машинного обучения, который состоит из трех этапов: разметчика, hashingTF и lr. Дополнительные сведения о возможностях конвейера и о том, как он работает, см. в статье <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Конвейер машинного обучения Spark</a>.
   
    Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. Документ обучения toohello соответствия hello конвейера. Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.
   
        model = pipeline.fit(training)
3. Проверьте hello обучения документа toocheckpoint хода выполнения с помощью приложения hello. Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.
   
        training.show()
   
    В конечном итоге будут следующие аналогичные toohello hello выходные данные:
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    Вернуться назад и проверить результаты hello hello необработанные CSV-файла. Например hello первая строка hello CSV-файл содержит эти данные:

    ![Моментальный снимок выходных данных для примера машинного обучения Spark](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Моментальный снимок выходных данных для примера машинного обучения Spark")

    Обратите внимание, как фактический температуры hello, меньше, чем предлагает построение hello температуры целевой hello холодного. Таким образом в выходных данных обучения hello hello значение **метка** в hello — первая строка **0,0**, это означает, что построение hello не активна.

1. Подготовьте набор данных toorun hello обученной модели по. toodo таким образом, мы бы передать на системный идентификатор и возраст резервной системы (обозначается как **SystemInfo** в выходных данных обучения hello), и предсказать hello модели, будет ли hello построение с возрастом идентификатор и системы, система может быть еще важнее (обозначается 1.0) или охлаждающего ( обозначается 0,0).
   
   Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. Наконец выполнение прогнозов по hello тестовых данных. Вставить hello, следующий фрагмент кода в пустую ячейку и нажать клавишу **SHIFT + ВВОД**.
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. Вы должны увидеть следующие выходные данные как toohello.
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   Из первой строки hello в прогнозе hello, можно увидеть, что для системы Отопления с Идентификатором 20 и системы возраст 25 лет hello построение будет горячей (**прогноза = 1,0**). Первое значение Hello DenseVector (0.49999) соответствует toohello прогноза 0,0 а hello второе значение (0.5001) toohello прогноза 1.0. В выходных данных hello, несмотря на то, что второе значение hello только выше, hello модель показывает **прогноза = 1,0**.
4. После завершения работы приложения hello, необходимо hello toorelease ресурсы для завершения работы hello ноутбуков. toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**. В этом будет завершена и закрыть hello ноутбука.

## <a name="anaconda"></a>Использование библиотеки scikit-learn Anaconda для машинного обучения Spark
Кластеры Apache Spark в HDInsight включают библиотеки Anaconda. Это также касается hello **scikit-узнать** библиотеки для машинного обучения. Библиотека Hello также содержит различные наборы данных, которые можно использовать образцы приложений toobuild непосредственно из записной книжке Jupyter. Для примеров с помощью hello scikit-библиотека Дополнительные сведения см. в разделе [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).

## <a name="seealso"></a>Дополнительные материалы
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Сценарии
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala основных приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
