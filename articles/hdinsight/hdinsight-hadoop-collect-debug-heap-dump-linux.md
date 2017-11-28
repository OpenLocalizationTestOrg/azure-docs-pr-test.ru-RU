---
title: "Включение дампов кучи для служб Hadoop в HDInsight — Azure | Документы Майкрософт"
description: "Включение дампов кучи для служб Hadoop с кластеров HDInsight, работающих под управлением Linux, для отладки и анализа."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 59942e989d622c2486edf181d76e13344c71e6f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="20923-103">Включение дампов кучи для служб Hadoop в HDInsight под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="20923-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="20923-104">Дампы кучи содержат снимок памяти приложения, включая значения переменных на момент создания дампа.</span><span class="sxs-lookup"><span data-stu-id="20923-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="20923-105">Поэтому они полезны для диагностики проблем, возникающих во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="20923-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20923-106">Шаги, описанные в этом документе, можно применять только к кластерам HDInsight под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="20923-106">The steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="20923-107">Linux — это единственная операционная система, используемая для работы с HDInsight 3.4 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="20923-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="20923-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="20923-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="20923-109"><a name="whichServices"></a>Службы</span><span class="sxs-lookup"><span data-stu-id="20923-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="20923-110">Вы можете включить дампы кучи для следующих служб:</span><span class="sxs-lookup"><span data-stu-id="20923-110">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="20923-111">**Hcatalog** — tempelton;</span><span class="sxs-lookup"><span data-stu-id="20923-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="20923-112">**Hive** — hiveserver2, metastore, derbyserver;</span><span class="sxs-lookup"><span data-stu-id="20923-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="20923-113">**Mapreduce** — jobhistoryserver;</span><span class="sxs-lookup"><span data-stu-id="20923-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="20923-114">**Yarn** — resourcemanager, nodemanager, timelineserver;</span><span class="sxs-lookup"><span data-stu-id="20923-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="20923-115">**HDFS** — datanode, secondarynamenode, namenode.</span><span class="sxs-lookup"><span data-stu-id="20923-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="20923-116">Вы можете также включить дампы кучи для процессов сопоставления и уменьшения, запущенных HDInsight.</span><span class="sxs-lookup"><span data-stu-id="20923-116">You can also enable heap dumps for the map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="20923-117"><a name="configuration"></a>Основные сведения о настройке дампа кучи</span><span class="sxs-lookup"><span data-stu-id="20923-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="20923-118">Дампы кучи включаются путем передачи параметров в виртуальную машину Java при запуске службы.</span><span class="sxs-lookup"><span data-stu-id="20923-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) to the JVM when a service is started.</span></span> <span data-ttu-id="20923-119">Чтобы передать эти параметры, для большинства служб Hadoop можно изменить сценарий оболочки, используемый для запуска службы.</span><span class="sxs-lookup"><span data-stu-id="20923-119">For most Hadoop services, you can modify the shell script used to start the service to pass these options.</span></span>

<span data-ttu-id="20923-120">В каждом сценарии есть экспорт для **\*\_OPTS**, который содержит параметры, передаваемые в виртуальную машину Java.</span><span class="sxs-lookup"><span data-stu-id="20923-120">In each script, there is an export for **\*\_OPTS**, which contains the options passed to the JVM.</span></span> <span data-ttu-id="20923-121">Например, в сценарии **hadoop-env.sh** строка, начинающаяся с `export HADOOP_NAMENODE_OPTS=`, содержит параметры для службы NameNode.</span><span class="sxs-lookup"><span data-stu-id="20923-121">For example, in the **hadoop-env.sh** script, the line that begins with `export HADOOP_NAMENODE_OPTS=` contains the options for the NameNode service.</span></span>

<span data-ttu-id="20923-122">Процессы сопоставления и уменьшения немного отличаются друг от друга, поскольку эти операции являются дочерним процессом службы MapReduce.</span><span class="sxs-lookup"><span data-stu-id="20923-122">Map and reduce processes are slightly different, as these operations are a child process of the MapReduce service.</span></span> <span data-ttu-id="20923-123">Каждый процесс сопоставления или уменьшения запускается в дочернем контейнере и существуют две записи, содержащие параметры виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="20923-123">Each map or reduce process runs in a child container, and there are two entries that contain the JVM options.</span></span> <span data-ttu-id="20923-124">Оба содержатся в файле **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="20923-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="20923-125">**MapReduce.Admin.map.child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="20923-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="20923-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="20923-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="20923-127">Рекомендуется использовать платформу Ambari для изменения сценариев и параметров mapred-site.xml, поскольку Ambari обрабатывает репликации изменений по всем узлам в кластере.</span><span class="sxs-lookup"><span data-stu-id="20923-127">We recommend using Ambari to modify both the scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in the cluster.</span></span> <span data-ttu-id="20923-128">Подробные сведения см. в разделе [Использование Ambari](#using-ambari).</span><span class="sxs-lookup"><span data-stu-id="20923-128">See the [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="20923-129">Включение дампов кучи</span><span class="sxs-lookup"><span data-stu-id="20923-129">Enable heap dumps</span></span>

<span data-ttu-id="20923-130">Следующий параметр включает дампы кучи при возникновении ошибки OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="20923-130">The following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="20923-131">Знак **+** означает, что этот параметр включен.</span><span class="sxs-lookup"><span data-stu-id="20923-131">The **+** indicates that this option is enabled.</span></span> <span data-ttu-id="20923-132">По умолчанию — отключен.</span><span class="sxs-lookup"><span data-stu-id="20923-132">The default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="20923-133">Дампы кучи для службы Hadoop в HDInsight не включены по умолчанию, поскольку файлы дампов могут быть очень большими.</span><span class="sxs-lookup"><span data-stu-id="20923-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as the dump files can be large.</span></span> <span data-ttu-id="20923-134">Включив их для устранения неполадок, не забудьте потом отключить, когда проблема будет воспроизведена и собраны файлы дампа.</span><span class="sxs-lookup"><span data-stu-id="20923-134">If you do enable them for troubleshooting, remember to disable them once you have reproduced the problem and gathered the dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="20923-135">Расположение дампа</span><span class="sxs-lookup"><span data-stu-id="20923-135">Dump location</span></span>

<span data-ttu-id="20923-136">По умолчанию файл дампа располагается в текущем рабочем каталоге.</span><span class="sxs-lookup"><span data-stu-id="20923-136">The default location for the dump file is the current working directory.</span></span> <span data-ttu-id="20923-137">Место сохранения файла можно выбрать, используя следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="20923-137">You can control where the file is stored using the following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="20923-138">Например, с помощью `-XX:HeapDumpPath=/tmp` задается место для сохранения дампов в каталоге /tmp.</span><span class="sxs-lookup"><span data-stu-id="20923-138">For example, using `-XX:HeapDumpPath=/tmp` causes the dumps to be stored in the /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="20923-139">Сценарии</span><span class="sxs-lookup"><span data-stu-id="20923-139">Scripts</span></span>

<span data-ttu-id="20923-140">Вы можете также запустить сценарий при возникновении ошибки **OutOfMemoryError** .</span><span class="sxs-lookup"><span data-stu-id="20923-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="20923-141">Например, можно запустить уведомление, благодаря которому можно будет узнать, что произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="20923-141">For example, triggering a notification so you know that the error has occurred.</span></span> <span data-ttu-id="20923-142">При возникновении ошибки __OutOfMemoryError__ используйте следующий параметр для запуска сценария:</span><span class="sxs-lookup"><span data-stu-id="20923-142">Use the following option to trigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="20923-143">Поскольку Hadoop является распределенной системой, каждый используемый сценарий необходимо помещать во все узлы кластера, на которых запущена служба.</span><span class="sxs-lookup"><span data-stu-id="20923-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in the cluster that the service runs on.</span></span>
> 
> <span data-ttu-id="20923-144">Сценарий также должен быть в расположении, доступном из учетной записи, с использованием которой запущена служба, и необходимо предоставить разрешение на выполнение.</span><span class="sxs-lookup"><span data-stu-id="20923-144">The script must also be in a location that is accessible by the account the service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="20923-145">Например, вы можете сохранить сценарии в `/usr/local/bin` и использовать `chmod go+rx /usr/local/bin/filename.sh` для предоставления прав на чтение и выполнение.</span><span class="sxs-lookup"><span data-stu-id="20923-145">For example, you may wish to store scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` to grant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="20923-146">Использование Ambari</span><span class="sxs-lookup"><span data-stu-id="20923-146">Using Ambari</span></span>

<span data-ttu-id="20923-147">Чтобы изменить конфигурацию службы, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="20923-147">To modify the configuration for a service, use the following steps:</span></span>

1. <span data-ttu-id="20923-148">Откройте веб-интерфейс Ambari для вашего кластера.</span><span class="sxs-lookup"><span data-stu-id="20923-148">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="20923-149">URL-адрес: https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="20923-149">The URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="20923-150">В ответ на запрос войдите на сайт с помощью имени учетной записи HTTP (по умолчанию — admin) и пароля для вашего кластера.</span><span class="sxs-lookup"><span data-stu-id="20923-150">When prompted, authenticate to the site using the HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="20923-151">Может потребоваться еще раз ввести имя пользователя и пароль по запросу Ambari.</span><span class="sxs-lookup"><span data-stu-id="20923-151">You may be prompted a second time by Ambari for the user name and password.</span></span> <span data-ttu-id="20923-152">В этом случае введите те же имя учетной записи и пароль.</span><span class="sxs-lookup"><span data-stu-id="20923-152">If so, enter the same account name and password</span></span>

2. <span data-ttu-id="20923-153">Используя список слева, выберите область службы, которую требуется изменить.</span><span class="sxs-lookup"><span data-stu-id="20923-153">Using the list of on the left, select the service area you want to modify.</span></span> <span data-ttu-id="20923-154">Например, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="20923-154">For example, **HDFS**.</span></span> <span data-ttu-id="20923-155">В центральной области выберите вкладку **Конфигурации** .</span><span class="sxs-lookup"><span data-stu-id="20923-155">In the center area, select the **Configs** tab.</span></span>

    ![Сеть Ambari с выбранной вкладкой конфигурации HDFS](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="20923-157">Используя запись **Фильтр...**, введите **параметры**.</span><span class="sxs-lookup"><span data-stu-id="20923-157">Using the **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="20923-158">Отобразятся только те элементы, в которых есть этот текст.</span><span class="sxs-lookup"><span data-stu-id="20923-158">Only items containing this text are displayed.</span></span>

    ![Фильтрованный список](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="20923-160">Найдите запись **\*\_OPTS** службы, для которой нужно включить дампы кучи, и добавьте параметры, которые требуется включить.</span><span class="sxs-lookup"><span data-stu-id="20923-160">Find the **\*\_OPTS** entry for the service you want to enable heap dumps for, and add the options you wish to enable.</span></span> <span data-ttu-id="20923-161">На изображении ниже вы можете увидеть, что я добавил `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` в запись **HADOOP\_NAMENODE\_OPTS**:</span><span class="sxs-lookup"><span data-stu-id="20923-161">In the following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` to the **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS с -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="20923-163">При включении дампов кучи для дочерних процессов сопоставления и уменьшения найдите поля **mapreduce.admin.map.child.java.opts** и **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="20923-163">When enabling heap dumps for the map or reduce child process, look for the fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="20923-164">Используйте кнопку **Сохранить** , чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="20923-164">Use the **Save** button to save the changes.</span></span> <span data-ttu-id="20923-165">Вы можете ввести краткое примечание, описывающее изменения.</span><span class="sxs-lookup"><span data-stu-id="20923-165">You can enter a short note describing the changes.</span></span>

5. <span data-ttu-id="20923-166">После применения изменений появится значок **Требуется перезапуск** рядом с одной или несколькими службами.</span><span class="sxs-lookup"><span data-stu-id="20923-166">Once the changes have been applied, the **Restart required** icon appears beside one or more services.</span></span>

    ![Значок «Требуется перезапуск» и кнопка «Перезапуск»](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="20923-168">Выберите все службы, которые требуют перезагрузки, и используйте кнопку **Действия службы** для **включения режима обслуживания**.</span><span class="sxs-lookup"><span data-stu-id="20923-168">Select each service that needs a restart, and use the **Service Actions** button to **Turn On Maintenance Mode**.</span></span> <span data-ttu-id="20923-169">Режим обслуживания не позволит создавать предупреждения от службы при ее перезапуске.</span><span class="sxs-lookup"><span data-stu-id="20923-169">Maintenance mode prevents alerts from being generated from the service when you restart it.</span></span>

    ![Включение меню режима обслуживания](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="20923-171">После включения режима обслуживания используйте кнопку **Перезапуск** для службы, чтобы **перезапустить все затронутые записи**.</span><span class="sxs-lookup"><span data-stu-id="20923-171">Once you have enabled maintenance mode, use the **Restart** button for the service to **Restart All Effected**</span></span>

    ![Перезапустить все затронутые записи](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="20923-173">записи для кнопки **Перезапуск** могут быть другими для других служб.</span><span class="sxs-lookup"><span data-stu-id="20923-173">the entries for the **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="20923-174">После перезапуска служб используйте кнопку **Действия службы** для **отключения режима обслуживания**.</span><span class="sxs-lookup"><span data-stu-id="20923-174">Once the services have been restarted, use the **Service Actions** button to **Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="20923-175">Эта Ambari для возобновления наблюдения за оповещениями для службы.</span><span class="sxs-lookup"><span data-stu-id="20923-175">This Ambari to resume monitoring for alerts for the service.</span></span>

