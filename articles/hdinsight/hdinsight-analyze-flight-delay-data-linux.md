---
title: "Анализ данных по задержке рейсов с помощью Hive в HDInsight — Azure | Документы Майкрософт"
description: "Узнайте, как анализировать данные о задержке рейсов с помощью Hive в HDInsight под управлением Linux, а затем экспортировать их в Базу данных SQL с помощью Sqoop."
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
ms.openlocfilehash: 8cdc19ac8a517b6d8eefabb5476a686aa252a332
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="6e806-103">Анализ данных о задержке рейсов с помощью Hive в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="6e806-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="6e806-104">Узнайте, как анализировать данные о задержке рейсов с помощью Hive в HDInsight под управлением Linux, а затем экспортировать их в Базу данных SQL Azure с помощью Sqoop.</span><span class="sxs-lookup"><span data-stu-id="6e806-104">Learn how to analyze flight delay data using Hive on Linux-based HDInsight then export the data to Azure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e806-105">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight, который использует Linux.</span><span class="sxs-lookup"><span data-stu-id="6e806-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="6e806-106">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="6e806-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6e806-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6e806-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="6e806-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6e806-108">Prerequisites</span></span>

* <span data-ttu-id="6e806-109">**Кластер HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="6e806-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="6e806-110">Действия для создания нового кластера HDInsight см. в статье [Руководство по Hadoop. Начало работы с Hadoop в HDInsight на платформе Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e806-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="6e806-111">**База данных SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="6e806-111">**Azure SQL Database**.</span></span> <span data-ttu-id="6e806-112">Вы используете базу данных SQL Azure в качестве конечного хранилища данных.</span><span class="sxs-lookup"><span data-stu-id="6e806-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="6e806-113">Если у вас еще нет базы данных SQL, см. статью [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e806-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="6e806-114">**Интерфейс командной строки Azure**.</span><span class="sxs-lookup"><span data-stu-id="6e806-114">**Azure CLI**.</span></span> <span data-ttu-id="6e806-115">Если вы еще не установили интерфейс командной строки Azure, см. статью [Установка Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6e806-115">If you have not installed the Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-the-flight-data"></a><span data-ttu-id="6e806-116">Скачивание данных о рейсах</span><span class="sxs-lookup"><span data-stu-id="6e806-116">Download the flight data</span></span>

1. <span data-ttu-id="6e806-117">Перейдите на страницу [бюро транспортной статистики при администрации по исследованиям и инновационным технологиям][rita-website].</span><span class="sxs-lookup"><span data-stu-id="6e806-117">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="6e806-118">На странице выберите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6e806-118">On the page, select the following values:</span></span>

   | <span data-ttu-id="6e806-119">Имя</span><span class="sxs-lookup"><span data-stu-id="6e806-119">Name</span></span> | <span data-ttu-id="6e806-120">Значение</span><span class="sxs-lookup"><span data-stu-id="6e806-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="6e806-121">Фильтр года</span><span class="sxs-lookup"><span data-stu-id="6e806-121">Filter Year</span></span> |<span data-ttu-id="6e806-122">2013</span><span class="sxs-lookup"><span data-stu-id="6e806-122">2013</span></span> |
   | <span data-ttu-id="6e806-123">Период фильтра</span><span class="sxs-lookup"><span data-stu-id="6e806-123">Filter Period</span></span> |<span data-ttu-id="6e806-124">Январь</span><span class="sxs-lookup"><span data-stu-id="6e806-124">January</span></span> |
   | <span data-ttu-id="6e806-125">Поля</span><span class="sxs-lookup"><span data-stu-id="6e806-125">Fields</span></span> |<span data-ttu-id="6e806-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="6e806-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="6e806-127">Очистите все остальные поля.</span><span class="sxs-lookup"><span data-stu-id="6e806-127">Clear all other fields</span></span> |

3. <span data-ttu-id="6e806-128">Щелкните элемент **Загрузить**.</span><span class="sxs-lookup"><span data-stu-id="6e806-128">Click **Download**.</span></span>

## <a name="upload-the-data"></a><span data-ttu-id="6e806-129">Передача данных</span><span class="sxs-lookup"><span data-stu-id="6e806-129">Upload the data</span></span>

1. <span data-ttu-id="6e806-130">Воспользуйтесь следующей командой, чтобы передать ZIP-файл в головной узел кластера HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6e806-130">Use the following command to upload the zip file to the HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="6e806-131">Замените **FILENAME** именем ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="6e806-131">Replace **FILENAME** with the name of the zip file.</span></span> <span data-ttu-id="6e806-132">Замените **USERNAME** именем для входа SSH для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e806-132">Replace **USERNAME** with the SSH login for the HDInsight cluster.</span></span> <span data-ttu-id="6e806-133">Замените CLUSTERNAME именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e806-133">Replace CLUSTERNAME with the name of the HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e806-134">Если для аутентификации входа посредством SSH используется пароль, будет предложено ввести пароль.</span><span class="sxs-lookup"><span data-stu-id="6e806-134">If you use a password to authenticate your SSH login, you are prompted for the password.</span></span> <span data-ttu-id="6e806-135">Если используется открытый ключ, может потребоваться использовать параметр `-i` и указать путь к соответствующему закрытому ключу.</span><span class="sxs-lookup"><span data-stu-id="6e806-135">If you used a public key, you may need to use the `-i` parameter and specify the path to the matching private key.</span></span> <span data-ttu-id="6e806-136">Например, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="6e806-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="6e806-137">После завершения передачи подключитесь к кластеру с помощью SSH:</span><span class="sxs-lookup"><span data-stu-id="6e806-137">Once the upload has completed, connect to the cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="6e806-138">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="6e806-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="6e806-139">После установления подключения используйте следующую команду, чтобы распаковать ZIP-файл:</span><span class="sxs-lookup"><span data-stu-id="6e806-139">Once connected, use the following to unzip the .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="6e806-140">Она извлекает CSV-файл, размер которого приблизительно 60 МБ.</span><span class="sxs-lookup"><span data-stu-id="6e806-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="6e806-141">Используйте следующую команду для создания каталога в хранилище HDInsight, затем скопируйте данный файл в этот каталог.</span><span class="sxs-lookup"><span data-stu-id="6e806-141">Use the following command to create a directory on HDInsight storage, and then copy the file to the directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-the-hiveql"></a><span data-ttu-id="6e806-142">Создание и запуск HiveQL</span><span class="sxs-lookup"><span data-stu-id="6e806-142">Create and run the HiveQL</span></span>

<span data-ttu-id="6e806-143">Выполните следующие действия для импорта данных из CSV-файла в таблицу Hive с именем **Delays**.</span><span class="sxs-lookup"><span data-stu-id="6e806-143">Use the following steps to import data from the CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="6e806-144">Для создания и редактирования нового файла **flightdelays.hql** выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="6e806-144">Use the following command to create and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="6e806-145">В качестве содержимого файла добавьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="6e806-145">Use the following text as the contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over the csv file
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
    -- The following lines describe the format and location of the file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop the delays table if it exists
    DROP TABLE delays;
    -- Create the delays table and populate it with data
    -- pulled in from the CSV file (via the external table defined previously)
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

2. <span data-ttu-id="6e806-146">Нажмите клавиши **CTRL+X**, а затем **Y** (Да) для сохранения файла.</span><span class="sxs-lookup"><span data-stu-id="6e806-146">To save the file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="6e806-147">Для запуска Hive и выполнения файла **flightdelays.hql** используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6e806-147">To start Hive and run the **flightdelays.hql** file, use the following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="6e806-148">В этом примере используется `localhost`, так как вы подключены к головному узлу кластера HDInsight, на котором выполняется HiveServer2.</span><span class="sxs-lookup"><span data-stu-id="6e806-148">In this example, `localhost` is used since you are connected to the head node of the HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="6e806-149">По завершении выполнения сценария __flightdelays.hql__ используйте следующую команду, чтобы открыть интерактивный сеанс Beeline:</span><span class="sxs-lookup"><span data-stu-id="6e806-149">Once the __flightdelays.hql__ script finishes running, use the following command to open an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="6e806-150">При появлении командной строки `jdbc:hive2://localhost:10001/>` используйте приведенный ниже запрос, чтобы извлечь информацию из импортированных данных о задержке рейсов.</span><span class="sxs-lookup"><span data-stu-id="6e806-150">When you receive the `jdbc:hive2://localhost:10001/>` prompt, use the following query to retrieve data from the imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="6e806-151">Вы получите список городов, рейсы в которых задержаны из-за погодных условий, а также среднее время задержки. Он будет сохранен в `/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="6e806-151">This query retrieves a list of cities that experienced weather delays, along with the average delay time, and save it to `/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="6e806-152">Позже Sqoop считает данные из этого расположения и экспортирует их в базу данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="6e806-152">Later, Sqoop reads the data from this location and export it to Azure SQL Database.</span></span>

6. <span data-ttu-id="6e806-153">Чтобы выйти из Beeline, введите `!quit` в командной строке.</span><span class="sxs-lookup"><span data-stu-id="6e806-153">To exit Beeline, enter `!quit` at the prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="6e806-154">Создание базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="6e806-154">Create a SQL Database</span></span>

<span data-ttu-id="6e806-155">Если у вас уже имеется база данных SQL, необходимо получить имя сервера.</span><span class="sxs-lookup"><span data-stu-id="6e806-155">If you already have a SQL Database, you must get the server name.</span></span> <span data-ttu-id="6e806-156">Его можно найти на [портале Azure](https://portal.azure.com), выбрав **Базы данных SQL** и применив фильтр по имени базы данных, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="6e806-156">You can find the server name in the [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on the name of the database you wish to use.</span></span> <span data-ttu-id="6e806-157">Имя сервера указано в столбце **СЕРВЕР** .</span><span class="sxs-lookup"><span data-stu-id="6e806-157">The server name is listed in the **SERVER** column.</span></span>

<span data-ttu-id="6e806-158">Если у вас еще нет базы данных SQL, создайте ее, ознакомившись с разделом [Руководство по базам данных SQL: создание базы данных SQL за несколько минут с помощью портала Azure](../sql-database/sql-database-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="6e806-158">If you do not already have a SQL Database, use the information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) to create one.</span></span> <span data-ttu-id="6e806-159">Сохраните имя сервера, используемое для базы данных.</span><span class="sxs-lookup"><span data-stu-id="6e806-159">Save the server name used for the database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="6e806-160">Создание таблицы базы данных SQL</span><span class="sxs-lookup"><span data-stu-id="6e806-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="6e806-161">Существует множество способов подключения к базе данных SQL и создания таблицы.</span><span class="sxs-lookup"><span data-stu-id="6e806-161">There are many ways to connect to SQL Database and create a table.</span></span> <span data-ttu-id="6e806-162">В приведенных ниже действиях используется [FreeTDS](http://www.freetds.org/) из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6e806-162">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="6e806-163">Используйте SSH для подключения к кластеру HDInsight под управлением Linux и выполните следующие действия в сеансе SSH.</span><span class="sxs-lookup"><span data-stu-id="6e806-163">Use SSH to connect to the Linux-based HDInsight cluster, and run the following steps from the SSH session.</span></span>

2. <span data-ttu-id="6e806-164">Используйте следующую команду для установки FreeTDS:</span><span class="sxs-lookup"><span data-stu-id="6e806-164">Use the following command to install FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="6e806-165">После установки используйте следующую команду для подключения к серверу базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6e806-165">Once the install completes, use the following command to connect to the SQL Database server.</span></span> <span data-ttu-id="6e806-166">Замените **serverName** именем сервера базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6e806-166">Replace **serverName** with the SQL Database server name.</span></span> <span data-ttu-id="6e806-167">Замените **adminLogin** и **adminPassword** именем для входа и паролем для базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="6e806-167">Replace **adminLogin** and **adminPassword** with the login for SQL Database.</span></span> <span data-ttu-id="6e806-168">Замените **databaseName** именем базы данных.</span><span class="sxs-lookup"><span data-stu-id="6e806-168">Replace **databaseName** with the database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="6e806-169">Должен появиться результат, аналогичный приведенному ниже тексту.</span><span class="sxs-lookup"><span data-stu-id="6e806-169">You receive output similar to the following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set to sqooptest
    1>
    ```

4. <span data-ttu-id="6e806-170">В командной строке `1>` введите следующее:</span><span class="sxs-lookup"><span data-stu-id="6e806-170">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="6e806-171">Если вводится инструкция `GO`, то оцениваются предыдущие инструкции.</span><span class="sxs-lookup"><span data-stu-id="6e806-171">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="6e806-172">Этот запрос создает таблицу **delays** с кластеризованным индексом.</span><span class="sxs-lookup"><span data-stu-id="6e806-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="6e806-173">Используйте следующий запрос команду для проверки создания таблицы.</span><span class="sxs-lookup"><span data-stu-id="6e806-173">Use the following query to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="6e806-174">Результат будет аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="6e806-174">The output is similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="6e806-175">Enter `exit` at the `1>` , чтобы выйти из служебной программы tsql.</span><span class="sxs-lookup"><span data-stu-id="6e806-175">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="6e806-176">Экспорт данных с помощью Sqoop</span><span class="sxs-lookup"><span data-stu-id="6e806-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="6e806-177">Чтобы проверить, видно ли в Sqoop базу данных SQL, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6e806-177">Use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="6e806-178">Эта команда выводит список баз данных, включая базу данных, в которой вы создали таблицу delays ранее.</span><span class="sxs-lookup"><span data-stu-id="6e806-178">This command returns a list of databases, including the database that you created the delays table in earlier.</span></span>

2. <span data-ttu-id="6e806-179">Для экспорта данных из hivesampletable в таблицу mobiledata используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="6e806-179">Use the following command to export data from hivesampletable to the mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="6e806-180">Sqoop подключается к базе данных, содержащей таблицу delays, и экспортирует данные из каталога `/tutorials/flightdelays/output` в эту таблицу.</span><span class="sxs-lookup"><span data-stu-id="6e806-180">Sqoop connects to the database containing the delays table, and exports data from the `/tutorials/flightdelays/output` directory to the delays table.</span></span>

3. <span data-ttu-id="6e806-181">После выполнения команды используйте следующую команду для подключения к базе данных с помощью TSQL:</span><span class="sxs-lookup"><span data-stu-id="6e806-181">After the command completes, use the following to connect to the database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="6e806-182">После установления подключения используйте следующие инструкции для проверки экспорта данных в таблицу mobiledata:</span><span class="sxs-lookup"><span data-stu-id="6e806-182">Once connected, use the following statements to verify that the data was exported to the mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="6e806-183">Вы увидите список данных в таблице.</span><span class="sxs-lookup"><span data-stu-id="6e806-183">You should see a listing of data in the table.</span></span> <span data-ttu-id="6e806-184">Введите `exit` для выхода из служебной программы tsql.</span><span class="sxs-lookup"><span data-stu-id="6e806-184">Type `exit` to exit the tsql utility.</span></span>

## <span data-ttu-id="6e806-185"><a id="nextsteps"></a> Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e806-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="6e806-186">Чтобы узнать больше о работе с данными в HDInsight, ознакомьтесь со следующими документами:</span><span class="sxs-lookup"><span data-stu-id="6e806-186">To learn more ways to work with data in HDInsight, see the following documents:</span></span>

* <span data-ttu-id="6e806-187">[Использование Hive с HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6e806-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="6e806-188">[Использование Oozie с HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="6e806-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="6e806-189">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="6e806-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="6e806-190">[Использование Pig с HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="6e806-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="6e806-191">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="6e806-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="6e806-192">[Разработка программ потоковой передачи на Python для HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="6e806-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
