---
title: "aaaKernels записной книжки Jupyter на Spark кластеров в Azure HDInsight | Документы Microsoft"
description: "Дополнительные сведения о версии ядра PySpark PySpark3 и Spark hello записной книжки Jupyter, доступные с кластерами Spark на Azure HDInsight."
keywords: "записная книжка jupyter в spark, jupyter в spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Ядра для записной книжки Jupyter в кластерах Spark в Azure HDInsight 

Кластеры HDInsight Spark предоставляют ядер, которые можно использовать для тестирования приложений с записной книжке Jupyter hello Spark. Ядра — это программа, которая выполняет и интерпретирует ваш код. приведены три ядра Hello.

- **PySpark** (для приложений, написанных на языке Python2).
- **PySpark3** (для приложений, написанных на языке Python3).
- **Spark** (для приложений, написанных на языке Scala).

В этой статье вы узнаете, как toouse эти ядер и hello преимущества их использования.

## <a name="prerequisites"></a>Предварительные требования

* Кластер Apache Spark в HDInsight. Инструкции см. в статье [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Создание записной книжки Jupyter в Spark HDInsight

1. Из hello [портал Azure](https://portal.azure.com/), откройте кластера.  В разделе [списка и Показывать кластеры](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) hello инструкции. Hello кластера будет открыт в Новая колонка портала.

2. Из hello **быстрые ссылки** щелкните **кластера панелей мониторинга** tooopen hello **кластера панелей мониторинга** колонку.  Если вы не видите **быстрые ссылки**, нажмите кнопку **Обзор** из меню слева hello в колонке hello.

    ![Записная книжка Jupyter в Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "Записная книжка Jupyter в Spark") 

3. Щелкните **Записная книжка Jupyter**. При появлении запроса введите учетные данные администратора hello hello кластера.
   
   > [!NOTE]
   > Кроме того, может попасть книжке Jupyter hello на кластере Spark путем открытия hello следующий URL-адрес в браузере. Замените **CLUSTERNAME** с hello имя кластера:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. Нажмите кнопку **New**, а затем — **Pyspark**, **PySpark3**, или **Spark** toocreate записной книжке. Используйте hello Spark ядра для приложений Scala PySpark ядра для Python2 приложений и PySpark3 ядра для Python3 приложений.
   
    ![Ядра для записной книжки Jupyter в Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "Ядра для записной книжки Jupyter в Spark") 

4. Записной книжке откроется ядра hello выбранный.

## <a name="benefits-of-using-hello-kernels"></a>Преимущества использования ядра hello

Ниже приведены несколько преимуществ использования новой версии ядра hello с книжке Jupyter в кластерах Spark HDInsight.

- **Предустановленные контексты**. С **PySpark**, **PySpark3**, или hello **Spark** ядра, не требуется tooset hello Spark или куст контекстов явно перед началом работы с приложениями. Они доступны по умолчанию. а именно:
   
   * **sc** для контекста Spark;
   * **sqlContext** для контекста Hive.

    Таким образом не имеют toorun выражения, например hello следующие tooset hello контекстах:

        sc = SparkContext('yarn-client')    sqlContext = HiveContext(sc)

    Вместо этого можно использовать непосредственно hello предустановленный набор контекстов в приложении.

- **Волшебные команды.** Hello ядра PySpark предоставляет некоторые предопределенные «magics», которые являются специальные команды, которые можно вызвать с `%%` (например, `%%MAGIC` <args>). Команда magic Hello должно быть первое слово hello в ячейке кода и разрешить для нескольких строк содержимого. magic слово Hello должен быть первым словом hello hello ячейки. Добавление ничего перед magic hello, даже комментарии, приводит к ошибке.     Дополнительные сведения о волшебных командах см. [здесь](http://ipython.readthedocs.org/en/stable/interactive/magics.html).
   
    Hello следующей таблице перечислены hello различных magics через hello ядер.

   | Волшебная команда | Пример | Описание |
   | --- | --- | --- |
   | help |`%%help` |Создает таблицу из всех доступных magics hello пример и описание |
   | info |`%%info` |Выводит сведения сеанса для hello текущей конечной точки Livy |
   | Настройка |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |Настраивает параметры hello для создания сеанса. Здравствуйте, флаг force (-f) является обязательным, если сеанс уже создан, который гарантирует hello сеанса удалить и создать заново. Список допустимых параметров приведен в разделе, посвященном [тексту запроса сеансов POST Livy](https://github.com/cloudera/livy#request-body) . Параметры должны передаваться в виде строки JSON и должен быть на следующую строку hello после hello magic, как показано в примере столбец hello. |
   | sql |`%%sql -o <variable name>`<br> `SHOW TABLES` |Выполняет запрос Hive в отношении hello sqlContext. Если hello `-o` передается параметр, результат hello hello запроса сохраняется в hello %% локального контекста Python как [Pandas](http://pandas.pydata.org/) кадр данных. |
   | local |`%%local`<br>`a=1` |Весь код hello в последующих строках выполняется локально. Код должен быть допустимым кодом Python2 даже независимо от ядра hello, которую вы используете. Таким образом, даже если вы выбрали **PySpark3** или **Spark** ядра при создании hello записной книжки, если вы используете hello `%%local` magic в ячейке, что ячейка должна иметь только допустимый код Python2... |
   | журналы |`%%logs` |Выходные данные журналов hello для текущего сеанса Livy hello. |
   | удалить |`%%delete -f -s <session number>` |Удаляет определенный сеанс hello текущей Livy конечной точки. Обратите внимание, нельзя удалить сеанс hello, обычно инициируемой для ядра hello сам. |
   | cleanup |`%%cleanup -f` |Удаляет все сеансы hello для hello текущей конечной точки Livy, включая записной книжки сеанс. флаг force Hello -f является обязательным. |

   > [!NOTE]
   > В дополнение к этому toohello magics добавленные ядра PySpark hello, можно также использовать hello [встроенные magics IPython](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics), в том числе `%%sh`. Можно использовать hello `%%sh` магическая toorun сценарии и блока кода на головному узлу кластера hello.
   >
   >
2. **Автоматическая визуализация**. Hello **Pyspark** ядра автоматически визуализирует hello выходных данных Hive и SQL-запросов. Вы можете выбрать различные типы средства визуализации, включая таблицы, круговые диаграммы, графики, диаграммы с областями и линейчатые диаграммы.

## <a name="parameters-supported-with-hello-sql-magic"></a>Параметры, поддерживаемые с hello %% sql magic
Hello `%%sql` magic поддерживает различные параметры, которые можно использовать toocontrol hello тип выходных данных, которое появляется при выполнении запросов. Привет, в следующей таблице перечислены hello выходных данных.

| Параметр | Пример | Описание |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |Используйте этот параметр toopersist hello результат запроса hello в hello %% локального контекста Python как [Pandas](http://pandas.pydata.org/) кадр данных. Hello переменной hello кадр данных называется hello переменной имя. |
| -q |`-q` |Используйте этот tooturn off визуализации для hello ячейки. Если вы не хотите tooauto-визуализировать hello содержимого ячейки и просто хотят toocapture его как кадр данных, затем с помощью `-q -o <VARIABLE>`. Если требуется tooturn off визуализации без записи hello результаты (например, выполнение запроса SQL, таких как `CREATE TABLE` инструкции), используйте `-q` без указания `-o` аргумент. |
| -m |`-m <METHOD>` |Параметр **METHOD** имеет значение **take** или **sample** (по умолчанию используется значение **take**). Если метод hello **принимать**, hello ядра выбирает элементы сверху hello hello результирующего набора данных, заданные MAXROWS (описывается далее в этой таблице). Если метод hello **пример**, hello ядра выполняют случайную выборку элементов набора данных hello слишком в соответствии с`-r` параметра, описанные далее в этой таблице. |
| -r |`-r <FRACTION>` |Здесь **FRACTION** — это число с плавающей запятой от 0,0 до 1,0. Если метод образец hello hello SQL-запрос `sample`, а затем hello ядра выполняют случайную выборку hello заданную долю элементов hello hello результирующего набора можно. Например, если выполнить SQL-запрос с аргументами hello `-m sample -r 0.01`, а затем случайным образом выбирается hello результирующие строки % 1. |
| -n |`-n <MAXROWS>` |**MAXROWS** должно быть выражено целым числом. Hello ядра ограничивает hello число выходных строк слишком**MAXROWS**. Если **MAXROWS** является отрицательным числом, такие как **-1**, то hello количество строк в результирующем наборе hello не ограничено. |

**Пример**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

выше инструкция Hello hello следующие:

* Выбирает все записи из таблицы **hivesampletable**.
* Отключает автоматическую визуализацию, так как включает параметр -q.
* Так как мы используем `-m sample -r 0.1 -n 500` его выполняют случайную выборку 10% строк hello в hello hivesampletable и ограничения hello размер строк too500 hello результирующего набора.
* Наконец так как мы использовали `-o query2` также сохраняет выходные данные hello в кадр данных под именем **query2**.

## <a name="considerations-while-using-hello-new-kernels"></a>Рекомендации при использовании нового ядра hello

Независимо от ядра используется, если оставить hello портативные компьютеры под управлением потребляет ресурсы кластера hello.  С этими ядер, поскольку заданы контексты hello, просто выход из записных книжек hello завершать контекст hello и таким образом ресурсы кластера hello продолжить toobe используется. Рекомендуется toouse hello **закрыть и остановить** параметр из записной книжки hello **файл** меню, появляющемся при завершении использования hello ноутбук, который ликвидирует контекст hello и затем завершает работу hello записной книжке.     

## <a name="show-me-some-examples"></a>Примеры

При открытии записной книжке Jupyter, вы видите две папки на корневом уровне hello.

* Hello **PySpark** папка содержит примеры записных книжек hello, используйте новый **Python** ядра.
* Hello **Scala** папка содержит примеры записных книжек hello, используйте новый **Spark** ядра.

Можно открыть hello **00 - [чтения первое Знакомство] компоненты ядра Magic Spark** записной книжки из hello **PySpark** или **Spark** папки toolearn о различных magics hello доступны. Также можно использовать как hello другие примеры записных книжек доступен в разделе hello двух папок toolearn tooachieve различных сценариев с помощью записные книжки Jupyter с кластерами HDInsight Spark.

## <a name="where-are-hello-notebooks-stored"></a>Где хранятся записных книжек hello

Записные книжки Jupyter сохраняются в учетной записи хранилища toohello, связанные с кластером hello под hello **/HdiNotebooks** папки.  Портативные компьютеры, текстовые файлы и папки, создаваемые на основе внутри Jupyter доступны из учетной записи хранилища hello.  Например, при использовании Jupyter toocreate папку **myfolder** и записной книжке **myfolder/mynotebook.ipynb**, можно получить доступ к этой записной книжки в `/HdiNotebooks/myfolder/mynotebook.ipynb` в учетной записи хранилища hello.  Hello обратного также имеет значение true, то есть, при передаче записной книжке непосредственно учетной записи хранилища tooyour в `/HdiNotebooks/mynotebook1.ipynb`, записной книжки hello также будет видимым в Jupyter.  Портативные компьютеры оставаться в учетной записи хранилища hello даже после удаления кластера hello.

Hello способом, сохраняются в учетной записи хранилища toohello записных книжек совместим с HDFS. Таким образом, если вы SSH в кластер hello, которые можно использовать файл команды управления, как показано в следующий фрагмент кода hello:

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


Если имеются проблемы с доступом к учетной записи хранилища hello кластера hello, портативные компьютеры hello также сохраняются на головному узлу hello `/var/lib/jupyter`.

## <a name="supported-browser"></a>Поддерживаемый браузер

Записные книжки Jupyter, выполняемые в кластерах HDInsight Spark, поддерживаются только браузером Google Chrome.

## <a name="feedback"></a>Отзыв
новые версии ядра Hello находятся в развивается рабочей области и будет взрослых со временем. Кроме того, это может означать, что по мере развития этих ядер API могут измениться. Мы будем признательны вам за любые отзывы о работе с новыми ядрами. Это полезно при формировании hello окончательной версии этих ядер. Можно оставить ваши комментарии и отзывы под hello **комментарии** раздел hello нижней части этой статьи.

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
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)
