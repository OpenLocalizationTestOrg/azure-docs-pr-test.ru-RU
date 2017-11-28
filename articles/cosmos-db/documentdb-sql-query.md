---
title: "SQL-запросы для API DocumentDB в Azure Cosmos DB | Документация Майкрософт"
description: "Сведения о синтаксисе SQL, основных понятиях баз данных и запросах SQL для Azure Cosmos DB. SQL можно использовать в качестве языка запросов JSON в Azure Cosmos DB."
keywords: "синтаксис SQL, запрос SQL, язык запросов JSON, понятия баз данных и запросы SQL, статистические функции"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: a73b4ab3-0786-42fd-b59b-555fce09db6e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: arramac
ms.openlocfilehash: 9b2b5668ef0552485a86f63a120b57c4623bfe35
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="ee6f7-105">SQL-запросы для API DocumentDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ee6f7-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="ee6f7-106">Служба Microsoft Azure Cosmos DB поддерживает запросы документов с помощью SQL (язык структурированных запросов) как языка запросов JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="ee6f7-107">Cosmos DB действительно не имеет схемы.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="ee6f7-108">В силу своей приверженности к модели данных JSON непосредственно внутри ядра СУБД, что обеспечивает автоматическое индексирование документов JSON, не требуя явной схемы или создания вторичных индексов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-108">By virtue of its commitment to the JSON data model directly within the database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="ee6f7-109">При проектировании языка запросов для Cosmos DB перед нами стояло две цели:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-109">While designing the query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="ee6f7-110">Вместо того чтобы изобретать новый язык запросов JSON, мы хотели поддержать SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-110">Instead of inventing a new JSON query language, we wanted to support SQL.</span></span> <span data-ttu-id="ee6f7-111">SQL — это один из самых популярных и хорошо известных языков формирования запросов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-111">SQL is one of the most familiar and popular query languages.</span></span> <span data-ttu-id="ee6f7-112">SQL в Cosmos DB предоставляет формальную модель программирования для выполнения многофункциональных запросов к документам JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="ee6f7-113">Поскольку база данных документов JSON способна выполнять JavaScript непосредственно в ядре базы данных, мы хотели использовать модель программирования JavaScript в качестве основы для нашего языка запросов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-113">As a JSON document database capable of executing JavaScript directly in the database engine, we wanted to use JavaScript's programming model as the foundation for our query language.</span></span> <span data-ttu-id="ee6f7-114">SQL в API DocumentDB основывается на системе типов, вычислении выражений и вызове функций JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-114">The DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="ee6f7-115">Это, в свою очередь, обеспечивает естественную модель программирования для реляционных проекций, иерархической навигации по документам JSON, внутренних соединений, пространственных данных и вызовов определяемых пользователем функций (UDF), написанных полностью на JavaScript, наряду с другими особенностями.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="ee6f7-116">Мы считаем, что эти возможности являются ключевыми для уменьшения рассогласованности между приложением и базой данных и имеют решающее значение для производительности разработчика.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-116">We believe that these capabilities are key to reducing the friction between the application and the database and are crucial for developer productivity.</span></span>

<span data-ttu-id="ee6f7-117">Прежде чем приступить к работе, рекомендуется просмотреть следующий видеоролик, в котором Аравинд Рамачадран (Aravind Ramachandran) демонстрирует возможности использования запросов Cosmos DB, и посетить нашу службу [Query Playground](http://www.documentdb.com/sql/demo), где можно опробовать Cosmos DB в работе и выполнить запросы SQL к нашему набору данных.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-117">We recommend getting started by watching the following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="ee6f7-118">После этого вернитесь к этой статье, где рассматриваем несколько простых документов JSON и команд SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-118">Then, return to this article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="ee6f7-119"><a id="GettingStarted"></a>Приступая к работе с командами SQL в Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ee6f7-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="ee6f7-120">Чтобы увидеть SQL Cosmos DB на деле, мы начнем с нескольких простых JSON документов и пройдемся через некоторые простые запросы к ним.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-120">To see Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="ee6f7-121">Рассмотрим эти два JSON документа о двух семьях.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="ee6f7-122">При работе с Cosmos DB нам не нужно явно создавать никаких схем или вторичных индексов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-122">With Cosmos DB, we do not need to create any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="ee6f7-123">Необходимо просто вставить документы JSON для использования в коллекции Cosmos DB и последующие запросы.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-123">We simply need to insert the JSON documents to a Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="ee6f7-124">Мы имеем простой JSON документ для семейства Андерсен, включая родителей, детей (с домашними животными), адресами и регистрационными данными.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-124">Here we have a simple JSON document for the Andersen family, the parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="ee6f7-125">В документе есть строки, числа, логические значения, массивы и вложенные свойства.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-125">The document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="ee6f7-126">**Документ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-126">**Document**</span></span>  

```JSON
{
  "id": "AndersenFamily",
  "lastName": "Andersen",
  "parents": [
     { "firstName": "Thomas" },
     { "firstName": "Mary Kay"}
  ],
  "children": [
     {
         "firstName": "Henriette Thaulow", 
         "gender": "female", 
         "grade": 5,
         "pets": [{ "givenName": "Fluffy" }]
     }
  ],
  "address": { "state": "WA", "county": "King", "city": "seattle" },
  "creationDate": 1431620472,
  "isRegistered": true
}
```

<span data-ttu-id="ee6f7-127">Это второй документ с одним небольшим различием: `givenName` и `familyName` используются вместо `firstName` и `lastName`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="ee6f7-128">**Документ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-128">**Document**</span></span>  

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

<span data-ttu-id="ee6f7-129">Давайте попробуем сформировать несколько запросов на этом массиве данных, чтобы понять некоторые основные принципы SQL для API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-129">Now let's try a few queries against this data to understand some of the key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="ee6f7-130">Например, следующий запрос вернет документы, в которых поле идентификатора совпадает с `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-130">For example, the following query returns the documents where the id field matches `AndersenFamily`.</span></span> <span data-ttu-id="ee6f7-131">Так как это `SELECT *`, результатом выполнения запроса является сформированный документ JSON:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-131">Since it's a `SELECT *`, the output of the query is the complete JSON document:</span></span>

<span data-ttu-id="ee6f7-132">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ee6f7-133">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-133">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]


<span data-ttu-id="ee6f7-134">Теперь рассмотрим случай, когда нам необходимо переформатировать вывод JSON в другую форму.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-134">Now consider the case where we need to reformat the JSON output in a different shape.</span></span> <span data-ttu-id="ee6f7-135">Этот запрос создает новый объект JSON с двумя выбранными полями, Имя и Город, если название города совпадает с названием штата.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-135">This query projects a new JSON object with two selected fields, Name and City, when the address' city has the same name as the state.</span></span> <span data-ttu-id="ee6f7-136">В этом случае совпадут NY и NY.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="ee6f7-137">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="ee6f7-138">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="ee6f7-139">Следующий запрос возвращает все заданные имена потомков в семействе, идентификатор которого соответствует `WakefieldFamily`, упорядоченному по городу проживания.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-139">The next query returns all the given names of children in the family whose id matches `WakefieldFamily` ordered by the city of residence.</span></span>

<span data-ttu-id="ee6f7-140">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="ee6f7-141">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="ee6f7-142">Мы хотели бы обратить внимание на несколько примечательных аспектов языка запросов Cosmos DB на примерах, которые мы уже рассмотрели:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-142">We would like to draw attention to a few noteworthy aspects of the Cosmos DB query language through the examples we've seen so far:</span></span>  

* <span data-ttu-id="ee6f7-143">В API DocumentDB язык SQL работает со значениями JSON, т. е. имеет дело с сущностями в виде деревьев, а не со строками и столбцами.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="ee6f7-144">Таким образом, язык позволяет обращаться к узлам дерева любой произвольной вложенности, как `Node1.Node2.Node3…..Nodem`, что похоже на реляционный SQL со ссылкой, состоящей из двух частей `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-144">Therefore, the language lets you refer to nodes of the tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar to relational SQL referring to the two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="ee6f7-145">Язык SQL работает с данными без схемы.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-145">The structured query language works with schema-less data.</span></span> <span data-ttu-id="ee6f7-146">Таким образом, система типов должна быть динамически связанной.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-146">Therefore, the type system needs to be bound dynamically.</span></span> <span data-ttu-id="ee6f7-147">Одно и то же выражение может возвращать различные типы на разных документах.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-147">The same expression could yield different types on different documents.</span></span> <span data-ttu-id="ee6f7-148">Результатом запроса является допустимое значение JSON, но оно не обязательно будет иметь фиксированную схему.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-148">The result of a query is a valid JSON value, but is not guaranteed to be of a fixed schema.</span></span>  
* <span data-ttu-id="ee6f7-149">Cosmos DB поддерживает только документы, строго соответствующие JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="ee6f7-150">Это означает, что система типов и выражения могут обрабатывать только типы JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-150">This means the type system and expressions are restricted to deal only with JSON types.</span></span> <span data-ttu-id="ee6f7-151">Дополнительные сведения см. в статье [Спецификации JSON](http://www.json.org/).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-151">Refer to the [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="ee6f7-152">Коллекция Cosmos DB является контейнером документов JSON, не имеющим схемы.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="ee6f7-153">Отношения между сущностями данных внутри документов и между документами в коллекции неявно захвачены сдерживанием, а не базируются на основе отношений между первичными и внешними ключами.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-153">The relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="ee6f7-154">Это является важным аспектом, на котором нужно заострить внимание, в свете внутренних соединений документа, которые будут обсуждаться позже в этой статье.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-154">This is an important aspect worth pointing out in light of the intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="ee6f7-155"><a id="Indexing"></a>Индексирование в Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ee6f7-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="ee6f7-156">Прежде чем мы перейдем к знакомству с синтаксисом SQL в API DocumentDB, стоит рассмотреть принципы индексирования в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-156">Before we get into the DocumentDB API SQL syntax, it is worth exploring the indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="ee6f7-157">Цель индексов базы данных заключается в обслуживании запросов в их различных формах с минимальным потреблением ресурсов (например, процессора, операций ввода-вывода), обеспечивая при этом хорошую пропускную способность и низкие задержки.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-157">The purpose of database indexes is to serve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="ee6f7-158">Часто, чтобы сделать правильный выбор индекса для запроса к базе данных, требуется много планирования и экспериментов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-158">Often, the choice of the right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="ee6f7-159">Такой подход представляет препятствие для баз данных, не имеющих схем, где данные не соответствуют строгим схемам и быстро развиваются.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-159">This approach poses a challenge for schema-less databases where the data doesn’t conform to a strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="ee6f7-160">Поэтому при разработке подсистемы индексирования Cosmos DB перед нами стояли следующие цели.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-160">Therefore, when we designed the Cosmos DB indexing subsystem, we set the following goals:</span></span>

* <span data-ttu-id="ee6f7-161">Индексация документов не должна требовать наличия схемы: подсистема индексации не требует информации о схеме и не делает никаких предположений о схеме документов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-161">Index documents without requiring schema: The indexing subsystem does not require any schema information or make any assumptions about schema of the documents.</span></span> 
* <span data-ttu-id="ee6f7-162">Поддержка эффективных, иерархически развитых и реляционных запросов: индекс эффективно поддерживает язык запросов Cosmos DB, в том числе иерархические и реляционные проекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-162">Support for efficient, rich hierarchical, and relational queries: The index supports the Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="ee6f7-163">Поддержка согласованных запросов при устойчивом объеме записи: в случае высоких нагрузок записи данных с согласованными запросами индекс обновляется постепенно, эффективно и оперативно при устойчивом объеме записи.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, the index is updated incrementally, efficiently, and online in the face of a sustained volume of writes.</span></span> <span data-ttu-id="ee6f7-164">Последовательное обновление индекса имеет решающее значение для удовлетворения запросов с уровнем согласованности, настроенным пользователем для службы документов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-164">The consistent index update is crucial to serve the queries at the consistency level in which the user configured the document service.</span></span>
* <span data-ttu-id="ee6f7-165">Поддержка мультитенантности: учитывая модель резервирования для управления ресурсами для всех клиентов, обновления индекса выполняются в рамках бюджета системных ресурсов (процессор, память и количество операций ввода/вывода в секунду), выделенных на реплики.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-165">Support for multi-tenancy: Given the reservation-based model for resource governance across tenants, index updates are performed within the budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="ee6f7-166">Эффективность хранения: для повышения эффективности затрат накладные расходы дискового пространства при индексировании являются ограниченными и предсказуемыми.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-166">Storage efficiency: For cost effectiveness, the on-disk storage overhead of the index is bounded and predictable.</span></span> <span data-ttu-id="ee6f7-167">Это очень важно, потому что Cosmos DB позволяет разработчику прийти к компромиссу между эффективностью запросов и накладными расходами.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-167">This is crucial because Cosmos DB allows the developer to make cost-based tradeoffs between index overhead in relation to the query performance.</span></span>  

<span data-ttu-id="ee6f7-168">Ознакомьтесь с [примерами Azure Cosmos DB ](https://github.com/Azure/azure-documentdb-net) на веб-сайте MSDN, чтобы увидеть, как настроить политику индексации для коллекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-168">Refer to the [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how to configure the indexing policy for a collection.</span></span> <span data-ttu-id="ee6f7-169">Давайте теперь перейдем к деталям синтаксиса SQL в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-169">Let’s now get into the details of the Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="ee6f7-170"><a id="Basics"></a>Основы использования SQL-запросов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ee6f7-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="ee6f7-171">Каждый запрос состоит из предложения SELECT и необязательных предложений FROM и WHERE в соответствии со стандартами ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="ee6f7-172">Как правило, в каждом запросе источник в предложении FROM является перечислимым.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-172">Typically, for each query, the source in the FROM clause is enumerated.</span></span> <span data-ttu-id="ee6f7-173">Затем к исходному множеству применяется предложение WHERE для извлечения подмножества документов JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-173">Then the filter in the WHERE clause is applied on the source to retrieve a subset of JSON documents.</span></span> <span data-ttu-id="ee6f7-174">И наконец, предложение SELECT используется для проекции запрошенных значений JSON в списке выборки.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-174">Finally, the SELECT clause is used to project the requested JSON values in the select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="ee6f7-175"><a id="FromClause"></a>Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="ee6f7-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="ee6f7-176">Выражение `FROM <from_specification>` является необязательным, если далее в запросе источник не фильтруется и не отображается.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-176">The `FROM <from_specification>` clause is optional unless the source is filtered or projected later in the query.</span></span> <span data-ttu-id="ee6f7-177">Назначение данного выражения заключается в указании источника данных, с которым работает запрос.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-177">The purpose of this clause is to specify the data source upon which the query must operate.</span></span> <span data-ttu-id="ee6f7-178">Как правило, в качестве источника выступает вся коллекция, но можно указать определенное подмножество вместо целой коллекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-178">Commonly the whole collection is the source, but one can specify a subset of the collection instead.</span></span> 

<span data-ttu-id="ee6f7-179">Запрос типа `SELECT * FROM Families` показывает, что вся коллекция Families является источником для перечисления.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-179">A query like `SELECT * FROM Families` indicates that the entire Families collection is the source over which to enumerate.</span></span> <span data-ttu-id="ee6f7-180">Специальный идентификатор ROOT может использоваться для представления коллекции вместо использования имени коллекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-180">A special identifier ROOT can be used to represent the collection instead of using the collection name.</span></span> <span data-ttu-id="ee6f7-181">Следующий список содержит правила, которые применяются для запроса:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-181">The following list contains the rules that are enforced per query:</span></span>

* <span data-ttu-id="ee6f7-182">Коллекция может иметь псевдоним, например `SELECT f.id FROM Families AS f` или просто `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-182">The collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="ee6f7-183">Здесь `f` является эквивалентом `Families`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-183">Here `f` is the equivalent of `Families`.</span></span> <span data-ttu-id="ee6f7-184">`AS` — необязательное ключевое слово для создания псевдонима идентификатора.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-184">`AS` is an optional keyword to alias the identifier.</span></span>
* <span data-ttu-id="ee6f7-185">После создания псевдонима оригинальный источник связывать нельзя.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-185">Once aliased, the original source cannot be bound.</span></span> <span data-ttu-id="ee6f7-186">Например, выражение `SELECT Families.id FROM Families f` является синтаксически неверным, так как идентификатор Families уже не может быть разрешен.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since the identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="ee6f7-187">Все свойства, на которые необходимо ссылаться, должны иметь полное название.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-187">All properties that need to be referenced must be fully qualified.</span></span> <span data-ttu-id="ee6f7-188">В отсутствие строгого следования схеме это реализуется для того, чтобы избежать любых неоднозначных привязок.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-188">In the absence of strict schema adherence, this is enforced to avoid any ambiguous bindings.</span></span> <span data-ttu-id="ee6f7-189">Это значит, что `SELECT id FROM Families f` синтаксически неверен, так как свойство `id` не имеет привязки.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since the property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="ee6f7-190">Вложенные документы</span><span class="sxs-lookup"><span data-stu-id="ee6f7-190">Subdocuments</span></span>
<span data-ttu-id="ee6f7-191">Исходные документы могут быть включены в еще меньшее подмножество.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-191">The source can also be reduced to a smaller subset.</span></span> <span data-ttu-id="ee6f7-192">Например, если нужно перечисление только вложенного дерева в каждом документе, корень вложенного дерева может стать источником, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-192">For instance, to enumerating only a subtree in each document, the subroot could then become the source, as shown in the following example:</span></span>

<span data-ttu-id="ee6f7-193">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="ee6f7-194">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-194">**Results**</span></span>  

    [
      [
        {
            "firstName": "Henriette Thaulow",
            "gender": "female",
            "grade": 5,
            "pets": [
              {
                  "givenName": "Fluffy"
              }
            ]
        }
      ],
      [
        {
            "familyName": "Merriam",
            "givenName": "Jesse",
            "gender": "female",
            "grade": 1
        },
        {
            "familyName": "Miller",
            "givenName": "Lisa",
            "gender": "female",
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="ee6f7-195">Хотя в приведенном выше примере массив используется как источник, объект также может использоваться как источник, как показано в следующем примере: любое допустимое значение JSON (не неопределенное), которое можно найти в источнике, считается включенным в результат запроса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-195">While the above example used an array as the source, an object could also be used as the source, which is what's shown in the following example: Any valid JSON value (not undefined) that can be found in the source is considered for inclusion in the result of the query.</span></span> <span data-ttu-id="ee6f7-196">Если в некоторых семействах отсутствует значение `address.state`, они исключаются из результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-196">If some families don’t have an `address.state` value, they are excluded in the query result.</span></span>

<span data-ttu-id="ee6f7-197">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="ee6f7-198">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="ee6f7-199"><a id="WhereClause"></a>Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="ee6f7-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="ee6f7-200">Предложение WHERE (**`WHERE <filter_condition>`**) не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-200">The WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="ee6f7-201">Оно определяет условие (условия), которым должны удовлетворять исходные документы JSON для того, чтобы быть включенными в результат.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-201">It specifies the condition(s) that the JSON documents provided by the source must satisfy in order to be included as part of the result.</span></span> <span data-ttu-id="ee6f7-202">Любой документ JSON должен при вычислении указанных условий возвращать истинное значение, чтобы быть включенным в результат.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-202">Any JSON document must evaluate the specified conditions to "true" to be considered for the result.</span></span> <span data-ttu-id="ee6f7-203">Выражение WHERE используется слоем индексирования для определения наименьшего подмножества исходных документов, которые могут входить в результат.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-203">The WHERE clause is used by the index layer in order to determine the absolute smallest subset of source documents that can be part of the result.</span></span> 

<span data-ttu-id="ee6f7-204">Следующий запрос запрашивает документы, содержащие имя свойства, значение которого равно `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-204">The following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="ee6f7-205">Все остальные документы, у которых нет свойства имени или в которых значение не соответствует `AndersenFamily`, исключаются.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-205">Any other document that does not have a name property, or where the value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="ee6f7-206">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ee6f7-207">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="ee6f7-208">В предыдущем примере показан простой запрос с условием равенства.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-208">The previous example showed a simple equality query.</span></span> <span data-ttu-id="ee6f7-209">SQL для API DocumentDB также поддерживает различные скалярные выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="ee6f7-210">Наиболее часто используются бинарные и унарные выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-210">The most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="ee6f7-211">Ссылки на свойства исходного объекта JSON также являются допустимыми выражениями.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-211">Property references from the source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="ee6f7-212">В настоящий момент поддерживаются следующие двоичные операторы, они могут быть использованы в запросах, как показано в следующих примерах:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-212">The following binary operators are currently supported and can be used in queries as shown in the following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="ee6f7-213">Арифметические</span><span class="sxs-lookup"><span data-stu-id="ee6f7-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="ee6f7-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="ee6f7-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ee6f7-215">Побитовые</span><span class="sxs-lookup"><span data-stu-id="ee6f7-215">Bitwise</span></span></td>    
<td><span data-ttu-id="ee6f7-216">|, &, ^, <<, >>, >>> (нулевой сдвиг вправо)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ee6f7-217">Логические</span><span class="sxs-lookup"><span data-stu-id="ee6f7-217">Logical</span></span></td>
<td><span data-ttu-id="ee6f7-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="ee6f7-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ee6f7-219">Сравнение</span><span class="sxs-lookup"><span data-stu-id="ee6f7-219">Comparison</span></span></td>    
<td><span data-ttu-id="ee6f7-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="ee6f7-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="ee6f7-221">Строка</span><span class="sxs-lookup"><span data-stu-id="ee6f7-221">String</span></span></td>    
<td><span data-ttu-id="ee6f7-222">|| (конкатенация)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="ee6f7-223">Давайте рассмотрим примеры запросов с двоичными операторами.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="ee6f7-224">Унарные операторы +,-, ~ и NOT также поддерживаются и могут использоваться в запросах, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-224">The unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in the following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="ee6f7-225">Кроме бинарных и унарных операторов, также разрешены ссылки на свойства.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-225">In addition to binary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="ee6f7-226">Например, `SELECT * FROM Families f WHERE f.isRegistered` возвращает документ JSON, содержащий свойство `isRegistered`, значение которого равно значению `true` для JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns the JSON document containing the property `isRegistered` where the property's value is equal to the JSON `true` value.</span></span> <span data-ttu-id="ee6f7-227">Любые другие значения (false, null, не определено, `<number>`, `<string>`, `<object>`, `<array>` и т. д.) приводят к тому, что исходный документ исключается из результата.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads to the source document being excluded from the result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="ee6f7-228">Операторы равенства и сравнения</span><span class="sxs-lookup"><span data-stu-id="ee6f7-228">Equality and comparison operators</span></span>
<span data-ttu-id="ee6f7-229">Ниже приведена таблица, в которой собраны результаты сравнения равенства в SQL для API DocumentDB между любыми двумя типами JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-229">The following table shows the result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="ee6f7-230">
            <strong>Оператор</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ee6f7-231">
            <strong>Не определено</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ee6f7-232">
            <strong>NULL</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ee6f7-233">
            <strong>Логическое значение</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ee6f7-234">
            <strong>Число</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ee6f7-235">
            <strong>Строка</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ee6f7-236">
            <strong>Объект</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="ee6f7-237">
            <strong>Массив</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ee6f7-238">
            <strong>Не определено<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-239">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-240">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-241">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-242">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-243">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-244">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-245">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ee6f7-246">
            <strong>NULL<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-247">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ee6f7-248">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-249">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-250">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-251">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-252">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-253">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ee6f7-254">
            <strong>Логическое значение<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-255">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-256">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ee6f7-257">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-258">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-259">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-260">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-261">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ee6f7-262">
            <strong>Число<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-263">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-264">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-265">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ee6f7-266">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-267">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-268">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-269">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ee6f7-270">
            <strong>Строка<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-271">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-272">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-273">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-274">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ee6f7-275">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-276">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-277">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ee6f7-278">
            <strong>Объект<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-279">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-280">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-281">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-282">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-283">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ee6f7-284">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-285">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="ee6f7-286">
            <strong>Массив<strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="ee6f7-287">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-288">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-289">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-290">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-291">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="ee6f7-292">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="ee6f7-293">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="ee6f7-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="ee6f7-294">Для других операторов сравнения, например >, > =,! =, < и < =, применяются следующие правила.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-294">For other comparison operators such as >, >=, !=, < and <=, the following rules apply:</span></span>   

* <span data-ttu-id="ee6f7-295">Сравнение типов приводит к неопределенному результату.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="ee6f7-296">Сравнение двух объектов или двух массивов приводит к неопределенному результату.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="ee6f7-297">Если результат скалярного выражения в фильтре не определен, соответствующий документ не будет включен в результат, так как значение «не определено» не равно логически значению «истина».</span><span class="sxs-lookup"><span data-stu-id="ee6f7-297">If the result of the scalar expression in the filter is Undefined, the corresponding document would not be included in the result, since Undefined doesn't logically equate to "true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="ee6f7-298">Ключевое слово BETWEEN (МЕЖДУ)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-298">BETWEEN keyword</span></span>
<span data-ttu-id="ee6f7-299">Можно также использовать ключевое слово BETWEEN для выражения запросов к диапазонам значений, как в ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-299">You can also use the BETWEEN keyword to express queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="ee6f7-300">BETWEEN может использоваться для строк или чисел.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="ee6f7-301">Например, этот запрос возвращает все документы семейств, в которых первый ребенок учится в 1-5 классах (оба числа включительно).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-301">For example, this query returns all family documents in which the first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="ee6f7-302">В отличие от ANSI-SQL можно также использовать предложение BETWEEN в предложении FROM, как в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-302">Unlike in ANSI-SQL, you can also use the BETWEEN clause in the FROM clause like in the following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="ee6f7-303">Чтобы сократить время выполнения запросов, не забудьте создать политику индексации, использующую тип индекса диапазона для любых числовых свойств и путей, которые фильтруются в предложении BETWEEN.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-303">For faster query execution times, remember to create an indexing policy that uses a range index type against any numeric properties/paths that are filtered in the BETWEEN clause.</span></span> 

<span data-ttu-id="ee6f7-304">Основное различие между использованием BETWEEN в API DocumentDB и ANSI SQL состоит в том, что можно выражать запросы в диапазоне для свойств различного типа. Например, можно использовать свойство grade (класс) в виде числа (5) в некоторых документах и в виде строк в других (grade4).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-304">The main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="ee6f7-305">В таких случаях, подобно тому, как это происходит в JavaScript, сравнение между результатами двух различных типов в "undefined", а также документ будут пропущены.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and the document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="ee6f7-306">Логические операторы (AND, OR или NOT)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="ee6f7-307">Логические операторы работают над значениями типа Boolean.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="ee6f7-308">Таблицы истинности для данных операторов приведены в следующих таблицах.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-308">The logical truth tables for these operators are shown in the following tables.</span></span>

| <span data-ttu-id="ee6f7-309">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="ee6f7-309">OR</span></span> | <span data-ttu-id="ee6f7-310">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-310">True</span></span> | <span data-ttu-id="ee6f7-311">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-311">False</span></span> | <span data-ttu-id="ee6f7-312">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ee6f7-313">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-313">True</span></span> |<span data-ttu-id="ee6f7-314">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-314">True</span></span> |<span data-ttu-id="ee6f7-315">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-315">True</span></span> |<span data-ttu-id="ee6f7-316">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-316">True</span></span> |
| <span data-ttu-id="ee6f7-317">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-317">False</span></span> |<span data-ttu-id="ee6f7-318">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-318">True</span></span> |<span data-ttu-id="ee6f7-319">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-319">False</span></span> |<span data-ttu-id="ee6f7-320">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-320">Undefined</span></span> |
| <span data-ttu-id="ee6f7-321">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-321">Undefined</span></span> |<span data-ttu-id="ee6f7-322">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-322">True</span></span> |<span data-ttu-id="ee6f7-323">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-323">Undefined</span></span> |<span data-ttu-id="ee6f7-324">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-324">Undefined</span></span> |

| <span data-ttu-id="ee6f7-325">И</span><span class="sxs-lookup"><span data-stu-id="ee6f7-325">AND</span></span> | <span data-ttu-id="ee6f7-326">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-326">True</span></span> | <span data-ttu-id="ee6f7-327">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-327">False</span></span> | <span data-ttu-id="ee6f7-328">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ee6f7-329">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-329">True</span></span> |<span data-ttu-id="ee6f7-330">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-330">True</span></span> |<span data-ttu-id="ee6f7-331">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-331">False</span></span> |<span data-ttu-id="ee6f7-332">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-332">Undefined</span></span> |
| <span data-ttu-id="ee6f7-333">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-333">False</span></span> |<span data-ttu-id="ee6f7-334">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-334">False</span></span> |<span data-ttu-id="ee6f7-335">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-335">False</span></span> |<span data-ttu-id="ee6f7-336">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-336">False</span></span> |
| <span data-ttu-id="ee6f7-337">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-337">Undefined</span></span> |<span data-ttu-id="ee6f7-338">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-338">Undefined</span></span> |<span data-ttu-id="ee6f7-339">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-339">False</span></span> |<span data-ttu-id="ee6f7-340">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-340">Undefined</span></span> |

| <span data-ttu-id="ee6f7-341">НЕ</span><span class="sxs-lookup"><span data-stu-id="ee6f7-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="ee6f7-342">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-342">True</span></span> |<span data-ttu-id="ee6f7-343">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-343">False</span></span> |
| <span data-ttu-id="ee6f7-344">Ложь</span><span class="sxs-lookup"><span data-stu-id="ee6f7-344">False</span></span> |<span data-ttu-id="ee6f7-345">Истина</span><span class="sxs-lookup"><span data-stu-id="ee6f7-345">True</span></span> |
| <span data-ttu-id="ee6f7-346">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-346">Undefined</span></span> |<span data-ttu-id="ee6f7-347">Не определено</span><span class="sxs-lookup"><span data-stu-id="ee6f7-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="ee6f7-348">Ключевое слово IN</span><span class="sxs-lookup"><span data-stu-id="ee6f7-348">IN keyword</span></span>
<span data-ttu-id="ee6f7-349">Ключевое слово IN может использоваться, чтобы проверить, соответствует ли указанное значение любому значению в списке.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-349">The IN keyword can be used to check whether a specified value matches any value in a list.</span></span> <span data-ttu-id="ee6f7-350">Например этот запрос возвращает все документы семейств, где идентификатор равен "WakefieldFamily" или "AndersenFamily".</span><span class="sxs-lookup"><span data-stu-id="ee6f7-350">For example, this query returns all family documents where the id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="ee6f7-351">Этот пример возвращает все документы, поле state которых равно любому из указанных значений.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-351">This example returns all documents where the state is any of the specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="ee6f7-352">Операторы Ternary (?) и Coalesce (??)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="ee6f7-353">Операторы Ternary (тройной) и Coalesce (объединение) могут использоваться для построения условных выражений, аналогичных тем, которые создаются в популярных языках программирования, например C# и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-353">The Ternary and Coalesce operators can be used to build conditional expressions, similar to popular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="ee6f7-354">Оператор Ternary (?) может оказаться очень удобным при создании новых свойств JSON в режиме реального времени.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-354">The Ternary (?) operator can be very handy when constructing new JSON properties on the fly.</span></span> <span data-ttu-id="ee6f7-355">Например, теперь можно писать запросы для классификации уровней класса в удобочитаемой форме, скажем, уровень Beginner/Intermediate/Advanced (начинающий, средний, продвинутый), как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-355">For example, now you can write queries to classify the class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="ee6f7-356">Можно также вложить вызовы операторов, как в следующем запросе.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-356">You can also nest the calls to the operator like in the query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="ee6f7-357">Как и при использовании других операторов запроса, если свойства, на которые имеются ссылки в условных выражениях, отсутствуют в любом документе, или, если сравниваемые типы различны, то указанные документы исключаются из результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-357">As with other query operators, if the referenced properties in the conditional expression are missing in any document, or if the types being compared are different, then those documents are excluded in the query results.</span></span>

<span data-ttu-id="ee6f7-358">Оператор Coalesce (??) может использоваться для выполнения эффективной проверки наличия свойства</span><span class="sxs-lookup"><span data-stu-id="ee6f7-358">The Coalesce (??) operator can be used to efficiently check for the presence of a property (a.k.a.</span></span> <span data-ttu-id="ee6f7-359">(или его определения) в документе.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-359">is defined) in a document.</span></span> <span data-ttu-id="ee6f7-360">Это удобно при запросах к частично структурированным данным или данным разных типов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="ee6f7-361">Например, этот запрос возвращает свойство "lastName" при его наличии или "surname", если оно отсутствует.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-361">For example, this query returns the "lastName" if present, or the "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="ee6f7-362"><a id="EscapingReservedKeywords"></a>Доступ к свойству, заключенному в кавычки</span><span class="sxs-lookup"><span data-stu-id="ee6f7-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="ee6f7-363">Также можно использовать свойства с помощью оператора заключенного в кавычки свойства `[]`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-363">You can also access properties using the quoted property operator `[]`.</span></span> <span data-ttu-id="ee6f7-364">Например, выражение `SELECT c.grade` and `SELECT c["grade"]` являются эквивалентными.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="ee6f7-365">Этот синтаксис полезен, когда необходимо экранировать свойство, которое содержит пробелы, специальные символы или совместно использует имя, совпадающее с именем ключевого слова SQL или зарезервированного слова.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-365">This syntax is useful when you need to escape a property that contains spaces, special characters, or happens to share the same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="ee6f7-366"><a id="SelectClause"></a>Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="ee6f7-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="ee6f7-367">Предложение SELECT (**`SELECT <select_list>`**) является обязательным и определяет, какие значения извлекаются из запроса так же, как и в ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-367">The SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from the query, just like in ANSI-SQL.</span></span> <span data-ttu-id="ee6f7-368">Подмножество, которое было отфильтрован на верхней части исходных документов, передаются на фазе проекции, где указанные значения JSON извлекаются и строится новый объект JSON, на него осуществляется передача для каждого входа.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-368">The subset that's been filtered on top of the source documents are passed onto the projection phase, where the specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="ee6f7-369">Пример ниже иллюстрирует типичный запрос SELECT.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-369">The following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="ee6f7-370">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ee6f7-371">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="ee6f7-372">Вложенные свойства</span><span class="sxs-lookup"><span data-stu-id="ee6f7-372">Nested properties</span></span>
<span data-ttu-id="ee6f7-373">В следующем примере мы отображаем два вложенных свойства — `f.address.state` and `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-373">In the following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="ee6f7-374">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ee6f7-375">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="ee6f7-376">Проекция также поддерживает выражения JSON, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-376">Projection also supports JSON expressions as shown in the following example:</span></span>

<span data-ttu-id="ee6f7-377">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ee6f7-378">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="ee6f7-379">Давайте посмотрим, какую роль играет `$1`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-379">Let's look at the role of `$1` here.</span></span> <span data-ttu-id="ee6f7-380">`SELECT` необходим для создания объекта JSON, и, так как ни один из ключей не предоставлен, мы используем имена неявных переменных аргументов, начиная с `$1`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-380">The `SELECT` clause needs to create a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="ee6f7-381">Например, этот запрос возвращает две неявные переменные аргументов, помеченные как `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="ee6f7-382">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ee6f7-383">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="ee6f7-384">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="ee6f7-384">Aliasing</span></span>
<span data-ttu-id="ee6f7-385">Теперь давайте расширим пример выше с явным использованием псевдонимов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-385">Now let's extend the example above with explicit aliasing of values.</span></span> <span data-ttu-id="ee6f7-386">AS – ключевое слово, используемое для создания псевдонимов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-386">AS is the keyword used for aliasing.</span></span> <span data-ttu-id="ee6f7-387">Оно не является обязательным, как это показано при отображении второго значения в виде `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-387">It's optional as shown while projecting the second value as `NameInfo`.</span></span> 

<span data-ttu-id="ee6f7-388">Если в запросе имеются два свойства с совпадающими именами, то должны использоваться псевдонимы для переименования одного или обоих свойств, чтобы устранить неоднозначность в отображаемом результате.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-388">In case a query has two properties with the same name, aliasing must be used to rename one or both of the properties so that they are disambiguated in the projected result.</span></span>

<span data-ttu-id="ee6f7-389">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ee6f7-390">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="ee6f7-391">Скалярные выражения</span><span class="sxs-lookup"><span data-stu-id="ee6f7-391">Scalar expressions</span></span>
<span data-ttu-id="ee6f7-392">Кроме ссылок на свойства, выражение SELECT также поддерживает скалярные выражения, такие как константы, арифметические выражения, логические выражения и т. д. Например, вот простой запрос "Hello World".</span><span class="sxs-lookup"><span data-stu-id="ee6f7-392">In addition to property references, the SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="ee6f7-393">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="ee6f7-394">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="ee6f7-395">Вот более сложный пример с использованием скалярного выражения:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="ee6f7-396">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="ee6f7-397">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="ee6f7-398">В следующем примере результатом скалярного выражения является логическое.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-398">In the following example, the result of the scalar expression is a Boolean.</span></span>

<span data-ttu-id="ee6f7-399">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="ee6f7-400">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="ee6f7-401">Создание объектов и массивов</span><span class="sxs-lookup"><span data-stu-id="ee6f7-401">Object and array creation</span></span>
<span data-ttu-id="ee6f7-402">Еще одной ключевой возможностью языка SQL для API DocumentDB является создание объектов и массивов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="ee6f7-403">Обратите внимание, что мы создали новый объект JSON в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-403">In the previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="ee6f7-404">Кроме того, можно также создавать массивы, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-404">Similarly, one can also construct arrays as shown in the following examples:</span></span>

<span data-ttu-id="ee6f7-405">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="ee6f7-406">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-406">**Results**</span></span>  

    [
      {
        "CityState": [
          "seattle", 
          "WA"
        ]
      }, 
      {
        "CityState": [
          "NY", 
          "NY"
        ]
      }
    ]

### <span data-ttu-id="ee6f7-407"><a id="ValueKeyword"></a>Ключевое слово VALUE</span><span class="sxs-lookup"><span data-stu-id="ee6f7-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="ee6f7-408">Ключевое слово **VALUE** обеспечивает способ для возврата значения JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-408">The **VALUE** keyword provides a way to return JSON value.</span></span> <span data-ttu-id="ee6f7-409">Например, показанный ниже запрос возвращает скалярное значение `"Hello World"` вместо `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-409">For example, the query shown below returns the scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="ee6f7-410">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="ee6f7-411">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="ee6f7-412">Следующий запрос возвращает значение JSON без метки `"address"` в результатах.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-412">The following query returns the JSON value without the `"address"` label in the results.</span></span>

<span data-ttu-id="ee6f7-413">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="ee6f7-414">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-414">**Results**</span></span>  

    [
      {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }, 
      {
        "state": "NY", 
        "county": "Manhattan", 
        "city": "NY"
      }
    ]

<span data-ttu-id="ee6f7-415">Следующий пример это расширяет, чтобы показать, как вернуть примитивные значения JSON, то есть на конечном уровне дерева JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-415">The following example extends this to show how to return JSON primitive values (the leaf level of the JSON tree).</span></span> 

<span data-ttu-id="ee6f7-416">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="ee6f7-417">**Результат**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="ee6f7-418">Оператор *</span><span class="sxs-lookup"><span data-stu-id="ee6f7-418">* Operator</span></span>
<span data-ttu-id="ee6f7-419">Специальный оператор (*) выводит проект документа в формате "как есть".</span><span class="sxs-lookup"><span data-stu-id="ee6f7-419">The special operator (*) is supported to project the document as-is.</span></span> <span data-ttu-id="ee6f7-420">При его использовании должно быть единственное отображаемое поле.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-420">When used, it must be the only projected field.</span></span> <span data-ttu-id="ee6f7-421">Хотя запрос наподобие `SELECT * FROM Families f` допустим, `SELECT VALUE * FROM Families f ` и `SELECT *, f.id FROM Families f ` недопустимы.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="ee6f7-422">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="ee6f7-423">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-423">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

### <span data-ttu-id="ee6f7-424"><a id="TopKeyword"></a>Оператор TOP</span><span class="sxs-lookup"><span data-stu-id="ee6f7-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="ee6f7-425">Ключевое слово TOP можно использовать для ограничения числа значений, получаемых из запроса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-425">The TOP keyword can be used to limit the number of values from a query.</span></span> <span data-ttu-id="ee6f7-426">Если TOP используется в сочетании с предложением ORDER BY, результирующий набор ограничен первыми N упорядоченными значениями; в противном случае возвращается N первых результатов в неопределенном порядке.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-426">When TOP is used in conjunction with the ORDER BY clause, the result set is limited to the first N number of ordered values; otherwise, it returns the first N number of results in an undefined order.</span></span> <span data-ttu-id="ee6f7-427">В инструкции SELECT рекомендуется всегда использовать предложение ORDER BY с предложением TOP.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with the TOP clause.</span></span> <span data-ttu-id="ee6f7-428">Это единственный способ, который позволяет предсказуемо указать, на какие строки распространяется действие TOP.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-428">This is the only way to predictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="ee6f7-429">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="ee6f7-430">**Результат**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-430">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
           { "firstName": "Thomas" },
           { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "creationDate": 1431620472,
        "isRegistered": true
    }]

<span data-ttu-id="ee6f7-431">TOP можно использовать с постоянным значением (как показано выше) или с переменным значением посредством параметризованных запросов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="ee6f7-432">Дополнительные сведения см. в описании параметризованных запросов ниже.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="ee6f7-433"><a id="Aggregates"></a>Статистические функции</span><span class="sxs-lookup"><span data-stu-id="ee6f7-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="ee6f7-434">Можно также выполнить статистическую обработку в предложении `SELECT`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-434">You can also perform aggregations in the `SELECT` clause.</span></span> <span data-ttu-id="ee6f7-435">Статистические функции выполняют вычисление на наборе значений и возвращают одиночное значение.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="ee6f7-436">Например, следующий запрос возвращает число документов семейств в коллекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-436">For example, the following query returns the count of family documents within the collection.</span></span>

<span data-ttu-id="ee6f7-437">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="ee6f7-438">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="ee6f7-439">Также можно вернуть скалярное значение статического вычисления, используя ключевое слово `VALUE`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-439">You can also return the scalar value of the aggregate by using the `VALUE` keyword.</span></span> <span data-ttu-id="ee6f7-440">Например следующий запрос возвращает число значений как одно число:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-440">For example, the following query returns the count of values as a single number:</span></span>

<span data-ttu-id="ee6f7-441">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="ee6f7-442">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="ee6f7-443">Также можно выполнять статистические вычисления в сочетании с фильтрами.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="ee6f7-444">Например, следующий запрос возвращает число документов с адресом в штате Вашингтон.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-444">For example, the following query returns the count of documents with the address in the state of Washington.</span></span>

<span data-ttu-id="ee6f7-445">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="ee6f7-446">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="ee6f7-447">В указанной ниже таблице представлен список поддерживаемых статистических функций в API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-447">The following table shows the list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="ee6f7-448">`SUM`и `AVG` выполняются над числовыми значениями, тогда как `COUNT`, `MIN` и `MAX` можно выполнять над числами, строками, логическими значениями и значениями NULL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="ee6f7-449">Использование</span><span class="sxs-lookup"><span data-stu-id="ee6f7-449">Usage</span></span> | <span data-ttu-id="ee6f7-450">Описание</span><span class="sxs-lookup"><span data-stu-id="ee6f7-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="ee6f7-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="ee6f7-451">COUNT</span></span> | <span data-ttu-id="ee6f7-452">Возвращает число элементов в выражении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-452">Returns the number of items in the expression.</span></span> |
| <span data-ttu-id="ee6f7-453">SUM</span><span class="sxs-lookup"><span data-stu-id="ee6f7-453">SUM</span></span>   | <span data-ttu-id="ee6f7-454">Возвращает сумму всех элементов в выражении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-454">Returns the sum of all the values in the expression.</span></span> |
| <span data-ttu-id="ee6f7-455">MIN</span><span class="sxs-lookup"><span data-stu-id="ee6f7-455">MIN</span></span>   | <span data-ttu-id="ee6f7-456">Возвращает минимальное значение в выражении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-456">Returns the minimum value in the expression.</span></span> |
| <span data-ttu-id="ee6f7-457">MAX</span><span class="sxs-lookup"><span data-stu-id="ee6f7-457">MAX</span></span>   | <span data-ttu-id="ee6f7-458">Возвращает максимальное значение в выражении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-458">Returns the maximum value in the expression.</span></span> |
| <span data-ttu-id="ee6f7-459">AVG</span><span class="sxs-lookup"><span data-stu-id="ee6f7-459">AVG</span></span>   | <span data-ttu-id="ee6f7-460">Возвращает среднее арифметическое значений в выражении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-460">Returns the average of the values in the expression.</span></span> |

<span data-ttu-id="ee6f7-461">Статистические вычисления также могут быть выполнены над результатом итерации массива.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-461">Aggregates can also be performed over the results of an array iteration.</span></span> <span data-ttu-id="ee6f7-462">Дополнительные сведения см. в разделе [Итерация](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="ee6f7-463">При использовании обозревателя запросов на портале Azure обратите внимание, что статистические запросы могут возвращать частично агрегированные результаты на странице запроса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-463">When using the Azure portal's Query Explorer, note that aggregation queries may return the partially aggregated results over a query page.</span></span> <span data-ttu-id="ee6f7-464">Пакеты SDK создают одно совокупное значение для всех страниц.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-464">The SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="ee6f7-465">Для выполнения статистических запросов с помощью кода, требуется пакет SDK версии 1.12.0 для .NET, пакет SDK версии 1.1.0 для .NET Core или пакет SDK версии 1.9.5 или выше для Java.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-465">In order to perform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="ee6f7-466"><a id="OrderByClause"></a>Предложение ORDER BY</span><span class="sxs-lookup"><span data-stu-id="ee6f7-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="ee6f7-467">Как и в ANSI-SQL, вы можете включить в запрос необязательное предложение ORDER BY.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="ee6f7-468">Предложение может включать необязательный аргумент ASC/DESC, указывающий порядок, в котором должны быть получены результаты.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-468">The clause can include an optional ASC/DESC argument to specify the order in which results must be retrieved.</span></span>

<span data-ttu-id="ee6f7-469">Например, ниже приведен запрос, возвращающий семьи, отсортированные по городу проживания.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-469">For example, here's a query that retrieves families in order of the resident city's name.</span></span>

<span data-ttu-id="ee6f7-470">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="ee6f7-471">**Результат**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-471">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "city": "NY"
      },
      {
        "id": "AndersenFamily",
        "city": "Seattle"    
      }
    ]

<span data-ttu-id="ee6f7-472">А в этом запросе возвращаются семьи, отсортированные по полю даты создания, которое хранится в виде числа и представляет собой время, прошедшее с начала эпохи, т. е. количество секунд, прошедшее с 1 января 1970 года.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing the epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="ee6f7-473">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="ee6f7-474">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-474">**Results**</span></span>

    [
      {
        "id": "WakefieldFamily",
        "creationDate": 1431620462
      },
      {
        "id": "AndersenFamily",
        "creationDate": 1431620472    
      }
    ]

## <span data-ttu-id="ee6f7-475"><a id="Advanced"></a>Дополнительные понятия базы данных и SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="ee6f7-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="ee6f7-476"><a id="Iteration"></a>Итерация</span><span class="sxs-lookup"><span data-stu-id="ee6f7-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="ee6f7-477">Мы добавили новую конструкцию, чтобы обеспечить поддержку перебора массивов JSON с помощью ключевого слова **IN** в SQL для API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-477">A new construct was added via the **IN** keyword in DocumentDB API SQL to provide support for iterating over JSON arrays.</span></span> <span data-ttu-id="ee6f7-478">Исходное выражение FROM поддерживает итерацию.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-478">The FROM source provides support for iteration.</span></span> <span data-ttu-id="ee6f7-479">Начнем с такого примера:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-479">Let's start with the following example:</span></span>

<span data-ttu-id="ee6f7-480">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="ee6f7-481">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-481">**Results**</span></span>  

    [
      [
        {
          "firstName": "Henriette Thaulow", 
          "gender": "female", 
          "grade": 5, 
          "pets": [{ "givenName": "Fluffy"}]
        }
      ], 
      [
        {
            "familyName": "Merriam", 
            "givenName": "Jesse", 
            "gender": "female", 
            "grade": 1
        }, 
        {
            "familyName": "Miller", 
            "givenName": "Lisa", 
            "gender": "female", 
            "grade": 8
        }
      ]
    ]

<span data-ttu-id="ee6f7-482">Теперь давайте посмотрим на другой запрос, который выполняет итерации над членами коллекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-482">Now let's look at another query that performs iteration over children in the collection.</span></span> <span data-ttu-id="ee6f7-483">Обратите внимание на различия в результирующем массиве.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-483">Note the difference in the output array.</span></span> <span data-ttu-id="ee6f7-484">Этот пример разбивает `children` и собирает результаты в единый массив.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-484">This example splits `children` and flattens the results into a single array.</span></span>  

<span data-ttu-id="ee6f7-485">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="ee6f7-486">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-486">**Results**</span></span>  

    [
      {
          "firstName": "Henriette Thaulow",
          "gender": "female",
          "grade": 5,
          "pets": [{ "givenName": "Fluffy" }]
      },
      {
          "familyName": "Merriam",
          "givenName": "Jesse",
          "gender": "female",
          "grade": 1
      },
      {
          "familyName": "Miller",
          "givenName": "Lisa",
          "gender": "female",
          "grade": 8
      }
    ]

<span data-ttu-id="ee6f7-487">Это можно в дальнейшем использовать для фильтрации каждой конкретной записи массива, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-487">This can be further used to filter on each individual entry of the array as shown in the following example:</span></span>

<span data-ttu-id="ee6f7-488">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="ee6f7-489">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="ee6f7-490">Можно также выполнить статистическую обработку результатов итерации массива.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-490">You can also perform aggregation over the result of array iteration.</span></span> <span data-ttu-id="ee6f7-491">Например, следующий запрос подсчитывает число детей во всех семьях.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-491">For example, the following query counts the number of children among all families.</span></span>

<span data-ttu-id="ee6f7-492">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="ee6f7-493">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="ee6f7-494"><a id="Joins"></a>Соединения</span><span class="sxs-lookup"><span data-stu-id="ee6f7-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="ee6f7-495">В реляционных базах данных возможность соединения таблиц является важной.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-495">In a relational database, the need to join across tables is important.</span></span> <span data-ttu-id="ee6f7-496">Это всего логическое следствие проектирования нормализованных схем.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-496">It's the logical corollary to designing normalized schemas.</span></span> <span data-ttu-id="ee6f7-497">В противоположность этому, API DocumentDB работает с денормализованной моделью данных документов без схемы.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-497">Contrary to this, DocumentDB API deals with the denormalized data model of schema-free documents.</span></span> <span data-ttu-id="ee6f7-498">Это является логическим аналогом «автообъединения».</span><span class="sxs-lookup"><span data-stu-id="ee6f7-498">This is the logical equivalent of a "self-join".</span></span>

<span data-ttu-id="ee6f7-499">Поддерживаемый языком синтаксис: <from_source1> JOIN <from_source2> JOIN... JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-499">The syntax that the language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="ee6f7-500">В целом будет возвращаться набор **N**-кортежей (кортежей, у которых число значений равно **N**).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="ee6f7-501">Каждый кортеж будет иметь значения, полученные путем итерации всех псевдонимов коллекции среди их наборов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="ee6f7-502">Другими словами, это полное векторное произведение множеств, участвующих в соединении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-502">In other words, this is a full cross product of the sets participating in the join.</span></span>

<span data-ttu-id="ee6f7-503">Ниже приведены примеры, иллюстрирующие работу соединений.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-503">The following examples show how the JOIN clause works.</span></span> <span data-ttu-id="ee6f7-504">В приведенном ниже примере результат пуст, так как векторное произведение каждого документа из исходного и пустого множества дает пустое множество.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-504">In the following example, the result is empty since the cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="ee6f7-505">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="ee6f7-506">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="ee6f7-507">В следующем примере показано соединение между корнем документа и подкорнем `children`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-507">In the following example, the join is between the document root and the `children` subroot.</span></span> <span data-ttu-id="ee6f7-508">Это векторное произведение между двумя объектами JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="ee6f7-509">Дочерние элементы этого массива не оказывают влияния в JOIN, так как мы имеем дело с одним корнем, который является массивом дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-509">The fact that children is an array is not effective in the JOIN since we are dealing with a single root that is the children array.</span></span> <span data-ttu-id="ee6f7-510">Отсюда и результат содержит только два результата, так как векторное произведение каждого документа с массивом дает точно только один документ.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-510">Hence the result contains only two results, since the cross product of each document with the array yields exactly only one document.</span></span>

<span data-ttu-id="ee6f7-511">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="ee6f7-512">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="ee6f7-513">Следующий пример является более традиционным присоединением:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-513">The following example shows a more conventional join:</span></span>

<span data-ttu-id="ee6f7-514">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="ee6f7-515">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-515">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]



<span data-ttu-id="ee6f7-516">Прежде всего, следует помнить, что `from_source` из предложения **JOIN** является итератором.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-516">The first thing to note is that the `from_source` of the **JOIN** clause is an iterator.</span></span> <span data-ttu-id="ee6f7-517">В этом случае поток выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-517">So, the flow in this case is as follows:</span></span>  

* <span data-ttu-id="ee6f7-518">Развернуть все дочерние элементы **c** в массиве.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-518">Expand each child element **c** in the array.</span></span>
* <span data-ttu-id="ee6f7-519">Примените векторное произведение корня документа **f** с каждым дочерним элементом **c**, развернутым на первом шаге.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-519">Apply a cross product with the root of the document **f** with each child element **c** that was flattened in the first step.</span></span>
* <span data-ttu-id="ee6f7-520">В конце выполните проецирование только для имени **f** свойства объекта корневого документа.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-520">Finally, project the root object **f** name property alone.</span></span> 

<span data-ttu-id="ee6f7-521">Первый документ (`AndersenFamily`) содержит только один дочерний элемент, так что результирующий набор содержит только один соответствующий этому документу объект.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-521">The first document (`AndersenFamily`) contains only one child element, so the result set contains only a single object corresponding to this document.</span></span> <span data-ttu-id="ee6f7-522">Второй документ (`WakefieldFamily`) имеет два дочерних объекта.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-522">The second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="ee6f7-523">Так, векторное произведение создает отдельный объект для каждого дочернего, в результате получаются два объекта, по одному для каждого дочернего, соответствующего этому документу.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-523">So, the cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding to this document.</span></span> <span data-ttu-id="ee6f7-524">Корневые поля в обоих этих документах будут такими же, как и следовало ожидать при векторном произведении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-524">The root fields in both these documents are the same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="ee6f7-525">Реальное применение соединения заключается в формировании кортежей из векторного произведения в форме, которую отобразить иначе сложно.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-525">The real utility of the JOIN is to form tuples from the cross-product in a shape that's otherwise difficult to project.</span></span> <span data-ttu-id="ee6f7-526">Кроме того, как мы увидим в следующем примере, можно фильтровать сочетания кортежа, что позволяет пользователю выбрать условие, которому удовлетворяют кортежи в целом.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-526">Furthermore, as we see in the example below, you could filter on the combination of a tuple that lets' the user chose a condition satisfied by the tuples overall.</span></span>

<span data-ttu-id="ee6f7-527">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="ee6f7-528">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-528">**Results**</span></span>

    [
      {
        "familyName": "AndersenFamily", 
        "childFirstName": "Henriette Thaulow", 
        "petName": "Fluffy"
      }, 
      {
        "familyName": "WakefieldFamily", 
        "childGivenName": "Jesse", 
        "petName": "Goofy"
      }, 
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]



<span data-ttu-id="ee6f7-529">Этот пример является естественным продолжением предыдущего и выполняет двойное соединение.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-529">This example is a natural extension of the preceding example, and performs a double join.</span></span> <span data-ttu-id="ee6f7-530">Таким образом, перекрестное произведение можно рассматривать как следующий псевдокод:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-530">So, the cross product can be viewed as the following pseudo-code:</span></span>

    for-each(Family f in Families)
    {    
        for-each(Child c in f.children)
        {
            for-each(Pet p in c.pets)
            {
                return (Tuple(f.id AS familyName, 
                  c.givenName AS childGivenName, 
                  c.firstName AS childFirstName,
                  p.givenName AS petName));
            }
        }
    }

<span data-ttu-id="ee6f7-531">`AndersenFamily` имеется один ребенок, у которого один питомец.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="ee6f7-532">Векторное произведение представляет собой одну строку (1\*1\*1) в случае этого семейства.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-532">So, the cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="ee6f7-533">Однако семейство Wakefield включает двух детей, но только у одного ребенка «Джесси» есть питомцы.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="ee6f7-534">У Джесси два питомца.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-534">Jesse has two pets though.</span></span> <span data-ttu-id="ee6f7-535">Векторное произведение представляет собой две строки (1\*1\*2 = 2) в случае этого семейства.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-535">Hence the cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="ee6f7-536">В следующем примере введен дополнительный фильтр по `pet`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-536">In the next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="ee6f7-537">Будут исключены все кортежи, у которых имя питомца не равно «Shadow».</span><span class="sxs-lookup"><span data-stu-id="ee6f7-537">This excludes all the tuples where the pet name is not "Shadow".</span></span> <span data-ttu-id="ee6f7-538">Обратите внимание, что мы можем построить кортежи из массивов, установить фильтр на любой из элементов набора и проецировать любую комбинацию из элементов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-538">Notice that we are able to build tuples from arrays, filter on any of the elements of the tuple, and project any combination of the elements.</span></span> 

<span data-ttu-id="ee6f7-539">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="ee6f7-540">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="ee6f7-541"><a id="JavaScriptIntegration"></a>Интеграция JavaScript</span><span class="sxs-lookup"><span data-stu-id="ee6f7-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="ee6f7-542">Azure Cosmos DB обеспечивает модель программирования для реализации логики приложения на основе JavaScript непосредственно в коллекциях в виде хранимых процедур и триггеров.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="ee6f7-543">Это позволяет:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-543">This allows for both:</span></span>

* <span data-ttu-id="ee6f7-544">Получить возможность создания высокопроизводительных транзакционных CRUD и запросов к документам в коллекции благодаря глубокой интеграции среды выполнения JavaScript непосредственно в базы данных.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-544">Ability to do high-performance transactional CRUD operations and queries against documents in a collection by virtue of the deep integration of JavaScript runtime directly within the database engine.</span></span> 
* <span data-ttu-id="ee6f7-545">Добиться естественного моделирования потока управления, областей видимости переменных, присвоения и интеграции обработки исключений примитивов с транзакциями базы данных.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="ee6f7-546">Дополнительные сведения о поддержке Azure Cosmos DB для интеграции JavaScript см. в документации по программированию для серверного JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer to the JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="ee6f7-547"><a id="UserDefinedFunctions"></a>Определяемые пользователем функции (UDF)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="ee6f7-548">Наряду с уже указанными в статье типами SQL API DocumentDB обеспечивает поддержку пользовательских функций.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-548">Along with the types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="ee6f7-549">В частности, поддерживаются скалярные пользовательские функции, где разработчики могут передавать или ни одного, или несколько аргументов и получить один результат.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-549">In particular, scalar UDFs are supported where the developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="ee6f7-550">Каждый из этих аргументов проверяется на соответствие допустимым значениям JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="ee6f7-551">Синтаксис SQL в API DocumentDB расширяется за счет использования этих определяемых пользователем функций для поддержки настраиваемой логики приложения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-551">The DocumentDB API SQL syntax is extended to support custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="ee6f7-552">Пользовательские функции могут быть зарегистрированы в API DocumentDB, а затем на них можно ссылаться как на часть SQL-запроса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="ee6f7-553">На самом деле пользовательские функции специально предназначены для вызовов из запросов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-553">In fact, the UDFs are exquisitely designed to be invoked by queries.</span></span> <span data-ttu-id="ee6f7-554">Как следствие этого выбора, UDF не имеют доступа к объекту контекста, какой имеется у других типов JavaScript (хранимых процедуры, триггеров).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-554">As a corollary to this choice, UDFs do not have access to the context object which the other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="ee6f7-555">Поскольку запросы выполняются только для чтения, они могут работать как на первичной, так на вторичной репликах.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="ee6f7-556">Поэтому UDF предназначены для работы на вторичных репликах, в отличие от других типов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-556">Therefore, UDFs are designed to run on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="ee6f7-557">Ниже приведен пример того, как UDF могут быть зарегистрированы в базе данных Cosmos DB, специально для коллекции с большим количеством документов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-557">Below is an example of how a UDF can be registered at the Cosmos DB database, specifically under a document collection.</span></span>

       UserDefinedFunction regexMatchUdf = new UserDefinedFunction
       {
           Id = "REGEX_MATCH",
           Body = @"function (input, pattern) { 
                       return input.match(pattern) !== null;
                   };",
       };

       UserDefinedFunction createdUdf = client.CreateUserDefinedFunctionAsync(
           UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
           regexMatchUdf).Result;  

<span data-ttu-id="ee6f7-558">В предыдущем примере создается определяемая пользователем функция с именем `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-558">The preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="ee6f7-559">Она принимает два строковых значения JSON — `input` and `pattern` — и проверяет, совпадает ли значение первого поля с шаблоном, указанным во втором поле, с помощью функции string.match() JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-559">It accepts two JSON string values `input` and `pattern` and checks if the first matches the pattern specified in the second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="ee6f7-560">Теперь мы можем использовать эту определяемую пользователем функцию в запросе в проекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="ee6f7-561">При вызовах внутри запросов определяемые пользователем функции следует дополнять префиксом udf.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-561">UDFs must be qualified with the case-sensitive prefix "udf."</span></span> <span data-ttu-id="ee6f7-562">с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="ee6f7-563">До 17 марта 2015 года компонент Cosmos DB поддерживал вызовы UDF без префикса udf.,</span><span class="sxs-lookup"><span data-stu-id="ee6f7-563">Prior to 3/17/2015, Cosmos DB supported UDF calls without the "udf."</span></span> <span data-ttu-id="ee6f7-564">например SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="ee6f7-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="ee6f7-565">Теперь этот метод выполнения вызовов устарел.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="ee6f7-566">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="ee6f7-567">**Результат**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="ee6f7-568">Определяемая пользователем функция также может быть использована внутри фильтра при условии дополнения префиксом udf.,</span><span class="sxs-lookup"><span data-stu-id="ee6f7-568">The UDF can also be used inside a filter as shown in the example below, also qualified with the "udf."</span></span> <span data-ttu-id="ee6f7-569">как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-569">prefix:</span></span>

<span data-ttu-id="ee6f7-570">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="ee6f7-571">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="ee6f7-572">В сущности, определяемые пользователем функции являются корректными скалярными выражениями и могут быть использованы в проекциях и фильтрах.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="ee6f7-573">Для расширения понимания возможностей пользовательских функций, давайте посмотрим на другой пример с условной логикой:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-573">To expand on the power of UDFs, let's look at another example with conditional logic:</span></span>

       UserDefinedFunction seaLevelUdf = new UserDefinedFunction()
       {
           Id = "SEALEVEL",
           Body = @"function(city) {
                   switch (city) {
                       case 'seattle':
                           return 520;
                       case 'NY':
                           return 410;
                       case 'Chicago':
                           return 673;
                       default:
                           return -1;
                    }"
            };

            UserDefinedFunction createdUdf = await client.CreateUserDefinedFunctionAsync(
                UriFactory.CreateDocumentCollectionUri("testdb", "families"), 
                seaLevelUdf);


<span data-ttu-id="ee6f7-574">Ниже приведен пример осуществления UDF.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-574">Below is an example that exercises the UDF.</span></span>

<span data-ttu-id="ee6f7-575">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="ee6f7-576">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-576">**Results**</span></span>

     [
      {
        "city": "seattle", 
        "seaLevel": 520
      }, 
      {
        "city": "NY", 
        "seaLevel": 410
      }
    ]


<span data-ttu-id="ee6f7-577">Как показывают приведенные выше примеры, определяемые пользователем функции объединяют мощь языка JavaScript и SQL API DocumentDB, чтобы обеспечить богатый программируемый интерфейс для реализации сложной процедурной, условной логики с помощью встроенных возможностей исполнения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-577">As the preceding examples showcase, UDFs integrate the power of JavaScript language with the DocumentDB API SQL to provide a rich programmable interface to do complex procedural, conditional logic with the help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="ee6f7-578">На современном этапе обработки UDF SQL API DocumentDB передает аргументы в определяемые пользователем функции для каждого документа в источнике (выражение WHERE или SELECT).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-578">DocumentDB API SQL provides the arguments to the UDFs for each document in the source at the current stage (WHERE clause or SELECT clause) of processing the UDF.</span></span> <span data-ttu-id="ee6f7-579">Результаты включены в общий поток выполнения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-579">The result is incorporated in the overall execution pipeline seamlessly.</span></span> <span data-ttu-id="ee6f7-580">Если свойства, на которые ссылаются параметры UDF, недоступны в значениях JSON, параметр рассматривается как неопределенный, и, следовательно, вызов UDF полностью пропускается.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-580">If the properties referred to by the UDF parameters are not available in the JSON value, the parameter is considered as undefined and hence the UDF invocation is entirely skipped.</span></span> <span data-ttu-id="ee6f7-581">Аналогично, если результат определяемой пользователем функции не определен, он не включается в результат.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-581">Similarly if the result of the UDF is undefined, it's not included in the result.</span></span> 

<span data-ttu-id="ee6f7-582">Таким образом, определяемые пользователем функции являются отличным средством для реализации сложной бизнес-логики в составе запроса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-582">In summary, UDFs are great tools to do complex business logic as part of the query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="ee6f7-583">Оценивание операторов</span><span class="sxs-lookup"><span data-stu-id="ee6f7-583">Operator evaluation</span></span>
<span data-ttu-id="ee6f7-584">Cosmos DB, в силу того что это база данных JSON, проводит параллели с операторами JavaScript и его оценочной семантикой.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-584">Cosmos DB, by the virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="ee6f7-585">В то время как Cosmos DB старается сохранить семантику JavaScript в плане поддержки JSON, оценка операторов в некоторых случаях не совпадает.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-585">While Cosmos DB tries to preserve JavaScript semantics in terms of JSON support, the operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="ee6f7-586">В SQL API DocumentDB, в отличие от традиционного SQL, типы значений зачастую неизвестны до тех пор, пока значения не будут извлечены из базы данных.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-586">In DocumentDB API SQL, unlike in traditional SQL, the types of values are often not known until the values are retrieved from database.</span></span> <span data-ttu-id="ee6f7-587">Для того чтобы эффективно выполнять запросы, большинство операторов имеют строгие требования к типам.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-587">In order to efficiently execute queries, most of the operators have strict type requirements.</span></span> 

<span data-ttu-id="ee6f7-588">SQL в API DocumentDB не выполняет неявные преобразования, в отличие от JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="ee6f7-589">Например, запрос `SELECT * FROM Person p WHERE p.Age = 21` соответствует документам, которые содержат свойство "Возраст" со значением 21.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="ee6f7-590">Любой документ, свойство "возраст" в котором равно строке "21" или другим вариациям, таким как "021", "21.0", "0021", "00021" и т. д. не будут возвращены.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="ee6f7-591">Это вступает в противоречие с JavaScript, в котором значения строк приведены к цифрам (в зависимости от оператора, например: ==).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-591">This is in contrast to the JavaScript where the string values are implicitly casted to numbers (based on operator, ex: ==).</span></span> <span data-ttu-id="ee6f7-592">Этот выбор имеет решающее значение для эффективного согласования индексов в SQL API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="ee6f7-593">Параметризованные SQL-запросы</span><span class="sxs-lookup"><span data-stu-id="ee6f7-593">Parameterized SQL queries</span></span>
<span data-ttu-id="ee6f7-594">Cosmos DB поддерживает запросы с параметрами, выраженными с помощью привычной нотации @.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-594">Cosmos DB supports queries with parameters expressed with the familiar @ notation.</span></span> <span data-ttu-id="ee6f7-595">Параметризованный SQL обеспечивает надежную обработку и экранирование пользовательского ввода, предотвращая случайное раскрытие данных через внедрение кода SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="ee6f7-596">Например, можно написать запрос, который принимает в качестве параметров фамилию и состояние адреса, а затем выполнить его для различных значений параметров фамилия и состояние адреса на основе ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="ee6f7-597">Этот запрос далее можно отправить в Cosmos DB в качестве параметризованного запроса JSON, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-597">This request can then be sent to Cosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="ee6f7-598">Аргумент для TOP можно задать с помощью параметризованных запросов, например, таких, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-598">The argument to TOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="ee6f7-599">Значениями параметров могут быть любые допустимые JSON (строки, числа, логические значения, значения null, даже массивы или вложенные JSON).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="ee6f7-600">Кроме этого, так как Cosmos DB не имеет схемы, параметры не проверяются на соответствие типам.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="ee6f7-601"><a id="BuiltinFunctions"></a>Встроенные функции</span><span class="sxs-lookup"><span data-stu-id="ee6f7-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="ee6f7-602">Cosmos DB также поддерживает несколько встроенных функций для общих операций, которые можно использовать в запросах как определяемые пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="ee6f7-603">Группа функций</span><span class="sxs-lookup"><span data-stu-id="ee6f7-603">Function group</span></span>          | <span data-ttu-id="ee6f7-604">Операции</span><span class="sxs-lookup"><span data-stu-id="ee6f7-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ee6f7-605">Математические функции</span><span class="sxs-lookup"><span data-stu-id="ee6f7-605">Mathematical functions</span></span>  | <span data-ttu-id="ee6f7-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN и TAN</span><span class="sxs-lookup"><span data-stu-id="ee6f7-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="ee6f7-607">Функции проверки типа</span><span class="sxs-lookup"><span data-stu-id="ee6f7-607">Type checking functions</span></span> | <span data-ttu-id="ee6f7-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED и IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="ee6f7-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="ee6f7-609">Строковые функции</span><span class="sxs-lookup"><span data-stu-id="ee6f7-609">String functions</span></span>        | <span data-ttu-id="ee6f7-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING и UPPER</span><span class="sxs-lookup"><span data-stu-id="ee6f7-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="ee6f7-611">Функции массивов</span><span class="sxs-lookup"><span data-stu-id="ee6f7-611">Array functions</span></span>         | <span data-ttu-id="ee6f7-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH и ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="ee6f7-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="ee6f7-613">Пространственные функции</span><span class="sxs-lookup"><span data-stu-id="ee6f7-613">Spatial functions</span></span>       | <span data-ttu-id="ee6f7-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID и ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="ee6f7-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="ee6f7-615">Если вы сейчас используете определяемую пользователем функцию (UDF), для которой теперь появилась встроенная функция, следует использовать соответствующую встроенную функцию, так как она будет выполняться быстрее и гораздо эффективнее.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use the corresponding built-in function as it is going to be quicker to run and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="ee6f7-616">Математические функции</span><span class="sxs-lookup"><span data-stu-id="ee6f7-616">Mathematical functions</span></span>
<span data-ttu-id="ee6f7-617">Математические функции выполняют вычисление, которое основано на входных значениях, предоставляемых в форме аргументов, и возвращают числовое значение.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-617">The mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="ee6f7-618">Здесь приведен список поддерживаемых встроенных математических функций.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="ee6f7-619">Использование</span><span class="sxs-lookup"><span data-stu-id="ee6f7-619">Usage</span></span> | <span data-ttu-id="ee6f7-620">Описание</span><span class="sxs-lookup"><span data-stu-id="ee6f7-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ee6f7-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="ee6f7-622">Возвращает модуль (положительное значение) указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-622">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="ee6f7-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="ee6f7-624">Возвращает наименьшее целочисленное значение, которое больше или равно указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-624">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| [<span data-ttu-id="ee6f7-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="ee6f7-626">Возвращает наибольшее целочисленное значение, которое меньше или равно указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-626">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| [<span data-ttu-id="ee6f7-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="ee6f7-628">Возвращает значение экспоненты для указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-628">Returns the exponent of the specified numeric expression.</span></span> |
| <span data-ttu-id="ee6f7-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="ee6f7-630">Возвращает натуральный логарифм от указанного числового выражения либо логарифм по заданному основанию</span><span class="sxs-lookup"><span data-stu-id="ee6f7-630">Returns the natural logarithm of the specified numeric expression, or the logarithm using the specified base</span></span> |
| [<span data-ttu-id="ee6f7-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="ee6f7-632">Возвращает десятичный логарифм от указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-632">Returns the base-10 logarithmic value of the specified numeric expression.</span></span> |
| [<span data-ttu-id="ee6f7-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="ee6f7-634">Возвращает числовое значение, округленное до ближайшего целого значения в большую сторону.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-634">Returns a numeric value, rounded to the closest integer value.</span></span> |
| [<span data-ttu-id="ee6f7-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="ee6f7-636">Возвращает числовое значение, округленное до ближайшего целого значения в меньшую сторону.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-636">Returns a numeric value, truncated to the closest integer value.</span></span> |
| [<span data-ttu-id="ee6f7-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="ee6f7-638">Возвращает квадратный корень из указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-638">Returns the square root of the specified numeric expression.</span></span> |
| [<span data-ttu-id="ee6f7-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="ee6f7-640">Возвращает указанное числовое выражение, возведенное в квадрат.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-640">Returns the square of the specified numeric expression.</span></span> |
| [<span data-ttu-id="ee6f7-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="ee6f7-642">Возвращает указанное числовое выражение, возведенное в заданную степень.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-642">Returns the power of the specified numeric expression to the value specified.</span></span> |
| [<span data-ttu-id="ee6f7-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="ee6f7-644">Возвращает значение, обозначающее знак (-1, 0, 1) указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-644">Returns the sign value (-1, 0, 1) of the specified numeric expression.</span></span> |
| [<span data-ttu-id="ee6f7-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="ee6f7-646">Возвращает угол в радианах, косинус которого равен указанному числовому выражению; также называется арккосинусом.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-646">Returns the angle, in radians, whose cosine is the specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="ee6f7-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="ee6f7-648">Возвращает угол в радианах, синус которого равен указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-648">Returns the angle, in radians, whose sine is the specified numeric expression.</span></span> <span data-ttu-id="ee6f7-649">Также называется арксинусом.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="ee6f7-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="ee6f7-651">Возвращает угол в радианах, тангенс которого равен указанному числовому выражению.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-651">Returns the angle, in radians, whose tangent is the specified numeric expression.</span></span> <span data-ttu-id="ee6f7-652">Также называется арктангенсом.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="ee6f7-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="ee6f7-654">Возвращает угол в радианах между положительным направлением оси x и лучом, проведенным из начала координат в точку (y, x), где x и y — значения двух заданных выражений с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-654">Returns the angle, in radians, between the positive x-axis and the ray from the origin to the point (y, x), where x and y are the values of the two specified float expressions.</span></span> |
| [<span data-ttu-id="ee6f7-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="ee6f7-656">Возвращает тригонометрический косинус указанного угла в радианах в указанном выражении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-656">Returns the trigonometric cosine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="ee6f7-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="ee6f7-658">Возвращает тригонометрический котангенс указанного угла в радианах в указанном числовом выражении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-658">Returns the trigonometric cotangent of the specified angle, in radians, in the specified numeric expression.</span></span> |
| [<span data-ttu-id="ee6f7-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="ee6f7-660">Возвращает соответствующее значение угла в градусах для угла, указанного в радианах.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-660">Returns the corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="ee6f7-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="ee6f7-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="ee6f7-662">Возвращает значение константы "пи".</span><span class="sxs-lookup"><span data-stu-id="ee6f7-662">Returns the constant value of PI.</span></span> |
| [<span data-ttu-id="ee6f7-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="ee6f7-664">Возвращает значение угла в радианах для числового значения, указанного в градусах.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="ee6f7-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="ee6f7-666">Возвращает тригонометрический синус заданного угла в радианах для указанного выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-666">Returns the trigonometric sine of the specified angle, in radians, in the specified expression.</span></span> |
| [<span data-ttu-id="ee6f7-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="ee6f7-668">Возвращает тангенс угла для указанного выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-668">Returns the tangent of the input expression, in the specified expression.</span></span> |

<span data-ttu-id="ee6f7-669">Например, теперь можно выполнять запросы следующего вида:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-669">For example, you can now run queries like the following:</span></span>

<span data-ttu-id="ee6f7-670">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="ee6f7-671">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-671">**Results**</span></span>

    [4]

<span data-ttu-id="ee6f7-672">Основное отличие функций Cosmos DB от ANSI SQL заключается в том, что они предназначены для работы с данными, не имеющими схемы или имеющими смешанную схему.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-672">The main difference between Cosmos DB’s functions compared to ANSI SQL is that they are designed to work well with schema-less and mixed schema data.</span></span> <span data-ttu-id="ee6f7-673">Если есть документ, где свойство Size отсутствует или имеет нечисловое значение, например «неизвестно», такой документ будет просто пропущен вместо того, чтобы возвратить ошибку.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-673">For example, if you have a document where the Size property is missing, or has a non-numeric value like “unknown”, then the document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="ee6f7-674">Функции проверки типа</span><span class="sxs-lookup"><span data-stu-id="ee6f7-674">Type checking functions</span></span>
<span data-ttu-id="ee6f7-675">Функции проверки типа позволяют проверять тип выражения в запросах SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-675">The type checking functions allow you to check the type of an expression within SQL queries.</span></span> <span data-ttu-id="ee6f7-676">Функции проверки типа можно использовать для оперативного определения типа свойств в документах, если он представлен переменной или неизвестен.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-676">Type checking functions can be used to determine the type of properties within documents on the fly when it is variable or unknown.</span></span> <span data-ttu-id="ee6f7-677">Здесь приведен список поддерживаемых встроенных функций проверки типа.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="ee6f7-678"><strong>Использование</strong></span><span class="sxs-lookup"><span data-stu-id="ee6f7-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="ee6f7-679"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="ee6f7-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ee6f7-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="ee6f7-681">Возвращает логическое значение, указывающее, является ли значение массивом.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-681">Returns a Boolean indicating if the type of the value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ee6f7-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="ee6f7-683">Возвращает логическое значение, указывающее, является ли значение логическим выражением.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-683">Returns a Boolean indicating if the type of the value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ee6f7-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="ee6f7-685">Возвращает логическое значение, указывающее, имеет ли значение тип NULL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-685">Returns a Boolean indicating if the type of the value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ee6f7-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="ee6f7-687">Возвращает логическое значение, указывающее, является ли значение числом.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-687">Returns a Boolean indicating if the type of the value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ee6f7-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="ee6f7-689">Возвращает логическое значение, указывающее, является ли значение объектом JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-689">Returns a Boolean indicating if the type of the value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ee6f7-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="ee6f7-691">Возвращает логическое значение, указывающее, является ли значение строкой.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-691">Returns a Boolean indicating if the type of the value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ee6f7-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="ee6f7-693">Возвращает логическое значение, указывающее, назначено ли свойству значение.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-693">Returns a Boolean indicating if the property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="ee6f7-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="ee6f7-695">Возвращает логическое значение, указывающее, является ли тип значения строковым, числовым, логическим или null.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-695">Returns a Boolean indicating if the type of the value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="ee6f7-696">С помощью этих функций можно выполнять запросы следующего вида:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-696">Using these functions, you can now run queries like the following:</span></span>

<span data-ttu-id="ee6f7-697">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="ee6f7-698">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="ee6f7-699">Строковые функции</span><span class="sxs-lookup"><span data-stu-id="ee6f7-699">String functions</span></span>
<span data-ttu-id="ee6f7-700">Следующие скалярные функции выполняют операцию над входным строковым значением и возвращают строковое, числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-700">The following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="ee6f7-701">Ниже приведена таблица встроенных строковых функций:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="ee6f7-702">Использование</span><span class="sxs-lookup"><span data-stu-id="ee6f7-702">Usage</span></span> | <span data-ttu-id="ee6f7-703">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ee6f7-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="ee6f7-705">Возвращает число символов указанного строкового выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-705">Returns the number of characters of the specified string expression</span></span> |
| <span data-ttu-id="ee6f7-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="ee6f7-707">Возвращает строку, являющуюся результатом объединения двух или более строковых значений.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-707">Returns a string that is the result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="ee6f7-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="ee6f7-709">Возвращает часть строкового выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="ee6f7-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="ee6f7-711">Возвращает значение логического типа, указывающее, начинается ли первое строковое выражение вторым</span><span class="sxs-lookup"><span data-stu-id="ee6f7-711">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="ee6f7-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="ee6f7-713">Возвращает значение логического типа, указывающее, начинается ли первое строковое выражение вторым</span><span class="sxs-lookup"><span data-stu-id="ee6f7-713">Returns a Boolean indicating whether the first string expression ends with the second</span></span> |
| [<span data-ttu-id="ee6f7-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="ee6f7-715">Возвращает значение логического типа, указывающее, содержит ли первое строковое выражение второе.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-715">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |
| [<span data-ttu-id="ee6f7-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="ee6f7-717">Возвращает начальную позицию первого вхождения второго строкового выражения в первое указанное строковое выражение или –1, если строка не найдена.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-717">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span> |
| [<span data-ttu-id="ee6f7-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="ee6f7-719">Возвращает левую часть строки с указанным количеством символов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-719">Returns the left part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="ee6f7-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="ee6f7-721">Возвращает правую часть строки с указанным количеством символов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-721">Returns the right part of a string with the specified number of characters.</span></span> |
| [<span data-ttu-id="ee6f7-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="ee6f7-723">Возвращает строковое выражение после удаления начальных пробелов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="ee6f7-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="ee6f7-725">Возвращает строковое выражение после усечения всех конечных пробелов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="ee6f7-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="ee6f7-727">Возвращает строковое выражение после преобразования символов верхнего регистра в нижний.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-727">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| [<span data-ttu-id="ee6f7-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="ee6f7-729">Возвращает строковое выражение после преобразования символов нижнего регистра в верхний.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-729">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| [<span data-ttu-id="ee6f7-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="ee6f7-731">Заменяет все вхождения указанного строкового значения другим строковым значением.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="ee6f7-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="ee6f7-733">Повторяет строковое значение указанное число раз.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="ee6f7-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="ee6f7-735">Возвращает обратный порядок строкового значения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-735">Returns the reverse order of a string value.</span></span> |

<span data-ttu-id="ee6f7-736">С помощью этих функций можно выполнять запросы следующего вида:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-736">Using these functions, you can now run queries like the following.</span></span> <span data-ttu-id="ee6f7-737">Например, вот таким образом можно возвратить имя семьи в верхнем регистре:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-737">For example, you can return the family name in uppercase as follows:</span></span>

<span data-ttu-id="ee6f7-738">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="ee6f7-739">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="ee6f7-740">Или объединить строки, как в этом примере:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="ee6f7-741">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="ee6f7-742">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="ee6f7-743">Кроме того, строковые функции можно использовать в предложении WHERE для фильтрации результатов, как это показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-743">String functions can also be used in the WHERE clause to filter results, like in the following example:</span></span>

<span data-ttu-id="ee6f7-744">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="ee6f7-745">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="ee6f7-746">Функции массивов</span><span class="sxs-lookup"><span data-stu-id="ee6f7-746">Array functions</span></span>
<span data-ttu-id="ee6f7-747">Следующие скалярные функции выполняют операцию над входным массивом и возвращают числовое или логическое значение, либо массив.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-747">The following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="ee6f7-748">Ниже приведена таблица встроенных функций над массивом:</span><span class="sxs-lookup"><span data-stu-id="ee6f7-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="ee6f7-749">Использование</span><span class="sxs-lookup"><span data-stu-id="ee6f7-749">Usage</span></span> | <span data-ttu-id="ee6f7-750">Описание</span><span class="sxs-lookup"><span data-stu-id="ee6f7-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ee6f7-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="ee6f7-752">Возвращает число элементов массива, указанного в выражении.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-752">Returns the number of elements of the specified array expression.</span></span> |
| <span data-ttu-id="ee6f7-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="ee6f7-754">Возвращает массив, который является результатом объединения значений двух или более массивов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-754">Returns an array that is the result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="ee6f7-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="ee6f7-756">Возвращает логическое значение, указывающее, содержит ли массив указанное значение.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-756">Returns a Boolean indicating whether the array contains the specified value.</span></span> <span data-ttu-id="ee6f7-757">Можно указать, будет ли сопоставление полным или частичным.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-757">Can specify if the match is full or partial.</span></span> |
| <span data-ttu-id="ee6f7-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="ee6f7-759">Возвращает часть выражения массива.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="ee6f7-760">Функции массивов могут использоваться для обработки массивов в JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-760">Array functions can be used to manipulate arrays within JSON.</span></span> <span data-ttu-id="ee6f7-761">Например, ниже приведен запрос, который возвращает все документы, в котором один из родительских элементов равен "Robin Wakefield".</span><span class="sxs-lookup"><span data-stu-id="ee6f7-761">For example, here's a query that returns all documents where one of the parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="ee6f7-762">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="ee6f7-763">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="ee6f7-764">Можно указать часть фрагмента для сопоставления элементов в массиве.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-764">You can specify a partial fragment for matching elements within the array.</span></span> <span data-ttu-id="ee6f7-765">Следующий запрос находит все родительские элементы, где для параметра `givenName` указано значение `Robin`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-765">The following query finds all parents with the `givenName` of `Robin`.</span></span>

<span data-ttu-id="ee6f7-766">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="ee6f7-767">**Результат**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="ee6f7-768">Вот другой пример, использующий функцию ARRAY_LENGTH для получения числа потомков каждого семейства.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-768">Here's another example that uses ARRAY_LENGTH to get the number of children per family.</span></span>

<span data-ttu-id="ee6f7-769">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="ee6f7-770">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="ee6f7-771">Пространственные функции</span><span class="sxs-lookup"><span data-stu-id="ee6f7-771">Spatial functions</span></span>
<span data-ttu-id="ee6f7-772">Cosmos DB поддерживает следующие встроенные функции Открытого геопространственного консорциума (OGC) для выполнения запросов к геопространственным данным.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-772">Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="ee6f7-773"><strong>Использование</strong></span><span class="sxs-lookup"><span data-stu-id="ee6f7-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="ee6f7-774"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="ee6f7-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="ee6f7-776">Возвращает расстояние между двумя выражениями точек GeoJSON, многоугольников или объектов LineString.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-776">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="ee6f7-778">Возвращает логическое выражение, указывающее, располагается ли первый объект GeoJSON (точка, многоугольник или LineString) внутри второго объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-778">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="ee6f7-780">Возвращает логическое выражение, указывающее, пересекаются ли два объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-780">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="ee6f7-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="ee6f7-782">Возвращает логическое значение, указывающее, является ли действительным выражение GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-782">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ee6f7-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="ee6f7-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="ee6f7-784">Возвращает значение JSON, содержащее логическое значение, указывающее, является ли выражение GeoJSON (точка, многоугольник или LineString) действительным. Если оно является недействительным, то возвращаемое значение также содержит строку с описанием причины.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-784">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="ee6f7-785">Пространственные функции могут использоваться для выполнения запросов близости к пространственным данным.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-785">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="ee6f7-786">Например, ниже приведен запрос, возвращающий все документы семейств, которые находятся в пределах 30 км от заданного расположения, с помощью встроенной функции ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-786">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="ee6f7-787">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="ee6f7-788">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="ee6f7-789">Дополнительные сведения о поддержке геопространственных данных в Cosmos DB см. в статье [Работа с геопространственными данными и данными расположений GeoJSON в Azure Cosmos DB](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="ee6f7-790">Он связывает пространственные функции и синтаксис SQL для Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-790">That wraps up spatial functions, and the SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="ee6f7-791">Теперь давайте рассмотрим схему работы запросов LINQ и их взаимодействие с синтаксисом, который мы уже видели.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-791">Now let's take a look at how LINQ querying works and how it interacts with the syntax we've seen so far.</span></span>

## <span data-ttu-id="ee6f7-792"><a id="Linq"></a>LINQ в SQL API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ee6f7-792"><a id="Linq"></a>LINQ to DocumentDB API SQL</span></span>
<span data-ttu-id="ee6f7-793">LINQ является моделью программирования .NET, которая выражает вычисления в виде запросов потоков объектов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="ee6f7-794">Cosmos DB обеспечивает клиентскую библиотеку для взаимодействия с LINQ путем облегчения преобразования между JSON и объектами .NET и сопоставления подмножества запросов LINQ с запросами Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-794">Cosmos DB provides a client-side library to interface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries to Cosmos DB queries.</span></span> 

<span data-ttu-id="ee6f7-795">На рисунке ниже показана архитектура поддержки запросов LINQ при использовании Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-795">The picture below shows the architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="ee6f7-796">Используя клиент Cosmos DB, разработчики могут создать объект **IQueryable**, который будет направлять запросы к поставщику запросов Cosmos DB, который затем транслирует запросы LINQ в запросы Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-796">Using the Cosmos DB client, developers can create an **IQueryable** object that directly queries the Cosmos DB query provider, which then translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="ee6f7-797">Затем запрос передается на сервер Cosmos DB для получения набора результатов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-797">The query is then passed to the Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="ee6f7-798">Возвращенные результаты десериализуются в поток объектов .NET на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-798">The returned results are deserialized into a stream of .NET objects on the client side.</span></span>

![Архитектура поддержки запросов LINQ с помощью API DocumentDB — синтаксис SQL, язык запросов JSON, основные понятия баз данных и SQL-запросы][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="ee6f7-800">Сопоставление .NET и JSON</span><span class="sxs-lookup"><span data-stu-id="ee6f7-800">.NET and JSON mapping</span></span>
<span data-ttu-id="ee6f7-801">Сопоставление между объектами .NET и документами JSON естественно: каждый член поля данных отображаются на объект JSON, где имя поля отображается на «ключевой» части объекта, а часть «значений» рекурсивно отображается на части значений объекта.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-801">The mapping between .NET objects and JSON documents is natural - each data member field is mapped to a JSON object, where the field name is mapped to the "key" part of the object and the "value" part is recursively mapped to the value part of the object.</span></span> <span data-ttu-id="ee6f7-802">Рассмотрим следующий пример: объект Family (Семья) создан и сопоставлен с документом JSON, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-802">Consider the following example: The Family object created is mapped to the JSON document as shown below.</span></span> <span data-ttu-id="ee6f7-803">И наоборот, документ JSON в свою очередь сопоставлен объекту .NET.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-803">And vice versa, the JSON document is mapped back to a .NET object.</span></span>

<span data-ttu-id="ee6f7-804">**Класс C#**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-804">**C# Class**</span></span>

    public class Family
    {
        [JsonProperty(PropertyName="id")]
        public string Id;
        public Parent[] parents;
        public Child[] children;
        public bool isRegistered;
    };

    public struct Parent
    {
        public string familyName;
        public string givenName;
    };

    public class Child
    {
        public string familyName;
        public string givenName;
        public string gender;
        public int grade;
        public List<Pet> pets;
    };

    public class Pet
    {
        public string givenName;
    };

    public class Address
    {
        public string state;
        public string county;
        public string city;
    };

    // Create a Family object.
    Parent mother = new Parent { familyName= "Wakefield", givenName="Robin" };
    Parent father = new Parent { familyName = "Miller", givenName = "Ben" };
    Child child = new Child { familyName="Merriam", givenName="Jesse", gender="female", grade=1 };
    Pet pet = new Pet { givenName = "Fluffy" };
    Address address = new Address { state = "NY", county = "Manhattan", city = "NY" };
    Family family = new Family { Id = "WakefieldFamily", parents = new Parent [] { mother, father}, children = new Child[] { child }, isRegistered = false };


<span data-ttu-id="ee6f7-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-805">**JSON**</span></span>  

    {
        "id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam", 
                "givenName": "Jesse", 
                "gender": "female", 
                "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            { 
              "familyName": "Miller", 
              "givenName": "Lisa", 
              "gender": "female", 
              "grade": 8 
            }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
    };



### <a name="linq-to-sql-translation"></a><span data-ttu-id="ee6f7-806">Трансляция из LINQ в SQL</span><span class="sxs-lookup"><span data-stu-id="ee6f7-806">LINQ to SQL translation</span></span>
<span data-ttu-id="ee6f7-807">Поставщик запросов Cosmos DB пытается как можно правильнее отобразить соответствие запроса LINQ запросу SQL Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-807">The Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="ee6f7-808">В дальнейшем мы предполагаем, что у читателя имеются базовые знания о LINQ.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-808">In the following description, we assume the reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="ee6f7-809">Во-первых, для системы типов; мы поддерживаем все примитивные типы JSON: числовые типы, логические, строковые и NULL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-809">First, for the type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="ee6f7-810">Поддерживаются только эти типы JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-810">Only these JSON types are supported.</span></span> <span data-ttu-id="ee6f7-811">Поддерживаются следующие скалярные выражения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-811">The following scalar expressions are supported.</span></span>

* <span data-ttu-id="ee6f7-812">Постоянные значения. Включают в себя постоянные значения примитивных типов данных, которые вычисляются на момент.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-812">Constant values – these include constant values of the primitive data types at the time the query is evaluated.</span></span>
* <span data-ttu-id="ee6f7-813">Выражения свойств/индексов массивов. Относятся к свойствам объекта или элемента массива.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-813">Property/array index expressions – these expressions refer to the property of an object or an array element.</span></span>
  
     <span data-ttu-id="ee6f7-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n — это целочисленная переменная</span><span class="sxs-lookup"><span data-stu-id="ee6f7-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="ee6f7-815">Арифметические выражения. К ним относятся общие арифметические выражения на основе численных и логических значений.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="ee6f7-816">Для получения полного списка обратитесь к спецификации SQL, указанной выше.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-816">For the complete list, refer to the SQL specification.</span></span>
  
     <span data-ttu-id="ee6f7-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="ee6f7-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="ee6f7-818">Выражение сравнения строк. Включает сравнение строкового значения с некоторым постоянным строковым значением.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-818">String comparison expression - these include comparing a string value to some constant string value.</span></span>  
  
     <span data-ttu-id="ee6f7-819">mother.familyName == "Smith";    child.givenName == s; //s — это строковая переменная</span><span class="sxs-lookup"><span data-stu-id="ee6f7-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="ee6f7-820">Выражение создания объекта/массива. Возвращают объект комбинированного типа, или анонимного типа, или массив таких объектов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="ee6f7-821">Эти значения могут быть вложенными.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-821">These values can be nested.</span></span>
  
     <span data-ttu-id="ee6f7-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //анонимный тип с двумя полями</span><span class="sxs-lookup"><span data-stu-id="ee6f7-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="ee6f7-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="ee6f7-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="ee6f7-824"><a id="SupportedLinqOperators"></a>Список поддерживаемых операторов LINQ</span><span class="sxs-lookup"><span data-stu-id="ee6f7-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="ee6f7-825">Ниже приведен список поддерживаемых операторов LINQ в поставщике LINQ, входящем в состав пакета SDK .NET DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-825">Here is a list of supported LINQ operators in the LINQ provider included with the DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="ee6f7-826">**Select**: проекции, преобразуются в SQL SELECT, включая создание объектов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-826">**Select**: Projections translate to the SQL SELECT including object construction</span></span>
* <span data-ttu-id="ee6f7-827">**Where**: фильтры преобразовываются в инструкцию SQL WHERE, а также поддерживают преобразование &&, || и !</span><span class="sxs-lookup"><span data-stu-id="ee6f7-827">**Where**: Filters translate to the SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="ee6f7-828">в операторы SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-828">to the SQL operators</span></span>
* <span data-ttu-id="ee6f7-829">**SelectMany**: позволяет выполнять очистку массивов в предложение SQL JOIN.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-829">**SelectMany**: Allows unwinding of arrays to the SQL JOIN clause.</span></span> <span data-ttu-id="ee6f7-830">Может использоваться для вложения выражений или объединения их в цепочку для фильтрации по элементам массива.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-830">Can be used to chain/nest expressions to filter on array elements</span></span>
* <span data-ttu-id="ee6f7-831">**OrderBy и OrderByDescending**: выполняет преобразование в ORDER BY по возрастанию или по убыванию.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-831">**OrderBy and OrderByDescending**: Translates to ORDER BY ascending/descending</span></span>
* <span data-ttu-id="ee6f7-832">Операторы для агрегирования **Count**, **Sum**, **Min**, **Max**, **Average** и их асинхронные эквиваленты **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** и **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="ee6f7-833">**CompareTo**: выполняет преобразование в сравнение диапазонов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-833">**CompareTo**: Translates to range comparisons.</span></span> <span data-ttu-id="ee6f7-834">Обычно используется для строк, так как их нельзя сравнивать в .NET.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="ee6f7-835">**Take**: выполняет преобразование в SQL TOP для ограничения результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-835">**Take**: Translates to the SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="ee6f7-836">**Math Functions**: поддерживает преобразование из Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate платформы .NET в эквивалентные встроенные функции SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="ee6f7-837">**String Functions**: поддерживает преобразование из Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper платформы .NET в эквивалентные встроенные функции SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="ee6f7-838">**Array Functions**: поддерживает преобразование из Concat, Contains и Count платформы .NET в эквивалентные встроенные функции SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="ee6f7-839">**Geospatial Extension Functions**: поддерживает преобразование из Distance, Within, IsValid и IsValidDetailed методов заглушки в эквивалентные встроенные функции SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed to the equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="ee6f7-840">**User Defined Function Extension Function**: поддерживает преобразование из UserDefinedFunctionProvider.Invoke метода заглушки в соответствующую определяемую пользователем функцию.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-840">**User-Defined Function Extension Function**: Supports translation from the stub method UserDefinedFunctionProvider.Invoke to the corresponding user-defined function.</span></span>
* <span data-ttu-id="ee6f7-841">**Miscellaneous**: поддерживает преобразование операторов объединения и условных операторов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-841">**Miscellaneous**: Supports translation of the coalesce and conditional operators.</span></span> <span data-ttu-id="ee6f7-842">Позволяет преобразовать Contains в строку CONTAINS, ARRAY_CONTAINS или SQL IN в зависимости от контекста.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-842">Can translate Contains to String CONTAINS, ARRAY_CONTAINS, or the SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="ee6f7-843">Операторы SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="ee6f7-843">SQL query operators</span></span>
<span data-ttu-id="ee6f7-844">Вот несколько примеров, которые иллюстрируют, как некоторые из стандартных операторов запросов LINQ транслируются в запросы Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-844">Here are some examples that illustrate how some of the standard LINQ query operators are translated down to Cosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="ee6f7-845">Оператор Select</span><span class="sxs-lookup"><span data-stu-id="ee6f7-845">Select Operator</span></span>
<span data-ttu-id="ee6f7-846">Синтаксис: `input.Select(x => f(x))`, где `f` — скалярное выражение.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-846">The syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="ee6f7-847">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="ee6f7-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="ee6f7-849">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="ee6f7-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="ee6f7-851">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="ee6f7-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="ee6f7-853">Оператор SelectMany</span><span class="sxs-lookup"><span data-stu-id="ee6f7-853">SelectMany operator</span></span>
<span data-ttu-id="ee6f7-854">Синтаксис: `input.SelectMany(x => f(x))`, где `f` — скалярное выражение, возвращающее тип коллекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-854">The syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="ee6f7-855">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="ee6f7-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="ee6f7-857">Оператор Where</span><span class="sxs-lookup"><span data-stu-id="ee6f7-857">Where operator</span></span>
<span data-ttu-id="ee6f7-858">Синтаксис: `input.Where(x => f(x))`, где `f` — скалярное выражение, возвращающее логическое значение.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-858">The syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="ee6f7-859">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="ee6f7-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="ee6f7-861">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="ee6f7-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="ee6f7-863">Составные SQL-запросы</span><span class="sxs-lookup"><span data-stu-id="ee6f7-863">Composite SQL queries</span></span>
<span data-ttu-id="ee6f7-864">Вышеуказанные операторы могут комбинироваться, чтобы формировать более расширенные запросы.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-864">The above operators can be composed to form more powerful queries.</span></span> <span data-ttu-id="ee6f7-865">Так как Cosmos DB поддерживает вложенные коллекции, такая композиция может быть либо объединением, либо вложением.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-865">Since Cosmos DB supports nested collections, the composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="ee6f7-866">Объединение</span><span class="sxs-lookup"><span data-stu-id="ee6f7-866">Concatenation</span></span>
<span data-ttu-id="ee6f7-867">Синтаксис: `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-867">The syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="ee6f7-868">Объединенный запрос может начинаться с необязательного запроса `SelectMany`, за которым идет несколько операторов `Select` или `Where`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="ee6f7-869">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="ee6f7-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="ee6f7-871">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="ee6f7-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="ee6f7-873">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="ee6f7-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="ee6f7-875">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="ee6f7-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="ee6f7-877">Вложенные операторы</span><span class="sxs-lookup"><span data-stu-id="ee6f7-877">Nesting</span></span>
<span data-ttu-id="ee6f7-878">Синтаксис: `input.SelectMany(x=>x.Q())`, где Q — оператор `Select`, `SelectMany` или `Where`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-878">The syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="ee6f7-879">Во вложенных запросах внутренний запрос применяется к каждому элементу внешнего отбора.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-879">In a nested query, the inner query is applied to each element of the outer collection.</span></span> <span data-ttu-id="ee6f7-880">Одной из важных особенностей является то, что внутренний запрос может ссылаться на поля элементов во внешней коллекции как к самостоятельно присоединенной.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-880">One important feature is that the inner query can refer to the fields of the elements in the outer collection like self-joins.</span></span>

<span data-ttu-id="ee6f7-881">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="ee6f7-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="ee6f7-883">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="ee6f7-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="ee6f7-885">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="ee6f7-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="ee6f7-887"><a id="ExecutingSqlQueries"></a>Выполнение SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="ee6f7-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="ee6f7-888">Cosmos DB предоставляет ресурсы через REST API, который можно вызвать с помощью любого языка, позволяющего отправлять запросы HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="ee6f7-889">Кроме того, Cosmos DB предлагает программные библиотеки для некоторых популярных языков программирования, таких как NET, Node.js, JavaScript и Python.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="ee6f7-890">Интерфейс REST API и различные библиотеки поддерживают запросы через SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-890">The REST API and the various libraries all support querying through SQL.</span></span> <span data-ttu-id="ee6f7-891">Пакет SDL .NET помимо SQL поддерживает запросы LINQ.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-891">The .NET SDK supports LINQ querying in addition to SQL.</span></span>

<span data-ttu-id="ee6f7-892">Следующие примеры показывают, как создать запрос и выполнить его в учетной записи базы данных Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-892">The following examples show how to create a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="ee6f7-893"><a id="RestAPI"></a>REST API</span><span class="sxs-lookup"><span data-stu-id="ee6f7-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="ee6f7-894">Cosmos DB предлагает простую и открытую модель программирования RESTful поверх HTTP.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="ee6f7-895">Учетные записи баз данных могут быть подготовлены с использованием подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="ee6f7-896">Модель ресурсов Cosmos DB состоит из набора ресурсов в учетной записи базы данных, каждый из которых доступен по логическому постоянному универсальному коду ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-896">The Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="ee6f7-897">Набор ресурсов в данном документе называется каналом.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-897">A set of resources is referred to as a feed in this document.</span></span> <span data-ttu-id="ee6f7-898">Учетная запись базы данных может состоять из набора баз данных, каждая из которых содержит несколько коллекций, каждая из которых, в свою очередь, содержит хранимые процедуры, триггеры, определяемые пользователем функции, документы и соответствующие вложения.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="ee6f7-899">Базовая модель взаимодействия с этими ресурсами осуществляется через команды HTTP GET, PUT, POST и DELETE в их стандартной интерпретации.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-899">The basic interaction model with these resources is through the HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="ee6f7-900">Команда POST используется как для создания ресурса, выполнения хранимой процедуры, так и для выполнения запроса Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-900">The POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="ee6f7-901">Запросы всегда включают только операции чтения без побочных эффектов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="ee6f7-902">Следующие примеры показывают, как сформировать запрос с командой POST для API DocumentDB к коллекции, содержащей два образца документа, которые мы рассматривали ранее.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-902">The following examples show a POST for a DocumentDB API query made against a collection containing the two sample documents we've reviewed so far.</span></span> <span data-ttu-id="ee6f7-903">Запрос имеет простой фильтр по свойству имени JSON.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-903">The query has a simple filter on the JSON name property.</span></span> <span data-ttu-id="ee6f7-904">Обратите внимание на использование `x-ms-documentdb-isquery` и Content-Type — заголовков `application/query+json` для обозначения того, что выполняемая операция является запросом.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-904">Note the use of the `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers to denote that the operation is a query.</span></span>

<span data-ttu-id="ee6f7-905">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-905">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT * FROM Families f WHERE f.id = @familyId",     
        "parameters": [          
            {"name": "@familyId", "value": "AndersenFamily"}         
        ] 
    }


<span data-ttu-id="ee6f7-906">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-906">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 8b4678fa-a947-47d3-8dd3-549a40da6eed
    x-ms-item-count: 1
    x-ms-request-charge: 0.32

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "id":"AndersenFamily",
             "lastName":"Andersen",
             "parents":[  
                {  
                   "firstName":"Thomas"
                },
                {  
                   "firstName":"Mary Kay"
                }
             ],
             "children":[  
                {  
                   "firstName":"Henriette Thaulow",
                   "gender":"female",
                   "grade":5,
                   "pets":[  
                      {  
                         "givenName":"Fluffy"
                      }
                   ]
                }
             ],
             "address":{  
                "state":"WA",
                "county":"King",
                "city":"seattle"
             },
             "_rid":"u1NXANcKogEcAAAAAAAAAA==",
             "_ts":1407691744,
             "_self":"dbs\/u1NXAA==\/colls\/u1NXANcKogE=\/docs\/u1NXANcKogEcAAAAAAAAAA==\/",
             "_etag":"00002b00-0000-0000-0000-53e7abe00000",
             "_attachments":"_attachments\/"
          }
       ],
       "count":1
    }


<span data-ttu-id="ee6f7-907">Второй пример показывает более сложный запрос, который возвращает несколько соединенных результатов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-907">The second example shows a more complex query that returns multiple results from the join.</span></span>

<span data-ttu-id="ee6f7-908">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-908">**Request**</span></span>

    POST https://<REST URI>/docs HTTP/1.1
    ...
    x-ms-documentdb-isquery: True
    Content-Type: application/query+json

    {      
        "query": "SELECT 
                     f.id AS familyName, 
                     c.givenName AS childGivenName, 
                     c.firstName AS childFirstName, 
                     p.givenName AS petName 
                  FROM Families f 
                  JOIN c IN f.children 
                  JOIN p in c.pets",     
        "parameters": [] 
    }


<span data-ttu-id="ee6f7-909">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="ee6f7-909">**Results**</span></span>

    HTTP/1.1 200 Ok
    x-ms-activity-id: 568f34e3-5695-44d3-9b7d-62f8b83e509d
    x-ms-item-count: 1
    x-ms-request-charge: 7.84

    <indented for readability, results highlighted>

    {  
       "_rid":"u1NXANcKogE=",
       "Documents":[  
          {  
             "familyName":"AndersenFamily",
             "childFirstName":"Henriette Thaulow",
             "petName":"Fluffy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Goofy"
          },
          {  
             "familyName":"WakefieldFamily",
             "childGivenName":"Jesse",
             "petName":"Shadow"
          }
       ],
       "count":3
    }


<span data-ttu-id="ee6f7-910">Если результаты запроса не помещаются на одной странице результатов, то API REST возвращает токен продолжения в заголовке ответа `x-ms-continuation-token`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-910">If a query's results cannot fit within a single page of results, then the REST API returns a continuation token through the `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="ee6f7-911">Клиенты могут разбивать результаты на страницы, включая заголовок в последующие результаты.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-911">Clients can paginate results by including the header in subsequent results.</span></span> <span data-ttu-id="ee6f7-912">Количеством результатов на одной странице также можно управлять через число в заголовке `x-ms-max-item-count`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-912">The number of results per page can also be controlled through the `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="ee6f7-913">Если указанный запрос содержит статистическую функцию как `COUNT`, страница запроса может возвращать частично агрегированное значение на странице результатов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-913">If the specified query has an aggregation function like `COUNT`, then the query page may return a partially aggregated value over the page of results.</span></span> <span data-ttu-id="ee6f7-914">Клиенты должны выполнить статистическую обработку второго уровня этих результатов, чтобы получить окончательные результаты, например, сумму чисел, возвращенных на отдельных страницах, для получения общего числа.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-914">The clients must perform a second-level aggregation over these results to produce the final results, for example, sum over the counts returned in the individual pages to return the total count.</span></span>

<span data-ttu-id="ee6f7-915">Для управления политикой согласованности данных используйте заголовок `x-ms-consistency-level`, как во всех запросах API REST.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-915">To manage the data consistency policy for queries, use the `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="ee6f7-916">В целях согласованности сеансов также обязательно нужно вернуть последний заголовок cookie `x-ms-session-token` в запросе.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-916">For session consistency, it is required to also echo the latest `x-ms-session-token` Cookie header in the query request.</span></span> <span data-ttu-id="ee6f7-917">Политика индексации запрашиваемой коллекции может также повлиять на согласованность результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-917">The queried collection's indexing policy can also influence the consistency of query results.</span></span> <span data-ttu-id="ee6f7-918">С настройками политики индексации по умолчанию для коллекций индекс всегда актуален и соответствует содержанию документов, и результаты запроса соответствуют выбранным для этого данным.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-918">With the default indexing policy settings, for collections the index is always current with the document contents and query results match the consistency chosen for data.</span></span> <span data-ttu-id="ee6f7-919">Если задействована политика отложенной индексации, запросы могут возвращать устаревшие результаты.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-919">If the indexing policy is relaxed to Lazy, then queries can return stale results.</span></span> <span data-ttu-id="ee6f7-920">Дополнительные сведения см. в статье [Настраиваемые уровни согласованности данных в Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="ee6f7-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="ee6f7-921">Если настроенная политика индексации в коллекции не поддерживает указанный запрос, сервер Azure Cosmos DB возвращает код ошибки 400 (недопустимый запрос).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-921">If the configured indexing policy on the collection cannot support the specified query, the Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="ee6f7-922">Он возвращается для запросов к путям, сконфигурированным для поиска по значениям хэшей (равенство), а также к путям, явно исключенным из индексации.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="ee6f7-923">Заголовок `x-ms-documentdb-query-enable-scan` можно задать для разрешения запросу проводить сканирование в случае отсутствия индекса.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-923">The `x-ms-documentdb-query-enable-scan` header can be specified to allow the query to perform a scan when an index is not available.</span></span>

<span data-ttu-id="ee6f7-924">Можно получить подробные метрики выполнения запроса, задав заголовку `x-ms-documentdb-populatequerymetrics` значение `True`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header to `True`.</span></span> <span data-ttu-id="ee6f7-925">Дополнительные сведения см. в статье [Tuning query performance with Azure Cosmos DB](documentdb-sql-query-metrics.md) (Настройка производительности запросов с помощью Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="ee6f7-926"><a id="DotNetSdk"></a>Пакет SDK для C# (.NET)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="ee6f7-927">Пакет .NET SDK поддерживает запросы как LINQ, так и SQL.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-927">The .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="ee6f7-928">В следующем примере показано, как выполнить простой фильтр для запроса, сформированного ранее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-928">The following example shows how to perform the simple filter query introduced earlier in this document.</span></span>

    foreach (var family in client.CreateDocumentQuery(collectionLink, 
        "SELECT * FROM Families f WHERE f.id = \"AndersenFamily\""))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    SqlQuerySpec query = new SqlQuerySpec("SELECT * FROM Families f WHERE f.id = @familyId");
    query.Parameters = new SqlParameterCollection();
    query.Parameters.Add(new SqlParameter("@familyId", "AndersenFamily"));

    foreach (var family in client.CreateDocumentQuery(collectionLink, query))
    {
        Console.WriteLine("\tRead {0} from parameterized SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery(collectionLink)
        where f.Id == "AndersenFamily"
        select f))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in client.CreateDocumentQuery(collectionLink)
        .Where(f => f.Id == "AndersenFamily")
        .Select(f => f))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="ee6f7-929">Этот пример сравнивает два свойства на равенство в каждом документе и использует анонимные проекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

    foreach (var family in client.CreateDocumentQuery(collectionLink,
        @"SELECT {""Name"": f.id, ""City"":f.address.city} AS Family 
        FROM Families f 
        WHERE f.address.city = f.address.state"))
    {
        Console.WriteLine("\tRead {0} from SQL", family);
    }

    foreach (var family in (
        from f in client.CreateDocumentQuery<Family>(collectionLink)
        where f.address.city == f.address.state
        select new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ query", family);
    }

    foreach (var family in
        client.CreateDocumentQuery<Family>(collectionLink)
        .Where(f => f.address.city == f.address.state)
        .Select(f => new { Name = f.Id, City = f.address.city }))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", family);
    }


<span data-ttu-id="ee6f7-930">Следующий пример демонстрирует объединение, выражаемое через LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-930">The next sample shows joins, expressed through LINQ SelectMany.</span></span>

    foreach (var pet in client.CreateDocumentQuery(collectionLink,
          @"SELECT p
            FROM Families f 
                 JOIN c IN f.children 
                 JOIN p in c.pets 
            WHERE p.givenName = ""Shadow"""))
    {
        Console.WriteLine("\tRead {0} from SQL", pet);
    }

    // Equivalent in Lambda expressions
    foreach (var pet in
        client.CreateDocumentQuery<Family>(collectionLink)
        .SelectMany(f => f.children)
        .SelectMany(c => c.pets)
        .Where(p => p.givenName == "Shadow"))
    {
        Console.WriteLine("\tRead {0} from LINQ lambda", pet);
    }



<span data-ttu-id="ee6f7-931">Клиент .NET автоматически перебирает все страницы результатов запроса в блоках FOREACH, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-931">The .NET client automatically iterates through all the pages of query results in the foreach blocks as shown above.</span></span> <span data-ttu-id="ee6f7-932">Параметры запроса, введенные в разделе API REST, также доступны в пакете SDK для .NET с помощью классов `FeedOptions` и `FeedResponse` в методе CreateDocumentQuery.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-932">The query options introduced in the REST API section are also available in the .NET SDK using the `FeedOptions` and `FeedResponse` classes in the CreateDocumentQuery method.</span></span> <span data-ttu-id="ee6f7-933">Количеством страниц можно управлять через настройку `MaxItemCount`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-933">The number of pages can be controlled using the `MaxItemCount` setting.</span></span> 

<span data-ttu-id="ee6f7-934">Можно также явно управлять разбиением на страницы, создав `IDocumentQueryable` с помощью объекта `IQueryable`, а затем считывая значения ` ResponseContinuationToken` и передавая их обратно как `RequestContinuationToken` в `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-934">You can also explicitly control paging by creating `IDocumentQueryable` using the `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="ee6f7-935">`EnableScanInQuery` можно настроить на включение сканирования, когда подобный запрос не поддерживается настроенной политикой индексации.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-935">`EnableScanInQuery` can be set to enable scans when the query cannot be supported by the configured indexing policy.</span></span> <span data-ttu-id="ee6f7-936">При работе с секционированными коллекциями можно использовать `PartitionKey` для выполнения запроса к одной секции (хотя Cosmos DB может автоматически извлекать этот ключ из текста запроса) и `EnableCrossPartitionQuery` для выполнения запросов к нескольким секциям.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-936">For partitioned collections, you can use `PartitionKey` to run the query against a single partition (though Cosmos DB can automatically extract this from the query text), and `EnableCrossPartitionQuery` to run queries that may need to be run against multiple partitions.</span></span> 

<span data-ttu-id="ee6f7-937">В разделе с [примерами .NET для Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) имеются дополнительные примеры, содержащие запросы.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-937">Refer to [Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="ee6f7-938"><a id="JavaScriptServerSideApi"></a>Интерфейс API для серверного JavaScript</span><span class="sxs-lookup"><span data-stu-id="ee6f7-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="ee6f7-939">Cosmos DB обеспечивает модель программирования для реализации логики приложения на основе JavaScript непосредственно в коллекциях, используя хранимые процедуры и триггеры.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on the collections using stored procedures and triggers.</span></span> <span data-ttu-id="ee6f7-940">Логика JavaScript регистрируется на уровне коллекции, может выполнять операции в базе данных над документами указанной коллекции.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-940">The JavaScript logic registered at a collection level can then issue database operations on the operations on the documents of the given collection.</span></span> <span data-ttu-id="ee6f7-941">Эти операции оборачиваются транзакциями ACID.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="ee6f7-942">В следующем примере показано, как использовать queryDocuments в интерфейсе API JavaScript для сервера, чтобы выполнять запросы из хранимых процедур и триггеров.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-942">The following example shows how to use the queryDocuments in the JavaScript server API to make queries from inside stored procedures and triggers.</span></span>

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            { name: name, author: author },
            function (err, documentCreated) {
                if (err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function (err, matchingDocuments) {
                        if (err) throw new Error(err.message);
    context.getResponse().setBody(matchingDocuments.length);

                        // Replace the author name for all documents that satisfied the query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need to execute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="ee6f7-943"><a id="References"></a>Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="ee6f7-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="ee6f7-944">[Знакомство со службой Azure Cosmos DB. API DocumentDB][introduction]</span><span class="sxs-lookup"><span data-stu-id="ee6f7-944">[Introduction to Azure Cosmos DB][introduction]</span></span>
2. <span data-ttu-id="ee6f7-945">[DocumentDB SQL Syntax](http://go.microsoft.com/fwlink/p/?LinkID=510612) (Синтаксис SQL в DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-945">[Azure Cosmos DB SQL specification](http://go.microsoft.com/fwlink/p/?LinkID=510612)</span></span>
3. [<span data-ttu-id="ee6f7-946">Примеры .NET для Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ee6f7-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="ee6f7-947">[Настраиваемые уровни согласованности данных в Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="ee6f7-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="ee6f7-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="ee6f7-949">JSON — [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="ee6f7-950">Спецификация JavaScript — [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="ee6f7-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="ee6f7-952">Методика вычисления запросов для больших баз данных — [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="ee6f7-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="ee6f7-953">Обработка запросов в параллельных реляционных СУБД (Query Processing in Parallel Relational Database Systems), IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="ee6f7-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="ee6f7-954">Lu, Ooi, Tan, Обработка запросов в параллельных реляционных СУБД (Query Processing in Parallel Relational Database Systems), IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="ee6f7-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="ee6f7-955">Кристофер Олстон (Christopher Olston), Бенджамин Рид (Benjamin Reed), Аткарш Сривастава (Utkarsh Srivastava), Рави Камар (Ravi Kumar), Эндрю Томкинс (Andrew Tomkins): Язык Pig. Не такой уж и незнакомый язык для обработки данных (Pig Latin: A Not-So-Foreign Language for Data Processing), SIGMOD 2008 г.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="ee6f7-956">Ж.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-956">G.</span></span> <span data-ttu-id="ee6f7-957">Графе (G. Graefe).</span><span class="sxs-lookup"><span data-stu-id="ee6f7-957">Graefe.</span></span> <span data-ttu-id="ee6f7-958">Каскадные платформы для оптимизации запросов.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-958">The Cascades framework for query optimization.</span></span> <span data-ttu-id="ee6f7-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-959">IEEE Data Eng.</span></span> <span data-ttu-id="ee6f7-960">Bull., 18(3): 1995 г.</span><span class="sxs-lookup"><span data-stu-id="ee6f7-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md