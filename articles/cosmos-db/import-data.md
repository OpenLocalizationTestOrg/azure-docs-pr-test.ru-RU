---
title: "Средство миграции базы данных для Azure Cosmos DB | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как использовать открытые средства миграции данных Azure Cosmos DB для импорта данных в Azure Cosmos DB из различных источников, включая MongoDB, SQL Server, хранилище таблиц, Amazon DynamoDB, файлы CSV и JSON. Преобразование CSV в JSON."
keywords: "csv в json, средства миграции базы данных, преобразование csv в json"
services: cosmos-db
author: andrewhoh
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: d173581d-782a-445c-98d9-5e3c49b00e25
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 23a4a82dbdb611f4da90562af936fca28da9b24d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-data-into-azure-cosmos-db-for-the-documentdb-api"></a><span data-ttu-id="d4488-105">Как импортировать данные в Azure Cosmos DB для API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="d4488-105">How to import data into Azure Cosmos DB for the DocumentDB API?</span></span>

<span data-ttu-id="d4488-106">В этом руководстве приведены инструкции по использованию Azure Cosmos DB: средства миграции данных API DocumentDB, которое может импортировать данные из разных источников, включая файлы JSON и CSV-файлы, SQL, MongoDB, Хранилище таблиц Azure, коллекции Amazon DynamoDB и API DocumentDB в Azure Cosmos DB для использования с Azure Cosmos DB и API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d4488-106">This tutorial provides instructions on using the Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and the DocumentDB API.</span></span> <span data-ttu-id="d4488-107">Средство миграции данных можно также использовать при миграции из односекционной коллекции в многосекционную для API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d4488-107">The Data Migration tool can also be used when migrating from a single partition collection to a multi-partition collection for the DocumentDB API.</span></span>

<span data-ttu-id="d4488-108">Это средство работает только при импорте данных в Azure Cosmos DB для использования с API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d4488-108">The Data Migration tool only works when importing data into Azure Cosmos DB for use with the DocumentDB API.</span></span> <span data-ttu-id="d4488-109">Импорт данных для использования с API таблицы или API Graph сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d4488-109">Importing data for use with the Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="d4488-110">Чтобы импортировать данные для использования с API MongoDB, ознакомьтесь со статьей [Перенос данных в DocumentDB с помощью mongoimport и mongorestore](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="d4488-110">To import data for use with the MongoDB API, see [Azure Cosmos DB: How to migrate data for the MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="d4488-111">В рамках этого руководства рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="d4488-111">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d4488-112">установка средства миграции данных;</span><span class="sxs-lookup"><span data-stu-id="d4488-112">Installing the Data Migration tool</span></span>
> * <span data-ttu-id="d4488-113">импорт данных из разных источников данных;</span><span class="sxs-lookup"><span data-stu-id="d4488-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="d4488-114">экспорт данных из Azure Cosmos DB в JSON.</span><span class="sxs-lookup"><span data-stu-id="d4488-114">Exporting from Azure Cosmos DB to JSON</span></span>

## <span data-ttu-id="d4488-115"><a id="Prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d4488-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="d4488-116">Перед выполнением инструкций, приведенных в этой статье, следует убедиться, что установлены следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="d4488-116">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="d4488-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="d4488-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="d4488-118"><a id="Overviewl"></a>Обзор средства миграции данных</span><span class="sxs-lookup"><span data-stu-id="d4488-118"><a id="Overviewl"></a>Overview of the Data Migration tool</span></span>
<span data-ttu-id="d4488-119">Средство миграции данных — это решение с открытым исходным кодом, которое импортирует данные в Azure Cosmos DB из различных источников, таких как:</span><span class="sxs-lookup"><span data-stu-id="d4488-119">The Data Migration tool is an open source solution that imports data to Azure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="d4488-120">файлы JSON;</span><span class="sxs-lookup"><span data-stu-id="d4488-120">JSON files</span></span>
* <span data-ttu-id="d4488-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="d4488-121">MongoDB</span></span>
* <span data-ttu-id="d4488-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4488-122">SQL Server</span></span>
* <span data-ttu-id="d4488-123">СЫМ-файлы;</span><span class="sxs-lookup"><span data-stu-id="d4488-123">CSV files</span></span>
* <span data-ttu-id="d4488-124">табличное хранилище Azure;</span><span class="sxs-lookup"><span data-stu-id="d4488-124">Azure Table storage</span></span>
* <span data-ttu-id="d4488-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="d4488-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="d4488-126">HBase</span><span class="sxs-lookup"><span data-stu-id="d4488-126">HBase</span></span>
* <span data-ttu-id="d4488-127">коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="d4488-128">Хотя средство импорта предоставляет графический интерфейс пользователя (dtui.exe), им также можно управлять из командной строки (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="d4488-128">While the import tool includes a graphical user interface (dtui.exe), it can also be driven from the command line (dt.exe).</span></span> <span data-ttu-id="d4488-129">К слову, существует параметр для вывода соответствующей команды после настройки импорта в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="d4488-129">In fact, there is an option to output the associated command after setting up an import through the UI.</span></span> <span data-ttu-id="d4488-130">Табличный источник данных (например, SQL Server или CSV-файлы) можно преобразовать так, чтобы создать иерархические связи (вложенные документы) во время импорта.</span><span class="sxs-lookup"><span data-stu-id="d4488-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="d4488-131">Читайте дальше, чтобы узнать о доступных источниках, примерах команд для импорта из каждого источника, возможных целевых объектах и просмотре результатов импорта.</span><span class="sxs-lookup"><span data-stu-id="d4488-131">Keep reading to learn more about source options, sample command lines to import from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="d4488-132"><a id="Install"></a>Установка средства миграции данных</span><span class="sxs-lookup"><span data-stu-id="d4488-132"><a id="Install"></a>Install the Data Migration tool</span></span>
<span data-ttu-id="d4488-133">Исходный код средства миграции доступен на портале GitHub в [этом репозитории](https://github.com/azure/azure-documentdb-datamigrationtool), а скомпилированная версия доступна в [Центре загрузки Майкрософт](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="d4488-133">The migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="d4488-134">Вы можете скомпилировать решение или просто скачать и извлечь скомпилированную версию в каталог по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="d4488-134">You may either compile the solution or simply download and extract the compiled version to a directory of your choice.</span></span> <span data-ttu-id="d4488-135">Затем запустите:</span><span class="sxs-lookup"><span data-stu-id="d4488-135">Then run either:</span></span>

* <span data-ttu-id="d4488-136">**Dtui.exe**— версия средства с графическим интерфейсом;</span><span class="sxs-lookup"><span data-stu-id="d4488-136">**Dtui.exe**: Graphical interface version of the tool</span></span>
* <span data-ttu-id="d4488-137">**Dt.exe**— версия средства с командной строкой.</span><span class="sxs-lookup"><span data-stu-id="d4488-137">**Dt.exe**: Command-line version of the tool</span></span>

## <a name="import-data"></a><span data-ttu-id="d4488-138">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="d4488-138">Import data</span></span>

<span data-ttu-id="d4488-139">После установки средства вы можете импортировать данные.</span><span class="sxs-lookup"><span data-stu-id="d4488-139">Once you've installed the tool, it's time to import your data.</span></span> <span data-ttu-id="d4488-140">Поддерживаются такие типы данных и виды импорта:</span><span class="sxs-lookup"><span data-stu-id="d4488-140">What kind of data do you want to import?</span></span>

* <span data-ttu-id="d4488-141">[файлы JSON](#JSON);</span><span class="sxs-lookup"><span data-stu-id="d4488-141">[JSON files](#JSON)</span></span>
* [<span data-ttu-id="d4488-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="d4488-142">MongoDB</span></span>](#MongoDB)
* <span data-ttu-id="d4488-143">[файлы экспорта MongoDB](#MongoDBExport);</span><span class="sxs-lookup"><span data-stu-id="d4488-143">[MongoDB Export files](#MongoDBExport)</span></span>
* [<span data-ttu-id="d4488-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4488-144">SQL Server</span></span>](#SQL)
* <span data-ttu-id="d4488-145">[CSV-файлы](#CSV);</span><span class="sxs-lookup"><span data-stu-id="d4488-145">[CSV files](#CSV)</span></span>
* [<span data-ttu-id="d4488-146">Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="d4488-146">Azure Table storage</span></span>](#AzureTableSource)
* <span data-ttu-id="d4488-147">[Amazon DynamoDB](#DynamoDBSource);</span><span class="sxs-lookup"><span data-stu-id="d4488-147">[Amazon DynamoDB](#DynamoDBSource)</span></span>
* [<span data-ttu-id="d4488-148">Большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="d4488-148">Blob</span></span>](#BlobImport)
* <span data-ttu-id="d4488-149">[коллекции Azure Cosmos DB](#DocumentDBSource);</span><span class="sxs-lookup"><span data-stu-id="d4488-149">[Azure Cosmos DB collections](#DocumentDBSource)</span></span>
* [<span data-ttu-id="d4488-150">HBase</span><span class="sxs-lookup"><span data-stu-id="d4488-150">HBase</span></span>](#HBaseSource)
* <span data-ttu-id="d4488-151">[массовый импорт Azure Cosmos DB](#DocumentDBBulkImport);</span><span class="sxs-lookup"><span data-stu-id="d4488-151">[Azure Cosmos DB bulk import](#DocumentDBBulkImport)</span></span>
* <span data-ttu-id="d4488-152">[последовательный импорт записей Azure Cosmos DB](#DocumentDSeqTarget).</span><span class="sxs-lookup"><span data-stu-id="d4488-152">[Azure Cosmos DB sequential record import](#DocumentDSeqTarget)</span></span>


## <span data-ttu-id="d4488-153"><a id="JSON"></a>Импорт JSON-файлов</span><span class="sxs-lookup"><span data-stu-id="d4488-153"><a id="JSON"></a>To import JSON files</span></span>
<span data-ttu-id="d4488-154">Параметр импорта файлов JSON позволяет импортировать файлы JSON с одним или несколькими документами или файлы JSON, каждый из которых содержит массив документов JSON.</span><span class="sxs-lookup"><span data-stu-id="d4488-154">The JSON file source importer option allows you to import one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="d4488-155">Во время добавления папок, содержащих JSON-файлы для импорта, вы можете выполнить рекурсивный поиск файлов во вложенных папках.</span><span class="sxs-lookup"><span data-stu-id="d4488-155">When adding folders that contain JSON files to import, you have the option of recursively searching for files in subfolders.</span></span>

![Снимок экрана: параметры исходного файла JSON — средства миграции базы данных](./media/import-data/jsonsource.png)

<span data-ttu-id="d4488-157">Ниже приведены некоторые примеры команд для импорта файлов JSON.</span><span class="sxs-lookup"><span data-stu-id="d4488-157">Here are some command line samples to import JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition the data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="d4488-158"><a id="MongoDB"></a>Импорт из MongoDB</span><span class="sxs-lookup"><span data-stu-id="d4488-158"><a id="MongoDB"></a>To import from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4488-159">При импорте в учетную запись Azure Cosmos DB с поддержкой MongoDB выполните эти [инструкции](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="d4488-159">If you are importing to an Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="d4488-160">Параметр импорта из MongoDB позволяет импортировать данные из отдельной коллекции MongoDB, фильтровать документы с помощью запроса, а также изменять структуру документа с помощью проекции.</span><span class="sxs-lookup"><span data-stu-id="d4488-160">The MongoDB source importer option allows you to import from an individual MongoDB collection and optionally filter documents using a query and/or modify the document structure by using a projection.</span></span>  

![Снимок экрана параметров источника MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="d4488-162">Строка подключения представляется в стандартном формате MongoDB:</span><span class="sxs-lookup"><span data-stu-id="d4488-162">The connection string is in the standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="d4488-163">Используйте команду Verify, чтобы проверить доступ к экземпляру MongoDB, указанному в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="d4488-163">Use the Verify command to ensure that the MongoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="d4488-164">Введите имя коллекции, из которой будут импортированы данные.</span><span class="sxs-lookup"><span data-stu-id="d4488-164">Enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="d4488-165">При необходимости можно указать или предоставить файл для запроса (например {pop: {$gt:5000}}) и проекцию (например {loc:0}) для фильтрации и обработки и импортируемых данных.</span><span class="sxs-lookup"><span data-stu-id="d4488-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) to both filter and shape the data to be imported.</span></span>

<span data-ttu-id="d4488-166">Ниже приведены некоторые примеры команд для импорта данных из MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d4488-166">Here are some command line samples to import from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match the query and exclude the loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="d4488-167"><a id="MongoDBExport"></a>Импорт файлов экспорта MongoDB</span><span class="sxs-lookup"><span data-stu-id="d4488-167"><a id="MongoDBExport"></a>To import MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4488-168">При импорте в учетную запись Azure Cosmos DB с поддержкой MongoDB выполните эти [инструкции](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="d4488-168">If you are importing to an Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="d4488-169">Параметр импорта JSON-файлов экспорта MongoDB позволяет импортировать файлы JSON, созданные с помощью служебной программы mongoexport.</span><span class="sxs-lookup"><span data-stu-id="d4488-169">The MongoDB export JSON file source importer option allows you to import one or more JSON files produced from the mongoexport utility.</span></span>  

![Снимок экрана параметров экспорта MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="d4488-171">При добавлении папок, содержащих JSON-файлы экспорта MongoDB, вы можете выполнить рекурсивный поиск файлов во вложенных папках.</span><span class="sxs-lookup"><span data-stu-id="d4488-171">When adding folders that contain MongoDB export JSON files for import, you have the option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="d4488-172">Ниже приведен пример команды для импорта данных из JSON-файлов экспорта MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d4488-172">Here is a command line sample to import from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="d4488-173"><a id="SQL"></a>Импорт из SQL Server</span><span class="sxs-lookup"><span data-stu-id="d4488-173"><a id="SQL"></a>To import from SQL Server</span></span>
<span data-ttu-id="d4488-174">Параметр импорта из источника SQL позволяет импортировать данные из отдельной базы данных SQL Server и фильтровать записи для импорта с помощью запроса.</span><span class="sxs-lookup"><span data-stu-id="d4488-174">The SQL source importer option allows you to import from an individual SQL Server database and optionally filter the records to be imported using a query.</span></span> <span data-ttu-id="d4488-175">Кроме того, можно изменить структуру документа, указав разделитель вложения (подробнее об этом чуть позже).</span><span class="sxs-lookup"><span data-stu-id="d4488-175">In addition, you can modify the document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Снимок экрана: параметры источника SQL — средства миграции базы данных](./media/import-data/sqlexportsource.png)

<span data-ttu-id="d4488-177">Формат строки подключения — это стандартный формат строки подключения SQL.</span><span class="sxs-lookup"><span data-stu-id="d4488-177">The format of the connection string is the standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="d4488-178">Используйте команду Verify, чтобы проверить доступ к экземпляру SQL Server, указанному в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="d4488-178">Use the Verify command to ensure that the SQL Server instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="d4488-179">Свойство разделителя вложения используется для создания иерархических связей (вложенных документов) во время импорта.</span><span class="sxs-lookup"><span data-stu-id="d4488-179">The nesting separator property is used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="d4488-180">Рассмотрим следующий запрос SQL:</span><span class="sxs-lookup"><span data-stu-id="d4488-180">Consider the following SQL query:</span></span>

<span data-ttu-id="d4488-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="d4488-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="d4488-182">Он возвращает следующие результаты (показаны частичные результаты):</span><span class="sxs-lookup"><span data-stu-id="d4488-182">Which returns the following (partial) results:</span></span>

![Снимок экрана: результаты запроса SQL](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="d4488-184">Обратите внимание на псевдонимы, например Address.AddressType и Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="d4488-184">Note the aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="d4488-185">Если указать разделитель вложения ".", средство импорта создает вложенные документы Address и Address.Location во время импорта.</span><span class="sxs-lookup"><span data-stu-id="d4488-185">By specifying a nesting separator of ‘.’, the import tool creates Address and Address.Location subdocuments during the import.</span></span> <span data-ttu-id="d4488-186">Ниже приведен пример полученного документа в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="d4488-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="d4488-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="d4488-188">Ниже приведены некоторые примеры команд для импорта данных из SQL Server:</span><span class="sxs-lookup"><span data-stu-id="d4488-188">Here are some command line samples to import from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="d4488-189"><a id="CSV"></a>Импорт CSV-файлов и преобразование CSV в JSON</span><span class="sxs-lookup"><span data-stu-id="d4488-189"><a id="CSV"></a>To import CSV files and convert CSV to JSON</span></span>
<span data-ttu-id="d4488-190">Параметр импорта из CSV-файла позволяет импортировать один или несколько CSV-файлов.</span><span class="sxs-lookup"><span data-stu-id="d4488-190">The CSV file source importer option enables you to import one or more CSV files.</span></span> <span data-ttu-id="d4488-191">Во время добавления папок, содержащих CSV-файлы для импорта, вы можете выполнить рекурсивный поиск файлов во вложенных папках.</span><span class="sxs-lookup"><span data-stu-id="d4488-191">When adding folders that contain CSV files for import, you have the option of recursively searching for files in subfolders.</span></span>

![Снимок экрана: параметры источника CSV — преобразование CSV в JSON](media/import-data/csvsource.png)

<span data-ttu-id="d4488-193">Как и для источника SQL, свойство разделителя вложения можно использовать для создания иерархических связей (вложенных документов) во время импорта.</span><span class="sxs-lookup"><span data-stu-id="d4488-193">Similar to the SQL source, the nesting separator property may be used to create hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="d4488-194">Рассмотрим следующую строку заголовков и строки данных CSV:</span><span class="sxs-lookup"><span data-stu-id="d4488-194">Consider the following CSV header row and data rows:</span></span>

![Снимок экрана: примеры записей CSV — преобразование CSV в JSON](./media/import-data/csvsample.png)

<span data-ttu-id="d4488-196">Обратите внимание на псевдонимы, например DomainInfo.Domain_Name и RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="d4488-196">Note the aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="d4488-197">Если указать разделитель вложения ".", средство импорта создает вложенные документы DomainInfo и RedirectInfo во время импорта.</span><span class="sxs-lookup"><span data-stu-id="d4488-197">By specifying a nesting separator of ‘.’, the import tool will create DomainInfo and RedirectInfo subdocuments during the import.</span></span> <span data-ttu-id="d4488-198">Ниже приведен пример полученного документа в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="d4488-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span><span class="sxs-lookup"><span data-stu-id="d4488-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of the United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="d4488-200">Средство импорта попытается определить сведения о типе для значений, которые не заключены в кавычки и находятся в CSV-файлах (значения, заключенные в кавычки, считаются строками).</span><span class="sxs-lookup"><span data-stu-id="d4488-200">The import tool will attempt to infer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="d4488-201">Типы определяются в таком порядке: номер, дата и время, логическое значение.</span><span class="sxs-lookup"><span data-stu-id="d4488-201">Types are identified in the following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="d4488-202">Следует отметить еще кое-что об импорте CSV-файлов.</span><span class="sxs-lookup"><span data-stu-id="d4488-202">There are two other things to note about CSV import:</span></span>

1. <span data-ttu-id="d4488-203">По умолчанию значения, не заключенные в кавычки, очищаются от табуляции и пробелов, а значения, заключенные в кавычки, остаются в нетронутом виде.</span><span class="sxs-lookup"><span data-stu-id="d4488-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="d4488-204">Вы можете переопределить это поведение, установив флажок «Обрезать значения, заключенные в кавычки» или воспользовавшись параметром командной строки /s.TrimQuoted.</span><span class="sxs-lookup"><span data-stu-id="d4488-204">This behavior can be overridden with the Trim quoted values checkbox or the /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="d4488-205">По умолчанию объект null, не заключенный в кавычки, считается значением null.</span><span class="sxs-lookup"><span data-stu-id="d4488-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="d4488-206">Вы можете переопределить это поведение (то есть сделать так, чтобы объект null, не заключенный в кавычки, считался строкой null). Для этого установите флажок «Считать объект NULL, не заключенный в кавычки, строкой» или настройте параметр командной строки /s.NoUnquotedNulls.</span><span class="sxs-lookup"><span data-stu-id="d4488-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with the Treat unquoted NULL as string checkbox or the /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="d4488-207">Далее показан пример команды для импорта CSV:</span><span class="sxs-lookup"><span data-stu-id="d4488-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="d4488-208"><a id="AzureTableSource"></a>Импорт из хранилища таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="d4488-208"><a id="AzureTableSource"></a>To import from Azure Table storage</span></span>
<span data-ttu-id="d4488-209">Параметр импорта из табличного хранилища Azure позволяет импортировать данные из отдельной таблицы хранилища Azure и фильтровать сущности таблицы для импорта при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d4488-209">The Azure Table storage source importer option allows you to import from an individual Azure Table storage table and optionally filter the table entities to be imported.</span></span> <span data-ttu-id="d4488-210">Обратите внимание, что вы не можете использовать средство миграции данных для импорта данных службы хранилища таблиц Azure в Azure Cosmos DB для использования с API таблицы.</span><span class="sxs-lookup"><span data-stu-id="d4488-210">Note that you cannot use the Data Migration tool to import Azure Table storage data into Azure Cosmos DB for use with the Table API.</span></span> <span data-ttu-id="d4488-211">Сейчас поддерживается только импорт в Azure Cosmos DB для использования с API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d4488-211">Only importing to Azure Cosmos DB for use with the DocumentDB API is supported at this time.</span></span>

![Снимок экрана: параметры источника табличного хранилища Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="d4488-213">Для строки подключения табличного хранилища Azure используется следующий формат:</span><span class="sxs-lookup"><span data-stu-id="d4488-213">The format of the Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="d4488-214">Используйте команду Verify, чтобы проверить доступ к экземпляру табличного хранилища Azure, указанному в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="d4488-214">Use the Verify command to ensure that the Azure Table storage instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="d4488-215">Введите имя таблицы Azure, из которой будут импортированы данные.</span><span class="sxs-lookup"><span data-stu-id="d4488-215">Enter the name of the Azure table from which data will be imported.</span></span> <span data-ttu-id="d4488-216">При необходимости можно указать [фильтра](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4488-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="d4488-217">Параметр импорта из табличного хранилища Azure предоставляет следующие дополнительные параметры:</span><span class="sxs-lookup"><span data-stu-id="d4488-217">The Azure Table storage source importer option has the following additional options:</span></span>

1. <span data-ttu-id="d4488-218">Включить внутренние поля</span><span class="sxs-lookup"><span data-stu-id="d4488-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="d4488-219">All — включить все внутренние поля (PartitionKey, RowKey и Timestamp)</span><span class="sxs-lookup"><span data-stu-id="d4488-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="d4488-220">None — исключить все внутренние поля</span><span class="sxs-lookup"><span data-stu-id="d4488-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="d4488-221">RowKey — включить только поле RowKey</span><span class="sxs-lookup"><span data-stu-id="d4488-221">RowKey - Only include the RowKey field</span></span>
2. <span data-ttu-id="d4488-222">Выбор столбцов</span><span class="sxs-lookup"><span data-stu-id="d4488-222">Select Columns</span></span>
   1. <span data-ttu-id="d4488-223">Фильтры табличного хранилища Azure не поддерживают проекции.</span><span class="sxs-lookup"><span data-stu-id="d4488-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="d4488-224">Если вы хотите импортировать только определенные свойства сущности таблицы Azure, их необходимо добавить в список "Выбор столбцов".</span><span class="sxs-lookup"><span data-stu-id="d4488-224">If you want to only import specific Azure Table entity properties, add them to the Select Columns list.</span></span> <span data-ttu-id="d4488-225">Все другие свойства сущностей будут игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="d4488-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="d4488-226">Ниже приведен пример команды для импорта данных из табличного хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="d4488-226">Here is a command line sample to import from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="d4488-227"><a id="DynamoDBSource"></a>Импорт из Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="d4488-227"><a id="DynamoDBSource"></a>To import from Amazon DynamoDB</span></span>
<span data-ttu-id="d4488-228">Параметр импортера источника Amazon DynamoDB позволяет выполнять импорт из отдельной таблицы Amazon DynamoDB и при необходимости фильтровать сущности для импорта.</span><span class="sxs-lookup"><span data-stu-id="d4488-228">The Amazon DynamoDB source importer option allows you to import from an individual Amazon DynamoDB table and optionally filter the entities to be imported.</span></span> <span data-ttu-id="d4488-229">Чтобы максимально упростить настройку импорта, представлено несколько шаблонов.</span><span class="sxs-lookup"><span data-stu-id="d4488-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Снимок экрана: параметры источника DynamoDB Amazon — средства миграции базы данных](./media/import-data/dynamodbsource1.png)

![Снимок экрана: параметры источника DynamoDB Amazon — средства миграции базы данных](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="d4488-232">Формат строки подключения Amazon DynamoDB выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d4488-232">The format of the Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="d4488-233">Используйте команду Verify, чтобы проверить доступ к экземпляру Amazon DynamoDB, указанному в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="d4488-233">Use the Verify command to ensure that the Amazon DynamoDB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="d4488-234">Ниже приведен пример команды для импорта данных из Amazon DynamoDB:</span><span class="sxs-lookup"><span data-stu-id="d4488-234">Here is a command line sample to import from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="d4488-235"><a id="BlobImport"></a>Импорт файлов из хранилища BLOB-объектов Azure</span><span class="sxs-lookup"><span data-stu-id="d4488-235"><a id="BlobImport"></a>To import files from Azure Blob storage</span></span>
<span data-ttu-id="d4488-236">JSON-файл, файл экспорта MongoDB и параметры импорта источника файла CSV позволяют импортировать из хранилища больших двоичных объектов Azure один или несколько файлов.</span><span class="sxs-lookup"><span data-stu-id="d4488-236">The JSON file, MongoDB export file, and CSV file source importer options allow you to import one or more files from Azure Blob storage.</span></span> <span data-ttu-id="d4488-237">Чтобы выбрать файлы для импорта, просто предоставьте регулярное выражение после указания URL-адреса или ключа учетной записи для контейнера больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="d4488-237">After specifying a Blob container URL and Account Key, simply provide a regular expression to select the file(s) to import.</span></span>

![Снимок экрана: параметры исходного файла больших двоичных объектов](./media/import-data/blobsource.png)

<span data-ttu-id="d4488-239">Ниже приведен пример команды для импорта JSON-файлов из хранилища больших двоичных объектов Azure:</span><span class="sxs-lookup"><span data-stu-id="d4488-239">Here is command line sample to import JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="d4488-240"><a id="DocumentDBSource"></a>Импорт из коллекции API Azure DocumentDB в Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d4488-240"><a id="DocumentDBSource"></a>To import from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="d4488-241">Параметр импортера источников Azure Cosmos DB позволяет импортировать данные из коллекций Azure Cosmos DB и, если нужно, фильтровать документы с помощью запроса.</span><span class="sxs-lookup"><span data-stu-id="d4488-241">The Azure Cosmos DB source importer option allows you to import data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Снимок экрана: параметры источника Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="d4488-243">Для строки подключения Azure Cosmos DB используется следующий формат:</span><span class="sxs-lookup"><span data-stu-id="d4488-243">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="d4488-244">Строку подключения учетной записи Azure Cosmos DB можно получить из колонки "Ключи" на портале Azure, как описано в статье об [управлении учетной записью Azure Cosmos DB](manage-account.md), однако в строку подключения необходимо добавить имя базы данных в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="d4488-244">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="d4488-245">Используйте команду Verify, чтобы проверить доступ к экземпляру Azure Cosmos DB, указанному в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="d4488-245">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="d4488-246">Чтобы импортировать данные из одной коллекции Azure Cosmos DB, введите ее имя.</span><span class="sxs-lookup"><span data-stu-id="d4488-246">To import from a single Azure Cosmos DB collection, enter the name of the collection from which data will be imported.</span></span> <span data-ttu-id="d4488-247">Чтобы выполнить импорт из нескольких коллекций Azure Cosmos DB, введите регулярное выражение, соответствующее имени одной коллекции либо именам нескольких (например, collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="d4488-247">To import from multiple Azure Cosmos DB collections, provide a regular expression to match one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="d4488-248">При необходимости можно указать или предоставить файл для запроса для фильтрации и обработки и импортируемых данных.</span><span class="sxs-lookup"><span data-stu-id="d4488-248">You may optionally specify, or provide a file for, a query to both filter and shape the data to be imported.</span></span>

> [!NOTE]
> <span data-ttu-id="d4488-249">Так как в поле коллекции можно вводить регулярные выражения, то, если вы импортируете данные из одной коллекции, имя которой содержит символы регулярного выражения, их нужно экранировать соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="d4488-249">Since the collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="d4488-250">Параметр импорта Azure Cosmos DB предоставляет следующие дополнительные параметры:</span><span class="sxs-lookup"><span data-stu-id="d4488-250">The Azure Cosmos DB source importer option has the following advanced options:</span></span>

1. <span data-ttu-id="d4488-251">Include Internal Fields (Включить внутренние поля). Указывает, следует ли включать системные свойства документа Azure Cosmos DB в экспорт (например, _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="d4488-251">Include Internal Fields: Specifies whether or not to include Azure Cosmos DB document system properties in the export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="d4488-252">Number of Retries on Failure (Число повторных попыток в случае сбоя). Указывает количество повторных попыток подключения к Azure Cosmos DB при временном сбое (например, прерывания сетевого подключения).</span><span class="sxs-lookup"><span data-stu-id="d4488-252">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="d4488-253">Retry Interval (Интервал повтора). Указывает время ожидания между повторными попытками подключения к Azure Cosmos DB при временном сбое (например, прерывания сетевого подключения).</span><span class="sxs-lookup"><span data-stu-id="d4488-253">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="d4488-254">Connection Mode (Режим подключения). Указывает режим подключения для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-254">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="d4488-255">Доступны варианты: DirectTcp, DirectHttps и Gateway.</span><span class="sxs-lookup"><span data-stu-id="d4488-255">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="d4488-256">Режимы прямого подключения быстрее, а режим шлюза более удобен для брандмауэра, так как использует только порт 443.</span><span class="sxs-lookup"><span data-stu-id="d4488-256">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Снимок экрана: дополнительные параметры источника Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="d4488-258">Средство импорта по умолчанию использует режим подключения DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="d4488-258">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="d4488-259">При возникновении проблем с брандмауэром перейдите на режим шлюза, так как он использует только порт 443.</span><span class="sxs-lookup"><span data-stu-id="d4488-259">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="d4488-260">Ниже приведены некоторые примеры команд для импорта данных из Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-260">Here are some command line samples to import from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection to another Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections to a single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection to a JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="d4488-261">Средство импорта данных Azure Cosmos DB также поддерживает импорт данных из [эмулятора Azure Cosmos DB](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="d4488-261">The Azure Cosmos DB Data Import Tool also supports import of data from the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="d4488-262">При импорте данных из локального эмулятора задайте следующую конечную точку: `https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="d4488-262">When importing data from a local emulator, set the endpoint to `https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="d4488-263"><a id="HBaseSource"></a>Импорт из HBase</span><span class="sxs-lookup"><span data-stu-id="d4488-263"><a id="HBaseSource"></a>To import from HBase</span></span>
<span data-ttu-id="d4488-264">Параметр импортера источника HBase позволяет импортировать данные из таблицы HBase и фильтровать данные при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d4488-264">The HBase source importer option allows you to import data from an HBase table and optionally filter the data.</span></span> <span data-ttu-id="d4488-265">Чтобы максимально упростить настройку импорта, представлено несколько шаблонов.</span><span class="sxs-lookup"><span data-stu-id="d4488-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Снимок экрана: параметры источника HBase](./media/import-data/hbasesource1.png)

![Снимок экрана: параметры источника HBase](./media/import-data/hbasesource2.png)

<span data-ttu-id="d4488-268">Формат строки подключения HBase Stargate выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d4488-268">The format of the HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="d4488-269">Используйте команду Verify, чтобы проверить доступ к экземпляру HBase, указанному в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="d4488-269">Use the Verify command to ensure that the HBase instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="d4488-270">Ниже приведен пример команды для импорта данных из HBase:</span><span class="sxs-lookup"><span data-stu-id="d4488-270">Here is a command line sample to import from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="d4488-271"><a id="DocumentDBBulkTarget"></a>Импорта в API DocumentDB (массовый импорт)</span><span class="sxs-lookup"><span data-stu-id="d4488-271"><a id="DocumentDBBulkTarget"></a>To import to the DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="d4488-272">Средство массового импорта Azure Cosmos DB позволяет импортировать данные из любого доступного источника, используя хранимую процедуру Azure Cosmos DB для повышения эффективности.</span><span class="sxs-lookup"><span data-stu-id="d4488-272">The Azure Cosmos DB Bulk importer allows you to import from any of the available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="d4488-273">Это средство поддерживает импорт в односекционную коллекцию Azure Cosmos DB, а также сегментированный импорт, в рамках которого данные распределяются по нескольким односекционным коллекциям Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-273">The tool supports import to one single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="d4488-274">Дополнительные сведения о секционировании данных см. в статье о [секционировании и масштабировании в Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="d4488-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="d4488-275">Кроме того, это средство создает, выполняет и удаляет хранимые процедуры из целевых коллекций.</span><span class="sxs-lookup"><span data-stu-id="d4488-275">The tool will create, execute, and then delete the stored procedure from the target collection(s).</span></span>  

![Снимок экрана: параметры массового импорта Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="d4488-277">Для строки подключения Azure Cosmos DB используется следующий формат:</span><span class="sxs-lookup"><span data-stu-id="d4488-277">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="d4488-278">Строку подключения учетной записи Azure Cosmos DB можно получить из колонки "Ключи" на портале Azure, как описано в статье об [управлении учетной записью Azure Cosmos DB](manage-account.md), однако в строку подключения необходимо добавить имя базы данных в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="d4488-278">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="d4488-279">Используйте команду Verify, чтобы проверить доступ к экземпляру Azure Cosmos DB, указанному в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="d4488-279">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="d4488-280">Чтобы импортировать данные в одну коллекцию, укажите имя этой коллекции и нажмите кнопку «Добавить».</span><span class="sxs-lookup"><span data-stu-id="d4488-280">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="d4488-281">Чтобы импортировать данные в несколько коллекций, укажите имя каждой коллекции отдельно или, чтобы указать несколько коллекций, воспользуйтесь таким синтаксисом: *префикс_коллекции*[начальный индекс - конечный индекс].</span><span class="sxs-lookup"><span data-stu-id="d4488-281">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="d4488-282">Когда вы указываете несколько коллекций с помощью приведенного выше синтаксиса, учитывайте следующие факторы.</span><span class="sxs-lookup"><span data-stu-id="d4488-282">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="d4488-283">Поддерживаются только шаблоны имени диапазона целых чисел.</span><span class="sxs-lookup"><span data-stu-id="d4488-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="d4488-284">Например, если указать [0–3], будут указаны такие коллекции: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="d4488-284">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="d4488-285">Вы можете использовать сокращенный синтаксис: если ввести collection[3], будет отображен тот же набор коллекций, что и на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="d4488-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="d4488-286">Вы можете указать несколько подстановок.</span><span class="sxs-lookup"><span data-stu-id="d4488-286">More than one substitution can be provided.</span></span> <span data-ttu-id="d4488-287">Например, коллекция [0–1] [0–9] создаст 20 имен коллекций с нулем в начале (collection01… 02… 03).</span><span class="sxs-lookup"><span data-stu-id="d4488-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="d4488-288">Указав имена коллекций, выберите нужную пропускную способность коллекций (от 400 до 10 000 ЕЗ).</span><span class="sxs-lookup"><span data-stu-id="d4488-288">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 10,000 RUs).</span></span> <span data-ttu-id="d4488-289">Для повышения производительности выберите большее значение.</span><span class="sxs-lookup"><span data-stu-id="d4488-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="d4488-290">Дополнительные сведения об уровнях производительности в Azure Cosmos DB см. в [этой статье](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d4488-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d4488-291">Параметр пропускной способности применяется только для создания коллекции.</span><span class="sxs-lookup"><span data-stu-id="d4488-291">The performance throughput setting only applies to collection creation.</span></span> <span data-ttu-id="d4488-292">Если указанная коллекция уже существует, ее пропускная способность не будет изменена.</span><span class="sxs-lookup"><span data-stu-id="d4488-292">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="d4488-293">Если нужно импортировать данные в несколько коллекций, средство импорта поддерживает сегментирование на основе хэша.</span><span class="sxs-lookup"><span data-stu-id="d4488-293">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="d4488-294">Укажите в этом сценарии свойство документа, которое нужно использовать в качестве ключа секции (если не указать ключ секции, сегментирование документов по целевым коллекциям будет происходить произвольным образом).</span><span class="sxs-lookup"><span data-stu-id="d4488-294">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="d4488-295">При необходимости можно указать, какое поле источника импорта следует использовать в качестве свойства идентификатора документа Azure Cosmos DB во время импорта (обратите внимание, что если документы не содержат это свойство, средство импорта создаст GUID для свойства идентификатора).</span><span class="sxs-lookup"><span data-stu-id="d4488-295">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="d4488-296">Во время импорта доступны ряд дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="d4488-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="d4488-297">Во-первых, хотя средство и предоставляет хранимую процедуру массового импорта по умолчанию (BulkInsert.js), вы можете указать собственную хранимую процедуру:</span><span class="sxs-lookup"><span data-stu-id="d4488-297">First, while the tool includes a default bulk import stored procedure (BulkInsert.js), you may choose to specify your own import stored procedure:</span></span>

 ![Снимок экрана: параметр хранимой процедуры массового импорта Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="d4488-299">Кроме того, при импорте типов даты (например, из SQL Server или MongoDB) можно выбрать три параметра импорта:</span><span class="sxs-lookup"><span data-stu-id="d4488-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Снимок экрана: параметры импорта даты и времени импорта Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="d4488-301">Строка: сохраняется как строковое значение.</span><span class="sxs-lookup"><span data-stu-id="d4488-301">String: Persist as a string value</span></span>
* <span data-ttu-id="d4488-302">Эпоха: сохраняется как век числовое значение эпохи.</span><span class="sxs-lookup"><span data-stu-id="d4488-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="d4488-303">Оба: сохраняются строковое значение и числовое значение эпохи.</span><span class="sxs-lookup"><span data-stu-id="d4488-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="d4488-304">Этот параметр создает вложенный документ, например "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="d4488-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="d4488-305">Средство массового импорта Azure Cosmos DB предоставляет следующие дополнительные параметры:</span><span class="sxs-lookup"><span data-stu-id="d4488-305">The Azure Cosmos DB Bulk importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="d4488-306">"Размер пакета": по умолчанию средство использует размер пакета 50.</span><span class="sxs-lookup"><span data-stu-id="d4488-306">Batch Size: The tool defaults to a batch size of 50.</span></span>  <span data-ttu-id="d4488-307">При импорте больших документов рекомендуется уменьшить размер пакета.</span><span class="sxs-lookup"><span data-stu-id="d4488-307">If the documents to be imported are large, consider lowering the batch size.</span></span> <span data-ttu-id="d4488-308">И наоборот, при импорте небольших документов рекомендуется увеличить размер пакета.</span><span class="sxs-lookup"><span data-stu-id="d4488-308">Conversely, if the documents to be imported are small, consider raising the batch size.</span></span>
2. <span data-ttu-id="d4488-309">"Максимальный размер скрипта (в байтах)": по умолчанию средство использует максимальный размер скрипта, равный 512 КБ.</span><span class="sxs-lookup"><span data-stu-id="d4488-309">Max Script Size (bytes): The tool defaults to a max script size of 512KB</span></span>
3. <span data-ttu-id="d4488-310">"Отключить автоматическое создание идентификатора": если каждый импортируемый документ содержит поле идентификатора, то выбор этого параметра может повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="d4488-310">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="d4488-311">Документы без поля уникального идентификатора не будут импортированы.</span><span class="sxs-lookup"><span data-stu-id="d4488-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="d4488-312">"Обновление существующих документов": по умолчанию средство не заменяет существующие документы с конфликтами идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="d4488-312">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="d4488-313">При выборе этого параметра существующие документы с совпадающими идентификаторами будут перезаписываться.</span><span class="sxs-lookup"><span data-stu-id="d4488-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="d4488-314">Эта функция пригодится для плановых миграций, которые используются для обновления существующих документов.</span><span class="sxs-lookup"><span data-stu-id="d4488-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="d4488-315">Number of Retries on Failure (Число повторных попыток в случае сбоя). Указывает количество повторных попыток подключения к Azure Cosmos DB при временном сбое (например, прерывания сетевого подключения).</span><span class="sxs-lookup"><span data-stu-id="d4488-315">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="d4488-316">Retry Interval (Интервал повтора). Указывает время ожидания между повторными попытками подключения к Azure Cosmos DB при временном сбое (например, прерывания сетевого подключения).</span><span class="sxs-lookup"><span data-stu-id="d4488-316">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="d4488-317">Connection Mode (Режим подключения). Указывает режим подключения для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-317">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="d4488-318">Доступны варианты: DirectTcp, DirectHttps и Gateway.</span><span class="sxs-lookup"><span data-stu-id="d4488-318">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="d4488-319">Режимы прямого подключения быстрее, а режим шлюза более удобен для брандмауэра, так как использует только порт 443.</span><span class="sxs-lookup"><span data-stu-id="d4488-319">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Снимок экрана: дополнительные параметры массового импорта Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="d4488-321">Средство импорта по умолчанию использует режим подключения DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="d4488-321">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="d4488-322">При возникновении проблем с брандмауэром перейдите на режим шлюза, так как он использует только порт 443.</span><span class="sxs-lookup"><span data-stu-id="d4488-322">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="d4488-323"><a id="DocumentDBSeqTarget"></a>Импорт в API DocumentDB (последовательный импорт записей)</span><span class="sxs-lookup"><span data-stu-id="d4488-323"><a id="DocumentDBSeqTarget"></a>To import to the DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="d4488-324">Средство последовательного импорта записей Azure Cosmos DB позволяет импортировать данные из любых доступных источников по одной записи.</span><span class="sxs-lookup"><span data-stu-id="d4488-324">The Azure Cosmos DB sequential record importer allows you to import from any of the available source options on a record by record basis.</span></span> <span data-ttu-id="d4488-325">Этот параметр можно выбрать при импорте в существующую коллекцию, для которой достигнута квота хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="d4488-325">You might choose this option if you’re importing to an existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="d4488-326">Это средство поддерживает импорт в отдельную (односекционную или многосекционную) коллекцию Azure Cosmos DB, а также сегментированный импорт, в рамках которого данные распределяются по нескольким односекционным и (или) многосекционным коллекциям Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-326">The tool supports import to a single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="d4488-327">Дополнительные сведения о секционировании данных см. в статье о [секционировании и масштабировании в Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="d4488-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Снимок экрана: параметры последовательного импорта записей Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="d4488-329">Для строки подключения Azure Cosmos DB используется следующий формат:</span><span class="sxs-lookup"><span data-stu-id="d4488-329">The format of the Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="d4488-330">Строку подключения учетной записи Azure Cosmos DB можно получить из колонки "Ключи" на портале Azure, как описано в статье об [управлении учетной записью Azure Cosmos DB](manage-account.md), однако в строку подключения необходимо добавить имя базы данных в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="d4488-330">The Azure Cosmos DB account connection string can be retrieved from the Keys blade of the Azure portal, as described in [How to manage an Azure Cosmos DB account](manage-account.md), however the name of the database needs to be appended to the connection string in the following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="d4488-331">Используйте команду Verify, чтобы проверить доступ к экземпляру Azure Cosmos DB, указанному в строке подключения.</span><span class="sxs-lookup"><span data-stu-id="d4488-331">Use the Verify command to ensure that the Azure Cosmos DB instance specified in the connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="d4488-332">Чтобы импортировать данные в одну коллекцию, укажите имя этой коллекции и нажмите кнопку «Добавить».</span><span class="sxs-lookup"><span data-stu-id="d4488-332">To import to a single collection, enter the name of the collection to which data will be imported and click the Add button.</span></span> <span data-ttu-id="d4488-333">Чтобы импортировать данные в несколько коллекций, укажите имя каждой коллекции отдельно или, чтобы указать несколько коллекций, воспользуйтесь таким синтаксисом: *префикс_коллекции*[начальный индекс - конечный индекс].</span><span class="sxs-lookup"><span data-stu-id="d4488-333">To import to multiple collections, either enter each collection name individually or use the following syntax to specify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="d4488-334">Когда вы указываете несколько коллекций с помощью приведенного выше синтаксиса, учитывайте следующие факторы.</span><span class="sxs-lookup"><span data-stu-id="d4488-334">When specifying multiple collections via the aforementioned syntax, keep the following in mind:</span></span>

1. <span data-ttu-id="d4488-335">Поддерживаются только шаблоны имени диапазона целых чисел.</span><span class="sxs-lookup"><span data-stu-id="d4488-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="d4488-336">Например, если указать [0–3], будут указаны такие коллекции: collection0, collection1, collection2, collection3.</span><span class="sxs-lookup"><span data-stu-id="d4488-336">For example, specifying collection[0-3] will produce the following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="d4488-337">Вы можете использовать сокращенный синтаксис: если ввести collection[3], будет отображен тот же набор коллекций, что и на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="d4488-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="d4488-338">Вы можете указать несколько подстановок.</span><span class="sxs-lookup"><span data-stu-id="d4488-338">More than one substitution can be provided.</span></span> <span data-ttu-id="d4488-339">Например, коллекция [0–1] [0–9] создаст 20 имен коллекций с нулем в начале (collection01… 02… 03).</span><span class="sxs-lookup"><span data-stu-id="d4488-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="d4488-340">Указав имена коллекций, выберите нужную пропускную способность коллекций (от 400 до 250 000 ЕЗ).</span><span class="sxs-lookup"><span data-stu-id="d4488-340">Once the collection name(s) have been specified, choose the desired throughput of the collection(s) (400 RUs to 250,000 RUs).</span></span> <span data-ttu-id="d4488-341">Для повышения производительности выберите большее значение.</span><span class="sxs-lookup"><span data-stu-id="d4488-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="d4488-342">Дополнительные сведения об уровнях производительности в Azure Cosmos DB см. в [этой статье](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="d4488-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="d4488-343">Для любой операции импорта в коллекции с пропускной способностью выше 10 000 ЕЗ потребуется ключ секции.</span><span class="sxs-lookup"><span data-stu-id="d4488-343">Any import to collections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="d4488-344">Если требуется пропускная способность более 250 000 ЕЗ, вам потребуется отправить запрос на портале, чтобы увеличить ограничения учетной записи.</span><span class="sxs-lookup"><span data-stu-id="d4488-344">If you choose to have more than 250,000 RUs, you will need to file a request in the portal to have your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="d4488-345">Параметр пропускной способности применяется только для создания коллекции.</span><span class="sxs-lookup"><span data-stu-id="d4488-345">The throughput setting only applies to collection creation.</span></span> <span data-ttu-id="d4488-346">Если указанная коллекция уже существует, ее пропускная способность не будет изменена.</span><span class="sxs-lookup"><span data-stu-id="d4488-346">If the specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="d4488-347">Если нужно импортировать данные в несколько коллекций, средство импорта поддерживает сегментирование на основе хэша.</span><span class="sxs-lookup"><span data-stu-id="d4488-347">When importing to multiple collections, the import tool supports hash based sharding.</span></span> <span data-ttu-id="d4488-348">Укажите в этом сценарии свойство документа, которое нужно использовать в качестве ключа секции (если не указать ключ секции, сегментирование документов по целевым коллекциям будет происходить произвольным образом).</span><span class="sxs-lookup"><span data-stu-id="d4488-348">In this scenario, specify the document property you wish to use as the Partition Key (if Partition Key is left blank, documents will be sharded randomly across the target collections).</span></span>

<span data-ttu-id="d4488-349">При необходимости можно указать, какое поле источника импорта следует использовать в качестве свойства идентификатора документа Azure Cosmos DB во время импорта (обратите внимание, что если документы не содержат это свойство, средство импорта создаст GUID для свойства идентификатора).</span><span class="sxs-lookup"><span data-stu-id="d4488-349">You may optionally specify which field in the import source should be used as the Azure Cosmos DB document id property during the import (note that if documents do not contain this property, then the import tool will generate a GUID as the id property value).</span></span>

<span data-ttu-id="d4488-350">Во время импорта доступны ряд дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="d4488-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="d4488-351">При импорте типов даты (например, из SQL Server или MongoDB) можно выбрать три параметра импорта:</span><span class="sxs-lookup"><span data-stu-id="d4488-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Снимок экрана: параметры импорта даты и времени импорта Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="d4488-353">Строка: сохраняется как строковое значение.</span><span class="sxs-lookup"><span data-stu-id="d4488-353">String: Persist as a string value</span></span>
* <span data-ttu-id="d4488-354">Эпоха: сохраняется как век числовое значение эпохи.</span><span class="sxs-lookup"><span data-stu-id="d4488-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="d4488-355">Оба: сохраняются строковое значение и числовое значение эпохи.</span><span class="sxs-lookup"><span data-stu-id="d4488-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="d4488-356">Этот параметр создает вложенный документ, например "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="d4488-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="d4488-357">Средство последовательного импорта записей Azure Cosmos DB предоставляет следующие дополнительные параметры:</span><span class="sxs-lookup"><span data-stu-id="d4488-357">The Azure Cosmos DB - Sequential record importer has the following additional advanced options:</span></span>

1. <span data-ttu-id="d4488-358">"Количество параллельных запросов": по умолчанию средство использует 2 параллельных запроса.</span><span class="sxs-lookup"><span data-stu-id="d4488-358">Number of Parallel Requests: The tool defaults to 2 parallel requests.</span></span> <span data-ttu-id="d4488-359">При импорте небольших документов рекомендуется увеличить число параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="d4488-359">If the documents to be imported are small, consider raising the number of parallel requests.</span></span> <span data-ttu-id="d4488-360">Обратите внимание, что если задать слишком большое число, производительность импорта может снизиться.</span><span class="sxs-lookup"><span data-stu-id="d4488-360">Note that if this number is raised too much, the import may experience throttling.</span></span>
2. <span data-ttu-id="d4488-361">"Отключить автоматическое создание идентификатора": если каждый импортируемый документ содержит поле идентификатора, то выбор этого параметра может повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="d4488-361">Disable Automatic Id Generation: If every document to be imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="d4488-362">Документы без поля уникального идентификатора не будут импортированы.</span><span class="sxs-lookup"><span data-stu-id="d4488-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="d4488-363">"Обновление существующих документов": по умолчанию средство не заменяет существующие документы с конфликтами идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="d4488-363">Update Existing Documents: The tool defaults to not replacing existing documents with id conflicts.</span></span> <span data-ttu-id="d4488-364">При выборе этого параметра существующие документы с совпадающими идентификаторами будут перезаписываться.</span><span class="sxs-lookup"><span data-stu-id="d4488-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="d4488-365">Эта функция пригодится для плановых миграций, которые используются для обновления существующих документов.</span><span class="sxs-lookup"><span data-stu-id="d4488-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="d4488-366">Number of Retries on Failure (Число повторных попыток в случае сбоя). Указывает количество повторных попыток подключения к Azure Cosmos DB при временном сбое (например, прерывания сетевого подключения).</span><span class="sxs-lookup"><span data-stu-id="d4488-366">Number of Retries on Failure: Specifies the number of times to retry the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="d4488-367">Retry Interval (Интервал повтора). Указывает время ожидания между повторными попытками подключения к Azure Cosmos DB при временном сбое (например, прерывания сетевого подключения).</span><span class="sxs-lookup"><span data-stu-id="d4488-367">Retry Interval: Specifies how long to wait between retrying the connection to Azure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="d4488-368">Connection Mode (Режим подключения). Указывает режим подключения для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-368">Connection Mode: Specifies the connection mode to use with Azure Cosmos DB.</span></span> <span data-ttu-id="d4488-369">Доступны варианты: DirectTcp, DirectHttps и Gateway.</span><span class="sxs-lookup"><span data-stu-id="d4488-369">The available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="d4488-370">Режимы прямого подключения быстрее, а режим шлюза более удобен для брандмауэра, так как использует только порт 443.</span><span class="sxs-lookup"><span data-stu-id="d4488-370">The direct connection modes are faster, while the gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Снимок экрана: дополнительные параметры последовательного импорта записей Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="d4488-372">Средство импорта по умолчанию использует режим подключения DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="d4488-372">The import tool defaults to connection mode DirectTcp.</span></span> <span data-ttu-id="d4488-373">При возникновении проблем с брандмауэром перейдите на режим шлюза, так как он использует только порт 443.</span><span class="sxs-lookup"><span data-stu-id="d4488-373">If you experience firewall issues, switch to connection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="d4488-374"><a id="IndexingPolicy"></a>Указание политики индексирования при создании коллекций Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d4488-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="d4488-375">Если вы разрешили средству миграции создавать коллекции во время импорта, можно указать политику индексирования коллекций.</span><span class="sxs-lookup"><span data-stu-id="d4488-375">When you allow the migration tool to create collections during import, you can specify the indexing policy of the collections.</span></span> <span data-ttu-id="d4488-376">В разделе дополнительных параметров массового импорта Azure Cosmos DB и параметров последовательной записи Azure Cosmos DB перейдите в раздел "Политика индексации".</span><span class="sxs-lookup"><span data-stu-id="d4488-376">In the advanced options section of the Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate to the Indexing Policy section.</span></span>

![Снимок экрана: дополнительные параметры политики индексации Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="d4488-378">С помощью дополнительного параметра политики индексации можно выбрать файл политики индексации, вручную ввести политику индексации или выбрать из набора шаблонов по умолчанию (щелкнув правой кнопкой в текстовом поле политики индексации).</span><span class="sxs-lookup"><span data-stu-id="d4488-378">Using the Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in the indexing policy textbox).</span></span>

<span data-ttu-id="d4488-379">Шаблоны политик, предоставляемые средством:</span><span class="sxs-lookup"><span data-stu-id="d4488-379">The policy templates the tool provides are:</span></span>

* <span data-ttu-id="d4488-380">По умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d4488-380">Default.</span></span> <span data-ttu-id="d4488-381">Эта политика лучше всего подходит при выполнении запросов равенства строк и использовании предложения ORDER BY, диапазона и запросов равенства для чисел.</span><span class="sxs-lookup"><span data-stu-id="d4488-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="d4488-382">Эта политика имеет более низкий индекс служебных данных хранилища, чем "Диапазон".</span><span class="sxs-lookup"><span data-stu-id="d4488-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="d4488-383">Диапазон.</span><span class="sxs-lookup"><span data-stu-id="d4488-383">Range.</span></span> <span data-ttu-id="d4488-384">Эта политика лучше всего подходит при использовании предложения ORDER BY, диапазона и запросов равенства на числах и строках.</span><span class="sxs-lookup"><span data-stu-id="d4488-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="d4488-385">Эта политика имеет более высокий индекс служебных данных хранилища, чем "По умолчанию" или "Хэш".</span><span class="sxs-lookup"><span data-stu-id="d4488-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Снимок экрана: дополнительные параметры политики индексации Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="d4488-387">Если не указать политику индексации, будет применена политика по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="d4488-387">If you do not specify an indexing policy, then the default policy will be applied.</span></span> <span data-ttu-id="d4488-388">Дополнительные сведения о политиках индексации Azure Cosmos DB см. в [этой статье](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d4488-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-to-json-file"></a><span data-ttu-id="d4488-389">Экспорт в файл JSON</span><span class="sxs-lookup"><span data-stu-id="d4488-389">Export to JSON file</span></span>
<span data-ttu-id="d4488-390">Средство экспорта JSON Azure Cosmos DB позволяет экспортировать любые доступные источники в JSON-файл, содержащий массив документов JSON.</span><span class="sxs-lookup"><span data-stu-id="d4488-390">The Azure Cosmos DB JSON exporter allows you to export any of the available source options to a JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="d4488-391">Средство автоматически выполняет экспорт или же вы можете просмотреть результирующую команду миграции и выполнить ее самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="d4488-391">The tool will handle the export for you, or you can choose to view the resulting migration command and run the command yourself.</span></span> <span data-ttu-id="d4488-392">Результирующий JSON-файл может храниться локально или в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="d4488-392">The resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Снимок экрана: параметры экспорта в локальный файл Azure Cosmos DB JSON](./media/import-data/jsontarget.png)

![Снимок экрана: параметр экспорта в хранилище BLOB-объектов Azure Cosmos DB JSON](./media/import-data/jsontarget2.png)

<span data-ttu-id="d4488-395">При необходимости можно настроить результирующий JSON, что приведет к увеличению размера полученного документа, но при этом содержимое станет более удобным для чтения.</span><span class="sxs-lookup"><span data-stu-id="d4488-395">You may optionally choose to prettify the resulting JSON, which will increase the size of the resulting document while making the contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places to see in Paris"}]}]

    Prettified JSON export
    [
     {
    "id": "Sample",
    "Title": "About Paris",
    "Language": {
      "Name": "English"
    },
    "Author": {
      "Name": "Don",
      "Location": {
        "City": "Paris",
        "Country": "France"
      }
    },
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by the JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places to see in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="d4488-396">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="d4488-396">Advanced configuration</span></span>
<span data-ttu-id="d4488-397">На экране расширенной конфигурации укажите расположение файла журнала, в который нужно записывать сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="d4488-397">In the Advanced configuration screen, specify the location of the log file to which you would like any errors written.</span></span> <span data-ttu-id="d4488-398">К этой странице применяются такие правила.</span><span class="sxs-lookup"><span data-stu-id="d4488-398">The following rules apply to this page:</span></span>

1. <span data-ttu-id="d4488-399">Если имя файла не указано, все сообщения об ошибках возвращаются на страницу результатов.</span><span class="sxs-lookup"><span data-stu-id="d4488-399">If a file name is not provided, then all errors will be returned on the Results page.</span></span>
2. <span data-ttu-id="d4488-400">Если указано имя файла, но не указан каталог, то файл будет создан (или перезаписан) в текущем каталоге среды.</span><span class="sxs-lookup"><span data-stu-id="d4488-400">If a file name is provided without a directory, then the file will be created (or overwritten) in the current environment directory.</span></span>
3. <span data-ttu-id="d4488-401">Если выбрать существующий файл, то файл будет перезаписан. Добавить его нельзя.</span><span class="sxs-lookup"><span data-stu-id="d4488-401">If you select an existing file, then the file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="d4488-402">Затем укажите, какие сообщение об ошибках необходимо регистрировать в журнале — все, критические или никакие.</span><span class="sxs-lookup"><span data-stu-id="d4488-402">Then, choose whether to log all, critical, or no error messages.</span></span> <span data-ttu-id="d4488-403">И, наконец, решите, как часто будет обновляться сообщение о переносе данных на экране.</span><span class="sxs-lookup"><span data-stu-id="d4488-403">Finally, decide how frequently the on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="d4488-404">Подтверждение параметров импорта и просмотр командной строки</span><span class="sxs-lookup"><span data-stu-id="d4488-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="d4488-405">Указав сведения об источнике и конечном объекте и настроив расширенную конфигурацию, просмотрите сводку миграции и, если нужно, просмотрите или скопируйте получившуюся команду миграции (копирование команды полезно для автоматизации операций импорта).</span><span class="sxs-lookup"><span data-stu-id="d4488-405">After specifying source information, target information, and advanced configuration, review the migration summary and, optionally, view/copy the resulting migration command (copying the command is useful to automate import operations):</span></span>
   
    ![Снимок экрана: окно сводки](./media/import-data/summary.png)
   
    ![Снимок экрана: окно сводки](./media/import-data/summarycommand.png)
2. <span data-ttu-id="d4488-408">После проверки источника и назначения нажмите кнопку **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="d4488-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="d4488-409">Затраченное время, число передаваемых объектов и сведения об ошибках (если вы не указали имя файла при настройке расширенной конфигурации) обновляются в процессе импорта.</span><span class="sxs-lookup"><span data-stu-id="d4488-409">The elapsed time, transferred count, and failure information (if you didn't provide a file name in the Advanced configuration) will update as the import is in process.</span></span> <span data-ttu-id="d4488-410">После завершения вы можете экспортировать результаты (например, для обработки ошибок импорта).</span><span class="sxs-lookup"><span data-stu-id="d4488-410">Once complete, you can export the results (e.g. to deal with any import failures).</span></span>
   
    ![Снимок экрана: параметры экспорта в Azure Cosmos DB JSON](./media/import-data/viewresults.png)
3. <span data-ttu-id="d4488-412">Можно также запустить новую операцию импорта, сохранив существующие параметры (например, строку подключения, источник и назначение и т. д.) или сбросить все значения.</span><span class="sxs-lookup"><span data-stu-id="d4488-412">You may also start a new import, either keeping the existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Снимок экрана: параметры экспорта в Azure Cosmos DB JSON](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="d4488-414">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4488-414">Next steps</span></span>

<span data-ttu-id="d4488-415">В этом руководстве вы выполнили следующее:</span><span class="sxs-lookup"><span data-stu-id="d4488-415">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d4488-416">установка средства миграции данных;</span><span class="sxs-lookup"><span data-stu-id="d4488-416">Installed the Data Migration tool</span></span>
> * <span data-ttu-id="d4488-417">импорт данных из разных источников данных;</span><span class="sxs-lookup"><span data-stu-id="d4488-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="d4488-418">экспорт данных из Azure Cosmos DB в JSON.</span><span class="sxs-lookup"><span data-stu-id="d4488-418">Exported from Azure Cosmos DB to JSON</span></span>

<span data-ttu-id="d4488-419">Теперь вы можете перейти к следующему руководству, из которого вы узнаете, как запрашивать данные с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d4488-419">You can now proceed to the next tutorial and learn how to query data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="d4488-420">Как выполнять запросы с помощью SQL в базе данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d4488-420">How to query data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
