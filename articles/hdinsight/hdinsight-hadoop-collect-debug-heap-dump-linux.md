---
title: "дампы кучи aaaEnable службам Hadoop в HDInsight - Azure | Документы Microsoft"
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
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="a5976-103">Включение дампов кучи для служб Hadoop в HDInsight под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="a5976-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="a5976-104">Файлы дампа кучи содержат снимок памяти приложения hello, включая hello значения переменных во время создания дампа hello hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="a5976-105">Поэтому они полезны для диагностики проблем, возникающих во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="a5976-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5976-106">Hello действия, описанные в этом документе работают только с кластерами HDInsight, использующих Linux.</span><span class="sxs-lookup"><span data-stu-id="a5976-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="a5976-107">Linux — hello только операционную систему, используемую в HDInsight версии 3.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a5976-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a5976-108">Дополнительные сведения см. в разделе [Приближается дата прекращения сопровождения HDI версии 3.3](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a5976-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="a5976-109"><a name="whichServices"></a>Службы</span><span class="sxs-lookup"><span data-stu-id="a5976-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="a5976-110">Можно включить дампы кучи для hello следующие службы:</span><span class="sxs-lookup"><span data-stu-id="a5976-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="a5976-111">**Hcatalog** — tempelton;</span><span class="sxs-lookup"><span data-stu-id="a5976-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="a5976-112">**Hive** — hiveserver2, metastore, derbyserver;</span><span class="sxs-lookup"><span data-stu-id="a5976-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="a5976-113">**Mapreduce** — jobhistoryserver;</span><span class="sxs-lookup"><span data-stu-id="a5976-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="a5976-114">**Yarn** — resourcemanager, nodemanager, timelineserver;</span><span class="sxs-lookup"><span data-stu-id="a5976-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="a5976-115">**HDFS** — datanode, secondarynamenode, namenode.</span><span class="sxs-lookup"><span data-stu-id="a5976-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="a5976-116">Можно также включить дампы кучи для карты hello и уменьшить процессы выполнялись по HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a5976-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="a5976-117"><a name="configuration"></a>Основные сведения о настройке дампа кучи</span><span class="sxs-lookup"><span data-stu-id="a5976-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="a5976-118">Дампы памяти кучи включены путем передачи параметров (также известных как opts, или параметров) toohello виртуальной машины Java при запуске службы.</span><span class="sxs-lookup"><span data-stu-id="a5976-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="a5976-119">Для большинства служб Hadoop службы hello оболочки скрипту toostart hello toopass могут изменять эти параметры.</span><span class="sxs-lookup"><span data-stu-id="a5976-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="a5976-120">В каждом сценарии является экспорта для  **\* \_OPTS**, который содержит параметры hello передан toohello виртуальной машины Java.</span><span class="sxs-lookup"><span data-stu-id="a5976-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="a5976-121">В примере hello **hadoop env.sh** скрипта, строка hello начинается с `export HADOOP_NAMENODE_OPTS=` содержит параметры hello для hello NameNode службы.</span><span class="sxs-lookup"><span data-stu-id="a5976-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="a5976-122">Сопоставления и уменьшения процессы могут немного отличаться, как эти операции являются дочерний процесс hello MapReduce службы.</span><span class="sxs-lookup"><span data-stu-id="a5976-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="a5976-123">Каждый сопоставления или уменьшите процесс выполняется в дочернем контейнере и присутствуют две записи, которые содержат параметры виртуальной машины Java hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="a5976-124">Оба содержатся в файле **mapred-site.xml**:</span><span class="sxs-lookup"><span data-stu-id="a5976-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="a5976-125">**MapReduce.Admin.map.child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="a5976-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="a5976-126">**mapreduce.admin.reduce.child.java.opts**</span><span class="sxs-lookup"><span data-stu-id="a5976-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="a5976-127">Рекомендуется с помощью Ambari hello toomodify обоих сценариев и параметры mapred-site.xml как Ambari обработки репликации изменений на узлах в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="a5976-128">В разделе hello [с помощью Ambari](#using-ambari) раздел конкретные действия.</span><span class="sxs-lookup"><span data-stu-id="a5976-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="a5976-129">Включение дампов кучи</span><span class="sxs-lookup"><span data-stu-id="a5976-129">Enable heap dumps</span></span>

<span data-ttu-id="a5976-130">Hello следующий параметр обеспечивает кучи файлы дампа при возникновении OutOfMemoryError:</span><span class="sxs-lookup"><span data-stu-id="a5976-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="a5976-131">Hello  **+**  указывает, что этот параметр включен.</span><span class="sxs-lookup"><span data-stu-id="a5976-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="a5976-132">по умолчанию Hello отключено.</span><span class="sxs-lookup"><span data-stu-id="a5976-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="a5976-133">Файлы дампа кучи не включены для служб Hadoop в HDInsight по умолчанию, как файлы дампа hello могут быть большими.</span><span class="sxs-lookup"><span data-stu-id="a5976-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="a5976-134">При включении их для устранения неполадок, помните toodisable их после воспроизвести hello проблемы и файлы дампа собрана hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="a5976-135">Расположение дампа</span><span class="sxs-lookup"><span data-stu-id="a5976-135">Dump location</span></span>

<span data-ttu-id="a5976-136">расположение по умолчанию Hello для файла дампа hello — hello текущий рабочий каталог.</span><span class="sxs-lookup"><span data-stu-id="a5976-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="a5976-137">Можно выбрать, где hello файл хранится с использованием hello следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="a5976-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="a5976-138">Например, с помощью `-XX:HeapDumpPath=/tmp` вызывает toobe дампы hello, хранятся в каталоге/tmp hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="a5976-139">Сценарии</span><span class="sxs-lookup"><span data-stu-id="a5976-139">Scripts</span></span>

<span data-ttu-id="a5976-140">Вы можете также запустить сценарий при возникновении ошибки **OutOfMemoryError** .</span><span class="sxs-lookup"><span data-stu-id="a5976-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="a5976-141">Например возникла запуска уведомление, чтобы быть в курсе ошибку hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="a5976-142">Используйте следующие hello параметр tootrigger сценарий на __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="a5976-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="a5976-143">Поскольку Hadoop распределенных систем, необходимо поместить сценарий, используемый на всех узлах в кластере hello, на котором запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="a5976-144">сценарий Hello должен также быть в расположении, которое доступно для hello hello служба выполняется как и необходимо предоставить разрешения выполнение.</span><span class="sxs-lookup"><span data-stu-id="a5976-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="a5976-145">Например, можно назвать toostore сценариев в `/usr/local/bin` и использовать `chmod go+rx /usr/local/bin/filename.sh` toogrant разрешения read и execute.</span><span class="sxs-lookup"><span data-stu-id="a5976-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="a5976-146">Использование Ambari</span><span class="sxs-lookup"><span data-stu-id="a5976-146">Using Ambari</span></span>

<span data-ttu-id="a5976-147">toomodify hello конфигурации для службы, hello используйте следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="a5976-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="a5976-148">Откройте hello Ambari web пользовательского интерфейса для кластера.</span><span class="sxs-lookup"><span data-stu-id="a5976-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="a5976-149">URL-адрес Hello — https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="a5976-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="a5976-150">В ответ на запрос проверки подлинности toohello сайт, используя имя учетной записи hello HTTP (по умолчанию: администратора) и пароль для кластера.</span><span class="sxs-lookup"><span data-stu-id="a5976-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a5976-151">Вам могут запрашиваться во второй раз, Ambari hello имя пользователя и пароль.</span><span class="sxs-lookup"><span data-stu-id="a5976-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="a5976-152">В этом случае введите hello же имя учетной записи и пароль</span><span class="sxs-lookup"><span data-stu-id="a5976-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="a5976-153">Используя список hello hello слева, выберите область hello службы, которую необходимо toomodify.</span><span class="sxs-lookup"><span data-stu-id="a5976-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="a5976-154">Например, **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="a5976-154">For example, **HDFS**.</span></span> <span data-ttu-id="a5976-155">В центре hello установите hello **Configs** вкладки.</span><span class="sxs-lookup"><span data-stu-id="a5976-155">In hello center area, select hello **Configs** tab.</span></span>

    ![Сеть Ambari с выбранной вкладкой конфигурации HDFS](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="a5976-157">С помощью hello **фильтра...**  запись, введите **opts**.</span><span class="sxs-lookup"><span data-stu-id="a5976-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="a5976-158">Отобразятся только те элементы, в которых есть этот текст.</span><span class="sxs-lookup"><span data-stu-id="a5976-158">Only items containing this text are displayed.</span></span>

    ![Фильтрованный список](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="a5976-160">Найти hello  **\* \_OPTS** tooenable обратиться в запись для службы hello tooenable дампы кучи для и добавьте параметры hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="a5976-161">В следующие изображения hello, я добавил `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** входа:</span><span class="sxs-lookup"><span data-stu-id="a5976-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS с -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="a5976-163">При включении дампы кучи для hello подключить или уменьшить дочерний процесс, найдите hello поля с именем **mapreduce.admin.map.child.java.opts** и **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="a5976-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="a5976-164">Используйте hello **Сохранить** кнопку toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="a5976-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="a5976-165">Можно ввести краткое примечание, описывающее изменения hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="a5976-166">После применения изменений hello hello **требуется перезапуск** значок отображается рядом с одной или нескольких служб.</span><span class="sxs-lookup"><span data-stu-id="a5976-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![Значок «Требуется перезапуск» и кнопка «Перезапуск»](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="a5976-168">Выберите каждую службу, которая требует перезагрузки и использовать hello **действий службы** кнопку слишком**включить в режим обслуживания**.</span><span class="sxs-lookup"><span data-stu-id="a5976-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="a5976-169">Режим обслуживания предотвращает создание предупреждений от службы hello при повторном запуске.</span><span class="sxs-lookup"><span data-stu-id="a5976-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![Включение меню режима обслуживания](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="a5976-171">После включения режима обслуживания, используют hello **перезапустите** кнопку для службы hello слишком**перезапустите все устаревший**</span><span class="sxs-lookup"><span data-stu-id="a5976-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![Перезапустить все затронутые записи](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="a5976-173">Здравствуйте, записи для hello **перезапустите** кнопка может быть разным для других служб.</span><span class="sxs-lookup"><span data-stu-id="a5976-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="a5976-174">После перезапуска службы hello использовать hello **действий службы** кнопку слишком**включить выключение режима обслуживания**.</span><span class="sxs-lookup"><span data-stu-id="a5976-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="a5976-175">Это tooresume Ambari, наблюдение за оповещения для службы hello.</span><span class="sxs-lookup"><span data-stu-id="a5976-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

