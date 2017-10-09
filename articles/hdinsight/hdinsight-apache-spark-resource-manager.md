---
title: "кластер aaaManage ресурсы для Apache Spark на Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse управления ресурсами для кластеров Spark на Azure HDInsight для повышения производительности."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Управление ресурсами для кластера Apache Spark в Azure HDInsight 

В этой статье вы узнаете, как интерфейсы hello tooaccess Ambari пользовательского интерфейса, YARN пользовательского интерфейса и hello Spark журнала сервера связан с свой кластер Spark. Вы также узнаете о как tootune hello конфигурации кластера для обеспечения оптимальной производительности.

**Предварительные требования:**

Необходимо иметь следующие hello.

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>Как запустить hello Ambari веб-интерфейса?
1. Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели). Вы также можете переходить tooyour кластера в списке **просмотреть все** > **кластеров HDInsight**.
2. В колонке кластера Spark hello, выберите **мониторинга**. При появлении запроса введите учетные данные администратора hello кластера Spark hello.

    ![Запуск Ambari](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Запуск Resource Manager")
3. Это должен быть запущен hello Ambari веб-интерфейса, как показано ниже.

    ![Веб-интерфейс Ambari](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Веб-интерфейс Ambari")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>Как запустить hello Spark журнала сервера?
1. Из hello [портала Azure](https://portal.azure.com/), hello начальной панели, щелкните плитку hello свой кластер Spark (Если вы закрепили toohello начальной панели).
2. Из hello кластера колонки, в разделе **быстрые ссылки**, нажмите кнопку **мониторинга кластера**. В hello **мониторинга кластера** колонка, щелкните **Spark журнала сервера**.

    ![Сервер журнала Spark](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Сервер журнала Spark")

    При появлении запроса введите учетные данные администратора hello кластера Spark hello.

## <a name="how-do-i-launch-hello-yarn-ui"></a>Как запустить hello Yarn пользовательского интерфейса?
Можно использовать hello пользовательского интерфейса YARN toomonitor приложений, запущенных на кластере Spark hello.

1. Из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **YARN**.

    ![Запуск пользовательского интерфейса YARN](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > Кроме того вы можете запустить hello YARN пользовательского интерфейса из hello Ambari пользовательского интерфейса. hello toolaunch Ambari пользовательского интерфейса, из колонки hello кластера, нажмите кнопку **мониторинга кластера**, а затем нажмите кнопку **мониторинга кластера HDInsight**. Hello Ambari пользовательского интерфейса, выберите **YARN**, нажмите кнопку **быстрые ссылки**, щелкните Диспетчер ресурсов active hello и нажмите кнопку **пользовательского интерфейса диспетчера ресурсов**.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>Что такое hello оптимальной конфигурации toorun Spark приложения кластера
Hello три ключевых параметров, которые можно использовать для конфигурации Spark в зависимости от требований приложения являются `spark.executor.instances`, `spark.executor.cores`, и `spark.executor.memory`. Исполнитель — это процесс, запущенный для приложения Spark. Он работает на узле работника hello и отвечает toocarry hello задач для приложения hello. Hello, по умолчанию число исполнителей и размеры hello исполнителя для каждого кластера, рассчитывается на основании hello число рабочих узлов и размер узла hello рабочего потока. Эти значения хранятся в `spark-defaults.conf` на головного узла кластера hello.

Hello трех параметров конфигурации можно настроить на уровне кластера hello (для всех приложений, работающих на кластере hello) или могут быть указаны для каждого отдельного приложения.

### <a name="change-hello-parameters-using-ambari-ui"></a>Изменение параметров hello, с помощью Ambari пользовательского интерфейса
1. Hello Ambari пользовательского интерфейса выберите **Spark**, нажмите кнопку **Configs**и разверните **spark значения по умолчанию пользовательский**.

    ![Изменение параметров с помощью Ambari](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. значения по умолчанию Hello — хороший toohave 4 Spark приложения, одновременно запускать на кластере hello. Можно изменять эти значения из hello пользовательского интерфейса, как показано ниже.

    ![Изменение параметров с помощью Ambari](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Нажмите кнопку **Сохранить** изменения конфигурации toosave hello. В начале hello страницы приветствия, вам будет предложено toorestart hello все затронутые службы. Щелкните **Перезапустить**.

    ![Перезапуск служб](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Изменение параметров приложения, работающего в записной книжке Jupyter hello
Для приложений, работающих в записной книжке Jupyter hello, можно использовать hello `%%configure` магическая изменения конфигурации toomake hello. В идеальном случае необходимо внести такие изменения в начале приложения hello, прежде чем выполнять первой ячейки кода hello. Это гарантирует, что конфигурация hello примененных toohello Livy сеанса, когда он создается. Если необходимо, чтобы конфигурация toochange hello позже в приложении hello, необходимо использовать hello `-f` параметра. Однако предположим, что все хода выполнения работы в hello приложения будут потеряны.

фрагмент кода Hello ниже показано, как toochange hello конфигурации для приложения, работающего в Jupyter.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

Параметры конфигурации должны передаваться в виде строки JSON и должен быть на следующую строку hello после hello magic, как показано в примере столбец hello.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>Изменение параметров hello для отправки с помощью приложения команду spark-submit
Следующая команда является примером как toochange hello параметры конфигурации для пакета приложения, которое отправляется с помощью `spark-submit`.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>Изменение параметров отправки с помощью перелистывание приложения hello
Следующая команда является примером как toochange hello параметры конфигурации для пакета приложения, которое отправляется с помощью cURL.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Как изменить эти параметры на сервере Thrift Spark?
Сервера Thrift Spark предоставляет кластера Spark tooa доступа JDBC/ODBC и используется tooservice Spark SQL-запросов. Он используется для обслуживания запросов к службе Spark SQL. Используйте toocommunicate протокол ODBC с запросами Spark SQL tooexecute сервера Thrift Spark как приложение Spark. При создании кластера Spark двух экземпляров hello запуска сервера Thrift Spark на каждый головной узел. Каждый сервер Thrift Spark отображается как приложение Spark в hello YARN пользовательского интерфейса.

Использует сервера Thrift Spark усилить исполнителя динамического выделения и поэтому hello `spark.executor.instances` не используется. Вместо этого использует сервера Thrift Spark `spark.dynamicAllocation.minExecutors` и `spark.dynamicAllocation.maxExecutors` toospecify hello исполнителя count. Здравствуйте, параметры конфигурации `spark.executor.cores` и `spark.executor.memory` — используемый размер исполнителя toomodify hello. Все эти параметры вы можете изменять, как показано ниже.

* Разверните hello **Advanced spark thrift-sparkconf** параметры hello категории tooupdate `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, и `spark.executor.memory`.

    ![Настройка сервера Thrift Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Разверните hello **настраиваемый spark-thrift-sparkconf** параметр hello категории tooupdate `spark.executor.cores`.

    ![Настройка сервера Thrift Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>Изменение памяти драйвера hello hello сервера Thrift Spark
Драйвер памяти сервера Thrift Spark предоставляется настроенных too25% от размера головного узла ОЗУ hello, общий размер ОЗУ hello головного узла hello больше 14 ГБ. Можно использовать hello конфигурации памяти драйвера hello toochange Ambari пользовательского интерфейса, как показано ниже.

* Hello Ambari пользовательского интерфейса выберите **Spark**, нажмите кнопку **конфигураций**, разверните **Advanced spark env**и затем задайте значение hello **spark_thrift_cmd_opts**.

    ![Настройка памяти сервера Thrift Spark](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>Я не использую бизнес-аналитику с кластером Spark. Как сделать ресурсы hello назад
Поскольку используется динамическое выделение Spark, hello только ресурсы, используемые сервером thrift — это hello ресурсы для двух шаблонов приложения hello. Эти ресурсы, которые необходимо остановить hello сервера Thrift служб, работающих в кластере hello tooreclaim.

1. Hello Ambari пользовательского интерфейса, hello левой панели щелкните **Spark**.
2. На следующей странице приветствия щелкните **серверы Thrift Spark**.

    ![Перезапуск сервера Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Вы увидите два headnodes hello, на какие hello выполняется сервера Thrift Spark. Выберите один из hello headnodes.

    ![Перезапуск сервера Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. Следующая страница приветствия перечислены все hello службы, запущенные на этом головному узлу. Щелкните hello разворачивающуюся кнопку Далее tooSpark сервера Thrift hello списке и нажмите кнопку **остановить**.

    ![Перезапуск сервера Thrift](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Повторите эти действия на hello других головному узлу.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>Мои записные книжки Jupyter работают не так, как ожидалось. Как можно перезапустить службу hello?
Запустите hello Ambari веб-интерфейса, как показано выше. Hello левой области навигации щелкните **Jupyter**, нажмите кнопку **действий службы**, а затем нажмите кнопку **перезапустите все**. Это приведет к запуску hello Jupyter службы на всех headnodes hello.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>Как узнать, что ресурсы заканчиваются?
Запустите hello Yarn пользовательского интерфейса, как показано выше. В таблице показателей кластера поверх экрана приветствия, проверьте значения **памяти,** и **общей памяти** столбцов. Если очень близкие значения hello 2, может не иметься достаточно ресурсов toostart hello Далее приложение. Hello применимо и к toohello **используется VCores** и **VCores всего** столбцов. Кроме того, в основном представлении hello, если имеется приложение лет в **ПРИНЯТО** состоянии и не переходит **под УПРАВЛЕНИЕМ** , ни **сбой** состоянии, это может также свидетельствовать об не становится toostart достаточно ресурсов.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>Как kill работающего приложения toofree ресурса?
1. В hello Yarn пользовательского интерфейса, с помощью hello левой панели, щелкните **под управлением**. Из списка выполняющихся приложений hello, определить toobe приложения hello завершен и щелкнуть hello **идентификатор**.

    ![Завершение работы приложения 1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "Завершение работы приложения 1")

2. Нажмите кнопку **Kill приложения** hello правом верхнем углу, затем щелкните **ОК**.

    ![Завершение работы приложения 2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "Завершение работы приложения 2")

## <a name="see-also"></a>См. также
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a>Для специалистов по анализу данных

* [Использование Spark с машинным обучением. Использование Spark в HDInsight для анализа температуры в здании на основе данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark с машинного обучения: используйте Spark в HDInsight toopredict food проверки результатов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Анализ журнала веб-сайта с использованием Spark в HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analyze Application Insights telemetry logs with Spark on HDInsight (Анализ журналов телеметрии Application Insights с помощью Spark в HDInsight)](hdinsight-spark-analyze-application-insight-logs.md)
* [Использование Caffe в кластере Azure HDInsight Spark для распределенного глубокого обучения](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Для разработчиков Spark

* [Создание автономного приложения с использованием Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Удаленный запуск заданий с помощью Livy в кластере Spark](hdinsight-apache-spark-livy-rest-interface.md)
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Потоковая передача Spark. Использование Spark в HDInsight для сборки приложений потоковой передачи данных в режиме реального времени](hdinsight-apache-spark-eventhub-streaming.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)
