---
title: "данные задержки рейсов aaaAnalyze с Hive в HDInsight - Azure | Документы Microsoft"
description: "Узнайте, как toouse Hive tooanalyze рейса данных на основе Linux HDInsight, а затем экспортировать tooSQL hello данных базы данных с помощью Sqoop."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Анализ данных о задержке рейсов с помощью Hive в HDInsight на платформе Linux

Узнайте, как задержки tooanalyze рейса данных с помощью Hive в HDInsight под управлением Linux, затем экспортировать tooAzure hello данных базы данных SQL с помощью Sqoop.

> [!IMPORTANT]
> Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux. Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней. Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="prerequisites"></a>Предварительные требования

* **Кластер HDInsight**. Действия для создания нового кластера HDInsight см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md).

* **База данных SQL Azure**. Вы используете базу данных SQL Azure в качестве конечного хранилища данных. Если у вас еще нет базы данных SQL, см. статью [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../sql-database/sql-database-get-started.md).

* **Azure CLI**. Если вы не установили hello Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) дополнительные шаги.

## <a name="download-hello-flight-data"></a>Загрузка данных рейса hello

1. Обзор слишком[исследования и инновационные технологии администрирования бюро статистики Транспортировка][rita-website].

2. На странице приветствия выберите hello следующие значения:

   | Имя | Значение |
   | --- | --- |
   | Фильтр года |2013 |
   | Период фильтра |Январь |
   | Поля |Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. Очистите все остальные поля. |

3. Щелкните элемент **Загрузить**.

## <a name="upload-hello-data"></a>Передача данных hello

1. Используйте hello, следующая команда tooupload hello zip файл toohello HDInsight головного узла кластера.

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    Замените **FILENAME** с именем hello hello ZIP-файла. Замените **USERNAME** с именем входа SSH hello hello кластера HDInsight. Замените ИМЯ_КЛАСТЕРА hello имя кластера HDInsight hello.

   > [!NOTE]
   > Если вы используете tooauthenticate пароль имени входа SSH, запрашивается пароль hello. Если вы использовали открытого ключа, может потребоваться toouse hello `-i` параметр и указать toohello путь hello сопоставления закрытый ключ. Например, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. После завершения отправки hello connect toohello кластера с помощью SSH:

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

3. После подключения используйте hello, следуя toounzip hello ZIP-файл:

    ```
    unzip FILENAME.zip
    ```

    Она извлекает CSV-файл, размер которого приблизительно 60 МБ.

4. Использовать hello, следующая команда toocreate каталог на HDInsight хранилища, а затем скопируйте каталог toohello hello файлов:

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>Создание и запуск hello HiveQL

Используйте hello следующие шаги tooimport данных из CSV-файла hello в таблицу Hive с именем **задержки**.

1. Используйте hello следующую команду toocreate и изменить новый файл с именем **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    Используйте hello после текста как hello содержимое этого файла:

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. toosave hello файла, используйте **Ctrl + X**, затем **Y** .

3. toostart Hive и выполнения hello **flightdelays.hql** файла следует использовать hello следующую команду:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > В этом примере `localhost` используется, так как представляют подключенных toohello головного узла кластера HDInsight hello, являющийся запущенным HiveServer2.

4. Здравствуйте, один раз __flightdelays.hql__ завершения, используйте hello следующая команда tooopen интерактивный сеанс Beeline сценария:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. При получении hello `jdbc:hive2://localhost:10001/>` запрос, используйте следующую tooretrieve запроса данных из данных задержки рейсов hello импортированы hello.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    Этот запрос извлекает список городов, задержек опытным погоды, вместе с hello среднего времени задержки и сохраните его слишком`/tutorials/flightdelays/output`. Позже Sqoop hello данные считываются из этого расположения и экспортируйте его tooAzure базы данных SQL.

6. Введите tooexit Beeline, `!quit` в строке приветствия.

## <a name="create-a-sql-database"></a>Создание базы данных SQL

Если уже имеется база данных SQL, необходимо получить имя сервера hello. Имя сервера hello можно найти в hello [портал Azure](https://portal.azure.com) , выбрав **баз данных SQL**, и последующей фильтрации по названию hello hello базы данных следует toouse. Имя сервера Hello, перечисленные в hello **сервера** столбца.

Если вы еще нет базы данных SQL, используйте сведения hello в [SQL Database tutorial: Создание базы данных SQL в минутах](../sql-database/sql-database-get-started.md) toocreate один. Сохраните hello имя сервера, используемое для hello базы данных.

## <a name="create-a-sql-database-table"></a>Создание таблицы базы данных SQL

> [!NOTE]
> Существует много способов tooconnect tooSQL базы данных и создайте таблицу. Здравствуйте, выполнив действия, используйте [FreeTDS](http://www.freetds.org/) из кластера HDInsight hello.


1. Используйте кластера HDInsight под управлением Linux toohello tooconnect SSH, а также выполнения hello, выполнив действия из сеанса SSH hello.

2. Используйте следующие команды tooinstall FreeTDS hello.

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. После завершения установки hello используйте hello, следующая команда tooconnect toohello базы данных SQL server. Замените **serverName** с hello имя сервера базы данных SQL. Замените **adminLogin** и **adminPassword** с именем входа hello для базы данных SQL. Замените **databaseName** с именем hello базы данных.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Появится примерно toohello выходных данных после текста:

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. В hello `1>` введите hello следующие строки:

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Здравствуйте, когда `GO` инструкция вводится, вычисляются hello предыдущих операторов. Этот запрос создает таблицу **delays** с кластеризованным индексом.

    Hello используйте следующий запрос tooverify, hello таблицы был создан:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Hello выходных данных аналогичные toohello следующий текст:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. Введите `exit` в hello `1>` строки tooexit hello tsql.

## <a name="export-data-with-sqoop"></a>Экспорт данных с помощью Sqoop

1. Используйте hello следующая команда tooverify, что Sqoop может просматривать базы данных SQL:

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    Эта команда возвращает список баз данных, включая hello созданную базу данных таблицы задержек hello в более ранних версий.

2. Используйте следующие команды tooexport данные из таблицы mobiledata toohello hivesampletable hello.

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop подключается toohello базы данных, содержащей таблицы задержек hello и экспортирует данные из hello `/tutorials/flightdelays/output` таблицы задержек toohello каталогов.

3. После завершения команды hello, используйте следующие toohello tooconnect базы данных, с помощью TSQL hello:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    После подключения используйте следующие инструкции tooverify, что hello данные были экспортированного toohello mobiledata таблицы hello:

    ```
    SELECT * FROM delays
    GO
    ```

    Вы увидите список данных в таблице hello. Тип `exit` tooexit hello tsql программы.

## <a id="nextsteps"></a> Дальнейшие действия

см. Дополнительные способы toowork с данными в HDInsight, toolearn hello следующие документы:

* [Использование Hive с HDInsight][hdinsight-use-hive]
* [Использование Oozie с HDInsight][hdinsight-use-oozie]
* [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]
* [Использование Pig с HDInsight][hdinsight-use-pig]
* [Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-mapreduce]
* [Разработка программ потоковой передачи на Python для HDInsight][hdinsight-develop-streaming]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
