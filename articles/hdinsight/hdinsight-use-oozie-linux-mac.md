---
title: "Использование рабочих процессов Hadoop Oozie в HDInsight на основе Linux | Документация Майкрософт"
description: "Использование Hadoop Oozie в HDInsight на основе Linux. Вы узнаете, как определить рабочий процесс и отправить задание для Oozie."
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
ms.openlocfilehash: e3206078e451aefe02689bfb61ce22a20dd0fa70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="a0d75-104">Использование Oozie с Hadoop для определения и запуска рабочих процессов в HDInsight под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="a0d75-104">Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="a0d75-105">Сведения об использовании Apache Oozie с Hadoop в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d75-105">Learn how to use Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="a0d75-106">Apache Oozie — это система рабочих процессов и координации, управляющая заданиями Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a0d75-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="a0d75-107">Служба Oozie интегрирована со стеком Hadoop и поддерживает следующие задания:</span><span class="sxs-lookup"><span data-stu-id="a0d75-107">Oozie is integrated with the Hadoop stack, and it supports the following jobs:</span></span>

* <span data-ttu-id="a0d75-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="a0d75-108">Apache MapReduce</span></span>
* <span data-ttu-id="a0d75-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="a0d75-109">Apache Pig</span></span>
* <span data-ttu-id="a0d75-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="a0d75-110">Apache Hive</span></span>
* <span data-ttu-id="a0d75-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="a0d75-111">Apache Sqoop</span></span>

<span data-ttu-id="a0d75-112">Oozie также можно использовать для планирования системных заданий, например, Java-программ и сценариев оболочки.</span><span class="sxs-lookup"><span data-stu-id="a0d75-112">Oozie can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="a0d75-113">Еще один способ определения рабочих процессов в HDInsight - Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a0d75-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="a0d75-114">Дополнительные сведения об использовании действий Pig и Hive см. в статье [Преобразование данных в фабрике данных Azure][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="a0d75-114">To learn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0d75-115">Диспетчер Oozie не включен в присоединенном к домену кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d75-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0d75-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a0d75-116">Prerequisites</span></span>

* <span data-ttu-id="a0d75-117">**Кластер HDInsight**: ознакомьтесь с [началом работы с HDInsight в Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a0d75-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="a0d75-118">Для выполнения действий, описанных в этом документе, необходим кластер HDInsight, который использует Linux.</span><span class="sxs-lookup"><span data-stu-id="a0d75-118">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="a0d75-119">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="a0d75-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a0d75-120">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a0d75-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="a0d75-121">Пример рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="a0d75-121">Example workflow</span></span>

<span data-ttu-id="a0d75-122">Рабочий процесс, используемый в этой статье, включает два действия.</span><span class="sxs-lookup"><span data-stu-id="a0d75-122">The workflow used in this document contains two actions.</span></span> <span data-ttu-id="a0d75-123">Действия являются определениями задач, таких как запуск Hive, Sqoop, MapReduce или других процессов:</span><span class="sxs-lookup"><span data-stu-id="a0d75-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Схема рабочих процессов][img-workflow-diagram]

1. <span data-ttu-id="a0d75-125">Действие Hive запускает скрипт HiveQL для извлечения записей из таблицы **hivesampletable** , входящей в состав в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d75-125">A Hive action runs a HiveQL script to extract records from the **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="a0d75-126">Каждая строка данных описывает посещение с определенного мобильного устройства.</span><span class="sxs-lookup"><span data-stu-id="a0d75-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="a0d75-127">Формат записи таков:</span><span class="sxs-lookup"><span data-stu-id="a0d75-127">The record format appears similar to the following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="a0d75-128">Скрипт Hive, используемый в данном документе, подсчитывает общее количество посещений для каждой платформы (например, Android или iPhone) и сохраняет результаты в новой таблице Hive.</span><span class="sxs-lookup"><span data-stu-id="a0d75-128">The Hive script used in this document counts the total visits for each platform (such as Android or iPhone) and stores the counts to a new Hive table.</span></span>

    <span data-ttu-id="a0d75-129">Дополнительные сведения о Hive см. в статье [Использование Hive с HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="a0d75-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="a0d75-130">Действие Sqoop экспортирует содержимое новой таблицы Hive в таблицу в базе данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d75-130">A Sqoop action exports the contents of the new Hive table to a table in an Azure SQL database.</span></span> <span data-ttu-id="a0d75-131">Дополнительные сведения о Sqoop см. в статье [Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="a0d75-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="a0d75-132">Сведения о поддерживаемых версиях Oozie в кластерах HDInsight см. в статье [Что представляют собой различные компоненты Hadoop, доступные в HDInsight?][hdinsight-versions]</span><span class="sxs-lookup"><span data-stu-id="a0d75-132">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-the-working-directory"></a><span data-ttu-id="a0d75-133">Создайте рабочий каталог</span><span class="sxs-lookup"><span data-stu-id="a0d75-133">Create the working directory</span></span>

<span data-ttu-id="a0d75-134">Ресурсы, необходимые для выполнения задания, должны находиться в том же каталоге.</span><span class="sxs-lookup"><span data-stu-id="a0d75-134">Oozie expects resources required for a job to be stored in the same directory.</span></span> <span data-ttu-id="a0d75-135">В этом примере используется каталог **wasb:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="a0d75-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="a0d75-136">Для создания этого каталога и каталога данных для новой таблицы Hive, которую создаст этот рабочий процесс, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a0d75-136">Use the following command to create this directory, and the data directory that holds the new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="a0d75-137">Параметр `-p` означает, что будут созданы все промежуточные каталоги для указанного пути.</span><span class="sxs-lookup"><span data-stu-id="a0d75-137">The `-p` parameter causes all directories in the path to be created.</span></span> <span data-ttu-id="a0d75-138">В каталоге **data** хранятся данные, используемые скриптом **useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="a0d75-138">The **data** directory is used to hold data used by the **useooziewf.hql** script.</span></span>

<span data-ttu-id="a0d75-139">Также можно выполнить следующую команду, которая гарантирует, что при выполнении заданий Hive и Sqoop Oozie сможет работать от имени вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="a0d75-139">Also run the following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="a0d75-140">Замените **USERNAME** на свое имя пользователя:</span><span class="sxs-lookup"><span data-stu-id="a0d75-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="a0d75-141">Ошибки о том, что пользователь уже является членом группы `users`, можно игнорировать.</span><span class="sxs-lookup"><span data-stu-id="a0d75-141">You can ignore errors that the user is already a member of the `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="a0d75-142">Добавление драйвера базы данных</span><span class="sxs-lookup"><span data-stu-id="a0d75-142">Add a database driver</span></span>

<span data-ttu-id="a0d75-143">Поскольку этот рабочий процесс использует Sqoop для экспорта данных в базу данных SQL, необходимо предоставить копию драйвера JDBC, используемого для обращения к базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a0d75-143">Since this workflow uses Sqoop to export data to SQL Database, you must provide a copy of the JDBC driver used to talk to SQL Database.</span></span> <span data-ttu-id="a0d75-144">Используйте следующую команду для копирования драйвера в рабочий каталог:</span><span class="sxs-lookup"><span data-stu-id="a0d75-144">Use the following command to copy it to the working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="a0d75-145">Если рабочий процесс использует другие ресурсы, например JAR-файл, содержащий приложение MapReduce, необходимо также добавить эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="a0d75-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need to add these resources as well.</span></span>

## <a name="define-the-hive-query"></a><span data-ttu-id="a0d75-146">Определение запроса Hive</span><span class="sxs-lookup"><span data-stu-id="a0d75-146">Define the Hive query</span></span>

<span data-ttu-id="a0d75-147">Выполните следующие действия, чтобы создать скрипт HiveQL для определения запроса. Этот запрос будет использоваться в рабочем процессе Oozie далее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a0d75-147">Use the following steps to create a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="a0d75-148">Подключитесь к кластеру с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="a0d75-148">Connect to the cluster using SSH.</span></span> <span data-ttu-id="a0d75-149">Следующая команда является примером использования команды `ssh`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-149">The following command is an example of using the `ssh` command.</span></span> <span data-ttu-id="a0d75-150">Замените __USERNAME__ именем пользователя для подключения к кластеру с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="a0d75-150">Replace __USERNAME__ with the SSH user for the cluster.</span></span> <span data-ttu-id="a0d75-151">Замените __CLUSTERNAME__ именем кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d75-151">Replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="a0d75-152">Дополнительные сведения см. в статье [Использование SSH с Hadoop на основе Linux в HDInsight из Linux, Unix или OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a0d75-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a0d75-153">В сеансе SSH создайте файл, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a0d75-153">From the SSH connection, use the following command to create a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="a0d75-154">После открытия редактора Nano используйте следующий запрос в качестве содержимого файла:</span><span class="sxs-lookup"><span data-stu-id="a0d75-154">Once the nano editor opens, use the following query as the contents of the file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="a0d75-155">В данном сценарии используются три следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="a0d75-155">There are two variables used in the script:</span></span>

    * <span data-ttu-id="a0d75-156">**${hiveTableName}** содержит имя создаваемой таблицы;</span><span class="sxs-lookup"><span data-stu-id="a0d75-156">**${hiveTableName}**: contains the name of the table to be created</span></span>

    * <span data-ttu-id="a0d75-157">**${hiveDataFolder}** содержит расположения файлов данных для таблицы.</span><span class="sxs-lookup"><span data-stu-id="a0d75-157">**${hiveDataFolder}**: contains the location to store the data files for the table</span></span>

    <span data-ttu-id="a0d75-158">Файл с определением рабочего процесса (workflow.xml в этом руководстве) передает эти значения в скрипт HiveQL во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="a0d75-158">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time</span></span>

4. <span data-ttu-id="a0d75-159">Нажмите CTRL+X, чтобы закрыть редактор.</span><span class="sxs-lookup"><span data-stu-id="a0d75-159">To exit the editor, press Ctrl-X.</span></span> <span data-ttu-id="a0d75-160">При появлении запроса нажмите **Y** для сохранения файла, затем нажмите клавишу **ВВОД**, чтобы использовать имя файла **useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="a0d75-160">When prompted, select **Y** to save the file, then use **Enter** to use the **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="a0d75-161">Используйте следующие команды для копирования **useooziewf.hql** в **wasb:///tutorials/useoozie/useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="a0d75-161">Use the following commands to copy **useooziewf.hql** to **wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="a0d75-162">Эти команды сохраняют файл **useooziewf.hql** в HDFS-совместимом хранилище кластера.</span><span class="sxs-lookup"><span data-stu-id="a0d75-162">These commands store the **useooziewf.hql** file on the HDFS-compatible storage for the cluster.</span></span>

## <a name="define-the-workflow"></a><span data-ttu-id="a0d75-163">Определение рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="a0d75-163">Define the workflow</span></span>

<span data-ttu-id="a0d75-164">Определения рабочих процессов Oozie записываются в формате hPDL (язык определения процессов XML).</span><span class="sxs-lookup"><span data-stu-id="a0d75-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="a0d75-165">Для определения рабочего процесса выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a0d75-165">Use the following steps to define the workflow:</span></span>

1. <span data-ttu-id="a0d75-166">Для создания и открытия файла выполните следующий запрос:</span><span class="sxs-lookup"><span data-stu-id="a0d75-166">Use the following statement to create and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="a0d75-167">После открытия редактора Nano введите следующий код XML в качестве содержимого файла:</span><span class="sxs-lookup"><span data-stu-id="a0d75-167">Once the nano editor opens, enter the following XML as the file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>
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

    <span data-ttu-id="a0d75-168">В рабочем процессе определены два действия:</span><span class="sxs-lookup"><span data-stu-id="a0d75-168">There are two actions defined in the workflow:</span></span>

   * <span data-ttu-id="a0d75-169">**RunHiveScript.** Это действие при запуске, которое запускает скрипт Hive **useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="a0d75-169">**RunHiveScript**: This action is the start action, and runs the **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="a0d75-170">**RunSqoopExport.** Это действие экспортирует созданные данные из скрипта Hive в базу данных SQL с использованием Sqoop.</span><span class="sxs-lookup"><span data-stu-id="a0d75-170">**RunSqoopExport**: This action exports the data created from the Hive script to SQL Database using Sqoop.</span></span> <span data-ttu-id="a0d75-171">Это действие будет выполнено, только если действие **RunHiveScript** завершится успешно.</span><span class="sxs-lookup"><span data-stu-id="a0d75-171">This action only runs if the **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="a0d75-172">В рабочем процессе есть несколько записей, таких как `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-172">The workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="a0d75-173">Они заменяются значениями, используемыми в определении задания,</span><span class="sxs-lookup"><span data-stu-id="a0d75-173">These entries are replaced by values you use in the job definition.</span></span> <span data-ttu-id="a0d75-174">которое будет создано позже в этом документе.</span><span class="sxs-lookup"><span data-stu-id="a0d75-174">The job definition is created later in this document.</span></span>

     <span data-ttu-id="a0d75-175">Также обратите внимание на параметр `<archive>sqljdbc4.jar</arcive>` в разделе Sqoop.</span><span class="sxs-lookup"><span data-stu-id="a0d75-175">Also note the `<archive>sqljdbc4.jar</arcive>` entry in the Sqoop section.</span></span> <span data-ttu-id="a0d75-176">Эта запись означает, что этот архив должен стать доступным для Sqoop при выполнении этого действия.</span><span class="sxs-lookup"><span data-stu-id="a0d75-176">This entry instructs Oozie to make this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="a0d75-177">Нажмите клавиши Ctrl + X, затем **Y** и **ВВОД**, чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="a0d75-177">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

4. <span data-ttu-id="a0d75-178">Скопируйте файл **workflow.xml** в каталог **/tutorials/useoozie/workflow.xml** с помощью следующей команды.</span><span class="sxs-lookup"><span data-stu-id="a0d75-178">Use the following command to copy the **workflow.xml** file to **/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-the-database"></a><span data-ttu-id="a0d75-179">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="a0d75-179">Create the database</span></span>

<span data-ttu-id="a0d75-180">Чтобы создать базу данных SQL Azure, следуйте инструкциям в документе [Создание базы данных SQL Azure на портале Azure](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a0d75-180">To create an Azure SQL Database, follow the steps in the [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="a0d75-181">При создании задайте для базы данных имя `oozietest`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-181">When creating the database, use `oozietest` as the database name.</span></span> <span data-ttu-id="a0d75-182">Запишите также имя сервера базы данных.</span><span class="sxs-lookup"><span data-stu-id="a0d75-182">Also make a note of the name of the database server.</span></span>

### <a name="create-the-table"></a><span data-ttu-id="a0d75-183">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="a0d75-183">Create the table</span></span>

> [!NOTE]
> <span data-ttu-id="a0d75-184">Существует множество способов подключения к базе данных SQL для создания таблицы.</span><span class="sxs-lookup"><span data-stu-id="a0d75-184">There are many ways to connect to SQL Database to create a table.</span></span> <span data-ttu-id="a0d75-185">В приведенных ниже действиях используется [FreeTDS](http://www.freetds.org/) из кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d75-185">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="a0d75-186">Для установки FreeTDS в кластер HDInsight воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a0d75-186">Use the following command to install FreeTDS on the HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="a0d75-187">После установки FreeTDS используйте следующую команду для подключения к созданному серверу базы данных SQL:</span><span class="sxs-lookup"><span data-stu-id="a0d75-187">Once FreeTDS has been installed, use the following command to connect to the SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="a0d75-188">Должен появиться результат, аналогичный приведенному ниже тексту.</span><span class="sxs-lookup"><span data-stu-id="a0d75-188">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to oozietest
        1>

3. <span data-ttu-id="a0d75-189">В командной строке `1>` введите следующее:</span><span class="sxs-lookup"><span data-stu-id="a0d75-189">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="a0d75-190">Если вводится инструкция `GO`, то оцениваются предыдущие инструкции.</span><span class="sxs-lookup"><span data-stu-id="a0d75-190">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="a0d75-191">С помощью этих инструкций создается таблица **mobiledata**, используемая рабочим процессом.</span><span class="sxs-lookup"><span data-stu-id="a0d75-191">These statements create a table named **mobiledata** that is used by the workflow.</span></span>

    <span data-ttu-id="a0d75-192">Используйте следующую команду для проверки создания таблицы:</span><span class="sxs-lookup"><span data-stu-id="a0d75-192">Use the following to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="a0d75-193">Должен появиться результат, аналогичный приведенному ниже.</span><span class="sxs-lookup"><span data-stu-id="a0d75-193">You see output similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="a0d75-194">Enter `exit` at the `1>` , чтобы выйти из служебной программы tsql.</span><span class="sxs-lookup"><span data-stu-id="a0d75-194">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="create-the-job-definition"></a><span data-ttu-id="a0d75-195">Создание определения задания</span><span class="sxs-lookup"><span data-stu-id="a0d75-195">Create the job definition</span></span>

<span data-ttu-id="a0d75-196">Определение задания содержит информацию о местонахождении файла workflow.xml,</span><span class="sxs-lookup"><span data-stu-id="a0d75-196">The job definition describes where to find the workflow.xml.</span></span> <span data-ttu-id="a0d75-197">а также других файлов, используемых рабочим процессом (например, useooziewf.hql). В нем также определяются значения свойств, используемых в рабочем процессе и сопутствующих файлов.</span><span class="sxs-lookup"><span data-stu-id="a0d75-197">It also describes where to find other files used by the workflow (such as useooziewf.hql.) It also defines the values for properties used within the workflow and associated files.</span></span>

1. <span data-ttu-id="a0d75-198">Для получения полного адреса хранилища по умолчанию воспользуйтесь указанной ниже командой.</span><span class="sxs-lookup"><span data-stu-id="a0d75-198">Use the following command to get the full address of the default storage.</span></span> <span data-ttu-id="a0d75-199">Немного позже он будет использован в файле конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a0d75-199">This address is used in the configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="a0d75-200">Эта команда возвращает информацию, как в следующем коде XML:</span><span class="sxs-lookup"><span data-stu-id="a0d75-200">This command returns information similar to the following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="a0d75-201">Если кластер HDInsight использует службу хранилища Azure в качестве хранилища по умолчанию, содержимое элемента `<value>` начинается с `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-201">If the HDInsight cluster uses Azure Storage as the default storage, the `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="a0d75-202">Если же используется Azure Data Lake Store, оно начинается с `adl://`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="a0d75-203">Сохраните содержимое элемента `<value>`, которое потребуется нам на следующих шагах.</span><span class="sxs-lookup"><span data-stu-id="a0d75-203">Save the contents of the `<value>` element, as it is used in the next steps.</span></span>

2. <span data-ttu-id="a0d75-204">Воспользуйтесь следующей командой для получения полного имени домена головного узла кластера:</span><span class="sxs-lookup"><span data-stu-id="a0d75-204">Use the following command to get FQDN of the cluster headnode.</span></span> <span data-ttu-id="a0d75-205">Эта информация используется для адреса кластера в JobTracker.</span><span class="sxs-lookup"><span data-stu-id="a0d75-205">This information is used for the JobTracker address for the cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="a0d75-206">Эта команда возвращает следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a0d75-206">This returns information similar to the following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="a0d75-207">JobTracker использует порт 8050, поэтому полный адрес для JobTracker выглядит так: `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-207">The port used for the JobTracker is 8050, so the full address to use for the JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="a0d75-208">Используйте следующую команду для создания конфигурации определения задания Oozie:</span><span class="sxs-lookup"><span data-stu-id="a0d75-208">Use the following to create the Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="a0d75-209">После открытия редактора Nano используйте следующий код XML в качестве содержимого файла:</span><span class="sxs-lookup"><span data-stu-id="a0d75-209">Once the nano editor opens, use the following XML as the contents of the file:</span></span>

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

   * <span data-ttu-id="a0d75-210">Замените все вхождения **wasb://mycontainer@mystorageaccount.blob.core.windows.net** значением, полученным ранее для хранилища по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a0d75-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with the value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="a0d75-211">Если используется путь `wasb`, его необходимо указать полностью.</span><span class="sxs-lookup"><span data-stu-id="a0d75-211">If the path is a `wasb` path, you must use the full path.</span></span> <span data-ttu-id="a0d75-212">Не сокращайте его до строки `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-212">Do not shorten it to just `wasb:///`.</span></span>

   * <span data-ttu-id="a0d75-213">Замените **JOBTRACKERADDRESS** на адрес JobTracker/ResourceManager, полученный ранее.</span><span class="sxs-lookup"><span data-stu-id="a0d75-213">Replace **JOBTRACKERADDRESS** with the JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="a0d75-214">Замените **YourName** на ваше имя пользователя для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d75-214">Replace **YourName** with your login name for the HDInsight cluster.</span></span>
   * <span data-ttu-id="a0d75-215">Замените **serverName**, **adminLogin** и **adminPassword** соответствующими значениями для своей базы данных SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a0d75-215">Replace **serverName**, **adminLogin**, and **adminPassword** with the information for your Azure SQL Database.</span></span>

     <span data-ttu-id="a0d75-216">Большая часть информации в этом файле используется для заполнения значений, используемых в файлах workflow.xml или ooziewf.hql (например, ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="a0d75-216">Most of the information in this file is used to populate the values used in the workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="a0d75-217">Параметр **oozie.wf.application.path** определяет местоположение файла workflow.xml, содержащего рабочий процесс, который запускается этим заданием.</span><span class="sxs-lookup"><span data-stu-id="a0d75-217">The **oozie.wf.application.path** entry defines where to find the workflow.xml file, which contains the workflow ran by this job.</span></span>

5. <span data-ttu-id="a0d75-218">Нажмите клавиши Ctrl + X, затем **Y** и **ВВОД**, чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="a0d75-218">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

## <a name="submit-and-manage-the-job"></a><span data-ttu-id="a0d75-219">Отправка задания и управление им</span><span class="sxs-lookup"><span data-stu-id="a0d75-219">Submit and manage the job</span></span>

<span data-ttu-id="a0d75-220">Далее используется команда Oozie для отправки рабочих процессов Oozie в кластер и управления ими.</span><span class="sxs-lookup"><span data-stu-id="a0d75-220">The following steps use the Oozie command to submit and manage Oozie workflows on the cluster.</span></span> <span data-ttu-id="a0d75-221">Команда Oozie предоставляет удобный интерфейс для [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="a0d75-221">The Oozie command is a friendly interface over the [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0d75-222">При использовании команды Oozie необходимо использовать полное доменное имя для головного узла HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d75-222">When using the Oozie command, you must use the FQDN for the HDInsight headnode.</span></span> <span data-ttu-id="a0d75-223">Это полное доменное имя доступно только из кластера, или если кластер находится в виртуальной сети Azure, с других компьютеров той же сети.</span><span class="sxs-lookup"><span data-stu-id="a0d75-223">This FQDN is only accessible from the cluster, or if the cluster is on an Azure Virtual Network, from other machines on the same network.</span></span>


1. <span data-ttu-id="a0d75-224">Для получения URL-адреса службы Oozie воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a0d75-224">Use the following to obtain the URL to the Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="a0d75-225">Эта команда возвращает информацию, как в следующем коде XML:</span><span class="sxs-lookup"><span data-stu-id="a0d75-225">This returns information similar to the following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="a0d75-226">Здесь фрагмент `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` обозначает URL-адрес, который используется в команде Oozie.</span><span class="sxs-lookup"><span data-stu-id="a0d75-226">The `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is the URL to use with the Oozie command.</span></span>

2. <span data-ttu-id="a0d75-227">Используйте следующую команду для создания переменной среды для URL-адреса, чтобы не вводить его в каждой команде:</span><span class="sxs-lookup"><span data-stu-id="a0d75-227">Use the following to create an environment variable for the URL, so you don't have to type it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="a0d75-228">Замените URL-адрес полученным ранее.</span><span class="sxs-lookup"><span data-stu-id="a0d75-228">Replace the URL with the one you received earlier.</span></span>
3. <span data-ttu-id="a0d75-229">Чтобы отправить задание, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a0d75-229">Use the following to submit the job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="a0d75-230">Она загружает сведения о задании из **job.xml** и отправляет их Oozie, но не запускает задание.</span><span class="sxs-lookup"><span data-stu-id="a0d75-230">This command loads the job information from **job.xml** and submits it to Oozie, but does not run it.</span></span>

    <span data-ttu-id="a0d75-231">После завершения команды она должна вернуть идентификатор задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-231">Once the command completes, it should return the ID of the job.</span></span> <span data-ttu-id="a0d75-232">Например, `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="a0d75-233">Этот идентификатор используется для управления заданием.</span><span class="sxs-lookup"><span data-stu-id="a0d75-233">This ID is used to manage the job.</span></span>

4. <span data-ttu-id="a0d75-234">Для просмотра состояния задания воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a0d75-234">View the status of the job using the following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="a0d75-235">Замените `<JOBID>` идентификатором, возвращенным на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="a0d75-235">Replace `<JOBID>` with the ID returned in the previous step.</span></span>

    <span data-ttu-id="a0d75-236">Эта команда возвращает следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a0d75-236">This returns information similar to the following text:</span></span>

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

    <span data-ttu-id="a0d75-237">Это задание находится в состоянии `PREP`,</span><span class="sxs-lookup"><span data-stu-id="a0d75-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="a0d75-238">Это состояние указывает на то, что задание было создано, но не запущено.</span><span class="sxs-lookup"><span data-stu-id="a0d75-238">This status indicates that the job was created, but not started.</span></span>

5. <span data-ttu-id="a0d75-239">Выполните следующую команду для запуска задания:</span><span class="sxs-lookup"><span data-stu-id="a0d75-239">Use the following command to start the job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="a0d75-240">Замените `<JOBID>` идентификатором, возвращенным ранее.</span><span class="sxs-lookup"><span data-stu-id="a0d75-240">Replace `<JOBID>` with the ID returned previously.</span></span>

    <span data-ttu-id="a0d75-241">Если вы проверите состояние после этой команды, то увидите состояние выполнения и информацию о действиях для этого задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-241">If you check the status after this command, it is in a running state, and information is returned for the actions within the job.</span></span>

6. <span data-ttu-id="a0d75-242">После успешного завершения задания с помощью следующих команд можно проверить, что данные были созданы и экспортированы в таблицу базы данных SQL:</span><span class="sxs-lookup"><span data-stu-id="a0d75-242">Once the task completes successfully, you can verify that the data was generated and exported to the SQL Database table by using the following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="a0d75-243">В командной строке `1>` введите следующий запрос.</span><span class="sxs-lookup"><span data-stu-id="a0d75-243">At the `1>` prompt, enter the following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="a0d75-244">Эта команда возвращает следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a0d75-244">The information returned is similar to the following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="a0d75-245">Дополнительные сведения о команде Oozie см. на [странице, посвященной программе командной строки Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="a0d75-245">For more information on the Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="a0d75-246">Oozie REST API</span><span class="sxs-lookup"><span data-stu-id="a0d75-246">Oozie REST API</span></span>

<span data-ttu-id="a0d75-247">Oozie REST API позволяет создавать собственные утилиты для работы с Oozie.</span><span class="sxs-lookup"><span data-stu-id="a0d75-247">The Oozie REST API allows you to build your own tools that work with Oozie.</span></span> <span data-ttu-id="a0d75-248">Ниже приведена информация об использовании Oozie REST API для HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d75-248">The following are HDInsight specific information about using the Oozie REST API:</span></span>

* <span data-ttu-id="a0d75-249">**URI**: К REST API можно обращаться из-за пределов кластера по адресу: `https://CLUSTERNAME.azurehdinsight.net/oozie`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-249">**URI**: The REST API can be accessed from outside the cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="a0d75-250">**Authentication.** Для использования API необходимо пройти проверку подлинности с учетной записью HTTP кластера (администратор), указав пароль.</span><span class="sxs-lookup"><span data-stu-id="a0d75-250">**Authentication**: Authenticate to the API using the cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="a0d75-251">Например:</span><span class="sxs-lookup"><span data-stu-id="a0d75-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="a0d75-252">Дополнительные сведения об использовании Oozie REST API приведены в разделе [API веб-служб Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="a0d75-252">For more information on using the Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="a0d75-253">Пользовательский веб-интерфейс Oozie</span><span class="sxs-lookup"><span data-stu-id="a0d75-253">Oozie Web UI</span></span>

<span data-ttu-id="a0d75-254">Веб-интерфейс Oozie позволяет получить информацию о состоянии задания Oozie в кластере.</span><span class="sxs-lookup"><span data-stu-id="a0d75-254">The Oozie Web UI provides a web-based view into the status of Oozie jobs on the cluster.</span></span> <span data-ttu-id="a0d75-255">Веб-интерфейс позволяет просматривать следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="a0d75-255">The web UI allows you to view the following information:</span></span>

* <span data-ttu-id="a0d75-256">Состояние задания</span><span class="sxs-lookup"><span data-stu-id="a0d75-256">Job status</span></span>
* <span data-ttu-id="a0d75-257">определение задания;</span><span class="sxs-lookup"><span data-stu-id="a0d75-257">Job definition</span></span>
* <span data-ttu-id="a0d75-258">Конфигурация</span><span class="sxs-lookup"><span data-stu-id="a0d75-258">Configuration</span></span>
* <span data-ttu-id="a0d75-259">диаграмму действий задания;</span><span class="sxs-lookup"><span data-stu-id="a0d75-259">A graph of the actions in the job</span></span>
* <span data-ttu-id="a0d75-260">журналы задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-260">Logs for the job</span></span>

<span data-ttu-id="a0d75-261">Также можно просмотреть подробную информацию о действиях в рамках задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="a0d75-262">Для доступа к веб-интерфейсу Oozie выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a0d75-262">To access the Oozie Web UI, use the following steps:</span></span>

1. <span data-ttu-id="a0d75-263">Создайте туннель SSH для кластера HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a0d75-263">Create an SSH tunnel to the HDInsight cluster.</span></span> <span data-ttu-id="a0d75-264">Дополнительные сведения см. в документе [Использование туннелирования SSH для доступа к веб-интерфейсу Ambari, JobHistory, NameNode, Oozie и другим веб-интерфейсам](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="a0d75-264">For information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="a0d75-265">После создания туннеля откройте веб-интерфейс Ambari в браузере.</span><span class="sxs-lookup"><span data-stu-id="a0d75-265">Once a tunnel has been created, open the Ambari web UI in your web browser.</span></span> <span data-ttu-id="a0d75-266">Универсальный код ресурса (URI) сайта Ambari — **https://имя_кластера.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="a0d75-266">The URI for the Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="a0d75-267">Замените **имя_кластера** именем своего кластера HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="a0d75-267">Replace **CLUSTERNAME** with the name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="a0d75-268">В левой части страницы выберите **Oozie**, затем **Быстрые ссылки** и, наконец, **Oozie Web UI** (Пользовательский веб-интерфейс Oozie).</span><span class="sxs-lookup"><span data-stu-id="a0d75-268">From the left side of the page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![изображение меню](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="a0d75-270">По умолчанию в веб-интерфейсе Oozie отображаются запущенные задания рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="a0d75-270">The Oozie Web UI defaults to displaying running Workflow Jobs.</span></span> <span data-ttu-id="a0d75-271">Чтобы просмотреть все задания рабочего процесса, выберите **All Jobs**.</span><span class="sxs-lookup"><span data-stu-id="a0d75-271">To see all workflow jobs, select **All Jobs**.</span></span>

    ![Отображаются все задания](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="a0d75-273">Чтобы просмотреть дополнительные сведения о задании, выберите это задание.</span><span class="sxs-lookup"><span data-stu-id="a0d75-273">Select a job to view more information about the job.</span></span>

    ![Job Info](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="a0d75-275">На вкладке "Сведения о работе" можно просмотреть базовую информацию о задании, а также отдельные действия в рамках задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-275">From the Job Info tab, you can see basic job information and the individual actions within the job.</span></span> <span data-ttu-id="a0d75-276">С помощью вкладок вверху можно просмотреть определение задания, конфигурацию задания, обратиться к журналу задания или просмотреть направленный ациклический граф (DAG) задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-276">Using the tabs at the top you can view the Job Definition, Job Configuration, access the Job Log or view a Directed Acyclic Graph (DAG) of the job.</span></span>

   * <span data-ttu-id="a0d75-277">**Журнал задания**: нажмите кнопку **GetLogs** для просмотра всех журналов задания или воспользуйтесь полем **Enter Search Filter** (Введите фильтр поиска) для выбора журналов с помощью фильтра.</span><span class="sxs-lookup"><span data-stu-id="a0d75-277">**Job Log**: Select the **GetLogs** button to get all logs for the job, or use the **Enter Search Filter** field to filter logs</span></span>

       ![Журнал задания](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="a0d75-279">**JobDAG**: DAG представляет собой графическое представление путей данных рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="a0d75-279">**JobDAG**: The DAG is a graphical overview of the data paths taken through the workflow</span></span>

       ![Направленный ациклический граф задания](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="a0d75-281">Выбрав одно из действий на вкладке **Job Info** (Сведения о задании), вы увидите информацию об этом действии.</span><span class="sxs-lookup"><span data-stu-id="a0d75-281">Selecting one of the actions from the **Job Info** tab brings up information for the action.</span></span> <span data-ttu-id="a0d75-282">Например, выберите действие **RunHiveScript** .</span><span class="sxs-lookup"><span data-stu-id="a0d75-282">For example, select the **RunHiveScript** action.</span></span>

    ![Информация о действии](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="a0d75-284">Вы можете просмотреть подробную информацию о действии, например ссылку на **URL-адрес консоли**.</span><span class="sxs-lookup"><span data-stu-id="a0d75-284">You can see details for the action, such as a link to the **Console URL**.</span></span> <span data-ttu-id="a0d75-285">Используйте эту ссылку для просмотра сведений о задании в JobTracker.</span><span class="sxs-lookup"><span data-stu-id="a0d75-285">This link can be used to view JobTracker information for the job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="a0d75-286">Планирование заданий</span><span class="sxs-lookup"><span data-stu-id="a0d75-286">Scheduling jobs</span></span>

<span data-ttu-id="a0d75-287">Координатор позволяет указать время начала, окончания и частоту выполнения заданий.</span><span class="sxs-lookup"><span data-stu-id="a0d75-287">The coordinator allows you to specify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="a0d75-288">Чтобы задать расписание для рабочего процесса выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a0d75-288">To define a schedule for the workflow, use the following steps:</span></span>

1. <span data-ttu-id="a0d75-289">Выполните следующую команду для создания файла с именем **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="a0d75-289">Use the following to create a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="a0d75-290">Используйте следующий код XML в качестве содержимого файла:</span><span class="sxs-lookup"><span data-stu-id="a0d75-290">Use the following XML as the contents of the file:</span></span>

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
    > <span data-ttu-id="a0d75-291">При запуске задания переменные `${...}` будут заменены значениями, указанными в определении задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-291">The `${...}` variables are replaced by values in the job definition at run-time.</span></span> <span data-ttu-id="a0d75-292">Используются следующие переменные:</span><span class="sxs-lookup"><span data-stu-id="a0d75-292">The variables are:</span></span>
    >
    > * <span data-ttu-id="a0d75-293">`${coordFrequency}`: интервал времени между запуском повторных экземпляров задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-293">`${coordFrequency}`: Time between running instances of the job.</span></span>
    > <span data-ttu-id="a0d75-294">** `${coordStart}`: время запуска задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-294">** `${coordStart}`: The job start time.</span></span>
    > * <span data-ttu-id="a0d75-295">`${coordEnd}`: время завершения задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-295">`${coordEnd}`: The job end time.</span></span>
    > * <span data-ttu-id="a0d75-296">`${coordTimezone}`: задания координатора задаются для конкретного часового пояса без летнего времени (обычно представляется в виде времени в формате UTC).</span><span class="sxs-lookup"><span data-stu-id="a0d75-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="a0d75-297">Этот часовой пояс называется часовым поясом обработки Oozie.</span><span class="sxs-lookup"><span data-stu-id="a0d75-297">This time zone is referred as the "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="a0d75-298">`${wfPath}`: путь к файлу workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="a0d75-298">`${wfPath}`: The path to the workflow.xml.</span></span>

2. <span data-ttu-id="a0d75-299">Чтобы сохранить файл, нажмите клавиши **CTRL+X**, затем — **Y** и ВВОД.</span><span class="sxs-lookup"><span data-stu-id="a0d75-299">To save the file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="a0d75-300">Чтобы скопировать этот файл в рабочий каталог задания, воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a0d75-300">Use the following command to copy the file to the working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="a0d75-301">Для изменения файла **job.xml** воспользуйтесь следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a0d75-301">Use the following to modify the **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="a0d75-302">Выполните следующие изменения:</span><span class="sxs-lookup"><span data-stu-id="a0d75-302">Make the following changes:</span></span>

   * <span data-ttu-id="a0d75-303">Чтобы служба Oozie запускала файл координатора вместо файла рабочего процесса, измените `<name>oozie.wf.application.path</name>` на `<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-303">To instruct oozie to run the coordinator file instead of the workflow, change `<name>oozie.wf.application.path</name>` to `<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="a0d75-304">Чтобы задать переменную `workflowPath`, используемую координатором, добавьте следующий код XML:</span><span class="sxs-lookup"><span data-stu-id="a0d75-304">To set the `workflowPath` variable used by the coordinator, add the following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="a0d75-305">Замените текст `wasb://mycontainer@mystorageaccount.blob.core.windows` значением, которое используется в других записях файла job.xml.</span><span class="sxs-lookup"><span data-stu-id="a0d75-305">Replace the `wasb://mycontainer@mystorageaccount.blob.core.windows` text with the value used in other entries in the job.xml file.</span></span>

   * <span data-ttu-id="a0d75-306">Чтобы определить начало, окончание и частоту выполнения для координатора, добавьте следующий код XML:</span><span class="sxs-lookup"><span data-stu-id="a0d75-306">To define the start, end, and frequency for the coordinator, add the following XML:</span></span>

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

       <span data-ttu-id="a0d75-307">Приведенные выше значения задают время начала — 12:00 10 мая 2017 года, а время окончания — 12 мая 2017 года.</span><span class="sxs-lookup"><span data-stu-id="a0d75-307">These values set the start time to 12:00PM on May 10, 2017, the end time to May 12, 2017.</span></span> <span data-ttu-id="a0d75-308">интервал запуска — "ежедневно".</span><span class="sxs-lookup"><span data-stu-id="a0d75-308">The interval for running this job daily.</span></span> <span data-ttu-id="a0d75-309">Интервал задается в минутах, то есть 24 часа x 60 минут = 1440 минут.</span><span class="sxs-lookup"><span data-stu-id="a0d75-309">The frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="a0d75-310">Наконец, часовой пояс устанавливается в UTC.</span><span class="sxs-lookup"><span data-stu-id="a0d75-310">Finally, the timezone is set to UTC.</span></span>

5. <span data-ttu-id="a0d75-311">Нажмите клавиши Ctrl + X, затем **Y** и **ВВОД**, чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="a0d75-311">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

6. <span data-ttu-id="a0d75-312">Для запуска задания используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a0d75-312">To run the job, use the following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="a0d75-313">Эта команда отправляет и запускает задание.</span><span class="sxs-lookup"><span data-stu-id="a0d75-313">This command submits and starts the job.</span></span>

7. <span data-ttu-id="a0d75-314">Если вы зайдете в веб-интерфейс Oozie и выберете вкладку **Coordinator Jobs** (Задания координатора), то увидите следующую информацию:</span><span class="sxs-lookup"><span data-stu-id="a0d75-314">If you visit the Oozie Web UI and select the **Coordinator Jobs** tab, you see information similar to the following image:</span></span>

    ![Вкладка задания координатора](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="a0d75-316">Запись **Next Materialization** (Следующая материализация) определяет момент следующего запуска задания.</span><span class="sxs-lookup"><span data-stu-id="a0d75-316">The **Next Materialization** entry contains the next time that the job runs.</span></span>

8. <span data-ttu-id="a0d75-317">Как и для предыдущих заданий рабочего процесса, вы можете выбрать это задание в веб-интерфейсе и увидеть информацию о нем:</span><span class="sxs-lookup"><span data-stu-id="a0d75-317">Similar to the earlier workflow job, selecting the job entry in the web UI displays information on the job:</span></span>

    ![Информация о задании координатора](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="a0d75-319">На этом изображении показаны только сведения об успешных запусках задания, а не сведения об отдельных действиях запланированного рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="a0d75-319">This image only shows successful runs of the job, not individual actions within the scheduled workflow.</span></span> <span data-ttu-id="a0d75-320">Для ее просмотра выберите одну из записей **Action** .</span><span class="sxs-lookup"><span data-stu-id="a0d75-320">To see that, select one of the **Action** entries.</span></span>

    ![Информация о действии](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="a0d75-322">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="a0d75-322">Troubleshooting</span></span>

<span data-ttu-id="a0d75-323">Вы можете просматривать журналы Oozie с помощью пользовательского интерфейса Oozie.</span><span class="sxs-lookup"><span data-stu-id="a0d75-323">The Oozie UI allows you to view Oozie logs.</span></span> <span data-ttu-id="a0d75-324">Он также содержит ссылки на журналы JobTracker для заданий MapReduce, запущенных рабочим процессом.</span><span class="sxs-lookup"><span data-stu-id="a0d75-324">It also contains links to JobTracker logs for MapReduce tasks started by the workflow.</span></span> <span data-ttu-id="a0d75-325">Действия по решению проблемы должны подчиняться следующему шаблону:</span><span class="sxs-lookup"><span data-stu-id="a0d75-325">The pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="a0d75-326">Просмотрите информацию о задании в веб-интерфейсе Oozie.</span><span class="sxs-lookup"><span data-stu-id="a0d75-326">View the job in Oozie Web UI.</span></span>

2. <span data-ttu-id="a0d75-327">Если произошел сбой или ошибка для конкретного действия, выберите действие и посмотрите, не содержится ли в поле **Error Message** дополнительной информации об ошибке.</span><span class="sxs-lookup"><span data-stu-id="a0d75-327">If there is an error or failure for a specific action, select the action to see if the **Error Message** field provides more information on the failure.</span></span>

3. <span data-ttu-id="a0d75-328">Если известен URL действия, воспользуйтесь им для просмотра дополнительной информации о действии (например, журналов JobTracker).</span><span class="sxs-lookup"><span data-stu-id="a0d75-328">If available, use the URL from the action to view more details (such as JobTracker logs) for the action.</span></span>

<span data-ttu-id="a0d75-329">Ниже приведены конкретные ошибки, которые могут возникнуть, и способы их устранения.</span><span class="sxs-lookup"><span data-stu-id="a0d75-329">The following are specific errors you may encounter, and how to resolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="a0d75-330">JA009: Не удается инициализировать кластер</span><span class="sxs-lookup"><span data-stu-id="a0d75-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="a0d75-331">**Симптомы**. Состояние задания изменяется на **SUSPENDED** (Приостановлено).</span><span class="sxs-lookup"><span data-stu-id="a0d75-331">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="a0d75-332">В подробной информации о задании состояние RunHiveScript отображается как **START_MANUAL** (Ручной запуск).</span><span class="sxs-lookup"><span data-stu-id="a0d75-332">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="a0d75-333">При выборе действия отображается следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="a0d75-333">Selecting the action displays the following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="a0d75-334">**Причина**. WASB-адреса, используемые в файле **job.xml**, не содержат контейнер хранилища или имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="a0d75-334">**Cause**: The WASB addresses used in the **job.xml** file do not contain the storage container or storage account name.</span></span> <span data-ttu-id="a0d75-335">Формат адреса WASB должен быть следующим `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="a0d75-335">The WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="a0d75-336">**Решение**: Измените адреса WASB, используемые заданием.</span><span class="sxs-lookup"><span data-stu-id="a0d75-336">**Resolution**: Change the WASB addresses used by the job.</span></span>

### <a name="ja002-oozie-is-not-allowed-to-impersonate-ltuser"></a><span data-ttu-id="a0d75-337">JA002: Oozie не разрешено работать от имени &lt;ПОЛЬЗОВАТЕЛЬ></span><span class="sxs-lookup"><span data-stu-id="a0d75-337">JA002: Oozie is not allowed to impersonate &lt;USER></span></span>

<span data-ttu-id="a0d75-338">**Симптомы**. Состояние задания изменяется на **SUSPENDED** (Приостановлено).</span><span class="sxs-lookup"><span data-stu-id="a0d75-338">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="a0d75-339">В подробной информации о задании состояние RunHiveScript отображается как **START_MANUAL** (Ручной запуск).</span><span class="sxs-lookup"><span data-stu-id="a0d75-339">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="a0d75-340">При выборе действия отображается следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="a0d75-340">Selecting the action shows the following error message:</span></span>

    JA002: User: oozie is not allowed to impersonate <USER>

<span data-ttu-id="a0d75-341">**Причина**: Текущие права доступа не позволяют Oozie работать от имени учетной записи указанного пользователя.</span><span class="sxs-lookup"><span data-stu-id="a0d75-341">**Cause**: Current permission settings do not allow Oozie to impersonate the specified user account.</span></span>

<span data-ttu-id="a0d75-342">**Решение**. Oozie не разрешено работать от имени пользователей из группы **users**.</span><span class="sxs-lookup"><span data-stu-id="a0d75-342">**Resolution**: Oozie is allowed to impersonate users in the **users** group.</span></span> <span data-ttu-id="a0d75-343">Для просмотра групп, в которые входит данный пользователь, воспользуйтесь командой `groups USERNAME` .</span><span class="sxs-lookup"><span data-stu-id="a0d75-343">Use the `groups USERNAME` to see the groups that the user account is a member of.</span></span> <span data-ttu-id="a0d75-344">Если пользователь не является членом группы **users**, добавьте его в группу следующей командой:</span><span class="sxs-lookup"><span data-stu-id="a0d75-344">If the user is not a member of the **users** group, use the following command to add the user to the group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="a0d75-345">Чтобы HDInsight понял, что пользователь добавлен в группу, может потребоваться несколько минут.</span><span class="sxs-lookup"><span data-stu-id="a0d75-345">It may take several minutes before HDInsight recognizes that the user has been added to the group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="a0d75-346">ОШИБКА запуска (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="a0d75-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="a0d75-347">**Симптомы**. Состояние задания изменяется на **KILLED** (Прекращено).</span><span class="sxs-lookup"><span data-stu-id="a0d75-347">**Symptoms**: The job status changes to **KILLED**.</span></span> <span data-ttu-id="a0d75-348">В подробной информации о задании состояние RunSqoopExport отображается как **ERROR** (Ошибка).</span><span class="sxs-lookup"><span data-stu-id="a0d75-348">Details for the job show the RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="a0d75-349">При выборе действия отображается следующее сообщение об ошибке:</span><span class="sxs-lookup"><span data-stu-id="a0d75-349">Selecting the action shows the following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="a0d75-350">**Причина**: Sqoop не удалось загрузить драйвер базы данных, необходимый для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="a0d75-350">**Cause**: Sqoop is unable to load the database driver required to access the database.</span></span>

<span data-ttu-id="a0d75-351">**Решение.** При использовании Sqoop из задания Oozie необходимо включить драйвер базы данных в ресурсы, используемые заданием (в файле workflow.xml).</span><span class="sxs-lookup"><span data-stu-id="a0d75-351">**Resolution**: When using Sqoop from an Oozie job, you must include the database driver with the other resources (such as the workflow.xml) used by the job.</span></span> <span data-ttu-id="a0d75-352">Также укажите архив, содержащий драйвер базы данных, из раздела `<sqoop>...</sqoop>` файла workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="a0d75-352">Also Reference the archive containing the database driver from the `<sqoop>...</sqoop>` section of the workflow.xml.</span></span>

<span data-ttu-id="a0d75-353">Например, для задания в этом документе необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="a0d75-353">For example, for the job in this document, you would use the following steps:</span></span>

1. <span data-ttu-id="a0d75-354">Скопируйте файл sqljdbc4.1.jar в каталог /tutorials/useoozie:</span><span class="sxs-lookup"><span data-stu-id="a0d75-354">Copy the sqljdbc4.1.jar file to the /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="a0d75-355">Измените файл workflow.xml, добавив следующие строки кода XML над `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="a0d75-355">Modify the workflow.xml to add the following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="a0d75-356">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a0d75-356">Next steps</span></span>

<span data-ttu-id="a0d75-357">Из этого руководства вы узнали, как задать рабочий процесс Oozie и как запустить задание Oozie.</span><span class="sxs-lookup"><span data-stu-id="a0d75-357">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job.</span></span> <span data-ttu-id="a0d75-358">Дополнительные сведения о работе с HDInsight приведены в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="a0d75-358">To learn more about working with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="a0d75-359">[Используйте учитывающий время координатор Oozie с Hadoop в HDInsight для определения рабочих процессов и координации заданий][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="a0d75-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="a0d75-360">[Отправка данных для заданий Hadoop в HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="a0d75-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="a0d75-361">[Использование Sqoop с Hadoop в HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="a0d75-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="a0d75-362">[Использование Hive с Hadoop в HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="a0d75-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="a0d75-363">[Использование Pig с Hadoop в HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="a0d75-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="a0d75-364">[Разработка программ MapReduce на Java для Hadoop в HDInsight на платформе Linux][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="a0d75-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
