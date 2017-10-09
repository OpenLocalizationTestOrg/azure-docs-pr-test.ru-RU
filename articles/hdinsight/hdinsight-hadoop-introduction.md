---
title: "aaaWhat, HDInsight, hello Hadoop технологии стек & кластеров? (Azure) | Документация Майкрософт"
description: "Введение tooHDInsight и hello Hadoop стека технологий и компонентов, включая Spark, Kafka, Hive, HBase для анализа больших данных."
keywords: "Azure hadoop, hadoop azure, начальный hadoop, введение hadoop, hadoop стека технологий, начальный toohadoop, toohadoop введение, какова кластера hadoop, что такое кластера hadoop hadoop для чего используется"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>Введение tooAzure HDInsight стека технологий Hadoop hello и кластеров Hadoop
 Эта статья содержит общие сведения tooAzure HDInsight, распределение облачные технологии стека hello Hadoop. Вы также узнаете, что такое кластер Hadoop и для чего он используется. 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>Что такое HDInsight и hello Hadoop технологическом стеке? 
Azure HDInsight — это распределение облака hello Hadoop компоненты из hello [Hortonworks Data Platform (HDP)](https://hortonworks.com/products/data-center/hdp/). [Apache Hadoop](http://hadoop.apache.org/) был hello исходного открытая платформа для распределенной обработки и анализа больших наборов данных на кластерах компьютеров. 


Hello Hadoop технологическом стеке включает программное обеспечение и служебные программы, включая Apache Hive, HBase, Spark, Kafka и многие другие. toosee доступных Hadoop технологии стек компонентов на HDInsight, в разделе [компоненты и доступны с HDInsight версии][component-versioning]. tooread Дополнительные сведения о Hadoop в HDInsight, в разделе hello [компоненты Azure страницы для HDInsight](https://azure.microsoft.com/services/hdinsight/).

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>Что такое кластер Hadoop и для чего его используют
Термин *Hadoop* также описывает тип кластера, который включает:

* YARN для планирования заданий и управления ресурсами.
* MapReduce для параллельной обработки.
* Здравствуйте, распределенная файловая система Hadoop (HDFS)
  
В большинстве случаев кластеры Hadoop используются для пакетной обработки хранимых данных. Другие типы кластеров в HDInsight включают дополнительные возможности. К примеру, популярность Spark выросла благодаря ускоренной обработке в памяти. Дополнительные сведения см. в разделе [Обзор экосистемы Hadoop в HDInsight](#overview).

## <a name="what-is-big-data"></a>Что такое данные большого объема?
Большие данные представляют любой большой массив цифровой информации, например:

* Данные датчиков промышленного оборудования.
* Действия клиентов, полученные с веб-сайта.
* Канал новостей Twitter.

Большие данные в различных форматах объединяются в большие тома с высокой скоростью обработки. Он может быть журнала (то есть хранящихся) или реального времени (то есть потоковой передачи из источника hello). 

## <a name="overview"></a>Типы кластеров в HDInsight
HDInsight включает определенные типы кластера и возможности его настройки, например добавление компонентов, служебных программ или языков.

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Типы кластеров Spark, Kafka, Interactive Hive, HBase, настраиваемые и другие типы
HDInsight предлагает следующие типы кластера hello.

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: использует [HDFS](#hdfs), [YARN](#yarn) управление ресурсами, а также простая [MapReduce](#mapreduce) tooprocess модели программирования и анализировать пакетные данные в параллельном режиме.
* **[Apache Spark](http://spark.apache.org/)**: платформа параллельной обработки, которая поддерживает обработки в памяти tooboost hello производительность приложений анализа больших данных, поместите здесь works для SQL, потоковой передачи данных и машинное обучение. Дополнительные сведения см. в статье [Обзор. Apache Spark в HDInsight](hdinsight-apache-spark-overview.md).
* **[Apache HBase](http://hbase.apache.org/)** — это база данных NoSQL, созданная на основе Hadoop и обеспечивающая прямой доступ и строгую согласованность для больших объемов неструктурированных и частично структурированных данных (с потенциальным размером таблиц в миллиарды строк и миллионы столбцов). Дополнительные сведения см. в статье [Что такое HBase в HDInsight: база данных NoSQL, которая предоставляет возможности, схожие BigTable, для Hadoop](hdinsight-hbase-overview.md).
* **[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)** — это сервер для размещения параллельных и распределенных процессов на языке R и управления ими. Он предоставляет специалистами по анализу данных, статистике и программисты R tooscalable доступ по запросу, распределенных методы анализа в HDInsight. Дополнительные сведения см. в статье [Общие сведения об R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-overview.md).
* **[Apache Storm](https://storm.incubator.apache.org/)** — это распределенная система для вычислений в реальном времени, позволяющая быстро обрабатывать потоки данных большого размера. Storm предлагается в качестве управляемого кластера в HDInsight. См. статью об [анализе данных, передаваемых датчиками в реальном времени, с помощью Storm и Hadoop](hdinsight-storm-sensor-data-analysis.md).
* **[Apache Interactive Hive (предварительная версия) (другое название — Live Long and Process)](https://cwiki.apache.org/confluence/display/Hive/LLAP)** выполняет кэширование в памяти для обеспечения интерактивных и ускоренных запросов Hive. См. статью [Использование Interactive Hive в HDInsight (предварительная версия)](hdinsight-hadoop-use-interactive-hive.md).
* **[Apache Kafka](https://kafka.apache.org/)** — это платформа с открытым исходным кодом, которая используется для создания конвейеров и приложений потоковой передачи данных. Kafka также предоставляет функциональные возможности очереди сообщений, позволяет вам toopublish и подписка toodata потоков. В разделе [tooApache введение Kafka на HDInsight](hdinsight-apache-kafka-introduction.md).

Можно также настроить кластеры, использующие hello следующие методы:
* **[Просмотр кластеров, присоединенных к домену](hdinsight-domain-joined-introduction.md)**: кластер быть присоединен к домену Active Directory tooan, можно управлять доступом и обеспечения управления для данных.
* **[Пользовательские кластеры с действиями скрипта](hdinsight-hadoop-customize-cluster-linux.md)** — это кластеры со скриптами, которые запускаются при подготовке кластера к работе и устанавливают дополнительные компоненты.

### <a name="example-cluster-customization-scripts"></a>Пример сценариев настройки кластеров
Действия сценариев, Bash-скриптов в Linux, которые выполняются во время подготовки кластера, а, может быть используется tooinstall дополнительные компоненты в кластере hello. 

Hello следующие образцы скриптов, предоставляемые командой HDInsight hello:

* **[Цветовой тон](hdinsight-hadoop-hue-linux.md)**: набор web toointeract приложений, используемых в кластере. Только кластеры Linux.
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**: Graph обработки toomodel связи между действия или людей.
* **[Solr](hdinsight-hadoop-solr-install-linux.md)** — это платформа корпоративного поиска, предоставляющая многофункциональные средства полнотекстового поиска данных.

Сведения о разработке собственных действий скриптов см. в статье [Разработка действий сценариев с помощью HDInsight](hdinsight-hadoop-script-actions-linux.md).

## <a name="components-and-utilities-on-hdinsight-clusters"></a>Компоненты и служебные программы в кластерах HDInsight
Hello следующие компоненты и служебные программы, включаются в кластерах HDInsight:

* **[Ambari](#ambari)**: подготовка, мониторинг кластеров и управление ими, служебные программы.
* **[Avro](#avro)**  (библиотека Microsoft .NET для Avro): сериализации данных для среды Microsoft .NET hello. 
* **[Hive и HCatalog](#hive)** — запросы, аналогичные SQL-запросам, а также уровень управления таблицами и хранилищами.
* **[Mahout](#mahout)** предназначен для масштабируемых приложений машинного обучения.
* **[MapReduce](#mapreduce)**: устаревшая платформа для распределенной системы обработки и управления ресурсами Hadoop. Дополнительные сведения см. в разделе [YARN](#yarn).
* **[Oozie](#oozie)**: управление рабочими процессами.
* **[Phoenix](#phoenix)**: уровень реляционной базы данных в HBase.
* **[Pig](#pig)**: более простое создание сценариев для преобразований MapReduce.
* **[Sqoop](#sqoop)**: импорт и экспорт данных.
* **[Tez](#tez)**: эффективно позволяет toorun процессов, интенсивно использующих данные в масштабе.
* **[YARN](#yarn)**: управление ресурсами, который входит в состав основной библиотеки hello Hadoop.
* **[ZooKeeper](#zookeeper)**: координация процессов в распределенных системах.

> [!NOTE]
> Сведения о конкретных компонентах hello и сведения о версии см. в разделе [Hadoop компоненты и их версии в HDInsight][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari используется для подготовки, отслеживания кластеров Apache Hadoop и управления ими. Содержит коллекцию интуитивно оператор средств и широкий набор API, которые скрывают сложность hello объекта Hadoop, упрощая операции hello кластеров. Кластеры HDInsight в Linux Укажите оба hello Ambari web пользовательского интерфейса и hello Ambari REST API. Представления Ambari в кластерах HDInsight позволяют использовать функции пользовательского интерфейса подключаемых модулей.
Дополнительные сведения см. в статье [Управление кластерами HDInsight с помощью веб-интерфейса Ambari](hdinsight-hadoop-manage-ambari.md) и в <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">справочнике по API Apache Ambari</a>.

### <a name="avro"></a>Avro (библиотека Microsoft .NET для Avro)
Библиотека Microsoft .NET для Avro Hello реализует формат обмена hello Apache Avro compact двоичные данные для сериализации для среды Microsoft .NET hello. Он определяет независимый от схемы язык, поэтому данные, сериализованные на одном языке, можно считать на другом. Можно найти подробные сведения о формате hello в hello < целевой объект = _ «blank» href = «http://avro.apache.org/docs/current/spec.html» > спецификация Apache Avro</a>. Формат Hello hello поддерживает файлов Avro распределенных MapReduce модели программирования: файлы являются «разбить таблицу», то есть можно приступить к чтению из определенного блока и поиска любой точки в файле. toofind о том, как, в разделе [сериализация данных с hello библиотеки Microsoft .NET для Avro](hdinsight-dotnet-avro-serialization.md). Toocome поддержки кластера под управлением Linux.

### <a name="hdfs"></a>HDFS
Системы распределенных файла Hadoop (HDFS) находится в файловой системе, с YARN и MapReduce, — основное hello технологии Hadoop. Он, hello стандартной файловой системы для кластеров Hadoop в HDInsight. Дополнительные сведения см. в статье [Использование HDFS-совместимой службы хранилища с Hadoop в HDInsight](hdinsight-hadoop-use-blob-storage.md).

### <a name="hive"></a>Hive и HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> данных программного обеспечения, встроенного в Hadoop, который позволяет вам tooquery в хранилище и управление большими наборами данных, в распределенном хранилище с помощью SQL-подобного языка, называется HiveQL. Как и Pig, Hive — это абстракция на основе MapReduce, преобразующая запросы в последовательность заданий MapReduce. Куст — подробный система управления реляционными базами данных tooa чем Pig и используется с более структурированных данных. Для неструктурированных данных Pig является лучшим выбором hello. См. статью [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md).

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a> — это уровень управления таблицами и хранилищами для Hadoop, который обеспечивает реляционное представление данных. В HCatalog можно считывать и записывать файлы в любом формате, который поддерживается Hive SerDe (сериализатор — десериализатор).

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a> — это библиотека алгоритмов машинного обучения, применяемых в Hadoop. С помощью принципы статистических данных, приложений обучения машины обучить toolearn систем на основе данных и toouse прошлое поведение будущих toodetermine результатов. См. статью [Создание списка рекомендуемых фильмов с использованием Apache Mahout и Hadoop в HDInsight](hdinsight-mahout.md).

### <a name="mapreduce"></a>MapReduce
MapReduce — hello framework предыдущих версий программного обеспечения для Hadoop для написания приложений toobatch процесс больших наборов данных в параллельном режиме. Задание MapReduce разбивает больших наборов данных и организует данные hello в пары "ключ значение", для обработки. Задания MapReduce выполняются в [YARN](#yarn). В разделе <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> в hello Hadoop вики-сайте.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a> — это система координации рабочих процессов, которая управляет заданиями Hadoop. Он интегрирован с hello Hadoop стека, а также поддерживает заданий Hadoop MapReduce, Pig, Hive и Sqoop. Он также может быть систему определенных tooa задания используется tooschedule, такую как Java программ или сценариев оболочки. См. статью [Использование Oozie с Hadoop для определения и выполнения рабочего процесса в HDInsight](hdinsight-use-oozie-linux-mac.md).

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a> — это уровень реляционной базы данных в HBase. Phoenix включает драйвер JDBC, который позволяет вам tooquery и управление таблицами SQL непосредственно. Phoenix преобразует запросы и другие инструкции в собственные вызовы API NoSQL — вместо использования MapReduce — что обеспечивает более быструю работу приложений на основе хранилищ NoSQL. См раздел [Использование Apache Phoenix и SQuirreL с кластерами HBase](hdinsight-hbase-phoenix-squirrel.md).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> высокого уровня платформой, которая позволяет вам tooperform сложные преобразования MapReduce с большими наборами данных с помощью простой язык сценариев, вызывается латиница Pig. Pig преобразует скрипты Pig латиница hello, что им будет выполняться в среде Hadoop. Можно создавать определяемые пользователем функции (UDF) tooextend Pig латиницы. См. статью [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a> — это инструмент, который обеспечивает оптимальную передачу данных большего объема между Hadoop и реляционными базами данных, такими как SQL, или другими структурированными хранилищами данных. См. статью [Использование Sqoop с Hadoop в HDInsight](hdinsight-use-sqoop.md).

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a> является платформой приложений, построенной на базе YARN Hadoop, которая выполняет сложные ациклические диаграммы обработки общих данных. Это более гибкими и мощными последователь toohello MapReduce платформу, которая позволяет ресурсоемких процессов, например Hive, toorun более эффективно в масштабе. См. раздел ["Использование Apache Tez для повышения производительности" в статье об использовании Hive и HiveQL](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Apache YARN hello следующего поколения MapReduce (MapReduce 2.0 или MRv2) и поддерживает сценарии обработки данных, чем MapReduce Пакетная обработка обеспечивает высокую масштабируемость и в режиме реального времени обработки. YARN включает диспетчер ресурсов и распределенную платформу приложений. Задания MapReduce выполняются в YARN. Дополнительные сведения о YARN см. на странице <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop YARN</a>.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a> координирует процессы в больших распределенных системах с помощью общего иерархического пространства имен регистров данных (z-узлов). Znodes содержит небольшое количество процессов toocoordinate сведения, необходимые метаданные: состояние, расположение, конфигурации и т. д. Ознакомьтесь с примером в статье [Использование Apache Phoenix с кластерами HBase под управлением Linux в HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md). 

## <a name="programming-languages-on-hdinsight"></a>Языки программирования, поддерживаемые в HDInsight
Кластеры HDInsight — Spark, HBase, Kafka, Hadoop и другие — поддерживают несколько языков программирования, но не все из них устанавливаются по умолчанию. Для библиотеки, модули и пакеты не устанавливаются по умолчанию [использовать компонент сценария tooinstall действие hello](hdinsight-hadoop-script-actions-linux.md). 

### <a name="default-programming-language-support"></a>Поддержка языков программирования по умолчанию
По умолчанию кластеры HDInsight поддерживают следующие языки:

* Java
* Python

Дополнительные языки можно установить с помощью [действий сценариев](hdinsight-hadoop-script-actions-linux.md).

### <a name="java-virtual-machine-jvm-languages"></a>Языки виртуальных машин Java
Многие языки, отличные от Java можно запускать на виртуальной машине Java (JVM); Тем не менее для выполнения некоторых из этих языков может потребоваться дополнительные компоненты, установленные на кластере hello.

В кластерах HDInsight поддерживаются следующие языки, использующие виртуальную машину Java:

* Clojure
* Jython (Python для Java)
* Scala

### <a name="hadoop-specific-languages"></a>Языки для Hadoop
Кластеры HDInsight поддерживают следующие языки, которые будут конкретных toohello Hadoop технологическом стеке hello:

* Pig Latin для заданий Pig
* HiveQL для заданий Hive и SparkSQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight "Стандартный" и HDInsight "Премиум"
HDInsight предлагает облачные решения для работы с большими данными в двух категориях: Стандартный и Премиум. HDInsight стандарт предоставляет кластер корпоративного уровня, организации могут использовать toorun их рабочих нагрузок больших данных. HDInsight уровня "Премиум" основан на выпуске "Стандартный" и предоставляет дополнительные возможности аналитики и защиты для кластера HDInsight. Дополнительные сведения см. в разделе об [HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium).

## <a name="microsoft-business-intelligence-and-hdinsight"></a>HDInsight и бизнес-аналитика Майкрософт
Средства знакомые бизнес-аналитики (BI) извлечения, анализа и интегрирована с HDInsight с помощью либо hello надстройка Power Query данные отчета или hello Hive Microsoft ODBC Driver:

* [Подключиться с помощью Power Query Excel tooHadoop](hdinsight-connect-excel-power-query.md): Узнайте, как Excel tooconnect toohello учетную запись хранилища Azure, в которой хранятся hello данные из кластера HDInsight с помощью Microsoft Power Query для Excel. Требуется рабочая станция Windows. 
* [Связь с hello Hive драйвер ODBC для Microsoft Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md): Узнайте, как данные tooimport из HDInsight с hello драйвер Microsoft ODBC Hive. Требуется рабочая станция Windows. 
* [Облачная платформа Майкрософт](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): Дополнительные сведения о Power BI для Office 365, загрузить пробную версию SQL Server hello и настройка SharePoint Server 2013 и бизнес-Аналитики SQL Server.
* [Руководства по службам Analysis Services (SSAS)](http://msdn.microsoft.com/library/hh231701.aspx)
* [Службы Reporting Services (SSRS)](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>Дальнейшие действия

* [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linuxt](hdinsight-hadoop-linux-tutorial-get-started.md): краткое руководство по подготовке кластеров HDInsight Hadoop и выполнению примеров запросов Hive.
* [Начало работы. Создание кластера Apache Spark в HDInsight на платформе Linux и выполнение интерактивных запросов с помощью SQL Spark](hdinsight-apache-spark-jupyter-spark-sql.md): краткое руководство по созданию кластера Spark и выполнению интерактивных запросов Spark SQL.
* [Приступая к работе с R Server в HDInsight (предварительная версия)](hdinsight-hadoop-r-server-get-started.md): начало работы с использованием R Server в HDInsight Premium.
* [Подготовка кластеров HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Узнайте, как hello tooprovision кластера HDInsight Hadoop через портал Azure, Azure PowerShell или Azure CLI.


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/