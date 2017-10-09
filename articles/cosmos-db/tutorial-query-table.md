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
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a><span data-ttu-id="1d070-104">Azure Cosmos DB: Как tooquery таблицу данных с помощью hello API таблиц (Предварительная версия)?</span><span class="sxs-lookup"><span data-stu-id="1d070-104">Azure Cosmos DB: How tooquery table data by using hello Table API (preview)?</span></span>

<span data-ttu-id="1d070-105">Hello Azure Cosmos DB [API таблиц](table-introduction.md) (Предварительная версия) поддерживает OData и [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) запросы к данным ключ значение (таблица).</span><span class="sxs-lookup"><span data-stu-id="1d070-105">hello Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="1d070-106">В этой статье рассматриваются hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="1d070-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="1d070-107">Запрос данных с помощью API таблиц hello</span><span class="sxs-lookup"><span data-stu-id="1d070-107">Querying data with hello Table API</span></span>

<span data-ttu-id="1d070-108">Hello запросы в этой статье используют следующий образец hello `People` таблицы:</span><span class="sxs-lookup"><span data-stu-id="1d070-108">hello queries in this article use hello following sample `People` table:</span></span>

| <span data-ttu-id="1d070-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="1d070-109">PartitionKey</span></span> | <span data-ttu-id="1d070-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="1d070-110">RowKey</span></span> | <span data-ttu-id="1d070-111">Email</span><span class="sxs-lookup"><span data-stu-id="1d070-111">Email</span></span> | <span data-ttu-id="1d070-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="1d070-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1d070-113">Harp</span><span class="sxs-lookup"><span data-stu-id="1d070-113">Harp</span></span> | <span data-ttu-id="1d070-114">Walter</span><span class="sxs-lookup"><span data-stu-id="1d070-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="1d070-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="1d070-115">425-555-0101</span></span> |
| <span data-ttu-id="1d070-116">Smith</span><span class="sxs-lookup"><span data-stu-id="1d070-116">Smith</span></span> | <span data-ttu-id="1d070-117">Ben</span><span class="sxs-lookup"><span data-stu-id="1d070-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="1d070-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="1d070-118">425-555-0102</span></span> |
| <span data-ttu-id="1d070-119">Smith</span><span class="sxs-lookup"><span data-stu-id="1d070-119">Smith</span></span> | <span data-ttu-id="1d070-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="1d070-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="1d070-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="1d070-121">425-555-0104</span></span> | 

<span data-ttu-id="1d070-122">Поскольку Azure Cosmos DB совместима с hello API хранилища таблиц Azure, см. [запрос таблицы и сущности] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) сведения о как hello tooquery с помощью Таблица API.</span><span class="sxs-lookup"><span data-stu-id="1d070-122">Because Azure Cosmos DB is compatible with hello Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how tooquery by using hello Table API.</span></span> 

<span data-ttu-id="1d070-123">Дополнительные сведения о функции расширенной hello, предлагаемые Azure Cosmos DB см. в разделе [Azure Cosmos DB: таблица API](table-introduction.md) и [разработка с hello API таблиц в .NET](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1d070-123">For more information on hello premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with hello Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="1d070-124">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1d070-124">Prerequisites</span></span>

<span data-ttu-id="1d070-125">Для toowork эти запросы необходимо иметь учетную запись Azure Cosmos DB и иметь данные сущности в контейнере hello.</span><span class="sxs-lookup"><span data-stu-id="1d070-125">For these queries toowork, you must have an Azure Cosmos DB account and have entity data in hello container.</span></span> <span data-ttu-id="1d070-126">У вас их нет?</span><span class="sxs-lookup"><span data-stu-id="1d070-126">Don't have any of those?</span></span> <span data-ttu-id="1d070-127">Полный hello [краткое руководство каждые пять минут](https://aka.ms/acdbtnetqs) или hello [учебнике для разработчиков](https://aka.ms/acdbtabletut) toocreate учетную запись и заполнить базу данных.</span><span class="sxs-lookup"><span data-stu-id="1d070-127">Complete hello [five-minute quickstart](https://aka.ms/acdbtnetqs) or hello [developer tutorial](https://aka.ms/acdbtabletut) toocreate an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="1d070-128">Запросы PartitionKey и RowKey</span><span class="sxs-lookup"><span data-stu-id="1d070-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="1d070-129">Поскольку свойства PartitionKey и RowKey hello составляют первичный ключ сущности, можно использовать следующий специальный синтаксис tooidentify hello сущности hello:</span><span class="sxs-lookup"><span data-stu-id="1d070-129">Because hello PartitionKey and RowKey properties form an entity's primary key, you can use hello following special syntax tooidentify hello entity:</span></span> 

<span data-ttu-id="1d070-130">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="1d070-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="1d070-131">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="1d070-131">**Results**</span></span>

| <span data-ttu-id="1d070-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="1d070-132">PartitionKey</span></span> | <span data-ttu-id="1d070-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="1d070-133">RowKey</span></span> | <span data-ttu-id="1d070-134">Email</span><span class="sxs-lookup"><span data-stu-id="1d070-134">Email</span></span> | <span data-ttu-id="1d070-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="1d070-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1d070-136">Harp</span><span class="sxs-lookup"><span data-stu-id="1d070-136">Harp</span></span> | <span data-ttu-id="1d070-137">Walter</span><span class="sxs-lookup"><span data-stu-id="1d070-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="1d070-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="1d070-138">425-555-0104</span></span> |

<span data-ttu-id="1d070-139">Кроме того, можно указать эти свойства как часть hello `$filter` параметра, как показано в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="1d070-139">Alternatively, you can specify these properties as part of hello `$filter` option, as shown in hello following section.</span></span> <span data-ttu-id="1d070-140">Обратите внимание, что приветствия имен свойств ключей и значения констант с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="1d070-140">Note that hello key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="1d070-141">Hello PartitionKey и rowkey имеют тип String.</span><span class="sxs-lookup"><span data-stu-id="1d070-141">Both hello PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="1d070-142">Запрос с помощью фильтра OData</span><span class="sxs-lookup"><span data-stu-id="1d070-142">Query by using an OData filter</span></span>
<span data-ttu-id="1d070-143">При построении строки фильтра помните о следующих правилах.</span><span class="sxs-lookup"><span data-stu-id="1d070-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="1d070-144">Используйте hello логические операторы, определенные hello спецификации протокола OData toocompare tooa значения свойства.</span><span class="sxs-lookup"><span data-stu-id="1d070-144">Use hello logical operators defined by hello OData Protocol Specification toocompare a property tooa value.</span></span> <span data-ttu-id="1d070-145">Обратите внимание, что нельзя сравнивать значение tooa динамические свойства.</span><span class="sxs-lookup"><span data-stu-id="1d070-145">Note that you can't compare a property tooa dynamic value.</span></span> <span data-ttu-id="1d070-146">Одна часть hello выражение должно быть константой.</span><span class="sxs-lookup"><span data-stu-id="1d070-146">One side of hello expression must be a constant.</span></span> 
* <span data-ttu-id="1d070-147">Имя свойства Hello, оператор и значение константы должны быть разделены URL-кодированными пробелами.</span><span class="sxs-lookup"><span data-stu-id="1d070-147">hello property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="1d070-148">Пробелы кодируются в формате URL-адреса как `%20`.</span><span class="sxs-lookup"><span data-stu-id="1d070-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="1d070-149">Все части hello строки фильтра учитывается регистр.</span><span class="sxs-lookup"><span data-stu-id="1d070-149">All parts of hello filter string are case-sensitive.</span></span> 
* <span data-ttu-id="1d070-150">должен иметь постоянное значение Hello hello и тех же данных введите в качестве свойства hello в порядке для hello фильтра tooreturn правильные результаты.</span><span class="sxs-lookup"><span data-stu-id="1d070-150">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="1d070-151">Дополнительные сведения о поддерживаемых типах свойств см. в разделе [hello основные сведения о модели данных службы таблиц](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="1d070-151">For more information about supported property types, see [Understanding hello Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="1d070-152">Ниже приведен пример запроса, показывающий, как toofilter по hello PartitionKey и электронной почты свойства с помощью OData `$filter`.</span><span class="sxs-lookup"><span data-stu-id="1d070-152">Here's an example query that shows how toofilter by hello PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="1d070-153">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="1d070-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="1d070-154">Дополнительные сведения о как tooconstruct фильтрацию выражения для различных типов данных см. в разделе [запрос таблицами и сущностями](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="1d070-154">For more information on how tooconstruct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="1d070-155">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="1d070-155">**Results**</span></span>

| <span data-ttu-id="1d070-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="1d070-156">PartitionKey</span></span> | <span data-ttu-id="1d070-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="1d070-157">RowKey</span></span> | <span data-ttu-id="1d070-158">Email</span><span class="sxs-lookup"><span data-stu-id="1d070-158">Email</span></span> | <span data-ttu-id="1d070-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="1d070-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1d070-160">Ben</span><span class="sxs-lookup"><span data-stu-id="1d070-160">Ben</span></span> |<span data-ttu-id="1d070-161">Smith</span><span class="sxs-lookup"><span data-stu-id="1d070-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="1d070-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="1d070-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="1d070-163">Запросы с помощью LINQ</span><span class="sxs-lookup"><span data-stu-id="1d070-163">Query by using LINQ</span></span> 
<span data-ttu-id="1d070-164">Также можно запрашивать с помощью LINQ, который преобразует toohello соответствующего выражения запросов OData.</span><span class="sxs-lookup"><span data-stu-id="1d070-164">You can also query by using LINQ, which translates toohello corresponding OData query expressions.</span></span> <span data-ttu-id="1d070-165">Ниже приведен пример как toobuild запросов с использованием hello .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="1d070-165">Here's an example of how toobuild queries by using hello .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1d070-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d070-166">Next steps</span></span>

<span data-ttu-id="1d070-167">В этом учебнике вы сделали hello следующее:</span><span class="sxs-lookup"><span data-stu-id="1d070-167">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1d070-168">Было рассмотрено, как tooquery с помощью hello API таблиц (Предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="1d070-168">Learned how tooquery by using hello Table API (preview)</span></span> 

<span data-ttu-id="1d070-169">Вы можете теперь приступить Далее учебника toolearn toohello как toodistribute данных глобально.</span><span class="sxs-lookup"><span data-stu-id="1d070-169">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1d070-170">Глобальное распределение данных</span><span class="sxs-lookup"><span data-stu-id="1d070-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
