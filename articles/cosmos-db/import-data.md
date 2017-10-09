---
title: "Средство миграции aaaDatabase для Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, каким образом toouse hello открыть tooAzure tooimport данных данных миграции источника Azure Cosmos DB средства Cosmos DB из различных источников, включая файлы, MongoDB, SQL Server, хранилище таблицы, Amazon DynamoDB, CSV и JSON. Преобразование tooJSON CSV."
keywords: "toojson CSV, инструменты миграции баз данных, преобразование csv toojson"
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
ms.openlocfilehash: 997648a31602d854db75bb6ce4e2ecff36fc1069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a><span data-ttu-id="6bc1b-105">Как tooimport данных в базе данных Azure Cosmos для hello DocumentDB API?</span><span class="sxs-lookup"><span data-stu-id="6bc1b-105">How tooimport data into Azure Cosmos DB for hello DocumentDB API?</span></span>

<span data-ttu-id="6bc1b-106">В этом учебнике содержатся инструкции по использованию hello Azure Cosmos DB: инструмент переноса данных API DocumentDB, который можно импортировать данные из различных источников, включая файлы JSON, CSV файлы SQL, MongoDB, хранилище таблиц Azure, Amazon DynamoDB и Azure Cosmos DB DocumentDB Коллекций API в коллекции для использования с Azure Cosmos DB и hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-106">This tutorial provides instructions on using hello Azure Cosmos DB: DocumentDB API Data Migration tool, which can import data from various sources, including JSON files, CSV files, SQL, MongoDB, Azure Table storage, Amazon DynamoDB and Azure Cosmos DB DocumentDB API collections into collections for use with Azure Cosmos DB and hello DocumentDB API.</span></span> <span data-ttu-id="6bc1b-107">также можно использовать средство переноса данных Hello, при миграции из коллекции несколькими разделами коллекции tooa одну секцию для hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-107">hello Data Migration tool can also be used when migrating from a single partition collection tooa multi-partition collection for hello DocumentDB API.</span></span>

<span data-ttu-id="6bc1b-108">Средство переноса данных Hello работает только в том случае, если импорт данных в базу данных Cosmos Azure для использования с hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-108">hello Data Migration tool only works when importing data into Azure Cosmos DB for use with hello DocumentDB API.</span></span> <span data-ttu-id="6bc1b-109">Импорт данных для использования с hello API таблиц или Graph API в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-109">Importing data for use with hello Table API or Graph API is not supported at this time.</span></span> 

<span data-ttu-id="6bc1b-110">tooimport данных для использования с hello MongoDB API. в статье [Azure Cosmos DB: как toomigrate данные для hello MongoDB API?](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-110">tooimport data for use with hello MongoDB API, see [Azure Cosmos DB: How toomigrate data for hello MongoDB API?](mongodb-migrate.md).</span></span>

<span data-ttu-id="6bc1b-111">В этом учебнике hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-111">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bc1b-112">Установка средства переноса данных hello</span><span class="sxs-lookup"><span data-stu-id="6bc1b-112">Installing hello Data Migration tool</span></span>
> * <span data-ttu-id="6bc1b-113">импорт данных из разных источников данных;</span><span class="sxs-lookup"><span data-stu-id="6bc1b-113">Importing data from different data sources</span></span>
> * <span data-ttu-id="6bc1b-114">Экспорт из Azure Cosmos DB tooJSON</span><span class="sxs-lookup"><span data-stu-id="6bc1b-114">Exporting from Azure Cosmos DB tooJSON</span></span>

## <span data-ttu-id="6bc1b-115"><a id="Prerequisites"></a>Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6bc1b-115"><a id="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="6bc1b-116">Перед выполнением инструкции hello в этой статье, убедитесь, что установлены следующие компоненты hello:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-116">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="6bc1b-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) или более поздняя версия.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-117">[Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) or higher.</span></span>

## <span data-ttu-id="6bc1b-118"><a id="Overviewl"></a>Обзор средства переноса данных hello</span><span class="sxs-lookup"><span data-stu-id="6bc1b-118"><a id="Overviewl"></a>Overview of hello Data Migration tool</span></span>
<span data-ttu-id="6bc1b-119">Средство переноса данных Hello — это решение открытым исходным кодом, которое импортирует данные tooAzure Cosmos DB из разнообразных источников, включая:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-119">hello Data Migration tool is an open source solution that imports data tooAzure Cosmos DB from a variety of sources, including:</span></span>

* <span data-ttu-id="6bc1b-120">файлы JSON;</span><span class="sxs-lookup"><span data-stu-id="6bc1b-120">JSON files</span></span>
* <span data-ttu-id="6bc1b-121">MongoDB</span><span class="sxs-lookup"><span data-stu-id="6bc1b-121">MongoDB</span></span>
* <span data-ttu-id="6bc1b-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6bc1b-122">SQL Server</span></span>
* <span data-ttu-id="6bc1b-123">СЫМ-файлы;</span><span class="sxs-lookup"><span data-stu-id="6bc1b-123">CSV files</span></span>
* <span data-ttu-id="6bc1b-124">табличное хранилище Azure;</span><span class="sxs-lookup"><span data-stu-id="6bc1b-124">Azure Table storage</span></span>
* <span data-ttu-id="6bc1b-125">Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="6bc1b-125">Amazon DynamoDB</span></span>
* <span data-ttu-id="6bc1b-126">HBase</span><span class="sxs-lookup"><span data-stu-id="6bc1b-126">HBase</span></span>
* <span data-ttu-id="6bc1b-127">коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-127">Azure Cosmos DB collections</span></span>

<span data-ttu-id="6bc1b-128">Хотя средство импорта hello включает графический интерфейс пользователя (dtui.exe), его также можно управлять из командной строки hello (dt.exe).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-128">While hello import tool includes a graphical user interface (dtui.exe), it can also be driven from hello command line (dt.exe).</span></span> <span data-ttu-id="6bc1b-129">На самом деле присутствует команда hello связанный параметр toooutput после настройки импорта через hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-129">In fact, there is an option toooutput hello associated command after setting up an import through hello UI.</span></span> <span data-ttu-id="6bc1b-130">Табличный источник данных (например, SQL Server или CSV-файлы) можно преобразовать так, чтобы создать иерархические связи (вложенные документы) во время импорта.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-130">Tabular source data (e.g. SQL Server or CSV files) can be transformed such that hierarchical relationships (subdocuments) can be created during import.</span></span> <span data-ttu-id="6bc1b-131">Сохраните чтения toolearn больше о параметрах источника, образец tooimport командные строки из каждого источника, target-параметры и при просмотре Импорт результатов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-131">Keep reading toolearn more about source options, sample command lines tooimport from each source, target options, and viewing import results.</span></span>

## <span data-ttu-id="6bc1b-132"><a id="Install"></a>Установка средства миграции данных hello</span><span class="sxs-lookup"><span data-stu-id="6bc1b-132"><a id="Install"></a>Install hello Data Migration tool</span></span>
<span data-ttu-id="6bc1b-133">Hello миграции средство исходный код доступен на GitHub в [этот репозиторий](https://github.com/azure/azure-documentdb-datamigrationtool) и скомпилированная версия доступна в [центра загрузки Майкрософт](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-133">hello migration tool source code is available on GitHub in [this repository](https://github.com/azure/azure-documentdb-datamigrationtool) and a compiled version is available from [Microsoft Download Center](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d).</span></span> <span data-ttu-id="6bc1b-134">Может либо компиляции решения hello, или просто загрузите и извлеките hello скомпилированная версия tooa каталога по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-134">You may either compile hello solution or simply download and extract hello compiled version tooa directory of your choice.</span></span> <span data-ttu-id="6bc1b-135">Затем запустите:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-135">Then run either:</span></span>

* <span data-ttu-id="6bc1b-136">**Dtui.exe**: графический интерфейс версия средства hello</span><span class="sxs-lookup"><span data-stu-id="6bc1b-136">**Dtui.exe**: Graphical interface version of hello tool</span></span>
* <span data-ttu-id="6bc1b-137">**DT.exe**: версией hello инструмента командной строки</span><span class="sxs-lookup"><span data-stu-id="6bc1b-137">**Dt.exe**: Command-line version of hello tool</span></span>

## <a name="import-data"></a><span data-ttu-id="6bc1b-138">Импорт данных</span><span class="sxs-lookup"><span data-stu-id="6bc1b-138">Import data</span></span>

<span data-ttu-id="6bc1b-139">После установки средство hello, это время tooimport данных.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-139">Once you've installed hello tool, it's time tooimport your data.</span></span> <span data-ttu-id="6bc1b-140">Тип данных действительно tooimport?</span><span class="sxs-lookup"><span data-stu-id="6bc1b-140">What kind of data do you want tooimport?</span></span>

* <span data-ttu-id="6bc1b-141">[файлы JSON](#JSON);</span><span class="sxs-lookup"><span data-stu-id="6bc1b-141">[JSON files](#JSON)</span></span>
* [<span data-ttu-id="6bc1b-142">MongoDB</span><span class="sxs-lookup"><span data-stu-id="6bc1b-142">MongoDB</span></span>](#MongoDB)
* <span data-ttu-id="6bc1b-143">[файлы экспорта MongoDB](#MongoDBExport);</span><span class="sxs-lookup"><span data-stu-id="6bc1b-143">[MongoDB Export files](#MongoDBExport)</span></span>
* [<span data-ttu-id="6bc1b-144">SQL Server</span><span class="sxs-lookup"><span data-stu-id="6bc1b-144">SQL Server</span></span>](#SQL)
* <span data-ttu-id="6bc1b-145">[CSV-файлы](#CSV);</span><span class="sxs-lookup"><span data-stu-id="6bc1b-145">[CSV files](#CSV)</span></span>
* [<span data-ttu-id="6bc1b-146">Хранилище таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="6bc1b-146">Azure Table storage</span></span>](#AzureTableSource)
* <span data-ttu-id="6bc1b-147">[Amazon DynamoDB](#DynamoDBSource);</span><span class="sxs-lookup"><span data-stu-id="6bc1b-147">[Amazon DynamoDB](#DynamoDBSource)</span></span>
* [<span data-ttu-id="6bc1b-148">Большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="6bc1b-148">Blob</span></span>](#BlobImport)
* <span data-ttu-id="6bc1b-149">[коллекции Azure Cosmos DB](#DocumentDBSource);</span><span class="sxs-lookup"><span data-stu-id="6bc1b-149">[Azure Cosmos DB collections](#DocumentDBSource)</span></span>
* [<span data-ttu-id="6bc1b-150">HBase</span><span class="sxs-lookup"><span data-stu-id="6bc1b-150">HBase</span></span>](#HBaseSource)
* <span data-ttu-id="6bc1b-151">[массовый импорт Azure Cosmos DB](#DocumentDBBulkImport);</span><span class="sxs-lookup"><span data-stu-id="6bc1b-151">[Azure Cosmos DB bulk import](#DocumentDBBulkImport)</span></span>
* <span data-ttu-id="6bc1b-152">[последовательный импорт записей Azure Cosmos DB](#DocumentDSeqTarget).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-152">[Azure Cosmos DB sequential record import](#DocumentDSeqTarget)</span></span>


## <span data-ttu-id="6bc1b-153"><a id="JSON"></a>tooimport JSON-файлов</span><span class="sxs-lookup"><span data-stu-id="6bc1b-153"><a id="JSON"></a>tooimport JSON files</span></span>
<span data-ttu-id="6bc1b-154">Hello параметр импортера исходный файл JSON можно tooimport один или более одного документа JSON-файлов или массив JSON документов, содержащих файлы JSON.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-154">hello JSON file source importer option allows you tooimport one or more single document JSON files or JSON files that each contain an array of JSON documents.</span></span> <span data-ttu-id="6bc1b-155">При добавлении папки, содержащие файлы tooimport JSON, предусмотрена возможность hello рекурсивный поиск файлов во вложенных папках.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-155">When adding folders that contain JSON files tooimport, you have hello option of recursively searching for files in subfolders.</span></span>

![Снимок экрана: параметры исходного файла JSON — средства миграции базы данных](./media/import-data/jsonsource.png)

<span data-ttu-id="6bc1b-157">Ниже приведены некоторые файлы JSON tooimport образцы командной строки.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-157">Here are some command line samples tooimport JSON files:</span></span>

    #Import a single JSON file
    dt.exe /s:JsonFile /s.Files:.\Sessions.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory of JSON files
    dt.exe /s:JsonFile /s.Files:C:\TESessions\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Sessions /t.CollectionThroughput:2500

    #Import a directory (including sub-directories) of JSON files
    dt.exe /s:JsonFile /s.Files:C:\LastFMMusic\**\*.json /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Music /t.CollectionThroughput:2500

    #Import a directory (single), directory (recursive), and individual JSON files
    dt.exe /s:JsonFile /s.Files:C:\Tweets\*.*;C:\LargeDocs\**\*.*;C:\TESessions\Session48172.json;C:\TESessions\Session48173.json;C:\TESessions\Session48174.json;C:\TESessions\Session48175.json;C:\TESessions\Session48177.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:subs /t.CollectionThroughput:2500

    #Import a single JSON file and partition hello data across 4 collections
    dt.exe /s:JsonFile /s.Files:D:\\CompanyData\\Companies.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:comp[1-4] /t.PartitionKey:name /t.CollectionThroughput:2500

## <span data-ttu-id="6bc1b-158"><a id="MongoDB"></a>tooimport из MongoDB</span><span class="sxs-lookup"><span data-stu-id="6bc1b-158"><a id="MongoDB"></a>tooimport from MongoDB</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bc1b-159">При импорте учетной записи Azure Cosmos DB tooan с поддержкой MongoDB, выполните следующие [инструкции](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-159">If you are importing tooan Azure Cosmos DB account with Support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="6bc1b-160">Hello MongoDB источника импорта параметр позволяет вам tooimport из отдельных MongoDB коллекции и при необходимости отфильтруйте документы с помощью запроса или изменить структуру документа hello с помощью проекции.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-160">hello MongoDB source importer option allows you tooimport from an individual MongoDB collection and optionally filter documents using a query and/or modify hello document structure by using a projection.</span></span>  

![Снимок экрана параметров источника MongoDB](./media/import-data/mongodbsource.png)

<span data-ttu-id="6bc1b-162">в стандартном формате MongoDB hello указана строка подключения Hello:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-162">hello connection string is in hello standard MongoDB format:</span></span>

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> <span data-ttu-id="6bc1b-163">Команда используйте hello проверьте tooensure, hello MongoDB экземпляр, указанный в поле Строка hello подключения может осуществляться.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-163">Use hello Verify command tooensure that hello MongoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bc1b-164">Введите имя hello hello коллекции, из которого будут импортированы данные.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-164">Enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="6bc1b-165">Можно при необходимости укажите или указать файл для запроса (например {pop: {$gt: 5000}}) или проекции (например {loc:0}) tooboth фильтра и форма hello данных toobe импортированы.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-165">You may optionally specify or provide a file for a query (e.g. {pop: {$gt:5000}} ) and/or projection (e.g. {loc:0} ) tooboth filter and shape hello data toobe imported.</span></span>

<span data-ttu-id="6bc1b-166">Ниже приведены некоторые tooimport образцы командной строки из MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-166">Here are some command line samples tooimport from MongoDB:</span></span>

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <span data-ttu-id="6bc1b-167"><a id="MongoDBExport"></a>файлы экспорта MongoDB tooimport</span><span class="sxs-lookup"><span data-stu-id="6bc1b-167"><a id="MongoDBExport"></a>tooimport MongoDB export files</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bc1b-168">При импорте учетной записи Azure Cosmos DB tooan с поддержкой MongoDB, выполните следующие [инструкции](mongodb-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-168">If you are importing tooan Azure Cosmos DB account with support for MongoDB, follow these [instructions](mongodb-migrate.md).</span></span>
> 
> 

<span data-ttu-id="6bc1b-169">Hello MongoDB JSON файл источника импорта экспорте позволяет tooimport одного или нескольких файлов JSON, полученных из служебной программы mongoexport hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-169">hello MongoDB export JSON file source importer option allows you tooimport one or more JSON files produced from hello mongoexport utility.</span></span>  

![Снимок экрана параметров экспорта MongoDB](./media/import-data/mongodbexportsource.png)

<span data-ttu-id="6bc1b-171">При добавлении папки, содержащие файлы JSON MongoDB экспорта для импорта, предусмотрена возможность hello рекурсивный поиск файлов во вложенных папках.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-171">When adding folders that contain MongoDB export JSON files for import, you have hello option of recursively searching for files in subfolders.</span></span>

<span data-ttu-id="6bc1b-172">Ниже приведен tooimport пример командной строки из экспорта MongoDB JSON-файлов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-172">Here is a command line sample tooimport from MongoDB export JSON files:</span></span>

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <span data-ttu-id="6bc1b-173"><a id="SQL"></a>tooimport из SQL Server</span><span class="sxs-lookup"><span data-stu-id="6bc1b-173"><a id="SQL"></a>tooimport from SQL Server</span></span>
<span data-ttu-id="6bc1b-174">Hello параметра импорта источника SQL дает tooimport из отдельной базы данных SQL Server и при необходимости отфильтруйте toobe записей hello, импортированные с помощью запроса.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-174">hello SQL source importer option allows you tooimport from an individual SQL Server database and optionally filter hello records toobe imported using a query.</span></span> <span data-ttu-id="6bc1b-175">Кроме того можно изменить структуру документа hello, указав разделитель вложения (Подробнее об этом позже).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-175">In addition, you can modify hello document structure by specifying a nesting separator (more on that in a moment).</span></span>  

![Снимок экрана: параметры источника SQL — средства миграции базы данных](./media/import-data/sqlexportsource.png)

<span data-ttu-id="6bc1b-177">Hello формат строки соединения hello является hello standard SQL соединения строки.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-177">hello format of hello connection string is hello standard SQL connection string format.</span></span>

> [!NOTE]
> <span data-ttu-id="6bc1b-178">Команда используйте hello проверьте tooensure, экземпляр SQL Server, указанной в поле Строка подключения hello hello возможен.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-178">Use hello Verify command tooensure that hello SQL Server instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bc1b-179">вложенные свойства разделителя Hello — иерархические связи используется toocreate (вложенные документы) во время импорта.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-179">hello nesting separator property is used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="6bc1b-180">Рассмотрим следующий SQL-запрос hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-180">Consider hello following SQL query:</span></span>

<span data-ttu-id="6bc1b-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span><span class="sxs-lookup"><span data-stu-id="6bc1b-181">*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*</span></span>

<span data-ttu-id="6bc1b-182">Выдаются следующие результаты (разделяемый) hello:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-182">Which returns hello following (partial) results:</span></span>

![Снимок экрана: результаты запроса SQL](./media/import-data/sqlqueryresults.png)

<span data-ttu-id="6bc1b-184">Обратите внимание, псевдонимы hello, такие как Address.AddressType и Address.Location.StateProvinceName.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-184">Note hello aliases such as Address.AddressType and Address.Location.StateProvinceName.</span></span> <span data-ttu-id="6bc1b-185">Указав разделитель вложения из '.', средство импорта hello создает адрес и импортировать Address.Location вложенные документы во время hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-185">By specifying a nesting separator of ‘.’, hello import tool creates Address and Address.Location subdocuments during hello import.</span></span> <span data-ttu-id="6bc1b-186">Ниже приведен пример полученного документа в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-186">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="6bc1b-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span><span class="sxs-lookup"><span data-stu-id="6bc1b-187">*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*</span></span>

<span data-ttu-id="6bc1b-188">Ниже приведены некоторые tooimport образцы командной строки из SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-188">Here are some command line samples tooimport from SQL Server:</span></span>

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <span data-ttu-id="6bc1b-189"><a id="CSV"></a>CSV-файлы tooimport и convert CSV tooJSON</span><span class="sxs-lookup"><span data-stu-id="6bc1b-189"><a id="CSV"></a>tooimport CSV files and convert CSV tooJSON</span></span>
<span data-ttu-id="6bc1b-190">Hello параметр импортера исходного файла CSV позволяет вам tooimport один или несколько файлов CSV.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-190">hello CSV file source importer option enables you tooimport one or more CSV files.</span></span> <span data-ttu-id="6bc1b-191">При добавлении папки, содержащие CSV-файлы для импорта, предусмотрена возможность hello рекурсивный поиск файлов во вложенных папках.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-191">When adding folders that contain CSV files for import, you have hello option of recursively searching for files in subfolders.</span></span>

![Параметры источника экрана CSV - CSV tooJSON](media/import-data/csvsource.png)

<span data-ttu-id="6bc1b-193">Аналогичные toohello SQL, вложенные свойства разделителя hello возможно, источник иерархические связи используется toocreate (вложенные документы) во время импорта.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-193">Similar toohello SQL source, hello nesting separator property may be used toocreate hierarchical relationships (sub-documents) during import.</span></span> <span data-ttu-id="6bc1b-194">Рассмотрим hello строку заголовка CSV-файла и строк данных.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-194">Consider hello following CSV header row and data rows:</span></span>

![Снимок экрана CSV образец записи - CSV tooJSON](./media/import-data/csvsample.png)

<span data-ttu-id="6bc1b-196">Обратите внимание, псевдонимы hello, такие как DomainInfo.Domain_Name и RedirectInfo.Redirecting.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-196">Note hello aliases such as DomainInfo.Domain_Name and RedirectInfo.Redirecting.</span></span> <span data-ttu-id="6bc1b-197">Указав разделитель вложения из '.', средство импорта hello создаст DomainInfo и импортировать RedirectInfo вложенные документы во время hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-197">By specifying a nesting separator of ‘.’, hello import tool will create DomainInfo and RedirectInfo subdocuments during hello import.</span></span> <span data-ttu-id="6bc1b-198">Ниже приведен пример полученного документа в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-198">Here is an example of a resulting document in Azure Cosmos DB:</span></span>

<span data-ttu-id="6bc1b-199">*{«DomainInfo»: {«Имя_домена»: «ACUS.GOV», «Domain_Name_Address»: «http://www. ACUS.GOV»}, «Федеральным агентство»: «Административные конференции; hello United States», «RedirectInfo»: {«Перенаправление»: «0», «Redirect_Destination»: «»}, «id»: «9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d»}*</span><span class="sxs-lookup"><span data-stu-id="6bc1b-199">*{ "DomainInfo": { "Domain_Name": "ACUS.GOV", "Domain_Name_Address": "http://www.ACUS.GOV" }, "Federal Agency": "Administrative Conference of hello United States", "RedirectInfo": { "Redirecting": "0", "Redirect_Destination": "" }, "id": "9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d" }*</span></span>

<span data-ttu-id="6bc1b-200">Средство импорта Hello попытается tooinfer сведения о типе значений без кавычек в CSV-файлы (заключенные в кавычки значения всегда обрабатываются как строки).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-200">hello import tool will attempt tooinfer type information for unquoted values in CSV files (quoted values are always treated as strings).</span></span>  <span data-ttu-id="6bc1b-201">Типы различаются по hello следующий порядок: номер, datetime, boolean.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-201">Types are identified in hello following order: number, datetime, boolean.</span></span>  

<span data-ttu-id="6bc1b-202">Существует два toonote вещей о импорта CSV.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-202">There are two other things toonote about CSV import:</span></span>

1. <span data-ttu-id="6bc1b-203">По умолчанию значения, не заключенные в кавычки, очищаются от табуляции и пробелов, а значения, заключенные в кавычки, остаются в нетронутом виде.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-203">By default, unquoted values are always trimmed for tabs and spaces, while quoted values are preserved as-is.</span></span> <span data-ttu-id="6bc1b-204">Это поведение можно переопределить с приветствия Trim значения флажок hello /s.TrimQuoted параметр командной строки или в кавычках.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-204">This behavior can be overridden with hello Trim quoted values checkbox or hello /s.TrimQuoted command line option.</span></span>
2. <span data-ttu-id="6bc1b-205">По умолчанию объект null, не заключенный в кавычки, считается значением null.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-205">By default, an unquoted null is treated as a null value.</span></span> <span data-ttu-id="6bc1b-206">Это поведение можно переопределить (т. е. обрабатывают без кавычек значение null как строка «null») с hello интерпретирует NULL как строка флажок hello /s.NoUnquotedNulls параметр командной строки или без кавычек.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-206">This behavior can be overridden (i.e. treat an unquoted null as a “null” string) with hello Treat unquoted NULL as string checkbox or hello /s.NoUnquotedNulls command line option.</span></span>

<span data-ttu-id="6bc1b-207">Далее показан пример команды для импорта CSV:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-207">Here is a command line sample for CSV import:</span></span>

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <span data-ttu-id="6bc1b-208"><a id="AzureTableSource"></a>tooimport из хранилища таблиц Azure</span><span class="sxs-lookup"><span data-stu-id="6bc1b-208"><a id="AzureTableSource"></a>tooimport from Azure Table storage</span></span>
<span data-ttu-id="6bc1b-209">Hello параметра импорта источника хранилища таблиц Azure позволяет вам tooimport из отдельной таблицы хранилища таблиц Azure и при необходимости отфильтруйте hello таблицы сущности toobe импортированы.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-209">hello Azure Table storage source importer option allows you tooimport from an individual Azure Table storage table and optionally filter hello table entities toobe imported.</span></span> <span data-ttu-id="6bc1b-210">Обратите внимание, нельзя использовать данные хранилища Azure Table tooimport средство hello переноса данных в базу данных Cosmos Azure для использования с hello API таблиц.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-210">Note that you cannot use hello Data Migration tool tooimport Azure Table storage data into Azure Cosmos DB for use with hello Table API.</span></span> <span data-ttu-id="6bc1b-211">В настоящее время поддерживается только импорт tooAzure Cosmos DB для использования с hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-211">Only importing tooAzure Cosmos DB for use with hello DocumentDB API is supported at this time.</span></span>

![Снимок экрана: параметры источника табличного хранилища Azure](./media/import-data/azuretablesource.png)

<span data-ttu-id="6bc1b-213">Hello объекта hello строки подключения к хранилищу таблиц Azure выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-213">hello format of hello Azure Table storage connection string is:</span></span>

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> <span data-ttu-id="6bc1b-214">Команда используйте hello проверьте tooensure, hello экземпляра хранилища Azure таблицы, указанной в поле Строка подключения hello возможен.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-214">Use hello Verify command tooensure that hello Azure Table storage instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bc1b-215">Введите имя hello hello Azure таблицы, из которого будут импортированы данные.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-215">Enter hello name of hello Azure table from which data will be imported.</span></span> <span data-ttu-id="6bc1b-216">При необходимости можно указать [фильтра](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-216">You may optionally specify a [filter](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>

<span data-ttu-id="6bc1b-217">Hello параметра импорта источника хранилища таблиц Azure имеет hello следующие дополнительные параметры:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-217">hello Azure Table storage source importer option has hello following additional options:</span></span>

1. <span data-ttu-id="6bc1b-218">Включить внутренние поля</span><span class="sxs-lookup"><span data-stu-id="6bc1b-218">Include Internal Fields</span></span>
   1. <span data-ttu-id="6bc1b-219">All — включить все внутренние поля (PartitionKey, RowKey и Timestamp)</span><span class="sxs-lookup"><span data-stu-id="6bc1b-219">All - Include all internal fields (PartitionKey, RowKey, and Timestamp)</span></span>
   2. <span data-ttu-id="6bc1b-220">None — исключить все внутренние поля</span><span class="sxs-lookup"><span data-stu-id="6bc1b-220">None - Exclude all internal fields</span></span>
   3. <span data-ttu-id="6bc1b-221">RowKey - содержать только поля RowKey hello</span><span class="sxs-lookup"><span data-stu-id="6bc1b-221">RowKey - Only include hello RowKey field</span></span>
2. <span data-ttu-id="6bc1b-222">Выбор столбцов</span><span class="sxs-lookup"><span data-stu-id="6bc1b-222">Select Columns</span></span>
   1. <span data-ttu-id="6bc1b-223">Фильтры табличного хранилища Azure не поддерживают проекции.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-223">Azure Table storage filters do not support projections.</span></span> <span data-ttu-id="6bc1b-224">Если требуется, чтобы свойства сущности определенных таблиц Azure tooonly импорта, их можно добавьте список toohello Выбор столбцов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-224">If you want tooonly import specific Azure Table entity properties, add them toohello Select Columns list.</span></span> <span data-ttu-id="6bc1b-225">Все другие свойства сущностей будут игнорироваться.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-225">All other entity properties will be ignored.</span></span>

<span data-ttu-id="6bc1b-226">Ниже приведен tooimport пример командной строки из хранилища Azure Table.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-226">Here is a command line sample tooimport from Azure Table storage:</span></span>

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <span data-ttu-id="6bc1b-227"><a id="DynamoDBSource"></a>tooimport из Amazon DynamoDB</span><span class="sxs-lookup"><span data-stu-id="6bc1b-227"><a id="DynamoDBSource"></a>tooimport from Amazon DynamoDB</span></span>
<span data-ttu-id="6bc1b-228">Hello Amazon DynamoDB источника импорта параметр дает tooimport из отдельной таблицы Amazon DynamoDB и при необходимости отфильтруйте toobe сущностей hello импортированы.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-228">hello Amazon DynamoDB source importer option allows you tooimport from an individual Amazon DynamoDB table and optionally filter hello entities toobe imported.</span></span> <span data-ttu-id="6bc1b-229">Чтобы максимально упростить настройку импорта, представлено несколько шаблонов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-229">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Снимок экрана: параметры источника DynamoDB Amazon — средства миграции базы данных](./media/import-data/dynamodbsource1.png)

![Снимок экрана: параметры источника DynamoDB Amazon — средства миграции базы данных](./media/import-data/dynamodbsource2.png)

<span data-ttu-id="6bc1b-232">Hello из строки подключения Amazon DynamoDB hello выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-232">hello format of hello Amazon DynamoDB connection string is:</span></span>

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> <span data-ttu-id="6bc1b-233">Команда используйте hello проверьте tooensure, hello экземпляр Amazon DynamoDB, указанный в поле Строка подключения hello возможен.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-233">Use hello Verify command tooensure that hello Amazon DynamoDB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bc1b-234">Ниже приведен tooimport пример командной строки из Amazon DynamoDB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-234">Here is a command line sample tooimport from Amazon DynamoDB:</span></span>

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <span data-ttu-id="6bc1b-235"><a id="BlobImport"></a>tooimport файлы из хранилища больших двоичных объектов Azure</span><span class="sxs-lookup"><span data-stu-id="6bc1b-235"><a id="BlobImport"></a>tooimport files from Azure Blob storage</span></span>
<span data-ttu-id="6bc1b-236">Hello JSON-файл, файл экспорта MongoDB и параметры импорта исходного файла CSV позволяют tooimport один или несколько файлов из хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-236">hello JSON file, MongoDB export file, and CSV file source importer options allow you tooimport one or more files from Azure Blob storage.</span></span> <span data-ttu-id="6bc1b-237">После указания URL-адрес контейнера больших двоичных объектов и ключ учетной записи, достаточно просто укажите tooimport файлов hello tooselect регулярного выражения.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-237">After specifying a Blob container URL and Account Key, simply provide a regular expression tooselect hello file(s) tooimport.</span></span>

![Снимок экрана: параметры исходного файла больших двоичных объектов](./media/import-data/blobsource.png)

<span data-ttu-id="6bc1b-239">Вот файлы JSON tooimport пример командной строки из хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-239">Here is command line sample tooimport JSON files from Azure Blob storage:</span></span>

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <span data-ttu-id="6bc1b-240"><a id="DocumentDBSource"></a>tooimport из коллекции Azure Cosmos DB DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="6bc1b-240"><a id="DocumentDBSource"></a>tooimport from an Azure Cosmos DB DocumentDB API collection</span></span>
<span data-ttu-id="6bc1b-241">Hello Azure Cosmos DB источника импорта параметр дает tooimport данные из одной или нескольких коллекциях Azure Cosmos DB и при необходимости отфильтруйте документы с помощью запроса.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-241">hello Azure Cosmos DB source importer option allows you tooimport data from one or more Azure Cosmos DB collections and optionally filter documents using a query.</span></span>  

![Снимок экрана: параметры источника Azure Cosmos DB](./media/import-data/documentdbsource.png)

<span data-ttu-id="6bc1b-243">Hello объекта hello Azure Cosmos DB строка подключения выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-243">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="6bc1b-244">Строка подключения учетной записи Azure Cosmos DB Hello могут быть получены из колонке ключи hello hello портал Azure, как описано в [как toomanage учетную запись Azure Cosmos DB](manage-account.md), однако имя hello hello базы данных должно toohello toobe добавляется Строка подключения в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-244">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="6bc1b-245">Команда используйте hello проверьте tooensure, hello Azure Cosmos DB экземпляр, указанный в поле Строка hello подключения может осуществляться.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-245">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bc1b-246">tooimport из одной коллекции Azure Cosmos DB, введите имя hello hello коллекции, из которого будут импортированы данные.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-246">tooimport from a single Azure Cosmos DB collection, enter hello name of hello collection from which data will be imported.</span></span> <span data-ttu-id="6bc1b-247">tooimport из нескольких коллекций Azure Cosmos DB предоставляют toomatch регулярное выражение одно или несколько имен коллекции (например collection01 | collection02 | collection03).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-247">tooimport from multiple Azure Cosmos DB collections, provide a regular expression toomatch one or more collection names (e.g. collection01 | collection02 | collection03).</span></span> <span data-ttu-id="6bc1b-248">При необходимости может указать, или указать файл для фильтра запросов tooboth и toobe данных hello импортировать фигуры.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-248">You may optionally specify, or provide a file for, a query tooboth filter and shape hello data toobe imported.</span></span>

> [!NOTE]
> <span data-ttu-id="6bc1b-249">Так как поле коллекции hello принимает регулярные выражения при импорте из одной коллекции, имя которого содержит знаки регулярного выражения, затем эти знаки необходимо экранировать соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-249">Since hello collection field accepts regular expressions, if you are importing from a single collection whose name contains regular expression characters, then those characters must be escaped accordingly.</span></span>
> 
> 

<span data-ttu-id="6bc1b-250">Hello Azure Cosmos DB источника импорта параметр имеет hello следующие дополнительные параметры:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-250">hello Azure Cosmos DB source importer option has hello following advanced options:</span></span>

1. <span data-ttu-id="6bc1b-251">Включить внутренние поля: Задает ли свойства системы tooinclude Azure Cosmos DB документа в hello экспорта (например _rid, _ts).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-251">Include Internal Fields: Specifies whether or not tooinclude Azure Cosmos DB document system properties in hello export (e.g. _rid, _ts).</span></span>
2. <span data-ttu-id="6bc1b-252">Число повторных попыток в случае неудачи: задает hello число tooretry hello tooAzure подключения Cosmos DB в случае временного сбоя (например прерывания подключений сети).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-252">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
3. <span data-ttu-id="6bc1b-253">Интервал повтора: Указывает, сколько времени toowait между повторная попытка подключения hello tooAzure Cosmos DB в случае временного сбоя (например прерывания подключений сети).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-253">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
4. <span data-ttu-id="6bc1b-254">Режим подключения: Указывает режим toouse hello соединения с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-254">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="6bc1b-255">доступны следующие возможности Hello: DirectTcp, DirectHttps и шлюз.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-255">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="6bc1b-256">режимы Hello прямое подключение являются быстрее, а режим hello шлюза — понятное дополнительные брандмауэра, как только он использует порт 443.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-256">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Снимок экрана: дополнительные параметры источника Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> <span data-ttu-id="6bc1b-258">Hello импортировать режим tooconnection значения по умолчанию средство DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-258">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="6bc1b-259">При возникновении неполадок брандмауэра режима tooconnection шлюза, для его выполнения требуется только порт 443.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-259">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

<span data-ttu-id="6bc1b-260">Ниже приведены некоторые tooimport образцы командной строки из базы данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-260">Here are some command line samples tooimport from Azure Cosmos DB:</span></span>

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> <span data-ttu-id="6bc1b-261">Средство импорта Azure Cosmos DB данных Hello также поддерживает импорт данных из hello [DB эмулятор Azure Cosmos](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-261">hello Azure Cosmos DB Data Import Tool also supports import of data from hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="6bc1b-262">При импорте данных из локального эмулятора, задать конечную точку hello слишком`https://localhost:<port>`.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-262">When importing data from a local emulator, set hello endpoint too`https://localhost:<port>`.</span></span> 
> 
> 

## <span data-ttu-id="6bc1b-263"><a id="HBaseSource"></a>tooimport из HBase</span><span class="sxs-lookup"><span data-stu-id="6bc1b-263"><a id="HBaseSource"></a>tooimport from HBase</span></span>
<span data-ttu-id="6bc1b-264">Hello HBase источника импорта параметр дает tooimport данных из таблицы HBase и при необходимости отфильтруйте данные hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-264">hello HBase source importer option allows you tooimport data from an HBase table and optionally filter hello data.</span></span> <span data-ttu-id="6bc1b-265">Чтобы максимально упростить настройку импорта, представлено несколько шаблонов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-265">Several templates are provided so that setting up an import is as easy as possible.</span></span>

![Снимок экрана: параметры источника HBase](./media/import-data/hbasesource1.png)

![Снимок экрана: параметры источника HBase](./media/import-data/hbasesource2.png)

<span data-ttu-id="6bc1b-268">имеет формат Hello hello строка подключения HBase Stargate:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-268">hello format of hello HBase Stargate connection string is:</span></span>

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> <span data-ttu-id="6bc1b-269">Команда используйте hello проверьте tooensure, hello HBase экземпляр, указанный в поле Строка hello подключения может осуществляться.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-269">Use hello Verify command tooensure that hello HBase instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bc1b-270">Ниже приведен tooimport пример командной строки из HBase:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-270">Here is a command line sample tooimport from HBase:</span></span>

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <span data-ttu-id="6bc1b-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello API DocumentDB (массового импорта)</span><span class="sxs-lookup"><span data-stu-id="6bc1b-271"><a id="DocumentDBBulkTarget"></a>tooimport toohello DocumentDB API (Bulk Import)</span></span>
<span data-ttu-id="6bc1b-272">Hello Azure Cosmos DB массового импорта позволяет tooimport из любой из параметров hello доступный источник, с помощью Azure DB Cosmos хранимые процедуры для повышения эффективности.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-272">hello Azure Cosmos DB Bulk importer allows you tooimport from any of hello available source options, using an Azure Cosmos DB stored procedure for efficiency.</span></span> <span data-ttu-id="6bc1b-273">Средство Hello поддерживает коллекцию Azure Cosmos DB секционированную одним tooone импорта, а также сегментированных импорта, при котором данные секционируются в различных коллекциях секционированную одним Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-273">hello tool supports import tooone single-partitioned Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partitioned Azure Cosmos DB collections.</span></span> <span data-ttu-id="6bc1b-274">Дополнительные сведения о секционировании данных см. в статье о [секционировании и масштабировании в Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-274">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span> <span data-ttu-id="6bc1b-275">Hello средство создания, выполнения и удалите hello хранимой процедуры из коллекций целевой hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-275">hello tool will create, execute, and then delete hello stored procedure from hello target collection(s).</span></span>  

![Снимок экрана: параметры массового импорта Azure Cosmos DB](./media/import-data/documentdbbulk.png)

<span data-ttu-id="6bc1b-277">Hello объекта hello Azure Cosmos DB строка подключения выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-277">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="6bc1b-278">Строка подключения учетной записи Azure Cosmos DB Hello могут быть получены из колонке ключи hello hello портал Azure, как описано в [как toomanage учетную запись Azure Cosmos DB](manage-account.md), однако имя hello hello базы данных должно toohello toobe добавляется Строка подключения в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-278">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<CosmosDB Database>;

> [!NOTE]
> <span data-ttu-id="6bc1b-279">Команда используйте hello проверьте tooensure, hello Azure Cosmos DB экземпляр, указанный в поле Строка hello подключения может осуществляться.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-279">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bc1b-280">tooimport tooa один коллекцию, введите имя hello hello toowhich коллекции данных будут импортированы и нажмите кнопку "Добавить" hello ".</span><span class="sxs-lookup"><span data-stu-id="6bc1b-280">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="6bc1b-281">коллекции toomultiple tooimport, введите имя каждой коллекции отдельно или используйте следующий синтаксис toospecify hello несколько коллекций: *collection_prefix*[начальный индекс - конечный индекс].</span><span class="sxs-lookup"><span data-stu-id="6bc1b-281">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="6bc1b-282">При указании нескольких коллекций hello упомянутой выше синтаксис, учитывайте следующие hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-282">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="6bc1b-283">Поддерживаются только шаблоны имени диапазона целых чисел.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-283">Only integer range name patterns are supported.</span></span> <span data-ttu-id="6bc1b-284">Например, указав коллекцию [0-3] сформирует hello следующие коллекции: collection0 collection1 collection2 collection3.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-284">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="6bc1b-285">Вы можете использовать сокращенный синтаксис: если ввести collection[3], будет отображен тот же набор коллекций, что и на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-285">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="6bc1b-286">Вы можете указать несколько подстановок.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-286">More than one substitution can be provided.</span></span> <span data-ttu-id="6bc1b-287">Например, коллекция [0–1] [0–9] создаст 20 имен коллекций с нулем в начале (collection01… 02… 03).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-287">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="6bc1b-288">Как только hello коллекции имена были заданы, выберите hello необходимой пропускной способности hello коллекций (400 RUs too10, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-288">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too10,000 RUs).</span></span> <span data-ttu-id="6bc1b-289">Для повышения производительности выберите большее значение.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-289">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="6bc1b-290">Дополнительные сведения об уровнях производительности в Azure Cosmos DB см. в [этой статье](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-290">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6bc1b-291">параметр пропускную способность производительности Hello применяется только toocollection создания.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-291">hello performance throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="6bc1b-292">Если указан hello коллекция уже существует, ее пропускная способность останутся без изменений.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-292">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="6bc1b-293">При импорте toomultiple коллекций, средство импорта hello поддерживает сегментирования на основе хэша.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-293">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="6bc1b-294">В этом случае укажите hello свойство документа, нужно toouse как hello ключ секционирования (если ключ раздела оставлено пустым, документы будут иметь сегментированных случайным образом в коллекциях целевой hello).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-294">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="6bc1b-295">При необходимости указать, какие поля в источнике импорта hello следует использовать в качестве hello Azure Cosmos DB свойство идентификатора документа во время импорта hello (Обратите внимание, что если это свойство не содержат документы, то средство импорта hello создаст GUID как значение свойства идентификатора hello).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-295">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="6bc1b-296">Во время импорта доступны ряд дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-296">There are a number of advanced options available during import.</span></span> <span data-ttu-id="6bc1b-297">Во-первых при этом включает средство hello по умолчанию массового импорта хранимой процедуры (BulkInsert.js), вы можете toospecify импорта хранимой процедуры:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-297">First, while hello tool includes a default bulk import stored procedure (BulkInsert.js), you may choose toospecify your own import stored procedure:</span></span>

 ![Снимок экрана: параметр хранимой процедуры массового импорта Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

<span data-ttu-id="6bc1b-299">Кроме того, при импорте типов даты (например, из SQL Server или MongoDB) можно выбрать три параметра импорта:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-299">Additionally, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Снимок экрана: параметры импорта даты и времени импорта Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="6bc1b-301">Строка: сохраняется как строковое значение.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-301">String: Persist as a string value</span></span>
* <span data-ttu-id="6bc1b-302">Эпоха: сохраняется как век числовое значение эпохи.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-302">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="6bc1b-303">Оба: сохраняются строковое значение и числовое значение эпохи.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-303">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="6bc1b-304">Этот параметр создает вложенный документ, например "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="6bc1b-304">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="6bc1b-305">Hello Azure Cosmos DB массового импорта имеет hello следующие дополнительные расширенные параметры:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-305">hello Azure Cosmos DB Bulk importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="6bc1b-306">Размер пакета: hello средство значения по умолчанию tooa размер пакета равным 50.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-306">Batch Size: hello tool defaults tooa batch size of 50.</span></span>  <span data-ttu-id="6bc1b-307">Если импортировать toobe документы hello большие, понижать hello размер пакета.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-307">If hello documents toobe imported are large, consider lowering hello batch size.</span></span> <span data-ttu-id="6bc1b-308">И наоборот Если импортировать toobe документы hello малы, рекомендуется обрабатывать hello размер пакета.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-308">Conversely, if hello documents toobe imported are small, consider raising hello batch size.</span></span>
2. <span data-ttu-id="6bc1b-309">Сценарий максимальный размер (байт): hello средство по умолчанию используется размер max скрипта tooa 512 КБ</span><span class="sxs-lookup"><span data-stu-id="6bc1b-309">Max Script Size (bytes): hello tool defaults tooa max script size of 512KB</span></span>
3. <span data-ttu-id="6bc1b-310">Отключить автоматическое создание идентификатора: Если каждый toobe документа импорта содержит поля id, затем при выборе этого параметра может повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-310">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="6bc1b-311">Документы без поля уникального идентификатора не будут импортированы.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-311">Documents missing a unique id field will not be imported.</span></span>
4. <span data-ttu-id="6bc1b-312">Обновление существующие документы: hello средство toonot значения по умолчанию, заменив существующие документы конфликтов идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-312">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="6bc1b-313">При выборе этого параметра существующие документы с совпадающими идентификаторами будут перезаписываться.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-313">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="6bc1b-314">Эта функция пригодится для плановых миграций, которые используются для обновления существующих документов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-314">This feature is useful for scheduled data migrations that update existing documents.</span></span>
5. <span data-ttu-id="6bc1b-315">Число повторных попыток в случае неудачи: задает hello число tooretry hello tooAzure подключения Cosmos DB в случае временного сбоя (например прерывания подключений сети).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-315">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="6bc1b-316">Интервал повтора: Указывает, сколько времени toowait между повторная попытка подключения hello tooAzure Cosmos DB в случае временного сбоя (например прерывания подключений сети).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-316">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
7. <span data-ttu-id="6bc1b-317">Режим подключения: Указывает режим toouse hello соединения с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-317">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="6bc1b-318">доступны следующие возможности Hello: DirectTcp, DirectHttps и шлюз.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-318">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="6bc1b-319">режимы Hello прямое подключение являются быстрее, а режим hello шлюза — понятное дополнительные брандмауэра, как только он использует порт 443.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-319">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Снимок экрана: дополнительные параметры массового импорта Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> <span data-ttu-id="6bc1b-321">Hello импортировать режим tooconnection значения по умолчанию средство DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-321">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="6bc1b-322">При возникновении неполадок брандмауэра режима tooconnection шлюза, для его выполнения требуется только порт 443.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-322">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="6bc1b-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello API DocumentDB (Импорт последовательной записи)</span><span class="sxs-lookup"><span data-stu-id="6bc1b-323"><a id="DocumentDBSeqTarget"></a>tooimport toohello DocumentDB API (Sequential Record Import)</span></span>
<span data-ttu-id="6bc1b-324">Hello Azure Cosmos DB последовательной записи импорта позволяет tooimport из hello доступные исходные параметры на основе по одной записи.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-324">hello Azure Cosmos DB sequential record importer allows you tooimport from any of hello available source options on a record by record basis.</span></span> <span data-ttu-id="6bc1b-325">Можно выбрать этот параметр, если вы импортируете tooan существующую коллекцию, достигнута квота хранимых процедур.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-325">You might choose this option if you’re importing tooan existing collection that has reached its quota of stored procedures.</span></span> <span data-ttu-id="6bc1b-326">поддерживает импорт Hello средство tooa одиночными коллекции Azure Cosmos DB (одной секции и несколькими секции), а также сегментированных импорта, при котором данные секционируются в различных коллекциях Azure Cosmos DB одной секции и/или несколько секций.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-326">hello tool supports import tooa single (both single-partition and multi-partition) Azure Cosmos DB collection, as well as sharded import whereby data is partitioned across multiple single-partition and/or multi-partition Azure Cosmos DB collections.</span></span> <span data-ttu-id="6bc1b-327">Дополнительные сведения о секционировании данных см. в статье о [секционировании и масштабировании в Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-327">For more information about partitioning data, see [Partitioning and scaling in Azure Cosmos DB](partition-data.md).</span></span>

![Снимок экрана: параметры последовательного импорта записей Azure Cosmos DB](./media/import-data/documentdbsequential.png)

<span data-ttu-id="6bc1b-329">Hello объекта hello Azure Cosmos DB строка подключения выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-329">hello format of hello Azure Cosmos DB connection string is:</span></span>

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

<span data-ttu-id="6bc1b-330">Строка подключения учетной записи Azure Cosmos DB Hello могут быть получены из колонке ключи hello hello портал Azure, как описано в [как toomanage учетную запись Azure Cosmos DB](manage-account.md), однако имя hello hello базы данных должно toohello toobe добавляется Строка подключения в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-330">hello Azure Cosmos DB account connection string can be retrieved from hello Keys blade of hello Azure portal, as described in [How toomanage an Azure Cosmos DB account](manage-account.md), however hello name of hello database needs toobe appended toohello connection string in hello following format:</span></span>

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> <span data-ttu-id="6bc1b-331">Команда используйте hello проверьте tooensure, hello Azure Cosmos DB экземпляр, указанный в поле Строка hello подключения может осуществляться.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-331">Use hello Verify command tooensure that hello Azure Cosmos DB instance specified in hello connection string field can be accessed.</span></span>
> 
> 

<span data-ttu-id="6bc1b-332">tooimport tooa один коллекцию, введите имя hello hello toowhich коллекции данных будут импортированы и нажмите кнопку "Добавить" hello ".</span><span class="sxs-lookup"><span data-stu-id="6bc1b-332">tooimport tooa single collection, enter hello name of hello collection toowhich data will be imported and click hello Add button.</span></span> <span data-ttu-id="6bc1b-333">коллекции toomultiple tooimport, введите имя каждой коллекции отдельно или используйте следующий синтаксис toospecify hello несколько коллекций: *collection_prefix*[начальный индекс - конечный индекс].</span><span class="sxs-lookup"><span data-stu-id="6bc1b-333">tooimport toomultiple collections, either enter each collection name individually or use hello following syntax toospecify multiple collections: *collection_prefix*[start index - end index].</span></span> <span data-ttu-id="6bc1b-334">При указании нескольких коллекций hello упомянутой выше синтаксис, учитывайте следующие hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-334">When specifying multiple collections via hello aforementioned syntax, keep hello following in mind:</span></span>

1. <span data-ttu-id="6bc1b-335">Поддерживаются только шаблоны имени диапазона целых чисел.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-335">Only integer range name patterns are supported.</span></span> <span data-ttu-id="6bc1b-336">Например, указав коллекцию [0-3] сформирует hello следующие коллекции: collection0 collection1 collection2 collection3.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-336">For example, specifying collection[0-3] will produce hello following collections: collection0, collection1, collection2, collection3.</span></span>
2. <span data-ttu-id="6bc1b-337">Вы можете использовать сокращенный синтаксис: если ввести collection[3], будет отображен тот же набор коллекций, что и на этапе 1.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-337">You can use an abbreviated syntax: collection[3] will emit same set of collections mentioned in step 1.</span></span>
3. <span data-ttu-id="6bc1b-338">Вы можете указать несколько подстановок.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-338">More than one substitution can be provided.</span></span> <span data-ttu-id="6bc1b-339">Например, коллекция [0–1] [0–9] создаст 20 имен коллекций с нулем в начале (collection01… 02… 03).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-339">For example, collection[0-1] [0-9] will generate 20 collection names with leading zeros (collection01, ..02, ..03).</span></span>

<span data-ttu-id="6bc1b-340">Как только hello коллекции имена были заданы, выберите hello необходимой пропускной способности hello коллекций (400 RUs too250, 000 RUs).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-340">Once hello collection name(s) have been specified, choose hello desired throughput of hello collection(s) (400 RUs too250,000 RUs).</span></span> <span data-ttu-id="6bc1b-341">Для повышения производительности выберите большее значение.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-341">For best import performance, choose a higher throughput.</span></span> <span data-ttu-id="6bc1b-342">Дополнительные сведения об уровнях производительности в Azure Cosmos DB см. в [этой статье](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-342">For more information about performance levels, see [Performance levels in Azure Cosmos DB](performance-levels.md).</span></span> <span data-ttu-id="6bc1b-343">Любой импортировать toocollections с пропускной способностью > 10 000 RUs потребуется ключ раздела.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-343">Any import toocollections with throughput >10,000 RUs will require a partition key.</span></span> <span data-ttu-id="6bc1b-344">При выборе более 250 RUs toohave потребуется toofile запрос портала toohave hello, увеличивается вашей учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-344">If you choose toohave more than 250,000 RUs, you will need toofile a request in hello portal toohave your account increased.</span></span>

> [!NOTE]
> <span data-ttu-id="6bc1b-345">пропускная способность приветствия применяется только toocollection создания.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-345">hello throughput setting only applies toocollection creation.</span></span> <span data-ttu-id="6bc1b-346">Если указан hello коллекция уже существует, ее пропускная способность останутся без изменений.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-346">If hello specified collection already exists, its throughput will not be modified.</span></span>
> 
> 

<span data-ttu-id="6bc1b-347">При импорте toomultiple коллекций, средство импорта hello поддерживает сегментирования на основе хэша.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-347">When importing toomultiple collections, hello import tool supports hash based sharding.</span></span> <span data-ttu-id="6bc1b-348">В этом случае укажите hello свойство документа, нужно toouse как hello ключ секционирования (если ключ раздела оставлено пустым, документы будут иметь сегментированных случайным образом в коллекциях целевой hello).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-348">In this scenario, specify hello document property you wish toouse as hello Partition Key (if Partition Key is left blank, documents will be sharded randomly across hello target collections).</span></span>

<span data-ttu-id="6bc1b-349">При необходимости указать, какие поля в источнике импорта hello следует использовать в качестве hello Azure Cosmos DB свойство идентификатора документа во время импорта hello (Обратите внимание, что если это свойство не содержат документы, то средство импорта hello создаст GUID как значение свойства идентификатора hello).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-349">You may optionally specify which field in hello import source should be used as hello Azure Cosmos DB document id property during hello import (note that if documents do not contain this property, then hello import tool will generate a GUID as hello id property value).</span></span>

<span data-ttu-id="6bc1b-350">Во время импорта доступны ряд дополнительных параметров.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-350">There are a number of advanced options available during import.</span></span> <span data-ttu-id="6bc1b-351">При импорте типов даты (например, из SQL Server или MongoDB) можно выбрать три параметра импорта:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-351">First, when importing date types (e.g. from SQL Server or MongoDB), you can choose between three import options:</span></span>

 ![Снимок экрана: параметры импорта даты и времени импорта Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* <span data-ttu-id="6bc1b-353">Строка: сохраняется как строковое значение.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-353">String: Persist as a string value</span></span>
* <span data-ttu-id="6bc1b-354">Эпоха: сохраняется как век числовое значение эпохи.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-354">Epoch: Persist as an Epoch number value</span></span>
* <span data-ttu-id="6bc1b-355">Оба: сохраняются строковое значение и числовое значение эпохи.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-355">Both: Persist both string and Epoch number values.</span></span> <span data-ttu-id="6bc1b-356">Этот параметр создает вложенный документ, например "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span><span class="sxs-lookup"><span data-stu-id="6bc1b-356">This option will create a subdocument, for example: "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }</span></span>

<span data-ttu-id="6bc1b-357">Hello Azure Cosmos DB - импортера последовательной записи имеет hello следующие дополнительные расширенные параметры:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-357">hello Azure Cosmos DB - Sequential record importer has hello following additional advanced options:</span></span>

1. <span data-ttu-id="6bc1b-358">Количество параллельных запросов: hello инструмент по умолчанию too2 параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-358">Number of Parallel Requests: hello tool defaults too2 parallel requests.</span></span> <span data-ttu-id="6bc1b-359">Если импортировать toobe документы hello малы, рекомендуется обрабатывать hello число параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-359">If hello documents toobe imported are small, consider raising hello number of parallel requests.</span></span> <span data-ttu-id="6bc1b-360">Обратите внимание, что если это число возникает слишком часто, hello импорта возможно возникновение регулирования.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-360">Note that if this number is raised too much, hello import may experience throttling.</span></span>
2. <span data-ttu-id="6bc1b-361">Отключить автоматическое создание идентификатора: Если каждый toobe документа импорта содержит поля id, затем при выборе этого параметра может повысить производительность.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-361">Disable Automatic Id Generation: If every document toobe imported contains an id field, then selecting this option can increase performance.</span></span> <span data-ttu-id="6bc1b-362">Документы без поля уникального идентификатора не будут импортированы.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-362">Documents missing a unique id field will not be imported.</span></span>
3. <span data-ttu-id="6bc1b-363">Обновление существующие документы: hello средство toonot значения по умолчанию, заменив существующие документы конфликтов идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-363">Update Existing Documents: hello tool defaults toonot replacing existing documents with id conflicts.</span></span> <span data-ttu-id="6bc1b-364">При выборе этого параметра существующие документы с совпадающими идентификаторами будут перезаписываться.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-364">Selecting this option will allow overwriting existing documents with matching ids.</span></span> <span data-ttu-id="6bc1b-365">Эта функция пригодится для плановых миграций, которые используются для обновления существующих документов.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-365">This feature is useful for scheduled data migrations that update existing documents.</span></span>
4. <span data-ttu-id="6bc1b-366">Число повторных попыток в случае неудачи: задает hello число tooretry hello tooAzure подключения Cosmos DB в случае временного сбоя (например прерывания подключений сети).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-366">Number of Retries on Failure: Specifies hello number of times tooretry hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
5. <span data-ttu-id="6bc1b-367">Интервал повтора: Указывает, сколько времени toowait между повторная попытка подключения hello tooAzure Cosmos DB в случае временного сбоя (например прерывания подключений сети).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-367">Retry Interval: Specifies how long toowait between retrying hello connection tooAzure Cosmos DB in case of transient failures (e.g. network connectivity interruption).</span></span>
6. <span data-ttu-id="6bc1b-368">Режим подключения: Указывает режим toouse hello соединения с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-368">Connection Mode: Specifies hello connection mode toouse with Azure Cosmos DB.</span></span> <span data-ttu-id="6bc1b-369">доступны следующие возможности Hello: DirectTcp, DirectHttps и шлюз.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-369">hello available choices are DirectTcp, DirectHttps, and Gateway.</span></span> <span data-ttu-id="6bc1b-370">режимы Hello прямое подключение являются быстрее, а режим hello шлюза — понятное дополнительные брандмауэра, как только он использует порт 443.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-370">hello direct connection modes are faster, while hello gateway mode is more firewall friendly as it only uses port 443.</span></span>

![Снимок экрана: дополнительные параметры последовательного импорта записей Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> <span data-ttu-id="6bc1b-372">Hello импортировать режим tooconnection значения по умолчанию средство DirectTcp.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-372">hello import tool defaults tooconnection mode DirectTcp.</span></span> <span data-ttu-id="6bc1b-373">При возникновении неполадок брандмауэра режима tooconnection шлюза, для его выполнения требуется только порт 443.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-373">If you experience firewall issues, switch tooconnection mode Gateway, as it only requires port 443.</span></span>
> 
> 

## <span data-ttu-id="6bc1b-374"><a id="IndexingPolicy"></a>Указание политики индексирования при создании коллекций Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6bc1b-374"><a id="IndexingPolicy"></a>Specify an indexing policy when creating Azure Cosmos DB collections</span></span>
<span data-ttu-id="6bc1b-375">Когда во время импорта коллекций toocreate средства позволяют hello миграции, можно указать политику индексации hello hello коллекций.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-375">When you allow hello migration tool toocreate collections during import, you can specify hello indexing policy of hello collections.</span></span> <span data-ttu-id="6bc1b-376">В hello Дополнительные параметры раздела hello Azure Cosmos DB массового импорта и параметры Azure Cosmos DB последовательной записи перейдите на раздел toohello политики индексирования.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-376">In hello advanced options section of hello Azure Cosmos DB Bulk import and Azure Cosmos DB Sequential record options, navigate toohello Indexing Policy section.</span></span>

![Снимок экрана: дополнительные параметры политики индексации Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

<span data-ttu-id="6bc1b-378">С помощью hello индексирования политики расширенный параметр, вы можно выберите файл политики индексирования, вручную введите политикой индексирования или выбрать один из шаблонов по умолчанию (щелкнув правой hello индексирования политики текстовое поле).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-378">Using hello Indexing Policy advanced option, you can select an indexing policy file, manually enter an indexing policy, or select from a set of default templates (by right clicking in hello indexing policy textbox).</span></span>

<span data-ttu-id="6bc1b-379">Hello политики предоставляет средство hello содержит:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-379">hello policy templates hello tool provides are:</span></span>

* <span data-ttu-id="6bc1b-380">По умолчанию.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-380">Default.</span></span> <span data-ttu-id="6bc1b-381">Эта политика лучше всего подходит при выполнении запросов равенства строк и использовании предложения ORDER BY, диапазона и запросов равенства для чисел.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-381">This policy is best when you’re performing equality queries against strings and using ORDER BY, range, and equality queries for numbers.</span></span> <span data-ttu-id="6bc1b-382">Эта политика имеет более низкий индекс служебных данных хранилища, чем "Диапазон".</span><span class="sxs-lookup"><span data-stu-id="6bc1b-382">This policy has a lower index storage overhead than Range.</span></span>
* <span data-ttu-id="6bc1b-383">Диапазон.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-383">Range.</span></span> <span data-ttu-id="6bc1b-384">Эта политика лучше всего подходит при использовании предложения ORDER BY, диапазона и запросов равенства на числах и строках.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-384">This policy is best you’re using ORDER BY, range and equality queries on both numbers and strings.</span></span> <span data-ttu-id="6bc1b-385">Эта политика имеет более высокий индекс служебных данных хранилища, чем "По умолчанию" или "Хэш".</span><span class="sxs-lookup"><span data-stu-id="6bc1b-385">This policy has a higher index storage overhead than Default or Hash.</span></span>

![Снимок экрана: дополнительные параметры политики индексации Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> <span data-ttu-id="6bc1b-387">Если политика индексирования не указан, будут применены политика по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-387">If you do not specify an indexing policy, then hello default policy will be applied.</span></span> <span data-ttu-id="6bc1b-388">Дополнительные сведения о политиках индексации Azure Cosmos DB см. в [этой статье](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-388">For more information about indexing policies, see [Azure Cosmos DB indexing policies](indexing-policies.md).</span></span>
> 
> 

## <a name="export-toojson-file"></a><span data-ttu-id="6bc1b-389">Файл экспорта tooJSON</span><span class="sxs-lookup"><span data-stu-id="6bc1b-389">Export tooJSON file</span></span>
<span data-ttu-id="6bc1b-390">Программа экспорта Hello Azure Cosmos DB JSON позволяет tooexport любой hello доступные исходные параметры tooa JSON-файл, содержащий массив документов JSON.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-390">hello Azure Cosmos DB JSON exporter allows you tooexport any of hello available source options tooa JSON file that contains an array of JSON documents.</span></span> <span data-ttu-id="6bc1b-391">Hello средство будет обрабатывать hello экспорта для вас, или можно выбрать команды tooview hello полученный миграции и выполните команду hello, самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-391">hello tool will handle hello export for you, or you can choose tooview hello resulting migration command and run hello command yourself.</span></span> <span data-ttu-id="6bc1b-392">Hello полученный файл JSON может храниться локально или в хранилище больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-392">hello resulting JSON file may be stored locally or in Azure Blob storage.</span></span>

![Снимок экрана: параметры экспорта в локальный файл Azure Cosmos DB JSON](./media/import-data/jsontarget.png)

![Снимок экрана: параметр экспорта в хранилище BLOB-объектов Azure Cosmos DB JSON](./media/import-data/jsontarget2.png)

<span data-ttu-id="6bc1b-395">При необходимости вы можете tooprettify hello, возникающие в JSON, что увеличивает размер hello hello итоговый документ во время внесения hello содержимое более удобной для чтения.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-395">You may optionally choose tooprettify hello resulting JSON, which will increase hello size of hello resulting document while making hello contents more human readable.</span></span>

    Standard JSON export
    [{"id":"Sample","Title":"About Paris","Language":{"Name":"English"},"Author":{"Name":"Don","Location":{"City":"Paris","Country":"France"}},"Content":"Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.","PageViews":10000,"Topics":[{"Title":"History of Paris"},{"Title":"Places toosee in Paris"}]}]

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
    "Content": "Don's document in Azure Cosmos DB is a valid JSON document as defined by hello JSON spec.",
    "PageViews": 10000,
    "Topics": [
      {
        "Title": "History of Paris"
      },
      {
        "Title": "Places toosee in Paris"
      }
    ]
    }]

## <a name="advanced-configuration"></a><span data-ttu-id="6bc1b-396">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="6bc1b-396">Advanced configuration</span></span>
<span data-ttu-id="6bc1b-397">На экране настройки дополнительных hello укажите расположение hello hello журнала файла toowhich хотелось бы записываются ошибки.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-397">In hello Advanced configuration screen, specify hello location of hello log file toowhich you would like any errors written.</span></span> <span data-ttu-id="6bc1b-398">Hello следующие правила применяются toothis страницы.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-398">hello following rules apply toothis page:</span></span>

1. <span data-ttu-id="6bc1b-399">Если имя файла не указано, все ошибки будет возвращаться на странице результатов hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-399">If a file name is not provided, then all errors will be returned on hello Results page.</span></span>
2. <span data-ttu-id="6bc1b-400">Если имя файла указано без каталога, затем hello файла будет быть создан (или перезаписан) в текущем каталоге среды hello.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-400">If a file name is provided without a directory, then hello file will be created (or overwritten) in hello current environment directory.</span></span>
3. <span data-ttu-id="6bc1b-401">Если выбрать существующий файл, а затем hello файл будет перезаписан, нет возможности добавления.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-401">If you select an existing file, then hello file will be overwritten, there is no append option.</span></span>

<span data-ttu-id="6bc1b-402">Затем выберите ли все toolog критического или сообщения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-402">Then, choose whether toolog all, critical, or no error messages.</span></span> <span data-ttu-id="6bc1b-403">Наконец решите, как часто hello на экране передачи сообщений будет обновляться ход его выполнения.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-403">Finally, decide how frequently hello on screen transfer message will be updated with its progress.</span></span>

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a><span data-ttu-id="6bc1b-404">Подтверждение параметров импорта и просмотр командной строки</span><span class="sxs-lookup"><span data-stu-id="6bc1b-404">Confirm import settings and view command line</span></span>
1. <span data-ttu-id="6bc1b-405">После указания сведений об источнике информации о целевой и расширенной конфигурации, изучите Сводка по миграции hello и, при необходимости, представление или копирования hello, возникающие в команды миграции (копирование hello команда является полезным tooautomate операций импорта).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-405">After specifying source information, target information, and advanced configuration, review hello migration summary and, optionally, view/copy hello resulting migration command (copying hello command is useful tooautomate import operations):</span></span>
   
    ![Снимок экрана: окно сводки](./media/import-data/summary.png)
   
    ![Снимок экрана: окно сводки](./media/import-data/summarycommand.png)
2. <span data-ttu-id="6bc1b-408">После проверки источника и назначения нажмите кнопку **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-408">Once you’re satisfied with your source and target options, click **Import**.</span></span> <span data-ttu-id="6bc1b-409">как в процессе импорта hello обновит Hello затраченное время, число переданных и сведения о сбое (если не указать имя файла в расширенной конфигурации hello).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-409">hello elapsed time, transferred count, and failure information (if you didn't provide a file name in hello Advanced configuration) will update as hello import is in process.</span></span> <span data-ttu-id="6bc1b-410">После завершения можно экспортировать результаты hello (например toodeal сбоев импорта).</span><span class="sxs-lookup"><span data-stu-id="6bc1b-410">Once complete, you can export hello results (e.g. toodeal with any import failures).</span></span>
   
    ![Снимок экрана: параметры экспорта в Azure Cosmos DB JSON](./media/import-data/viewresults.png)
3. <span data-ttu-id="6bc1b-412">Можно также запустить новый импорт хранение hello существующих параметров (например, выбор сведения, источник и целевой строки подключения, т. д.) или сброс всех значений.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-412">You may also start a new import, either keeping hello existing settings (e.g. connection string information, source and target choice, etc.) or resetting all values.</span></span>
   
    ![Снимок экрана: параметры экспорта в Azure Cosmos DB JSON](./media/import-data/newimport.png)

## <a name="next-steps"></a><span data-ttu-id="6bc1b-414">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6bc1b-414">Next steps</span></span>

<span data-ttu-id="6bc1b-415">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="6bc1b-415">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bc1b-416">Установить средство переноса данных hello</span><span class="sxs-lookup"><span data-stu-id="6bc1b-416">Installed hello Data Migration tool</span></span>
> * <span data-ttu-id="6bc1b-417">импорт данных из разных источников данных;</span><span class="sxs-lookup"><span data-stu-id="6bc1b-417">Imported data from different data sources</span></span>
> * <span data-ttu-id="6bc1b-418">Экспортированный из Azure Cosmos DB tooJSON</span><span class="sxs-lookup"><span data-stu-id="6bc1b-418">Exported from Azure Cosmos DB tooJSON</span></span>

<span data-ttu-id="6bc1b-419">Теперь можно продолжить toohello следующее руководство и узнайте, как tooquery данных с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6bc1b-419">You can now proceed toohello next tutorial and learn how tooquery data using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="6bc1b-420">Как tooquery данных?</span><span class="sxs-lookup"><span data-stu-id="6bc1b-420">How tooquery data?</span></span>](../cosmos-db/tutorial-query-documentdb.md)
