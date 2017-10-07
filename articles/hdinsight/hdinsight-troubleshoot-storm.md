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
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="64c56-104">Устранение неполадок в Storm с помощью Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="64c56-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="64c56-105">Дополнительные сведения о hello основные проблемы и способы их устранения для работы с полезными данными Apache Storm Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="64c56-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="64c56-106">Как получить доступ к hello Storm пользовательского интерфейса в кластере</span><span class="sxs-lookup"><span data-stu-id="64c56-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="64c56-107">Есть два способа для доступа к hello Storm пользовательского интерфейса из браузера:</span><span class="sxs-lookup"><span data-stu-id="64c56-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="64c56-108">Пользовательский интерфейс Ambari</span><span class="sxs-lookup"><span data-stu-id="64c56-108">Ambari UI</span></span>
1. <span data-ttu-id="64c56-109">Откройте панель мониторинга toohello Ambari.</span><span class="sxs-lookup"><span data-stu-id="64c56-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="64c56-110">Выберите в списке hello служб **Storm**.</span><span class="sxs-lookup"><span data-stu-id="64c56-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="64c56-111">В hello **быстрые ссылки** последовательно выберите пункты **Storm пользовательского интерфейса**.</span><span class="sxs-lookup"><span data-stu-id="64c56-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="64c56-112">Прямая ссылка</span><span class="sxs-lookup"><span data-stu-id="64c56-112">Direct link</span></span>
<span data-ttu-id="64c56-113">Вы можете использовать hello Storm пользовательского интерфейса на hello URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="64c56-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="64c56-114">https://\<DNS-имя кластера\>/stormui</span><span class="sxs-lookup"><span data-stu-id="64c56-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="64c56-115">Пример:</span><span class="sxs-lookup"><span data-stu-id="64c56-115">Example:</span></span>

 <span data-ttu-id="64c56-116">https://stormcluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="64c56-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="64c56-117">Способ передачи сведений о контрольных точках spout концентратора событий Storm из одной топологии tooanother</span><span class="sxs-lookup"><span data-stu-id="64c56-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="64c56-118">При разработке топологий, которые считываются из концентраторов событий Azure с помощью hello HDInsight Storm события концентратора spout JAR-файлу, необходимо развернуть топологию, которая имеет точно такое же имя в новом кластере hello.</span><span class="sxs-lookup"><span data-stu-id="64c56-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="64c56-119">Тем не менее необходимо сохранить данные hello контрольных точек, которые были зафиксированы tooApache ZooKeeper hello старом кластере.</span><span class="sxs-lookup"><span data-stu-id="64c56-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="64c56-120">Где хранятся данные контрольных точек</span><span class="sxs-lookup"><span data-stu-id="64c56-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="64c56-121">Хранит данные контрольных точек для смещения spout концентратора событий hello в ZooKeeper в два корневых путей:</span><span class="sxs-lookup"><span data-stu-id="64c56-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="64c56-122">внетранзакционные контрольные точки spout хранятся в /eventhubspout;</span><span class="sxs-lookup"><span data-stu-id="64c56-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="64c56-123">данные транзакционных контрольных точек хранятся в /transactional.</span><span class="sxs-lookup"><span data-stu-id="64c56-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="64c56-124">Как toorestore</span><span class="sxs-lookup"><span data-stu-id="64c56-124">How toorestore</span></span>
<span data-ttu-id="64c56-125">сценарии tooget hello и библиотеки, используйте tooexport данных из ZooKeeper и затем импортировать задней tooZooKeeper hello данных с новым именем, см. [HDInsight Storm примеры](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="64c56-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="64c56-126">Папка lib Hello содержит .jar файлы, содержащие hello реализации для операции экспорта импорта hello.</span><span class="sxs-lookup"><span data-stu-id="64c56-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="64c56-127">Папка bash Hello содержит пример сценария, демонстрирующий, как данные tooexport из hello ZooKeeper сервера на старом кластере hello, а затем импортировать его назад toohello ZooKeeper сервера на новый кластер hello.</span><span class="sxs-lookup"><span data-stu-id="64c56-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="64c56-128">Запустите hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) сценарий из tooexport узлы ZooKeeper hello, а затем импорт данных.</span><span class="sxs-lookup"><span data-stu-id="64c56-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="64c56-129">Обновление hello toohello правильный Hortonworks Data Platform (HDP) версия сценария.</span><span class="sxs-lookup"><span data-stu-id="64c56-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="64c56-130">(Мы работаем над универсальностью этих скриптов в HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64c56-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="64c56-131">Универсальный сценарии могут выполняться с любого узла в кластере hello без изменения пользователем hello.)</span><span class="sxs-lookup"><span data-stu-id="64c56-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="64c56-132">Команда экспорта Hello записывает hello метаданных tooan системы файл распределенных Apache Hadoop (HDFS) путь (в хранилище BLOB-хранилища Azure или хранилища Озера данных Azure) в местоположение, устанавливаемое.</span><span class="sxs-lookup"><span data-stu-id="64c56-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="64c56-133">Примеры</span><span class="sxs-lookup"><span data-stu-id="64c56-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="64c56-134">Экспорт метаданных смещения</span><span class="sxs-lookup"><span data-stu-id="64c56-134">Export offset metadata</span></span>
1. <span data-ttu-id="64c56-135">Использование SSH toogo toohello ZooKeeper кластера на кластере hello с контрольных точек какой hello смещение должно toobe экспортировать.</span><span class="sxs-lookup"><span data-stu-id="64c56-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="64c56-136">Выполнения hello следующая команда (после обновления hello строку версии HDP) tooexport ZooKeeper смещение данных toohello /stormmetadta/zkdata HDFS путь:</span><span class="sxs-lookup"><span data-stu-id="64c56-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="64c56-137">Импорт метаданных смещения</span><span class="sxs-lookup"><span data-stu-id="64c56-137">Import offset metadata</span></span>
1. <span data-ttu-id="64c56-138">Использование SSH toogo toohello ZooKeeper кластера на кластере hello с контрольных точек какой hello смещение должно toobe экспортировать.</span><span class="sxs-lookup"><span data-stu-id="64c56-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="64c56-139">Выполнения hello следующую команду (после обновления версии строку hello HDP) tooimport ZooKeeper смещение данных hello HDFS путь/stormmetadata/zkdata toohello ZooKeeper сервера на приветствия целевого кластера:</span><span class="sxs-lookup"><span data-stu-id="64c56-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="64c56-140">Удалите смещения метаданных, топологии, могут начинать обработку данных с начала hello, или из отметки времени выбирает этот пользователь hello</span><span class="sxs-lookup"><span data-stu-id="64c56-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="64c56-141">Использование SSH toogo toohello ZooKeeper кластера на кластере hello с контрольных точек какой hello смещение должно toobe экспортировать.</span><span class="sxs-lookup"><span data-stu-id="64c56-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="64c56-142">Выполнения hello следующую команду (после обновления версии строку hello HDP) toodelete все ZooKeeper смещение данных в hello текущего кластера:</span><span class="sxs-lookup"><span data-stu-id="64c56-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="64c56-143">Как найти двоичные файлы Storm в кластере?</span><span class="sxs-lookup"><span data-stu-id="64c56-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="64c56-144">Storm двоичных файлов для текущего стека HDP hello находятся в /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="64c56-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="64c56-145">расположение Hello hello же, как для головного узла, так и для рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="64c56-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="64c56-146">Для определенных версий HDP в /usr/hdp (например, /usr/hdp/2.5.0.1233/storm) может существовать несколько двоичных файлов.</span><span class="sxs-lookup"><span data-stu-id="64c56-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="64c56-147">Папка /usr/hdp/current/storm-client Hello является последней версии toohello symlinked, которая работает на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="64c56-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="64c56-148">Дополнительные сведения см. в разделе [кластера HDInsight tooan подключение с помощью SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) и [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="64c56-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="64c56-149">Определение топологии развертывания hello кластер Storm</span><span class="sxs-lookup"><span data-stu-id="64c56-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="64c56-150">Сначала определяются все компоненты, установленные с помощью HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="64c56-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="64c56-151">Кластер Storm состоит из четырех категорий узлов:</span><span class="sxs-lookup"><span data-stu-id="64c56-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="64c56-152">Узлы шлюза</span><span class="sxs-lookup"><span data-stu-id="64c56-152">Gateway nodes</span></span>
* <span data-ttu-id="64c56-153">Головные узлы</span><span class="sxs-lookup"><span data-stu-id="64c56-153">Head nodes</span></span>
* <span data-ttu-id="64c56-154">Узлы Zookeeper</span><span class="sxs-lookup"><span data-stu-id="64c56-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="64c56-155">Рабочие узлы</span><span class="sxs-lookup"><span data-stu-id="64c56-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="64c56-156">Узлы шлюза</span><span class="sxs-lookup"><span data-stu-id="64c56-156">Gateway nodes</span></span>
<span data-ttu-id="64c56-157">Узел шлюз является шлюзом и службу обратного прокси-сервера, которая обеспечивает службы управления active Ambari tooan общего доступа.</span><span class="sxs-lookup"><span data-stu-id="64c56-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="64c56-158">Он также управляет выбором лидера Ambari.</span><span class="sxs-lookup"><span data-stu-id="64c56-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="64c56-159">Головные узлы</span><span class="sxs-lookup"><span data-stu-id="64c56-159">Head nodes</span></span>
<span data-ttu-id="64c56-160">Storm головного узла выполните hello следующие службы:</span><span class="sxs-lookup"><span data-stu-id="64c56-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="64c56-161">Nimbus;</span><span class="sxs-lookup"><span data-stu-id="64c56-161">Nimbus</span></span>
* <span data-ttu-id="64c56-162">сервер Ambari;</span><span class="sxs-lookup"><span data-stu-id="64c56-162">Ambari server</span></span>
* <span data-ttu-id="64c56-163">сервер метрик Ambari;</span><span class="sxs-lookup"><span data-stu-id="64c56-163">Ambari Metrics server</span></span>
* <span data-ttu-id="64c56-164">сборщик метрик Ambari.</span><span class="sxs-lookup"><span data-stu-id="64c56-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="64c56-165">Узлы Zookeeper</span><span class="sxs-lookup"><span data-stu-id="64c56-165">ZooKeeper nodes</span></span>
<span data-ttu-id="64c56-166">HDInsight поставляется с кворумом Zookeeper, включающим три узла.</span><span class="sxs-lookup"><span data-stu-id="64c56-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="64c56-167">размер кворума Hello фиксируется и не могут быть перенастроены.</span><span class="sxs-lookup"><span data-stu-id="64c56-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="64c56-168">Службы storm hello кластера, настроенного tooautomatically используйте hello ZooKeeper кворума.</span><span class="sxs-lookup"><span data-stu-id="64c56-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="64c56-169">Рабочие узлы</span><span class="sxs-lookup"><span data-stu-id="64c56-169">Worker nodes</span></span>
<span data-ttu-id="64c56-170">Storm рабочих узлов выполните hello следующие службы:</span><span class="sxs-lookup"><span data-stu-id="64c56-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="64c56-171">Supervisor;</span><span class="sxs-lookup"><span data-stu-id="64c56-171">Supervisor</span></span>
* <span data-ttu-id="64c56-172">виртуальные машины Java (JVM) рабочей роли для выполнения топологий;</span><span class="sxs-lookup"><span data-stu-id="64c56-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="64c56-173">агент Ambari.</span><span class="sxs-lookup"><span data-stu-id="64c56-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="64c56-174">Как найти двоичные файлы объекта spout концентратора событий Storm для разработки</span><span class="sxs-lookup"><span data-stu-id="64c56-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="64c56-175">Дополнительные сведения об использовании файлов .jar spout концентратора событий Storm топологии см. следующие ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="64c56-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="64c56-176">Топология на основе Java</span><span class="sxs-lookup"><span data-stu-id="64c56-176">Java-based topology</span></span>
[<span data-ttu-id="64c56-177">Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="64c56-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="64c56-178">Топология на основе C# (Mono в кластерах Linux Storm для HDInsight 3.4+)</span><span class="sxs-lookup"><span data-stu-id="64c56-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="64c56-179">Обработка событий из службы концентраторов событий Azure с помощью Storm в HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="64c56-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="64c56-180">Последние двоичные файлы spout концентратора событий Storm для кластеров Linux Storm для HDInsight 3.5+</span><span class="sxs-lookup"><span data-stu-id="64c56-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="64c56-181">toolearn toouse hello последнюю Storm события концентратора spout, работающего с HDInsight 3.5 + Linux Storm, кластеров разделе hello mvn-repo [файл readme](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="64c56-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="64c56-182">Примеры исходного кода</span><span class="sxs-lookup"><span data-stu-id="64c56-182">Source code examples</span></span>
<span data-ttu-id="64c56-183">В разделе [примеры](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) как tooread и записи концентратор событий Azure с помощью Apache Storm топологии (написаны на Java) в кластере Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="64c56-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="64c56-184">Как найти файлы конфигурации Storm Log4J в кластерах?</span><span class="sxs-lookup"><span data-stu-id="64c56-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="64c56-185">файлы конфигурации tooidentify Apache Log4J Storm служб.</span><span class="sxs-lookup"><span data-stu-id="64c56-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="64c56-186">На головных узлах</span><span class="sxs-lookup"><span data-stu-id="64c56-186">On head nodes</span></span>
<span data-ttu-id="64c56-187">Конфигурация Hello Nimbus Log4J считывается из/usr/hdp/\<HDP версии\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="64c56-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="64c56-188">На рабочих узлах</span><span class="sxs-lookup"><span data-stu-id="64c56-188">On worker nodes</span></span>
<span data-ttu-id="64c56-189">конфигурации администратора Log4J Hello считывается из/usr/hdp/\<HDP версии\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="64c56-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="64c56-190">файл конфигурации рабочих Log4J Hello считывается из/usr/hdp/\<HDP версии\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="64c56-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="64c56-191">Пример: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="64c56-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

