---
title: "Действие aaaScript — пакеты установки Python с Jupyter на Azure HDInsight | Документы Microsoft"
description: "Пошаговые инструкции по как toouse сценария действия tooconfigure Jupyter портативные компьютеры с HDInsight Spark кластеры пакеты toouse внешних python."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Используйте действие сценария tooinstall внешние пакеты Python для записные книжки Jupyter в кластерах Apache Spark в HDInsight
> [!div class="op_single_selector"]
> * [Использование волшебных команд](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Использование действия сценария](hdinsight-apache-spark-python-package-installation.md)
>
>

Узнайте, как tooconfigure toouse действия скрипта кластера с Apache Spark на HDInsight (Linux) toouse внешних, сообществом **python** пакеты, которые не включены out of box в кластере hello.

> [!NOTE]
> Можно также настроить с помощью записной книжке Jupyter `%%configure` магическая toouse внешние пакеты. Дополнительные сведения см. в статье [Использование внешних пакетов с записными книжками Jupyter в кластерах Apache Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

Можно выполнить поиск hello [индекса пакета](https://pypi.python.org/pypi) для hello полного списка доступных пакетов. Его также можно получить из других источников. Например, можно установить пакеты, предоставляемые посредством [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) или [conda-forge](https://conda-forge.github.io/feedstocks.html).

В этой статье вы узнаете, как tooinstall hello [TensorFlow](https://www.tensorflow.org/) пакета с помощью сценария Actoin в кластере и использовать его с помощью книжке Jupyter hello.

## <a name="prerequisites"></a>Предварительные требования
Необходимо иметь следующие hello.

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Если у вас еще нет кластера Spark в HDInsight на платформе Linux, можно выполнить действия сценария во время его создания. Обратитесь к документации hello на [как toouse пользовательского скрипта действия](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Использование внешних пакетов с записными книжками Jupyter

1. Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели). Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.   

2. Из колонки кластера Spark hello, нажмите кнопку **действия скрипта** под **использование**. Выполните пользовательское действие hello, устанавливающий TensorFlow в hello головного узла и hello рабочих узлов. Hello bash сценария можно ссылаться из: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh посещение hello документацию по [как toouse пользовательского скрипта действия](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Существует два python установок в кластере hello. Spark будет использовать установки python hello Anaconda, расположенный в `/usr/bin/anaconda/bin`. Укажите его в настраиваемых действиях с помощью `/usr/bin/anaconda/bin/pip` и `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Открытие Jupyter Notebook PySpark

    ![Создание записной книжки Jupyter](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Создание записной книжки Jupyter")

4. Создается и открывается с именем hello Untitled.pynb новый блокнот. Щелкните имя записной книжки hello вверху hello и введите понятное имя.

    ![Введите имя для ноутбука hello](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "укажите имя для ноутбука hello")

5. Теперь будет выполнена команда `import tensorflow` и запущен пример hello world. 

    Toocopy кода:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    Hello результат будет выглядеть следующим образом:
    
    ![Выполнение кода TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "Выполнение кода TensorFlow")



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
* [Использование внешних пакетов с записными книжками Jupyter в кластерах Apache Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)
