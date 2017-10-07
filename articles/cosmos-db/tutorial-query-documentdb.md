---
title: "tooquery aaaHow с помощью SQL в базе данных Azure Cosmos? | Документация Майкрософт"
description: "Узнайте, tooquery с данным DocumentDB с помощью SQL в базе данных Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Azure Cosmos DB: Как tooquery, с помощью SQL?

Hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) поддерживает запросы документов с помощью SQL. В этой статье содержится пример документа и два примера SQL-запросов и результатов.

В этой статье рассматриваются hello следующие задачи: 

> [!div class="checklist"]
> * Выполнение запросов к данным с помощью SQL.

## <a name="sample-document"></a>Пример документа

Hello SQL-запросы в этой статье используйте следующий пример документа hello.

```json
{
  "id": "WakefieldFamily",
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
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a>Где могут выполняться SQL-запросы

Может запускать запросы с использованием hello обозреватель данных в hello портал Azure, через hello [API-Интерфейс REST и пакеты SDK](documentdb-sdk-dotnet.md)и даже hello [площадку запросов](https://www.documentdb.com/sql/demo), который выполняет запросы в существующий набор данных выборки.

Дополнительные сведения об SQL-запросах см. в статье:
* [SQL-запросы и синтаксис SQL в DocumentDB](documentdb-sql-query.md)

## <a name="prerequisites"></a>Предварительные требования

В этом руководстве предполагается, что у вас есть учетная запись и коллекция базы данных Azure Cosmos DB. У вас их нет? Полный hello [краткое руководство 5-минутного](create-mongodb-nodejs.md) или hello [учебнике для разработчиков](tutorial-develop-mongodb.md) toocreate учетную запись и коллекции.

## <a name="example-query-1"></a>Пример запроса 1

Заданы hello образец семейства документа выше, следующий SQL-запрос возвращает документы hello которых соответствует поле id hello `WakefieldFamily`. Поскольку это `SELECT *` инструкции hello выходных данных запроса hello является весь документ JSON hello:

**Запрос**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**Результаты**

```json
{
  "id": "WakefieldFamily",
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
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a>Пример запроса 2

Hello следующий запрос возвращает все имена заданным hello дочерних элементов в hello семейства, идентификатор которого соответствует `WakefieldFamily` упорядоченный по их оценку.

**Запрос**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**Результаты**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * Узнать, как с помощью SQL tooquery  

Вы можете теперь приступить Далее учебника toolearn toohello как toodistribute данных глобально.

> [!div class="nextstepaction"]
> [Глобальное распределение данных](tutorial-global-distribution-documentdb.md)

