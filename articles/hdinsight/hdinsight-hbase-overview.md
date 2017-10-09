---
title: "aaaWhat возможности Azure HDInsight HBase? | Документация Майкрософт"
description: "Введение tooApache HBase в HDInsight баз данных NoSQL сборки в Hadoop. Дополнительные сведения о вариантах использования и сравнение кластеров Hadoop tooother HBase."
keywords: "bigtable nosql, что такое hbase, apache hbase, hbase, обзор habase"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>Что такое HBase в HDInsight: база данных NoSQL, которая предоставляет возможности, схожие BigTable, для Hadoop
Apache HBase — это база данных NoSQL с открытым кодом, созданная на основе Hadoop и смоделированная после Google BigTable. HBase обеспечивает прямой доступ и строгую согласованность для больших объемов неструктурированных и слабоструктурированных данных, упорядоченных в семейства столбцов.

Данные хранятся в строках таблицы hello и группируются по семейства столбца данных в строке. HBase — schemaless базы данных в hello смысле, что ни один hello столбцов, ни тип данных, хранящиеся в них hello требуется toobe определенные перед их использованием. Hello открытый исходный код линейно масштабирует toohandle петабайт данных в тысячах узлов. Они могут использовать избыточность данных, пакетной обработки и другие возможности, предоставляемые распределенных приложений в экосистеме Hadoop hello.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>Как HBase реализована в Azure HDInsight?
HDInsight HBase предлагается в качестве управляемого кластера, который интегрирован в среду Azure hello. кластеры Hello, настроенных toostore данные непосредственно в [хранилища Azure](./hdinsight-hadoop-use-blob-storage.md) или [хранилища Озера данных Azure](./hdinsight-hadoop-use-data-lake-store.md), обеспечивающего низкой задержкой и повысить гибкость в производительности и стоимости вариантов. Это позволяет клиентам toobuild интерактивных веб-сайтов, работать с большими наборами данных, toobuild служб, сохраняющих данные датчика и телеметрии из миллионов конечных точек и tooanalyze этих данных с помощью заданий Hadoop. HBase и Hadoop являются приемлемыми отправная точка для больших данных проекта в Azure; в частности их можно включить toowork приложений в режиме реального времени с большими наборами данных.

Реализация Hello HDInsight использует hello масштабируемой архитектуры HBase tooprovide автоматического сегментирования таблиц, строгая согласованность операций чтения и записи и автоматической отработки отказа. Производительность повышается за счет кэширования операций чтения в памяти и потоковой записи с высокой пропускной способностью Также для HDInsight HBase доступна подготовка виртуальных сетей. Кластер HBase можно создать внутри виртуальной сети. Дополнительные сведения см. в статье [Создание кластеров HBase в виртуальной сети Azure][hbase-provision-vnet].

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>Как происходит управление данными в HDInsight HBase?
Можно управлять данными в HBase с помощью hello `create`, `get`, `put`, и `scan` команды из hello оболочки HBase. Данные записываются с помощью базы данных toohello `put` и чтения с помощью `get`. Hello `scan` команда является используется tooobtain данные из нескольких строк в таблице. Данные можно также управлять с помощью hello HBase C# API, который предоставляет клиентскую библиотеку поверх hello HBase REST API. Запросы к базе данных HBase также могут осуществляться с помощью Hive. Toothese введение, в модели программирования, в разделе [приступить к работе с базой HBase на Hadoop в HDInsight][hbase-get-started]. Совместное процессоров, также доступны, которая разрешает обработки данных в узлах hello, hello базы данных.

> [!NOTE]
> Thrift не поддерживается HBase в HDInsight.
>

## <a name="scenarios-use-cases-for-hbase"></a>Сценарии: варианты использования HBase
Hello вариант использования канонические, для которых BigTable (и по мере расширения HBase) был создан был поиск в Интернете. Поисковые системы построения индексов, которые сопоставляются условия toohello веб-страниц, содержащих их. Но есть много других вариантов использования, для которых подходит HBase; некоторые из них перечислены в этом разделе.

* Хранилище ключ-значение
  
    HBase можно использовать как хранилище пар «ключ-значение», оно подходит для управления системами обмена сообщениями. Facebook использует HBase для системы обмена сообщениями, она идеально подходит для хранения и управления интернет-коммуникациями. Таблицы WebTable использует toosearch HBase для и управление таблицами, которые извлекаются из веб-страниц.
* Данные от датчиков
  
    HBase удобно использовать для записи данных, накопленных при сборе из различных источников. К ним относятся социальные аналитики, временные ряды, обновления интерактивных информационных панели и счетчиков, а также управление системами ведения журналов аудита. Примеры включают Bloomberg trader терминалов и Привет открыть времени серии базу данных (OpenTSDB), которой хранятся и предоставляет доступ toometrics собранные об исправности hello серверных систем.
* Запросы в режиме реального времени
  
    [Phoenix](http://phoenix.apache.org/) система запросов SQL для Apache HBase. Доступ к системе осуществляется с помощью драйвера JDBC, она позволяет создавать запросы и управлять таблицами HBase с использованием SQL.
* HBase как платформа
  
    Поверх HBase могут выполняться приложения, используя ее как хранилище данных. Например, это используется в Phoenix, OpenTSDB, Kiji и Titan. Также возможна интеграция приложений с HBase. Примеры: Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia и Drill.

## <a name="next-steps"></a>Дальнейшие действия
* [Приступая к работе с HBase с Hadoop в HDInsight][hbase-get-started]
* [Создание кластеров HBase в виртуальной сети Azure][hbase-provision-vnet]
* [Настройка репликации HBase в HDInsight](hdinsight-hbase-replication.md)
* [Анализ мнений пользователей Twitter с использованием HBase в HDInsight][hbase-twitter-sentiment]
* [Используйте Maven toobuild Java приложений, использующих HBase с HDInsight (Hadoop)][hbase-build-java-maven]

## <a name="see-also"></a>Дополнительные материалы
* [Apache HBase](https://hbase.apache.org/)
* [Bigtable: распределенная система хранения структурированных данных](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
