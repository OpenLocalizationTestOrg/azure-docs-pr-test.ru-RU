---
title: "aaaUse Hadoop Hive и удаленного рабочего стола в HDInsight — Azure | Документы Microsoft"
description: "Узнайте, как tooconnect tooHadoop кластера в HDInsight с помощью удаленного рабочего стола, а затем запустите запросов Hive с помощью hello Hive интерфейс командной строки."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="0653a-103">Использование Hive с Hadoop в HDInsight с помощью удаленного рабочего стола</span><span class="sxs-lookup"><span data-stu-id="0653a-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="0653a-104">В этой статье вы узнаете, как tooan tooconnect HDInsight кластер с помощью удаленного рабочего стола, а затем запустите Hive запросов с использованием hello Hive интерфейс командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="0653a-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0653a-105">Удаленный рабочий стол доступен только в кластерах HDInsight, использование в качестве hello операционной системы Windows.</span><span class="sxs-lookup"><span data-stu-id="0653a-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="0653a-106">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="0653a-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0653a-107">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0653a-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="0653a-108">Для HDInsight 3.4 или выше в разделе [используйте Hive с HDInsight и Beeline](hdinsight-hadoop-use-hive-beeline.md) сведения об использовании запросов Hive непосредственно на hello кластера из командной строки.</span><span class="sxs-lookup"><span data-stu-id="0653a-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="0653a-109"><a id="prereq"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0653a-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="0653a-110">в этой статье инструкциям toocomplete hello, вам потребуется hello следующие:</span><span class="sxs-lookup"><span data-stu-id="0653a-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="0653a-111">Кластер HDInsight на платформе Windows (Hadoop в HDInsight).</span><span class="sxs-lookup"><span data-stu-id="0653a-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="0653a-112">Клиентский компьютер под управлением Windows 10, Windows 8 или Windows 7.</span><span class="sxs-lookup"><span data-stu-id="0653a-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="0653a-113"><a id="connect"></a>Подключение к удаленному рабочему столу</span><span class="sxs-lookup"><span data-stu-id="0653a-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="0653a-114">Включить удаленный рабочий стол для кластера HDInsight hello, а затем соедините tooit в соответствии с инструкциями hello в [tooHDInsight кластерами, с помощью протокола удаленного рабочего СТОЛА подключиться](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="0653a-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="0653a-115"><a id="hive"></a>Команда Hive hello</span><span class="sxs-lookup"><span data-stu-id="0653a-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="0653a-116">При подключении toohello рабочий стол для кластера HDInsight hello, используйте следующие шаги toowork с Hive hello:</span><span class="sxs-lookup"><span data-stu-id="0653a-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="0653a-117">С рабочего стола HDInsight hello, запустите hello **командной строки Hadoop**.</span><span class="sxs-lookup"><span data-stu-id="0653a-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="0653a-118">Введите следующая команда toostart hello Hive CLI hello:</span><span class="sxs-lookup"><span data-stu-id="0653a-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="0653a-119">При запуске hello CLI, вы увидите строку hello Hive CLI: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="0653a-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="0653a-120">С помощью hello (CLI), введите следующие инструкции toocreate новую таблицу с именем hello **log4jLogs** использует образец данных:</span><span class="sxs-lookup"><span data-stu-id="0653a-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="0653a-121">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0653a-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="0653a-122">**DROP TABLE**: Удаляет hello таблицы и файла данных hello, существует ли таблица hello.</span><span class="sxs-lookup"><span data-stu-id="0653a-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="0653a-123">**CREATE EXTERNAL TABLE**: создание новой "внешней" таблицы в Hive.</span><span class="sxs-lookup"><span data-stu-id="0653a-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="0653a-124">Внешние таблицы хранить только определение таблицы hello в кусте (приветствия данные остаются в исходном расположении hello).</span><span class="sxs-lookup"><span data-stu-id="0653a-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="0653a-125">Предполагается, что базовые данные toobe обновлены из внешнего источника (например, в процессе загрузки данных) или другой операцией MapReduce hello, когда требуется, чтобы последние данные toouse hello запросов Hive, следует использовать внешние таблицы.</span><span class="sxs-lookup"><span data-stu-id="0653a-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="0653a-126">Удаление внешней таблицы **не** удаление данных hello, только определение таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="0653a-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="0653a-127">**ФОРМАТ СТРОК**: сообщает Hive форматирование данных hello.</span><span class="sxs-lookup"><span data-stu-id="0653a-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="0653a-128">В этом случае hello полей в каждом журнале разделенные пробелом.</span><span class="sxs-lookup"><span data-stu-id="0653a-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="0653a-129">**ХРАНИМЫЕ РАСПОЛОЖЕНИЕ текстового файла AS**: сообщает Hive, где данные hello хранимых (hello данные примера и каталог), которые он хранится в виде текста.</span><span class="sxs-lookup"><span data-stu-id="0653a-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="0653a-130">**ВЫБЕРИТЕ**: выбирает число всех строк где столбца **t4** содержит значение hello **[ошибка]**.</span><span class="sxs-lookup"><span data-stu-id="0653a-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="0653a-131">Эта команда должна вернуть значение **3** , так как данное значение содержат три строки.</span><span class="sxs-lookup"><span data-stu-id="0653a-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="0653a-132">**INPUT__FILE__NAME LIKE '%.log'** — указывает Hive, что вернуть нужно только данные из файлов с расширением LOG.</span><span class="sxs-lookup"><span data-stu-id="0653a-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="0653a-133">Это ограничивает hello toohello поиска sample.log файл, содержащий данные hello и предотвращает возвращение данных из других примере файлы данных, которые не соответствуют схеме hello, который мы определили.</span><span class="sxs-lookup"><span data-stu-id="0653a-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="0653a-134">Hello используйте следующие инструкции toocreate новую таблицу «internal» с именем **журналы ошибок**:</span><span class="sxs-lookup"><span data-stu-id="0653a-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="0653a-135">Эти операторы выполняют hello, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0653a-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="0653a-136">**CREATE TABLE IF NOT EXISTS**: создание таблицы, если она до этого не существовала.</span><span class="sxs-lookup"><span data-stu-id="0653a-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="0653a-137">Поскольку hello **ВНЕШНИХ** не используется ключевое слово, это внутренней таблицы, которые хранятся в хранилище данных Hive hello и полностью управляются Hive.</span><span class="sxs-lookup"><span data-stu-id="0653a-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="0653a-138">В отличие от **ВНЕШНИХ** таблиц, удаление внутренней таблицы также удаляет hello базовым данным.</span><span class="sxs-lookup"><span data-stu-id="0653a-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="0653a-139">**ORC ХРАНИМОЙ AS**: сохраняет hello данные в табличном формате (ORC) оптимизированного строки.</span><span class="sxs-lookup"><span data-stu-id="0653a-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="0653a-140">Это высокооптимизированный и эффективный формат для хранения данных Hive.</span><span class="sxs-lookup"><span data-stu-id="0653a-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="0653a-141">**INSERT OVERWRITE ... ВЫБЕРИТЕ**: выбирает строки из hello **log4jLogs** таблицы, которые содержат **[ошибка]**, а затем вставки данных hello в hello **журналы ошибок** таблицы.</span><span class="sxs-lookup"><span data-stu-id="0653a-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="0653a-142">tooverify, только строки, которые содержат **[ошибка]** в столбец t4 были хранимых toohello **журналы ошибок** таблицы, используйте hello, следующая инструкция tooreturn Здравствуйте, все строки из **журналы ошибок**:</span><span class="sxs-lookup"><span data-stu-id="0653a-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="0653a-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="0653a-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="0653a-144">В результате операции должны быть возвращены три строки, в которых столбец t4 содержит значение **[ERROR]** .</span><span class="sxs-lookup"><span data-stu-id="0653a-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="0653a-145"><a id="summary"></a>Сводка</span><span class="sxs-lookup"><span data-stu-id="0653a-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="0653a-146">Как видите, hello hello Hive команда предоставляет toointeractively простой способ выполнения запросов Hive в кластере HDInsight, монитор hello состояние задания и получение выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="0653a-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="0653a-147"><a id="nextsteps"></a>Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0653a-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="0653a-148">Общая информация о Hive в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0653a-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="0653a-149">Использование Hive с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0653a-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="0653a-150">Дополнительная информация о других способах работы с Hadoop в HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0653a-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="0653a-151">Использование Pig с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0653a-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0653a-152">Использование MapReduce с Hadoop в HDInsight</span><span class="sxs-lookup"><span data-stu-id="0653a-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="0653a-153">При использовании Tez с куста см. следующие документы отладочной информации hello:</span><span class="sxs-lookup"><span data-stu-id="0653a-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="0653a-154">Использовать hello Tez пользовательского интерфейса на основе Windows HDInsight</span><span class="sxs-lookup"><span data-stu-id="0653a-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="0653a-155">Использовать hello Ambari Tez представление на основе Linux HDInsight</span><span class="sxs-lookup"><span data-stu-id="0653a-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
