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
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a>Ускорение аналитика в реальном времени большие наборы данных с помощью соединителя Cosmos DB tooAzure Spark hello

Соединитель БД Cosmos tooAzure Spark Hello позволяет Azure Cosmos DB tooact как входной источник или приемник выходных данных для задания Apache Spark. Подключение [Spark](http://spark.apache.org/) слишком[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) ускоряется вашей возможность toosolve быстро меняющихся данных обработки и анализа проблем, где можно использовать базу данных Azure Cosmos tooquickly сохранять и запрашивать данные. Соединитель БД Cosmos tooAzure Spark Hello эффективно использует hello собственного Azure DB Cosmos управляемых индексов. индексы Hello позволяют обновляемых столбцов, при выполнении аналитика и принудительной передачи предикат фильтрации быстро изменяющиеся глобально распределенных данных, что в диапазоне от обработки и анализа и анализа сценариев toodata Интернета вещей (IoT).

Для работы с Spark GraphX и hello Gremlin graph API-интерфейсы из Cosmos базу данных Azure, в разделе [выполнить анализ графа, с помощью Spark и Apache TinkerPop Gremlin](spark-connector-graph.md).

## <a name="download"></a>Загрузить

tooget работы, загрузите hello Spark tooAzure Cosmos DB соединитель (Предварительная версия) из hello [azure cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) репозитория в GitHub.

## <a name="connector-components"></a>Компоненты соединителя

Соединитель Hello использует hello следующие компоненты:

* [Azure Cosmos DB](http://documentdb.com) включает tooprovision клиентов и гибко масштабирования пропускной способности и хранения в пределах любое количество географических регионах. Здравствуйте, предлагаемым службой:
   * Готовое решение [глобального распределения](distribute-data-globally.md) и горизонтального масштабирования.
   * Гарантируется задержкой цифра процентиля 99 hello
   * [Множество точно определенных моделей согласованности](consistency-levels.md).
   * Гарантии высокой доступности с возможностями множественной адресации.
   * Все возможности прописаны в ведущих в отрасли универсальных [соглашениях об уровне обслуживания](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA).

* [Apache Spark](http://spark.apache.org/) — высокопроизводительная подсистема обработки с открытым исходным кодом, призванная ускорить разработку, повысить удобство использования и реализовать сложную аналитику.

* [Apache Spark на Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) , чтобы выполнить развертывание Apache Spark в облаке hello для критически важных развертываний с помощью [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Официально поддерживаемые версии:

| Компонент | Версия |
|---------|-------|
|Apache Spark|2.0+|
| Scala| 2.11|
| Пакет SDK для Java в Azure DocumentDB | 1.10.0 |

Эта статья поможет вам выполнять некоторые простые примеры с помощью Python (через pyDocumentDB) и hello Scala интерфейсов.

Существует два подхода tooconnect Apache Spark Azure Cosmos DB:
- Использовать pyDocumentDB через hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).
- Создать соединитель Cosmos DB tooAzure Spark на языке Java, используя hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).

## <a name="pydocumentdb-implementation"></a>Реализация pyDocumentDB
Hello текущей [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) позволяет вам tooAzure Spark tooconnect Cosmos DB, как показано в hello, следующая схема:

![Spark tooAzure Cosmos DB потока данных через pyDocumentDB DB](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a>Поток данных в реализации pyDocumentDB hello

поток данных Hello выглядит следующим образом:

1. главный узел Spark Hello подключается узлу шлюза Azure Cosmos DB toohello через pyDocumentDB. Пользователь указывает только hello Spark и Azure Cosmos DB подключения. Подключения toohello соответствующих master и шлюза узлы представляют собой прозрачное toohello пользователя.
2. узел шлюза Hello делает запрос hello DB Cosmos Azure, где запрос hello впоследствии выполняется к коллекции hello секций в hello узлы данных. Hello для таких запросов отправке ответа toohello узла шлюза, а этот результирующий набор возвращается toohello Spark главного узла.
3. Последующие запросы (например, к Spark кадр данных под) отправляются toohello Spark рабочих узлов для обработки.

Связь между Spark и Azure Cosmos DB является ограниченной toohello Spark главного узла и узлы шлюза Azure Cosmos DB.  запросы Hello перейдите быстро позволяет hello транспортный уровень между этими двумя узлами.

### <a name="install-pydocumentdb"></a>Установка pyDocumentDB
pyDocumentDB можно установить на узел драйвера с помощью **pip** следующим образом:

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a>Подключение tooAzure Spark Cosmos DB через pyDocumentDB
Простота Hello транспорта взаимодействия hello делает выполнения запроса из Spark tooAzure Cosmos DB с помощью pyDocumentDB относительно проста.

Здравствуйте, в следующем фрагменте кода показан код как pyDocumentDB toouse в контексте Spark.

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

Как отмечено во фрагмент кода hello:

* Hello Azure Cosmos DB Python SDK (`pyDocumentDB`) содержит hello Здравствуйте, все параметры, необходимые для подключения. Например hello предпочитаемых параметров расположения выбирает реплики и приоритет порядка чтения hello.
*  Импортируйте необходимые библиотеки hello и настройте ваш **masterKey** и **узла** toocreate hello Azure Cosmos DB *клиента* (**pydocumentdb.document_ клиент**).


### <a name="execute-spark-queries-via-pydocumentdb"></a>Выполнение запросов Spark с помощью pyDocumentDB
Следующие примеры использования hello Azure Cosmos DB экземпляр, который был создан в предыдущем фрагменте кода hello с помощью hello Hello указан ключей только для чтения. Hello следующий фрагмент кода подключается toohello **airports.codes** коллекции в учетной записи DoctorWho hello указанный ранее и выполняется запрос tooextract hello аэропорта города в штате Вашингтон.

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

После выполнения запроса hello через **запроса**, результат hello **query_iterable. QueryIterable** то есть список преобразованный tooa Python. Список Python может быть легко преобразованный tooa Spark кадр данных с помощью hello, следующий код:

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a>Зачем использовать hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?
Подключение tooAzure Spark Cosmos DB с помощью pyDocumentDB обычно предназначен для сценариев, где:

* Вы хотите toouse Python.
* Вы возвращаете относительно небольшой результирующий набор из tooSpark Azure Cosmos DB. Обратите внимание, что hello базового набора данных в базе данных Azure Cosmos может быть достаточно большим. К источнику Azure Cosmos DB можно применить фильтры предиката.  

## <a name="spark-tooazure-cosmos-db-connector"></a>Spark tooAzure соединитель БД Cosmos

Соединитель БД Cosmos tooAzure Spark Hello использует hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) и перемещает данные между hello Spark рабочих узлов и Azure Cosmos DB, как показано в hello, следующая схема:

![Поток данных в соединитель БД Cosmos tooAzure Spark hello](./media/spark-connector/spark-connector.png)

поток данных Hello выглядит следующим образом:

1. главный узел Spark Hello подключается toohello узел шлюза Azure Cosmos DB tooobtain схема секционирования hello. Пользователь указывает только hello Spark и Azure Cosmos DB подключения. Подключения toohello соответствующих master и шлюза узлы представляют собой прозрачное toohello пользователя.
2. Эти сведения предоставляются задней toohello Spark главного узла.  На этом этапе следует секций может tooparse hello запросов toodetermine hello и их расположения в необходимые tooaccess DB Cosmos Azure.
3. Эта информация является передаваемых toohello Spark рабочих узлов.
4. Hello Spark рабочих узлов подключиться секций Azure Cosmos DB toohello напрямую tooextract hello данных и возвращает toohello данных hello Spark разделы в hello Spark рабочих узлов.

Обмен данными между Spark и Azure Cosmos DB работает значительно быстрее, так как hello перемещение данных между hello Spark рабочих узлов и узлы данных Azure Cosmos DB hello (секции).

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a>Построение соединитель БД Cosmos tooAzure Spark hello
В настоящее время проект hello соединитель использует maven. Соединитель hello toobuild без зависимостей, можно запустить:
```
mvn clean package
```
Можно также загрузить последние версии hello JAR hello из hello *освобождает* папки.

### <a name="include-hello-azure-cosmos-db-spark-jar"></a>Включить hello Azure Spark Cosmos DB JAR
Перед выполнением любого кода необходимо tooinclude hello Azure Spark Cosmos DB JAR.  Если вы используете hello **spark оболочки**, hello JAR-ФАЙЛ можно включить с помощью hello **--JAR-файлов** параметр.  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

Hello tooexecute JAR без зависимостей, используйте hello, следующий код:

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

Если вы используете ноутбук службы, например службы записной книжки Azure HDInsight Jupyter, можно использовать hello **усилить магическое** команды:

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

Hello **JAR-файлов** команда включает вы tooinclude hello две JAR-файлов, необходимых для **azure cosmosdb-spark** (сам и hello Azure DocumentDB Java SDK) и исключить **scala-отражают** , чтобы он не будет мешать работе hello вызывает Livy (книжке Jupyter > Livy > Spark).

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a>Spark подключиться с помощью Cosmos DB tooAzure hello соединителя
Несмотря на то, что hello связи транспортом является несколько более сложен, выполнение запроса из Spark tooAzure Cosmos DB с помощью соединителя hello значительно быстрее.

Привет, следующий фрагмент кода показывает, как toouse hello соединителя в контексте Spark.

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

Как отмечено во фрагмент кода hello:

- **Azure-cosmosdb-spark** содержит hello все Здравствуйте, необходимые для подключения параметры, которые включают hello предпочитаемый расположения. Например вы можете hello чтения реплики и приоритет порядка.
- Просто hello необходимые библиотеки импорта и настроить клиент Azure Cosmos DB hello masterKey и узла toocreate.

### <a name="execute-spark-queries-via-hello-connector"></a>Выполнение запросов Spark через соединитель hello

Следующий пример использует hello Azure Cosmos DB экземпляром, созданный в предыдущем фрагменте кода hello с помощью hello Hello указан ключей только для чтения. Hello следующий фрагмент кода подключается коллекции DepartureDelays.flights_pcoll toohello (в hello DoctorWho учетной записи, как указано ранее) и запускает запрос tooextract hello рейса задержки сведения рейсов, которые отправления Сиэтл.

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a>Зачем использовать hello Spark tooAzure Cosmos соединителя реализации DB?

Подключение tooAzure Spark Cosmos DB с помощью соединителя hello обычно предназначен для сценариев, где:

* Вы хотите toouse Scala и обновить его tooinclude оболочку Python, как указано в [проблема 3: Добавление Python оболочки и примеры](https://github.com/Azure/azure-cosmosdb-spark/issues/3).
* У вас есть большой объем данных tootransfer между Apache Spark и Azure Cosmos DB.

toogive отображается представление о hello разницы в производительности запросов, hello [запрос тестовых запусков вики-сайте](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).

## <a name="distributed-aggregation-example"></a>Пример распределенного агрегирования
В этом разделе приведены некоторые примеры того, как можно выполнить распределенное агрегирование и аналитику с помощью Apache Spark и Azure Cosmos DB. Azure Cosmos DB уже поддерживает агрегаты, которые рассматриваются в hello [планеты шкалы агрегаты с блог Azure Cosmos DB](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/). Вот как можно использовать его toohello рядом с Apache Spark уровня.

Обратите внимание, что эти агрегаты — в ссылку toohello [ноутбук соединитель БД Cosmos Spark tooAzure](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).

### <a name="connect-tooflights-sample-data"></a>Подключение tooflights образца данных
Эти примеры агрегаций получают доступ к данным о выполнении рейсов, которые хранятся в базе данных Azure Cosmos DB **DoctorWho**. tooconnect tooit требуется tooutilize hello, следующий фрагмент кода:

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

Следующим фрагментом мы также являются постоянной toorun базовый запрос, что передачи hello отфильтрованный набор данных из базы данных Azure Cosmos tooSpark где hello последнее можно выполнить распределенные статистических выражений. В этом случае мы запрашиваем сведения об авиарейсах, вылетающих из Сиэтла (SEA).

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

Hello следующие результаты были созданы при выполнении запросов hello из службы записной книжки Jupyter hello.  Обратите внимание, что все фрагменты кода hello универсальных и не только tooany службы.

### <a name="running-limit-and-count-queries"></a>Выполнение запросов LIMIT и COUNT
Точно так же, как вы будете использовать tooin SQL/Spark SQL, давайте начать с **ограничение** запроса:

![Запрос Spark LIMIT](./media/spark-connector/spark-sql-query.png)

Hello следующего запроса является простой и быстрый **число** запроса:

![Запрос Spark COUNT](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a>Запрос GROUP BY
В следующем наборе можно легко выполнять запросы **GROUP BY** к базе данных Azure Cosmos DB:

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![График запроса Spark GROUP BY](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a>Запросы DISTINCT и ORDER BY
Запросы **DISTINCT и ORDER BY** выглядят так:

![График запроса Spark GROUP BY](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a>Продолжить анализ данных рейса hello
Можно использовать пример запросов toocontinue анализа данных рейса hello hello.

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a>Первые 5 задержанных рейсов, вылетающих из Сиэтла
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![График Spark для первых задержанных рейсов](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a>Вычисление медианы задержки вылетов из Сиэтла по городам назначения
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![График медианы задержки Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a>Дальнейшие действия

Если это еще не сделано, загрузите соединитель БД Cosmos tooAzure Spark hello с hello [azure cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) репозитории GitHub и исследовать hello дополнительные ресурсы в репозитории hello:

* [Aggregations Examples](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples) (Примеры агрегирований)
* [Sample Scripts and Notebooks](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples) (Примеры скриптов и записных книжек)

Можно также tooreview hello [Apache Spark SQL, блоки данных и наборы данных руководство](http://spark.apache.org/docs/latest/sql-programming-guide.html) и hello [Apache Spark в Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) статьи.
