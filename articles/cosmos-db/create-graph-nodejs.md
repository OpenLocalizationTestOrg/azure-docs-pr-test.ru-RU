---
title: "aaaBuild приложения Azure Cosmos DB Node.js с помощью Graph API | Документы Microsoft"
description: "Содержит образец кода Node.js tooconnect tooand можно использовать запрос Azure Cosmos DB"
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
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a>Azure Cosmos DB. Создание приложения Node.js с помощью API Graph

Azure Cosmos DB — глобально распределенных hello моделей базы данных службы от корпорации Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

В этой статье краткого руководства показано, как toocreate Cosmos Azure DB записи для Graph API (Предварительная версия), базы данных и диаграммы с помощью hello портал Azure. Построить и запустить консольное приложение с открытым исходным кодом hello [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) драйвера.  

> [!NOTE]
> модуль Hello npm `gremlin-secure` является модификацией `gremlin` модуль с поддержкой SSL и необходимые для соединения с Azure Cosmos DB SASL. Исходный код доступен на сайте [GitHub](https://github.com/CosmosDB/gremlin-javascript).
>

## <a name="prerequisites"></a>Предварительные требования

Перед запуском этого образца необходимо иметь hello следующие предварительные требования:
* [Node.js](https://nodejs.org/en/) v0.10.29 или более поздней версии;
* [Git.](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Создание учетной записи базы данных

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Добавление графа

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Теперь давайте клон Graph API приложение из GitHub, задайте строку подключения hello и запустите его. Вы увидите, как просто можно toowork с данными программными средствами. 

1. Откройте окно терминала Git, например Git Bash и измените (через `cd` команда) tooa рабочий каталог.  

2. Выполнения hello следующая команда репозитории примеров tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. Откройте файл решения hello в Visual Studio. 

## <a name="review-hello-code"></a>Проверка кода hello

Убедитесь, что происходит в приложение hello быстро ознакомиться. Откройте hello `app.js` файл и вы найдете следующие строки кода hello. 

* создается клиент Gremlin Hello.

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  Hello конфигурации находятся в `config.js`, который мы изменения в следующем разделе hello.

* Последовательность шагов Gremlin выполняются с hello `client.execute` метод.

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a>Обновление строки подключения

1. Привет открыть файл config.js. 

2. Config.js, заполните в ключ config.endpoint hello с hello **Gremlin URI** значение из hello **Обзор** страница hello портал Azure. 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-graph-nodejs/gremlin-uri.png)

   Если hello **Gremlin URI** имеет пустое значение, можно создать значение hello из hello **ключей** hello портала с помощью hello **URI** значение https:// удаление и изменение toographs документы.

   Конечная точка Gremlin Hello должна быть только имя узла hello без номера протокола и порта hello, таких как `mygraphdb.graphs.azure.com` (не `https://mygraphdb.graphs.azure.com` или `mygraphdb.graphs.azure.com:433`).

3. В config.js, заполните значения config.primaryKey hello вход с помощью hello **первичного ключа** значение из hello **ключей** страница hello портал Azure. 

    `config.primaryKey = "PRIMARYKEY";`

   ![Hello Azure портала колонке ключей](./media/create-graph-nodejs/keys.png)

4. Введите имя базы данных hello и имя диаграммы (контейнер) для значения hello config.database и config.collection. 

Вот как должен выглядеть файл config.js:

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a>Запустите консольное приложение hello

1. Откройте окно терминала и измените (через `cd` команда) toohello каталог установки для файла package.json hello, включенный в проект hello.  

2. Запустите `npm install` tooinstall hello необходимые модули npm, включая `gremlin-secure`.

3. Запустите `node app.js` в терминалов toostart узла приложения.

## <a name="browse-with-data-explorer"></a>Просмотр с помощью обозревателя данных

Теперь можно вернуться tooData обозревателя в hello Azure tooview портала, запрос, изменить и работы с данными новый график.

В обозревателе данных hello новой базы данных отображается в hello **графы** области. Hello базы данных, а затем с помощью коллекции hello, а затем выберите пункт **Graph**.

созданные hello пример приложения Hello данные отображаются в области далее hello в hello **Graph** вкладке при нажатии кнопки **применить фильтр**.

Повторите выполнение `g.V()` с `.has('firstName', 'Thomas')` tootest hello фильтра. Обратите внимание, что значение hello с учетом регистра.

## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a>Очистка ресурсов

Если вы не планируете использовать это приложение toocontinue, удалите все ресурсы, созданные в этой статье, выполнив hello ниже: 

1. В hello портал Azure, в меню навигации слева hello, щелкните **групп ресурсов**и щелкните имя hello hello ресурса, который был создан. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toobe ресурсов hello удален и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этой статье вы узнали, как создать граф, с помощью данных обозревателя toocreate учетную запись Azure Cosmos DB и запуск приложения. Теперь вы можете создавать более сложные запросы и внедрять эффективную логику обхода графа с помощью Gremlin. 

> [!div class="nextstepaction"]
> [Как выполнять запросы к данным в базе данных Azure Cosmos DB с помощью API Graph (предварительная версия)](tutorial-query-graph.md)
