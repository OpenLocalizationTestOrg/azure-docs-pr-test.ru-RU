---
title: "Устранение неполадок в HBase с помощью Azure HDInsight | Документация Майкрософт"
description: "Получите ответы на распространенные вопросы о работе с HBase и Azure HDInsight."
services: hdinsight
documentationcenter: 
author: nitinver
manager: ashitg
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 7/7/2017
ms.author: nitinver
ms.openlocfilehash: 15412c3853a2b8436c5e96034c9a92a2a1094662
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="0a1d3-103">Устранение неполадок в HBase с помощью Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a1d3-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="0a1d3-104">Ознакомьтесь с основными проблемами и их разрешением при работе с полезными данными Apache HBase в Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-104">Learn about the top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="0a1d3-105">Как запускать отчеты о командах hbck с несколькими неназначенными регионами</span><span class="sxs-lookup"><span data-stu-id="0a1d3-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="0a1d3-106">При выполнении команды `hbase hbck` часто можно увидеть сообщение об ошибке "multiple regions being unassigned or holes in the chain of regions" (несколько регионов не назначены, или присутствуют пропуски в цепочке регионов).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-106">A common error message that you might see when you run the `hbase hbck` command is "multiple regions being unassigned or holes in the chain of regions."</span></span>

<span data-ttu-id="0a1d3-107">В пользовательском интерфейсе главного узла HBase можно увидеть количество регионов, которые не сбалансированы по всем региональным серверам.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-107">In the HBase Master UI, you can see the number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="0a1d3-108">Затем можно выполнить команду `hbase hbck`, чтобы увидеть пропуски в цепочке регионов.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-108">Then, you can run `hbase hbck` command to see holes in the region chain.</span></span>

<span data-ttu-id="0a1d3-109">Пропуски могут возникнуть по причине отключенных регионов, поэтому сначала следует исправить назначения.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-109">Holes might be caused by the offline regions, so fix the assignments first.</span></span> 

<span data-ttu-id="0a1d3-110">Чтобы вернуть неназначенные регионы в нормальное состояние, выполните такие действия:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-110">To bring the unassigned regions back to a normal state, complete the following steps:</span></span>

1. <span data-ttu-id="0a1d3-111">Войдите в кластер HDInsight HBase с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-111">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="0a1d3-112">Для подключения к оболочке ZooKeeper выполните команду `hbase zkcli`.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-112">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="0a1d3-113">Выполните команду `rmr /hbase/regions-in-transition` или `rmr /hbase-unsecure/regions-in-transition`.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-113">Run the `rmr /hbase/regions-in-transition` command or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="0a1d3-114">Для выхода из оболочки `hbase zkcli` используйте команду `exit`.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-114">To exit from the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="0a1d3-115">Откройте пользовательский интерфейс Ambari Apache и перезапустите службу активного главного узла HBase.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-115">Open the Apache Ambari UI, and then restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="0a1d3-116">Выполните команду `hbase hbck` еще раз (без каких-либо параметров).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-116">Run the `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="0a1d3-117">Проверьте выходные данные этой команды и убедитесь, что все регионы назначены.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-117">Check the output of this command to ensure that all regions are being assigned.</span></span>


## <span data-ttu-id="0a1d3-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Как устранить проблемы с временем ожидания при использовании команд hbck для назначения регионов</span><span class="sxs-lookup"><span data-stu-id="0a1d3-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="0a1d3-119">Проблема</span><span class="sxs-lookup"><span data-stu-id="0a1d3-119">Issue</span></span>

<span data-ttu-id="0a1d3-120">Потенциальной причиной проблем с временем ожидания при использовании команды `hbck` может быть то, что несколько регионов находятся в состоянии "идет переход" в течение долгого времени.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-120">A potential cause for timeout issues when you use the `hbck` command might be that several regions are in the "in transition" state for a long time.</span></span> <span data-ttu-id="0a1d3-121">Эти регионы можно увидеть как отключенные в пользовательском интерфейсе главного узла HBase.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-121">You can see those regions as offline in the HBase Master UI.</span></span> <span data-ttu-id="0a1d3-122">Так как большое количество областей пытается выполнить переход, главный узел HBase может превысить время ожидания и не сможет вернуть регионы обратно в оперативное состояние.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-122">Because a high number of regions are attempting to transition, HBase Master might timeout and be unable to bring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0a1d3-123">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="0a1d3-123">Resolution steps</span></span>

1. <span data-ttu-id="0a1d3-124">Войдите в кластер HDInsight HBase с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-124">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="0a1d3-125">Для подключения к оболочке ZooKeeper выполните команду `hbase zkcli`.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-125">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="0a1d3-126">Выполните команду `rmr /hbase/regions-in-transition` или `rmr /hbase-unsecure/regions-in-transition`.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-126">Run the `rmr /hbase/regions-in-transition` or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="0a1d3-127">Чтобы выйти из оболочки `hbase zkcli`, используйте команду `exit`.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-127">To exit the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="0a1d3-128">Перезапустите службу активного главного узла HBase в пользовательском интерфейсе Ambari.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-128">In the Ambari UI, restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="0a1d3-129">Выполните команду `hbase hbck -fixAssignments` еще раз.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-129">Run the `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="0a1d3-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Как принудительно отключить безопасный режим HDFS в кластере</span><span class="sxs-lookup"><span data-stu-id="0a1d3-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="0a1d3-131">Проблема</span><span class="sxs-lookup"><span data-stu-id="0a1d3-131">Issue</span></span>

<span data-ttu-id="0a1d3-132">Локальная распределенная файловая система Hadoop (HDFS) зависла в безопасном режиме в кластере HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-132">The local Hadoop Distributed File System (HDFS) is stuck in safe mode on the HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="0a1d3-133">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="0a1d3-133">Detailed description</span></span>

<span data-ttu-id="0a1d3-134">Эта ошибка может быть вызвана сбоем при выполнении такой команды HDFS:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-134">This error might be caused by a failure when you run the following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="0a1d3-135">Ошибка, которую вы могли увидеть при попытке запустить команду, выглядит так:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-135">The error you might see when you try to run the command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" to turn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="0a1d3-136">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="0a1d3-136">Probable cause</span></span>

<span data-ttu-id="0a1d3-137">Кластер HDInsight был уменьшен до небольшого числа узлов.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-137">The HDInsight cluster has been scaled down to a very few nodes.</span></span> <span data-ttu-id="0a1d3-138">Число узлов ниже фактора репликации HDFS или близко к нему.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-138">The number of nodes is below or close to the HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0a1d3-139">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="0a1d3-139">Resolution steps</span></span> 

1. <span data-ttu-id="0a1d3-140">Получите состояние HDFS в кластере HDInsight, выполнив следующие команды:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-140">Get the status of the HDFS on the HDInsight cluster by running the following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="0a1d3-141">Также можно проверить целостность HDFS в кластере HDInsight с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-141">You also can check the integrity of the HDFS on the HDInsight cluster by using the following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting to namenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   The filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="0a1d3-142">Если вы определили, что отсутствующих, поврежденных, либо нереплицированных блоков нет или что такие блоки можно игнорировать, выполните следующую команду, чтобы вывести узел имен из безопасного режима:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run the following command to take the name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="0a1d3-143">Как устранить проблемы с подключением JDBC или SQLLine к Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="0a1d3-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0a1d3-144">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="0a1d3-144">Resolution steps</span></span>

<span data-ttu-id="0a1d3-145">Чтобы подключиться к Phoenix, необходимо предоставить IP-адрес активного узла ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-145">To connect with Phoenix, you must provide the IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="0a1d3-146">Убедитесь, что служба Zookeeper, к которой подключается sqlline.py, запущена и работает.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-146">Ensure that the ZooKeeper service to which sqlline.py is trying to connect is up and running.</span></span>
1. <span data-ttu-id="0a1d3-147">Войдите в кластер HDInsight с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-147">Sign in to the HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="0a1d3-148">Введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-148">Enter the following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="0a1d3-149">IP-адрес активного узла ZooKeeper можно получить из пользовательского интерфейса Ambari.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-149">You can get the IP address of the active ZooKeeper node from the Ambari UI.</span></span> <span data-ttu-id="0a1d3-150">Последовательно выберите **HBase** > **Quick Links** (Быстрые ссылки) > **ZK\* (Активно)** > **Zookeeper Info** (Сведения о Zookeeper).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-150">Go to **HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="0a1d3-151">Если sqlline.py подключается к Phoenix и время ожидания не истекает, выполните следующую команду, чтобы проверить доступность и работоспособность Phoenix:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-151">If the sqlline.py connects to Phoenix and does not timeout, run the following command to validate the availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="0a1d3-152">Если эта команда работает, проблемы нет.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-152">If this command works, there is no issue.</span></span> <span data-ttu-id="0a1d3-153">IP-адрес, предоставленный пользователем, может быть неправильным.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-153">The IP address provided by the user might be incorrect.</span></span> <span data-ttu-id="0a1d3-154">Однако если команда приостанавливается на длительное время, а затем отображается следующая ошибка, перейдите к шагу 5.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-154">However, if the command pauses for an extended time and then displays the following error, continue to step 5.</span></span>

   ```apache
           Error while connecting to sqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting to jdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="0a1d3-155">Выполните следующие команды на головном узле (hn0) для диагностики состояния таблицы Phoenix SYSTEM.CATALOG:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-155">Run the following commands from the head node (hn0) to diagnose the condition of the Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="0a1d3-156">Команда должна вернуть следующую ошибку:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-156">The command should return an error similar to the following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="0a1d3-157">В пользовательском интерфейсе Ambari выполните следующие действия, чтобы перезапустить службу HMaster на всех узлах ZooKeeper:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-157">In the Ambari UI, complete the following steps to restart the HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="0a1d3-158">В разделе **Summary** (Сводка) HBase перейдите к **HBase** > **Active HBase Master** (Активный главный узел HBase).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-158">In the **Summary** section of HBase, go to **HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="0a1d3-159">В разделе **Components** (Компоненты) перезапустите службу главного узла HBase.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-159">In the **Components** section, restart the HBase Master service.</span></span>
    3. <span data-ttu-id="0a1d3-160">Повторите описанные выше шаги для остальных служб **главного узла HBase в режиме ожидания**.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="0a1d3-161">Для стабилизации и завершения процесса восстановления службы главного узла HBase может потребоваться до пяти минут.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-161">It can take up to five minutes for the HBase Master service to stabilize and finish the recovery process.</span></span> <span data-ttu-id="0a1d3-162">Через несколько минут повторите команды sqlline.py, чтобы убедиться, что таблица SYSTEM.CATALOG включена и может запрашиваться.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-162">After a few minutes, repeat the sqlline.py commands to confirm that the SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="0a1d3-163">Когда таблица SYSTEM.CATALOG вернется к нормальной работе, проблема подключения к Phoenix должна быть автоматически разрешена.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-163">When the SYSTEM.CATALOG table is back to normal, the connectivity issue to Phoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-to-fail-to-start"></a><span data-ttu-id="0a1d3-164">Что вызывает сбой запуска главного сервера</span><span class="sxs-lookup"><span data-stu-id="0a1d3-164">What causes a master server to fail to start</span></span>

### <a name="error"></a><span data-ttu-id="0a1d3-165">Ошибка</span><span class="sxs-lookup"><span data-stu-id="0a1d3-165">Error</span></span> 

<span data-ttu-id="0a1d3-166">Возникает сбой атомарной операции переименования.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="0a1d3-167">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="0a1d3-167">Detailed description</span></span>

<span data-ttu-id="0a1d3-168">Во время запуска HMaster выполняет многоэтапную инициализацию,</span><span class="sxs-lookup"><span data-stu-id="0a1d3-168">During the startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="0a1d3-169">включая перенос данных из временной папки (.tmp) в папку данных,</span><span class="sxs-lookup"><span data-stu-id="0a1d3-169">These include moving data from the scratch (.tmp) folder to the data folder.</span></span> <span data-ttu-id="0a1d3-170">а также проверяет в папке WAL (упреждающее протоколирование) наличие неработающих региональных серверов и т. д.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-170">HMaster also looks at the write-ahead logs (WALs) folder to see if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="0a1d3-171">Во время запуска HMaster выполняет базовую команду `list` в этих папках.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="0a1d3-172">Каждый раз, когда в любой из этих папок обнаруживается непредвиденный файл, возникает исключение и сервер не будет запущен.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="0a1d3-173">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="0a1d3-173">Probable cause</span></span>

<span data-ttu-id="0a1d3-174">В журналах регионального сервера попытайтесь определить время ожидания создания файла, а затем посмотрите, произошел ли сбой во время создания файла.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-174">In the region server logs, try to identify the timeline of the file creation, and then see if there was a process crash around the time the file was created.</span></span> <span data-ttu-id="0a1d3-175">(Обратитесь в службу поддержки HBase, чтобы она могла помочь вам в этом.) Это поможет нам предоставить более надежные механизмы защиты от таких ошибок и обеспечить надлежащий процесс завершения работы.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-175">(Contact HBase support to assist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="0a1d3-176">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="0a1d3-176">Resolution steps</span></span>

<span data-ttu-id="0a1d3-177">Проверьте стек вызовов и попытайтесь определить папку, которая может быть причиной проблемы (например, это может быть папка WAL или папка .tmp).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-177">Check the call stack and try to determine which folder might be causing the problem (for instance, it might be the WALs folder or the .tmp folder).</span></span> <span data-ttu-id="0a1d3-178">Затем в Cloud Explorer или с помощью команд HDFS попытайтесь найти файл с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-178">Then, in Cloud Explorer or by using HDFS commands, try to locate the problem file.</span></span> <span data-ttu-id="0a1d3-179">Обычно это файл \*-renamePending.json.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="0a1d3-180">(Файл \*-renamePending.json является файлом журнала, который используется для реализации атомарной операции переименования в драйвере WASB.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-180">(The \*-renamePending.json file is a journal file that's used to implement the atomic rename operation in the WASB driver.</span></span> <span data-ttu-id="0a1d3-181">Из-за ошибок в реализации такие файлы могут оставаться в случае сбоя процесса и т. д.) Принудительно удалите этот файл в Cloud Explorer или с помощью команд HDFS.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-181">Due to bugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="0a1d3-182">В этом расположении в некоторых случаях может иметься временный файл с именем наподобие *$$$.$$$*.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="0a1d3-183">Чтобы увидеть этот файл, необходимо использовать команду `ls` HDFS. Этот файл не отображается в Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-183">You have to use HDFS `ls` command to see this file; you cannot see the file in Cloud Explorer.</span></span> <span data-ttu-id="0a1d3-184">Чтобы удалить этот файл, используйте команду HDFS `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-184">To delete this file, use the HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="0a1d3-185">После выполнения этих команд HMaster должен сразу запуститься.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="0a1d3-186">Ошибка</span><span class="sxs-lookup"><span data-stu-id="0a1d3-186">Error</span></span>

<span data-ttu-id="0a1d3-187">Отсутствуют адреса серверов в *метаданных HBase* для региона xxx.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="0a1d3-188">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="0a1d3-188">Detailed description</span></span>

<span data-ttu-id="0a1d3-189">В кластере Linux может появиться сообщение, которое указывает, что таблица *hbase: meta* находится в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-189">You might see a message on your Linux cluster that indicates that the *hbase: meta* table is not online.</span></span> <span data-ttu-id="0a1d3-190">При выполнении `hbck` может появиться сообщение "hbase: meta table replicaId 0 is not found on any region" (Таблица метаданных HBase реплики 0 не найдена ни в одном из регионов).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="0a1d3-191">Проблема может заключаться в том, что серверу HMaster не удалось выполнить инициализацию после перезагрузки HBase.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-191">The problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="0a1d3-192">В журналах HMaster может появиться сообщение: "No server address listed in hbase: meta for region hbase: backup \<region name\>" (Отсутствуют адреса серверов в метаданных hbase для региона hbase: резервное копирование <имя региона>).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-192">In the HMaster logs, you might see the message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="0a1d3-193">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="0a1d3-193">Resolution steps</span></span>

1. <span data-ttu-id="0a1d3-194">В оболочке HBase введите следующие команды (при необходимости измените на фактические значения):</span><span class="sxs-lookup"><span data-stu-id="0a1d3-194">In the HBase shell, enter the following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="0a1d3-195">Удалите запись *пространства имен HBase*.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-195">Delete the *hbase: namespace* entry.</span></span> <span data-ttu-id="0a1d3-196">Эта запись может быть той же ошибкой, о которой сообщалось в отчете при сканировании таблицы *пространства имен HBase*.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-196">This entry might be the same error that's being reported when the *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="0a1d3-197">Чтобы вернуть HBase в состояние выполнения, в пользовательском интерфейсе Ambari перезапустите службу активного главного узла HMaster.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-197">To bring up HBase in a running state, in the Ambari UI, restart the Active HMaster service.</span></span>  

4. <span data-ttu-id="0a1d3-198">В оболочке HBase выполните следующую команду, чтобы подключиться ко всем автономным таблицам:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-198">In the HBase shell, to bring up all offline tables, run the following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="0a1d3-199">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="0a1d3-199">Additional reading</span></span>

<span data-ttu-id="0a1d3-200">[Не удается обработать таблицу HBase](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-200">[Unable to process the HBase table](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)</span></span>


### <a name="error"></a><span data-ttu-id="0a1d3-201">Ошибка</span><span class="sxs-lookup"><span data-stu-id="0a1d3-201">Error</span></span>

<span data-ttu-id="0a1d3-202">Время ожидания HMaster истекает, и возникает неустранимое исключение следующего вида "java.io.IOException: Timedout 300000ms waiting for namespace table to be assigned" (java.io.IOException: истекло время ожидания назначения таблицы пространства имен (300 000 мс)).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-202">HMaster times out with a fatal exception similar to "java.io.IOException: Timedout 300000ms waiting for namespace table to be assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="0a1d3-203">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="0a1d3-203">Detailed description</span></span>

<span data-ttu-id="0a1d3-204">Такая проблема может возникнуть при наличии большого количества таблиц и регионов, которые не были удалены при перезагрузке служб HMaster.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="0a1d3-205">Перезапуск может завершиться ошибкой, и вы увидите сообщение об ошибке, которое указано выше.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-205">Restart might fail, and you'll see the preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="0a1d3-206">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="0a1d3-206">Probable cause</span></span>

<span data-ttu-id="0a1d3-207">Это известная проблема со службой HMaster.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-207">This is a known issue with the HMaster service.</span></span> <span data-ttu-id="0a1d3-208">Общие задачи запуска кластера могут занять много времени.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="0a1d3-209">Служба HMaster завершает работу, так как таблица пространства имен еще не назначена.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-209">HMaster shuts down because the namespace table isn’t yet assigned.</span></span> <span data-ttu-id="0a1d3-210">Это происходит только в том случае, если имеется большой объем неочищенных данных и пять минут ожидания недостаточно.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="0a1d3-211">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="0a1d3-211">Resolution steps</span></span>

1. <span data-ttu-id="0a1d3-212">В пользовательском интерфейсе Ambari перейдите к **HBase** > **Configs** (Конфигурации).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-212">In the Ambari UI, go to **HBase** > **Configs**.</span></span> <span data-ttu-id="0a1d3-213">В пользовательском файле hbase-site.xml file добавьте следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-213">In the custom hbase-site.xml file, add the following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="0a1d3-214">Перезапустите необходимые службы (HMaster или другие службы HBase).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-214">Restart the required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="0a1d3-215">Что вызывает сбой перезапуска на сервере региона</span><span class="sxs-lookup"><span data-stu-id="0a1d3-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="0a1d3-216">Проблема</span><span class="sxs-lookup"><span data-stu-id="0a1d3-216">Issue</span></span>

<span data-ttu-id="0a1d3-217">Сбой перезапуска на региональном сервере можно предотвратить, следуя рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="0a1d3-218">Рекомендуется приостановить действие высокой рабочей нагрузки при планировании перезагрузки региональных серверов HBase.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-218">We recommend that you pause heavy workload activity when you are planning to restart HBase region servers.</span></span> <span data-ttu-id="0a1d3-219">Если приложение продолжит подключаться к региональным серверам во время завершения работы, это замедлит перезапуск регионального сервера на несколько минут.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-219">If an application continues to connect with region servers when shutdown is in progress, the region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="0a1d3-220">Кроме того рекомендуется сначала очистить все таблицы.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-220">Also, it's a good idea to first flush all the tables.</span></span> <span data-ttu-id="0a1d3-221">Подробные сведения об очистке таблиц см. в статье [HDInsight HBase: How to improve the HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/) (HDInsight HBase: как уменьшить время перезапуска кластера HBase с помощью очистки таблиц).</span><span class="sxs-lookup"><span data-stu-id="0a1d3-221">For a reference on how to flush tables, see [HDInsight HBase: How to improve the HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="0a1d3-222">При запуске операции перезапуска на региональных серверах HBase в пользовательском интерфейсе Ambari региональные серверы будут сразу же отключены, но они не будут немедленно перезапущены.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-222">If you initiate the restart operation on HBase region servers from the Ambari UI, you immediately see that the region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="0a1d3-223">Вот, что происходит в этот момент:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-223">Here's what's happening behind the scenes:</span></span> 

1. <span data-ttu-id="0a1d3-224">Агент Ambari отправляет запрос на завершение работы к региональному серверу.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-224">The Ambari agent sends a stop request to the region server.</span></span>
2. <span data-ttu-id="0a1d3-225">Агент Ambari ожидает 30 секунд, пока региональный сервер завершит работу надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-225">The Ambari agent waits for 30 seconds for the region server to shut down gracefully.</span></span> 
3. <span data-ttu-id="0a1d3-226">Если приложение продолжает подключаться к региональному серверу, его работа не будет завершена немедленно.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-226">If your application continues to connect with the region server, the server won't shut down immediately.</span></span> <span data-ttu-id="0a1d3-227">Перед завершением работы должно истечь 30-секундное время ожидания.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-227">The 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="0a1d3-228">Через 30 секунд агент Ambari отправляет команду force-kill (`kill -9`) на региональный сервер.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-228">After 30 seconds, the Ambari agent sends a force-kill (`kill -9`) command to the region server.</span></span> <span data-ttu-id="0a1d3-229">Это можно увидеть в журнале агента Ambari (в каталоге /var/log/ соответствующего рабочего узла):</span><span class="sxs-lookup"><span data-stu-id="0a1d3-229">You can see this in the ambari-agent log (in the /var/log/ directory of the respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="0a1d3-230">Из-за аварийного завершения работы порт, связанный с процессом, может не освободиться несмотря на завершение процесса на региональном сервере.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-230">Because of the abrupt shutdown, the port associated with the process might not be released, even though the region server process is stopped.</span></span> <span data-ttu-id="0a1d3-231">В результате при запуске регионального сервера может возникнуть AddressBindException, как показано в следующих журналах.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-231">This situation can lead to an AddressBindException when the region server is starting, as shown in the following logs.</span></span> <span data-ttu-id="0a1d3-232">Это можно проверить это в файле region-server.log в каталоге /var/log/hbase на рабочих узлах, где региональный сервер не запускается.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-232">You can verify this in the region-server.log in the /var/log/hbase directory on the worker nodes where the region server fails to start.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding to /10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="0a1d3-233">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="0a1d3-233">Resolution steps</span></span>

1. <span data-ttu-id="0a1d3-234">Попробуйте уменьшить нагрузку на региональные серверы HBase перед выполнением перезапуска.</span><span class="sxs-lookup"><span data-stu-id="0a1d3-234">Try to reduce the load on the HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="0a1d3-235">Также можно (если шаг 1не помог) попробовать выполнить перезапуск региональных серверов на рабочих узлах вручную с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="0a1d3-235">Alternatively (if step 1 doesn't help), try to manually restart region servers on the worker nodes by using the following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

