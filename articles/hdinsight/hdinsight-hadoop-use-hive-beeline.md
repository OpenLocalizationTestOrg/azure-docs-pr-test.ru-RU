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
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="67d06-105">Использование клиента Beeline hello с Apache Hive</span><span class="sxs-lookup"><span data-stu-id="67d06-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="67d06-106">Узнайте, как toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) запрашивает toorun Hive в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67d06-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="67d06-107">Beeline является клиентом Hive, который включен в hello головного узла кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67d06-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="67d06-108">Beeline использует tooHiveServer2 tooconnect JDBC, службы, размещенной в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67d06-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="67d06-109">Также можно использовать Beeline tooaccess Hive в HDInsight удаленно через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="67d06-110">в следующей таблице Hello предоставляет строки подключения для использования с Beeline:</span><span class="sxs-lookup"><span data-stu-id="67d06-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="67d06-111">Где запускается Beeline</span><span class="sxs-lookup"><span data-stu-id="67d06-111">Where you run Beeline from</span></span> | <span data-ttu-id="67d06-112">Параметры</span><span class="sxs-lookup"><span data-stu-id="67d06-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67d06-113">SSH tooa головному узлу или край узел подключения</span><span class="sxs-lookup"><span data-stu-id="67d06-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="67d06-114">Вне кластера hello</span><span class="sxs-lookup"><span data-stu-id="67d06-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="67d06-115">Замените `admin` с учетной записью входа hello кластера для кластера.</span><span class="sxs-lookup"><span data-stu-id="67d06-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="67d06-116">Замените `password` hello пароль для учетной записи входа hello кластера.</span><span class="sxs-lookup"><span data-stu-id="67d06-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="67d06-117">Замените `clustername` с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67d06-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="67d06-118"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="67d06-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="67d06-119">Hadoop в кластере HDInsight на платформе Linux.</span><span class="sxs-lookup"><span data-stu-id="67d06-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="67d06-120">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="67d06-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="67d06-121">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="67d06-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="67d06-122">SSH-клиент или локальный клиент Beeline.</span><span class="sxs-lookup"><span data-stu-id="67d06-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="67d06-123">Большая часть hello в данном пошаговом руководстве предполагается, что вы используете Beeline из кластера toohello сеансу SSH.</span><span class="sxs-lookup"><span data-stu-id="67d06-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="67d06-124">Сведения о запуске Beeline из внешней hello кластера см. в разделе hello [удаленно использовать Beeline](#remote) раздела.</span><span class="sxs-lookup"><span data-stu-id="67d06-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="67d06-125">Дополнительные сведения об использовании SSH см. в разделе [Подключение к HDInsight (Hadoop) с помощью SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="67d06-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="67d06-126"><a id="beeline"></a>Использование Beeline</span><span class="sxs-lookup"><span data-stu-id="67d06-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="67d06-127">При запуске Beeline необходимо указать строку подключения к HiveServer2 в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67d06-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="67d06-128">Команда hello toorun из внешней hello кластера, необходимо также указать имя учетной записи входа hello кластера (по умолчанию `admin`) и пароль.</span><span class="sxs-lookup"><span data-stu-id="67d06-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="67d06-129">Используйте следующие таблицы toofind hello подключения строковое формат и параметры toouse hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="67d06-130">Где запускается Beeline</span><span class="sxs-lookup"><span data-stu-id="67d06-130">Where you run Beeline from</span></span> | <span data-ttu-id="67d06-131">Параметры</span><span class="sxs-lookup"><span data-stu-id="67d06-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="67d06-132">SSH tooa головному узлу или край узел подключения</span><span class="sxs-lookup"><span data-stu-id="67d06-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="67d06-133">Вне кластера hello</span><span class="sxs-lookup"><span data-stu-id="67d06-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="67d06-134">Например hello следующую команду можно используется toostart Beeline из кластера toohello сеансу SSH:</span><span class="sxs-lookup"><span data-stu-id="67d06-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="67d06-135">Эта команда запускает клиент Beeline hello и подключается tooHiveServer2 на головном узле кластера hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="67d06-136">После выполнения команды hello, будет выполнен переход на `jdbc:hive2://headnodehost:10001/>` строки.</span><span class="sxs-lookup"><span data-stu-id="67d06-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="67d06-137">Команды Beeline начинаются со знака `!`. Например, `!help` выводит справку.</span><span class="sxs-lookup"><span data-stu-id="67d06-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="67d06-138">Здравствуйте, однако `!` может быть опущено для некоторых команд.</span><span class="sxs-lookup"><span data-stu-id="67d06-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="67d06-139">Например, `help` также работает.</span><span class="sxs-lookup"><span data-stu-id="67d06-139">For example, `help` also works.</span></span>

    <span data-ttu-id="67d06-140">Отсутствует `!sql`, который является HiveQL инструкции используемые tooexecute.</span><span class="sxs-lookup"><span data-stu-id="67d06-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="67d06-141">Однако HiveQL активно используется, можно опустить hello выше `!sql`.</span><span class="sxs-lookup"><span data-stu-id="67d06-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="67d06-142">Привет, следующие две инструкции эквивалентны:</span><span class="sxs-lookup"><span data-stu-id="67d06-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="67d06-143">В новом кластере отображена только одна таблица, **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="67d06-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="67d06-144">Используйте следующие команды toodisplay hello схемы для hello hivesampletable hello:</span><span class="sxs-lookup"><span data-stu-id="67d06-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="67d06-145">Эта команда возвращает hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="67d06-145">This command returns hello following information:</span></span>

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

    <span data-ttu-id="67d06-146">Описываются hello столбцов в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="67d06-147">Хотя мы удалось выполнить некоторые запросы к данным, вместо создадим новый toodemonstrate таблицы как tooload данных Hive и применить схему.</span><span class="sxs-lookup"><span data-stu-id="67d06-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="67d06-148">Введите следующие инструкции toocreate таблицу с именем hello **log4jLogs** , используя образцы данных с кластером HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="67d06-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="67d06-149">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="67d06-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="67d06-150">`DROP TABLE`-Если hello таблица существует, она удаляется.</span><span class="sxs-lookup"><span data-stu-id="67d06-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="67d06-151">`CREATE EXTERNAL TABLE`. Создает **внешнюю** таблицу в Hive.</span><span class="sxs-lookup"><span data-stu-id="67d06-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="67d06-152">Внешние таблицы в кусте хранить только определение таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="67d06-153">Hello данные остаются в исходном расположении hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="67d06-154">`ROW FORMAT`-Способа форматирования данных hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="67d06-155">В этом случае hello полей в каждом журнале разделенные пробелом.</span><span class="sxs-lookup"><span data-stu-id="67d06-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="67d06-156">`STORED AS TEXTFILE LOCATION`— Там, где хранятся данные hello и какой формат файла.</span><span class="sxs-lookup"><span data-stu-id="67d06-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="67d06-157">`SELECT`-Выбор количество всех строк где столбца **t4** содержит значение hello **[ошибка]**.</span><span class="sxs-lookup"><span data-stu-id="67d06-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="67d06-158">Этот запрос должен вернуть значение **3**, так как таблица содержит три строки с данным значением.</span><span class="sxs-lookup"><span data-stu-id="67d06-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="67d06-159">`INPUT__FILE__NAME LIKE '%.log'`-Hive попыток tooapply hello схемы tooall файлы в каталоге hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="67d06-160">В этом случае hello каталог содержит файлы, не соответствующие схеме hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="67d06-161">tooprevent данных сборки мусора в результатах hello, этот оператор указывает Hive, мы должны возвращать только данные из файлы которых заканчиваются. журнала.</span><span class="sxs-lookup"><span data-stu-id="67d06-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="67d06-162">Внешние таблицы следует использовать, если ожидается hello toobe базовых данных обновлены из внешнего источника.</span><span class="sxs-lookup"><span data-stu-id="67d06-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="67d06-163">Например, процессом автоматизированной передачи данных или другой операцией MapReduce.</span><span class="sxs-lookup"><span data-stu-id="67d06-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="67d06-164">Удаление внешней таблицы **не** удаление данных hello, только определение таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="67d06-165">Hello выходные данные этой команды примерно toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="67d06-165">hello output of this command is similar toohello following text:</span></span>

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

5. <span data-ttu-id="67d06-166">использовать tooexit Beeline, `!exit`.</span><span class="sxs-lookup"><span data-stu-id="67d06-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="67d06-167"><a id="file"></a>Используйте Beeline toorun файл HiveQL</span><span class="sxs-lookup"><span data-stu-id="67d06-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="67d06-168">Используйте следующие шаги toocreate файл, затем запустите его с помощью Beeline hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="67d06-169">Используйте hello следующая команда toocreate файл с именем **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="67d06-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="67d06-170">Используйте hello после текста как hello содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="67d06-171">Этот запрос создает "внутреннюю" таблицу **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="67d06-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="67d06-172">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="67d06-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="67d06-173">**Создание таблицы IF NOT EXISTS** -Если hello таблица еще не существует, он будет создан.</span><span class="sxs-lookup"><span data-stu-id="67d06-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="67d06-174">С момента hello **ВНЕШНИХ** не используется ключевое слово, эта инструкция создает внутреннюю таблицу.</span><span class="sxs-lookup"><span data-stu-id="67d06-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="67d06-175">Внутренние таблицы хранятся в хранилище данных Hive hello и полностью управляются Hive.</span><span class="sxs-lookup"><span data-stu-id="67d06-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="67d06-176">**ORC ХРАНИМОЙ AS** -хранит данные hello в оптимизированные строк по столбцам (формат ORC.).</span><span class="sxs-lookup"><span data-stu-id="67d06-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="67d06-177">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="67d06-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="67d06-178">**INSERT OVERWRITE ... ВЫБЕРИТЕ** -выбирает строки из hello **log4jLogs** таблицы, которые содержат **[ошибка]**, а затем вставки данных hello в hello **журналы ошибок** таблицы.</span><span class="sxs-lookup"><span data-stu-id="67d06-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="67d06-179">В отличие от внешних таблиц при удалении внутренней таблицы удаляются hello базовые данные.</span><span class="sxs-lookup"><span data-stu-id="67d06-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="67d06-180">toosave hello файла, используйте **Ctrl**+**_X**, затем введите **Y**и, наконец, **ввод**.</span><span class="sxs-lookup"><span data-stu-id="67d06-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="67d06-181">Используйте следующие toorun hello файл с помощью Beeline hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="67d06-182">Hello `-i` параметр начинает Beeline, выполняется hello инструкций в файле query.hql hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="67d06-183">После завершения выполнения запроса hello, будет выполнен переход на hello `jdbc:hive2://headnodehost:10001/>` строки.</span><span class="sxs-lookup"><span data-stu-id="67d06-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="67d06-184">Можно также запустить файл с помощью hello `-f` параметр, который завершает работу Beeline после завершения выполнения запроса hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="67d06-185">tooverify, hello **журналы ошибок** таблица была создана, используйте hello, следующая инструкция tooreturn Здравствуйте, все строки из **журналы ошибок**:</span><span class="sxs-lookup"><span data-stu-id="67d06-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="67d06-186">В результате операции должны быть возвращены три строки со значением **[ERROR]** в столбце t4.</span><span class="sxs-lookup"><span data-stu-id="67d06-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="67d06-187"><a id="remote"></a>Удаленное использование Beeline</span><span class="sxs-lookup"><span data-stu-id="67d06-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="67d06-188">Если у вас есть Beeline, установленные локально или используете его до образа Docker такие как [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), необходимо использовать hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="67d06-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="67d06-189">__Строка подключения__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`.</span><span class="sxs-lookup"><span data-stu-id="67d06-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="67d06-190">__Имя для входа на кластер__:`-n admin`.</span><span class="sxs-lookup"><span data-stu-id="67d06-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="67d06-191">__Пароль для входа на кластер__: `-p 'password'`.</span><span class="sxs-lookup"><span data-stu-id="67d06-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="67d06-192">Замените hello `clustername` в строке подключения hello с hello имя кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67d06-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="67d06-193">Замените `admin` с именем hello входа кластера, а `password` с hello пароль для имени входа кластера.</span><span class="sxs-lookup"><span data-stu-id="67d06-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="67d06-194"><a id="sparksql"></a>Использование Beeline со Spark</span><span class="sxs-lookup"><span data-stu-id="67d06-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="67d06-195">Spark обеспечивает собственную реализацию HiveServer2, который часто сервера Spark Thrift указанной tooas hello.</span><span class="sxs-lookup"><span data-stu-id="67d06-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="67d06-196">Эта служба использует запросы tooresolve Spark SQL вместо Hive и может обеспечить более высокую производительность в зависимости от запроса.</span><span class="sxs-lookup"><span data-stu-id="67d06-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="67d06-197">Spark в кластер HDInsight, использование портов сервера Spark Thrift toohello tooconnect `10002` вместо `10001`.</span><span class="sxs-lookup"><span data-stu-id="67d06-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="67d06-198">Например, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="67d06-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67d06-199">Hello сервера Spark Thrift — не напрямую Здравствуйте, доступны через Интернет.</span><span class="sxs-lookup"><span data-stu-id="67d06-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="67d06-200">Можно только подключение tooit из сеанса SSH или внутри hello одной виртуальной сети Azure, как hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67d06-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="67d06-201"><a id="summary"></a><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67d06-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="67d06-202">Дополнительные сведения о Hive в HDInsight см. следующий документ hello:</span><span class="sxs-lookup"><span data-stu-id="67d06-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="67d06-203">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="67d06-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="67d06-204">Дополнительные сведения о том, как другие могут работать с Hadoop в HDInsight, см. следующие документы hello:</span><span class="sxs-lookup"><span data-stu-id="67d06-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="67d06-205">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="67d06-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="67d06-206">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="67d06-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="67d06-207">Если вы используете Tez с Hive, см. следующие документы hello:</span><span class="sxs-lookup"><span data-stu-id="67d06-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="67d06-208">Использовать hello Tez пользовательского интерфейса на основе Windows HDInsight</span><span class="sxs-lookup"><span data-stu-id="67d06-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="67d06-209">Использовать hello Ambari Tez представление на основе Linux HDInsight</span><span class="sxs-lookup"><span data-stu-id="67d06-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
