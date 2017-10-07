---
title: "Azure Cosmos DB. Создание веб-приложения с проверкой подлинности Xamarin и Facebook | Документация Майкрософт"
description: "Содержит образец кода .NET можно использовать tooconnect tooand запросов Azure Cosmos DB"
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
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure Cosmos DB. Создание веб-приложения с проверкой подлинности .NET, Xamarin и Facebook

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

В этом кратком руководстве показано, как toocreate учетную запись Azure Cosmos DB документа базы данных и коллекцию с помощью hello портал Azure. Затем будет построения и развертывания веб-приложения todo список лежит hello [API .NET для DocumentDB](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)и hello Azure Cosmos авторизации СУБД. Hello todo список веб-приложение реализует шаблон данных пользователя, который позволяет toologin пользователей с помощью проверки подлинности Facebook и управлять toodo элементами.

## <a name="prerequisites"></a>Предварительные требования

Если у вас еще нет Visual Studio 2017 г. установлен, можно загрузить и использовать hello **свободного** [2017 г. Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Убедитесь, что включен **разработки Azure** во время установки Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Создание учетной записи базы данных

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Добавление коллекции

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Пример приложения hello клонирования

Теперь давайте клонирование DocumentDB API приложений из github, задайте строку подключения hello и запустите его. Вы увидите, как просто можно toowork с данными программными средствами. 

1. Откройте окно терминала git, таких как git bash и `cd` tooa рабочий каталог.  

2. Выполнения hello следующая команда репозитории примеров tooclone hello. 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. Затем откройте файл DocumentDBTodo.sln hello из папки samples/xamarin/UserItems/xamarin.forms hello в Visual Studio. 

## <a name="review-hello-code"></a>Проверка кода hello

Код Hello в папке Xamarin hello содержит:

* Приложение Xamarin. приложение Hello сохраняет элементов todo пользователя hello в секционированную коллекцию с именем UserItems.
* Брокер маркера ресурса API. Простой веб-API ASP.NET toobroker ресурс Azure Cosmos DB маркеры toohello вход пользователей приложения hello. Маркеры ресурсов — маркеры доступа короткоживущими, предоставить приложение hello toohello доступа hello в данных пользователя.

в приведенной ниже схеме hello проиллюстрирован Hello проверки подлинности и потоки данных.

* Hello UserItems сбора создается с ключом секции hello "и ИД пользователя". Указание ключа секции для коллекции позволяет Azure Cosmos DB tooscale бесконечно hello количества пользователей и элементов возрастает.
* приложение Xamarin Hello позволяет toologin пользователей с учетными данными с Facebook.
* приложение Xamarin Hello использует tooauthenticate маркера доступа Facebook с ResourceTokenBroker API
* broker маркера ресурсов Hello API выполняет проверку подлинности с помощью функции проверки подлинности службы приложения запроса hello и запрашивает маркер ресурсов Azure Cosmos DB с документами tooall доступа чтения и записи, прошедший проверку пользователь hello ключ раздела для управления доступом.
* Broker маркера ресурсов возвращает hello ресурсов маркера toohello клиентского приложения.
* приложение Hello обращается к элементов todo пользователя hello, с помощью маркера ресурсов hello.

![Приложение со списком задач с демонстрационными данными](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>Обновление строки подключения

Теперь вернитесь toohello Azure портала tooget данные строки подключения и скопируйте его в приложение hello.

1. В hello [портал Azure](http://portal.azure.com/), в вашей Azure Cosmos DB учетной записи, в hello навигации слева щелкните **ключей**и нажмите кнопку **чтения и записи ключей**. Вы будете использовать кнопки копия hello hello правой части hello toocopy экрана приветствия URI и первичный ключ в файл Web.config hello в следующем шаге hello.

    ![Просмотреть и скопировать ключ доступа в hello портал Azure, ключи колонку](./media/create-documentdb-xamarin-dotnet/keys.png)

2. В Visual Studio 2017 г. Откройте файл Web.config hello в папке azure-documentdb-dotnet/образцы/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker hello. 

3. Скопируйте значение URI с портала hello (с использованием "Копировать" hello ") и сделать его hello значение accountUrl hello в файле Web.config. 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. Затем скопируйте значение ПЕРВИЧНОГО ключа из портала hello и сделать его значение accountKey hello в Web.congif hello. 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

Теперь вы обновили приложения с все hello сведения учетной записи, он должен toocommunicate с Azure Cosmos DB. 

## <a name="build-and-deploy-hello-web-app"></a>Построение и развертывание веб-приложения hello

1. В hello портал Azure создают службы приложений веб-сайта toohost hello ресурсов маркера broker API.
2. Hello портал Azure откройте колонку параметров приложения hello брокера маркера ресурсов hello API веб-сайта. Заполните следующие параметры приложения hello.

    * accountUrl - URL-адрес учетной записи Azure Cosmos DB hello hello вкладки ключи учетной записи Azure Cosmos DB.
    * accountKey - hello Azure Cosmos DB учетной записи главного ключа из hello вкладка ключей учетной записи Azure Cosmos DB.
    * databaseId и collectionId созданной базы данных и коллекции.

3. Опубликуйте hello tooyour ResourceTokenBroker решения, созданные веб-сайта.

4. Откройте проект Xamarin hello и перейдите tooTodoItemManager.cs. Заполните значения hello accountURL, collectionId, databaseId, а также resourceTokenBrokerURL hello базовый https URL-адрес веб-сайта маркера broker hello ресурсов.

5. Полный hello [как tooconfigure имени входа Facebook toouse приложения службы приложений](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) учебника toosetup проверки подлинности Facebook и настроить веб-сайт ResourceTokenBroker hello.

    Запустите приложение Xamarin hello.

## <a name="review-slas-in-hello-azure-portal"></a>Просмотрите соглашений об уровне обслуживания в hello портал Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом кратком руководстве в hello портал Azure с hello следующие шаги: 

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и щелкните имя только что созданный ресурс hello hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы узнали, как toocreate учетную запись Azure Cosmos DB, создайте коллекцию, с помощью hello обозреватель данных и построение приложения Xamarin. Теперь можно импортировать учетной записи Cosmos DB tooyour дополнительные данные. 

> [!div class="nextstepaction"]
> [Импорт данных в DocumentDB с помощью средства миграции базы данных](import-data.md)
