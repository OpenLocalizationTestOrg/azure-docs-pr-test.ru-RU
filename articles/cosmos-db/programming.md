---
title: "Программирование серверных компонентов на JavaScript для Azure Cosmos DB | Документация Майкрософт"
description: "Узнайте, как с помощью Azure Cosmos DB писать хранимые процедуры, триггеры базы данных и определяемые пользователем функции (UDF) на JavaScript. Здесь вы найдете советы по программированию баз данных и многое другое."
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
ms.openlocfilehash: 8cddc7a8c9aa677b9c93bee3a7e05c226cc1f655
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a><span data-ttu-id="f3d42-105">Программирование Azure Cosmos DB на стороне сервера: хранимые процедуры, триггеры баз данных и определяемые пользователем функции</span><span class="sxs-lookup"><span data-stu-id="f3d42-105">Azure Cosmos DB server-side programming: Stored procedures, database triggers, and UDFs</span></span>
<span data-ttu-id="f3d42-106">Узнайте, каким образом интегрированное транзакционное выполнение JavaScript в Azure Cosmos DB позволяет разработчикам создавать **хранимые процедуры**, **триггеры** и **определяемые пользователем функции (UDF)** непосредственно на платформе JavaScript [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/).</span><span class="sxs-lookup"><span data-stu-id="f3d42-106">Learn how Azure Cosmos DB’s language integrated, transactional execution of JavaScript lets developers write **stored procedures**, **triggers** and **user defined functions (UDFs)** natively in an [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) JavaScript.</span></span> <span data-ttu-id="f3d42-107">Это позволяет разработчикам писать логику приложения для баз данных, которая может быть отправлена и выполнена непосредственно в разделе хранения базы данных.</span><span class="sxs-lookup"><span data-stu-id="f3d42-107">This allows you to write database program application logic that can be shipped and executed directly on the database storage partitions.</span></span> 

<span data-ttu-id="f3d42-108">Прежде чем приступить к работе, рекомендуется просмотреть следующий видеоролик, где Эндрю Лю (Andrew Liu) кратко представляет модель программирования баз данных на стороне сервера Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3d42-108">We recommend getting started by watching the following video, where Andrew Liu provides a brief introduction to Cosmos DB's server-side database programming model.</span></span> 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

<span data-ttu-id="f3d42-109">Затем вернитесь в эту статью, из которой вы узнаете ответы на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="f3d42-109">Then, return to this article, where you'll learn the answers to the following questions:</span></span>  

* <span data-ttu-id="f3d42-110">Как написать хранимую процедуру, триггер или определяемую пользователем Функцию на JavaScript?</span><span class="sxs-lookup"><span data-stu-id="f3d42-110">How do I write a a stored procedure, trigger, or UDF using JavaScript?</span></span>
* <span data-ttu-id="f3d42-111">Каким образом Cosmos DB предоставляет гарантию выполнения принципа ACID?</span><span class="sxs-lookup"><span data-stu-id="f3d42-111">How does Cosmos DB guarantee ACID?</span></span>
* <span data-ttu-id="f3d42-112">Каков принцип работы транзакций в Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="f3d42-112">How do transactions work in Cosmos DB?</span></span>
* <span data-ttu-id="f3d42-113">Что такое пред- и пост-триггеры, и как их написать?</span><span class="sxs-lookup"><span data-stu-id="f3d42-113">What are pre-triggers and post-triggers and how do I write one?</span></span>
* <span data-ttu-id="f3d42-114">Как зарегистрировать и выполнить хранимую процедуру, триггер или определяемую пользователем функции RESTful-образом по протоколу HTTP?</span><span class="sxs-lookup"><span data-stu-id="f3d42-114">How do I register and execute a stored procedure, trigger, or UDF in a RESTful manner by using HTTP?</span></span>
* <span data-ttu-id="f3d42-115">Какие пакеты SDK Cosmos DB доступны для создания и выполнения хранимых процедур, триггеров и определяемых пользователем функций?</span><span class="sxs-lookup"><span data-stu-id="f3d42-115">What Cosmos DB SDKs are available to create and execute stored procedures, triggers, and UDFs?</span></span>

## <a name="introduction-to-stored-procedure-and-udf-programming"></a><span data-ttu-id="f3d42-116">Введение в программирование хранимых процедур и определяемых пользователем функций</span><span class="sxs-lookup"><span data-stu-id="f3d42-116">Introduction to Stored Procedure and UDF Programming</span></span>
<span data-ttu-id="f3d42-117">Подход *«JavaScript — это современный T-SQL»* освобождает разработчиков приложений от сложностей системы, связанных с несоответствием типов и объектно-реляционных технологий сопоставления.</span><span class="sxs-lookup"><span data-stu-id="f3d42-117">This approach of *“JavaScript as a modern day T-SQL”* frees application developers from the complexities of type system mismatches and object-relational mapping technologies.</span></span> <span data-ttu-id="f3d42-118">Он также имеет ряд своих собственных преимуществ, которые могут быть использованы для создания мощных приложений:</span><span class="sxs-lookup"><span data-stu-id="f3d42-118">It also has a number of intrinsic advantages that can be utilized to build rich applications:</span></span>  

* <span data-ttu-id="f3d42-119">**Процедурная логика.** JavaScript, как язык программирования высокого уровня, обеспечивает многофункциональный и знакомый интерфейс для реализации бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="f3d42-119">**Procedural Logic:** JavaScript as a high level programming language, provides a rich and familiar interface to express business logic.</span></span> <span data-ttu-id="f3d42-120">Вы можете выполнять сложные последовательности операций ближе к данным.</span><span class="sxs-lookup"><span data-stu-id="f3d42-120">You can perform complex sequences of operations closer to the data.</span></span>
* <span data-ttu-id="f3d42-121">**Атомарные транзакции.** Cosmos DB гарантирует атомарность операций с базой данных, выполняемых внутри одной хранимой процедуры или триггера.</span><span class="sxs-lookup"><span data-stu-id="f3d42-121">**Atomic Transactions:** Cosmos DB guarantees that database operations performed inside a single stored procedure or trigger are atomic.</span></span> <span data-ttu-id="f3d42-122">Это позволяет приложению объединить соответствующие операции в пакетном режиме; таким образом, успешно будут выполнены либо все из них, либо ни одна.</span><span class="sxs-lookup"><span data-stu-id="f3d42-122">This lets an application combine related operations in a single batch so that either all of them succeed or none of them succeed.</span></span> 
* <span data-ttu-id="f3d42-123">**Производительность.** Тот факт, что JSON неразрывно связан с системой типов языка Javascript, а также является основной единицей хранения в Cosmos DB, позволяет использовать ряд оптимизаций, таких как отложенная материализация документов JSON в буферном пуле и доступ к ним для исполняемого кода по требованию.</span><span class="sxs-lookup"><span data-stu-id="f3d42-123">**Performance:** The fact that JSON is intrinsically mapped to the Javascript language type system and is also the basic unit of storage in Cosmos DB allows for a number of optimizations like lazy materialization of JSON documents in the buffer pool and making them available on-demand to the executing code.</span></span> <span data-ttu-id="f3d42-124">Есть еще больший выигрыш в производительности, связанный с доставкой бизнес-логики в базу данных:</span><span class="sxs-lookup"><span data-stu-id="f3d42-124">There are more performance benefits associated with shipping business logic to the database:</span></span>
  
  * <span data-ttu-id="f3d42-125">Пакеты — разработчики могут группировать операции, такие как вставка, и запускать их в пакетном режиме.</span><span class="sxs-lookup"><span data-stu-id="f3d42-125">Batching – Developers can group operations like inserts and submit them in bulk.</span></span> <span data-ttu-id="f3d42-126">Значительно сокращаются затраты на задержку сетевого трафика и накладные расходы для хранения при создании отдельных операций.</span><span class="sxs-lookup"><span data-stu-id="f3d42-126">The network traffic latency cost and the store overhead to create separate transactions are reduced significantly.</span></span> 
  * <span data-ttu-id="f3d42-127">Предварительная компиляция — Cosmos DB предварительно компилирует хранимые процедуры, триггеры и пользовательские функции (UDF), чтобы избежать задержки JavaScript при компиляции для каждого вызова.</span><span class="sxs-lookup"><span data-stu-id="f3d42-127">Pre-compilation – Cosmos DB precompiles stored procedures, triggers and user defined functions (UDFs) to avoid JavaScript compilation cost for each invocation.</span></span> <span data-ttu-id="f3d42-128">Накладные расходы на компиляцию байт-кода для процедурной логики амортизируются до минимального значения.</span><span class="sxs-lookup"><span data-stu-id="f3d42-128">The overhead of building the byte code for the procedural logic is amortized to a minimal value.</span></span>
  * <span data-ttu-id="f3d42-129">Секвенcирование — многим операции нужен побочный эффект («триггер»), что потенциально задействует выполнение одной или множества вторичных операций хранения.</span><span class="sxs-lookup"><span data-stu-id="f3d42-129">Sequencing – Many operations need a side-effect (“trigger”) that potentially involves doing one or many secondary store operations.</span></span> <span data-ttu-id="f3d42-130">Помимо обеспечения атомарности, приводит к повышению производительности при переносе на сервер.</span><span class="sxs-lookup"><span data-stu-id="f3d42-130">Aside from atomicity, this is more performant when moved to the server.</span></span> 
* <span data-ttu-id="f3d42-131">**Инкапсуляция.** Хранимые процедуры могут быть использованы для группировки бизнес-логики в одном месте.</span><span class="sxs-lookup"><span data-stu-id="f3d42-131">**Encapsulation:** Stored procedures can be used to group business logic in one place.</span></span> <span data-ttu-id="f3d42-132">Это принесет два преимущества:</span><span class="sxs-lookup"><span data-stu-id="f3d42-132">This has two advantages:</span></span>
  * <span data-ttu-id="f3d42-133">Добавление уровня абстракции поверх исходных данных, что позволяет архитекторам данных развивать свои приложения независимо от данных.</span><span class="sxs-lookup"><span data-stu-id="f3d42-133">It adds an abstraction layer on top of the raw data, which enables data architects to evolve their applications independently from the data.</span></span> <span data-ttu-id="f3d42-134">Это особенно выгодно, когда данные не имеют схемы, в связи с предположениями, что, возможно, потребуется реализованная в приложении схема, если придется работать с данными напрямую.</span><span class="sxs-lookup"><span data-stu-id="f3d42-134">This is particularly advantageous when the data is schema-less, due to the brittle assumptions that may need to be baked into the application if they have to deal with data directly.</span></span>  
  * <span data-ttu-id="f3d42-135">Эта абстракция позволяет предприятиям сохранить свои данные в безопасности, упрощая доступ к ним из сценариев.</span><span class="sxs-lookup"><span data-stu-id="f3d42-135">This abstraction lets enterprises keep their data secure by streamlining the access from the scripts.</span></span>  

<span data-ttu-id="f3d42-136">Создание и выполнение триггеров баз данных, хранимых процедур и операторов пользовательских запросов поддерживается с помощью [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases) и [клиентских пакетов SDK](documentdb-sdk-dotnet.md) на различных платформах, включая .NET, Node.js и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f3d42-136">The creation and execution of database triggers, stored procedure and custom query operators is supported through the [REST API](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), and [client SDKs](documentdb-sdk-dotnet.md) in many platforms including .NET, Node.js and JavaScript.</span></span>

<span data-ttu-id="f3d42-137">Для иллюстрации синтаксиса и использования хранимых процедур, триггеров и пользовательских функций в этом учебнике используется [пакет SDK для Node.js с обещаниями Q](http://azure.github.io/azure-documentdb-node-q/).</span><span class="sxs-lookup"><span data-stu-id="f3d42-137">This tutorial uses the [Node.js SDK with Q Promises](http://azure.github.io/azure-documentdb-node-q/) to illustrate syntax and usage of stored procedures, triggers, and UDFs.</span></span>   

## <a name="stored-procedures"></a><span data-ttu-id="f3d42-138">Хранимые процедуры</span><span class="sxs-lookup"><span data-stu-id="f3d42-138">Stored procedures</span></span>
### <a name="example-write-a-simple-stored-procedure"></a><span data-ttu-id="f3d42-139">Пример: написание простой хранимой процедуры</span><span class="sxs-lookup"><span data-stu-id="f3d42-139">Example: Write a simple stored procedure</span></span>
<span data-ttu-id="f3d42-140">Давайте начнем с простой хранимой процедуры, которая возвращает «Hello World» в ответ.</span><span class="sxs-lookup"><span data-stu-id="f3d42-140">Let’s start with a simple stored procedure that returns a “Hello World” response.</span></span>

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


<span data-ttu-id="f3d42-141">Хранимые процедуры регистрируются в коллекциях и могут работать с любым документом и вложением, существующим в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-141">Stored procedures are registered per collection, and can operate on any document and attachment present in that collection.</span></span> <span data-ttu-id="f3d42-142">Следующий фрагмент кода показывает, как зарегистрировать хранимую процедуру HelloWorld в коллекции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-142">The following snippet shows how to register the helloWorld stored procedure with a collection.</span></span> 

    // register the stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


<span data-ttu-id="f3d42-143">После того как хранимая процедура зарегистрирована, мы можем выполнить ее на коллекции и получить результаты обратно на клиенте.</span><span class="sxs-lookup"><span data-stu-id="f3d42-143">Once the stored procedure is registered, we can execute it against the collection, and read the results back at the client.</span></span> 

    // execute the stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


<span data-ttu-id="f3d42-144">Контекст объекта предоставляет доступ ко всем операциям, которые можно выполнить в хранилище Cosmos DB, а также доступ к объектам запросов и ответов.</span><span class="sxs-lookup"><span data-stu-id="f3d42-144">The context object provides access to all operations that can be performed on Cosmos DB storage, as well as access to the request and response objects.</span></span> <span data-ttu-id="f3d42-145">В этом случае мы использовали объект ответа, чтобы установить тело ответа, который был отправлен обратно клиенту.</span><span class="sxs-lookup"><span data-stu-id="f3d42-145">In this case, we used the response object to set the body of the response that was sent back to the client.</span></span> <span data-ttu-id="f3d42-146">Более подробные сведения можно найти в [документации к серверному пакету SDK JavaScript для Azure Cosmos DB](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="f3d42-146">For more details, refer to the [Azure Cosmos DB JavaScript server SDK documentation](http://azure.github.io/azure-documentdb-js-server/).</span></span>  

<span data-ttu-id="f3d42-147">Давайте подробнее остановимся на этом примере и добавим в хранимую процедуру дополнительную функциональность баз данных.</span><span class="sxs-lookup"><span data-stu-id="f3d42-147">Let us expand on this example and add more database related functionality to the stored procedure.</span></span> <span data-ttu-id="f3d42-148">Хранимые процедуры могут создавать, обновлять, читать, запрашивать и удалять документы и приложения внутри коллекции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-148">Stored procedures can create, update, read, query and delete documents and attachments inside the collection.</span></span>    

### <a name="example-write-a-stored-procedure-to-create-a-document"></a><span data-ttu-id="f3d42-149">Пример: написание хранимой процедуры для создания документа</span><span class="sxs-lookup"><span data-stu-id="f3d42-149">Example: Write a stored procedure to create a document</span></span>
<span data-ttu-id="f3d42-150">В следующем фрагменте показано, как использовать объект контекста для взаимодействия с ресурсами Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3d42-150">The next snippet shows how to use the context object to interact with Cosmos DB resources.</span></span>

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


<span data-ttu-id="f3d42-151">Эта хранимая процедура принимает в качестве входного параметра documentToCreate, тело документа, который будет создан в текущей коллекции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-151">This stored procedure takes as input documentToCreate, the body of a document to be created in the current collection.</span></span> <span data-ttu-id="f3d42-152">Все эти операции являются асинхронными и зависят от функций обратных вызовов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f3d42-152">All such operations are asynchronous and depend on JavaScript function callbacks.</span></span> <span data-ttu-id="f3d42-153">Функция обратного вызова имеет два параметра: один для объекта ошибки в случае, если операция не выполнится, и один для созданного объекта.</span><span class="sxs-lookup"><span data-stu-id="f3d42-153">The callback function has two parameters, one for the error object in case the operation fails, and one for the created object.</span></span> <span data-ttu-id="f3d42-154">Внутри функции обратного вызова пользователи могут либо обработать исключение, либо вызвать ошибку.</span><span class="sxs-lookup"><span data-stu-id="f3d42-154">Inside the callback, users can either handle the exception or throw an error.</span></span> <span data-ttu-id="f3d42-155">Если обратного вызова не предусмотрено и возникла ошибка, то среда выполнения Azure Cosmos DB выдаст ошибку.</span><span class="sxs-lookup"><span data-stu-id="f3d42-155">In case a callback is not provided and there is an error, the Azure Cosmos DB runtime throws an error.</span></span>   

<span data-ttu-id="f3d42-156">В приведенном выше примере обратный вызов возвращает ошибку, если операция не удалась.</span><span class="sxs-lookup"><span data-stu-id="f3d42-156">In the example above, the callback throws an error if the operation failed.</span></span> <span data-ttu-id="f3d42-157">В противном случае он устанавливает идентификатор созданного документа в качестве тела ответа клиенту.</span><span class="sxs-lookup"><span data-stu-id="f3d42-157">Otherwise, it sets the id of the created document as the body of the response to the client.</span></span> <span data-ttu-id="f3d42-158">Таким образом, данная хранимая процедура выполняется с входными параметрами.</span><span class="sxs-lookup"><span data-stu-id="f3d42-158">Here is how this stored procedure is executed with input parameters.</span></span>

    // register the stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure to create a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "The Hitchhiker’s Guide to the Galaxy",
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


<span data-ttu-id="f3d42-159">Обратите внимание, что эта хранимая процедура может быть изменена, чтобы принять массив тел документов в качестве входных данных и создания их все в том же исполнении хранимой процедуры вместо нескольких сетевых запросов для создания каждого из них в отдельности.</span><span class="sxs-lookup"><span data-stu-id="f3d42-159">Note that this stored procedure can be modified to take an array of document bodies as input and create them all in the same stored procedure execution instead of multiple network requests to create each of them individually.</span></span> <span data-ttu-id="f3d42-160">Это может быть использовано, чтобы внедрить эффективный импорт большого количества данных в Cosmos DB (обсуждается далее в этой статье).</span><span class="sxs-lookup"><span data-stu-id="f3d42-160">This can be used to implement an efficient bulk importer for Cosmos DB (discussed later in this tutorial).</span></span>   

<span data-ttu-id="f3d42-161">Описанный пример продемонстрировал, как использовать хранимые процедуры.</span><span class="sxs-lookup"><span data-stu-id="f3d42-161">The example described demonstrated how to use stored procedures.</span></span> <span data-ttu-id="f3d42-162">Мы рассмотрим триггеры и пользовательские функции (UDF) позже в этом уроке.</span><span class="sxs-lookup"><span data-stu-id="f3d42-162">We will cover triggers and user defined functions (UDFs) later in the tutorial.</span></span>

## <a name="database-program-transactions"></a><span data-ttu-id="f3d42-163">Транзакции программы базы данных</span><span class="sxs-lookup"><span data-stu-id="f3d42-163">Database program transactions</span></span>
<span data-ttu-id="f3d42-164">Транзакции в типичной базе данных могут быть определены как последовательность операций, выполняемых в одной логической единице работы.</span><span class="sxs-lookup"><span data-stu-id="f3d42-164">Transaction in a typical database can be defined as a sequence of operations performed as a single logical unit of work.</span></span> <span data-ttu-id="f3d42-165">Каждая транзакция предоставляет **гарантию выполнения принципа ACID**.</span><span class="sxs-lookup"><span data-stu-id="f3d42-165">Each transaction provides **ACID guarantees**.</span></span> <span data-ttu-id="f3d42-166">Широко известный акроним ACID обозначает четыре свойства: Atomicity (атомарность), Consistency (согласованность), Isolation (изолированность) и Durability (надежность).</span><span class="sxs-lookup"><span data-stu-id="f3d42-166">ACID is a well-known acronym that stands for four properties -  Atomicity, Consistency, Isolation and Durability.</span></span>  

<span data-ttu-id="f3d42-167">Вкратце, атомарность гарантирует, что все действия, проделанные в транзакции, рассматриваются как единое целое, они могут быть либо выполнены все, либо не выполнены вообще.</span><span class="sxs-lookup"><span data-stu-id="f3d42-167">Briefly, atomicity guarantees that all the work done inside a transaction is treated as a single unit where either all of it is committed or none.</span></span> <span data-ttu-id="f3d42-168">Согласованность гарантирует, что данные всегда находятся в правильном внутреннем состоянии между транзакциями.</span><span class="sxs-lookup"><span data-stu-id="f3d42-168">Consistency makes sure that the data is always in a good internal state across transactions.</span></span> <span data-ttu-id="f3d42-169">Изолированность гарантирует, что никакие две транзакции не будут мешать друг другу. Как правило, большинство коммерческих систем обеспечивают несколько уровней изолированности, которые могут быть использованы в зависимости от потребностей приложений.</span><span class="sxs-lookup"><span data-stu-id="f3d42-169">Isolation guarantees that no two transactions interfere with each other – generally, most commercial systems provide multiple isolation levels that can be used based on the application needs.</span></span> <span data-ttu-id="f3d42-170">Надежность гарантирует, что любое изменение, которое было совершено в базе данных, всегда будет присутствовать.</span><span class="sxs-lookup"><span data-stu-id="f3d42-170">Durability ensures that any change that’s committed in the database will always be present.</span></span>   

<span data-ttu-id="f3d42-171">В Cosmos DB JavaScript размещается в том же пространстве памяти, что и базы данных.</span><span class="sxs-lookup"><span data-stu-id="f3d42-171">In Cosmos DB, JavaScript is hosted in the same memory space as the database.</span></span> <span data-ttu-id="f3d42-172">Следовательно, запросы, хранимые процедуры и триггеры выполняются в том же пространстве базы данных.</span><span class="sxs-lookup"><span data-stu-id="f3d42-172">Hence, requests made within stored procedures and triggers execute in the same scope of a database session.</span></span> <span data-ttu-id="f3d42-173">Это позволяет Cosmos DB гарантировать принцип ACID для всех операций, которые являются частью одной хранимой процедуры/триггера.</span><span class="sxs-lookup"><span data-stu-id="f3d42-173">This enables Cosmos DB to guarantee ACID for all operations that are part of a single stored procedure/trigger.</span></span> <span data-ttu-id="f3d42-174">Рассмотрим следующее определение хранимой процедуры:</span><span class="sxs-lookup"><span data-stu-id="f3d42-174">Consider the following stored procedure definition:</span></span>

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

                    if (documents.length != 1) throw "Unable to find both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable to find both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable to read player details, abort ";
                });

            if (!accept) throw "Unable to read player details, abort ";

            // swap the two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable to update player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable to update player 2, abort"
                            });

                        if (!accept2) throw "Unable to update player 2, abort";
                    });

                if (!accept) throw "Unable to update player 1, abort";
            }
        }
    }

    // register the stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

<span data-ttu-id="f3d42-175">Эта хранимая процедура использует транзакции внутри игрового приложения, позволяющего торговать товарами между двумя игроками в одной операции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-175">This stored procedure uses transactions within a gaming app to trade items between two players in a single operation.</span></span> <span data-ttu-id="f3d42-176">Хранимая процедура пытается прочитать два документа, каждый из которых соответствует идентификаторам игроков, поступивших в качестве аргументов.</span><span class="sxs-lookup"><span data-stu-id="f3d42-176">The stored procedure attempts to read two documents each corresponding to the player IDs passed in as an argument.</span></span> <span data-ttu-id="f3d42-177">Если оба документа игрока будут найдены, то хранимая процедура обновляет документы, меняя их элементы.</span><span class="sxs-lookup"><span data-stu-id="f3d42-177">If both player documents are found, then the stored procedure updates the documents by swapping their items.</span></span> <span data-ttu-id="f3d42-178">При обнаружении ошибок вызывается исключение JavaScript, которое неявно отменяет транзакцию.</span><span class="sxs-lookup"><span data-stu-id="f3d42-178">If any errors are encountered along the way, it throws a JavaScript exception that implicitly aborts the transaction.</span></span>

<span data-ttu-id="f3d42-179">Если коллекция, в которой регистрируется хранимая процедура, является коллекцией с одной секцией, транзакция действует для всех документов в коллекции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-179">If the collection the stored procedure is registered against is a single-partition collection, then the transaction is scoped to all the documents within the collection.</span></span> <span data-ttu-id="f3d42-180">Если коллекция секционирована, то хранимые процедуры выполняются в области транзакции для ключа одной секции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-180">If the collection is partitioned, then stored procedures are executed in the transaction scope of a single partition key.</span></span> <span data-ttu-id="f3d42-181">Поэтому каждая хранимая процедура должна включать значение ключа секции, соответствующего области применения транзакции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-181">Each stored procedure execution must then include a partition key value corresponding to the scope the transaction must run under.</span></span> <span data-ttu-id="f3d42-182">Дополнительные сведения см. в статье [Секционирование, ключи секции и масштабирование в Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="f3d42-182">For more details, see [Azure Cosmos DB Partitioning](partition-data.md).</span></span>

### <a name="commit-and-rollback"></a><span data-ttu-id="f3d42-183">Фиксация и откат транзакций</span><span class="sxs-lookup"><span data-stu-id="f3d42-183">Commit and rollback</span></span>
<span data-ttu-id="f3d42-184">Транзакции глубоко и изначально интегрированы в модель программирования JavaScript в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3d42-184">Transactions are deeply and natively integrated into Cosmos DB’s JavaScript programming model.</span></span> <span data-ttu-id="f3d42-185">Внутри функции JavaScript все операции автоматически обернуты в одной транзакции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-185">Inside a JavaScript function, all operations are automatically wrapped under a single transaction.</span></span> <span data-ttu-id="f3d42-186">Если JavaScript завершает выполнение функции без исключения, операции в базе данных фиксируются.</span><span class="sxs-lookup"><span data-stu-id="f3d42-186">If the JavaScript completes without any exception, the operations to the database are committed.</span></span> <span data-ttu-id="f3d42-187">По сути, это аналог операторов BEGIN TRANSACTION и COMMIT TRANSACTION в реляционных базах данных, подразумевающихся в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3d42-187">In effect, the “BEGIN TRANSACTION” and “COMMIT TRANSACTION” statements in relational databases are implicit in Cosmos DB.</span></span>  

<span data-ttu-id="f3d42-188">Если есть исключения, которые возникли в сценарии, среда выполнения JavaScript в Cosmos DB откатит всю транзакцию.</span><span class="sxs-lookup"><span data-stu-id="f3d42-188">If there is any exception that’s propagated from the script, Cosmos DB’s JavaScript runtime will roll back the whole transaction.</span></span> <span data-ttu-id="f3d42-189">Как показано в предыдущем примере, выбрасывание исключения аналогично оператору ROLLBACK TRANSACTION в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3d42-189">As shown in the earlier example, throwing an exception is effectively equivalent to a “ROLLBACK TRANSACTION” in Cosmos DB.</span></span>

### <a name="data-consistency"></a><span data-ttu-id="f3d42-190">Согласованность данных</span><span class="sxs-lookup"><span data-stu-id="f3d42-190">Data consistency</span></span>
<span data-ttu-id="f3d42-191">Хранимые процедуры и триггеры всегда выполняются на основной реплике контейнера Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3d42-191">Stored procedures and triggers are always executed on the primary replica of the Azure Cosmos DB container.</span></span> <span data-ttu-id="f3d42-192">Гарантируется, что операции чтения в хранимых процедурах обеспечивают сильную согласованность.</span><span class="sxs-lookup"><span data-stu-id="f3d42-192">This ensures that reads from inside stored procedures offer strong consistency.</span></span> <span data-ttu-id="f3d42-193">Запросы, использующие пользовательские функции, могут быть выполнены на первичной или любой вторичной реплике, но чтобы обеспечить требуемый уровень согласованности, необходимо выбрать соответствующую реплику.</span><span class="sxs-lookup"><span data-stu-id="f3d42-193">Queries using user defined functions can be executed on the primary or any secondary replica, but we ensure to meet the requested consistency level by choosing the appropriate replica.</span></span>

## <a name="bounded-execution"></a><span data-ttu-id="f3d42-194">Ограниченное выполнение</span><span class="sxs-lookup"><span data-stu-id="f3d42-194">Bounded execution</span></span>
<span data-ttu-id="f3d42-195">Все операции Cosmos DB должны завершаться за определенный на уровне сервера период времени.</span><span class="sxs-lookup"><span data-stu-id="f3d42-195">All Cosmos DB operations must complete within the server specified request timeout duration.</span></span> <span data-ttu-id="f3d42-196">Это ограничение также относится к функциям JavaScript (хранимые процедуры, триггеры и определяемые пользователем функции).</span><span class="sxs-lookup"><span data-stu-id="f3d42-196">This constraint also applies to JavaScript functions (stored procedures, triggers and user-defined functions).</span></span> <span data-ttu-id="f3d42-197">Если операция не завершается в этот период времени, транзакция откатывается.</span><span class="sxs-lookup"><span data-stu-id="f3d42-197">If an operation does not complete with that time limit, the transaction is rolled back.</span></span> <span data-ttu-id="f3d42-198">Функции JavaScript должны завершаться в период времени или реализовывать модель продолжения работы для пакета/возобновления выполнения.</span><span class="sxs-lookup"><span data-stu-id="f3d42-198">JavaScript functions must finish within the time limit or implement a continuation based model to batch/resume execution.</span></span>  

<span data-ttu-id="f3d42-199">Для упрощения разработки хранимых процедур и триггеров и ограничения времени их выполнения все функции в соответствии с объектом коллекции (для создания, чтения, замены и удаления документов и вложений) возвращают логическое значение, которое представляет, будет ли эта операция завершена.</span><span class="sxs-lookup"><span data-stu-id="f3d42-199">In order to simplify development of stored procedures and triggers to handle time limits, all functions under the collection object (for create, read, replace, and delete of documents and attachments) return a Boolean value that represents whether that operation will complete.</span></span> <span data-ttu-id="f3d42-200">Если это значение является ложным, то это означает, что срок выполнения истекает в ближайшее время и что процедура должна завершить выполнение.</span><span class="sxs-lookup"><span data-stu-id="f3d42-200">If this value is false, it is an indication that the time limit is about to expire and that the procedure must wrap up execution.</span></span>  <span data-ttu-id="f3d42-201">Операции, предшествующие первой неакцептованной операции сохранения данных, помещаются в очередь и гарантированно будут завершены, если хранимая процедура завершается в срок и очередь пуста.</span><span class="sxs-lookup"><span data-stu-id="f3d42-201">Operations queued prior to the first unaccepted store operation are guaranteed to complete if the stored procedure completes in time and does not queue any more requests.</span></span>  

<span data-ttu-id="f3d42-202">Функции JavaScript также ограничены в потреблении ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f3d42-202">JavaScript functions are also bounded on resource consumption.</span></span> <span data-ttu-id="f3d42-203">Cosmos DB резервирует пропускную способность для коллекции, основанной на подготовленном размере учетной записи базы данных.</span><span class="sxs-lookup"><span data-stu-id="f3d42-203">Cosmos DB reserves throughput per collection based on the provisioned size of a database account.</span></span> <span data-ttu-id="f3d42-204">Пропускная способность выражается в форме нормализованных единиц потребления ресурсов процессора, памяти и ввода-вывода, именуемых «единица запроса» или RU.</span><span class="sxs-lookup"><span data-stu-id="f3d42-204">Throughput is expressed in terms of a normalized unit of CPU, memory and IO consumption called request units or RUs.</span></span> <span data-ttu-id="f3d42-205">Функции JavaScript могут потенциально использовать большое количество RU в течение короткого времени и, возможно, получить ограничение скорости выполнения при достижении предела, выделенного для коллекции.</span><span class="sxs-lookup"><span data-stu-id="f3d42-205">JavaScript functions can potentially use up a large number of RUs within a short time, and might get rate-limited if the collection’s limit is reached.</span></span> <span data-ttu-id="f3d42-206">Ресурсоемкие хранимые процедуры также могут быть помещены в режим ожидания, чтобы обеспечить доступность примитивных операций с базами данных.</span><span class="sxs-lookup"><span data-stu-id="f3d42-206">Resource intensive stored procedures might also be quarantined to ensure availability of primitive database operations.</span></span>  

### <a name="example-bulk-importing-data-into-a-database-program"></a><span data-ttu-id="f3d42-207">Пример. Массовый импорт данных в программу базы данных</span><span class="sxs-lookup"><span data-stu-id="f3d42-207">Example: Bulk importing data into a database program</span></span>
<span data-ttu-id="f3d42-208">Ниже приведен пример хранимой процедуры, реализующей массовый импорт документов в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="f3d42-208">Below is an example of a stored procedure that is written to bulk-import documents into a collection.</span></span> <span data-ttu-id="f3d42-209">Обратите внимание, как хранимая процедура обрабатывает ограниченное выполнение, проверяя логическое значение, возвращаемое из createDocument, а затем использует подсчет документов, помещенных в каждом вызове хранимой процедуры, чтобы отслеживать и возобновить пакетное задание.</span><span class="sxs-lookup"><span data-stu-id="f3d42-209">Note how the stored procedure handles bounded execution by checking the Boolean return value from createDocument, and then uses the count of documents inserted in each invocation of the stored procedure to track and resume progress across batches.</span></span>

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // The count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("The array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call the create API to create a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) The createDocument request was not accepted. 
        //    In this case the callback will not be called, we just call setBody and we are done.
        // 2) The callback was called docs.length times.
        //    In this case all documents were created and we don’t need to call tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If the request was accepted, callback will be called.
            // Otherwise report current count back to the client, 
            // which will call the script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order to process the result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment the count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set the response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <span data-ttu-id="f3d42-210"><a id="trigger"></a> Триггеры базы данных</span><span class="sxs-lookup"><span data-stu-id="f3d42-210"><a id="trigger"></a> Database triggers</span></span>
### <a name="database-pre-triggers"></a><span data-ttu-id="f3d42-211">Триггеры базы данных со срабатыванием до наступления события</span><span class="sxs-lookup"><span data-stu-id="f3d42-211">Database pre-triggers</span></span>
<span data-ttu-id="f3d42-212">Cosmos DB предоставляет триггеры, которые выполняются или запускаются при выполнении операций над документом.</span><span class="sxs-lookup"><span data-stu-id="f3d42-212">Cosmos DB provides triggers that are executed or triggered by an operation on a document.</span></span> <span data-ttu-id="f3d42-213">Например, можно задать предварительный триггер, когда вы создаете документ, и он будет запускаться перед созданием документа.</span><span class="sxs-lookup"><span data-stu-id="f3d42-213">For example, you can specify a pre-trigger when you are creating a document – this pre-trigger will run before the document is created.</span></span> <span data-ttu-id="f3d42-214">Ниже приведен пример того, как предварительные триггеры можно использовать для проверки свойств документа, который создается:</span><span class="sxs-lookup"><span data-stu-id="f3d42-214">The following is an example of how pre-triggers can be used to validate the properties of a document that is being created:</span></span>

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document to be created in the current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update the document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


<span data-ttu-id="f3d42-215">И соответствующий клиентский код Node.js для регистрации триггера:</span><span class="sxs-lookup"><span data-stu-id="f3d42-215">And the corresponding Node.js client-side registration code for the trigger:</span></span>

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


<span data-ttu-id="f3d42-216">Триггеры со срабатыванием до наступления события не могут иметь никаких входных параметров.</span><span class="sxs-lookup"><span data-stu-id="f3d42-216">Pre-triggers cannot have any input parameters.</span></span> <span data-ttu-id="f3d42-217">Объект запроса может быть использован для манипулирования сообщением запроса, связанного с операцией.</span><span class="sxs-lookup"><span data-stu-id="f3d42-217">The request object can be used to manipulate the request message associated with the operation.</span></span> <span data-ttu-id="f3d42-218">Здесь триггеры со срабатыванием до наступления события запускаются до создания документа, и сообщение тела запроса содержит документ, который будет создан в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="f3d42-218">Here, the pre-trigger is being run with the creation of a document, and the request message body contains the document to be created in JSON format.</span></span>   

<span data-ttu-id="f3d42-219">При регистрации триггеров пользователи могут указать операции, с которыми они запускаются.</span><span class="sxs-lookup"><span data-stu-id="f3d42-219">When triggers are registered, users can specify the operations that it can run with.</span></span> <span data-ttu-id="f3d42-220">Этот триггер был создан с TriggerOperation.Create, это означает, что последующее не допускается.</span><span class="sxs-lookup"><span data-stu-id="f3d42-220">This trigger was created with TriggerOperation.Create, which means the following is not permitted.</span></span>

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a><span data-ttu-id="f3d42-221">Пост-триггеры базы данных</span><span class="sxs-lookup"><span data-stu-id="f3d42-221">Database post-triggers</span></span>
<span data-ttu-id="f3d42-222">Пост-триггеры, как и пред-триггеры, связаны с операцией на документе и не принимают никаких входных параметров.</span><span class="sxs-lookup"><span data-stu-id="f3d42-222">Post-triggers, like pre-triggers, are associated with an operation on a document and don’t take any input parameters.</span></span> <span data-ttu-id="f3d42-223">Они запускаются **после** завершения операции и получают доступ к ответному сообщению, которое отправляется клиенту.</span><span class="sxs-lookup"><span data-stu-id="f3d42-223">They run **after** the operation has completed, and have access to the response message that is sent to the client.</span></span>   

<span data-ttu-id="f3d42-224">В следующем примере используются триггеры со срабатыванием после наступления события:</span><span class="sxs-lookup"><span data-stu-id="f3d42-224">The following example shows post-triggers in action:</span></span>

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
            if(!accept) throw "Unable to update metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable to find metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable to update metadata, abort";
                               });
                         if(!accept) throw "Unable to update metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


<span data-ttu-id="f3d42-225">Триггер можно зарегистрировать, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="f3d42-225">The trigger can be registered as shown in the following sample.</span></span>

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "The Band",
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


<span data-ttu-id="f3d42-226">Этот триггер запрашивает метаданные документа и обновляет их дополнительными сведениями о вновь созданных документах.</span><span class="sxs-lookup"><span data-stu-id="f3d42-226">This trigger queries for the metadata document and updates it with details about the newly created document.</span></span>  

<span data-ttu-id="f3d42-227">Важно отметить одну вещь, а именно — **транзакционное** выполнение триггеров в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3d42-227">One thing that is important to note is the **transactional** execution of triggers in Cosmos DB.</span></span> <span data-ttu-id="f3d42-228">Этот триггер со срабатыванием после наступления события работает как часть той же самой транзакции при создании оригинального документа.</span><span class="sxs-lookup"><span data-stu-id="f3d42-228">This post-trigger runs as part of the same transaction as the creation of the original document.</span></span> <span data-ttu-id="f3d42-229">Поэтому, если мы формируем исключение из триггера (скажем, если мы не в состоянии обновить метаданные документа), вся транзакция будет прервана и произойдет ее откат.</span><span class="sxs-lookup"><span data-stu-id="f3d42-229">Therefore, if we throw an exception from the post-trigger (say if we are unable to update the metadata document), the whole transaction will fail and be rolled back.</span></span> <span data-ttu-id="f3d42-230">Ни один документ не будет создан, будет возвращено исключение.</span><span class="sxs-lookup"><span data-stu-id="f3d42-230">No document will be created, and an exception will be returned.</span></span>  

## <span data-ttu-id="f3d42-231"><a id="udf"></a>Функции, определяемые пользователем</span><span class="sxs-lookup"><span data-stu-id="f3d42-231"><a id="udf"></a>User-defined functions</span></span>
<span data-ttu-id="f3d42-232">Функции, определяемые пользователем (UDF), используются для расширения грамматики языка запросов SQL для API Cosmos DB и реализации пользовательской бизнес-логики.</span><span class="sxs-lookup"><span data-stu-id="f3d42-232">User-defined functions (UDFs) are used to extend the DocumentDB API SQL query language grammar and implement custom business logic.</span></span> <span data-ttu-id="f3d42-233">Функции можно вызывать только из запросов.</span><span class="sxs-lookup"><span data-stu-id="f3d42-233">They can only be called from inside queries.</span></span> <span data-ttu-id="f3d42-234">Они не имеют доступа к объектам контекста и предназначены для использования только в качестве вычислимых JavaScript-сценариев.</span><span class="sxs-lookup"><span data-stu-id="f3d42-234">They do not have access to the context object and are meant to be used as compute-only JavaScript.</span></span> <span data-ttu-id="f3d42-235">Таким образом, UDF могут запускаться только на дополнительных репликах службы Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f3d42-235">Therefore, UDFs can be run on secondary replicas of the Cosmos DB service.</span></span>  

<span data-ttu-id="f3d42-236">Следующий пример создает UDF для расчета налога на прибыль на основе ставок для различных доходов, а затем использует его в запросе, чтобы найти всех людей, которые заплатили более 20 000 долларов США в виде налогов.</span><span class="sxs-lookup"><span data-stu-id="f3d42-236">The following sample creates a UDF to calculate income tax based on rates for various income brackets, and then uses it inside a query to find all people who paid more than $20,000 in taxes.</span></span>

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


<span data-ttu-id="f3d42-237">UDF впоследствии могут быть использованы в запросах как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="f3d42-237">The UDF can subsequently be used in queries like in the following sample:</span></span>

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

## <a name="javascript-language-integrated-query-api"></a><span data-ttu-id="f3d42-238">API запросов, интегрированный в язык JavaScript</span><span class="sxs-lookup"><span data-stu-id="f3d42-238">JavaScript language-integrated query API</span></span>
<span data-ttu-id="f3d42-239">Кроме выдачи запросов с использованием грамматики SQL DocumentDB, серверный пакет SDK позволяет создавать оптимизированные запросы с помощью гибкого интерфейса JavaScript без знания SQL.</span><span class="sxs-lookup"><span data-stu-id="f3d42-239">In addition to issuing queries using DocumentDB’s SQL grammar, the server-side SDK allows you to perform optimized queries using a fluent JavaScript interface without any knowledge of SQL.</span></span> <span data-ttu-id="f3d42-240">API запросов в JavaScript позволяет программно создавать запросы, передавая предикатные функции в образующие цепочку вызовы функций. Для этого используется синтаксис, который понимают встроенные элементы массива ECMAScript5 и популярные библиотеки JavaScript, например lodash.</span><span class="sxs-lookup"><span data-stu-id="f3d42-240">The JavaScript query API allows you to programmatically build queries by passing predicate functions into chainable function calls, with a syntax familiar to ECMAScript5's Array built-ins and popular JavaScript libraries like lodash.</span></span> <span data-ttu-id="f3d42-241">Чтобы запросы были эффективно выполнены с помощью индексов Azure Cosmos DB, их анализирует среда выполнения JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f3d42-241">Queries are parsed by the JavaScript runtime to be executed efficiently using Azure Cosmos DB’s indices.</span></span>

> [!NOTE]
> <span data-ttu-id="f3d42-242">`__` (двойное подчеркивание) является псевдонимом для `getContext().getCollection()`.</span><span class="sxs-lookup"><span data-stu-id="f3d42-242">`__` (double-underscore) is an alias to `getContext().getCollection()`.</span></span>
> <br/>
> <span data-ttu-id="f3d42-243">Другими словами, вы можете использовать `__` или `getContext().getCollection()`, чтобы получить доступ к API запросов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f3d42-243">In other words, you can use `__` or `getContext().getCollection()` to access the JavaScript query API.</span></span>
> 
> 

<span data-ttu-id="f3d42-244">Поддерживаемые функции включают:</span><span class="sxs-lookup"><span data-stu-id="f3d42-244">Supported functions include:</span></span>

<ul>
<li><span data-ttu-id="f3d42-245">
<b>chain() ... .value([обратный вызов] [, параметры])</b>
</span><span class="sxs-lookup"><span data-stu-id="f3d42-245">
<b>chain() ... .value([callback] [, options])</b>
</span></span><ul>
<li>
<span data-ttu-id="f3d42-246">Запускается вызов по цепочке, который должен завершаться value().</span><span class="sxs-lookup"><span data-stu-id="f3d42-246">Starts a chained call which must be terminated with value().</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f3d42-247">
<b>filter(predicateFunction [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="f3d42-247">
<b>filter(predicateFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f3d42-248">Фильтрует входные данные с помощью функции предиката, которая возвращает значение true или false для фильтрации входных документов в набор результатов.</span><span class="sxs-lookup"><span data-stu-id="f3d42-248">Filters the input using a predicate function which returns true/false in order to filter in/out input documents into the resulting set.</span></span> <span data-ttu-id="f3d42-249">Эта функция похожа на предложение WHERE в SQL.</span><span class="sxs-lookup"><span data-stu-id="f3d42-249">This behaves similar to a WHERE clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f3d42-250">
<b>map(transformationFunction [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="f3d42-250">
<b>map(transformationFunction [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f3d42-251">Применяет проекцию, заданную функцией преобразования, которая сопоставляет каждый входной элемент объекту или значению JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f3d42-251">Applies a projection given a transformation function which maps each input item to a JavaScript object or value.</span></span> <span data-ttu-id="f3d42-252">Эта функция похожа на предложение SELECT в SQL.</span><span class="sxs-lookup"><span data-stu-id="f3d42-252">This behaves similar to a SELECT clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f3d42-253">
<b>pluck([propertyName] [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="f3d42-253">
<b>pluck([propertyName] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f3d42-254">Это ярлык для сопоставления, которое извлекает из каждого входного элемента значение одного свойства.</span><span class="sxs-lookup"><span data-stu-id="f3d42-254">This is a shortcut for a map which extracts the value of a single property from each input item.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f3d42-255">
<b>flatten([isShallow] [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="f3d42-255">
<b>flatten([isShallow] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f3d42-256">Собирает и объединяет массивы для каждого входного элемента в один массив.</span><span class="sxs-lookup"><span data-stu-id="f3d42-256">Combines and flattens arrays from each input item in to a single array.</span></span> <span data-ttu-id="f3d42-257">Эта функция похожа на предложение SelectMany в LINQ.</span><span class="sxs-lookup"><span data-stu-id="f3d42-257">This behaves similar to SelectMany in LINQ.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f3d42-258">
<b>sortBy([предикат] [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="f3d42-258">
<b>sortBy([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f3d42-259">Используя заданный предикат, создает новый набор документов путем сортировки документов во входном потоке документов по возрастанию.</span><span class="sxs-lookup"><span data-stu-id="f3d42-259">Produce a new set of documents by sorting the documents in the input document stream in ascending order using the given predicate.</span></span> <span data-ttu-id="f3d42-260">Эта функция похожа на предложение ORDER BY в SQL.</span><span class="sxs-lookup"><span data-stu-id="f3d42-260">This behaves similar to a ORDER BY clause in SQL.</span></span>
</li>
</ul>
</li>
<li><span data-ttu-id="f3d42-261">
<b>sortByDescending([предикат] [, параметры] [, обратный вызов])</b>
</span><span class="sxs-lookup"><span data-stu-id="f3d42-261">
<b>sortByDescending([predicate] [, options] [, callback])</b>
</span></span><ul>
<li>
<span data-ttu-id="f3d42-262">Используя заданный предикат, создает новый набор документов путем сортировки документов во входном потоке документов по убыванию.</span><span class="sxs-lookup"><span data-stu-id="f3d42-262">Produce a new set of documents by sorting the documents in the input document stream in descending order using the given predicate.</span></span> <span data-ttu-id="f3d42-263">Эта функция похожа на предложение ORDER BY x DESC в SQL.</span><span class="sxs-lookup"><span data-stu-id="f3d42-263">This behaves similar to a ORDER BY x DESC clause in SQL.</span></span>
</li>
</ul>
</li>
</ul>


<span data-ttu-id="f3d42-264">Если конструкции JavaScript включены в предикатную функцию и/или селектор, они автоматически оптимизированы для непосредственного выполнения в индексах Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="f3d42-264">When included inside predicate and/or selector functions, the following JavaScript constructs get automatically optimized to run directly on Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="f3d42-265">Простые операторы: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span><span class="sxs-lookup"><span data-stu-id="f3d42-265">Simple operators: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;!</span></span> ~
* <span data-ttu-id="f3d42-266">литералы, включая литерал объекта: {}</span><span class="sxs-lookup"><span data-stu-id="f3d42-266">Literals, including the object literal: {}</span></span>
* <span data-ttu-id="f3d42-267">var, return.</span><span class="sxs-lookup"><span data-stu-id="f3d42-267">var, return</span></span>

<span data-ttu-id="f3d42-268">Следующие конструкции JavaScript не оптимизированы для использования в индексах Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="f3d42-268">The following JavaScript constructs do not get optimized for Azure Cosmos DB indices:</span></span>

* <span data-ttu-id="f3d42-269">поток управления (например, if, for, while);</span><span class="sxs-lookup"><span data-stu-id="f3d42-269">Control flow (e.g. if, for, while)</span></span>
* <span data-ttu-id="f3d42-270">вызовы функций.</span><span class="sxs-lookup"><span data-stu-id="f3d42-270">Function calls</span></span>

<span data-ttu-id="f3d42-271">Чтобы узнать больше, ознакомьтесь с [документацией JavaScript по серверам](http://azure.github.io/azure-documentdb-js-server/).</span><span class="sxs-lookup"><span data-stu-id="f3d42-271">For more information, please see our [Server-Side JSDocs](http://azure.github.io/azure-documentdb-js-server/).</span></span>

### <a name="example-write-a-stored-procedure-using-the-javascript-query-api"></a><span data-ttu-id="f3d42-272">Пример создания хранимой процедуры с помощью API запросов в JavaScript</span><span class="sxs-lookup"><span data-stu-id="f3d42-272">Example: Write a stored procedure using the JavaScript query API</span></span>
<span data-ttu-id="f3d42-273">В следующем образце кода приведен пример использования API запросов в JavaScript для создания хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="f3d42-273">The following code sample is an example of how the JavaScript Query API can be used in the context of a stored procedure.</span></span> <span data-ttu-id="f3d42-274">Хранимая процедура вставляет заданный входным параметром документ, после чего обновляет метаданные документа с помощью метода `__.filter()` , а также на основе свойств размера входного документа minSize, maxSize и totalSize.</span><span class="sxs-lookup"><span data-stu-id="f3d42-274">The stored procedure inserts a document, given by an input parameter, and updates a metadata document, using the `__.filter()` method, with minSize, maxSize, and totalSize based upon the input document's size property.</span></span>

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent to our callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check the doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get the meta document. We keep it in the same collection. it's the only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed to find the metadata document.");

            // The metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all the rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace the metadata document in the store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read the meta again 
              //       and update again because due to Snapshot isolation we will read same exact version (we are in same transaction).
              //       We have to take care of that on the client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-to-javascript-cheat-sheet"></a><span data-ttu-id="f3d42-275">Таблица соответствия запросов SQL и Javascript</span><span class="sxs-lookup"><span data-stu-id="f3d42-275">SQL to Javascript cheat sheet</span></span>
<span data-ttu-id="f3d42-276">В следующей таблице представлены разные запросы SQL и соответствующие им запросы JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f3d42-276">The following table presents various SQL queries and the corresponding JavaScript queries.</span></span>

<span data-ttu-id="f3d42-277">Как и запросы SQL, ключи свойств документов (например, `doc.id`) чувствительны к регистру.</span><span class="sxs-lookup"><span data-stu-id="f3d42-277">As with SQL queries, document property keys (e.g. `doc.id`) are case-sensitive.</span></span>

|<span data-ttu-id="f3d42-278">SQL</span><span class="sxs-lookup"><span data-stu-id="f3d42-278">SQL</span></span>| <span data-ttu-id="f3d42-279">API запроса JavaScript</span><span class="sxs-lookup"><span data-stu-id="f3d42-279">JavaScript Query API</span></span>|<span data-ttu-id="f3d42-280">Описание приведено ниже</span><span class="sxs-lookup"><span data-stu-id="f3d42-280">Description below</span></span>|
|---|---|---|
|<span data-ttu-id="f3d42-281">SELECT *</span><span class="sxs-lookup"><span data-stu-id="f3d42-281">SELECT *</span></span><br><span data-ttu-id="f3d42-282">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f3d42-282">FROM docs</span></span>| <span data-ttu-id="f3d42-283">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f3d42-283">__.map(function(doc) {</span></span> <br><span data-ttu-id="f3d42-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span><span class="sxs-lookup"><span data-stu-id="f3d42-284">&nbsp;&nbsp;&nbsp;&nbsp;return doc;</span></span><br><span data-ttu-id="f3d42-285">});</span><span class="sxs-lookup"><span data-stu-id="f3d42-285">});</span></span>|<span data-ttu-id="f3d42-286">1</span><span class="sxs-lookup"><span data-stu-id="f3d42-286">1</span></span>|
|<span data-ttu-id="f3d42-287">SELECT docs.id, docs.message AS msg, docs.actions</span><span class="sxs-lookup"><span data-stu-id="f3d42-287">SELECT docs.id, docs.message AS msg, docs.actions</span></span> <br><span data-ttu-id="f3d42-288">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f3d42-288">FROM docs</span></span>|<span data-ttu-id="f3d42-289">__.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f3d42-289">__.map(function(doc) {</span></span><br><span data-ttu-id="f3d42-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="f3d42-290">&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="f3d42-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="f3d42-291">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="f3d42-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span><span class="sxs-lookup"><span data-stu-id="f3d42-292">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,</span></span><br><span data-ttu-id="f3d42-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span><span class="sxs-lookup"><span data-stu-id="f3d42-293">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions</span></span><br><span data-ttu-id="f3d42-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="f3d42-294">&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="f3d42-295">});</span><span class="sxs-lookup"><span data-stu-id="f3d42-295">});</span></span>|<span data-ttu-id="f3d42-296">2</span><span class="sxs-lookup"><span data-stu-id="f3d42-296">2</span></span>|
|<span data-ttu-id="f3d42-297">SELECT *</span><span class="sxs-lookup"><span data-stu-id="f3d42-297">SELECT *</span></span><br><span data-ttu-id="f3d42-298">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f3d42-298">FROM docs</span></span><br><span data-ttu-id="f3d42-299">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="f3d42-299">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="f3d42-300">__.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f3d42-300">__.filter(function(doc) {</span></span><br><span data-ttu-id="f3d42-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="f3d42-301">&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="f3d42-302">});</span><span class="sxs-lookup"><span data-stu-id="f3d42-302">});</span></span>|<span data-ttu-id="f3d42-303">3</span><span class="sxs-lookup"><span data-stu-id="f3d42-303">3</span></span>|
|<span data-ttu-id="f3d42-304">SELECT *</span><span class="sxs-lookup"><span data-stu-id="f3d42-304">SELECT *</span></span><br><span data-ttu-id="f3d42-305">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f3d42-305">FROM docs</span></span><br><span data-ttu-id="f3d42-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span><span class="sxs-lookup"><span data-stu-id="f3d42-306">WHERE ARRAY_CONTAINS(docs.Tags, 123)</span></span>|<span data-ttu-id="f3d42-307">__.filter(function(x) {</span><span class="sxs-lookup"><span data-stu-id="f3d42-307">__.filter(function(x) {</span></span><br><span data-ttu-id="f3d42-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span><span class="sxs-lookup"><span data-stu-id="f3d42-308">&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;</span></span><br><span data-ttu-id="f3d42-309">});</span><span class="sxs-lookup"><span data-stu-id="f3d42-309">});</span></span>|<span data-ttu-id="f3d42-310">4.</span><span class="sxs-lookup"><span data-stu-id="f3d42-310">4</span></span>|
|<span data-ttu-id="f3d42-311">SELECT docs.id, docs.message AS msg</span><span class="sxs-lookup"><span data-stu-id="f3d42-311">SELECT docs.id, docs.message AS msg</span></span><br><span data-ttu-id="f3d42-312">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f3d42-312">FROM docs</span></span><br><span data-ttu-id="f3d42-313">WHERE docs.id="X998_Y998"</span><span class="sxs-lookup"><span data-stu-id="f3d42-313">WHERE docs.id="X998_Y998"</span></span>|<span data-ttu-id="f3d42-314">__.chain()</span><span class="sxs-lookup"><span data-stu-id="f3d42-314">__.chain()</span></span><br><span data-ttu-id="f3d42-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f3d42-315">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="f3d42-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span><span class="sxs-lookup"><span data-stu-id="f3d42-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";</span></span><br><span data-ttu-id="f3d42-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="f3d42-317">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="f3d42-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f3d42-318">&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {</span></span><br><span data-ttu-id="f3d42-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span><span class="sxs-lookup"><span data-stu-id="f3d42-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {</span></span><br><span data-ttu-id="f3d42-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span><span class="sxs-lookup"><span data-stu-id="f3d42-320">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,</span></span><br><span data-ttu-id="f3d42-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span><span class="sxs-lookup"><span data-stu-id="f3d42-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message</span></span><br><span data-ttu-id="f3d42-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span><span class="sxs-lookup"><span data-stu-id="f3d42-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};</span></span><br><span data-ttu-id="f3d42-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="f3d42-323">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="f3d42-324">.value();</span><span class="sxs-lookup"><span data-stu-id="f3d42-324">.value();</span></span>|<span data-ttu-id="f3d42-325">5</span><span class="sxs-lookup"><span data-stu-id="f3d42-325">5</span></span>|
|<span data-ttu-id="f3d42-326">SELECT VALUE tag</span><span class="sxs-lookup"><span data-stu-id="f3d42-326">SELECT VALUE tag</span></span><br><span data-ttu-id="f3d42-327">FROM docs</span><span class="sxs-lookup"><span data-stu-id="f3d42-327">FROM docs</span></span><br><span data-ttu-id="f3d42-328">JOIN tag IN docs.Tags</span><span class="sxs-lookup"><span data-stu-id="f3d42-328">JOIN tag IN docs.Tags</span></span><br><span data-ttu-id="f3d42-329">ORDER BY docs._ts</span><span class="sxs-lookup"><span data-stu-id="f3d42-329">ORDER BY docs._ts</span></span>|<span data-ttu-id="f3d42-330">__.chain()</span><span class="sxs-lookup"><span data-stu-id="f3d42-330">__.chain()</span></span><br><span data-ttu-id="f3d42-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f3d42-331">&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {</span></span><br><span data-ttu-id="f3d42-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span><span class="sxs-lookup"><span data-stu-id="f3d42-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);</span></span><br><span data-ttu-id="f3d42-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="f3d42-333">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="f3d42-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span><span class="sxs-lookup"><span data-stu-id="f3d42-334">&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {</span></span><br><span data-ttu-id="f3d42-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span><span class="sxs-lookup"><span data-stu-id="f3d42-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;</span></span><br><span data-ttu-id="f3d42-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span><span class="sxs-lookup"><span data-stu-id="f3d42-336">&nbsp;&nbsp;&nbsp;&nbsp;})</span></span><br><span data-ttu-id="f3d42-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span><span class="sxs-lookup"><span data-stu-id="f3d42-337">&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")</span></span><br><span data-ttu-id="f3d42-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span><span class="sxs-lookup"><span data-stu-id="f3d42-338">&nbsp;&nbsp;&nbsp;&nbsp;.flatten()</span></span><br><span data-ttu-id="f3d42-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span><span class="sxs-lookup"><span data-stu-id="f3d42-339">&nbsp;&nbsp;&nbsp;&nbsp;.value()</span></span>|<span data-ttu-id="f3d42-340">6</span><span class="sxs-lookup"><span data-stu-id="f3d42-340">6</span></span>|

<span data-ttu-id="f3d42-341">Далее следуют описания, которые объясняют каждый запрос из приведенной выше таблицы.</span><span class="sxs-lookup"><span data-stu-id="f3d42-341">The following descriptions explain each query in the table above.</span></span>
1. <span data-ttu-id="f3d42-342">Возвращает все документы (с разбивкой на страницы с отметками "продолжить").</span><span class="sxs-lookup"><span data-stu-id="f3d42-342">Results in all documents (paginated with continuation token) as is.</span></span>
2. <span data-ttu-id="f3d42-343">Создает проекцию идентификатора, сообщения (msg) и действия для всех документов.</span><span class="sxs-lookup"><span data-stu-id="f3d42-343">Projects the id, message (aliased to msg), and action from all documents.</span></span>
3. <span data-ttu-id="f3d42-344">Запрашивает документы с предикатом: id = "X998_Y998".</span><span class="sxs-lookup"><span data-stu-id="f3d42-344">Queries for documents with the predicate: id = "X998_Y998".</span></span>
4. <span data-ttu-id="f3d42-345">Запрашивает все документы, имеющие свойство Tags. Tags является массивом, содержащим значение 123.</span><span class="sxs-lookup"><span data-stu-id="f3d42-345">Queries for documents that have a Tags property and Tags is an array containing the value 123.</span></span>
5. <span data-ttu-id="f3d42-346">Запрашивает документы с предикатом id = "X998_Y998" и затем выполняет проекцию идентификатора и сообщения (msg).</span><span class="sxs-lookup"><span data-stu-id="f3d42-346">Queries for documents with a predicate, id = "X998_Y998", and then projects the id and message (aliased to msg).</span></span>
6. <span data-ttu-id="f3d42-347">Выполняет фильтрацию для получения документов, у которых есть свойство Tags, и сортирует результирующие документы по системному свойству временной отметки _ts, после чего выполняет проекцию и объединение массива Tags.</span><span class="sxs-lookup"><span data-stu-id="f3d42-347">Filters for documents which have an array property, Tags, and sorts the resulting documents by the _ts timestamp system property, and then projects + flattens the Tags array.</span></span>


## <a name="runtime-support"></a><span data-ttu-id="f3d42-348">Поддержка времени выполнения</span><span class="sxs-lookup"><span data-stu-id="f3d42-348">Runtime support</span></span>
<span data-ttu-id="f3d42-349">[Серверный API JavaScript для DocumentDB](http://azure.github.io/azure-documentdb-js-server/) поддерживает большинство возможностей языка JavaScript в соответствии со стандартами [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span><span class="sxs-lookup"><span data-stu-id="f3d42-349">[DocumentDB JavaScript server side API](http://azure.github.io/azure-documentdb-js-server/) provides support for the most of the mainstream JavaScript language features as standardized by [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).</span></span>

### <a name="security"></a><span data-ttu-id="f3d42-350">Безопасность</span><span class="sxs-lookup"><span data-stu-id="f3d42-350">Security</span></span>
<span data-ttu-id="f3d42-351">Хранимые процедуры и триггеры JavaScript выполняются в изолированной среде, поэтому действия одного сценария не оказывают какого-либо воздействия на другие сценарии, за счет изоляции снимков транзакций на уровне базы данных.</span><span class="sxs-lookup"><span data-stu-id="f3d42-351">JavaScript stored procedures and triggers are sandboxed so that the effects of one script do not leak to the other without going through the snapshot transaction isolation at the database level.</span></span> <span data-ttu-id="f3d42-352">Среды выполнения объединяются в пул, но удаляются из контекста после каждого запуска.</span><span class="sxs-lookup"><span data-stu-id="f3d42-352">The runtime environments are pooled but cleaned of the context after each run.</span></span> <span data-ttu-id="f3d42-353">Следовательно, они гарантированно безопасны от появления непреднамеренных побочных эффектов друг для друга.</span><span class="sxs-lookup"><span data-stu-id="f3d42-353">Hence they are guaranteed to be safe of any unintended side effects from each other.</span></span>

### <a name="pre-compilation"></a><span data-ttu-id="f3d42-354">Предварительная компиляция</span><span class="sxs-lookup"><span data-stu-id="f3d42-354">Pre-compilation</span></span>
<span data-ttu-id="f3d42-355">Хранимые процедуры, триггеры и пользовательские функции неявно прекомпилированы в формате байт-кода, чтобы избежать затрат на компиляцию во время каждого вызова сценария.</span><span class="sxs-lookup"><span data-stu-id="f3d42-355">Stored procedures, triggers and UDFs are implicitly precompiled to the byte code format in order to avoid compilation cost at the time of each script invocation.</span></span> <span data-ttu-id="f3d42-356">Это гарантирует высокую скорость и низкие затраты на вызовы хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="f3d42-356">This ensures invocations of stored procedures are fast and have a low footprint.</span></span>

## <a name="client-sdk-support"></a><span data-ttu-id="f3d42-357">Поддержка клиентских пакетов SDK</span><span class="sxs-lookup"><span data-stu-id="f3d42-357">Client SDK support</span></span>
<span data-ttu-id="f3d42-358">В дополнение к API DocumentDB для клиента [Node.js](documentdb-sdk-node.md) Azure Cosmos DB поддерживает [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/) и [пакеты SDK для Python](documentdb-sdk-python.md) для API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="f3d42-358">In addition to the DocumentDB API for [Node.js](documentdb-sdk-node.md) client, Azure Cosmos DB has [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [JavaScript](http://azure.github.io/azure-documentdb-js/), and [Python SDKs](documentdb-sdk-python.md) for the DocumentDB API.</span></span> <span data-ttu-id="f3d42-359">Хранимые процедуры, триггеры и пользовательские функции могут быть созданы и выполнены с использованием любого из этих пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="f3d42-359">Stored procedures, triggers and UDFs can be created and executed using any of these SDKs as well.</span></span> <span data-ttu-id="f3d42-360">В следующем примере показано, как создать и выполнить хранимую процедуру с помощью клиента .NET.</span><span class="sxs-lookup"><span data-stu-id="f3d42-360">The following example shows how to create and execute a stored procedure using the .NET client.</span></span> <span data-ttu-id="f3d42-361">Обратите внимание, что типы .NET передаются в хранимую процедуру и возвращаются в виде объектов JSON.</span><span class="sxs-lookup"><span data-stu-id="f3d42-361">Note how the .NET types are passed into the stored procedure as JSON and read back.</span></span>

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


<span data-ttu-id="f3d42-362">В этом примере показано, как использовать [API DocumentDB для .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet), чтобы создать триггер со срабатыванием до наступления события, а также документ со включенным триггером.</span><span class="sxs-lookup"><span data-stu-id="f3d42-362">This sample shows how to use the [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) to create a pre-trigger and create a document with the trigger enabled.</span></span> 

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


<span data-ttu-id="f3d42-363">А в следующем примере показано, как создать определенную пользователем функцию для последующего использования в [запросе SQL API Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="f3d42-363">And the following example shows how to create a user defined function (UDF) and use it in a [DocumentDB API SQL query](documentdb-sql-query.md).</span></span>

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

## <a name="rest-api"></a><span data-ttu-id="f3d42-364">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="f3d42-364">REST API</span></span>
<span data-ttu-id="f3d42-365">Все операции Azure Cosmos DB могут быть выполнены в RESTful-образе.</span><span class="sxs-lookup"><span data-stu-id="f3d42-365">All Azure Cosmos DB operations can be performed in a RESTful manner.</span></span> <span data-ttu-id="f3d42-366">Хранимые процедуры, триггеры и пользовательские функции могут быть зарегистрированы в соответствии с коллекцией с помощью команды POST HTTP.</span><span class="sxs-lookup"><span data-stu-id="f3d42-366">Stored procedures, triggers and user-defined functions can be registered under a collection by using HTTP POST.</span></span> <span data-ttu-id="f3d42-367">Ниже приведен пример, как зарегистрировать хранимую процедуру:</span><span class="sxs-lookup"><span data-stu-id="f3d42-367">The following is an example of how to register a stored procedure:</span></span>

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


<span data-ttu-id="f3d42-368">Хранимая процедура регистрируется путем выполнения запроса POST с URI "dbs/testdb/colls/testColl/sprocs" с телом, содержащим создаваемую хранимую процедуру.</span><span class="sxs-lookup"><span data-stu-id="f3d42-368">The stored procedure is registered by executing a POST request against the URI dbs/testdb/colls/testColl/sprocs with the body containing the stored procedure to create.</span></span> <span data-ttu-id="f3d42-369">Триггеры и функции UDF могут быть зарегистрированы аналогичным образом путем выполнения команды POST с идентификаторами /triggers и /udfs соответственно.</span><span class="sxs-lookup"><span data-stu-id="f3d42-369">Triggers and UDFs can be registered similarly by issuing a POST against /triggers and /udfs respectively.</span></span>
<span data-ttu-id="f3d42-370">Эту хранимую процедуру затем можно выполнить, отправив запрос POST со ссылкой на ее ресурс.</span><span class="sxs-lookup"><span data-stu-id="f3d42-370">This stored procedure can then be executed by issuing a POST request against its resource link:</span></span>

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of the Patriarch"}, "Price", 200 ]


<span data-ttu-id="f3d42-371">Здесь входные параметры в хранимую процедуру передаются в теле запроса.</span><span class="sxs-lookup"><span data-stu-id="f3d42-371">Here, the input to the stored procedure is passed in the request body.</span></span> <span data-ttu-id="f3d42-372">Обратите внимание, что входные параметры передаются в виде массива JSON входных параметров.</span><span class="sxs-lookup"><span data-stu-id="f3d42-372">Note that the input is passed as a JSON array of input parameters.</span></span> <span data-ttu-id="f3d42-373">Хранимая процедура принимает первый параметр как документ, который является телом ответа.</span><span class="sxs-lookup"><span data-stu-id="f3d42-373">The stored procedure takes the first input as a document that is a response body.</span></span> <span data-ttu-id="f3d42-374">В ответ мы получаем следующее:</span><span class="sxs-lookup"><span data-stu-id="f3d42-374">The response we receive is as follows:</span></span>

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of the Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


<span data-ttu-id="f3d42-375">Триггеры, в отличие от хранимых процедур, не могут быть выполнены непосредственно.</span><span class="sxs-lookup"><span data-stu-id="f3d42-375">Triggers, unlike stored procedures, cannot be executed directly.</span></span> <span data-ttu-id="f3d42-376">Вместо этого они выполняются как часть операции над документом.</span><span class="sxs-lookup"><span data-stu-id="f3d42-376">Instead they are executed as part of an operation on a document.</span></span> <span data-ttu-id="f3d42-377">Мы можем указать триггеры для запуска, отправив запрос с заголовками HTTP.</span><span class="sxs-lookup"><span data-stu-id="f3d42-377">We can specify the triggers to run with a request using HTTP headers.</span></span> <span data-ttu-id="f3d42-378">Ниже приведен запрос для создания документа.</span><span class="sxs-lookup"><span data-stu-id="f3d42-378">The following is request to create a document.</span></span>

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “The Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


<span data-ttu-id="f3d42-379">Здесь в заголовке x-ms-documentdb-pre-trigger-include указан триггер со срабатыванием до наступления события, который будет запущен при запросе.</span><span class="sxs-lookup"><span data-stu-id="f3d42-379">Here the pre-trigger to be run with the request is specified in the x-ms-documentdb-pre-trigger-include header.</span></span> <span data-ttu-id="f3d42-380">Соответственно, любые триггер со срабатыванием после наступления события могут быть приведены заголовке x-ms-documentdb-post-trigger-include.</span><span class="sxs-lookup"><span data-stu-id="f3d42-380">Correspondingly, any post-triggers are given in the x-ms-documentdb-post-trigger-include header.</span></span> <span data-ttu-id="f3d42-381">Обратите внимание, что для данного запроса могут быть определены оба вида триггеров.</span><span class="sxs-lookup"><span data-stu-id="f3d42-381">Note that both pre- and post-triggers can be specified for a given request.</span></span>

## <a name="sample-code"></a><span data-ttu-id="f3d42-382">Пример кода</span><span class="sxs-lookup"><span data-stu-id="f3d42-382">Sample code</span></span>
<span data-ttu-id="f3d42-383">Дополнительные примеры кода, используемого на сервере (включая операции [массового удаления](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) и [обновления](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)), представлены в нашем [репозитории GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="f3d42-383">You can find more server-side code examples (including [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js), and [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) on our [GitHub repository](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).</span></span>

<span data-ttu-id="f3d42-384">Хотите поделиться своей потрясающей хранимой процедурой?</span><span class="sxs-lookup"><span data-stu-id="f3d42-384">Want to share your awesome stored procedure?</span></span> <span data-ttu-id="f3d42-385">Отправьте нам запрос на получение.</span><span class="sxs-lookup"><span data-stu-id="f3d42-385">Please, send us a pull-request!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f3d42-386">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f3d42-386">Next steps</span></span>
<span data-ttu-id="f3d42-387">После создания хранимых процедур, триггеров и определяемых пользователем функций вы сможете загружать их на портале Azure и просматривать их с помощью обозревателя данных.</span><span class="sxs-lookup"><span data-stu-id="f3d42-387">Once you have one or more stored procedures, triggers, and user-defined functions created, you can load them and view them in the Azure portal using Data Explorer.</span></span>

<span data-ttu-id="f3d42-388">Кроме того, при изучении программирования Azure Cosmos DB на стороне сервера могут оказаться полезными следующие ссылки и ресурсы:</span><span class="sxs-lookup"><span data-stu-id="f3d42-388">You may also find the following references and resources useful in your path to learn more about Azure Cosmos dB server-side programming:</span></span>

* <span data-ttu-id="f3d42-389">[Пакет SDK для DocumentDB .NET: скачивание и заметки о выпуске](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f3d42-389">[Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md)</span></span>
* [<span data-ttu-id="f3d42-390">DocumentDB Studio</span><span class="sxs-lookup"><span data-stu-id="f3d42-390">DocumentDB Studio</span></span>](https://github.com/mingaliu/DocumentDBStudio/releases)
* [<span data-ttu-id="f3d42-391">JSON</span><span class="sxs-lookup"><span data-stu-id="f3d42-391">JSON</span></span>](http://www.json.org/) 
* [<span data-ttu-id="f3d42-392">JavaScript ECMA-262</span><span class="sxs-lookup"><span data-stu-id="f3d42-392">JavaScript ECMA-262</span></span>](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [<span data-ttu-id="f3d42-393">Безопасность и расширяемость переносной базы данных</span><span class="sxs-lookup"><span data-stu-id="f3d42-393">Secure and Portable Database Extensibility</span></span>](http://dl.acm.org/citation.cfm?id=276339) 
* [<span data-ttu-id="f3d42-394">Сервис-ориентированная архитектура баз данных</span><span class="sxs-lookup"><span data-stu-id="f3d42-394">Service Oriented Database Architecture</span></span>](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [<span data-ttu-id="f3d42-395">Размещение среды выполнения .NET на Microsoft SQL server</span><span class="sxs-lookup"><span data-stu-id="f3d42-395">Hosting the .NET Runtime in Microsoft SQL server</span></span>](http://dl.acm.org/citation.cfm?id=1007669)

