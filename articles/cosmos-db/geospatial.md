---
title: "aaaWorking с геопространственных данных в базе данных Azure Cosmos | Документы Microsoft"
description: "Сведения об toocreate, индекс и запрос пространственных объектов с помощью Azure Cosmos DB и hello DocumentDB API."
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
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a><span data-ttu-id="8e155-103">Работа с геопространственными данными и данными расположений GeoJSON в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8e155-103">Working with geospatial and GeoJSON location data in Azure Cosmos DB</span></span>
<span data-ttu-id="8e155-104">В этой статье представлено введение toohello геопространственные функции [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="8e155-104">This article is an introduction toohello geospatial functionality in [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="8e155-105">После прочтения этого, можно будет tooanswer hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="8e155-105">After reading this, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="8e155-106">Как хранить пространственные данные в Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="8e155-106">How do I store spatial data in Azure Cosmos DB?</span></span>
* <span data-ttu-id="8e155-107">Как запрашивать геопространственные данные в Azure Cosmos DB с помощью SQL и LINQ?</span><span class="sxs-lookup"><span data-stu-id="8e155-107">How can I query geospatial data in Azure Cosmos DB in SQL and LINQ?</span></span>
* <span data-ttu-id="8e155-108">Как включить или отключить пространственное индексирование в Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="8e155-108">How do I enable or disable spatial indexing in Azure Cosmos DB?</span></span>

<span data-ttu-id="8e155-109">В этой статье показано, как toowork с пространственными данными с hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="8e155-109">This article shows how toowork with spatial data with hello DocumentDB API.</span></span> <span data-ttu-id="8e155-110">Примеры кода можно найти в [следующем проекте GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="8e155-110">Please see this [GitHub project](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) for code samples.</span></span>

## <a name="introduction-toospatial-data"></a><span data-ttu-id="8e155-111">Введение toospatial данных</span><span class="sxs-lookup"><span data-stu-id="8e155-111">Introduction toospatial data</span></span>
<span data-ttu-id="8e155-112">Пространственные данные Описание позиции hello и форме объектов в пространстве.</span><span class="sxs-lookup"><span data-stu-id="8e155-112">Spatial data describes hello position and shape of objects in space.</span></span> <span data-ttu-id="8e155-113">В большинстве приложений они соответствуют tooobjects на Земле hello, т. е. геопространственных данных.</span><span class="sxs-lookup"><span data-stu-id="8e155-113">In most applications, these correspond tooobjects on hello earth, i.e. geospatial data.</span></span> <span data-ttu-id="8e155-114">Пространственные данные могут быть расположение hello используется toorepresent человека, мест, представляющих интерес или границ hello города или озере.</span><span class="sxs-lookup"><span data-stu-id="8e155-114">Spatial data can be used toorepresent hello location of a person, a place of interest, or hello boundary of a city, or a lake.</span></span> <span data-ttu-id="8e155-115">Наиболее распространенные случаи часто включают запросы близости, например "найти все кафе рядом с моим текущим местоположением".</span><span class="sxs-lookup"><span data-stu-id="8e155-115">Common use cases often involve proximity queries, for e.g., "find all coffee shops near my current location".</span></span> 

### <a name="geojson"></a><span data-ttu-id="8e155-116">GeoJSON</span><span class="sxs-lookup"><span data-stu-id="8e155-116">GeoJSON</span></span>
<span data-ttu-id="8e155-117">Azure Cosmos DB поддерживает индексирование и запросы геопространственных точки данных, которые представляются в виде hello [GeoJSON спецификации](https://tools.ietf.org/html/rfc7946).</span><span class="sxs-lookup"><span data-stu-id="8e155-117">Azure Cosmos DB supports indexing and querying of geospatial point data that's represented using hello [GeoJSON specification](https://tools.ietf.org/html/rfc7946).</span></span> <span data-ttu-id="8e155-118">Структуры данных GeoJSON всегда являются действительными объектами JSON, поэтому их можно сохранять и опрашивать с помощью Azure Cosmos DB без специальных средств или библиотек.</span><span class="sxs-lookup"><span data-stu-id="8e155-118">GeoJSON data structures are always valid JSON objects, so they can be stored and queried using Azure Cosmos DB without any specialized tools or libraries.</span></span> <span data-ttu-id="8e155-119">Hello пакеты SDK Azure Cosmos DB предоставляют вспомогательные классы и методы, которые позволяют легко toowork с пространственными данными.</span><span class="sxs-lookup"><span data-stu-id="8e155-119">hello Azure Cosmos DB SDKs provide helper classes and methods that make it easy toowork with spatial data.</span></span> 

### <a name="points-linestrings-and-polygons"></a><span data-ttu-id="8e155-120">Точки, объекты LineString и многоугольники</span><span class="sxs-lookup"><span data-stu-id="8e155-120">Points, LineStrings and Polygons</span></span>
<span data-ttu-id="8e155-121">**Точка** обозначает одно положение в пространстве.</span><span class="sxs-lookup"><span data-stu-id="8e155-121">A **Point** denotes a single position in space.</span></span> <span data-ttu-id="8e155-122">В геопространственные данные точки представляет hello точное расположение, которое может быть адрес продуктового магазина, киоске, автомобиль или города.</span><span class="sxs-lookup"><span data-stu-id="8e155-122">In geospatial data, a Point represents hello exact location, which could be a street address of a grocery store, a kiosk, an automobile or a city.</span></span>  <span data-ttu-id="8e155-123">В GeoJSON (и Azure Cosmos DB) точка представляется в виде пары координат или широты и долготы.</span><span class="sxs-lookup"><span data-stu-id="8e155-123">A point is represented in GeoJSON (and Azure Cosmos DB) using its coordinate pair or longitude and latitude.</span></span> <span data-ttu-id="8e155-124">Ниже приведен пример JSON для точки.</span><span class="sxs-lookup"><span data-stu-id="8e155-124">Here's an example JSON for a point.</span></span>

<span data-ttu-id="8e155-125">**Точки в базе данных Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="8e155-125">**Points in Azure Cosmos DB**</span></span>

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> <span data-ttu-id="8e155-126">Спецификация GeoJSON Hello указывает долготы first и широту второй.</span><span class="sxs-lookup"><span data-stu-id="8e155-126">hello GeoJSON specification specifies longitude first and latitude second.</span></span> <span data-ttu-id="8e155-127">Как и в других картах, широта и долгота представляют собой углы и выражаются в градусах.</span><span class="sxs-lookup"><span data-stu-id="8e155-127">Like in other mapping applications, longitude and latitude are angles and represented in terms of degrees.</span></span> <span data-ttu-id="8e155-128">Значения долготы измеряются от главного меридиана hello и находятся в диапазоне от -180 и 180.0 градусов и широту значения отсчитываются от экватора hello и находятся в диапазоне от-90.0 до 90.0 градусов.</span><span class="sxs-lookup"><span data-stu-id="8e155-128">Longitude values are measured from hello Prime Meridian and are between -180 and 180.0 degrees, and latitude values are measured from hello equator and are between -90.0 and 90.0 degrees.</span></span> 
> 
> <span data-ttu-id="8e155-129">Azure Cosmos DB интерпретирует координаты, представленных в системе ссылок WGS 84 hello.</span><span class="sxs-lookup"><span data-stu-id="8e155-129">Azure Cosmos DB interprets coordinates as represented per hello WGS-84 reference system.</span></span> <span data-ttu-id="8e155-130">Дополнительные сведения о системах координат см. ниже.</span><span class="sxs-lookup"><span data-stu-id="8e155-130">Please see below for more details about coordinate reference systems.</span></span>
> 
> 

<span data-ttu-id="8e155-131">Их можно включить в документ Azure Cosmos DB, как показано в следующем примере профиля пользователя, содержащего данные о местоположении:</span><span class="sxs-lookup"><span data-stu-id="8e155-131">This can be embedded in an Azure Cosmos DB document as shown in this example of a user profile containing location data:</span></span>

<span data-ttu-id="8e155-132">**Использование профиля с данными о местоположении, которые хранятся в Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="8e155-132">**Use Profile with Location stored in Azure Cosmos DB**</span></span>

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

<span data-ttu-id="8e155-133">Кроме toopoints GeoJSON поддерживает LineStrings и многоугольники.</span><span class="sxs-lookup"><span data-stu-id="8e155-133">In addition toopoints, GeoJSON also supports LineStrings and Polygons.</span></span> <span data-ttu-id="8e155-134">**LineStrings** представляют ряд двух или более точек в пространстве и hello сегменты линии, которые их соединяют.</span><span class="sxs-lookup"><span data-stu-id="8e155-134">**LineStrings** represent a series of two or more points in space and hello line segments that connect them.</span></span> <span data-ttu-id="8e155-135">В геопространственных данных LineStrings, часто используемые toorepresent автомагистралях или реки.</span><span class="sxs-lookup"><span data-stu-id="8e155-135">In geospatial data, LineStrings are commonly used toorepresent highways or rivers.</span></span> <span data-ttu-id="8e155-136">**Многоугольник** представляет собой область, ограниченную соединенными друг с другом точками, которая образует замкнутый объект LineString.</span><span class="sxs-lookup"><span data-stu-id="8e155-136">A **Polygon** is a boundary of connected points that forms a closed LineString.</span></span> <span data-ttu-id="8e155-137">Многоугольники, часто используемые toorepresent естественное структур как Озера или политическая юрисдикции как города и области.</span><span class="sxs-lookup"><span data-stu-id="8e155-137">Polygons are commonly used toorepresent natural formations like lakes or political jurisdictions like cities and states.</span></span> <span data-ttu-id="8e155-138">Ниже приведен пример многоугольника в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8e155-138">Here's an example of a Polygon in Azure Cosmos DB.</span></span> 

<span data-ttu-id="8e155-139">**Многоугольники в GeoJSON**</span><span class="sxs-lookup"><span data-stu-id="8e155-139">**Polygons in GeoJSON**</span></span>

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
> <span data-ttu-id="8e155-140">Hello GeoJSON спецификация требует допустимый многоугольников hello последней парой координат предоставленный следует hello же, как первого, toocreate hello замкнутую фигуру.</span><span class="sxs-lookup"><span data-stu-id="8e155-140">hello GeoJSON specification requires that for valid Polygons, hello last coordinate pair provided should be hello same as hello first, toocreate a closed shape.</span></span>
> 
> <span data-ttu-id="8e155-141">Точки внутри многоугольника должны указываться в порядке против часовой стрелки.</span><span class="sxs-lookup"><span data-stu-id="8e155-141">Points within a Polygon must be specified in counter-clockwise order.</span></span> <span data-ttu-id="8e155-142">Многоугольник, указанным в заказе по часовой стрелке представляет обратное hello hello области внутри него.</span><span class="sxs-lookup"><span data-stu-id="8e155-142">A Polygon specified in clockwise order represents hello inverse of hello region within it.</span></span>
> 
> 

<span data-ttu-id="8e155-143">В дополнение tooPoint, LineString, а также многоугольников, GeoJSON также задает представление hello как toogroup несколько геопространственных, а также tooassociate произвольные свойства с географическом расположении, что **функция**.</span><span class="sxs-lookup"><span data-stu-id="8e155-143">In addition tooPoint, LineString and Polygon, GeoJSON also specifies hello representation for how toogroup multiple geospatial locations, as well as how tooassociate arbitrary properties with geolocation as a **Feature**.</span></span> <span data-ttu-id="8e155-144">Так как эти объекты являются действительными объектами JSON, их можно хранить и обрабатывать в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8e155-144">Since these objects are valid JSON, they can all be stored and processed in Azure Cosmos DB.</span></span> <span data-ttu-id="8e155-145">Однако Azure Cosmos DB поддерживает только автоматическую индексацию точек.</span><span class="sxs-lookup"><span data-stu-id="8e155-145">However Azure Cosmos DB only supports automatic indexing of points.</span></span>

### <a name="coordinate-reference-systems"></a><span data-ttu-id="8e155-146">Системы координат</span><span class="sxs-lookup"><span data-stu-id="8e155-146">Coordinate reference systems</span></span>
<span data-ttu-id="8e155-147">Поскольку нестандартные фигуры hello hello земли, координаты геопространственных данных представляется во многих системах отсчета координат (CRS), каждый из которых собственных кадров для ссылок и единицы измерения.</span><span class="sxs-lookup"><span data-stu-id="8e155-147">Since hello shape of hello earth is irregular, coordinates of geospatial data is represented in many coordinate reference systems (CRS), each with their own frames of reference and units of measurement.</span></span> <span data-ttu-id="8e155-148">Например, «National сетки для Великобритании» hello является эталонной системы имеет высокую точность для hello United Kingdom, но не вне его.</span><span class="sxs-lookup"><span data-stu-id="8e155-148">For example, hello "National Grid of Britain" is a reference system is very accurate for hello United Kingdom, but not outside it.</span></span> 

<span data-ttu-id="8e155-149">Hello наиболее популярных CRS используется на сегодняшний день является hello системе [WGS 84](http://earth-info.nga.mil/GandG/wgs84/).</span><span class="sxs-lookup"><span data-stu-id="8e155-149">hello most popular CRS in use today is hello World Geodetic System  [WGS-84](http://earth-info.nga.mil/GandG/wgs84/).</span></span> <span data-ttu-id="8e155-150">WGS-84 используют устройства GPS и многие службы географических карт, в том числе Карты Google и API-интерфейсы Карт Bing.</span><span class="sxs-lookup"><span data-stu-id="8e155-150">GPS devices, and many mapping services including Google Maps and Bing Maps APIs use WGS-84.</span></span> <span data-ttu-id="8e155-151">Azure Cosmos DB поддерживает индексирование и запросы геопространственных данных с помощью только hello CRS WGS 84.</span><span class="sxs-lookup"><span data-stu-id="8e155-151">Azure Cosmos DB supports indexing and querying of geospatial data using hello WGS-84 CRS only.</span></span> 

## <a name="creating-documents-with-spatial-data"></a><span data-ttu-id="8e155-152">Создание документов с пространственными данными</span><span class="sxs-lookup"><span data-stu-id="8e155-152">Creating documents with spatial data</span></span>
<span data-ttu-id="8e155-153">При создании документов, содержащих GeoJSON значения, они автоматически индексируются в пространственном индексе в политике индексирования toohello пикселями hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="8e155-153">When you create documents that contain GeoJSON values, they are automatically indexed with a spatial index in accordance toohello indexing policy of hello collection.</span></span> <span data-ttu-id="8e155-154">При работе с пакетом SDK Azure Cosmos DB в динамически типизированных языках программирования, таких как Python или Node.js, необходимо создавать действительные объекты GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="8e155-154">If you're working with an Azure Cosmos DB SDK in a dynamically typed language like Python or Node.js, you must create valid GeoJSON.</span></span>

<span data-ttu-id="8e155-155">**Создание документа с геопространственными данными в Node.js**</span><span class="sxs-lookup"><span data-stu-id="8e155-155">**Create Document with Geospatial data in Node.js**</span></span>

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

<span data-ttu-id="8e155-156">Можно использовать при работе с hello интерфейсы API DocumentDB hello `Point` и `Polygon` классов внутри hello `Microsoft.Azure.Documents.Spatial` сведения о расположении tooembed пространства имен в пределах объектов приложения.</span><span class="sxs-lookup"><span data-stu-id="8e155-156">If you're working with hello DocumentDB APIs, you can use hello `Point` and `Polygon` classes within hello `Microsoft.Azure.Documents.Spatial` namespace tooembed location information within your application objects.</span></span> <span data-ttu-id="8e155-157">Эти классы упростить hello сериализации и десериализации пространственных данных в GeoJSON.</span><span class="sxs-lookup"><span data-stu-id="8e155-157">These classes help simplify hello serialization and deserialization of spatial data into GeoJSON.</span></span>

<span data-ttu-id="8e155-158">**Создание документа с геопространственными данными в .NET**</span><span class="sxs-lookup"><span data-stu-id="8e155-158">**Create Document with Geospatial data in .NET**</span></span>

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

<span data-ttu-id="8e155-159">Если нет данных широты и долготы hello, но иметь hello физические адреса или имя расположения, например города или страны, фактический координаты hello производить поиск с помощью службы геокодирования, таких как службы Bing Maps REST.</span><span class="sxs-lookup"><span data-stu-id="8e155-159">If you don't have hello latitude and longitude information, but have hello physical addresses or location name like city or country, you can look up hello actual coordinates by using a geocoding service like Bing Maps REST Services.</span></span> <span data-ttu-id="8e155-160">Дополнительные сведения о геокодировании в Картах Bing можно найти [здесь](https://msdn.microsoft.com/library/ff701713.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e155-160">Learn more about Bing Maps geocoding [here](https://msdn.microsoft.com/library/ff701713.aspx).</span></span>

## <a name="querying-spatial-types"></a><span data-ttu-id="8e155-161">Типы запросов к пространственным данным</span><span class="sxs-lookup"><span data-stu-id="8e155-161">Querying spatial types</span></span>
<span data-ttu-id="8e155-162">Теперь, когда мы воспользовались обсуждается tooinsert геопространственные данные, давайте взглянем на как tooquery эти данные с помощью DB Cosmos Azure с помощью SQL и технологии LINQ.</span><span class="sxs-lookup"><span data-stu-id="8e155-162">Now that we've taken a look at how tooinsert geospatial data, let's take a look at how tooquery this data using Azure Cosmos DB using SQL and LINQ.</span></span>

### <a name="spatial-sql-built-in-functions"></a><span data-ttu-id="8e155-163">Встроенные функции для обработки пространственных данных в SQL</span><span class="sxs-lookup"><span data-stu-id="8e155-163">Spatial SQL built-in functions</span></span>
<span data-ttu-id="8e155-164">Azure Cosmos DB поддерживает следующие встроенные функции Open Geospatial Consortium (OGC) для выполнения запросов к геопространственных hello.</span><span class="sxs-lookup"><span data-stu-id="8e155-164">Azure Cosmos DB supports hello following Open Geospatial Consortium (OGC) built-in functions for geospatial querying.</span></span> <span data-ttu-id="8e155-165">Дополнительные сведения о hello полный набор встроенных функций в hello языка SQL можно найти слишком[запросов Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="8e155-165">For more details on hello complete set of built-in functions in hello SQL language, please refer too[Query Azure Cosmos DB](documentdb-sql-query.md).</span></span>

<table>
<tr>
  <td><span data-ttu-id="8e155-166"><strong>Использование</strong></span><span class="sxs-lookup"><span data-stu-id="8e155-166"><strong>Usage</strong></span></span></td>
  <td><span data-ttu-id="8e155-167"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="8e155-167"><strong>Description</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8e155-168">ST_DISTANCE (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="8e155-168">ST_DISTANCE (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="8e155-169">Возвращает hello расстояние между выражениями hello две точки GeoJSON Polygon и LineString.</span><span class="sxs-lookup"><span data-stu-id="8e155-169">Returns hello distance between hello two GeoJSON Point, Polygon, or LineString expressions.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8e155-170">ST_WITHIN (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="8e155-170">ST_WITHIN (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="8e155-171">Возвращает выражение типа Boolean, показывающего, является hello GeoJSON сперва (точка Polygon и LineString) в рамках hello второй GeoJSON объекта (точка Polygon и LineString).</span><span class="sxs-lookup"><span data-stu-id="8e155-171">Returns a Boolean expression indicating whether hello first GeoJSON object (Point, Polygon, or LineString) is within hello second GeoJSON object (Point, Polygon, or LineString).</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8e155-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span><span class="sxs-lookup"><span data-stu-id="8e155-172">ST_INTERSECTS (spatial_expr, spatial_expr)</span></span></td>
  <td><span data-ttu-id="8e155-173">Возвращает логическое выражение, указывающее, пересекается ли hello двух указанных GeoJSON объектов (точка Polygon и LineString).</span><span class="sxs-lookup"><span data-stu-id="8e155-173">Returns a Boolean expression indicating whether hello two specified GeoJSON objects (Point, Polygon, or LineString) intersect.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8e155-174">ST_ISVALID</span><span class="sxs-lookup"><span data-stu-id="8e155-174">ST_ISVALID</span></span></td>
  <td><span data-ttu-id="8e155-175">Возвращает логическое значение, указывающее, является ли hello точки GeoJSON Polygon и LineString выражение допустимо.</span><span class="sxs-lookup"><span data-stu-id="8e155-175">Returns a Boolean value indicating whether hello specified GeoJSON Point, Polygon, or LineString expression is valid.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="8e155-176">ST_ISVALIDDETAILED</span><span class="sxs-lookup"><span data-stu-id="8e155-176">ST_ISVALIDDETAILED</span></span></td>
  <td><span data-ttu-id="8e155-177">Возвращает значение JSON, содержащий логическое значение, указываемое hello точки GeoJSON Polygon и LineString выражение является допустимым и если недействительной, кроме того hello причина как строковое значение.</span><span class="sxs-lookup"><span data-stu-id="8e155-177">Returns a JSON value containing a Boolean value if hello specified GeoJSON Point, Polygon, or LineString expression is valid, and if invalid, additionally hello reason as a string value.</span></span></td>
</tr>
</table>

<span data-ttu-id="8e155-178">Пространственные функции могут быть запросами сходству используется tooperform пространственных данных.</span><span class="sxs-lookup"><span data-stu-id="8e155-178">Spatial functions can be used tooperform proximity queries against spatial data.</span></span> <span data-ttu-id="8e155-179">Например ниже приведен запрос, возвращающий все семейство документы, в течение 30 км hello указанное расположение используется встроенная функция ST_DISTANCE hello.</span><span class="sxs-lookup"><span data-stu-id="8e155-179">For example, here's a query that returns all family documents that are within 30 km of hello specified location using hello ST_DISTANCE built-in function.</span></span> 

<span data-ttu-id="8e155-180">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="8e155-180">**Query**</span></span>

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

<span data-ttu-id="8e155-181">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="8e155-181">**Results**</span></span>

    [{
      "id": "WakefieldFamily"
    }]

<span data-ttu-id="8e155-182">При включении пространственное индексирование в политику индексации, затем «расстояние запросы» будет обслуживаться эффективно hello индекса.</span><span class="sxs-lookup"><span data-stu-id="8e155-182">If you include spatial indexing in your indexing policy, then "distance queries" will be served efficiently through hello index.</span></span> <span data-ttu-id="8e155-183">Дополнительные сведения о пространственных индексирования см. в разделе ниже hello.</span><span class="sxs-lookup"><span data-stu-id="8e155-183">For more details on spatial indexing, please see hello section below.</span></span> <span data-ttu-id="8e155-184">Если у вас нет пространственного индекса для hello указано пути, по-прежнему выполнять Пространственные запросы, указав `x-ms-documentdb-query-enable-scan` заголовок запроса со значением hello установлен слишком «true».</span><span class="sxs-lookup"><span data-stu-id="8e155-184">If you don't have a spatial index for hello specified paths, you can still perform spatial queries by specifying `x-ms-documentdb-query-enable-scan` request header with hello value set too"true".</span></span> <span data-ttu-id="8e155-185">В .NET, это можно сделать путем передачи hello необязательно **FeedOptions** tooqueries аргумент с [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) задать tootrue.</span><span class="sxs-lookup"><span data-stu-id="8e155-185">In .NET, this can be done by passing hello optional **FeedOptions** argument tooqueries with [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) set tootrue.</span></span> 

<span data-ttu-id="8e155-186">ST_WITHIN может быть toocheck используется, если точка находится внутри многоугольника.</span><span class="sxs-lookup"><span data-stu-id="8e155-186">ST_WITHIN can be used toocheck if a point lies within a Polygon.</span></span> <span data-ttu-id="8e155-187">Часто многоугольников, используемые toorepresent границ, например почтовые индексы, состояние границы или естественным структур.</span><span class="sxs-lookup"><span data-stu-id="8e155-187">Commonly Polygons are used toorepresent boundaries like zip codes, state boundaries, or natural formations.</span></span> <span data-ttu-id="8e155-188">Еще раз при включении пространственное индексирование в политику индексации, затем запросов «в» будет обслуживаться эффективно hello индекса.</span><span class="sxs-lookup"><span data-stu-id="8e155-188">Again if you include spatial indexing in your indexing policy, then "within" queries will be served efficiently through hello index.</span></span> 

<span data-ttu-id="8e155-189">Аргументы многоугольника в ST_WITHIN может содержать только один кольцо, т. е. hello многоугольников не должен содержать уязвимости в них.</span><span class="sxs-lookup"><span data-stu-id="8e155-189">Polygon arguments in ST_WITHIN can contain only a single ring, i.e. hello Polygons must not contain holes in them.</span></span> 

<span data-ttu-id="8e155-190">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="8e155-190">**Query**</span></span>

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

<span data-ttu-id="8e155-191">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="8e155-191">**Results**</span></span>

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> <span data-ttu-id="8e155-192">Похожих несоответствие toohow работает в Azure Cosmos DB запроса, указываемое значение расположения hello в либо аргумент имеет неправильный формат или является недопустимым, то он будет оценен слишком**не определено** и пропуска toobe документа hello вычисляется из hello результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="8e155-192">Similar toohow mismatched types works in Azure Cosmos DB query, if hello location value specified in either argument is malformed or invalid, then it will evaluate too**undefined** and hello evaluated document toobe skipped from hello query results.</span></span> <span data-ttu-id="8e155-193">Если запрос не возвращает результатов, запустите toodebug ST_ISVALIDDETAILED, почему имеет недопустимый тип spatail hello.</span><span class="sxs-lookup"><span data-stu-id="8e155-193">If your query returns no results, run ST_ISVALIDDETAILED toodebug why hello spatail type is invalid.</span></span>     
> 
> 

<span data-ttu-id="8e155-194">Azure Cosmos DB также поддерживает выполнение обратный запросы, т. е. можно индексировать многоугольников и линий в базе данных Azure Cosmos, а затем запросить hello области, которые содержат указанную точку.</span><span class="sxs-lookup"><span data-stu-id="8e155-194">Azure Cosmos DB also supports performing inverse queries, i.e. you can index Polygons or lines in Azure Cosmos DB, then query for hello areas that contain a specified point.</span></span> <span data-ttu-id="8e155-195">Этот шаблон обычно используется в tooidentify материально-технического обеспечения например когда грузовик или выходе из указанной области.</span><span class="sxs-lookup"><span data-stu-id="8e155-195">This pattern is commonly used in logistics tooidentify e.g. when a truck enters or leaves a designated area.</span></span> 

<span data-ttu-id="8e155-196">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="8e155-196">**Query**</span></span>

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


<span data-ttu-id="8e155-197">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="8e155-197">**Results**</span></span>

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

<span data-ttu-id="8e155-198">ST_ISVALID и ST_ISVALIDDETAILED могут быть toocheck используется, если пространственный объект является допустимым.</span><span class="sxs-lookup"><span data-stu-id="8e155-198">ST_ISVALID and ST_ISVALIDDETAILED can be used toocheck if a spatial object is valid.</span></span> <span data-ttu-id="8e155-199">Например приветствия при следующем запросе проверяет допустимость hello точки с вне диапазона значений широты (-132.8).</span><span class="sxs-lookup"><span data-stu-id="8e155-199">For example, hello following query checks hello validity of a point with an out of range latitude value (-132.8).</span></span> <span data-ttu-id="8e155-200">ST_ISVALID возвращает логическое значение, и hello ST_ISVALIDDETAILED возвращает логическое значение и строка, содержащая hello причины, почему он считается недопустимым.</span><span class="sxs-lookup"><span data-stu-id="8e155-200">ST_ISVALID returns just a Boolean value, and ST_ISVALIDDETAILED returns hello Boolean and a string containing hello reason why it is considered invalid.</span></span>

<span data-ttu-id="8e155-201">** Запрос **</span><span class="sxs-lookup"><span data-stu-id="8e155-201">** Query **</span></span>

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

<span data-ttu-id="8e155-202">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="8e155-202">**Results**</span></span>

    [{
      "$1": false
    }]

<span data-ttu-id="8e155-203">Эти функции также могут быть многоугольниками используется toovalidate.</span><span class="sxs-lookup"><span data-stu-id="8e155-203">These functions can also be used toovalidate Polygons.</span></span> <span data-ttu-id="8e155-204">Например здесь мы используем ST_ISVALIDDETAILED toovalidate многоугольник, который не закрывается.</span><span class="sxs-lookup"><span data-stu-id="8e155-204">For example, here we use ST_ISVALIDDETAILED toovalidate a Polygon that is not closed.</span></span> 

<span data-ttu-id="8e155-205">**Запрос**</span><span class="sxs-lookup"><span data-stu-id="8e155-205">**Query**</span></span>

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

<span data-ttu-id="8e155-206">**Результаты**</span><span class="sxs-lookup"><span data-stu-id="8e155-206">**Results**</span></span>

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a><span data-ttu-id="8e155-207">В .NET SDK hello запросов LINQ</span><span class="sxs-lookup"><span data-stu-id="8e155-207">LINQ Querying in hello .NET SDK</span></span>
<span data-ttu-id="8e155-208">Hello DocumentDB .NET SDK также поставщики заглушки методов `Distance()` и `Within()` для использования в выражениях LINQ.</span><span class="sxs-lookup"><span data-stu-id="8e155-208">hello DocumentDB .NET SDK also providers stub methods `Distance()` and `Within()` for use within LINQ expressions.</span></span> <span data-ttu-id="8e155-209">Hello DocumentDB LINQ поставщик преобразует эти вызовы toohello эквивалент SQL встроенной функции вызовы методов (ST_DISTANCE и ST_WITHIN соответственно).</span><span class="sxs-lookup"><span data-stu-id="8e155-209">hello DocumentDB LINQ provider translates these method calls toohello equivalent SQL built-in function calls (ST_DISTANCE and ST_WITHIN respectively).</span></span> 

<span data-ttu-id="8e155-210">Вот пример запроса LINQ, который находит все документы в коллекции Azure Cosmos DB hello, «местоположение», значение которого в пределах радиуса 30 км hello указывается точки с использованием LINQ.</span><span class="sxs-lookup"><span data-stu-id="8e155-210">Here's an example of a LINQ query that finds all documents in hello Azure Cosmos DB collection whose "location" value is within a radius of 30km of hello specified point using LINQ.</span></span>

<span data-ttu-id="8e155-211">**Запросы LINQ для определения расстояния**</span><span class="sxs-lookup"><span data-stu-id="8e155-211">**LINQ query for Distance**</span></span>

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

<span data-ttu-id="8e155-212">Аналогичным образом ниже приведен запрос для поиска всех документов hello, «местоположение» находится в пределах hello указанное поле или многоугольник.</span><span class="sxs-lookup"><span data-stu-id="8e155-212">Similarly, here's a query for finding all hello documents whose "location" is within hello specified box/Polygon.</span></span> 

<span data-ttu-id="8e155-213">**Запросы LINQ для определения принадлежности**</span><span class="sxs-lookup"><span data-stu-id="8e155-213">**LINQ query for Within**</span></span>

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


<span data-ttu-id="8e155-214">Теперь, когда мы воспользовались обсуждается tooquery документы с помощью LINQ и SQL, давайте взглянем на как tooconfigure Azure Cosmos DB для пространственного индексирования.</span><span class="sxs-lookup"><span data-stu-id="8e155-214">Now that we've taken a look at how tooquery documents using LINQ and SQL, let's take a look at how tooconfigure Azure Cosmos DB for spatial indexing.</span></span>

## <a name="indexing"></a><span data-ttu-id="8e155-215">Индексация</span><span class="sxs-lookup"><span data-stu-id="8e155-215">Indexing</span></span>
<span data-ttu-id="8e155-216">Как было описано в hello [схемы независимой от индексирования с помощью Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) бумаги, мы разработали toobe ядра базы данных Azure Cosmos DB действительно зависит от схемы и обеспечивают превосходную поддержку JSON.</span><span class="sxs-lookup"><span data-stu-id="8e155-216">As we described in hello [Schema Agnostic Indexing with Azure Cosmos DB](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) paper, we designed Azure Cosmos DB’s database engine toobe truly schema agnostic and provide first class support for JSON.</span></span> <span data-ttu-id="8e155-217">Hello записи оптимизированной СУБД Azure Cosmos DB собственными средствами различает Пространственные данные (указывает, многоугольников и линий), представлен в стандартном GeoJSON hello.</span><span class="sxs-lookup"><span data-stu-id="8e155-217">hello write optimized database engine of Azure Cosmos DB natively understands spatial data (points, Polygons and lines) represented in hello GeoJSON standard.</span></span>

<span data-ttu-id="8e155-218">По сути, hello geometry спроецировано из геодезические координаты на двумерной плоскости затем постепенно разделить ячеек с помощью **quadtree**.</span><span class="sxs-lookup"><span data-stu-id="8e155-218">In a nutshell, hello geometry is projected from geodetic coordinates onto a 2D plane then divided progressively into cells using a **quadtree**.</span></span> <span data-ttu-id="8e155-219">Эти ячейки являются сопоставленных too1D на основе расположения hello hello ячейки **пространства кривой Гильберта**, сохраняющее локальность точек.</span><span class="sxs-lookup"><span data-stu-id="8e155-219">These cells are mapped too1D based on hello location of hello cell within a **Hilbert space filling curve**, which preserves locality of points.</span></span> <span data-ttu-id="8e155-220">Кроме того при индексировании данных расположения, он проходит через этот процесс называется **тесселяции**, т. е. все ячейки hello, пересекающих расположение идентифицируются и находящиеся в качестве ключей в индексе hello Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8e155-220">Additionally when location data is indexed, it goes through a process known as **tessellation**, i.e. all hello cells that intersect a location are identified and stored as keys in hello Azure Cosmos DB index.</span></span> <span data-ttu-id="8e155-221">Во время обработки запроса аргументы, такие как точки и многоугольники, также тесселированных tooextract hello диапазоны Идентификаторов соответствующую ячейку, а затем использовать tooretrieve данным из индекса hello.</span><span class="sxs-lookup"><span data-stu-id="8e155-221">At query time, arguments like points and Polygons are also tessellated tooextract hello relevant cell ID ranges, then used tooretrieve data from hello index.</span></span>

<span data-ttu-id="8e155-222">При указании индексирования политики, которая включает пространственного индекса для / * (все пути), а затем все точки, найденных в коллекции hello индексируются для обеспечения эффективного поиска пространственных (ST_WITHIN и ST_DISTANCE).</span><span class="sxs-lookup"><span data-stu-id="8e155-222">If you specify an indexing policy that includes spatial index for /* (all paths), then all points found within hello collection are indexed for efficient spatial queries (ST_WITHIN and ST_DISTANCE).</span></span> <span data-ttu-id="8e155-223">Пространственные индексы не имеют значения точности и всегда используют значение точности по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="8e155-223">Spatial indexes do not have a precision value, and always use a default precision value.</span></span>

> [!NOTE]
> <span data-ttu-id="8e155-224">Azure Cosmos DB поддерживает автоматическое индексирование данных типа Point, Polygon и LineString.</span><span class="sxs-lookup"><span data-stu-id="8e155-224">Azure Cosmos DB supports automatic indexing of Points, Polygons, and LineStrings</span></span>
> 
> 

<span data-ttu-id="8e155-225">Hello следующем фрагменте JSON показан политику индексации с пространственное индексирование включено, т. е. индекс любой точке GeoJSON, найденных в документах для пространственных запросов.</span><span class="sxs-lookup"><span data-stu-id="8e155-225">hello following JSON snippet shows an indexing policy with spatial indexing enabled, i.e. index any GeoJSON point found within documents for spatial querying.</span></span> <span data-ttu-id="8e155-226">При добавлении или изменении с помощью портала Azure hello политика индексирования hello, можно указать hello, следуя JSON для индексирования tooenable политики пространственного индексирования в коллекции.</span><span class="sxs-lookup"><span data-stu-id="8e155-226">If you are modifying hello indexing policy using hello Azure Portal, you can specify hello following JSON for indexing policy tooenable spatial indexing on your collection.</span></span>

<span data-ttu-id="8e155-227">**JSON политики пространственного индексирования коллекций для точек и многоугольников**</span><span class="sxs-lookup"><span data-stu-id="8e155-227">**Collection Indexing Policy JSON with Spatial enabled for points and Polygons**</span></span>

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

<span data-ttu-id="8e155-228">Ниже приведен фрагмент кода в .NET, который показывает, как toocreate пространственное индексирование коллекции установлен в on для всех путей, содержащий точки.</span><span class="sxs-lookup"><span data-stu-id="8e155-228">Here's a code snippet in .NET that shows how toocreate a collection with spatial indexing turned on for all paths containing points.</span></span> 

<span data-ttu-id="8e155-229">**Создание коллекции с пространственным индексированием**</span><span class="sxs-lookup"><span data-stu-id="8e155-229">**Create a collection with spatial indexing**</span></span>

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

<span data-ttu-id="8e155-230">И вот как можно изменять существующие коллекции tootake преимущество пространственное индексирование через все точки, которые хранятся в документах.</span><span class="sxs-lookup"><span data-stu-id="8e155-230">And here's how you can modify an existing collection tootake advantage of spatial indexing over any points that are stored within documents.</span></span>

<span data-ttu-id="8e155-231">**Изменение коллекции с пространственным индексированием**</span><span class="sxs-lookup"><span data-stu-id="8e155-231">**Modify an existing collection with spatial indexing**</span></span>

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> <span data-ttu-id="8e155-232">Если расположение hello GeoJSON значение в документе hello имеет неправильный формат или является недопустимым, затем его не получить индексироваться для пространственных запросов.</span><span class="sxs-lookup"><span data-stu-id="8e155-232">If hello location GeoJSON value within hello document is malformed or invalid, then it will not get indexed for spatial querying.</span></span> <span data-ttu-id="8e155-233">Проверить значение расположения можно с помощью ST_ISVALID и ST_ISVALIDDETAILED.</span><span class="sxs-lookup"><span data-stu-id="8e155-233">You can validate location values using ST_ISVALID and ST_ISVALIDDETAILED.</span></span>
> 
> <span data-ttu-id="8e155-234">Если определение коллекции включает ключ секции, информация о ходе выполнения преобразования индекса не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="8e155-234">If your collection definition includes a partition key, indexing transformation progress is not reported.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8e155-235">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8e155-235">Next steps</span></span>
<span data-ttu-id="8e155-236">Теперь, когда вы узнали о том, как tooget работы с поддержку геопространственных в базе данных Azure Cosmos, вы можете:</span><span class="sxs-lookup"><span data-stu-id="8e155-236">Now that you've learnt about how tooget started with geospatial support in Azure Cosmos DB, you can:</span></span>

* <span data-ttu-id="8e155-237">Начать создание кода с hello [образцы кода геопространственных .NET на GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span><span class="sxs-lookup"><span data-stu-id="8e155-237">Start coding with hello [Geospatial .NET code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)</span></span>
* <span data-ttu-id="8e155-238">Получить руки на с геопространственных запросов для hello [площадку запросов DB Cosmos Azure](http://www.documentdb.com/sql/demo#geospatial)</span><span class="sxs-lookup"><span data-stu-id="8e155-238">Get hands on with geospatial querying at hello [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)</span></span>
* <span data-ttu-id="8e155-239">Дополнительные сведения о запросах Azure Cosmos DB см. [здесь](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="8e155-239">Learn more about [Azure Cosmos DB Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="8e155-240">Дополнительные сведения о политиках индексации в Azure Cosmos DB см. в [этой статье](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8e155-240">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>

