---
title: "Azure Cosmos DB: Разработку с использованием API Graph в .NET hello | Документы Microsoft"
description: "Узнайте, как toodevelop с API Azure Cosmos DB DocumentDB, с помощью .NET"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Azure Cosmos DB: Разработку с использованием hello API Graph в .NET
Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

В этом учебнике показано, как Azure Cosmos DB учетной записи с помощью toocreate hello портал Azure и как toocreate диаграммы базы данных и контейнера. Затем приложение Hello создает простой социальных сетей с четырьмя пользователями hello [Graph API](graph-sdk-dotnet.md) (Предварительная версия), затем проходит через и запросы с помощью Gremlin граф hello.

В этом учебнике hello следующие задачи:

> [!div class="checklist"]
> * создание учетной записи Azure Cosmos DB; 
> * создание базы данных графа и контейнера;
> * Сериализовать объекты too.NET вершин и контуров
> * Добавление вершин и ребер
> * С помощью Gremlin граф запроса hello

## <a name="graphs-in-azure-cosmos-db"></a>Графы в базе данных Azure Cosmos DB
Можно использовать базу данных Azure Cosmos toocreate, обновления и графиков запроса с помощью hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) библиотеки. Библиотека Microsoft.Azure.Graph Hello предоставляет метод одно расширение `CreateGremlinQuery<T>` поверх hello `DocumentClient` класса tooexecute Gremlin запросов.

Gremlin — это функциональный язык программирования, поддерживающий операции записи (DML) и операции запросов и обхода. Мы рассмотрим несколько примеров в этой статье tooget к работе с Gremlin. Подробное пошаговое руководство о возможностях Gremlin, доступных в базе данных Azure Cosmos DB, см. в статье [Azure Cosmos DB Gremlin graph support](gremlin-support.md) (Поддержка графа Gremlin в базе данных Azure Cosmos DB). 

## <a name="prerequisites"></a>Предварительные требования
Убедитесь, что у вас есть следующие hello:

* Активная учетная запись Azure. Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/). 
    * Кроме того, можно использовать hello [эмулятор Azure DocumentDB](local-emulator.md) для этого учебника.
* [Visual Studio](http://www.visualstudio.com/)

## <a name="create-database-account"></a>Создание учетной записи базы данных

Давайте начнем с создания учетной записи Azure Cosmos DB в hello портал Azure.  

> [!TIP]
> * Уже есть учетная запись Azure Cosmos DB? Если Да, пропустить слишком[Настройка решения Visual Studio](#SetupVS)
> * У вас была учетная запись Azure DocumentDB? Если таким образом, учетной записи теперь учетную запись Azure Cosmos DB и можно сразу перейти слишком[Настройка решения Visual Studio](#SetupVS).  
> * Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[настроить решение Visual Studio](#SetupVS). 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Настройка решения Visual Studio
1. Откройте **Visual Studio** у себя на компьютере.
2. На hello **файл** последовательно выберите пункты **New**и нажмите кнопку **проекта**.
3. В hello **новый проект** диалогового окна выберите **шаблоны** / **Visual C#** / **консольного приложения (.NET Framework)**, имя проекта и нажмите кнопку **ОК**.
4. В hello **обозревателе решений**, щелкните правой кнопкой мыши новое консольное приложение, который находится под управлением решения Visual Studio, и нажмите кнопку **управление пакетами NuGet...**
5. В hello **NuGet** щелкните **Обзор**и тип **Microsoft.Azure.Graphs** в поле поиска hello и проверка hello **включать предварительные версии**.
6. В результатах поиска hello, найти **Microsoft.Azure.Graphs** и нажмите кнопку **установить**.
   
   Если вы получите сообщение о рецензировании решения toohello изменения, нажмите кнопку **ОК**. Если появится сообщение о принятии условий лицензионного соглашения, щелкните **Принимаю**.
   
    Hello `Microsoft.Azure.Graphs` библиотека предоставляет методы расширения в одном `CreateGremlinQuery<T>` для выполнения Gremlin операций. Gremlin — это функциональный язык программирования, поддерживающий операции записи (DML) и операции запросов и обхода. Мы рассмотрим несколько примеров в этой статье tooget к работе с Gremlin. Подробное пошаговое руководство о возможностях Gremlin, доступных в базе данных Azure Cosmos DB, см. в статье [Azure Cosmos DB Gremlin graph support](gremlin-support.md) (Поддержка графа Gremlin в базе данных Azure Cosmos DB).

## <a id="add-references"></a>Подключение приложения

Добавьте эти две константы и переменную *client* в приложение. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
Далее head резервное toohello [портал Azure](https://portal.azure.com) tooretrieve URL-адрес конечной точки и первичный ключ. URL-адрес конечной точки Hello и первичный ключ, необходимые для вашего приложения toounderstand где tooconnect, а для Azure Cosmos DB tootrust подключения вашего приложения. 

В hello портал Azure, перейдите учетная запись Azure Cosmos DB tooyour, щелкните **ключи**, а затем нажмите кнопку **ключи для чтения и записи**. 

Скопируйте hello URI с портала hello и вставьте его через `Endpoint` свойства конечной точки hello выше. А затем копировать hello первичный ключ с портала hello и вставьте его в hello `AuthKey` свойство выше. 

! [Снимок экрана приветствия портал Azure используется hello учебника toocreate приложение C#. Показывает учетную запись Azure Cosmos DB hello ключи кнопки выделены на hello Azure Cosmos DB навигации и значения URI и первичный ключ hello выделены на hello колонке ключи] [ключи] 
 
## <a id="instantiate"></a>Создать экземпляр hello DocumentClient 
Создайте новый экземпляр hello **DocumentClient**.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>Создание базы данных 

Теперь создайте Azure Cosmos DB [базы данных](documentdb-resources.md#databases) с помощью hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) метода или [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) метод hello  **DocumentClient** класс из hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>Создание графа 

Создайте контейнер диаграммы с помощью с помощью hello hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) метода или [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) метод hello **DocumentClient**  класса. Коллекция — это контейнер сущностей графа. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>Сериализовать объекты too.NET вершин и контуров
Azure Cosmos DB использует hello [формата подключения GraphSON](gremlin-support.md), который определяет схему JSON для свойств, границ и вершин. Hello Azure Cosmos DB .NET SDK включает JSON.NET как зависимость, и мы сможем tooserialize и десериализации GraphSON в объекты .NET, можно работать в коде.

В качестве примера возьмем обычную социальную сеть с четырьмя пользователями. Мы рассмотрим, как toocreate `Person` вершин, добавьте `Knows` отношения между ними, а затем запроса и toofind «друг друга» hello graph связи. 

Hello `Microsoft.Azure.Graphs.Elements` пространство имен предоставляет `Vertex`, `Edge`, `Property` и `VertexProperty` классы для десериализации объектов определенных toowell .NET GraphSON ответов.

## <a name="run-gremlin-using-creategremlinquery"></a>Запуск Gremlin с помощью CreateGremlinQuery
Язык Gremlin, как и SQL, поддерживает операции чтения, записи и запроса. Hello следующем фрагменте кода показано, как toocreate вершин, края, выполнить некоторые примеры запросов с использованием `CreateGremlinQuery<T>`, асинхронно пройти через эти результаты с помощью `ExecuteNextAsync` и "HasMoreResults.

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>Добавление вершин и ребер

Давайте взглянем на инструкции Gremlin hello показано hello предшествующий разделе более подробно. Сначала добавим некоторые вершины с помощью метода Gremlin `addV`. Например hello следующий фрагмент кода создает вершина «Thomas Андерсен» типа «Person» со свойствами для имени, фамилии и возраст.

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

Затем мы создадим некоторые ребра между этими вершинами с помощью метода Gremlin `addE`. 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

Имеющуюся вершину можно обновить, используя шаг `properties` в Gremlin. Мы пропустить запрос hello tooexecute hello вызов через `HasMoreResults` и `ExecuteNextAsync` для оставшихся hello примеры hello.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

Вы можете удалять ребра и вершины с помощью шага Gremlin `drop`. Ниже приведен фрагмент, который показывает, как toodelete a вершин и edge. Обратите внимание, что удаление вершина выполняет каскадное удаление hello связанные краев.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>Граф запроса hello

С помощью Gremlin также можно выполнять запросы и обходы графа. Следующий фрагмент кода hello показано, как toocount hello число вершин в hello graph:

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
Можно выполнять фильтров с помощью элемента Gremlin `has` и `hasLabel` действия, а затем объедините их с помощью `and`, `or`, и `not` toobuild более сложные фильтры:

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

Вы можете проецировать некоторые свойства в hello результатов запроса, с помощью hello `values` шаг:

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

Пока мы видели только операторы запросов, которые работают в любой базе данных. Графы быстрым и эффективным для обхода операций при необходимости toonavigate toorelated границ и вершин. Давайте найдем всех друзей Томаса. Это делается с помощью элемента Gremlin `outE` шаг все hello исходящей линии Томаса toofind, а затем обходе toohello в вершины с границ с помощью элемента Gremlin `inV` шаг:

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

Hello следующий запрос выполняет два toofind прыжков все Thomas» друзьях друзей», путем вызова `outE` и `inV` два раза. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

Можно создавать более сложные запросы и реализовать логику обхода мощные graph с помощью Gremlin, включая смешивание фильтра, выражения, выполнение цикла с помощью hello `loop` шаг и реализации условной навигации с помощью hello `choose` шаг. Дополнительные сведения о возможностях, допустимых благодаря поддержке Gremlin, см. в [этой статье](gremlin-support.md).

Вот и все! С руководством по базе данных Azure Cosmos DB вы ознакомлены. 

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, используйте следующие шаги toodelete все ресурсы, созданные этого учебника в hello портал Azure hello.  

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * создали учетную запись Azure Cosmos DB; 
> * создали базу данных графа и контейнер;
> * Сериализованные объекты too.NET вершин и контуров
> * добавили вершины и ребра;
> * С помощью Gremlin граф запрашиваемые hello

Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin. 

> [!div class="nextstepaction"]
> [Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)](tutorial-query-graph.md)
