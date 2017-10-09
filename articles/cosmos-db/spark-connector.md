---
title: "Apache Spark aaaConnecting tooAzure Cosmos DB | Документы Microsoft"
description: "Использовать этот учебник toolearn о соединителе Azure Cosmos DB Spark hello, позволяющая tooconnect Apache Spark tooAzure Cosmos DB tooperform распределенных статистические схемы и данных наук на hello несколькими клиентами глобально распределенную систему баз данных от корпорации Майкрософт который предназначен для облака hello."
keywords: apache spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="77608-104">Ускорение аналитика в реальном времени большие наборы данных с помощью соединителя Cosmos DB tooAzure Spark hello</span><span class="sxs-lookup"><span data-stu-id="77608-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="77608-105">Соединитель БД Cosmos tooAzure Spark Hello позволяет Azure Cosmos DB tooact как входной источник или приемник выходных данных для задания Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="77608-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="77608-106">Подключение [Spark](http://spark.apache.org/) слишком[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) ускоряется вашей возможность toosolve быстро меняющихся данных обработки и анализа проблем, где можно использовать базу данных Azure Cosmos tooquickly сохранять и запрашивать данные.</span><span class="sxs-lookup"><span data-stu-id="77608-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="77608-107">Соединитель БД Cosmos tooAzure Spark Hello эффективно использует hello собственного Azure DB Cosmos управляемых индексов.</span><span class="sxs-lookup"><span data-stu-id="77608-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="77608-108">индексы Hello позволяют обновляемых столбцов, при выполнении аналитика и принудительной передачи предикат фильтрации быстро изменяющиеся глобально распределенных данных, что в диапазоне от обработки и анализа и анализа сценариев toodata Интернета вещей (IoT).</span><span class="sxs-lookup"><span data-stu-id="77608-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="77608-109">Для работы с Spark GraphX и hello Gremlin graph API-интерфейсы из Cosmos базу данных Azure, в разделе [выполнить анализ графа, с помощью Spark и Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="77608-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="77608-110">Загрузить</span><span class="sxs-lookup"><span data-stu-id="77608-110">Download</span></span>

<span data-ttu-id="77608-111">tooget работы, загрузите hello Spark tooAzure Cosmos DB соединитель (Предварительная версия) из hello [azure cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="77608-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="77608-112">Компоненты соединителя</span><span class="sxs-lookup"><span data-stu-id="77608-112">Connector components</span></span>

<span data-ttu-id="77608-113">Соединитель Hello использует hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="77608-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="77608-114">[Azure Cosmos DB](http://documentdb.com) включает tooprovision клиентов и гибко масштабирования пропускной способности и хранения в пределах любое количество географических регионах.</span><span class="sxs-lookup"><span data-stu-id="77608-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="77608-115">Здравствуйте, предлагаемым службой:</span><span class="sxs-lookup"><span data-stu-id="77608-115">hello service offers:</span></span>
   * <span data-ttu-id="77608-116">Готовое решение [глобального распределения](distribute-data-globally.md) и горизонтального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="77608-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="77608-117">Гарантируется задержкой цифра процентиля 99 hello</span><span class="sxs-lookup"><span data-stu-id="77608-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * <span data-ttu-id="77608-118">[Множество точно определенных моделей согласованности](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="77608-118">[Multiple well-defined consistency models](consistency-levels.md)</span></span>
   * <span data-ttu-id="77608-119">Гарантии высокой доступности с возможностями множественной адресации.</span><span class="sxs-lookup"><span data-stu-id="77608-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="77608-120">Все возможности прописаны в ведущих в отрасли универсальных [соглашениях об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA).</span><span class="sxs-lookup"><span data-stu-id="77608-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="77608-121">[Apache Spark](http://spark.apache.org/) — высокопроизводительная подсистема обработки с открытым исходным кодом, призванная ускорить разработку, повысить удобство использования и реализовать сложную аналитику.</span><span class="sxs-lookup"><span data-stu-id="77608-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="77608-122">[Apache Spark на Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) , чтобы выполнить развертывание Apache Spark в облаке hello для критически важных развертываний с помощью [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="77608-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="77608-123">Официально поддерживаемые версии:</span><span class="sxs-lookup"><span data-stu-id="77608-123">Officially supported versions:</span></span>

| <span data-ttu-id="77608-124">Компонент</span><span class="sxs-lookup"><span data-stu-id="77608-124">Component</span></span> | <span data-ttu-id="77608-125">Версия</span><span class="sxs-lookup"><span data-stu-id="77608-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="77608-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="77608-126">Apache Spark</span></span>|<span data-ttu-id="77608-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="77608-127">2.0+</span></span>|
| <span data-ttu-id="77608-128">Scala</span><span class="sxs-lookup"><span data-stu-id="77608-128">Scala</span></span>| <span data-ttu-id="77608-129">2.11</span><span class="sxs-lookup"><span data-stu-id="77608-129">2.11</span></span>|
| <span data-ttu-id="77608-130">Пакет SDK для Java в Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="77608-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="77608-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="77608-131">1.10.0</span></span> |

<span data-ttu-id="77608-132">Эта статья поможет вам выполнять некоторые простые примеры с помощью Python (через pyDocumentDB) и hello Scala интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="77608-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="77608-133">Существует два подхода tooconnect Apache Spark Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="77608-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="77608-134">Использовать pyDocumentDB через hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="77608-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="77608-135">Создать соединитель Cosmos DB tooAzure Spark на языке Java, используя hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="77608-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="77608-136">Реализация pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="77608-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="77608-137">Hello текущей [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) позволяет вам tooAzure Spark tooconnect Cosmos DB, как показано в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="77608-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Spark tooAzure Cosmos DB потока данных через pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="77608-139">Поток данных в реализации pyDocumentDB hello</span><span class="sxs-lookup"><span data-stu-id="77608-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="77608-140">поток данных Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="77608-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="77608-141">главный узел Spark Hello подключается узлу шлюза Azure Cosmos DB toohello через pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="77608-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="77608-142">Пользователь указывает только hello Spark и Azure Cosmos DB подключения.</span><span class="sxs-lookup"><span data-stu-id="77608-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="77608-143">Подключения toohello соответствующих master и шлюза узлы представляют собой прозрачное toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="77608-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="77608-144">узел шлюза Hello делает запрос hello DB Cosmos Azure, где запрос hello впоследствии выполняется к коллекции hello секций в hello узлы данных.</span><span class="sxs-lookup"><span data-stu-id="77608-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="77608-145">Hello для таких запросов отправке ответа toohello узла шлюза, а этот результирующий набор возвращается toohello Spark главного узла.</span><span class="sxs-lookup"><span data-stu-id="77608-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="77608-146">Последующие запросы (например, к Spark кадр данных под) отправляются toohello Spark рабочих узлов для обработки.</span><span class="sxs-lookup"><span data-stu-id="77608-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="77608-147">Связь между Spark и Azure Cosmos DB является ограниченной toohello Spark главного узла и узлы шлюза Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77608-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="77608-148">запросы Hello перейдите быстро позволяет hello транспортный уровень между этими двумя узлами.</span><span class="sxs-lookup"><span data-stu-id="77608-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="77608-149">Установка pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="77608-149">Install pyDocumentDB</span></span>
<span data-ttu-id="77608-150">pyDocumentDB можно установить на узел драйвера с помощью **pip** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="77608-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="77608-151">Подключение tooAzure Spark Cosmos DB через pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="77608-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="77608-152">Простота Hello транспорта взаимодействия hello делает выполнения запроса из Spark tooAzure Cosmos DB с помощью pyDocumentDB относительно проста.</span><span class="sxs-lookup"><span data-stu-id="77608-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="77608-153">Здравствуйте, в следующем фрагменте кода показан код как pyDocumentDB toouse в контексте Spark.</span><span class="sxs-lookup"><span data-stu-id="77608-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="77608-154">Как отмечено во фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="77608-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="77608-155">Hello Azure Cosmos DB Python SDK (`pyDocumentDB`) содержит hello Здравствуйте, все параметры, необходимые для подключения.</span><span class="sxs-lookup"><span data-stu-id="77608-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="77608-156">Например hello предпочитаемых параметров расположения выбирает реплики и приоритет порядка чтения hello.</span><span class="sxs-lookup"><span data-stu-id="77608-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="77608-157">Импортируйте необходимые библиотеки hello и настройте ваш **masterKey** и **узла** toocreate hello Azure Cosmos DB *клиента* (**pydocumentdb.document_ клиент**).</span><span class="sxs-lookup"><span data-stu-id="77608-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="77608-158">Выполнение запросов Spark с помощью pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="77608-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="77608-159">Следующие примеры использования hello Azure Cosmos DB экземпляр, который был создан в предыдущем фрагменте кода hello с помощью hello Hello указан ключей только для чтения.</span><span class="sxs-lookup"><span data-stu-id="77608-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="77608-160">Hello следующий фрагмент кода подключается toohello **airports.codes** коллекции в учетной записи DoctorWho hello указанный ранее и выполняется запрос tooextract hello аэропорта города в штате Вашингтон.</span><span class="sxs-lookup"><span data-stu-id="77608-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

<span data-ttu-id="77608-161">После выполнения запроса hello через **запроса**, результат hello **query_iterable. QueryIterable** то есть список преобразованный tooa Python.</span><span class="sxs-lookup"><span data-stu-id="77608-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="77608-162">Список Python может быть легко преобразованный tooa Spark кадр данных с помощью hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="77608-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="77608-163">Зачем использовать hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="77608-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="77608-164">Подключение tooAzure Spark Cosmos DB с помощью pyDocumentDB обычно предназначен для сценариев, где:</span><span class="sxs-lookup"><span data-stu-id="77608-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="77608-165">Вы хотите toouse Python.</span><span class="sxs-lookup"><span data-stu-id="77608-165">You want toouse Python.</span></span>
* <span data-ttu-id="77608-166">Вы возвращаете относительно небольшой результирующий набор из tooSpark Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77608-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="77608-167">Обратите внимание, что hello базового набора данных в базе данных Azure Cosmos может быть достаточно большим.</span><span class="sxs-lookup"><span data-stu-id="77608-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="77608-168">К источнику Azure Cosmos DB можно применить фильтры предиката.</span><span class="sxs-lookup"><span data-stu-id="77608-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="77608-169">Spark tooAzure соединитель БД Cosmos</span><span class="sxs-lookup"><span data-stu-id="77608-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="77608-170">Соединитель БД Cosmos tooAzure Spark Hello использует hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) и перемещает данные между hello Spark рабочих узлов и Azure Cosmos DB, как показано в hello, следующая схема:</span><span class="sxs-lookup"><span data-stu-id="77608-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Поток данных в соединитель БД Cosmos tooAzure Spark hello](./media/spark-connector/spark-connector.png)

<span data-ttu-id="77608-172">поток данных Hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="77608-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="77608-173">главный узел Spark Hello подключается toohello узел шлюза Azure Cosmos DB tooobtain схема секционирования hello.</span><span class="sxs-lookup"><span data-stu-id="77608-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="77608-174">Пользователь указывает только hello Spark и Azure Cosmos DB подключения.</span><span class="sxs-lookup"><span data-stu-id="77608-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="77608-175">Подключения toohello соответствующих master и шлюза узлы представляют собой прозрачное toohello пользователя.</span><span class="sxs-lookup"><span data-stu-id="77608-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="77608-176">Эти сведения предоставляются задней toohello Spark главного узла.</span><span class="sxs-lookup"><span data-stu-id="77608-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="77608-177">На этом этапе следует секций может tooparse hello запросов toodetermine hello и их расположения в необходимые tooaccess DB Cosmos Azure.</span><span class="sxs-lookup"><span data-stu-id="77608-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="77608-178">Эта информация является передаваемых toohello Spark рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="77608-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="77608-179">Hello Spark рабочих узлов подключиться секций Azure Cosmos DB toohello напрямую tooextract hello данных и возвращает toohello данных hello Spark разделы в hello Spark рабочих узлов.</span><span class="sxs-lookup"><span data-stu-id="77608-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="77608-180">Обмен данными между Spark и Azure Cosmos DB работает значительно быстрее, так как hello перемещение данных между hello Spark рабочих узлов и узлы данных Azure Cosmos DB hello (секции).</span><span class="sxs-lookup"><span data-stu-id="77608-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="77608-181">Построение соединитель БД Cosmos tooAzure Spark hello</span><span class="sxs-lookup"><span data-stu-id="77608-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="77608-182">В настоящее время проект hello соединитель использует maven.</span><span class="sxs-lookup"><span data-stu-id="77608-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="77608-183">Соединитель hello toobuild без зависимостей, можно запустить:</span><span class="sxs-lookup"><span data-stu-id="77608-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="77608-184">Можно также загрузить последние версии hello JAR hello из hello *освобождает* папки.</span><span class="sxs-lookup"><span data-stu-id="77608-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="77608-185">Включить hello Azure Spark Cosmos DB JAR</span><span class="sxs-lookup"><span data-stu-id="77608-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="77608-186">Перед выполнением любого кода необходимо tooinclude hello Azure Spark Cosmos DB JAR.</span><span class="sxs-lookup"><span data-stu-id="77608-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="77608-187">Если вы используете hello **spark оболочки**, hello JAR-ФАЙЛ можно включить с помощью hello **--JAR-файлов** параметр.</span><span class="sxs-lookup"><span data-stu-id="77608-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="77608-188">Hello tooexecute JAR без зависимостей, используйте hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="77608-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="77608-189">Если вы используете ноутбук службы, например службы записной книжки Azure HDInsight Jupyter, можно использовать hello **усилить магическое** команды:</span><span class="sxs-lookup"><span data-stu-id="77608-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="77608-190">Hello **JAR-файлов** команда включает вы tooinclude hello две JAR-файлов, необходимых для **azure cosmosdb-spark** (сам и hello Azure DocumentDB Java SDK) и исключить **scala-отражают** , чтобы он не будет мешать работе hello вызывает Livy (книжке Jupyter > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="77608-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="77608-191">Spark подключиться с помощью Cosmos DB tooAzure hello соединителя</span><span class="sxs-lookup"><span data-stu-id="77608-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="77608-192">Несмотря на то, что hello связи транспортом является несколько более сложен, выполнение запроса из Spark tooAzure Cosmos DB с помощью соединителя hello значительно быстрее.</span><span class="sxs-lookup"><span data-stu-id="77608-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="77608-193">Привет, следующий фрагмент кода показывает, как toouse hello соединителя в контексте Spark.</span><span class="sxs-lookup"><span data-stu-id="77608-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="77608-194">Как отмечено во фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="77608-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="77608-195">**Azure-cosmosdb-spark** содержит hello все Здравствуйте, необходимые для подключения параметры, которые включают hello предпочитаемый расположения.</span><span class="sxs-lookup"><span data-stu-id="77608-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="77608-196">Например вы можете hello чтения реплики и приоритет порядка.</span><span class="sxs-lookup"><span data-stu-id="77608-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="77608-197">Просто hello необходимые библиотеки импорта и настроить клиент Azure Cosmos DB hello masterKey и узла toocreate.</span><span class="sxs-lookup"><span data-stu-id="77608-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="77608-198">Выполнение запросов Spark через соединитель hello</span><span class="sxs-lookup"><span data-stu-id="77608-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="77608-199">Следующий пример использует hello Azure Cosmos DB экземпляром, созданный в предыдущем фрагменте кода hello с помощью hello Hello указан ключей только для чтения.</span><span class="sxs-lookup"><span data-stu-id="77608-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="77608-200">Hello следующий фрагмент кода подключается коллекции DepartureDelays.flights_pcoll toohello (в hello DoctorWho учетной записи, как указано ранее) и запускает запрос tooextract hello рейса задержки сведения рейсов, которые отправления Сиэтл.</span><span class="sxs-lookup"><span data-stu-id="77608-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="77608-201">Зачем использовать hello Spark tooAzure Cosmos соединителя реализации DB?</span><span class="sxs-lookup"><span data-stu-id="77608-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="77608-202">Подключение tooAzure Spark Cosmos DB с помощью соединителя hello обычно предназначен для сценариев, где:</span><span class="sxs-lookup"><span data-stu-id="77608-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="77608-203">Вы хотите toouse Scala и обновить его tooinclude оболочку Python, как указано в [проблема 3: Добавление Python оболочки и примеры](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="77608-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="77608-204">У вас есть большой объем данных tootransfer между Apache Spark и Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77608-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="77608-205">toogive отображается представление о hello разницы в производительности запросов, hello [запрос тестовых запусков вики-сайте](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="77608-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="77608-206">Пример распределенного агрегирования</span><span class="sxs-lookup"><span data-stu-id="77608-206">Distributed aggregation example</span></span>
<span data-ttu-id="77608-207">В этом разделе приведены некоторые примеры того, как можно выполнить распределенное агрегирование и аналитику с помощью Apache Spark и Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77608-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="77608-208">Azure Cosmos DB уже поддерживает агрегаты, которые рассматриваются в hello [планеты шкалы агрегаты с блог Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="77608-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="77608-209">Вот как можно использовать его toohello рядом с Apache Spark уровня.</span><span class="sxs-lookup"><span data-stu-id="77608-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="77608-210">Обратите внимание, что эти агрегаты — в ссылку toohello [ноутбук соединитель БД Cosmos Spark tooAzure](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="77608-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="77608-211">Подключение tooflights образца данных</span><span class="sxs-lookup"><span data-stu-id="77608-211">Connect tooflights sample data</span></span>
<span data-ttu-id="77608-212">Эти примеры агрегаций получают доступ к данным о выполнении рейсов, которые хранятся в базе данных Azure Cosmos DB **DoctorWho**.</span><span class="sxs-lookup"><span data-stu-id="77608-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="77608-213">tooconnect tooit требуется tooutilize hello, следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="77608-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="77608-214">Следующим фрагментом мы также являются постоянной toorun базовый запрос, что передачи hello отфильтрованный набор данных из базы данных Azure Cosmos tooSpark где hello последнее можно выполнить распределенные статистических выражений.</span><span class="sxs-lookup"><span data-stu-id="77608-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="77608-215">В этом случае мы запрашиваем сведения об авиарейсах, вылетающих из Сиэтла (SEA).</span><span class="sxs-lookup"><span data-stu-id="77608-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="77608-216">Hello следующие результаты были созданы при выполнении запросов hello из службы записной книжки Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="77608-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="77608-217">Обратите внимание, что все фрагменты кода hello универсальных и не только tooany службы.</span><span class="sxs-lookup"><span data-stu-id="77608-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="77608-218">Выполнение запросов LIMIT и COUNT</span><span class="sxs-lookup"><span data-stu-id="77608-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="77608-219">Точно так же, как вы будете использовать tooin SQL/Spark SQL, давайте начать с **ограничение** запроса:</span><span class="sxs-lookup"><span data-stu-id="77608-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Запрос Spark LIMIT](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="77608-221">Hello следующего запроса является простой и быстрый **число** запроса:</span><span class="sxs-lookup"><span data-stu-id="77608-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Запрос Spark COUNT](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="77608-223">Запрос GROUP BY</span><span class="sxs-lookup"><span data-stu-id="77608-223">GROUP BY query</span></span>
<span data-ttu-id="77608-224">В следующем наборе можно легко выполнять запросы **GROUP BY** к базе данных Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="77608-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![График запроса Spark GROUP BY](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="77608-226">Запросы DISTINCT и ORDER BY</span><span class="sxs-lookup"><span data-stu-id="77608-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="77608-227">Запросы **DISTINCT и ORDER BY** выглядят так:</span><span class="sxs-lookup"><span data-stu-id="77608-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![График запроса Spark GROUP BY](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="77608-229">Продолжить анализ данных рейса hello</span><span class="sxs-lookup"><span data-stu-id="77608-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="77608-230">Можно использовать пример запросов toocontinue анализа данных рейса hello hello.</span><span class="sxs-lookup"><span data-stu-id="77608-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="77608-231">Первые 5 задержанных рейсов, вылетающих из Сиэтла</span><span class="sxs-lookup"><span data-stu-id="77608-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![График Spark для первых задержанных рейсов](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="77608-233">Вычисление медианы задержки вылетов из Сиэтла по городам назначения</span><span class="sxs-lookup"><span data-stu-id="77608-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![График медианы задержки Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="77608-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="77608-235">Next steps</span></span>

<span data-ttu-id="77608-236">Если это еще не сделано, загрузите соединитель БД Cosmos tooAzure Spark hello с hello [azure cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) репозитории GitHub и исследовать hello дополнительные ресурсы в репозитории hello:</span><span class="sxs-lookup"><span data-stu-id="77608-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* <span data-ttu-id="77608-237">[Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples) (Примеры агрегирований)</span><span class="sxs-lookup"><span data-stu-id="77608-237">[Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)</span></span>
* <span data-ttu-id="77608-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples) (Примеры скриптов и записных книжек)</span><span class="sxs-lookup"><span data-stu-id="77608-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)</span></span>

<span data-ttu-id="77608-239">Можно также tooreview hello [Apache Spark SQL, блоки данных и наборы данных руководство](http://spark.apache.org/docs/latest/sql-programming-guide.html) и hello [Apache Spark в Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="77608-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
