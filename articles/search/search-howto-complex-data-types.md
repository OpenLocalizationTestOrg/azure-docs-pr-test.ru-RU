---
title: "Моделирование сложных типов данных в службе поиска Azure | Документация Майкрософт"
description: "Вложенные или иерархические структуры данных можно моделировать в индексе Поиска Azure с помощью плоских наборов строк и типа данных \"Коллекции\"."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: d576fd7bb267ae7a100589413185b595e3b2be42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-model-complex-data-types-in-azure-search"></a><span data-ttu-id="2e206-103">Моделирование сложных типов данных в службе поиска Azure</span><span class="sxs-lookup"><span data-stu-id="2e206-103">How to model complex data types in Azure Search</span></span>
<span data-ttu-id="2e206-104">Внешние наборы данных, используемые для заполнения индекса Поиска Azure, иногда включают иерархические или вложенные подструктуры, которые невозможно аккуратно разделить на табличные наборы строк.</span><span class="sxs-lookup"><span data-stu-id="2e206-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="2e206-105">К примерам таких структур можно отнести несколько расположений и номеров телефонов для одного клиента, несколько цветов и размеров для одного SKU, несколько авторов на одну книгу и т. д.</span><span class="sxs-lookup"><span data-stu-id="2e206-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="2e206-106">В моделировании эти структуры называются *сложные типы данных*, *составные типы данных*, *композитные типы данных*, *агрегатные типы данных* и т. д.</span><span class="sxs-lookup"><span data-stu-id="2e206-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span></span>

<span data-ttu-id="2e206-107">В службе поиска Azure не предусмотрена встроенная поддержка сложных типов данных. Однако в такой ситуации есть проверенное решение — процесс, состоящий из двух этапов: преобразование в плоскую структуру и воссоздание внутренней структуры с помощью типа данных **Коллекция**.</span><span class="sxs-lookup"><span data-stu-id="2e206-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span></span> <span data-ttu-id="2e206-108">Метод, описанный в этой статье, можно использовать для поиска содержимого, поиска содержимого с использованием фасетов, а также фильтрации и сортировки содержимого.</span><span class="sxs-lookup"><span data-stu-id="2e206-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="2e206-109">Пример сложной структуры данных</span><span class="sxs-lookup"><span data-stu-id="2e206-109">Example of a complex data structure</span></span>
<span data-ttu-id="2e206-110">Как правило, соответствующие данные представляют собой набор документов в формате JSON или XML или элементы в хранилище NoSQL, например Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2e206-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="2e206-111">Структурно проблема возникает из-за наличия нескольких дочерних элементов, по которым нужно выполнить поиск и фильтрацию.</span><span class="sxs-lookup"><span data-stu-id="2e206-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span></span>  <span data-ttu-id="2e206-112">Для демонстрации решения используйте в качестве примера следующий документ JSON, в котором указан набор контактов:</span><span class="sxs-lookup"><span data-stu-id="2e206-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span></span>

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

<span data-ttu-id="2e206-113">Поля id, name и company можно легко сопоставить друг с другом как поля в индексе Поиска Azure. Однако поле locations содержит массив расположений с набором идентификаторов и описаниями расположений.</span><span class="sxs-lookup"><span data-stu-id="2e206-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="2e206-114">С учетом того, что в Поиске Azure нет типа данных, поддерживающего такое поле, нужно подобрать другой способ моделирования в Поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="2e206-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="2e206-115">Этот прием также описан в записи блога Кирка Эванса (Kirk Evans) [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/) (Индексирование DocumentDB с помощью службы поиска Azure). В ней показан метод преобразования структуры данных в плоскую форму с получением полей `locationsID` и `locationsDescription`, которые являются [коллекциями](https://msdn.microsoft.com/library/azure/dn798938.aspx) (или массивом строк).</span><span class="sxs-lookup"><span data-stu-id="2e206-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-the-array-into-individual-fields"></a><span data-ttu-id="2e206-116">Часть 1. Преобразование массива в отдельные поля</span><span class="sxs-lookup"><span data-stu-id="2e206-116">Part 1: Flatten the array into individual fields</span></span>
<span data-ttu-id="2e206-117">Чтобы создать индекс службы поиска Azure, вмещающий этот набор данных, создайте отдельные поля для вложенной подструктуры: `locationsID` и `locationsDescription` с типом данных [Коллекция](https://msdn.microsoft.com/library/azure/dn798938.aspx) (или массив строк).</span><span class="sxs-lookup"><span data-stu-id="2e206-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="2e206-118">В этих полях будут проиндексированы значения "1" и "2" в поле `locationsID` для Артема Кузнецова и "3" и "4" в поле `locationsID` для Алины Ковалевой.</span><span class="sxs-lookup"><span data-stu-id="2e206-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="2e206-119">Данные в Поиске Azure будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2e206-119">Your data within Azure Search would look like this:</span></span> 

![пример данных, 2 строки](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-the-index-definition"></a><span data-ttu-id="2e206-121">Часть 2. Добавление поля коллекции в определении индекса</span><span class="sxs-lookup"><span data-stu-id="2e206-121">Part 2: Add a collection field in the index definition</span></span>
<span data-ttu-id="2e206-122">В схеме индекса определения полей могут выглядеть примерно как в приведенном ниже примере.</span><span class="sxs-lookup"><span data-stu-id="2e206-122">In the index schema, the field definitions might look similar to this example.</span></span>

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-the-index"></a><span data-ttu-id="2e206-123">Проверка поведения при поиске и расширение индекса при необходимости</span><span class="sxs-lookup"><span data-stu-id="2e206-123">Validate search behaviors and optionally extend the index</span></span>
<span data-ttu-id="2e206-124">Если индекс создан, а данные загружены, можно проверить выполнение запроса на поиск к набору данных в решении.</span><span class="sxs-lookup"><span data-stu-id="2e206-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span></span> <span data-ttu-id="2e206-125">Каждое поле типа **Коллекция** должно поддерживать **поиск**, **фильтрацию** и **поиск с использованием фасетов**.</span><span class="sxs-lookup"><span data-stu-id="2e206-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="2e206-126">Вы сможете выполнять такие запросы:</span><span class="sxs-lookup"><span data-stu-id="2e206-126">You should be able to run queries like:</span></span>

* <span data-ttu-id="2e206-127">поиск всех людей, работающих в центральном офисе AdventureWorks (значение Adventureworks Headquarters);</span><span class="sxs-lookup"><span data-stu-id="2e206-127">Find all people who work at the ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="2e206-128">получение числа людей, работающих в главном офисе (значение Home Office);</span><span class="sxs-lookup"><span data-stu-id="2e206-128">Get a count of the number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="2e206-129">определение отделов, в которых трудятся люди, работающие в главном офисе (значение Home Office), а также определение количества людей в каждом из офисов.</span><span class="sxs-lookup"><span data-stu-id="2e206-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span></span>  

<span data-ttu-id="2e206-130">Этот прием не подходит в ситуациях, когда нужно выполнить поиск с использованием идентификатора и описания расположения.</span><span class="sxs-lookup"><span data-stu-id="2e206-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span></span> <span data-ttu-id="2e206-131">Например:</span><span class="sxs-lookup"><span data-stu-id="2e206-131">For example:</span></span>

* <span data-ttu-id="2e206-132">Найти всех людей, работающих в главном офисе (значение Home Office) с идентификатором расположения 4.</span><span class="sxs-lookup"><span data-stu-id="2e206-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="2e206-133">Если помните, исходное содержимое выглядело так:</span><span class="sxs-lookup"><span data-stu-id="2e206-133">If you recall the original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="2e206-134">Однако теперь, когда данные разделены на отдельные поля, мы не знаем, какой из идентификаторов относится к главному офису, в котором работает Алина Ковалева (`locationsID 3` или `locationsID 4`).</span><span class="sxs-lookup"><span data-stu-id="2e206-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="2e206-135">В этом случае определите в индексе другое поле, объединяющее все данные в одну коллекцию.</span><span class="sxs-lookup"><span data-stu-id="2e206-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span></span>  <span data-ttu-id="2e206-136">В нашем примере это поле будет называться `locationsCombined`. Содержимое мы разделим с помощью значка `||`, хотя можно выбрать любой разделитель, который, по вашему мнению, будет уникальным набором символов для содержимого.</span><span class="sxs-lookup"><span data-stu-id="2e206-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="2e206-137">Например:</span><span class="sxs-lookup"><span data-stu-id="2e206-137">For example:</span></span> 

![пример данных, 2 строки с разделителем](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="2e206-139">С помощью поля `locationsCombined` теперь можно разместить еще больше запросов, например:</span><span class="sxs-lookup"><span data-stu-id="2e206-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="2e206-140">отображение числа людей, работающих в главном офисе (значение Home Office) с идентификатором расположения "4";</span><span class="sxs-lookup"><span data-stu-id="2e206-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="2e206-141">поиск людей, работающих в главном офисе (значение Home Office) с идентификатором расположения "4".</span><span class="sxs-lookup"><span data-stu-id="2e206-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="2e206-142">Ограничения</span><span class="sxs-lookup"><span data-stu-id="2e206-142">Limitations</span></span>
<span data-ttu-id="2e206-143">Этот метод полезен в ряде сценариев, но не подходит в каждом случае.</span><span class="sxs-lookup"><span data-stu-id="2e206-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="2e206-144">Например:</span><span class="sxs-lookup"><span data-stu-id="2e206-144">For example:</span></span>

1. <span data-ttu-id="2e206-145">Если в сложном типе данных нет статического набора полей и было невозможно сопоставить все возможные типы с одним полем.</span><span class="sxs-lookup"><span data-stu-id="2e206-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span></span> 
2. <span data-ttu-id="2e206-146">Обновление вложенных объектов требует дополнительных усилий, так как необходимо определить, что именно нужно обновить в индексе Поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="2e206-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="2e206-147">Пример кода</span><span class="sxs-lookup"><span data-stu-id="2e206-147">Sample code</span></span>
<span data-ttu-id="2e206-148">Пример индексирования сложного набора данных JSON в Поиск Azure и выполнения запросов к этому набору данных см. в этом [репозитории GitHub](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="2e206-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="2e206-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e206-149">Next step</span></span>
<span data-ttu-id="2e206-150">[Голосуйте за встроенную поддержку сложных типов данных](https://feedback.azure.com/forums/263029-azure-search) на странице UserVoice Поиска Azure и предоставьте дополнительные сведения о реализации функции на наше рассмотрение.</span><span class="sxs-lookup"><span data-stu-id="2e206-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span></span> <span data-ttu-id="2e206-151">Для связи со мной вы можете написать в Twitter через канал @liamca.</span><span class="sxs-lookup"><span data-stu-id="2e206-151">You can also reach out to me directly on Twitter at @liamca.</span></span>

