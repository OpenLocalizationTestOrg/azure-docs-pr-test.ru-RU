---
title: "aaaAzure Cosmos DB глобального распространения учебник по DocumentDB API | Документы Microsoft"
description: "Узнайте, как toosetup Azure Cosmos DB глобального распространителя с помощью hello DocumentDB API."
services: cosmos-db
keywords: "глобальное распределение, documentdb"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a><span data-ttu-id="e75b7-104">Как toosetup Azure Cosmos DB глобального распространителя с помощью hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="e75b7-104">How toosetup Azure Cosmos DB global distribution using hello DocumentDB API</span></span>

<span data-ttu-id="e75b7-105">В этой статье показано, как toouse hello Azure toosetup портала Azure Cosmos DB глобального распространения, а затем подключитесь с помощью DocumentDB API hello.</span><span class="sxs-lookup"><span data-stu-id="e75b7-105">In this article, we show how toouse hello Azure portal toosetup Azure Cosmos DB global distribution and then connect using hello DocumentDB API.</span></span>

<span data-ttu-id="e75b7-106">В этой статье рассматриваются hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="e75b7-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="e75b7-107">Настройка глобальных распространения, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="e75b7-107">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="e75b7-108">Настройка глобальных распространения, с помощью hello [интерфейсы API DocumentDB](documentdb-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="e75b7-108">Configure global distribution using hello [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a><span data-ttu-id="e75b7-109">Подключение с помощью DocumentDB API hello предпочтительную область tooa</span><span class="sxs-lookup"><span data-stu-id="e75b7-109">Connecting tooa preferred region using hello DocumentDB API</span></span>

<span data-ttu-id="e75b7-110">В порядке tootake преимуществами [глобального распространения](distribute-data-globally.md), клиентских приложений можно указать hello упорядоченный список предпочтения toobe области используется tooperform операции с документом.</span><span class="sxs-lookup"><span data-stu-id="e75b7-110">In order tootake advantage of [global distribution](distribute-data-globally.md), client applications can specify hello ordered preference list of regions toobe used tooperform document operations.</span></span> <span data-ttu-id="e75b7-111">Это можно сделать, задав политику подключений hello.</span><span class="sxs-lookup"><span data-stu-id="e75b7-111">This can be done by setting hello connection policy.</span></span> <span data-ttu-id="e75b7-112">В зависимости от конфигурации учетной записи Azure Cosmos DB hello доступности текущий язык и список предпочтения hello указана, приветствия большинство оптимальной конечная точка будет выбираемого hello tooperform SDK DocumentDB для записи и чтения операций.</span><span class="sxs-lookup"><span data-stu-id="e75b7-112">Based on hello Azure Cosmos DB account configuration, current regional availability and hello preference list specified, hello most optimal endpoint will be chosen by hello DocumentDB SDK tooperform write and read operations.</span></span>

<span data-ttu-id="e75b7-113">Этот список предпочтения указывается при инициализации подключения с помощью пакеты SDK DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="e75b7-113">This preference list is specified when initializing a connection using hello DocumentDB SDKs.</span></span> <span data-ttu-id="e75b7-114">Необязательный параметр «PreferredLocations» примите Hello пакеты SDK, упорядоченный список регионов Azure.</span><span class="sxs-lookup"><span data-stu-id="e75b7-114">hello SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="e75b7-115">пакет SDK для Hello будет автоматически отправлять все записи toohello текущей записи области.</span><span class="sxs-lookup"><span data-stu-id="e75b7-115">hello SDK will automatically send all writes toohello current write region.</span></span>

<span data-ttu-id="e75b7-116">Все операции чтения будут отправляться toohello первой доступной области в списке PreferredLocations hello.</span><span class="sxs-lookup"><span data-stu-id="e75b7-116">All reads will be sent toohello first available region in hello PreferredLocations list.</span></span> <span data-ttu-id="e75b7-117">Если hello запрос завершается неудачно, клиент hello ошибкой вниз область Далее toohello списка hello и так далее.</span><span class="sxs-lookup"><span data-stu-id="e75b7-117">If hello request fails, hello client will fail down hello list toohello next region, and so on.</span></span>

<span data-ttu-id="e75b7-118">предпринимает попытку tooread из регионов hello, указанный в PreferredLocations Hello пакеты SDK.</span><span class="sxs-lookup"><span data-stu-id="e75b7-118">hello SDKs will only attempt tooread from hello regions specified in PreferredLocations.</span></span> <span data-ttu-id="e75b7-119">Таким образом например, если hello учетной записи базы данных доступен в трех регионах, но клиент hello только задает два hello записи областей для PreferredLocations, затем никаких операций чтения будет предоставляться вне области записи hello, даже в случае hello перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="e75b7-119">So, for example, if hello Database Account is available in three regions, but hello client only specifies two of hello non-write regions for PreferredLocations, then no reads will be served out of hello write region, even in hello case of failover.</span></span>

<span data-ttu-id="e75b7-120">приложение Hello можно проверить hello текущей конечной точки записи и чтения конечная точка выбрана по hello SDK путем проверки два свойства: WriteEndpoint и ReadEndpoint, доступные в пакете SDK версии 1.8 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="e75b7-120">hello application can verify hello current write endpoint and read endpoint chosen by hello SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="e75b7-121">Если hello PreferredLocations свойство не задано, все запросы будут поступать из hello текущей записи области.</span><span class="sxs-lookup"><span data-stu-id="e75b7-121">If hello PreferredLocations property is not set, all requests will be served from hello current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="e75b7-122">ПАКЕТ SDK .NET</span><span class="sxs-lookup"><span data-stu-id="e75b7-122">.NET SDK</span></span>
<span data-ttu-id="e75b7-123">Hello SDK можно использовать без необходимости изменения кода.</span><span class="sxs-lookup"><span data-stu-id="e75b7-123">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="e75b7-124">В этом случае hello SDK автоматически направляет чтения и записи toohello текущей записи области.</span><span class="sxs-lookup"><span data-stu-id="e75b7-124">In this case, hello SDK automatically directs both reads and writes toohello current write region.</span></span>

<span data-ttu-id="e75b7-125">В версии 1.8 и более поздних версиях hello .NET SDK параметр ConnectionPolicy hello hello DocumentClient конструктор имеет свойство с именем Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="e75b7-125">In version 1.8 and later of hello .NET SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="e75b7-126">Это свойство имеет тип коллекции `<string>` и должно содержать список имен регионов.</span><span class="sxs-lookup"><span data-stu-id="e75b7-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="e75b7-127">Hello строковые значения форматируются в столбце Имя области hello на hello [регионы Azure] [ regions] страницы без пробелов до или после hello сначала и последний символ соответственно.</span><span class="sxs-lookup"><span data-stu-id="e75b7-127">hello string values are formatted per hello Region Name column on hello [Azure Regions][regions] page, with no spaces before or after hello first and last character respectively.</span></span>

<span data-ttu-id="e75b7-128">Hello текущей записи и чтения конечные точки доступны в DocumentClient.WriteEndpoint и DocumentClient.ReadEndpoint соответственно.</span><span class="sxs-lookup"><span data-stu-id="e75b7-128">hello current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="e75b7-129">Hello URL-адресов для конечных точек hello не может считаться долгоживущие константы.</span><span class="sxs-lookup"><span data-stu-id="e75b7-129">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="e75b7-130">Hello службы может обновить в любой момент.</span><span class="sxs-lookup"><span data-stu-id="e75b7-130">hello service may update these at any point.</span></span> <span data-ttu-id="e75b7-131">Это изменение автоматически обрабатывает Hello SDK.</span><span class="sxs-lookup"><span data-stu-id="e75b7-131">hello SDK handles this change automatically.</span></span>
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="e75b7-132">Пакеты SDK для NodeJS, JavaScript и Python</span><span class="sxs-lookup"><span data-stu-id="e75b7-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="e75b7-133">Hello SDK можно использовать без необходимости изменения кода.</span><span class="sxs-lookup"><span data-stu-id="e75b7-133">hello SDK can be used without any code changes.</span></span> <span data-ttu-id="e75b7-134">В этом случае приветствия SDK автоматически перенаправит считывает и записывает toohello текущей записи области.</span><span class="sxs-lookup"><span data-stu-id="e75b7-134">In this case, hello SDK will automatically direct both reads and writes toohello current write region.</span></span>

<span data-ttu-id="e75b7-135">В версии 1.8 и более поздних версий каждый пакет SDK hello ConnectionPolicy параметр конструктора DocumentClient hello новое свойство с именем DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="e75b7-135">In version 1.8 and later of each SDK, hello ConnectionPolicy parameter for hello DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="e75b7-136">Этот параметр является массивом строк, который принимает список имен регионов.</span><span class="sxs-lookup"><span data-stu-id="e75b7-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="e75b7-137">имена Hello форматируются в столбце Имя области hello в hello [регионы Azure] [ regions] страницы.</span><span class="sxs-lookup"><span data-stu-id="e75b7-137">hello names are formatted per hello Region Name column in hello [Azure Regions][regions] page.</span></span> <span data-ttu-id="e75b7-138">Можно также использовать hello предопределенные константы в объекте удобства hello AzureDocuments.Regions</span><span class="sxs-lookup"><span data-stu-id="e75b7-138">You can also use hello predefined constants in hello convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="e75b7-139">Hello текущей записи и чтения конечные точки доступны в DocumentClient.getWriteEndpoint и DocumentClient.getReadEndpoint соответственно.</span><span class="sxs-lookup"><span data-stu-id="e75b7-139">hello current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="e75b7-140">Hello URL-адресов для конечных точек hello не может считаться долгоживущие константы.</span><span class="sxs-lookup"><span data-stu-id="e75b7-140">hello URLs for hello endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="e75b7-141">Hello службы может обновить в любой момент.</span><span class="sxs-lookup"><span data-stu-id="e75b7-141">hello service may update these at any point.</span></span> <span data-ttu-id="e75b7-142">пакет SDK для Hello будет обработать это изменение автоматически.</span><span class="sxs-lookup"><span data-stu-id="e75b7-142">hello SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="e75b7-143">Ниже приведен пример кода для NodeJS и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="e75b7-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="e75b7-144">Python и Java будет следовать hello таким шаблоном.</span><span class="sxs-lookup"><span data-stu-id="e75b7-144">Python and Java will follow hello same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="e75b7-145">REST</span><span class="sxs-lookup"><span data-stu-id="e75b7-145">REST</span></span>
<span data-ttu-id="e75b7-146">После учетную запись базы данных станет доступным в нескольких регионах, клиенты могут запрашивать его доступности с помощью запроса GET для hello, следующий URI.</span><span class="sxs-lookup"><span data-stu-id="e75b7-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on hello following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="e75b7-147">Hello служба будет возвращать список областей и их соответствующие Azure Cosmos DB URI конечных точек для реплик hello.</span><span class="sxs-lookup"><span data-stu-id="e75b7-147">hello service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for hello replicas.</span></span> <span data-ttu-id="e75b7-148">Текущий регион записи Hello указывается в ответ hello.</span><span class="sxs-lookup"><span data-stu-id="e75b7-148">hello current write region will be indicated in hello response.</span></span> <span data-ttu-id="e75b7-149">Hello клиент затем может выбрать hello соответствующую конечную точку для всех последующих запросов REST API следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e75b7-149">hello client can then select hello appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="e75b7-150">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="e75b7-150">Example response</span></span>

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* <span data-ttu-id="e75b7-151">Все PUT, POST и DELETE запросы должны проходить toohello указано записи URI</span><span class="sxs-lookup"><span data-stu-id="e75b7-151">All PUT, POST and DELETE requests must go toohello indicated write URI</span></span>
* <span data-ttu-id="e75b7-152">Другие (например, запросы) запросов только для чтения и возвращает все может перейти в конечную точку tooany по выбору приветствия клиента</span><span class="sxs-lookup"><span data-stu-id="e75b7-152">All GETs and other read-only requests (for example queries) may go tooany endpoint of hello client’s choice</span></span>

<span data-ttu-id="e75b7-153">Напишите запросы только для tooread областей завершится ошибкой с кодом ошибки HTTP 403 («доступ запрещен»).</span><span class="sxs-lookup"><span data-stu-id="e75b7-153">Write requests tooread-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="e75b7-154">При изменении области hello записи после фазы начального обнаружения клиента hello, последующие записывает toohello предыдущей области записи завершится ошибкой с кодом ошибки HTTP 403 («доступ запрещен»).</span><span class="sxs-lookup"><span data-stu-id="e75b7-154">If hello write region changes after hello client’s initial discovery phase, subsequent writes toohello previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="e75b7-155">Hello клиента должен затем получить список регионов hello снова tooget hello обновленной записи область.</span><span class="sxs-lookup"><span data-stu-id="e75b7-155">hello client should then GET hello list of regions again tooget hello updated write region.</span></span>

<span data-ttu-id="e75b7-156">На этом руководство завершено.</span><span class="sxs-lookup"><span data-stu-id="e75b7-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="e75b7-157">Вы узнаете, как toomanage hello согласованности глобально реплицируемым учетной записи пользователя, считывая [уровни согласованности в базе данных Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="e75b7-157">You can learn how toomanage hello consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="e75b7-158">Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="e75b7-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e75b7-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e75b7-159">Next steps</span></span>

<span data-ttu-id="e75b7-160">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="e75b7-160">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e75b7-161">Настройка глобальных распространения, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="e75b7-161">Configure global distribution using hello Azure portal</span></span>
> * <span data-ttu-id="e75b7-162">Настройка глобальных распространения, с помощью hello интерфейсы API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="e75b7-162">Configure global distribution using hello DocumentDB APIs</span></span>

<span data-ttu-id="e75b7-163">Теперь можно перейти далее учебника toolearn toohello как toodevelop локально с помощью hello локальный эмулятор Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e75b7-163">You can now proceed toohello next tutorial toolearn how toodevelop locally using hello Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e75b7-164">Разрабатывать локально в эмуляторе hello</span><span class="sxs-lookup"><span data-stu-id="e75b7-164">Develop locally with hello emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

