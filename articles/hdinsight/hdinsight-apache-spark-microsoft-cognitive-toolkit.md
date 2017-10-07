---
title: "aaaMicrosoft Когнитивных Toolkit с Azure HDInsight Spark для углубленного обучения | Документы Microsoft"
description: "Дополнительные сведения как обученной Когнитивных набор средств Майкрософт глубокой модели обучения может быть применен tooa набора данных, с помощью hello Spark Python API в кластере Azure HDInsight Spark."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Использование модели глубокого обучения Microsoft Cognitive Toolkit в кластере Azure HDInsight Spark

В этой статье hello следующие действия.

1. Выполнения пользовательского скрипта tooinstall Когнитивных набор средств Microsoft на кластере Azure HDInsight Spark.

2. Как отправить Jupyter записной книжки toohello Spark кластера toosee tooapply обученной Когнитивных набор средств Майкрософт глубокого изучения toofiles модели в учетной записи хранения BLOB-объектов Azure с помощью hello [API Spark Python (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>Предварительные требования

* **Подписка Azure**. Прежде чем приступать к изучению этого руководства, необходимо оформить подписку Azure. Ознакомьтесь со страницей [Создайте бесплатную учетную запись Azure уже сегодня](https://azure.microsoft.com/free).

* **Кластер Azure HDInsight Spark**. В этой статье создайте кластер Spark 2.0. Инструкции см. в разделе [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-does-this-solution-flow"></a>Каково предназначение этой последовательности решения?

Для описания этого решения используются данная статья и элемент Jupyter Notebook, переданный в рамках данного руководства. В этой статье выполните следующие шаги hello.

* Выполните действие сценария в кластере HDInsight Spark tooinstall пакетов Когнитивных набор средств Майкрософт и Python.
* Отправьте книжке Jupyter hello, запускаемую toohello решения hello кластера HDInsight Spark.

Hello следующие оставшиеся шаги описаны в записной книжке Jupyter hello.

- Загрузка примеров изображений в устойчивый распределенный набор данных Spark (RDD).
   - Загрузка модулей и определение предустановок.
   - Скачать набор данных hello локально на кластере Spark hello
   - Преобразовать в RDD hello набора данных
- Оценка hello изображения с помощью обученной модели Когнитивных Toolkit
   - Загрузите кластера Spark toohello модели Когнитивных Toolkit hello обучения
   - Определение функции toobe используемых рабочих узлов
   - Оценка hello изображений на рабочих узлов
   - Анализ точности модели.


## <a name="install-microsoft-cognitive-toolkit"></a>Установка Microsoft Cognitive Toolkit

Microsoft Cognitive Toolkit в кластере Spark можно установить с помощью действия сценария. Действие сценария использует компоненты tooinstall пользовательские сценарии в кластере hello, которые недоступны по умолчанию. С помощью HDInsight .NET SDK, или с помощью Azure PowerShell можно использовать hello пользовательского скрипта из hello портала Azure. Hello сценария tooinstall hello toolkit также можно использовать либо в процессе создания кластера или после hello кластера запущен и работает. 

В этой статье мы используем toolkit hello портала tooinstall hello, после создания кластера hello. Другие способы toorun hello пользовательского скрипта, в разделе [HDInsight настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md).

### <a name="using-hello-azure-portal"></a>С помощью портала Azure hello

Как портал Azure toorun toouse hello записать действие в скрипт инструкции см. в разделе [HDInsight настроить кластеры, использующие действие сценария](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation). Убедитесь, что предоставляют следующие входные данные tooinstall Когнитивных набор средств Microsoft hello.

* Укажите значение для имени действия сценария hello.

* В поле **URI bash-скрипта** введите `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.

* Убедитесь, что выполнение сценария hello только для hello head и рабочих узлов и снимите все hello остальные флажки.

* Щелкните **Создать**.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Отправка tooAzure записной книжки Jupyter hello кластера HDInsight Spark

hello toouse Когнитивных набор средств Microsoft с кластера Azure HDInsight Spark hello, необходимо загрузить hello книжке Jupyter **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello кластера Azure HDInsight Spark. Этот элемент Notebook можно найти на сайте GitHub: [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).

1. Репозитории GitHub клон hello [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration). Tooclone инструкции в разделе [клонирование репозитория](https://help.github.com/articles/cloning-a-repository/).

2. Hello портал Azure, откройте колонку кластера Spark hello, которая уже подготовлена, щелкните **мониторинга кластера**, а затем нажмите кнопку **книжке Jupyter**.

    Можно также запустить книжке Jupyter hello, последовательно выбрав URL-адрес toohello `https://<clustername>.azurehdinsight.net/jupyter/`. Замените \<имя_кластера > с именем hello кластера HDInsight.

3. Из записной книжки Jupyter hello, нажмите кнопку **отправить** в hello в правом верхнем углу, а затем toohello расположение, где клонировать репозиторий GitHub hello.

    ![Отправка tooAzure записной книжки Jupyter кластера HDInsight Spark](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "tooAzure записной книжки Jupyter отправить кластера HDInsight Spark")

4. Еще раз нажмите кнопку **Upload** (Передать).

5. После передачи записной книжки hello щелкните имя hello hello портативного компьютера и следуйте указаниям hello в записной книжке hello сам как tooload hello набора данных и выполнять учебника hello.

## <a name="see-also"></a>См. также
* [Обзор: Apache Spark в Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Сценарии
* [Использование Spark со средствами бизнес-аналитики. Выполнение интерактивного анализа данных с использованием Spark в HDInsight с помощью средств бизнес-аналитики](hdinsight-apache-spark-use-bi-tools.md)
* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analyze Application Insights telemetry logs with Spark on HDInsight (Анализ журналов телеметрии Application Insights с помощью Spark в HDInsight)](hdinsight-spark-analyze-application-insight-logs.md)

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

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
