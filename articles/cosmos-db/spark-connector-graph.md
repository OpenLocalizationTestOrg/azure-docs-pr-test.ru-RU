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
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="c6e13-103">Azure Cosmos DB. Аналитика графов с помощью Spark и Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="c6e13-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="c6e13-104">[Azure Cosmos DB](introduction.md) является распределенной, моделей базы данных службы от корпорации Майкрософт "hello".</span><span class="sxs-lookup"><span data-stu-id="c6e13-104">[Azure Cosmos DB](introduction.md) is hello globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="c6e13-105">Вы можете создать и запрашивать документа, ключ значение и graph баз данных, каждый из которых преимущества возможностей глобального распространения и масштаба по горизонтали hello в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="c6e13-105">You can create and query document, key/value, and graph databases, all of which benefit from hello global-distribution and horizontal-scale capabilities at hello core of Azure Cosmos DB.</span></span> <span data-ttu-id="c6e13-106">Azure Cosmos DB поддерживает рабочие нагрузки графов оперативной обработки транзакций (OLTP), использующие [Gremlin Apache TinkerPop](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c6e13-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="c6e13-107">[Spark](http://spark.apache.org/) — это проект Apache Software Foundation, в котором основное внимание уделяется обработке данных оперативной аналитической обработки (OLAP) общего назначения.</span><span class="sxs-lookup"><span data-stu-id="c6e13-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="c6e13-108">Spark предоставляет гибридную в памяти или на диске распределенной вычислительной модель, аналогичные toohello Hadoop MapReduce модели.</span><span class="sxs-lookup"><span data-stu-id="c6e13-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar toohello Hadoop MapReduce model.</span></span> <span data-ttu-id="c6e13-109">Можно развернуть с помощью Apache Spark в облаке hello [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="c6e13-109">You can deploy Apache Spark in hello cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="c6e13-110">Используя одновременно Azure Cosmos DB и Spark, вы можете выполнять рабочие нагрузки OLTP и OLAP с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="c6e13-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="c6e13-111">В этой статье краткого руководства показано, как toorun Gremlin запросов к базе данных Azure Cosmos в кластере Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="c6e13-111">This quick-start article demonstrates how toorun Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6e13-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c6e13-112">Prerequisites</span></span>

<span data-ttu-id="c6e13-113">Перед запуском этого образца необходимо иметь hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="c6e13-113">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="c6e13-114">Кластер Azure HDInsight Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="c6e13-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="c6e13-115">Пакет JDK 1.8+ (если у вас нет пакета JDK, выполните `apt-get install default-jdk`).</span><span class="sxs-lookup"><span data-stu-id="c6e13-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="c6e13-116">Maven (если у вас нет Maven, выполните `apt-get install maven`).</span><span class="sxs-lookup"><span data-stu-id="c6e13-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="c6e13-117">Подписка Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]).</span><span class="sxs-lookup"><span data-stu-id="c6e13-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="c6e13-118">Сведения о разделе tooset кластера Azure HDInsight Spark [кластеры HDInsight подготовки](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="c6e13-118">For information about how tooset up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="c6e13-119">Создание учетной записи базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c6e13-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="c6e13-120">Сначала создайте учетную запись базы данных с hello Graph API, выполнив следующие hello.</span><span class="sxs-lookup"><span data-stu-id="c6e13-120">First, create a database account with hello Graph API by doing hello following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="c6e13-121">Добавление коллекции</span><span class="sxs-lookup"><span data-stu-id="c6e13-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="c6e13-122">Получение Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="c6e13-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="c6e13-123">Получите Apache TinkerPop, выполните следующие hello:</span><span class="sxs-lookup"><span data-stu-id="c6e13-123">Get Apache TinkerPop by doing hello following:</span></span>

1. <span data-ttu-id="c6e13-124">Главный узел кластера HDInsight hello удаленного toohello `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-124">Remote toohello master node of hello HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="c6e13-125">Клонирование hello TinkerPop3 исходного кода, выполните его построение локально и установить его tooMaven кэша.</span><span class="sxs-lookup"><span data-stu-id="c6e13-125">Clone hello TinkerPop3 source code, build it locally, and install it tooMaven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="c6e13-126">Установка hello Spark-Gremlin подключаемого модуля</span><span class="sxs-lookup"><span data-stu-id="c6e13-126">Install hello Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="c6e13-127">а.</span><span class="sxs-lookup"><span data-stu-id="c6e13-127">a.</span></span> <span data-ttu-id="c6e13-128">Виноград обрабатываются Hello установки hello подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="c6e13-128">hello installation of hello plug-in is handled by Grape.</span></span> <span data-ttu-id="c6e13-129">Заполните сведения о репозитории hello для виноград, чтобы скачать hello подключаемого модуля и его зависимости.</span><span class="sxs-lookup"><span data-stu-id="c6e13-129">Populate hello repositories information for Grape so it can download hello plug-in and its dependencies.</span></span> 

      <span data-ttu-id="c6e13-130">Создание файла конфигурации виноград hello, если не присутствует `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-130">Create hello grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="c6e13-131">Используйте hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="c6e13-131">Use hello following settings:</span></span>

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

    <span data-ttu-id="c6e13-132">b.</span><span class="sxs-lookup"><span data-stu-id="c6e13-132">b.</span></span> <span data-ttu-id="c6e13-133">Запустите консоль Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="c6e13-134">c.</span><span class="sxs-lookup"><span data-stu-id="c6e13-134">c.</span></span> <span data-ttu-id="c6e13-135">Устанавливать hello Spark-Gremlin подключаемого модуля с версией 3.3.0-SNAPSHOT, который встроен в предыдущих шагах hello:</span><span class="sxs-lookup"><span data-stu-id="c6e13-135">Install hello Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in hello previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
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

4. <span data-ttu-id="c6e13-136">Проверьте toosee ли `Hadoop-Gremlin` активируется по `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-136">Check toosee whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="c6e13-137">Отключите этот подключаемый модуль, поскольку она может мешать hello Spark Gremlin подключаемый модуль `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-137">Disable this plug-in, because it could interfere with hello Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="c6e13-138">Подготовка зависимых компонентов TinkerPop3</span><span class="sxs-lookup"><span data-stu-id="c6e13-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="c6e13-139">При построении TinkerPop3 в предыдущем шаге hello hello процесс также извлечены все зависимости jar Spark и Hadoop hello целевой каталог.</span><span class="sxs-lookup"><span data-stu-id="c6e13-139">When you built TinkerPop3 in hello previous step, hello process also pulled all jar dependencies for Spark and Hadoop in hello target directory.</span></span> <span data-ttu-id="c6e13-140">Используйте hello JAR-файлов, предварительно установлены в HDI и получить дополнительные зависимости только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="c6e13-140">Use hello jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="c6e13-141">Последовательно выберите toohello Gremlin консоли целевой каталог на `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-141">Go toohello Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="c6e13-142">Перемещение всех файлов в списке `ext/` слишком`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-142">Move all jars under `ext/` too`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="c6e13-143">Удалить все jar-библиотеки `lib/` , находятся не в hello после списка:</span><span class="sxs-lookup"><span data-stu-id="c6e13-143">Remove all jar libraries under `lib/` that are not in hello following list:</span></span>

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a><span data-ttu-id="c6e13-144">Получить hello Azure Cosmos DB Spark соединителя</span><span class="sxs-lookup"><span data-stu-id="c6e13-144">Get hello Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="c6e13-145">Получить соединитель Azure Cosmos DB Spark hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` и пакет SDK для Java DB Cosmos `azure-documentdb-1.10.0.jar` из [соединителя Azure Cosmos DB Spark на GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="c6e13-145">Get hello Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="c6e13-146">Кроме того, вы можете создать его локально.</span><span class="sxs-lookup"><span data-stu-id="c6e13-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="c6e13-147">Так как последняя версия Spark Gremlin hello был построен с Spark 1.6.1 и не совместим с Spark 2.0.2, используемый в текущий момент в соединителе Azure Cosmos DB Spark hello, можно создать последнюю TinkerPop3 кода hello и вручную установить hello JAR-файлов.</span><span class="sxs-lookup"><span data-stu-id="c6e13-147">Because hello latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in hello Azure Cosmos DB Spark connector, you can build hello latest TinkerPop3 code and install hello jars manually.</span></span> <span data-ttu-id="c6e13-148">Здравствуйте, следующие:</span><span class="sxs-lookup"><span data-stu-id="c6e13-148">Do hello following:</span></span>

    <span data-ttu-id="c6e13-149">а.</span><span class="sxs-lookup"><span data-stu-id="c6e13-149">a.</span></span> <span data-ttu-id="c6e13-150">Клонирование hello Azure Cosmos DB Spark соединителя.</span><span class="sxs-lookup"><span data-stu-id="c6e13-150">Clone hello Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="c6e13-151">b.</span><span class="sxs-lookup"><span data-stu-id="c6e13-151">b.</span></span> <span data-ttu-id="c6e13-152">Создайте TinkerPop3 (сделано ранее).</span><span class="sxs-lookup"><span data-stu-id="c6e13-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="c6e13-153">Установите все JAR-файлы TinkerPop 3.3.0-SNAPSHOT локально.</span><span class="sxs-lookup"><span data-stu-id="c6e13-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="c6e13-154">c.</span><span class="sxs-lookup"><span data-stu-id="c6e13-154">c.</span></span> <span data-ttu-id="c6e13-155">Обновление `tinkerpop.version` `azure-documentdb-spark/pom.xml` слишком`3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` too`3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="c6e13-156">d.</span><span class="sxs-lookup"><span data-stu-id="c6e13-156">d.</span></span> <span data-ttu-id="c6e13-157">Выполните сборку с помощью Maven.</span><span class="sxs-lookup"><span data-stu-id="c6e13-157">Build with Maven.</span></span> <span data-ttu-id="c6e13-158">Hello необходимые JAR-файлов, помещаются в `target` и `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-158">hello needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="c6e13-159">Копировать hello упомянутых выше JAR-файлов tooa локальный каталог на ~ / azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="c6e13-159">Copy hello previously mentioned jars tooa local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a><span data-ttu-id="c6e13-160">Распространение hello зависимости toohello Spark рабочих узлов</span><span class="sxs-lookup"><span data-stu-id="c6e13-160">Distribute hello dependencies toohello Spark worker nodes</span></span> 

1. <span data-ttu-id="c6e13-161">Поскольку hello преобразования данных диаграммы зависит от TinkerPop3, необходимо распространить hello связанные зависимости tooall Spark рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="c6e13-161">Because hello transformation of graph data depends on TinkerPop3, you must distribute hello related dependencies tooall Spark worker nodes.</span></span>

2. <span data-ttu-id="c6e13-162">Копировать hello упомянутых выше Gremlin зависимости, hello jar соединитель CosmosDB Spark и пакет SDK для Java CosmosDB toohello рабочих узлов, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="c6e13-162">Copy hello previously mentioned Gremlin dependencies, hello CosmosDB Spark connector jar, and CosmosDB Java SDK toohello worker nodes by doing hello following:</span></span>

    <span data-ttu-id="c6e13-163">а.</span><span class="sxs-lookup"><span data-stu-id="c6e13-163">a.</span></span> <span data-ttu-id="c6e13-164">Копирование всех файлов hello в `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-164">Copy all hello jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="c6e13-165">b.</span><span class="sxs-lookup"><span data-stu-id="c6e13-165">b.</span></span> <span data-ttu-id="c6e13-166">Получить список всех Spark рабочих узлов, которые можно найти на Ambari мониторинга в hello hello `Spark2 Clients` списка в hello `Spark2` раздела.</span><span class="sxs-lookup"><span data-stu-id="c6e13-166">Get hello list of all Spark worker nodes, which you can find on Ambari Dashboard, in hello `Spark2 Clients` list in hello `Spark2` section.</span></span>

    <span data-ttu-id="c6e13-167">c.</span><span class="sxs-lookup"><span data-stu-id="c6e13-167">c.</span></span> <span data-ttu-id="c6e13-168">Скопируйте этот каталог tooeach hello узлов.</span><span class="sxs-lookup"><span data-stu-id="c6e13-168">Copy that directory tooeach of hello nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a><span data-ttu-id="c6e13-169">Настройка переменных среды hello</span><span class="sxs-lookup"><span data-stu-id="c6e13-169">Set up hello environment variables</span></span>

1. <span data-ttu-id="c6e13-170">Найти версию HDP hello кластера Spark hello.</span><span class="sxs-lookup"><span data-stu-id="c6e13-170">Find hello HDP version of hello Spark cluster.</span></span> <span data-ttu-id="c6e13-171">Это имя каталога hello в `/usr/hdp/` (например, 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="c6e13-171">It is hello directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="c6e13-172">Задайте значение hdp.version для всех узлов.</span><span class="sxs-lookup"><span data-stu-id="c6e13-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="c6e13-173">На панели мониторинга Ambari go слишком**раздел YARN** > **конфигураций** > **Дополнительно**и затем hello следующие:</span><span class="sxs-lookup"><span data-stu-id="c6e13-173">In Ambari Dashboard, go too**YARN section** > **Configs** > **Advanced**, and then do hello following:</span></span> 
 
    <span data-ttu-id="c6e13-174">а.</span><span class="sxs-lookup"><span data-stu-id="c6e13-174">a.</span></span> <span data-ttu-id="c6e13-175">В `Custom yarn-site`, добавить новое свойство `hdp.version` со значением hello hello HDP версии на главном узле hello.</span><span class="sxs-lookup"><span data-stu-id="c6e13-175">In `Custom yarn-site`, add a new property `hdp.version` with hello value of hello HDP version on hello master node.</span></span> 
     
    <span data-ttu-id="c6e13-176">b.</span><span class="sxs-lookup"><span data-stu-id="c6e13-176">b.</span></span> <span data-ttu-id="c6e13-177">Сохраните настройки hello.</span><span class="sxs-lookup"><span data-stu-id="c6e13-177">Save hello configurations.</span></span> <span data-ttu-id="c6e13-178">Могут появиться предупреждения, которые можно проигнорировать.</span><span class="sxs-lookup"><span data-stu-id="c6e13-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="c6e13-179">c.</span><span class="sxs-lookup"><span data-stu-id="c6e13-179">c.</span></span> <span data-ttu-id="c6e13-180">Перезапустите службы hello YARN и Oozie, как указывают значка уведомления о hello.</span><span class="sxs-lookup"><span data-stu-id="c6e13-180">Restart hello YARN and Oozie services as hello notification icons indicate.</span></span>

3. <span data-ttu-id="c6e13-181">Набор hello следующие переменные среды на главном узле hello (замена значений hello соответствующим образом):</span><span class="sxs-lookup"><span data-stu-id="c6e13-181">Set hello following environment variables on hello master node (replace hello values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a><span data-ttu-id="c6e13-182">Подготовка конфигурации graph hello</span><span class="sxs-lookup"><span data-stu-id="c6e13-182">Prepare hello graph configuration</span></span>

1. <span data-ttu-id="c6e13-183">Создайте файл конфигурации с hello Azure Cosmos DB параметры соединения и Поместите здесь параметры и поместить его в `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-183">Create a configuration file with hello Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

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

    # Classpath for hello driver and executors
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

2. <span data-ttu-id="c6e13-184">Обновление hello `spark.driver.extraClassPath` и `spark.executor.extraClassPath` tooinclude каталог hello hello JAR-файлов, распределенных hello в предыдущем шаге, в этом случае `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-184">Update hello `spark.driver.extraClassPath` and `spark.executor.extraClassPath` tooinclude hello directory of hello jars that you distributed in hello previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="c6e13-185">Укажите приведенные ниже сведения для Azure Cosmos DB hello:</span><span class="sxs-lookup"><span data-stu-id="c6e13-185">Provide hello following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a><span data-ttu-id="c6e13-186">Загрузка hello TinkerPop graph и сохраните его tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c6e13-186">Load hello TinkerPop graph, and save it tooAzure Cosmos DB</span></span>
<span data-ttu-id="c6e13-187">toodemonstrate как toopersist graph в Azure DB Cosmos, в этом примере используется hello TinkerPop предопределенные TinkerPop современных графа.</span><span class="sxs-lookup"><span data-stu-id="c6e13-187">toodemonstrate how toopersist a graph into Azure Cosmos DB, this example uses hello TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="c6e13-188">График Hello хранятся в формате Kryo и предоставляется в репозитории TinkerPop hello.</span><span class="sxs-lookup"><span data-stu-id="c6e13-188">hello graph is stored in Kryo format, and it's provided in hello TinkerPop repository.</span></span>

1. <span data-ttu-id="c6e13-189">Так как выполняется в режиме YARN Gremlin hello графические данные необходимо сделать доступным в hello файловой системы Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c6e13-189">Because you are running Gremlin in YARN mode, you must make hello graph data available in hello Hadoop file system.</span></span> <span data-ttu-id="c6e13-190">Используйте следующие hello команды toomake каталог и копирование hello graph локального файла в него.</span><span class="sxs-lookup"><span data-stu-id="c6e13-190">Use hello following commands toomake a directory and copy hello local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="c6e13-191">Временно обновить hello `gremlin-spark.properties` файл toouse `GryoInputFormat` tooread hello графа.</span><span class="sxs-lookup"><span data-stu-id="c6e13-191">Temporarily update hello `gremlin-spark.properties` file toouse `GryoInputFormat` tooread hello graph.</span></span> <span data-ttu-id="c6e13-192">Также указывать `inputLocation` как hello каталог создается, как показано ниже hello:</span><span class="sxs-lookup"><span data-stu-id="c6e13-192">Also indicate `inputLocation` as hello directory you create, as in hello following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="c6e13-193">Запустите консоль Gremlin, а затем создайте hello после вычисления действия toopersist данных toohello настроен Azure Cosmos DB коллекции:</span><span class="sxs-lookup"><span data-stu-id="c6e13-193">Start Gremlin Console, and then create hello following computation steps toopersist data toohello configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="c6e13-194">а.</span><span class="sxs-lookup"><span data-stu-id="c6e13-194">a.</span></span> <span data-ttu-id="c6e13-195">Создать граф hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-195">Create hello graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="c6e13-196">b.</span><span class="sxs-lookup"><span data-stu-id="c6e13-196">b.</span></span> <span data-ttu-id="c6e13-197">Используйте SparkGraphComputer для записи: `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

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

4. <span data-ttu-id="c6e13-198">Из обозревателя данных можно убедитесь, что приветствия, данные были сохранены tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6e13-198">From Data Explorer, you can verify that hello data has been persisted tooAzure Cosmos DB.</span></span>

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="c6e13-199">Загрузка hello graph из Azure Cosmos DB и выполнять запросы Gremlin</span><span class="sxs-lookup"><span data-stu-id="c6e13-199">Load hello graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="c6e13-200">График tooload hello, изменить `gremlin-spark.properties` tooset `graphReader` слишком`DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="c6e13-200">tooload hello graph, edit `gremlin-spark.properties` tooset `graphReader` too`DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="c6e13-201">График hello нагрузки, перемещаться по данным hello и выполнять запросы Gremlin с ним, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="c6e13-201">Load hello graph, traverse hello data, and run Gremlin queries with it by doing hello following:</span></span>

    <span data-ttu-id="c6e13-202">а.</span><span class="sxs-lookup"><span data-stu-id="c6e13-202">a.</span></span> <span data-ttu-id="c6e13-203">Запуск консоли Gremlin hello `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-203">Start hello Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="c6e13-204">b.</span><span class="sxs-lookup"><span data-stu-id="c6e13-204">b.</span></span> <span data-ttu-id="c6e13-205">Создать граф hello с конфигурацией hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-205">Create hello graph with hello configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="c6e13-206">c.</span><span class="sxs-lookup"><span data-stu-id="c6e13-206">c.</span></span> <span data-ttu-id="c6e13-207">Создайте обход графа со SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="c6e13-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="c6e13-208">d.</span><span class="sxs-lookup"><span data-stu-id="c6e13-208">d.</span></span> <span data-ttu-id="c6e13-209">Выполните следующие запросы graph Gremlin hello.</span><span class="sxs-lookup"><span data-stu-id="c6e13-209">Run hello following Gremlin graph queries:</span></span>

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
> <span data-ttu-id="c6e13-210">toosee более подробное ведение журнала, задайте уровень журнала hello в `conf/log4j-console.properties` tooa более подробный уровень.</span><span class="sxs-lookup"><span data-stu-id="c6e13-210">toosee more detailed logging, set hello log level in `conf/log4j-console.properties` tooa more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="c6e13-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c6e13-211">Next steps</span></span>

<span data-ttu-id="c6e13-212">В этой статье краткого руководства вы узнали, как toowork с диаграммах, объединяя Azure Cosmos DB и Spark.</span><span class="sxs-lookup"><span data-stu-id="c6e13-212">In this quick-start article, you've learned how toowork with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
