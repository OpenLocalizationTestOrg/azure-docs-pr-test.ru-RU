---
title: "aaaSQL запрашивает Azure Cosmos DB DocumentDB API | Документы Microsoft"
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
ms.openlocfilehash: f4db95b87f5796c4e4299aaf016435cb6301bbfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-queries-for-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="5729c-105">SQL-запросы для API DocumentDB в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5729c-105">SQL queries for Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="5729c-106">Служба Microsoft Azure Cosmos DB поддерживает запросы документов с помощью SQL (язык структурированных запросов) как языка запросов JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-106">Microsoft Azure Cosmos DB supports querying documents using SQL (Structured Query Language) as a JSON query language.</span></span> <span data-ttu-id="5729c-107">Cosmos DB действительно не имеет схемы.</span><span class="sxs-lookup"><span data-stu-id="5729c-107">Cosmos DB is truly schema-free.</span></span> <span data-ttu-id="5729c-108">Посредством его обязательств toohello JSON модели данных непосредственно в компонент database engine hello он обеспечивает автоматическое индексирование документов JSON не требуя явной схемы или создания вторичных индексов.</span><span class="sxs-lookup"><span data-stu-id="5729c-108">By virtue of its commitment toohello JSON data model directly within hello database engine, it provides automatic indexing of JSON documents without requiring explicit schema or creation of secondary indexes.</span></span> 

<span data-ttu-id="5729c-109">При проектировании Cosmos DB hello язык запросов, мы должны были в уме две цели:</span><span class="sxs-lookup"><span data-stu-id="5729c-109">While designing hello query language for Cosmos DB, we had two goals in mind:</span></span>

* <span data-ttu-id="5729c-110">Вместо изобретать новый язык запросов JSON, нам необходимо было toosupport SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-110">Instead of inventing a new JSON query language, we wanted toosupport SQL.</span></span> <span data-ttu-id="5729c-111">SQL является одним из языков запросов наиболее знакомых и популярных hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-111">SQL is one of hello most familiar and popular query languages.</span></span> <span data-ttu-id="5729c-112">SQL в Cosmos DB предоставляет формальную модель программирования для выполнения многофункциональных запросов к документам JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-112">Cosmos DB SQL provides a formal programming model for rich queries over JSON documents.</span></span>
* <span data-ttu-id="5729c-113">Как JSON документа база данных может выполнять JavaScript непосредственно в ядре СУБД hello нам необходимо было модель программирования toouse JavaScript как hello foundation нашей языка запросов.</span><span class="sxs-lookup"><span data-stu-id="5729c-113">As a JSON document database capable of executing JavaScript directly in hello database engine, we wanted toouse JavaScript's programming model as hello foundation for our query language.</span></span> <span data-ttu-id="5729c-114">Hello DocumentDB API SQL заключена в системе типов языка JavaScript, вычисление выражений и вызова функции.</span><span class="sxs-lookup"><span data-stu-id="5729c-114">hello DocumentDB API SQL is rooted in JavaScript's type system, expression evaluation, and function invocation.</span></span> <span data-ttu-id="5729c-115">Это, в свою очередь, обеспечивает естественную модель программирования для реляционных проекций, иерархической навигации по документам JSON, внутренних соединений, пространственных данных и вызовов определяемых пользователем функций (UDF), написанных полностью на JavaScript, наряду с другими особенностями.</span><span class="sxs-lookup"><span data-stu-id="5729c-115">This in-turn provides a natural programming model for relational projections, hierarchical navigation across JSON documents, self joins, spatial queries, and invocation of user-defined functions (UDFs) written entirely in JavaScript, among other features.</span></span> 

<span data-ttu-id="5729c-116">Мы надеемся, что эти возможности являются трения hello ключа tooreducing между приложения hello и hello базы данных и особенно важны для повышения производительности разработчиков.</span><span class="sxs-lookup"><span data-stu-id="5729c-116">We believe that these capabilities are key tooreducing hello friction between hello application and hello database and are crucial for developer productivity.</span></span>

<span data-ttu-id="5729c-117">Мы рекомендуем Приступая к работе, посмотрите следующие видео, где Aravind Ramachandran показывает Cosmos DB возможности выполнения запросов, hello и, посетив нашей [площадку запросов](http://www.documentdb.com/sql/demo), где можно опробовать Cosmos DB и выполнения запросов SQL к наш набор данных.</span><span class="sxs-lookup"><span data-stu-id="5729c-117">We recommend getting started by watching hello following video, where Aravind Ramachandran shows Cosmos DB's querying capabilities, and by visiting our [Query Playground](http://www.documentdb.com/sql/demo), where you can try out Cosmos DB and run SQL queries against our dataset.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/DataExposedQueryingDocumentDB/player]
> 
> 

<span data-ttu-id="5729c-118">После этого вернитесь toothis статьи, где мы начнем с учебник запроса SQL, в котором рассматриваются некоторые простые документы JSON и команды SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-118">Then, return toothis article, where we start with a SQL query tutorial that walks you through some simple JSON documents and SQL commands.</span></span>

## <span data-ttu-id="5729c-119"><a id="GettingStarted"></a>Приступая к работе с командами SQL в Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5729c-119"><a id="GettingStarted"></a>Getting started with SQL commands in Cosmos DB</span></span>
<span data-ttu-id="5729c-120">toosee Cosmos SQL базы данных на работы, давайте начинаются с несколько простых документов JSON и показывает, как некоторые простые запросы.</span><span class="sxs-lookup"><span data-stu-id="5729c-120">toosee Cosmos DB SQL at work, let's begin with a few simple JSON documents and walk through some simple queries against it.</span></span> <span data-ttu-id="5729c-121">Рассмотрим эти два JSON документа о двух семьях.</span><span class="sxs-lookup"><span data-stu-id="5729c-121">Consider these two JSON documents about two families.</span></span> <span data-ttu-id="5729c-122">С помощью Cosmos DB не должны toocreate любой схемы или вторичных индексов явным образом.</span><span class="sxs-lookup"><span data-stu-id="5729c-122">With Cosmos DB, we do not need toocreate any schemas or secondary indices explicitly.</span></span> <span data-ttu-id="5729c-123">Мы просто tooinsert hello JSON документы tooa Cosmos DB коллекции и впоследствии запросов.</span><span class="sxs-lookup"><span data-stu-id="5729c-123">We simply need tooinsert hello JSON documents tooa Cosmos DB collection and subsequently query.</span></span> <span data-ttu-id="5729c-124">Здесь у нас есть простая JSON документов для семейства Андерсен hello, hello родительских, дочерних (и их животных), адрес и сведения о регистрации.</span><span class="sxs-lookup"><span data-stu-id="5729c-124">Here we have a simple JSON document for hello Andersen family, hello parents, children (and their pets), address, and registration information.</span></span> <span data-ttu-id="5729c-125">Hello документ имеет строки, числа, логические значения, массивы и вложенных свойств.</span><span class="sxs-lookup"><span data-stu-id="5729c-125">hello document has strings, numbers, Booleans, arrays, and nested properties.</span></span> 

<span data-ttu-id="5729c-126">**Документ**</span><span class="sxs-lookup"><span data-stu-id="5729c-126">**Document**</span></span>  

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

<span data-ttu-id="5729c-127">Это второй документ с одним небольшим различием: `givenName` и `familyName` используются вместо `firstName` и `lastName`.</span><span class="sxs-lookup"><span data-stu-id="5729c-127">Here's a second document with one subtle difference – `givenName` and `familyName` are used instead of `firstName` and `lastName`.</span></span>

<span data-ttu-id="5729c-128">**Документ**</span><span class="sxs-lookup"><span data-stu-id="5729c-128">**Document**</span></span>  

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

<span data-ttu-id="5729c-129">Теперь попробуем несколько запросов от этого toounderstand данных некоторые hello ключевые аспекты DocumentDB API SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-129">Now let's try a few queries against this data toounderstand some of hello key aspects of DocumentDB API SQL.</span></span> <span data-ttu-id="5729c-130">Например, hello следующий запрос возвращает документы hello которых соответствует поле id hello `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="5729c-130">For example, hello following query returns hello documents where hello id field matches `AndersenFamily`.</span></span> <span data-ttu-id="5729c-131">Так как она является `SELECT *`, hello выходные данные запроса hello: hello полный документ JSON:</span><span class="sxs-lookup"><span data-stu-id="5729c-131">Since it's a `SELECT *`, hello output of hello query is hello complete JSON document:</span></span>

<span data-ttu-id="5729c-132">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-132">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="5729c-133">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-133">**Results**</span></span>

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


<span data-ttu-id="5729c-134">Теперь рассмотрим случай hello, где мы должны tooreformat hello выходных данных JSON в другой форме.</span><span class="sxs-lookup"><span data-stu-id="5729c-134">Now consider hello case where we need tooreformat hello JSON output in a different shape.</span></span> <span data-ttu-id="5729c-135">Этот запрос, проекты новый JSON объекта с двумя выбранные поля Name и City, когда hello адрес Город hello одинаковые имена, как состояние hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-135">This query projects a new JSON object with two selected fields, Name and City, when hello address' city has hello same name as hello state.</span></span> <span data-ttu-id="5729c-136">В этом случае совпадут NY и NY.</span><span class="sxs-lookup"><span data-stu-id="5729c-136">In this case, "NY, NY" matches.</span></span>

<span data-ttu-id="5729c-137">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-137">**Query**</span></span>    

    SELECT {"Name":f.id, "City":f.address.city} AS Family 
    FROM Families f 
    WHERE f.address.city = f.address.state

<span data-ttu-id="5729c-138">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-138">**Results**</span></span>

    [{
        "Family": {
            "Name": "WakefieldFamily", 
            "City": "NY"
        }
    }]


<span data-ttu-id="5729c-139">Hello следующий запрос возвращает все имена заданным hello дочерних элементов в hello семейства, идентификатор которого соответствует `WakefieldFamily` упорядоченные по hello города проживания.</span><span class="sxs-lookup"><span data-stu-id="5729c-139">hello next query returns all hello given names of children in hello family whose id matches `WakefieldFamily` ordered by hello city of residence.</span></span>

<span data-ttu-id="5729c-140">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-140">**Query**</span></span>

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.address.city ASC

<span data-ttu-id="5729c-141">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-141">**Results**</span></span>

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


<span data-ttu-id="5729c-142">Мы хотели бы tooa внимания toodraw мало внимания аспектов hello Cosmos DB языка hello примеров, которые мы видели в данный момент запросов:</span><span class="sxs-lookup"><span data-stu-id="5729c-142">We would like toodraw attention tooa few noteworthy aspects of hello Cosmos DB query language through hello examples we've seen so far:</span></span>  

* <span data-ttu-id="5729c-143">В API DocumentDB язык SQL работает со значениями JSON, т. е. имеет дело с сущностями в виде деревьев, а не со строками и столбцами.</span><span class="sxs-lookup"><span data-stu-id="5729c-143">Since DocumentDB API SQL works on JSON values, it deals with tree shaped entities instead of rows and columns.</span></span> <span data-ttu-id="5729c-144">Таким образом, hello языка позволяет ссылаться toonodes дерева hello любой произвольной глубины, таких как `Node1.Node2.Node3…..Nodem`, аналогичные toorelational SQL обращения toohello две ссылки на компонент из `<table>.<column>`.</span><span class="sxs-lookup"><span data-stu-id="5729c-144">Therefore, hello language lets you refer toonodes of hello tree at any arbitrary depth, like `Node1.Node2.Node3…..Nodem`, similar toorelational SQL referring toohello two part reference of `<table>.<column>`.</span></span>   
* <span data-ttu-id="5729c-145">Hello структуру языка запрос будет работать с данными без схемы.</span><span class="sxs-lookup"><span data-stu-id="5729c-145">hello structured query language works with schema-less data.</span></span> <span data-ttu-id="5729c-146">Таким образом, динамически hello границы toobe требованиям системы типа.</span><span class="sxs-lookup"><span data-stu-id="5729c-146">Therefore, hello type system needs toobe bound dynamically.</span></span> <span data-ttu-id="5729c-147">Hello того же выражения может дать различных типов в различных документах.</span><span class="sxs-lookup"><span data-stu-id="5729c-147">hello same expression could yield different types on different documents.</span></span> <span data-ttu-id="5729c-148">Hello результатом запроса является допустимым значением JSON, но не гарантируется, что toobe фиксированной схемы.</span><span class="sxs-lookup"><span data-stu-id="5729c-148">hello result of a query is a valid JSON value, but is not guaranteed toobe of a fixed schema.</span></span>  
* <span data-ttu-id="5729c-149">Cosmos DB поддерживает только документы, строго соответствующие JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-149">Cosmos DB only supports strict JSON documents.</span></span> <span data-ttu-id="5729c-150">Это означает, что система типов hello и выражения являются ограниченными toodeal только с типами JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-150">This means hello type system and expressions are restricted toodeal only with JSON types.</span></span> <span data-ttu-id="5729c-151">См. toohello [спецификации JSON](http://www.json.org/) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="5729c-151">Refer toohello [JSON specification](http://www.json.org/) for more details.</span></span>  
* <span data-ttu-id="5729c-152">Коллекция Cosmos DB является контейнером документов JSON, не имеющим схемы.</span><span class="sxs-lookup"><span data-stu-id="5729c-152">A Cosmos DB collection is a schema-free container of JSON documents.</span></span> <span data-ttu-id="5729c-153">Hello связи в данных сущности в одной и нескольких документов в коллекции регистрируются неявно путем включения, а не первичного ключа и внешнего ключа связи.</span><span class="sxs-lookup"><span data-stu-id="5729c-153">hello relations in data entities within and across documents in a collection are implicitly captured by containment and not by primary key and foreign key relations.</span></span> <span data-ttu-id="5729c-154">Это важный аспект стоит обратить внимание в свете hello соединения внутри документа, описанных далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="5729c-154">This is an important aspect worth pointing out in light of hello intra-document joins discussed later in this article.</span></span>

## <span data-ttu-id="5729c-155"><a id="Indexing"></a>Индексирование в Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5729c-155"><a id="Indexing"></a> Cosmos DB indexing</span></span>
<span data-ttu-id="5729c-156">Прежде чем мы перейдем hello синтаксис DocumentDB API SQL, стоит изучение hello индексирования конструктора в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5729c-156">Before we get into hello DocumentDB API SQL syntax, it is worth exploring hello indexing design in Cosmos DB.</span></span> 

<span data-ttu-id="5729c-157">Hello индексов базы данных предназначено tooserve запросов в различных форм и фигур с потреблением ресурсов минимальное (например, ЦП и ввода вывода) то же время предоставляя высокой пропускной способности и низкой задержкой.</span><span class="sxs-lookup"><span data-stu-id="5729c-157">hello purpose of database indexes is tooserve queries in their various forms and shapes with minimum resource consumption (like CPU and input/output) while providing good throughput and low latency.</span></span> <span data-ttu-id="5729c-158">Часто Выбор hello hello правой индекса для запросов к базе данных требует много планирования и экспериментов.</span><span class="sxs-lookup"><span data-stu-id="5729c-158">Often, hello choice of hello right index for querying a database requires much planning and experimentation.</span></span> <span data-ttu-id="5729c-159">Этот подход возникают сложности для баз данных без схемы, где hello данные не соответствуют tooa strict схемы и развития быстро.</span><span class="sxs-lookup"><span data-stu-id="5729c-159">This approach poses a challenge for schema-less databases where hello data doesn’t conform tooa strict schema and evolves rapidly.</span></span> 

<span data-ttu-id="5729c-160">Таким образом когда мы разработали hello Cosmos DB индексирования подсистемы, задается hello следующих целей:</span><span class="sxs-lookup"><span data-stu-id="5729c-160">Therefore, when we designed hello Cosmos DB indexing subsystem, we set hello following goals:</span></span>

* <span data-ttu-id="5729c-161">Индексировать документы без необходимости схемы: hello индексирования подсистемы требует информации о схеме, и не делать никаких предположений о схеме hello документов.</span><span class="sxs-lookup"><span data-stu-id="5729c-161">Index documents without requiring schema: hello indexing subsystem does not require any schema information or make any assumptions about schema of hello documents.</span></span> 
* <span data-ttu-id="5729c-162">Поддержка для эффективных и многофункциональных иерархических и реляционных запросов: hello индексы поддерживают язык запросов Cosmos DB hello эффективно, включая поддержку иерархических и реляционные проекции.</span><span class="sxs-lookup"><span data-stu-id="5729c-162">Support for efficient, rich hierarchical, and relational queries: hello index supports hello Cosmos DB query language efficiently, including support for hierarchical and relational projections.</span></span>
* <span data-ttu-id="5729c-163">Поддержка согласованное запросов на длительной объем операций записи: для высокого уровня записи пропускная способность рабочих нагрузок с согласованной запросами hello индекс обновляется постепенно, эффективно и через Интернет в лицевой стороны hello тома длительной операции записи.</span><span class="sxs-lookup"><span data-stu-id="5729c-163">Support for consistent queries in face of a sustained volume of writes: For high write throughput workloads with consistent queries, hello index is updated incrementally, efficiently, and online in hello face of a sustained volume of writes.</span></span> <span data-ttu-id="5729c-164">Обновление согласованное индекса Hello является ключевым tooserve hello запросы на уровне согласованности hello в какой hello пользователя настроен hello документа службы.</span><span class="sxs-lookup"><span data-stu-id="5729c-164">hello consistent index update is crucial tooserve hello queries at hello consistency level in which hello user configured hello document service.</span></span>
* <span data-ttu-id="5729c-165">Поддержка мультитенантности: задано модель на основе резервирования hello регулирование ресурсов клиентов, в пределах бюджета hello системных ресурсов (ЦП, памяти и операций ввода вывода в секунду) в реплике, выделенных выполняется обновление индекса.</span><span class="sxs-lookup"><span data-stu-id="5729c-165">Support for multi-tenancy: Given hello reservation-based model for resource governance across tenants, index updates are performed within hello budget of system resources (CPU, memory, and input/output operations per second) allocated per replica.</span></span> 
* <span data-ttu-id="5729c-166">Эффективность хранения: для экономической эффективности hello хранилище на диске издержки hello индекса является связанной и прогнозируемого.</span><span class="sxs-lookup"><span data-stu-id="5729c-166">Storage efficiency: For cost effectiveness, hello on-disk storage overhead of hello index is bounded and predictable.</span></span> <span data-ttu-id="5729c-167">Это важно, поскольку Cosmos DB допускает hello разработчика toomake основанный на стоимости компромисса между затраты на индекса производительности запроса toohello отношения.</span><span class="sxs-lookup"><span data-stu-id="5729c-167">This is crucial because Cosmos DB allows hello developer toomake cost-based tradeoffs between index overhead in relation toohello query performance.</span></span>  

<span data-ttu-id="5729c-168">См. toohello [примеров Azure Cosmos DB](https://github.com/Azure/azure-documentdb-net) в MSDN для образцов, показывающий, каким образом tooconfigure hello политики индексирования для коллекции.</span><span class="sxs-lookup"><span data-stu-id="5729c-168">Refer toohello [Azure Cosmos DB samples](https://github.com/Azure/azure-documentdb-net) on MSDN for samples showing how tooconfigure hello indexing policy for a collection.</span></span> <span data-ttu-id="5729c-169">Теперь давайте hello Дополнительные сведения о hello синтаксис SQL базы данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5729c-169">Let’s now get into hello details of hello Azure Cosmos DB SQL syntax.</span></span>

## <span data-ttu-id="5729c-170"><a id="Basics"></a>Основы использования SQL-запросов Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5729c-170"><a id="Basics"></a>Basics of an Azure Cosmos DB SQL query</span></span>
<span data-ttu-id="5729c-171">Каждый запрос состоит из предложения SELECT и необязательных предложений FROM и WHERE в соответствии со стандартами ANSI-SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-171">Every query consists of a SELECT clause and optional FROM and WHERE clauses per ANSI-SQL standards.</span></span> <span data-ttu-id="5729c-172">Как правило для каждого запроса перечисляется hello источника в предложении FROM hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-172">Typically, for each query, hello source in hello FROM clause is enumerated.</span></span> <span data-ttu-id="5729c-173">После этого hello фильтрацию в предложение WHERE применяется на tooretrieve источника hello hello подмножество документов JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-173">Then hello filter in hello WHERE clause is applied on hello source tooretrieve a subset of JSON documents.</span></span> <span data-ttu-id="5729c-174">Наконец, используется предложение SELECT hello tooproject hello запрошенный список выбора значения JSON в hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-174">Finally, hello SELECT clause is used tooproject hello requested JSON values in hello select list.</span></span>

    SELECT <select_list> 
    [FROM <from_specification>] 
    [WHERE <filter_condition>]
    [ORDER BY <sort_specification]    


## <span data-ttu-id="5729c-175"><a id="FromClause"></a>Предложение FROM</span><span class="sxs-lookup"><span data-stu-id="5729c-175"><a id="FromClause"></a>FROM clause</span></span>
<span data-ttu-id="5729c-176">Hello `FROM <from_specification>` предложение является необязательным, если источник hello отфильтрованы или спроецировать позже в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-176">hello `FROM <from_specification>` clause is optional unless hello source is filtered or projected later in hello query.</span></span> <span data-ttu-id="5729c-177">Hello это предложение предназначено источника данных toospecify hello, после которого hello запрос должен работать.</span><span class="sxs-lookup"><span data-stu-id="5729c-177">hello purpose of this clause is toospecify hello data source upon which hello query must operate.</span></span> <span data-ttu-id="5729c-178">Часто вся коллекция hello является источником hello, но один вместо этого указать подмножество hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="5729c-178">Commonly hello whole collection is hello source, but one can specify a subset of hello collection instead.</span></span> 

<span data-ttu-id="5729c-179">Запрос, например `SELECT * FROM Families` указывает, hello всего семейства коллекция источника hello через какие tooenumerate.</span><span class="sxs-lookup"><span data-stu-id="5729c-179">A query like `SELECT * FROM Families` indicates that hello entire Families collection is hello source over which tooenumerate.</span></span> <span data-ttu-id="5729c-180">Специальный идентификатор КОРНЕВОГО может представлять коллекцию hello используется toorepresent вместо использования имени коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-180">A special identifier ROOT can be used toorepresent hello collection instead of using hello collection name.</span></span> <span data-ttu-id="5729c-181">Hello следующий список содержит hello правила, которые применяются для каждого запроса.</span><span class="sxs-lookup"><span data-stu-id="5729c-181">hello following list contains hello rules that are enforced per query:</span></span>

* <span data-ttu-id="5729c-182">Hello коллекции может быть присвоен псевдоним, таких как `SELECT f.id FROM Families AS f` или просто `SELECT f.id FROM Families f`.</span><span class="sxs-lookup"><span data-stu-id="5729c-182">hello collection can be aliased, such as `SELECT f.id FROM Families AS f` or simply `SELECT f.id FROM Families f`.</span></span> <span data-ttu-id="5729c-183">Здесь `f` является эквивалентом hello `Families`.</span><span class="sxs-lookup"><span data-stu-id="5729c-183">Here `f` is hello equivalent of `Families`.</span></span> <span data-ttu-id="5729c-184">`AS`является идентификатором hello tooalias Необязательное ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="5729c-184">`AS` is an optional keyword tooalias hello identifier.</span></span>
* <span data-ttu-id="5729c-185">Один раз псевдоним hello исходный источник не может быть привязана.</span><span class="sxs-lookup"><span data-stu-id="5729c-185">Once aliased, hello original source cannot be bound.</span></span> <span data-ttu-id="5729c-186">Например `SELECT Families.id FROM Families f` является синтаксически недопустимым, поскольку не удается разрешить больше hello идентификатор «Семейства».</span><span class="sxs-lookup"><span data-stu-id="5729c-186">For example, `SELECT Families.id FROM Families f` is syntactically invalid since hello identifier "Families" cannot be resolved anymore.</span></span>
* <span data-ttu-id="5729c-187">Все свойства, которые требуется ссылка на toobe должно быть полным.</span><span class="sxs-lookup"><span data-stu-id="5729c-187">All properties that need toobe referenced must be fully qualified.</span></span> <span data-ttu-id="5729c-188">В отсутствие hello схемы строгого соответствия, это принудительная tooavoid неоднозначных привязок.</span><span class="sxs-lookup"><span data-stu-id="5729c-188">In hello absence of strict schema adherence, this is enforced tooavoid any ambiguous bindings.</span></span> <span data-ttu-id="5729c-189">Таким образом `SELECT id FROM Families f` является синтаксически недопустимый с момента hello свойство `id` не привязан.</span><span class="sxs-lookup"><span data-stu-id="5729c-189">Therefore, `SELECT id FROM Families f` is syntactically invalid since hello property `id` is not bound.</span></span>

### <a name="subdocuments"></a><span data-ttu-id="5729c-190">Вложенные документы</span><span class="sxs-lookup"><span data-stu-id="5729c-190">Subdocuments</span></span>
<span data-ttu-id="5729c-191">Источник Hello также может быть более ограниченной tooa ограниченный набор.</span><span class="sxs-lookup"><span data-stu-id="5729c-191">hello source can also be reduced tooa smaller subset.</span></span> <span data-ttu-id="5729c-192">Для экземпляра tooenumerating поддерево в каждом документе hello subroot затем станут hello источника, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="5729c-192">For instance, tooenumerating only a subtree in each document, hello subroot could then become hello source, as shown in hello following example:</span></span>

<span data-ttu-id="5729c-193">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-193">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="5729c-194">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-194">**Results**</span></span>  

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

<span data-ttu-id="5729c-195">Хотя hello в приведенном выше примере массив используется как источник hello, объект также может использоваться в качестве источника hello, которым элементы, отображаемые в следующий пример hello: для включения в результат hello считается любым допустимым значением JSON (не определено), можно найти в источнике hello запрос Hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-195">While hello above example used an array as hello source, an object could also be used as hello source, which is what's shown in hello following example: Any valid JSON value (not undefined) that can be found in hello source is considered for inclusion in hello result of hello query.</span></span> <span data-ttu-id="5729c-196">Если у вас нет некоторые семейства `address.state` значения, они исключаются из результата запроса hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-196">If some families don’t have an `address.state` value, they are excluded in hello query result.</span></span>

<span data-ttu-id="5729c-197">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-197">**Query**</span></span>

    SELECT * 
    FROM Families.address.state

<span data-ttu-id="5729c-198">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-198">**Results**</span></span>

    [
      "WA", 
      "NY"
    ]


## <span data-ttu-id="5729c-199"><a id="WhereClause"></a>Предложение WHERE</span><span class="sxs-lookup"><span data-stu-id="5729c-199"><a id="WhereClause"></a>WHERE clause</span></span>
<span data-ttu-id="5729c-200">Здравствуйте, предложение WHERE (**`WHERE <filter_condition>`**) является необязательным.</span><span class="sxs-lookup"><span data-stu-id="5729c-200">hello WHERE clause (**`WHERE <filter_condition>`**) is optional.</span></span> <span data-ttu-id="5729c-201">Он указывает, что hello условия, которым документы JSON hello hello источника должны удовлетворять в порядке toobe включается как часть результата hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-201">It specifies hello condition(s) that hello JSON documents provided by hello source must satisfy in order toobe included as part of hello result.</span></span> <span data-ttu-id="5729c-202">Любой документ JSON должно быть указано hello условия слишком «true» toobe рассматриваться в качестве результата hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-202">Any JSON document must evaluate hello specified conditions too"true" toobe considered for hello result.</span></span> <span data-ttu-id="5729c-203">Здравствуйте, ГДЕ используется предложение hello уровне индекса в порядке toodetermine hello абсолютный наименьшее подмножество исходных документов, которые могут быть частью результирующего hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-203">hello WHERE clause is used by hello index layer in order toodetermine hello absolute smallest subset of source documents that can be part of hello result.</span></span> 

<span data-ttu-id="5729c-204">Hello следующий запрос запрашивает документы, содержащие имя свойства, значение которого является `AndersenFamily`.</span><span class="sxs-lookup"><span data-stu-id="5729c-204">hello following query requests documents that contain a name property whose value is `AndersenFamily`.</span></span> <span data-ttu-id="5729c-205">Любой другой документ, у которого нет свойства name, или где hello значение не соответствует `AndersenFamily` исключается.</span><span class="sxs-lookup"><span data-stu-id="5729c-205">Any other document that does not have a name property, or where hello value does not match `AndersenFamily` is excluded.</span></span> 

<span data-ttu-id="5729c-206">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-206">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="5729c-207">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-207">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


<span data-ttu-id="5729c-208">Hello предыдущем примере показан запрос простого равенства.</span><span class="sxs-lookup"><span data-stu-id="5729c-208">hello previous example showed a simple equality query.</span></span> <span data-ttu-id="5729c-209">SQL для API DocumentDB также поддерживает различные скалярные выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-209">DocumentDB API SQL also supports a variety of scalar expressions.</span></span> <span data-ttu-id="5729c-210">наиболее часто используемые Hello — это двоичное кодирование и унарные выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-210">hello most commonly used are binary and unary expressions.</span></span> <span data-ttu-id="5729c-211">Ссылки на свойства из объекта JSON источника hello также являются допустимыми выражениями.</span><span class="sxs-lookup"><span data-stu-id="5729c-211">Property references from hello source JSON object are also valid expressions.</span></span> 

<span data-ttu-id="5729c-212">Следующие бинарные операторы Hello в настоящее время поддерживаются и могут использоваться в запросах, как показано в следующих примерах hello:</span><span class="sxs-lookup"><span data-stu-id="5729c-212">hello following binary operators are currently supported and can be used in queries as shown in hello following examples:</span></span>  

<table>
<tr>
<td><span data-ttu-id="5729c-213">Арифметические</span><span class="sxs-lookup"><span data-stu-id="5729c-213">Arithmetic</span></span></td>    
<td><span data-ttu-id="5729c-214">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="5729c-214">+,-,*,/,%</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5729c-215">Побитовые</span><span class="sxs-lookup"><span data-stu-id="5729c-215">Bitwise</span></span></td>    
<td><span data-ttu-id="5729c-216">|, &, ^, <<, >>, >>> (нулевой сдвиг вправо)</span><span class="sxs-lookup"><span data-stu-id="5729c-216">|, &, ^, <<, >>, >>> (zero-fill right shift)</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5729c-217">Логические</span><span class="sxs-lookup"><span data-stu-id="5729c-217">Logical</span></span></td>
<td><span data-ttu-id="5729c-218">AND, OR, NOT</span><span class="sxs-lookup"><span data-stu-id="5729c-218">AND, OR, NOT</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5729c-219">Сравнение</span><span class="sxs-lookup"><span data-stu-id="5729c-219">Comparison</span></span></td>    
<td><span data-ttu-id="5729c-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span><span class="sxs-lookup"><span data-stu-id="5729c-220">=, !=, &lt;, &gt;, &lt;=, &gt;=, <></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="5729c-221">Строка</span><span class="sxs-lookup"><span data-stu-id="5729c-221">String</span></span></td>    
<td><span data-ttu-id="5729c-222">|| (конкатенация)</span><span class="sxs-lookup"><span data-stu-id="5729c-222">|| (concatenate)</span></span></td>
</tr>
</table>  


<span data-ttu-id="5729c-223">Давайте рассмотрим примеры запросов с двоичными операторами.</span><span class="sxs-lookup"><span data-stu-id="5729c-223">Let’s take a look at some queries using binary operators.</span></span>

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade % 2 = 1     -- matching grades == 5, 1

    SELECT * 
    FROM Families.children[0] c
    WHERE c.grade ^ 4 = 1    -- matching grades == 5

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade >= 5     -- matching grades == 5


<span data-ttu-id="5729c-224">Здравствуйте, унарные операторы +,-, ~ не поддерживаются также и может использоваться в запросах, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="5729c-224">hello unary operators +,-, ~ and NOT are also supported, and can be used inside queries as shown in hello following example:</span></span>

    SELECT *
    FROM Families.children[0] c
    WHERE NOT(c.grade = 5)  -- matching grades == 1

    SELECT *
    FROM Families.children[0] c
    WHERE (-c.grade = -5)  -- matching grades == 5



<span data-ttu-id="5729c-225">В дополнение к этому toobinary и унарные операторы, ссылки на свойства также можно использовать.</span><span class="sxs-lookup"><span data-stu-id="5729c-225">In addition toobinary and unary operators, property references are also allowed.</span></span> <span data-ttu-id="5729c-226">Например `SELECT * FROM Families f WHERE f.isRegistered` возвращает hello документ JSON, содержащий свойства hello `isRegistered` которого значение свойства hello равно toohello JSON `true` значение.</span><span class="sxs-lookup"><span data-stu-id="5729c-226">For example, `SELECT * FROM Families f WHERE f.isRegistered` returns hello JSON document containing hello property `isRegistered` where hello property's value is equal toohello JSON `true` value.</span></span> <span data-ttu-id="5729c-227">Любые другие значения (false, значение null, определено, `<number>`, `<string>`, `<object>`, `<array>`и т.д.) ведет toohello исходного документа, исключенного из результата hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-227">Any other values (false, null, Undefined, `<number>`, `<string>`, `<object>`, `<array>`, etc.) leads toohello source document being excluded from hello result.</span></span> 

### <a name="equality-and-comparison-operators"></a><span data-ttu-id="5729c-228">Операторы равенства и сравнения</span><span class="sxs-lookup"><span data-stu-id="5729c-228">Equality and comparison operators</span></span>
<span data-ttu-id="5729c-229">Hello приведенной ниже таблице показано hello результат сравнения на равенство в DocumentDB API SQL любые два типа JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-229">hello following table shows hello result of equality comparisons in DocumentDB API SQL between any two JSON types.</span></span>

<table style = "width:300px">
   <tbody>
      <tr>
         <td valign="top"><span data-ttu-id="5729c-230">
            <strong>Оператор</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-230">
            <strong>Op</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="5729c-231">
            <strong>Не определено</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-231">
            <strong>Undefined</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="5729c-232">
            <strong>NULL</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-232">
            <strong>Null</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="5729c-233">
            <strong>Логическое значение</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-233">
            <strong>Boolean</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="5729c-234">
            <strong>Число</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-234">
            <strong>Number</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="5729c-235">
            <strong>Строка</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-235">
            <strong>String</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="5729c-236">
            <strong>Объект</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-236">
            <strong>Object</strong>
         </span></span></td>
         <td valign="top"><span data-ttu-id="5729c-237">
            <strong>Массив</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-237">
            <strong>Array</strong>
         </span></span></td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="5729c-238">
            <strong>Не определено<strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-238">
            <strong>Undefined<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-239">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-239">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-240">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-240">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-241">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-241">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-242">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-242">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-243">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-243">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-244">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-244">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-245">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-245">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="5729c-246">
            <strong>NULL<strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-246">
            <strong>Null<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-247">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-247">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="5729c-248">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-248">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-249">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-249">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-250">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-250">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-251">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-251">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-252">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-252">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-253">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-253">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="5729c-254">
            <strong>Логическое значение<strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-254">
            <strong>Boolean<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-255">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-255">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-256">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-256">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="5729c-257">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-257">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-258">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-258">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-259">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-259">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-260">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-260">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-261">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-261">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="5729c-262">
            <strong>Число<strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-262">
            <strong>Number<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-263">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-263">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-264">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-264">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-265">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-265">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="5729c-266">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-266">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-267">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-267">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-268">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-268">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-269">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-269">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="5729c-270">
            <strong>Строка<strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-270">
            <strong>String<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-271">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-271">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-272">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-272">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-273">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-273">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-274">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-274">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="5729c-275">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-275">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-276">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-276">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-277">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-277">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="5729c-278">
            <strong>Объект<strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-278">
            <strong>Object<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-279">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-279">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-280">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-280">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-281">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-281">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-282">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-282">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-283">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-283">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="5729c-284">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-284">
            <strong>OK</strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-285">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-285">Undefined</span></span> </td>
      </tr>
      <tr>
         <td valign="top"><span data-ttu-id="5729c-286">
            <strong>Массив<strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-286">
            <strong>Array<strong>
         </span></span></td>
         <td valign="top">
<span data-ttu-id="5729c-287">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-287">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-288">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-288">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-289">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-289">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-290">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-290">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-291">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-291">Undefined</span></span> </td>
         <td valign="top">
<span data-ttu-id="5729c-292">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-292">Undefined</span></span> </td>
         <td valign="top"><span data-ttu-id="5729c-293">
            <strong>Допустимо</strong>
         </span><span class="sxs-lookup"><span data-stu-id="5729c-293">
            <strong>OK</strong>
         </span></span></td>
      </tr>
   </tbody>
</table>

<span data-ttu-id="5729c-294">Для других операторов сравнения, например, >, > =,! =, < и < =, hello применяются следующие правила:</span><span class="sxs-lookup"><span data-stu-id="5729c-294">For other comparison operators such as >, >=, !=, < and <=, hello following rules apply:</span></span>   

* <span data-ttu-id="5729c-295">Сравнение типов приводит к неопределенному результату.</span><span class="sxs-lookup"><span data-stu-id="5729c-295">Comparison across types results in Undefined.</span></span>
* <span data-ttu-id="5729c-296">Сравнение двух объектов или двух массивов приводит к неопределенному результату.</span><span class="sxs-lookup"><span data-stu-id="5729c-296">Comparison between two objects or two arrays results in Undefined.</span></span>   

<span data-ttu-id="5729c-297">Если результат hello hello скалярное выражение в фильтре hello не определен, соответствующего документа hello бы не будут включены в результат hello, так как не определено не соответствуют логически слишком «true».</span><span class="sxs-lookup"><span data-stu-id="5729c-297">If hello result of hello scalar expression in hello filter is Undefined, hello corresponding document would not be included in hello result, since Undefined doesn't logically equate too"true".</span></span>

### <a name="between-keyword"></a><span data-ttu-id="5729c-298">Ключевое слово BETWEEN (МЕЖДУ)</span><span class="sxs-lookup"><span data-stu-id="5729c-298">BETWEEN keyword</span></span>
<span data-ttu-id="5729c-299">Также можно использовать hello BETWEEN ключевое слово tooexpress запросами диапазоны значений как в ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-299">You can also use hello BETWEEN keyword tooexpress queries against ranges of values like in ANSI SQL.</span></span> <span data-ttu-id="5729c-300">BETWEEN может использоваться для строк или чисел.</span><span class="sxs-lookup"><span data-stu-id="5729c-300">BETWEEN can be used against strings or numbers.</span></span>

<span data-ttu-id="5729c-301">Например этот запрос возвращает все семейства документы, в которых hello оценка первый дочерний элемент — от 1 до 5 (включительно для обоих).</span><span class="sxs-lookup"><span data-stu-id="5729c-301">For example, this query returns all family documents in which hello first child's grade is between 1-5 (both inclusive).</span></span> 

    SELECT *
    FROM Families.children[0] c
    WHERE c.grade BETWEEN 1 AND 5

<span data-ttu-id="5729c-302">В отличие от в ANSI SQL, можно также использовать предложение BETWEEN hello в предложении FROM hello как следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-302">Unlike in ANSI-SQL, you can also use hello BETWEEN clause in hello FROM clause like in hello following example.</span></span>

    SELECT (c.grade BETWEEN 0 AND 10)
    FROM Families.children[0] c

<span data-ttu-id="5729c-303">Для ускорения времени выполнения запроса помните toocreate политику индексации, которая использует тип диапазона индекса для любого числового свойства и пути, которые фильтруются в предложении BETWEEN hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-303">For faster query execution times, remember toocreate an indexing policy that uses a range index type against any numeric properties/paths that are filtered in hello BETWEEN clause.</span></span> 

<span data-ttu-id="5729c-304">Hello основное различие между использованием BETWEEN в DocumentDB API и ANSI SQL — что можно выразить запросов в диапазоне от свойства смешанных типов — например, возможно, «уровень» быть числом (5) в некоторых документах и строк в других («grade4»).</span><span class="sxs-lookup"><span data-stu-id="5729c-304">hello main difference between using BETWEEN in DocumentDB API and ANSI SQL is that you can express range queries against properties of mixed types – for example, you might have "grade" be a number (5) in some documents and strings in others ("grade4").</span></span> <span data-ttu-id="5729c-305">Таким образом как на языке JavaScript, сравнение двух различных типов результатов в «undefined» и hello документа будут пропущены.</span><span class="sxs-lookup"><span data-stu-id="5729c-305">In these cases, like in JavaScript, a comparison between two different types results in "undefined", and hello document will be skipped.</span></span>

### <a name="logical-and-or-and-not-operators"></a><span data-ttu-id="5729c-306">Логические операторы (AND, OR или NOT)</span><span class="sxs-lookup"><span data-stu-id="5729c-306">Logical (AND, OR and NOT) operators</span></span>
<span data-ttu-id="5729c-307">Логические операторы работают над значениями типа Boolean.</span><span class="sxs-lookup"><span data-stu-id="5729c-307">Logical operators operate on Boolean values.</span></span> <span data-ttu-id="5729c-308">в hello в следующей таблице показаны Hello логические таблицы истинности этих операторов.</span><span class="sxs-lookup"><span data-stu-id="5729c-308">hello logical truth tables for these operators are shown in hello following tables.</span></span>

| <span data-ttu-id="5729c-309">ИЛИ</span><span class="sxs-lookup"><span data-stu-id="5729c-309">OR</span></span> | <span data-ttu-id="5729c-310">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-310">True</span></span> | <span data-ttu-id="5729c-311">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-311">False</span></span> | <span data-ttu-id="5729c-312">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-312">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5729c-313">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-313">True</span></span> |<span data-ttu-id="5729c-314">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-314">True</span></span> |<span data-ttu-id="5729c-315">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-315">True</span></span> |<span data-ttu-id="5729c-316">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-316">True</span></span> |
| <span data-ttu-id="5729c-317">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-317">False</span></span> |<span data-ttu-id="5729c-318">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-318">True</span></span> |<span data-ttu-id="5729c-319">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-319">False</span></span> |<span data-ttu-id="5729c-320">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-320">Undefined</span></span> |
| <span data-ttu-id="5729c-321">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-321">Undefined</span></span> |<span data-ttu-id="5729c-322">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-322">True</span></span> |<span data-ttu-id="5729c-323">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-323">Undefined</span></span> |<span data-ttu-id="5729c-324">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-324">Undefined</span></span> |

| <span data-ttu-id="5729c-325">И</span><span class="sxs-lookup"><span data-stu-id="5729c-325">AND</span></span> | <span data-ttu-id="5729c-326">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-326">True</span></span> | <span data-ttu-id="5729c-327">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-327">False</span></span> | <span data-ttu-id="5729c-328">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-328">Undefined</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5729c-329">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-329">True</span></span> |<span data-ttu-id="5729c-330">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-330">True</span></span> |<span data-ttu-id="5729c-331">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-331">False</span></span> |<span data-ttu-id="5729c-332">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-332">Undefined</span></span> |
| <span data-ttu-id="5729c-333">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-333">False</span></span> |<span data-ttu-id="5729c-334">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-334">False</span></span> |<span data-ttu-id="5729c-335">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-335">False</span></span> |<span data-ttu-id="5729c-336">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-336">False</span></span> |
| <span data-ttu-id="5729c-337">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-337">Undefined</span></span> |<span data-ttu-id="5729c-338">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-338">Undefined</span></span> |<span data-ttu-id="5729c-339">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-339">False</span></span> |<span data-ttu-id="5729c-340">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-340">Undefined</span></span> |

| <span data-ttu-id="5729c-341">НЕ</span><span class="sxs-lookup"><span data-stu-id="5729c-341">NOT</span></span> |  |
| --- | --- |
| <span data-ttu-id="5729c-342">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-342">True</span></span> |<span data-ttu-id="5729c-343">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-343">False</span></span> |
| <span data-ttu-id="5729c-344">Ложь</span><span class="sxs-lookup"><span data-stu-id="5729c-344">False</span></span> |<span data-ttu-id="5729c-345">Истина</span><span class="sxs-lookup"><span data-stu-id="5729c-345">True</span></span> |
| <span data-ttu-id="5729c-346">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-346">Undefined</span></span> |<span data-ttu-id="5729c-347">Не определено</span><span class="sxs-lookup"><span data-stu-id="5729c-347">Undefined</span></span> |

### <a name="in-keyword"></a><span data-ttu-id="5729c-348">Ключевое слово IN</span><span class="sxs-lookup"><span data-stu-id="5729c-348">IN keyword</span></span>
<span data-ttu-id="5729c-349">Ключевое слово Hello в может быть используется toocheck, является ли указанное значение совпадает с любым значением в виде списка.</span><span class="sxs-lookup"><span data-stu-id="5729c-349">hello IN keyword can be used toocheck whether a specified value matches any value in a list.</span></span> <span data-ttu-id="5729c-350">Например этот запрос возвращает все документы семейства идентификатор hello где «WakefieldFamily» или «AndersenFamily».</span><span class="sxs-lookup"><span data-stu-id="5729c-350">For example, this query returns all family documents where hello id is one of "WakefieldFamily" or "AndersenFamily".</span></span> 

    SELECT *
    FROM Families 
    WHERE Families.id IN ('AndersenFamily', 'WakefieldFamily')

<span data-ttu-id="5729c-351">Этот пример возвращает все документы, где hello состояния — это любые hello указанного значения.</span><span class="sxs-lookup"><span data-stu-id="5729c-351">This example returns all documents where hello state is any of hello specified values.</span></span>

    SELECT *
    FROM Families 
    WHERE Families.address.state IN ("NY", "WA", "CA", "PA", "OH", "OR", "MI", "WI", "MN", "FL")

### <a name="ternary--and-coalesce--operators"></a><span data-ttu-id="5729c-352">Операторы Ternary (?) и Coalesce (??)</span><span class="sxs-lookup"><span data-stu-id="5729c-352">Ternary (?) and Coalesce (??) operators</span></span>
<span data-ttu-id="5729c-353">операторы Hello троичный и Coalesce может быть используется toobuild условные выражения, примерно toopopular программирования языками, такими как C# и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5729c-353">hello Ternary and Coalesce operators can be used toobuild conditional expressions, similar toopopular programming languages like C# and JavaScript.</span></span> 

<span data-ttu-id="5729c-354">оператор Hello троичный (?) могут быть очень удобны при создании новых свойств JSON hello полет.</span><span class="sxs-lookup"><span data-stu-id="5729c-354">hello Ternary (?) operator can be very handy when constructing new JSON properties on hello fly.</span></span> <span data-ttu-id="5729c-355">Например теперь можно написать запросы tooclassify hello класс уровни в удобной для чтения форме, как и для новичков/промежуточных и дополнительно как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5729c-355">For example, now you can write queries tooclassify hello class levels into a human readable form like Beginner/Intermediate/Advanced as shown below.</span></span>

     SELECT (c.grade < 5)? "elementary": "other" AS gradeLevel 
     FROM Families.children[0] c

<span data-ttu-id="5729c-356">Также можно вложить hello вызовов toohello оператором, например в запросе hello ниже.</span><span class="sxs-lookup"><span data-stu-id="5729c-356">You can also nest hello calls toohello operator like in hello query below.</span></span>

    SELECT (c.grade < 5)? "elementary": ((c.grade < 9)? "junior": "high")  AS gradeLevel 
    FROM Families.children[0] c

<span data-ttu-id="5729c-357">Как с другими операторами запроса, если hello упоминаемого в условном выражении hello отсутствуют свойства в любой документ или типы hello сравниваемых различны, затем эти документы исключаются в результатах запроса hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-357">As with other query operators, if hello referenced properties in hello conditional expression are missing in any document, or if hello types being compared are different, then those documents are excluded in hello query results.</span></span>

<span data-ttu-id="5729c-358">Hello Coalesce (?) оператор может быть (так называемый используется tooefficiently Проверьте наличие hello свойства</span><span class="sxs-lookup"><span data-stu-id="5729c-358">hello Coalesce (??) operator can be used tooefficiently check for hello presence of a property (a.k.a.</span></span> <span data-ttu-id="5729c-359">(или его определения) в документе.</span><span class="sxs-lookup"><span data-stu-id="5729c-359">is defined) in a document.</span></span> <span data-ttu-id="5729c-360">Это удобно при запросах к частично структурированным данным или данным разных типов.</span><span class="sxs-lookup"><span data-stu-id="5729c-360">This is useful when querying against semi-structured or data of mixed types.</span></span> <span data-ttu-id="5729c-361">Например этот запрос возвращает hello «lastName» при его наличии или hello «Фамилия», если он отсутствует.</span><span class="sxs-lookup"><span data-stu-id="5729c-361">For example, this query returns hello "lastName" if present, or hello "surname" if it isn't present.</span></span>

    SELECT f.lastName ?? f.surname AS familyName
    FROM Families f

### <span data-ttu-id="5729c-362"><a id="EscapingReservedKeywords"></a>Доступ к свойству, заключенному в кавычки</span><span class="sxs-lookup"><span data-stu-id="5729c-362"><a id="EscapingReservedKeywords"></a>Quoted property accessor</span></span>
<span data-ttu-id="5729c-363">Также можно использовать свойства, с помощью оператора hello указанное свойство `[]`.</span><span class="sxs-lookup"><span data-stu-id="5729c-363">You can also access properties using hello quoted property operator `[]`.</span></span> <span data-ttu-id="5729c-364">Например, выражение `SELECT c.grade` and `SELECT c["grade"]` являются эквивалентными.</span><span class="sxs-lookup"><span data-stu-id="5729c-364">For example, `SELECT c.grade` and `SELECT c["grade"]` are equivalent.</span></span> <span data-ttu-id="5729c-365">Этот синтаксис полезно в тех случаях, когда требуется свойство, которое содержит пробелы, специальные символы, или происходит точно такое же имя, как ключевое слово SQL или зарезервированное слово hello tooshare tooescape.</span><span class="sxs-lookup"><span data-stu-id="5729c-365">This syntax is useful when you need tooescape a property that contains spaces, special characters, or happens tooshare hello same name as a SQL keyword or reserved word.</span></span>

    SELECT f["lastName"]
    FROM Families f
    WHERE f["id"] = "AndersenFamily"


## <span data-ttu-id="5729c-366"><a id="SelectClause"></a>Предложение SELECT</span><span class="sxs-lookup"><span data-stu-id="5729c-366"><a id="SelectClause"></a>SELECT clause</span></span>
<span data-ttu-id="5729c-367">предложение SELECT Hello (**`SELECT <select_list>`**) является обязательным и указывает, какие значения извлекаются из запроса hello так же, как в ANSI SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-367">hello SELECT clause (**`SELECT <select_list>`**) is mandatory and specifies what values are retrieved from hello query, just like in ANSI-SQL.</span></span> <span data-ttu-id="5729c-368">подмножество Hello, фильтруется на основе hello исходные документы передаются на этап отображения hello, где указан hello извлекаются значения JSON и создается новый объект JSON, для каждой входной параметр, переданный в него.</span><span class="sxs-lookup"><span data-stu-id="5729c-368">hello subset that's been filtered on top of hello source documents are passed onto hello projection phase, where hello specified JSON values are retrieved and a new JSON object is constructed, for each input passed onto it.</span></span> 

<span data-ttu-id="5729c-369">Hello в следующем примере показан типичный запрос SELECT.</span><span class="sxs-lookup"><span data-stu-id="5729c-369">hello following example shows a typical SELECT query.</span></span> 

<span data-ttu-id="5729c-370">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-370">**Query**</span></span>

    SELECT f.address
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="5729c-371">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-371">**Results**</span></span>

    [{
      "address": {
        "state": "WA", 
        "county": "King", 
        "city": "seattle"
      }
    }]


### <a name="nested-properties"></a><span data-ttu-id="5729c-372">Вложенные свойства</span><span class="sxs-lookup"><span data-stu-id="5729c-372">Nested properties</span></span>
<span data-ttu-id="5729c-373">В следующем примере hello, мы проецирование двух вложенных свойств `f.address.state` и `f.address.city`.</span><span class="sxs-lookup"><span data-stu-id="5729c-373">In hello following example, we are projecting two nested properties `f.address.state` and `f.address.city`.</span></span>

<span data-ttu-id="5729c-374">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-374">**Query**</span></span>

    SELECT f.address.state, f.address.city
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="5729c-375">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-375">**Results**</span></span>

    [{
      "state": "WA", 
      "city": "seattle"
    }]


<span data-ttu-id="5729c-376">Проекция также поддерживает выражения JSON, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="5729c-376">Projection also supports JSON expressions as shown in hello following example:</span></span>

<span data-ttu-id="5729c-377">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-377">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city, "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="5729c-378">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-378">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle", 
        "name": "AndersenFamily"
      }
    }]


<span data-ttu-id="5729c-379">Давайте рассмотрим роль hello `$1` здесь.</span><span class="sxs-lookup"><span data-stu-id="5729c-379">Let's look at hello role of `$1` here.</span></span> <span data-ttu-id="5729c-380">Hello `SELECT` предложение должен toocreate объекта JSON и без ключа предоставляется, мы используем неявный аргумент имена переменных, начиная с `$1`.</span><span class="sxs-lookup"><span data-stu-id="5729c-380">hello `SELECT` clause needs toocreate a JSON object and since no key is provided, we use implicit argument variable names starting with `$1`.</span></span> <span data-ttu-id="5729c-381">Например, этот запрос возвращает две неявные переменные аргументов, помеченные как `$1` and `$2`.</span><span class="sxs-lookup"><span data-stu-id="5729c-381">For example, this query returns two implicit argument variables, labeled `$1` and `$2`.</span></span>

<span data-ttu-id="5729c-382">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-382">**Query**</span></span>

    SELECT { "state": f.address.state, "city": f.address.city }, 
           { "name": f.id }
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="5729c-383">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-383">**Results**</span></span>

    [{
      "$1": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "$2": {
        "name": "AndersenFamily"
      }
    }]


### <a name="aliasing"></a><span data-ttu-id="5729c-384">Псевдонимы</span><span class="sxs-lookup"><span data-stu-id="5729c-384">Aliasing</span></span>
<span data-ttu-id="5729c-385">Теперь давайте расширить hello приведенном выше примере с помощью явных псевдонимов значений.</span><span class="sxs-lookup"><span data-stu-id="5729c-385">Now let's extend hello example above with explicit aliasing of values.</span></span> <span data-ttu-id="5729c-386">КАК ключевое слово, используемое для присвоения псевдонимов hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-386">AS is hello keyword used for aliasing.</span></span> <span data-ttu-id="5729c-387">Это необязательно, как показано во время проецирования hello второе значение как `NameInfo`.</span><span class="sxs-lookup"><span data-stu-id="5729c-387">It's optional as shown while projecting hello second value as `NameInfo`.</span></span> 

<span data-ttu-id="5729c-388">Если запрос содержит два свойства с hello таким же именем, совмещение имен должно быть используется toorename одно или оба hello свойства, чтобы они отличаются в hello проецируется результат.</span><span class="sxs-lookup"><span data-stu-id="5729c-388">In case a query has two properties with hello same name, aliasing must be used toorename one or both of hello properties so that they are disambiguated in hello projected result.</span></span>

<span data-ttu-id="5729c-389">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-389">**Query**</span></span>

    SELECT 
           { "state": f.address.state, "city": f.address.city } AS AddressInfo, 
           { "name": f.id } NameInfo
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="5729c-390">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-390">**Results**</span></span>

    [{
      "AddressInfo": {
        "state": "WA", 
        "city": "seattle"
      }, 
      "NameInfo": {
        "name": "AndersenFamily"
      }
    }]


### <a name="scalar-expressions"></a><span data-ttu-id="5729c-391">Скалярные выражения</span><span class="sxs-lookup"><span data-stu-id="5729c-391">Scalar expressions</span></span>
<span data-ttu-id="5729c-392">Кроме ссылается tooproperty, предложение SELECT hello также поддерживает скалярные выражения, такие как константы, арифметических выражений, логические выражения и т. д. Например, вот простой запрос "Hello World".</span><span class="sxs-lookup"><span data-stu-id="5729c-392">In addition tooproperty references, hello SELECT clause also supports scalar expressions like constants, arithmetic expressions, logical expressions, etc. For example, here's a simple "Hello World" query.</span></span>

<span data-ttu-id="5729c-393">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-393">**Query**</span></span>

    SELECT "Hello World"

<span data-ttu-id="5729c-394">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-394">**Results**</span></span>

    [{
      "$1": "Hello World"
    }]


<span data-ttu-id="5729c-395">Вот более сложный пример с использованием скалярного выражения:</span><span class="sxs-lookup"><span data-stu-id="5729c-395">Here's a more complex example that uses a scalar expression.</span></span>

<span data-ttu-id="5729c-396">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-396">**Query**</span></span>

    SELECT ((2 + 11 % 7)-2)/3    

<span data-ttu-id="5729c-397">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-397">**Results**</span></span>

    [{
      "$1": 1.33333
    }]


<span data-ttu-id="5729c-398">В следующем примере hello результат hello hello скалярное выражение является логическим.</span><span class="sxs-lookup"><span data-stu-id="5729c-398">In hello following example, hello result of hello scalar expression is a Boolean.</span></span>

<span data-ttu-id="5729c-399">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-399">**Query**</span></span>

    SELECT f.address.city = f.address.state AS AreFromSameCityState
    FROM Families f    

<span data-ttu-id="5729c-400">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-400">**Results**</span></span>

    [
      {
        "AreFromSameCityState": false
      }, 
      {
        "AreFromSameCityState": true
      }
    ]


### <a name="object-and-array-creation"></a><span data-ttu-id="5729c-401">Создание объектов и массивов</span><span class="sxs-lookup"><span data-stu-id="5729c-401">Object and array creation</span></span>
<span data-ttu-id="5729c-402">Еще одной ключевой возможностью языка SQL для API DocumentDB является создание объектов и массивов.</span><span class="sxs-lookup"><span data-stu-id="5729c-402">Another key feature of DocumentDB API SQL is array/object creation.</span></span> <span data-ttu-id="5729c-403">В предыдущем примере hello Обратите внимание, что мы создали новый объект JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-403">In hello previous example, note that we created a new JSON object.</span></span> <span data-ttu-id="5729c-404">Аналогично один можно также создать массивы как показано в следующих примерах hello:</span><span class="sxs-lookup"><span data-stu-id="5729c-404">Similarly, one can also construct arrays as shown in hello following examples:</span></span>

<span data-ttu-id="5729c-405">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-405">**Query**</span></span>

    SELECT [f.address.city, f.address.state] AS CityState 
    FROM Families f    

<span data-ttu-id="5729c-406">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-406">**Results**</span></span>  

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

### <span data-ttu-id="5729c-407"><a id="ValueKeyword"></a>Ключевое слово VALUE</span><span class="sxs-lookup"><span data-stu-id="5729c-407"><a id="ValueKeyword"></a>VALUE keyword</span></span>
<span data-ttu-id="5729c-408">Hello **значение** ключевое слово предоставляет значение JSON tooreturn способом.</span><span class="sxs-lookup"><span data-stu-id="5729c-408">hello **VALUE** keyword provides a way tooreturn JSON value.</span></span> <span data-ttu-id="5729c-409">Например, запрос hello, показано ниже hello возвращает скалярное `"Hello World"` вместо `{$1: "Hello World"}`.</span><span class="sxs-lookup"><span data-stu-id="5729c-409">For example, hello query shown below returns hello scalar `"Hello World"` instead of `{$1: "Hello World"}`.</span></span>

<span data-ttu-id="5729c-410">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-410">**Query**</span></span>

    SELECT VALUE "Hello World"

<span data-ttu-id="5729c-411">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-411">**Results**</span></span>

    [
      "Hello World"
    ]


<span data-ttu-id="5729c-412">Hello следующий запрос возвращает значение JSON hello без hello `"address"` метки в результатах hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-412">hello following query returns hello JSON value without hello `"address"` label in hello results.</span></span>

<span data-ttu-id="5729c-413">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-413">**Query**</span></span>

    SELECT VALUE f.address
    FROM Families f    

<span data-ttu-id="5729c-414">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-414">**Results**</span></span>  

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

<span data-ttu-id="5729c-415">Hello следующий пример расширяет это tooshow как простые значения в JSON tooreturn (hello конечный уровень дерева hello JSON).</span><span class="sxs-lookup"><span data-stu-id="5729c-415">hello following example extends this tooshow how tooreturn JSON primitive values (hello leaf level of hello JSON tree).</span></span> 

<span data-ttu-id="5729c-416">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-416">**Query**</span></span>

    SELECT VALUE f.address.state
    FROM Families f    

<span data-ttu-id="5729c-417">**Результат**</span><span class="sxs-lookup"><span data-stu-id="5729c-417">**Results**</span></span>

    [
      "WA",
      "NY"
    ]


### <a name="-operator"></a><span data-ttu-id="5729c-418">Оператор *</span><span class="sxs-lookup"><span data-stu-id="5729c-418">* Operator</span></span>
<span data-ttu-id="5729c-419">Hello специальный оператор (*) — поддерживаемые tooproject hello документ как-является.</span><span class="sxs-lookup"><span data-stu-id="5729c-419">hello special operator (*) is supported tooproject hello document as-is.</span></span> <span data-ttu-id="5729c-420">При использовании, он должен быть hello проецировать только поля.</span><span class="sxs-lookup"><span data-stu-id="5729c-420">When used, it must be hello only projected field.</span></span> <span data-ttu-id="5729c-421">Хотя запрос наподобие `SELECT * FROM Families f` допустим, `SELECT VALUE * FROM Families f ` и `SELECT *, f.id FROM Families f ` недопустимы.</span><span class="sxs-lookup"><span data-stu-id="5729c-421">While a query like `SELECT * FROM Families f` is valid, `SELECT VALUE * FROM Families f ` and  `SELECT *, f.id FROM Families f ` are not valid.</span></span>

<span data-ttu-id="5729c-422">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-422">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE f.id = "AndersenFamily"

<span data-ttu-id="5729c-423">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-423">**Results**</span></span>

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

### <span data-ttu-id="5729c-424"><a id="TopKeyword"></a>Оператор TOP</span><span class="sxs-lookup"><span data-stu-id="5729c-424"><a id="TopKeyword"></a>TOP Operator</span></span>
<span data-ttu-id="5729c-425">Ключевое слово TOP Hello может быть использован toolimit hello количество значения из запроса.</span><span class="sxs-lookup"><span data-stu-id="5729c-425">hello TOP keyword can be used toolimit hello number of values from a query.</span></span> <span data-ttu-id="5729c-426">Если предложение TOP используется в сочетании с предложением ORDER BY hello, hello результирующего набора является ограниченной toohello первое число N последовательных значений; в противном случае возвращается первое число N hello результатов в неопределенном порядке.</span><span class="sxs-lookup"><span data-stu-id="5729c-426">When TOP is used in conjunction with hello ORDER BY clause, hello result set is limited toohello first N number of ordered values; otherwise, it returns hello first N number of results in an undefined order.</span></span> <span data-ttu-id="5729c-427">Рекомендуется в инструкции SELECT всегда используйте предложение ORDER BY с предложением TOP hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-427">As a best practice, in a SELECT statement, always use an ORDER BY clause with hello TOP clause.</span></span> <span data-ttu-id="5729c-428">Это является единственным способом hello toopredictably указывают, какие строки будут изменены предложением TOP.</span><span class="sxs-lookup"><span data-stu-id="5729c-428">This is hello only way toopredictably indicate which rows are affected by TOP.</span></span> 

<span data-ttu-id="5729c-429">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-429">**Query**</span></span>

    SELECT TOP 1 * 
    FROM Families f 

<span data-ttu-id="5729c-430">**Результат**</span><span class="sxs-lookup"><span data-stu-id="5729c-430">**Results**</span></span>

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

<span data-ttu-id="5729c-431">TOP можно использовать с постоянным значением (как показано выше) или с переменным значением посредством параметризованных запросов.</span><span class="sxs-lookup"><span data-stu-id="5729c-431">TOP can be used with a constant value (as shown above) or with a variable value using parameterized queries.</span></span> <span data-ttu-id="5729c-432">Дополнительные сведения см. в описании параметризованных запросов ниже.</span><span class="sxs-lookup"><span data-stu-id="5729c-432">For more details, please see parameterized queries below.</span></span>

### <span data-ttu-id="5729c-433"><a id="Aggregates"></a>Статистические функции</span><span class="sxs-lookup"><span data-stu-id="5729c-433"><a id="Aggregates"></a>Aggregate Functions</span></span>
<span data-ttu-id="5729c-434">Можно также выполнить агрегатов в hello `SELECT` предложения.</span><span class="sxs-lookup"><span data-stu-id="5729c-434">You can also perform aggregations in hello `SELECT` clause.</span></span> <span data-ttu-id="5729c-435">Статистические функции выполняют вычисление на наборе значений и возвращают одиночное значение.</span><span class="sxs-lookup"><span data-stu-id="5729c-435">Aggregate functions perform a calculation on a set of values and return a single value.</span></span> <span data-ttu-id="5729c-436">Например, hello следующий запрос возвращает число hello семейства документов в коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-436">For example, hello following query returns hello count of family documents within hello collection.</span></span>

<span data-ttu-id="5729c-437">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-437">**Query**</span></span>

    SELECT COUNT(1) 
    FROM Families f 

<span data-ttu-id="5729c-438">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-438">**Results**</span></span>

    [{
        "$1": 2
    }]

<span data-ttu-id="5729c-439">Можно также вернуть hello скалярное значение hello статистические с помощью hello `VALUE` ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="5729c-439">You can also return hello scalar value of hello aggregate by using hello `VALUE` keyword.</span></span> <span data-ttu-id="5729c-440">Например, hello следующий запрос возвращает количество значений в hello как одно число:</span><span class="sxs-lookup"><span data-stu-id="5729c-440">For example, hello following query returns hello count of values as a single number:</span></span>

<span data-ttu-id="5729c-441">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-441">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f 

<span data-ttu-id="5729c-442">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-442">**Results**</span></span>

    [ 2 ]

<span data-ttu-id="5729c-443">Также можно выполнять статистические вычисления в сочетании с фильтрами.</span><span class="sxs-lookup"><span data-stu-id="5729c-443">You can also perform aggregates in combination with filters.</span></span> <span data-ttu-id="5729c-444">Например, hello следующий запрос возвращает hello число документов с адресом hello в hello штата Вашингтон, США.</span><span class="sxs-lookup"><span data-stu-id="5729c-444">For example, hello following query returns hello count of documents with hello address in hello state of Washington.</span></span>

<span data-ttu-id="5729c-445">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-445">**Query**</span></span>

    SELECT VALUE COUNT(1) 
    FROM Families f
    WHERE f.address.state = "WA" 

<span data-ttu-id="5729c-446">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-446">**Results**</span></span>

    [ 1 ]

<span data-ttu-id="5729c-447">Hello Следующая таблица показывает hello список статистических функций, поддерживаемых в DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="5729c-447">hello following table shows hello list of supported aggregate functions in DocumentDB API.</span></span> <span data-ttu-id="5729c-448">`SUM`и `AVG` выполняются над числовыми значениями, тогда как `COUNT`, `MIN` и `MAX` можно выполнять над числами, строками, логическими значениями и значениями NULL.</span><span class="sxs-lookup"><span data-stu-id="5729c-448">`SUM` and `AVG` are performed over numeric values, whereas `COUNT`, `MIN`, and `MAX` can be performed over numbers, strings, Booleans, and nulls.</span></span> 

| <span data-ttu-id="5729c-449">Использование</span><span class="sxs-lookup"><span data-stu-id="5729c-449">Usage</span></span> | <span data-ttu-id="5729c-450">Описание</span><span class="sxs-lookup"><span data-stu-id="5729c-450">Description</span></span> |
|-------|-------------|
| <span data-ttu-id="5729c-451">COUNT</span><span class="sxs-lookup"><span data-stu-id="5729c-451">COUNT</span></span> | <span data-ttu-id="5729c-452">Возвращает hello количество элементов в выражении hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-452">Returns hello number of items in hello expression.</span></span> |
| <span data-ttu-id="5729c-453">SUM</span><span class="sxs-lookup"><span data-stu-id="5729c-453">SUM</span></span>   | <span data-ttu-id="5729c-454">Возвращает hello сумму всех значений hello в выражении hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-454">Returns hello sum of all hello values in hello expression.</span></span> |
| <span data-ttu-id="5729c-455">MIN</span><span class="sxs-lookup"><span data-stu-id="5729c-455">MIN</span></span>   | <span data-ttu-id="5729c-456">Возвращает hello минимальное значение в выражении hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-456">Returns hello minimum value in hello expression.</span></span> |
| <span data-ttu-id="5729c-457">MAX</span><span class="sxs-lookup"><span data-stu-id="5729c-457">MAX</span></span>   | <span data-ttu-id="5729c-458">Возвращает hello максимальное значение в выражении hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-458">Returns hello maximum value in hello expression.</span></span> |
| <span data-ttu-id="5729c-459">AVG</span><span class="sxs-lookup"><span data-stu-id="5729c-459">AVG</span></span>   | <span data-ttu-id="5729c-460">Возвращает hello среднее значений hello в выражении hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-460">Returns hello average of hello values in hello expression.</span></span> |

<span data-ttu-id="5729c-461">Статистические функции также могут быть выполнены над hello результатов итерации массива.</span><span class="sxs-lookup"><span data-stu-id="5729c-461">Aggregates can also be performed over hello results of an array iteration.</span></span> <span data-ttu-id="5729c-462">Дополнительные сведения см. в разделе [Итерация](#Iteration).</span><span class="sxs-lookup"><span data-stu-id="5729c-462">For more information, see [Array Iteration in Queries](#Iteration).</span></span>

> [!NOTE]
> <span data-ttu-id="5729c-463">При с помощью hello Explorer запроса портал Azure, обратите внимание, что статистических запросов может возвращать hello частично сводных результатов по запроса страницы.</span><span class="sxs-lookup"><span data-stu-id="5729c-463">When using hello Azure portal's Query Explorer, note that aggregation queries may return hello partially aggregated results over a query page.</span></span> <span data-ttu-id="5729c-464">Hello SDK создает одно совокупное значение на всех страницах.</span><span class="sxs-lookup"><span data-stu-id="5729c-464">hello SDKs produces a single cumulative value across all pages.</span></span> 
> 
> <span data-ttu-id="5729c-465">В порядке tooperform статистических запросов с помощью кода, .NET SDK 1.12.0, пакет SDK для .NET Core 1.1.0 или Java SDK 1.9.5.\ или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="5729c-465">In order tooperform aggregation queries using code, you need .NET SDK 1.12.0, .NET Core SDK 1.1.0, or Java SDK 1.9.5 or above.</span></span>    
>

## <span data-ttu-id="5729c-466"><a id="OrderByClause"></a>Предложение ORDER BY</span><span class="sxs-lookup"><span data-stu-id="5729c-466"><a id="OrderByClause"></a>ORDER BY clause</span></span>
<span data-ttu-id="5729c-467">Как и в ANSI-SQL, вы можете включить в запрос необязательное предложение ORDER BY.</span><span class="sxs-lookup"><span data-stu-id="5729c-467">Like in ANSI-SQL, you can include an optional Order By clause while querying.</span></span> <span data-ttu-id="5729c-468">Hello предложение может включать необязательный ASC или DESC toospecify hello порядок аргументов получить результаты.</span><span class="sxs-lookup"><span data-stu-id="5729c-468">hello clause can include an optional ASC/DESC argument toospecify hello order in which results must be retrieved.</span></span>

<span data-ttu-id="5729c-469">Например ниже приведен запрос, получающий семейств в порядке название резидентного города hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-469">For example, here's a query that retrieves families in order of hello resident city's name.</span></span>

<span data-ttu-id="5729c-470">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-470">**Query**</span></span>

    SELECT f.id, f.address.city
    FROM Families f 
    ORDER BY f.address.city

<span data-ttu-id="5729c-471">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-471">**Results**</span></span>

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

<span data-ttu-id="5729c-472">А вот запрос, получающий семейств в порядке, Дата создания, который хранится как число, представляющее hello времени начала эпохи, т. е., затраченного времени с 1 января 1970 года в секундах.</span><span class="sxs-lookup"><span data-stu-id="5729c-472">And here's a query that retrieves families in order of creation date, which is stored as a number representing hello epoch time, i.e, elapsed time since Jan 1, 1970 in seconds.</span></span>

<span data-ttu-id="5729c-473">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-473">**Query**</span></span>

    SELECT f.id, f.creationDate
    FROM Families f 
    ORDER BY f.creationDate DESC

<span data-ttu-id="5729c-474">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-474">**Results**</span></span>

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

## <span data-ttu-id="5729c-475"><a id="Advanced"></a>Дополнительные понятия базы данных и SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="5729c-475"><a id="Advanced"></a>Advanced database concepts and SQL queries</span></span>

### <span data-ttu-id="5729c-476"><a id="Iteration"></a>Итерация</span><span class="sxs-lookup"><span data-stu-id="5729c-476"><a id="Iteration"></a>Iteration</span></span>
<span data-ttu-id="5729c-477">Было добавлено новую конструкцию hello **в** ключевое слово в DocumentDB API SQL tooprovide поддержку перебора массивов JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-477">A new construct was added via hello **IN** keyword in DocumentDB API SQL tooprovide support for iterating over JSON arrays.</span></span> <span data-ttu-id="5729c-478">Источник Hello FROM обеспечивает поддержку для итерации.</span><span class="sxs-lookup"><span data-stu-id="5729c-478">hello FROM source provides support for iteration.</span></span> <span data-ttu-id="5729c-479">Начнем с hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="5729c-479">Let's start with hello following example:</span></span>

<span data-ttu-id="5729c-480">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-480">**Query**</span></span>

    SELECT * 
    FROM Families.children

<span data-ttu-id="5729c-481">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-481">**Results**</span></span>  

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

<span data-ttu-id="5729c-482">Теперь давайте рассмотрим другой запрос, который выполняет итерацию по дочерним элементам в коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-482">Now let's look at another query that performs iteration over children in hello collection.</span></span> <span data-ttu-id="5729c-483">Обратите внимание, hello разница в выходном массиве hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-483">Note hello difference in hello output array.</span></span> <span data-ttu-id="5729c-484">В этом примере разбивает `children` и сводит результаты hello в один массив.</span><span class="sxs-lookup"><span data-stu-id="5729c-484">This example splits `children` and flattens hello results into a single array.</span></span>  

<span data-ttu-id="5729c-485">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-485">**Query**</span></span>

    SELECT * 
    FROM c IN Families.children

<span data-ttu-id="5729c-486">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-486">**Results**</span></span>  

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

<span data-ttu-id="5729c-487">Это может быть дополнительно используется toofilter на каждой отдельной операции hello массива, как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="5729c-487">This can be further used toofilter on each individual entry of hello array as shown in hello following example:</span></span>

<span data-ttu-id="5729c-488">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-488">**Query**</span></span>

    SELECT c.givenName
    FROM c IN Families.children
    WHERE c.grade = 8

<span data-ttu-id="5729c-489">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-489">**Results**</span></span>  

    [{
      "givenName": "Lisa"
    }]

<span data-ttu-id="5729c-490">Можно также выполнить статистическую результирующим hello итерации массива.</span><span class="sxs-lookup"><span data-stu-id="5729c-490">You can also perform aggregation over hello result of array iteration.</span></span> <span data-ttu-id="5729c-491">Например hello следующий запрос подсчитывает hello количество дочерних элементов среди всех семейств.</span><span class="sxs-lookup"><span data-stu-id="5729c-491">For example, hello following query counts hello number of children among all families.</span></span>

<span data-ttu-id="5729c-492">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-492">**Query**</span></span>

    SELECT COUNT(child) 
    FROM child IN Families.children

<span data-ttu-id="5729c-493">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-493">**Results**</span></span>  

    [
      { 
        "$1": 3
      }
    ]

### <span data-ttu-id="5729c-494"><a id="Joins"></a>Соединения</span><span class="sxs-lookup"><span data-stu-id="5729c-494"><a id="Joins"></a>Joins</span></span>
<span data-ttu-id="5729c-495">В реляционной базе данных важно toojoin необходимость hello по таблицам.</span><span class="sxs-lookup"><span data-stu-id="5729c-495">In a relational database, hello need toojoin across tables is important.</span></span> <span data-ttu-id="5729c-496">Он является hello логических toodesigning следствие нормализовать схемы.</span><span class="sxs-lookup"><span data-stu-id="5729c-496">It's hello logical corollary toodesigning normalized schemas.</span></span> <span data-ttu-id="5729c-497">Противоположные toothis, DocumentDB API связана с моделью hello денормализованные данные без схемы документов.</span><span class="sxs-lookup"><span data-stu-id="5729c-497">Contrary toothis, DocumentDB API deals with hello denormalized data model of schema-free documents.</span></span> <span data-ttu-id="5729c-498">Это hello логический эквивалент a «самосоединение».</span><span class="sxs-lookup"><span data-stu-id="5729c-498">This is hello logical equivalent of a "self-join".</span></span>

<span data-ttu-id="5729c-499">синтаксис Hello, поддерживающий язык hello является СОЕДИНЕНИЕМ СОЕДИНЕНИЯ < from_source2 > < from_source1 >... JOIN <from_sourceN>.</span><span class="sxs-lookup"><span data-stu-id="5729c-499">hello syntax that hello language supports is <from_source1> JOIN <from_source2> JOIN ... JOIN <from_sourceN>.</span></span> <span data-ttu-id="5729c-500">В целом будет возвращаться набор **N**-кортежей (кортежей, у которых число значений равно **N**).</span><span class="sxs-lookup"><span data-stu-id="5729c-500">Overall, this returns a set of **N**-tuples (tuple with **N** values).</span></span> <span data-ttu-id="5729c-501">Каждый кортеж будет иметь значения, полученные путем итерации всех псевдонимов коллекции среди их наборов.</span><span class="sxs-lookup"><span data-stu-id="5729c-501">Each tuple has values produced by iterating all collection aliases over their respective sets.</span></span> <span data-ttu-id="5729c-502">Другими словами это полное перекрестное произведение наборов hello, участвующих в соединении hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-502">In other words, this is a full cross product of hello sets participating in hello join.</span></span>

<span data-ttu-id="5729c-503">Hello примеры показывают, как работает предложение JOIN hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-503">hello following examples show how hello JOIN clause works.</span></span> <span data-ttu-id="5729c-504">В следующем примере hello hello результат является пустым, поскольку hello перекрестное произведение каждого документа из источника и пустой набор пуст.</span><span class="sxs-lookup"><span data-stu-id="5729c-504">In hello following example, hello result is empty since hello cross product of each document from source and an empty set is empty.</span></span>

<span data-ttu-id="5729c-505">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-505">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.NonExistent

<span data-ttu-id="5729c-506">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-506">**Results**</span></span>  

    [{
    }]


<span data-ttu-id="5729c-507">В следующем примере hello, hello соединения находится между корень документа hello и hello `children` subroot.</span><span class="sxs-lookup"><span data-stu-id="5729c-507">In hello following example, hello join is between hello document root and hello `children` subroot.</span></span> <span data-ttu-id="5729c-508">Это векторное произведение между двумя объектами JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-508">It's a cross product between two JSON objects.</span></span> <span data-ttu-id="5729c-509">Hello факт, что дочерние элементы массива не позволяет эффективно hello СОЕДИНЕНИЯ, так как мы работаем с один корень, hello дочерних элементов массива.</span><span class="sxs-lookup"><span data-stu-id="5729c-509">hello fact that children is an array is not effective in hello JOIN since we are dealing with a single root that is hello children array.</span></span> <span data-ttu-id="5729c-510">Таким образом hello результат содержит только два результата, поскольку hello перекрестное произведение каждого документа с массивом hello дает точно только один документ.</span><span class="sxs-lookup"><span data-stu-id="5729c-510">Hence hello result contains only two results, since hello cross product of each document with hello array yields exactly only one document.</span></span>

<span data-ttu-id="5729c-511">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-511">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN f.children

<span data-ttu-id="5729c-512">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-512">**Results**</span></span>

    [
      {
        "id": "AndersenFamily"
      }, 
      {
        "id": "WakefieldFamily"
      }
    ]


<span data-ttu-id="5729c-513">Следующий пример Hello показано более традиционных соединение:</span><span class="sxs-lookup"><span data-stu-id="5729c-513">hello following example shows a more conventional join:</span></span>

<span data-ttu-id="5729c-514">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-514">**Query**</span></span>

    SELECT f.id
    FROM Families f
    JOIN c IN f.children 

<span data-ttu-id="5729c-515">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-515">**Results**</span></span>

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



<span data-ttu-id="5729c-516">Hello первое, что toonote является, hello `from_source` из hello **JOIN** предложение является итератором.</span><span class="sxs-lookup"><span data-stu-id="5729c-516">hello first thing toonote is that hello `from_source` of hello **JOIN** clause is an iterator.</span></span> <span data-ttu-id="5729c-517">Таким образом поток hello в данном случае составляет:</span><span class="sxs-lookup"><span data-stu-id="5729c-517">So, hello flow in this case is as follows:</span></span>  

* <span data-ttu-id="5729c-518">Разверните каждый дочерний элемент **c** в массиве hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-518">Expand each child element **c** in hello array.</span></span>
* <span data-ttu-id="5729c-519">Применение перекрестного произведения со hello корень документа hello **f** с каждого дочернего элемента **c** , плоский формат в первом шаге hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-519">Apply a cross product with hello root of hello document **f** with each child element **c** that was flattened in hello first step.</span></span>
* <span data-ttu-id="5729c-520">Наконец, проект hello корневой объект **f** только свойство name.</span><span class="sxs-lookup"><span data-stu-id="5729c-520">Finally, project hello root object **f** name property alone.</span></span> 

<span data-ttu-id="5729c-521">Первый документ Hello (`AndersenFamily`) содержит только один дочерний элемент, поэтому hello результирующий набор содержит только один объект соответствующего toothis документа.</span><span class="sxs-lookup"><span data-stu-id="5729c-521">hello first document (`AndersenFamily`) contains only one child element, so hello result set contains only a single object corresponding toothis document.</span></span> <span data-ttu-id="5729c-522">Hello второго документа (`WakefieldFamily`) содержит два дочерних элемента.</span><span class="sxs-lookup"><span data-stu-id="5729c-522">hello second document (`WakefieldFamily`) contains two children.</span></span> <span data-ttu-id="5729c-523">Таким образом hello перекрестное произведение создает отдельный объект для каждого дочернего элемента, тем самым в результате чего два объекта: один для каждого дочернего соответствующий toothis документа.</span><span class="sxs-lookup"><span data-stu-id="5729c-523">So, hello cross product produces a separate object for each child, thereby resulting in two objects, one for each child corresponding toothis document.</span></span> <span data-ttu-id="5729c-524">поля в обоих этих документов являются корневым Hello hello таким же, как и следовало ожидать в перекрестное произведение.</span><span class="sxs-lookup"><span data-stu-id="5729c-524">hello root fields in both these documents are hello same, just as you would expect in a cross product.</span></span>

<span data-ttu-id="5729c-525">Hello real служебной программы из hello СОЕДИНЕНИЯ является tooform кортежей из перекрестного произведения hello в форме, в противном случае сложно tooproject.</span><span class="sxs-lookup"><span data-stu-id="5729c-525">hello real utility of hello JOIN is tooform tuples from hello cross-product in a shape that's otherwise difficult tooproject.</span></span> <span data-ttu-id="5729c-526">Кроме того, как показано в следующем примере hello, можно отфильтровать hello сочетания кортеж hello, которая позволяет пользователь выбрал условия удовлетворены hello кортежей в целом.</span><span class="sxs-lookup"><span data-stu-id="5729c-526">Furthermore, as we see in hello example below, you could filter on hello combination of a tuple that lets' hello user chose a condition satisfied by hello tuples overall.</span></span>

<span data-ttu-id="5729c-527">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-527">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets

<span data-ttu-id="5729c-528">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-528">**Results**</span></span>

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



<span data-ttu-id="5729c-529">В этом примере является естественным расширением предшествующий пример hello и выполняет двойные соединения.</span><span class="sxs-lookup"><span data-stu-id="5729c-529">This example is a natural extension of hello preceding example, and performs a double join.</span></span> <span data-ttu-id="5729c-530">Таким образом hello векторное произведение можно рассматривать как hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="5729c-530">So, hello cross product can be viewed as hello following pseudo-code:</span></span>

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

<span data-ttu-id="5729c-531">`AndersenFamily` имеется один ребенок, у которого один питомец.</span><span class="sxs-lookup"><span data-stu-id="5729c-531">`AndersenFamily` has one child who has one pet.</span></span> <span data-ttu-id="5729c-532">Таким образом, hello перекрестное произведение возвращает одну строку (1\*1\*1) из этого семейства.</span><span class="sxs-lookup"><span data-stu-id="5729c-532">So, hello cross product yields one row (1\*1\*1) from this family.</span></span> <span data-ttu-id="5729c-533">Однако семейство Wakefield включает двух детей, но только у одного ребенка «Джесси» есть питомцы.</span><span class="sxs-lookup"><span data-stu-id="5729c-533">WakefieldFamily however has two children, but only one child "Jesse" has pets.</span></span> <span data-ttu-id="5729c-534">У Джесси два питомца.</span><span class="sxs-lookup"><span data-stu-id="5729c-534">Jesse has two pets though.</span></span> <span data-ttu-id="5729c-535">Поэтому hello перекрестное произведение дает результат 1\*1\*2 = 2 строки из этого семейства.</span><span class="sxs-lookup"><span data-stu-id="5729c-535">Hence hello cross product yields 1\*1\*2 = 2 rows from this family.</span></span>

<span data-ttu-id="5729c-536">В следующем примере hello имеется дополнительный фильтр на `pet`.</span><span class="sxs-lookup"><span data-stu-id="5729c-536">In hello next example, there is an additional filter on `pet`.</span></span> <span data-ttu-id="5729c-537">Это исключает все кортежи hello, где имя pet hello не является «Тени».</span><span class="sxs-lookup"><span data-stu-id="5729c-537">This excludes all hello tuples where hello pet name is not "Shadow".</span></span> <span data-ttu-id="5729c-538">Обратите внимание, что мы являются кортежами может toobuild из массивов, фильтр для любого из элементов hello кортежа hello любое сочетание hello элементов проекта.</span><span class="sxs-lookup"><span data-stu-id="5729c-538">Notice that we are able toobuild tuples from arrays, filter on any of hello elements of hello tuple, and project any combination of hello elements.</span></span> 

<span data-ttu-id="5729c-539">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-539">**Query**</span></span>

    SELECT 
        f.id AS familyName,
        c.givenName AS childGivenName,
        c.firstName AS childFirstName,
        p.givenName AS petName 
    FROM Families f 
    JOIN c IN f.children 
    JOIN p IN c.pets
    WHERE p.givenName = "Shadow"

<span data-ttu-id="5729c-540">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-540">**Results**</span></span>

    [
      {
       "familyName": "WakefieldFamily", 
       "childGivenName": "Jesse", 
       "petName": "Shadow"
      }
    ]


## <span data-ttu-id="5729c-541"><a id="JavaScriptIntegration"></a>Интеграция JavaScript</span><span class="sxs-lookup"><span data-stu-id="5729c-541"><a id="JavaScriptIntegration"></a>JavaScript integration</span></span>
<span data-ttu-id="5729c-542">Azure Cosmos DB предоставляет модель программирования для выполнения логики приложения на основе JavaScript непосредственно в коллекциях hello с точки зрения хранимых процедур и триггеров.</span><span class="sxs-lookup"><span data-stu-id="5729c-542">Azure Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections in terms of stored procedures and triggers.</span></span> <span data-ttu-id="5729c-543">Это позволяет:</span><span class="sxs-lookup"><span data-stu-id="5729c-543">This allows for both:</span></span>

* <span data-ttu-id="5729c-544">Транзакционных операций CRUD возможность toodo высокой производительности и запросов к документам в коллекции посредством hello глубокой интеграции среды выполнения JavaScript непосредственно в компонент database engine hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-544">Ability toodo high-performance transactional CRUD operations and queries against documents in a collection by virtue of hello deep integration of JavaScript runtime directly within hello database engine.</span></span> 
* <span data-ttu-id="5729c-545">Добиться естественного моделирования потока управления, областей видимости переменных, присвоения и интеграции обработки исключений примитивов с транзакциями базы данных.</span><span class="sxs-lookup"><span data-stu-id="5729c-545">A natural modeling of control flow, variable scoping, and assignment and integration of exception handling primitives with database transactions.</span></span> <span data-ttu-id="5729c-546">Дополнительные сведения о поддержке Azure Cosmos DB интеграция с JavaScript см. документацию программирования на стороне сервера toohello JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5729c-546">For more details about Azure Cosmos DB support for JavaScript integration, please refer toohello JavaScript server-side programmability documentation.</span></span>

### <span data-ttu-id="5729c-547"><a id="UserDefinedFunctions"></a>Определяемые пользователем функции (UDF)</span><span class="sxs-lookup"><span data-stu-id="5729c-547"><a id="UserDefinedFunctions"></a>User-Defined Functions (UDFs)</span></span>
<span data-ttu-id="5729c-548">Вместе с типами hello уже определен в этой статье DocumentDB API SQL обеспечивает поддержку для пользовательской функции (UDF).</span><span class="sxs-lookup"><span data-stu-id="5729c-548">Along with hello types already defined in this article, DocumentDB API SQL provides support for User Defined Functions (UDF).</span></span> <span data-ttu-id="5729c-549">В частности определяемые пользователем скалярные функции поддерживаются, где разработчики hello можно передавать в ноль или несколько аргументов и возвращают результат обратно один аргумент.</span><span class="sxs-lookup"><span data-stu-id="5729c-549">In particular, scalar UDFs are supported where hello developers can pass in zero or many arguments and return a single argument result back.</span></span> <span data-ttu-id="5729c-550">Каждый из этих аргументов проверяется на соответствие допустимым значениям JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-550">Each of these arguments is checked for being legal JSON values.</span></span>  

<span data-ttu-id="5729c-551">синтаксис DocumentDB API SQL Hello расширяется toosupport настраиваемую прикладную логику, с помощью этих определяемые пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="5729c-551">hello DocumentDB API SQL syntax is extended toosupport custom application logic using these User-Defined Functions.</span></span> <span data-ttu-id="5729c-552">Пользовательские функции могут быть зарегистрированы в API DocumentDB, а затем на них можно ссылаться как на часть SQL-запроса.</span><span class="sxs-lookup"><span data-stu-id="5729c-552">UDFs can be registered with DocumentDB API and then be referenced as part of a SQL query.</span></span> <span data-ttu-id="5729c-553">На самом деле hello exquisitely представляют UDFs предназначены toobe вызывается по запросам.</span><span class="sxs-lookup"><span data-stu-id="5729c-553">In fact, hello UDFs are exquisitely designed toobe invoked by queries.</span></span> <span data-ttu-id="5729c-554">Как следствие toothis выбора, определяемые пользователем функции не имеют доступа к toohello контекста объекта Здравствуйте, других JavaScript имеют типы (хранимые процедуры и триггеры).</span><span class="sxs-lookup"><span data-stu-id="5729c-554">As a corollary toothis choice, UDFs do not have access toohello context object which hello other JavaScript types (stored procedures and triggers) have.</span></span> <span data-ttu-id="5729c-555">Поскольку запросы выполняются только для чтения, они могут работать как на первичной, так на вторичной репликах.</span><span class="sxs-lookup"><span data-stu-id="5729c-555">Since queries execute as read-only, they can run either on primary or on secondary replicas.</span></span> <span data-ttu-id="5729c-556">Таким образом определяемые пользователем функции, разработанные toorun во вторичных репликах, в отличие от других типов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5729c-556">Therefore, UDFs are designed toorun on secondary replicas unlike other JavaScript types.</span></span>

<span data-ttu-id="5729c-557">Ниже приведен пример как определяемой пользователем функции могут быть зарегистрированы в базе данных Cosmos DB hello, в частности в коллекции документов.</span><span class="sxs-lookup"><span data-stu-id="5729c-557">Below is an example of how a UDF can be registered at hello Cosmos DB database, specifically under a document collection.</span></span>

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

<span data-ttu-id="5729c-558">Hello предыдущий пример создает определяемую пользователем Функцию с именем `REGEX_MATCH`.</span><span class="sxs-lookup"><span data-stu-id="5729c-558">hello preceding example creates a UDF whose name is `REGEX_MATCH`.</span></span> <span data-ttu-id="5729c-559">Он принимает два строковых значения JSON `input` и `pattern` и проверяет, не указан шаблон hello в первые совпадения hello Здравствуйте, во-вторых, с помощью функции string.match() языка JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5729c-559">It accepts two JSON string values `input` and `pattern` and checks if hello first matches hello pattern specified in hello second using JavaScript's string.match() function.</span></span>

<span data-ttu-id="5729c-560">Теперь мы можем использовать эту определяемую пользователем функцию в запросе в проекции.</span><span class="sxs-lookup"><span data-stu-id="5729c-560">We can now use this UDF in a query in a projection.</span></span> <span data-ttu-id="5729c-561">Определяемые пользователем функции должны быть дополнены hello с учетом регистра префикс «udf.»</span><span class="sxs-lookup"><span data-stu-id="5729c-561">UDFs must be qualified with hello case-sensitive prefix "udf."</span></span> <span data-ttu-id="5729c-562">с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="5729c-562">when called from within queries.</span></span> 

> [!NOTE]
> <span data-ttu-id="5729c-563">Предыдущий too3/17/2015, Cosmos DB поддерживаются вызовы определяемых пользователем Функций без hello «udf.»</span><span class="sxs-lookup"><span data-stu-id="5729c-563">Prior too3/17/2015, Cosmos DB supported UDF calls without hello "udf."</span></span> <span data-ttu-id="5729c-564">например SELECT REGEX_MATCH().</span><span class="sxs-lookup"><span data-stu-id="5729c-564">prefix like SELECT REGEX_MATCH().</span></span> <span data-ttu-id="5729c-565">Теперь этот метод выполнения вызовов устарел.</span><span class="sxs-lookup"><span data-stu-id="5729c-565">This calling pattern has been deprecated.</span></span>  
> 
> 

<span data-ttu-id="5729c-566">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-566">**Query**</span></span>

    SELECT udf.REGEX_MATCH(Families.address.city, ".*eattle")
    FROM Families

<span data-ttu-id="5729c-567">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-567">**Results**</span></span>

    [
      {
        "$1": true
      }, 
      {
        "$1": false
      }
    ]

<span data-ttu-id="5729c-568">Hello определяемой пользователем функции также может использоваться внутри фильтра, как показано в hello приведенном ниже примере также дополнены hello «udf.»</span><span class="sxs-lookup"><span data-stu-id="5729c-568">hello UDF can also be used inside a filter as shown in hello example below, also qualified with hello "udf."</span></span> <span data-ttu-id="5729c-569">как показано в примере ниже.</span><span class="sxs-lookup"><span data-stu-id="5729c-569">prefix:</span></span>

<span data-ttu-id="5729c-570">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-570">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE udf.REGEX_MATCH(Families.address.city, ".*eattle")

<span data-ttu-id="5729c-571">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-571">**Results**</span></span>

    [{
        "id": "AndersenFamily",
        "city": "Seattle"
    }]


<span data-ttu-id="5729c-572">В сущности, определяемые пользователем функции являются корректными скалярными выражениями и могут быть использованы в проекциях и фильтрах.</span><span class="sxs-lookup"><span data-stu-id="5729c-572">In essence, UDFs are valid scalar expressions and can be used in both projections and filters.</span></span> 

<span data-ttu-id="5729c-573">tooexpand на степень hello определяемых пользователем функций, давайте рассмотрим другой пример с условной логики:</span><span class="sxs-lookup"><span data-stu-id="5729c-573">tooexpand on hello power of UDFs, let's look at another example with conditional logic:</span></span>

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


<span data-ttu-id="5729c-574">Ниже приведен пример hello, упражнения определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="5729c-574">Below is an example that exercises hello UDF.</span></span>

<span data-ttu-id="5729c-575">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-575">**Query**</span></span>

    SELECT f.address.city, udf.SEALEVEL(f.address.city) AS seaLevel
    FROM Families f    

<span data-ttu-id="5729c-576">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-576">**Results**</span></span>

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


<span data-ttu-id="5729c-577">Как hello предыдущей демонстрации примеры, определяемые пользователем функции интегрировать power hello языка JavaScript tooprovide DocumentDB API SQL hello форматированного программируемый интерфейс toodo сложную процедурных, условного логику с помощью hello встроенных среды выполнения JavaScript возможности.</span><span class="sxs-lookup"><span data-stu-id="5729c-577">As hello preceding examples showcase, UDFs integrate hello power of JavaScript language with hello DocumentDB API SQL tooprovide a rich programmable interface toodo complex procedural, conditional logic with hello help of inbuilt JavaScript runtime capabilities.</span></span>

<span data-ttu-id="5729c-578">DocumentDB API SQL аргументы hello toohello определяемых пользователем функций для каждого документа в источнике hello по использованию hello текущую стадию (предложение WHERE или предложение SELECT) обработки hello определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="5729c-578">DocumentDB API SQL provides hello arguments toohello UDFs for each document in hello source at hello current stage (WHERE clause or SELECT clause) of processing hello UDF.</span></span> <span data-ttu-id="5729c-579">Hello результат будет включено в легко hello общую конвейерной обработки.</span><span class="sxs-lookup"><span data-stu-id="5729c-579">hello result is incorporated in hello overall execution pipeline seamlessly.</span></span> <span data-ttu-id="5729c-580">Если ссылка tooby hello UDF параметры недоступны в hello значение JSON hello, параметр считается свойства hello не определено и поэтому hello полностью пропускается вызова определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="5729c-580">If hello properties referred tooby hello UDF parameters are not available in hello JSON value, hello parameter is considered as undefined and hence hello UDF invocation is entirely skipped.</span></span> <span data-ttu-id="5729c-581">Аналогично, если результат hello hello определяемой пользователем функции не определен, он не включается в результат hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-581">Similarly if hello result of hello UDF is undefined, it's not included in hello result.</span></span> 

<span data-ttu-id="5729c-582">Таким образом определяемые пользователем функции являются значительные средства toodo сложной бизнес-логики как часть запроса hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-582">In summary, UDFs are great tools toodo complex business logic as part of hello query.</span></span>

### <a name="operator-evaluation"></a><span data-ttu-id="5729c-583">Оценивание операторов</span><span class="sxs-lookup"><span data-stu-id="5729c-583">Operator evaluation</span></span>
<span data-ttu-id="5729c-584">Cosmos база данных с тем hello того, что базы данных JSON, рисование parallels с операторами JavaScript и его семантику оценки.</span><span class="sxs-lookup"><span data-stu-id="5729c-584">Cosmos DB, by hello virtue of being a JSON database, draws parallels with JavaScript operators and its evaluation semantics.</span></span> <span data-ttu-id="5729c-585">Время Cosmos DB семантики JavaScript toopreserve с точки зрения поддержки JSON, в некоторых случаях отличается hello операцию вычисления.</span><span class="sxs-lookup"><span data-stu-id="5729c-585">While Cosmos DB tries toopreserve JavaScript semantics in terms of JSON support, hello operation evaluation deviates in some instances.</span></span>

<span data-ttu-id="5729c-586">В API SQL DocumentDB в отличие от традиционных SQL, hello типы значений часто неизвестны до hello значения извлекаются из базы данных.</span><span class="sxs-lookup"><span data-stu-id="5729c-586">In DocumentDB API SQL, unlike in traditional SQL, hello types of values are often not known until hello values are retrieved from database.</span></span> <span data-ttu-id="5729c-587">В tooefficiently порядок выполнения запросов, большинство hello операторов имеют строгие требования к типам.</span><span class="sxs-lookup"><span data-stu-id="5729c-587">In order tooefficiently execute queries, most of hello operators have strict type requirements.</span></span> 

<span data-ttu-id="5729c-588">SQL в API DocumentDB не выполняет неявные преобразования, в отличие от JavaScript.</span><span class="sxs-lookup"><span data-stu-id="5729c-588">DocumentDB API SQL doesn't perform implicit conversions, unlike JavaScript.</span></span> <span data-ttu-id="5729c-589">Например, запрос `SELECT * FROM Person p WHERE p.Age = 21` соответствует документам, которые содержат свойство "Возраст" со значением 21.</span><span class="sxs-lookup"><span data-stu-id="5729c-589">For instance, a query like `SELECT * FROM Person p WHERE p.Age = 21` matches documents that contain an Age property whose value is 21.</span></span> <span data-ttu-id="5729c-590">Любой документ, свойство "возраст" в котором равно строке "21" или другим вариациям, таким как "021", "21.0", "0021", "00021" и т. д. не будут возвращены.</span><span class="sxs-lookup"><span data-stu-id="5729c-590">Any other document whose Age property matches string "21", or other possibly infinite variations like "021", "21.0", "0021", "00021", etc. will not be matched.</span></span> <span data-ttu-id="5729c-591">Это напротив toohello JavaScript, где hello строковые значения, неявно приведен toonumbers (зависимости от оператора, например: ==).</span><span class="sxs-lookup"><span data-stu-id="5729c-591">This is in contrast toohello JavaScript where hello string values are implicitly casted toonumbers (based on operator, ex: ==).</span></span> <span data-ttu-id="5729c-592">Этот выбор имеет решающее значение для эффективного согласования индексов в SQL API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="5729c-592">This choice is crucial for efficient index matching in DocumentDB API SQL.</span></span> 

## <a name="parameterized-sql-queries"></a><span data-ttu-id="5729c-593">Параметризованные SQL-запросы</span><span class="sxs-lookup"><span data-stu-id="5729c-593">Parameterized SQL queries</span></span>
<span data-ttu-id="5729c-594">Cosmos DB поддерживают запросы с параметрами, в соответствии со знаком нотацию @ hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-594">Cosmos DB supports queries with parameters expressed with hello familiar @ notation.</span></span> <span data-ttu-id="5729c-595">Параметризованный SQL обеспечивает надежную обработку и экранирование пользовательского ввода, предотвращая случайное раскрытие данных через внедрение кода SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-595">Parameterized SQL provides robust handling and escaping of user input, preventing accidental exposure of data through SQL injection.</span></span> 

<span data-ttu-id="5729c-596">Например, можно написать запрос, который принимает в качестве параметров фамилию и состояние адреса, а затем выполнить его для различных значений параметров фамилия и состояние адреса на основе ввода пользователя.</span><span class="sxs-lookup"><span data-stu-id="5729c-596">For example, you can write a query that takes last name and address state as parameters, and then execute it for various values of last name and address state based on user input.</span></span>

    SELECT * 
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState

<span data-ttu-id="5729c-597">Этот запрос можно затем отправить tooCosmos DB как параметризованный запрос JSON, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5729c-597">This request can then be sent tooCosmos DB as a parameterized JSON query like shown below.</span></span>

    {      
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",     
        "parameters": [          
            {"name": "@lastName", "value": "Wakefield"},         
            {"name": "@addressState", "value": "NY"},           
        ] 
    }

<span data-ttu-id="5729c-598">Аргумент tooTOP Hello можно задать использование параметризованных запросов, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5729c-598">hello argument tooTOP can be set using parameterized queries like shown below.</span></span>

    {      
        "query": "SELECT TOP @n * FROM Families",     
        "parameters": [          
            {"name": "@n", "value": 10},         
        ] 
    }

<span data-ttu-id="5729c-599">Значениями параметров могут быть любые допустимые JSON (строки, числа, логические значения, значения null, даже массивы или вложенные JSON).</span><span class="sxs-lookup"><span data-stu-id="5729c-599">Parameter values can be any valid JSON (strings, numbers, Booleans, null, even arrays or nested JSON).</span></span> <span data-ttu-id="5729c-600">Кроме этого, так как Cosmos DB не имеет схемы, параметры не проверяются на соответствие типам.</span><span class="sxs-lookup"><span data-stu-id="5729c-600">Also since Cosmos DB is schema-less, parameters are not validated against any type.</span></span>

## <span data-ttu-id="5729c-601"><a id="BuiltinFunctions"></a>Встроенные функции</span><span class="sxs-lookup"><span data-stu-id="5729c-601"><a id="BuiltinFunctions"></a>Built-in functions</span></span>
<span data-ttu-id="5729c-602">Cosmos DB также поддерживает несколько встроенных функций для общих операций, которые можно использовать в запросах как определяемые пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="5729c-602">Cosmos DB also supports a number of built-in functions for common operations, that can be used inside queries like user-defined functions (UDFs).</span></span>

| <span data-ttu-id="5729c-603">Группа функций</span><span class="sxs-lookup"><span data-stu-id="5729c-603">Function group</span></span>          | <span data-ttu-id="5729c-604">Операции</span><span class="sxs-lookup"><span data-stu-id="5729c-604">Operations</span></span>                                                                                                                                          |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5729c-605">Математические функции</span><span class="sxs-lookup"><span data-stu-id="5729c-605">Mathematical functions</span></span>  | <span data-ttu-id="5729c-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN и TAN</span><span class="sxs-lookup"><span data-stu-id="5729c-606">ABS, CEILING, EXP, FLOOR, LOG, LOG10, POWER, ROUND, SIGN, SQRT, SQUARE, TRUNC, ACOS, ASIN, ATAN, ATN2, COS, COT, DEGREES, PI, RADIANS, SIN, and TAN</span></span> |
| <span data-ttu-id="5729c-607">Функции проверки типа</span><span class="sxs-lookup"><span data-stu-id="5729c-607">Type checking functions</span></span> | <span data-ttu-id="5729c-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED и IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="5729c-608">IS_ARRAY, IS_BOOL, IS_NULL, IS_NUMBER, IS_OBJECT, IS_STRING, IS_DEFINED, and IS_PRIMITIVE</span></span>                                                           |
| <span data-ttu-id="5729c-609">Строковые функции</span><span class="sxs-lookup"><span data-stu-id="5729c-609">String functions</span></span>        | <span data-ttu-id="5729c-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING и UPPER</span><span class="sxs-lookup"><span data-stu-id="5729c-610">CONCAT, CONTAINS, ENDSWITH, INDEX_OF, LEFT, LENGTH, LOWER, LTRIM, REPLACE, REPLICATE, REVERSE, RIGHT, RTRIM, STARTSWITH, SUBSTRING, and UPPER</span></span>       |
| <span data-ttu-id="5729c-611">Функции массивов</span><span class="sxs-lookup"><span data-stu-id="5729c-611">Array functions</span></span>         | <span data-ttu-id="5729c-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH и ARRAY_SLICE</span><span class="sxs-lookup"><span data-stu-id="5729c-612">ARRAY_CONCAT, ARRAY_CONTAINS, ARRAY_LENGTH, and ARRAY_SLICE</span></span>                                                                                         |
| <span data-ttu-id="5729c-613">Пространственные функции</span><span class="sxs-lookup"><span data-stu-id="5729c-613">Spatial functions</span></span>       | <span data-ttu-id="5729c-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID и ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="5729c-614">ST_DISTANCE, ST_WITHIN, ST_INTERSECTS, ST_ISVALID, and ST_ISVALIDDETAILED</span></span>                                                                           | 

<span data-ttu-id="5729c-615">Если вы используете определяемой пользователем функции (UDF) для которого доступна встроенной функции, соответствующей встроенной функции hello следует использовать как он будет быстрее toorun toobe и многое другое эффективно.</span><span class="sxs-lookup"><span data-stu-id="5729c-615">If you’re currently using a user-defined function (UDF) for which a built-in function is now available, you should use hello corresponding built-in function as it is going toobe quicker toorun and more efficiently.</span></span> 

### <a name="mathematical-functions"></a><span data-ttu-id="5729c-616">Математические функции</span><span class="sxs-lookup"><span data-stu-id="5729c-616">Mathematical functions</span></span>
<span data-ttu-id="5729c-617">Hello математические функции производят вычисления, основанные на числовых значениях, заданных в качестве аргументов и возвращают числовое значение.</span><span class="sxs-lookup"><span data-stu-id="5729c-617">hello mathematical functions each perform a calculation, based on input values that are provided as arguments, and return a numeric value.</span></span> <span data-ttu-id="5729c-618">Здесь приведен список поддерживаемых встроенных математических функций.</span><span class="sxs-lookup"><span data-stu-id="5729c-618">Here’s a table of supported built-in mathematical functions.</span></span>


| <span data-ttu-id="5729c-619">Использование</span><span class="sxs-lookup"><span data-stu-id="5729c-619">Usage</span></span> | <span data-ttu-id="5729c-620">Описание</span><span class="sxs-lookup"><span data-stu-id="5729c-620">Description</span></span> |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5729c-621">[[ABS (num_expr)](#bk_abs)</span><span class="sxs-lookup"><span data-stu-id="5729c-621">[[ABS (num_expr)](#bk_abs)</span></span> | <span data-ttu-id="5729c-622">Возвращает hello абсолютное (положительное) значение hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-622">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="5729c-623">CEILING (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-623">CEILING (num_expr)</span></span>](#bk_ceiling) | <span data-ttu-id="5729c-624">Возвращает hello наименьшее целочисленное значение больше или равно, hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-624">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| [<span data-ttu-id="5729c-625">FLOOR (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-625">FLOOR (num_expr)</span></span>](#bk_floor) | <span data-ttu-id="5729c-626">Возвращает наибольшее целое число hello меньше или равно toohello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-626">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| [<span data-ttu-id="5729c-627">EXP (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-627">EXP (num_expr)</span></span>](#bk_exp) | <span data-ttu-id="5729c-628">Возвращает экспоненты hello hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-628">Returns hello exponent of hello specified numeric expression.</span></span> |
| <span data-ttu-id="5729c-629">[LOG (num_expr [,base])](#bk_log)</span><span class="sxs-lookup"><span data-stu-id="5729c-629">[LOG (num_expr [,base])](#bk_log)</span></span> | <span data-ttu-id="5729c-630">Возвращает hello натуральный логарифм hello указаны числовое выражение, или с помощью hello логарифм hello базы</span><span class="sxs-lookup"><span data-stu-id="5729c-630">Returns hello natural logarithm of hello specified numeric expression, or hello logarithm using hello specified base</span></span> |
| [<span data-ttu-id="5729c-631">LOG10 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-631">LOG10 (num_expr)</span></span>](#bk_log10) | <span data-ttu-id="5729c-632">Возвращает hello по основанию 10 логарифмической значение hello заданное числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="5729c-632">Returns hello base-10 logarithmic value of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="5729c-633">ROUND (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-633">ROUND (num_expr)</span></span>](#bk_round) | <span data-ttu-id="5729c-634">Возвращает числовое значение, округленное toohello ближайшего целого значения.</span><span class="sxs-lookup"><span data-stu-id="5729c-634">Returns a numeric value, rounded toohello closest integer value.</span></span> |
| [<span data-ttu-id="5729c-635">TRUNC (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-635">TRUNC (num_expr)</span></span>](#bk_trunc) | <span data-ttu-id="5729c-636">Возвращает числовое значение, усеченное toohello ближайшего целого значения.</span><span class="sxs-lookup"><span data-stu-id="5729c-636">Returns a numeric value, truncated toohello closest integer value.</span></span> |
| [<span data-ttu-id="5729c-637">SQRT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-637">SQRT (num_expr)</span></span>](#bk_sqrt) | <span data-ttu-id="5729c-638">Возвращает hello квадратный корень из hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-638">Returns hello square root of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="5729c-639">SQUARE (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-639">SQUARE (num_expr)</span></span>](#bk_square) | <span data-ttu-id="5729c-640">Hello возвращает квадрат для hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-640">Returns hello square of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="5729c-641">POWER (num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-641">POWER (num_expr, num_expr)</span></span>](#bk_power) | <span data-ttu-id="5729c-642">Возвращает степень hello hello указан toohello значение числового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-642">Returns hello power of hello specified numeric expression toohello value specified.</span></span> |
| [<span data-ttu-id="5729c-643">SIGN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-643">SIGN (num_expr)</span></span>](#bk_sign) | <span data-ttu-id="5729c-644">Возвращает hello знак (-1, 0, 1) hello указано нулевое значение числового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-644">Returns hello sign value (-1, 0, 1) of hello specified numeric expression.</span></span> |
| [<span data-ttu-id="5729c-645">ACOS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-645">ACOS (num_expr)</span></span>](#bk_acos) | <span data-ttu-id="5729c-646">Возвращает hello угол в радианах, косинус которого является hello указанного числового выражения; также называется арккосинусом.</span><span class="sxs-lookup"><span data-stu-id="5729c-646">Returns hello angle, in radians, whose cosine is hello specified numeric expression; also called arccosine.</span></span> |
| [<span data-ttu-id="5729c-647">ASIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-647">ASIN (num_expr)</span></span>](#bk_asin) | <span data-ttu-id="5729c-648">Hello Возвращает угол в радианах, синус которого равен hello указано числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="5729c-648">Returns hello angle, in radians, whose sine is hello specified numeric expression.</span></span> <span data-ttu-id="5729c-649">Также называется арксинусом.</span><span class="sxs-lookup"><span data-stu-id="5729c-649">This is also called arcsine.</span></span> |
| [<span data-ttu-id="5729c-650">ATAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-650">ATAN (num_expr)</span></span>](#bk_atan) | <span data-ttu-id="5729c-651">Hello Возвращает угол в радианах, тангенс которого равен hello указано числовое выражение.</span><span class="sxs-lookup"><span data-stu-id="5729c-651">Returns hello angle, in radians, whose tangent is hello specified numeric expression.</span></span> <span data-ttu-id="5729c-652">Также называется арктангенсом.</span><span class="sxs-lookup"><span data-stu-id="5729c-652">This is also called arctangent.</span></span> |
| [<span data-ttu-id="5729c-653">ATN2 (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-653">ATN2 (num_expr)</span></span>](#bk_atn2) | <span data-ttu-id="5729c-654">Возвращает hello угол в радианах между положительным направлением оси x hello и hello лучом, проведенным из hello toohello координат (y, x), где x и y являются значениями hello hello два числа с плавающей выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-654">Returns hello angle, in radians, between hello positive x-axis and hello ray from hello origin toohello point (y, x), where x and y are hello values of hello two specified float expressions.</span></span> |
| [<span data-ttu-id="5729c-655">COS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-655">COS (num_expr)</span></span>](#bk_cos) | <span data-ttu-id="5729c-656">Возвращает hello hello в тригонометрический косинус указанного угла в радианах, в hello указанного выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-656">Returns hello trigonometric cosine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="5729c-657">COT (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-657">COT (num_expr)</span></span>](#bk_cot) | <span data-ttu-id="5729c-658">Возвращает hello hello в тригонометрический котангенс указанного угла в радианах, в hello указанного числового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-658">Returns hello trigonometric cotangent of hello specified angle, in radians, in hello specified numeric expression.</span></span> |
| [<span data-ttu-id="5729c-659">DEGREES (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-659">DEGREES (num_expr)</span></span>](#bk_degrees) | <span data-ttu-id="5729c-660">Возвращает hello соответствующее значение угла в градусах для значения угла в радианах.</span><span class="sxs-lookup"><span data-stu-id="5729c-660">Returns hello corresponding angle in degrees for an angle specified in radians.</span></span> |
| [<span data-ttu-id="5729c-661">PI ()</span><span class="sxs-lookup"><span data-stu-id="5729c-661">PI ()</span></span>](#bk_pi) | <span data-ttu-id="5729c-662">Возвращает hello константное значение PI.</span><span class="sxs-lookup"><span data-stu-id="5729c-662">Returns hello constant value of PI.</span></span> |
| [<span data-ttu-id="5729c-663">RADIANS (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-663">RADIANS (num_expr)</span></span>](#bk_radians) | <span data-ttu-id="5729c-664">Возвращает значение угла в радианах для числового значения, указанного в градусах.</span><span class="sxs-lookup"><span data-stu-id="5729c-664">Returns radians when a numeric expression, in degrees, is entered.</span></span> |
| [<span data-ttu-id="5729c-665">SIN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-665">SIN (num_expr)</span></span>](#bk_sin) | <span data-ttu-id="5729c-666">Возвращает hello hello в Тригонометрический синус указанного угла в радианах, в hello указанное выражение.</span><span class="sxs-lookup"><span data-stu-id="5729c-666">Returns hello trigonometric sine of hello specified angle, in radians, in hello specified expression.</span></span> |
| [<span data-ttu-id="5729c-667">TAN (num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-667">TAN (num_expr)</span></span>](#bk_tan) | <span data-ttu-id="5729c-668">Возвращает тангенс hello входное выражение hello в hello указанном выражении.</span><span class="sxs-lookup"><span data-stu-id="5729c-668">Returns hello tangent of hello input expression, in hello specified expression.</span></span> |

<span data-ttu-id="5729c-669">Например теперь можно запускать запросы hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5729c-669">For example, you can now run queries like hello following:</span></span>

<span data-ttu-id="5729c-670">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-670">**Query**</span></span>

    SELECT VALUE ABS(-4)

<span data-ttu-id="5729c-671">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-671">**Results**</span></span>

    [4]

<span data-ttu-id="5729c-672">Hello основное различие между tooANSI функций по сравнению Cosmos DB SQL является они спроектированный toowork с данные без схемы, так и схемы.</span><span class="sxs-lookup"><span data-stu-id="5729c-672">hello main difference between Cosmos DB’s functions compared tooANSI SQL is that they are designed toowork well with schema-less and mixed schema data.</span></span> <span data-ttu-id="5729c-673">Например при наличии документа, где свойство размера hello отсутствует или имеет нечисловое значение, например «неизвестно», а затем hello документов пропускается, вместо возвращения ошибки.</span><span class="sxs-lookup"><span data-stu-id="5729c-673">For example, if you have a document where hello Size property is missing, or has a non-numeric value like “unknown”, then hello document is skipped over, instead of returning an error.</span></span>

### <a name="type-checking-functions"></a><span data-ttu-id="5729c-674">Функции проверки типа</span><span class="sxs-lookup"><span data-stu-id="5729c-674">Type checking functions</span></span>
<span data-ttu-id="5729c-675">функции проверки типа Hello разрешить toocheck hello тип выражения в запросах SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-675">hello type checking functions allow you toocheck hello type of an expression within SQL queries.</span></span> <span data-ttu-id="5729c-676">Тип может иметь функции проверки используется тип hello toodetermine свойств в документах на лету hello, когда переменная или неизвестный.</span><span class="sxs-lookup"><span data-stu-id="5729c-676">Type checking functions can be used toodetermine hello type of properties within documents on hello fly when it is variable or unknown.</span></span> <span data-ttu-id="5729c-677">Здесь приведен список поддерживаемых встроенных функций проверки типа.</span><span class="sxs-lookup"><span data-stu-id="5729c-677">Here’s a table of supported built-in type checking functions.</span></span>

<table>
<tr>
  <td><span data-ttu-id="5729c-678"><strong>Использование</strong></span><span class="sxs-lookup"><span data-stu-id="5729c-678"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="5729c-679"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="5729c-679"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span><span class="sxs-lookup"><span data-stu-id="5729c-680"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_array">IS_ARRAY (expr)</a></span></span></td>
  <td><span data-ttu-id="5729c-681">Возвращает логическое значение, указывающее, если тип hello hello значения массива.</span><span class="sxs-lookup"><span data-stu-id="5729c-681">Returns a Boolean indicating if hello type of hello value is an array.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="5729c-682"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_bool">IS_BOOL (expr)</a></span></span></td>
  <td><span data-ttu-id="5729c-683">Возвращает логическое значение, указывающее, если тип hello значения hello логическое значение.</span><span class="sxs-lookup"><span data-stu-id="5729c-683">Returns a Boolean indicating if hello type of hello value is a Boolean.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span><span class="sxs-lookup"><span data-stu-id="5729c-684"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_null">IS_NULL (expr)</a></span></span></td>
  <td><span data-ttu-id="5729c-685">Возвращает логическое значение, указывающее, если тип hello hello значения null.</span><span class="sxs-lookup"><span data-stu-id="5729c-685">Returns a Boolean indicating if hello type of hello value is null.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span><span class="sxs-lookup"><span data-stu-id="5729c-686"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_number">IS_NUMBER (expr)</a></span></span></td>
  <td><span data-ttu-id="5729c-687">Возвращает логическое значение, указывающее, если тип hello hello значение является числом.</span><span class="sxs-lookup"><span data-stu-id="5729c-687">Returns a Boolean indicating if hello type of hello value is a number.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span><span class="sxs-lookup"><span data-stu-id="5729c-688"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_object">IS_OBJECT (expr)</a></span></span></td>
  <td><span data-ttu-id="5729c-689">Возвращает логическое значение, указывающее, если тип hello значения hello объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-689">Returns a Boolean indicating if hello type of hello value is a JSON object.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span><span class="sxs-lookup"><span data-stu-id="5729c-690"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_string">IS_STRING (expr)</a></span></span></td>
  <td><span data-ttu-id="5729c-691">Возвращает логическое значение, указывающее, если тип hello hello значение является строкой.</span><span class="sxs-lookup"><span data-stu-id="5729c-691">Returns a Boolean indicating if hello type of hello value is a string.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span><span class="sxs-lookup"><span data-stu-id="5729c-692"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_defined">IS_DEFINED (expr)</a></span></span></td>
  <td><span data-ttu-id="5729c-693">Возвращает логическое значение, указывающее, если свойство hello назначено значение.</span><span class="sxs-lookup"><span data-stu-id="5729c-693">Returns a Boolean indicating if hello property has been assigned a value.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span><span class="sxs-lookup"><span data-stu-id="5729c-694"><a href="https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_is_primitive">IS_PRIMITIVE (expr)</a></span></span></td>
  <td><span data-ttu-id="5729c-695">Возвращает логическое значение, указывающее, если тип hello значения hello является строка, число, логическое значение или значение null.</span><span class="sxs-lookup"><span data-stu-id="5729c-695">Returns a Boolean indicating if hello type of hello value is a string, number, Boolean or null.</span></span></td>
</tr>

</table>

<span data-ttu-id="5729c-696">Используя эти функции, теперь можно выполнить запросы hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5729c-696">Using these functions, you can now run queries like hello following:</span></span>

<span data-ttu-id="5729c-697">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-697">**Query**</span></span>

    SELECT VALUE IS_NUMBER(-4)

<span data-ttu-id="5729c-698">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-698">**Results**</span></span>

    [true]

### <a name="string-functions"></a><span data-ttu-id="5729c-699">Строковые функции</span><span class="sxs-lookup"><span data-stu-id="5729c-699">String functions</span></span>
<span data-ttu-id="5729c-700">Hello следующие скалярные функции выполняют операцию над входным строковым значением и возвращают строковое, числовое или логическое значение.</span><span class="sxs-lookup"><span data-stu-id="5729c-700">hello following scalar functions perform an operation on a string input value and return a string, numeric or Boolean value.</span></span> <span data-ttu-id="5729c-701">Ниже приведена таблица встроенных строковых функций:</span><span class="sxs-lookup"><span data-stu-id="5729c-701">Here's a table of built-in string functions:</span></span>

| <span data-ttu-id="5729c-702">Использование</span><span class="sxs-lookup"><span data-stu-id="5729c-702">Usage</span></span> | <span data-ttu-id="5729c-703">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="5729c-703">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="5729c-704">LENGTH (str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-704">LENGTH (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_length) |<span data-ttu-id="5729c-705">Количество символов для hello hello возвращает указанного строкового выражения</span><span class="sxs-lookup"><span data-stu-id="5729c-705">Returns hello number of characters of hello specified string expression</span></span> |
| <span data-ttu-id="5729c-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span><span class="sxs-lookup"><span data-stu-id="5729c-706">[CONCAT (str_expr, str_expr [, str_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_concat)</span></span> |<span data-ttu-id="5729c-707">Возвращает строку, являющуюся результатом объединения двух или более строковых значений hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-707">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| [<span data-ttu-id="5729c-708">SUBSTRING (str_expr, num_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-708">SUBSTRING (str_expr, num_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_substring) |<span data-ttu-id="5729c-709">Возвращает часть строкового выражения.</span><span class="sxs-lookup"><span data-stu-id="5729c-709">Returns part of a string expression.</span></span> |
| [<span data-ttu-id="5729c-710">STARTSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-710">STARTSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_startswith) |<span data-ttu-id="5729c-711">Возвращает логическое значение, указывающее, было ли первое строковое выражение hello заканчивается hello второй</span><span class="sxs-lookup"><span data-stu-id="5729c-711">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="5729c-712">ENDSWITH (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-712">ENDSWITH (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_endswith) |<span data-ttu-id="5729c-713">Возвращает логическое значение, указывающее, было ли первое строковое выражение hello заканчивается hello второй</span><span class="sxs-lookup"><span data-stu-id="5729c-713">Returns a Boolean indicating whether hello first string expression ends with hello second</span></span> |
| [<span data-ttu-id="5729c-714">CONTAINS (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-714">CONTAINS (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_contains) |<span data-ttu-id="5729c-715">Возвращает логическое значение, указывающее, является ли hello первое строковое выражение содержит hello второй.</span><span class="sxs-lookup"><span data-stu-id="5729c-715">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |
| [<span data-ttu-id="5729c-716">INDEX_OF (str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-716">INDEX_OF (str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_index_of) |<span data-ttu-id="5729c-717">Возвращает hello, начальная позиция первого вхождения hello hello второго строкового выражения внутри первого указанного строкового выражения hello, или значение -1, если строка hello не найдена.</span><span class="sxs-lookup"><span data-stu-id="5729c-717">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span> |
| [<span data-ttu-id="5729c-718">LEFT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-718">LEFT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_left) |<span data-ttu-id="5729c-719">Возвращает hello левую часть строки с hello указанное число символов.</span><span class="sxs-lookup"><span data-stu-id="5729c-719">Returns hello left part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="5729c-720">RIGHT (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-720">RIGHT (str_expr, num_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_right) |<span data-ttu-id="5729c-721">Возвращает hello правой части строки с hello указанное число символов.</span><span class="sxs-lookup"><span data-stu-id="5729c-721">Returns hello right part of a string with hello specified number of characters.</span></span> |
| [<span data-ttu-id="5729c-722">LTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-722">LTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_ltrim) |<span data-ttu-id="5729c-723">Возвращает строковое выражение после удаления начальных пробелов.</span><span class="sxs-lookup"><span data-stu-id="5729c-723">Returns a string expression after it removes leading blanks.</span></span> |
| [<span data-ttu-id="5729c-724">RTRIM (str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-724">RTRIM (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_rtrim) |<span data-ttu-id="5729c-725">Возвращает строковое выражение после усечения всех конечных пробелов.</span><span class="sxs-lookup"><span data-stu-id="5729c-725">Returns a string expression after truncating all trailing blanks.</span></span> |
| [<span data-ttu-id="5729c-726">LOWER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-726">LOWER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_lower) |<span data-ttu-id="5729c-727">Возвращает строковое выражение после преобразования данных toolowercase символ верхнего регистра.</span><span class="sxs-lookup"><span data-stu-id="5729c-727">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| [<span data-ttu-id="5729c-728">UPPER (str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-728">UPPER (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_upper) |<span data-ttu-id="5729c-729">Возвращает строковое выражение после преобразования данных toouppercase строчные буквы.</span><span class="sxs-lookup"><span data-stu-id="5729c-729">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| [<span data-ttu-id="5729c-730">REPLACE (str_expr, str_expr, str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-730">REPLACE (str_expr, str_expr, str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_replace) |<span data-ttu-id="5729c-731">Заменяет все вхождения указанного строкового значения другим строковым значением.</span><span class="sxs-lookup"><span data-stu-id="5729c-731">Replaces all occurrences of a specified string value with another string value.</span></span> |
| [<span data-ttu-id="5729c-732">REPLICATE (str_expr, num_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-732">REPLICATE (str_expr, num_expr)</span></span>](https://docs.microsoft.com/azure/cosmos-db/documentdb-sql-query-reference#bk_replicate) |<span data-ttu-id="5729c-733">Повторяет строковое значение указанное число раз.</span><span class="sxs-lookup"><span data-stu-id="5729c-733">Repeats a string value a specified number of times.</span></span> |
| [<span data-ttu-id="5729c-734">REVERSE (str_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-734">REVERSE (str_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_reverse) |<span data-ttu-id="5729c-735">Возвращает hello строковое значение в обратном порядке.</span><span class="sxs-lookup"><span data-stu-id="5729c-735">Returns hello reverse order of a string value.</span></span> |

<span data-ttu-id="5729c-736">Используя эти функции, теперь можно запустить запросы hello следующим образом.</span><span class="sxs-lookup"><span data-stu-id="5729c-736">Using these functions, you can now run queries like hello following.</span></span> <span data-ttu-id="5729c-737">Например можно получить имя семейства hello в верхнем регистре следующим образом:</span><span class="sxs-lookup"><span data-stu-id="5729c-737">For example, you can return hello family name in uppercase as follows:</span></span>

<span data-ttu-id="5729c-738">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-738">**Query**</span></span>

    SELECT VALUE UPPER(Families.id)
    FROM Families

<span data-ttu-id="5729c-739">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-739">**Results**</span></span>

    [
        "WAKEFIELDFAMILY", 
        "ANDERSENFAMILY"
    ]

<span data-ttu-id="5729c-740">Или объединить строки, как в этом примере:</span><span class="sxs-lookup"><span data-stu-id="5729c-740">Or concatenate strings like in this example:</span></span>

<span data-ttu-id="5729c-741">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-741">**Query**</span></span>

    SELECT Families.id, CONCAT(Families.address.city, ",", Families.address.state) AS location
    FROM Families

<span data-ttu-id="5729c-742">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-742">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "location": "NY,NY"
    },
    {
      "id": "AndersenFamily",
      "location": "seattle,WA"
    }]


<span data-ttu-id="5729c-743">Строковые функции могут также использоваться в hello ГДЕ предложение toofilter результаты, например в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="5729c-743">String functions can also be used in hello WHERE clause toofilter results, like in hello following example:</span></span>

<span data-ttu-id="5729c-744">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-744">**Query**</span></span>

    SELECT Families.id, Families.address.city
    FROM Families
    WHERE STARTSWITH(Families.id, "Wakefield")

<span data-ttu-id="5729c-745">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-745">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "city": "NY"
    }]

### <a name="array-functions"></a><span data-ttu-id="5729c-746">Функции массивов</span><span class="sxs-lookup"><span data-stu-id="5729c-746">Array functions</span></span>
<span data-ttu-id="5729c-747">Следующие скалярные функции Hello операции над входным значением массива и возвращают числовое, логическое значение или значение массива.</span><span class="sxs-lookup"><span data-stu-id="5729c-747">hello following scalar functions perform an operation on an array input value and return numeric, Boolean or array value.</span></span> <span data-ttu-id="5729c-748">Ниже приведена таблица встроенных функций над массивом:</span><span class="sxs-lookup"><span data-stu-id="5729c-748">Here's a table of built-in array functions:</span></span>

| <span data-ttu-id="5729c-749">Использование</span><span class="sxs-lookup"><span data-stu-id="5729c-749">Usage</span></span> | <span data-ttu-id="5729c-750">Описание</span><span class="sxs-lookup"><span data-stu-id="5729c-750">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="5729c-751">ARRAY_LENGTH (arr_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-751">ARRAY_LENGTH (arr_expr)</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_length) |<span data-ttu-id="5729c-752">Возвращает число hello элементов hello указано выражение массива.</span><span class="sxs-lookup"><span data-stu-id="5729c-752">Returns hello number of elements of hello specified array expression.</span></span> |
| <span data-ttu-id="5729c-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span><span class="sxs-lookup"><span data-stu-id="5729c-753">[ARRAY_CONCAT (arr_expr, arr_expr [, arr_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_concat)</span></span> |<span data-ttu-id="5729c-754">Возвращает массив, который является результатом объединения двух или более значений массивов hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-754">Returns an array that is hello result of concatenating two or more array values.</span></span> |
| <span data-ttu-id="5729c-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span><span class="sxs-lookup"><span data-stu-id="5729c-755">[ARRAY_CONTAINS (arr_expr, expr [, bool_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_contains)</span></span> |<span data-ttu-id="5729c-756">Возвращает логическое значение, указывающее, содержит ли массив hello hello заданного значения.</span><span class="sxs-lookup"><span data-stu-id="5729c-756">Returns a Boolean indicating whether hello array contains hello specified value.</span></span> <span data-ttu-id="5729c-757">Можно указать, если hello совпадение полной или частичной.</span><span class="sxs-lookup"><span data-stu-id="5729c-757">Can specify if hello match is full or partial.</span></span> |
| <span data-ttu-id="5729c-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span><span class="sxs-lookup"><span data-stu-id="5729c-758">[ARRAY_SLICE (arr_expr, num_expr [, num_expr])](https://msdn.microsoft.com/library/azure/dn782250.aspx#bk_array_slice)</span></span> |<span data-ttu-id="5729c-759">Возвращает часть выражения массива.</span><span class="sxs-lookup"><span data-stu-id="5729c-759">Returns part of an array expression.</span></span> |

<span data-ttu-id="5729c-760">Функции массивов можно использовать toomanipulate массивов в JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-760">Array functions can be used toomanipulate arrays within JSON.</span></span> <span data-ttu-id="5729c-761">Например ниже приведен запрос, возвращающий все документы, где hello родительских элементов он «Циклический перебор Wakefield».</span><span class="sxs-lookup"><span data-stu-id="5729c-761">For example, here's a query that returns all documents where one of hello parents is "Robin Wakefield".</span></span> 

<span data-ttu-id="5729c-762">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-762">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin", familyName: "Wakefield" })

<span data-ttu-id="5729c-763">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-763">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="5729c-764">Можно указать фрагмент частичного для сопоставления элементов в массиве hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-764">You can specify a partial fragment for matching elements within hello array.</span></span> <span data-ttu-id="5729c-765">Hello следующем запросе выполняется поиск всех родительских элементов с hello `givenName` из `Robin`.</span><span class="sxs-lookup"><span data-stu-id="5729c-765">hello following query finds all parents with hello `givenName` of `Robin`.</span></span>

<span data-ttu-id="5729c-766">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-766">**Query**</span></span>

    SELECT Families.id 
    FROM Families 
    WHERE ARRAY_CONTAINS(Families.parents, { givenName: "Robin" }, true)

<span data-ttu-id="5729c-767">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-767">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]


<span data-ttu-id="5729c-768">Вот другой пример, использующий ARRAY_LENGTH tooget hello количество детей в семействе.</span><span class="sxs-lookup"><span data-stu-id="5729c-768">Here's another example that uses ARRAY_LENGTH tooget hello number of children per family.</span></span>

<span data-ttu-id="5729c-769">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-769">**Query**</span></span>

    SELECT Families.id, ARRAY_LENGTH(Families.children) AS numberOfChildren
    FROM Families 

<span data-ttu-id="5729c-770">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-770">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
      "numberOfChildren": 2
    },
    {
      "id": "AndersenFamily",
      "numberOfChildren": 1
    }]

### <a name="spatial-functions"></a><span data-ttu-id="5729c-771">Пространственные функции</span><span class="sxs-lookup"><span data-stu-id="5729c-771">Spatial functions</span></span>
<span data-ttu-id="5729c-772">Cosmos DB поддерживает следующие встроенные функции Open Geospatial Consortium (OGC) для выполнения запросов к геопространственных hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-772">Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> 

<table>
<tr>
  <td><span data-ttu-id="5729c-773"><strong>Использование</strong></span><span class="sxs-lookup"><span data-stu-id="5729c-773"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="5729c-774"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="5729c-774"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-775">ST_DISTANCE (point_expr, point_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-775">ST_DISTANCE (point_expr, point_expr)</span></span></td>
  <td><span data-ttu-id="5729c-776">Возвращает hello расстояние между выражениями hello две точки GeoJSON Polygon и LineString.</span><span class="sxs-lookup"><span data-stu-id="5729c-776">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-777">ST_WITHIN (point_expr, polygon_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-777">ST_WITHIN (point_expr, polygon_expr)</span></span></td>
  <td><span data-ttu-id="5729c-778">Возвращает выражение типа Boolean, показывающего, является hello GeoJSON сперва (точка Polygon и LineString) в рамках hello второй GeoJSON объекта (точка Polygon и LineString).</span><span class="sxs-lookup"><span data-stu-id="5729c-778">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="5729c-779">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="5729c-780">Возвращает логическое выражение, указывающее, пересекается ли hello двух указанных GeoJSON объектов (точка Polygon и LineString).</span><span class="sxs-lookup"><span data-stu-id="5729c-780">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-781">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="5729c-781">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="5729c-782">Возвращает логическое значение, указывающее, является ли hello точки GeoJSON Polygon и LineString выражение допустимо.</span><span class="sxs-lookup"><span data-stu-id="5729c-782">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="5729c-783">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="5729c-783">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="5729c-784">Возвращает значение JSON, содержащий логическое значение, указываемое hello точки GeoJSON Polygon и LineString выражение является допустимым и если недействительной, кроме того hello причина как строковое значение.</span><span class="sxs-lookup"><span data-stu-id="5729c-784">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="5729c-785">Пространственные функции могут быть запросами сходству используется tooperform пространственных данных.</span><span class="sxs-lookup"><span data-stu-id="5729c-785">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="5729c-786">Например ниже приведен запрос, возвращающий все семейство документы, в течение 30 км hello указанное расположение используется встроенная функция ST_DISTANCE hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-786">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="5729c-787">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-787">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="5729c-788">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-788">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="5729c-789">Дополнительные сведения о поддержке геопространственных данных в Cosmos DB см. в статье [Работа с геопространственными данными и данными расположений GeoJSON в Azure Cosmos DB](geospatial.md).</span><span class="sxs-lookup"><span data-stu-id="5729c-789">For more details on geospatial support in Cosmos DB, please see [Working with geospatial data in Azure Cosmos DB](geospatial.md).</span></span> <span data-ttu-id="5729c-790">Что мы и добрались до Пространственные функции и hello синтаксис SQL для Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5729c-790">That wraps up spatial functions, and hello SQL syntax for Cosmos DB.</span></span> <span data-ttu-id="5729c-791">Теперь давайте рассмотрим как LINQ запрос работает и его взаимодействия с синтаксисом hello мы видели к текущему моменту.</span><span class="sxs-lookup"><span data-stu-id="5729c-791">Now let's take a look at how LINQ querying works and how it interacts with hello syntax we've seen so far.</span></span>

## <span data-ttu-id="5729c-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span><span class="sxs-lookup"><span data-stu-id="5729c-792"><a id="Linq"></a>LINQ tooDocumentDB API SQL</span></span>
<span data-ttu-id="5729c-793">LINQ является моделью программирования .NET, которая выражает вычисления в виде запросов потоков объектов.</span><span class="sxs-lookup"><span data-stu-id="5729c-793">LINQ is a .NET programming model that expresses computation as queries on streams of objects.</span></span> <span data-ttu-id="5729c-794">Cosmos DB предоставляет клиентская библиотека toointerface с помощью LINQ, облегчая преобразование между объектами JSON и .NET и сопоставления из подмножества LINQ запросы tooCosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5729c-794">Cosmos DB provides a client-side library toointerface with LINQ by facilitating a conversion between JSON and .NET objects and a mapping from a subset of LINQ queries tooCosmos DB queries.</span></span> 

<span data-ttu-id="5729c-795">Hello рисунок ниже показана архитектура hello, поддерживающих запросы LINQ с помощью Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5729c-795">hello picture below shows hello architecture of supporting LINQ queries using Cosmos DB.</span></span>  <span data-ttu-id="5729c-796">С помощью клиента Cosmos DB hello, разработчики могут создавать **IQueryable** объекта, напрямую запросы hello Cosmos DB поставщик запросов, который затем преобразует запрос LINQ hello в запрос Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5729c-796">Using hello Cosmos DB client, developers can create an **IQueryable** object that directly queries hello Cosmos DB query provider, which then translates hello LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="5729c-797">Hello запрос передается toohello tooretrieve server Cosmos DB набор результатов в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-797">hello query is then passed toohello Cosmos DB server tooretrieve a set of results in JSON format.</span></span> <span data-ttu-id="5729c-798">Hello возвращаемые результаты будут десериализованы в поток объектов .NET на стороне клиента hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-798">hello returned results are deserialized into a stream of .NET objects on hello client side.</span></span>

![Архитектура поддержки запросов LINQ с помощью API DocumentDB — синтаксис SQL, язык запросов JSON, основные понятия баз данных и SQL-запросы][1]

### <a name="net-and-json-mapping"></a><span data-ttu-id="5729c-800">Сопоставление .NET и JSON</span><span class="sxs-lookup"><span data-stu-id="5729c-800">.NET and JSON mapping</span></span>
<span data-ttu-id="5729c-801">Hello сопоставление объектов .NET и документы JSON является естественным - для каждого поля данных элемент сопоставляется tooa объект JSON, где — имя поля hello сопоставлены toohello «ключ» часть hello объекта и часть «value» hello будет сопоставлен рекурсивно toohello часть значения hello объекта.</span><span class="sxs-lookup"><span data-stu-id="5729c-801">hello mapping between .NET objects and JSON documents is natural - each data member field is mapped tooa JSON object, where hello field name is mapped toohello "key" part of hello object and hello "value" part is recursively mapped toohello value part of hello object.</span></span> <span data-ttu-id="5729c-802">Рассмотрим следующий пример hello: hello семейства объектом, созданным — сопоставленных toohello JSON документ, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5729c-802">Consider hello following example: hello Family object created is mapped toohello JSON document as shown below.</span></span> <span data-ttu-id="5729c-803">И наоборот, hello JSON документ сопоставленных задней tooa объект .NET.</span><span class="sxs-lookup"><span data-stu-id="5729c-803">And vice versa, hello JSON document is mapped back tooa .NET object.</span></span>

<span data-ttu-id="5729c-804">**Класс C#**</span><span class="sxs-lookup"><span data-stu-id="5729c-804">**C# Class**</span></span>

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


<span data-ttu-id="5729c-805">**JSON**</span><span class="sxs-lookup"><span data-stu-id="5729c-805">**JSON**</span></span>  

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



### <a name="linq-toosql-translation"></a><span data-ttu-id="5729c-806">Перевод tooSQL LINQ</span><span class="sxs-lookup"><span data-stu-id="5729c-806">LINQ tooSQL translation</span></span>
<span data-ttu-id="5729c-807">Поставщик запросов Cosmos DB Hello выполняет сопоставление наиболее усилий из запроса LINQ в Cosmos DB SQL-запроса.</span><span class="sxs-lookup"><span data-stu-id="5729c-807">hello Cosmos DB query provider performs a best effort mapping from a LINQ query into a Cosmos DB SQL query.</span></span> <span data-ttu-id="5729c-808">В следующих описание hello предполагается, что hello читатель имеет общее представление о языка LINQ.</span><span class="sxs-lookup"><span data-stu-id="5729c-808">In hello following description, we assume hello reader has a basic familiarity of LINQ.</span></span>

<span data-ttu-id="5729c-809">Во-первых для системы типов hello, поддерживают все JSON примитивные типы — числовые типы, логическое значение, строка и null.</span><span class="sxs-lookup"><span data-stu-id="5729c-809">First, for hello type system, we support all JSON primitive types – numeric types, boolean, string, and null.</span></span> <span data-ttu-id="5729c-810">Поддерживаются только эти типы JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-810">Only these JSON types are supported.</span></span> <span data-ttu-id="5729c-811">поддерживаются следующие скалярные выражения Hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-811">hello following scalar expressions are supported.</span></span>

* <span data-ttu-id="5729c-812">Постоянные значения — следующие значения констант hello примитивных типов данных во время hello, оценки запроса hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-812">Constant values – these include constant values of hello primitive data types at hello time hello query is evaluated.</span></span>
* <span data-ttu-id="5729c-813">Индексные выражения свойства или массива — эти выражения см. свойство toohello объекта или элемента массива.</span><span class="sxs-lookup"><span data-stu-id="5729c-813">Property/array index expressions – these expressions refer toohello property of an object or an array element.</span></span>
  
     <span data-ttu-id="5729c-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n — это целочисленная переменная</span><span class="sxs-lookup"><span data-stu-id="5729c-814">family.Id;    family.children[0].familyName;    family.children[0].grade;    family.children[n].grade; //n is an int variable</span></span>
* <span data-ttu-id="5729c-815">Арифметические выражения. К ним относятся общие арифметические выражения на основе численных и логических значений.</span><span class="sxs-lookup"><span data-stu-id="5729c-815">Arithmetic expressions - These include common arithmetic expressions on numerical and boolean values.</span></span> <span data-ttu-id="5729c-816">Полный список hello можно найти toohello спецификации SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-816">For hello complete list, refer toohello SQL specification.</span></span>
  
     <span data-ttu-id="5729c-817">2 * family.children[0].grade;    x + y;</span><span class="sxs-lookup"><span data-stu-id="5729c-817">2 * family.children[0].grade;    x + y;</span></span>
* <span data-ttu-id="5729c-818">Строка выражения сравнения — к ним относятся сравнивают строковое значение toosome постоянное строковое значение.</span><span class="sxs-lookup"><span data-stu-id="5729c-818">String comparison expression - these include comparing a string value toosome constant string value.</span></span>  
  
     <span data-ttu-id="5729c-819">mother.familyName == "Smith";    child.givenName == s; //s — это строковая переменная</span><span class="sxs-lookup"><span data-stu-id="5729c-819">mother.familyName == "Smith";    child.givenName == s; //s is a string variable</span></span>
* <span data-ttu-id="5729c-820">Выражение создания объекта/массива. Возвращают объект комбинированного типа, или анонимного типа, или массив таких объектов.</span><span class="sxs-lookup"><span data-stu-id="5729c-820">Object/array creation expression - these expressions return an object of compound value type or anonymous type or an array of such objects.</span></span> <span data-ttu-id="5729c-821">Эти значения могут быть вложенными.</span><span class="sxs-lookup"><span data-stu-id="5729c-821">These values can be nested.</span></span>
  
     <span data-ttu-id="5729c-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //анонимный тип с двумя полями</span><span class="sxs-lookup"><span data-stu-id="5729c-822">new Parent { familyName = "Smith", givenName = "Joe" }; new { first = 1, second = 2 }; //an anonymous type with two fields</span></span>              
     <span data-ttu-id="5729c-823">new int[] { 3, child.grade, 5 };</span><span class="sxs-lookup"><span data-stu-id="5729c-823">new int[] { 3, child.grade, 5 };</span></span>

### <span data-ttu-id="5729c-824"><a id="SupportedLinqOperators"></a>Список поддерживаемых операторов LINQ</span><span class="sxs-lookup"><span data-stu-id="5729c-824"><a id="SupportedLinqOperators"></a>List of supported LINQ operators</span></span>
<span data-ttu-id="5729c-825">Ниже приведен список поддерживаемых операторов LINQ в поставщике LINQ hello, входящий в состав пакета SDK для .NET DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-825">Here is a list of supported LINQ operators in hello LINQ provider included with hello DocumentDB .NET SDK.</span></span>

* <span data-ttu-id="5729c-826">**Выберите**: проекций перевести toohello SQL SELECT, включая создание объектов</span><span class="sxs-lookup"><span data-stu-id="5729c-826">**Select**: Projections translate toohello SQL SELECT including object construction</span></span>
* <span data-ttu-id="5729c-827">**Где**: фильтры переводить toohello SQL WHERE и поддерживает преобразование между & &, || и!</span><span class="sxs-lookup"><span data-stu-id="5729c-827">**Where**: Filters translate toohello SQL WHERE, and support translation between && , || and !</span></span> <span data-ttu-id="5729c-828">операторы SQL toohello</span><span class="sxs-lookup"><span data-stu-id="5729c-828">toohello SQL operators</span></span>
* <span data-ttu-id="5729c-829">**SelectMany**: позволяет очистки массивы toohello SQL JOIN предложения.</span><span class="sxs-lookup"><span data-stu-id="5729c-829">**SelectMany**: Allows unwinding of arrays toohello SQL JOIN clause.</span></span> <span data-ttu-id="5729c-830">Может быть toofilter используется toochain или вложенные выражения на элементы массива</span><span class="sxs-lookup"><span data-stu-id="5729c-830">Can be used toochain/nest expressions toofilter on array elements</span></span>
* <span data-ttu-id="5729c-831">**OrderBy и OrderByDescending**: преобразует tooORDER по возрастанию или по убыванию</span><span class="sxs-lookup"><span data-stu-id="5729c-831">**OrderBy and OrderByDescending**: Translates tooORDER BY ascending/descending</span></span>
* <span data-ttu-id="5729c-832">Операторы для агрегирования **Count**, **Sum**, **Min**, **Max**, **Average** и их асинхронные эквиваленты **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync** и **AverageAsync**.</span><span class="sxs-lookup"><span data-stu-id="5729c-832">**Count**, **Sum**, **Min**, **Max**, and **Average** operators for aggregation, and their async equivalents **CountAsync**, **SumAsync**, **MinAsync**, **MaxAsync**, and **AverageAsync**.</span></span>
* <span data-ttu-id="5729c-833">**CompareTo**: преобразует toorange сравнения.</span><span class="sxs-lookup"><span data-stu-id="5729c-833">**CompareTo**: Translates toorange comparisons.</span></span> <span data-ttu-id="5729c-834">Обычно используется для строк, так как их нельзя сравнивать в .NET.</span><span class="sxs-lookup"><span data-stu-id="5729c-834">Commonly used for strings since they’re not comparable in .NET</span></span>
* <span data-ttu-id="5729c-835">**Принимать**: преобразует toohello SQL TOP для ограничения результатов запроса</span><span class="sxs-lookup"><span data-stu-id="5729c-835">**Take**: Translates toohello SQL TOP for limiting results from a query</span></span>
* <span data-ttu-id="5729c-836">**Математические функции**: поддерживает преобразование. В NET Abs Acos, Asin, Atan, верхний предел, Cos, Exp, функция Floor, журнал, Log10, Pow, циклов, знак, Sin, Sqrt, Tan, Truncate toohello эквивалент SQL встроенных функций.</span><span class="sxs-lookup"><span data-stu-id="5729c-836">**Math Functions**: Supports translation from .NET’s Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="5729c-837">**Строковые функции**: поддерживает преобразование. NET Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, обратное, TrimEnd, StartsWith, подстроку, ToUpper toohello эквивалентные встроенные функции SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-837">**String Functions**: Supports translation from .NET’s Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="5729c-838">**Массив функции**: поддерживает преобразование. В NET Concat "," содержит "и" число toohello эквивалент SQL встроенных функций.</span><span class="sxs-lookup"><span data-stu-id="5729c-838">**Array Functions**: Supports translation from .NET’s Concat, Contains, and Count toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="5729c-839">**Геопространственные функции расширения**: поддерживает преобразование из методы-заглушки расстояние в пределах IsValid и IsValidDetailed toohello эквивалентные встроенные функции SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-839">**Geospatial Extension Functions**: Supports translation from stub methods Distance, Within, IsValid, and IsValidDetailed toohello equivalent SQL built-in functions.</span></span>
* <span data-ttu-id="5729c-840">**Пользовательские функции расширения**: поддерживает преобразования из hello заглушки метода UserDefinedFunctionProvider.Invoke toohello соответствующего определяемой пользователем функции.</span><span class="sxs-lookup"><span data-stu-id="5729c-840">**User-Defined Function Extension Function**: Supports translation from hello stub method UserDefinedFunctionProvider.Invoke toohello corresponding user-defined function.</span></span>
* <span data-ttu-id="5729c-841">**Прочие**: поддерживает объединенный перевод hello и условные операторы.</span><span class="sxs-lookup"><span data-stu-id="5729c-841">**Miscellaneous**: Supports translation of hello coalesce and conditional operators.</span></span> <span data-ttu-id="5729c-842">Может транслировать Contains tooString CONTAINS, ARRAY_CONTAINS или hello в SQL, в зависимости от контекста.</span><span class="sxs-lookup"><span data-stu-id="5729c-842">Can translate Contains tooString CONTAINS, ARRAY_CONTAINS, or hello SQL IN depending on context.</span></span>

### <a name="sql-query-operators"></a><span data-ttu-id="5729c-843">Операторы SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="5729c-843">SQL query operators</span></span>
<span data-ttu-id="5729c-844">Ниже приведены некоторые примеры, иллюстрирующие, как некоторые стандартные операторы запросов LINQ hello преобразуются вниз tooCosmos DB запросов.</span><span class="sxs-lookup"><span data-stu-id="5729c-844">Here are some examples that illustrate how some of hello standard LINQ query operators are translated down tooCosmos DB queries.</span></span>

#### <a name="select-operator"></a><span data-ttu-id="5729c-845">Оператор Select</span><span class="sxs-lookup"><span data-stu-id="5729c-845">Select Operator</span></span>
<span data-ttu-id="5729c-846">синтаксис Hello `input.Select(x => f(x))`, где `f` является скалярным выражением.</span><span class="sxs-lookup"><span data-stu-id="5729c-846">hello syntax is `input.Select(x => f(x))`, where `f` is a scalar expression.</span></span>

<span data-ttu-id="5729c-847">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-847">**LINQ lambda expression**</span></span>

    input.Select(family => family.parents[0].familyName);

<span data-ttu-id="5729c-848">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-848">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f



<span data-ttu-id="5729c-849">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-849">**LINQ lambda expression**</span></span>

    input.Select(family => family.children[0].grade + c); // c is an int variable


<span data-ttu-id="5729c-850">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-850">**SQL**</span></span> 

    SELECT VALUE f.children[0].grade + c
    FROM Families f 



<span data-ttu-id="5729c-851">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-851">**LINQ lambda expression**</span></span>

    input.Select(family => new
    {
        name = family.children[0].familyName,
        grade = family.children[0].grade + 3
    });


<span data-ttu-id="5729c-852">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-852">**SQL**</span></span> 

    SELECT VALUE {"name":f.children[0].familyName, 
                  "grade": f.children[0].grade + 3 }
    FROM Families f



#### <a name="selectmany-operator"></a><span data-ttu-id="5729c-853">Оператор SelectMany</span><span class="sxs-lookup"><span data-stu-id="5729c-853">SelectMany operator</span></span>
<span data-ttu-id="5729c-854">синтаксис Hello `input.SelectMany(x => f(x))`, где `f` является скалярным выражением, которое возвращает тип коллекции.</span><span class="sxs-lookup"><span data-stu-id="5729c-854">hello syntax is `input.SelectMany(x => f(x))`, where `f` is a scalar expression that returns a collection type.</span></span>

<span data-ttu-id="5729c-855">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-855">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children);

<span data-ttu-id="5729c-856">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-856">**SQL**</span></span> 

    SELECT VALUE child
    FROM child IN Families.children



#### <a name="where-operator"></a><span data-ttu-id="5729c-857">Оператор Where</span><span class="sxs-lookup"><span data-stu-id="5729c-857">Where operator</span></span>
<span data-ttu-id="5729c-858">синтаксис Hello `input.Where(x => f(x))`, где `f` является скалярным выражением, которое возвращает значение типа Boolean.</span><span class="sxs-lookup"><span data-stu-id="5729c-858">hello syntax is `input.Where(x => f(x))`, where `f` is a scalar expression, which returns a Boolean value.</span></span>

<span data-ttu-id="5729c-859">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-859">**LINQ lambda expression**</span></span>

    input.Where(family=> family.parents[0].familyName == "Smith");

<span data-ttu-id="5729c-860">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-860">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith" 



<span data-ttu-id="5729c-861">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-861">**LINQ lambda expression**</span></span>

    input.Where(
        family => family.parents[0].familyName == "Smith" && 
        family.children[0].grade < 3);

<span data-ttu-id="5729c-862">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-862">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"
    AND f.children[0].grade < 3


### <a name="composite-sql-queries"></a><span data-ttu-id="5729c-863">Составные SQL-запросы</span><span class="sxs-lookup"><span data-stu-id="5729c-863">Composite SQL queries</span></span>
<span data-ttu-id="5729c-864">Hello выше операторы можно включать tooform более мощные средства запросов.</span><span class="sxs-lookup"><span data-stu-id="5729c-864">hello above operators can be composed tooform more powerful queries.</span></span> <span data-ttu-id="5729c-865">Поскольку Cosmos DB поддерживает вложенные коллекции, hello композиции может быть сцеплены или вложенные.</span><span class="sxs-lookup"><span data-stu-id="5729c-865">Since Cosmos DB supports nested collections, hello composition can either be concatenated or nested.</span></span>

#### <a name="concatenation"></a><span data-ttu-id="5729c-866">Объединение</span><span class="sxs-lookup"><span data-stu-id="5729c-866">Concatenation</span></span>
<span data-ttu-id="5729c-867">синтаксис Hello `input(.|.SelectMany())(.Select()|.Where())*`.</span><span class="sxs-lookup"><span data-stu-id="5729c-867">hello syntax is `input(.|.SelectMany())(.Select()|.Where())*`.</span></span> <span data-ttu-id="5729c-868">Объединенный запрос может начинаться с необязательного запроса `SelectMany`, за которым идет несколько операторов `Select` или `Where`.</span><span class="sxs-lookup"><span data-stu-id="5729c-868">A concatenated query can start with an optional `SelectMany` query followed by multiple `Select` or `Where` operators.</span></span>

<span data-ttu-id="5729c-869">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-869">**LINQ lambda expression**</span></span>

    input.Select(family=>family.parents[0])
        .Where(familyName == "Smith");

<span data-ttu-id="5729c-870">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-870">**SQL**</span></span>

    SELECT *
    FROM Families f
    WHERE f.parents[0].familyName = "Smith"



<span data-ttu-id="5729c-871">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-871">**LINQ lambda expression**</span></span>

    input.Where(family => family.children[0].grade > 3)
        .Select(family => family.parents[0].familyName);

<span data-ttu-id="5729c-872">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-872">**SQL**</span></span> 

    SELECT VALUE f.parents[0].familyName
    FROM Families f
    WHERE f.children[0].grade > 3



<span data-ttu-id="5729c-873">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-873">**LINQ lambda expression**</span></span>

    input.Select(family => new { grade=family.children[0].grade}).
        Where(anon=> anon.grade < 3);

<span data-ttu-id="5729c-874">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-874">**SQL**</span></span> 

    SELECT *
    FROM Families f
    WHERE ({grade: f.children[0].grade}.grade > 3)



<span data-ttu-id="5729c-875">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-875">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.parents)
        .Where(parent => parents.familyName == "Smith");

<span data-ttu-id="5729c-876">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-876">**SQL**</span></span> 

    SELECT *
    FROM p IN Families.parents
    WHERE p.familyName = "Smith"



#### <a name="nesting"></a><span data-ttu-id="5729c-877">Вложенные операторы</span><span class="sxs-lookup"><span data-stu-id="5729c-877">Nesting</span></span>
<span data-ttu-id="5729c-878">синтаксис Hello `input.SelectMany(x=>x.Q())` где Q является `Select`, `SelectMany`, или `Where` оператор.</span><span class="sxs-lookup"><span data-stu-id="5729c-878">hello syntax is `input.SelectMany(x=>x.Q())` where Q is a `Select`, `SelectMany`, or `Where` operator.</span></span>

<span data-ttu-id="5729c-879">Во вложенном запросе внутренний запрос hello является элементом примененных tooeach hello внешней коллекции.</span><span class="sxs-lookup"><span data-stu-id="5729c-879">In a nested query, hello inner query is applied tooeach element of hello outer collection.</span></span> <span data-ttu-id="5729c-880">Один является важной функцией, hello внутренний запрос может ссылаться поля toohello элементов hello hello внешней коллекции как самосоединения.</span><span class="sxs-lookup"><span data-stu-id="5729c-880">One important feature is that hello inner query can refer toohello fields of hello elements in hello outer collection like self-joins.</span></span>

<span data-ttu-id="5729c-881">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-881">**LINQ lambda expression**</span></span>

    input.SelectMany(family=> 
        family.parents.Select(p => p.familyName));

<span data-ttu-id="5729c-882">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-882">**SQL**</span></span> 

    SELECT VALUE p.familyName
    FROM Families f
    JOIN p IN f.parents


<span data-ttu-id="5729c-883">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-883">**LINQ lambda expression**</span></span>

    input.SelectMany(family => 
        family.children.Where(child => child.familyName == "Jeff"));

<span data-ttu-id="5729c-884">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-884">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = "Jeff"



<span data-ttu-id="5729c-885">**Лямбда-выражение LINQ**</span><span class="sxs-lookup"><span data-stu-id="5729c-885">**LINQ lambda expression**</span></span>

    input.SelectMany(family => family.children.Where(
        child => child.familyName == family.parents[0].familyName));

<span data-ttu-id="5729c-886">**SQL**</span><span class="sxs-lookup"><span data-stu-id="5729c-886">**SQL**</span></span> 

    SELECT *
    FROM Families f
    JOIN c IN f.children
    WHERE c.familyName = f.parents[0].familyName


## <span data-ttu-id="5729c-887"><a id="ExecutingSqlQueries"></a>Выполнение SQL-запросов</span><span class="sxs-lookup"><span data-stu-id="5729c-887"><a id="ExecutingSqlQueries"></a>Executing SQL queries</span></span>
<span data-ttu-id="5729c-888">Cosmos DB предоставляет ресурсы через REST API, который можно вызвать с помощью любого языка, позволяющего отправлять запросы HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5729c-888">Cosmos DB exposes resources through a REST API that can be called by any language capable of making HTTP/HTTPS requests.</span></span> <span data-ttu-id="5729c-889">Кроме того, Cosmos DB предлагает программные библиотеки для некоторых популярных языков программирования, таких как NET, Node.js, JavaScript и Python.</span><span class="sxs-lookup"><span data-stu-id="5729c-889">Additionally, Cosmos DB offers programming libraries for several popular languages like .NET, Node.js, JavaScript, and Python.</span></span> <span data-ttu-id="5729c-890">Hello REST API и hello различных библиотеках все поддержку запросов через SQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-890">hello REST API and hello various libraries all support querying through SQL.</span></span> <span data-ttu-id="5729c-891">Hello .NET SDK поддерживает LINQ, кроме запросов tooSQL.</span><span class="sxs-lookup"><span data-stu-id="5729c-891">hello .NET SDK supports LINQ querying in addition tooSQL.</span></span>

<span data-ttu-id="5729c-892">Здравствуйте, в следующих примерах показано, как toocreate запрос и отправить его с учетной записью Cosmos DB базы данных.</span><span class="sxs-lookup"><span data-stu-id="5729c-892">hello following examples show how toocreate a query and submit it against a Cosmos DB database account.</span></span>

### <span data-ttu-id="5729c-893"><a id="RestAPI"></a>REST API</span><span class="sxs-lookup"><span data-stu-id="5729c-893"><a id="RestAPI"></a>REST API</span></span>
<span data-ttu-id="5729c-894">Cosmos DB предлагает простую и открытую модель программирования RESTful поверх HTTP.</span><span class="sxs-lookup"><span data-stu-id="5729c-894">Cosmos DB offers an open RESTful programming model over HTTP.</span></span> <span data-ttu-id="5729c-895">Учетные записи баз данных могут быть подготовлены с использованием подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="5729c-895">Database accounts can be provisioned using an Azure subscription.</span></span> <span data-ttu-id="5729c-896">модель ресурсов Cosmos DB Hello состоит из набора ресурсов под учетной записью базы данных, каждый из которых можно с помощью логического и стабильный URI.</span><span class="sxs-lookup"><span data-stu-id="5729c-896">hello Cosmos DB resource model consists of a set of resources under a database account, each  of which is addressable using a logical and stable URI.</span></span> <span data-ttu-id="5729c-897">Набор ресурсов — ссылка tooas канала в этом документе.</span><span class="sxs-lookup"><span data-stu-id="5729c-897">A set of resources is referred tooas a feed in this document.</span></span> <span data-ttu-id="5729c-898">Учетная запись базы данных может состоять из набора баз данных, каждая из которых содержит несколько коллекций, каждая из которых, в свою очередь, содержит хранимые процедуры, триггеры, определяемые пользователем функции, документы и соответствующие вложения.</span><span class="sxs-lookup"><span data-stu-id="5729c-898">A database account consists of a set of databases, each containing multiple collections, each of which in-turn contain documents, UDFs, and other resource types.</span></span>

<span data-ttu-id="5729c-899">модель Hello основные взаимодействия с этими ресурсами выполняется с помощью команд hello HTTP GET, PUT, POST и DELETE с их стандартных интерпретацию.</span><span class="sxs-lookup"><span data-stu-id="5729c-899">hello basic interaction model with these resources is through hello HTTP verbs GET, PUT, POST, and DELETE with their standard interpretation.</span></span> <span data-ttu-id="5729c-900">Hello команды POST используется для создания нового ресурса, выполнение хранимой процедуры или при выдаче запроса Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5729c-900">hello POST verb is used for creation of a new resource, for executing a stored procedure or for issuing a Cosmos DB query.</span></span> <span data-ttu-id="5729c-901">Запросы всегда включают только операции чтения без побочных эффектов.</span><span class="sxs-lookup"><span data-stu-id="5729c-901">Queries are always read-only operations with no side-effects.</span></span>

<span data-ttu-id="5729c-902">Hello следующих примерах POST для запроса DocumentDB API к коллекцию, содержащую два образца документов hello, когда мы рассмотрели к текущему моменту.</span><span class="sxs-lookup"><span data-stu-id="5729c-902">hello following examples show a POST for a DocumentDB API query made against a collection containing hello two sample documents we've reviewed so far.</span></span> <span data-ttu-id="5729c-903">запрос Hello имеет простой фильтр для имени свойства hello JSON.</span><span class="sxs-lookup"><span data-stu-id="5729c-903">hello query has a simple filter on hello JSON name property.</span></span> <span data-ttu-id="5729c-904">Обратите внимание на использование hello hello `x-ms-documentdb-isquery` и Content-Type: `application/query+json` toodenote заголовки, hello операции — это запрос.</span><span class="sxs-lookup"><span data-stu-id="5729c-904">Note hello use of hello `x-ms-documentdb-isquery` and Content-Type: `application/query+json` headers toodenote that hello operation is a query.</span></span>

<span data-ttu-id="5729c-905">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-905">**Request**</span></span>

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


<span data-ttu-id="5729c-906">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-906">**Results**</span></span>

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


<span data-ttu-id="5729c-907">Во втором примере Hello показывает более сложный запрос, возвращающий несколько результатов из соединения hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-907">hello second example shows a more complex query that returns multiple results from hello join.</span></span>

<span data-ttu-id="5729c-908">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="5729c-908">**Request**</span></span>

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


<span data-ttu-id="5729c-909">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="5729c-909">**Results**</span></span>

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


<span data-ttu-id="5729c-910">Если результаты запроса не может поместиться на одной странице результатов, а затем hello API-интерфейса REST возвращает токен продолжения через hello `x-ms-continuation-token` заголовок ответа.</span><span class="sxs-lookup"><span data-stu-id="5729c-910">If a query's results cannot fit within a single page of results, then hello REST API returns a continuation token through hello `x-ms-continuation-token` response header.</span></span> <span data-ttu-id="5729c-911">Клиенты может разбивать на страницы результатов, включив заголовок hello в последующие результаты.</span><span class="sxs-lookup"><span data-stu-id="5729c-911">Clients can paginate results by including hello header in subsequent results.</span></span> <span data-ttu-id="5729c-912">Hello количество результатов на странице также можно управлять с помощью hello `x-ms-max-item-count` номера заголовка.</span><span class="sxs-lookup"><span data-stu-id="5729c-912">hello number of results per page can also be controlled through hello `x-ms-max-item-count` number header.</span></span> <span data-ttu-id="5729c-913">Если указанный запрос hello в статистической функции, такие как `COUNT`, то страница hello запроса может возвращать частично статистические значения по hello страницы результатов.</span><span class="sxs-lookup"><span data-stu-id="5729c-913">If hello specified query has an aggregation function like `COUNT`, then hello query page may return a partially aggregated value over hello page of results.</span></span> <span data-ttu-id="5729c-914">Hello клиентов необходимо выполнять статистическую второго уровня через эти результаты tooproduce hello окончательные результаты, например, суммирования hello счетчики возвращаются в hello отдельных страниц tooreturn hello общее число объектов.</span><span class="sxs-lookup"><span data-stu-id="5729c-914">hello clients must perform a second-level aggregation over these results tooproduce hello final results, for example, sum over hello counts returned in hello individual pages tooreturn hello total count.</span></span>

<span data-ttu-id="5729c-915">политика согласованности данных hello toomanage для запросов, используйте hello `x-ms-consistency-level` заголовок, как и все запросы REST API.</span><span class="sxs-lookup"><span data-stu-id="5729c-915">toomanage hello data consistency policy for queries, use hello `x-ms-consistency-level` header like all REST API requests.</span></span> <span data-ttu-id="5729c-916">Для согласованности сеанса это hello echo tooalso требуется последняя версия `x-ms-session-token` заголовка файла Cookie в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-916">For session consistency, it is required tooalso echo hello latest `x-ms-session-token` Cookie header in hello query request.</span></span> <span data-ttu-id="5729c-917">Hello политика индексирования запрашиваемые коллекции может также повлиять на hello согласованности результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="5729c-917">hello queried collection's indexing policy can also influence hello consistency of query results.</span></span> <span data-ttu-id="5729c-918">Параметры политики индексирования по умолчанию hello, для коллекций hello индекс всегда является содержимого документа hello и результатов, удовлетворяющих согласованности hello, выбранного для данных запросов.</span><span class="sxs-lookup"><span data-stu-id="5729c-918">With hello default indexing policy settings, for collections hello index is always current with hello document contents and query results match hello consistency chosen for data.</span></span> <span data-ttu-id="5729c-919">Если политика индексирования hello ослабленной tooLazy, запросы могут возвращать устаревших результаты.</span><span class="sxs-lookup"><span data-stu-id="5729c-919">If hello indexing policy is relaxed tooLazy, then queries can return stale results.</span></span> <span data-ttu-id="5729c-920">Дополнительные сведения см. в статье [Настраиваемые уровни согласованности данных в Azure Cosmos DB][consistency-levels].</span><span class="sxs-lookup"><span data-stu-id="5729c-920">For more information, see [Azure Cosmos DB Consistency Levels][consistency-levels].</span></span>

<span data-ttu-id="5729c-921">Если политика индексирования hello настроен на коллекцию hello не поддерживает указанный запрос hello, hello Azure Cosmos DB сервер возвращает 400 «Ошибочный запрос».</span><span class="sxs-lookup"><span data-stu-id="5729c-921">If hello configured indexing policy on hello collection cannot support hello specified query, hello Azure Cosmos DB server returns 400 "Bad Request".</span></span> <span data-ttu-id="5729c-922">Он возвращается для запросов к путям, сконфигурированным для поиска по значениям хэшей (равенство), а также к путям, явно исключенным из индексации.</span><span class="sxs-lookup"><span data-stu-id="5729c-922">This is returned for range queries against paths configured for hash (equality) lookups, and for paths explicitly excluded from indexing.</span></span> <span data-ttu-id="5729c-923">Hello `x-ms-documentdb-query-enable-scan` заголовок может быть указанного tooallow hello запроса tooperform проверку, если индекс недоступен.</span><span class="sxs-lookup"><span data-stu-id="5729c-923">hello `x-ms-documentdb-query-enable-scan` header can be specified tooallow hello query tooperform a scan when an index is not available.</span></span>

<span data-ttu-id="5729c-924">Можно получить подробные метрики на выполнение запроса, задав `x-ms-documentdb-populatequerymetrics` заголовок слишком`True`.</span><span class="sxs-lookup"><span data-stu-id="5729c-924">You can get detailed metrics on query execution by setting `x-ms-documentdb-populatequerymetrics` header too`True`.</span></span> <span data-ttu-id="5729c-925">Дополнительные сведения см. в статье [Tuning query performance with Azure Cosmos DB](documentdb-sql-query-metrics.md) (Настройка производительности запросов с помощью Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="5729c-925">For more information, see [SQL query metrics for Azure Cosmos DB DocumentDB API](documentdb-sql-query-metrics.md).</span></span>

### <span data-ttu-id="5729c-926"><a id="DotNetSdk"></a>Пакет SDK для C# (.NET)</span><span class="sxs-lookup"><span data-stu-id="5729c-926"><a id="DotNetSdk"></a>C# (.NET) SDK</span></span>
<span data-ttu-id="5729c-927">Hello .NET SDK поддерживает LINQ и SQL запрос.</span><span class="sxs-lookup"><span data-stu-id="5729c-927">hello .NET SDK supports both LINQ and SQL querying.</span></span> <span data-ttu-id="5729c-928">Hello следующем примере показано, как tooperform hello простого фильтра запроса, представленные ранее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="5729c-928">hello following example shows how tooperform hello simple filter query introduced earlier in this document.</span></span>

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


<span data-ttu-id="5729c-929">Этот пример сравнивает два свойства на равенство в каждом документе и использует анонимные проекции.</span><span class="sxs-lookup"><span data-stu-id="5729c-929">This sample compares two properties for equality within each document and uses anonymous projections.</span></span> 

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


<span data-ttu-id="5729c-930">Следующий пример Hello показывает соединения, выраженных через LINQ SelectMany.</span><span class="sxs-lookup"><span data-stu-id="5729c-930">hello next sample shows joins, expressed through LINQ SelectMany.</span></span>

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



<span data-ttu-id="5729c-931">клиент .NET Hello автоматически выполняет итерацию всех страниц hello результатов запроса в блоках foreach hello, как показано выше.</span><span class="sxs-lookup"><span data-stu-id="5729c-931">hello .NET client automatically iterates through all hello pages of query results in hello foreach blocks as shown above.</span></span> <span data-ttu-id="5729c-932">запрос Hello, параметры, представленные в hello раздел REST API также доступны в hello .NET SDK, с помощью hello `FeedOptions` и `FeedResponse` классов в метод CreateDocumentQuery hello.</span><span class="sxs-lookup"><span data-stu-id="5729c-932">hello query options introduced in hello REST API section are also available in hello .NET SDK using hello `FeedOptions` and `FeedResponse` classes in hello CreateDocumentQuery method.</span></span> <span data-ttu-id="5729c-933">Hello количество страниц, можно управлять с помощью hello `MaxItemCount` параметр.</span><span class="sxs-lookup"><span data-stu-id="5729c-933">hello number of pages can be controlled using hello `MaxItemCount` setting.</span></span> 

<span data-ttu-id="5729c-934">Можно также явно контроль разбиения на страницы, создав `IDocumentQueryable` с помощью hello `IQueryable` объекта, затем путем чтения` ResponseContinuationToken` значения и их передача в качестве `RequestContinuationToken` в `FeedOptions`.</span><span class="sxs-lookup"><span data-stu-id="5729c-934">You can also explicitly control paging by creating `IDocumentQueryable` using hello `IQueryable` object, then by reading the` ResponseContinuationToken` values and passing them back as `RequestContinuationToken` in `FeedOptions`.</span></span> <span data-ttu-id="5729c-935">`EnableScanInQuery`может быть просмотров tooenable набор, если запрос hello не поддерживаются hello настроена политика индексирования.</span><span class="sxs-lookup"><span data-stu-id="5729c-935">`EnableScanInQuery` can be set tooenable scans when hello query cannot be supported by hello configured indexing policy.</span></span> <span data-ttu-id="5729c-936">Для секционированных коллекций можно использовать `PartitionKey` toorun hello запрос к одной секции (хотя Cosmos DB автоматически этот можно извлечь из текста hello запроса), и `EnableCrossPartitionQuery` toorun запросы, которые может потребоваться toobe выполняться несколько секций.</span><span class="sxs-lookup"><span data-stu-id="5729c-936">For partitioned collections, you can use `PartitionKey` toorun hello query against a single partition (though Cosmos DB can automatically extract this from hello query text), and `EnableCrossPartitionQuery` toorun queries that may need toobe run against multiple partitions.</span></span> 

<span data-ttu-id="5729c-937">См. слишком[примеры Azure Cosmos DB .NET](https://github.com/Azure/azure-documentdb-net) дополнительные образцы, содержащий запросы.</span><span class="sxs-lookup"><span data-stu-id="5729c-937">Refer too[Azure Cosmos DB .NET samples](https://github.com/Azure/azure-documentdb-net) for more samples containing queries.</span></span> 

### <span data-ttu-id="5729c-938"><a id="JavaScriptServerSideApi"></a>Интерфейс API для серверного JavaScript</span><span class="sxs-lookup"><span data-stu-id="5729c-938"><a id="JavaScriptServerSideApi"></a>JavaScript server-side API</span></span>
<span data-ttu-id="5729c-939">Cosmos DB предоставляет модель программирования для выполнения логики приложения на основе JavaScript непосредственно на hello коллекций, с помощью хранимых процедур и триггеров.</span><span class="sxs-lookup"><span data-stu-id="5729c-939">Cosmos DB provides a programming model for executing JavaScript based application logic directly on hello collections using stored procedures and triggers.</span></span> <span data-ttu-id="5729c-940">Hello логику JavaScript, зарегистрированных на уровне коллекции, затем может выдавать операции базы данных в операции hello в документах hello hello, Получает коллекцию.</span><span class="sxs-lookup"><span data-stu-id="5729c-940">hello JavaScript logic registered at a collection level can then issue database operations on hello operations on hello documents of hello given collection.</span></span> <span data-ttu-id="5729c-941">Эти операции оборачиваются транзакциями ACID.</span><span class="sxs-lookup"><span data-stu-id="5729c-941">These operations are wrapped in ambient ACID transactions.</span></span>

<span data-ttu-id="5729c-942">Hello следующем примере показано, как запросы toouse queryDocuments hello в toomake hello API сервера JavaScript внутри хранимых процедур и триггеров.</span><span class="sxs-lookup"><span data-stu-id="5729c-942">hello following example shows how toouse hello queryDocuments in hello JavaScript server API toomake queries from inside stored procedures and triggers.</span></span>

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

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don't need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);
                        }
                    })
            });
    }

## <span data-ttu-id="5729c-943"><a id="References"></a>Справочные материалы</span><span class="sxs-lookup"><span data-stu-id="5729c-943"><a id="References"></a>References</span></span>
1. <span data-ttu-id="5729c-944">[Введение tooAzure Cosmos DB][introduction]</span><span class="sxs-lookup"><span data-stu-id="5729c-944">[Introduction tooAzure Cosmos DB][introduction]</span></span>
2. <span data-ttu-id="5729c-945">[DocumentDB SQL Syntax](http://go.microsoft.com/fwlink/p/?LinkID=510612) (Синтаксис SQL в DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="5729c-945">[Azure Cosmos DB SQL specification](http://go.microsoft.com/fwlink/p/?LinkID=510612)</span></span>
3. [<span data-ttu-id="5729c-946">Примеры .NET для Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5729c-946">Azure Cosmos DB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
4. <span data-ttu-id="5729c-947">[Настраиваемые уровни согласованности данных в Azure Cosmos DB][consistency-levels]</span><span class="sxs-lookup"><span data-stu-id="5729c-947">[Azure Cosmos DB Consistency Levels][consistency-levels]</span></span>
5. <span data-ttu-id="5729c-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span><span class="sxs-lookup"><span data-stu-id="5729c-948">ANSI SQL 2011 [http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681](http://www.iso.org/iso/iso_catalogue/catalogue_tc/catalogue_detail.htm?csnumber=53681)</span></span>
6. <span data-ttu-id="5729c-949">JSON — [http://json.org/](http://json.org/)</span><span class="sxs-lookup"><span data-stu-id="5729c-949">JSON [http://json.org/](http://json.org/)</span></span>
7. <span data-ttu-id="5729c-950">Спецификация JavaScript — [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span><span class="sxs-lookup"><span data-stu-id="5729c-950">Javascript Specification [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)</span></span> 
8. <span data-ttu-id="5729c-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span><span class="sxs-lookup"><span data-stu-id="5729c-951">LINQ [http://msdn.microsoft.com/library/bb308959.aspx](http://msdn.microsoft.com/library/bb308959.aspx)</span></span> 
9. <span data-ttu-id="5729c-952">Методика вычисления запросов для больших баз данных — [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span><span class="sxs-lookup"><span data-stu-id="5729c-952">Query evaluation techniques for large databases [http://dl.acm.org/citation.cfm?id=152611](http://dl.acm.org/citation.cfm?id=152611)</span></span>
10. <span data-ttu-id="5729c-953">Обработка запросов в параллельных реляционных СУБД (Query Processing in Parallel Relational Database Systems), IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="5729c-953">Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994</span></span>
11. <span data-ttu-id="5729c-954">Lu, Ooi, Tan, Обработка запросов в параллельных реляционных СУБД (Query Processing in Parallel Relational Database Systems), IEEE Computer Society Press, 1994</span><span class="sxs-lookup"><span data-stu-id="5729c-954">Lu, Ooi, Tan, Query Processing in Parallel Relational Database Systems, IEEE Computer Society Press, 1994.</span></span>
12. <span data-ttu-id="5729c-955">Кристофер Олстон (Christopher Olston), Бенджамин Рид (Benjamin Reed), Аткарш Сривастава (Utkarsh Srivastava), Рави Камар (Ravi Kumar), Эндрю Томкинс (Andrew Tomkins): Язык Pig. Не такой уж и незнакомый язык для обработки данных (Pig Latin: A Not-So-Foreign Language for Data Processing), SIGMOD 2008 г.</span><span class="sxs-lookup"><span data-stu-id="5729c-955">Christopher Olston, Benjamin Reed, Utkarsh Srivastava, Ravi Kumar, Andrew Tomkins: Pig Latin: A Not-So-Foreign Language for Data Processing, SIGMOD 2008.</span></span>
13. <span data-ttu-id="5729c-956">Ж.</span><span class="sxs-lookup"><span data-stu-id="5729c-956">G.</span></span> <span data-ttu-id="5729c-957">Графе (G. Graefe).</span><span class="sxs-lookup"><span data-stu-id="5729c-957">Graefe.</span></span> <span data-ttu-id="5729c-958">Hello каскадные платформа для оптимизации запросов.</span><span class="sxs-lookup"><span data-stu-id="5729c-958">hello Cascades framework for query optimization.</span></span> <span data-ttu-id="5729c-959">IEEE Data Eng.</span><span class="sxs-lookup"><span data-stu-id="5729c-959">IEEE Data Eng.</span></span> <span data-ttu-id="5729c-960">Bull., 18(3): 1995 г.</span><span class="sxs-lookup"><span data-stu-id="5729c-960">Bull., 18(3): 1995.</span></span>

[1]: ./media/documentdb-sql-query/sql-query1.png
[introduction]: introduction.md
[consistency-levels]: consistency-levels.md