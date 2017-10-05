---
title: "Использование клиента Beeline с Apache Hive в Azure HDInsight | Документация Майкрософт"
description: "Сведения о выполнении запросов Hive с помощью Hadoop в HDInsight с использованием клиента Beeline. Beeline — это служебная программа для работы с HiveServer2 через JDBC."
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
ms.openlocfilehash: 153044aafa3a67ee85bb1997beb821777c938563
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-beeline-client-with-apache-hive"></a><span data-ttu-id="0978c-105">Использование клиента Beeline с Apache Hive</span><span class="sxs-lookup"><span data-stu-id="0978c-105">Use the Beeline client with Apache Hive</span></span>

<span data-ttu-id="0978c-106">Узнайте, как использовать [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) для выполнения запросов Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0978c-106">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span></span>

<span data-ttu-id="0978c-107">Beeline — это клиент Hive, установленный на головных узлах кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0978c-107">Beeline is a Hive client that is included on the head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="0978c-108">Он подключается к службе HiveServer2, размещенной на кластере HDInsight, с помощью JDBC.</span><span class="sxs-lookup"><span data-stu-id="0978c-108">Beeline uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="0978c-109">Beeline также позволяет удаленно подключаться к Hive в HDInsight через Интернет.</span><span class="sxs-lookup"><span data-stu-id="0978c-109">You can also use Beeline to access Hive on HDInsight remotely over the internet.</span></span> <span data-ttu-id="0978c-110">В следующей таблице приведены строки подключения для Beeline.</span><span class="sxs-lookup"><span data-stu-id="0978c-110">The following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="0978c-111">Где запускается Beeline</span><span class="sxs-lookup"><span data-stu-id="0978c-111">Where you run Beeline from</span></span> | <span data-ttu-id="0978c-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="0978c-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0978c-113">SSH-подключение к головному или граничному узлу</span><span class="sxs-lookup"><span data-stu-id="0978c-113">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="0978c-114">Вне кластера</span><span class="sxs-lookup"><span data-stu-id="0978c-114">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="0978c-115">Замените `admin` учетной записью для входа в кластер.</span><span class="sxs-lookup"><span data-stu-id="0978c-115">Replace `admin` with the cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="0978c-116">Замените `password` паролем этой учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0978c-116">Replace `password` with the password for the cluster login account.</span></span>
>
> <span data-ttu-id="0978c-117">Замените `clustername` на имя вашего кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0978c-117">Replace `clustername` with the name of your HDInsight cluster.</span></span>

## <span data-ttu-id="0978c-118"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0978c-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="0978c-119">Hadoop в кластере HDInsight на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="0978c-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0978c-120">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="0978c-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0978c-121">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0978c-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="0978c-122">SSH-клиент или локальный клиент Beeline.</span><span class="sxs-lookup"><span data-stu-id="0978c-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="0978c-123">Большинство действий, описанных в этом руководстве, выполняются в клиенте Beeline из сеанса SSH в кластере.</span><span class="sxs-lookup"><span data-stu-id="0978c-123">Most of the steps in this document assume that you are using Beeline from an SSH session to the cluster.</span></span> <span data-ttu-id="0978c-124">Сведения о запуске Beeline вне кластера см. в разделе [Удаленное использование Beeline](#remote).</span><span class="sxs-lookup"><span data-stu-id="0978c-124">For information on running Beeline from outside the cluster, see the [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="0978c-125">Дополнительные сведения об использовании SSH см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0978c-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="0978c-126"><a id="beeline"></a>Использование Beeline</span><span class="sxs-lookup"><span data-stu-id="0978c-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="0978c-127">При запуске Beeline необходимо указать строку подключения к HiveServer2 в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0978c-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="0978c-128">Чтобы выполнить команду вне кластера, укажите также имя учетной записи (по умолчанию `admin`) и пароль для входа в кластер.</span><span class="sxs-lookup"><span data-stu-id="0978c-128">To run the command from outside the cluster, you must also provide the cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="0978c-129">Ниже приведена таблица с форматами строки подключения и необходимыми параметрами.</span><span class="sxs-lookup"><span data-stu-id="0978c-129">Use the following table to find the connection string format and parameters to use:</span></span>

    | <span data-ttu-id="0978c-130">Где запускается Beeline</span><span class="sxs-lookup"><span data-stu-id="0978c-130">Where you run Beeline from</span></span> | <span data-ttu-id="0978c-131">Параметры</span><span class="sxs-lookup"><span data-stu-id="0978c-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="0978c-132">SSH-подключение к головному или граничному узлу</span><span class="sxs-lookup"><span data-stu-id="0978c-132">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="0978c-133">Вне кластера</span><span class="sxs-lookup"><span data-stu-id="0978c-133">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="0978c-134">Например, следующая команда позволяет запустить Beeline из сеанса SSH в кластере:</span><span class="sxs-lookup"><span data-stu-id="0978c-134">For example, the following command can be used to start Beeline from an SSH session to the cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="0978c-135">Эта команда запускает клиент Beeline и подключает его к HiveServer2 на головном узле кластера.</span><span class="sxs-lookup"><span data-stu-id="0978c-135">This command starts the Beeline client, and connects to HiveServer2 on the cluster head node.</span></span> <span data-ttu-id="0978c-136">После выполнения команды отобразится командная строка `jdbc:hive2://headnodehost:10001/>`.</span><span class="sxs-lookup"><span data-stu-id="0978c-136">Once the command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="0978c-137">Команды Beeline начинаются со знака `!`. Например, `!help` выводит справку.</span><span class="sxs-lookup"><span data-stu-id="0978c-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="0978c-138">Однако в некоторых командах `!` можно опустить.</span><span class="sxs-lookup"><span data-stu-id="0978c-138">However the `!` can be omitted for some commands.</span></span> <span data-ttu-id="0978c-139">Например, `help` также работает.</span><span class="sxs-lookup"><span data-stu-id="0978c-139">For example, `help` also works.</span></span>

    <span data-ttu-id="0978c-140">Для выполнения инструкций HiveQL используется `!sql`.</span><span class="sxs-lookup"><span data-stu-id="0978c-140">There is a `!sql`, which is used to execute HiveQL statements.</span></span> <span data-ttu-id="0978c-141">Однако эти инструкции настолько распространены, что `!sql`тоже можно опустить.</span><span class="sxs-lookup"><span data-stu-id="0978c-141">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span></span> <span data-ttu-id="0978c-142">Приведенные ниже две инструкции эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="0978c-142">The following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="0978c-143">В новом кластере отображена только одна таблица, **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="0978c-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="0978c-144">Используйте следующую команду, чтобы отобразить схему для таблицы hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="0978c-144">Use the following command to display the schema for the hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="0978c-145">Эта команда возвращает приведенные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="0978c-145">This command returns the following information:</span></span>

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

    <span data-ttu-id="0978c-146">Они описывают столбцы в таблице.</span><span class="sxs-lookup"><span data-stu-id="0978c-146">This information describes the columns in the table.</span></span> <span data-ttu-id="0978c-147">Хотя мы можем выполнять отдельные запросы к этим данным, мы создадим новую таблицу, чтобы продемонстрировать загрузку данных в Hive и применение схемы.</span><span class="sxs-lookup"><span data-stu-id="0978c-147">While we could perform some queries against this data, let's instead create a brand new table to demonstrate how to load data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="0978c-148">Введите следующие инструкции, чтобы создать таблицу **log4jLogs**, используя демонстрационные данные, предоставляемые с кластером HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0978c-148">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="0978c-149">Эти операторы выполняют следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0978c-149">These statements perform the following actions:</span></span>

    * <span data-ttu-id="0978c-150">`DROP TABLE`. Если таблица уже создана, она будет удалена.</span><span class="sxs-lookup"><span data-stu-id="0978c-150">`DROP TABLE` - If the table exists, it is deleted.</span></span>

    * <span data-ttu-id="0978c-151">`CREATE EXTERNAL TABLE`. Создает **внешнюю** таблицу в Hive.</span><span class="sxs-lookup"><span data-stu-id="0978c-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="0978c-152">Внешние таблицы хранят только определения таблицы в Hive.</span><span class="sxs-lookup"><span data-stu-id="0978c-152">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="0978c-153">Данные остаются в исходном расположении.</span><span class="sxs-lookup"><span data-stu-id="0978c-153">The data is left in the original location.</span></span>

    * <span data-ttu-id="0978c-154">`ROW FORMAT` — настройка форматирования данных.</span><span class="sxs-lookup"><span data-stu-id="0978c-154">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="0978c-155">В данном случае поля всех журналов разделены пробелом.</span><span class="sxs-lookup"><span data-stu-id="0978c-155">In this case, the fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="0978c-156">`STORED AS TEXTFILE LOCATION`. Указывает расположение для хранения данных и их формат.</span><span class="sxs-lookup"><span data-stu-id="0978c-156">`STORED AS TEXTFILE LOCATION` - Where the data is stored and in what file format.</span></span>

    * <span data-ttu-id="0978c-157">`SELECT`. Подсчитывает количество строк, в которых столбец **t4** содержит значение **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="0978c-157">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="0978c-158">Этот запрос должен вернуть значение **3**, так как таблица содержит три строки с данным значением.</span><span class="sxs-lookup"><span data-stu-id="0978c-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="0978c-159">`INPUT__FILE__NAME LIKE '%.log'`. Hive пытается применить схему ко всем файлам в каталоге.</span><span class="sxs-lookup"><span data-stu-id="0978c-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="0978c-160">В этом случае каталог содержит файлы, которые не соответствуют схеме.</span><span class="sxs-lookup"><span data-stu-id="0978c-160">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="0978c-161">Чтобы исключить лишние данные в результатах, эта инструкция указывает Hive возвращать данные только из файлов, заканчивающихся на .log.</span><span class="sxs-lookup"><span data-stu-id="0978c-161">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0978c-162">Внешние таблицы следует использовать, если исходные данные должны обновляться с использованием внешних источников.</span><span class="sxs-lookup"><span data-stu-id="0978c-162">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="0978c-163">Например, процессом автоматизированной передачи данных или другой операцией MapReduce.</span><span class="sxs-lookup"><span data-stu-id="0978c-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="0978c-164">Удаление внешней таблицы **не** приводит к удалению данных, будет удалено только определение таблицы.</span><span class="sxs-lookup"><span data-stu-id="0978c-164">Dropping an external table does **not** delete the data, only the table definition.</span></span>

    <span data-ttu-id="0978c-165">После выполнения этой команды вы должны увидеть текст, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="0978c-165">The output of this command is similar to the following text:</span></span>

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

5. <span data-ttu-id="0978c-166">Чтобы выйти из Beeline, используйте инструкцию `!exit`.</span><span class="sxs-lookup"><span data-stu-id="0978c-166">To exit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="0978c-167"><a id="file"></a>Запуск файла HiveQL с помощью Beeline</span><span class="sxs-lookup"><span data-stu-id="0978c-167"><a id="file"></a>Use Beeline to run a HiveQL file</span></span>

<span data-ttu-id="0978c-168">Чтобы создать файл, а затем запустить его с помощью Beeline, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0978c-168">Use the following steps to create a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="0978c-169">Создайте файл **query.hql**, используя следующую команду.</span><span class="sxs-lookup"><span data-stu-id="0978c-169">Use the following command to create a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="0978c-170">В качестве содержимого файла добавьте следующий текст:</span><span class="sxs-lookup"><span data-stu-id="0978c-170">Use the following text as the contents of the file.</span></span> <span data-ttu-id="0978c-171">Этот запрос создает "внутреннюю" таблицу **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="0978c-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="0978c-172">Эти операторы выполняют следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0978c-172">These statements perform the following actions:</span></span>

    * <span data-ttu-id="0978c-173">**CREATE TABLE IF NOT EXISTS** — создание таблицы, если ее не существует.</span><span class="sxs-lookup"><span data-stu-id="0978c-173">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span></span> <span data-ttu-id="0978c-174">Так как не используется ключевое слово **EXTERNAL**, эта инструкция создает внутреннюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="0978c-174">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="0978c-175">Внутренние таблицы хранятся в хранилище данных Hive и полностью управляются Hive.</span><span class="sxs-lookup"><span data-stu-id="0978c-175">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="0978c-176">**STORED AS ORC** : хранение данных в формате ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="0978c-176">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="0978c-177">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="0978c-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="0978c-178">**INSERT OVERWRITE ... SELECT**: выбирает строки из таблицы **log4jLogs**, которые содержат значение **[ERROR]**, а затем вставляет данные в таблицу **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="0978c-178">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0978c-179">В отличие от внешних таблиц, удаление внутренней таблицы приводит к удалению базовых данных.</span><span class="sxs-lookup"><span data-stu-id="0978c-179">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

3. <span data-ttu-id="0978c-180">Чтобы сохранить файл, нажмите клавиши **CTRL**+**+X**, введите **Y** и нажмите клавишу **ВВОД**.</span><span class="sxs-lookup"><span data-stu-id="0978c-180">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="0978c-181">Запустите файл с помощью Beeline, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0978c-181">Use the following to run the file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="0978c-182">Параметр `-i` запускает Beeline и выполняет инструкции в файле query.hql.</span><span class="sxs-lookup"><span data-stu-id="0978c-182">The `-i` parameter starts Beeline, runs the statements in the query.hql file.</span></span> <span data-ttu-id="0978c-183">После выполнения запроса отобразится командная строка `jdbc:hive2://headnodehost:10001/>`.</span><span class="sxs-lookup"><span data-stu-id="0978c-183">Once the query completes, you arrive at the `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="0978c-184">Можно также выполнить файл с помощью параметра `-f`, который завершает работу Beeline после завершения выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="0978c-184">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span></span>

5. <span data-ttu-id="0978c-185">Чтобы убедиться, что таблица **errorLogs** создана, выполните приведенную ниже инструкцию (она выводит все строки из таблицы **errorLogs**).</span><span class="sxs-lookup"><span data-stu-id="0978c-185">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="0978c-186">В результате операции должны быть возвращены три строки со значением **[ERROR]** в столбце t4.</span><span class="sxs-lookup"><span data-stu-id="0978c-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="0978c-187"><a id="remote"></a>Удаленное использование Beeline</span><span class="sxs-lookup"><span data-stu-id="0978c-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="0978c-188">Если программа Beeline установлена локально или используется посредством образа Docker, например [sutoiku или beeline](https://hub.docker.com/r/sutoiku/beeline/), необходимо использовать следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="0978c-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use the following parameters:</span></span>

* <span data-ttu-id="0978c-189">__Строка подключения__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`.</span><span class="sxs-lookup"><span data-stu-id="0978c-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="0978c-190">__Имя для входа на кластер__:`-n admin`.</span><span class="sxs-lookup"><span data-stu-id="0978c-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="0978c-191">__Пароль для входа на кластер__: `-p 'password'`.</span><span class="sxs-lookup"><span data-stu-id="0978c-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="0978c-192">Замените `clustername` в строке подключения именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0978c-192">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span></span>

<span data-ttu-id="0978c-193">Замените `admin` именем для входа на кластер, а `password` — паролем этого имени для входа.</span><span class="sxs-lookup"><span data-stu-id="0978c-193">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span></span>

## <span data-ttu-id="0978c-194"><a id="sparksql"></a>Использование Beeline со Spark</span><span class="sxs-lookup"><span data-stu-id="0978c-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="0978c-195">Spark предоставляет собственную реализацию HiveServer2, также известную как сервер Thrift Spark.</span><span class="sxs-lookup"><span data-stu-id="0978c-195">Spark provides its own implementation of HiveServer2, which is often refered to as the Spark Thrift server.</span></span> <span data-ttu-id="0978c-196">Для разрешения запросов эта служба использует Spark SQL вместо Hive и может обеспечить более высокую производительность в зависимости от запроса.</span><span class="sxs-lookup"><span data-stu-id="0978c-196">This service uses Spark SQL to resolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="0978c-197">Чтобы подключиться к серверу Thrift Spark в кластере HDInsight, используйте порт `10002` вместо `10001`.</span><span class="sxs-lookup"><span data-stu-id="0978c-197">To connect to the Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="0978c-198">Например, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="0978c-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0978c-199">К серверу Thrift Spark невозможно получить доступ непосредственно через Интернет.</span><span class="sxs-lookup"><span data-stu-id="0978c-199">The Spark Thrift server is not directly accessible over the internet.</span></span> <span data-ttu-id="0978c-200">К нему можно подключиться только из сеанса SSH или из виртуальной сети Azure, в которой развернут кластер HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0978c-200">You can only connect to it from an SSH session or inside the same Azure Virtual Network as the HDInsight cluster.</span></span>

## <span data-ttu-id="0978c-201"><a id="summary"></a><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0978c-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="0978c-202">Дополнительные общие сведения об использовании Hadoop в HDInsight см. в следующем документе:</span><span class="sxs-lookup"><span data-stu-id="0978c-202">For more general information on Hive in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="0978c-203">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0978c-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="0978c-204">Дополнительные сведения о способах работы с Hadoop в HDInsight см. в следующих документах:</span><span class="sxs-lookup"><span data-stu-id="0978c-204">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="0978c-205">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0978c-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0978c-206">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0978c-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="0978c-207">Если вы используете Tez с Hive, ознакомьтесь со следующими документами:</span><span class="sxs-lookup"><span data-stu-id="0978c-207">If you are using Tez with Hive, see the following documents:</span></span>

* [<span data-ttu-id="0978c-208">Использование пользовательского интерфейса Tez в HDInsight на платформе Windows</span><span class="sxs-lookup"><span data-stu-id="0978c-208">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="0978c-209">Использование представления Ambari Tez в HDInsight на платформе Linux</span><span class="sxs-lookup"><span data-stu-id="0978c-209">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
