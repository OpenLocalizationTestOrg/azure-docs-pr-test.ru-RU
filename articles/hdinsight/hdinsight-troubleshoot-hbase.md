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
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a>Устранение неполадок в HBase с помощью Azure HDInsight

Дополнительные сведения о hello основные проблемы и способы их устранения при работе с полезными данными Apache HBase Apache Ambari.

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a>Как запускать отчеты о командах hbck с несколькими неназначенными регионами

Общие сообщение об ошибке, может видеть при выполнении hello `hbase hbck` команда является «несколько областей назначение которых отменено или уязвимости в цепочке областей hello.»

В hello HBase Master пользовательского интерфейса вы увидите номер hello областей Несбалансированная по всем серверам области. Затем можно выполнить `hbase hbck` команды toosee уязвимости в цепочке области hello.

Уязвимости в системе могут вызываться hello автономного регионов, поэтому назначения hello исправление сначала. 

toobring Здравствуйте неназначенные областей задней tooa нормальное состояние, выполните следующие шаги hello:

1. Войдите в toohello кластеров HDInsight HBase с помощью SSH.
2. tooconnect с оболочкой ZooKeeper hello, запустите hello `hbase zkcli` команды.
3. Запустите hello `rmr /hbase/regions-in-transition` команды или hello `rmr /hbase-unsecure/regions-in-transition` команды.
4. tooexit из hello `hbase zkcli` оболочки, используйте hello `exit` команды.
5. Откройте hello пользовательского интерфейса Ambari Apache и затем перезапустите службу Master HBase активный hello.
6. Запустите hello `hbase hbck` команду еще раз (без параметров). Проверьте выходные данные этой команды tooensure, которому назначаются все области hello.


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a>Как устранить проблемы с временем ожидания при использовании команд hbck для назначения регионов

### <a name="issue"></a>Проблема

Может вызвать проблемы с временем ожидания при использовании hello `hbck` команда может быть несколько областей принадлежат hello «переходными» состоянии в течение долгого времени. Вы увидите этих областей, как вне сети в hello HBase Master пользовательского интерфейса. Так как большое количество областей пытаетесь tootransition, HBase Master может время ожидания и будет невозможно toobring этих областей обратно в оперативный режим.

### <a name="resolution-steps"></a>Способы устранения

1. Войдите в toohello кластеров HDInsight HBase с помощью SSH.
2. tooconnect с оболочкой ZooKeeper hello, запустите hello `hbase zkcli` команды.
3. Запустите hello `rmr /hbase/regions-in-transition` или hello `rmr /hbase-unsecure/regions-in-transition` команды.
4. tooexit hello `hbase zkcli` оболочки, используйте hello `exit` команды.
5. В hello Ambari пользовательского интерфейса перезапустите службу Master HBase активный hello.
6. Запустите hello `hbase hbck -fixAssignments` еще раз.

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a>Как принудительно отключить безопасный режим HDFS в кластере

### <a name="issue"></a>Проблема

Здравствуйте, локальный Hadoop распределенных файл системы (HDFS) застряла в безопасном режиме, в кластере HDInsight hello.

### <a name="detailed-description"></a>Подробное описание

Эта ошибка может быть вызвана сбоя при запустите следующую команду HDFS hello:

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

Ошибка может появиться при попытке команды hello toorun Hello выглядит следующим образом:

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

### <a name="probable-cause"></a>Возможные причины

Hello кластера HDInsight был уменьшен tooa очень небольшое число узлов. Hello количество узлов ниже или закройте коэффициентом репликации toohello HDFS.

### <a name="resolution-steps"></a>Способы устранения 

1. Получите состояние hello hello HDFS на hello HDInsight кластера, запустив hello, следующие команды:

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
2. Также можно проверить целостность hello hello HDFS на hello HDInsight кластера с использованием hello, следующие команды:

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

3. Если вы установили, нет нет отсутствует, поврежден или under-реплицированных блоков, игнорирование этих блоков, выполните hello, следующая команда tootake hello имя узла из безопасного режима:

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a>Как устранить проблемы с подключением JDBC или SQLLine к Apache Phoenix

### <a name="resolution-steps"></a>Способы устранения

tooconnect с Финиксе необходимо указать IP-адрес hello ZooKeeper активного узла. Убедитесь, что hello ZooKeeper sqlline.py toowhich служба пытается tooconnect он работоспособен.
1. Войдите в toohello кластера HDInsight с помощью SSH.
2. Введите следующую команду hello:
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > Можно получить IP-адрес hello hello активного узла ZooKeeper hello Ambari пользовательского интерфейса. Go слишком**HBase** > **быстрые ссылки** > **ZK\* (активный)** > **Zookeeper сведения**. 

3. Если hello sqlline.py подключается tooPhoenix и времени ожидания, выполнения hello следующая команда, toovalidate hello доступность и работоспособность Финиксе:

   ```apache
           !tables
           !quit
   ```      
4. Если эта команда работает, проблемы нет. Hello IP-адрес, предоставленный пользователем hello могут быть неправильными. Однако если команда hello приостанавливается на длительное время, а затем отображает hello следующая ошибка, по-прежнему toostep 5.

   ```apache
           Error while connecting toosqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting toojdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. Выполните следующие команды из головного узла (hn0) hello toodiagnose условие hello hello Финиксе системы hello. Таблица КАТАЛОГА:

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   Команда Hello должен возвращать ошибки аналогичные toohello следующее: 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. В hello Ambari пользовательского интерфейса выполните следующие шаги toorestart hello HMaster службы на всех узлах ZooKeeper hello.

    1. В hello **Сводка** раздел из HBase, перейти слишком**HBase** > **Active HBase Master**. 
    2. В hello **компоненты** статьи, перезапустите службу HBase Master hello.
    3. Повторите описанные выше шаги для остальных служб **главного узла HBase в режиме ожидания**. 

Он может занять несколько минут toofive toostabilize службы HBase образец hello и завершения процесса восстановления hello. Через несколько минут повторите tooconfirm команды sqlline.py hello, hello системы. КАТАЛОГ таблицы работает и что он может запрашиваться. 

Здравствуйте, когда система. КАТАЛОГ таблицы обратной toonormal, tooPhoenix проблема подключения hello должен быть автоматически разрешено.


## <a name="what-causes-a-master-server-toofail-toostart"></a>В каком случае toofail toostart главного сервера

### <a name="error"></a>Ошибка 

Возникает сбой атомарной операции переименования.

### <a name="detailed-description"></a>Подробное описание

Во время выполнения процесса запуска hello HMaster выполняет многие действия для инициализации. К ним относятся перемещение данных с нуля hello (.tmp) папки toohello данных. HMaster также просматривает папки toosee hello упреждающей журналы (WALs) при наличии серверам отвечать на запросы области и т. д. 

Во время запуска HMaster выполняет базовую команду `list` в этих папках. Каждый раз, когда в любой из этих папок обнаруживается непредвиденный файл, возникает исключение и сервер не будет запущен.  

### <a name="probable-cause"></a>Возможные причины

В журналах сервера hello регион попробуйте временная шкала hello tooidentify hello создания файла, а затем посмотреть в случае отсутствия сбоя процесса вокруг файла hello hello времени создания. (Обратитесь в службу поддержки tooassist HBase вы таким образом.) Это поможет нам предоставить более надежные механизмы защиты от таких ошибок и обеспечить надлежащий процесс завершения работы.

### <a name="resolution-steps"></a>Способы устранения

Стек вызовов hello и повторите toodetermine папку, которой может причиной hello (например, бывает hello WAL, журналы или hello .tmp папки). В Cloud Explorer или с помощью команд HDFS, запустите файл с ошибкой toolocate hello. Обычно это файл \*-renamePending.json. (hello \*-renamePending.json файл является файлом журнала, которое использовалось в WASB драйвер hello tooimplement hello atomic переименование. Из-за toobugs в этой реализации можно оставить эти файлы после сбоев process и т. д.) Принудительно удалите этот файл в Cloud Explorer или с помощью команд HDFS. 

В этом расположении в некоторых случаях может иметься временный файл с именем наподобие *$$$.$$$*. У вас есть toouse HDFS `ls` команду toosee этот файл; файлов hello в Cloud Explorer не отображаются. toodelete этот файл, используйте hello HDFS команда `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.  

После выполнения этих команд HMaster должен сразу запуститься. 

### <a name="error"></a>Ошибка

Отсутствуют адреса серверов в *метаданных HBase* для региона xxx.

### <a name="detailed-description"></a>Подробное описание

Сообщение может появиться в кластере Linux, которое указывает, что hello *hbase: meta* таблицы находится в автономном режиме. При выполнении `hbck` может появиться сообщение "hbase: meta table replicaId 0 is not found on any region" (Таблица метаданных HBase реплики 0 не найдена ни в одном из регионов). Hello проблема может быть что HMaster не удалось инициализировать после перезагрузки HBase. В журналах HMaster hello, может появиться сообщение hello: «не адрес сервера, перечисленные в hbase: метаданные для региона hbase: резервного копирования \<название региона\>».  

### <a name="resolution-steps"></a>Способы устранения

1. Введите следующие команды (Изменение фактических значений как применимое) hello в hello оболочки HBase:  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. Удалить hello *hbase: пространство имен* входа. Эта запись может быть hello же ошибка, которая сообщается при hello *hbase: пространство имен* сканирование таблицы.

3. toobring копирование HBase в состоянии выполнения, в hello Ambari пользовательского интерфейса, перезапустите службу Active HMaster hello.  

4. Hello оболочки HBase, toobring всех таблиц вне сети, выполните следующую команду hello:

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a>Дополнительные материалы

[Не удается tooprocess таблице HBase hello](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a>Ошибка

HMaster время ожидания, и аналогичные too"java.io.IOException неустранимое исключение: ожидание toobe таблицы имен назначенный 300000ms Timedout.»

### <a name="detailed-description"></a>Подробное описание

Такая проблема может возникнуть при наличии большого количества таблиц и регионов, которые не были удалены при перезагрузке служб HMaster. Перезапуск может завершиться ошибкой, и вы увидите hello предшествующий сообщение об ошибке.  

### <a name="probable-cause"></a>Возможные причины

Это известная проблема с hello HMaster службы. Общие задачи запуска кластера могут занять много времени. HMaster завершает работу, так как таблица пространства имен hello еще не связана. Это происходит только в том случае, если имеется большой объем неочищенных данных и пять минут ожидания недостаточно.
  
### <a name="resolution-steps"></a>Способы устранения

1. В hello Ambari пользовательского интерфейса, перейдите слишком**HBase** > **Configs**. В файле пользовательских hbase-site.xml hello добавьте hello следующий параметр: 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. Перезапустите службы требуется hello (HMaster и другие службы HBase).  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a>Что вызывает сбой перезапуска на сервере региона

### <a name="issue"></a>Проблема

Сбой перезапуска на региональном сервере можно предотвратить, следуя рекомендациям. Рекомендуется приостановить действие высокой рабочей нагрузки при планировании серверов области toorestart HBase. Если приложение продолжает tooconnect с серверами области во время завершения работы, операция перезапуска сервера hello области будет работать медленнее на несколько минут. Кроме того это toofirst смысл, записи на диск всех hello таблиц. Справочную информацию о том, как таблицы tooflush см. [HDInsight HBase: как кластер HBase tooimprove hello перезапустите времени, Очистка таблиц](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).

Если запустить операцию перезапуска hello серверы области HBase hello Ambari пользовательского интерфейса, сразу же видеть серверы области hello вышел из строя, что не перезапустить прямо сейчас. 

Вот, что происходит в фоновом hello. 

1. Hello Ambari агент отправляет toohello области остановки запроса сервера.
2. Hello Ambari агент ожидает в течение 30 секунд для hello области сервера tooshut работу надлежащим образом. 
3. Если приложение продолжает работать tooconnect с hello области сервера, сервер hello не завершает работу немедленно. время ожидания 30 секунд Hello истекает до завершения работы. 
4. Через 30 секунд hello Ambari агент отправляет force-kill (`kill -9`) команда toohello области сервера. Вы увидите в журнале агента ambari hello (в hello/var/журнала или каталог hello соответствующих рабочий узел):

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
Из-за аварийного завершения работы hello hello порт, связанный с процессом hello не может быть освобождена, несмотря на то, что hello области серверный процесс остановлен. Такая ситуация может привести tooan AddressBindException при запуске сервера hello области, как показано в следующие журналы hello. Это можно проверить в области server.log hello в каталоге /var/log/hbase hello на hello рабочих узлов отказом toostart hello области сервера. 

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

### <a name="resolution-steps"></a>Способы устранения

1. Попробуйте tooreduce hello нагрузку на серверы области HBase hello, прежде чем начать перезагрузку. 
2. Можно также (Если шаг 1 не имеет смысла), попробуйте toomanually перезапуска региона hello серверов на hello рабочих узлов с помощью следующих команд:

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

