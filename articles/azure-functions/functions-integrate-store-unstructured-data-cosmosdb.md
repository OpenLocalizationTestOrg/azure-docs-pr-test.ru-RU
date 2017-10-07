---
title: "aaaStore неструктурированные данные, с помощью функции Azure и Cosmos DB"
description: "Хранение неструктурированных данных с помощью служб Функции Azure и Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, Cosmos DB, динамические вычисления, бессерверная архитектура"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a>Хранение неструктурированных данных с помощью служб Функции Azure и Cosmos DB

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) — это отличный способ toostore неструктурированных и данных JSON. В сочетании с функциями Azure Cosmos DB позволяет быстро и просто сохранять данные, используя код гораздо меньшего объема, чем требуется для хранения данных в реляционной базе данных.

В функциях Azure привязки ввода-вывода предоставляют декларативным способом tooconnect tooexternal данные службы при помощи функции. В этом разделе рассказано, как tooupdate существующие C# функции tooadd привязку выходных данных, которая хранит неструктурированные данные в документе Cosmos DB. 

![База данных Cosmos](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>Добавление выходной привязки

1. Разверните ваше приложение-функцию и функцию.

1. Выберите **Интеграция** и **+ новый Выход**, который находится на hello верхнем правом углу страницы приветствия. Выберите **Azure Cosmos DB** и щелкните **Выбрать**.

    ![Добавление выходной привязки Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. Используйте hello **вывод Azure Cosmos DB** параметры, как указано в таблице hello: 

    ![Настройка выходной привязки Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | Настройка      | Рекомендуемое значение  | Описание                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Имя параметра документа** | taskDocument | Имя, которое ссылается объект Cosmos DB toohello в коде. |
    | **Database name** (Имя базы данных) | taskDatabase | Имя базы данных toosave документов. |
    | **Имя коллекции** | TaskCollection | Имя коллекции баз данных Cosmos DB. |
    | **Если значение равно true, создается база данных Cosmos DB hello и коллекции** | Флажок установлен | Hello коллекции не существует, поэтому следует создать его. |

4. Выберите **New** Далее toohello **подключение документа Cosmos DB** метки и выберите **+ создать новый**. 

5. Используйте hello **новой учетной записи** параметры, как указано в таблице hello: 

    ![Настройка подключения к Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | Настройка      | Рекомендуемое значение  | Описание                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **Идентификатор** | Имя базы данных | Уникальный идентификатор для базы данных Cosmos DB hello  |
    | **API** | SQL (DocumentDB) | Выберите hello API базы данных документа.  |
    | **Подписка** | Подписка Azure | Подписка Azure  |
    | **Группа ресурсов** | myResourceGroup |  Используйте hello существующую группу ресурсов, содержащий функции приложения. |
    | **Расположение**  | WestEurope | Выберите местоположение рядом tooeither функция приложением или tooother приложений, использующих hello хранятся документы.  |

6. Нажмите кнопку **ОК** базы данных toocreate hello. Может потребоваться несколько баз данных hello toocreate минут. После создания базы данных hello hello строку подключения базы данных хранятся как параметр функции приложения. Имя параметра приложения Hello вставляется в **подключения к учетной записи Cosmos DB**. 
 
8. Если задана строка соединения hello, выберите **Сохранить** toocreate hello привязки.

## <a name="update-hello-function-code"></a>Изменения кода hello

Замените hello существующий код C# функции hello, следующий код:

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
Этот пример кода считывает строки запроса HTTP-запроса hello и назначает им toofields в hello `taskDocument` объекта. Hello `taskDocument` привязки отправляет hello объекта данные из этой привязки параметра toobe, хранящихся в базе данных связанного документа hello. Hello база данных создается в hello впервые запускается функции hello.

## <a name="test-hello-function-and-database"></a>Функции проверки hello и базы данных

1. Разверните в правом окне hello и выберите **теста**. В разделе **запроса**, нажмите кнопку **+ добавить параметр** и добавьте следующие параметры строки запроса toohello hello:

    + `name`
    + `task`
    + `duedate`

2. Щелкните **Выполнить**. Должно быть возвращено состояние 200.

    ![Настройка выходной привязки Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. На hello слева от оператора hello портал Azure, разверните панель значков hello, тип `cosmos` в hello найдите и выберите **Azure Cosmos DB**.

    ![Поиск hello службы Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. Выберите hello базы данных был создан, затем выберите **обозреватель данных**. Разверните hello **коллекций** узлов, выберите новый документ hello и подтвердить hello документ содержит ваш значения строки запроса, а также некоторые дополнительные метаданные. 

    ![Проверка записи Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

Вы успешно добавили триггер HTTP tooyour привязки, который хранит неструктурированные данные в базе данных Cosmos DB.

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

Дополнительные сведения о базе данных Cosmos DB tooa привязки см. в разделе [Azure DB Cosmos функции привязки](functions-bindings-documentdb.md).
