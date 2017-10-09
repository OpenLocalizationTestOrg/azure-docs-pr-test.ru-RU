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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="fce8b-103">Анализ данных о задержке рейсов с помощью Hive в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="fce8b-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="fce8b-104">Узнайте, как задержки tooanalyze рейса данных с помощью Hive в HDInsight под управлением Linux, затем экспортировать tooAzure hello данных базы данных SQL с помощью Sqoop.</span><span class="sxs-lookup"><span data-stu-id="fce8b-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fce8b-105">Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="fce8b-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="fce8b-106">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="fce8b-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fce8b-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fce8b-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fce8b-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fce8b-108">Prerequisites</span></span>

* <span data-ttu-id="fce8b-109">**Кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fce8b-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="fce8b-110">Действия для создания нового кластера HDInsight см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fce8b-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="fce8b-111">**База данных SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="fce8b-111">**Azure SQL Database**.</span></span> <span data-ttu-id="fce8b-112">Вы используете базу данных SQL Azure в качестве конечного хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="fce8b-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="fce8b-113">Если у вас еще нет базы данных SQL, см. статью [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fce8b-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="fce8b-114">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="fce8b-114">**Azure CLI**.</span></span> <span data-ttu-id="fce8b-115">Если вы не установили hello Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) дополнительные шаги.</span><span class="sxs-lookup"><span data-stu-id="fce8b-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="fce8b-116">Загрузка данных рейса hello</span><span class="sxs-lookup"><span data-stu-id="fce8b-116">Download hello flight data</span></span>

1. <span data-ttu-id="fce8b-117">Обзор слишком[исследования и инновационные технологии администрирования бюро статистики Транспортировка][rita-website].</span><span class="sxs-lookup"><span data-stu-id="fce8b-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="fce8b-118">На странице приветствия выберите hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="fce8b-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="fce8b-119">Имя</span><span class="sxs-lookup"><span data-stu-id="fce8b-119">Name</span></span> | <span data-ttu-id="fce8b-120">Значение</span><span class="sxs-lookup"><span data-stu-id="fce8b-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="fce8b-121">Фильтр года</span><span class="sxs-lookup"><span data-stu-id="fce8b-121">Filter Year</span></span> |<span data-ttu-id="fce8b-122">2013</span><span class="sxs-lookup"><span data-stu-id="fce8b-122">2013</span></span> |
   | <span data-ttu-id="fce8b-123">Период фильтра</span><span class="sxs-lookup"><span data-stu-id="fce8b-123">Filter Period</span></span> |<span data-ttu-id="fce8b-124">Январь</span><span class="sxs-lookup"><span data-stu-id="fce8b-124">January</span></span> |
   | <span data-ttu-id="fce8b-125">Поля</span><span class="sxs-lookup"><span data-stu-id="fce8b-125">Fields</span></span> |<span data-ttu-id="fce8b-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="fce8b-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="fce8b-127">Очистите все остальные поля.</span><span class="sxs-lookup"><span data-stu-id="fce8b-127">Clear all other fields</span></span> |

3. <span data-ttu-id="fce8b-128">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="fce8b-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="fce8b-129">Передача данных hello</span><span class="sxs-lookup"><span data-stu-id="fce8b-129">Upload hello data</span></span>

1. <span data-ttu-id="fce8b-130">Используйте hello, следующая команда tooupload hello zip файл toohello HDInsight головного узла кластера.</span><span class="sxs-lookup"><span data-stu-id="fce8b-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="fce8b-131">Замените **FILENAME** с именем hello hello ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="fce8b-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="fce8b-132">Замените **USERNAME** с именем входа SSH hello hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fce8b-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="fce8b-133">Замените ИМЯ_КЛАСТЕРА hello имя кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fce8b-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fce8b-134">Если вы используете tooauthenticate пароль имени входа SSH, запрашивается пароль hello.</span><span class="sxs-lookup"><span data-stu-id="fce8b-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="fce8b-135">Если вы использовали открытого ключа, может потребоваться toouse hello `-i` параметр и указать toohello путь hello сопоставления закрытый ключ.</span><span class="sxs-lookup"><span data-stu-id="fce8b-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="fce8b-136">Например, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="fce8b-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="fce8b-137">После завершения отправки hello connect toohello кластера с помощью SSH:</span><span class="sxs-lookup"><span data-stu-id="fce8b-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="fce8b-138">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="fce8b-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="fce8b-139">После подключения используйте hello, следуя toounzip hello ZIP-файл:</span><span class="sxs-lookup"><span data-stu-id="fce8b-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="fce8b-140">Она извлекает CSV-файл, размер которого приблизительно 60 МБ.</span><span class="sxs-lookup"><span data-stu-id="fce8b-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="fce8b-141">Использовать hello, следующая команда toocreate каталог на HDInsight хранилища, а затем скопируйте каталог toohello hello файлов:</span><span class="sxs-lookup"><span data-stu-id="fce8b-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="fce8b-142">Создание и запуск hello HiveQL</span><span class="sxs-lookup"><span data-stu-id="fce8b-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="fce8b-143">Используйте hello следующие шаги tooimport данных из CSV-файла hello в таблицу Hive с именем **задержки**.</span><span class="sxs-lookup"><span data-stu-id="fce8b-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="fce8b-144">Используйте hello следующую команду toocreate и изменить новый файл с именем **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="fce8b-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="fce8b-145">Используйте hello после текста как hello содержимое этого файла:</span><span class="sxs-lookup"><span data-stu-id="fce8b-145">Use hello following text as hello contents of this file:</span></span>

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

2. <span data-ttu-id="fce8b-146">toosave hello файла, используйте **Ctrl + X**, затем **Y** .</span><span class="sxs-lookup"><span data-stu-id="fce8b-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="fce8b-147">toostart Hive и выполнения hello **flightdelays.hql** файла следует использовать hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fce8b-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="fce8b-148">В этом примере `localhost` используется, так как представляют подключенных toohello головного узла кластера HDInsight hello, являющийся запущенным HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="fce8b-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="fce8b-149">Здравствуйте, один раз __flightdelays.hql__ завершения, используйте hello следующая команда tooopen интерактивный сеанс Beeline сценария:</span><span class="sxs-lookup"><span data-stu-id="fce8b-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="fce8b-150">При получении hello `jdbc:hive2://localhost:10001/>` запрос, используйте следующую tooretrieve запроса данных из данных задержки рейсов hello импортированы hello.</span><span class="sxs-lookup"><span data-stu-id="fce8b-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="fce8b-151">Этот запрос извлекает список городов, задержек опытным погоды, вместе с hello среднего времени задержки и сохраните его слишком`/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="fce8b-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="fce8b-152">Позже Sqoop hello данные считываются из этого расположения и экспортируйте его tooAzure базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fce8b-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="fce8b-153">Введите tooexit Beeline, `!quit` в строке приветствия.</span><span class="sxs-lookup"><span data-stu-id="fce8b-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="fce8b-154">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="fce8b-154">Create a SQL Database</span></span>

<span data-ttu-id="fce8b-155">Если уже имеется база данных SQL, необходимо получить имя сервера hello.</span><span class="sxs-lookup"><span data-stu-id="fce8b-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="fce8b-156">Имя сервера hello можно найти в hello [портал Azure](https://portal.azure.com) , выбрав **баз данных SQL**, и последующей фильтрации по названию hello hello базы данных следует toouse.</span><span class="sxs-lookup"><span data-stu-id="fce8b-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="fce8b-157">Имя сервера Hello, перечисленные в hello **сервера** столбца.</span><span class="sxs-lookup"><span data-stu-id="fce8b-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="fce8b-158">Если вы еще нет базы данных SQL, используйте сведения hello в [SQL Database tutorial: Создание базы данных SQL в минутах](../sql-database/sql-database-get-started.md) toocreate один.</span><span class="sxs-lookup"><span data-stu-id="fce8b-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="fce8b-159">Сохраните hello имя сервера, используемое для hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="fce8b-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="fce8b-160">Создание таблицы базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="fce8b-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="fce8b-161">Существует много способов tooconnect tooSQL базы данных и создайте таблицу.</span><span class="sxs-lookup"><span data-stu-id="fce8b-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="fce8b-162">Здравствуйте, выполнив действия, используйте [FreeTDS](http://www.freetds.org/) из кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="fce8b-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="fce8b-163">Используйте кластера HDInsight под управлением Linux toohello tooconnect SSH, а также выполнения hello, выполнив действия из сеанса SSH hello.</span><span class="sxs-lookup"><span data-stu-id="fce8b-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="fce8b-164">Используйте следующие команды tooinstall FreeTDS hello.</span><span class="sxs-lookup"><span data-stu-id="fce8b-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="fce8b-165">После завершения установки hello используйте hello, следующая команда tooconnect toohello базы данных SQL server.</span><span class="sxs-lookup"><span data-stu-id="fce8b-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="fce8b-166">Замените **serverName** с hello имя сервера базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fce8b-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="fce8b-167">Замените **adminLogin** и **adminPassword** с именем входа hello для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="fce8b-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="fce8b-168">Замените **databaseName** с именем hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="fce8b-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="fce8b-169">Появится примерно toohello выходных данных после текста:</span><span class="sxs-lookup"><span data-stu-id="fce8b-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="fce8b-170">В hello `1>` введите hello следующие строки:</span><span class="sxs-lookup"><span data-stu-id="fce8b-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="fce8b-171">Здравствуйте, когда `GO` инструкция вводится, вычисляются hello предыдущих операторов.</span><span class="sxs-lookup"><span data-stu-id="fce8b-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="fce8b-172">Этот запрос создает таблицу **delays** с кластеризованным индексом.</span><span class="sxs-lookup"><span data-stu-id="fce8b-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="fce8b-173">Hello используйте следующий запрос tooverify, hello таблицы был создан:</span><span class="sxs-lookup"><span data-stu-id="fce8b-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="fce8b-174">Hello выходных данных аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="fce8b-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="fce8b-175">Введите `exit` в hello `1>` строки tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="fce8b-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="fce8b-176">Экспорт данных с помощью Sqoop</span><span class="sxs-lookup"><span data-stu-id="fce8b-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="fce8b-177">Используйте hello следующая команда tooverify, что Sqoop может просматривать базы данных SQL:</span><span class="sxs-lookup"><span data-stu-id="fce8b-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="fce8b-178">Эта команда возвращает список баз данных, включая hello созданную базу данных таблицы задержек hello в более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="fce8b-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="fce8b-179">Используйте следующие команды tooexport данные из таблицы mobiledata toohello hivesampletable hello.</span><span class="sxs-lookup"><span data-stu-id="fce8b-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="fce8b-180">Sqoop подключается toohello базы данных, содержащей таблицы задержек hello и экспортирует данные из hello `/tutorials/flightdelays/output` таблицы задержек toohello каталогов.</span><span class="sxs-lookup"><span data-stu-id="fce8b-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="fce8b-181">После завершения команды hello, используйте следующие toohello tooconnect базы данных, с помощью TSQL hello:</span><span class="sxs-lookup"><span data-stu-id="fce8b-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="fce8b-182">После подключения используйте следующие инструкции tooverify, что hello данные были экспортированного toohello mobiledata таблицы hello:</span><span class="sxs-lookup"><span data-stu-id="fce8b-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="fce8b-183">Вы увидите список данных в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="fce8b-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="fce8b-184">Тип `exit` tooexit hello tsql программы.</span><span class="sxs-lookup"><span data-stu-id="fce8b-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="fce8b-185"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fce8b-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="fce8b-186">см. Дополнительные способы toowork с данными в HDInsight, toolearn hello следующие документы:</span><span class="sxs-lookup"><span data-stu-id="fce8b-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="fce8b-187">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="fce8b-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="fce8b-188">[Использование Oozie с HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="fce8b-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="fce8b-189">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="fce8b-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="fce8b-190">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="fce8b-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="fce8b-191">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="fce8b-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="fce8b-192">[Разработка программ потоковой передачи на Python для HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="fce8b-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
