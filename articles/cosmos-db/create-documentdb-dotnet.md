---
title: "Azure Cosmos DB: Построение веб-приложения с помощью .NET и hello DocumentDB API | Документы Microsoft"
description: "Содержит образец кода .NET можно использовать запрос tooand tooconnect hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB: Построение веб-приложения с помощью .NET DocumentDB API и hello портал Azure

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure. Затем будет построения и развертывания веб-приложения todo список лежит hello [API .NET для DocumentDB](documentdb-sdk-dotnet.md), как показано в следующих экрана приветствия. 

![Приложение со списком задач с демонстрационными данными](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>Предварительные требования

Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Создание учетной записи базы данных

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a>Добавление коллекции

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Добавление демонстрационных данных

Теперь можно добавить новую коллекцию tooyour данных с помощью обозревателя данных.

1. В обозревателе данных hello новой базы данных отображается в области коллекций hello. Разверните hello **задачи** базы данных, разверните hello **элементы** коллекции, нажмите кнопку **документов**и нажмите кнопку **новые документы**. 

   ![Создавать новые документы в обозревателе данных hello портал Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Теперь можно добавьте коллекцию toohello документа с hello следующие структуры.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. После добавления hello json toohello **документов** щелкните **Сохранить**.

    ![Копировать данные json и нажмите кнопку Сохранить в обозревателе данных в hello портал Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Создать и сохранить один дополнительные документ, который вставляются уникальное значение для hello `id` и измените hello других свойств по своему усмотрению. Новые документы могут иметь любую структуру, так как Azure Cosmos DB не устанавливает определенные схемы данных.

     Теперь можно использовать запросы в обозреватель данных tooretrieve данные. По умолчанию используется обозреватель данных `SELECT * FROM c` tooretrieve всех документов в коллекции hello, но можно изменить, другой tooa [SQL-запроса](documentdb-sql-query.md), такие как `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn на основе все документы hello в порядке убывания их отметки времени.
 
     Можно также использовать обозреватель данных toocreate хранимых процедур, определяемых пользователем функций и триггеров tooperform серверных бизнес-логику, также как масштаб пропускной способности. Обозреватель данных предоставляет все hello встроенного программного доступа к данным, доступны в API-интерфейсы hello, но предоставляет простой доступ к данным tooyour hello портал Azure.

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Теперь давайте переключения tooworking с кодом. Давайте клонировать приложении DocumentDB API из GitHub, задайте строку подключения hello и запустите его. Вы увидите, как просто можно toowork с данными программными средствами. 

1. Откройте окно терминала git, таких как git bash и `CD` tooa рабочий каталог.  

2. Выполнения hello следующая команда репозитории примеров tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. Затем откройте файл решения todo hello в Visual Studio. 

## <a name="review-hello-code"></a>Проверка кода hello

Убедитесь, что происходит в приложение hello быстро ознакомиться. Привет открыть файл DocumentDBRepository.cs и вы найдете следующие строки кода создать hello Azure Cosmos DB ресурсы. 

* Hello DocumentClient инициализируется в строке 73.

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* База данных создается в строке 88.

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* Коллекция создается в строке 107.

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>Обновление строки подключения

Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.

1. В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**. Вы будете использовать кнопки копия hello hello правой части hello toocopy экрана приветствия URI и первичный ключ в файл web.config hello в следующем шаге hello.

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-dotnet/keys.png)

2. Откройте файл web.config hello в Visual Studio 2017 г. 

3. Скопируйте значение URI с портала hello (с использованием "Копировать" hello ") и сделать его hello значение ключа hello конечной точки в файле web.config. 

    `<add key="endpoint" value="FILLME" />`

4. Затем скопируйте значение ПЕРВИЧНОГО ключа из портала hello и сделать его hello значение authKey hello в файле web.config. Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB. 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a>Запустите веб-приложение hello
1. В Visual Studio щелкните правой кнопкой мыши проект hello в **обозревателе решений** и нажмите кнопку **управление пакетами NuGet**. 

2. В hello NuGet **Обзор** введите *DocumentDB*.

3. На основе результатов hello установить hello **Microsoft.Azure.DocumentDB** библиотеки. При этом устанавливаются hello Microsoft.Azure.DocumentDB пакета, а также все зависимости.

4. Нажмите сочетание клавиш CTRL + F5 toorun приложения hello. Приложение откроется в браузере. 

5. Нажмите кнопку **создать новый** в hello браузера и создать несколько новых задач в приложении задачи.

   ![Приложение со списком задач с демонстрационными данными](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

Теперь можно вернуться tooData обозревателя и запроса в разделе, изменения и работать с новые данные. 

## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как создать коллекцию с помощью hello обозреватель данных toocreate учетной записи Azure Cosmos DB и запуска веб-приложения. Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные. 

> [!div class="nextstepaction"]
> [Импорт данных в DocumentDB с помощью средства миграции базы данных](import-data.md)


