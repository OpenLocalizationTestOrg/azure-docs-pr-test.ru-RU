---
title: "журналы веб-сайт aaaAnalyze с библиотеками Python в Spark - Azure | Документы Microsoft"
description: "Записной книжки показано, как tooanalyze данных журнала с помощью пользовательская библиотека с Spark на Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a>Анализ журналов веб-сайтов с помощью пользовательской библиотеки Python и кластера Spark в HDInsight

Записной книжки показано, как tooanalyze данных журнала с помощью пользовательская библиотека с Spark в HDInsight. Мы используем пользовательская библиотека Hello является именем библиотеки Python **iislogparser.py**.

> [!TIP]
> Кроме того, это руководство доступно в виде записной книжки Jupyter в кластере Spark (на платформе Linux), созданном в HDInsight. взаимодействие с ноутбука Hello позволяет выполнять фрагменты кода Python hello из записной книжки hello сам. Учебник hello tooperform в записной книжке создать кластер Spark, запустить записной книжке Jupyter (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), и запустите записной книжки hello **анализировать журналы с помощью Spark, с помощью пользовательских library.ipynb** под hello  **PySpark** папки.
>
>

**Предварительные требования:**

Необходимо иметь следующие hello.

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="save-raw-data-as-an-rdd"></a>Сохранение необработанных данных в формате RDD
В этом разделе мы используем hello [Jupyter](https://jupyter.org) ноутбук, связанные с кластера с Apache Spark в HDInsight toorun задания, которые обрабатывают необработанные образцы данных и сохраните его как таблицу Hive. Образец Hello данных является CSV-файла (hvac.csv) доступен во всех кластерах по умолчанию.

После сохранения данных как таблицу Hive в следующем разделе hello мы будут подключаться с помощью средств бизнес-Аналитики, таких как Power BI и Tableau таблицу Hive toohello.

1. Из hello [портал Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели). Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.   
2. Из колонки кластера Spark hello, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **книжке Jupyter**. При появлении запроса введите учетные данные администратора hello hello кластера.

   > [!NOTE]
   > Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Создайте новую записную книжку. Щелкните **Создать**, а затем выберите **PySpark**.

    ![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Создание записной книжки Jupyter")
4. Создается и открывается с именем hello Untitled.pynb новый блокнот. Щелкните имя записной книжки hello вверху hello и введите понятное имя.

    ![Введите имя для ноутбука hello](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "укажите имя для ноутбука hello")
5. Поскольку вы создали записной книжке с использованием ядра PySpark hello, вы не обязательно toocreate контекстов явным образом. контексты Spark и Hive Hello автоматически создается автоматически при выполнении первой ячейке кода hello. Можно запустить, импортировав hello типы, необходимые для этого сценария. Вставьте следующий фрагмент кода в пустой ячейке hello и нажмите клавишу **SHIFT + ВВОД**.

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. Создайте RDD, используя данные журнала образца hello уже доступны в кластере hello. Доступ к hello в учетной записи хранения по умолчанию hello связанные с кластером hello в **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. Получить образец tooverify набор журнала, который hello в предыдущем шаге, завершилась успешно.

        logs.take(5)

    Вы должны увидеть следующие выходные данные как toohello.

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a>Анализ данных журнала с помощью пользовательской библиотеки Python
1. В приведенных выше входных данных hello hello первые несколько строк учитываются сведения заголовков hello и hello схема, описанная в заголовок, соответствующий каждой оставшиеся строки. Анализ таких журналов может быть сложным, поэтому мы используем настраиваемую библиотеку Python (**iislogparser.py**), которая делает эту задачу намного проще. По умолчанию эта библиотека входит в состав кластера Spark в HDInsight и расположена в **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.

    Однако эта библиотека не является hello `PYTHONPATH` , нельзя использовать с помощью инструкции импорта, как `import iislogparser`. toouse этой библиотеки, нам необходимо распространить tooall hello рабочих узлов. Запустите следующий фрагмент кода hello.

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. `iislogparser`предоставляет функцию `parse_log_line` , возвращающий `None` Если строку журнала представляет собой строку и возвращает экземпляр hello `LogLine` класса при обнаружении строки журнала. Используйте hello `LogLine` tooextract класс только hello строк журнала из hello RDD:

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. Получить несколько tooverify извлеченных строк журнала, hello шаге, завершилась успешно.

       logLines.take(2)

   Hello выходные данные должны быть примерно toohello следующее:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. Hello `LogLine` класс, в свою очередь, имеет некоторые методы, например `is_error()`, который показывает, имеет ли запись в журнал код ошибки. Использовать это число hello toocompute ошибок в строках журнала извлечены hello и войдите все hello ошибки tooa другой файл.

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   Вы должны увидеть результаты hello следующим образом:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. Можно также использовать **Matplotlib** tooconstruct визуализации данных hello. Например следует tooisolate причину hello запросы выполняются в течение длительного времени может потребоваться toofind hello файлы hello tooserve большая часть времени в среднем.
   в приведенном ниже фрагменте Hello извлекает hello top 25 ресурсы, предпринятые большинство tooserve время запроса.

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   Вы должны увидеть результаты hello следующим образом:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. Можно также представить эти сведения в виде hello построения. Как первый toocreate шаг построения, сообщите нам сначала создать временную таблицу **AverageTime**. Hello таблицы групп hello регистрирует по toosee времени при наличии каких-либо пиков необычные задержки в определенный момент времени.

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. Можно выполнять hello, следуя tooget запроса SQL все записи hello в hello **AverageTime** таблицы.

       %%sql -o averagetime
       SELECT * FROM AverageTime

   Hello `%%sql` следуют магическое `-o averagetime` гарантирует, что hello выходных данных запроса hello сохраняется локально на сервере Jupyter hello (обычно hello головному узлу кластера hello). Hello выходные данные сохраняются в виде [Pandas](http://pandas.pydata.org/) кадр данных с hello указано имя **averagetime**.

   Вы должны увидеть результаты hello следующим образом:

   ![Результат SQL-запроса](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "Результат SQL-запроса")

   Дополнительные сведения о hello `%%sql` magic, см. в разделе [поддерживает параметры с hello %% sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
7. Теперь вы можете использовать Matplotlib, библиотеку используется tooconstruct визуализации данных, toocreate построение. Так как hello рисунка должны быть созданы из локально hello материализованные **averagetime** кадр данных, фрагмент кода hello должно начинаться с hello `%%local` магическое значение. Это гарантирует, что hello код запускается локально на сервере Jupyter hello.

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   Вы должны увидеть результаты hello следующим образом:

   ![Выходные данные Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Выходные данные Matplotlib")
8. После завершения работы приложения hello, необходимо hello toorelease ресурсы для завершения работы hello ноутбуков. toodo так, hello **файл** меню на ноутбуке hello щелкните **закрыть и остановить**. В этом будет завершена и закрыть hello ноутбука.

## <a name="seealso"></a>Дополнительные материалы
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Сценарии
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)
