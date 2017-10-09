---
title: "aaaHow tooquery данные таблицы в базе данных Azure Cosmos? | Документация Майкрософт"
description: "Узнайте, tooquery данные таблицы в базе данных Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>Azure Cosmos DB: Как tooquery таблицу данных с помощью hello API таблиц (Предварительная версия)?

Hello Azure Cosmos DB [API таблиц](table-introduction.md) (Предварительная версия) поддерживает OData и [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) запросы к данным ключ значение (таблица).  

В этой статье рассматриваются hello следующие задачи: 

> [!div class="checklist"]
> * Запрос данных с помощью API таблиц hello

Hello запросы в этой статье используют следующий образец hello `People` таблицы:

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Поскольку Azure Cosmos DB совместима с hello API хранилища таблиц Azure, см. [запрос таблицы и сущности] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) сведения о как hello tooquery с помощью Таблица API. 

Дополнительные сведения о функции расширенной hello, предлагаемые Azure Cosmos DB см. в разделе [Azure Cosmos DB: таблица API](table-introduction.md) и [разработка с hello API таблиц в .NET](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Предварительные требования

Для toowork эти запросы необходимо иметь учетную запись Azure Cosmos DB и иметь данные сущности в контейнере hello. У вас их нет? Полный hello [краткое руководство каждые пять минут](https://aka.ms/acdbtnetqs) или hello [учебнике для разработчиков](https://aka.ms/acdbtabletut) toocreate учетную запись и заполнить базу данных.

## <a name="query-on-partitionkey-and-rowkey"></a>Запросы PartitionKey и RowKey
Поскольку свойства PartitionKey и RowKey hello составляют первичный ключ сущности, можно использовать следующий специальный синтаксис tooidentify hello сущности hello: 

**Запрос**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Результаты**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

Кроме того, можно указать эти свойства как часть hello `$filter` параметра, как показано в следующем разделе hello. Обратите внимание, что приветствия имен свойств ключей и значения констант с учетом регистра. Hello PartitionKey и rowkey имеют тип String. 

## <a name="query-by-using-an-odata-filter"></a>Запрос с помощью фильтра OData
При построении строки фильтра помните о следующих правилах. 

* Используйте hello логические операторы, определенные hello спецификации протокола OData toocompare tooa значения свойства. Обратите внимание, что нельзя сравнивать значение tooa динамические свойства. Одна часть hello выражение должно быть константой. 
* Имя свойства Hello, оператор и значение константы должны быть разделены URL-кодированными пробелами. Пробелы кодируются в формате URL-адреса как `%20`. 
* Все части hello строки фильтра учитывается регистр. 
* должен иметь постоянное значение Hello hello и тех же данных введите в качестве свойства hello в порядке для hello фильтра tooreturn правильные результаты. Дополнительные сведения о поддерживаемых типах свойств см. в разделе [hello основные сведения о модели данных службы таблиц](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Ниже приведен пример запроса, показывающий, как toofilter по hello PartitionKey и электронной почты свойства с помощью OData `$filter`.

**Запрос**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Дополнительные сведения о как tooconstruct фильтрацию выражения для различных типов данных см. в разделе [запрос таблицами и сущностями](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Результаты**

| PartitionKey | RowKey | Email | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>Запросы с помощью LINQ 
Также можно запрашивать с помощью LINQ, который преобразует toohello соответствующего выражения запросов OData. Ниже приведен пример как toobuild запросов с использованием hello .NET SDK:

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

В этом учебнике вы сделали hello следующее:

> [!div class="checklist"]
> * Было рассмотрено, как tooquery с помощью hello API таблиц (Предварительная версия) 

Вы можете теперь приступить Далее учебника toolearn toohello как toodistribute данных глобально.

> [!div class="nextstepaction"]
> [Глобальное распределение данных](tutorial-global-distribution-documentdb.md)
