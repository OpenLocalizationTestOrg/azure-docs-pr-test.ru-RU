---
title: "Программирование JavaScript на стороне aaaServer для Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, toowrite Azure Cosmos DB toouse хранение процедуры, триггеры базы данных и определяемые пользователем функции (UDF) в JavaScript. Здесь вы найдете советы по программированию баз данных и многое другое."
keywords: "Триггеры базы данных, хранимая процедура, хранимая процедура, программа базы данных, хранимая процедура, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="704f6-105">Программирование Azure Cosmos DB на стороне сервера: хранимые процедуры, триггеры баз данных и определяемые пользователем функции</span><span class="sxs-lookup"><span data-stu-id="704f6-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="704f6-106">Узнайте, каким образом интегрированное транзакционное выполнение JavaScript в Azure Cosmos DB позволяет разработчикам создавать **хранимые процедуры**, **триггеры** и **определяемые пользователем функции (UDF)** непосредственно на платформе JavaScript [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/).</span><span class="sxs-lookup"><span data-stu-id="704f6-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="704f6-107">Это позволяет toowrite базы данных программы логики приложения, которая может поставляться и выполнена непосредственно в хранилище секций hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="704f6-107">This allows you toowrite database program application logic that can be shipped and executed directly on hello database storage partitions.</span></span> 

<span data-ttu-id="704f6-108">Мы рекомендуем, запущенную за просмотром hello следующие видео, где лю Эндрю предоставляет модель программирования tooCosmos Краткое введение DB серверной базы данных.</span><span class="sxs-lookup"><span data-stu-id="704f6-108">We recommend getting started by watching hello following video, where Andrew Liu provides a brief introduction tooCosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="704f6-109">После этого вернитесь toothis статьи, где вы узнаете о toohello ответы hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="704f6-109">Then, return toothis article, where you'll learn hello answers toohello following questions:</span></span>  

* <span data-ttu-id="704f6-110">Как написать хранимую процедуру, триггер или определяемую пользователем Функцию на JavaScript?</span><span class="sxs-lookup"><span data-stu-id="704f6-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="704f6-111">Каким образом Cosmos DB предоставляет гарантию выполнения принципа ACID?</span><span class="sxs-lookup"><span data-stu-id="704f6-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="704f6-112">Каков принцип работы транзакций в Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="704f6-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="704f6-113">Что такое пред- и пост-триггеры, и как их написать?</span><span class="sxs-lookup"><span data-stu-id="704f6-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="704f6-114">Как зарегистрировать и выполнить хранимую процедуру, триггер или определяемую пользователем функции RESTful-образом по протоколу HTTP?</span><span class="sxs-lookup"><span data-stu-id="704f6-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="704f6-115">Какие пакеты SDK DB Cosmos доступных toocreate, а выполнение хранимых процедур, триггеров и определяемых пользователем функций?</span><span class="sxs-lookup"><span data-stu-id="704f6-115">What Cosmos DB SDKs are available toocreate and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-toostored-procedure-and-udf-programming"></a><span data-ttu-id="704f6-116">Введение tooStored процедуре и определяемой пользователем функции программирования</span><span class="sxs-lookup"><span data-stu-id="704f6-116">Introduction tooStored Procedure and UDF Programming</span></span>
<span data-ttu-id="704f6-117">В этом подходе *«JavaScript как современного T-SQL»* освобождает разработчиков приложения от сложности hello несоответствий системы типа и технологий объектно реляционного сопоставления.</span><span class="sxs-lookup"><span data-stu-id="704f6-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from hello complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="704f6-118">Он также имеет ряд преимуществ встроенная функция, которые могут быть загруженные toobuild многофункциональных приложений:</span><span class="sxs-lookup"><span data-stu-id="704f6-118">It also has a number of intrinsic advantages that can be utilized toobuild rich applications:</span></span>  

* <span data-ttu-id="704f6-119">**Процедурная логика:** JavaScript в качестве верхнего уровня языка программирования, предоставляет tooexpress привычного полнофункционального интерфейса бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="704f6-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface tooexpress business logic.</span></span> <span data-ttu-id="704f6-120">Можно выполнять сложные последовательности операций ближе toohello данных.</span><span class="sxs-lookup"><span data-stu-id="704f6-120">You can perform complex sequences of operations closer toohello data.</span></span>
* <span data-ttu-id="704f6-121">**Атомарные транзакции.** Cosmos DB гарантирует атомарность операций с базой данных, выполняемых внутри одной хранимой процедуры или триггера.</span><span class="sxs-lookup"><span data-stu-id="704f6-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="704f6-122">Это позволяет приложению объединить соответствующие операции в пакетном режиме; таким образом, успешно будут выполнены либо все из них, либо ни одна.</span><span class="sxs-lookup"><span data-stu-id="704f6-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="704f6-123">**Производительность:** hello факт, что JSON — система типов языка Javascript по своей природе сопоставленных toohello также является основной единицей хранилища в базу данных, Cosmos hello означает количество оптимизаций как отложенный материализации JSON документов в буфер hello пул и сделать их доступными по требованию toohello, выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="704f6-123">**Performance:** hello fact that JSON is intrinsically mapped toohello Javascript language type system and is also hello basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in hello buffer pool and making them available on-demand toohello executing code.</span></span> <span data-ttu-id="704f6-124">Существуют дополнительные преимущества производительности, связанные с базой данных toohello для доставки бизнес логики:</span><span class="sxs-lookup"><span data-stu-id="704f6-124">There are more performance benefits associated with shipping business logic toohello database:</span></span>
  
  * <span data-ttu-id="704f6-125">Пакеты — разработчики могут группировать операции, такие как вставка, и запускать их в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="704f6-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="704f6-126">Задержка трафика сети Hello затрат и значительно уменьшить hello хранилища toocreate издержек на отдельные транзакции.</span><span class="sxs-lookup"><span data-stu-id="704f6-126">hello network traffic latency cost and hello store overhead toocreate separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="704f6-127">Предварительная компиляция — Cosmos DB выполняет компиляцию хранимые процедуры, триггеры и определяемые пользователем функции (UDF) tooavoid стоимости компиляции JavaScript для каждого вызова.</span><span class="sxs-lookup"><span data-stu-id="704f6-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) tooavoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="704f6-128">Hello издержки построения hello байтовый код для hello процедурной логики занимающие tooa минимальное значение.</span><span class="sxs-lookup"><span data-stu-id="704f6-128">hello overhead of building hello byte code for hello procedural logic is amortized tooa minimal value.</span></span>
  * <span data-ttu-id="704f6-129">Секвенcирование — многим операции нужен побочный эффект («триггер»), что потенциально задействует выполнение одной или множества вторичных операций хранения.</span><span class="sxs-lookup"><span data-stu-id="704f6-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="704f6-130">Помимо атомарности, это обеспечивает более высокую производительность при перемещении сервера toohello.</span><span class="sxs-lookup"><span data-stu-id="704f6-130">Aside from atomicity, this is more performant when moved toohello server.</span></span> 
* <span data-ttu-id="704f6-131">**Инкапсуляция:** хранимые процедуры можно использовать toogroup бизнес-логики в одном месте.</span><span class="sxs-lookup"><span data-stu-id="704f6-131">**Encapsulation:** Stored procedures can be used toogroup business logic in one place.</span></span> <span data-ttu-id="704f6-132">Это принесет два преимущества:</span><span class="sxs-lookup"><span data-stu-id="704f6-132">This has two advantages:</span></span>
  * <span data-ttu-id="704f6-133">Он добавляет дополнительный уровень абстракции относительно hello необработанные данные, что позволит tooevolve архитекторы данных свои приложения, независимо от данных hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-133">It adds an abstraction layer on top of hello raw data, which enables data architects tooevolve their applications independently from hello data.</span></span> <span data-ttu-id="704f6-134">Это особенно удобно, когда данные hello без схемы, из-за toohello негибкие предположения, которые требуют toobe, помещенного в приложения hello, если они имеют toodeal с данными непосредственно.</span><span class="sxs-lookup"><span data-stu-id="704f6-134">This is particularly advantageous when hello data is schema-less, due toohello brittle assumptions that may need toobe baked into hello application if they have toodeal with data directly.</span></span>  
  * <span data-ttu-id="704f6-135">Эта абстракция позволяет защитить свои данные за счет оптимизации доступа hello из сценариев hello предприятий.</span><span class="sxs-lookup"><span data-stu-id="704f6-135">This abstraction lets enterprises keep their data secure by streamlining hello access from hello scripts.</span></span>  

<span data-ttu-id="704f6-136">Hello создания и выполнения триггеры базы данных, хранимые процедуры и пользовательские операторы поддерживаются через hello [API-интерфейса REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), и [клиентских SDK](documentdb-sdk-dotnet.md) на многих платформах, включая .NET, Node.js и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="704f6-136">hello creation and execution of database triggers, stored procedure and custom query operators is supported through hello [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="704f6-137">В этом учебнике используется hello [пакет SDK для Node.js с Q обещания](http://azure.github.io/azure-documentdb-node-q/) tooillustrate синтаксисе и использовании хранимых процедур, триггеров и определяемых пользователем функций.</span><span class="sxs-lookup"><span data-stu-id="704f6-137">This tutorial uses hello [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="704f6-138">Хранимые процедуры</span><span class="sxs-lookup"><span data-stu-id="704f6-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="704f6-139">Пример: написание простой хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="704f6-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="704f6-140">Давайте начнем с простой хранимой процедуры, которая возвращает «Hello World» в ответ.</span><span class="sxs-lookup"><span data-stu-id="704f6-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="704f6-141">Хранимые процедуры регистрируются в коллекциях и могут работать с любым документом и вложением, существующим в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="704f6-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="704f6-142">Hello следующий фрагмент кода показывает, как tooregister hello helloWorld хранимой процедуры с коллекцией.</span><span class="sxs-lookup"><span data-stu-id="704f6-142">hello following snippet shows how tooregister hello helloWorld stored procedure with a collection.</span></span> 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="704f6-143">После регистрации hello хранимые процедуры, мы применяемыми коллекции hello и чтение результатов hello обратно на приветствия клиента.</span><span class="sxs-lookup"><span data-stu-id="704f6-143">Once hello stored procedure is registered, we can execute it against hello collection, and read hello results back at hello client.</span></span> 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="704f6-144">объект контекста Hello доступ tooall операций, которые могут выполняться над хранилища Cosmos базы данных, а также для доступа к объектам toohello запроса и ответа.</span><span class="sxs-lookup"><span data-stu-id="704f6-144">hello context object provides access tooall operations that can be performed on Cosmos DB storage, as well as access toohello request and response objects.</span></span> <span data-ttu-id="704f6-145">В этом случае мы использовали hello объекта tooset hello в тексте ответа hello ответ, который был отправлен назад toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="704f6-145">In this case, we used hello response object tooset hello body of hello response that was sent back toohello client.</span></span> <span data-ttu-id="704f6-146">Дополнительные сведения см. в разделе toohello [сервера Azure Cosmos DB JavaScript документации по пакету SDK](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="704f6-146">For more details, refer toohello [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="704f6-147">Сообщите нам расширить этот пример и добавить дополнительные базы данных связанные функциональные возможности toohello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="704f6-147">Let us expand on this example and add more database related functionality toohello stored procedure.</span></span> <span data-ttu-id="704f6-148">Хранимые процедуры можно создавать, обновлять, чтение, запросов и удалять документы и вложения внутри коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-148">Stored procedures can create, update, read, query and delete documents and attachments inside hello collection.</span></span>    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a><span data-ttu-id="704f6-149">Пример: Записи toocreate хранимой процедуры документа</span><span class="sxs-lookup"><span data-stu-id="704f6-149">Example: Write a stored procedure toocreate a document</span></span>
<span data-ttu-id="704f6-150">Следующий фрагмент кода Hello показано, как toouse hello toointeract объект контекста с ресурсами Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="704f6-150">hello next snippet shows how toouse hello context object toointeract with Cosmos DB resources.</span></span>

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


<span data-ttu-id="704f6-151">Эта хранимая процедура принимает в качестве входного documentToCreate, текст hello toobe документов, созданных в текущей коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-151">This stored procedure takes as input documentToCreate, hello body of a document toobe created in hello current collection.</span></span> <span data-ttu-id="704f6-152">Все эти операции являются асинхронными и зависят от функций обратных вызовов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="704f6-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="704f6-153">функция обратного вызова Hello имеет два параметра: hello объекта ошибки в случае сбоя операции hello и один для hello создан объект.</span><span class="sxs-lookup"><span data-stu-id="704f6-153">hello callback function has two parameters, one for hello error object in case hello operation fails, and one for hello created object.</span></span> <span data-ttu-id="704f6-154">Внутри обратного вызова hello пользователи могут обрабатывать исключение hello или вызывают ошибку.</span><span class="sxs-lookup"><span data-stu-id="704f6-154">Inside hello callback, users can either handle hello exception or throw an error.</span></span> <span data-ttu-id="704f6-155">Если обратный вызов не предоставлен, а ошибка, среда выполнения Azure Cosmos DB hello вызывает ошибку.</span><span class="sxs-lookup"><span data-stu-id="704f6-155">In case a callback is not provided and there is an error, hello Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="704f6-156">В приведенном выше примере hello hello обратного вызова вызывает ошибку, если не удалось выполнить операцию hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-156">In hello example above, hello callback throws an error if hello operation failed.</span></span> <span data-ttu-id="704f6-157">В противном случае он задает идентификатор hello hello создан документ как текст hello hello ответа toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="704f6-157">Otherwise, it sets hello id of hello created document as hello body of hello response toohello client.</span></span> <span data-ttu-id="704f6-158">Таким образом, данная хранимая процедура выполняется с входными параметрами.</span><span class="sxs-lookup"><span data-stu-id="704f6-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="704f6-159">Обратите внимание, что эта хранимая процедура могут измененный tootake массив тела документа в качестве входных данных и создавать их все в hello же хранимой процедуры выполнения вместо несколько сетевых запросов toocreate каждого из них по отдельности.</span><span class="sxs-lookup"><span data-stu-id="704f6-159">Note that this stored procedure can be modified tootake an array of document bodies as input and create them all in hello same stored procedure execution instead of multiple network requests toocreate each of them individually.</span></span> <span data-ttu-id="704f6-160">Это может быть используется tooimplement компонента эффективного массового импорта для Cosmos DB (см. Далее в этом учебнике).</span><span class="sxs-lookup"><span data-stu-id="704f6-160">This can be used tooimplement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="704f6-161">описанном примере Hello показано, как toouse хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="704f6-161">hello example described demonstrated how toouse stored procedures.</span></span> <span data-ttu-id="704f6-162">Триггеры и определяемые пользователем функции (UDF) будут рассмотрены далее в учебнике hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-162">We will cover triggers and user defined functions (UDFs) later in hello tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="704f6-163">Транзакции программы базы данных</span><span class="sxs-lookup"><span data-stu-id="704f6-163">Database program transactions</span></span>
<span data-ttu-id="704f6-164">Транзакции в типичной базе данных могут быть определены как последовательность операций, выполняемых в одной логической единице работы.</span><span class="sxs-lookup"><span data-stu-id="704f6-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="704f6-165">Каждая транзакция предоставляет **гарантию выполнения принципа ACID**.</span><span class="sxs-lookup"><span data-stu-id="704f6-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="704f6-166">Широко известный акроним ACID обозначает четыре свойства: Atomicity (атомарность), Consistency (согласованность), Isolation (изолированность) и Durability (надежность).</span><span class="sxs-lookup"><span data-stu-id="704f6-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="704f6-167">Коротко говоря, Атомарность гарантирует, все операции hello, выполняемые внутри транзакции обрабатываются как единое целое где либо все его фиксируется или none.</span><span class="sxs-lookup"><span data-stu-id="704f6-167">Briefly, atomicity guarantees that all hello work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="704f6-168">Согласованность гарантирует hello данных всегда в рабочее состояние внутреннего по всем транзакциям.</span><span class="sxs-lookup"><span data-stu-id="704f6-168">Consistency makes sure that hello data is always in a good internal state across transactions.</span></span> <span data-ttu-id="704f6-169">Изоляция гарантирует, что никакие две транзакции взаимодействуют между собой — как правило, большинство коммерческих системы обеспечивают несколько уровней изоляции, которые могут использоваться с учетом потребностей приложения hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on hello application needs.</span></span> <span data-ttu-id="704f6-170">Устойчивость гарантирует, что любые изменения, зафиксированные в базе данных hello всегда будут представлены.</span><span class="sxs-lookup"><span data-stu-id="704f6-170">Durability ensures that any change that’s committed in hello database will always be present.</span></span>   

<span data-ttu-id="704f6-171">В Cosmos DB JavaScript размещается в hello же области памяти, что hello базы данных.</span><span class="sxs-lookup"><span data-stu-id="704f6-171">In Cosmos DB, JavaScript is hosted in hello same memory space as hello database.</span></span> <span data-ttu-id="704f6-172">Таким образом, запросы, входящие в хранимые процедуры и триггеры выполняются в hello же области сеанса базы данных.</span><span class="sxs-lookup"><span data-stu-id="704f6-172">Hence, requests made within stored procedures and triggers execute in hello same scope of a database session.</span></span> <span data-ttu-id="704f6-173">Это позволяет tooguarantee Cosmos DB ACID для всех операций, которые являются частью одной хранимой процедуры или триггера.</span><span class="sxs-lookup"><span data-stu-id="704f6-173">This enables Cosmos DB tooguarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="704f6-174">Рассмотрим следующие hello хранимой процедуры определение:</span><span class="sxs-lookup"><span data-stu-id="704f6-174">Consider hello following stored procedure definition:</span></span>

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="704f6-175">Эта хранимая процедура использует транзакции внутри элементов игры приложения tootrade между двумя участниками в одной операции.</span><span class="sxs-lookup"><span data-stu-id="704f6-175">This stored procedure uses transactions within a gaming app tootrade items between two players in a single operation.</span></span> <span data-ttu-id="704f6-176">Hello хранимой процедуры попыток tooread двух документов, над которыми игроки toohello соответствующие идентификаторы переданному в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="704f6-176">hello stored procedure attempts tooread two documents each corresponding toohello player IDs passed in as an argument.</span></span> <span data-ttu-id="704f6-177">При обнаружении оба проигрывателя документов, hello хранимой процедуры обновляет hello документов путем переключения их элементов.</span><span class="sxs-lookup"><span data-stu-id="704f6-177">If both player documents are found, then hello stored procedure updates hello documents by swapping their items.</span></span> <span data-ttu-id="704f6-178">Все ошибки, возникающие в процессе страницы приветствия, выдает исключение JavaScript, который неявно прерывает транзакцию hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-178">If any errors are encountered along hello way, it throws a JavaScript exception that implicitly aborts hello transaction.</span></span>

<span data-ttu-id="704f6-179">Если hello коллекции hello хранимой процедуры регистрации для коллекции одной секции, то hello транзакция с областью tooall hello документы в коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-179">If hello collection hello stored procedure is registered against is a single-partition collection, then hello transaction is scoped tooall hello documents within hello collection.</span></span> <span data-ttu-id="704f6-180">Если коллекция hello секционирована, хранимые процедуры выполняются в области транзакции hello ключа одной секции.</span><span class="sxs-lookup"><span data-stu-id="704f6-180">If hello collection is partitioned, then stored procedures are executed in hello transaction scope of a single partition key.</span></span> <span data-ttu-id="704f6-181">Каждый хранимой процедуры выполнения затем должен включать значение ключа секции соответствующей транзакции hello области toohello должны запускаться от имени.</span><span class="sxs-lookup"><span data-stu-id="704f6-181">Each stored procedure execution must then include a partition key value corresponding toohello scope hello transaction must run under.</span></span> <span data-ttu-id="704f6-182">Дополнительные сведения см. в статье [Секционирование, ключи секции и масштабирование в Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="704f6-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="704f6-183">Фиксация и откат транзакций</span><span class="sxs-lookup"><span data-stu-id="704f6-183">Commit and rollback</span></span>
<span data-ttu-id="704f6-184">Транзакции глубоко и изначально интегрированы в модель программирования JavaScript в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="704f6-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="704f6-185">Внутри функции JavaScript все операции автоматически обернуты в одной транзакции.</span><span class="sxs-lookup"><span data-stu-id="704f6-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="704f6-186">Если hello JavaScript завершается без любое исключение, фиксируются hello toohello рабочей базы данных.</span><span class="sxs-lookup"><span data-stu-id="704f6-186">If hello JavaScript completes without any exception, hello operations toohello database are committed.</span></span> <span data-ttu-id="704f6-187">В результате hello «BEGIN TRANSACTION» и «ЗАФИКСИРОВАТЬ ТРАНЗАКЦИИ» инструкции в реляционных базах данных являются неявно в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="704f6-187">In effect, hello “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="704f6-188">Если любое исключение, которое распространяется от сценария hello, Cosmos DB среды выполнения JavaScript будет откат всей транзакции hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-188">If there is any exception that’s propagated from hello script, Cosmos DB’s JavaScript runtime will roll back hello whole transaction.</span></span> <span data-ttu-id="704f6-189">Как показано выше в hello пример, исключение является эффективно эквивалентные tooa «ОТКАТ ТРАНЗАКЦИИ» в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="704f6-189">As shown in hello earlier example, throwing an exception is effectively equivalent tooa “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="704f6-190">Согласованность данных</span><span class="sxs-lookup"><span data-stu-id="704f6-190">Data consistency</span></span>
<span data-ttu-id="704f6-191">Хранимые процедуры и триггеры, всегда выполняются в первичной реплике hello hello Azure Cosmos DB контейнера.</span><span class="sxs-lookup"><span data-stu-id="704f6-191">Stored procedures and triggers are always executed on hello primary replica of hello Azure Cosmos DB container.</span></span> <span data-ttu-id="704f6-192">Гарантируется, что операции чтения в хранимых процедурах обеспечивают сильную согласованность.</span><span class="sxs-lookup"><span data-stu-id="704f6-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="704f6-193">Запросы, использующие определяемые пользователем функции могут быть выполнены для hello первичного или любой из вторичных реплик, но мы обеспечиваем toomeet hello запрошенный уровень согласованности, выбрав соответствующую реплику hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-193">Queries using user defined functions can be executed on hello primary or any secondary replica, but we ensure toomeet hello requested consistency level by choosing hello appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="704f6-194">Ограниченное выполнение</span><span class="sxs-lookup"><span data-stu-id="704f6-194">Bounded execution</span></span>
<span data-ttu-id="704f6-195">Все операции Cosmos DB должен быть выполнен в указанный сервер hello длительность времени ожидания запроса.</span><span class="sxs-lookup"><span data-stu-id="704f6-195">All Cosmos DB operations must complete within hello server specified request timeout duration.</span></span> <span data-ttu-id="704f6-196">Это ограничение также применяется tooJavaScript функции (хранимые процедуры, триггеры и определяемые пользователем функции).</span><span class="sxs-lookup"><span data-stu-id="704f6-196">This constraint also applies tooJavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="704f6-197">Если операция не выполнена с указанного времени, hello транзакция откатывается.</span><span class="sxs-lookup"><span data-stu-id="704f6-197">If an operation does not complete with that time limit, hello transaction is rolled back.</span></span> <span data-ttu-id="704f6-198">Функции JavaScript необходимо завершить в течение ограниченного времени hello или реализовать продолжение на основе модели toobatch или возобновления выполнения.</span><span class="sxs-lookup"><span data-stu-id="704f6-198">JavaScript functions must finish within hello time limit or implement a continuation based model toobatch/resume execution.</span></span>  

<span data-ttu-id="704f6-199">Порядок разработки toosimplify хранимых процедур и триггеров toohandle ограничений по времени, все функции hello объекта коллекции (для создание, чтение, замена и удаление документов и вложения) возвращают логическое значение, представляющее ли, Операция будет завершена.</span><span class="sxs-lookup"><span data-stu-id="704f6-199">In order toosimplify development of stored procedures and triggers toohandle time limits, all functions under hello collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="704f6-200">Если это значение равно false, это означает, что лимит времени hello о tooexpire и заключать скорость выполнения этой процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-200">If this value is false, it is an indication that hello time limit is about tooexpire and that hello procedure must wrap up execution.</span></span>  <span data-ttu-id="704f6-201">Первая операция неподдерживаемого хранилища операций в очереди предыдущих toohello гарантируется toocomplete, если hello хранимой процедуры завершается за время, а не помещает в очередь запросы.</span><span class="sxs-lookup"><span data-stu-id="704f6-201">Operations queued prior toohello first unaccepted store operation are guaranteed toocomplete if hello stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="704f6-202">Функции JavaScript также ограничены в потреблении ресурсов.</span><span class="sxs-lookup"><span data-stu-id="704f6-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="704f6-203">Cosmos DB резервирование пропускной способности для коллекции, в зависимости от размера hello подготовить учетную запись базы данных.</span><span class="sxs-lookup"><span data-stu-id="704f6-203">Cosmos DB reserves throughput per collection based on hello provisioned size of a database account.</span></span> <span data-ttu-id="704f6-204">Пропускная способность выражается в форме нормализованных единиц потребления ресурсов процессора, памяти и ввода-вывода, именуемых «единица запроса» или RU.</span><span class="sxs-lookup"><span data-stu-id="704f6-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="704f6-205">Функции JavaScript потенциально можно использовать большое количество RUs через короткое время и может получить ограниченной по скорости при достижении ограничения объема hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="704f6-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if hello collection’s limit is reached.</span></span> <span data-ttu-id="704f6-206">Хранимые процедуры с большим объемом ресурсов также может доступности помещенные в карантин tooensure операций примитивов базы данных.</span><span class="sxs-lookup"><span data-stu-id="704f6-206">Resource intensive stored procedures might also be quarantined tooensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="704f6-207">Пример. Массовый импорт данных в программу базы данных</span><span class="sxs-lookup"><span data-stu-id="704f6-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="704f6-208">Ниже приведен пример хранимой процедуры, которая записывается в коллекцию toobulk импорта документов.</span><span class="sxs-lookup"><span data-stu-id="704f6-208">Below is an example of a stored procedure that is written toobulk-import documents into a collection.</span></span> <span data-ttu-id="704f6-209">Примечание о том, как hello выполнения хранимой процедуры ограниченных дескрипторов, проверьте hello логическое значение возвращаемое значение из createDocument и затем использует hello число документов, которые вставлены при каждом вызове hello хранимой процедуры tootrack и resume ход выполнения для пакетов.</span><span class="sxs-lookup"><span data-stu-id="704f6-209">Note how hello stored procedure handles bounded execution by checking hello Boolean return value from createDocument, and then uses hello count of documents inserted in each invocation of hello stored procedure tootrack and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="704f6-210"><a id="trigger"></a> Триггеры базы данных</span><span class="sxs-lookup"><span data-stu-id="704f6-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="704f6-211">Триггеры базы данных со срабатыванием до наступления события</span><span class="sxs-lookup"><span data-stu-id="704f6-211">Database pre-triggers</span></span>
<span data-ttu-id="704f6-212">Cosmos DB предоставляет триггеры, которые выполняются или запускаются при выполнении операций над документом.</span><span class="sxs-lookup"><span data-stu-id="704f6-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="704f6-213">Например можно указать до триггер при создании документа — это предварительная триггер будет запущен до создания документа hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before hello document is created.</span></span> <span data-ttu-id="704f6-214">Hello ниже приведен пример как Pre-триггеры могут быть используется toovalidate hello свойства документа, который находится в процессе создания:</span><span class="sxs-lookup"><span data-stu-id="704f6-214">hello following is an example of how pre-triggers can be used toovalidate hello properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="704f6-215">И соответствующее Node.js регистрации клиентского кода для триггера hello hello:</span><span class="sxs-lookup"><span data-stu-id="704f6-215">And hello corresponding Node.js client-side registration code for hello trigger:</span></span>

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


<span data-ttu-id="704f6-216">Триггеры со срабатыванием до наступления события не могут иметь никаких входных параметров.</span><span class="sxs-lookup"><span data-stu-id="704f6-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="704f6-217">Hello объекта запроса может быть запроса используется toomanipulate приветственное сообщение, связанное с операцией hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-217">hello request object can be used toomanipulate hello request message associated with hello operation.</span></span> <span data-ttu-id="704f6-218">Здесь hello предварительной триггер запускается с hello Создание документа, а тело сообщения hello запроса содержит toobe hello документа, созданные в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="704f6-218">Here, hello pre-trigger is being run with hello creation of a document, and hello request message body contains hello document toobe created in JSON format.</span></span>   

<span data-ttu-id="704f6-219">Когда зарегистрировать триггеры, пользователи могут указать hello операций, которые она может использовать.</span><span class="sxs-lookup"><span data-stu-id="704f6-219">When triggers are registered, users can specify hello operations that it can run with.</span></span> <span data-ttu-id="704f6-220">Этот триггер был создан с TriggerOperation.Create, это означает, что следующие hello не допускается.</span><span class="sxs-lookup"><span data-stu-id="704f6-220">This trigger was created with TriggerOperation.Create, which means hello following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="704f6-221">Пост-триггеры базы данных</span><span class="sxs-lookup"><span data-stu-id="704f6-221">Database post-triggers</span></span>
<span data-ttu-id="704f6-222">Пост-триггеры, как и пред-триггеры, связаны с операцией на документе и не принимают никаких входных параметров.</span><span class="sxs-lookup"><span data-stu-id="704f6-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="704f6-223">Они выполняются **после** hello операции завершения, а также иметь доступ toohello ответное сообщение, отправляемое toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="704f6-223">They run **after** hello operation has completed, and have access toohello response message that is sent toohello client.</span></span>   

<span data-ttu-id="704f6-224">Следующий пример Hello показывает POST-триггеры в действии:</span><span class="sxs-lookup"><span data-stu-id="704f6-224">hello following example shows post-triggers in action:</span></span>

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="704f6-225">Hello триггера может быть зарегистрирован как показано в следующих образец hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-225">hello trigger can be registered as shown in hello following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


<span data-ttu-id="704f6-226">Этот триггер запрашивает документ метаданных hello и обновляет его с подробными сведениями о только что созданный hello документа.</span><span class="sxs-lookup"><span data-stu-id="704f6-226">This trigger queries for hello metadata document and updates it with details about hello newly created document.</span></span>  

<span data-ttu-id="704f6-227">Одно из важных toonote — hello **транзакций** выполнения триггеров в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="704f6-227">One thing that is important toonote is hello **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="704f6-228">После триггера запускается как часть hello же транзакции, что создание hello hello исходного документа.</span><span class="sxs-lookup"><span data-stu-id="704f6-228">This post-trigger runs as part of hello same transaction as hello creation of hello original document.</span></span> <span data-ttu-id="704f6-229">Таким образом Если мы создаем исключение из триггера после hello (скажем, если настоящий документ метаданных не удается tooupdate hello), hello вся транзакция завершится ошибкой и будет выполнен откат.</span><span class="sxs-lookup"><span data-stu-id="704f6-229">Therefore, if we throw an exception from hello post-trigger (say if we are unable tooupdate hello metadata document), hello whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="704f6-230">Ни один документ не будет создан, будет возвращено исключение.</span><span class="sxs-lookup"><span data-stu-id="704f6-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="704f6-231"><a id="udf"></a>Функции, определяемые пользователем</span><span class="sxs-lookup"><span data-stu-id="704f6-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="704f6-232">Определяемые пользователем функции (UDF), грамматики языка запросов DocumentDB API SQL hello используется tooextend и реализации пользовательской бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="704f6-232">User-defined functions (UDFs) are used tooextend hello DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="704f6-233">Функции можно вызывать только из запросов.</span><span class="sxs-lookup"><span data-stu-id="704f6-233">They can only be called from inside queries.</span></span> <span data-ttu-id="704f6-234">Они не имеют доступа к toohello контекста объекта и предназначены toobe служит только для вычислительных JavaScript.</span><span class="sxs-lookup"><span data-stu-id="704f6-234">They do not have access toohello context object and are meant toobe used as compute-only JavaScript.</span></span> <span data-ttu-id="704f6-235">Таким образом определяемые пользователем функции выполняются во вторичных репликах hello Cosmos DB службы.</span><span class="sxs-lookup"><span data-stu-id="704f6-235">Therefore, UDFs can be run on secondary replicas of hello Cosmos DB service.</span></span>  

<span data-ttu-id="704f6-236">Hello следующий пример создает подоходного налога toocalculate определяемой пользователем функции, в зависимости от скорости для различных скобки доход и использует его внутри toofind запрос всех лиц, которые оплачено налогов более 20 000 долларов США.</span><span class="sxs-lookup"><span data-stu-id="704f6-236">hello following sample creates a UDF toocalculate income tax based on rates for various income brackets, and then uses it inside a query toofind all people who paid more than $20,000 in taxes.</span></span>

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


<span data-ttu-id="704f6-237">Hello определяемой пользователем функции могут использоваться в дальнейшем в запросах, как и в следующий образец hello:</span><span class="sxs-lookup"><span data-stu-id="704f6-237">hello UDF can subsequently be used in queries like in hello following sample:</span></span>

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="704f6-238">API запросов, интегрированный в язык JavaScript</span><span class="sxs-lookup"><span data-stu-id="704f6-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="704f6-239">Кроме tooissuing запросов с помощью элемента DocumentDB грамматику SQL, hello SDK на стороне сервера можно tooperform оптимизированных запросов, с помощью интерфейса Fluent на основе JavaScript, без знания SQL.</span><span class="sxs-lookup"><span data-stu-id="704f6-239">In addition tooissuing queries using DocumentDB’s SQL grammar, hello server-side SDK allows you tooperform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="704f6-240">вызывает запрос Hello JavaScript, который прикладной программный Интерфейс позволяет tooprogrammatically построения запросов путем передачи в функцию цепочкам функции предикатов с встроенных элементов массива и популярные библиотек JavaScript, таких как lodash синтаксис знакомый tooECMAScript5 элемента.</span><span class="sxs-lookup"><span data-stu-id="704f6-240">hello JavaScript query API allows you tooprogrammatically build queries by passing predicate functions into chainable function calls, with a syntax familiar tooECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="704f6-241">Запросы, обрабатываются с toobe среды выполнения JavaScript hello, выполнен эффективно с использованием Azure Cosmos DB индексов.</span><span class="sxs-lookup"><span data-stu-id="704f6-241">Queries are parsed by hello JavaScript runtime toobe executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="704f6-242">`__`(двойным подчеркиванием) — это псевдоним слишком`getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="704f6-242">`__` (double-underscore) is an alias too`getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="704f6-243">Другими словами, можно использовать `__` или `getContext().getCollection()` tooaccess hello запроса API JavaScript.</span><span class="sxs-lookup"><span data-stu-id="704f6-243">In other words, you can use `__` or `getContext().getCollection()` tooaccess hello JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="704f6-244">Поддерживаемые функции включают:</span><span class="sxs-lookup"><span data-stu-id="704f6-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="704f6-245">
<b>chain() ... .value([обратный вызов] [, параметры])</b>
</span><span class="sxs-lookup"><span data-stu-id="704f6-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="704f6-246">Запускается вызов по цепочке, который должен завершаться value().</span><span class="sxs-lookup"><span data-stu-id="704f6-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="704f6-247">
<b>filter(predicateFunction [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="704f6-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="704f6-248">Фильтрация ввода с помощью функции предиката, которая возвращает true или false, в порядке toofilter ожидания входных документов в результирующем наборе hello hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-248">Filters hello input using a predicate function which returns true/false in order toofilter in/out input documents into hello resulting set.</span></span> <span data-ttu-id="704f6-249">Это поведение аналогично tooa предложения WHERE в SQL.</span><span class="sxs-lookup"><span data-stu-id="704f6-249">This behaves similar tooa WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="704f6-250">
<b>map(transformationFunction [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="704f6-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="704f6-251">Применяет проекции, функции преобразования, используемый для сопоставления каждого входного элемента tooa JavaScript объект или значение.</span><span class="sxs-lookup"><span data-stu-id="704f6-251">Applies a projection given a transformation function which maps each input item tooa JavaScript object or value.</span></span> <span data-ttu-id="704f6-252">Это ведет себя аналогично tooa предложении SELECT SQL.</span><span class="sxs-lookup"><span data-stu-id="704f6-252">This behaves similar tooa SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="704f6-253">
<b>pluck([propertyName] [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="704f6-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="704f6-254">Это ярлык для карты, которая извлекает значение hello одно свойство из каждого входного элемента.</span><span class="sxs-lookup"><span data-stu-id="704f6-254">This is a shortcut for a map which extracts hello value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="704f6-255">
<b>flatten([isShallow] [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="704f6-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="704f6-256">Объединяет и выполняет сведение массивов из каждого входного элемента в один массив tooa.</span><span class="sxs-lookup"><span data-stu-id="704f6-256">Combines and flattens arrays from each input item in tooa single array.</span></span> <span data-ttu-id="704f6-257">Это ведет себя аналогично tooSelectMany в LINQ.</span><span class="sxs-lookup"><span data-stu-id="704f6-257">This behaves similar tooSelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="704f6-258">
<b>sortBy([предикат] [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="704f6-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="704f6-259">Создает новый набор документов, сортируя документов hello в потоке входной документ hello в возрастающем порядке, с помощью hello заданному предикату.</span><span class="sxs-lookup"><span data-stu-id="704f6-259">Produce a new set of documents by sorting hello documents in hello input document stream in ascending order using hello given predicate.</span></span> <span data-ttu-id="704f6-260">Это ведет себя аналогично tooa предложение ORDER BY в SQL.</span><span class="sxs-lookup"><span data-stu-id="704f6-260">This behaves similar tooa ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="704f6-261">
<b>sortByDescending([предикат] [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="704f6-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="704f6-262">Создает новый набор документов, сортируя документов hello в потоке входной документ hello в порядке убывания с использованием hello заданному предикату.</span><span class="sxs-lookup"><span data-stu-id="704f6-262">Produce a new set of documents by sorting hello documents in hello input document stream in descending order using hello given predicate.</span></span> <span data-ttu-id="704f6-263">Это ведет себя аналогично предложения ORDER BY x DESC tooa в SQL.</span><span class="sxs-lookup"><span data-stu-id="704f6-263">This behaves similar tooa ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="704f6-264">При включении в функции предиката или селектор hello следующие конструкции JavaScript получить автоматически оптимизированного toorun непосредственно на Azure Cosmos DB индексов:</span><span class="sxs-lookup"><span data-stu-id="704f6-264">When included inside predicate and/or selector functions, hello following JavaScript constructs get automatically optimized toorun directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="704f6-265">Простые операторы: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="704f6-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="704f6-266">Литералы, включая литерал hello объекта: {}</span><span class="sxs-lookup"><span data-stu-id="704f6-266">Literals, including hello object literal: {}</span></span>
* <span data-ttu-id="704f6-267">var, return.</span><span class="sxs-lookup"><span data-stu-id="704f6-267">var, return</span></span>

<span data-ttu-id="704f6-268">создает следующие JavaScript приветствия получить не оптимизирован для индексов Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="704f6-268">hello following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="704f6-269">поток управления (например, if, for, while);</span><span class="sxs-lookup"><span data-stu-id="704f6-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="704f6-270">вызовы функций.</span><span class="sxs-lookup"><span data-stu-id="704f6-270">Function calls</span></span>

<span data-ttu-id="704f6-271">Чтобы узнать больше, ознакомьтесь с [документацией JavaScript по серверам](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="704f6-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a><span data-ttu-id="704f6-272">Пример: Написать хранимую процедуру с помощью API-Интерфейс запросов JavaScript hello</span><span class="sxs-lookup"><span data-stu-id="704f6-272">Example: Write a stored procedure using hello JavaScript query API</span></span>
<span data-ttu-id="704f6-273">Привет, следующий образец кода приведен пример использования hello запроса API JavaScript в контексте hello хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="704f6-273">hello following code sample is an example of how hello JavaScript Query API can be used in hello context of a stored procedure.</span></span> <span data-ttu-id="704f6-274">Hello хранимая процедура вставляет документ, выданный входного параметра и обновляет документ метаданных с помощью hello `__.filter()` метод minSize, maxSize и totalSize на основе свойства size hello входной документ.</span><span class="sxs-lookup"><span data-stu-id="704f6-274">hello stored procedure inserts a document, given by an input parameter, and updates a metadata document, using hello `__.filter()` method, with minSize, maxSize, and totalSize based upon hello input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a><span data-ttu-id="704f6-275">SQL tooJavascript памятку.</span><span class="sxs-lookup"><span data-stu-id="704f6-275">SQL tooJavascript cheat sheet</span></span>
<span data-ttu-id="704f6-276">Hello следующей таблице представлены различные запросы SQL и соответствующих запросах JavaScript hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-276">hello following table presents various SQL queries and hello corresponding JavaScript queries.</span></span>

<span data-ttu-id="704f6-277">Как и запросы SQL, ключи свойств документов (например, `doc.id`) чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="704f6-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="704f6-278">SQL</span><span class="sxs-lookup"><span data-stu-id="704f6-278">SQL</span></span>| <span data-ttu-id="704f6-279">API запроса JavaScript</span><span class="sxs-lookup"><span data-stu-id="704f6-279">JavaScript Query API</span></span>|<span data-ttu-id="704f6-280">Описание приведено ниже</span><span class="sxs-lookup"><span data-stu-id="704f6-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="704f6-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="704f6-281">SELECT *</span></span><br><span data-ttu-id="704f6-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="704f6-282">FROM docs</span></span>| <span data-ttu-id="704f6-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="704f6-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="704f6-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="704f6-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="704f6-285">});</span><span class="sxs-lookup"><span data-stu-id="704f6-285">});</span></span>|<span data-ttu-id="704f6-286">1</span><span class="sxs-lookup"><span data-stu-id="704f6-286">1</span></span>|
|<span data-ttu-id="704f6-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="704f6-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="704f6-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="704f6-288">FROM docs</span></span>|<span data-ttu-id="704f6-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="704f6-289">__.map(function(doc) {</span></span><br><span data-ttu-id="704f6-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="704f6-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="704f6-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="704f6-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="704f6-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="704f6-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="704f6-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="704f6-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="704f6-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="704f6-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="704f6-295">});</span><span class="sxs-lookup"><span data-stu-id="704f6-295">});</span></span>|<span data-ttu-id="704f6-296">2</span><span class="sxs-lookup"><span data-stu-id="704f6-296">2</span></span>|
|<span data-ttu-id="704f6-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="704f6-297">SELECT *</span></span><br><span data-ttu-id="704f6-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="704f6-298">FROM docs</span></span><br><span data-ttu-id="704f6-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="704f6-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="704f6-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="704f6-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="704f6-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="704f6-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="704f6-302">});</span><span class="sxs-lookup"><span data-stu-id="704f6-302">});</span></span>|<span data-ttu-id="704f6-303">3</span><span class="sxs-lookup"><span data-stu-id="704f6-303">3</span></span>|
|<span data-ttu-id="704f6-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="704f6-304">SELECT *</span></span><br><span data-ttu-id="704f6-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="704f6-305">FROM docs</span></span><br><span data-ttu-id="704f6-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="704f6-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="704f6-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="704f6-307">__.filter(function(x) {</span></span><br><span data-ttu-id="704f6-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="704f6-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="704f6-309">});</span><span class="sxs-lookup"><span data-stu-id="704f6-309">});</span></span>|<span data-ttu-id="704f6-310">4.</span><span class="sxs-lookup"><span data-stu-id="704f6-310">4</span></span>|
|<span data-ttu-id="704f6-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="704f6-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="704f6-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="704f6-312">FROM docs</span></span><br><span data-ttu-id="704f6-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="704f6-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="704f6-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="704f6-314">__.chain()</span></span><br><span data-ttu-id="704f6-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="704f6-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="704f6-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="704f6-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="704f6-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="704f6-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="704f6-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="704f6-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="704f6-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="704f6-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="704f6-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="704f6-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="704f6-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="704f6-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="704f6-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="704f6-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="704f6-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="704f6-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="704f6-324">.value();</span><span class="sxs-lookup"><span data-stu-id="704f6-324">.value();</span></span>|<span data-ttu-id="704f6-325">5</span><span class="sxs-lookup"><span data-stu-id="704f6-325">5</span></span>|
|<span data-ttu-id="704f6-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="704f6-326">SELECT VALUE tag</span></span><br><span data-ttu-id="704f6-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="704f6-327">FROM docs</span></span><br><span data-ttu-id="704f6-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="704f6-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="704f6-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="704f6-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="704f6-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="704f6-330">__.chain()</span></span><br><span data-ttu-id="704f6-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="704f6-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="704f6-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="704f6-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="704f6-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="704f6-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="704f6-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="704f6-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="704f6-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="704f6-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="704f6-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="704f6-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="704f6-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="704f6-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="704f6-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="704f6-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="704f6-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="704f6-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="704f6-340">6</span><span class="sxs-lookup"><span data-stu-id="704f6-340">6</span></span>|

<span data-ttu-id="704f6-341">Hello следующие описания объясняется каждый запрос в приведенной выше таблице hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-341">hello following descriptions explain each query in hello table above.</span></span>
1. <span data-ttu-id="704f6-342">Возвращает все документы (с разбивкой на страницы с отметками "продолжить").</span><span class="sxs-lookup"><span data-stu-id="704f6-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="704f6-343">Идентификатор hello проекты, сообщение (псевдоним toomsg) и действия из всех документов.</span><span class="sxs-lookup"><span data-stu-id="704f6-343">Projects hello id, message (aliased toomsg), and action from all documents.</span></span>
3. <span data-ttu-id="704f6-344">Запросы для документов с предикатом hello: идентификатор = «X998_Y998».</span><span class="sxs-lookup"><span data-stu-id="704f6-344">Queries for documents with hello predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="704f6-345">Количество запросов для документов, имеющих свойство метки и тегов — массив, содержащий значение hello 123.</span><span class="sxs-lookup"><span data-stu-id="704f6-345">Queries for documents that have a Tags property and Tags is an array containing hello value 123.</span></span>
5. <span data-ttu-id="704f6-346">Запросы для документов с предикатом, id = «X998_Y998», а затем id hello проекты и сообщений (псевдоним toomsg).</span><span class="sxs-lookup"><span data-stu-id="704f6-346">Queries for documents with a predicate, id = "X998_Y998", and then projects hello id and message (aliased toomsg).</span></span>
6. <span data-ttu-id="704f6-347">Фильтры для документов, которые имеют свойства массива, теги, и сортирует полученный документы hello свойством hello _ts отметка времени системы и затем + выполняет сведение массив тегов hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-347">Filters for documents which have an array property, Tags, and sorts hello resulting documents by hello _ts timestamp system property, and then projects + flattens hello Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="704f6-348">Поддержка времени выполнения</span><span class="sxs-lookup"><span data-stu-id="704f6-348">Runtime support</span></span>
<span data-ttu-id="704f6-349">[API стороны сервера DocumentDB JavaScript](http://azure.github.io/azure-documentdb-js-server/) обеспечивает поддержку hello большинство hello массовых функции языка JavaScript по мере стандартизированные по [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="704f6-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for hello most of hello mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="704f6-350">Безопасность</span><span class="sxs-lookup"><span data-stu-id="704f6-350">Security</span></span>
<span data-ttu-id="704f6-351">JavaScript хранимых процедур и триггеров в виде изолированного, эффекты hello один скрипт не приводят к утечке toohello других минуя hello изоляцию транзакций моментальных снимков на уровне базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-351">JavaScript stored procedures and triggers are sandboxed so that hello effects of one script do not leak toohello other without going through hello snapshot transaction isolation at hello database level.</span></span> <span data-ttu-id="704f6-352">среды выполнения Hello в пул, но удаляются контекста hello после каждого запуска.</span><span class="sxs-lookup"><span data-stu-id="704f6-352">hello runtime environments are pooled but cleaned of hello context after each run.</span></span> <span data-ttu-id="704f6-353">Поэтому они гарантированно toobe безопасный из любой непредвиденные побочные эффекты друг от друга.</span><span class="sxs-lookup"><span data-stu-id="704f6-353">Hence they are guaranteed toobe safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="704f6-354">Предварительная компиляция</span><span class="sxs-lookup"><span data-stu-id="704f6-354">Pre-compilation</span></span>
<span data-ttu-id="704f6-355">Хранимые процедуры, триггеры и определяемые пользователем функции являются неявно предкомпилированного toohello формат кода байтов в стоимости компиляции tooavoid порядок во время каждого вызова скрипта hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-355">Stored procedures, triggers and UDFs are implicitly precompiled toohello byte code format in order tooavoid compilation cost at hello time of each script invocation.</span></span> <span data-ttu-id="704f6-356">Это гарантирует высокую скорость и низкие затраты на вызовы хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="704f6-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="704f6-357">Поддержка клиентских пакетов SDK</span><span class="sxs-lookup"><span data-stu-id="704f6-357">Client SDK support</span></span>
<span data-ttu-id="704f6-358">В дополнение toohello DocumentDB API для [Node.js](documentdb-sdk-node.md) клиента Azure Cosmos DB [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), и [Python SDK](documentdb-sdk-python.md) для hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="704f6-358">In addition toohello DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for hello DocumentDB API.</span></span> <span data-ttu-id="704f6-359">Хранимые процедуры, триггеры и пользовательские функции могут быть созданы и выполнены с использованием любого из этих пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="704f6-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="704f6-360">Следующий пример показывает как Hello toocreate и выполнение хранимой процедуры с помощью клиента .NET hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-360">hello following example shows how toocreate and execute a stored procedure using hello .NET client.</span></span> <span data-ttu-id="704f6-361">Обратите внимание, как типы .NET hello передаются в hello хранимую процедуру как JSON и повторного считывания.</span><span class="sxs-lookup"><span data-stu-id="704f6-361">Note how hello .NET types are passed into hello stored procedure as JSON and read back.</span></span>

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


<span data-ttu-id="704f6-362">В этом примере показано, как toouse hello [API .NET для DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate предварительной триггера и Создание документа с включен триггер hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-362">This sample shows how toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate a pre-trigger and create a document with hello trigger enabled.</span></span> 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


<span data-ttu-id="704f6-363">И hello в следующем примере показано, как toocreate пользователь определяемой функции (UDF) и использовать его в [запроса DocumentDB API SQL](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="704f6-363">And hello following example shows how toocreate a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a><span data-ttu-id="704f6-364">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="704f6-364">REST API</span></span>
<span data-ttu-id="704f6-365">Все операции Azure Cosmos DB могут быть выполнены в RESTful-образе.</span><span class="sxs-lookup"><span data-stu-id="704f6-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="704f6-366">Хранимые процедуры, триггеры и пользовательские функции могут быть зарегистрированы в соответствии с коллекцией с помощью команды POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="704f6-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="704f6-367">Hello ниже приведен пример того, как tooregister хранимой процедуры:</span><span class="sxs-lookup"><span data-stu-id="704f6-367">hello following is an example of how tooregister a stored procedure:</span></span>

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


<span data-ttu-id="704f6-368">Hello хранимую процедуру регистрации, выполнив запрос методом POST для hello URI баз данных SQL Server/testdb/colls/testColl/sprocs содержит текст hello hello toocreate хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="704f6-368">hello stored procedure is registered by executing a POST request against hello URI dbs/testdb/colls/testColl/sprocs with hello body containing hello stored procedure toocreate.</span></span> <span data-ttu-id="704f6-369">Триггеры и функции UDF могут быть зарегистрированы аналогичным образом путем выполнения команды POST с идентификаторами /triggers и /udfs соответственно.</span><span class="sxs-lookup"><span data-stu-id="704f6-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="704f6-370">Эту хранимую процедуру затем можно выполнить, отправив запрос POST со ссылкой на ее ресурс.</span><span class="sxs-lookup"><span data-stu-id="704f6-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


<span data-ttu-id="704f6-371">Здесь hello ввода toohello хранимой процедуры передается в тексте запроса hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-371">Here, hello input toohello stored procedure is passed in hello request body.</span></span> <span data-ttu-id="704f6-372">Обратите внимание, что hello входные данные передаются как массив JSON входных параметров.</span><span class="sxs-lookup"><span data-stu-id="704f6-372">Note that hello input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="704f6-373">Hello хранимые процедуры принимает hello первого входа как документ, текст ответа.</span><span class="sxs-lookup"><span data-stu-id="704f6-373">hello stored procedure takes hello first input as a document that is a response body.</span></span> <span data-ttu-id="704f6-374">Hello ответа, которые мы получили выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="704f6-374">hello response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="704f6-375">Триггеры, в отличие от хранимых процедур, не могут быть выполнены непосредственно.</span><span class="sxs-lookup"><span data-stu-id="704f6-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="704f6-376">Вместо этого они выполняются как часть операции над документом.</span><span class="sxs-lookup"><span data-stu-id="704f6-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="704f6-377">Можно указать триггеры toorun hello вместе с запросом с помощью заголовков HTTP.</span><span class="sxs-lookup"><span data-stu-id="704f6-377">We can specify hello triggers toorun with a request using HTTP headers.</span></span> <span data-ttu-id="704f6-378">Hello ниже приведен запрос toocreate документа.</span><span class="sxs-lookup"><span data-stu-id="704f6-378">hello following is request toocreate a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="704f6-379">Здесь toobe предварительной триггер hello, запустите с запросом hello указывается в заголовке x-ms-documentdb-pre-trigger-include hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-379">Here hello pre-trigger toobe run with hello request is specified in hello x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="704f6-380">Соответственно либо после триггеров приведены в заголовок x-ms-documentdb-post-trigger-include hello.</span><span class="sxs-lookup"><span data-stu-id="704f6-380">Correspondingly, any post-triggers are given in hello x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="704f6-381">Обратите внимание, что для данного запроса могут быть определены оба вида триггеров.</span><span class="sxs-lookup"><span data-stu-id="704f6-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="704f6-382">Пример кода</span><span class="sxs-lookup"><span data-stu-id="704f6-382">Sample code</span></span>
<span data-ttu-id="704f6-383">Дополнительные примеры кода, используемого на сервере (включая операции [массового удаления](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) и [обновления](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)), представлены в нашем [репозитории GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="704f6-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="704f6-384">Требуется tooshare здорово хранимой процедуры?</span><span class="sxs-lookup"><span data-stu-id="704f6-384">Want tooshare your awesome stored procedure?</span></span> <span data-ttu-id="704f6-385">Отправьте нам запрос на получение.</span><span class="sxs-lookup"><span data-stu-id="704f6-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="704f6-386">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="704f6-386">Next steps</span></span>
<span data-ttu-id="704f6-387">После создания одного или нескольких хранимых процедур, триггеров и определяемых пользователем функций, созданных можно загрузить их и просматривать их в hello портал Azure с помощью данных обозревателя.</span><span class="sxs-lookup"><span data-stu-id="704f6-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in hello Azure portal using Data Explorer.</span></span>

<span data-ttu-id="704f6-388">Кроме того, возможно следующее hello ссылки и ресурсы, которые полезны в ваш путь toolearn больше о Azure Cosmos программирование на сервере базы данных:</span><span class="sxs-lookup"><span data-stu-id="704f6-388">You may also find hello following references and resources useful in your path toolearn more about Azure Cosmos dB server-side programming:</span></span>

* <span data-ttu-id="704f6-389">[Пакет SDK для DocumentDB .NET: скачивание и заметки о выпуске](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="704f6-389">[Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md)</span></span>
* [<span data-ttu-id="704f6-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="704f6-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="704f6-391">JSON</span><span class="sxs-lookup"><span data-stu-id="704f6-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="704f6-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="704f6-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="704f6-393">Безопасность и расширяемость переносной базы данных</span><span class="sxs-lookup"><span data-stu-id="704f6-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="704f6-394">Сервис-ориентированная архитектура баз данных</span><span class="sxs-lookup"><span data-stu-id="704f6-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="704f6-395">Размещение hello среды выполнения .NET в Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="704f6-395">Hosting hello .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

