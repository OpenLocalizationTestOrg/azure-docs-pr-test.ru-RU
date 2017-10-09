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
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>Как toosetup Azure Cosmos DB глобального распространителя с помощью hello DocumentDB API

В этой статье показано, как toouse hello Azure toosetup портала Azure Cosmos DB глобального распространения, а затем подключитесь с помощью DocumentDB API hello.

В этой статье рассматриваются hello следующие задачи: 

> [!div class="checklist"]
> * Настройка глобальных распространения, с помощью портала Azure hello
> * Настройка глобальных распространения, с помощью hello [интерфейсы API DocumentDB](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>Подключение с помощью DocumentDB API hello предпочтительную область tooa

В порядке tootake преимуществами [глобального распространения](distribute-data-globally.md), клиентских приложений можно указать hello упорядоченный список предпочтения toobe области используется tooperform операции с документом. Это можно сделать, задав политику подключений hello. В зависимости от конфигурации учетной записи Azure Cosmos DB hello доступности текущий язык и список предпочтения hello указана, приветствия большинство оптимальной конечная точка будет выбираемого hello tooperform SDK DocumentDB для записи и чтения операций.

Этот список предпочтения указывается при инициализации подключения с помощью пакеты SDK DocumentDB hello. Необязательный параметр «PreferredLocations» примите Hello пакеты SDK, упорядоченный список регионов Azure.

пакет SDK для Hello будет автоматически отправлять все записи toohello текущей записи области.

Все операции чтения будут отправляться toohello первой доступной области в списке PreferredLocations hello. Если hello запрос завершается неудачно, клиент hello ошибкой вниз область Далее toohello списка hello и так далее.

предпринимает попытку tooread из регионов hello, указанный в PreferredLocations Hello пакеты SDK. Таким образом например, если hello учетной записи базы данных доступен в трех регионах, но клиент hello только задает два hello записи областей для PreferredLocations, затем никаких операций чтения будет предоставляться вне области записи hello, даже в случае hello перехода на другой ресурс.

приложение Hello можно проверить hello текущей конечной точки записи и чтения конечная точка выбрана по hello SDK путем проверки два свойства: WriteEndpoint и ReadEndpoint, доступные в пакете SDK версии 1.8 и более поздних версий.

Если hello PreferredLocations свойство не задано, все запросы будут поступать из hello текущей записи области.

## <a name="net-sdk"></a>ПАКЕТ SDK .NET
Hello SDK можно использовать без необходимости изменения кода. В этом случае hello SDK автоматически направляет чтения и записи toohello текущей записи области.

В версии 1.8 и более поздних версиях hello .NET SDK параметр ConnectionPolicy hello hello DocumentClient конструктор имеет свойство с именем Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations. Это свойство имеет тип коллекции `<string>` и должно содержать список имен регионов. Hello строковые значения форматируются в столбце Имя области hello на hello [регионы Azure] [ regions] страницы без пробелов до или после hello сначала и последний символ соответственно.

Hello текущей записи и чтения конечные точки доступны в DocumentClient.WriteEndpoint и DocumentClient.ReadEndpoint соответственно.

> [!NOTE]
> Hello URL-адресов для конечных точек hello не может считаться долгоживущие константы. Hello службы может обновить в любой момент. Это изменение автоматически обрабатывает Hello SDK.
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

## <a name="nodejs-javascript-and-python-sdks"></a>Пакеты SDK для NodeJS, JavaScript и Python
Hello SDK можно использовать без необходимости изменения кода. В этом случае приветствия SDK автоматически перенаправит считывает и записывает toohello текущей записи области.

В версии 1.8 и более поздних версий каждый пакет SDK hello ConnectionPolicy параметр конструктора DocumentClient hello новое свойство с именем DocumentClient.ConnectionPolicy.PreferredLocations. Этот параметр является массивом строк, который принимает список имен регионов. имена Hello форматируются в столбце Имя области hello в hello [регионы Azure] [ regions] страницы. Можно также использовать hello предопределенные константы в объекте удобства hello AzureDocuments.Regions

Hello текущей записи и чтения конечные точки доступны в DocumentClient.getWriteEndpoint и DocumentClient.getReadEndpoint соответственно.

> [!NOTE]
> Hello URL-адресов для конечных точек hello не может считаться долгоживущие константы. Hello службы может обновить в любой момент. пакет SDK для Hello будет обработать это изменение автоматически.
>
>

Ниже приведен пример кода для NodeJS и JavaScript. Python и Java будет следовать hello таким шаблоном.

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

## <a name="rest"></a>REST
После учетную запись базы данных станет доступным в нескольких регионах, клиенты могут запрашивать его доступности с помощью запроса GET для hello, следующий URI.

    https://{databaseaccount}.documents.azure.com/

Hello служба будет возвращать список областей и их соответствующие Azure Cosmos DB URI конечных точек для реплик hello. Текущий регион записи Hello указывается в ответ hello. Hello клиент затем может выбрать hello соответствующую конечную точку для всех последующих запросов REST API следующим образом.

Пример ответа

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


* Все PUT, POST и DELETE запросы должны проходить toohello указано записи URI
* Другие (например, запросы) запросов только для чтения и возвращает все может перейти в конечную точку tooany по выбору приветствия клиента

Напишите запросы только для tooread областей завершится ошибкой с кодом ошибки HTTP 403 («доступ запрещен»).

При изменении области hello записи после фазы начального обнаружения клиента hello, последующие записывает toohello предыдущей области записи завершится ошибкой с кодом ошибки HTTP 403 («доступ запрещен»). Hello клиента должен затем получить список регионов hello снова tooget hello обновленной записи область.

На этом руководство завершено. Вы узнаете, как toomanage hello согласованности глобально реплицируемым учетной записи пользователя, считывая [уровни согласованности в базе данных Azure Cosmos](consistency-levels.md). Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * Настройка глобальных распространения, с помощью портала Azure hello
> * Настройка глобальных распространения, с помощью hello интерфейсы API DocumentDB

Теперь можно перейти далее учебника toolearn toohello как toodevelop локально с помощью hello локальный эмулятор Azure Cosmos DB.

> [!div class="nextstepaction"]
> [Разрабатывать локально в эмуляторе hello](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

