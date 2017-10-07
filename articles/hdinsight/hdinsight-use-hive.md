---
title: "aaaWhat — Apache Hive и HiveQL - Azure HDInsight | Документы Microsoft"
description: "Apache Hive — это система хранилища данных для Hadoop. Вы можете запрашивать данные, хранящиеся в кусте, с помощью HiveQL, аналогичные tooTransact-SQL. В этом документе, узнайте, как toouse Hive и HiveQL с Azure HDInsight."
keywords: "hiveql, какова куст hadoop hiveql hive, какова hive Узнайте, как toouse hive,"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>Обзор Apache Hive и HiveQL в Azure HDInsight

[Apache Hive](http://hive.apache.org/) — это система хранилища данных для Hadoop. Hive позволяет обобщать, запрашивать и анализировать данные. HiveQL, являющийся аналогичные tooSQL языка запросов языке запросов Hive.

Куст позволяет tooproject структуры в значительной степени неструктурированных данных. После определения структуры hello, можно использовать HiveQL tooquery hello данных без ведома Java или MapReduce.

HDInsight предоставляет несколько типов кластера, которые подходят для конкретных рабочих нагрузок. следующие типы кластера Hello чаще всего используются для запросов Hive:

* __Интерактивный куст__: кластера Hadoop, который предоставляет [Низкая задержка аналитической обработки (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) время ответа tooimprove функциональные возможности для интерактивной обработки запросов. Дополнительные сведения см. в разделе hello [начинаться с интерактивной Hive в HDInsight](hdinsight-hadoop-use-interactive-hive.md) документа.

* __Hadoop:__ кластер Hadoop, который предназначен для рабочих нагрузок пакетной обработки. Дополнительные сведения см. в разделе hello [начинаться с Hadoop в HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) документа.

* __Spark:__ Apache Spark содержит встроенные функциональные возможности для работы с Hive. Дополнительные сведения см. в разделе hello [начать с Spark в HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) документа.

* __HBase__: HiveQL может быть tooquery используемые данные, хранящиеся в HBase. Дополнительные сведения см. в разделе hello [начинаться с HBase на HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) документа.

## <a name="how-toouse-hive"></a>Как toouse Hive

Используйте следующие таблицы toodiscover как toouse Hive с HDInsight hello.

| **Используйте этот метод**, если требуется: | ... **интерактивная** оболочка | ...**пакетная** обработка | ...with этим **кластером операционной системы** | ...из этого **кластера операционной системы** |
|:--- |:---:|:---:|:--- |:--- |
| [Представление Hive](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |Для приложений на основе браузера |
| [клиент Beeline](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X или Windows |
| [REST API](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux или Windows* |Linux, Unix, Mac OS X или Windows |
| [Средства HDInsight для Visual Studio](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux или Windows* |Windows |
| [Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux или Windows* |Windows |

> [!IMPORTANT]
> \*Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> При использовании кластера HDInsight под управлением Windows, можно использовать hello [консоль запросов](hdinsight-hadoop-use-hive-query-console.md) из браузера или [удаленного рабочего стола](hdinsight-hadoop-use-hive-remote-desktop.md) toorun запросов Hive.

## <a name="hiveql-language-reference"></a>Справочник по языку HiveQL

Справочник по языку HiveQL доступен в hello [вручную языка (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).

## <a name="hive-and-data-structure"></a>Hive и структура данных

Куст понимает структуру toowork с и частично структурированных данных. Например текстовые файлы где hello поля разделены с определенных символов. Привет, следующем за инструкцией HiveQL создает таблицу данных, разделенных пробелами:

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

Hive также поддерживает пользовательские **сериализаторы/десериализаторы (SerDe)** для сложных или беспорядочно структурированных данных. Дополнительные сведения см. в разделе hello [как toouse пользовательские SerDe JSON с HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) документа.

Дополнительные сведения о форматах файлов, поддерживаемых куста см. в разделе hello [вручную языка (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>Сравнение внутренних и внешних таблиц Hive

Существует два типа таблиц, которые вы можете создать с помощью Hive:

* __Внутренняя__: данные хранятся в хранилище данных Hive hello. Hello хранилища данных находится в `/hive/warehouse/` на hello хранилища по умолчанию для кластера hello.

    Используйте внутренние таблицы, если:

    * данные являются временными;
    * Вы хотите куст toomanage hello жизненного цикла hello таблицы и данных.

* __Внешние__: данные хранятся за пределами hello хранилища данных. Hello данные могут храниться в хранилище, доступное кластером hello.

    Используйте внешние таблицы, если:

    * Hello данные также используются за пределами Hive. Например файлы данных hello обновляются другим процессом (который не блокирует файлы hello.)
    * Данные должны tooremain в базовый расположения, даже после удаления таблицы hello hello.
    * вам нужно пользовательское расположение, например нестандартная учетная запись хранилища;
    * Программа, отличная от hive управляет hello формат данных, расположение и т. д.

Дополнительные сведения см. в разделе hello [Hive внутренних и внешних таблиц начальный] [ cindygross-hive-tables] записи блога.

## <a name="user-defined-functions-udf"></a>Определяемые пользователем функции (UDF)

Инфраструктура Hive также может быть расширена с помощью **определяемых пользователем функций (UDF)**. Определяемая пользователем Функция позволяет tooimplement функциональность или логику, которая не легко моделируется в HiveQL. Пример использования определяемых пользователем функций с Hive см. следующие документы hello:

* [Работа с определяемыми пользователем функциями Java с использованием Hive в HDInsight](hdinsight-hadoop-hive-java-udf.md)

* [Использование пользовательских функций Python с Hive и Pig в Azure HDInsight](hdinsight-python.md)

* [Использование определяемых пользователем функций C# при потоковой передаче Hive и Pig в Hadoop HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Как tooadd пользовательские Hive определяемой пользователем функции tooHDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [Пример Hive определяемая пользователем функция tooconvert форматы даты и времени tooHive отметки времени](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>Демонстрационные данные

Hive в HDInsight поставляется предварительно загруженным с внутренней таблицей `hivesampletable`. HDInsight также предоставляет пример наборов данных, которые могут использоваться с Hive. Эти наборы данных хранятся в hello `/example/data` и `/HdiSamples` каталоги. Эти каталоги существуют в хранилище по умолчанию hello для кластера.

## <a id="job"></a>Пример запроса Hive

Здравствуйте, следующие столбцы проекта операторы HiveQL hello `/example/data/sample.log` файла:

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

В предыдущем примере hello hello HiveQL инструкции выполняют hello, следующие действия:

* `set hive.execution.engine=tez;`: Задает hello toouse ядра выполнения Tez. Использование Tez вместо MapReduce позволяет повысить производительность запросов. Дополнительные сведения о Tez см. в разделе hello [Tez Apache используется для повышения производительности](#usetez) раздела.

    > [!NOTE]
    > Эта инструкция необходима только при использовании кластера HDInsight под управлением Windows. Tez — подсистема выполнения по умолчанию hello для HDInsight под управлением Linux.

* `DROP TABLE`: Если hello таблица уже существует, удалите его.

* `CREATE EXTERNAL TABLE`: создает новую **внешнюю** таблицу в Hive. Внешние таблицы в кусте хранить только определение таблицы hello. Hello данных остается в исходном расположении hello и в исходном формате hello.

* `ROW FORMAT`: Указывает способ форматирования hello данных Hive. В этом случае hello полей в каждом журнале разделенные пробелом.

* `STORED AS TEXTFILE LOCATION`: Указывает Hive там, где hello хранения данных (hello `example/data` directory) и что он хранится в виде текста. Hello данные в одном файле или распределены по нескольким файлам в каталоге hello.

* `SELECT`: Выбирает число всех строк, где hello столбца **t4** содержит значение hello **[ошибка]**. Эта инструкция должна вернуть значение **3**, так как данное значение содержат три строки.

* `INPUT__FILE__NAME LIKE '%.log'`-Hive попыток tooapply hello схемы tooall файлы в каталоге hello. В этом случае hello каталог содержит файлы, не соответствующие схеме hello. tooprevent данных сборки мусора в результатах hello, этот оператор указывает Hive, мы должны возвращать только данные из файлы которых заканчиваются. журнала.

> [!NOTE]
> Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника. Например, процессом автоматизированной передачи данных или другой операцией MapReduce.
>
> Удаление внешней таблицы **не** удаление данных hello удаляет только определение таблицы hello.

toocreate **внутренней** вместо внешней таблицы, используйте следующие HiveQL hello:

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

Эти операторы выполняют hello, следующие действия:

* `CREATE TABLE IF NOT EXISTS`: Если hello таблица не существует, создайте его. Поскольку hello **ВНЕШНИХ** не используется ключевое слово, эта инструкция создает внутреннюю таблицу. Hello таблица хранится в хранилище данных Hive hello и полностью управляются Hive.

* `STORED AS ORC`: Хранит данные hello оптимизированными строк по столбцам (формат ORC.). Это высокооптимизированный и эффективный формат для хранения данных Hive.

* `INSERT OVERWRITE ... SELECT`: Выбирает строки из hello **log4jLogs** таблицу, содержащую **[ошибка]**, а затем вставляет hello данных в hello **журналы ошибок** таблицы.

> [!NOTE]
> В отличие от внешних таблиц удаление внутренней таблицы также будут удалены hello базовых данных.

## <a name="improve-hive-query-performance"></a>Повышение производительности запросов Hive

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org) — платформа, которая позволяет приложения с большим объемом данных, например Hive toorun гораздо эффективнее в масштабе. По умолчанию Tez включена для кластеров HDInsight под управлением Linux.

> [!NOTE]
> В настоящее время Tez по умолчанию отключена для кластеров HDInsight под управлением Windows. Необходимо включить эту платформу. для запроса Hive должны устанавливаться tootake преимуществами Tez hello следующие значения:
>
> `set hive.execution.engine=tez;`
>
> Tez — механизм по умолчанию hello для кластеров HDInsight под управлением Linux.

Hello [Hive в документах разработки Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) содержит подробные сведения о реализации вариантов hello и настройки конфигурации.

tooaid при отладке заданий выполнялась с использованием Tez, HDInsight предоставляет следующие пользовательских веб-интерфейсов, позволяющих tooview подробные сведения о заданиях Tez hello:

* [Использовать hello Ambari Tez представление на основе Linux HDInsight](hdinsight-debug-ambari-tez-view.md)

* [Использовать hello Tez пользовательского интерфейса на основе Windows HDInsight](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>Аналитическая обработка с низкой задержкой (LLAP)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (иногда называемая Live Long and Process) — это новая функция в Hive 2.0, которая разрешает кэширование запросов в памяти. LLAP делает запросы Hive значительно быстрее, копирование слишком[26 x быстрее, чем Hive 1.x в некоторых случаях](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).

HDInsight предоставляет LLAP hello тип интерактивный Hive кластера. Дополнительные сведения см. в разделе hello [начинаться с интерактивной Hive](hdinsight-hadoop-use-interactive-hive.md) документа.

## <a name="hive-jobs-and-sql-server-integration-services"></a>Задания Pig и SQL Server Integration Services

Можно использовать SQL Server Integration Services (SSIS) toorun задания Hive. пакет дополнительных компонентов Azure для служб SSIS Hello предоставляет следующие компоненты, которые работают с задания Hive в HDInsight hello.

* [Задача Hive в Azure HDInsight][hivetask]

* [Диспетчер подключений по подпискам Azure][connectionmanager]

Дополнительные сведения о hello пакет дополнительных компонентов Azure для служб SSIS [здесь][ssispack].

## <a id="nextsteps"></a>Дальнейшие действия

Теперь, когда вы узнали куст — и как toouse на Hadoop в HDInsight hello используйте следующие ссылки tooexplore toowork другими способами с Azure HDInsight.

* [Отправка данных tooHDInsight][hdinsight-upload-data]
* [Использование Pig с HDInsight][hdinsight-use-pig]
* [Использование заданий MapReduce с HDInsight][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
