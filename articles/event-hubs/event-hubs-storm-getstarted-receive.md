---
title: "события aaaReceive из концентраторов событий Azure с помощью Apache Storm | Документы Microsoft"
description: "Узнайте основные сведения о получении событий от концентраторов событий с помощью Apache Storm."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a0ab860ee8d504a28aac380c504c928f0d6dbc1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="6988e-103">Получение событий из концентраторов событий с помощью Apache Storm</span><span class="sxs-lookup"><span data-stu-id="6988e-103">Receive events from Event Hubs using Apache Storm</span></span>

<span data-ttu-id="6988e-104">[Apache Storm](https://storm.incubator.apache.org) — это распределенная система вычислений в реальном времени, упрощающая надежную обработку неограниченных потоков данных.</span><span class="sxs-lookup"><span data-stu-id="6988e-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="6988e-105">В этом разделе показано, как toouse потока концентраторов событий Azure spout tooreceive события из концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="6988e-105">This section shows how toouse an Azure Event Hubs Storm spout tooreceive events from Event Hubs.</span></span> <span data-ttu-id="6988e-106">С помощью Apache Storm можно разделить события между несколькими процессами, размещенными в разных узлах.</span><span class="sxs-lookup"><span data-stu-id="6988e-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="6988e-107">Hello интеграции концентраторов событий с Storm упрощает использование событий, прозрачно контрольных ход его выполнения с помощью элемента Storm Zookeeper установки, управления постоянно контрольные точки и одновременно получает от концентраторов событий.</span><span class="sxs-lookup"><span data-stu-id="6988e-107">hello Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="6988e-108">Дополнительные сведения о концентраторах событий получения шаблонов см. в разделе hello [Обзор концентраторов событий][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="6988e-108">For more information about Event Hubs receive patterns, see hello [Event Hubs overview][Event Hubs overview].</span></span>

## <a name="create-project-and-add-code"></a><span data-ttu-id="6988e-109">Создание проекта и добавление кода</span><span class="sxs-lookup"><span data-stu-id="6988e-109">Create project and add code</span></span>

<span data-ttu-id="6988e-110">В этом учебнике используется [HDInsight Storm] [ HDInsight Storm] установки, который поставляется вместе с hello spout концентраторов событий уже доступны.</span><span class="sxs-lookup"><span data-stu-id="6988e-110">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with hello Event Hubs spout already available.</span></span>

1. <span data-ttu-id="6988e-111">Выполните hello [HDInsight Storm - приступить к работе](../hdinsight/hdinsight-storm-overview.md) процедура toocreate новый HDInsight кластера и подключения tooit через удаленный рабочий стол.</span><span class="sxs-lookup"><span data-stu-id="6988e-111">Follow hello [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure toocreate a new HDInsight cluster, and connect tooit via Remote Desktop.</span></span>
2. <span data-ttu-id="6988e-112">Копировать hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` файл tooyour локальной среде разработки.</span><span class="sxs-lookup"><span data-stu-id="6988e-112">Copy hello `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file tooyour local development environment.</span></span> <span data-ttu-id="6988e-113">Этот элемент содержит hello события storm-spout.</span><span class="sxs-lookup"><span data-stu-id="6988e-113">This contains hello events-storm-spout.</span></span>
3. <span data-ttu-id="6988e-114">Используйте следующие команды tooinstall hello пакет в локальном хранилище Maven hello hello.</span><span class="sxs-lookup"><span data-stu-id="6988e-114">Use hello following command tooinstall hello package into hello local Maven store.</span></span> <span data-ttu-id="6988e-115">Это позволит вам tooadd его в hello ураган в качестве ссылки проекта на более позднем этапе.</span><span class="sxs-lookup"><span data-stu-id="6988e-115">This enables you tooadd it as a reference in hello Storm project in a later step.</span></span>

    ```shell
    mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
    ```
4. <span data-ttu-id="6988e-116">В Eclipse создайте проект Maven (щелкните **File** (Файл), **New** (Создать), а затем **Project** (Проект)).</span><span class="sxs-lookup"><span data-stu-id="6988e-116">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="6988e-117">Выберите параметр **Use default Workspace location** (Использовать расположение рабочей области по умолчанию), а затем нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="6988e-117">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="6988e-118">Выберите hello **maven архетипа краткое руководство** архетипа, нажмите кнопку **Далее**</span><span class="sxs-lookup"><span data-stu-id="6988e-118">Select hello **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="6988e-119">Вставьте параметры **GroupId** и **ArtifactId**, а затем нажмите кнопку **Finish** (Готово).</span><span class="sxs-lookup"><span data-stu-id="6988e-119">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="6988e-120">В **pom.xml**, добавить следующие зависимости в hello hello `<dependency>` узла.</span><span class="sxs-lookup"><span data-stu-id="6988e-120">In **pom.xml**, add hello following dependencies in hello `<dependency>` node.</span></span>

    ```xml  
    <dependency>
        <groupId>org.apache.storm</groupId>
        <artifactId>storm-core</artifactId>
        <version>0.9.2-incubating</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.microsoft.eventhubs</groupId>
        <artifactId>eventhubs-storm-spout</artifactId>
        <version>0.9</version>
    </dependency>
    <dependency>
        <groupId>com.netflix.curator</groupId>
        <artifactId>curator-framework</artifactId>
        <version>1.3.3</version>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
            <exclusion>
                <groupId>org.slf4j</groupId>
                <artifactId>slf4j-log4j12</artifactId>
            </exclusion>
        </exclusions>
        <scope>provided</scope>
    </dependency>
    ```

9. <span data-ttu-id="6988e-121">В hello **src** папки, создайте файл с именем **Config.properties** и копирования hello вслед содержимым, заменив hello `receive rule key` и `event hub name` значения:</span><span class="sxs-lookup"><span data-stu-id="6988e-121">In hello **src** folder, create a file called **Config.properties** and copy hello following content, substituting hello `receive rule key` and `event hub name` values:</span></span>

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    <span data-ttu-id="6988e-122">Здравствуйте, значение для **eventhub.receiver.credits** определяет, сколько событий являются пакетными прежде чем освободить их toohello Storm конвейера.</span><span class="sxs-lookup"><span data-stu-id="6988e-122">hello value for **eventhub.receiver.credits** determines how many events are batched before releasing them toohello Storm pipeline.</span></span> <span data-ttu-id="6988e-123">Ради hello простоты в этом примере задается too10 это значение.</span><span class="sxs-lookup"><span data-stu-id="6988e-123">For hello sake of simplicity, this example sets this value too10.</span></span> <span data-ttu-id="6988e-124">В рабочей среде он обычно значение должно быть toohigher значений; Например, 1024.</span><span class="sxs-lookup"><span data-stu-id="6988e-124">In production, it should usually be set toohigher values; for example, 1024.</span></span>
10. <span data-ttu-id="6988e-125">Создайте новый класс с именем **LoggerBolt** с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="6988e-125">Create a new class called **LoggerBolt** with hello following code:</span></span>
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    <span data-ttu-id="6988e-126">Это Storm молнии регистрирует содержимое hello hello полученных событий.</span><span class="sxs-lookup"><span data-stu-id="6988e-126">This Storm bolt logs hello content of hello received events.</span></span> <span data-ttu-id="6988e-127">Это можно легко расширить toostore кортежей в службе хранилища.</span><span class="sxs-lookup"><span data-stu-id="6988e-127">This can easily be extended toostore tuples in a storage service.</span></span> <span data-ttu-id="6988e-128">Hello [учебник по службам analysis датчика HDInsight] использует подход toostore тех же данных в HBase.</span><span class="sxs-lookup"><span data-stu-id="6988e-128">hello [HDInsight sensor analysis tutorial] uses this same approach toostore data into HBase.</span></span>
11. <span data-ttu-id="6988e-129">Создайте класс с именем **LogTopology** с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="6988e-129">Create a class called **LogTopology** with hello following code:</span></span>
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set hello number of workers toobe hello same as partition number.
            // hello idea is toohave a spout and a logger bolt co-exist in one
            // worker tooavoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    <span data-ttu-id="6988e-130">Этот класс создает новый spout концентраторов событий, с помощью свойств hello в tooinstantiate файла конфигурации hello его.</span><span class="sxs-lookup"><span data-stu-id="6988e-130">This class creates a new Event Hubs spout, using hello properties in hello configuration file tooinstantiate it.</span></span> <span data-ttu-id="6988e-131">Очень важно, что toonote, этот пример создает столько spouts задач как hello количество разделов в концентраторе событий hello в порядке toouse hello Максимальная параллелизма запрещаемых этот концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="6988e-131">It is important toonote that this example creates as many spouts tasks as hello number of partitions in hello event hub, in order toouse hello maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6988e-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6988e-132">Next steps</span></span>
<span data-ttu-id="6988e-133">На сайте ссылкам hello, изучите более подробную концентраторов событий:</span><span class="sxs-lookup"><span data-stu-id="6988e-133">You can learn more about Event Hubs by visiting hello following links:</span></span>

* <span data-ttu-id="6988e-134">[Обзор концентраторов событий Azure][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="6988e-134">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="6988e-135">Создание концентратора событий</span><span class="sxs-lookup"><span data-stu-id="6988e-135">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="6988e-136">Часто задаваемые вопросы о концентраторах событий</span><span class="sxs-lookup"><span data-stu-id="6988e-136">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[учебник по службам analysis датчика HDInsight]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: ./media/event-hubs-get-started-receive-storm/create-storm1.png
