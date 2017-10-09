---
title: "AAA «создание индекса (API .NET - поиска Azure) | Документы Microsoft»"
description: "Создайте индекс в коде, используя пакет SDK Azure Search .NET hello."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 3a851647-fc7b-4fb6-8506-6aaa519e77cd
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 7fa4030b8c3565bc02b1d6bb4426331657cf3a5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-net-sdk"></a>Создание индекса поиска Azure с помощью hello .NET SDK
> [!div class="op_single_selector"]
> * [Обзор](search-what-is-an-index.md)
> * [Портал](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

В этой статье приведена пошаговая процедура hello процесс создания поиска Azure [индекс](https://docs.microsoft.com/rest/api/searchservice/Create-Index) с помощью hello [пакет SDK Azure Search .NET](https://aka.ms/search-sdk).

Перед выполнением инструкций, приведенных в этом руководстве, и созданием индекса следует [создать службу поиска Azure](search-create-service-portal.md).

> [!NOTE]
> Все приведенные здесь примеры кода написаны на языке C#. Можно найти полный исходный код hello [на GitHub](http://aka.ms/search-dotnet-howto). Вы также можете прочесть об hello [пакет SDK Azure Search .NET](search-howto-dotnet-sdk.md) для более подробные руководства по hello примеров кода.


## <a name="identify-your-azure-search-services-admin-api-key"></a>Определение ключа API администратора службы поиска Azure
Теперь, подготовки службы поиска Azure все почти готово tooissue запросы с конечной точкой службы, с помощью hello .NET SDK. Во-первых необходимо будет tooobtain один hello admin api-ключей, созданных для подготовленной службы поиска hello. Hello .NET SDK будет отправлять этот ключ api для каждой службы tooyour запроса. Наличие действительного ключа позволяет установить отношения доверия, для каждого запроса, между Отправка запроса hello hello приложения и службы hello, обрабатывает его.

1. toofind ключи api службы, войдите в toohello [портал Azure](https://portal.azure.com/)
2. Перейдите в колонку службы поиска Azure tooyour
3. Щелкните значок «Ключи» hello

Ваша служба получит *ключи администратора* и *ключи запросов*.

* Первичная и Вторичная *ключей администратора* предоставить полные права tooall операций, включая toomanage hello hello возможности службы, создания и удаления индексов, индексаторов и источников данных. Существует два ключа, чтобы продолжить toouse hello вторичный ключ в случае tooregenerate hello первичного ключа и наоборот.
* Ваш *запрос ключей* предоставить доступ только для чтения tooindexes и документы и представляют собой tooclient обычно распределенного приложения, издающие запросы поиска.

Создание индекса целях hello, можно использовать ключ администратора первичной или вторичной.

<a name="CreateSearchServiceClient"></a>

## <a name="create-an-instance-of-hello-searchserviceclient-class"></a>Создайте экземпляр класса SearchServiceClient hello
с помощью toostart hello пакет SDK Azure Search .NET, вам понадобится toocreate экземпляр hello `SearchServiceClient` класса. Этот класс имеет несколько конструкторов. Hello один требуется принимает имя службы поиска и `SearchCredentials` объект в качестве параметров. `SearchCredentials` содержит ключ API.

Приведенный ниже код Hello создает новый `SearchServiceClient` с использованием значений для hello имя службы поиска и ключ api, которые хранятся в файле конфигурации приложения hello (`appsettings.json` в случае, когда hello hello [образец приложения](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

`SearchServiceClient` имеет свойство `Indexes`. Это свойство предоставляет все методы hello необходимости toocreate, список, обновления или удаления индексов поиска Azure.

> [!NOTE]
> Hello `SearchServiceClient` класс управляет служба поиска tooyour подключений. В порядке tooavoid открытия слишком много подключений, попробуйте tooshare один экземпляр `SearchServiceClient` в приложении, если это возможно. Его методы являются поточно ориентированного tooenable такого управления доступом.
> 
> 

<a name="DefineIndex"></a>

## <a name="define-your-azure-search-index"></a>Определение индекса службы поиска Azure
Toohello один вызов `Indexes.Create` метод будет создан индекс. В качестве параметра этот метод принимает объект `Index` , определяющий индекс службы поиска Azure. Требуется toocreate `Index` и инициализируйте его, как показано ниже:

1. Набор hello `Name` свойство hello `Index` toohello имя объекта индекса.
2. Набор hello `Fields` свойство hello `Index` tooan объекта из массива `Field` объектов. Hello простым способом toocreate hello `Field` объектов выполняется путем вызова hello `FieldBuilder.BuildForType` метод, передавая класс модели для параметра типа hello. Класс модели имеет свойства, которые соответствуют toohello полей индекса. Это позволяет toobind документов из вашей tooinstances индекса поиска класса модели.

> [!NOTE]
> Если вы не собираетесь toouse класс модели, можно определять индекса, создав `Field` объекты непосредственно. Можно указать имя hello конструктора toohello поле hello вместе с типом данных hello (или анализатор для строковых полей). Можно также задать другие свойства, например `IsSearchable`, `IsFilterable` и т. д.
>
>

Очень важно, следует найти качества и бизнес-потребностей организации помнить при проектировании индекса, как каждое поле необходимо назначить hello [соответствующие свойства](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Эти свойства выбирать поиск функций (фильтрация, аспекта, сортировка полнотекстового поиска, т. д.) применяются toowhich поля. Любое свойство не задано явно, hello `Field` класса по умолчанию устанавливается toodisabling hello соответствующей функции поиска, если явно задействовать его.

В нашем примере мы присвоили индексу имя hotels и определили поля с помощью класса модели. Каждое свойство класса модели hello имеет атрибуты, которые определяют hello поведения, связанные с поиска соответствующего поля индекса hello. класс модели Hello определяется следующим образом:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

Мы выбрали тщательно hello атрибуты для каждого свойства, в зависимости от того, как мы думаем, что они будут использоваться в приложении. Например, вполне вероятно, что поиск гостиницы пользователей может заинтересовать ключевым словам, совпадениям hello `description` поле, поэтому мы включить полнотекстовый поиск для этого поля, добавив hello `IsSearchable` атрибута toohello `Description` свойство.

Обратите внимание, только одно поле в индексе типа `string` быть hello назначенным hello *ключ* поле путем добавления hello `Key` атрибута (см. `HotelId` в hello в приведенном выше примере).

Определение индекса Hello выше использует анализатора языка для hello `description_fr` поле, так как он является предполагаемым toostore текстом на французском языке. В разделе [hello языковой поддержки раздела](https://docs.microsoft.com/rest/api/searchservice/Language-support) а также соответствующий hello [блога](https://azure.microsoft.com/blog/language-support-in-azure-search/) Дополнительные сведения о языковых анализаторов.

> [!NOTE]
> По умолчанию hello имя каждого свойства в классе модели используется как имя hello hello соответствующего поля в индексе hello. Если вы хотите toomap имена toocamel регистр имен всех свойств, пометить класс hello с hello `SerializePropertyNamesAsCamelCase` атрибута. Если требуется другое имя tooa toomap, можно использовать hello `JsonProperty` атрибут как hello `DescriptionFr` свойство выше. Hello `JsonProperty` атрибут имеет приоритет над hello `SerializePropertyNamesAsCamelCase` атрибута.
> 
> 

Теперь, когда мы определили класс модели, можно легко создать определение индекса.

```csharp
var definition = new Index()
{
    Name = "hotels",
    Fields = FieldBuilder.BuildForType<Hotel>()
};
```

## <a name="create-hello-index"></a>Создание индекса hello
Теперь, когда имеется инициализированная `Index` объекта, можно создать индекс hello просто вызвав `Indexes.Create` на ваш `SearchServiceClient` объекта:

```csharp
serviceClient.Indexes.Create(definition);
```

Успешный запрос hello метод будет возвращать обычным образом. Если имеется проблема с запросом hello, таких как недопустимый параметр, будет вызывать метод hello `CloudException`.

После завершения операции с индексом и хотите toodelete он просто вызвать hello `Indexes.Delete` метод вашей `SearchServiceClient`. Например это, как мы удалить индекс «гостиницы» hello:

```csharp
serviceClient.Indexes.Delete("hotels");
```

> [!NOTE]
> пример кода Hello в этой статье использует синхронные методы hello hello пакет SDK Azure Search .NET для простоты. Рекомендуется использовать асинхронные методы hello в собственных приложениях tookeep их быстрые и масштабируемые. Например, в hello примерах выше можно использовать `CreateAsync` и `DeleteAsync` вместо `Create` и `Delete`.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
После создания индекс поиска Azure, вы будете готовы слишком[отправки содержимого в индекс hello](search-what-is-data-import.md) чтобы вы могли начать поиск данных.

