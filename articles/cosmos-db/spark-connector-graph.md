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
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a>Azure Cosmos DB. Аналитика графов с помощью Spark и Apache TinkerPop Gremlin

[Azure Cosmos DB](introduction.md) является распределенной, моделей базы данных службы от корпорации Майкрософт "hello". Вы можете создать и запрашивать документа, ключ значение и graph баз данных, каждый из которых преимущества возможностей глобального распространения и масштаба по горизонтали hello в основе hello Azure Cosmos БД. Azure Cosmos DB поддерживает рабочие нагрузки графов оперативной обработки транзакций (OLTP), использующие [Gremlin Apache TinkerPop](graph-introduction.md).

[Spark](http://spark.apache.org/) — это проект Apache Software Foundation, в котором основное внимание уделяется обработке данных оперативной аналитической обработки (OLAP) общего назначения. Spark предоставляет гибридную в памяти или на диске распределенной вычислительной модель, аналогичные toohello Hadoop MapReduce модели. Можно развернуть с помощью Apache Spark в облаке hello [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Используя одновременно Azure Cosmos DB и Spark, вы можете выполнять рабочие нагрузки OLTP и OLAP с помощью Gremlin. В этой статье краткого руководства показано, как toorun Gremlin запросов к базе данных Azure Cosmos в кластере Azure HDInsight Spark.

## <a name="prerequisites"></a>Предварительные требования

Перед запуском этого образца необходимо иметь hello следующие предварительные требования:
* Кластер Azure HDInsight Spark 2.0.
* Пакет JDK 1.8+ (если у вас нет пакета JDK, выполните `apt-get install default-jdk`).
* Maven (если у вас нет Maven, выполните `apt-get install maven`).
* Подписка Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]).

Сведения о разделе tooset кластера Azure HDInsight Spark [кластеры HDInsight подготовки](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

## <a name="create-an-azure-cosmos-db-database-account"></a>Создание учетной записи базы данных Azure Cosmos DB

Сначала создайте учетную запись базы данных с hello Graph API, выполнив следующие hello.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Добавление коллекции

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a>Получение Apache TinkerPop

Получите Apache TinkerPop, выполните следующие hello:

1. Главный узел кластера HDInsight hello удаленного toohello `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.

2. Клонирование hello TinkerPop3 исходного кода, выполните его построение локально и установить его tooMaven кэша.

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. Установка hello Spark-Gremlin подключаемого модуля 

    а. Виноград обрабатываются Hello установки hello подключаемого модуля. Заполните сведения о репозитории hello для виноград, чтобы скачать hello подключаемого модуля и его зависимости. 

      Создание файла конфигурации виноград hello, если не присутствует `~/.groovy/grapeConfig.xml`. Используйте hello следующие параметры:

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

    b. Запустите консоль Gremlin `bin/gremlin.sh`.
        
    c. Устанавливать hello Spark-Gremlin подключаемого модуля с версией 3.3.0-SNAPSHOT, который встроен в предыдущих шагах hello:

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

4. Проверьте toosee ли `Hadoop-Gremlin` активируется по `:plugin list`. Отключите этот подключаемый модуль, поскольку она может мешать hello Spark Gremlin подключаемый модуль `:plugin unuse tinkerpop.hadoop`.

## <a name="prepare-tinkerpop3-dependencies"></a>Подготовка зависимых компонентов TinkerPop3

При построении TinkerPop3 в предыдущем шаге hello hello процесс также извлечены все зависимости jar Spark и Hadoop hello целевой каталог. Используйте hello JAR-файлов, предварительно установлены в HDI и получить дополнительные зависимости только при необходимости.

1. Последовательно выберите toohello Gremlin консоли целевой каталог на `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`. 

2. Перемещение всех файлов в списке `ext/` слишком`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.

3. Удалить все jar-библиотеки `lib/` , находятся не в hello после списка:

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a>Получить hello Azure Cosmos DB Spark соединителя

1. Получить соединитель Azure Cosmos DB Spark hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` и пакет SDK для Java DB Cosmos `azure-documentdb-1.10.0.jar` из [соединителя Azure Cosmos DB Spark на GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).

2. Кроме того, вы можете создать его локально. Так как последняя версия Spark Gremlin hello был построен с Spark 1.6.1 и не совместим с Spark 2.0.2, используемый в текущий момент в соединителе Azure Cosmos DB Spark hello, можно создать последнюю TinkerPop3 кода hello и вручную установить hello JAR-файлов. Здравствуйте, следующие:

    а. Клонирование hello Azure Cosmos DB Spark соединителя.

    b. Создайте TinkerPop3 (сделано ранее). Установите все JAR-файлы TinkerPop 3.3.0-SNAPSHOT локально.

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    c. Обновление `tinkerpop.version` `azure-documentdb-spark/pom.xml` слишком`3.3.0-SNAPSHOT`.
    
    d. Выполните сборку с помощью Maven. Hello необходимые JAR-файлов, помещаются в `target` и `target/alternateLocation`.

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. Копировать hello упомянутых выше JAR-файлов tooa локальный каталог на ~ / azure-documentdb-spark:

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a>Распространение hello зависимости toohello Spark рабочих узлов 

1. Поскольку hello преобразования данных диаграммы зависит от TinkerPop3, необходимо распространить hello связанные зависимости tooall Spark рабочих узлов.

2. Копировать hello упомянутых выше Gremlin зависимости, hello jar соединитель CosmosDB Spark и пакет SDK для Java CosmosDB toohello рабочих узлов, выполнив hello ниже:

    а. Копирование всех файлов hello в `~/azure-documentdb-spark`.

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    b. Получить список всех Spark рабочих узлов, которые можно найти на Ambari мониторинга в hello hello `Spark2 Clients` списка в hello `Spark2` раздела.

    c. Скопируйте этот каталог tooeach hello узлов.

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a>Настройка переменных среды hello

1. Найти версию HDP hello кластера Spark hello. Это имя каталога hello в `/usr/hdp/` (например, 2.5.4.2-7).

2. Задайте значение hdp.version для всех узлов. На панели мониторинга Ambari go слишком**раздел YARN** > **конфигураций** > **Дополнительно**и затем hello следующие: 
 
    а. В `Custom yarn-site`, добавить новое свойство `hdp.version` со значением hello hello HDP версии на главном узле hello. 
     
    b. Сохраните настройки hello. Могут появиться предупреждения, которые можно проигнорировать. 
     
    c. Перезапустите службы hello YARN и Oozie, как указывают значка уведомления о hello.

3. Набор hello следующие переменные среды на главном узле hello (замена значений hello соответствующим образом):

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a>Подготовка конфигурации graph hello

1. Создайте файл конфигурации с hello Azure Cosmos DB параметры соединения и Поместите здесь параметры и поместить его в `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.

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

2. Обновление hello `spark.driver.extraClassPath` и `spark.executor.extraClassPath` tooinclude каталог hello hello JAR-файлов, распределенных hello в предыдущем шаге, в этом случае `/home/sshuser/azure-documentdb-spark/*`.

3. Укажите приведенные ниже сведения для Azure Cosmos DB hello:

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a>Загрузка hello TinkerPop graph и сохраните его tooAzure Cosmos DB
toodemonstrate как toopersist graph в Azure DB Cosmos, в этом примере используется hello TinkerPop предопределенные TinkerPop современных графа. График Hello хранятся в формате Kryo и предоставляется в репозитории TinkerPop hello.

1. Так как выполняется в режиме YARN Gremlin hello графические данные необходимо сделать доступным в hello файловой системы Hadoop. Используйте следующие hello команды toomake каталог и копирование hello graph локального файла в него. 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. Временно обновить hello `gremlin-spark.properties` файл toouse `GryoInputFormat` tooread hello графа. Также указывать `inputLocation` как hello каталог создается, как показано ниже hello:

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. Запустите консоль Gremlin, а затем создайте hello после вычисления действия toopersist данных toohello настроен Azure Cosmos DB коллекции:  

    а. Создать граф hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.

    b. Используйте SparkGraphComputer для записи: `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.

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

4. Из обозревателя данных можно убедитесь, что приветствия, данные были сохранены tooAzure Cosmos DB.

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a>Загрузка hello graph из Azure Cosmos DB и выполнять запросы Gremlin

1. График tooload hello, изменить `gremlin-spark.properties` tooset `graphReader` слишком`DocumentDBInputRDD`:

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. График hello нагрузки, перемещаться по данным hello и выполнять запросы Gremlin с ним, выполнив hello ниже:

    а. Запуск консоли Gremlin hello `bin/gremlin.sh`.

    b. Создать граф hello с конфигурацией hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.

    c. Создайте обход графа со SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.

    d. Выполните следующие запросы graph Gremlin hello.

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
> toosee более подробное ведение журнала, задайте уровень журнала hello в `conf/log4j-console.properties` tooa более подробный уровень.
>

## <a name="next-steps"></a>Дальнейшие действия

В этой статье краткого руководства вы узнали, как toowork с диаграммах, объединяя Azure Cosmos DB и Spark.

> [!div class="nextstepaction"]
