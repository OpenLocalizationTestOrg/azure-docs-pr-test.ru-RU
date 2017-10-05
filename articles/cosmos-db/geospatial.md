---
title: "Работа с геопространственными данными в Azure Cosmos DB | Документация Майкрософт"
description: "Сведения о создании, индексировании и запрашивании пространственных объектов в Azure Cosmos DB и API DocumentDB."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d5785c81fb597e7d30eb7d3a880e7194d8358ed5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="9eee0-103">Работа с геопространственными данными и данными расположений GeoJSON в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9eee0-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="9eee0-104">Эта статья содержит вводную информацию о геопространственной функциональности [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="9eee0-104">This article is an introduction to the geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="9eee0-105">После прочтения этой статьи вы сможете ответить на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="9eee0-105">After reading this, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="9eee0-106">Как хранить пространственные данные в Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="9eee0-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="9eee0-107">Как запрашивать геопространственные данные в Azure Cosmos DB с помощью SQL и LINQ?</span><span class="sxs-lookup"><span data-stu-id="9eee0-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="9eee0-108">Как включить или отключить пространственное индексирование в Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="9eee0-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="9eee0-109">В этой статье показано, как работать с пространственными данными с помощью API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="9eee0-109">This article shows how to work with spatial data with the DocumentDB API.</span></span> <span data-ttu-id="9eee0-110">Примеры кода можно найти в [следующем проекте GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="9eee0-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-to-spatial-data"></a><span data-ttu-id="9eee0-111">Общие сведения о пространственных данных</span><span class="sxs-lookup"><span data-stu-id="9eee0-111">Introduction to spatial data</span></span>
<span data-ttu-id="9eee0-112">Пространственные данные описывают положение и форму объектов в пространстве.</span><span class="sxs-lookup"><span data-stu-id="9eee0-112">Spatial data describes the position and shape of objects in space.</span></span> <span data-ttu-id="9eee0-113">В большинстве приложений они соответствуют объектам на поверхности Земли, т. е. геопространственным данным.</span><span class="sxs-lookup"><span data-stu-id="9eee0-113">In most applications, these correspond to objects on the earth, i.e. geospatial data.</span></span> <span data-ttu-id="9eee0-114">Пространственные данные могут использоваться для представления местонахождения человека, мест, представляющих интерес, или границ города или озера.</span><span class="sxs-lookup"><span data-stu-id="9eee0-114">Spatial data can be used to represent the location of a person, a place of interest, or the boundary of a city, or a lake.</span></span> <span data-ttu-id="9eee0-115">Наиболее распространенные случаи часто включают запросы близости, например "найти все кафе рядом с моим текущим местоположением".</span><span class="sxs-lookup"><span data-stu-id="9eee0-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="9eee0-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="9eee0-116">GeoJSON</span></span>
<span data-ttu-id="9eee0-117">Azure Cosmos DB поддерживает индексацию и запросы к геопространственным данным точки, представляемым [спецификацией GeoJSON](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="9eee0-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using the [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="9eee0-118">Структуры данных GeoJSON всегда являются действительными объектами JSON, поэтому их можно сохранять и опрашивать с помощью Azure Cosmos DB без специальных средств или библиотек.</span><span class="sxs-lookup"><span data-stu-id="9eee0-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="9eee0-119">Пакеты SDK Azure Cosmos DB предоставляют вспомогательные классы и методы, которые позволяют легко работать с пространственными данными.</span><span class="sxs-lookup"><span data-stu-id="9eee0-119">The Azure Cosmos DB SDKs provide helper classes and methods that make it easy to work with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="9eee0-120">Точки, объекты LineString и многоугольники</span><span class="sxs-lookup"><span data-stu-id="9eee0-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="9eee0-121">**Точка** обозначает одно положение в пространстве.</span><span class="sxs-lookup"><span data-stu-id="9eee0-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="9eee0-122">В геопространственных данных точка представляет точное расположение, которое может быть адресом продуктового магазина, киоска, точкой расположения автомобиля или города.</span><span class="sxs-lookup"><span data-stu-id="9eee0-122">In geospatial data, a Point represents the exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="9eee0-123">В GeoJSON (и Azure Cosmos DB) точка представляется в виде пары координат или широты и долготы.</span><span class="sxs-lookup"><span data-stu-id="9eee0-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="9eee0-124">Ниже приведен пример JSON для точки.</span><span class="sxs-lookup"><span data-stu-id="9eee0-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="9eee0-125">**Точки в базе данных Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="9eee0-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="9eee0-126">В спецификации GeoJSON сначала указывается широта, затем долгота.</span><span class="sxs-lookup"><span data-stu-id="9eee0-126">The GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="9eee0-127">Как и в других картах, широта и долгота представляют собой углы и выражаются в градусах.</span><span class="sxs-lookup"><span data-stu-id="9eee0-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="9eee0-128">Значение долготы отсчитывается от нулевого меридиана и находится в диапазоне от -180 до 180.0 градусов, а значение широты отсчитывается от экватора и находится в диапазоне от-90.0 до 90.0 градусов.</span><span class="sxs-lookup"><span data-stu-id="9eee0-128">Longitude values are measured from the Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from the equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="9eee0-129">В Azure Cosmos DB координаты интерпретируются в соответствии с системой координат WGS-84.</span><span class="sxs-lookup"><span data-stu-id="9eee0-129">Azure Cosmos DB interprets coordinates as represented per the WGS-84 reference system.</span></span> <span data-ttu-id="9eee0-130">Дополнительные сведения о системах координат см. ниже.</span><span class="sxs-lookup"><span data-stu-id="9eee0-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="9eee0-131">Их можно включить в документ Azure Cosmos DB, как показано в следующем примере профиля пользователя, содержащего данные о местоположении:</span><span class="sxs-lookup"><span data-stu-id="9eee0-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="9eee0-132">**Использование профиля с данными о местоположении, которые хранятся в Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="9eee0-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

<span data-ttu-id="9eee0-133">Наряду с точками GeoJSON также поддерживает объекты LineString и многоугольники.</span><span class="sxs-lookup"><span data-stu-id="9eee0-133">In addition to points, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="9eee0-134">**Объект LineString** представляет собой последовательность из двух или более точек в пространстве и отрезков, которые их соединяют.</span><span class="sxs-lookup"><span data-stu-id="9eee0-134">**LineStrings** represent a series of two or more points in space and the line segments that connect them.</span></span> <span data-ttu-id="9eee0-135">В геопространственных данных объекты LineString обычно используются для представления автомагистралей или рек.</span><span class="sxs-lookup"><span data-stu-id="9eee0-135">In geospatial data, LineStrings are commonly used to represent highways or rivers.</span></span> <span data-ttu-id="9eee0-136">**Многоугольник** представляет собой область, ограниченную соединенными друг с другом точками, которая образует замкнутый объект LineString.</span><span class="sxs-lookup"><span data-stu-id="9eee0-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="9eee0-137">Многоугольники обычно используются для представления естественных природных образований, таких как озера, или географических единиц, таких как города и области.</span><span class="sxs-lookup"><span data-stu-id="9eee0-137">Polygons are commonly used to represent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="9eee0-138">Ниже приведен пример многоугольника в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9eee0-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="9eee0-139">**Многоугольники в GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="9eee0-139">**Polygons in GeoJSON**</span></span>

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> <span data-ttu-id="9eee0-140">По спецификации GeoJSON для действительного многоугольника последняя пара координат должна совпадать с первой, чтобы фигура стала замкнутой.</span><span class="sxs-lookup"><span data-stu-id="9eee0-140">The GeoJSON specification requires that for valid Polygons, the last coordinate pair provided should be the same as the first, to create a closed shape.</span></span>
> 
> <span data-ttu-id="9eee0-141">Точки внутри многоугольника должны указываться в порядке против часовой стрелки.</span><span class="sxs-lookup"><span data-stu-id="9eee0-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="9eee0-142">Если точки указаны в порядке по часовой стрелке, то многоугольник представляет регион, расположенный снаружи от него.</span><span class="sxs-lookup"><span data-stu-id="9eee0-142">A Polygon specified in clockwise order represents the inverse of the region within it.</span></span>
> 
> 

<span data-ttu-id="9eee0-143">Наряду с точками, объектами LineString и многоугольниками в GeoJSON также определяется способ группировки нескольких геопространственных местоположений, а также способ задания произвольных свойств географического положения в качестве **Функций**.</span><span class="sxs-lookup"><span data-stu-id="9eee0-143">In addition to Point, LineString and Polygon, GeoJSON also specifies the representation for how to group multiple geospatial locations, as well as how to associate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="9eee0-144">Так как эти объекты являются действительными объектами JSON, их можно хранить и обрабатывать в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9eee0-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="9eee0-145">Однако Azure Cosmos DB поддерживает только автоматическую индексацию точек.</span><span class="sxs-lookup"><span data-stu-id="9eee0-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="9eee0-146">Системы координат</span><span class="sxs-lookup"><span data-stu-id="9eee0-146">Coordinate reference systems</span></span>
<span data-ttu-id="9eee0-147">Поскольку Земля имеет неправильную форму, координаты геопространственных данных представляются во многих системах координат, каждая из которых имеет собственные границы отсчета и единицы измерения.</span><span class="sxs-lookup"><span data-stu-id="9eee0-147">Since the shape of the earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="9eee0-148">Например, "Национальная система координат Великобритании" (National Grid of Britain) обладает высокой точностью в Великобритании, но не за ее пределами.</span><span class="sxs-lookup"><span data-stu-id="9eee0-148">For example, the "National Grid of Britain" is a reference system is very accurate for the United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="9eee0-149">Самой популярной системой координат на данный момент является [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="9eee0-149">The most popular CRS in use today is the World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="9eee0-150">WGS-84 используют устройства GPS и многие службы географических карт, в том числе Карты Google и API-интерфейсы Карт Bing.</span><span class="sxs-lookup"><span data-stu-id="9eee0-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="9eee0-151">Azure Cosmos DB поддерживает индексирование и опрашивание геопространственных данных только с использованием WGS-84.</span><span class="sxs-lookup"><span data-stu-id="9eee0-151">Azure Cosmos DB supports indexing and querying of geospatial data using the WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="9eee0-152">Создание документов с пространственными данными</span><span class="sxs-lookup"><span data-stu-id="9eee0-152">Creating documents with spatial data</span></span>
<span data-ttu-id="9eee0-153">При создании документов, содержащих значения GeoJSON, они автоматически индексируются с пространственным индексом в соответствии с политикой индексирования коллекции.</span><span class="sxs-lookup"><span data-stu-id="9eee0-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance to the indexing policy of the collection.</span></span> <span data-ttu-id="9eee0-154">При работе с пакетом SDK Azure Cosmos DB в динамически типизированных языках программирования, таких как Python или Node.js, необходимо создавать действительные объекты GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="9eee0-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="9eee0-155">**Создание документа с геопространственными данными в Node.js**</span><span class="sxs-lookup"><span data-stu-id="9eee0-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within the callback
});
```

<span data-ttu-id="9eee0-156">Если вы работаете с API DocumentDB, то можете использовать классы `Point` и `Polygon` в пространстве имен `Microsoft.Azure.Documents.Spatial` для включения информации о местоположении в свои объекты приложения.</span><span class="sxs-lookup"><span data-stu-id="9eee0-156">If you're working with the DocumentDB APIs, you can use the `Point` and `Polygon` classes within the `Microsoft.Azure.Documents.Spatial` namespace to embed location information within your application objects.</span></span> <span data-ttu-id="9eee0-157">Эти классы помогают упростить сериализацию и десериализацию пространственных данных в GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="9eee0-157">These classes help simplify the serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="9eee0-158">**Создание документа с геопространственными данными в .NET**</span><span class="sxs-lookup"><span data-stu-id="9eee0-158">**Create Document with Geospatial data in .NET**</span></span>

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

<span data-ttu-id="9eee0-159">Если у вас нет информации о широте и долготе, но есть физический адрес или название местоположения, например название города или страны, то фактические координаты можно определить с помощью службы геокодирования, такой как служба REST Карт Bing.</span><span class="sxs-lookup"><span data-stu-id="9eee0-159">If you don't have the latitude and longitude information, but have the physical addresses or location name like city or country, you can look up the actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="9eee0-160">Дополнительные сведения о геокодировании в Картах Bing можно найти [здесь](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="9eee0-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="9eee0-161">Типы запросов к пространственным данным</span><span class="sxs-lookup"><span data-stu-id="9eee0-161">Querying spatial types</span></span>
<span data-ttu-id="9eee0-162">Теперь, когда мы рассмотрели способы внедрения геопространственных данных, обратимся к тому, как запрашивать эти данные в Azure Cosmos DB с помощью SQL и LINQ.</span><span class="sxs-lookup"><span data-stu-id="9eee0-162">Now that we've taken a look at how to insert geospatial data, let's take a look at how to query this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="9eee0-163">Встроенные функции для обработки пространственных данных в SQL</span><span class="sxs-lookup"><span data-stu-id="9eee0-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="9eee0-164">Azure Cosmos DB поддерживает следующие встроенные функции Открытого геопространственного консорциума (OGC) для выполнения запросов к геопространственным данным.</span><span class="sxs-lookup"><span data-stu-id="9eee0-164">Azure Cosmos DB supports the following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="9eee0-165">Дополнительные сведения о всех встроенных функциях SQL см. в статье [SQL-запросы и синтаксис SQL в Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="9eee0-165">For more details on the complete set of built-in functions in the SQL language, please refer to [Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="9eee0-166"><strong>Использование</strong></span><span class="sxs-lookup"><span data-stu-id="9eee0-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="9eee0-167"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="9eee0-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9eee0-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="9eee0-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="9eee0-169">Возвращает расстояние между двумя выражениями точек GeoJSON, многоугольников или объектов LineString.</span><span class="sxs-lookup"><span data-stu-id="9eee0-169">Returns the distance between the two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9eee0-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="9eee0-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="9eee0-171">Возвращает логическое выражение, указывающее, располагается ли первый объект GeoJSON (точка, многоугольник или LineString) внутри второго объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="9eee0-171">Returns a Boolean expression indicating whether the first GeoJSON object (Point, Polygon, or LineString) is within the second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9eee0-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="9eee0-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="9eee0-173">Возвращает логическое выражение, указывающее, пересекаются ли два объекта GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="9eee0-173">Returns a Boolean expression indicating whether the two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9eee0-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="9eee0-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="9eee0-175">Возвращает логическое значение, указывающее, является ли действительным выражение GeoJSON (точка, многоугольник или LineString).</span><span class="sxs-lookup"><span data-stu-id="9eee0-175">Returns a Boolean value indicating whether the specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="9eee0-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="9eee0-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="9eee0-177">Возвращает значение JSON, содержащее логическое значение, указывающее, является ли выражение GeoJSON (точка, многоугольник или LineString) действительным. Если оно является недействительным, то возвращаемое значение также содержит строку с описанием причины.</span><span class="sxs-lookup"><span data-stu-id="9eee0-177">Returns a JSON value containing a Boolean value if the specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally the reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="9eee0-178">Пространственные функции могут использоваться для выполнения запросов близости к пространственным данным.</span><span class="sxs-lookup"><span data-stu-id="9eee0-178">Spatial functions can be used to perform proximity queries against spatial data.</span></span> <span data-ttu-id="9eee0-179">Например, ниже приведен запрос, возвращающий все документы семейств, которые находятся в пределах 30 км от заданного расположения, с помощью встроенной функции ST_DISTANCE.</span><span class="sxs-lookup"><span data-stu-id="9eee0-179">For example, here's a query that returns all family documents that are within 30 km of the specified location using the ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="9eee0-180">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="9eee0-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="9eee0-181">**Результат**</span><span class="sxs-lookup"><span data-stu-id="9eee0-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="9eee0-182">При включении пространственного индексирования в политику индексирования "запросы для определения расстояния" будут эффективно обрабатываться с помощью индекса.</span><span class="sxs-lookup"><span data-stu-id="9eee0-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through the index.</span></span> <span data-ttu-id="9eee0-183">Дополнительные сведения о пространственном индексировании см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="9eee0-183">For more details on spatial indexing, please see the section below.</span></span> <span data-ttu-id="9eee0-184">При отсутствии пространственного индекса для указанных путей вы все равно сможете выполнять пространственные запросы, указывая заголовок запроса `x-ms-documentdb-query-enable-scan` со значением "true".</span><span class="sxs-lookup"><span data-stu-id="9eee0-184">If you don't have a spatial index for the specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with the value set to "true".</span></span> <span data-ttu-id="9eee0-185">В .NET это можно сделать, указав необязательный аргумент запроса **FeedOptions** со свойством [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery), имеющим значение true.</span><span class="sxs-lookup"><span data-stu-id="9eee0-185">In .NET, this can be done by passing the optional **FeedOptions** argument to queries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set to true.</span></span> 

<span data-ttu-id="9eee0-186">С помощью ST_WITHIN можно проверить, находится ли точка внутри многоугольника.</span><span class="sxs-lookup"><span data-stu-id="9eee0-186">ST_WITHIN can be used to check if a point lies within a Polygon.</span></span> <span data-ttu-id="9eee0-187">Многоугольники обычно используются для представления границ, например почтовых зон, границ штатов или границ природных образований.</span><span class="sxs-lookup"><span data-stu-id="9eee0-187">Commonly Polygons are used to represent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="9eee0-188">При включении пространственного индексирования в политику индексирования "запросы нахождения внутри" будут эффективно обрабатываться с помощью индекса.</span><span class="sxs-lookup"><span data-stu-id="9eee0-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through the index.</span></span> 

<span data-ttu-id="9eee0-189">Аргументы многоугольника в ST_WITHIN могут содержать только одно кольцо, т. е. в многоугольниках не должно быть "дыр".</span><span class="sxs-lookup"><span data-stu-id="9eee0-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. the Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="9eee0-190">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="9eee0-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="9eee0-191">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="9eee0-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="9eee0-192">По аналогии с несоответствием типов в запросе Azure Cosmos DB: если значение местоположения, указанное в любом из аргументов, имеет неправильный формат или является недопустимым, то оно приравнивается к значению **не определено** и соответствующий документ исключается из результатов запроса.</span><span class="sxs-lookup"><span data-stu-id="9eee0-192">Similar to how mismatched types works in Azure Cosmos DB query, if the location value specified in either argument is malformed or invalid, then it will evaluate to **undefined** and the evaluated document to be skipped from the query results.</span></span> <span data-ttu-id="9eee0-193">Если запрос не возвращает результатов, выполните запрос ST_ISVALIDDETAILED для выяснения причин, по которым тип пространственных данных является недействительным.</span><span class="sxs-lookup"><span data-stu-id="9eee0-193">If your query returns no results, run ST_ISVALIDDETAILED To debug why the spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="9eee0-194">Azure Cosmos DB поддерживает также выполнение обратных запросов, т. е. можно индексировать многоугольники или линии в Azure Cosmos DB, а затем выполнять запросы к областям, которые содержат указанную точку.</span><span class="sxs-lookup"><span data-stu-id="9eee0-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for the areas that contain a specified point.</span></span> <span data-ttu-id="9eee0-195">Этот шаблон часто используется в логистике, например, чтобы определить, когда грузовик прибывает в указанную область или выезжает из нее.</span><span class="sxs-lookup"><span data-stu-id="9eee0-195">This pattern is commonly used in logistics to identify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="9eee0-196">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="9eee0-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="9eee0-197">**Результат**</span><span class="sxs-lookup"><span data-stu-id="9eee0-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="9eee0-198">Чтобы проверить, является ли пространственный объект действительным, можно воспользоваться ST_ISVALID и ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="9eee0-198">ST_ISVALID and ST_ISVALIDDETAILED can be used to check if a spatial object is valid.</span></span> <span data-ttu-id="9eee0-199">Например, следующий запрос проверяет действительность точки, значение широты для которой выходит за пределы допустимого диапазона (-132.8).</span><span class="sxs-lookup"><span data-stu-id="9eee0-199">For example, the following query checks the validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="9eee0-200">ST_ISVALID возвращает логическое значение, а ST_ISVALIDDETAILED возвращает логическое значение и строку, содержащую причину, по которой значение считается недействительным.</span><span class="sxs-lookup"><span data-stu-id="9eee0-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns the Boolean and a string containing the reason why it is considered invalid.</span></span>

<span data-ttu-id="9eee0-201">** Запрос **</span><span class="sxs-lookup"><span data-stu-id="9eee0-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="9eee0-202">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="9eee0-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="9eee0-203">Эти функции также могут использоваться для проверки многоугольников.</span><span class="sxs-lookup"><span data-stu-id="9eee0-203">These functions can also be used to validate Polygons.</span></span> <span data-ttu-id="9eee0-204">Например, здесь мы используем ST_ISVALIDDETAILED для того, чтобы проверить, что многоугольник не является замкнутым.</span><span class="sxs-lookup"><span data-stu-id="9eee0-204">For example, here we use ST_ISVALIDDETAILED to validate a Polygon that is not closed.</span></span> 

<span data-ttu-id="9eee0-205">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="9eee0-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="9eee0-206">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="9eee0-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "The Polygon input is not valid because the start and end points of the ring number 1 are not the same. Each ring of a Polygon must have the same start and end points." 
          }
    }]

### <a name="linq-querying-in-the-net-sdk"></a><span data-ttu-id="9eee0-207">Запросы LINQ в пакете SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="9eee0-207">LINQ Querying in the .NET SDK</span></span>
<span data-ttu-id="9eee0-208">В пакете SDK для .NET DocumentDB также содержатся заглушки методов `Distance()` и `Within()` для использования с помощью выражений LINQ.</span><span class="sxs-lookup"><span data-stu-id="9eee0-208">The DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="9eee0-209">Поставщик LINQ DocumentDB преобразует эти вызовы методов в эквивалентные вызовы встроенных функций SQL (ST_DISTANCE и ST_WITHIN соответственно).</span><span class="sxs-lookup"><span data-stu-id="9eee0-209">The DocumentDB LINQ provider translates these method calls to the equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="9eee0-210">Ниже приведен пример запроса LINQ, который находит все документы в коллекции Azure Cosmos DB с "местоположением" в радиусе 30 км от указанной точки.</span><span class="sxs-lookup"><span data-stu-id="9eee0-210">Here's an example of a LINQ query that finds all documents in the Azure Cosmos DB collection whose "location" value is within a radius of 30km of the specified point using LINQ.</span></span>

<span data-ttu-id="9eee0-211">**Запросы LINQ для определения расстояния**</span><span class="sxs-lookup"><span data-stu-id="9eee0-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="9eee0-212">Ниже приведен аналогичный запрос для поиска всех документов с "местоположением" в пределах указанного прямоугольника или многоугольника.</span><span class="sxs-lookup"><span data-stu-id="9eee0-212">Similarly, here's a query for finding all the documents whose "location" is within the specified box/Polygon.</span></span> 

<span data-ttu-id="9eee0-213">**Запросы LINQ для определения принадлежности**</span><span class="sxs-lookup"><span data-stu-id="9eee0-213">**LINQ query for Within**</span></span>

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


<span data-ttu-id="9eee0-214">Теперь, когда мы познакомились с запросами к документам с помощью LINQ и SQL, рассмотрим способы настройки Azure Cosmos DB для пространственного индексирования.</span><span class="sxs-lookup"><span data-stu-id="9eee0-214">Now that we've taken a look at how to query documents using LINQ and SQL, let's take a look at how to configure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="9eee0-215">Индексация</span><span class="sxs-lookup"><span data-stu-id="9eee0-215">Indexing</span></span>
<span data-ttu-id="9eee0-216">Как описано в документе [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) (Схемонезависимое индексирование в Azure Cosmos DB), СУБД Azure Cosmos DB является по-настоящему схемонезависимой и обеспечивает превосходную поддержку JSON.</span><span class="sxs-lookup"><span data-stu-id="9eee0-216">As we described in the [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine to be truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="9eee0-217">В СУБД Azure Cosmos DB с оптимизацией записи также реализована поддержка пространственных данных (точек, многоугольников и линий), представленных в стандарте GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="9eee0-217">The write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in the GeoJSON standard.</span></span>

<span data-ttu-id="9eee0-218">По сути, геометрия формируется путем проецирования геодезических координат на двумерную плоскость, которая затем постепенно разделяется на ячейки с помощью **дерева квадрантов**.</span><span class="sxs-lookup"><span data-stu-id="9eee0-218">In a nutshell, the geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="9eee0-219">Эти ячейки связываются с одномерным пространством на основе расположения ячейки на **кривой заполнения гильбертова пространства**, что позволяет сохранить расположение точек.</span><span class="sxs-lookup"><span data-stu-id="9eee0-219">These cells are mapped to 1D based on the location of the cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="9eee0-220">Кроме того, при индексировании данных расположения ячейки проходят так называемый процесс **тесселяции**, т. е. все ячейки, которые пересекают расположение, обнаруживаются и сохраняются в виде ключей в индексе Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9eee0-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all the cells that intersect a location are identified and stored as keys in the Azure Cosmos DB index.</span></span> <span data-ttu-id="9eee0-221">Во время обработки запроса такие аргументы, как точки и многоугольники, также тесселируются для извлечения диапазонов идентификаторов соответствующих ячеек, а затем используются для получения данных из индекса.</span><span class="sxs-lookup"><span data-stu-id="9eee0-221">At query time, arguments like points and Polygons are also tessellated to extract the relevant cell ID ranges, then used to retrieve data from the index.</span></span>

<span data-ttu-id="9eee0-222">При указании политики индексирования, которая включает пространственный индекс для /* (все пути), все точки, обнаруженные внутри коллекции, индексируются для эффективного выполнения пространственных запросов (ST_WITHIN и ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="9eee0-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within the collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="9eee0-223">Пространственные индексы не имеют значения точности и всегда используют значение точности по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9eee0-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="9eee0-224">Azure Cosmos DB поддерживает автоматическое индексирование данных типа Point, Polygon и LineString.</span><span class="sxs-lookup"><span data-stu-id="9eee0-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="9eee0-225">Следующий фрагмент JSON демонстрирует политику индексирования с включенным пространственным индексированием, т. е. индексированием любой точки GeoJSON, обнаруженной в документах, для пространственных запросов.</span><span class="sxs-lookup"><span data-stu-id="9eee0-225">The following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="9eee0-226">При изменении политики индексирования с помощью портала Azure можно указать следующий JSON политики индексирования для включения в коллекции пространственного индексирования.</span><span class="sxs-lookup"><span data-stu-id="9eee0-226">If you are modifying the indexing policy using the Azure Portal, you can specify the following JSON for indexing policy to enable spatial indexing on your collection.</span></span>

<span data-ttu-id="9eee0-227">**JSON политики пространственного индексирования коллекций для точек и многоугольников**</span><span class="sxs-lookup"><span data-stu-id="9eee0-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

<span data-ttu-id="9eee0-228">Ниже приведен фрагмент кода .NET, который показывает, как создать коллекцию со включенным пространственным индексированием для всех путей, содержащих точки.</span><span class="sxs-lookup"><span data-stu-id="9eee0-228">Here's a code snippet in .NET that shows how to create a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="9eee0-229">**Создание коллекции с пространственным индексированием**</span><span class="sxs-lookup"><span data-stu-id="9eee0-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override to turn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="9eee0-230">А вот как можно изменить существующую коллекцию, чтобы воспользоваться преимуществами пространственного индексирования всех точек, которые хранятся в документах.</span><span class="sxs-lookup"><span data-stu-id="9eee0-230">And here's how you can modify an existing collection to take advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="9eee0-231">**Изменение коллекции с пространственным индексированием**</span><span class="sxs-lookup"><span data-stu-id="9eee0-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing to complete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="9eee0-232">Если значение расположения GeoJSON в документе сформировано неверно или является недействительным, оно не будет индексироваться для пространственных запросов.</span><span class="sxs-lookup"><span data-stu-id="9eee0-232">If the location GeoJSON value within the document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="9eee0-233">Проверить значение расположения можно с помощью ST_ISVALID и ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="9eee0-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="9eee0-234">Если определение коллекции включает ключ секции, информация о ходе выполнения преобразования индекса не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="9eee0-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9eee0-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9eee0-235">Next steps</span></span>
<span data-ttu-id="9eee0-236">Теперь, когда вы ознакомились с предварительными сведениями о поддержке геопространственных данных в Azure Cosmos DB, вы можете сделать следующее.</span><span class="sxs-lookup"><span data-stu-id="9eee0-236">Now that you've learnt about how to get started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="9eee0-237">Начните программировать с помощью [примеров кода для работы с геопространственными данными посредством .NET, доступных на GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="9eee0-237">Start coding with the [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="9eee0-238">Освойте геопространственные запросы на [Игровой площадке запросов Azure Cosmos DB](http://www.documentdb.com/sql/demo#geospatial).</span><span class="sxs-lookup"><span data-stu-id="9eee0-238">Get hands on with geospatial querying at the [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="9eee0-239">Дополнительные сведения о запросах Azure Cosmos DB см. [здесь](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="9eee0-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="9eee0-240">Дополнительные сведения о политиках индексации в Azure Cosmos DB см. в [этой статье](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="9eee0-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

