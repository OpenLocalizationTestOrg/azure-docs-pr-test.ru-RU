---
title: "aaaUse Beeline с Apache Hive - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как запросы toouse hello Beeline клиента toorun Hive с Hadoop в HDInsight. Beeline — это служебная программа для работы с HiveServer2 через JDBC."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive,hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a>Использование клиента Beeline hello с Apache Hive

Узнайте, как toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) запрашивает toorun Hive в HDInsight.

Beeline является клиентом Hive, который включен в hello головного узла кластера HDInsight. Beeline использует tooHiveServer2 tooconnect JDBC, службы, размещенной в кластере HDInsight. Также можно использовать Beeline tooaccess Hive в HDInsight удаленно через Интернет hello. в следующей таблице Hello предоставляет строки подключения для использования с Beeline:

| Где запускается Beeline | Параметры |
| --- | --- | --- |
| SSH tooa головному узлу или край узел подключения | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| Вне кластера hello | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> Замените `admin` с учетной записью входа hello кластера для кластера.
>
> Замените `password` hello пароль для учетной записи входа hello кластера.
>
> Замените `clustername` с hello имя кластера HDInsight.

## <a id="prereq"></a>Предварительные требования

* Hadoop в кластере HDInsight на платформе Linux.

  > [!IMPORTANT]
  > Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* SSH-клиент или локальный клиент Beeline. Большая часть hello в данном пошаговом руководстве предполагается, что вы используете Beeline из кластера toohello сеансу SSH. Сведения о запуске Beeline из внешней hello кластера см. в разделе hello [удаленно использовать Beeline](#remote) раздела.

    Дополнительные сведения об использовании SSH см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="beeline"></a>Использование Beeline

1. При запуске Beeline необходимо указать строку подключения к HiveServer2 в кластере HDInsight. Команда hello toorun из внешней hello кластера, необходимо также указать имя учетной записи входа hello кластера (по умолчанию `admin`) и пароль. Используйте следующие таблицы toofind hello подключения строковое формат и параметры toouse hello.

    | Где запускается Beeline | Параметры |
    | --- | --- | --- |
    | SSH tooa головному узлу или край узел подключения | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | Вне кластера hello | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    Например hello следующую команду можно используется toostart Beeline из кластера toohello сеансу SSH:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    Эта команда запускает клиент Beeline hello и подключается tooHiveServer2 на головном узле кластера hello. После выполнения команды hello, будет выполнен переход на `jdbc:hive2://headnodehost:10001/>` строки.

2. Команды Beeline начинаются со знака `!`. Например, `!help` выводит справку. Здравствуйте, однако `!` может быть опущено для некоторых команд. Например, `help` также работает.

    Отсутствует `!sql`, который является HiveQL инструкции используемые tooexecute. Однако HiveQL активно используется, можно опустить hello выше `!sql`. Привет, следующие две инструкции эквивалентны:

    ```hiveql
    !sql show tables;
    show tables;
    ```

    В новом кластере отображена только одна таблица, **hivesampletable**.

3. Используйте следующие команды toodisplay hello схемы для hello hivesampletable hello:

    ```hiveql
    describe hivesampletable;
    ```

    Эта команда возвращает hello следующую информацию:

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    Описываются hello столбцов в таблице hello. Хотя мы удалось выполнить некоторые запросы к данным, вместо создадим новый toodemonstrate таблицы как tooload данных Hive и применить схему.

4. Введите следующие инструкции toocreate таблицу с именем hello **log4jLogs** , используя образцы данных с кластером HDInsight hello:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    Эти операторы выполняют hello, следующие действия:

    * `DROP TABLE`-Если hello таблица существует, она удаляется.

    * `CREATE EXTERNAL TABLE`. Создает **внешнюю** таблицу в Hive. Внешние таблицы в кусте хранить только определение таблицы hello. Hello данные остаются в исходном расположении hello.

    * `ROW FORMAT`-Способа форматирования данных hello. В этом случае hello полей в каждом журнале разделенные пробелом.

    * `STORED AS TEXTFILE LOCATION`— Там, где хранятся данные hello и какой формат файла.

    * `SELECT`-Выбор количество всех строк где столбца **t4** содержит значение hello **[ошибка]**. Этот запрос должен вернуть значение **3**, так как таблица содержит три строки с данным значением.

    * `INPUT__FILE__NAME LIKE '%.log'`-Hive попыток tooapply hello схемы tooall файлы в каталоге hello. В этом случае hello каталог содержит файлы, не соответствующие схеме hello. tooprevent данных сборки мусора в результатах hello, этот оператор указывает Hive, мы должны возвращать только данные из файлы которых заканчиваются. журнала.

  > [!NOTE]
  > Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника. Например, процессом автоматизированной передачи данных или другой операцией MapReduce.
  >
  > Удаление внешней таблицы **не** удаление данных hello, только определение таблицы hello.

    Hello выходные данные этой команды примерно toohello следующий текст:

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. использовать tooexit Beeline, `!exit`.

## <a id="file"></a>Используйте Beeline toorun файл HiveQL

Используйте следующие шаги toocreate файл, затем запустите его с помощью Beeline hello.

1. Используйте hello следующая команда toocreate файл с именем **query.hql**:

    ```bash
    nano query.hql
    ```

2. Используйте hello после текста как hello содержимое файла hello. Этот запрос создает "внутреннюю" таблицу **errorLogs**.

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    Эти операторы выполняют hello, следующие действия:

    * **Создание таблицы IF NOT EXISTS** -Если hello таблица еще не существует, он будет создан. С момента hello **ВНЕШНИХ** не используется ключевое слово, эта инструкция создает внутреннюю таблицу. Внутренние таблицы хранятся в хранилище данных Hive hello и полностью управляются Hive.
    * **ORC ХРАНИМОЙ AS** -хранит данные hello в оптимизированные строк по столбцам (формат ORC.). Это высокооптимизированный и эффективный формат для хранения данных Hive.
    * **INSERT OVERWRITE ... ВЫБЕРИТЕ** -выбирает строки из hello **log4jLogs** таблицы, которые содержат **[ошибка]**, а затем вставки данных hello в hello **журналы ошибок** таблицы.

    > [!NOTE]
    > В отличие от внешних таблиц при удалении внутренней таблицы удаляются hello базовые данные.

3. toosave hello файла, используйте **Ctrl**+**_X**, затем введите **Y**и, наконец, **ввод**.

4. Используйте следующие toorun hello файл с помощью Beeline hello.

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > Hello `-i` параметр начинает Beeline, выполняется hello инструкций в файле query.hql hello. После завершения выполнения запроса hello, будет выполнен переход на hello `jdbc:hive2://headnodehost:10001/>` строки. Можно также запустить файл с помощью hello `-f` параметр, который завершает работу Beeline после завершения выполнения запроса hello.

5. tooverify, hello **журналы ошибок** таблица была создана, используйте hello, следующая инструкция tooreturn Здравствуйте, все строки из **журналы ошибок**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    В результате операции должны быть возвращены три строки со значением **[ERROR]** в столбце t4.

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Удаленное использование Beeline

Если у вас есть Beeline, установленные локально или используете его до образа Docker такие как [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), необходимо использовать hello следующие параметры:

* __Строка подключения__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`.

* __Имя для входа на кластер__:`-n admin`.

* __Пароль для входа на кластер__: `-p 'password'`.

Замените hello `clustername` в строке подключения hello с hello имя кластера HDInsight.

Замените `admin` с именем hello входа кластера, а `password` с hello пароль для имени входа кластера.

## <a id="sparksql"></a>Использование Beeline со Spark

Spark обеспечивает собственную реализацию HiveServer2, который часто сервера Spark Thrift указанной tooas hello. Эта служба использует запросы tooresolve Spark SQL вместо Hive и может обеспечить более высокую производительность в зависимости от запроса.

Spark в кластер HDInsight, использование портов сервера Spark Thrift toohello tooconnect `10002` вместо `10001`. Например, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> Hello сервера Spark Thrift — не напрямую Здравствуйте, доступны через Интернет. Можно только подключение tooit из сеанса SSH или внутри hello одной виртуальной сети Azure, как hello кластера HDInsight.

## <a id="summary"></a><a id="nextsteps"></a>Дальнейшие действия

Дополнительные сведения о Hive в HDInsight см. следующий документ hello:

* [Использование Hive с Hadoop в HDInsight](hdinsight-use-hive.md)

Дополнительные сведения о том, как другие могут работать с Hadoop в HDInsight, см. следующие документы hello:

* [Использование Pig с Hadoop в HDInsight](hdinsight-use-pig.md)
* [Использование MapReduce с Hadoop в HDInsight](hdinsight-use-mapreduce.md)

Если вы используете Tez с Hive, см. следующие документы hello:

* [Использовать hello Tez пользовательского интерфейса на основе Windows HDInsight](hdinsight-debug-tez-ui.md)
* [Использовать hello Ambari Tez представление на основе Linux HDInsight](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
