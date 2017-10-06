---
title: "aaaAzure Cosmos DB глобального распространения учебник по Graph API | Документы Microsoft"
description: "Узнайте, как hello toosetup Azure Cosmos DB глобального распространителя с помощью Graph API."
services: cosmos-db
keywords: "глобальное распределение, graph, gremlin"
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: 1629a31e12a18079f63e07c4909862b36b5f4c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-graph-api"></a>Как hello toosetup Azure Cosmos DB глобального распространителя с помощью Graph API

В этой статье показано, как toouse hello Azure toosetup портала Azure Cosmos DB глобального распространения, а затем подключитесь с помощью hello API Graph (Предварительная версия).

В этой статье рассматриваются hello следующие задачи: 

> [!div class="checklist"]
> * Настройка глобальных распространения, с помощью портала Azure hello
> * Настройка глобальных распространения, с помощью hello [Graph API-интерфейсы](graph-introduction.md) (Предварительная версия)

[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-graph-api-using-hello-net-sdk"></a>Подключение tooa предпочтительную область с помощью API Graph hello, с помощью hello .NET SDK

Hello Graph API указывается в виде библиотеки расширений на основе hello DocumentDB SDK.

В порядке tootake преимуществами [глобального распространения](distribute-data-globally.md), клиентских приложений можно указать hello упорядоченный список предпочтения toobe области используется tooperform операции с документом. Это можно сделать, задав политику подключений hello. В зависимости от конфигурации учетной записи Azure Cosmos DB hello доступности текущий язык и список предпочтения hello указана, hello большинство оптимальной конечная точка будет выбранные записи tooperform SDK hello и операции чтения.

Этот список предпочтения указывается при инициализации подключения с помощью пакетов SDK hello. Необязательный параметр «PreferredLocations» примите Hello пакеты SDK, упорядоченный список регионов Azure.

* **Записывает**: hello SDK будет автоматически отправлять все записывает toohello текущей записи области.
* **Считывает**: все операции чтения будут отправляться toohello первой доступной области, в списке PreferredLocations hello. Если hello запрос завершается неудачно, клиент hello ошибкой вниз область Далее toohello списка hello и так далее. предпринимает попытку tooread из регионов hello, указанный в PreferredLocations Hello пакеты SDK. Таким образом например, если hello Cosmos DB учетная запись доступна в трех регионах, но клиент hello только задает два hello записи областей для PreferredLocations, затем никаких операций чтения будет предоставляться вне области записи hello, даже в случае hello перехода на другой ресурс.

приложение Hello можно проверить hello текущей конечной точки записи и чтения конечная точка выбрана по hello SDK путем проверки два свойства: WriteEndpoint и ReadEndpoint, доступные в пакете SDK версии 1.8 и более поздних версий. Если hello PreferredLocations свойство не задано, все запросы будут поступать из hello текущей записи области.

### <a name="using-hello-sdk"></a>С помощью пакета SDK для hello

Например, в hello .NET SDK, hello `ConnectionPolicy` параметр hello `DocumentClient` конструктор имеет свойство с именем `PreferredLocations`. Это свойство можно задать список tooa имена областей. экран приветствия имен для [регионы Azure] [ regions] может быть указан как часть `PreferredLocations`.

> [!NOTE]
> Hello URL-адресов для конечных точек hello не может считаться долгоживущие константы. Hello службы может обновить в любой момент. Это изменение автоматически обрабатывает Hello SDK.
>
>

```cs
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

// connect tooAzure Cosmos DB
await docClient.OpenAsync().ConfigureAwait(false);
```

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

