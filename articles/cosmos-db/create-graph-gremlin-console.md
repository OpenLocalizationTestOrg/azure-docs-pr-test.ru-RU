---
title: "Руководство по Azure Cosmos DB. Создание, запрос и просмотр в консоли Apache TinkerPops Gremlin | Документация Майкрософт"
description: "Краткое руководство по созданию вершин, границ и запросов с помощью Graph API в Azure Cosmos DB."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: fd5cc93ce1ed2a8c7da090666ef539b338ac61c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-the-gremlin-console"></a><span data-ttu-id="9e78a-103">Azure Cosmos DB. Создание, запрос и просмотр в консоли Gremlin</span><span class="sxs-lookup"><span data-stu-id="9e78a-103">Azure Cosmos DB: Create, query, and traverse a graph in the Gremlin console</span></span>

<span data-ttu-id="9e78a-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9e78a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="9e78a-105">Вы можете быстро создавать и запрашивать документы, пары "ключ — значение" и базы данных графов, используя преимущества возможностей глобального распределения и горизонтального масштабирования Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9e78a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="9e78a-106">В этом кратком руководстве показано, как создать учетную запись Azure Cosmos DB, базу данных и граф (контейнер) с помощью портала Azure, а затем использовать [консоль Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) из [Apache TinkerPop](http://tinkerpop.apache.org) для работы с данными API Graph (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="9e78a-106">This quick start demonstrates how to create an Azure Cosmos DB account, database, and graph (container) using the Azure portal and then use the [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) to work with Graph API (preview) data.</span></span> <span data-ttu-id="9e78a-107">В этом руководстве вы создадите вершины и границы и отправите к ним запрос, обновите свойства вершины, отправите запросы к вершинам, просмотрите граф и удалите вершину.</span><span class="sxs-lookup"><span data-stu-id="9e78a-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse the graph, and drop a vertex.</span></span>

![Azure DB Cosmos в консоли Apache Gremlin](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="9e78a-109">Консоль Gremlin создана на базе Groovy и Java и работает на компьютерах Linux, Mac и Windows.</span><span class="sxs-lookup"><span data-stu-id="9e78a-109">The Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="9e78a-110">Ее можно скачать с [сайта Apache TinkerPop](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span><span class="sxs-lookup"><span data-stu-id="9e78a-110">You can download it from the [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e78a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9e78a-111">Prerequisites</span></span>

<span data-ttu-id="9e78a-112">Для создания учетной записи Azure Cosmos DB во время работы с этим кратким руководством вам потребуется подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="9e78a-112">You need to have an Azure subscription to create an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="9e78a-113">Вам также нужно установить [консоль Gremlin](http://tinkerpop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="9e78a-113">You also need to install the [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="9e78a-114">Используйте версию 3.2.5 или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="9e78a-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="9e78a-115">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="9e78a-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="9e78a-116">Добавление графа</span><span class="sxs-lookup"><span data-stu-id="9e78a-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="9e78a-117"><a id="ConnectAppService"></a>Подключение к службе приложений</span><span class="sxs-lookup"><span data-stu-id="9e78a-117"><a id="ConnectAppService"></a>Connect to your app service</span></span>
1. <span data-ttu-id="9e78a-118">Перед запуском консоли Gremlin создайте или измените файл конфигурации remote-secure.yaml в каталоге apache-tinkerpop-gremlin-console-3.2.5/conf.</span><span class="sxs-lookup"><span data-stu-id="9e78a-118">Before starting the Gremlin Console, create or modify the remote-secure.yaml configuration file in the apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="9e78a-119">Укажите *узел*, *порт*, *пользователя*, *пароль*, *пул подключений* и *сериализатор*:</span><span class="sxs-lookup"><span data-stu-id="9e78a-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="9e78a-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="9e78a-120">Setting</span></span>|<span data-ttu-id="9e78a-121">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="9e78a-121">Suggested value</span></span>|<span data-ttu-id="9e78a-122">Описание</span><span class="sxs-lookup"><span data-stu-id="9e78a-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="9e78a-123">Узлы</span><span class="sxs-lookup"><span data-stu-id="9e78a-123">hosts</span></span>|<span data-ttu-id="9e78a-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="9e78a-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="9e78a-125">Просмотрите указанный ниже снимок экрана.</span><span class="sxs-lookup"><span data-stu-id="9e78a-125">See screenshot below.</span></span> <span data-ttu-id="9e78a-126">Это значение Gremlin URI на странице обзора портала Azure, заключенное в квадратные скобки и без окончания 443/.</span><span class="sxs-lookup"><span data-stu-id="9e78a-126">This is the Gremlin URI value on the Overview page of the Azure portal, in square brackets, with the trailing :443/ removed.</span></span><br><br><span data-ttu-id="9e78a-127">Его также можно получить на вкладке "Ключи" с помощью значения URI, удалив https://, изменив документы на диаграммы и удалив окончание 443/.</span><span class="sxs-lookup"><span data-stu-id="9e78a-127">This value can also be retrieved from the Keys tab, using the URI value by removing https://, changing documents to graphs, and removing the trailing :443/.</span></span>
    <span data-ttu-id="9e78a-128">порт</span><span class="sxs-lookup"><span data-stu-id="9e78a-128">port</span></span>|<span data-ttu-id="9e78a-129">443</span><span class="sxs-lookup"><span data-stu-id="9e78a-129">443</span></span>|<span data-ttu-id="9e78a-130">Задайте значение 443.</span><span class="sxs-lookup"><span data-stu-id="9e78a-130">Set to 443.</span></span>
    <span data-ttu-id="9e78a-131">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="9e78a-131">username</span></span>|<span data-ttu-id="9e78a-132">*Имя пользователя*</span><span class="sxs-lookup"><span data-stu-id="9e78a-132">*Your username*</span></span>|<span data-ttu-id="9e78a-133">Ресурс в формате `/dbs/<db>/colls/<coll>`, где `<db>` — это имя базы данных, а `<coll>` — имя коллекции.</span><span class="sxs-lookup"><span data-stu-id="9e78a-133">The resource of the form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="9e78a-134">пароль</span><span class="sxs-lookup"><span data-stu-id="9e78a-134">password</span></span>|<span data-ttu-id="9e78a-135">*Значение первичного ключа*</span><span class="sxs-lookup"><span data-stu-id="9e78a-135">*Your primary key*</span></span>| <span data-ttu-id="9e78a-136">Просмотрите второй снимок экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="9e78a-136">See second screenshot below.</span></span> <span data-ttu-id="9e78a-137">Это первичный ключ, который можно получить на странице "Ключи" на портале Azure в поле "Первичный ключ".</span><span class="sxs-lookup"><span data-stu-id="9e78a-137">This is your primary key, which you can retrieve from the Keys page of the Azure portal, in the Primary Key box.</span></span> <span data-ttu-id="9e78a-138">Скопируйте значение с помощью кнопки копирования в левой части поля.</span><span class="sxs-lookup"><span data-stu-id="9e78a-138">Use the copy button on the left side of the box to copy the value.</span></span>
    <span data-ttu-id="9e78a-139">Пул подключений</span><span class="sxs-lookup"><span data-stu-id="9e78a-139">connectionPool</span></span>|<span data-ttu-id="9e78a-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="9e78a-140">{enableSsl: true}</span></span>|<span data-ttu-id="9e78a-141">Параметр пула подключений для SSL.</span><span class="sxs-lookup"><span data-stu-id="9e78a-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="9e78a-142">serializer</span><span class="sxs-lookup"><span data-stu-id="9e78a-142">serializer</span></span>|<span data-ttu-id="9e78a-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="9e78a-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="9e78a-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="9e78a-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="9e78a-145">config: { serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="9e78a-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="9e78a-146">Задайте это значение и удалите все разрывы строк `\n` при вставке значения.</span><span class="sxs-lookup"><span data-stu-id="9e78a-146">Set to this value and delete any `\n` line breaks when pasting in the value.</span></span>

    <span data-ttu-id="9e78a-147">Для значений узлов скопируйте значение **Gremlin URI** со страницы **обзора**: ![Просмотр и копирование значения Gremlin URI на странице обзора на портале Azure](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="9e78a-147">For the hosts value, copy the **Gremlin URI** value from the **Overview** page: ![View and copy the Gremlin URI value on the Overview page in the Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="9e78a-148">Для значений пароля скопируйте **первичный ключ** со страницы **Ключи**: ![Просмотр и копирование первичного ключа на портале Azure из страницы "Ключи"](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="9e78a-148">For the password value, copy the **Primary key** from the **Keys** page: ![View and copy your primary key in the Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="9e78a-149">В окне терминала запустите файл `bin/gremlin.bat` или `bin/gremlin.sh`, чтобы запустить [консоль Gremlin](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="9e78a-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` to start the [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="9e78a-150">Чтобы подключиться к службе приложений, в окне терминала запустите файл `:remote connect tinkerpop.server conf/remote-secure.yaml`.</span><span class="sxs-lookup"><span data-stu-id="9e78a-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` to connect to your app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="9e78a-151">При возникновении ошибки `No appenders could be found for logger` убедитесь, что значение сериализатора в файле remote-secure.yaml обновлено, как описано на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="9e78a-151">If you receive the error `No appenders could be found for logger` ensure that you updated the serializer value in the remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="9e78a-152">Отлично!</span><span class="sxs-lookup"><span data-stu-id="9e78a-152">Great!</span></span> <span data-ttu-id="9e78a-153">Теперь, когда мы завершили настройку, начнем выполнять команды консоли.</span><span class="sxs-lookup"><span data-stu-id="9e78a-153">Now that we finished the setup, let's start running some console commands.</span></span>

<span data-ttu-id="9e78a-154">Выполним простую команду count().</span><span class="sxs-lookup"><span data-stu-id="9e78a-154">Let's try a simple count() command.</span></span> <span data-ttu-id="9e78a-155">Введите следующее в командную строку консоли:</span><span class="sxs-lookup"><span data-stu-id="9e78a-155">Type the following into the console at the prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="9e78a-156">Обратите внимание на символы `:>`, предшествующие тексту `g.V().count()`.</span><span class="sxs-lookup"><span data-stu-id="9e78a-156">Notice the `:>` that precedes the `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="9e78a-157">Это — часть выполняемой команды,</span><span class="sxs-lookup"><span data-stu-id="9e78a-157">This is part of the command you need to type.</span></span> <span data-ttu-id="9e78a-158">необходимая при использовании консоли Gremlin с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9e78a-158">It is important when using the Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="9e78a-159">Пропуск префикса `:>` указывает консоли выполнять команду локально — часто в отношении выполняющегося в памяти графа.</span><span class="sxs-lookup"><span data-stu-id="9e78a-159">Omitting this `:>` prefix instructs the console to execute the command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="9e78a-160">Наличие префикса `:>` указывает консоли выполнять команду удаленно — на этот раз в отношении Cosmos DB (либо эмулятора localhost, либо > экземпляра Azure).</span><span class="sxs-lookup"><span data-stu-id="9e78a-160">Using this `:>` tells the console to execute a remote command, in this case against Cosmos DB (either the localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="9e78a-161">Создание вершин и границ</span><span class="sxs-lookup"><span data-stu-id="9e78a-161">Create vertices and edges</span></span>

<span data-ttu-id="9e78a-162">Начнем с добавления пяти вершин для пользователей *Thomas*, *Mary Kay*, *Robin*, *Ben* и *Jack*.</span><span class="sxs-lookup"><span data-stu-id="9e78a-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="9e78a-163">Входные данные (Thomas):</span><span class="sxs-lookup"><span data-stu-id="9e78a-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="9e78a-164">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="9e78a-165">Входные данные (Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="9e78a-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="9e78a-166">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="9e78a-167">Входные данные (Robin):</span><span class="sxs-lookup"><span data-stu-id="9e78a-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="9e78a-168">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="9e78a-169">Входные данные (Ben):</span><span class="sxs-lookup"><span data-stu-id="9e78a-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="9e78a-170">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="9e78a-171">Входные данные (Jack):</span><span class="sxs-lookup"><span data-stu-id="9e78a-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="9e78a-172">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="9e78a-173">Далее добавим границы для создания связей между пользователями.</span><span class="sxs-lookup"><span data-stu-id="9e78a-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="9e78a-174">Входные данные (Thomas -> Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="9e78a-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="9e78a-175">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="9e78a-176">Входные данные (Thomas -> Robin):</span><span class="sxs-lookup"><span data-stu-id="9e78a-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="9e78a-177">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="9e78a-178">Входные данные (Robin -> Ben):</span><span class="sxs-lookup"><span data-stu-id="9e78a-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="9e78a-179">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="9e78a-180">Обновление вершины</span><span class="sxs-lookup"><span data-stu-id="9e78a-180">Update a vertex</span></span>

<span data-ttu-id="9e78a-181">Давайте обновим вершину *Thomas* и добавим свойство возраста (*45*).</span><span class="sxs-lookup"><span data-stu-id="9e78a-181">Let's update the *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="9e78a-182">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="9e78a-183">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="9e78a-184">Запрос графа</span><span class="sxs-lookup"><span data-stu-id="9e78a-184">Query your graph</span></span>

<span data-ttu-id="9e78a-185">Теперь давайте отправим разные запросы к графу.</span><span class="sxs-lookup"><span data-stu-id="9e78a-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="9e78a-186">Сначала давайте отправим запрос с фильтрацией, который возвращает сведения только о людях старше 40 лет.</span><span class="sxs-lookup"><span data-stu-id="9e78a-186">First, let's try a query with a filter to return only people who are older than 40 years old.</span></span>

<span data-ttu-id="9e78a-187">Входные данные (запрос с фильтрацией):</span><span class="sxs-lookup"><span data-stu-id="9e78a-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="9e78a-188">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="9e78a-189">Далее давайте спроектируем имя для людей старше 40 лет.</span><span class="sxs-lookup"><span data-stu-id="9e78a-189">Next, let's project the first name for the people who are older than 40 years old.</span></span>

<span data-ttu-id="9e78a-190">Входные данные (запрос с фильтрацией и проекцией):</span><span class="sxs-lookup"><span data-stu-id="9e78a-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="9e78a-191">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="9e78a-192">Просмотр графа</span><span class="sxs-lookup"><span data-stu-id="9e78a-192">Traverse your graph</span></span>

<span data-ttu-id="9e78a-193">Давайте просмотрим граф, чтобы возвратить сведения обо всех друзьях пользователя Thomas.</span><span class="sxs-lookup"><span data-stu-id="9e78a-193">Let's traverse the graph to return all of Thomas's friends.</span></span>

<span data-ttu-id="9e78a-194">Входные данные (друзья пользователя Thomas):</span><span class="sxs-lookup"><span data-stu-id="9e78a-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="9e78a-195">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="9e78a-196">Далее рассмотрим следующий уровень вершин.</span><span class="sxs-lookup"><span data-stu-id="9e78a-196">Next, let's get the next layer of vertices.</span></span> <span data-ttu-id="9e78a-197">Давайте просмотрим граф, чтобы возвратить сведения обо всех знакомых пользователя Thomas.</span><span class="sxs-lookup"><span data-stu-id="9e78a-197">Traverse the graph to return all the friends of Thomas's friends.</span></span>

<span data-ttu-id="9e78a-198">Входные данные (знакомые пользователя Thomas):</span><span class="sxs-lookup"><span data-stu-id="9e78a-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="9e78a-199">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="9e78a-200">Удаление вершины</span><span class="sxs-lookup"><span data-stu-id="9e78a-200">Drop a vertex</span></span>

<span data-ttu-id="9e78a-201">Теперь давайте удалим вершину из базы данных графа.</span><span class="sxs-lookup"><span data-stu-id="9e78a-201">Let's now delete a vertex from the graph database.</span></span>

<span data-ttu-id="9e78a-202">Входные данные (удаление вершины Jack):</span><span class="sxs-lookup"><span data-stu-id="9e78a-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="9e78a-203">Очистка графа</span><span class="sxs-lookup"><span data-stu-id="9e78a-203">Clear your graph</span></span>

<span data-ttu-id="9e78a-204">Наконец, давайте очистим базу данных ото всех вершин и границ.</span><span class="sxs-lookup"><span data-stu-id="9e78a-204">Finally, let's clear the database of all vertices and edges.</span></span>

<span data-ttu-id="9e78a-205">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="9e78a-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="9e78a-206">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="9e78a-206">Congratulations!</span></span> <span data-ttu-id="9e78a-207">Вы завершили работу с этим руководством по использованию API Graph в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9e78a-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="9e78a-208">Просмотр соглашений об уровне обслуживания на портале Azure</span><span class="sxs-lookup"><span data-stu-id="9e78a-208">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="9e78a-209">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="9e78a-209">Clean up resources</span></span>

<span data-ttu-id="9e78a-210">Если вы не собираетесь использовать это приложение дальше, удалите все ресурсы, созданные в ходе работы с этим руководством, на портале Azure, сделав следующее:</span><span class="sxs-lookup"><span data-stu-id="9e78a-210">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>  

1. <span data-ttu-id="9e78a-211">В меню слева на портале Azure щелкните **Группы ресурсов**, а затем выберите имя созданного ресурса.</span><span class="sxs-lookup"><span data-stu-id="9e78a-211">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="9e78a-212">На странице группы ресурсов щелкните **Удалить**, в текстовом поле введите имя ресурса для удаления и щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="9e78a-212">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e78a-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9e78a-213">Next steps</span></span>

<span data-ttu-id="9e78a-214">В этом кратком руководстве вы узнали, как создать учетную запись Azure Cosmos DB, создать граф с помощью обозревателя данных, вершины и границы, а также просмотреть граф с помощью консоли Gremlin.</span><span class="sxs-lookup"><span data-stu-id="9e78a-214">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a graph using the Data Explorer, create vertices and edges, and traverse your graph using the Gremlin console.</span></span> <span data-ttu-id="9e78a-215">Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="9e78a-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="9e78a-216">Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="9e78a-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
