---
title: "процессы aaaUse Hadoop Oozie в HDInsight под управлением Linux | Документы Microsoft"
description: "Использование Hadoop Oozie в HDInsight на основе Linux. Узнайте, как toodefine Oozie рабочего процесса и отправка задания Oozie."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="79251-104">Используйте Oozie с Hadoop toodefine и запуск рабочего процесса на основе Linux HDInsight</span><span class="sxs-lookup"><span data-stu-id="79251-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="79251-105">Узнайте, как toouse Oozie Apache с Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79251-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="79251-106">Apache Oozie — это система рабочих процессов и координации, управляющая заданиями Hadoop.</span><span class="sxs-lookup"><span data-stu-id="79251-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="79251-107">Oozie интегрирована с hello Hadoop стека, и он поддерживает hello следующие задания:</span><span class="sxs-lookup"><span data-stu-id="79251-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="79251-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="79251-108">Apache MapReduce</span></span>
* <span data-ttu-id="79251-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="79251-109">Apache Pig</span></span>
* <span data-ttu-id="79251-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="79251-110">Apache Hive</span></span>
* <span data-ttu-id="79251-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="79251-111">Apache Sqoop</span></span>

<span data-ttu-id="79251-112">Также можно использовать tooschedule заданий, определенных tooa систему, такую как Java программ или сценариев оболочки Oozie</span><span class="sxs-lookup"><span data-stu-id="79251-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="79251-113">Еще один способ определения рабочих процессов в HDInsight - Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="79251-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="79251-114">toolearn Дополнительные сведения о фабрики данных Azure, в разделе [использование Pig и Hive с фабрикой данных][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="79251-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79251-115">Диспетчер Oozie не включен в присоединенном к домену кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79251-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79251-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="79251-116">Prerequisites</span></span>

* <span data-ttu-id="79251-117">**Кластер HDInsight**: ознакомьтесь с [началом работы с HDInsight в Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="79251-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="79251-118">Hello в данном пошаговом руководстве требуется кластер HDInsight, использующий Linux.</span><span class="sxs-lookup"><span data-stu-id="79251-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="79251-119">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="79251-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="79251-120">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="79251-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="79251-121">Пример рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="79251-121">Example workflow</span></span>

<span data-ttu-id="79251-122">Hello рабочего процесса, используемого в данном документе содержатся два действия.</span><span class="sxs-lookup"><span data-stu-id="79251-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="79251-123">Действия являются определениями задач, таких как запуск Hive, Sqoop, MapReduce или других процессов:</span><span class="sxs-lookup"><span data-stu-id="79251-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Схема рабочих процессов][img-workflow-diagram]

1. <span data-ttu-id="79251-125">Действие Hive запускает сценарий HiveQL tooextract записей из hello **hivesampletable** состав HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79251-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="79251-126">Каждая строка данных описывает посещение с определенного мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="79251-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="79251-127">Формат записи Hello появится примерно toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="79251-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="79251-128">Hello скрипт Hive, используемые в этом документе подсчитывает общее посещений hello для каждой платформы (например, Android или iPhone) и сохраняет новую таблицу Hive hello счетчиков tooa.</span><span class="sxs-lookup"><span data-stu-id="79251-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="79251-129">Дополнительные сведения о Hive см. в статье [Использование Hive с HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="79251-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="79251-130">Действие Sqoop экспортирует содержимое hello hello новый куст таблицы tooa таблицы в базе данных Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="79251-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="79251-131">Дополнительные сведения о Sqoop см. в статье [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="79251-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="79251-132">О поддерживаемых версиях Oozie в кластерах HDInsight см. в разделе [новые возможности версии кластера Hadoop hello, предоставляемые HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="79251-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="79251-133">Создать рабочий каталог hello</span><span class="sxs-lookup"><span data-stu-id="79251-133">Create hello working directory</span></span>

<span data-ttu-id="79251-134">Oozie ожидает, что ресурсы, необходимые для toobe задания, сохраненные в hello же каталог.</span><span class="sxs-lookup"><span data-stu-id="79251-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="79251-135">В этом примере используется каталог **wasb:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="79251-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="79251-136">Используйте следующие команды toocreate hello каталог и hello каталог данных, содержащий таблицу Hive новый hello, созданную с помощью этого рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="79251-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="79251-137">Hello `-p` параметр вызывает все каталоги в созданные toobe путь hello.</span><span class="sxs-lookup"><span data-stu-id="79251-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="79251-138">Hello **данные** каталогом является toohold используемые данные, используемые hello **useooziewf.hql** сценария.</span><span class="sxs-lookup"><span data-stu-id="79251-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="79251-139">Также можно выполнить следующую команду, которая гарантирует, что ваша учетная запись пользователя может олицетворять Oozie при выполнении задания Hive и Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="79251-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="79251-140">Замените **USERNAME** на свое имя пользователя:</span><span class="sxs-lookup"><span data-stu-id="79251-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="79251-141">Ошибки можно игнорировать, hello пользователь уже является членом hello `users` группы.</span><span class="sxs-lookup"><span data-stu-id="79251-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="79251-142">Добавление драйвера базы данных</span><span class="sxs-lookup"><span data-stu-id="79251-142">Add a database driver</span></span>

<span data-ttu-id="79251-143">Поскольку этот рабочий процесс использует Sqoop tooexport данные tooSQL базы данных, необходимо предоставить копию драйвера JDBC hello используемых tootalk tooSQL базы данных.</span><span class="sxs-lookup"><span data-stu-id="79251-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="79251-144">Используйте hello следующие команды toocopy его toohello рабочий каталог:</span><span class="sxs-lookup"><span data-stu-id="79251-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="79251-145">Если рабочий процесс используется другими ресурсами, например JAR-файл, содержащий приложение MapReduce, потребовалось бы tooadd этих ресурсов, а также.</span><span class="sxs-lookup"><span data-stu-id="79251-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="79251-146">Определение запроса Hive hello</span><span class="sxs-lookup"><span data-stu-id="79251-146">Define hello Hive query</span></span>

<span data-ttu-id="79251-147">Используйте следующие шаги toocreate сценарий HiveQL, который определяет запрос, который используется в рабочем процессе Oozie далее в этом документе hello.</span><span class="sxs-lookup"><span data-stu-id="79251-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="79251-148">Подключите кластер toohello с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="79251-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="79251-149">Hello следующая команда является примером использования hello `ssh` команды.</span><span class="sxs-lookup"><span data-stu-id="79251-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="79251-150">Замените __USERNAME__ пользователю hello SSH для hello кластера.</span><span class="sxs-lookup"><span data-stu-id="79251-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="79251-151">Замените __CLUSTERNAME__ с именем hello hello кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="79251-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="79251-152">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="79251-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="79251-153">В hello SSH-подключения используйте следующие команды toocreate файл hello:</span><span class="sxs-lookup"><span data-stu-id="79251-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="79251-154">Как только откроется окно редактора nano hello, используйте приветствия при следующем запросе в качестве hello содержимое файла hello:</span><span class="sxs-lookup"><span data-stu-id="79251-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="79251-155">Существует две переменные, используемые в скрипте hello.</span><span class="sxs-lookup"><span data-stu-id="79251-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="79251-156">**${hiveTableName}**: содержит имя hello создан toobe таблицы hello</span><span class="sxs-lookup"><span data-stu-id="79251-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="79251-157">**${hiveDataFolder}**: файлами hello расположение toostore hello данных для таблицы hello</span><span class="sxs-lookup"><span data-stu-id="79251-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="79251-158">файл определения рабочего процесса Hello (workflow.xml в этом учебнике) передает эти значения toothis сценарий HiveQL во время выполнения</span><span class="sxs-lookup"><span data-stu-id="79251-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="79251-159">Редактор tooexit hello, нажмите клавиши Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="79251-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="79251-160">При появлении запроса выберите **Y** toosave hello файла, а затем используйте **ввод** toouse hello **useooziewf.hql** имя файла.</span><span class="sxs-lookup"><span data-stu-id="79251-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="79251-161">Используйте hello следующими командами toocopy **useooziewf.hql** слишком**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="79251-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="79251-162">Эти команды хранения hello **useooziewf.hql** файл на hello HDFS-совместимой хранилища для кластера hello.</span><span class="sxs-lookup"><span data-stu-id="79251-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="79251-163">Определение рабочего процесса hello</span><span class="sxs-lookup"><span data-stu-id="79251-163">Define hello workflow</span></span>

<span data-ttu-id="79251-164">Определения рабочих процессов Oozie записываются в формате hPDL (язык определения процессов XML).</span><span class="sxs-lookup"><span data-stu-id="79251-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="79251-165">Используйте следующие шаги toodefine hello workflow hello.</span><span class="sxs-lookup"><span data-stu-id="79251-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="79251-166">Используйте следующие инструкции toocreate hello и изменить новый файл:</span><span class="sxs-lookup"><span data-stu-id="79251-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="79251-167">Когда откроется окно редактора nano hello, введите следующий XML-код в качестве содержимого файла hello hello:</span><span class="sxs-lookup"><span data-stu-id="79251-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="79251-168">Существует два действия, определенные в рабочем процессе hello.</span><span class="sxs-lookup"><span data-stu-id="79251-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="79251-169">**RunHiveScript**: это действие hello действие при запуске и запускает hello **useooziewf.hql** скрипта Hive</span><span class="sxs-lookup"><span data-stu-id="79251-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="79251-170">**RunSqoopExport**: это действие экспортирует данные hello, созданные на основе tooSQL скрипт Hive hello базы данных с помощью Sqoop.</span><span class="sxs-lookup"><span data-stu-id="79251-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="79251-171">Это действие выполняется, только если hello **RunHiveScript** действие выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="79251-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="79251-172">Hello рабочего процесса имеет несколько операций, таких как `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="79251-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="79251-173">Эти записи заменяются значений, используемых в определении задания hello.</span><span class="sxs-lookup"><span data-stu-id="79251-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="79251-174">Определение задания Hello создается далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="79251-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="79251-175">Также Обратите внимание hello `<archive>sqljdbc4.jar</arcive>` запись в раздел Sqoop hello.</span><span class="sxs-lookup"><span data-stu-id="79251-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="79251-176">Эта запись указывает, что Oozie toomake этот архив доступных Sqoop при запуске этого действия.</span><span class="sxs-lookup"><span data-stu-id="79251-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="79251-177">Затем используйте сочетание клавиш Ctrl-X **Y** и **ввод** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="79251-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="79251-178">Используйте hello следующая команда toocopy hello **workflow.xml** файла слишком**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="79251-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="79251-179">Создание базы данных hello</span><span class="sxs-lookup"><span data-stu-id="79251-179">Create hello database</span></span>

<span data-ttu-id="79251-180">toocreate базы данных SQL Azure, выполните действия hello в hello [создать базу данных SQL](../sql-database/sql-database-get-started.md) документа.</span><span class="sxs-lookup"><span data-stu-id="79251-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="79251-181">При создании базы данных hello используйте `oozietest` как hello имя базы данных.</span><span class="sxs-lookup"><span data-stu-id="79251-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="79251-182">Также запишите hello имя сервера базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="79251-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="79251-183">Создать таблицу hello</span><span class="sxs-lookup"><span data-stu-id="79251-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="79251-184">Существуют tooSQL tooconnect много способов – toocreate базы данных таблицы.</span><span class="sxs-lookup"><span data-stu-id="79251-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="79251-185">Здравствуйте, выполнив действия, используйте [FreeTDS](http://www.freetds.org/) из кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="79251-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="79251-186">Используйте следующие команды tooinstall FreeTDS в кластере HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="79251-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="79251-187">После установки FreeTDS используйте hello, следующая команда toohello tooconnect базы данных SQL server, созданный ранее.</span><span class="sxs-lookup"><span data-stu-id="79251-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="79251-188">Появится примерно toohello выходных данных после текста:</span><span class="sxs-lookup"><span data-stu-id="79251-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="79251-189">В hello `1>` введите hello следующие строки:</span><span class="sxs-lookup"><span data-stu-id="79251-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="79251-190">Здравствуйте, когда `GO` инструкция вводится, вычисляются hello предыдущих операторов.</span><span class="sxs-lookup"><span data-stu-id="79251-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="79251-191">Следующие инструкции создают таблицу с именем **mobiledata** , используемый hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="79251-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="79251-192">Используйте hello, следуя tooverify, hello таблицы был создан:</span><span class="sxs-lookup"><span data-stu-id="79251-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="79251-193">Можно увидеть примерно toohello выходных данных после текста:</span><span class="sxs-lookup"><span data-stu-id="79251-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="79251-194">Введите `exit` в hello `1>` строки tooexit hello tsql.</span><span class="sxs-lookup"><span data-stu-id="79251-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="79251-195">Создание определения задания hello</span><span class="sxs-lookup"><span data-stu-id="79251-195">Create hello job definition</span></span>

<span data-ttu-id="79251-196">Определение задания Hello описывает, где toofind hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="79251-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="79251-197">Он также описывает, куда toofind другие файлы, используемые hello рабочего процесса (например, useooziewf.hql). Он также определяет hello значения для свойства, используемые в рамках рабочего процесса hello и связанные файлы.</span><span class="sxs-lookup"><span data-stu-id="79251-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="79251-198">Используйте следующие команды tooget hello полный адрес хранилища по умолчанию hello hello.</span><span class="sxs-lookup"><span data-stu-id="79251-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="79251-199">Этот адрес будет использоваться в файле конфигурации hello позже:</span><span class="sxs-lookup"><span data-stu-id="79251-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="79251-200">Эта команда возвращает сведения аналогичные toohello следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="79251-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="79251-201">Если кластер HDInsight hello использует хранилища Azure в качестве хранилища по умолчанию hello, hello `<value>` содержимое элемента начинаются с `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="79251-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="79251-202">Если же используется Azure Data Lake Store, оно начинается с `adl://`.</span><span class="sxs-lookup"><span data-stu-id="79251-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="79251-203">Сохранить содержимое hello hello `<value>` элемент, как оно используется в hello дальнейшие действия.</span><span class="sxs-lookup"><span data-stu-id="79251-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="79251-204">Используйте следующие команды tooget полное доменное имя головному узлу кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="79251-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="79251-205">Эта информация используется для hello JobTracker адрес hello кластера:</span><span class="sxs-lookup"><span data-stu-id="79251-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="79251-206">Возвращает сведения аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="79251-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="79251-207">Hello — порт, используемый для hello JobTracker 8050, поэтому toouse hello полный адрес для hello JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="79251-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="79251-208">Используйте следующие настройки описания задания Oozie hello toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="79251-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="79251-209">После открывается редактор nano hello, используйте следующий XML-код в виде hello содержимое файла hello hello:</span><span class="sxs-lookup"><span data-stu-id="79251-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * <span data-ttu-id="79251-210">Замените все вхождения  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  со значением hello, полученная ранее для хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="79251-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="79251-211">Если путь hello `wasb` пути, необходимо использовать полный путь hello.</span><span class="sxs-lookup"><span data-stu-id="79251-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="79251-212">Не сокращайте его toojust `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="79251-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="79251-213">Замените **JOBTRACKERADDRESS** с hello адрес JobTracker/ResourceManager, полученная ранее.</span><span class="sxs-lookup"><span data-stu-id="79251-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="79251-214">Замените **YourName** с вашим именем входа для кластера HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="79251-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="79251-215">Замените **serverName**, **adminLogin**, и **adminPassword** данными hello для базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="79251-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="79251-216">Большая часть hello сведения в этом файле находится используется toopopulate hello значений, используемых в hello workflow.xml или ooziewf.hql файлов (например, ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="79251-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="79251-217">Hello **oozie.wf.application.path** входа определяет, где toofind hello workflow.xml файл, который содержит рабочий процесс hello запускалось этого задания.</span><span class="sxs-lookup"><span data-stu-id="79251-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="79251-218">Затем используйте сочетание клавиш Ctrl-X **Y** и **ввод** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="79251-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="79251-219">Отправка и управлять заданием hello</span><span class="sxs-lookup"><span data-stu-id="79251-219">Submit and manage hello job</span></span>

<span data-ttu-id="79251-220">Hello следующее использование toosubmit команда Oozie hello и управления Oozie рабочих процессов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="79251-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="79251-221">Команда Oozie Hello превышает дружественный интерфейс hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="79251-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79251-222">При использовании команды Oozie hello, необходимо использовать hello полное доменное имя для головному узлу HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="79251-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="79251-223">Это полное доменное имя доступно только из кластера hello, или если hello кластер находится в виртуальной сети Azure, с других компьютеров на hello одной сети.</span><span class="sxs-lookup"><span data-stu-id="79251-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="79251-224">Используйте следующие tooobtain hello URL-адрес toohello Oozie службы hello.</span><span class="sxs-lookup"><span data-stu-id="79251-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="79251-225">Возвращает сведения аналогичные toohello следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="79251-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="79251-226">Hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` часть числа равна hello toouse URL-адрес с hello Oozie команды.</span><span class="sxs-lookup"><span data-stu-id="79251-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="79251-227">Следующие toocreate переменной среды для URL-адреса hello, поэтому не нужно tootype hello используйте его для каждой команды:</span><span class="sxs-lookup"><span data-stu-id="79251-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="79251-228">Замените URL-адрес hello hello, полученная ранее.</span><span class="sxs-lookup"><span data-stu-id="79251-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="79251-229">Используйте следующие задания hello toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="79251-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="79251-230">Эта команда загружает сведения о задании hello из **job.xml** и передает его tooOozie, но он не не запустите его.</span><span class="sxs-lookup"><span data-stu-id="79251-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="79251-231">После выполнения команды hello, он должен возвращать идентификатор hello hello задания.</span><span class="sxs-lookup"><span data-stu-id="79251-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="79251-232">Например, `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="79251-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="79251-233">Этот идентификатор является задание используется toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="79251-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="79251-234">Просмотр состояния hello hello задания с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="79251-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="79251-235">Замените `<JOBID>` hello идентификатор, возвращаемый в предыдущем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="79251-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="79251-236">Возвращает сведения аналогичные toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="79251-236">This returns information similar toohello following text:</span></span>

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    <span data-ttu-id="79251-237">Это задание находится в состоянии `PREP`,</span><span class="sxs-lookup"><span data-stu-id="79251-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="79251-238">Этот статус указывает hello задания был создан, но не запущена.</span><span class="sxs-lookup"><span data-stu-id="79251-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="79251-239">Используйте hello следующая команда toostart hello задания:</span><span class="sxs-lookup"><span data-stu-id="79251-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="79251-240">Замените `<JOBID>` с hello идентификатор возвращается ранее.</span><span class="sxs-lookup"><span data-stu-id="79251-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="79251-241">При проверке состояния hello после этой команды, он находится в состоянии выполнения, и возвращаются сведения для действия hello в задании hello.</span><span class="sxs-lookup"><span data-stu-id="79251-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="79251-242">После успешного завершения задачи hello можно проверить созданный hello данных, а также экспортировать toohello таблица базы данных SQL с помощью следующих команд hello:</span><span class="sxs-lookup"><span data-stu-id="79251-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="79251-243">В hello `1>` введите приветствия при следующем запросе:</span><span class="sxs-lookup"><span data-stu-id="79251-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="79251-244">Hello сведения, возвращаемые — примерно toohello следующий текст:</span><span class="sxs-lookup"><span data-stu-id="79251-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="79251-245">Дополнительные сведения о hello Oozie команды в разделе [Oozie средство командной строки](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="79251-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="79251-246">Oozie REST API</span><span class="sxs-lookup"><span data-stu-id="79251-246">Oozie REST API</span></span>

<span data-ttu-id="79251-247">Hello Oozie REST API позволяет toobuild собственные средства, которые работают с Oozie.</span><span class="sxs-lookup"><span data-stu-id="79251-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="79251-248">Здесь представлены Hello HDInsight подробные сведения об использовании hello Oozie REST API:</span><span class="sxs-lookup"><span data-stu-id="79251-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="79251-249">**URI**: hello, REST API можно получить доступ из внешней hello кластеру на`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="79251-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="79251-250">**Проверка подлинности**: toohello API, с помощью учетной записи кластера HTTP hello (администратор) и пароль проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="79251-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="79251-251">Например:</span><span class="sxs-lookup"><span data-stu-id="79251-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="79251-252">Дополнительные сведения об использовании hello Oozie REST API см. в разделе [Oozie API веб-служб](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="79251-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="79251-253">Пользовательский веб-интерфейс Oozie</span><span class="sxs-lookup"><span data-stu-id="79251-253">Oozie Web UI</span></span>

<span data-ttu-id="79251-254">Hello Oozie веб-Интерфейс обеспечивает представление веб-статуса hello Oozie заданий в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="79251-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="79251-255">Hello веб-Интерфейс позволяет tooview hello следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="79251-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="79251-256">Состояние задания</span><span class="sxs-lookup"><span data-stu-id="79251-256">Job status</span></span>
* <span data-ttu-id="79251-257">определение задания;</span><span class="sxs-lookup"><span data-stu-id="79251-257">Job definition</span></span>
* <span data-ttu-id="79251-258">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="79251-258">Configuration</span></span>
* <span data-ttu-id="79251-259">График действий hello в задании hello</span><span class="sxs-lookup"><span data-stu-id="79251-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="79251-260">Журналы для задания hello</span><span class="sxs-lookup"><span data-stu-id="79251-260">Logs for hello job</span></span>

<span data-ttu-id="79251-261">Также можно просмотреть подробную информацию о действиях в рамках задания.</span><span class="sxs-lookup"><span data-stu-id="79251-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="79251-262">tooaccess hello Oozie веб-интерфейса, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="79251-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="79251-263">Создание кластера HDInsight toohello туннеля SSH.</span><span class="sxs-lookup"><span data-stu-id="79251-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="79251-264">Сведения см. в разделе hello [использование SSH туннелирование с HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) документа.</span><span class="sxs-lookup"><span data-stu-id="79251-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="79251-265">После создания туннеля, откройте hello Ambari web пользовательского интерфейса в веб-браузере.</span><span class="sxs-lookup"><span data-stu-id="79251-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="79251-266">Hello URI для сайта hello Ambari — **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="79251-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="79251-267">Замените **CLUSTERNAME** с hello имя кластера HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="79251-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="79251-268">Левая сторона страницы приветствия hello, выберите **Oozie**, затем **быстрые ссылки**и, наконец, **Oozie веб-интерфейса**.</span><span class="sxs-lookup"><span data-stu-id="79251-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![Изображение меню hello](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="79251-270">значения по умолчанию веб-интерфейса Oozie Hello toodisplaying выполняющиеся задания рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="79251-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="79251-271">Выберите задания для всех рабочих процессов, toosee **все задания**.</span><span class="sxs-lookup"><span data-stu-id="79251-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![Отображаются все задания](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="79251-273">Выберите Дополнительные сведения о задании hello tooview задания.</span><span class="sxs-lookup"><span data-stu-id="79251-273">Select a job tooview more information about hello job.</span></span>

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="79251-275">На вкладке сведений о задании hello видно основные сведения и hello отдельных действий в рамках задания hello.</span><span class="sxs-lookup"><span data-stu-id="79251-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="79251-276">С помощью hello вкладок в верхней hello, пользователи могут просматривать hello определения задания конфигурации задания доступа hello журнала задания или просмотр направленный ациклического графа (DAG) задания hello.</span><span class="sxs-lookup"><span data-stu-id="79251-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="79251-277">**Журнал задания**: выберите hello **GetLogs** кнопку tooget все журналы для задания hello, или использовать hello **введите фильтр поиска** поле toofilter журналы</span><span class="sxs-lookup"><span data-stu-id="79251-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![Журнал задания](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="79251-279">**JobDAG**: hello DAG является графическим обзором hello пути к данным по hello рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="79251-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![Направленный ациклический граф задания](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="79251-281">Выбрав одно из действий hello hello **сведения о задании** вкладке появится сведения для действия hello.</span><span class="sxs-lookup"><span data-stu-id="79251-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="79251-282">Например, выберите hello **RunHiveScript** действия.</span><span class="sxs-lookup"><span data-stu-id="79251-282">For example, select hello **RunHiveScript** action.</span></span>

    ![Информация о действии](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="79251-284">Чтобы просмотреть сведения для действия hello, например toohello ссылку **URL-адрес консоли**.</span><span class="sxs-lookup"><span data-stu-id="79251-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="79251-285">Эта ссылка может указывать сведения о JobTracker tooview используется для задания hello.</span><span class="sxs-lookup"><span data-stu-id="79251-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="79251-286">Планирование заданий</span><span class="sxs-lookup"><span data-stu-id="79251-286">Scheduling jobs</span></span>

<span data-ttu-id="79251-287">Координатор Hello позволяет toospecify частотой начало, конец и вхождения для заданий.</span><span class="sxs-lookup"><span data-stu-id="79251-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="79251-288">toodefine расписание для процесса hello, hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="79251-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="79251-289">Hello используйте следующий файл с именем toocreate **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="79251-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="79251-290">Используйте следующий XML-код в виде hello содержимое файла hello hello.</span><span class="sxs-lookup"><span data-stu-id="79251-290">Use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > <span data-ttu-id="79251-291">Hello `${...}` переменные заменяются значениями в определении задания hello во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="79251-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="79251-292">имеются следующие переменные Hello:</span><span class="sxs-lookup"><span data-stu-id="79251-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="79251-293">`${coordFrequency}`: Время между запуском экземпляров задания hello.</span><span class="sxs-lookup"><span data-stu-id="79251-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="79251-294">** `${coordStart}`: время начала задания hello.</span><span class="sxs-lookup"><span data-stu-id="79251-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="79251-295">`${coordEnd}`: время завершения задания hello.</span><span class="sxs-lookup"><span data-stu-id="79251-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="79251-296">`${coordTimezone}`: задания координатора задаются для конкретного часового пояса без летнего времени (обычно представляется в виде времени в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="79251-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="79251-297">Этот часовой пояс называется hello» Oozie обработки часовой пояс.»</span><span class="sxs-lookup"><span data-stu-id="79251-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="79251-298">`${wfPath}`: hello workflow.xml toohello пути.</span><span class="sxs-lookup"><span data-stu-id="79251-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="79251-299">toosave hello файла следует использовать сочетание клавиш Ctrl-X **Y**, и **ввод**.</span><span class="sxs-lookup"><span data-stu-id="79251-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="79251-300">Используйте hello, следующая команда toocopy hello файл toohello рабочий каталог для этого задания.</span><span class="sxs-lookup"><span data-stu-id="79251-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="79251-301">Используйте hello, следуя toomodify hello **job.xml** файла:</span><span class="sxs-lookup"><span data-stu-id="79251-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="79251-302">Сделать hello следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="79251-302">Make hello following changes:</span></span>

   * <span data-ttu-id="79251-303">файл tooinstruct oozie toorun hello координатора вместо hello рабочего процесса, изменение `<name>oozie.wf.application.path</name>` слишком`<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="79251-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="79251-304">tooset hello `workflowPath` переменной, используемой координатором hello добавить hello, следующий XML-код:</span><span class="sxs-lookup"><span data-stu-id="79251-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="79251-305">Замените hello `wasb://mycontainer@mystorageaccount.blob.core.windows` текст hello значение, используемое в других записях в файле job.xml hello.</span><span class="sxs-lookup"><span data-stu-id="79251-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="79251-306">toodefine hello начала, окончания и частоты для координатора hello, добавьте следующий XML-код hello:</span><span class="sxs-lookup"><span data-stu-id="79251-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       <span data-ttu-id="79251-307">Эти значения задают too12 времени начала hello: 00 PM на 10 мая 2017 г., hello tooMay время окончания 12, 2017 г.</span><span class="sxs-lookup"><span data-stu-id="79251-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="79251-308">Интервал приветствия для выполнения этого задания ежедневно.</span><span class="sxs-lookup"><span data-stu-id="79251-308">hello interval for running this job daily.</span></span> <span data-ttu-id="79251-309">частота Hello — в минутах, поэтому 24 часов x 60 минут = 1440 минут.</span><span class="sxs-lookup"><span data-stu-id="79251-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="79251-310">Наконец часовой пояс hello устанавливается tooUTC.</span><span class="sxs-lookup"><span data-stu-id="79251-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="79251-311">Затем используйте сочетание клавиш Ctrl-X **Y** и **ввод** toosave hello файла.</span><span class="sxs-lookup"><span data-stu-id="79251-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="79251-312">Задание toorun hello, hello используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="79251-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="79251-313">Эта команда запускает задание hello и отправляет.</span><span class="sxs-lookup"><span data-stu-id="79251-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="79251-314">Если посетите hello Oozie веб-интерфейса пользователя и выберите hello **заданий координатора** вкладку, появится примерно toohello сведения после изображения:</span><span class="sxs-lookup"><span data-stu-id="79251-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![Вкладка задания координатора](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="79251-316">Hello **Далее материализации** запись содержит hello очередном hello запуска заданий.</span><span class="sxs-lookup"><span data-stu-id="79251-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="79251-317">Аналогичные toohello предыдущих задания рабочего процесса, выбрав запись задания hello в hello веб-интерфейса отображает информацию на hello задания:</span><span class="sxs-lookup"><span data-stu-id="79251-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![Информация о задании координатора](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="79251-319">На данном рисунке показан только успешных выполнений задания hello, не отдельные действия в рабочем процессе запланированные hello.</span><span class="sxs-lookup"><span data-stu-id="79251-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="79251-320">toosee, выберите один из hello **действия** записей.</span><span class="sxs-lookup"><span data-stu-id="79251-320">toosee that, select one of hello **Action** entries.</span></span>

    ![Информация о действии](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="79251-322">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="79251-322">Troubleshooting</span></span>

<span data-ttu-id="79251-323">Hello Oozie пользовательский Интерфейс позволяет tooview Oozie журналы.</span><span class="sxs-lookup"><span data-stu-id="79251-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="79251-324">Он также содержит ссылки в журналах tooJobTracker MapReduce задачи, запущенные hello рабочим процессом.</span><span class="sxs-lookup"><span data-stu-id="79251-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="79251-325">должен быть Hello шаблон для устранения неполадок:</span><span class="sxs-lookup"><span data-stu-id="79251-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="79251-326">Просмотр заданий hello в Oozie веб-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="79251-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="79251-327">При возникновении ошибки или сбоя для определенных действий выберите hello toosee действие, если hello **сообщение об ошибке** поля содержатся дополнительные сведения о сбое hello.</span><span class="sxs-lookup"><span data-stu-id="79251-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="79251-328">При наличии используйте hello URL-адрес из tooview действие hello Дополнительные сведения (такие как журналы JobTracker) для действия hello.</span><span class="sxs-lookup"><span data-stu-id="79251-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="79251-329">Hello ниже приведены конкретные ошибки могут возникнуть, и как tooresolve их.</span><span class="sxs-lookup"><span data-stu-id="79251-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="79251-330">JA009: Не удается инициализировать кластер</span><span class="sxs-lookup"><span data-stu-id="79251-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="79251-331">**Проблема**: hello изменения состояния задания слишком**SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="79251-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="79251-332">Сведения для задания hello отображения состояния RunHiveScript hello как **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="79251-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="79251-333">При выборе действия hello отображаются hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="79251-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="79251-334">**Причина**: hello WASB адреса, используемые в hello **job.xml** файл содержит контейнер хранилища hello или имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="79251-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="79251-335">Формат адреса WASB Hello должен быть `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="79251-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="79251-336">**Разрешение**: изменить адреса hello WASB, используемая заданием hello.</span><span class="sxs-lookup"><span data-stu-id="79251-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="79251-337">JA002: Oozie запрещено tooimpersonate &lt;пользователя ></span><span class="sxs-lookup"><span data-stu-id="79251-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="79251-338">**Проблема**: hello изменения состояния задания слишком**SUSPENDED**.</span><span class="sxs-lookup"><span data-stu-id="79251-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="79251-339">Сведения для задания hello отображения состояния RunHiveScript hello как **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="79251-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="79251-340">Выбрав действие hello показано hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="79251-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="79251-341">**Причина**: текущие параметры разрешений не допускают Oozie tooimpersonate hello указанную учетную запись пользователя.</span><span class="sxs-lookup"><span data-stu-id="79251-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="79251-342">**Разрешение**: Oozie допускается пользователей tooimpersonate hello **пользователей** группы.</span><span class="sxs-lookup"><span data-stu-id="79251-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="79251-343">Используйте hello `groups USERNAME` toosee hello группы, которые hello учетная запись пользователя является членом.</span><span class="sxs-lookup"><span data-stu-id="79251-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="79251-344">Если пользователь hello не является членом hello **пользователей** группы, используйте следующие группы команд tooadd hello пользователя toohello hello:</span><span class="sxs-lookup"><span data-stu-id="79251-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="79251-345">Он может занять несколько минут, прежде чем HDInsight распознает, что этот пользователь hello добавлен toohello группы.</span><span class="sxs-lookup"><span data-stu-id="79251-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="79251-346">ОШИБКА запуска (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="79251-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="79251-347">**Проблема**: hello изменения состояния задания слишком**KILLED**.</span><span class="sxs-lookup"><span data-stu-id="79251-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="79251-348">Сведения для задания hello отображения состояния RunSqoopExport hello как **ошибка**.</span><span class="sxs-lookup"><span data-stu-id="79251-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="79251-349">Выбрав действие hello показано hello следующие сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="79251-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="79251-350">**Причина**: Sqoop база данных не удается tooload hello базы данных драйвер необходимые tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="79251-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="79251-351">**Разрешение**: при использовании Sqoop из задания Oozie, необходимо включить драйвер hello базы данных с hello другие ресурсы (например, «hello workflow.xml), используемая заданием hello.</span><span class="sxs-lookup"><span data-stu-id="79251-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="79251-352">Также ссылаться hello архив, содержащий hello драйвер базы данных из hello `<sqoop>...</sqoop>` раздел hello workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="79251-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="79251-353">Например для задания hello в этом документе, используется hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="79251-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="79251-354">Скопируйте каталог /tutorials/useoozie toohello файла sqljdbc4.1.jar hello:</span><span class="sxs-lookup"><span data-stu-id="79251-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="79251-355">Изменение hello workflow.xml tooadd hello следующий XML-код в новой строке `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="79251-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="79251-356">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79251-356">Next steps</span></span>

<span data-ttu-id="79251-357">В этом учебнике вы узнали, как toodefine Oozie рабочего процесса и как toorun задание Oozie.</span><span class="sxs-lookup"><span data-stu-id="79251-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="79251-358">toolearn Дополнительные сведения о работе с HDInsight, см. следующие статьи hello.</span><span class="sxs-lookup"><span data-stu-id="79251-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="79251-359">[Используйте учитывающий время координатор Oozie с Hadoop в HDInsight для определения рабочих процессов и координации заданий][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="79251-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="79251-360">[Отправка данных для заданий Hadoop в HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="79251-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="79251-361">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="79251-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="79251-362">[Использование Hive с Hadoop в HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="79251-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="79251-363">[Использование Pig с Hadoop в HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="79251-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="79251-364">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="79251-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
