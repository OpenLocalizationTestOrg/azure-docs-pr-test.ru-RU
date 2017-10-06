---
title: "aaaApache Sqoop с Hadoop - Azure HDInsight | Документы Microsoft"
description: "Узнайте, как toouse tooimport Apache Sqoop и экспорт между Hadoop в HDInsight и базы данных SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop,sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="9a16e-104">Используйте tooimport Apache Sqoop и экспортируют данные Hadoop в HDInsight и база данных SQL</span><span class="sxs-lookup"><span data-stu-id="9a16e-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="9a16e-105">Узнайте, как Apache Sqoop tooimport toouse и экспорт между Hadoop кластере в Azure HDInsight и база данных SQL Azure или Microsoft SQL Server базы данных.</span><span class="sxs-lookup"><span data-stu-id="9a16e-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="9a16e-106">Hello шагов в этот документ используйте hello `sqoop` непосредственно из hello головному узлу кластера Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="9a16e-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="9a16e-107">Использовать SSH tooconnect toohello головного узла и выполнения команд hello в этом документе.</span><span class="sxs-lookup"><span data-stu-id="9a16e-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a16e-108">Hello действия, описанные в этом документе работают только с кластерами HDInsight, использующих Linux.</span><span class="sxs-lookup"><span data-stu-id="9a16e-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="9a16e-109">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="9a16e-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9a16e-110">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9a16e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="9a16e-111">Установка FreeTDS</span><span class="sxs-lookup"><span data-stu-id="9a16e-111">Install FreeTDS</span></span>

1. <span data-ttu-id="9a16e-112">Используйте кластер HDInsight toohello tooconnect SSH.</span><span class="sxs-lookup"><span data-stu-id="9a16e-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="9a16e-113">Например, следующую команду hello подключается toohello первичного головному узлу кластера с именем `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="9a16e-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="9a16e-114">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9a16e-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="9a16e-115">Используйте следующие команды tooinstall FreeTDS hello.</span><span class="sxs-lookup"><span data-stu-id="9a16e-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="9a16e-116">FreeTDS используется в нескольких tooSQL tooconnect действия базы данных.</span><span class="sxs-lookup"><span data-stu-id="9a16e-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="9a16e-117">Создать таблицу hello в базе данных SQL</span><span class="sxs-lookup"><span data-stu-id="9a16e-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9a16e-118">Если вы используете кластера HDInsight hello и создать базу данных SQL в [создания кластера и базы данных SQL](hdinsight-use-sqoop.md), пропустите шаги hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="9a16e-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="9a16e-119">Hello базы данных и таблицы были созданы как часть hello шагов в hello [создания кластера и базы данных SQL](hdinsight-use-sqoop.md) документа.</span><span class="sxs-lookup"><span data-stu-id="9a16e-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="9a16e-120">Из сеанса SSH hello используйте hello, следующая команда tooconnect toohello базы данных SQL server.</span><span class="sxs-lookup"><span data-stu-id="9a16e-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="9a16e-121">Появится примерно toohello выходных данных после текста:</span><span class="sxs-lookup"><span data-stu-id="9a16e-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="9a16e-122">В hello `1>` введите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="9a16e-122">At hello `1>` prompt, enter hello following query:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    <span data-ttu-id="9a16e-123">Здравствуйте, когда `GO` инструкция вводится, вычисляются hello предыдущих операторов.</span><span class="sxs-lookup"><span data-stu-id="9a16e-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="9a16e-124">Во-первых, hello **mobiledata** создается таблица, а затем кластеризованный индекс добавляется tooit (требуется в базе данных SQL).</span><span class="sxs-lookup"><span data-stu-id="9a16e-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="9a16e-125">Hello используйте следующий запрос tooverify, hello таблицы был создан:</span><span class="sxs-lookup"><span data-stu-id="9a16e-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="9a16e-126">Можно увидеть примерно toohello выходных данных после текста:</span><span class="sxs-lookup"><span data-stu-id="9a16e-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="9a16e-127">Введите `exit` в hello `1>` строки tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="9a16e-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="9a16e-128">Экспорт Sqoop</span><span class="sxs-lookup"><span data-stu-id="9a16e-128">Sqoop export</span></span>

1. <span data-ttu-id="9a16e-129">В кластере toohello подключения SSH hello используйте hello, выполнив команду tooverify, Sqoop можно увидеть базы данных SQL:</span><span class="sxs-lookup"><span data-stu-id="9a16e-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="9a16e-130">При появлении запроса введите пароль hello для входа базы данных SQL hello.</span><span class="sxs-lookup"><span data-stu-id="9a16e-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="9a16e-131">Эта команда возвращает список баз данных, включая hello **sqooptest** базы данных, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="9a16e-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="9a16e-132">данные tooexport **hivesampletable** toohello **mobiledata** таблицы, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="9a16e-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="9a16e-133">Эта команда указывает, что Sqoop tooconnect toohello **sqooptest** базы данных.</span><span class="sxs-lookup"><span data-stu-id="9a16e-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="9a16e-134">Sqoop затем экспортирует данные из **wasb: / / / hive или хранилище или hivesampletable** toohello **mobiledata** таблицы.</span><span class="sxs-lookup"><span data-stu-id="9a16e-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9a16e-135">Используйте `wasb:///` hello хранилища по умолчанию для кластера в случае учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="9a16e-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="9a16e-136">Используйте `adl:///`, если это Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9a16e-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="9a16e-137">После выполнения команды hello используйте hello, следующая команда tooconnect toohello базы данных с помощью TSQL:</span><span class="sxs-lookup"><span data-stu-id="9a16e-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="9a16e-138">После подключения hello используйте следующие инструкции tooverify, hello данных был экспортированного toohello **mobiledata** таблицы:</span><span class="sxs-lookup"><span data-stu-id="9a16e-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="9a16e-139">Вы увидите список данных в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="9a16e-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="9a16e-140">Тип `exit` tooexit hello tsql программы.</span><span class="sxs-lookup"><span data-stu-id="9a16e-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="9a16e-141">Импорт Sqoop</span><span class="sxs-lookup"><span data-stu-id="9a16e-141">Sqoop import</span></span>

1. <span data-ttu-id="9a16e-142">Используйте hello следующая команда tooimport данные из hello **mobiledata** таблицы в базе данных SQL, toohello **wasb: / / / учебники/usesqoop/importeddata** на HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9a16e-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="9a16e-143">поля Hello в данных hello разделяются символ табуляции и строки hello завершаются символом новой строки.</span><span class="sxs-lookup"><span data-stu-id="9a16e-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="9a16e-144">После завершения операции импорта hello, используйте следующие команды toolist hello данных в новый каталог hello hello:</span><span class="sxs-lookup"><span data-stu-id="9a16e-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="9a16e-145">Использование SQL Server</span><span class="sxs-lookup"><span data-stu-id="9a16e-145">Using SQL Server</span></span>

<span data-ttu-id="9a16e-146">Можно также использовать Sqoop tooimport и экспортировать данные из SQL Server в центре обработки данных или на виртуальной машине, размещенной в Azure.</span><span class="sxs-lookup"><span data-stu-id="9a16e-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="9a16e-147">перечислены Hello различия между использованием базы данных SQL и SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9a16e-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="9a16e-148">HDInsight и SQL Server должен быть на hello одной виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="9a16e-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="9a16e-149">Пример см. в разделе hello [HDInsight подключения tooyour локальной сети](./connect-on-premises-network.md) документа.</span><span class="sxs-lookup"><span data-stu-id="9a16e-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="9a16e-150">Дополнительные сведения об использовании HDInsight с помощью виртуальной сети Azure см. в разделе hello [расширить HDInsight с помощью виртуальной сети Azure](hdinsight-extend-hadoop-virtual-network.md) документа.</span><span class="sxs-lookup"><span data-stu-id="9a16e-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="9a16e-151">Дополнительные сведения о виртуальной сети Azure см. в разделе hello [Обзор виртуальной сети](../virtual-network/virtual-networks-overview.md) документа.</span><span class="sxs-lookup"><span data-stu-id="9a16e-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="9a16e-152">SQL Server должны быть настроенный tooallow проверки подлинности SQL.</span><span class="sxs-lookup"><span data-stu-id="9a16e-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="9a16e-153">Дополнительные сведения см. в разделе hello [Выбор режима проверки подлинности](https://msdn.microsoft.com/ms144284.aspx) документа.</span><span class="sxs-lookup"><span data-stu-id="9a16e-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="9a16e-154">Вы можете иметь tooconfigure SQL Server tooaccept удаленные соединения.</span><span class="sxs-lookup"><span data-stu-id="9a16e-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="9a16e-155">Дополнительные сведения см. в разделе hello [как подключающегося toohello tootroubleshoot SQL Server компонент database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) документа.</span><span class="sxs-lookup"><span data-stu-id="9a16e-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="9a16e-156">Создать hello **sqooptest** базы данных SQL Server, такие как с помощью программы **SQL Server Management Studio** или **tsql**.</span><span class="sxs-lookup"><span data-stu-id="9a16e-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="9a16e-157">этапы использования hello Azure CLI Hello работают только для базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9a16e-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="9a16e-158">Используйте hello, следуя hello toocreate инструкций Transact-SQL **mobiledata** таблицы:</span><span class="sxs-lookup"><span data-stu-id="9a16e-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="9a16e-159">При подключении toohello SQL Server с HDInsight, возможно toouse hello IP-адрес hello SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9a16e-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="9a16e-160">Например:</span><span class="sxs-lookup"><span data-stu-id="9a16e-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="9a16e-161">Ограничения</span><span class="sxs-lookup"><span data-stu-id="9a16e-161">Limitations</span></span>

* <span data-ttu-id="9a16e-162">Для массового экспорта — под управлением Linux с HDInsight, hello Sqoop соединитель, используемый tooexport данных tooMicrosoft SQL Server или база данных SQL Azure в настоящее время не поддерживает операции массовой вставки.</span><span class="sxs-lookup"><span data-stu-id="9a16e-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="9a16e-163">Пакетное выполнение — с hdinsight под управлением Linux, при использовании hello `-batch` переключение при выполнении вставки, Sqoop выполняет вставку нескольких вместо Пакетная обработка операций вставки hello.</span><span class="sxs-lookup"><span data-stu-id="9a16e-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a16e-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a16e-164">Next steps</span></span>

<span data-ttu-id="9a16e-165">Теперь вы узнали, как toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="9a16e-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="9a16e-166">toolearn более, см.:</span><span class="sxs-lookup"><span data-stu-id="9a16e-166">toolearn more, see:</span></span>

* <span data-ttu-id="9a16e-167">[Использование Oozie с HDInsight][hdinsight-use-oozie]: используйте действие Sqoop в рабочем процессе Oozie.</span><span class="sxs-lookup"><span data-stu-id="9a16e-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="9a16e-168">[Анализ данных задержки рейсов, с помощью HDInsight][hdinsight-analyze-flight-data]: используйте Hive рейса tooanalyze задержка данных, а затем использовать базы данных Azure SQL tooan Sqoop tooexport данных.</span><span class="sxs-lookup"><span data-stu-id="9a16e-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="9a16e-169">[Отправка данных tooHDInsight][hdinsight-upload-data]: найти другие методы для отправки данных tooHDInsight/Azure BLOB-объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="9a16e-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
