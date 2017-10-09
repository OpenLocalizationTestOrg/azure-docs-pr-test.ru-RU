---
title: "aaaHow toomodel сложных типов данных в поиске Azure | Документы Microsoft"
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
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="b5a4d-103">Как типы toomodel сложных данных в поиске Azure</span><span class="sxs-lookup"><span data-stu-id="b5a4d-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="b5a4d-104">Внешних наборов данных используется toopopulate индекс поиска Azure иногда содержат иерархические или вложенном вложенные структуры, которые не нарушают аккуратно в виде табличного набора строк.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="b5a4d-105">К примерам таких структур можно отнести несколько расположений и номеров телефонов для одного клиента, несколько цветов и размеров для одного SKU, несколько авторов на одну книгу и т. д.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="b5a4d-106">Моделирование условия, вы видите, эти структуры называется tooas *сложные типы данных*, *составные типы данных*, *составные типы данных*, или *статистические типы данных*, tooname несколько.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="b5a4d-107">Сложные типы данных не поддерживаются изначально в поиске Azure, но проверенные решение включает два этапа выравнивание структуры hello и затем с помощью **коллекции** типа tooreconstitute hello внутренние структуры данных.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="b5a4d-108">Следование hello способ, описанный в этой статье позволяет содержимого toobe hello которой выполняется поиск, аспекта, фильтрация и сортировка.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="b5a4d-109">Пример сложной структуры данных</span><span class="sxs-lookup"><span data-stu-id="b5a4d-109">Example of a complex data structure</span></span>
<span data-ttu-id="b5a4d-110">Обычно данные hello рассматриваемой находится как JSON или XML-документов или элементов в хранилище NoSQL, таких как Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="b5a4d-111">Структурно запрос hello основанная на наличие нескольких дочерних элементов, которые требуется toobe поиска и фильтрации.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="b5a4d-112">В качестве отправной точки для наглядного hello решение выполните hello следующий документ JSON, который содержит набор контакты в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="b5a4d-113">Хотя hello поля с именем «id», «name» и «компания» могут легко быть сопоставлены одному как поля в индекс поиска Azure, поле «расположение» hello содержит массив расположений, применения оба набора идентификаторов расположение, а также расположение описания.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="b5a4d-114">Учитывая, что поиск Azure не имеет тип данных, который поддерживает это, мы должны toomodel иначе это в поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="b5a4d-115">Этот метод также представлено Evans Кирк в записи блога [индексирования DocumentDB с поиском Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), который демонстрирует метод, называемый «обработки прозрачности hello данных», согласно которому будет иметь поле с именем `locationsID` и `locationsDescription` которые оба [коллекций](https://msdn.microsoft.com/library/azure/dn798938.aspx) (или массив строк).</span><span class="sxs-lookup"><span data-stu-id="b5a4d-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="b5a4d-116">Часть 1: Сведение hello массива в отдельные поля</span><span class="sxs-lookup"><span data-stu-id="b5a4d-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="b5a4d-117">toocreate индекс поиска Azure, который допустим для этого набора данных, создайте отдельные поля для вложенных подструктуре hello: `locationsID` и `locationsDescription` с типом данных [коллекций](https://msdn.microsoft.com/library/azure/dn798938.aspx) (или массив строк).</span><span class="sxs-lookup"><span data-stu-id="b5a4d-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="b5a4d-118">В этих полях будет индексировать hello значения "1" и "2" в hello `locationsID` поля для значений John Smith "и" hello, "3" и "4" в hello `locationsID` для Jen Campbell.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="b5a4d-119">Данные в Поиске Azure будут выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b5a4d-119">Your data within Azure Search would look like this:</span></span> 

![пример данных, 2 строки](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="b5a4d-121">Часть 2: Добавление поля коллекции в определение индекса hello</span><span class="sxs-lookup"><span data-stu-id="b5a4d-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="b5a4d-122">В схеме индекса hello hello определения полей может выглядеть аналогичный пример toothis.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="b5a4d-123">Проверить режимы работы поиска и при необходимости расширить индекс hello</span><span class="sxs-lookup"><span data-stu-id="b5a4d-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="b5a4d-124">При условии, что индекс созданного hello hello загруженных данных, теперь можно проверить выполнение hello решения tooverify поиска запросов на hello набора данных.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="b5a4d-125">Каждое поле типа **Коллекция** должно поддерживать **поиск**, **фильтрацию** и **поиск с использованием фасетов**.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="b5a4d-126">Вы должны быть запросов может toorun как:</span><span class="sxs-lookup"><span data-stu-id="b5a4d-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="b5a4d-127">Поиск всех лиц, которые работают на «Adventureworks штаб-квартире» hello.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="b5a4d-128">Получение числа hello количество пользователей, работающих в «Домашнего офиса».</span><span class="sxs-lookup"><span data-stu-id="b5a4d-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="b5a4d-129">Hello людей, которые работают на «Домашнего офиса» показано, какие офисов, они работают вместе с count hello людей в каждом местоположении.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="b5a4d-130">Где друг от друга, этот метод становится — при необходимости toodo поиск, который объединяет ИД расположения hello как, так и описание размещения hello.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="b5a4d-131">Например:</span><span class="sxs-lookup"><span data-stu-id="b5a4d-131">For example:</span></span>

* <span data-ttu-id="b5a4d-132">Найти всех людей, работающих в главном офисе (значение Home Office) с идентификатором расположения 4.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="b5a4d-133">Если вы вспомните исходного содержимого hello выглядело следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b5a4d-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="b5a4d-134">Однако теперь, когда был разделен hello данных в отдельные поля, у нас есть не может определить, если слишком относятся hello домашнего офиса для Jen Campbell`locationsID 3` или `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="b5a4d-135">toohandle в данном случае определение другого поля в индексе hello, объединяющее все данные hello в одну коллекцию.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="b5a4d-136">В нашем примере мы называем это поле `locationsCombined` и будет разделить hello содержимое с `||` несмотря на то, что можно выбрать любой разделитель, которая будет уникальный набор символов для содержимого.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="b5a4d-137">Например:</span><span class="sxs-lookup"><span data-stu-id="b5a4d-137">For example:</span></span> 

![пример данных, 2 строки с разделителем](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="b5a4d-139">С помощью поля `locationsCombined` теперь можно разместить еще больше запросов, например:</span><span class="sxs-lookup"><span data-stu-id="b5a4d-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="b5a4d-140">отображение числа людей, работающих в главном офисе (значение Home Office) с идентификатором расположения "4";</span><span class="sxs-lookup"><span data-stu-id="b5a4d-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="b5a4d-141">поиск людей, работающих в главном офисе (значение Home Office) с идентификатором расположения "4".</span><span class="sxs-lookup"><span data-stu-id="b5a4d-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="b5a4d-142">Ограничения</span><span class="sxs-lookup"><span data-stu-id="b5a4d-142">Limitations</span></span>
<span data-ttu-id="b5a4d-143">Этот метод полезен в ряде сценариев, но не подходит в каждом случае.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="b5a4d-144">Например:</span><span class="sxs-lookup"><span data-stu-id="b5a4d-144">For example:</span></span>

1. <span data-ttu-id="b5a4d-145">Если у вас набор статических полей в типе сложных данных и возникла не toomap способом все возможные hello типами tooa одно поле.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="b5a4d-146">При обновлении hello вложенных объектов требуется некоторые дополнительные действия toodetermine точно, требующие обновления в индекс поиска Azure hello toobe</span><span class="sxs-lookup"><span data-stu-id="b5a4d-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="b5a4d-147">Пример кода</span><span class="sxs-lookup"><span data-stu-id="b5a4d-147">Sample code</span></span>
<span data-ttu-id="b5a4d-148">Можно увидеть пример на tooindex сложных данных JSON настроек в поиске Azure и выполнять запросы через этот набор данных на этом [в репозитории GitHub](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="b5a4d-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="b5a4d-149">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b5a4d-149">Next step</span></span>
<span data-ttu-id="b5a4d-150">[Голоса для собственная поддержка для сложных типов данных](https://feedback.azure.com/forums/263029-azure-search) на hello UserVoice поиска Azure страницы и укажите любые дополнительные входные данные, желательно нам tooconsider относительно реализации функций.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="b5a4d-151">Также можно войти toome непосредственно в Twitter с @liamca.</span><span class="sxs-lookup"><span data-stu-id="b5a4d-151">You can also reach out toome directly on Twitter at @liamca.</span></span>

