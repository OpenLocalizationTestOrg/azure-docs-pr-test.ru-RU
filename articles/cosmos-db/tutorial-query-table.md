---
title: "Как выполнять запросы к данным таблиц в базе данных Azure Cosmos DB | Документация Майкрософт"
description: "Узнайте, как запрашивать данные таблиц в базе данных Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 11/15/2017
ms.author: govindk
ms.custom: mvc
ms.openlocfilehash: 80fed91c45ae19193f6b8dfcaef747f8c4253dee
ms.sourcegitcommit: 7136d06474dd20bb8ef6a821c8d7e31edf3a2820
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/05/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api"></a>База данных Azure Cosmos DB. Запрос табличных данных с помощью API таблицы

[API таблицы](table-introduction.md) в службе Azure Cosmos DB поддерживает OData и запросы [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) к данным "ключ — значение" (таблицы).  

В этой статье рассматриваются следующие задачи: 

> [!div class="checklist"]
> * Запрос данных с помощью API таблицы.

Запросы в этой статье используют следующий пример таблицы `People`:

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Прочитайте раздел [База данных Azure Cosmos DB. Запрос табличных данных с помощью API таблицы](https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities), чтобы получить подробные сведения о том, как отправить запрос с помощью API таблиц. 

Дополнительные сведения о расширенных возможностях, предлагаемых базой данных Azure Cosmos DB, см. в статьях [Знакомство со службой Azure Cosmos DB. API таблицы](table-introduction.md) и [Разработка с помощью API таблицы базы данных Azure Cosmos DB на языке .NET](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Предварительные требования

Чтобы эти запросы работали, у вас должна быть учетная запись базы данных Azure Cosmos DB и данные сущности в контейнере. У вас их нет? Выполните процедуры [краткого руководства](create-table-dotnet.md) или [руководства разработчика](tutorial-develop-table-dotnet.md), чтобы создать учетную запись и заполнить базу данных.

## <a name="query-on-partitionkey-and-rowkey"></a>Запросы PartitionKey и RowKey
Так как свойства PartitionKey и RowKey образуют первичный ключ сущности, вы можете использовать специальный синтаксис, чтобы идентифицировать сущность: 

**Запрос**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Результаты**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

В качестве альтернативы вы можете указать эти свойства как часть параметра `$filter`, как показано в следующем разделе. Обратите внимание, что в именах ключевых свойств и значениях констант учитывается регистр. Свойства PartitionKey и RowKey имеют тип String. 

## <a name="query-by-using-an-odata-filter"></a>Запрос с помощью фильтра OData
При построении строки фильтра помните о следующих правилах. 

* Используйте логические операторы, определенные спецификацией протокола OData, чтобы сравнить свойство со значением. Обратите внимание, что нельзя сравнивать свойство с динамическим значением. Одна часть выражения должна быть константой. 
* Имя свойства, оператор и значение константы должны быть разделены пробелами, закодированными в формате URL-адреса. Пробелы кодируются в формате URL-адреса как `%20`. 
* Во всех частях строки фильтра учитывается регистр. 
* Для получения допустимых результатов фильтра значения константы и свойства должны иметь одинаковый тип данных. Дополнительные сведения о поддерживаемых типах свойств см. в статье [Общие сведения о модели данных службы таблиц](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Вот пример запроса, который показывает, как выполнить фильтрацию по свойствам PartitionKey и свойству Email с помощью `$filter` OData.

**Запрос**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Дополнительные сведения о том, как строить выражения фильтра для разных типов данных, см. в статье [Запрос таблиц и сущностей](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Результаты**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>Запросы с помощью LINQ 
Вы также можете выполнить запрос с помощью LINQ, который преобразуется в соответствующие выражения запроса OData. Ниже приведен пример создания запросов с использованием пакета SDK .NET.

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a>Дальнейшие действия

В этом руководстве вы выполнили следующее:

> [!div class="checklist"]
> * Научились выполнять запросы с помощью API таблицы

Теперь вы можете приступать к следующему руководству, чтобы узнать, как глобально распределять данные.

> [!div class="nextstepaction"]
> [Глобальное распределение данных](tutorial-global-distribution-table.md)
