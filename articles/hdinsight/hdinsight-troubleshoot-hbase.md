---
title: "aaaTroubleshoot HBase с помощью Azure HDInsight | Документы Microsoft"
description: "Ответы toocommon вопросов о работе с HBase и Azure HDInsight."
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
ms.openlocfilehash: 5210184f8ea95628952a95df8c98f5b98e37c53e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="b6591-103">Устранение неполадок в HBase с помощью Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b6591-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="b6591-104">Дополнительные сведения о hello основные проблемы и способы их устранения при работе с полезными данными Apache HBase Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="b6591-104">Learn about hello top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="b6591-105">Как запускать отчеты о командах hbck с несколькими неназначенными регионами</span><span class="sxs-lookup"><span data-stu-id="b6591-105">How do I run hbck command reports with multiple unassigned regions</span></span>

<span data-ttu-id="b6591-106">Общие сообщение об ошибке, может видеть при выполнении hello `hbase hbck` команда является «несколько областей назначение которых отменено или уязвимости в цепочке областей hello.»</span><span class="sxs-lookup"><span data-stu-id="b6591-106">A common error message that you might see when you run hello `hbase hbck` command is "multiple regions being unassigned or holes in hello chain of regions."</span></span>

<span data-ttu-id="b6591-107">В hello HBase Master пользовательского интерфейса вы увидите номер hello областей Несбалансированная по всем серверам области.</span><span class="sxs-lookup"><span data-stu-id="b6591-107">In hello HBase Master UI, you can see hello number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="b6591-108">Затем можно выполнить `hbase hbck` команды toosee уязвимости в цепочке области hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-108">Then, you can run `hbase hbck` command toosee holes in hello region chain.</span></span>

<span data-ttu-id="b6591-109">Уязвимости в системе могут вызываться hello автономного регионов, поэтому назначения hello исправление сначала.</span><span class="sxs-lookup"><span data-stu-id="b6591-109">Holes might be caused by hello offline regions, so fix hello assignments first.</span></span> 

<span data-ttu-id="b6591-110">toobring Здравствуйте неназначенные областей задней tooa нормальное состояние, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="b6591-110">toobring hello unassigned regions back tooa normal state, complete hello following steps:</span></span>

1. <span data-ttu-id="b6591-111">Войдите в toohello кластеров HDInsight HBase с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="b6591-111">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="b6591-112">tooconnect с оболочкой ZooKeeper hello, запустите hello `hbase zkcli` команды.</span><span class="sxs-lookup"><span data-stu-id="b6591-112">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="b6591-113">Запустите hello `rmr /hbase/regions-in-transition` команды или hello `rmr /hbase-unsecure/regions-in-transition` команды.</span><span class="sxs-lookup"><span data-stu-id="b6591-113">Run hello `rmr /hbase/regions-in-transition` command or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="b6591-114">tooexit из hello `hbase zkcli` оболочки, используйте hello `exit` команды.</span><span class="sxs-lookup"><span data-stu-id="b6591-114">tooexit from hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="b6591-115">Откройте hello пользовательского интерфейса Ambari Apache и затем перезапустите службу Master HBase активный hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-115">Open hello Apache Ambari UI, and then restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="b6591-116">Запустите hello `hbase hbck` команду еще раз (без параметров).</span><span class="sxs-lookup"><span data-stu-id="b6591-116">Run hello `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="b6591-117">Проверьте выходные данные этой команды tooensure, которому назначаются все области hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-117">Check hello output of this command tooensure that all regions are being assigned.</span></span>


## <span data-ttu-id="b6591-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Как устранить проблемы с временем ожидания при использовании команд hbck для назначения регионов</span><span class="sxs-lookup"><span data-stu-id="b6591-118"><a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>How do I fix timeout issues when using hbck commands for region assignments</span></span>

### <a name="issue"></a><span data-ttu-id="b6591-119">Проблема</span><span class="sxs-lookup"><span data-stu-id="b6591-119">Issue</span></span>

<span data-ttu-id="b6591-120">Может вызвать проблемы с временем ожидания при использовании hello `hbck` команда может быть несколько областей принадлежат hello «переходными» состоянии в течение долгого времени.</span><span class="sxs-lookup"><span data-stu-id="b6591-120">A potential cause for timeout issues when you use hello `hbck` command might be that several regions are in hello "in transition" state for a long time.</span></span> <span data-ttu-id="b6591-121">Вы увидите этих областей, как вне сети в hello HBase Master пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b6591-121">You can see those regions as offline in hello HBase Master UI.</span></span> <span data-ttu-id="b6591-122">Так как большое количество областей пытаетесь tootransition, HBase Master может время ожидания и будет невозможно toobring этих областей обратно в оперативный режим.</span><span class="sxs-lookup"><span data-stu-id="b6591-122">Because a high number of regions are attempting tootransition, HBase Master might timeout and be unable toobring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="b6591-123">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="b6591-123">Resolution steps</span></span>

1. <span data-ttu-id="b6591-124">Войдите в toohello кластеров HDInsight HBase с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="b6591-124">Sign in toohello HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="b6591-125">tooconnect с оболочкой ZooKeeper hello, запустите hello `hbase zkcli` команды.</span><span class="sxs-lookup"><span data-stu-id="b6591-125">tooconnect with hello ZooKeeper shell, run hello `hbase zkcli` command.</span></span>
3. <span data-ttu-id="b6591-126">Запустите hello `rmr /hbase/regions-in-transition` или hello `rmr /hbase-unsecure/regions-in-transition` команды.</span><span class="sxs-lookup"><span data-stu-id="b6591-126">Run hello `rmr /hbase/regions-in-transition` or hello `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="b6591-127">tooexit hello `hbase zkcli` оболочки, используйте hello `exit` команды.</span><span class="sxs-lookup"><span data-stu-id="b6591-127">tooexit hello `hbase zkcli` shell, use hello `exit` command.</span></span>
5. <span data-ttu-id="b6591-128">В hello Ambari пользовательского интерфейса перезапустите службу Master HBase активный hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-128">In hello Ambari UI, restart hello Active HBase Master service.</span></span>
6. <span data-ttu-id="b6591-129">Запустите hello `hbase hbck -fixAssignments` еще раз.</span><span class="sxs-lookup"><span data-stu-id="b6591-129">Run hello `hbase hbck -fixAssignments` command again.</span></span>

## <span data-ttu-id="b6591-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Как принудительно отключить безопасный режим HDFS в кластере</span><span class="sxs-lookup"><span data-stu-id="b6591-130"><a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>How do I force-disable HDFS safe mode in a cluster</span></span>

### <a name="issue"></a><span data-ttu-id="b6591-131">Проблема</span><span class="sxs-lookup"><span data-stu-id="b6591-131">Issue</span></span>

<span data-ttu-id="b6591-132">Здравствуйте, локальный Hadoop распределенных файл системы (HDFS) застряла в безопасном режиме, в кластере HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-132">hello local Hadoop Distributed File System (HDFS) is stuck in safe mode on hello HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="b6591-133">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="b6591-133">Detailed description</span></span>

<span data-ttu-id="b6591-134">Эта ошибка может быть вызвана сбоя при запустите следующую команду HDFS hello:</span><span class="sxs-lookup"><span data-stu-id="b6591-134">This error might be caused by a failure when you run hello following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="b6591-135">Ошибка может появиться при попытке команды hello toorun Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b6591-135">hello error you might see when you try toorun hello command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" tooturn safe mode off.
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

### <a name="probable-cause"></a><span data-ttu-id="b6591-136">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="b6591-136">Probable cause</span></span>

<span data-ttu-id="b6591-137">Hello кластера HDInsight был уменьшен tooa очень небольшое число узлов.</span><span class="sxs-lookup"><span data-stu-id="b6591-137">hello HDInsight cluster has been scaled down tooa very few nodes.</span></span> <span data-ttu-id="b6591-138">Hello количество узлов ниже или закройте коэффициентом репликации toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="b6591-138">hello number of nodes is below or close toohello HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="b6591-139">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="b6591-139">Resolution steps</span></span> 

1. <span data-ttu-id="b6591-140">Получите состояние hello hello HDFS на hello HDInsight кластера, запустив hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="b6591-140">Get hello status of hello HDFS on hello HDInsight cluster by running hello following commands:</span></span>

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
2. <span data-ttu-id="b6591-141">Также можно проверить целостность hello hello HDFS на hello HDInsight кластера с использованием hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="b6591-141">You also can check hello integrity of hello HDFS on hello HDInsight cluster by using hello following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting toonamenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
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

   hello filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="b6591-142">Если вы установили, нет нет отсутствует, поврежден или under-реплицированных блоков, игнорирование этих блоков, выполните hello, следующая команда tootake hello имя узла из безопасного режима:</span><span class="sxs-lookup"><span data-stu-id="b6591-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run hello following command tootake hello name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="b6591-143">Как устранить проблемы с подключением JDBC или SQLLine к Apache Phoenix</span><span class="sxs-lookup"><span data-stu-id="b6591-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="b6591-144">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="b6591-144">Resolution steps</span></span>

<span data-ttu-id="b6591-145">tooconnect с Финиксе необходимо указать IP-адрес hello ZooKeeper активного узла.</span><span class="sxs-lookup"><span data-stu-id="b6591-145">tooconnect with Phoenix, you must provide hello IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="b6591-146">Убедитесь, что hello ZooKeeper sqlline.py toowhich служба пытается tooconnect он работоспособен.</span><span class="sxs-lookup"><span data-stu-id="b6591-146">Ensure that hello ZooKeeper service toowhich sqlline.py is trying tooconnect is up and running.</span></span>
1. <span data-ttu-id="b6591-147">Войдите в toohello кластера HDInsight с помощью SSH.</span><span class="sxs-lookup"><span data-stu-id="b6591-147">Sign in toohello HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="b6591-148">Введите следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b6591-148">Enter hello following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="b6591-149">Можно получить IP-адрес hello hello активного узла ZooKeeper hello Ambari пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="b6591-149">You can get hello IP address of hello active ZooKeeper node from hello Ambari UI.</span></span> <span data-ttu-id="b6591-150">Go слишком**HBase** > **быстрые ссылки** > **ZK\* (активный)** > **Zookeeper сведения**.</span><span class="sxs-lookup"><span data-stu-id="b6591-150">Go too**HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="b6591-151">Если hello sqlline.py подключается tooPhoenix и времени ожидания, выполнения hello следующая команда, toovalidate hello доступность и работоспособность Финиксе:</span><span class="sxs-lookup"><span data-stu-id="b6591-151">If hello sqlline.py connects tooPhoenix and does not timeout, run hello following command toovalidate hello availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="b6591-152">Если эта команда работает, проблемы нет.</span><span class="sxs-lookup"><span data-stu-id="b6591-152">If this command works, there is no issue.</span></span> <span data-ttu-id="b6591-153">Hello IP-адрес, предоставленный пользователем hello могут быть неправильными.</span><span class="sxs-lookup"><span data-stu-id="b6591-153">hello IP address provided by hello user might be incorrect.</span></span> <span data-ttu-id="b6591-154">Однако если команда hello приостанавливается на длительное время, а затем отображает hello следующая ошибка, по-прежнему toostep 5.</span><span class="sxs-lookup"><span data-stu-id="b6591-154">However, if hello command pauses for an extended time and then displays hello following error, continue toostep 5.</span></span>

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="b6591-155">Выполните следующие команды из головного узла (hn0) hello toodiagnose условие hello hello Финиксе системы hello. Таблица КАТАЛОГА:</span><span class="sxs-lookup"><span data-stu-id="b6591-155">Run hello following commands from hello head node (hn0) toodiagnose hello condition of hello Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="b6591-156">Команда Hello должен возвращать ошибки аналогичные toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="b6591-156">hello command should return an error similar toohello following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="b6591-157">В hello Ambari пользовательского интерфейса выполните следующие шаги toorestart hello HMaster службы на всех узлах ZooKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-157">In hello Ambari UI, complete hello following steps toorestart hello HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="b6591-158">В hello **Сводка** раздел из HBase, перейти слишком**HBase** > **Active HBase Master**.</span><span class="sxs-lookup"><span data-stu-id="b6591-158">In hello **Summary** section of HBase, go too**HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="b6591-159">В hello **компоненты** статьи, перезапустите службу HBase Master hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-159">In hello **Components** section, restart hello HBase Master service.</span></span>
    3. <span data-ttu-id="b6591-160">Повторите описанные выше шаги для остальных служб **главного узла HBase в режиме ожидания**.</span><span class="sxs-lookup"><span data-stu-id="b6591-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="b6591-161">Он может занять несколько минут toofive toostabilize службы HBase образец hello и завершения процесса восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-161">It can take up toofive minutes for hello HBase Master service toostabilize and finish hello recovery process.</span></span> <span data-ttu-id="b6591-162">Через несколько минут повторите tooconfirm команды sqlline.py hello, hello системы. КАТАЛОГ таблицы работает и что он может запрашиваться.</span><span class="sxs-lookup"><span data-stu-id="b6591-162">After a few minutes, repeat hello sqlline.py commands tooconfirm that hello SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="b6591-163">Здравствуйте, когда система. КАТАЛОГ таблицы обратной toonormal, tooPhoenix проблема подключения hello должен быть автоматически разрешено.</span><span class="sxs-lookup"><span data-stu-id="b6591-163">When hello SYSTEM.CATALOG table is back toonormal, hello connectivity issue tooPhoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-toofail-toostart"></a><span data-ttu-id="b6591-164">В каком случае toofail toostart главного сервера</span><span class="sxs-lookup"><span data-stu-id="b6591-164">What causes a master server toofail toostart</span></span>

### <a name="error"></a><span data-ttu-id="b6591-165">Ошибка</span><span class="sxs-lookup"><span data-stu-id="b6591-165">Error</span></span> 

<span data-ttu-id="b6591-166">Возникает сбой атомарной операции переименования.</span><span class="sxs-lookup"><span data-stu-id="b6591-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="b6591-167">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="b6591-167">Detailed description</span></span>

<span data-ttu-id="b6591-168">Во время выполнения процесса запуска hello HMaster выполняет многие действия для инициализации.</span><span class="sxs-lookup"><span data-stu-id="b6591-168">During hello startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="b6591-169">К ним относятся перемещение данных с нуля hello (.tmp) папки toohello данных.</span><span class="sxs-lookup"><span data-stu-id="b6591-169">These include moving data from hello scratch (.tmp) folder toohello data folder.</span></span> <span data-ttu-id="b6591-170">HMaster также просматривает папки toosee hello упреждающей журналы (WALs) при наличии серверам отвечать на запросы области и т. д.</span><span class="sxs-lookup"><span data-stu-id="b6591-170">HMaster also looks at hello write-ahead logs (WALs) folder toosee if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="b6591-171">Во время запуска HMaster выполняет базовую команду `list` в этих папках.</span><span class="sxs-lookup"><span data-stu-id="b6591-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="b6591-172">Каждый раз, когда в любой из этих папок обнаруживается непредвиденный файл, возникает исключение и сервер не будет запущен.</span><span class="sxs-lookup"><span data-stu-id="b6591-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="b6591-173">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="b6591-173">Probable cause</span></span>

<span data-ttu-id="b6591-174">В журналах сервера hello регион попробуйте временная шкала hello tooidentify hello создания файла, а затем посмотреть в случае отсутствия сбоя процесса вокруг файла hello hello времени создания.</span><span class="sxs-lookup"><span data-stu-id="b6591-174">In hello region server logs, try tooidentify hello timeline of hello file creation, and then see if there was a process crash around hello time hello file was created.</span></span> <span data-ttu-id="b6591-175">(Обратитесь в службу поддержки tooassist HBase вы таким образом.) Это поможет нам предоставить более надежные механизмы защиты от таких ошибок и обеспечить надлежащий процесс завершения работы.</span><span class="sxs-lookup"><span data-stu-id="b6591-175">(Contact HBase support tooassist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="b6591-176">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="b6591-176">Resolution steps</span></span>

<span data-ttu-id="b6591-177">Стек вызовов hello и повторите toodetermine папку, которой может причиной hello (например, бывает hello WAL, журналы или hello .tmp папки).</span><span class="sxs-lookup"><span data-stu-id="b6591-177">Check hello call stack and try toodetermine which folder might be causing hello problem (for instance, it might be hello WALs folder or hello .tmp folder).</span></span> <span data-ttu-id="b6591-178">В Cloud Explorer или с помощью команд HDFS, запустите файл с ошибкой toolocate hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-178">Then, in Cloud Explorer or by using HDFS commands, try toolocate hello problem file.</span></span> <span data-ttu-id="b6591-179">Обычно это файл \*-renamePending.json.</span><span class="sxs-lookup"><span data-stu-id="b6591-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="b6591-180">(hello \*-renamePending.json файл является файлом журнала, которое использовалось в WASB драйвер hello tooimplement hello atomic переименование.</span><span class="sxs-lookup"><span data-stu-id="b6591-180">(hello \*-renamePending.json file is a journal file that's used tooimplement hello atomic rename operation in hello WASB driver.</span></span> <span data-ttu-id="b6591-181">Из-за toobugs в этой реализации можно оставить эти файлы после сбоев process и т. д.) Принудительно удалите этот файл в Cloud Explorer или с помощью команд HDFS.</span><span class="sxs-lookup"><span data-stu-id="b6591-181">Due toobugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="b6591-182">В этом расположении в некоторых случаях может иметься временный файл с именем наподобие *$$$.$$$*.</span><span class="sxs-lookup"><span data-stu-id="b6591-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="b6591-183">У вас есть toouse HDFS `ls` команду toosee этот файл; файлов hello в Cloud Explorer не отображаются.</span><span class="sxs-lookup"><span data-stu-id="b6591-183">You have toouse HDFS `ls` command toosee this file; you cannot see hello file in Cloud Explorer.</span></span> <span data-ttu-id="b6591-184">toodelete этот файл, используйте hello HDFS команда `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="b6591-184">toodelete this file, use hello HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="b6591-185">После выполнения этих команд HMaster должен сразу запуститься.</span><span class="sxs-lookup"><span data-stu-id="b6591-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="b6591-186">Ошибка</span><span class="sxs-lookup"><span data-stu-id="b6591-186">Error</span></span>

<span data-ttu-id="b6591-187">Отсутствуют адреса серверов в *метаданных HBase* для региона xxx.</span><span class="sxs-lookup"><span data-stu-id="b6591-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="b6591-188">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="b6591-188">Detailed description</span></span>

<span data-ttu-id="b6591-189">Сообщение может появиться в кластере Linux, которое указывает, что hello *hbase: meta* таблицы находится в автономном режиме.</span><span class="sxs-lookup"><span data-stu-id="b6591-189">You might see a message on your Linux cluster that indicates that hello *hbase: meta* table is not online.</span></span> <span data-ttu-id="b6591-190">При выполнении `hbck` может появиться сообщение "hbase: meta table replicaId 0 is not found on any region" (Таблица метаданных HBase реплики 0 не найдена ни в одном из регионов).</span><span class="sxs-lookup"><span data-stu-id="b6591-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="b6591-191">Hello проблема может быть что HMaster не удалось инициализировать после перезагрузки HBase.</span><span class="sxs-lookup"><span data-stu-id="b6591-191">hello problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="b6591-192">В журналах HMaster hello, может появиться сообщение hello: «не адрес сервера, перечисленные в hbase: метаданные для региона hbase: резервного копирования \<название региона\>».</span><span class="sxs-lookup"><span data-stu-id="b6591-192">In hello HMaster logs, you might see hello message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="b6591-193">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="b6591-193">Resolution steps</span></span>

1. <span data-ttu-id="b6591-194">Введите следующие команды (Изменение фактических значений как применимое) hello в hello оболочки HBase:</span><span class="sxs-lookup"><span data-stu-id="b6591-194">In hello HBase shell, enter hello following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="b6591-195">Удалить hello *hbase: пространство имен* входа.</span><span class="sxs-lookup"><span data-stu-id="b6591-195">Delete hello *hbase: namespace* entry.</span></span> <span data-ttu-id="b6591-196">Эта запись может быть hello же ошибка, которая сообщается при hello *hbase: пространство имен* сканирование таблицы.</span><span class="sxs-lookup"><span data-stu-id="b6591-196">This entry might be hello same error that's being reported when hello *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="b6591-197">toobring копирование HBase в состоянии выполнения, в hello Ambari пользовательского интерфейса, перезапустите службу Active HMaster hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-197">toobring up HBase in a running state, in hello Ambari UI, restart hello Active HMaster service.</span></span>  

4. <span data-ttu-id="b6591-198">Hello оболочки HBase, toobring всех таблиц вне сети, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b6591-198">In hello HBase shell, toobring up all offline tables, run hello following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="b6591-199">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="b6591-199">Additional reading</span></span>

[<span data-ttu-id="b6591-200">Не удается tooprocess таблице HBase hello</span><span class="sxs-lookup"><span data-stu-id="b6591-200">Unable tooprocess hello HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="b6591-201">Ошибка</span><span class="sxs-lookup"><span data-stu-id="b6591-201">Error</span></span>

<span data-ttu-id="b6591-202">HMaster время ожидания, и аналогичные too"java.io.IOException неустранимое исключение: ожидание toobe таблицы имен назначенный 300000ms Timedout.»</span><span class="sxs-lookup"><span data-stu-id="b6591-202">HMaster times out with a fatal exception similar too"java.io.IOException: Timedout 300000ms waiting for namespace table toobe assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="b6591-203">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="b6591-203">Detailed description</span></span>

<span data-ttu-id="b6591-204">Такая проблема может возникнуть при наличии большого количества таблиц и регионов, которые не были удалены при перезагрузке служб HMaster.</span><span class="sxs-lookup"><span data-stu-id="b6591-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="b6591-205">Перезапуск может завершиться ошибкой, и вы увидите hello предшествующий сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="b6591-205">Restart might fail, and you'll see hello preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="b6591-206">Возможные причины</span><span class="sxs-lookup"><span data-stu-id="b6591-206">Probable cause</span></span>

<span data-ttu-id="b6591-207">Это известная проблема с hello HMaster службы.</span><span class="sxs-lookup"><span data-stu-id="b6591-207">This is a known issue with hello HMaster service.</span></span> <span data-ttu-id="b6591-208">Общие задачи запуска кластера могут занять много времени.</span><span class="sxs-lookup"><span data-stu-id="b6591-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="b6591-209">HMaster завершает работу, так как таблица пространства имен hello еще не связана.</span><span class="sxs-lookup"><span data-stu-id="b6591-209">HMaster shuts down because hello namespace table isn’t yet assigned.</span></span> <span data-ttu-id="b6591-210">Это происходит только в том случае, если имеется большой объем неочищенных данных и пять минут ожидания недостаточно.</span><span class="sxs-lookup"><span data-stu-id="b6591-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="b6591-211">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="b6591-211">Resolution steps</span></span>

1. <span data-ttu-id="b6591-212">В hello Ambari пользовательского интерфейса, перейдите слишком**HBase** > **Configs**.</span><span class="sxs-lookup"><span data-stu-id="b6591-212">In hello Ambari UI, go too**HBase** > **Configs**.</span></span> <span data-ttu-id="b6591-213">В файле пользовательских hbase-site.xml hello добавьте hello следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="b6591-213">In hello custom hbase-site.xml file, add hello following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="b6591-214">Перезапустите службы требуется hello (HMaster и другие службы HBase).</span><span class="sxs-lookup"><span data-stu-id="b6591-214">Restart hello required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="b6591-215">Что вызывает сбой перезапуска на сервере региона</span><span class="sxs-lookup"><span data-stu-id="b6591-215">What causes a restart failure on a region server</span></span>

### <a name="issue"></a><span data-ttu-id="b6591-216">Проблема</span><span class="sxs-lookup"><span data-stu-id="b6591-216">Issue</span></span>

<span data-ttu-id="b6591-217">Сбой перезапуска на региональном сервере можно предотвратить, следуя рекомендациям.</span><span class="sxs-lookup"><span data-stu-id="b6591-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="b6591-218">Рекомендуется приостановить действие высокой рабочей нагрузки при планировании серверов области toorestart HBase.</span><span class="sxs-lookup"><span data-stu-id="b6591-218">We recommend that you pause heavy workload activity when you are planning toorestart HBase region servers.</span></span> <span data-ttu-id="b6591-219">Если приложение продолжает tooconnect с серверами области во время завершения работы, операция перезапуска сервера hello области будет работать медленнее на несколько минут.</span><span class="sxs-lookup"><span data-stu-id="b6591-219">If an application continues tooconnect with region servers when shutdown is in progress, hello region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="b6591-220">Кроме того это toofirst смысл, записи на диск всех hello таблиц.</span><span class="sxs-lookup"><span data-stu-id="b6591-220">Also, it's a good idea toofirst flush all hello tables.</span></span> <span data-ttu-id="b6591-221">Справочную информацию о том, как таблицы tooflush см. [HDInsight HBase: как кластер HBase tooimprove hello перезапустите времени, Очистка таблиц](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="b6591-221">For a reference on how tooflush tables, see [HDInsight HBase: How tooimprove hello HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="b6591-222">Если запустить операцию перезапуска hello серверы области HBase hello Ambari пользовательского интерфейса, сразу же видеть серверы области hello вышел из строя, что не перезапустить прямо сейчас.</span><span class="sxs-lookup"><span data-stu-id="b6591-222">If you initiate hello restart operation on HBase region servers from hello Ambari UI, you immediately see that hello region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="b6591-223">Вот, что происходит в фоновом hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-223">Here's what's happening behind hello scenes:</span></span> 

1. <span data-ttu-id="b6591-224">Hello Ambari агент отправляет toohello области остановки запроса сервера.</span><span class="sxs-lookup"><span data-stu-id="b6591-224">hello Ambari agent sends a stop request toohello region server.</span></span>
2. <span data-ttu-id="b6591-225">Hello Ambari агент ожидает в течение 30 секунд для hello области сервера tooshut работу надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="b6591-225">hello Ambari agent waits for 30 seconds for hello region server tooshut down gracefully.</span></span> 
3. <span data-ttu-id="b6591-226">Если приложение продолжает работать tooconnect с hello области сервера, сервер hello не завершает работу немедленно.</span><span class="sxs-lookup"><span data-stu-id="b6591-226">If your application continues tooconnect with hello region server, hello server won't shut down immediately.</span></span> <span data-ttu-id="b6591-227">время ожидания 30 секунд Hello истекает до завершения работы.</span><span class="sxs-lookup"><span data-stu-id="b6591-227">hello 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="b6591-228">Через 30 секунд hello Ambari агент отправляет force-kill (`kill -9`) команда toohello области сервера.</span><span class="sxs-lookup"><span data-stu-id="b6591-228">After 30 seconds, hello Ambari agent sends a force-kill (`kill -9`) command toohello region server.</span></span> <span data-ttu-id="b6591-229">Вы увидите в журнале агента ambari hello (в hello/var/журнала или каталог hello соответствующих рабочий узел):</span><span class="sxs-lookup"><span data-stu-id="b6591-229">You can see this in hello ambari-agent log (in hello /var/log/ directory of hello respective worker node):</span></span>

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
<span data-ttu-id="b6591-230">Из-за аварийного завершения работы hello hello порт, связанный с процессом hello не может быть освобождена, несмотря на то, что hello области серверный процесс остановлен.</span><span class="sxs-lookup"><span data-stu-id="b6591-230">Because of hello abrupt shutdown, hello port associated with hello process might not be released, even though hello region server process is stopped.</span></span> <span data-ttu-id="b6591-231">Такая ситуация может привести tooan AddressBindException при запуске сервера hello области, как показано в следующие журналы hello.</span><span class="sxs-lookup"><span data-stu-id="b6591-231">This situation can lead tooan AddressBindException when hello region server is starting, as shown in hello following logs.</span></span> <span data-ttu-id="b6591-232">Это можно проверить в области server.log hello в каталоге /var/log/hbase hello на hello рабочих узлов отказом toostart hello области сервера.</span><span class="sxs-lookup"><span data-stu-id="b6591-232">You can verify this in hello region-server.log in hello /var/log/hbase directory on hello worker nodes where hello region server fails toostart.</span></span> 

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
        
   Caused by: java.net.BindException: Problem binding too/10.2.0.4:16020 : Address already in use
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

### <a name="resolution-steps"></a><span data-ttu-id="b6591-233">Способы устранения</span><span class="sxs-lookup"><span data-stu-id="b6591-233">Resolution steps</span></span>

1. <span data-ttu-id="b6591-234">Попробуйте tooreduce hello нагрузку на серверы области HBase hello, прежде чем начать перезагрузку.</span><span class="sxs-lookup"><span data-stu-id="b6591-234">Try tooreduce hello load on hello HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="b6591-235">Можно также (Если шаг 1 не имеет смысла), попробуйте toomanually перезапуска региона hello серверов на hello рабочих узлов с помощью следующих команд:</span><span class="sxs-lookup"><span data-stu-id="b6591-235">Alternatively (if step 1 doesn't help), try toomanually restart region servers on hello worker nodes by using hello following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

