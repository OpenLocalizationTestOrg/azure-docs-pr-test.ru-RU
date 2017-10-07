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
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a>Программирование Azure Cosmos DB на стороне сервера: хранимые процедуры, триггеры баз данных и определяемые пользователем функции
Узнайте, каким образом интегрированное транзакционное выполнение JavaScript в Azure Cosmos DB позволяет разработчикам создавать **хранимые процедуры**, **триггеры** и **определяемые пользователем функции (UDF)** непосредственно на платформе JavaScript [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/). Это позволяет toowrite базы данных программы логики приложения, которая может поставляться и выполнена непосредственно в хранилище секций hello базы данных. 

Мы рекомендуем, запущенную за просмотром hello следующие видео, где лю Эндрю предоставляет модель программирования tooCosmos Краткое введение DB серверной базы данных. 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

После этого вернитесь toothis статьи, где вы узнаете о toohello ответы hello следующие вопросы:  

* Как написать хранимую процедуру, триггер или определяемую пользователем Функцию на JavaScript?
* Каким образом Cosmos DB предоставляет гарантию выполнения принципа ACID?
* Каков принцип работы транзакций в Cosmos DB?
* Что такое пред- и пост-триггеры, и как их написать?
* Как зарегистрировать и выполнить хранимую процедуру, триггер или определяемую пользователем функции RESTful-образом по протоколу HTTP?
* Какие пакеты SDK DB Cosmos доступных toocreate, а выполнение хранимых процедур, триггеров и определяемых пользователем функций?

## <a name="introduction-toostored-procedure-and-udf-programming"></a>Введение tooStored процедуре и определяемой пользователем функции программирования
В этом подходе *«JavaScript как современного T-SQL»* освобождает разработчиков приложения от сложности hello несоответствий системы типа и технологий объектно реляционного сопоставления. Он также имеет ряд преимуществ встроенная функция, которые могут быть загруженные toobuild многофункциональных приложений:  

* **Процедурная логика:** JavaScript в качестве верхнего уровня языка программирования, предоставляет tooexpress привычного полнофункционального интерфейса бизнес-логики. Можно выполнять сложные последовательности операций ближе toohello данных.
* **Атомарные транзакции.** Cosmos DB гарантирует атомарность операций с базой данных, выполняемых внутри одной хранимой процедуры или триггера. Это позволяет приложению объединить соответствующие операции в пакетном режиме; таким образом, успешно будут выполнены либо все из них, либо ни одна. 
* **Производительность:** hello факт, что JSON — система типов языка Javascript по своей природе сопоставленных toohello также является основной единицей хранилища в базу данных, Cosmos hello означает количество оптимизаций как отложенный материализации JSON документов в буфер hello пул и сделать их доступными по требованию toohello, выполнение кода. Существуют дополнительные преимущества производительности, связанные с базой данных toohello для доставки бизнес логики:
  
  * Пакеты — разработчики могут группировать операции, такие как вставка, и запускать их в пакетном режиме. Задержка трафика сети Hello затрат и значительно уменьшить hello хранилища toocreate издержек на отдельные транзакции. 
  * Предварительная компиляция — Cosmos DB выполняет компиляцию хранимые процедуры, триггеры и определяемые пользователем функции (UDF) tooavoid стоимости компиляции JavaScript для каждого вызова. Hello издержки построения hello байтовый код для hello процедурной логики занимающие tooa минимальное значение.
  * Секвенcирование — многим операции нужен побочный эффект («триггер»), что потенциально задействует выполнение одной или множества вторичных операций хранения. Помимо атомарности, это обеспечивает более высокую производительность при перемещении сервера toohello. 
* **Инкапсуляция:** хранимые процедуры можно использовать toogroup бизнес-логики в одном месте. Это принесет два преимущества:
  * Он добавляет дополнительный уровень абстракции относительно hello необработанные данные, что позволит tooevolve архитекторы данных свои приложения, независимо от данных hello. Это особенно удобно, когда данные hello без схемы, из-за toohello негибкие предположения, которые требуют toobe, помещенного в приложения hello, если они имеют toodeal с данными непосредственно.  
  * Эта абстракция позволяет защитить свои данные за счет оптимизации доступа hello из сценариев hello предприятий.  

Hello создания и выполнения триггеры базы данных, хранимые процедуры и пользовательские операторы поддерживаются через hello [API-интерфейса REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), и [клиентских SDK](documentdb-sdk-dotnet.md) на многих платформах, включая .NET, Node.js и JavaScript.

В этом учебнике используется hello [пакет SDK для Node.js с Q обещания](http://azure.github.io/azure-documentdb-node-q/) tooillustrate синтаксисе и использовании хранимых процедур, триггеров и определяемых пользователем функций.   

## <a name="stored-procedures"></a>Хранимые процедуры
### <a name="example-write-a-simple-stored-procedure"></a>Пример: написание простой хранимой процедуры
Давайте начнем с простой хранимой процедуры, которая возвращает «Hello World» в ответ.

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


Хранимые процедуры регистрируются в коллекциях и могут работать с любым документом и вложением, существующим в этой коллекции. Hello следующий фрагмент кода показывает, как tooregister hello helloWorld хранимой процедуры с коллекцией. 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


После регистрации hello хранимые процедуры, мы применяемыми коллекции hello и чтение результатов hello обратно на приветствия клиента. 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


объект контекста Hello доступ tooall операций, которые могут выполняться над хранилища Cosmos базы данных, а также для доступа к объектам toohello запроса и ответа. В этом случае мы использовали hello объекта tooset hello в тексте ответа hello ответ, который был отправлен назад toohello клиента. Дополнительные сведения см. в разделе toohello [сервера Azure Cosmos DB JavaScript документации по пакету SDK](http://azure.github.io/azure-documentdb-js-server/).  

Сообщите нам расширить этот пример и добавить дополнительные базы данных связанные функциональные возможности toohello хранимой процедуры. Хранимые процедуры можно создавать, обновлять, чтение, запросов и удалять документы и вложения внутри коллекции hello.    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a>Пример: Записи toocreate хранимой процедуры документа
Следующий фрагмент кода Hello показано, как toouse hello toointeract объект контекста с ресурсами Cosmos DB.

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


Эта хранимая процедура принимает в качестве входного documentToCreate, текст hello toobe документов, созданных в текущей коллекции hello. Все эти операции являются асинхронными и зависят от функций обратных вызовов JavaScript. функция обратного вызова Hello имеет два параметра: hello объекта ошибки в случае сбоя операции hello и один для hello создан объект. Внутри обратного вызова hello пользователи могут обрабатывать исключение hello или вызывают ошибку. Если обратный вызов не предоставлен, а ошибка, среда выполнения Azure Cosmos DB hello вызывает ошибку.   

В приведенном выше примере hello hello обратного вызова вызывает ошибку, если не удалось выполнить операцию hello. В противном случае он задает идентификатор hello hello создан документ как текст hello hello ответа toohello клиента. Таким образом, данная хранимая процедура выполняется с входными параметрами.

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


Обратите внимание, что эта хранимая процедура могут измененный tootake массив тела документа в качестве входных данных и создавать их все в hello же хранимой процедуры выполнения вместо несколько сетевых запросов toocreate каждого из них по отдельности. Это может быть используется tooimplement компонента эффективного массового импорта для Cosmos DB (см. Далее в этом учебнике).   

описанном примере Hello показано, как toouse хранимых процедур. Триггеры и определяемые пользователем функции (UDF) будут рассмотрены далее в учебнике hello.

## <a name="database-program-transactions"></a>Транзакции программы базы данных
Транзакции в типичной базе данных могут быть определены как последовательность операций, выполняемых в одной логической единице работы. Каждая транзакция предоставляет **гарантию выполнения принципа ACID**. Широко известный акроним ACID обозначает четыре свойства: Atomicity (атомарность), Consistency (согласованность), Isolation (изолированность) и Durability (надежность).  

Коротко говоря, Атомарность гарантирует, все операции hello, выполняемые внутри транзакции обрабатываются как единое целое где либо все его фиксируется или none. Согласованность гарантирует hello данных всегда в рабочее состояние внутреннего по всем транзакциям. Изоляция гарантирует, что никакие две транзакции взаимодействуют между собой — как правило, большинство коммерческих системы обеспечивают несколько уровней изоляции, которые могут использоваться с учетом потребностей приложения hello. Устойчивость гарантирует, что любые изменения, зафиксированные в базе данных hello всегда будут представлены.   

В Cosmos DB JavaScript размещается в hello же области памяти, что hello базы данных. Таким образом, запросы, входящие в хранимые процедуры и триггеры выполняются в hello же области сеанса базы данных. Это позволяет tooguarantee Cosmos DB ACID для всех операций, которые являются частью одной хранимой процедуры или триггера. Рассмотрим следующие hello хранимой процедуры определение:

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

Эта хранимая процедура использует транзакции внутри элементов игры приложения tootrade между двумя участниками в одной операции. Hello хранимой процедуры попыток tooread двух документов, над которыми игроки toohello соответствующие идентификаторы переданному в качестве аргумента. При обнаружении оба проигрывателя документов, hello хранимой процедуры обновляет hello документов путем переключения их элементов. Все ошибки, возникающие в процессе страницы приветствия, выдает исключение JavaScript, который неявно прерывает транзакцию hello.

Если hello коллекции hello хранимой процедуры регистрации для коллекции одной секции, то hello транзакция с областью tooall hello документы в коллекции hello. Если коллекция hello секционирована, хранимые процедуры выполняются в области транзакции hello ключа одной секции. Каждый хранимой процедуры выполнения затем должен включать значение ключа секции соответствующей транзакции hello области toohello должны запускаться от имени. Дополнительные сведения см. в статье [Секционирование, ключи секции и масштабирование в Cosmos DB](partition-data.md).

### <a name="commit-and-rollback"></a>Фиксация и откат транзакций
Транзакции глубоко и изначально интегрированы в модель программирования JavaScript в Cosmos DB. Внутри функции JavaScript все операции автоматически обернуты в одной транзакции. Если hello JavaScript завершается без любое исключение, фиксируются hello toohello рабочей базы данных. В результате hello «BEGIN TRANSACTION» и «ЗАФИКСИРОВАТЬ ТРАНЗАКЦИИ» инструкции в реляционных базах данных являются неявно в Cosmos DB.  

Если любое исключение, которое распространяется от сценария hello, Cosmos DB среды выполнения JavaScript будет откат всей транзакции hello. Как показано выше в hello пример, исключение является эффективно эквивалентные tooa «ОТКАТ ТРАНЗАКЦИИ» в Cosmos DB.

### <a name="data-consistency"></a>Согласованность данных
Хранимые процедуры и триггеры, всегда выполняются в первичной реплике hello hello Azure Cosmos DB контейнера. Гарантируется, что операции чтения в хранимых процедурах обеспечивают сильную согласованность. Запросы, использующие определяемые пользователем функции могут быть выполнены для hello первичного или любой из вторичных реплик, но мы обеспечиваем toomeet hello запрошенный уровень согласованности, выбрав соответствующую реплику hello.

## <a name="bounded-execution"></a>Ограниченное выполнение
Все операции Cosmos DB должен быть выполнен в указанный сервер hello длительность времени ожидания запроса. Это ограничение также применяется tooJavaScript функции (хранимые процедуры, триггеры и определяемые пользователем функции). Если операция не выполнена с указанного времени, hello транзакция откатывается. Функции JavaScript необходимо завершить в течение ограниченного времени hello или реализовать продолжение на основе модели toobatch или возобновления выполнения.  

Порядок разработки toosimplify хранимых процедур и триггеров toohandle ограничений по времени, все функции hello объекта коллекции (для создание, чтение, замена и удаление документов и вложения) возвращают логическое значение, представляющее ли, Операция будет завершена. Если это значение равно false, это означает, что лимит времени hello о tooexpire и заключать скорость выполнения этой процедуры hello.  Первая операция неподдерживаемого хранилища операций в очереди предыдущих toohello гарантируется toocomplete, если hello хранимой процедуры завершается за время, а не помещает в очередь запросы.  

Функции JavaScript также ограничены в потреблении ресурсов. Cosmos DB резервирование пропускной способности для коллекции, в зависимости от размера hello подготовить учетную запись базы данных. Пропускная способность выражается в форме нормализованных единиц потребления ресурсов процессора, памяти и ввода-вывода, именуемых «единица запроса» или RU. Функции JavaScript потенциально можно использовать большое количество RUs через короткое время и может получить ограниченной по скорости при достижении ограничения объема hello коллекции. Хранимые процедуры с большим объемом ресурсов также может доступности помещенные в карантин tooensure операций примитивов базы данных.  

### <a name="example-bulk-importing-data-into-a-database-program"></a>Пример. Массовый импорт данных в программу базы данных
Ниже приведен пример хранимой процедуры, которая записывается в коллекцию toobulk импорта документов. Примечание о том, как hello выполнения хранимой процедуры ограниченных дескрипторов, проверьте hello логическое значение возвращаемое значение из createDocument и затем использует hello число документов, которые вставлены при каждом вызове hello хранимой процедуры tootrack и resume ход выполнения для пакетов.

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

## <a id="trigger"></a> Триггеры базы данных
### <a name="database-pre-triggers"></a>Триггеры базы данных со срабатыванием до наступления события
Cosmos DB предоставляет триггеры, которые выполняются или запускаются при выполнении операций над документом. Например можно указать до триггер при создании документа — это предварительная триггер будет запущен до создания документа hello. Hello ниже приведен пример как Pre-триггеры могут быть используется toovalidate hello свойства документа, который находится в процессе создания:

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


И соответствующее Node.js регистрации клиентского кода для триггера hello hello:

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


Триггеры со срабатыванием до наступления события не могут иметь никаких входных параметров. Hello объекта запроса может быть запроса используется toomanipulate приветственное сообщение, связанное с операцией hello. Здесь hello предварительной триггер запускается с hello Создание документа, а тело сообщения hello запроса содержит toobe hello документа, созданные в формате JSON.   

Когда зарегистрировать триггеры, пользователи могут указать hello операций, которые она может использовать. Этот триггер был создан с TriggerOperation.Create, это означает, что следующие hello не допускается.

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a>Пост-триггеры базы данных
Пост-триггеры, как и пред-триггеры, связаны с операцией на документе и не принимают никаких входных параметров. Они выполняются **после** hello операции завершения, а также иметь доступ toohello ответное сообщение, отправляемое toohello клиента.   

Следующий пример Hello показывает POST-триггеры в действии:

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


Hello триггера может быть зарегистрирован как показано в следующих образец hello.

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


Этот триггер запрашивает документ метаданных hello и обновляет его с подробными сведениями о только что созданный hello документа.  

Одно из важных toonote — hello **транзакций** выполнения триггеров в Cosmos DB. После триггера запускается как часть hello же транзакции, что создание hello hello исходного документа. Таким образом Если мы создаем исключение из триггера после hello (скажем, если настоящий документ метаданных не удается tooupdate hello), hello вся транзакция завершится ошибкой и будет выполнен откат. Ни один документ не будет создан, будет возвращено исключение.  

## <a id="udf"></a>Функции, определяемые пользователем
Определяемые пользователем функции (UDF), грамматики языка запросов DocumentDB API SQL hello используется tooextend и реализации пользовательской бизнес-логики. Функции можно вызывать только из запросов. Они не имеют доступа к toohello контекста объекта и предназначены toobe служит только для вычислительных JavaScript. Таким образом определяемые пользователем функции выполняются во вторичных репликах hello Cosmos DB службы.  

Hello следующий пример создает подоходного налога toocalculate определяемой пользователем функции, в зависимости от скорости для различных скобки доход и использует его внутри toofind запрос всех лиц, которые оплачено налогов более 20 000 долларов США.

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


Hello определяемой пользователем функции могут использоваться в дальнейшем в запросах, как и в следующий образец hello:

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

## <a name="javascript-language-integrated-query-api"></a>API запросов, интегрированный в язык JavaScript
Кроме tooissuing запросов с помощью элемента DocumentDB грамматику SQL, hello SDK на стороне сервера можно tooperform оптимизированных запросов, с помощью интерфейса Fluent на основе JavaScript, без знания SQL. вызывает запрос Hello JavaScript, который прикладной программный Интерфейс позволяет tooprogrammatically построения запросов путем передачи в функцию цепочкам функции предикатов с встроенных элементов массива и популярные библиотек JavaScript, таких как lodash синтаксис знакомый tooECMAScript5 элемента. Запросы, обрабатываются с toobe среды выполнения JavaScript hello, выполнен эффективно с использованием Azure Cosmos DB индексов.

> [!NOTE]
> `__`(двойным подчеркиванием) — это псевдоним слишком`getContext().getCollection()`.
> <br/>
> Другими словами, можно использовать `__` или `getContext().getCollection()` tooaccess hello запроса API JavaScript.
> 
> 

Поддерживаемые функции включают:

<ul>
<li>
<b>chain() ... .value([обратный вызов] [, параметры])</b>
<ul>
<li>
Запускается вызов по цепочке, который должен завершаться value().
</li>
</ul>
</li>
<li>
<b>filter(predicateFunction [, параметры] [, обратный вызов])</b>
<ul>
<li>
Фильтрация ввода с помощью функции предиката, которая возвращает true или false, в порядке toofilter ожидания входных документов в результирующем наборе hello hello. Это поведение аналогично tooa предложения WHERE в SQL.
</li>
</ul>
</li>
<li>
<b>map(transformationFunction [, параметры] [, обратный вызов])</b>
<ul>
<li>
Применяет проекции, функции преобразования, используемый для сопоставления каждого входного элемента tooa JavaScript объект или значение. Это ведет себя аналогично tooa предложении SELECT SQL.
</li>
</ul>
</li>
<li>
<b>pluck([propertyName] [, параметры] [, обратный вызов])</b>
<ul>
<li>
Это ярлык для карты, которая извлекает значение hello одно свойство из каждого входного элемента.
</li>
</ul>
</li>
<li>
<b>flatten([isShallow] [, параметры] [, обратный вызов])</b>
<ul>
<li>
Объединяет и выполняет сведение массивов из каждого входного элемента в один массив tooa. Это ведет себя аналогично tooSelectMany в LINQ.
</li>
</ul>
</li>
<li>
<b>sortBy([предикат] [, параметры] [, обратный вызов])</b>
<ul>
<li>
Создает новый набор документов, сортируя документов hello в потоке входной документ hello в возрастающем порядке, с помощью hello заданному предикату. Это ведет себя аналогично tooa предложение ORDER BY в SQL.
</li>
</ul>
</li>
<li>
<b>sortByDescending([предикат] [, параметры] [, обратный вызов])</b>
<ul>
<li>
Создает новый набор документов, сортируя документов hello в потоке входной документ hello в порядке убывания с использованием hello заданному предикату. Это ведет себя аналогично предложения ORDER BY x DESC tooa в SQL.
</li>
</ul>
</li>
</ul>


При включении в функции предиката или селектор hello следующие конструкции JavaScript получить автоматически оптимизированного toorun непосредственно на Azure Cosmos DB индексов:

* Простые операторы: = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;! ~
* Литералы, включая литерал hello объекта: {}
* var, return.

создает следующие JavaScript приветствия получить не оптимизирован для индексов Azure Cosmos DB:

* поток управления (например, if, for, while);
* вызовы функций.

Чтобы узнать больше, ознакомьтесь с [документацией JavaScript по серверам](http://azure.github.io/azure-documentdb-js-server/).

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a>Пример: Написать хранимую процедуру с помощью API-Интерфейс запросов JavaScript hello
Привет, следующий образец кода приведен пример использования hello запроса API JavaScript в контексте hello хранимой процедуры. Hello хранимая процедура вставляет документ, выданный входного параметра и обновляет документ метаданных с помощью hello `__.filter()` метод minSize, maxSize и totalSize на основе свойства size hello входной документ.

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

## <a name="sql-toojavascript-cheat-sheet"></a>SQL tooJavascript памятку.
Hello следующей таблице представлены различные запросы SQL и соответствующих запросах JavaScript hello.

Как и запросы SQL, ключи свойств документов (например, `doc.id`) чувствительны к регистру.

|SQL| API запроса JavaScript|Описание приведено ниже|
|---|---|---|
|SELECT *<br>FROM docs| __.map(function(doc) { <br>&nbsp;&nbsp;&nbsp;&nbsp;return doc;<br>});|1|
|SELECT docs.id, docs.message AS msg, docs.actions <br>FROM docs|__.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;actions:doc.actions<br>&nbsp;&nbsp;&nbsp;&nbsp;};<br>});|2|
|SELECT *<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>});|3|
|SELECT *<br>FROM docs<br>WHERE ARRAY_CONTAINS(docs.Tags, 123)|__.filter(function(x) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags && x.Tags.indexOf(123) > -1;<br>});|4.|
|SELECT docs.id, docs.message AS msg<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;msg: doc.message<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>.value();|5|
|SELECT VALUE tag<br>FROM docs<br>JOIN tag IN docs.Tags<br>ORDER BY docs._ts|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc.Tags && Array.isArray(doc.Tags);<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return doc._ts;<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")<br>&nbsp;&nbsp;&nbsp;&nbsp;.flatten()<br>&nbsp;&nbsp;&nbsp;&nbsp;.value()|6|

Hello следующие описания объясняется каждый запрос в приведенной выше таблице hello.
1. Возвращает все документы (с разбивкой на страницы с отметками "продолжить").
2. Идентификатор hello проекты, сообщение (псевдоним toomsg) и действия из всех документов.
3. Запросы для документов с предикатом hello: идентификатор = «X998_Y998».
4. Количество запросов для документов, имеющих свойство метки и тегов — массив, содержащий значение hello 123.
5. Запросы для документов с предикатом, id = «X998_Y998», а затем id hello проекты и сообщений (псевдоним toomsg).
6. Фильтры для документов, которые имеют свойства массива, теги, и сортирует полученный документы hello свойством hello _ts отметка времени системы и затем + выполняет сведение массив тегов hello.


## <a name="runtime-support"></a>Поддержка времени выполнения
[API стороны сервера DocumentDB JavaScript](http://azure.github.io/azure-documentdb-js-server/) обеспечивает поддержку hello большинство hello массовых функции языка JavaScript по мере стандартизированные по [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).

### <a name="security"></a>Безопасность
JavaScript хранимых процедур и триггеров в виде изолированного, эффекты hello один скрипт не приводят к утечке toohello других минуя hello изоляцию транзакций моментальных снимков на уровне базы данных hello. среды выполнения Hello в пул, но удаляются контекста hello после каждого запуска. Поэтому они гарантированно toobe безопасный из любой непредвиденные побочные эффекты друг от друга.

### <a name="pre-compilation"></a>Предварительная компиляция
Хранимые процедуры, триггеры и определяемые пользователем функции являются неявно предкомпилированного toohello формат кода байтов в стоимости компиляции tooavoid порядок во время каждого вызова скрипта hello. Это гарантирует высокую скорость и низкие затраты на вызовы хранимых процедур.

## <a name="client-sdk-support"></a>Поддержка клиентских пакетов SDK
В дополнение toohello DocumentDB API для [Node.js](documentdb-sdk-node.md) клиента Azure Cosmos DB [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), и [Python SDK](documentdb-sdk-python.md) для hello DocumentDB API. Хранимые процедуры, триггеры и пользовательские функции могут быть созданы и выполнены с использованием любого из этих пакетов SDK. Следующий пример показывает как Hello toocreate и выполнение хранимой процедуры с помощью клиента .NET hello. Обратите внимание, как типы .NET hello передаются в hello хранимую процедуру как JSON и повторного считывания.

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


В этом примере показано, как toouse hello [API .NET для DocumentDB](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate предварительной триггера и Создание документа с включен триггер hello. 

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


И hello в следующем примере показано, как toocreate пользователь определяемой функции (UDF) и использовать его в [запроса DocumentDB API SQL](documentdb-sql-query.md).

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

## <a name="rest-api"></a>Интерфейс REST API
Все операции Azure Cosmos DB могут быть выполнены в RESTful-образе. Хранимые процедуры, триггеры и пользовательские функции могут быть зарегистрированы в соответствии с коллекцией с помощью команды POST HTTP. Hello ниже приведен пример того, как tooregister хранимой процедуры:

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


Hello хранимую процедуру регистрации, выполнив запрос методом POST для hello URI баз данных SQL Server/testdb/colls/testColl/sprocs содержит текст hello hello toocreate хранимой процедуры. Триггеры и функции UDF могут быть зарегистрированы аналогичным образом путем выполнения команды POST с идентификаторами /triggers и /udfs соответственно.
Эту хранимую процедуру затем можно выполнить, отправив запрос POST со ссылкой на ее ресурс.

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


Здесь hello ввода toohello хранимой процедуры передается в тексте запроса hello. Обратите внимание, что hello входные данные передаются как массив JSON входных параметров. Hello хранимые процедуры принимает hello первого входа как документ, текст ответа. Hello ответа, которые мы получили выглядит следующим образом:

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


Триггеры, в отличие от хранимых процедур, не могут быть выполнены непосредственно. Вместо этого они выполняются как часть операции над документом. Можно указать триггеры toorun hello вместе с запросом с помощью заголовков HTTP. Hello ниже приведен запрос toocreate документа.

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


Здесь toobe предварительной триггер hello, запустите с запросом hello указывается в заголовке x-ms-documentdb-pre-trigger-include hello. Соответственно либо после триггеров приведены в заголовок x-ms-documentdb-post-trigger-include hello. Обратите внимание, что для данного запроса могут быть определены оба вида триггеров.

## <a name="sample-code"></a>Пример кода
Дополнительные примеры кода, используемого на сервере (включая операции [массового удаления](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) и [обновления](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)), представлены в нашем [репозитории GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).

Требуется tooshare здорово хранимой процедуры? Отправьте нам запрос на получение. 

## <a name="next-steps"></a>Дальнейшие действия
После создания одного или нескольких хранимых процедур, триггеров и определяемых пользователем функций, созданных можно загрузить их и просматривать их в hello портал Azure с помощью данных обозревателя.

Кроме того, возможно следующее hello ссылки и ресурсы, которые полезны в ваш путь toolearn больше о Azure Cosmos программирование на сервере базы данных:

* [Пакет SDK для DocumentDB .NET: скачивание и заметки о выпуске](documentdb-sdk-dotnet.md).
* [DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases)
* [JSON](http://www.json.org/) 
* [JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [Безопасность и расширяемость переносной базы данных](http://dl.acm.org/citation.cfm?id=276339) 
* [Сервис-ориентированная архитектура баз данных](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [Размещение hello среды выполнения .NET в Microsoft SQL server](http://dl.acm.org/citation.cfm?id=1007669)

