---
title: "aaaUse MongoChef для Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, как toouse MongoChef с Azure DB Cosmos: API для MongoDB учетной записи"
keywords: MongoChef
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Использование MongoChef с учетной записью API для MongoDB в Azure Cosmos DB

tooconnect tooan Azure Cosmos DB: API для MongoDB учетной записи, необходимо:

* скачать и установить [MongoChef](http://3t.io/mongochef)
* Подготовить сведения о [строке подключения](connect-mongodb-account.md) для учетной записи API для MongoDB в Azure Cosmos DB.

## <a name="create-hello-connection-in-mongochef"></a>Создание соединения hello в MongoChef
tooadd Cosmos базы данных Azure: API для MongoDB учетной записи toohello MongoChef диспетчера подключений, выполнения hello следующие шаги.

1. Получить Cosmos базы данных Azure: API для MongoDB сведений о соединении с помощью инструкций hello [здесь](connect-mongodb-account.md).

    ![Снимок экрана: колонка строка подключения hello](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. Нажмите кнопку **Connect** tooopen hello диспетчера соединений, а затем щелкните **нового подключения**

    ![Снимок экрана диспетчера соединений MongoChef hello](./media/mongodb-mongochef/ConnectionManager.png)
3. В hello **новое подключение** в hello окна **сервера** введите hello узла (полное доменное имя) hello Azure Cosmos DB: API для учетной записи и hello порта MongoDB.

    ![Снимок экрана: вкладка hello MongoChef подключение диспетчера сервера](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. В hello **новое подключение** в hello окна **проверки подлинности** выберите режим проверки подлинности **Standard (MONGODB CR или SCARM-SHA-1)** и введите имя пользователя hello и ПАРОЛЬ.  Оставьте db проверки подлинности по умолчанию hello (администратор) или введите другое значение.

    ![Снимок экрана: вкладка hello MongoChef подключение диспетчер проверки подлинности](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. В hello **новое подключение** в hello окна **SSL** проверьте hello **tooconnect протокол SSL используется** флажок и hello **server принимать самозаверяющие SSL Сертификаты** переключатель.

    ![Снимок экрана MongoChef hello на вкладке SSL диспетчер соединений](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. Нажмите кнопку hello **проверить подключение** toovalidate сведения о соединении hello, выберите элемент **ОК** tooreturn toohello новое подключение окна и нажмите кнопку **Сохранить**.

    ![Снимок экрана: окно hello MongoChef тестирования подключения](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a>Используйте MongoChef toocreate базы данных, коллекции и документов
toocreate базы данных, коллекции и документов с помощью MongoChef, выполнить следующие шаги hello.

1. В **диспетчера соединений**, выделите hello соединения и нажмите кнопку **Connect**.

    ![Снимок экрана диспетчера соединений MongoChef hello](./media/mongodb-mongochef/ConnectToAccount.png)
2. Щелкните правой кнопкой мыши узел hello и выберите **добавления базы данных**.  Укажите имя базы данных и нажмите кнопку **ОК**.

    ![Снимок экрана: hello параметр MongoChef добавления базы данных](./media/mongodb-mongochef/AddDatabase1.png)
3. Щелкните правой кнопкой мыши базу данных hello и выберите **добавить коллекцию**.  Укажите имя коллекции и нажмите кнопку **Создать**.

    ![Снимок экрана: hello параметр MongoChef добавить коллекцию](./media/mongodb-mongochef/AddCollection.png)
4. Нажмите кнопку hello **коллекции** меню элемента, затем щелкните **добавить документ**.

    ![Снимок экрана: hello MongoChef добавить элемент меню](./media/mongodb-mongochef/AddDocument1.png)
5. В диалоговом окне Добавить документ hello, вставьте следующую hello и нажмите кнопку **добавить документ**.

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. Добавьте другой документ теперь hello после содержимого.

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. Выполните пробный запрос. Например поиск семейства с Фамилия «Андерсен» hello и возврата hello родительских элементов, а также состояние поля.

    ![Снимок экрана Mongo Chef, результаты запроса](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с [примерами](mongodb-samples.md) API для MongoDB в Azure Cosmos DB.
