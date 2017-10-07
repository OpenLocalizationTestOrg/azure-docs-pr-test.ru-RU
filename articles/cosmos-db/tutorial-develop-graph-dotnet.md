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
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="3c2c3-103">Azure Cosmos DB: Разработку с использованием hello API Graph в .NET</span><span class="sxs-lookup"><span data-stu-id="3c2c3-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="3c2c3-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="3c2c3-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="3c2c3-106">В этом учебнике показано, как Azure Cosmos DB учетной записи с помощью toocreate hello портал Azure и как toocreate диаграммы базы данных и контейнера.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="3c2c3-107">Затем приложение Hello создает простой социальных сетей с четырьмя пользователями hello [Graph API](graph-sdk-dotnet.md) (Предварительная версия), затем проходит через и запросы с помощью Gremlin граф hello.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="3c2c3-108">В этом учебнике hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="3c2c3-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3c2c3-109">создание учетной записи Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="3c2c3-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="3c2c3-110">создание базы данных графа и контейнера;</span><span class="sxs-lookup"><span data-stu-id="3c2c3-110">Create a graph database and container</span></span>
> * <span data-ttu-id="3c2c3-111">Сериализовать объекты too.NET вершин и контуров</span><span class="sxs-lookup"><span data-stu-id="3c2c3-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="3c2c3-112">Добавление вершин и ребер</span><span class="sxs-lookup"><span data-stu-id="3c2c3-112">Add vertices and edges</span></span>
> * <span data-ttu-id="3c2c3-113">С помощью Gremlin граф запроса hello</span><span class="sxs-lookup"><span data-stu-id="3c2c3-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="3c2c3-114">Графы в базе данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3c2c3-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="3c2c3-115">Можно использовать базу данных Azure Cosmos toocreate, обновления и графиков запроса с помощью hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) библиотеки.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="3c2c3-116">Библиотека Microsoft.Azure.Graph Hello предоставляет метод одно расширение `CreateGremlinQuery<T>` поверх hello `DocumentClient` класса tooexecute Gremlin запросов.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="3c2c3-117">Gremlin — это функциональный язык программирования, поддерживающий операции записи (DML) и операции запросов и обхода.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="3c2c3-118">Мы рассмотрим несколько примеров в этой статье tooget к работе с Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="3c2c3-119">Подробное пошаговое руководство о возможностях Gremlin, доступных в базе данных Azure Cosmos DB, см. в статье [Azure Cosmos DB Gremlin graph support](gremlin-support.md) (Поддержка графа Gremlin в базе данных Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="3c2c3-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3c2c3-120">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3c2c3-120">Prerequisites</span></span>
<span data-ttu-id="3c2c3-121">Убедитесь, что у вас есть следующие hello:</span><span class="sxs-lookup"><span data-stu-id="3c2c3-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="3c2c3-122">Активная учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-122">An active Azure account.</span></span> <span data-ttu-id="3c2c3-123">Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3c2c3-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="3c2c3-124">Кроме того, можно использовать hello [эмулятор Azure DocumentDB](local-emulator.md) для этого учебника.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="3c2c3-125">[Visual Studio](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="3c2c3-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="3c2c3-126">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="3c2c3-126">Create database account</span></span>

<span data-ttu-id="3c2c3-127">Давайте начнем с создания учетной записи Azure Cosmos DB в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="3c2c3-128">Уже есть учетная запись Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="3c2c3-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="3c2c3-129">Если Да, пропустить слишком[Настройка решения Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="3c2c3-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="3c2c3-130">У вас была учетная запись Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="3c2c3-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="3c2c3-131">Если таким образом, учетной записи теперь учетную запись Azure Cosmos DB и можно сразу перейти слишком[Настройка решения Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="3c2c3-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="3c2c3-132">Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[настроить решение Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="3c2c3-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="3c2c3-133"><a id="SetupVS"></a>Настройка решения Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c2c3-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="3c2c3-134">Откройте **Visual Studio** у себя на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="3c2c3-135">На hello **файл** последовательно выберите пункты **New**и нажмите кнопку **проекта**.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="3c2c3-136">В hello **новый проект** диалогового окна выберите **шаблоны** / **Visual C#** / **консольного приложения (.NET Framework)**, имя проекта и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="3c2c3-137">В hello **обозревателе решений**, щелкните правой кнопкой мыши новое консольное приложение, который находится под управлением решения Visual Studio, и нажмите кнопку **управление пакетами NuGet...**</span><span class="sxs-lookup"><span data-stu-id="3c2c3-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="3c2c3-138">В hello **NuGet** щелкните **Обзор**и тип **Microsoft.Azure.Graphs** в поле поиска hello и проверка hello **включать предварительные версии**.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="3c2c3-139">В результатах поиска hello, найти **Microsoft.Azure.Graphs** и нажмите кнопку **установить**.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="3c2c3-140">Если вы получите сообщение о рецензировании решения toohello изменения, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="3c2c3-141">Если появится сообщение о принятии условий лицензионного соглашения, щелкните **Принимаю**.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="3c2c3-142">Hello `Microsoft.Azure.Graphs` библиотека предоставляет методы расширения в одном `CreateGremlinQuery<T>` для выполнения Gremlin операций.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="3c2c3-143">Gremlin — это функциональный язык программирования, поддерживающий операции записи (DML) и операции запросов и обхода.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="3c2c3-144">Мы рассмотрим несколько примеров в этой статье tooget к работе с Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="3c2c3-145">Подробное пошаговое руководство о возможностях Gremlin, доступных в базе данных Azure Cosmos DB, см. в статье [Azure Cosmos DB Gremlin graph support](gremlin-support.md) (Поддержка графа Gremlin в базе данных Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="3c2c3-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="3c2c3-146"><a id="add-references"></a>Подключение приложения</span><span class="sxs-lookup"><span data-stu-id="3c2c3-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="3c2c3-147">Добавьте эти две константы и переменную *client* в приложение.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="3c2c3-148">Далее head резервное toohello [портал Azure](https://portal.azure.com) tooretrieve URL-адрес конечной точки и первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="3c2c3-149">URL-адрес конечной точки Hello и первичный ключ, необходимые для вашего приложения toounderstand где tooconnect, а для Azure Cosmos DB tootrust подключения вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="3c2c3-150">В hello портал Azure, перейдите учетная запись Azure Cosmos DB tooyour, щелкните **ключи**, а затем нажмите кнопку **ключи для чтения и записи**.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="3c2c3-151">Скопируйте hello URI с портала hello и вставьте его через `Endpoint` свойства конечной точки hello выше.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="3c2c3-152">А затем копировать hello первичный ключ с портала hello и вставьте его в hello `AuthKey` свойство выше.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="3c2c3-153">! [Снимок экрана приветствия портал Azure используется hello учебника toocreate приложение C#.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="3c2c3-154">Показывает учетную запись Azure Cosmos DB hello ключи кнопки выделены на hello Azure Cosmos DB навигации и значения URI и первичный ключ hello выделены на hello колонке ключи] [ключи]</span><span class="sxs-lookup"><span data-stu-id="3c2c3-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="3c2c3-155"><a id="instantiate"></a>Создать экземпляр hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="3c2c3-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="3c2c3-156">Создайте новый экземпляр hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="3c2c3-157"><a id="create-database"></a>Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="3c2c3-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="3c2c3-158">Теперь создайте Azure Cosmos DB [базы данных](documentdb-resources.md#databases) с помощью hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) метода или [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) метод hello  **DocumentClient** класс из hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3c2c3-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="3c2c3-159">Создание графа</span><span class="sxs-lookup"><span data-stu-id="3c2c3-159">Create a graph</span></span> 

<span data-ttu-id="3c2c3-160">Создайте контейнер диаграммы с помощью с помощью hello hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) метода или [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) метод hello **DocumentClient**  класса.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="3c2c3-161">Коллекция — это контейнер сущностей графа.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="3c2c3-162"><a id="serializing"></a>Сериализовать объекты too.NET вершин и контуров</span><span class="sxs-lookup"><span data-stu-id="3c2c3-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="3c2c3-163">Azure Cosmos DB использует hello [формата подключения GraphSON](gremlin-support.md), который определяет схему JSON для свойств, границ и вершин.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="3c2c3-164">Hello Azure Cosmos DB .NET SDK включает JSON.NET как зависимость, и мы сможем tooserialize и десериализации GraphSON в объекты .NET, можно работать в коде.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="3c2c3-165">В качестве примера возьмем обычную социальную сеть с четырьмя пользователями.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="3c2c3-166">Мы рассмотрим, как toocreate `Person` вершин, добавьте `Knows` отношения между ними, а затем запроса и toofind «друг друга» hello graph связи.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="3c2c3-167">Hello `Microsoft.Azure.Graphs.Elements` пространство имен предоставляет `Vertex`, `Edge`, `Property` и `VertexProperty` классы для десериализации объектов определенных toowell .NET GraphSON ответов.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="3c2c3-168">Запуск Gremlin с помощью CreateGremlinQuery</span><span class="sxs-lookup"><span data-stu-id="3c2c3-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="3c2c3-169">Язык Gremlin, как и SQL, поддерживает операции чтения, записи и запроса.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="3c2c3-170">Hello следующем фрагменте кода показано, как toocreate вершин, края, выполнить некоторые примеры запросов с использованием `CreateGremlinQuery<T>`, асинхронно пройти через эти результаты с помощью `ExecuteNextAsync` и "HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

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

## <a name="add-vertices-and-edges"></a><span data-ttu-id="3c2c3-171">Добавление вершин и ребер</span><span class="sxs-lookup"><span data-stu-id="3c2c3-171">Add vertices and edges</span></span>

<span data-ttu-id="3c2c3-172">Давайте взглянем на инструкции Gremlin hello показано hello предшествующий разделе более подробно.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="3c2c3-173">Сначала добавим некоторые вершины с помощью метода Gremlin `addV`.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="3c2c3-174">Например hello следующий фрагмент кода создает вершина «Thomas Андерсен» типа «Person» со свойствами для имени, фамилии и возраст.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

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

<span data-ttu-id="3c2c3-175">Затем мы создадим некоторые ребра между этими вершинами с помощью метода Gremlin `addE`.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

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

<span data-ttu-id="3c2c3-176">Имеющуюся вершину можно обновить, используя шаг `properties` в Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="3c2c3-177">Мы пропустить запрос hello tooexecute hello вызов через `HasMoreResults` и `ExecuteNextAsync` для оставшихся hello примеры hello.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="3c2c3-178">Вы можете удалять ребра и вершины с помощью шага Gremlin `drop`.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="3c2c3-179">Ниже приведен фрагмент, который показывает, как toodelete a вершин и edge.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="3c2c3-180">Обратите внимание, что удаление вершина выполняет каскадное удаление hello связанные краев.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="3c2c3-181">Граф запроса hello</span><span class="sxs-lookup"><span data-stu-id="3c2c3-181">Query hello graph</span></span>

<span data-ttu-id="3c2c3-182">С помощью Gremlin также можно выполнять запросы и обходы графа.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="3c2c3-183">Следующий фрагмент кода hello показано, как toocount hello число вершин в hello graph:</span><span class="sxs-lookup"><span data-stu-id="3c2c3-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="3c2c3-184">Можно выполнять фильтров с помощью элемента Gremlin `has` и `hasLabel` действия, а затем объедините их с помощью `and`, `or`, и `not` toobuild более сложные фильтры:</span><span class="sxs-lookup"><span data-stu-id="3c2c3-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="3c2c3-185">Вы можете проецировать некоторые свойства в hello результатов запроса, с помощью hello `values` шаг:</span><span class="sxs-lookup"><span data-stu-id="3c2c3-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="3c2c3-186">Пока мы видели только операторы запросов, которые работают в любой базе данных.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="3c2c3-187">Графы быстрым и эффективным для обхода операций при необходимости toonavigate toorelated границ и вершин.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="3c2c3-188">Давайте найдем всех друзей Томаса.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="3c2c3-189">Это делается с помощью элемента Gremlin `outE` шаг все hello исходящей линии Томаса toofind, а затем обходе toohello в вершины с границ с помощью элемента Gremlin `inV` шаг:</span><span class="sxs-lookup"><span data-stu-id="3c2c3-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="3c2c3-190">Hello следующий запрос выполняет два toofind прыжков все Thomas» друзьях друзей», путем вызова `outE` и `inV` два раза.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="3c2c3-191">Можно создавать более сложные запросы и реализовать логику обхода мощные graph с помощью Gremlin, включая смешивание фильтра, выражения, выполнение цикла с помощью hello `loop` шаг и реализации условной навигации с помощью hello `choose` шаг.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="3c2c3-192">Дополнительные сведения о возможностях, допустимых благодаря поддержке Gremlin, см. в [этой статье](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="3c2c3-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="3c2c3-193">Вот и все! С руководством по базе данных Azure Cosmos DB вы ознакомлены.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="3c2c3-194">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="3c2c3-194">Clean up resources</span></span>

<span data-ttu-id="3c2c3-195">Если вы не будете toocontinue toouse это приложение, используйте следующие шаги toodelete все ресурсы, созданные этого учебника в hello портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="3c2c3-196">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="3c2c3-197">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c2c3-198">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3c2c3-198">Next Steps</span></span>

<span data-ttu-id="3c2c3-199">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="3c2c3-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3c2c3-200">создали учетную запись Azure Cosmos DB;</span><span class="sxs-lookup"><span data-stu-id="3c2c3-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="3c2c3-201">создали базу данных графа и контейнер;</span><span class="sxs-lookup"><span data-stu-id="3c2c3-201">Created a graph database and container</span></span>
> * <span data-ttu-id="3c2c3-202">Сериализованные объекты too.NET вершин и контуров</span><span class="sxs-lookup"><span data-stu-id="3c2c3-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="3c2c3-203">добавили вершины и ребра;</span><span class="sxs-lookup"><span data-stu-id="3c2c3-203">Added vertices and edges</span></span>
> * <span data-ttu-id="3c2c3-204">С помощью Gremlin граф запрашиваемые hello</span><span class="sxs-lookup"><span data-stu-id="3c2c3-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="3c2c3-205">Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="3c2c3-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c2c3-206">Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="3c2c3-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
