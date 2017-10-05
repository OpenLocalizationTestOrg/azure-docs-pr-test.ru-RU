---
title: "Подключение Apache Spark к Azure Cosmos DB | Документация Майкрософт"
description: "В этом руководстве приведены сведения о соединителе Azure Cosmos DB Spark, который позволяет подключать Apache Spark к Azure Cosmos DB для выполнения распределенного агрегирования и обработки данных в мультитенантной глобально распределенной системе баз данных Майкрософт, разработанной для использования в облачной среде."
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
ms.openlocfilehash: 8ecbb478c81cde25bbd0d1c9ee07ae02b07f8cc7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="f418b-104">Ускорение аналитики больших данных в реальном времени с помощью соединителя Spark для Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f418b-104">Accelerate real-time big-data analytics with the Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="f418b-105">Соединитель Spark для Azure Cosmos DB дает возможность использовать Azure Cosmos DB в качестве источника входных данных или приемника выходных данных для заданий Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="f418b-105">The Spark to Azure Cosmos DB connector enables Azure Cosmos DB to act as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="f418b-106">Подключение [Spark](http://spark.apache.org/) к [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) ускоряет решение проблем анализа данных, используя Azure Cosmos DB для быстрого сохранения и запроса данных.</span><span class="sxs-lookup"><span data-stu-id="f418b-106">Connecting [Spark](http://spark.apache.org/) to [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability to solve fast-moving data science problems where you can use Azure Cosmos DB to quickly persist and query data.</span></span> <span data-ttu-id="f418b-107">Соединитель Spark для Azure Cosmos DB эффективно использует собственные управляемые индексы Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f418b-107">The Spark to Azure Cosmos DB connector efficiently utilizes the native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="f418b-108">Эти индексы позволяют использовать обновляемые столбцы при выполнении анализа, применять фильтры предиката к быстро меняющимся глобально распределенным данным, начиная от Интернета вещей, обработки и анализа данных и до сценариев аналитики.</span><span class="sxs-lookup"><span data-stu-id="f418b-108">The indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) to data science and analytics scenarios.</span></span>

<span data-ttu-id="f418b-109">Дополнительные сведения о работе с API Spark GraphX и графами Gremlin в Azure Cosmos DB см.в статье [Azure Cosmos DB. Аналитика графов с помощью Spark и Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="f418b-109">For working with Spark GraphX and the Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="f418b-110">Загрузить</span><span class="sxs-lookup"><span data-stu-id="f418b-110">Download</span></span>

<span data-ttu-id="f418b-111">Чтобы приступить к работе, скачайте соединитель Spark для Azure Cosmos DB (предварительная версия) из репозитория [azure cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) в GitHub.</span><span class="sxs-lookup"><span data-stu-id="f418b-111">To get started, download the Spark to Azure Cosmos DB connector (preview) from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="f418b-112">Компоненты соединителя</span><span class="sxs-lookup"><span data-stu-id="f418b-112">Connector components</span></span>

<span data-ttu-id="f418b-113">Соединитель использует следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="f418b-113">The connector utilizes the following components:</span></span>

* <span data-ttu-id="f418b-114">[Azure Cosmos DB](http://documentdb.com) позволяет клиентам подготавливать и эластично масштабировать пропускную способность и ресурсы хранилища в любом количестве географических регионов.</span><span class="sxs-lookup"><span data-stu-id="f418b-114">[Azure Cosmos DB](http://documentdb.com) enables customers to provision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="f418b-115">Служба предлагает следующее:</span><span class="sxs-lookup"><span data-stu-id="f418b-115">The service offers:</span></span>
   * <span data-ttu-id="f418b-116">Готовое решение [глобального распределения](distribute-data-globally.md) и горизонтального масштабирования.</span><span class="sxs-lookup"><span data-stu-id="f418b-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="f418b-117">Гарантия задержки, измеряемой единицами, на уровне 99-го процентиля.</span><span class="sxs-lookup"><span data-stu-id="f418b-117">Guaranteed single digit latencies at the 99th percentile</span></span>
   * <span data-ttu-id="f418b-118">[Множество точно определенных моделей согласованности](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="f418b-118">[Multiple well-defined consistency models](consistency-levels.md)</span></span>
   * <span data-ttu-id="f418b-119">Гарантии высокой доступности с возможностями множественной адресации.</span><span class="sxs-lookup"><span data-stu-id="f418b-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="f418b-120">Все возможности прописаны в ведущих в отрасли универсальных [соглашениях об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA).</span><span class="sxs-lookup"><span data-stu-id="f418b-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="f418b-121">[Apache Spark](http://spark.apache.org/) — высокопроизводительная подсистема обработки с открытым исходным кодом, призванная ускорить разработку, повысить удобство использования и реализовать сложную аналитику.</span><span class="sxs-lookup"><span data-stu-id="f418b-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="f418b-122">[Apache Spark в Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) — чтобы Apache Spark можно было развернуть в облаке для критически важных приложений, используя [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="f418b-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in the cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="f418b-123">Официально поддерживаемые версии:</span><span class="sxs-lookup"><span data-stu-id="f418b-123">Officially supported versions:</span></span>

| <span data-ttu-id="f418b-124">Компонент</span><span class="sxs-lookup"><span data-stu-id="f418b-124">Component</span></span> | <span data-ttu-id="f418b-125">Версия</span><span class="sxs-lookup"><span data-stu-id="f418b-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="f418b-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="f418b-126">Apache Spark</span></span>|<span data-ttu-id="f418b-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="f418b-127">2.0+</span></span>|
| <span data-ttu-id="f418b-128">Scala</span><span class="sxs-lookup"><span data-stu-id="f418b-128">Scala</span></span>| <span data-ttu-id="f418b-129">2.11</span><span class="sxs-lookup"><span data-stu-id="f418b-129">2.11</span></span>|
| <span data-ttu-id="f418b-130">Пакет SDK для Java в Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="f418b-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="f418b-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="f418b-131">1.10.0</span></span> |

<span data-ttu-id="f418b-132">Эта статья поможет вам выполнить некоторые простые примеры на языке Python (через pyDocumentDB) с помощью интерфейса Scala.</span><span class="sxs-lookup"><span data-stu-id="f418b-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and the Scala interfaces.</span></span>

<span data-ttu-id="f418b-133">Существует два способа подключения Apache Spark и Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="f418b-133">There are two approaches to connect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="f418b-134">с помощью pyDocumentDB через [пакет SDK для Java в Azure DocumentDB](https://github.com/Azure/azure-documentdb-python);</span><span class="sxs-lookup"><span data-stu-id="f418b-134">Use pyDocumentDB via the [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="f418b-135">с помощью соединителя Spark для Azure Cosmos DB на основе Java, использующего [пакет SDK для Java в Azure DocumentDB](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="f418b-135">Create a Java-based Spark to Azure Cosmos DB connector by utilizing the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="f418b-136">Реализация pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="f418b-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="f418b-137">Текущий [пакет SDK для pyDocumentDB](https://github.com/Azure/azure-documentdb-python) дает возможность подключить Spark к Azure Cosmos DB, как показано на следующей схеме:</span><span class="sxs-lookup"><span data-stu-id="f418b-137">The current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you to connect Spark to Azure Cosmos DB as shown in the following diagram:</span></span>

![Поток данных из Spark в Azure Cosmos DB через pyDocument DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-the-pydocumentdb-implementation"></a><span data-ttu-id="f418b-139">Путь потока данных в pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="f418b-139">Data flow of the pyDocumentDB implementation</span></span>

<span data-ttu-id="f418b-140">Путь потока данных выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f418b-140">The data flow is as follows:</span></span>

1. <span data-ttu-id="f418b-141">Главный узел Spark подключается к узлу шлюза Azure Cosmos DB через pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f418b-141">The Spark master node connects to the Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="f418b-142">Пользователь указывает только подключения Spark и Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f418b-142">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="f418b-143">Соединения в соответствующих главном узле и узле шлюза прозрачны для пользователя.</span><span class="sxs-lookup"><span data-stu-id="f418b-143">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="f418b-144">Узел шлюза делает запрос к Azure Cosmos DB. Далее запрос отправляется к разделам коллекции в узлах данных.</span><span class="sxs-lookup"><span data-stu-id="f418b-144">The gateway node makes the query against Azure Cosmos DB where the query subsequently runs against the collection's partitions in the data nodes.</span></span> <span data-ttu-id="f418b-145">Ответ на эти запросы возвращается в узел шлюза, а результирующий набор — в главный узел Spark.</span><span class="sxs-lookup"><span data-stu-id="f418b-145">The response for those queries is sent back to the gateway node, and that result set is returned to the Spark master node.</span></span>
3. <span data-ttu-id="f418b-146">Последующие запросы (например, к таблице данных Spark) отправляются в рабочие узлы Spark для обработки.</span><span class="sxs-lookup"><span data-stu-id="f418b-146">Subsequent queries (for example, against a Spark DataFrame) are sent to the Spark worker nodes for processing.</span></span>

<span data-ttu-id="f418b-147">Взаимодействие между Spark и Azure Cosmos DB происходит в пределах главного узла Spark и узлов шлюза Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f418b-147">Communication between Spark and Azure Cosmos DB is limited to the Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="f418b-148">Скорость запросов зависит от транспортного уровня между двумя этими узлами.</span><span class="sxs-lookup"><span data-stu-id="f418b-148">The queries go as fast as the transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="f418b-149">Установка pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="f418b-149">Install pyDocumentDB</span></span>
<span data-ttu-id="f418b-150">pyDocumentDB можно установить на узел драйвера с помощью **pip** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f418b-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-to-azure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="f418b-151">Подключение Spark к Azure Cosmos DB через pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="f418b-151">Connect Spark to Azure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="f418b-152">Благодаря простоте обмена данными выполнение запроса из Spark в Azure Cosmos DB с помощью pyDocumentDB относительно простое.</span><span class="sxs-lookup"><span data-stu-id="f418b-152">The simplicity of the communication transport makes execution of a query from Spark to Azure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="f418b-153">В приведенном ниже фрагменте кода показано, как использовать pyDocumentDB в контексте Spark.</span><span class="sxs-lookup"><span data-stu-id="f418b-153">The following code snippet shows how to use pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring the connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys to connect to Azure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="f418b-154">Во фрагменте кода указано:</span><span class="sxs-lookup"><span data-stu-id="f418b-154">As noted in the code snippet:</span></span>

* <span data-ttu-id="f418b-155">Пакет SDK Python для Azure Cosmos DB (`pyDocumentDB`) содержит все необходимые параметры подключения.</span><span class="sxs-lookup"><span data-stu-id="f418b-155">The Azure Cosmos DB Python SDK (`pyDocumentDB`) contains the all the necessary connection parameters.</span></span> <span data-ttu-id="f418b-156">Например, параметр предпочтительных расположений выбирает реплику чтения и приоритет.</span><span class="sxs-lookup"><span data-stu-id="f418b-156">For example, the preferred locations parameter chooses the read replica and priority order.</span></span>
*  <span data-ttu-id="f418b-157">Импортируйте необходимые библиотеки, а затем настройте **главный ключ** и **узел** для создания *клиента* Azure Cosmos DB (**pydocumentdb.document_client**).</span><span class="sxs-lookup"><span data-stu-id="f418b-157">Import the necessary libraries and configure your **masterKey** and **host** to create the Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="f418b-158">Выполнение запросов Spark с помощью pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="f418b-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="f418b-159">В следующих примерах используется экземпляр Azure Cosmos DB, созданный в предыдущем фрагменте с использованием указанных ключей, доступных только для чтения.</span><span class="sxs-lookup"><span data-stu-id="f418b-159">The following examples use the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="f418b-160">Следующий фрагмент кода подключается к коллекции **airports.codes** (в учетной записи DoctorWho, как указано ранее) и выполняет запрос для извлечения городов с аэропортами в штате Вашингтон.</span><span class="sxs-lookup"><span data-stu-id="f418b-160">The following code snippet connects to the **airports.codes** collection in the DoctorWho account as specified earlier and runs a query to extract the airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations the Azure Cosmos DB client will use to connect to the database and collection
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

<span data-ttu-id="f418b-161">После выполнения запроса с использованием команды **query** в результате отобразится значение **query_iterable. QueryIterable**, преобразованное в список Python.</span><span class="sxs-lookup"><span data-stu-id="f418b-161">After the query has been executed via **query**, the result is a **query_iterable.QueryIterable** that is converted to a Python list.</span></span> <span data-ttu-id="f418b-162">Список Python можно легко преобразовать в таблицу данных Spark, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="f418b-162">A Python list can be easily converted to a Spark DataFrame by using the following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-the-pydocumentdb-to-connect-spark-to-azure-cosmos-db"></a><span data-ttu-id="f418b-163">Зачем использовать pyDocumentDB для подключения Spark к Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="f418b-163">Why use the pyDocumentDB to connect Spark to Azure Cosmos DB?</span></span>
<span data-ttu-id="f418b-164">Подключение Spark к Azure Cosmos DB с помощью pyDocumentDB в основном предназначено для следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="f418b-164">Connecting Spark to Azure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="f418b-165">Необходимо использовать Python.</span><span class="sxs-lookup"><span data-stu-id="f418b-165">You want to use Python.</span></span>
* <span data-ttu-id="f418b-166">Необходимо вернуть относительно небольшой набор результатов из Azure Cosmos DB в Spark.</span><span class="sxs-lookup"><span data-stu-id="f418b-166">You are returning a relatively small result set from Azure Cosmos DB to Spark.</span></span> <span data-ttu-id="f418b-167">Обратите внимание, что базовый набор данных в Azure Cosmos DB может быть достаточно большим.</span><span class="sxs-lookup"><span data-stu-id="f418b-167">Note that the underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="f418b-168">К источнику Azure Cosmos DB можно применить фильтры предиката.</span><span class="sxs-lookup"><span data-stu-id="f418b-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="f418b-169">Соединитель Spark для Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f418b-169">Spark to Azure Cosmos DB connector</span></span>

<span data-ttu-id="f418b-170">Соединитель Spark для Azure Cosmos DB использует [пакет SDK для Java в Azure DocumentDB](https://github.com/Azure/azure-documentdb-java) и перемещает данные между рабочими узлами Spark и Azure Cosmos DB, как показано на следующей схеме:</span><span class="sxs-lookup"><span data-stu-id="f418b-170">The Spark to Azure Cosmos DB connector utilizes the [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between the Spark worker nodes and Azure Cosmos DB as shown in the following diagram:</span></span>

![Поток данных в соединителе Spark для Azure Cosmos DB](./media/spark-connector/spark-connector.png)

<span data-ttu-id="f418b-172">Путь потока данных выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f418b-172">The data flow is as follows:</span></span>

1. <span data-ttu-id="f418b-173">Главный узел Spark подключается к узлу шлюза Azure Cosmos DB, чтобы получить схему секционирования.</span><span class="sxs-lookup"><span data-stu-id="f418b-173">The Spark master node connects to the Azure Cosmos DB gateway node to obtain the partition map.</span></span> <span data-ttu-id="f418b-174">Пользователь указывает только подключения Spark и Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f418b-174">A user specifies only the Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="f418b-175">Соединения в соответствующих главном узле и узле шлюза прозрачны для пользователя.</span><span class="sxs-lookup"><span data-stu-id="f418b-175">Connections to the respective master and gateway nodes are transparent to the user.</span></span>
2. <span data-ttu-id="f418b-176">Эта информация возвращается в главный узел Spark.</span><span class="sxs-lookup"><span data-stu-id="f418b-176">This information is provided back to the Spark master node.</span></span>  <span data-ttu-id="f418b-177">На этом этапе вы можете проанализировать запрос, чтобы определить разделы (и их расположения) в Azure Cosmos DB, к которым требуется получить доступ.</span><span class="sxs-lookup"><span data-stu-id="f418b-177">At this point, you should be able to parse the query to determine the partitions and their locations in Azure Cosmos DB that you need to access.</span></span>
3. <span data-ttu-id="f418b-178">Эта информация передается в рабочие узлы Spark.</span><span class="sxs-lookup"><span data-stu-id="f418b-178">This information is transmitted to the Spark worker nodes.</span></span>
4. <span data-ttu-id="f418b-179">Таким образом, рабочие узлы Spark подключаются к разделам Azure Cosmos DB, чтобы извлечь необходимые данные и вернуть их в разделы рабочих узлов Spark.</span><span class="sxs-lookup"><span data-stu-id="f418b-179">The Spark worker nodes connect to the Azure Cosmos DB partitions directly to extract the data and return the data to the Spark partitions in the Spark worker nodes.</span></span>

<span data-ttu-id="f418b-180">Взаимодействие между Spark и Azure Cosmos DB происходит значительно быстрее, так как данные перемещаются между рабочими узлами Spark и узлами данных Azure Cosmos DB (разделами).</span><span class="sxs-lookup"><span data-stu-id="f418b-180">Communication between Spark and Azure Cosmos DB is significantly faster because the data movement is between the Spark worker nodes and the Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-the-spark-to-azure-cosmos-db-connector"></a><span data-ttu-id="f418b-181">Создание соединителя Spark для Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f418b-181">Build the Spark to Azure Cosmos DB connector</span></span>
<span data-ttu-id="f418b-182">Сейчас в проекте соединителя используется maven.</span><span class="sxs-lookup"><span data-stu-id="f418b-182">Currently, the connector project uses maven.</span></span> <span data-ttu-id="f418b-183">Чтобы создать соединитель без зависимостей, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f418b-183">To build the connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="f418b-184">Вы также можете скачать последние версии JAR-файла из папки *releases*.</span><span class="sxs-lookup"><span data-stu-id="f418b-184">You can also download the latest versions of the JAR from the *releases* folder.</span></span>

### <a name="include-the-azure-cosmos-db-spark-jar"></a><span data-ttu-id="f418b-185">Включение JAR-файла Azure Cosmos DB Spark</span><span class="sxs-lookup"><span data-stu-id="f418b-185">Include the Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="f418b-186">Перед выполнением любого кода необходимо добавить JAR-файл Azure Cosmos DB Spark.</span><span class="sxs-lookup"><span data-stu-id="f418b-186">Before you execute any code, you need to include the Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="f418b-187">Если вы используете **spark-shell**, JAR-файл можно включить с помощью параметра **--jars**.</span><span class="sxs-lookup"><span data-stu-id="f418b-187">If you are using the **spark-shell**, then you can include the JAR by using the **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="f418b-188">JAR-файл можно также выполнить без зависимостей, используя следующий код:</span><span class="sxs-lookup"><span data-stu-id="f418b-188">If you want to execute the JAR without dependencies, use the following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="f418b-189">При использовании записной книжки (например, Azure HDInsight Jupyter) вы можете использовать команды **spark magic**:</span><span class="sxs-lookup"><span data-stu-id="f418b-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use the **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="f418b-190">Команда **jars** позволяет включить два JAR-файла, необходимые для **azure-cosmosdb-spark**(и пакета SDK для Java в Azure DocumentDB), и исключает **scala-reflect** для предотвращения конфликта с вызовами Livy (Jupyter Notebook > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="f418b-190">The **jars** command enables you to include the two JARs that are needed for **azure-cosmosdb-spark** (itself and the Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with the Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-to-azure-cosmos-db-using-the-connector"></a><span data-ttu-id="f418b-191">Подключение Spark и Azure Cosmos DB с помощью соединителя</span><span class="sxs-lookup"><span data-stu-id="f418b-191">Connect Spark to Azure Cosmos DB using the connector</span></span>
<span data-ttu-id="f418b-192">Несмотря на то что обмен данными происходит сложнее, запрос из Spark в Azure Cosmos DB с помощью соединителя выполняется значительно быстрее.</span><span class="sxs-lookup"><span data-stu-id="f418b-192">Although the communication transport is a little more complicated, executing a query from Spark to Azure Cosmos DB by using the connector is significantly faster.</span></span>

<span data-ttu-id="f418b-193">В следующем фрагменте кода показано, как использовать соединитель в контексте Spark.</span><span class="sxs-lookup"><span data-stu-id="f418b-193">The following code snippet shows how to use the connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection to your collection
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

<span data-ttu-id="f418b-194">Во фрагменте кода указано:</span><span class="sxs-lookup"><span data-stu-id="f418b-194">As noted in the code snippet:</span></span>

- <span data-ttu-id="f418b-195">**azure-cosmosdb-spark** содержит все необходимые параметры подключения, включая предпочтительное расположения.</span><span class="sxs-lookup"><span data-stu-id="f418b-195">**azure-cosmosdb-spark** contains the all the necessary connection parameters, which include the preferred locations.</span></span> <span data-ttu-id="f418b-196">Например, можно выбрать реплику чтения и приоритет.</span><span class="sxs-lookup"><span data-stu-id="f418b-196">For example, you can choose the read replica and priority order.</span></span>
- <span data-ttu-id="f418b-197">Импортируйте необходимые библиотеки и настройте главный ключ и узел для создания клиента Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f418b-197">Just import the necessary libraries and configure your masterKey and host to create the Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-the-connector"></a><span data-ttu-id="f418b-198">Выполнение запросов Spark с помощью соединителя</span><span class="sxs-lookup"><span data-stu-id="f418b-198">Execute Spark queries via the connector</span></span>

<span data-ttu-id="f418b-199">В следующем примере используется экземпляр Azure Cosmos DB, созданный в предыдущем фрагменте с использованием указанных ключей, доступных только для чтения.</span><span class="sxs-lookup"><span data-stu-id="f418b-199">The following example uses the Azure Cosmos DB instance that was created in the previous snippet by using the specified read-only keys.</span></span> <span data-ttu-id="f418b-200">Следующий фрагмент кода подключается к коллекции DepartureDelays.flights_pcoll (в учетной записи DoctorWho, как указано ранее) и выполняет запрос для извлечения сведений о задержке рейсов, вылетающих из Сиэтла.</span><span class="sxs-lookup"><span data-stu-id="f418b-200">The following code snippet connects to the DepartureDelays.flights_pcoll collection (in the DoctorWho account as specified earlier) and runs a query to extract the flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-the-spark-to-azure-cosmos-db-connector-implementation"></a><span data-ttu-id="f418b-201">Зачем использовать соединитель Spark для Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="f418b-201">Why use the Spark to Azure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="f418b-202">Подключение Spark к Azure Cosmos DB с помощью соединителя в основном предназначено для следующих сценариев:</span><span class="sxs-lookup"><span data-stu-id="f418b-202">Connecting Spark to Azure Cosmos DB by using the connector is typically for scenarios where:</span></span>

* <span data-ttu-id="f418b-203">Необходимо использовать Scala (и обновить его для включения оболочки Python, как указано на странице [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3) (Проблема 3. Добавление оболочки Python с примерами)).</span><span class="sxs-lookup"><span data-stu-id="f418b-203">You want to use Scala and update it to include a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="f418b-204">Необходимо передать большой объем данных между Apache Spark и Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f418b-204">You have a large amount of data to transfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="f418b-205">Чтобы получить представление о разнице в производительности запросов, см. сведения в статье [Query Test Runs](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs) (Тестовые выполнения запросов).</span><span class="sxs-lookup"><span data-stu-id="f418b-205">To give you an idea of the query performance difference, see the [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="f418b-206">Пример распределенного агрегирования</span><span class="sxs-lookup"><span data-stu-id="f418b-206">Distributed aggregation example</span></span>
<span data-ttu-id="f418b-207">В этом разделе приведены некоторые примеры того, как можно выполнить распределенное агрегирование и аналитику с помощью Apache Spark и Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f418b-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="f418b-208">В Azure Cosmos DB уже реализована поддержка агрегирования,как описано в записи блога [Planet scale aggregates with Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/) (Глобальное агрегирование с помощью Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="f418b-208">Azure Cosmos DB already supports aggregations, which is discussed in the [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="f418b-209">Вот как с помощью Apache Spark этот процесс можно выполнить на новом уровне.</span><span class="sxs-lookup"><span data-stu-id="f418b-209">Here is how you can take it to the next level with Apache Spark.</span></span>

<span data-ttu-id="f418b-210">Обратите внимание, что эти агрегирования относятся к [соединителю Spark для Azure Cosmos DB](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="f418b-210">Note that these aggregations are in reference to the [Spark to Azure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-to-flights-sample-data"></a><span data-ttu-id="f418b-211">Подключение к примеру данных о полетах</span><span class="sxs-lookup"><span data-stu-id="f418b-211">Connect to flights sample data</span></span>
<span data-ttu-id="f418b-212">Эти примеры агрегаций получают доступ к данным о выполнении рейсов, которые хранятся в базе данных Azure Cosmos DB **DoctorWho**.</span><span class="sxs-lookup"><span data-stu-id="f418b-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="f418b-213">Чтобы подключиться к ней, используйте следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="f418b-213">To connect to it, you need to utilize the following code snippet:</span></span>

```
// Import Spark to Azure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect to Azure Cosmos DB Database
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

<span data-ttu-id="f418b-214">С помощью этого фрагмента кода мы также выполним базовый запрос, передающий отфильтрованный набор данных из Azure Cosmos DB в Spark (где впоследствии можно выполнить распределенные агрегирования).</span><span class="sxs-lookup"><span data-stu-id="f418b-214">With this snippet, we are also going to run a base query that transfers the filtered set of data from Azure Cosmos DB to Spark where the latter can perform distributed aggregates.</span></span> <span data-ttu-id="f418b-215">В этом случае мы запрашиваем сведения об авиарейсах, вылетающих из Сиэтла (SEA).</span><span class="sxs-lookup"><span data-stu-id="f418b-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="f418b-216">Следующие результаты были получены с помощью запросов от службы Jupyter Notebook.</span><span class="sxs-lookup"><span data-stu-id="f418b-216">The following results were generated by running the queries from the Jupyter notebook service.</span></span>  <span data-ttu-id="f418b-217">Обратите внимание, что все фрагменты кода являются универсальными и не относятся к конкретной службе.</span><span class="sxs-lookup"><span data-stu-id="f418b-217">Note that all the code snippets are generic and not specific to any service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="f418b-218">Выполнение запросов LIMIT и COUNT</span><span class="sxs-lookup"><span data-stu-id="f418b-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="f418b-219">Так же как и в случае с SQL или Spark SQL, начнем с запроса **LIMIT**:</span><span class="sxs-lookup"><span data-stu-id="f418b-219">Just like you're used to in SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Запрос Spark LIMIT](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="f418b-221">Следующий запрос это простой и быстрый запрос **COUNT**:</span><span class="sxs-lookup"><span data-stu-id="f418b-221">The next query is a simple and fast **COUNT** query:</span></span>

![Запрос Spark COUNT](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="f418b-223">Запрос GROUP BY</span><span class="sxs-lookup"><span data-stu-id="f418b-223">GROUP BY query</span></span>
<span data-ttu-id="f418b-224">В следующем наборе можно легко выполнять запросы **GROUP BY** к базе данных Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="f418b-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![График запроса Spark GROUP BY](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="f418b-226">Запросы DISTINCT и ORDER BY</span><span class="sxs-lookup"><span data-stu-id="f418b-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="f418b-227">Запросы **DISTINCT и ORDER BY** выглядят так:</span><span class="sxs-lookup"><span data-stu-id="f418b-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![График запроса Spark GROUP BY](./media/spark-connector/order-by-query.png)

### <a name="continue-the-flight-data-analysis"></a><span data-ttu-id="f418b-229">Дальнейший анализ данных о рейсах</span><span class="sxs-lookup"><span data-stu-id="f418b-229">Continue the flight data analysis</span></span>
<span data-ttu-id="f418b-230">Следующие примеры запросов можно использовать, чтобы продолжить анализ данных о рейсах:</span><span class="sxs-lookup"><span data-stu-id="f418b-230">You can use the following example queries to continue analysis of the flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="f418b-231">Первые 5 задержанных рейсов, вылетающих из Сиэтла</span><span class="sxs-lookup"><span data-stu-id="f418b-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![График Spark для первых задержанных рейсов](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="f418b-233">Вычисление медианы задержки вылетов из Сиэтла по городам назначения</span><span class="sxs-lookup"><span data-stu-id="f418b-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![График медианы задержки Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="f418b-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f418b-235">Next steps</span></span>

<span data-ttu-id="f418b-236">Скачайте соединитель Azure Cosmos DB для Spark из репозитория [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) на сайте GitHub и изучите дополнительные ресурсы в этом репозитории:</span><span class="sxs-lookup"><span data-stu-id="f418b-236">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore the additional resources in the repo:</span></span>

* <span data-ttu-id="f418b-237">[Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples) (Примеры агрегирований)</span><span class="sxs-lookup"><span data-stu-id="f418b-237">[Distributed Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)</span></span>
* <span data-ttu-id="f418b-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples) (Примеры скриптов и записных книжек)</span><span class="sxs-lookup"><span data-stu-id="f418b-238">[Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)</span></span>

<span data-ttu-id="f418b-239">Дополнительные сведения см. также в [руководстве по SQL, таблицам и наборам данных Apache Spark](http://spark.apache.org/docs/latest/sql-programming-guide.html) и в статье [Начало работы. Создание кластера Apache Spark в Azure HDInsight и выполнение интерактивных запросов с помощью SQL Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="f418b-239">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
