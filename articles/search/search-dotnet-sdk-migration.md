---
title: "aaaUpgrading toohello поиска Azure .NET SDK версии 1.1 | Документы Microsoft"
description: "Обновление toohello поиска Azure .NET SDK версии 1.1"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="d3a60-103">Обновление toohello поиска Azure .NET SDK версии 3</span><span class="sxs-lookup"><span data-stu-id="d3a60-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="d3a60-104">Если вы используете версию предварительной версии 2.0 или более hello [пакет SDK Azure Search .NET](https://aka.ms/search-sdk), эта статья поможет вам обновить версию приложения toouse 3.</span><span class="sxs-lookup"><span data-stu-id="d3a60-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="d3a60-105">Более общие Пошаговое руководство по hello SDK включая примеры, см. в [как toouse Azure поиска из приложения .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d3a60-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="d3a60-106">Пакет SDK Azure Search .NET hello версии 3 содержит некоторые изменения из более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="d3a60-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="d3a60-107">Эти отличия в основном незначительные, поэтому изменение кода потребует минимальных усилий.</span><span class="sxs-lookup"><span data-stu-id="d3a60-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="d3a60-108">В разделе [tooupgrade действия](#UpgradeSteps) инструкции toochange новой версии пакета SDK кода toouse hello.</span><span class="sxs-lookup"><span data-stu-id="d3a60-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="d3a60-109">Если вы используете версию 1.0.2-preview или более ранней версии, необходимо сначала обновить tooversion 1.1, а затем обновите tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="d3a60-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="d3a60-110">В разделе [приложение: tooversion tooupgrade действия 1.1](#UpgradeStepsV1) инструкции.</span><span class="sxs-lookup"><span data-stu-id="d3a60-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="d3a60-111">Экземпляр службы поиска Azure поддерживает несколько версий API-Интерфейс REST, включая hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="d3a60-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="d3a60-112">Вы можете продолжить toouse версии, когда он больше не hello последнюю версию, но рекомендуется перейти к toouse кода hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="d3a60-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="d3a60-113">При использовании hello REST API, необходимо указать версию API hello в каждом запросе через параметр api-version hello.</span><span class="sxs-lookup"><span data-stu-id="d3a60-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="d3a60-114">При использовании hello .NET SDK, версия hello hello SDK вы используете определяет соответствующую версию hello hello REST API.</span><span class="sxs-lookup"><span data-stu-id="d3a60-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="d3a60-115">При использовании старых SDK можно продолжить toorun без изменения кода, даже если служба hello версии обновленных toosupport новых API.</span><span class="sxs-lookup"><span data-stu-id="d3a60-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="d3a60-116">Новые возможности в версии 3</span><span class="sxs-lookup"><span data-stu-id="d3a60-116">What's new in version 3</span></span>
<span data-ttu-id="d3a60-117">Версии 3 hello целевых объектов пакет SDK Azure Search .NET hello последней общедоступной версии hello REST API поиска Azure, в частности 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="d3a60-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="d3a60-118">В результате возможно toouse множество новых функций поиска Azure из приложения .NET, включая hello следующее:</span><span class="sxs-lookup"><span data-stu-id="d3a60-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="d3a60-119">Пользовательские анализаторы</span><span class="sxs-lookup"><span data-stu-id="d3a60-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="d3a60-120">поддержка индексатора [хранилища BLOB-объектов Azure](search-howto-indexing-azure-blob-storage.md) и [хранилища таблиц Azure](search-howto-indexing-azure-tables.md);</span><span class="sxs-lookup"><span data-stu-id="d3a60-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="d3a60-121">настройка индексатора посредством [сопоставления полей](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="d3a60-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="d3a60-122">Теги eTag поддерживает tooenable безопасном параллельных обновление индекса определений, индексаторов и источников данных</span><span class="sxs-lookup"><span data-stu-id="d3a60-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="d3a60-123">Поддержка создания определения полей индекса декларативно декорирования классе модели и используя hello новый `FieldBuilder` класса.</span><span class="sxs-lookup"><span data-stu-id="d3a60-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="d3a60-124">поддержка .NET Core и .NET Portable Profile 111.</span><span class="sxs-lookup"><span data-stu-id="d3a60-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="d3a60-125">Tooupgrade действия</span><span class="sxs-lookup"><span data-stu-id="d3a60-125">Steps tooupgrade</span></span>
<span data-ttu-id="d3a60-126">Во-первых, обновите NuGet справочной информации для `Microsoft.Azure.Search` либо hello консоль диспетчера пакетов NuGet с помощью или путем щелкнув ссылки проекта и выбрав «Управление... пакеты NuGet» в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3a60-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="d3a60-127">После загрузки NuGet hello новые пакеты и их зависимости, перестройте проект.</span><span class="sxs-lookup"><span data-stu-id="d3a60-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="d3a60-128">Сборка может быть выполнена успешно — в зависимости от того, как структурирован ваш код.</span><span class="sxs-lookup"><span data-stu-id="d3a60-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="d3a60-129">В этом случае вы будете готовы toogo!</span><span class="sxs-lookup"><span data-stu-id="d3a60-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="d3a60-130">Если сборку не удается, появится ошибка сборки hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="d3a60-131">Hello следующим шагом является toofix ошибки построения.</span><span class="sxs-lookup"><span data-stu-id="d3a60-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="d3a60-132">В разделе [критические изменения в версии 3](#ListOfChanges) сведения о том, что вызывает ошибку hello и как toofix его.</span><span class="sxs-lookup"><span data-stu-id="d3a60-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="d3a60-133">Вы можете увидеть дополнительные сборки tooobsolete методов и свойств, связанных с предупреждениями.</span><span class="sxs-lookup"><span data-stu-id="d3a60-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="d3a60-134">Hello предупреждения будут включены инструкции по какой toouse вместо из hello нерекомендуемая функция.</span><span class="sxs-lookup"><span data-stu-id="d3a60-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="d3a60-135">Например, если приложение использует hello `IndexingParameters.Base64EncodeKeys` следует получать предупреждение об ошибке`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="d3a60-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="d3a60-136">После устранения ошибки сборки можно внести изменения tooyour приложения tootake преимуществами новых функций, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d3a60-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="d3a60-137">Новые возможности в hello SDK подробно описаны в [новые возможности в версии 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="d3a60-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="d3a60-138">Критические изменения в версии 3</span><span class="sxs-lookup"><span data-stu-id="d3a60-138">Breaking changes in version 3</span></span>
<span data-ttu-id="d3a60-139">Существует небольшое количество критические изменения в версии 3, которые могут потребовать код изменяет Кроме toorebuilding приложения.</span><span class="sxs-lookup"><span data-stu-id="d3a60-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="d3a60-140">Тип возвращаемого значения Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="d3a60-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="d3a60-141">Hello `Indexes.GetClient` метод имеет новый тип возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="d3a60-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="d3a60-142">Раньше он возвращал `SearchIndexClient`, но он был изменен слишком`ISearchIndexClient` в предварительной версии версии 2.0, которые передает изменения по tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="d3a60-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="d3a60-143">Это toosupport клиентов, которые хотите toomock hello `GetClient` метод для модульных тестов, возвращая макетной реализации `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="d3a60-144">Пример</span><span class="sxs-lookup"><span data-stu-id="d3a60-144">Example</span></span>
<span data-ttu-id="d3a60-145">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="d3a60-146">Его можно изменить toothis toofix все ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="d3a60-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="d3a60-147">AnalyzerName, тип данных и другие больше не могут быть неявно преобразованы toostrings</span><span class="sxs-lookup"><span data-stu-id="d3a60-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="d3a60-148">Существует много типов в пакет SDK Azure Search .NET являются производными от hello `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="d3a60-149">Ранее эти типы были все неявно преобразовываться tootype `string`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="d3a60-150">Тем не менее, ошибка была обнаружена на hello `Object.Equals` реализации этих классов и исправление hello ошибки требуется отключить это неявное преобразование.</span><span class="sxs-lookup"><span data-stu-id="d3a60-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="d3a60-151">Явное преобразование слишком`string` по-прежнему разрешено.</span><span class="sxs-lookup"><span data-stu-id="d3a60-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="d3a60-152">Пример</span><span class="sxs-lookup"><span data-stu-id="d3a60-152">Example</span></span>
<span data-ttu-id="d3a60-153">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-153">If your code looks like this:</span></span>

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

<span data-ttu-id="d3a60-154">Его можно изменить toothis toofix все ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="d3a60-154">You can change it toothis toofix any build errors:</span></span>

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a><span data-ttu-id="d3a60-155">Удалены устаревшие члены</span><span class="sxs-lookup"><span data-stu-id="d3a60-155">Removed obsolete members</span></span>

<span data-ttu-id="d3a60-156">Можно просматривать связанные toomethods ошибки сборки или свойства, которые были помечены как устаревшие в предварительной версии версии 2.0, а затем удаляется в версии 3.</span><span class="sxs-lookup"><span data-stu-id="d3a60-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="d3a60-157">При возникновении таких ошибок, вот как tooresolve их:</span><span class="sxs-lookup"><span data-stu-id="d3a60-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="d3a60-158">Если вы использовали конструктор `ScoringParameter(string name, string value)`, то вместо него воспользуйтесь этим: `ScoringParameter(string name, IEnumerable<string> values)`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="d3a60-159">Если вы использовали hello `ScoringParameter.Value` свойство, используйте hello `ScoringParameter.Values` свойства или hello `ToString` метод вместо.</span><span class="sxs-lookup"><span data-stu-id="d3a60-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="d3a60-160">Если вы использовали hello `SearchRequestOptions.RequestId` свойство, используйте hello `ClientRequestId` свойство вместо него.</span><span class="sxs-lookup"><span data-stu-id="d3a60-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="d3a60-161">Удалены функции предварительной версии</span><span class="sxs-lookup"><span data-stu-id="d3a60-161">Removed preview features</span></span>

<span data-ttu-id="d3a60-162">При обновлении от tooversion предварительной версии 2.0 версии 3, имейте в виду, что JSON и CSV при синтаксическом анализе поддержки для индексаторов большой двоичный объект был удален, так как эти возможности все еще находятся в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="d3a60-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="d3a60-163">Здравствуйте, в частности, следующие методы hello `IndexingParametersExtensions` класса будут удалены:</span><span class="sxs-lookup"><span data-stu-id="d3a60-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="d3a60-164">Если приложение имеет жесткие зависимости от этих функций, нельзя будет tooupgrade tooversion 3 из hello пакет SDK Azure Search .NET.</span><span class="sxs-lookup"><span data-stu-id="d3a60-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="d3a60-165">Вы можете продолжить toouse версии 2.0-preview.</span><span class="sxs-lookup"><span data-stu-id="d3a60-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="d3a60-166">Однако необходимо учитывать, что **использовать предварительные версии пакетов SDK в рабочих приложениях не рекомендуется**.</span><span class="sxs-lookup"><span data-stu-id="d3a60-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="d3a60-167">Предварительные версии функций предназначены исключительно для оценки и могут изменяться.</span><span class="sxs-lookup"><span data-stu-id="d3a60-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d3a60-168">Заключение</span><span class="sxs-lookup"><span data-stu-id="d3a60-168">Conclusion</span></span>
<span data-ttu-id="d3a60-169">Если требуются дополнительные сведения об использовании hello пакет SDK Azure Search .NET, см. раздел последние обновленные [руководства, посвященные](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d3a60-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="d3a60-170">Мы будем рады вашим отзывам на hello SDK.</span><span class="sxs-lookup"><span data-stu-id="d3a60-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="d3a60-171">Если возникли проблемы, вы бесплатно tooask нам для получения справки по hello [форум MSDN поиска Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="d3a60-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="d3a60-172">При обнаружении ошибки можно зарегистрировать ошибку в hello [репозитории Azure .NET SDK GitHub](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="d3a60-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="d3a60-173">Убедитесь, что tooprefix название вашей проблемы с «пакет SDK для поиска: «.</span><span class="sxs-lookup"><span data-stu-id="d3a60-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="d3a60-174">Благодарим вас за использование поиска Azure!</span><span class="sxs-lookup"><span data-stu-id="d3a60-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="d3a60-175">Приложение: Действия tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="d3a60-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="d3a60-176">Этот раздел применим только toousers из версии 1.0.2-preview hello пакет SDK Azure Search .NET и более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="d3a60-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="d3a60-177">Во-первых, обновите NuGet справочной информации для `Microsoft.Azure.Search` либо hello консоль диспетчера пакетов NuGet с помощью или путем щелкнув ссылки проекта и выбрав «Управление... пакеты NuGet» в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3a60-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="d3a60-178">После загрузки NuGet hello новые пакеты и их зависимости, перестройте проект.</span><span class="sxs-lookup"><span data-stu-id="d3a60-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="d3a60-179">Если ранее с помощью построения hello версии 1.0.0-preview, 1.0.1-preview или 1.0.2-preview, должны выполняться успешно, и вы будете готовы toogo!</span><span class="sxs-lookup"><span data-stu-id="d3a60-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="d3a60-180">Если вы ранее использовали версии 0.13.0-preview или более ранней версии, вы увидите построения ошибки hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="d3a60-181">Hello следующий шаг — ошибки сборки hello toofix по одному.</span><span class="sxs-lookup"><span data-stu-id="d3a60-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="d3a60-182">Большинство требует изменения некоторых имен классов и методов, которые были переименованы в hello SDK.</span><span class="sxs-lookup"><span data-stu-id="d3a60-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="d3a60-183">[Список критических изменений в версии 1.1](#ListOfChangesV1) содержит список этих изменений имен.</span><span class="sxs-lookup"><span data-stu-id="d3a60-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="d3a60-184">Если вы используете toomodel пользовательские классы документов и эти классы имеют свойства, не допускающим простых типов (например, `int` или `bool` в C#), отсутствует исправления ошибки в версии hello 1.1 hello пакета SDK, из которых следует иметь в виду.</span><span class="sxs-lookup"><span data-stu-id="d3a60-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="d3a60-185">Дополнительные сведения см. в разделе [Исправления в версии 1.1](#BugFixesV1).</span><span class="sxs-lookup"><span data-stu-id="d3a60-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="d3a60-186">Наконец после устранения ошибки сборки можно внести изменения tooyour приложения tootake преимуществами новых функциональных возможностей при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d3a60-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="d3a60-187">Список критических изменений в версии 1.1</span><span class="sxs-lookup"><span data-stu-id="d3a60-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="d3a60-188">Hello следующий список упорядочен по вероятности hello, изменение hello может повлиять на код приложения.</span><span class="sxs-lookup"><span data-stu-id="d3a60-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="d3a60-189">Изменения IndexBatch и IndexAction</span><span class="sxs-lookup"><span data-stu-id="d3a60-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="d3a60-190">`IndexBatch.Create`был переименован слишком`IndexBatch.New` и больше не имеет `params` аргумент.</span><span class="sxs-lookup"><span data-stu-id="d3a60-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="d3a60-191">Можно использовать `IndexBatch.New` для пакетов, сочетающих в себе различные типы действий (слияние, удаление и т. д.).</span><span class="sxs-lookup"><span data-stu-id="d3a60-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="d3a60-192">Кроме того, существуют новые статические методы для создания пакетов где все действия hello являются одинаковыми hello: `Delete`, `Merge`, `MergeOrUpload`, и `Upload`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="d3a60-193">`IndexAction` больше не имеет открытых конструкторов, и его свойства теперь являются неизменяемыми.</span><span class="sxs-lookup"><span data-stu-id="d3a60-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="d3a60-194">Следует использовать hello новые статические методы для создания действий для разных целей: `Delete`, `Merge`, `MergeOrUpload`, и `Upload`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="d3a60-195">`IndexAction.Create` был удален.</span><span class="sxs-lookup"><span data-stu-id="d3a60-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="d3a60-196">При использовании hello перегрузку, которая принимает только документа, убедитесь, что toouse `Upload` вместо него.</span><span class="sxs-lookup"><span data-stu-id="d3a60-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="d3a60-197">Пример</span><span class="sxs-lookup"><span data-stu-id="d3a60-197">Example</span></span>
<span data-ttu-id="d3a60-198">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="d3a60-199">Его можно изменить toothis toofix все ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="d3a60-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="d3a60-200">Если требуется, можно дополнительно упростить его toothis.</span><span class="sxs-lookup"><span data-stu-id="d3a60-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="d3a60-201">Изменения IndexBatchException</span><span class="sxs-lookup"><span data-stu-id="d3a60-201">IndexBatchException changes</span></span>
<span data-ttu-id="d3a60-202">Hello `IndexBatchException.IndexResponse` свойство было изменено слишком`IndexingResults`, а его тип — теперь `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="d3a60-203">Пример</span><span class="sxs-lookup"><span data-stu-id="d3a60-203">Example</span></span>
<span data-ttu-id="d3a60-204">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="d3a60-205">Его можно изменить toothis toofix все ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="d3a60-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="d3a60-206">Изменение метода операции</span><span class="sxs-lookup"><span data-stu-id="d3a60-206">Operation method changes</span></span>
<span data-ttu-id="d3a60-207">Каждая операция hello пакет SDK Azure Search .NET представляется как набор перегруженных версий метода синхронные и асинхронные вызовы.</span><span class="sxs-lookup"><span data-stu-id="d3a60-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="d3a60-208">Hello подписи и разбиение эти перегрузки метода изменено в версии 1.1.</span><span class="sxs-lookup"><span data-stu-id="d3a60-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="d3a60-209">Например операция «Получить статистика индекса» в более ранних версиях пакета SDK для hello hello предоставлено следующими сигнатурами:</span><span class="sxs-lookup"><span data-stu-id="d3a60-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="d3a60-210">В `IIndexOperations` добавьте:</span><span class="sxs-lookup"><span data-stu-id="d3a60-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="d3a60-211">В `IndexOperationsExtensions` добавьте:</span><span class="sxs-lookup"><span data-stu-id="d3a60-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="d3a60-212">сигнатуры методов Hello для hello одной операции в версии 1.1 выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="d3a60-213">В `IIndexesOperations` добавьте:</span><span class="sxs-lookup"><span data-stu-id="d3a60-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="d3a60-214">В `IndexesOperationsExtensions` добавьте:</span><span class="sxs-lookup"><span data-stu-id="d3a60-214">In `IndexesOperationsExtensions`:</span></span>

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

<span data-ttu-id="d3a60-215">Начиная с версии 1.1 hello пакет SDK Azure Search .NET классифицирует методы операций по-разному.</span><span class="sxs-lookup"><span data-stu-id="d3a60-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="d3a60-216">Необязательные параметры теперь моделируются как параметры по умолчанию, а не как дополнительные перегрузки метода.</span><span class="sxs-lookup"><span data-stu-id="d3a60-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="d3a60-217">Это иногда значительно сокращает hello число перегрузок метода.</span><span class="sxs-lookup"><span data-stu-id="d3a60-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="d3a60-218">методы расширения Hello теперь скрыть много hello лишние сведений HTTP вызывающего hello.</span><span class="sxs-lookup"><span data-stu-id="d3a60-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="d3a60-219">Например, более старые версии пакета SDK вернул объект ответа с кодом состояния HTTP, который вы часто hello не требуется toocheck, так как операция методы создают исключение `CloudException` для любой код состояния, отображается сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="d3a60-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="d3a60-220">Здравствуйте, новые объекты модели только возвращаемым методы расширения, сохранение вы hello трудностей toounwrap их в коде.</span><span class="sxs-lookup"><span data-stu-id="d3a60-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="d3a60-221">И наоборот hello базовых интерфейсов теперь предоставляют методы, которые помогают управлять на уровне hello HTTP при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d3a60-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="d3a60-222">Теперь можно передавать в пользовательских toobe заголовки HTTP, входящие в запросы и новый hello `AzureOperationResponse<T>` возвращают тип предоставляет прямой доступ toohello `HttpRequestMessage` и `HttpResponseMessage` для операции hello.</span><span class="sxs-lookup"><span data-stu-id="d3a60-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="d3a60-223">`AzureOperationResponse`определен в hello `Microsoft.Rest.Azure` пространства имен и заменяет `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="d3a60-224">Изменения в параметрах оценки</span><span class="sxs-lookup"><span data-stu-id="d3a60-224">ScoringParameters changes</span></span>
<span data-ttu-id="d3a60-225">Новый класс с именем `ScoringParameter` был добавлен в последней toomake SDK hello его проще tooprovide tooscoring профилей параметры в запросе поиска.</span><span class="sxs-lookup"><span data-stu-id="d3a60-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="d3a60-226">Здравствуйте, ранее `ScoringProfiles` свойство hello `SearchParameters` был типом класса `IList<string>`; Теперь типизируется как `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="d3a60-227">Пример</span><span class="sxs-lookup"><span data-stu-id="d3a60-227">Example</span></span>
<span data-ttu-id="d3a60-228">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="d3a60-229">Его можно изменить toothis toofix все ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="d3a60-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="d3a60-230">Изменение классов модели</span><span class="sxs-lookup"><span data-stu-id="d3a60-230">Model class changes</span></span>
<span data-ttu-id="d3a60-231">Из-за изменения подписи toohello, описанные в [изменение метода операции](#OperationMethodChanges), во многих классах в hello `Microsoft.Azure.Search.Models` пространство имен был переименован или удален.</span><span class="sxs-lookup"><span data-stu-id="d3a60-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="d3a60-232">Например:</span><span class="sxs-lookup"><span data-stu-id="d3a60-232">For example:</span></span>

* <span data-ttu-id="d3a60-233">`IndexDefinitionResponse` был заменен на `AzureOperationResponse<Index>`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="d3a60-234">`DocumentSearchResponse`был переименован слишком`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="d3a60-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="d3a60-235">`IndexResult`был переименован слишком`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="d3a60-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="d3a60-236">`Documents.Count()`Теперь возвращает `long` с числом документов hello вместо`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="d3a60-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="d3a60-237">`IndexGetStatisticsResponse`был переименован слишком`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="d3a60-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="d3a60-238">`IndexListResponse`был переименован слишком`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="d3a60-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="d3a60-239">toosummarize, `OperationResponse`-производные классы, которые существовали только toowrap объекта модели будут удалены.</span><span class="sxs-lookup"><span data-stu-id="d3a60-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="d3a60-240">Hello остальные классы имели их суффикс изменилось с `Response` слишком`Result`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="d3a60-241">Пример</span><span class="sxs-lookup"><span data-stu-id="d3a60-241">Example</span></span>
<span data-ttu-id="d3a60-242">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-242">If your code looks like this:</span></span>

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

<span data-ttu-id="d3a60-243">Его можно изменить toothis toofix все ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="d3a60-243">You can change it toothis toofix any build errors:</span></span>

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="d3a60-244">Классы ответа и IEnumerable</span><span class="sxs-lookup"><span data-stu-id="d3a60-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="d3a60-245">Дополнительное изменение, которое может повлиять на код, состоит в том, что классы ответов, содержащие коллекции, больше не реализуют `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="d3a60-246">Вместо этого свойство коллекции hello можно работать напрямую.</span><span class="sxs-lookup"><span data-stu-id="d3a60-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="d3a60-247">Например, если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="d3a60-248">Его можно изменить toothis toofix все ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="d3a60-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="d3a60-249">Исключение, касающееся веб-приложений</span><span class="sxs-lookup"><span data-stu-id="d3a60-249">Special case for web applications</span></span>
<span data-ttu-id="d3a60-250">Если у вас есть веб-приложения, который выполняет сериализацию `DocumentSearchResponse` напрямую результаты поиска toosend toohello браузера, необходимо будет toochange кода или hello результаты не будут правильно сериализовать.</span><span class="sxs-lookup"><span data-stu-id="d3a60-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="d3a60-251">Например, если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="d3a60-252">Его можно изменить путем получения hello `.Results` свойство hello поиска ответа toofix поиска результат подготовки к просмотру:</span><span class="sxs-lookup"><span data-stu-id="d3a60-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="d3a60-253">Необходимо будет toolook в таких случаях в коде самостоятельно; **компилятора hello не выдаст** из-за `JsonResult.Data` относится к типу `object`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="d3a60-254">Изменения CloudException</span><span class="sxs-lookup"><span data-stu-id="d3a60-254">CloudException changes</span></span>
<span data-ttu-id="d3a60-255">Hello `CloudException` класс перемещен из hello `Hyak.Common` toohello имен `Microsoft.Rest.Azure` пространства имен.</span><span class="sxs-lookup"><span data-stu-id="d3a60-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="d3a60-256">Кроме того его `Error` свойство было изменено слишком`Body`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="d3a60-257">Изменения SearchServiceClient и SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="d3a60-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="d3a60-258">Здравствуйте, тип hello `Credentials` изменилось свойство с `SearchCredentials` tooits базового класса, `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="d3a60-259">Если вам требуется tooaccess hello `SearchCredentials` из `SearchIndexClient` или `SearchServiceClient`, используйте новый hello `SearchCredentials` свойство.</span><span class="sxs-lookup"><span data-stu-id="d3a60-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="d3a60-260">В более ранних версиях пакета SDK, hello `SearchServiceClient` и `SearchIndexClient` конструкторов, потребовалось бы `HttpClient` параметра.</span><span class="sxs-lookup"><span data-stu-id="d3a60-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="d3a60-261">Они были заменены конструкторами, принимающими `HttpClientHandler` и массив объектов `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="d3a60-262">Это позволяет упростить tooinstall пользовательские обработчики toopre процесса HTTP-запросов при необходимости.</span><span class="sxs-lookup"><span data-stu-id="d3a60-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="d3a60-263">Наконец, hello конструкторы, которое ушло `Uri` и `SearchCredentials` были изменены.</span><span class="sxs-lookup"><span data-stu-id="d3a60-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="d3a60-264">Например, если у вас есть код, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="d3a60-265">Его можно изменить toothis toofix все ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="d3a60-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="d3a60-266">Также Обратите внимание, что тип hello hello учетные данные параметра изменилось слишком`ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="d3a60-267">Это маловероятно, что tooaffect кода с момента `SearchCredentials` является производным от `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="d3a60-268">Передача идентификатора запроса</span><span class="sxs-lookup"><span data-stu-id="d3a60-268">Passing a request ID</span></span>
<span data-ttu-id="d3a60-269">В предыдущих версиях пакета SDK для hello, можно задать идентификатор запроса на hello `SearchServiceClient` или `SearchIndexClient` и он будет включен в каждый запрос toohello API-интерфейса REST.</span><span class="sxs-lookup"><span data-stu-id="d3a60-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="d3a60-270">Это полезно для устранения неполадок со службой поиска, если требуется поддержка toocontact.</span><span class="sxs-lookup"><span data-stu-id="d3a60-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="d3a60-271">Однако это более полезным tooset уникальный идентификатор запроса для каждой операции, а не toouse hello таким же Идентификатором для всех операций.</span><span class="sxs-lookup"><span data-stu-id="d3a60-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="d3a60-272">По этой причине hello `SetClientRequestId` методы `SearchServiceClient` и `SearchIndexClient` были удалены.</span><span class="sxs-lookup"><span data-stu-id="d3a60-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="d3a60-273">Вместо этого можно передать в метод операции tooeach идентификатор запроса через hello необязательно `SearchRequestOptions` параметра.</span><span class="sxs-lookup"><span data-stu-id="d3a60-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="d3a60-274">В следующем выпуске пакета SDK для hello мы добавим новый механизм для ИД запроса глобально на клиенте hello объектам параметров, согласованной с hello, который используется в других пакетах SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="d3a60-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="d3a60-275">Пример</span><span class="sxs-lookup"><span data-stu-id="d3a60-275">Example</span></span>
<span data-ttu-id="d3a60-276">Если у вас есть код, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="d3a60-277">Его можно изменить toothis toofix все ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="d3a60-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="d3a60-278">Изменение имени интерфейса</span><span class="sxs-lookup"><span data-stu-id="d3a60-278">Interface name changes</span></span>
<span data-ttu-id="d3a60-279">имена интерфейсов Hello операции группы имеют все измененные toobe согласуется с их соответствующих именах свойств:</span><span class="sxs-lookup"><span data-stu-id="d3a60-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="d3a60-280">Здравствуйте, тип `ISearchServiceClient.Indexes` было изменено с `IIndexOperations` слишком`IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="d3a60-281">Здравствуйте, тип `ISearchServiceClient.Indexers` было изменено с `IIndexerOperations` слишком`IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="d3a60-282">Здравствуйте, тип `ISearchServiceClient.DataSources` было изменено с `IDataSourceOperations` слишком`IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="d3a60-283">Здравствуйте, тип `ISearchIndexClient.Documents` было изменено с `IDocumentOperations` слишком`IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="d3a60-284">Это изменение — tooaffect маловероятно, что ваш код, если вы создали макеты этих интерфейсов для целей тестирования.</span><span class="sxs-lookup"><span data-stu-id="d3a60-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="d3a60-285">Исправления в версии 1.1</span><span class="sxs-lookup"><span data-stu-id="d3a60-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="d3a60-286">Произошла ошибка в более старых версиях tooserialization связанные пакет SDK Azure Search .NET hello классов пользовательскую модель.</span><span class="sxs-lookup"><span data-stu-id="d3a60-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="d3a60-287">Hello ошибка может произойти, если создан класс пользовательскую модель со свойством типа не допускающим значения.</span><span class="sxs-lookup"><span data-stu-id="d3a60-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="d3a60-288">Tooreproduce действия</span><span class="sxs-lookup"><span data-stu-id="d3a60-288">Steps tooreproduce</span></span>
<span data-ttu-id="d3a60-289">Создайте класс пользовательской модели со свойством типа значения, не допускающего нуля.</span><span class="sxs-lookup"><span data-stu-id="d3a60-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="d3a60-290">Например, добавьте открытое свойство `UnitCount` типа `int` вместо `int?`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="d3a60-291">Если индекс со значением по умолчанию hello этого типа документа (например, 0 для `int`), hello поле будет иметь значение null, если в службе поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="d3a60-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="d3a60-292">Если впоследствии вы ищете этого документа, hello `Search` вызова вызывает исключение `JsonSerializationException` обнаруживших, она не может преобразовать `null` слишком`int`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="d3a60-293">Кроме того фильтры могут не работать должным образом, поскольку null был написан toohello индекса вместо значения предназначен hello.</span><span class="sxs-lookup"><span data-stu-id="d3a60-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="d3a60-294">Сведения об исправлении</span><span class="sxs-lookup"><span data-stu-id="d3a60-294">Fix details</span></span>
<span data-ttu-id="d3a60-295">Эта проблема устранена в версии 1.1 hello SDK.</span><span class="sxs-lookup"><span data-stu-id="d3a60-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="d3a60-296">Теперь, если имеется такой класс модели:</span><span class="sxs-lookup"><span data-stu-id="d3a60-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="d3a60-297">и задать `IntValue` too0, что значение теперь правильно сериализуется как 0 сети hello и сохраняется как "0" в индексе hello.</span><span class="sxs-lookup"><span data-stu-id="d3a60-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="d3a60-298">Циклы обработки также работают ожидаемым образом.</span><span class="sxs-lookup"><span data-stu-id="d3a60-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="d3a60-299">Имеется один toobe потенциальные проблемы, учитывать при таком подходе: при использовании типа модели с запретом свойством, у вас есть слишком**гарантирует** что документов в индексе не будет содержать значение null для соответствующего поля hello.</span><span class="sxs-lookup"><span data-stu-id="d3a60-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="d3a60-300">Hello SDK ни hello REST API поиска Azure поможет вам tooenforce это.</span><span class="sxs-lookup"><span data-stu-id="d3a60-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="d3a60-301">Это не относится только к гипотетической: представьте себе ситуацию, когда Добавление нового поля tooan существующего индекса, тип которого `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="d3a60-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="d3a60-302">После обновления определения индекса hello, все документы будет иметь значение null для этого нового поля (поскольку все типы допускают значение NULL, если в службе поиска Azure).</span><span class="sxs-lookup"><span data-stu-id="d3a60-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="d3a60-303">При использовании модели с запретом `int` свойства для этого поля, вы получите `JsonSerializationException` при попытке документы tooretrieve следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d3a60-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="d3a60-304">По этой причине по-прежнему рекомендуется использовать типы, допускающие значения NULL, в классах модели.</span><span class="sxs-lookup"><span data-stu-id="d3a60-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="d3a60-305">Дополнительные сведения о исправления ошибок и hello см. в разделе [эту проблему на GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="d3a60-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

