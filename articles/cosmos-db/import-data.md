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
# <a name="how-tooimport-data-into-azure-cosmos-db-for-hello-documentdb-api"></a>Как tooimport данных в базе данных Azure Cosmos для hello DocumentDB API?

В этом учебнике содержатся инструкции по использованию hello Azure Cosmos DB: инструмент переноса данных API DocumentDB, который можно импортировать данные из различных источников, включая файлы JSON, CSV файлы SQL, MongoDB, хранилище таблиц Azure, Amazon DynamoDB и Azure Cosmos DB DocumentDB Коллекций API в коллекции для использования с Azure Cosmos DB и hello DocumentDB API. также можно использовать средство переноса данных Hello, при миграции из коллекции несколькими разделами коллекции tooa одну секцию для hello DocumentDB API.

Средство переноса данных Hello работает только в том случае, если импорт данных в базу данных Cosmos Azure для использования с hello DocumentDB API. Импорт данных для использования с hello API таблиц или Graph API в настоящее время не поддерживается. 

tooimport данных для использования с hello MongoDB API. в статье [Azure Cosmos DB: как toomigrate данные для hello MongoDB API?](mongodb-migrate.md).

В этом учебнике hello следующие задачи:

> [!div class="checklist"]
> * Установка средства переноса данных hello
> * импорт данных из разных источников данных;
> * Экспорт из Azure Cosmos DB tooJSON

## <a id="Prerequisites"></a>Предварительные требования
Перед выполнением инструкции hello в этой статье, убедитесь, что установлены следующие компоненты hello:

* [Microsoft .NET Framework 4.51](https://www.microsoft.com/download/developer-tools.aspx) или более поздняя версия.

## <a id="Overviewl"></a>Обзор средства переноса данных hello
Средство переноса данных Hello — это решение открытым исходным кодом, которое импортирует данные tooAzure Cosmos DB из разнообразных источников, включая:

* файлы JSON;
* MongoDB
* SQL Server
* СЫМ-файлы;
* табличное хранилище Azure;
* Amazon DynamoDB
* HBase
* коллекции Azure Cosmos DB.

Хотя средство импорта hello включает графический интерфейс пользователя (dtui.exe), его также можно управлять из командной строки hello (dt.exe). На самом деле присутствует команда hello связанный параметр toooutput после настройки импорта через hello пользовательского интерфейса. Табличный источник данных (например, SQL Server или CSV-файлы) можно преобразовать так, чтобы создать иерархические связи (вложенные документы) во время импорта. Сохраните чтения toolearn больше о параметрах источника, образец tooimport командные строки из каждого источника, target-параметры и при просмотре Импорт результатов.

## <a id="Install"></a>Установка средства миграции данных hello
Hello миграции средство исходный код доступен на GitHub в [этот репозиторий](https://github.com/azure/azure-documentdb-datamigrationtool) и скомпилированная версия доступна в [центра загрузки Майкрософт](http://www.microsoft.com/downloads/details.aspx?FamilyID=cda7703a-2774-4c07-adcc-ad02ddc1a44d). Может либо компиляции решения hello, или просто загрузите и извлеките hello скомпилированная версия tooa каталога по своему усмотрению. Затем запустите:

* **Dtui.exe**: графический интерфейс версия средства hello
* **DT.exe**: версией hello инструмента командной строки

## <a name="import-data"></a>Импорт данных

После установки средство hello, это время tooimport данных. Тип данных действительно tooimport?

* [файлы JSON](#JSON);
* [MongoDB](#MongoDB)
* [файлы экспорта MongoDB](#MongoDBExport);
* [SQL Server](#SQL)
* [CSV-файлы](#CSV);
* [Хранилище таблиц Azure](#AzureTableSource)
* [Amazon DynamoDB](#DynamoDBSource);
* [Большой двоичный объект](#BlobImport)
* [коллекции Azure Cosmos DB](#DocumentDBSource);
* [HBase](#HBaseSource)
* [массовый импорт Azure Cosmos DB](#DocumentDBBulkImport);
* [последовательный импорт записей Azure Cosmos DB](#DocumentDSeqTarget).


## <a id="JSON"></a>tooimport JSON-файлов
Hello параметр импортера исходный файл JSON можно tooimport один или более одного документа JSON-файлов или массив JSON документов, содержащих файлы JSON. При добавлении папки, содержащие файлы tooimport JSON, предусмотрена возможность hello рекурсивный поиск файлов во вложенных папках.

![Снимок экрана: параметры исходного файла JSON — средства миграции базы данных](./media/import-data/jsonsource.png)

Ниже приведены некоторые файлы JSON tooimport образцы командной строки.

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

## <a id="MongoDB"></a>tooimport из MongoDB

> [!IMPORTANT]
> При импорте учетной записи Azure Cosmos DB tooan с поддержкой MongoDB, выполните следующие [инструкции](mongodb-migrate.md).
> 
> 

Hello MongoDB источника импорта параметр позволяет вам tooimport из отдельных MongoDB коллекции и при необходимости отфильтруйте документы с помощью запроса или изменить структуру документа hello с помощью проекции.  

![Снимок экрана параметров источника MongoDB](./media/import-data/mongodbsource.png)

в стандартном формате MongoDB hello указана строка подключения Hello:

    mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database>

> [!NOTE]
> Команда используйте hello проверьте tooensure, hello MongoDB экземпляр, указанный в поле Строка hello подключения может осуществляться.
> 
> 

Введите имя hello hello коллекции, из которого будут импортированы данные. Можно при необходимости укажите или указать файл для запроса (например {pop: {$gt: 5000}}) или проекции (например {loc:0}) tooboth фильтра и форма hello данных toobe импортированы.

Ниже приведены некоторые tooimport образцы командной строки из MongoDB.

    #Import all documents from a MongoDB collection
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZips /t.IdField:_id /t.CollectionThroughput:2500

    #Import documents from a MongoDB collection which match hello query and exclude hello loc field
    dt.exe /s:MongoDB /s.ConnectionString:mongodb://<dbuser>:<dbpassword>@<host>:<port>/<database> /s.Collection:zips /s.Query:{pop:{$gt:50000}} /s.Projection:{loc:0} /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:BulkZipsTransform /t.IdField:_id/t.CollectionThroughput:2500

## <a id="MongoDBExport"></a>файлы экспорта MongoDB tooimport

> [!IMPORTANT]
> При импорте учетной записи Azure Cosmos DB tooan с поддержкой MongoDB, выполните следующие [инструкции](mongodb-migrate.md).
> 
> 

Hello MongoDB JSON файл источника импорта экспорте позволяет tooimport одного или нескольких файлов JSON, полученных из служебной программы mongoexport hello.  

![Снимок экрана параметров экспорта MongoDB](./media/import-data/mongodbexportsource.png)

При добавлении папки, содержащие файлы JSON MongoDB экспорта для импорта, предусмотрена возможность hello рекурсивный поиск файлов во вложенных папках.

Ниже приведен tooimport пример командной строки из экспорта MongoDB JSON-файлов.

    dt.exe /s:MongoDBExport /s.Files:D:\mongoemployees.json /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:employees /t.IdField:_id /t.Dates:Epoch /t.CollectionThroughput:2500

## <a id="SQL"></a>tooimport из SQL Server
Hello параметра импорта источника SQL дает tooimport из отдельной базы данных SQL Server и при необходимости отфильтруйте toobe записей hello, импортированные с помощью запроса. Кроме того можно изменить структуру документа hello, указав разделитель вложения (Подробнее об этом позже).  

![Снимок экрана: параметры источника SQL — средства миграции базы данных](./media/import-data/sqlexportsource.png)

Hello формат строки соединения hello является hello standard SQL соединения строки.

> [!NOTE]
> Команда используйте hello проверьте tooensure, экземпляр SQL Server, указанной в поле Строка подключения hello hello возможен.
> 
> 

вложенные свойства разделителя Hello — иерархические связи используется toocreate (вложенные документы) во время импорта. Рассмотрим следующий SQL-запрос hello.

*select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'*

Выдаются следующие результаты (разделяемый) hello:

![Снимок экрана: результаты запроса SQL](./media/import-data/sqlqueryresults.png)

Обратите внимание, псевдонимы hello, такие как Address.AddressType и Address.Location.StateProvinceName. Указав разделитель вложения из '.', средство импорта hello создает адрес и импортировать Address.Location вложенные документы во время hello. Ниже приведен пример полученного документа в Azure Cosmos DB.

*{ "id": "956", "Name": "Finer Sales and Service", "Address": { "AddressType": "Main Office", "AddressLine1": "#500-75 O'Connor Street", "Location": { "City": "Ottawa", "StateProvinceName": "Ontario" }, "PostalCode": "K4B 1S2", "CountryRegionName": "Canada" } }*

Ниже приведены некоторые tooimport образцы командной строки из SQL Server.

    #Import records from SQL which match a query
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, * from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Stores /t.IdField:Id /t.CollectionThroughput:2500

    #Import records from sql which match a query and create hierarchical relationships
    dt.exe /s:SQL /s.ConnectionString:"Data Source=<server>;Initial Catalog=AdventureWorks;User Id=advworks;Password=<password>;" /s.Query:"select CAST(BusinessEntityID AS varchar) as Id, Name, AddressType as [Address.AddressType], AddressLine1 as [Address.AddressLine1], City as [Address.Location.City], StateProvinceName as [Address.Location.StateProvinceName], PostalCode as [Address.PostalCode], CountryRegionName as [Address.CountryRegionName] from Sales.vStoreWithAddresses WHERE AddressType='Main Office'" /s.NestingSeparator:. /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:StoresSub /t.IdField:Id /t.CollectionThroughput:2500

## <a id="CSV"></a>CSV-файлы tooimport и convert CSV tooJSON
Hello параметр импортера исходного файла CSV позволяет вам tooimport один или несколько файлов CSV. При добавлении папки, содержащие CSV-файлы для импорта, предусмотрена возможность hello рекурсивный поиск файлов во вложенных папках.

![Параметры источника экрана CSV - CSV tooJSON](media/import-data/csvsource.png)

Аналогичные toohello SQL, вложенные свойства разделителя hello возможно, источник иерархические связи используется toocreate (вложенные документы) во время импорта. Рассмотрим hello строку заголовка CSV-файла и строк данных.

![Снимок экрана CSV образец записи - CSV tooJSON](./media/import-data/csvsample.png)

Обратите внимание, псевдонимы hello, такие как DomainInfo.Domain_Name и RedirectInfo.Redirecting. Указав разделитель вложения из '.', средство импорта hello создаст DomainInfo и импортировать RedirectInfo вложенные документы во время hello. Ниже приведен пример полученного документа в Azure Cosmos DB.

*{«DomainInfo»: {«Имя_домена»: «ACUS.GOV», «Domain_Name_Address»: «http://www. ACUS.GOV»}, «Федеральным агентство»: «Административные конференции; hello United States», «RedirectInfo»: {«Перенаправление»: «0», «Redirect_Destination»: «»}, «id»: «9cc565c5-ebcd-1c03-ebd3-cc3e2ecd814d»}*

Средство импорта Hello попытается tooinfer сведения о типе значений без кавычек в CSV-файлы (заключенные в кавычки значения всегда обрабатываются как строки).  Типы различаются по hello следующий порядок: номер, datetime, boolean.  

Существует два toonote вещей о импорта CSV.

1. По умолчанию значения, не заключенные в кавычки, очищаются от табуляции и пробелов, а значения, заключенные в кавычки, остаются в нетронутом виде. Это поведение можно переопределить с приветствия Trim значения флажок hello /s.TrimQuoted параметр командной строки или в кавычках.
2. По умолчанию объект null, не заключенный в кавычки, считается значением null. Это поведение можно переопределить (т. е. обрабатывают без кавычек значение null как строка «null») с hello интерпретирует NULL как строка флажок hello /s.NoUnquotedNulls параметр командной строки или без кавычек.

Далее показан пример команды для импорта CSV:

    dt.exe /s:CsvFile /s.Files:.\Employees.csv /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:Employees /t.IdField:EntityID /t.CollectionThroughput:2500

## <a id="AzureTableSource"></a>tooimport из хранилища таблиц Azure
Hello параметра импорта источника хранилища таблиц Azure позволяет вам tooimport из отдельной таблицы хранилища таблиц Azure и при необходимости отфильтруйте hello таблицы сущности toobe импортированы. Обратите внимание, нельзя использовать данные хранилища Azure Table tooimport средство hello переноса данных в базу данных Cosmos Azure для использования с hello API таблиц. В настоящее время поддерживается только импорт tooAzure Cosmos DB для использования с hello DocumentDB API.

![Снимок экрана: параметры источника табличного хранилища Azure](./media/import-data/azuretablesource.png)

Hello объекта hello строки подключения к хранилищу таблиц Azure выглядит следующим образом:

    DefaultEndpointsProtocol=<protocol>;AccountName=<Account Name>;AccountKey=<Account Key>;

> [!NOTE]
> Команда используйте hello проверьте tooensure, hello экземпляра хранилища Azure таблицы, указанной в поле Строка подключения hello возможен.
> 
> 

Введите имя hello hello Azure таблицы, из которого будут импортированы данные. При необходимости можно указать [фильтра](https://msdn.microsoft.com/library/azure/ff683669.aspx).

Hello параметра импорта источника хранилища таблиц Azure имеет hello следующие дополнительные параметры:

1. Включить внутренние поля
   1. All — включить все внутренние поля (PartitionKey, RowKey и Timestamp)
   2. None — исключить все внутренние поля
   3. RowKey - содержать только поля RowKey hello
2. Выбор столбцов
   1. Фильтры табличного хранилища Azure не поддерживают проекции. Если требуется, чтобы свойства сущности определенных таблиц Azure tooonly импорта, их можно добавьте список toohello Выбор столбцов. Все другие свойства сущностей будут игнорироваться.

Ниже приведен tooimport пример командной строки из хранилища Azure Table.

    dt.exe /s:AzureTable /s.ConnectionString:"DefaultEndpointsProtocol=https;AccountName=<Account Name>;AccountKey=<Account Key>" /s.Table:metrics /s.InternalFields:All /s.Filter:"PartitionKey eq 'Partition1' and RowKey gt '00001'" /s.Projection:ObjectCount;ObjectSize  /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:metrics /t.CollectionThroughput:2500

## <a id="DynamoDBSource"></a>tooimport из Amazon DynamoDB
Hello Amazon DynamoDB источника импорта параметр дает tooimport из отдельной таблицы Amazon DynamoDB и при необходимости отфильтруйте toobe сущностей hello импортированы. Чтобы максимально упростить настройку импорта, представлено несколько шаблонов.

![Снимок экрана: параметры источника DynamoDB Amazon — средства миграции базы данных](./media/import-data/dynamodbsource1.png)

![Снимок экрана: параметры источника DynamoDB Amazon — средства миграции базы данных](./media/import-data/dynamodbsource2.png)

Hello из строки подключения Amazon DynamoDB hello выглядит следующим образом:

    ServiceURL=<Service Address>;AccessKey=<Access Key>;SecretKey=<Secret Key>;

> [!NOTE]
> Команда используйте hello проверьте tooensure, hello экземпляр Amazon DynamoDB, указанный в поле Строка подключения hello возможен.
> 
> 

Ниже приведен tooimport пример командной строки из Amazon DynamoDB.

    dt.exe /s:DynamoDB /s.ConnectionString:ServiceURL=https://dynamodb.us-east-1.amazonaws.com;AccessKey=<accessKey>;SecretKey=<secretKey> /s.Request:"{   """TableName""": """ProductCatalog""" }" /t:DocumentDBBulk /t.ConnectionString:"AccountEndpoint=<Azure Cosmos DB Endpoint>;AccountKey=<Azure Cosmos DB Key>;Database=<Azure Cosmos DB Database>;" /t.Collection:catalogCollection /t.CollectionThroughput:2500

## <a id="BlobImport"></a>tooimport файлы из хранилища больших двоичных объектов Azure
Hello JSON-файл, файл экспорта MongoDB и параметры импорта исходного файла CSV позволяют tooimport один или несколько файлов из хранилища больших двоичных объектов Azure. После указания URL-адрес контейнера больших двоичных объектов и ключ учетной записи, достаточно просто укажите tooimport файлов hello tooselect регулярного выражения.

![Снимок экрана: параметры исходного файла больших двоичных объектов](./media/import-data/blobsource.png)

Вот файлы JSON tooimport пример командной строки из хранилища больших двоичных объектов Azure.

    dt.exe /s:JsonFile /s.Files:"blobs://<account key>@account.blob.core.windows.net:443/importcontainer/.*" /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:doctest

## <a id="DocumentDBSource"></a>tooimport из коллекции Azure Cosmos DB DocumentDB API
Hello Azure Cosmos DB источника импорта параметр дает tooimport данные из одной или нескольких коллекциях Azure Cosmos DB и при необходимости отфильтруйте документы с помощью запроса.  

![Снимок экрана: параметры источника Azure Cosmos DB](./media/import-data/documentdbsource.png)

Hello объекта hello Azure Cosmos DB строка подключения выглядит следующим образом:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Строка подключения учетной записи Azure Cosmos DB Hello могут быть получены из колонке ключи hello hello портал Azure, как описано в [как toomanage учетную запись Azure Cosmos DB](manage-account.md), однако имя hello hello базы данных должно toohello toobe добавляется Строка подключения в hello следующий формат:

    Database=<CosmosDB Database>;

> [!NOTE]
> Команда используйте hello проверьте tooensure, hello Azure Cosmos DB экземпляр, указанный в поле Строка hello подключения может осуществляться.
> 
> 

tooimport из одной коллекции Azure Cosmos DB, введите имя hello hello коллекции, из которого будут импортированы данные. tooimport из нескольких коллекций Azure Cosmos DB предоставляют toomatch регулярное выражение одно или несколько имен коллекции (например collection01 | collection02 | collection03). При необходимости может указать, или указать файл для фильтра запросов tooboth и toobe данных hello импортировать фигуры.

> [!NOTE]
> Так как поле коллекции hello принимает регулярные выражения при импорте из одной коллекции, имя которого содержит знаки регулярного выражения, затем эти знаки необходимо экранировать соответствующим образом.
> 
> 

Hello Azure Cosmos DB источника импорта параметр имеет hello следующие дополнительные параметры:

1. Включить внутренние поля: Задает ли свойства системы tooinclude Azure Cosmos DB документа в hello экспорта (например _rid, _ts).
2. Число повторных попыток в случае неудачи: задает hello число tooretry hello tooAzure подключения Cosmos DB в случае временного сбоя (например прерывания подключений сети).
3. Интервал повтора: Указывает, сколько времени toowait между повторная попытка подключения hello tooAzure Cosmos DB в случае временного сбоя (например прерывания подключений сети).
4. Режим подключения: Указывает режим toouse hello соединения с Azure Cosmos DB. доступны следующие возможности Hello: DirectTcp, DirectHttps и шлюз. режимы Hello прямое подключение являются быстрее, а режим hello шлюза — понятное дополнительные брандмауэра, как только он использует порт 443.

![Снимок экрана: дополнительные параметры источника Azure Cosmos DB](./media/import-data/documentdbsourceoptions.png)

> [!TIP]
> Hello импортировать режим tooconnection значения по умолчанию средство DirectTcp. При возникновении неполадок брандмауэра режима tooconnection шлюза, для его выполнения требуется только порт 443.
> 
> 

Ниже приведены некоторые tooimport образцы командной строки из базы данных Azure Cosmos.

    #Migrate data from one Azure Cosmos DB collection tooanother Azure Cosmos DB collections
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:TEColl /t:CosmosDBBulk /t.ConnectionString:" AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:TESessions /t.CollectionThroughput:2500

    #Migrate data from multiple Azure Cosmos DB collections tooa single Azure Cosmos DB collection
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:comp1|comp2|comp3|comp4 /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:singleCollection /t.CollectionThroughput:2500

    #Export an Azure Cosmos DB collection tooa JSON file
    dt.exe /s:CosmosDB /s.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /s.Collection:StoresSub /t:JsonFile /t.File:StoresExport.json /t.Overwrite /t.CollectionThroughput:2500

> [!TIP]
> Средство импорта Azure Cosmos DB данных Hello также поддерживает импорт данных из hello [DB эмулятор Azure Cosmos](local-emulator.md). При импорте данных из локального эмулятора, задать конечную точку hello слишком`https://localhost:<port>`. 
> 
> 

## <a id="HBaseSource"></a>tooimport из HBase
Hello HBase источника импорта параметр дает tooimport данных из таблицы HBase и при необходимости отфильтруйте данные hello. Чтобы максимально упростить настройку импорта, представлено несколько шаблонов.

![Снимок экрана: параметры источника HBase](./media/import-data/hbasesource1.png)

![Снимок экрана: параметры источника HBase](./media/import-data/hbasesource2.png)

имеет формат Hello hello строка подключения HBase Stargate:

    ServiceURL=<server-address>;Username=<username>;Password=<password>

> [!NOTE]
> Команда используйте hello проверьте tooensure, hello HBase экземпляр, указанный в поле Строка hello подключения может осуществляться.
> 
> 

Ниже приведен tooimport пример командной строки из HBase:

    dt.exe /s:HBase /s.ConnectionString:ServiceURL=<server-address>;Username=<username>;Password=<password> /s.Table:Contacts /t:CosmosDBBulk /t.ConnectionString:"AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;" /t.Collection:hbaseimport

## <a id="DocumentDBBulkTarget"></a>tooimport toohello API DocumentDB (массового импорта)
Hello Azure Cosmos DB массового импорта позволяет tooimport из любой из параметров hello доступный источник, с помощью Azure DB Cosmos хранимые процедуры для повышения эффективности. Средство Hello поддерживает коллекцию Azure Cosmos DB секционированную одним tooone импорта, а также сегментированных импорта, при котором данные секционируются в различных коллекциях секционированную одним Azure Cosmos DB. Дополнительные сведения о секционировании данных см. в статье о [секционировании и масштабировании в Azure Cosmos DB](partition-data.md). Hello средство создания, выполнения и удалите hello хранимой процедуры из коллекций целевой hello.  

![Снимок экрана: параметры массового импорта Azure Cosmos DB](./media/import-data/documentdbbulk.png)

Hello объекта hello Azure Cosmos DB строка подключения выглядит следующим образом:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Строка подключения учетной записи Azure Cosmos DB Hello могут быть получены из колонке ключи hello hello портал Azure, как описано в [как toomanage учетную запись Azure Cosmos DB](manage-account.md), однако имя hello hello базы данных должно toohello toobe добавляется Строка подключения в hello следующий формат:

    Database=<CosmosDB Database>;

> [!NOTE]
> Команда используйте hello проверьте tooensure, hello Azure Cosmos DB экземпляр, указанный в поле Строка hello подключения может осуществляться.
> 
> 

tooimport tooa один коллекцию, введите имя hello hello toowhich коллекции данных будут импортированы и нажмите кнопку "Добавить" hello ". коллекции toomultiple tooimport, введите имя каждой коллекции отдельно или используйте следующий синтаксис toospecify hello несколько коллекций: *collection_prefix*[начальный индекс - конечный индекс]. При указании нескольких коллекций hello упомянутой выше синтаксис, учитывайте следующие hello.

1. Поддерживаются только шаблоны имени диапазона целых чисел. Например, указав коллекцию [0-3] сформирует hello следующие коллекции: collection0 collection1 collection2 collection3.
2. Вы можете использовать сокращенный синтаксис: если ввести collection[3], будет отображен тот же набор коллекций, что и на этапе 1.
3. Вы можете указать несколько подстановок. Например, коллекция [0–1] [0–9] создаст 20 имен коллекций с нулем в начале (collection01… 02… 03).

Как только hello коллекции имена были заданы, выберите hello необходимой пропускной способности hello коллекций (400 RUs too10, 000 RUs). Для повышения производительности выберите большее значение. Дополнительные сведения об уровнях производительности в Azure Cosmos DB см. в [этой статье](performance-levels.md).

> [!NOTE]
> параметр пропускную способность производительности Hello применяется только toocollection создания. Если указан hello коллекция уже существует, ее пропускная способность останутся без изменений.
> 
> 

При импорте toomultiple коллекций, средство импорта hello поддерживает сегментирования на основе хэша. В этом случае укажите hello свойство документа, нужно toouse как hello ключ секционирования (если ключ раздела оставлено пустым, документы будут иметь сегментированных случайным образом в коллекциях целевой hello).

При необходимости указать, какие поля в источнике импорта hello следует использовать в качестве hello Azure Cosmos DB свойство идентификатора документа во время импорта hello (Обратите внимание, что если это свойство не содержат документы, то средство импорта hello создаст GUID как значение свойства идентификатора hello).

Во время импорта доступны ряд дополнительных параметров. Во-первых при этом включает средство hello по умолчанию массового импорта хранимой процедуры (BulkInsert.js), вы можете toospecify импорта хранимой процедуры:

 ![Снимок экрана: параметр хранимой процедуры массового импорта Azure Cosmos DB](./media/import-data/bulkinsertsp.png)

Кроме того, при импорте типов даты (например, из SQL Server или MongoDB) можно выбрать три параметра импорта:

 ![Снимок экрана: параметры импорта даты и времени импорта Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* Строка: сохраняется как строковое значение.
* Эпоха: сохраняется как век числовое значение эпохи.
* Оба: сохраняются строковое значение и числовое значение эпохи. Этот параметр создает вложенный документ, например "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }

Hello Azure Cosmos DB массового импорта имеет hello следующие дополнительные расширенные параметры:

1. Размер пакета: hello средство значения по умолчанию tooa размер пакета равным 50.  Если импортировать toobe документы hello большие, понижать hello размер пакета. И наоборот Если импортировать toobe документы hello малы, рекомендуется обрабатывать hello размер пакета.
2. Сценарий максимальный размер (байт): hello средство по умолчанию используется размер max скрипта tooa 512 КБ
3. Отключить автоматическое создание идентификатора: Если каждый toobe документа импорта содержит поля id, затем при выборе этого параметра может повысить производительность. Документы без поля уникального идентификатора не будут импортированы.
4. Обновление существующие документы: hello средство toonot значения по умолчанию, заменив существующие документы конфликтов идентификаторов. При выборе этого параметра существующие документы с совпадающими идентификаторами будут перезаписываться. Эта функция пригодится для плановых миграций, которые используются для обновления существующих документов.
5. Число повторных попыток в случае неудачи: задает hello число tooretry hello tooAzure подключения Cosmos DB в случае временного сбоя (например прерывания подключений сети).
6. Интервал повтора: Указывает, сколько времени toowait между повторная попытка подключения hello tooAzure Cosmos DB в случае временного сбоя (например прерывания подключений сети).
7. Режим подключения: Указывает режим toouse hello соединения с Azure Cosmos DB. доступны следующие возможности Hello: DirectTcp, DirectHttps и шлюз. режимы Hello прямое подключение являются быстрее, а режим hello шлюза — понятное дополнительные брандмауэра, как только он использует порт 443.

![Снимок экрана: дополнительные параметры массового импорта Azure Cosmos DB](./media/import-data/docdbbulkoptions.png)

> [!TIP]
> Hello импортировать режим tooconnection значения по умолчанию средство DirectTcp. При возникновении неполадок брандмауэра режима tooconnection шлюза, для его выполнения требуется только порт 443.
> 
> 

## <a id="DocumentDBSeqTarget"></a>tooimport toohello API DocumentDB (Импорт последовательной записи)
Hello Azure Cosmos DB последовательной записи импорта позволяет tooimport из hello доступные исходные параметры на основе по одной записи. Можно выбрать этот параметр, если вы импортируете tooan существующую коллекцию, достигнута квота хранимых процедур. поддерживает импорт Hello средство tooa одиночными коллекции Azure Cosmos DB (одной секции и несколькими секции), а также сегментированных импорта, при котором данные секционируются в различных коллекциях Azure Cosmos DB одной секции и/или несколько секций. Дополнительные сведения о секционировании данных см. в статье о [секционировании и масштабировании в Azure Cosmos DB](partition-data.md).

![Снимок экрана: параметры последовательного импорта записей Azure Cosmos DB](./media/import-data/documentdbsequential.png)

Hello объекта hello Azure Cosmos DB строка подключения выглядит следующим образом:

    AccountEndpoint=<CosmosDB Endpoint>;AccountKey=<CosmosDB Key>;Database=<CosmosDB Database>;

Строка подключения учетной записи Azure Cosmos DB Hello могут быть получены из колонке ключи hello hello портал Azure, как описано в [как toomanage учетную запись Azure Cosmos DB](manage-account.md), однако имя hello hello базы данных должно toohello toobe добавляется Строка подключения в hello следующий формат:

    Database=<Azure Cosmos DB Database>;

> [!NOTE]
> Команда используйте hello проверьте tooensure, hello Azure Cosmos DB экземпляр, указанный в поле Строка hello подключения может осуществляться.
> 
> 

tooimport tooa один коллекцию, введите имя hello hello toowhich коллекции данных будут импортированы и нажмите кнопку "Добавить" hello ". коллекции toomultiple tooimport, введите имя каждой коллекции отдельно или используйте следующий синтаксис toospecify hello несколько коллекций: *collection_prefix*[начальный индекс - конечный индекс]. При указании нескольких коллекций hello упомянутой выше синтаксис, учитывайте следующие hello.

1. Поддерживаются только шаблоны имени диапазона целых чисел. Например, указав коллекцию [0-3] сформирует hello следующие коллекции: collection0 collection1 collection2 collection3.
2. Вы можете использовать сокращенный синтаксис: если ввести collection[3], будет отображен тот же набор коллекций, что и на этапе 1.
3. Вы можете указать несколько подстановок. Например, коллекция [0–1] [0–9] создаст 20 имен коллекций с нулем в начале (collection01… 02… 03).

Как только hello коллекции имена были заданы, выберите hello необходимой пропускной способности hello коллекций (400 RUs too250, 000 RUs). Для повышения производительности выберите большее значение. Дополнительные сведения об уровнях производительности в Azure Cosmos DB см. в [этой статье](performance-levels.md). Любой импортировать toocollections с пропускной способностью > 10 000 RUs потребуется ключ раздела. При выборе более 250 RUs toohave потребуется toofile запрос портала toohave hello, увеличивается вашей учетной записи.

> [!NOTE]
> пропускная способность приветствия применяется только toocollection создания. Если указан hello коллекция уже существует, ее пропускная способность останутся без изменений.
> 
> 

При импорте toomultiple коллекций, средство импорта hello поддерживает сегментирования на основе хэша. В этом случае укажите hello свойство документа, нужно toouse как hello ключ секционирования (если ключ раздела оставлено пустым, документы будут иметь сегментированных случайным образом в коллекциях целевой hello).

При необходимости указать, какие поля в источнике импорта hello следует использовать в качестве hello Azure Cosmos DB свойство идентификатора документа во время импорта hello (Обратите внимание, что если это свойство не содержат документы, то средство импорта hello создаст GUID как значение свойства идентификатора hello).

Во время импорта доступны ряд дополнительных параметров. При импорте типов даты (например, из SQL Server или MongoDB) можно выбрать три параметра импорта:

 ![Снимок экрана: параметры импорта даты и времени импорта Azure Cosmos DB](./media/import-data/datetimeoptions.png)

* Строка: сохраняется как строковое значение.
* Эпоха: сохраняется как век числовое значение эпохи.
* Оба: сохраняются строковое значение и числовое значение эпохи. Этот параметр создает вложенный документ, например "date_joined": { "Value": "2013-10-21T21:17:25.2410000Z", "Epoch": 1382390245 }

Hello Azure Cosmos DB - импортера последовательной записи имеет hello следующие дополнительные расширенные параметры:

1. Количество параллельных запросов: hello инструмент по умолчанию too2 параллельных запросов. Если импортировать toobe документы hello малы, рекомендуется обрабатывать hello число параллельных запросов. Обратите внимание, что если это число возникает слишком часто, hello импорта возможно возникновение регулирования.
2. Отключить автоматическое создание идентификатора: Если каждый toobe документа импорта содержит поля id, затем при выборе этого параметра может повысить производительность. Документы без поля уникального идентификатора не будут импортированы.
3. Обновление существующие документы: hello средство toonot значения по умолчанию, заменив существующие документы конфликтов идентификаторов. При выборе этого параметра существующие документы с совпадающими идентификаторами будут перезаписываться. Эта функция пригодится для плановых миграций, которые используются для обновления существующих документов.
4. Число повторных попыток в случае неудачи: задает hello число tooretry hello tooAzure подключения Cosmos DB в случае временного сбоя (например прерывания подключений сети).
5. Интервал повтора: Указывает, сколько времени toowait между повторная попытка подключения hello tooAzure Cosmos DB в случае временного сбоя (например прерывания подключений сети).
6. Режим подключения: Указывает режим toouse hello соединения с Azure Cosmos DB. доступны следующие возможности Hello: DirectTcp, DirectHttps и шлюз. режимы Hello прямое подключение являются быстрее, а режим hello шлюза — понятное дополнительные брандмауэра, как только он использует порт 443.

![Снимок экрана: дополнительные параметры последовательного импорта записей Azure Cosmos DB](./media/import-data/documentdbsequentialoptions.png)

> [!TIP]
> Hello импортировать режим tooconnection значения по умолчанию средство DirectTcp. При возникновении неполадок брандмауэра режима tooconnection шлюза, для его выполнения требуется только порт 443.
> 
> 

## <a id="IndexingPolicy"></a>Указание политики индексирования при создании коллекций Azure Cosmos DB
Когда во время импорта коллекций toocreate средства позволяют hello миграции, можно указать политику индексации hello hello коллекций. В hello Дополнительные параметры раздела hello Azure Cosmos DB массового импорта и параметры Azure Cosmos DB последовательной записи перейдите на раздел toohello политики индексирования.

![Снимок экрана: дополнительные параметры политики индексации Azure Cosmos DB](./media/import-data/indexingpolicy1.png)

С помощью hello индексирования политики расширенный параметр, вы можно выберите файл политики индексирования, вручную введите политикой индексирования или выбрать один из шаблонов по умолчанию (щелкнув правой hello индексирования политики текстовое поле).

Hello политики предоставляет средство hello содержит:

* По умолчанию. Эта политика лучше всего подходит при выполнении запросов равенства строк и использовании предложения ORDER BY, диапазона и запросов равенства для чисел. Эта политика имеет более низкий индекс служебных данных хранилища, чем "Диапазон".
* Диапазон. Эта политика лучше всего подходит при использовании предложения ORDER BY, диапазона и запросов равенства на числах и строках. Эта политика имеет более высокий индекс служебных данных хранилища, чем "По умолчанию" или "Хэш".

![Снимок экрана: дополнительные параметры политики индексации Azure Cosmos DB](./media/import-data/indexingpolicy2.png)

> [!NOTE]
> Если политика индексирования не указан, будут применены политика по умолчанию hello. Дополнительные сведения о политиках индексации Azure Cosmos DB см. в [этой статье](indexing-policies.md).
> 
> 

## <a name="export-toojson-file"></a>Файл экспорта tooJSON
Программа экспорта Hello Azure Cosmos DB JSON позволяет tooexport любой hello доступные исходные параметры tooa JSON-файл, содержащий массив документов JSON. Hello средство будет обрабатывать hello экспорта для вас, или можно выбрать команды tooview hello полученный миграции и выполните команду hello, самостоятельно. Hello полученный файл JSON может храниться локально или в хранилище больших двоичных объектов Azure.

![Снимок экрана: параметры экспорта в локальный файл Azure Cosmos DB JSON](./media/import-data/jsontarget.png)

![Снимок экрана: параметр экспорта в хранилище BLOB-объектов Azure Cosmos DB JSON](./media/import-data/jsontarget2.png)

При необходимости вы можете tooprettify hello, возникающие в JSON, что увеличивает размер hello hello итоговый документ во время внесения hello содержимое более удобной для чтения.

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

## <a name="advanced-configuration"></a>Расширенная конфигурация
На экране настройки дополнительных hello укажите расположение hello hello журнала файла toowhich хотелось бы записываются ошибки. Hello следующие правила применяются toothis страницы.

1. Если имя файла не указано, все ошибки будет возвращаться на странице результатов hello.
2. Если имя файла указано без каталога, затем hello файла будет быть создан (или перезаписан) в текущем каталоге среды hello.
3. Если выбрать существующий файл, а затем hello файл будет перезаписан, нет возможности добавления.

Затем выберите ли все toolog критического или сообщения об ошибке. Наконец решите, как часто hello на экране передачи сообщений будет обновляться ход его выполнения.

    ![Screenshot of Advanced configuration screen](./media/import-data/AdvancedConfiguration.png)

## <a name="confirm-import-settings-and-view-command-line"></a>Подтверждение параметров импорта и просмотр командной строки
1. После указания сведений об источнике информации о целевой и расширенной конфигурации, изучите Сводка по миграции hello и, при необходимости, представление или копирования hello, возникающие в команды миграции (копирование hello команда является полезным tooautomate операций импорта).
   
    ![Снимок экрана: окно сводки](./media/import-data/summary.png)
   
    ![Снимок экрана: окно сводки](./media/import-data/summarycommand.png)
2. После проверки источника и назначения нажмите кнопку **Импорт**. как в процессе импорта hello обновит Hello затраченное время, число переданных и сведения о сбое (если не указать имя файла в расширенной конфигурации hello). После завершения можно экспортировать результаты hello (например toodeal сбоев импорта).
   
    ![Снимок экрана: параметры экспорта в Azure Cosmos DB JSON](./media/import-data/viewresults.png)
3. Можно также запустить новый импорт хранение hello существующих параметров (например, выбор сведения, источник и целевой строки подключения, т. д.) или сброс всех значений.
   
    ![Снимок экрана: параметры экспорта в Azure Cosmos DB JSON](./media/import-data/newimport.png)

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * Установить средство переноса данных hello
> * импорт данных из разных источников данных;
> * Экспортированный из Azure Cosmos DB tooJSON

Теперь можно продолжить toohello следующее руководство и узнайте, как tooquery данных с помощью Azure Cosmos DB. 

> [!div class="nextstepaction"]
>[Как tooquery данных?](../cosmos-db/tutorial-query-documentdb.md)
