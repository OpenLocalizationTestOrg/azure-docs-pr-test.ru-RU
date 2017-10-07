---
title: "aaaTroubleshoot Storm с помощью Azure HDInsight | Документы Microsoft"
description: "Ответы toocommon вопросы об использовании Apache Storm с Azure HDInsight."
keywords: "Azure HDInsight, Storm, вопросы и ответы, руководство по устранению неполадок, часто задаваемые вопросы"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Устранение неполадок в Storm с помощью Azure HDInsight

Дополнительные сведения о hello основные проблемы и способы их устранения для работы с полезными данными Apache Storm Apache Ambari.

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>Как получить доступ к hello Storm пользовательского интерфейса в кластере
Есть два способа для доступа к hello Storm пользовательского интерфейса из браузера:

### <a name="ambari-ui"></a>Пользовательский интерфейс Ambari
1. Откройте панель мониторинга toohello Ambari.
2. Выберите в списке hello служб **Storm**.
3. В hello **быстрые ссылки** последовательно выберите пункты **Storm пользовательского интерфейса**.

### <a name="direct-link"></a>Прямая ссылка
Вы можете использовать hello Storm пользовательского интерфейса на hello URL-адреса:

https://\<DNS-имя кластера\>/stormui

Пример:

 https://stormcluster.azurehdinsight.net/stormui.

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>Способ передачи сведений о контрольных точках spout концентратора событий Storm из одной топологии tooanother

При разработке топологий, которые считываются из концентраторов событий Azure с помощью hello HDInsight Storm события концентратора spout JAR-файлу, необходимо развернуть топологию, которая имеет точно такое же имя в новом кластере hello. Тем не менее необходимо сохранить данные hello контрольных точек, которые были зафиксированы tooApache ZooKeeper hello старом кластере.

### <a name="where-checkpoint-data-is-stored"></a>Где хранятся данные контрольных точек
Хранит данные контрольных точек для смещения spout концентратора событий hello в ZooKeeper в два корневых путей:
- внетранзакционные контрольные точки spout хранятся в /eventhubspout;
- данные транзакционных контрольных точек хранятся в /transactional.

### <a name="how-toorestore"></a>Как toorestore
сценарии tooget hello и библиотеки, используйте tooexport данных из ZooKeeper и затем импортировать задней tooZooKeeper hello данных с новым именем, см. [HDInsight Storm примеры](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

Папка lib Hello содержит .jar файлы, содержащие hello реализации для операции экспорта импорта hello. Папка bash Hello содержит пример сценария, демонстрирующий, как данные tooexport из hello ZooKeeper сервера на старом кластере hello, а затем импортировать его назад toohello ZooKeeper сервера на новый кластер hello.

Запустите hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) сценарий из tooexport узлы ZooKeeper hello, а затем импорт данных. Обновление hello toohello правильный Hortonworks Data Platform (HDP) версия сценария. (Мы работаем над универсальностью этих скриптов в HDInsight. Универсальный сценарии могут выполняться с любого узла в кластере hello без изменения пользователем hello.)

Команда экспорта Hello записывает hello метаданных tooan системы файл распределенных Apache Hadoop (HDFS) путь (в хранилище BLOB-хранилища Azure или хранилища Озера данных Azure) в местоположение, устанавливаемое.

### <a name="examples"></a>Примеры

#### <a name="export-offset-metadata"></a>Экспорт метаданных смещения
1. Использование SSH toogo toohello ZooKeeper кластера на кластере hello с контрольных точек какой hello смещение должно toobe экспортировать.
2. Выполнения hello следующая команда (после обновления hello строку версии HDP) tooexport ZooKeeper смещение данных toohello /stormmetadta/zkdata HDFS путь:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Импорт метаданных смещения
1. Использование SSH toogo toohello ZooKeeper кластера на кластере hello с контрольных точек какой hello смещение должно toobe экспортировать.
2. Выполнения hello следующую команду (после обновления версии строку hello HDP) tooimport ZooKeeper смещение данных hello HDFS путь/stormmetadata/zkdata toohello ZooKeeper сервера на приветствия целевого кластера:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>Удалите смещения метаданных, топологии, могут начинать обработку данных с начала hello, или из отметки времени выбирает этот пользователь hello
1. Использование SSH toogo toohello ZooKeeper кластера на кластере hello с контрольных точек какой hello смещение должно toobe экспортировать.
2. Выполнения hello следующую команду (после обновления версии строку hello HDP) toodelete все ZooKeeper смещение данных в hello текущего кластера:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Как найти двоичные файлы Storm в кластере?
Storm двоичных файлов для текущего стека HDP hello находятся в /usr/hdp/current/storm-client. расположение Hello hello же, как для головного узла, так и для рабочих узлов.
 
Для определенных версий HDP в /usr/hdp (например, /usr/hdp/2.5.0.1233/storm) может существовать несколько двоичных файлов. Папка /usr/hdp/current/storm-client Hello является последней версии toohello symlinked, которая работает на кластере hello.

Дополнительные сведения см. в разделе [кластера HDInsight tooan подключение с помощью SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) и [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>Определение топологии развертывания hello кластер Storm
Сначала определяются все компоненты, установленные с помощью HDInsight Storm. Кластер Storm состоит из четырех категорий узлов:

* Узлы шлюза
* Головные узлы
* Узлы Zookeeper
* Рабочие узлы
 
### <a name="gateway-nodes"></a>Узлы шлюза
Узел шлюз является шлюзом и службу обратного прокси-сервера, которая обеспечивает службы управления active Ambari tooan общего доступа. Он также управляет выбором лидера Ambari.
 
### <a name="head-nodes"></a>Головные узлы
Storm головного узла выполните hello следующие службы:
* Nimbus;
* сервер Ambari;
* сервер метрик Ambari;
* сборщик метрик Ambari.
 
### <a name="zookeeper-nodes"></a>Узлы Zookeeper
HDInsight поставляется с кворумом Zookeeper, включающим три узла. размер кворума Hello фиксируется и не могут быть перенастроены.
 
Службы storm hello кластера, настроенного tooautomatically используйте hello ZooKeeper кворума.
 
### <a name="worker-nodes"></a>Рабочие узлы
Storm рабочих узлов выполните hello следующие службы:
* Supervisor;
* виртуальные машины Java (JVM) рабочей роли для выполнения топологий;
* агент Ambari.
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Как найти двоичные файлы объекта spout концентратора событий Storm для разработки
 
Дополнительные сведения об использовании файлов .jar spout концентратора событий Storm топологии см. следующие ресурсы hello.
 
### <a name="java-based-topology"></a>Топология на основе Java
[Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>Топология на основе C# (Mono в кластерах Linux Storm для HDInsight 3.4+)
[Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Последние двоичные файлы spout концентратора событий Storm для кластеров Linux Storm для HDInsight 3.5+
toolearn toouse hello последнюю Storm события концентратора spout, работающего с HDInsight 3.5 + Linux Storm, кластеров разделе hello mvn-repo [файл readme](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Примеры исходного кода
В разделе [примеры](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) как tooread и записи концентратор событий Azure с помощью Apache Storm топологии (написаны на Java) в кластере Azure HDInsight.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>Как найти файлы конфигурации Storm Log4J в кластерах?
 
файлы конфигурации tooidentify Apache Log4J Storm служб.
 
### <a name="on-head-nodes"></a>На головных узлах
Конфигурация Hello Nimbus Log4J считывается из/usr/hdp/\<HDP версии\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>На рабочих узлах
конфигурации администратора Log4J Hello считывается из/usr/hdp/\<HDP версии\>/storm/log4j2/cluster.xml.
 
файл конфигурации рабочих Log4J Hello считывается из/usr/hdp/\<HDP версии\>/storm/log4j2/worker.xml.
 
Пример: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml.

