---
title: "Руководство по настройке глобального распределения Azure Cosmos DB с помощью API DocumentDB | Документация Майкрософт"
description: "Сведения о настройке глобального распределения Azure Cosmos DB с помощью API DocumentDB."
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
ms.openlocfilehash: f4d8efe9814bd28bb902567a23b541bc9b5414a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-documentdb-api"></a><span data-ttu-id="2c609-104">Как настроить глобальное распределение Azure Cosmos DB с помощью API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="2c609-104">How to setup Azure Cosmos DB global distribution using the DocumentDB API</span></span>

<span data-ttu-id="2c609-105">В этой статье показано, как настроить глобальное распределение базы данных Azure Cosmos DB и подключиться к ней с помощью API DocumentDB на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="2c609-105">In this article, we show how to use the Azure portal to setup Azure Cosmos DB global distribution and then connect using the DocumentDB API.</span></span>

<span data-ttu-id="2c609-106">В этой статье рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2c609-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="2c609-107">настройка глобального распределения на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="2c609-107">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="2c609-108">настройка глобального распределения с помощью [API-интерфейсов DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2c609-108">Configure global distribution using the [DocumentDB APIs](documentdb-introduction.md)</span></span>

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-documentdb-api"></a><span data-ttu-id="2c609-109">Подключение к предпочтительному региону с помощью API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="2c609-109">Connecting to a preferred region using the DocumentDB API</span></span>

<span data-ttu-id="2c609-110">Чтобы воспользоваться преимуществами [глобального распределения](distribute-data-globally.md), клиентские приложения могут указать упорядоченный список предпочитаемых регионов, который будет использоваться для операций с документами.</span><span class="sxs-lookup"><span data-stu-id="2c609-110">In order to take advantage of [global distribution](distribute-data-globally.md), client applications can specify the ordered preference list of regions to be used to perform document operations.</span></span> <span data-ttu-id="2c609-111">Это можно сделать, настроив политику подключения.</span><span class="sxs-lookup"><span data-stu-id="2c609-111">This can be done by setting the connection policy.</span></span> <span data-ttu-id="2c609-112">Для операций записи и чтения с помощью пакета SDK для DocumentDB выбирается наиболее оптимальная конечная точка на основании текущих данных о региональной доступности и списка предпочтений, указанного в конфигурации учетной записи Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c609-112">Based on the Azure Cosmos DB account configuration, current regional availability and the preference list specified, the most optimal endpoint will be chosen by the DocumentDB SDK to perform write and read operations.</span></span>

<span data-ttu-id="2c609-113">Этот список предпочтений указывается при инициализации подключения с помощью пакетов SDK для DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2c609-113">This preference list is specified when initializing a connection using the DocumentDB SDKs.</span></span> <span data-ttu-id="2c609-114">Пакеты SDK принимают необязательный параметр PreferredLocations, представляющий собой упорядоченный список регионов Azure.</span><span class="sxs-lookup"><span data-stu-id="2c609-114">The SDKs accept an optional parameter "PreferredLocations" that is an ordered list of Azure regions.</span></span>

<span data-ttu-id="2c609-115">Пакет SDK будет автоматически отправлять все операции записи в текущий регион записи.</span><span class="sxs-lookup"><span data-stu-id="2c609-115">The SDK will automatically send all writes to the current write region.</span></span>

<span data-ttu-id="2c609-116">Все операции чтения будут отправляться в первой доступный регион из списка PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="2c609-116">All reads will be sent to the first available region in the PreferredLocations list.</span></span> <span data-ttu-id="2c609-117">Если запрос завершится неудачей, клиент перейдет к следующему региону дальше по списку и так далее.</span><span class="sxs-lookup"><span data-stu-id="2c609-117">If the request fails, the client will fail down the list to the next region, and so on.</span></span>

<span data-ttu-id="2c609-118">Пакеты SDK будут пытаться выполнять чтение данных из регионов, указанных в PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="2c609-118">The SDKs will only attempt to read from the regions specified in PreferredLocations.</span></span> <span data-ttu-id="2c609-119">Например, если учетная запись базы данных доступна в трех регионах, но клиент указывает в PreferredLocations только два региона не для записи, то операции чтения из региона записи не будут обслуживаться даже в случае отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="2c609-119">So, for example, if the Database Account is available in three regions, but the client only specifies two of the non-write regions for PreferredLocations, then no reads will be served out of the write region, even in the case of failover.</span></span>

<span data-ttu-id="2c609-120">Приложение может проверить текущие конечную точку записи и конечную точку чтения, выбранные пакетом SDK, просмотрев два свойства, WriteEndpoint и ReadEndpoint, доступные в SDK 1.8 и более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2c609-120">The application can verify the current write endpoint and read endpoint chosen by the SDK by checking two properties, WriteEndpoint and ReadEndpoint, available in SDK version 1.8 and above.</span></span>

<span data-ttu-id="2c609-121">Если свойство PreferredLocations не задано, будут обслуживаться все запросы из текущего региона записи.</span><span class="sxs-lookup"><span data-stu-id="2c609-121">If the PreferredLocations property is not set, all requests will be served from the current write region.</span></span>

## <a name="net-sdk"></a><span data-ttu-id="2c609-122">ПАКЕТ SDK .NET</span><span class="sxs-lookup"><span data-stu-id="2c609-122">.NET SDK</span></span>
<span data-ttu-id="2c609-123">Пакет SDK можно использовать без изменения кода.</span><span class="sxs-lookup"><span data-stu-id="2c609-123">The SDK can be used without any code changes.</span></span> <span data-ttu-id="2c609-124">В этом случае пакет SDK автоматически направляет операции чтения и записи в текущий регион записи.</span><span class="sxs-lookup"><span data-stu-id="2c609-124">In this case, the SDK automatically directs both reads and writes to the current write region.</span></span>

<span data-ttu-id="2c609-125">В пакете SDK для .NET 1.8 и более поздней версии параметр ConnectionPolicy конструктора DocumentClient имеет свойство Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="2c609-125">In version 1.8 and later of the .NET SDK, the ConnectionPolicy parameter for the DocumentClient constructor has a property called Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="2c609-126">Это свойство имеет тип коллекции `<string>` и должно содержать список имен регионов.</span><span class="sxs-lookup"><span data-stu-id="2c609-126">This property is of type Collection `<string>` and should contain a list of region names.</span></span> <span data-ttu-id="2c609-127">Строковые значения форматируются по столбцу "Имя региона" на странице [Регионы Azure][regions], без пробелов до или после первого и последнего знака, соответственно.</span><span class="sxs-lookup"><span data-stu-id="2c609-127">The string values are formatted per the Region Name column on the [Azure Regions][regions] page, with no spaces before or after the first and last character respectively.</span></span>

<span data-ttu-id="2c609-128">Текущие конечные точки записи и чтения доступны в DocumentClient.WriteEndpoint и DocumentClient.ReadEndpoint, соответственно.</span><span class="sxs-lookup"><span data-stu-id="2c609-128">The current write and read endpoints are available in DocumentClient.WriteEndpoint and DocumentClient.ReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="2c609-129">Не следует считать URL-адреса конечных точек долговременными константами.</span><span class="sxs-lookup"><span data-stu-id="2c609-129">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="2c609-130">Служба может обновить их в любой момент.</span><span class="sxs-lookup"><span data-stu-id="2c609-130">The service may update these at any point.</span></span> <span data-ttu-id="2c609-131">Пакет SDK обрабатывает это изменение автоматически.</span><span class="sxs-lookup"><span data-stu-id="2c609-131">The SDK handles this change automatically.</span></span>
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

// connect to DocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a><span data-ttu-id="2c609-132">Пакеты SDK для NodeJS, JavaScript и Python</span><span class="sxs-lookup"><span data-stu-id="2c609-132">NodeJS, JavaScript, and Python SDKs</span></span>
<span data-ttu-id="2c609-133">Пакет SDK можно использовать без изменения кода.</span><span class="sxs-lookup"><span data-stu-id="2c609-133">The SDK can be used without any code changes.</span></span> <span data-ttu-id="2c609-134">В этом случае пакет SDK будет автоматически направлять операции чтения и записи в текущий регион записи.</span><span class="sxs-lookup"><span data-stu-id="2c609-134">In this case, the SDK will automatically direct both reads and writes to the current write region.</span></span>

<span data-ttu-id="2c609-135">В пакете SDK 1.8 и более поздней версии параметр ConnectionPolicy конструктора DocumentClient имеет новое свойство DocumentClient.ConnectionPolicy.PreferredLocations.</span><span class="sxs-lookup"><span data-stu-id="2c609-135">In version 1.8 and later of each SDK, the ConnectionPolicy parameter for the DocumentClient constructor a new property called DocumentClient.ConnectionPolicy.PreferredLocations.</span></span> <span data-ttu-id="2c609-136">Этот параметр является массивом строк, который принимает список имен регионов.</span><span class="sxs-lookup"><span data-stu-id="2c609-136">This is parameter is an array of strings that takes a list of region names.</span></span> <span data-ttu-id="2c609-137">Имена форматируются по столбцу "Имя региона" на странице [Регионы Azure][regions].</span><span class="sxs-lookup"><span data-stu-id="2c609-137">The names are formatted per the Region Name column in the [Azure Regions][regions] page.</span></span> <span data-ttu-id="2c609-138">Можно также использовать предопределенные константы во вспомогательном объекте AzureDocuments.Regions.</span><span class="sxs-lookup"><span data-stu-id="2c609-138">You can also use the predefined constants in the convenience object AzureDocuments.Regions</span></span>

<span data-ttu-id="2c609-139">Текущие конечные точки записи и чтения доступны в DocumentClient.getWriteEndpoint и DocumentClient.getReadEndpoint, соответственно.</span><span class="sxs-lookup"><span data-stu-id="2c609-139">The current write and read endpoints are available in DocumentClient.getWriteEndpoint and DocumentClient.getReadEndpoint respectively.</span></span>

> [!NOTE]
> <span data-ttu-id="2c609-140">Не следует считать URL-адреса конечных точек долговременными константами.</span><span class="sxs-lookup"><span data-stu-id="2c609-140">The URLs for the endpoints should not be considered as long-lived constants.</span></span> <span data-ttu-id="2c609-141">Служба может обновить их в любой момент.</span><span class="sxs-lookup"><span data-stu-id="2c609-141">The service may update these at any point.</span></span> <span data-ttu-id="2c609-142">Пакет SDK обработает это изменение автоматически.</span><span class="sxs-lookup"><span data-stu-id="2c609-142">The SDK will handle this change automatically.</span></span>
>
>

<span data-ttu-id="2c609-143">Ниже приведен пример кода для NodeJS и JavaScript.</span><span class="sxs-lookup"><span data-stu-id="2c609-143">Below is a code example for NodeJS/Javascript.</span></span> <span data-ttu-id="2c609-144">В Python и Java используется тот же шаблон.</span><span class="sxs-lookup"><span data-stu-id="2c609-144">Python and Java will follow the same pattern.</span></span>

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in the following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize the connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a><span data-ttu-id="2c609-145">REST</span><span class="sxs-lookup"><span data-stu-id="2c609-145">REST</span></span>
<span data-ttu-id="2c609-146">После того, как учетная запись базы данных станет доступной в нескольких регионах, клиенты смогут запрашивать ее доступность с помощью запроса GET к следующему универсальному коду ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="2c609-146">Once a database account has been made available in multiple regions, clients can query its availability by performing a GET request on the following URI.</span></span>

    https://{databaseaccount}.documents.azure.com/

<span data-ttu-id="2c609-147">Служба вернет список регионов и соответствующих универсальных кодов ресурса (URI) конечных точек Azure Cosmos DB для реплик.</span><span class="sxs-lookup"><span data-stu-id="2c609-147">The service will return a list of regions and their corresponding Azure Cosmos DB endpoint URIs for the replicas.</span></span> <span data-ttu-id="2c609-148">В ответе будет указан текущий регион записи.</span><span class="sxs-lookup"><span data-stu-id="2c609-148">The current write region will be indicated in the response.</span></span> <span data-ttu-id="2c609-149">Затем клиент сможет выбрать подходящую конечную точку для всех последующих запросов REST API следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2c609-149">The client can then select the appropriate endpoint for all further REST API requests as follows.</span></span>

<span data-ttu-id="2c609-150">Пример ответа</span><span class="sxs-lookup"><span data-stu-id="2c609-150">Example response</span></span>

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


* <span data-ttu-id="2c609-151">Все запросы PUT, POST и DELETE должны направляться на указанный универсальный код ресурса (URI) записи.</span><span class="sxs-lookup"><span data-stu-id="2c609-151">All PUT, POST and DELETE requests must go to the indicated write URI</span></span>
* <span data-ttu-id="2c609-152">Все запросы GET и другие запросы только для чтения могут направляться к любой конечной точке на выбор клиента.</span><span class="sxs-lookup"><span data-stu-id="2c609-152">All GETs and other read-only requests (for example queries) may go to any endpoint of the client’s choice</span></span>

<span data-ttu-id="2c609-153">Запросы на запись к регионам только для чтения завершатся ошибкой HTTP с кодом 403 ("Запрещено").</span><span class="sxs-lookup"><span data-stu-id="2c609-153">Write requests to read-only regions will fail with HTTP error code 403 (“Forbidden”).</span></span>

<span data-ttu-id="2c609-154">В случае изменения региона записи после этапа начального обнаружения клиента все последующие операции записи в предыдущий регион записи завершатся ошибкой HTTP с кодом 403 ("Запрещено").</span><span class="sxs-lookup"><span data-stu-id="2c609-154">If the write region changes after the client’s initial discovery phase, subsequent writes to the previous write region will fail with HTTP error code 403 (“Forbidden”).</span></span> <span data-ttu-id="2c609-155">Клиенту следует еще раз получить список регионов (запрос GET), чтобы получить обновленный регион записи.</span><span class="sxs-lookup"><span data-stu-id="2c609-155">The client should then GET the list of regions again to get the updated write region.</span></span>

<span data-ttu-id="2c609-156">На этом руководство завершено.</span><span class="sxs-lookup"><span data-stu-id="2c609-156">That's it, that completes this tutorial.</span></span> <span data-ttu-id="2c609-157">Сведения об управлении согласованностью глобально реплицируемой учетной записи Azure Cosmos DB см. в [этой статье](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="2c609-157">You can learn how to manage the consistency of your globally replicated account by reading [Consistency levels in Azure Cosmos DB](consistency-levels.md).</span></span> <span data-ttu-id="2c609-158">Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="2c609-158">And for more information about how global database replication works in Azure Cosmos DB, see [Distribute data globally with Azure Cosmos DB](distribute-data-globally.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c609-159">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2c609-159">Next steps</span></span>

<span data-ttu-id="2c609-160">В этом руководстве вы выполнили следующее:</span><span class="sxs-lookup"><span data-stu-id="2c609-160">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c609-161">настроили глобальное распределение на портале Azure;</span><span class="sxs-lookup"><span data-stu-id="2c609-161">Configure global distribution using the Azure portal</span></span>
> * <span data-ttu-id="2c609-162">настроили глобальное распределение с помощью API-интерфейсов DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2c609-162">Configure global distribution using the DocumentDB APIs</span></span>

<span data-ttu-id="2c609-163">Перейдите к следующему руководству, чтобы узнать о разработке в локальной среде с помощью локального эмулятора Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2c609-163">You can now proceed to the next tutorial to learn how to develop locally using the Azure Cosmos DB local emulator.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2c609-164">Разработка в локальной среде с помощью эмулятора</span><span class="sxs-lookup"><span data-stu-id="2c609-164">Develop locally with the emulator</span></span>](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

