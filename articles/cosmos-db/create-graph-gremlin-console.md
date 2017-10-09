---
title: "Руководство по Azure Cosmos DB. Создание, запрос и просмотр в консоли Apache TinkerPops Gremlin | Документация Майкрософт"
description: "Быстрый запуск Azure Cosmos DB toocreates вершин, границ и запросы, использующие hello Azure Cosmos DB Graph API."
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
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a><span data-ttu-id="0673e-103">Azure Cosmos DB: Создавать запросы и просматривать диаграммы, в консоли Gremlin hello</span><span class="sxs-lookup"><span data-stu-id="0673e-103">Azure Cosmos DB: Create, query, and traverse a graph in hello Gremlin console</span></span>

<span data-ttu-id="0673e-104">Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="0673e-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="0673e-105">Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД.</span><span class="sxs-lookup"><span data-stu-id="0673e-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="0673e-106">В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB, базы данных и graph (контейнер) с помощью hello портала управления Azure, а затем используйте hello [консоли Gremlin](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) из [Apache TinkerPop](http://tinkerpop.apache.org) toowork с Диаграмма данным API (Предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="0673e-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal and then use hello [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) toowork with Graph API (preview) data.</span></span> <span data-ttu-id="0673e-107">В этом учебнике Создание и запрос вершин и края, обновление свойства вершин вершины запроса, проходят через hello graph и drop вершина.</span><span class="sxs-lookup"><span data-stu-id="0673e-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse hello graph, and drop a vertex.</span></span>

![Azure DB Cosmos из консоли Apache Gremlin hello](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="0673e-109">консоль Gremlin Hello — на основе Groovy/Java и выполняется в Linux, Mac и Windows.</span><span class="sxs-lookup"><span data-stu-id="0673e-109">hello Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="0673e-110">Его можно загрузить из hello [Apache TinkerPop сайта](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span><span class="sxs-lookup"><span data-stu-id="0673e-110">You can download it from hello [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0673e-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0673e-111">Prerequisites</span></span>

<span data-ttu-id="0673e-112">Для краткого руководства потребуется toohave подписки Azure toocreate учетную запись Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0673e-112">You need toohave an Azure subscription toocreate an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="0673e-113">Необходимо также tooinstall hello [Gremlin консоли](http://tinkerpop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="0673e-113">You also need tooinstall hello [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="0673e-114">Используйте версию 3.2.5 или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="0673e-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="0673e-115">Создание учетной записи базы данных</span><span class="sxs-lookup"><span data-stu-id="0673e-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="0673e-116">Добавление графа</span><span class="sxs-lookup"><span data-stu-id="0673e-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="0673e-117"><a id="ConnectAppService"></a>Подключение tooyour службы приложений</span><span class="sxs-lookup"><span data-stu-id="0673e-117"><a id="ConnectAppService"></a>Connect tooyour app service</span></span>
1. <span data-ttu-id="0673e-118">Перед началом hello Gremlin консоли, создать или изменить файл конфигурации удаленного secure.yaml hello в каталоге apache-tinkerpop-gremlin-console-3.2.5/conf hello.</span><span class="sxs-lookup"><span data-stu-id="0673e-118">Before starting hello Gremlin Console, create or modify hello remote-secure.yaml configuration file in hello apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="0673e-119">Укажите *узел*, *порт*, *пользователя*, *пароль*, *пул подключений* и *сериализатор*:</span><span class="sxs-lookup"><span data-stu-id="0673e-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="0673e-120">Настройка</span><span class="sxs-lookup"><span data-stu-id="0673e-120">Setting</span></span>|<span data-ttu-id="0673e-121">Рекомендуемое значение</span><span class="sxs-lookup"><span data-stu-id="0673e-121">Suggested value</span></span>|<span data-ttu-id="0673e-122">Описание</span><span class="sxs-lookup"><span data-stu-id="0673e-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="0673e-123">Узлы</span><span class="sxs-lookup"><span data-stu-id="0673e-123">hosts</span></span>|<span data-ttu-id="0673e-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="0673e-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="0673e-125">Просмотрите указанный ниже снимок экрана.</span><span class="sxs-lookup"><span data-stu-id="0673e-125">See screenshot below.</span></span> <span data-ttu-id="0673e-126">Это значение hello Gremlin URI на странице общих сведений hello hello в квадратных скобках с конечными hello портале Azure: 443 / удален.</span><span class="sxs-lookup"><span data-stu-id="0673e-126">This is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="0673e-127">Это значение также можно получить из вкладки ключи hello, используя значение URI hello, удаляя https://, документы toographs изменение и удаление в конце hello: 443 /.</span><span class="sxs-lookup"><span data-stu-id="0673e-127">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="0673e-128">порт</span><span class="sxs-lookup"><span data-stu-id="0673e-128">port</span></span>|<span data-ttu-id="0673e-129">443</span><span class="sxs-lookup"><span data-stu-id="0673e-129">443</span></span>|<span data-ttu-id="0673e-130">Задать too443.</span><span class="sxs-lookup"><span data-stu-id="0673e-130">Set too443.</span></span>
    <span data-ttu-id="0673e-131">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="0673e-131">username</span></span>|<span data-ttu-id="0673e-132">*Имя пользователя*</span><span class="sxs-lookup"><span data-stu-id="0673e-132">*Your username*</span></span>|<span data-ttu-id="0673e-133">Здравствуйте ресурсов hello формы `/dbs/<db>/colls/<coll>` где `<db>` — это имя базы данных и `<coll>` — это имя коллекции.</span><span class="sxs-lookup"><span data-stu-id="0673e-133">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="0673e-134">пароль</span><span class="sxs-lookup"><span data-stu-id="0673e-134">password</span></span>|<span data-ttu-id="0673e-135">*Значение первичного ключа*</span><span class="sxs-lookup"><span data-stu-id="0673e-135">*Your primary key*</span></span>| <span data-ttu-id="0673e-136">Просмотрите второй снимок экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="0673e-136">See second screenshot below.</span></span> <span data-ttu-id="0673e-137">Это первичного ключа, которое можно получить со страницы приветствия ключи hello портал Azure, в поле hello первичный ключ.</span><span class="sxs-lookup"><span data-stu-id="0673e-137">This is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="0673e-138">Используйте "Копировать" hello "hello левой части toocopy hello hello поле значение.</span><span class="sxs-lookup"><span data-stu-id="0673e-138">Use hello copy button on hello left side of hello box toocopy hello value.</span></span>
    <span data-ttu-id="0673e-139">Пул подключений</span><span class="sxs-lookup"><span data-stu-id="0673e-139">connectionPool</span></span>|<span data-ttu-id="0673e-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="0673e-140">{enableSsl: true}</span></span>|<span data-ttu-id="0673e-141">Параметр пула подключений для SSL.</span><span class="sxs-lookup"><span data-stu-id="0673e-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="0673e-142">serializer</span><span class="sxs-lookup"><span data-stu-id="0673e-142">serializer</span></span>|<span data-ttu-id="0673e-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="0673e-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="0673e-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="0673e-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="0673e-145">config: { serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="0673e-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="0673e-146">Задайте значение toothis и удалять любые `\n` разрывы строки, при вставке в значение hello.</span><span class="sxs-lookup"><span data-stu-id="0673e-146">Set toothis value and delete any `\n` line breaks when pasting in hello value.</span></span>

    <span data-ttu-id="0673e-147">Для значения узлов hello, скопируйте hello **Gremlin URI** значение из hello **Обзор** страницы: ![представление и скопируйте значение Gremlin URI hello на странице Обзор hello в hello портал Azure](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="0673e-147">For hello hosts value, copy hello **Gremlin URI** value from hello **Overview** page: ![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="0673e-148">Значение пароля hello, скопируйте hello **первичного ключа** из hello **ключей** страницы: ![Просмотр и копирование первичного ключа в hello портал Azure, ключи страницы](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="0673e-148">For hello password value, copy hello **Primary key** from hello **Keys** page: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="0673e-149">В окне терминала выполните `bin/gremlin.bat` или `bin/gremlin.sh` toostart hello [Gremlin консоли](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="0673e-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` toostart hello [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="0673e-150">В окне терминала выполните `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour приложения службы.</span><span class="sxs-lookup"><span data-stu-id="0673e-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="0673e-151">Если ошибка hello `No appenders could be found for logger` убедитесь, что значение сериализатора hello в файле secure.yaml удаленного hello обновлена как описано в шаге 2.</span><span class="sxs-lookup"><span data-stu-id="0673e-151">If you receive hello error `No appenders could be found for logger` ensure that you updated hello serializer value in hello remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="0673e-152">Отлично!</span><span class="sxs-lookup"><span data-stu-id="0673e-152">Great!</span></span> <span data-ttu-id="0673e-153">Теперь, когда мы hello Настройка завершена, давайте начнем, выполнение некоторых команд консоли.</span><span class="sxs-lookup"><span data-stu-id="0673e-153">Now that we finished hello setup, let's start running some console commands.</span></span>

<span data-ttu-id="0673e-154">Выполним простую команду count().</span><span class="sxs-lookup"><span data-stu-id="0673e-154">Let's try a simple count() command.</span></span> <span data-ttu-id="0673e-155">Введите ниже hello в консоль hello в строке приветствия:</span><span class="sxs-lookup"><span data-stu-id="0673e-155">Type hello following into hello console at hello prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="0673e-156">Обратите внимание hello `:>` , предшествующий hello `g.V().count()` текста?</span><span class="sxs-lookup"><span data-stu-id="0673e-156">Notice hello `:>` that precedes hello `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="0673e-157">Это является частью команды hello, необходимые tootype.</span><span class="sxs-lookup"><span data-stu-id="0673e-157">This is part of hello command you need tootype.</span></span> <span data-ttu-id="0673e-158">Очень важно при использовании консоли Gremlin hello Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0673e-158">It is important when using hello Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="0673e-159">Пропуск это `:>` префикс указывает, что команда hello tooexecute консоли hello локально, часто для графа в памяти.</span><span class="sxs-lookup"><span data-stu-id="0673e-159">Omitting this `:>` prefix instructs hello console tooexecute hello command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="0673e-160">С помощью этого `:>` сообщает tooexecute консоли hello удаленной команды в этом случае для Cosmos DB (либо эмулятор localhost hello, или > экземпляра Azure).</span><span class="sxs-lookup"><span data-stu-id="0673e-160">Using this `:>` tells hello console tooexecute a remote command, in this case against Cosmos DB (either hello localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="0673e-161">Создание вершин и границ</span><span class="sxs-lookup"><span data-stu-id="0673e-161">Create vertices and edges</span></span>

<span data-ttu-id="0673e-162">Начнем с добавления пяти вершин для пользователей *Thomas*, *Mary Kay*, *Robin*, *Ben* и *Jack*.</span><span class="sxs-lookup"><span data-stu-id="0673e-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="0673e-163">Входные данные (Thomas):</span><span class="sxs-lookup"><span data-stu-id="0673e-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="0673e-164">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="0673e-165">Входные данные (Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="0673e-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="0673e-166">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="0673e-167">Входные данные (Robin):</span><span class="sxs-lookup"><span data-stu-id="0673e-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="0673e-168">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="0673e-169">Входные данные (Ben):</span><span class="sxs-lookup"><span data-stu-id="0673e-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="0673e-170">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="0673e-171">Входные данные (Jack):</span><span class="sxs-lookup"><span data-stu-id="0673e-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="0673e-172">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="0673e-173">Далее добавим границы для создания связей между пользователями.</span><span class="sxs-lookup"><span data-stu-id="0673e-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="0673e-174">Входные данные (Thomas -> Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="0673e-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="0673e-175">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="0673e-176">Входные данные (Thomas -> Robin):</span><span class="sxs-lookup"><span data-stu-id="0673e-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="0673e-177">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="0673e-178">Входные данные (Robin -> Ben):</span><span class="sxs-lookup"><span data-stu-id="0673e-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="0673e-179">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="0673e-180">Обновление вершины</span><span class="sxs-lookup"><span data-stu-id="0673e-180">Update a vertex</span></span>

<span data-ttu-id="0673e-181">Давайте обновить hello *Thomas* вершин с новой возраст *45*.</span><span class="sxs-lookup"><span data-stu-id="0673e-181">Let's update hello *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="0673e-182">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="0673e-183">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="0673e-184">Запрос графа</span><span class="sxs-lookup"><span data-stu-id="0673e-184">Query your graph</span></span>

<span data-ttu-id="0673e-185">Теперь давайте отправим разные запросы к графу.</span><span class="sxs-lookup"><span data-stu-id="0673e-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="0673e-186">Во-первых давайте попробуем запроса фильтра tooreturn только тем, кто являются более старыми, чем 40 лет.</span><span class="sxs-lookup"><span data-stu-id="0673e-186">First, let's try a query with a filter tooreturn only people who are older than 40 years old.</span></span>

<span data-ttu-id="0673e-187">Входные данные (запрос с фильтрацией):</span><span class="sxs-lookup"><span data-stu-id="0673e-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="0673e-188">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="0673e-189">Далее, давайте hello первого имя проекта для hello людей, которые являются более старыми, чем 40 лет.</span><span class="sxs-lookup"><span data-stu-id="0673e-189">Next, let's project hello first name for hello people who are older than 40 years old.</span></span>

<span data-ttu-id="0673e-190">Входные данные (запрос с фильтрацией и проекцией):</span><span class="sxs-lookup"><span data-stu-id="0673e-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="0673e-191">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="0673e-192">Просмотр графа</span><span class="sxs-lookup"><span data-stu-id="0673e-192">Traverse your graph</span></span>

<span data-ttu-id="0673e-193">Давайте перекрестной hello graph tooreturn все его Thomas друзей.</span><span class="sxs-lookup"><span data-stu-id="0673e-193">Let's traverse hello graph tooreturn all of Thomas's friends.</span></span>

<span data-ttu-id="0673e-194">Входные данные (друзья пользователя Thomas):</span><span class="sxs-lookup"><span data-stu-id="0673e-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="0673e-195">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="0673e-196">Теперь давайте hello следующий уровень вершин.</span><span class="sxs-lookup"><span data-stu-id="0673e-196">Next, let's get hello next layer of vertices.</span></span> <span data-ttu-id="0673e-197">Просматривает все hello друзьях друзей Томас hello graph tooreturn.</span><span class="sxs-lookup"><span data-stu-id="0673e-197">Traverse hello graph tooreturn all hello friends of Thomas's friends.</span></span>

<span data-ttu-id="0673e-198">Входные данные (знакомые пользователя Thomas):</span><span class="sxs-lookup"><span data-stu-id="0673e-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="0673e-199">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="0673e-200">Удаление вершины</span><span class="sxs-lookup"><span data-stu-id="0673e-200">Drop a vertex</span></span>

<span data-ttu-id="0673e-201">Давайте теперь удалить узел из базы данных graph hello.</span><span class="sxs-lookup"><span data-stu-id="0673e-201">Let's now delete a vertex from hello graph database.</span></span>

<span data-ttu-id="0673e-202">Входные данные (удаление вершины Jack):</span><span class="sxs-lookup"><span data-stu-id="0673e-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="0673e-203">Очистка графа</span><span class="sxs-lookup"><span data-stu-id="0673e-203">Clear your graph</span></span>

<span data-ttu-id="0673e-204">Наконец давайте очистить базу данных hello всех вершин и границ.</span><span class="sxs-lookup"><span data-stu-id="0673e-204">Finally, let's clear hello database of all vertices and edges.</span></span>

<span data-ttu-id="0673e-205">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="0673e-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="0673e-206">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="0673e-206">Congratulations!</span></span> <span data-ttu-id="0673e-207">Вы завершили работу с этим руководством по использованию API Graph в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0673e-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="0673e-208">Просмотрите соглашений об уровне обслуживания в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="0673e-208">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="0673e-209">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="0673e-209">Clean up resources</span></span>

<span data-ttu-id="0673e-210">Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="0673e-210">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>  

1. <span data-ttu-id="0673e-211">Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="0673e-211">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="0673e-212">На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="0673e-212">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0673e-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0673e-213">Next steps</span></span>

<span data-ttu-id="0673e-214">В этом кратком руководстве вы узнали, как toocreate учетную запись Azure Cosmos DB, создать граф, с помощью hello обозреватель данных, создать вершин и ребра и просматривать диаграммы с помощью консоли Gremlin hello.</span><span class="sxs-lookup"><span data-stu-id="0673e-214">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, create vertices and edges, and traverse your graph using hello Gremlin console.</span></span> <span data-ttu-id="0673e-215">Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin.</span><span class="sxs-lookup"><span data-stu-id="0673e-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="0673e-216">Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="0673e-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
