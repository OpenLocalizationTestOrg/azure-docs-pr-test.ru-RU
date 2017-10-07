---
title: "Azure Cosmos DB: Построение веб-приложения с помощью .NET и hello MongoDB API | Документы Microsoft"
description: "Содержит образец кода .NET можно использовать запрос tooand tooconnect hello Azure Cosmos базы данных MongoDB API"
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB: Построение MongoDB API веб-приложения с помощью .NET и hello портал Azure

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure. Затем будет построение и развертывание веб-приложения списка задач, построенные на hello [драйвер MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/). 

## <a name="prerequisites"></a>Предварительные требования

Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Создание учетной записи базы данных

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Теперь давайте клонирование MongoDB API приложений из github, задайте строку подключения hello и запустите его. Вы увидите, как просто можно toowork с данными программными средствами. 

1. Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.  

2. Выполнения hello следующая команда репозитории примеров tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. Затем откройте файл решения hello в Visual Studio. 

## <a name="review-hello-code"></a>Проверка кода hello

Убедитесь, что происходит в приложение hello быстро ознакомиться. Откройте hello **Dal.cs** файл в папке hello **DAL** каталог и вы найдете следующие строки кода создать hello Azure Cosmos DB ресурсы. 

* Инициализируйте hello Mongo клиента.

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* Получить hello базу данных и коллекцию hello.

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* Получение всех документов.

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a>Обновление строки подключения

Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.

1. В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **строка подключения**и нажмите кнопку **чтения и записи ключей**. В файл Dal.cs hello в hello следующим шагом будет использоваться кнопки копия hello hello правой части hello toocopy экрана приветствия имя пользователя, пароль и узла.

2. Откройте hello **Dal.cs** файла в hello **DAL** каталога. 

3. Копировать вашей **имя пользователя** из портала hello (с использованием "Копировать" hello ") и сделать его hello значение hello **username** в вашей **Dal.cs** файла. 

4. Затем скопируйте вашей **узла** из портала hello и сделать его hello значение hello **узла** в ваш **Dal.cs** файла. 

5. Наконец, скопируйте вашей **пароль** из портала hello и сделать его hello значение hello **пароль** в вашей **Dal.cs** файла. 

Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB. 
    
## <a name="run-hello-web-app"></a>Запустите веб-приложение hello

1. В Visual Studio щелкните правой кнопкой мыши проект hello в **обозревателе решений** и нажмите кнопку **управление пакетами NuGet**. 

2. В hello NuGet **Обзор** введите *MongoDB.Driver*.

3. На основе результатов hello установить hello **MongoDB.Driver** библиотеки. При этом устанавливаются hello MongoDB.Driver пакета, а также все зависимости.

4. Нажмите сочетание клавиш CTRL + F5 toorun приложения hello. Приложение откроется в браузере. 

5. Нажмите кнопку **создать** в hello браузера и создать несколько новых задач в приложение списка задач.

## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как учетную запись Azure Cosmos DB toocreate и выполнения веб-приложения с использованием hello API для MongoDB. Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные. 

> [!div class="nextstepaction"]
> [Импорт данных в базе данных Azure Cosmos для hello MongoDB API](mongodb-migrate.md)

