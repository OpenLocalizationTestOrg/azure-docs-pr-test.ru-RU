---
title: "пользовательские пакеты Maven aaaUse с Jupyter в Spark на Azure HDInsight | Документы Microsoft"
description: "Пошаговые инструкции по как доступные с HDInsight Spark записные книжки Jupyter tooconfigure кластеры toouse пользовательские пакеты Maven."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Использование внешних пакетов с записными книжками Jupyter в кластерах Apache Spark в HDInsight
> [!div class="op_single_selector"]
> * [Использование волшебных команд](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Использование действия сценария](hdinsight-apache-spark-python-package-installation.md)
>
>

Узнайте, как tooconfigure записной книжке Jupyter в кластере Apache Spark на HDInsight toouse внешних, сообществом **maven** пакетов, которые не включены out of box в кластере hello. 

Можно выполнить поиск hello [Maven репозитория](http://search.maven.org/) hello полный список доступных пакетов. Его также можно получить из других источников. Например, полный список предоставленных сообществом пакетов можно найти в разделе [Пакеты Spark](http://spark-packages.org/).

В этой статье вы узнаете, как toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) пакет записной книжки Jupyter hello.



## <a name="prerequisites"></a>Предварительные требования
Необходимо иметь следующие hello.

* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Использование внешних пакетов с записными книжками Jupyter
1. Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели). Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.   
2. Из колонки кластера Spark hello, нажмите кнопку **быстрые ссылки**, а затем из hello **мониторинга кластера** колонке нажмите кнопку **книжке Jupyter**. При появлении запроса введите учетные данные администратора hello hello кластера.

    > [!NOTE]
    > Также может достигать hello книжке Jupyter для кластера, открыв hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Создайте новую записную книжку. Щелкните **Создать**, а затем выберите **Spark**.
   
    ![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Создание записной книжки Jupyter")

4. Создается и открывается с именем hello Untitled.pynb новый блокнот. Щелкните имя записной книжки hello вверху hello и введите понятное имя.
   
    ![Введите имя для ноутбука hello](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "укажите имя для ноутбука hello")

5. Вы воспользуетесь hello `%%configure` magic tooconfigure hello записной книжки toouse внешнего пакета. Портативные компьютеры, использующие внешние пакеты, убедитесь в вызове hello `%%configure` magic в первую ячейку кода hello. Это гарантирует, что hello ядра — настроенное toouse hello пакета до начала сеанса hello.

    >[!IMPORTANT] 
    >Если вы забыли ядра tooconfigure hello в первую ячейку hello, можно использовать hello `%%configure` с hello `-f` параметра, но будет перезапустить сеанс hello и ход выполнения всех будут потеряны.

    | Версия HDInsight | Команда |
    |-------------------|---------|
    |Для HDInsight 3.3 и HDInsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | Для HDInsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. фрагмент кода Hello выше ожидает координаты maven hello для hello внешнего пакета в центральном репозитории Maven. В этом фрагменте кода `com.databricks:spark-csv_2.10:1.4.0` имеет координаты maven hello **spark csv** пакета. Ниже показано, как построить hello координаты для пакета.
   
    а. Найдите пакет hello в hello Maven репозитория. В этом руководстве мы используем [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Из репозитория hello сбора значений hello **GroupId**, **ArtifactId**, и **версии**. Убедитесь, что hello значения, собранные соответствуют кластера. В этом случае мы используем Scala 2.10 и Spark 1.4.0 пакета, но могут потребоваться различные версии tooselect для версии Scala или Spark соответствующие hello в кластере. Можно узнать версию Scala hello в кластере, запустив `scala.util.Properties.versionString` ядра Spark Jupyter hello или отправить Spark. Можно узнать версию Spark hello в кластере, запустив `sc.version` на записные книжки Jupyter.
   
    ![Использование внешних пакетов с записными книжками Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Использование внешних пакетов с записными книжками Jupyter")
   
    c. Объединение hello трех значений, разделенных точкой с запятой (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Запустите hello кода ячейки с hello `%%configure` магическое значение. Эта операция настроит hello базового Livy сеанса toouse hello пакета, который вы указали. В последующих ячейках hello в записной книжке hello теперь можно использовать пакет hello, как показано ниже.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. После этого можно выполнить фрагменты кода hello, как показано ниже, tooview hello данные из hello кадр данных был создан в предыдущем шаге hello.
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a>Дополнительные материалы
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Сценарии
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Создание и запуск приложений
* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Средства и расширения

* [Использование внешних пакетов Python с элементами Jupyter Notebook в кластерах Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-python-package-installation.md)
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)

