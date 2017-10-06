---
title: "Здравствуйте, aaaBuild приложения Azure Cosmos DB .NET с помощью Graph API | Документы Microsoft"
description: "Содержит образец кода .NET можно использовать tooconnect tooand запросов Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a>Azure Cosmos DB: Сборка приложений .NET, использующих hello Graph API

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB, базы данных и graph (контейнер) с помощью hello портал Azure. Затем постройте и запустите консольное приложение, построенных на hello [Graph API](graph-sdk-dotnet.md) (Предварительная версия).  

## <a name="prerequisites"></a>Предварительные требования

Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Создание учетной записи базы данных

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Добавление графа

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Теперь давайте клон Graph API приложение из github, задайте строку подключения hello и запустите его. Вы увидите, как просто можно toowork с данными программными средствами. 

1. Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.  

2. Выполнения hello следующая команда репозитории примеров tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. Откройте Visual Studio и Привет открыть файл решения. 

## <a name="review-hello-code"></a>Проверка кода hello

Убедитесь, что происходит в приложение hello быстро ознакомиться. Привет открыть файл Program.cs и вы найдете следующие строки кода создать hello Azure Cosmos DB ресурсы. 

* Hello DocumentClient инициализируется. В режиме предварительного просмотра hello мы добавили расширение graph API на клиенте Azure Cosmos DB hello. Мы работаем над автономный клиент графа, связаны с клиентом Azure Cosmos DB hello и ресурсы.

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* Создание базы данных.

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* Создание графа.

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* Последовательность шагов Gremlin выполняются с помощью hello `CreateGremlinQuery` метод.

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a>Обновление строки подключения

Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.

1. Откройте файл App.config hello в Visual Studio 2017 г. 

2. В hello в учетной записи Azure Cosmos DB портала Azure щелкните **ключей** в hello навигации слева. 

    ![Просмотр и копирование первичного ключа в hello портал Azure, на странице приветствия ключей](./media/create-graph-dotnet/keys.png)

3. Копия вашего **URI** из портала hello и сделать его hello значение ключа hello конечной точки в файле App.config. Можно использовать "Копировать" hello ", как показано в предшествующих значение hello toocopy экрана приветствия.

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. Копия вашего **ПЕРВИЧНОГО ключа** из портала hello и сделать его hello значение ключа AuthKey hello в файл App.config, а затем сохранить изменения. 

    `<add key="AuthKey" value="FILLME" />`

Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB. 

## <a name="run-hello-console-app"></a>Запустите консольное приложение hello

1. В Visual Studio щелкните правой кнопкой мыши на hello **GraphGetStarted** проекта в **обозревателе решений** и нажмите кнопку **управление пакетами NuGet**. 

2. В hello NuGet **Обзор** введите *Microsoft.Azure.Graphs* и проверьте hello **включает предварительный выпуск** поле. 

3. На основе результатов hello установить hello **Microsoft.Azure.Graphs** библиотеки. При этом устанавливаются пакет библиотеки расширения graph Azure Cosmos DB hello и все зависимости.

    Если вы получите сообщение о рецензировании решения toohello изменения, нажмите кнопку **ОК**. Если появится сообщение о принятии условий лицензионного соглашения, щелкните **Принимаю**.

4. Нажмите сочетание клавиш CTRL + F5 toorun приложения hello.

   окно консоли Hello отображает hello вершин и ребра, добавляемом toohello графа. После завершения скрипта hello, нажмите клавишу ВВОД дважды tooclose окна консоли hello. 

## <a name="browse-using-hello-data-explorer"></a>Просмотр с помощью hello обозреватель данных

Теперь можно будет вернуться tooData обозревателя в hello портал Azure и просматривать и запрашивать данные новой диаграммы.

1. В обозревателе данных hello новой базы данных отображается в области диаграмм hello. Разверните **graphdb** и **graphcollz**, а затем щелкните **График**.

2. Нажмите кнопку hello **применить фильтр** по умолчанию hello toouse кнопку запрос tooview все verticies hello графике hello. созданные hello пример приложения Hello данные отображаются в области диаграмм hello.

    Вы можете увеличить и из него hello диаграммы, можно развернуть места на экране приветствия graph, добавить дополнительные verticies и перемещать поверхность отображения verticies на hello.

    ![Просмотр графика hello в обозревателе данных в hello портал Azure](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги: 

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как создать граф, с помощью hello обозреватель данных toocreate учетную запись Azure Cosmos DB и запуск приложения. Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin. 

> [!div class="nextstepaction"]
> [Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)](tutorial-query-graph.md)

