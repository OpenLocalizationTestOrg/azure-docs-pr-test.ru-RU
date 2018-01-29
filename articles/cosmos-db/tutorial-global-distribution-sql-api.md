---
title: "Учебник по глобальной рассылки Azure Cosmos DB для API-Интерфейсы SQL | Документы Microsoft"
description: "Узнайте, как настроить глобальные распространения Azure Cosmos DB с помощью API-Интерфейсы SQL."
services: cosmos-db
keywords: "Глобальные распространения"
documentationcenter: 
author: rafats
manager: jhubbard
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 05/10/2017
ms.author: rafats
ms.custom: mvc
ms.openlocfilehash: 0cee55673c8abca29b7e389fa4fd62a48566904b
ms.sourcegitcommit: 0e4491b7fdd9ca4408d5f2d41be42a09164db775
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/14/2017
---
# <a name="how-to-setup-azure-cosmos-db-global-distribution-using-the-sql-api"></a>Как настроить глобальные распространения Azure Cosmos DB с помощью API-Интерфейсы SQL

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

В этой статье мы показано, как использовать портал Azure для установки глобальных распространения Azure Cosmos DB и подключитесь с помощью API-Интерфейсы SQL.

В этой статье рассматриваются следующие задачи: 

> [!div class="checklist"]
> * настроили глобальное распределение на портале Azure;
> * Настройка глобальных распространителя с помощью [API-интерфейсы SQL](sql-api-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-to-a-preferred-region-using-the-sql-api"></a>Подключение к предпочтительной области с помощью API-Интерфейсы SQL

Чтобы воспользоваться преимуществами [глобального распределения](distribute-data-globally.md), клиентские приложения могут указать упорядоченный список предпочитаемых регионов, который будет использоваться для операций с документами. Это можно сделать, настроив политику подключения. На основе конфигурации учетной записи Azure Cosmos DB, текущий язык доступности и список предпочтения, указанный, оптимальный конечная точка будет выбрана пакетом SDK SQL для операций чтения и записи.

Этот список предпочтения указывается при инициализации подключения с помощью пакетов SDK SQL. Пакеты SDK принимают необязательный параметр PreferredLocations, представляющий собой упорядоченный список регионов Azure.

Пакет SDK будет автоматически отправлять все операции записи в текущий регион записи.

Все операции чтения будут отправляться в первой доступный регион из списка PreferredLocations. Если запрос завершится неудачей, клиент перейдет к следующему региону дальше по списку и так далее.

Пакеты SDK будут пытаться выполнять чтение данных из регионов, указанных в PreferredLocations. Например, если учетная запись базы данных доступна в четырех регионах, но клиент указывает в PreferredLocations только два региона для чтения (не для записи), то операции чтения не будут обслуживаться для региона, который не указан в PreferredLocations. Если указанные в PreferredLocations регионы не доступны, операции чтения обслуживаются в регионе записи.

Приложение может проверить текущие конечную точку записи и конечную точку чтения, выбранные пакетом SDK, просмотрев два свойства, WriteEndpoint и ReadEndpoint, доступные в SDK 1.8 и более поздней версии.

Если свойство PreferredLocations не задано, будут обслуживаться все запросы из текущего региона записи.

## <a name="net-sdk"></a>ПАКЕТ SDK .NET
Пакет SDK можно использовать без изменения кода. В этом случае пакет SDK автоматически направляет операции чтения и записи в текущий регион записи.

В пакете SDK для .NET 1.8 и более поздней версии параметр ConnectionPolicy конструктора DocumentClient имеет свойство Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations. Это свойство имеет тип коллекции `<string>` и должно содержать список имен регионов. Строковые значения форматируются по столбцу "Имя региона" на странице [Регионы Azure][regions], без пробелов до или после первого и последнего знака, соответственно.

Текущие конечные точки записи и чтения доступны в DocumentClient.WriteEndpoint и DocumentClient.ReadEndpoint, соответственно.

> [!NOTE]
> Не следует считать URL-адреса конечных точек долговременными константами. Служба может обновить их в любой момент. Пакет SDK обрабатывает это изменение автоматически.
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

## <a name="nodejs-javascript-and-python-sdks"></a>Пакеты SDK для NodeJS, JavaScript и Python
Пакет SDK можно использовать без изменения кода. В этом случае пакет SDK будет автоматически направлять операции чтения и записи в текущий регион записи.

В пакете SDK 1.8 и более поздней версии параметр ConnectionPolicy конструктора DocumentClient имеет новое свойство DocumentClient.ConnectionPolicy.PreferredLocations. Этот параметр является массивом строк, который принимает список имен регионов. Имена форматируются по столбцу "Имя региона" на странице [Регионы Azure][regions]. Можно также использовать предопределенные константы во вспомогательном объекте AzureDocuments.Regions.

Текущие конечные точки записи и чтения доступны в DocumentClient.getWriteEndpoint и DocumentClient.getReadEndpoint, соответственно.

> [!NOTE]
> Не следует считать URL-адреса конечных точек долговременными константами. Служба может обновить их в любой момент. Пакет SDK обработает это изменение автоматически.
>
>

Ниже приведен пример кода для NodeJS и JavaScript. В Python и Java используется тот же шаблон.

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

## <a name="rest"></a>REST
После того, как учетная запись базы данных станет доступной в нескольких регионах, клиенты смогут запрашивать ее доступность с помощью запроса GET к следующему универсальному коду ресурса (URI).

    https://{databaseaccount}.documents.azure.com/

Служба вернет список регионов и соответствующих универсальных кодов ресурса (URI) конечных точек Azure Cosmos DB для реплик. В ответе будет указан текущий регион записи. Затем клиент сможет выбрать подходящую конечную точку для всех последующих запросов REST API следующим образом.

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


* Все запросы PUT, POST и DELETE должны направляться на указанный универсальный код ресурса (URI) записи.
* Все запросы GET и другие запросы только для чтения могут направляться к любой конечной точке на выбор клиента.

Запросы на запись к регионам только для чтения завершатся ошибкой HTTP с кодом 403 ("Запрещено").

В случае изменения региона записи после этапа начального обнаружения клиента все последующие операции записи в предыдущий регион записи завершатся ошибкой HTTP с кодом 403 ("Запрещено"). Клиенту следует еще раз получить список регионов (запрос GET), чтобы получить обновленный регион записи.

На этом руководство завершено. Сведения об управлении согласованностью глобально реплицируемой учетной записи Azure Cosmos DB см. в [этой статье](consistency-levels.md). Сведения о том, как функционирует репликация глобальной базы данных в Azure Cosmos DB, см. в статье о [глобальном распределении данных в Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы выполнили следующее:

> [!div class="checklist"]
> * настроили глобальное распределение на портале Azure;
> * Настройка глобальных распространения, с помощью API-интерфейсов SQL

Перейдите к следующему руководству, чтобы узнать о разработке в локальной среде с помощью локального эмулятора Azure Cosmos DB.

> [!div class="nextstepaction"]
> [Разработка в локальной среде с помощью эмулятора](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

