---
title: "aaaInstall Jupyter локально & подключения кластера Azure HDInsight Spark tooan | Документы Microsoft"
description: "Узнайте, как книжке Jupyter tooinstall на локальном компьютере и его подключения кластера tooan Apache Spark на Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>Установка книжке Jupyter на вашем компьютере и подключение tooApache Spark в HDInsight

В этой статье вы узнаете, как записной книжки Jupyter tooinstall с hello пользовательских PySpark (для Python) и ядра Spark (для Scala) с усилить magic и подключения кластера HDInsight tooan записной книжки hello. Может быть несколько причин tooinstall Jupyter на локальном компьютере и может быть также некоторые проблемы. Для получения дополнительных сведений в данном разделе hello [Зачем устанавливать Jupyter на моем компьютере](#why-should-i-install-jupyter-on-my-computer) конце hello в этой статье.

Существует три ключевых действия, участвующие в процессе установки Jupyter и hello Spark magic на компьютере.

* Установка записной книжки Jupyter
* Установите hello PySpark и Spark ядер hello Spark magic
* Настройка Spark magic tooaccess кластера Spark в HDInsight

Дополнительные сведения о пользовательских ядер hello и magic Spark hello для записные книжки Jupyter с кластером HDInsight см. в разделе [кластеры ядер, доступных для записные книжки Jupyter с Apache Spark Linux в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Предварительные требования
Hello предварительные требования, перечисленные здесь не для установки Jupyter. Это подключение hello кластера HDInsight tooan Jupyter записной книжки после установки записной книжки hello.

* Подписка Azure. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="install-jupyter-notebook-on-your-computer"></a>Установка записной книжки Jupyter на компьютер

Перед установкой записных книжек Jupyter необходимо установить Python. Python и Jupyter доступны как часть hello [дистрибутив Anaconda](https://www.continuum.io/downloads). При установке Anaconda устанавливается дистрибутив Python. После установки Anaconda, чтобы добавить hello Jupyter установки, запустите соответствующие команды.

1. Загрузите hello [Anaconda установщика](https://www.continuum.io/downloads) для платформы и hello выполнения установки. Во время выполнения мастера установки hello убедитесь, что выбран hello параметр tooadd Anaconda tooyour переменной PATH.
2. Выполните следующие команды tooinstall Jupyter hello.

        conda install jupyter

    Дополнительные сведения об установке Jupyter см. [здесь](http://jupyter.readthedocs.io/en/latest/install.html).

## <a name="install-hello-kernels-and-spark-magic"></a>Установка ядра hello и Spark magic

Инструкции по как tooinstall hello Spark magic, hello PySpark и Spark ядер, следуйте инструкциям по установке hello в hello [sparkmagic документации](https://github.com/jupyter-incubator/sparkmagic#installation) на GitHub. Hello первым шагом в документации magic Spark hello предлагает магическое tooinstall Spark. Замените первый шаг в ссылке hello hello, следующие команды, в зависимости от версии hello hello кластера HDInsight, которую вы будете подключаться. Затем выполните оставшиеся действия, описанные в документации magic Spark hello hello. Если вы хотите tooinstall hello других ядер, необходимо выполнить шаг 3 в hello Spark magic инструкции см.

* Для кластеров версии 3.4 установите sparkmagic версии 0.2.3, выполнив команду `pip install sparkmagic==0.2.3`

* Для кластеров версий 3.5 и 3.6 установите sparkmagic версии 0.11.2, выполнив команду `pip install sparkmagic==0.11.2`

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>Настройка кластера Spark tooHDInsight magic tooconnect Spark

В этом разделе Настройка magic Spark hello, установленного ранее tooconnect tooan Apache Spark кластер, необходимо уже созданных в Azure HDInsight.

1. Hello Jupyter сведения о конфигурации обычно хранятся в домашнем каталоге hello пользователей. toolocate вашим домашним каталогом на любой платформе операционной системы, тип hello следующие команды.

    Запустите консоль hello Python. В окно командной строки введите ниже hello:

        python

    Hello оболочки Python введите hello, следующая команда toofind hello домашнего каталога.

        import os
        print(os.path.expanduser('~'))

2. Перейдите в корневой каталог toohello и создайте папку с именем **.sparkmagic** , если он еще не существует.
3. В папке hello, создайте файл с именем **config.json** и добавьте следующий фрагмент JSON внутри него hello.

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. Замените **{USERNAME}**, **{CLUSTERDNSNAME}** и **{BASE64ENCODEDPASSWORD}** соответствующими значениями. Фактический пароль можно использовать несколько служебных программ избранные языка программирования и зашифрованный пароль online toogenerate кодировке base64.

5. Настройка параметров правой периодического сигнала hello в `config.json`. Эти параметры следует добавить во же уровня как hello hello `kernel_python_credentials` и `kernel_scala_credentials` фрагменты вашей добавленные ранее. Пример hello как и где tooadd параметры периодических сигналов, см. в этой [config.json пример](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).

    * Для `sparkmagic 0.2.3` (кластеры версии 3.4) добавьте:

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * Для `sparkmagic 0.11.2` (кластеры версий 3.5 и 3.6) добавьте:

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >Тактовые импульсы отправляются tooensure сеансы не попадают. При переходит toosleep или завершить работу компьютера, не передается пульса hello, приведет к hello сеанса, удаляются. Для v3.4 кластеров, при желании toodisable такое поведение, можно задать hello Livy config `livy.server.interactive.heartbeat.timeout` слишком`0` из hello Ambari пользовательского интерфейса. Для кластеров версии 3.5 если конфигурации hello 3.5 выше, не устанавливайте hello сеанса не удаляются.

6. Запустите Jupyter. Используйте следующую команду из командной строки hello hello.

        jupyter notebook

7. Убедитесь, что можно подключиться toohello кластер, использующий книжке Jupyter hello и могут использовать доступные magic Spark hello с ядром hello. Выполните следующие шаги hello.

    а. Создайте новую записную книжку. В правом углу hello, выберите **New**. Вы увидите ядра по умолчанию hello **Python2** и hello два новых ядер, которые можно установить **PySpark** и **Spark**. Щелкните **PySpark**.

    ![Ядра в записной книжке Jupyter](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Ядра в записной книжке Jupyter")

    b. Запустите следующий фрагмент кода hello.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Если можно успешно получить выходные данные hello, проверяется кластеру HDInsight toohello соединения.

    >[!TIP]
    >Tooupdate hello записной книжки конфигурации tooconnect tooa другой кластер, обновите hello config.json hello новый набор значений, как показано в шаге 3 выше.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>Зачем устанавливать Jupyter на моем компьютере?
Может быть несколько причин, почему вы хотите tooinstall Jupyter на вашем компьютере и подключить его кластера tooa Spark на HDInsight.

* Даже если записные книжки Jupyter уже доступны hello кластере Spark в Azure HDInsight, установка Jupyter на компьютере обеспечивает hello toocreate параметр записных книжек локально, протестировать приложение на запущенному кластеру и затем передать hello портативные компьютеры toohello кластера. tooupload hello записных книжек toohello кластера, вы можете отправить их с помощью hello книжке Jupyter, на котором выполняется или hello кластера и сохранить toohello /HdiNotebooks папки в учетной записи хранилища hello, связанной с кластером hello. Дополнительные сведения о хранении портативные компьютеры в кластере hello см. в разделе [записные книжки Jupyter хранения](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?
* Портативные компьютеры hello доступны локально, позволяет подключаться toodifferent Spark кластеров на основе требований вашего приложения.
* Можно использовать GitHub tooimplement системы управления версиями и управления версиями для ноутбуков hello. Вы также можете среде совместной работы, где могут работать несколько пользователей с hello же записной книжке.
* Вы можете работать с записными книжками локально даже без кластера. Требуется только tootest кластера записных книжек от, не toomanually управлять записных книжек, либо в среде разработки.
* Он может быть проще tooconfigure собственные локальной среде разработки, чем tooconfigure hello Jupyter установки на кластере hello.  Вы сможете использовать все hello программного обеспечения, установленных локально без настройки одного или нескольких удаленных кластеров.

> [!WARNING]
> С Jupyter установлен на локальном компьютере, несколько пользователей могут запустить hello же записной книжке hello же Spark кластера на hello то же время. В такой ситуации создаются несколько сеансов Livy. Если возникли проблемы и требуется, он будет tootrack сложной задачей, принадлежит какой Livy сеанс пользователя toowhich toodebug.
>
>

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
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)
