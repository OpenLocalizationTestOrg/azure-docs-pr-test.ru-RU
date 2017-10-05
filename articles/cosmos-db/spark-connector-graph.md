---
title: "Azure Cosmos DB. Аналитика графов с помощью Spark и Apache TinkerPop Gremlin | Документация Майкрософт"
description: "Эта статья содержит инструкции по настройке и выполнению аналитики графов и параллельного вычисления в Azure Cosmos DB с помощью Spark и TinkerPop SparkGraphComputer."
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 27c4d945e418b130c68cfde845571eb93658101e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="f4fed-103">Azure Cosmos DB. Аналитика графов с помощью Spark и Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="f4fed-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="f4fed-104">[Azure Cosmos DB](introduction.md) — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="f4fed-104">[Azure Cosmos DB](introduction.md) is the globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="f4fed-105">Вы можете создавать и запрашивать документы, пары "ключ — значение" и базы данных графов, используя преимущества возможностей глобального распределения и горизонтального масштабирования Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f4fed-105">You can create and query document, key/value, and graph databases, all of which benefit from the global-distribution and horizontal-scale capabilities at the core of Azure Cosmos DB.</span></span> <span data-ttu-id="f4fed-106">Azure Cosmos DB поддерживает рабочие нагрузки графов оперативной обработки транзакций (OLTP), использующие [Gremlin Apache TinkerPop](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f4fed-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="f4fed-107">[Spark](http://spark.apache.org/) — это проект Apache Software Foundation, в котором основное внимание уделяется обработке данных оперативной аналитической обработки (OLAP) общего назначения.</span><span class="sxs-lookup"><span data-stu-id="f4fed-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="f4fed-108">Spark предоставляет гибридную модель распределенных вычислений в памяти и на дисках, аналогичную модели MapReduce в Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f4fed-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar to the Hadoop MapReduce model.</span></span> <span data-ttu-id="f4fed-109">Apache Spark можно развернуть в облаке с помощью [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="f4fed-109">You can deploy Apache Spark in the cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="f4fed-110">Используя одновременно Azure Cosmos DB и Spark, вы можете выполнять рабочие нагрузки OLTP и OLAP с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="f4fed-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="f4fed-111">В этом кратком руководстве показано, как выполнять запросы Gremlin в Azure Cosmos DB в кластере Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="f4fed-111">This quick-start article demonstrates how to run Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4fed-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f4fed-112">Prerequisites</span></span>

<span data-ttu-id="f4fed-113">Для выполнения этого примера вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="f4fed-113">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="f4fed-114">Кластер Azure HDInsight Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="f4fed-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="f4fed-115">Пакет JDK 1.8+ (если у вас нет пакета JDK, выполните `apt-get install default-jdk`).</span><span class="sxs-lookup"><span data-stu-id="f4fed-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="f4fed-116">Maven (если у вас нет Maven, выполните `apt-get install maven`).</span><span class="sxs-lookup"><span data-stu-id="f4fed-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="f4fed-117">Подписка Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]).</span><span class="sxs-lookup"><span data-stu-id="f4fed-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="f4fed-118">Дополнительные сведения о том, как настроить кластер Azure HDInsight Spark, см. в статье [Создание кластеров Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="f4fed-118">For information about how to set up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="f4fed-119">Создание учетной записи базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f4fed-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="f4fed-120">Сначала создайте учетную запись базы данных с помощью API Graph. Для этого сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f4fed-120">First, create a database account with the Graph API by doing the following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="f4fed-121">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="f4fed-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="f4fed-122">Получение Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="f4fed-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="f4fed-123">Получите Apache TinkerPop следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f4fed-123">Get Apache TinkerPop by doing the following:</span></span>

1. <span data-ttu-id="f4fed-124">Выполните удаленное подключение к главному узлу кластера HDInsight `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-124">Remote to the master node of the HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="f4fed-125">Клонируйте исходный код TinkerPop3, создайте его локально и установите в кэш Maven.</span><span class="sxs-lookup"><span data-stu-id="f4fed-125">Clone the TinkerPop3 source code, build it locally, and install it to Maven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="f4fed-126">Установите подключаемый модуль Spark-Gremlin.</span><span class="sxs-lookup"><span data-stu-id="f4fed-126">Install the Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="f4fed-127">а.</span><span class="sxs-lookup"><span data-stu-id="f4fed-127">a.</span></span> <span data-ttu-id="f4fed-128">За установку подключаемого модуля отвечает Grape.</span><span class="sxs-lookup"><span data-stu-id="f4fed-128">The installation of the plug-in is handled by Grape.</span></span> <span data-ttu-id="f4fed-129">Укажите сведения о репозитории для Grape для скачивания подключаемого модуля и его зависимостей.</span><span class="sxs-lookup"><span data-stu-id="f4fed-129">Populate the repositories information for Grape so it can download the plug-in and its dependencies.</span></span> 

      <span data-ttu-id="f4fed-130">Создайте файл конфигурации Grape, если его нет в каталоге `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-130">Create the grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="f4fed-131">Используйте следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="f4fed-131">Use the following settings:</span></span>

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    <span data-ttu-id="f4fed-132">b.</span><span class="sxs-lookup"><span data-stu-id="f4fed-132">b.</span></span> <span data-ttu-id="f4fed-133">Запустите консоль Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="f4fed-134">c.</span><span class="sxs-lookup"><span data-stu-id="f4fed-134">c.</span></span> <span data-ttu-id="f4fed-135">Установите подключаемый модуль Spark-Gremlin версии 3.3.0-SNAPSHOT, созданный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="f4fed-135">Install the Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in the previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart the console to use [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. <span data-ttu-id="f4fed-136">С помощью `:plugin list` активируйте `Hadoop-Gremlin`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-136">Check to see whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="f4fed-137">Отключите этот подключаемый модуль, так как он может мешать выполнению подключаемого модуля Spark-Gremlin `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-137">Disable this plug-in, because it could interfere with the Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="f4fed-138">Подготовка зависимых компонентов TinkerPop3</span><span class="sxs-lookup"><span data-stu-id="f4fed-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="f4fed-139">При создании TinkerPop3 на предыдущем шаге также были извлечены все зависимые компоненты с форматом JAR Spark и Hadoop в целевом каталоге.</span><span class="sxs-lookup"><span data-stu-id="f4fed-139">When you built TinkerPop3 in the previous step, the process also pulled all jar dependencies for Spark and Hadoop in the target directory.</span></span> <span data-ttu-id="f4fed-140">Используйте JAR-файлы, предварительно установленные с помощью HDI, и при необходимости извлеките только дополнительные зависимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="f4fed-140">Use the jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="f4fed-141">Перейдите в целевой каталог консоли Gremlin: `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-141">Go to the Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="f4fed-142">Переместите все JAR-файлы из каталога `ext/` в каталог `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-142">Move all jars under `ext/` to `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="f4fed-143">Удалите все библиотеки формата JAR в `lib/`, которых нет в списке ниже.</span><span class="sxs-lookup"><span data-stu-id="f4fed-143">Remove all jar libraries under `lib/` that are not in the following list:</span></span>

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-the-azure-cosmos-db-spark-connector"></a><span data-ttu-id="f4fed-144">Получение соединителя Spark для Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f4fed-144">Get the Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="f4fed-145">Получите соединитель Spark для Azure Cosmos DB `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` и пакет SDK для Java для Cosmos DB `azure-documentdb-1.10.0.jar` из [соединителя Spark для Azure Cosmos DB в GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="f4fed-145">Get the Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="f4fed-146">Кроме того, вы можете создать его локально.</span><span class="sxs-lookup"><span data-stu-id="f4fed-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="f4fed-147">Так как последняя версия Spark-Gremlin создана с помощью Spark 1.6.1 и не совместима со Spark версии 2.0.2, которая сейчас используется в соединителе Spark для Azure Cosmos DB, вы можете создать новейший код TinkerPop3 и установить JAR-файлы вручную.</span><span class="sxs-lookup"><span data-stu-id="f4fed-147">Because the latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in the Azure Cosmos DB Spark connector, you can build the latest TinkerPop3 code and install the jars manually.</span></span> <span data-ttu-id="f4fed-148">Выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="f4fed-148">Do the following:</span></span>

    <span data-ttu-id="f4fed-149">а.</span><span class="sxs-lookup"><span data-stu-id="f4fed-149">a.</span></span> <span data-ttu-id="f4fed-150">Клонируйте соединитель Spark для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f4fed-150">Clone the Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="f4fed-151">b.</span><span class="sxs-lookup"><span data-stu-id="f4fed-151">b.</span></span> <span data-ttu-id="f4fed-152">Создайте TinkerPop3 (сделано ранее).</span><span class="sxs-lookup"><span data-stu-id="f4fed-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="f4fed-153">Установите все JAR-файлы TinkerPop 3.3.0-SNAPSHOT локально.</span><span class="sxs-lookup"><span data-stu-id="f4fed-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="f4fed-154">c.</span><span class="sxs-lookup"><span data-stu-id="f4fed-154">c.</span></span> <span data-ttu-id="f4fed-155">Обновите `tinkerpop.version` `azure-documentdb-spark/pom.xml` до версии `3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` to `3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="f4fed-156">г)</span><span class="sxs-lookup"><span data-stu-id="f4fed-156">d.</span></span> <span data-ttu-id="f4fed-157">Выполните сборку с помощью Maven.</span><span class="sxs-lookup"><span data-stu-id="f4fed-157">Build with Maven.</span></span> <span data-ttu-id="f4fed-158">Необходимые JAR-файлы помещаются в каталоги `target` и `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-158">The needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="f4fed-159">Скопируйте упомянутые выше JAR-файлы в локальный каталог ~/azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="f4fed-159">Copy the previously mentioned jars to a local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-the-dependencies-to-the-spark-worker-nodes"></a><span data-ttu-id="f4fed-160">Распространение зависимых компонентов по рабочим узлам Spark</span><span class="sxs-lookup"><span data-stu-id="f4fed-160">Distribute the dependencies to the Spark worker nodes</span></span> 

1. <span data-ttu-id="f4fed-161">Так как преобразование данных графа зависит от TinkerPop3, вам необходимо распределить связанные зависимости по всем рабочим узлам Spark.</span><span class="sxs-lookup"><span data-stu-id="f4fed-161">Because the transformation of graph data depends on TinkerPop3, you must distribute the related dependencies to all Spark worker nodes.</span></span>

2. <span data-ttu-id="f4fed-162">Скопируйте зависимости Gremlin, перечисленные выше, JAR-файл соединителя Spark для CosmosDB и пакет SDK для Java для CosmosDB в рабочие узлы следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f4fed-162">Copy the previously mentioned Gremlin dependencies, the CosmosDB Spark connector jar, and CosmosDB Java SDK to the worker nodes by doing the following:</span></span>

    <span data-ttu-id="f4fed-163">а.</span><span class="sxs-lookup"><span data-stu-id="f4fed-163">a.</span></span> <span data-ttu-id="f4fed-164">Скопируйте все JAR-файлы в каталог `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-164">Copy all the jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="f4fed-165">b.</span><span class="sxs-lookup"><span data-stu-id="f4fed-165">b.</span></span> <span data-ttu-id="f4fed-166">Получите список всех рабочих узлов Spark, которые можно найти на панели мониторинга Ambari, в списке `Spark2 Clients` в разделе `Spark2`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-166">Get the list of all Spark worker nodes, which you can find on Ambari Dashboard, in the `Spark2 Clients` list in the `Spark2` section.</span></span>

    <span data-ttu-id="f4fed-167">c.</span><span class="sxs-lookup"><span data-stu-id="f4fed-167">c.</span></span> <span data-ttu-id="f4fed-168">Скопируйте этот каталог для каждого узла.</span><span class="sxs-lookup"><span data-stu-id="f4fed-168">Copy that directory to each of the nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-the-environment-variables"></a><span data-ttu-id="f4fed-169">Настройка переменных среды</span><span class="sxs-lookup"><span data-stu-id="f4fed-169">Set up the environment variables</span></span>

1. <span data-ttu-id="f4fed-170">Найдите версию HDP кластера Spark.</span><span class="sxs-lookup"><span data-stu-id="f4fed-170">Find the HDP version of the Spark cluster.</span></span> <span data-ttu-id="f4fed-171">Это имя каталога в разделе `/usr/hdp/` (например, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="f4fed-171">It is the directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="f4fed-172">Задайте значение hdp.version для всех узлов.</span><span class="sxs-lookup"><span data-stu-id="f4fed-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="f4fed-173">На панели мониторинга Ambari перейдите к **разделу YARN** > **Configs (Конфигурации)** > **Advanced** (Дополнительные), а затем сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f4fed-173">In Ambari Dashboard, go to **YARN section** > **Configs** > **Advanced**, and then do the following:</span></span> 
 
    <span data-ttu-id="f4fed-174">а.</span><span class="sxs-lookup"><span data-stu-id="f4fed-174">a.</span></span> <span data-ttu-id="f4fed-175">В разделе `Custom yarn-site` добавьте новое свойство `hdp.version` со значением версии HDP на главном узле.</span><span class="sxs-lookup"><span data-stu-id="f4fed-175">In `Custom yarn-site`, add a new property `hdp.version` with the value of the HDP version on the master node.</span></span> 
     
    <span data-ttu-id="f4fed-176">b.</span><span class="sxs-lookup"><span data-stu-id="f4fed-176">b.</span></span> <span data-ttu-id="f4fed-177">Сохраните конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f4fed-177">Save the configurations.</span></span> <span data-ttu-id="f4fed-178">Могут появиться предупреждения, которые можно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="f4fed-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="f4fed-179">c.</span><span class="sxs-lookup"><span data-stu-id="f4fed-179">c.</span></span> <span data-ttu-id="f4fed-180">Перезапустите службы YARN и Oozie в соответствии с сообщением в значках с уведомлением.</span><span class="sxs-lookup"><span data-stu-id="f4fed-180">Restart the YARN and Oozie services as the notification icons indicate.</span></span>

3. <span data-ttu-id="f4fed-181">Задайте следующие переменные среды на главном узле (замените значения соответствующим образом):</span><span class="sxs-lookup"><span data-stu-id="f4fed-181">Set the following environment variables on the master node (replace the values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-the-graph-configuration"></a><span data-ttu-id="f4fed-182">Подготовка конфигурации графа</span><span class="sxs-lookup"><span data-stu-id="f4fed-182">Prepare the graph configuration</span></span>

1. <span data-ttu-id="f4fed-183">Создайте файл конфигурации с параметрами подключения Azure Cosmos DB и параметрами Spark и поместите его в каталог `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-183">Create a configuration file with the Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for the driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. <span data-ttu-id="f4fed-184">Обновите значения `spark.driver.extraClassPath` и `spark.executor.extraClassPath`, чтобы включить каталог JAR-файлов, распределенных на предыдущем шаге (в этом случае `/home/sshuser/azure-documentdb-spark/*`).</span><span class="sxs-lookup"><span data-stu-id="f4fed-184">Update the `spark.driver.extraClassPath` and `spark.executor.extraClassPath` to include the directory of the jars that you distributed in the previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="f4fed-185">Укажите следующие сведения для Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="f4fed-185">Provide the following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-the-tinkerpop-graph-and-save-it-to-azure-cosmos-db"></a><span data-ttu-id="f4fed-186">Загрузка графа TinkerPop и его сохранение в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f4fed-186">Load the TinkerPop graph, and save it to Azure Cosmos DB</span></span>
<span data-ttu-id="f4fed-187">Чтобы продемонстрировать, как можно сохранить граф в Azure Cosmos DB, в этом примере используется предопределенный современный граф TinkerPop.</span><span class="sxs-lookup"><span data-stu-id="f4fed-187">To demonstrate how to persist a graph into Azure Cosmos DB, this example uses the TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="f4fed-188">Граф сохранен в формате Kryo и добавлен в репозиторий TinkerPop.</span><span class="sxs-lookup"><span data-stu-id="f4fed-188">The graph is stored in Kryo format, and it's provided in the TinkerPop repository.</span></span>

1. <span data-ttu-id="f4fed-189">Так как вы работаете с Gremlin в режиме YARN, необходимо сделать данные графа доступными в файловой системе Hadoop.</span><span class="sxs-lookup"><span data-stu-id="f4fed-189">Because you are running Gremlin in YARN mode, you must make the graph data available in the Hadoop file system.</span></span> <span data-ttu-id="f4fed-190">Используйте команды ниже, чтобы создать каталог, а затем скопируйте в него локальный файл графа.</span><span class="sxs-lookup"><span data-stu-id="f4fed-190">Use the following commands to make a directory and copy the local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="f4fed-191">Временно обновите файл `gremlin-spark.properties`, чтобы использовать `GryoInputFormat` для считывания графа.</span><span class="sxs-lookup"><span data-stu-id="f4fed-191">Temporarily update the `gremlin-spark.properties` file to use `GryoInputFormat` to read the graph.</span></span> <span data-ttu-id="f4fed-192">Кроме того, укажите `inputLocation` как созданный каталог следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f4fed-192">Also indicate `inputLocation` as the directory you create, as in the following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="f4fed-193">Запустите консоль Gremlin и создайте следующие шаги вычисления, чтобы сохранить данные в настроенную коллекцию Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="f4fed-193">Start Gremlin Console, and then create the following computation steps to persist data to the configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="f4fed-194">а.</span><span class="sxs-lookup"><span data-stu-id="f4fed-194">a.</span></span> <span data-ttu-id="f4fed-195">Создайте граф `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-195">Create the graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="f4fed-196">b.</span><span class="sxs-lookup"><span data-stu-id="f4fed-196">b.</span></span> <span data-ttu-id="f4fed-197">Используйте SparkGraphComputer для записи: `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. <span data-ttu-id="f4fed-198">С помощью обозревателя данных можно проверить, сохранены ли данные в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f4fed-198">From Data Explorer, you can verify that the data has been persisted to Azure Cosmos DB.</span></span>

## <a name="load-the-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="f4fed-199">Загрузка графа из Azure Cosmos DB и выполнение запросов Gremlin</span><span class="sxs-lookup"><span data-stu-id="f4fed-199">Load the graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="f4fed-200">Для загрузки графа измените `gremlin-spark.properties`, чтобы задать параметру `graphReader` значение `DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="f4fed-200">To load the graph, edit `gremlin-spark.properties` to set `graphReader` to `DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="f4fed-201">Загрузите граф, просмотрите данные и выполните запросы Gremlin следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f4fed-201">Load the graph, traverse the data, and run Gremlin queries with it by doing the following:</span></span>

    <span data-ttu-id="f4fed-202">а.</span><span class="sxs-lookup"><span data-stu-id="f4fed-202">a.</span></span> <span data-ttu-id="f4fed-203">Запустите консоль Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-203">Start the Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="f4fed-204">b.</span><span class="sxs-lookup"><span data-stu-id="f4fed-204">b.</span></span> <span data-ttu-id="f4fed-205">Создайте граф с помощью конфигурации `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-205">Create the graph with the configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="f4fed-206">c.</span><span class="sxs-lookup"><span data-stu-id="f4fed-206">c.</span></span> <span data-ttu-id="f4fed-207">Создайте обход графа со SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="f4fed-208">г)</span><span class="sxs-lookup"><span data-stu-id="f4fed-208">d.</span></span> <span data-ttu-id="f4fed-209">Выполните следующие запросы графа Gremlin:</span><span class="sxs-lookup"><span data-stu-id="f4fed-209">Run the following Gremlin graph queries:</span></span>

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> <span data-ttu-id="f4fed-210">Чтобы увидеть более подробные сведения журнала, задайте более подробный уровень ведения журнала в каталоге `conf/log4j-console.properties`.</span><span class="sxs-lookup"><span data-stu-id="f4fed-210">To see more detailed logging, set the log level in `conf/log4j-console.properties` to a more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="f4fed-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4fed-211">Next steps</span></span>

<span data-ttu-id="f4fed-212">Из этого краткого руководства вы узнали, как работать с графами с помощью Azure Cosmos DB и Spark.</span><span class="sxs-lookup"><span data-stu-id="f4fed-212">In this quick-start article, you've learned how to work with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
