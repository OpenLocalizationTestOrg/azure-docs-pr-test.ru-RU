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
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="21469-104">Запрос табличных данных в базе данных Azure Cosmos DB с помощью API таблицы (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="21469-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="21469-105">[API таблицы](table-introduction.md) (предварительная версия) в базе данных Azure Cosmos DB поддерживает OData и запросы [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) к данным "ключ — значение" (таблицы).</span><span class="sxs-lookup"><span data-stu-id="21469-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="21469-106">В этой статье рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="21469-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="21469-107">Запрос данных с помощью API таблицы.</span><span class="sxs-lookup"><span data-stu-id="21469-107">Querying data with the Table API</span></span>

<span data-ttu-id="21469-108">Запросы в этой статье используют следующий пример таблицы `People`:</span><span class="sxs-lookup"><span data-stu-id="21469-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="21469-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="21469-109">PartitionKey</span></span> | <span data-ttu-id="21469-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="21469-110">RowKey</span></span> | <span data-ttu-id="21469-111">Email</span><span class="sxs-lookup"><span data-stu-id="21469-111">Email</span></span> | <span data-ttu-id="21469-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="21469-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21469-113">Harp</span><span class="sxs-lookup"><span data-stu-id="21469-113">Harp</span></span> | <span data-ttu-id="21469-114">Walter</span><span class="sxs-lookup"><span data-stu-id="21469-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="21469-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="21469-115">425-555-0101</span></span> |
| <span data-ttu-id="21469-116">Smith</span><span class="sxs-lookup"><span data-stu-id="21469-116">Smith</span></span> | <span data-ttu-id="21469-117">Ben</span><span class="sxs-lookup"><span data-stu-id="21469-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="21469-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="21469-118">425-555-0102</span></span> |
| <span data-ttu-id="21469-119">Smith</span><span class="sxs-lookup"><span data-stu-id="21469-119">Smith</span></span> | <span data-ttu-id="21469-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="21469-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="21469-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="21469-121">425-555-0104</span></span> | 

<span data-ttu-id="21469-122">Так как база данных Azure Cosmos DB совместима с API хранилища таблиц Azure, сведения о запросе с помощью API таблицы см. в [этой статье] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="21469-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="21469-123">Дополнительные сведения о расширенных возможностях, предлагаемых базой данных Azure Cosmos DB, см. в статьях [Введение в базу данных Azure Cosmos DB: API таблицы](table-introduction.md) и [Разработка с помощью API таблицы на .NET в базе данных Azure Cosmos DB](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="21469-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="21469-124">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="21469-124">Prerequisites</span></span>

<span data-ttu-id="21469-125">Чтобы эти запросы работали, у вас должна быть учетная запись базы данных Azure Cosmos DB и данные сущности в контейнере.</span><span class="sxs-lookup"><span data-stu-id="21469-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="21469-126">У вас их нет?</span><span class="sxs-lookup"><span data-stu-id="21469-126">Don't have any of those?</span></span> <span data-ttu-id="21469-127">Выполните процедуры [краткого руководства](https://aka.ms/acdbtnetqs) или [руководства разработчика](https://aka.ms/acdbtabletut), чтобы создать учетную запись и заполнить базу данных.</span><span class="sxs-lookup"><span data-stu-id="21469-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="21469-128">Запросы PartitionKey и RowKey</span><span class="sxs-lookup"><span data-stu-id="21469-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="21469-129">Так как свойства PartitionKey и RowKey образуют первичный ключ сущности, вы можете использовать специальный синтаксис, чтобы идентифицировать сущность:</span><span class="sxs-lookup"><span data-stu-id="21469-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="21469-130">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="21469-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="21469-131">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="21469-131">**Results**</span></span>

| <span data-ttu-id="21469-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="21469-132">PartitionKey</span></span> | <span data-ttu-id="21469-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="21469-133">RowKey</span></span> | <span data-ttu-id="21469-134">Email</span><span class="sxs-lookup"><span data-stu-id="21469-134">Email</span></span> | <span data-ttu-id="21469-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="21469-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21469-136">Harp</span><span class="sxs-lookup"><span data-stu-id="21469-136">Harp</span></span> | <span data-ttu-id="21469-137">Walter</span><span class="sxs-lookup"><span data-stu-id="21469-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="21469-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="21469-138">425-555-0104</span></span> |

<span data-ttu-id="21469-139">В качестве альтернативы вы можете указать эти свойства как часть параметра `$filter`, как показано в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="21469-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="21469-140">Обратите внимание, что в именах ключевых свойств и значениях констант учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="21469-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="21469-141">Свойства PartitionKey и RowKey имеют тип String.</span><span class="sxs-lookup"><span data-stu-id="21469-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="21469-142">Запрос с помощью фильтра OData</span><span class="sxs-lookup"><span data-stu-id="21469-142">Query by using an OData filter</span></span>
<span data-ttu-id="21469-143">При построении строки фильтра помните о следующих правилах.</span><span class="sxs-lookup"><span data-stu-id="21469-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="21469-144">Используйте логические операторы, определенные спецификацией протокола OData, чтобы сравнить свойство со значением.</span><span class="sxs-lookup"><span data-stu-id="21469-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="21469-145">Обратите внимание, что нельзя сравнивать свойство с динамическим значением.</span><span class="sxs-lookup"><span data-stu-id="21469-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="21469-146">Одна часть выражения должна быть константой.</span><span class="sxs-lookup"><span data-stu-id="21469-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="21469-147">Имя свойства, оператор и значение константы должны быть разделены пробелами, закодированными в формате URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="21469-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="21469-148">Пробелы кодируются в формате URL-адреса как `%20`.</span><span class="sxs-lookup"><span data-stu-id="21469-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="21469-149">Во всех частях строки фильтра учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="21469-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="21469-150">Для получения допустимых результатов фильтра значения константы и свойства должны иметь одинаковый тип данных.</span><span class="sxs-lookup"><span data-stu-id="21469-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="21469-151">Дополнительные сведения о поддерживаемых типах свойств см. в статье [Общие сведения о модели данных службы таблиц](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="21469-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="21469-152">Вот пример запроса, который показывает, как выполнить фильтрацию по свойствам PartitionKey и свойству Email с помощью `$filter` OData.</span><span class="sxs-lookup"><span data-stu-id="21469-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="21469-153">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="21469-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="21469-154">Дополнительные сведения о том, как строить выражения фильтра для разных типов данных, см. в статье [Запрос таблиц и сущностей](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="21469-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="21469-155">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="21469-155">**Results**</span></span>

| <span data-ttu-id="21469-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="21469-156">PartitionKey</span></span> | <span data-ttu-id="21469-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="21469-157">RowKey</span></span> | <span data-ttu-id="21469-158">Email</span><span class="sxs-lookup"><span data-stu-id="21469-158">Email</span></span> | <span data-ttu-id="21469-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="21469-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21469-160">Ben</span><span class="sxs-lookup"><span data-stu-id="21469-160">Ben</span></span> |<span data-ttu-id="21469-161">Smith</span><span class="sxs-lookup"><span data-stu-id="21469-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="21469-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="21469-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="21469-163">Запросы с помощью LINQ</span><span class="sxs-lookup"><span data-stu-id="21469-163">Query by using LINQ</span></span> 
<span data-ttu-id="21469-164">Вы также можете выполнить запрос с помощью LINQ, который преобразуется в соответствующие выражения запроса OData.</span><span class="sxs-lookup"><span data-stu-id="21469-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="21469-165">Ниже приведен пример создания запросов с использованием пакета SDK .NET.</span><span class="sxs-lookup"><span data-stu-id="21469-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="21469-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21469-166">Next steps</span></span>

<span data-ttu-id="21469-167">В этом руководстве вы выполнили следующее:</span><span class="sxs-lookup"><span data-stu-id="21469-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="21469-168">Научились запрашивать данные таблиц в базе данных Azure Cosmos с помощью API таблицы (предварительная версия).</span><span class="sxs-lookup"><span data-stu-id="21469-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="21469-169">Теперь вы можете приступать к следующему руководству, чтобы узнать, как глобально распределять данные.</span><span class="sxs-lookup"><span data-stu-id="21469-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="21469-170">Глобальное распределение данных</span><span class="sxs-lookup"><span data-stu-id="21469-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
