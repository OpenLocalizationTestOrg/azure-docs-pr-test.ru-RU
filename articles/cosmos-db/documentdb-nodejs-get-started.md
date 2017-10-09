---
title: "Учебник aaaNode.js для hello API DocumentDB для Azure Cosmos DB | Документы Microsoft"
description: "Node.js учебник, в котором создается Cosmos DB с hello DocumentDB API."
keywords: "node.js, руководство, база данных node"
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Учебник по node.js: hello использования DocumentDB API в базу данных Azure Cosmos toocreate консольное приложение Node.js
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js для MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Вас приветствует учебник toohello Node.js для пакета SDK для Node.js DB Cosmos Azure hello! После изучения этого руководства у вас будет консольное приложение, которое создает ресурсы Azure Cosmos DB и отправляет запросы к ним.

Мы рассмотрим следующие вопросы:

* Создание и подключение учетной записи Azure Cosmos DB tooan
* Настройка приложения
* Создание базы данных Node
* создание коллекции;
* создание документов JSON;
* Запрос к коллекции hello
* замена документа;
* удаление документа;
* Удаление базы данных узла hello

У вас нет времени? Не беспокойтесь! законченное решение Hello можно найти в [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started). В разделе [получить комплексное решение hello](#GetSolution) быстрого инструкции.

После прохождения учебника Node.js hello, пожалуйста голосования hello используйте кнопки в hello верхней и нижней части этой страницы toogive нам отзыв. Если вы хотите нам toocontact напрямую, если вам свободного tooinclude адрес вашей электронной почты в комментарии.

А теперь приступим к работе!

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Необходимые условия для учебника Node.js hello
Убедитесь, что у вас есть следующие hello:

* Активная учетная запись Azure. Если у вас нет такой учетной записи, вы можете зарегистрироваться для использования [бесплатной пробной версии Azure](https://azure.microsoft.com/pricing/free-trial/).
    * Кроме того, можно использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) для этого учебника.
* [Node.js](https://nodejs.org/) версии v0.10.29 или выше.

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Шаг 1. Создание учетной записи Azure Cosmos DB
Давайте создадим учетную запись Azure Cosmos DB. При наличии учетной записи требуется toouse можно сразу перейти слишком[настроить приложение Node.js](#SetupNode). Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[настроить приложение Node.js](#SetupNode).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>Шаг 2. Настройка приложения Node.js
1. Откройте удобный для вас терминал.
2. Найдите папку hello или каталог, куда toosave приложение Node.js.
3. Создайте две пустые файлы JavaScript с hello, следующие команды:
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux или OS X:
     * ```touch app.js```
     * ```touch config.js```
4. Установите модуль hello documentdb через npm. Hello используйте следующую команду:
   * ```npm install documentdb --save```

Отлично! Теперь, когда настройка завершена, можно начать писать код.

## <a id="Config"></a>Шаг 3. Настройка конфигурации приложения
Откройте файл ```config.js``` в предпочитаемом текстовом редакторе.

Затем скопировать и вставить hello Приведенный далее фрагмент кода и задайте свойства ```config.endpoint``` и ```config.primaryKey``` tooyour Azure Cosmos DB uri конечной точки и первичный ключ. Оба эти конфигурации можно найти в hello [портал Azure](https://portal.azure.com).

![Учебник node.js — снимок экрана приветствия портал Azure, показывающая Azure Cosmos DB учетная запись, с hello общаются выделяются hello ключи кнопки выделены на hello Azure Cosmos DB учетной записи и, при необходимости hello URI, первичный ключ и ВТОРИЧНЫЙ ключ значения, которые выделены на hello Ключи колонке - узел базы данных][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

Скопируйте и вставьте hello ```database id```, ```collection id```, и ```JSON documents``` tooyour ```config``` объект ниже задаются вашей ```config.endpoint``` и ```config.authKey``` свойства. При наличии данных, отсылаемых toostore в базе данных можно использовать базу данных Cosmos Azure [средство переноса данных](import-data.md) вместо добавления определения hello документа.

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


Hello базы данных, коллекции и определения документов будет выступать в качестве базы данных Azure Cosmos ```database id```, ```collection id```и данные документа.

Наконец, экспортировать вашей ```config``` объекта, чтобы на него можно ссылаться в hello ```app.js``` файла.

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>Шаг 4: Учетная запись Azure Cosmos DB tooan подключения
Откройте ваш пустым ```app.js``` файл в текстовом редакторе hello. Скопируйте и вставьте код hello ниже tooimport hello ```documentdb``` модуль и только что созданный ```config``` модуля.

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

Скопируйте и вставьте hello кода toouse hello ранее сохраненные ```config.endpoint``` и ```config.primaryKey``` toocreate новый DocumentClient.

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

Теперь, когда имеется hello кода tooinitialize hello Azure Cosmos DB клиента, давайте рассмотрим работы с ресурсами Azure Cosmos DB.

## <a name="step-5-create-a-node-database"></a>Шаг 5. Создание базы данных Node
Скопируйте и вставьте код hello ниже hello tooset код состояния HTTP не найден, URL-адрес hello базы данных и URL-адрес коллекции hello. Эти URL-адреса — это процесс поиска клиента Azure Cosmos DB hello, hello подходящей базы данных и коллекции.

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

Объект [базы данных](documentdb-resources.md#databases) могут быть созданы с помощью hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) функции hello **DocumentClient** класса. База данных находится hello логический контейнер для хранения документов, секционированный по коллекциям.

Скопируйте и вставьте hello **getDatabase** функции для создания новой базы данных в файле в файле app.js hello с hello ```id``` , указываемой hello ```config``` объекта. Hello функция будет проверять при hello базы данных с hello же ```FamilyRegistry``` идентификатор еще не существует. Если она существует, мы вернем ее вместо создания новой базы данных.

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Скопируйте и вставьте приведенный ниже код hello задаются hello **getDatabase** функции tooadd hello вспомогательную функцию **выхода** , будет печататься приветственное сообщение выхода и вызов hello слишком**getDatabase** функции.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```

Поздравляем! Вы успешно создали базу данных Azure Cosmos DB.

## <a id="CreateColl"></a>Шаг 6. Создание коллекции
> [!WARNING]
> Элемент **CreateDocumentCollectionAsync** создаст коллекцию, с которой связаны ценовые требования. Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Объект [коллекции](documentdb-resources.md#collections) могут быть созданы с помощью hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) функции hello **DocumentClient** класса. Коллекция представляет собой контейнер документов JSON и связанную с ними логику в виде приложения JavaScript.

Скопируйте и вставьте hello **getCollection** функция под hello **getDatabase** функции в файл toocreate hello в файле app.js новой коллекции с hello ```id``` указан в hello ```config```объекта. Опять же, мы проверим toomake убедитесь, что коллекция с таким же hello ```FamilyCollection``` идентификатор еще не существует. Если она существует, мы вернем ее вместо создания новой коллекции.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

Скопируйте и вставьте код hello вызова hello слишком**getDatabase** tooexecute hello **getCollection** функции.

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```

Поздравляем! Вы успешно создали коллекцию Azure Cosmos DB.

## <a id="CreateDoc"></a>Шаг 7. Создание документа
Объект [документа](documentdb-resources.md#documents) могут быть созданы с помощью hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) функции hello **DocumentClient** класса. Документы относятся к пользовательскому (произвольному) содержимому JSON. Теперь можно вставить документ в Azure Cosmos DB.

Скопируйте и вставьте hello **getFamilyDocument** функция под hello **getCollection** функции для создания hello документы, содержащие данные JSON hello, сохраненные в hello ```config``` объекта. Опять же, мы проверим toomake убедитесь, что документ с таким же идентификатором уже существует hello.

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

Скопируйте и вставьте код hello вызова hello слишком**getCollection** tooexecute hello **getFamilyDocument** функции.

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```

Поздравляем! Вы успешно создали документ Azure Cosmos DB.

![Node.js в учебной базе данных - диаграмма, иллюстрирующая hello иерархическую связь между hello учетной записи, hello базы данных, коллекции hello и документы hello - узла](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>Шаг 8. Запрос ресурсов Azure Cosmos DB
Azure Cosmos DB поддерживает [полнофункциональные запросы](documentdb-sql-query.md) к документам JSON, хранящимся в каждой коллекции. Hello следующем образце кода показан запрос, который можно запустить с документами hello в коллекции.

Скопируйте и вставьте hello **queryCollection** функция под hello **getFamilyDocument** функции в файле в файле app.js hello. Azure Cosmos DB поддерживает SQL-подобные запросы, как показано ниже. Дополнительные сведения о построении сложных запросов извлечь hello [площадку запросов](https://www.documentdb.com/sql/demo) и hello [запрос документации](documentdb-sql-query.md).

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
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
        });
    };


Hello, следующая диаграмма иллюстрирует, как hello базы данных SQL Azure Cosmos синтаксис называется с коллекцией hello созданный запрос.

![Node.js в учебной базе данных - схеме наглядного области hello и это означает запроса hello - узла](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

Hello [FROM](documentdb-sql-query.md#FromClause) ключевое слово является необязательным в hello запроса, так как запросы Azure Cosmos DB уже области tooa одну коллекцию. Поэтому слова "FROM Families f" можно заменить на "FROM root r" или любое другое имя переменной. Azure Cosmos DB определит, что семейств, корень или имя переменной hello выбрана, ссылка hello текущей коллекции по умолчанию.

Скопируйте и вставьте код hello вызова hello слишком**getFamilyDocument** tooexecute hello **queryCollection** функции.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```

Поздравляем! Вы успешно выполнили запрос к базе данных Azure Cosmos DB.

## <a id="ReplaceDocument"></a>Шаг 9. Замена документа
Azure Cosmos DB поддерживает замену документов JSON.

Скопируйте и вставьте hello **replaceFamilyDocument** функция под hello **queryCollection** функции в файле в файле app.js hello.

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Скопируйте и вставьте код hello вызова hello слишком**queryCollection** tooexecute hello **replaceDocument** функции. Кроме того, добавьте toocall кода hello **queryCollection** снова tooverify hello документ успешно изменен.

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```

Поздравляем! Вы успешно заменили документ Azure Cosmos DB.

## <a id="DeleteDocument"></a>Шаг 10. Удаление документа
Azure Cosmos DB поддерживает удаление документов JSON.

Скопируйте и вставьте hello **deleteFamilyDocument** функция под hello **replaceFamilyDocument** функции.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

Скопируйте и вставьте код hello ниже hello вызовов toohello второй **queryCollection** tooexecute hello **deleteDocument** функции.

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```

Поздравляем! Вы успешно удалили документ Azure Cosmos DB.

## <a id="DeleteDatabase"></a>Шаг 11: Удалите базу данных узла hello
Идет удаление hello создана база данных приведет к удалению hello базы данных и все дочерние ресурсы (коллекции, документы, и т. д.).

Скопируйте и вставьте hello **очистки** функция под hello **deleteFamilyDocument** функции базы данных tooremove hello и все дочерние ресурсы hello.

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

Скопируйте и вставьте код hello вызова hello слишком**deleteFamilyDocument** tooexecute hello **очистки** функции.

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a> Шаг 12. Запуск приложения Node.js
В общей сложности для вызова функций hello последовательности должен выглядеть следующим образом:

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

Найдите в окне терминала вашей ```app.js``` файл и выполните команду hello:```node app.js```

Вы увидите выходные данные get работы приложения hello. Hello выходные данные должны соответствовать hello пример текста ниже.

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key tooexit

Поздравляем! Вы создали после завершения Node.js учебника hello и иметь первого приложения консоли Azure Cosmos DB!

## <a id="GetSolution"></a>Получить комплексное решение учебника hello Node.js
Если бы не было времени toocomplete hello шаги в этом учебнике, или просто toodownload hello кода, можно получить его из [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).

решение GetStarted toorun hello, содержащий все образцы hello в этой статье, вам потребуется hello следующее:

* [Учетная запись Azure Cosmos DB][create-account].
* Hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) решения на сайте GitHub.

Установка hello **documentdb** модуль через npm. Hello используйте следующую команду:

* ```npm install documentdb --save```

Затем в hello ```config.js``` файла обновления hello config.endpoint и config.authKey значений как описано в [шаг 3: задать настройки приложения](#Config). 

В окне терминала найдите вашей ```app.js``` файл и выполните команду hello: ```node app.js```.

Теперь все готово. Выполните сборку и начинайте работу с решением. 

## <a name="next-steps"></a>Дальнейшие действия
* Требуется более сложный пример Node.js? См. статью о [создании веб-приложения Node.js с использованием Azure Cosmos DB](documentdb-nodejs-application.md).
* Узнайте, каким образом слишком[мониторинг учетной записи Azure Cosmos DB](monitor-accounts.md).
* Выполнять запросы к нашей образец набора данных в hello [площадку запросов](https://www.documentdb.com/sql/demo).
* Дополнительные сведения о модели программирования hello в разделе Разработка hello hello [страницы документации Azure Cosmos DB](https://azure.microsoft.com/documentation/services/documentdb/).

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
