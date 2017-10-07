---
title: "запросы aaaOptimize Hive в Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toooptimize вашей Hive запрашивает Hadoop в HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>Оптимизация запросов Hive в Azure HDInsight

По умолчанию производительность кластеров Hadoop не оптимизирована. В этой статье описываются некоторые наиболее распространенные Hive производительности оптимизации методы, могут быть применены tooyour запросов.

## <a name="scale-out-worker-nodes"></a>Горизонтальное масштабирование рабочих узлов

При увеличении числа hello рабочих узлов в кластере могут использовать дополнительные модули сопоставления и reducers toobe параллельного выполнения. Горизонтальное масштабирование в HDInsight можно выполнить двумя способами:

* Во время подготовки hello можно указать hello число рабочих узлов, используя hello портал Azure, Azure PowerShell или межплатформенного интерфейса командной строки.  Дополнительные сведения см. в статье [Создание кластеров Hadoop в HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Hello следующем снимке экрана показан рабочий hello конфигурации узла на портал Azure hello:
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* Во время выполнения hello можно масштабировать кластер без повторного создания один:

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

Дополнительные сведения о разных виртуальных машин hello поддерживается HDInsight см. в разделе [цены на HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="enable-tez"></a>Включение Tez

[Apache Tez](http://hortonworks.com/hadoop/tez/) — это ядро MapReduce альтернативных выполнения toohello ядра:

![tez_1][image-hdi-optimize-hive-tez_1]

Tez работает быстрее, так как:

* **Выполнение направленный ациклического графа (DAG) как единое задание MapReduce ядра hello**. Hello DAG требует каждого набора следуют один набор reducers toobe модули сопоставления. В этом случае несколько toobe заданий MapReduce, она появится для каждого запроса Hive. Tez не имеет такого ограничения и может обрабатывать сложные DAG как единое задание, тем самым  сводя к минимуму затраты на создание новых заданий.
* **Позволяет избежать ненужных операций записи.** Из-за toomultiple заданий она появится для hello того же запроса Hive подсистемы hello MapReduce, выходные данные каждого задания hello записывается tooHDFS для промежуточных данных. Поскольку Tez сводит к минимуму количество заданий для каждого запроса Hive, она будет может tooavoid ненужные записи.
* **Сводит к минимуму задержки при загрузке.** Tez — более высокую задержку при запуске может toominimize за счет сокращения числа hello модули сопоставления, необходимые toostart, а также улучшение оптимизацию во всей.
* **Повторно использует контейнеры.** Всякий раз, когда возможно Tez tooensure контейнеры могут tooreuse этой задержки из-за toostarting копирование контейнеры уменьшается.
* **Применяет методы непрерывной оптимизации.** Традиционно оптимизация выполняется на этапе компиляции. Однако можно найти дополнительные сведения о входных атрибутах hello, позволяющие лучше оптимизации во время выполнения. Tez используются методы непрерывной оптимизации, которые позволяет toooptimize дальнейшей hello плана на этап выполнения hello.

Дополнительные сведения об этих понятиях см. в документе об [Apache Tez](http://hortonworks.com/hadoop/tez/).

Можно выбрать любой запрос Hive Tez включена с помощью префикса hello запроса с параметром hello ниже:

    set hive.execution.engine=tez;

При подготовке кластеров HDInsight под управлением Linux платформа Tez включена по умолчанию.


## <a name="hive-partitioning"></a>Секционирование данных в Hive

Операции ввода-вывода является узким местом производительности основных hello для выполнения запросов Hive. Hello производительность можно повысить, если hello объем данных, которые должны toobe прочитать может быть уменьшен. По умолчанию запросы Hive просматривают все таблицы Hive. Это очень удобно для запросов, выполняющих сканирование таблиц. Однако для запросов, которым требуется только tooscan небольшой объем данных (например, запросы с фильтрацией), это поведение создает ненужные затраты. Куст секционирование позволяет Hive запросы tooaccess только hello необходимые объем данных в таблицах Hive.

Секционирование Hive реализуется путем реорганизации hello необработанных данных в новые каталоги с каждой секцией, имеющих свой собственный каталог - где определена секция hello пользователем hello. Hello следующая схема иллюстрирует секционирование таблицу Hive по столбцу hello *год*. Для каждого года создается новый каталог.

![Секционирование][image-hdi-optimize-hive-partitioning_1]

Некоторые рекомендации для выполнения секционирования:

* **Секций не должно быть слишком мало.** Секционирование по столбцам, содержащим только небольшое количество значений, может привести к малому количеству секций. Например, только секционирование по полу создает два toobe секции, созданные (Мужской» и «Женский), таким образом только уменьшить задержку hello, более половины.
* **Не увеличивайте секции** : В Здравствуйте другой стороны, Создание секции для столбца с уникальным значением (например, userid) вызывает несколько секций. Через секции вызывает объем нагрузки namenode hello кластера как с toohandle hello большое количество папок.
* **Избегайте неравномерного распределения данных** — выбирайте ключ секционирования рационально, таким образом, чтобы все секции были одинакового размера. Примером является секционирования на *состояние* может привести к hello число записей в Калифорнии toobe почти 30 x, Вермонт из-за разницы toohello в совокупности.

toocreate секции таблицы, используйте hello *секционированы по* предложения:

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

После создания секционированной таблицы hello, можно создать статическое разделение или динамическое секционирование.

* **Статическое разделение** означает, что имеется уже сегментированных данных в hello соответствующими каталоги и вы можете запросить Hive секций вручную по расположение каталога hello. Следующий фрагмент кода Hello приведен пример.
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **Динамическое секционирование** означает потребность автоматически куст toocreate секций для вас. Так как мы уже создали hello секционирование таблицы из промежуточной таблицы hello, нам нужно toodo всего таблицы секционированы toohello вставки данных:
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

Для получения дополнительных сведений обратитесь к разделу [Секционированные таблицы](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).

## <a name="use-hello-orcfile-format"></a>Используйте формат ORCFile hello
Hive поддерживает различные форматы. Например:

* **Текст**: это формат файла по умолчанию hello и работает с большинство сценариев
* **Avro**: хорошо подходит для сценариев взаимодействия
* **ORC/Parquet**: лучше всего подходит для повышения производительности

Формат ORC (оптимизированный строк по столбцам) является очень эффективным способом toostore данных Hive. Форматы сравниваемых tooother, ORC имеет hello следующие преимущества:

* поддержка сложных типов, включая даты и время и частично структурированные и сложные типы
* Сжатие % too70
* индексирует каждые 10 000 строк, что позволяет пропускать строки;
* обеспечивает существенное снижение времени выполнения запросов

Формат ORC tooenable, то сначала нужно создать таблицу с предложением hello *хранятся в виде ORC*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

Затем можно вставить таблицу ORC toohello данных из hello, Промежуточная таблица. Например:

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

Вы можете прочитать больше на формат ORC hello [здесь](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).

## <a name="vectorization"></a>Векторизация

Векторизации позволяет куст tooprocess пакет 1024 вместе строк вместо обработки одной строке за раз. Это означает, что простые операции выполняются быстрее, так как toorun требуется меньше внутреннего кода.

запрос Hive векторизации tooenable префикс hello следующий параметр:

    set hive.vectorized.execution.enabled = true;

Для получения дополнительных сведений обратитесь к разделу [Выполнение векторизованного запроса](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).

## <a name="other-optimization-methods"></a>Другие методы оптимизации
Существуют дополнительные методы оптимизации, которые также можно использовать, например:

* **Куст сегментацию:** технику, которая позволяет больших наборов данных производительности запросов toooptimize toocluster или сегмента.
* **Оптимизации соединения:** оптимизации выполнения запроса Hive планирование tooimprove hello эффективности соединений и уменьшают затраты hello указаний пользователя. Для получения дополнительных сведений обратитесь к разделу [Оптимизация объединений](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).
* **Увеличение модулей сжатия.**

## <a name="next-steps"></a>Дальнейшие действия
В этой статье вы узнали некоторые распространенные методы оптимизации запросов Hive. toolearn более, см. следующие статьи hello.

* [Использование Apache Hive в HDInsight](hdinsight-use-hive.md)
* [Анализ данных о задержке рейсов с помощью Hadoop в HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Анализ данных Twitter с помощью Hive в HDInsight](hdinsight-analyze-twitter-data.md)
* [Анализ данных датчика с помощью hello Hive консоль запросов в Hadoop в HDInsight](hdinsight-hive-analyze-sensor-data.md)
* [Используйте Hive в HDInsight tooanalyze журналы веб-сайтов](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
