---
title: "tooSpark aaaIntroduction на Azure HDInsight | Документы Microsoft"
description: "Эта статья содержит общие сведения tooSpark на HDInsight и hello различных сценариев, в которых можно использовать кластер Spark в HDInsight."
keywords: "что такое apache spark, кластер spark, toospark введение spark в hdinsight"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>TooSpark введение в HDInsight

В этой статье предоставляются tooSpark введение в HDInsight. <a href="http://spark.apache.org/" target="_blank">Apache Spark</a> платформу параллельной обработки с открытым исходным кодом, поддерживающий в памяти обрабатывает tooboost hello производительность приложений для анализа больших данных. Кластер Spark в HDInsight совместим со службой хранилища Azure (WASB), а также с Azure Data Lake Store. Поэтому имеющиеся данные, хранящиеся в Azure, можно легко обработать с помощью кластера Spark.

При создании кластера Spark в HDInsight создание вычислительных ресурсов Azure следует выполнять после установки и настройки Spark. Это займет примерно каждые 10 минут, кластер toocreate Spark в HDInsight. обработано toobe данных Hello хранится в хранилище Azure или хранилища Озера данных Azure. Дополнительные сведения см. в статье [Использование HDFS-совместимой службы хранилища с Hadoop в HDInsight](hdinsight-hadoop-use-blob-storage.md).

**кластер toocreate Spark на HDInsight**, в разделе [краткое руководство: создать кластер Spark в HDInsight и выполнить интерактивный запрос с помощью Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>Apache Spark в Azure HDInsight
Кластеры Spark в HDInsight предлагают полностью управляемую службу Spark. Преимущества создания кластера Spark в HDInsight приведены здесь.

| Функция | Описание |
| --- | --- |
| Простота создания кластеров Spark |Можно создать новый кластер Spark на HDInsight в минутах, с помощью hello портал Azure, Azure PowerShell или hello HDInsight .NET SDK. См. инструкции по [началу работы с кластером Spark в HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md). |
| Простота использования |Кластер Spark в HDInsight включает записные книжки Jupyter и Zeppelin. Их можно использовать для интерактивной обработки и визуализации данных.|
| Интерфейсы API REST |Кластере Spark в HDInsight [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server), Spark на основе REST API задания сервера tooremotely монитора и отправки заданий. |
| Поддержка хранилища озера данных Azure | Кластер Spark на HDInsight может быть настроенный toouse хранилища Озера данных Azure как дополнительное хранилище, а также основного хранилища (только с кластерами HDInsight 3.5). Дополнительные сведения о Data Lake Store см. в [обзоре Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md). |
| Интеграция со службами Azure |Кластер Spark на HDInsight поставляется с tooAzure соединитель концентраторов событий. Клиентам создавать потоковую передачу приложений с помощью концентраторов событий hello, кроме слишком[Kafka](http://kafka.apache.org/), который уже доступен как часть Spark. |
| Поддержка R Server | Можно настроить R Server на кластере toorun распределенных вычислений R со скоростью hello, ожидаемая в кластере Spark в HDInsight Spark. Дополнительные сведения см. в статье [Приступая к работе с R Server в HDInsight](hdinsight-hadoop-r-server-get-started.md). |
| Интеграция со сторонними IDE | HDInsight предоставляет подключаемые модули для интегрированных средах разработки, как ПРЕДСТАВЛЕНИЕ IntelliJ и Eclipse, можно использовать toocreate и отправить tooan приложений кластера HDInsight Spark. Дополнительные сведения см. в статье [Создание приложений Spark для кластера HDInsight с помощью набора средств Azure для IntelliJ](hdinsight-apache-spark-intellij-tool-plugin.md) и [Создание приложений Spark для кластера HDInsight с помощью набора средств Azure для Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md).|
| Параллельные запросы |Кластеры Spark в HDInsight поддерживают параллельные запросы. Это позволяет несколько запросов из одного пользователя или несколько запросов от различных пользователей и приложений tooshare hello же ресурсов кластера. |
| Кэширование на накопители SSD |Можно выбрать toocache данных в памяти или в SSDs присоединен toohello узлов кластера. Кэширование в памяти обеспечивает наилучшую производительность запросов hello, но может быть затратной; кэширование в SSDs предоставляет отличный вариант для повышения производительности запросов без необходимости hello toocreate кластер размер, который является обязательным toofit hello весь набор данных в памяти. |
| Интеграция со средствами бизнес-аналитики |В состав кластеров Spark для HDInsight входят соединители для средств бизнес-аналитики, таких как [Power BI](http://www.powerbi.com/) и [Tableau](http://www.tableau.com/products/desktop) для анализа данных. |
| Предварительно загруженные библиотеки Anaconda |Кластеры Spark в HDInsight поставляются с предустановленными библиотеками Anaconda. [Anaconda](http://docs.continuum.io/anaconda/) предоставляет закрыть too200 библиотеки машинного обучения, анализа данных, визуализации и т. д. |
| Масштабируемость |Несмотря на то, что можно указать hello количество узлов кластера во время создания, может потребоваться toogrow или сжатие рабочей нагрузки toomatch hello кластера. Все кластеры HDInsight разрешить toochange hello количество узлов в кластере hello. Кроме того Spark кластеры могут быть удалены без потери данных все hello данные хранятся в хранилище Azure или хранилище Озера данных. |
| Круглосуточная и ежедневная поддержка |Для кластеров Spark в HDInsight предоставляется круглосуточная и ежедневная поддержка корпоративного уровня и соглашения об уровне обслуживания, гарантирующие время 99,9 % бесперебойной работы. |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>Что такое варианты использования hello Spark в HDInsight
Кластеры Spark в HDInsight включить следующие ключевые сценарии hello.

### <a name="interactive-data-analysis-and-bi"></a>Интерактивный анализ данных и бизнес-аналитика
[Учебник](hdinsight-apache-spark-use-bi-tools.md)

Apache Spark в HDInsight хранит данные в службе хранилища Azure или Azure Data Lake Store. Специалистам и принимающее бизнес-решения можно анализировать и создавать отчеты, к этим данным и использовать Microsoft Power BI toobuild интерактивные отчеты на основе данных анализа hello. Аналитики можно запустить из неструктурированных/semi структурированные данные в хранилище кластера, определение схемы для hello данных, с помощью ноутбуков и затем построения модели данных с использованием Microsoft Power BI. Кластеры Spark в HDInsight также поддерживают ряд средств бизнес-аналитики сторонних разработчиков, такие как Tableau, что делает Spark идеальной платформой для аналитиков, бизнес-экспертов и лиц, ответственных за принятие решений.

### <a name="spark-machine-learning"></a>Машинное обучение Spark
[Учебник. Прогнозирование температуры зданий с помощью данных системы кондиционирования](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[Учебник. Прогнозирование результатов контроля качества пищевых продуктов](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

В состав Apache Spark входит [MLlib](http://spark.apache.org/mllib/), библиотека машинного обучения, созданная на основе Spark, которую вы можете использовать из кластера Spark в HDInsight. Кластер Spark в HDInsight также включает библиотеку Anaconda, распространяемую Python и содержащую различные пакеты для машинного обучения. Все это дополнено встроенной поддержкой записных книжек Jupyter и Zeppelin — в итоге вы получаете в свое распоряжение первоклассную среду для создания приложений машинного обучения.

### <a name="spark-streaming-and-real-time-data-analysis"></a>Потоковая передача и анализ данных в режиме реального времени в Spark
[Учебник](hdinsight-apache-spark-eventhub-streaming.md)

Кластеры Spark в HDInsight обладают широкой поддержкой для создания решений для аналитики в режиме реального времени. Хотя Spark уже имеет соединители tooingest данные из многих источников, например сокеты Kafka, Flume, Twitter, ZeroMQ или TCP, Spark в HDInsight добавляет поддержку для получения данных из концентраторов событий Azure. Концентраторы событий — это hello наиболее широко используемых службы очередей в Azure. Встроенная поддержка концентраторов событий делает кластеры Spark в HDInsight идеальной платформой для создания конвейеров аналитики в режиме реального времени.

## <a name="next-steps"></a>Какие компоненты входят в состав кластера Spark?
Кластеры Spark в HDInsight включают следующие компоненты, доступные в кластерах hello по умолчанию hello.

* [Ядро Spark](https://spark.apache.org/docs/1.5.1/). Включает ядро Spark, Spark SQL, потоковые API-интерфейсы Spark, GraphX и MLlib.
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Записная книжка Jupyter](https://jupyter.org)
* [Записная книжка Zeppelin](http://zeppelin-project.org/)

Кластеры Spark на HDInsight также предоставляют [драйвер ODBC](http://go.microsoft.com/fwlink/?LinkId=616229) для подключения к tooSpark кластеров в HDInsight из средств бизнес-Аналитики, такие как Microsoft Power BI и Tableau.

## <a name="where-do-i-start"></a>С чего начать?
Начните с создания кластера Spark в HDInsight. Дополнительные сведения см. в статье [Начало работы. Создание кластера Apache Spark в Azure HDInsight и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="next-steps"></a>Дальнейшие действия
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
* [Использование подключаемого модуля средства HDInsight для toocreate ИДЕЯ IntelliJ и отправка Spark Scala основных приложений](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Удаленно использовать подключаемый модуль средства HDInsight для приложений Spark toodebug ИДЕЯ IntelliJ](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Использование записных книжек Zeppelin с кластером Spark в HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Ядра, доступные для записной книжки Jupyter в кластере Spark в HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Использование внешних пакетов с записными книжками Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Установка Jupyter на вашем компьютере и подключение tooan кластера HDInsight Spark](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Управление ресурсами
* [Управление ресурсами кластера hello Apache Spark в Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Отслеживание и отладка заданий в кластере Apache Spark в HDInsight на платформе Linux](hdinsight-apache-spark-job-debugging.md)
* [Известные проблемы в работе кластера Apache Spark в HDInsight](hdinsight-apache-spark-known-issues.md).
