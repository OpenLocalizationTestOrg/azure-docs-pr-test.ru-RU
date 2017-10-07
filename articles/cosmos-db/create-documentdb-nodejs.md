---
title: "Azure Cosmos DB: Сборка приложения с помощью Node.js и hello DocumentDB API | Документы Microsoft"
description: "Представляет запрос tooand tooconnect можно использовать образец кода Node.js hello Azure Cosmos DB DocumentDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a>Azure Cosmos DB: Создать приложение DocumentDB API с Node.js и hello портал Azure

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure. Затем постройте и запустите консольное приложение, построенных на hello [DocumentDB Node.js API](documentdb-sdk-node.md).

## <a name="prerequisites"></a>Предварительные требования

* Перед запуском этого образца необходимо иметь hello следующие предварительные требования:
    * [Node.js](https://nodejs.org/en/) версии 0.10.29 или более поздней.
    * [Git.](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Создание учетной записи базы данных

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Добавление коллекции

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Теперь давайте клонирование DocumentDB API приложений из github, задайте строку подключения hello и запустите его. Вы видите, как просто можно toowork с данными программными средствами. 

1. Откройте окно терминала git, таких как git bash и `CD` tooa рабочий каталог.  

2. Выполнения hello следующая команда репозитории примеров tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a>Проверка кода hello

Убедитесь, что происходит в приложение hello быстро ознакомиться. Откройте hello `app.js` файл а можно найти следующие строки кода создать hello Azure Cosmos DB ресурсы. 

* Hello `documentClient` инициализируется.

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* Создание базы данных.

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Создание коллекции.

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Создание нескольких документов.

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Выполнение запроса SQL через JSON.

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a>Обновление строки подключения

Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.

1. В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**. Кнопки копирования hello будет использоваться на правой стороне hello hello toocopy экрана приветствия URI и первичный ключ в hello `config.js` файла в следующем шаге hello.

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-dotnet/keys.png)

2. В открытых hello `config.js` файла. 

3. Скопируйте значение URI с портала hello (с использованием "Копировать" hello ") и сделать его hello значение ключа hello конечной точки в `config.js`. 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. Затем скопируйте значение ПЕРВИЧНОГО ключа из портала hello и сделать его значение hello hello `config.primaryKey` в `config.js`. Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB. 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a>Выполните приложение hello
1. Запустите `npm install` в терминалов tooinstall необходимые модули npm

2. Запустите `node app.js` в терминалов toostart узла приложения.

Теперь можно вернуться tooData обозревателя и запроса в разделе, изменения и работать с новые данные. 

## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги:

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя hello созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как создать коллекцию с помощью hello обозреватель данных toocreate учетную запись Azure Cosmos DB и запуск приложения. Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные. 

> [!div class="nextstepaction"]
> [Импорт данных в DocumentDB с помощью средства миграции базы данных](import-data.md)


