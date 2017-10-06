---
title: "aaaAnalyze Application Insight заносит в журнал с Spark - Azure HDInsight | Документы Microsoft"
description: "Узнайте, каким образом tooexport Application Insight ведет журнал tooblob хранилища, а затем проанализировать журналы hello с Spark в HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>Анализ журналов телеметрии Application Insights с помощью Spark в HDInsight

Узнайте, как любые блестящие toouse на HDInsight tooanalyze данные телеметрии Application Insight.

[Visual Studio Application Insights](../application-insights/app-insights-overview.md) — это служба аналитики, которая отслеживает ваши веб-приложения. Данные телеметрии, созданные Application Insights может быть экспортированного tooAzure хранилища. После hello данных в хранилище Azure, HDInsight можно использовать tooanalyze его.

## <a name="prerequisites"></a>Предварительные требования

* Это приложение, настроить toouse Application Insights.

* Умение создавать кластеры HDInsight под управлением Linux. Дополнительные сведения см. в статье [Начало работы. Создание кластера Apache Spark в Azure HDInsight и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

  > [!IMPORTANT]
  > Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Веб-браузер.

Hello следующие ресурсы были использованы при разработке и тестировании, в этом документе:

* Данные телеметрии Application Insights была создана с помощью [toouse Application Insights настроена веб-приложение Node.js](../application-insights/app-insights-nodejs.md).

* Spark на основе Linux в кластере HDInsight версии 3.5 был данных используется tooanalyze hello.

## <a name="architecture-and-planning"></a>Архитектура и планирование

Следующая схема Hello показана архитектура службы hello в этом примере:

![Схема, показывающая данных, передаваемых из хранилища tooblob Application Insights, а затем, обрабатываемых Spark в HDInsight](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Хранилище Azure

Application Insights может быть настроенный toocontinuously экспорта телеметрии сведения tooblobs. HDInsight затем может считывать данные, хранящиеся в hello больших двоичных объектов. Однако существует ряд требований, которые необходимо выполнить. Они описаны ниже.

* **Расположение**: hello учетной записи хранилища и HDInsight находятся в разных регионах, это может увеличить Если задержки. Также увеличивает затраты, как расходов на исходящие данные будут применяться toodata перемещение между областями.

    > [!WARNING]
    > Использование учетной записи хранения, расположение которой отличается от расположения кластера HDInsight, не поддерживается.

* **Тип большого двоичного объекта.** HDInsight поддерживает только блочные BLOB-объекты. Application Insights по умолчанию toousing блочных больших двоичных объектов, поэтому должны работать по умолчанию с HDInsight.

Сведения о добавлении существующий кластер HDInsight tooan дополнительного хранилища см. в разделе hello [добавить дополнительные учетные записи хранения](hdinsight-hadoop-add-storage.md) документа.

### <a name="data-schema"></a>Схема данных

Предоставляет Application Insights [Экспорт модели данных](../application-insights/app-insights-export-data-model.md) tooblobs экспортировать сведения о формате данных телеметрии hello. Hello в данном пошаговом руководстве используется toowork Spark SQL с данными hello. Spark SQL может автоматически сформировать схему для структуры данных JSON hello, записанных службой Application Insights.

## <a name="export-telemetry-data"></a>Экспорт данных телеметрии

Следуйте указаниям hello [Настройка непрерывного экспорта](../application-insights/app-insights-export-telemetry.md) tooconfigure к Application Insights tooexport телеметрии сведения tooan хранилища Azure BLOB-объектов.

## <a name="configure-hdinsight-tooaccess-hello-data"></a>Настройка данных hello tooaccess HDInsight

При создании кластера HDInsight, добавьте учетную запись хранилища hello во время создания кластера.

hello tooadd существующего кластера tooan учетной записи хранилища Azure, используйте сведения hello hello [добавить дополнительные учетные записи хранения](hdinsight-hadoop-add-storage.md) документа.

## <a name="analyze-hello-data-pyspark"></a>Анализ данных hello: PySpark

1. Из hello [портал Azure](https://portal.azure.com), выберите в кластере HDInsight Spark. Из hello **быстрые ссылки** выберите **панели мониторинга кластера**, а затем выберите **книжке Jupyter** из колонки Dashboard__ кластера hello.

    ![панели мониторинга кластера Hello](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. Hello верхний правый угол hello Jupyter страницы, выберите **New**, а затем **PySpark**. При этом откроется новая вкладка браузера, содержащая записную книжку Jupyter на основе Python.

3. В первом поле hello (называется **ячейки**) на странице приветствия введите следующий текст hello:

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    Этот код настраивает Spark toorecursively доступа hello структуру каталогов hello входных данных. Телеметрию Application Insights — toohello аналогичные структуры каталогов регистрируется tooa `/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Используйте **SHIFT + ВВОД** toorun кода hello. На hello левая сторона ячейки hello "\*" отображается между hello скобки tooindicate выполнение кода hello в этой ячейке. По завершении его hello "\*" изменяет номер tooa и выходные данные, аналогичные toohello после текста отображается под hello ячейки:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Ниже hello создается новая ячейка первый из них. Введите следующий текст в новую ячейку hello hello. Замените `CONTAINER` и `STORAGEACCOUNT` с именем учетной записи хранилища Azure hello и имя контейнера BLOB-объект, содержащий данные Application Insights.

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Используйте **SHIFT + ВВОД** tooexecute эту ячейку. Можно увидеть примерно toohello результат, следующий текст:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    Возвращаемый путь wasb Hello — расположение hello hello данные телеметрии Application Insights. Изменение hello `hdfs dfs -ls` hello ячейки toouse hello wasb пути возвращаются строки, а затем используйте **SHIFT + ВВОД** ячейки hello toorun еще раз. На этот раз результаты hello отображать hello каталогов, содержащих данные телеметрии.

   > [!NOTE]
   > Здравствуйте, hello оставшуюся часть hello шагов в этом разделе, `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` каталог был использован. Структура каталога может отличаться.

6. В следующей ячейке hello, введите после кода hello: замените `WASB_PATH` с путем hello из предыдущего шага hello.

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    Этот код создает кадр данных из файлов JSON hello экспортировать процессом hello непрерывный экспорт. Используйте **SHIFT + ВВОД** toorun эту ячейку.
7. Hello следующую ячейку введите и выполните следующие схемы hello tooview создания Spark для файлов JSON hello hello.

   ```python
   jsonData.printSchema()
   ```

    Схема Hello для каждого типа телеметрии отличается. Hello следующий пример является hello схемы, формируемой для веб-запросов (данные, хранящиеся в hello `Requests` подкаталог):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. Используйте следующий кадр данных hello tooregister как временную таблицу hello и выполнить запрос данных hello:

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    Этот запрос возвращает сведения о городе hello для hello top 20 записей, где context.location.city не имеет значение null.

   > [!NOTE]
   > структура контекста Hello присутствует во все данные телеметрии, записанных службой Application Insights. элемент Город Hello не могут быть заполнены в журналах. Используйте схему tooidentify hello другим элементам, которые можно выполнить запрос, может содержать данные для журналов.

    Этот запрос возвращает сведения аналогичные toohello следующий текст:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>Анализ данных hello: Scala

1. Из hello [портал Azure](https://portal.azure.com), выберите в кластере HDInsight Spark. Из hello **быстрые ссылки** выберите **панели мониторинга кластера**, а затем выберите **книжке Jupyter** из колонки Dashboard__ кластера hello.

    ![панели мониторинга кластера Hello](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. Hello верхний правый угол hello Jupyter страницы, выберите **New**, а затем **Scala**. При этом откроется новая вкладка браузера, содержащая записную книжку Jupyter на основе Scala.
3. В первом поле hello (называется **ячейки**) на странице приветствия введите следующий текст hello:

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    Этот код настраивает Spark toorecursively доступа hello структуру каталогов hello входных данных. Данные телеметрии Application Insights в журнал аналогичную структуру каталогов tooa слишком`/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Используйте **SHIFT + ВВОД** toorun кода hello. На hello левая сторона ячейки hello "\*" отображается между hello скобки tooindicate выполнение кода hello в этой ячейке. По завершении его hello "\*" изменяет номер tooa и выходные данные, аналогичные toohello после текста отображается под hello ячейки:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Ниже hello создается новая ячейка первый из них. Введите следующий текст в новую ячейку hello hello. Замените `CONTAINER` и `STORAGEACCOUNT` с именем учетной записи хранилища Azure hello и имя контейнера BLOB-объект, содержащий Application Insights журналы.

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Используйте **SHIFT + ВВОД** tooexecute эту ячейку. Можно увидеть примерно toohello результат, следующий текст:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    Возвращаемый путь wasb Hello — расположение hello hello данные телеметрии Application Insights. Изменение hello `hdfs dfs -ls` hello ячейки toouse hello wasb пути возвращаются строки, а затем используйте **SHIFT + ВВОД** ячейки hello toorun еще раз. На этот раз результаты hello отображать hello каталогов, содержащих данные телеметрии.

   > [!NOTE]
   > Здравствуйте, hello оставшуюся часть hello шагов в этом разделе, `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` каталог был использован. Этот каталог может отсутствовать, если ваши данные телеметрии не предназначены для веб-приложения.

6. В следующей ячейке hello, введите после кода hello: замените `WASB\_PATH` с путем hello из предыдущего шага hello.

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    Этот код создает кадр данных из файлов JSON hello экспортировать процессом hello непрерывный экспорт. Используйте **SHIFT + ВВОД** toorun эту ячейку.

7. Hello следующую ячейку введите и выполните следующие схемы hello tooview создания Spark для файлов JSON hello hello.

   ```scala
   jsonData.printSchema
   ```

    Схема Hello для каждого типа телеметрии отличается. Hello следующий пример является hello схемы, формируемой для веб-запросов (данные, хранящиеся в hello `Requests` подкаталог):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. Используйте следующий кадр данных hello tooregister как временную таблицу hello и выполнить запрос данных hello:

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    Этот запрос возвращает сведения о городе hello для hello top 20 записей, где context.location.city не имеет значение null.

   > [!NOTE]
   > структура контекста Hello присутствует во все данные телеметрии, записанных службой Application Insights. элемент Город Hello не могут быть заполнены в журналах. Используйте схему tooidentify hello другим элементам, которые можно выполнить запрос, может содержать данные для журналов.
   >
   >

    Этот запрос возвращает сведения аналогичные toohello следующий текст:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные примеры использования Spark toowork с данными и служб в Azure см. в разделе hello следующие документы:

* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Обработка событий из концентраторов событий Azure с помощью кластера Apache Spark в HDInsight](hdinsight-apache-spark-eventhub-streaming.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

См. сведения о создании и запуске приложений Spark hello следующие документы:

* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)
