---
title: "Обновление пакета SDK службы поиска Azure для .NET до версии 1.1 | Документация Майкрософт"
description: "Обновление пакета SDK службы поиска Azure для .NET до версии 1.1"
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
ms.openlocfilehash: 9782454e3bfc697b63cde8aa28a14be0c393c36b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-net-sdk-version-3"></a><span data-ttu-id="db9c7-103">Обновление пакета SDK службы поиска Azure для .NET до версии 3</span><span class="sxs-lookup"><span data-stu-id="db9c7-103">Upgrading to the Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="db9c7-104">Если вы используете версию 2.0-preview [пакета SDK службы поиска Azure для .NET](https://aka.ms/search-sdk) или более раннюю, то эта статья поможет вам обновить приложение для использования версии 3.</span><span class="sxs-lookup"><span data-stu-id="db9c7-104">If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.</span></span>

<span data-ttu-id="db9c7-105">Более общее пошаговое руководство по пакету SDK, включая примеры, см. в разделе [Использование службы поиска Azure в приложении .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="db9c7-105">For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="db9c7-106">Версия 3 пакета SDK службы поиска Azure для .NET содержит некоторые отличия от более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="db9c7-106">Version 3 of the Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="db9c7-107">Эти отличия в основном незначительные, поэтому изменение кода потребует минимальных усилий.</span><span class="sxs-lookup"><span data-stu-id="db9c7-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="db9c7-108">В разделе [Действия по обновлению](#UpgradeSteps) вы найдете инструкции о том, как изменить код для использования новой версии пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="db9c7-108">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="db9c7-109">Если вы используете версию 1.0.2-preview или более раннюю, то сначала следует установить версию 1.1, и только затем обновить ее до версии 3.</span><span class="sxs-lookup"><span data-stu-id="db9c7-109">If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3.</span></span> <span data-ttu-id="db9c7-110">Ознакомьтесь с инструкциями в разделе [Приложение. Инструкции по обновлению до версии 1.1](#UpgradeStepsV1) .</span><span class="sxs-lookup"><span data-stu-id="db9c7-110">See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="db9c7-111">Экземпляр службы поиска Azure поддерживает несколько версий REST API, включая последнюю.</span><span class="sxs-lookup"><span data-stu-id="db9c7-111">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="db9c7-112">Можно продолжать использовать версию, которая больше не является последней, но рекомендуется выполнить перенос кода, чтобы использовать последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="db9c7-112">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span> <span data-ttu-id="db9c7-113">При использовании REST API необходимо указывать версию API в каждом запросе с помощью параметра api-version.</span><span class="sxs-lookup"><span data-stu-id="db9c7-113">When using the REST API, you must specify the API version in every request via the api-version parameter.</span></span> <span data-ttu-id="db9c7-114">При использовании пакета SDK для .NET версия пакета SDK, которую вы используете, определяет соответствующую версию REST API.</span><span class="sxs-lookup"><span data-stu-id="db9c7-114">When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API.</span></span> <span data-ttu-id="db9c7-115">Если вы используете устаревшую версию пакета SDK, можно продолжать выполнять этот код без изменений, даже если служба обновлена для поддержки более новой версии API.</span><span class="sxs-lookup"><span data-stu-id="db9c7-115">If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="db9c7-116">Новые возможности в версии 3</span><span class="sxs-lookup"><span data-stu-id="db9c7-116">What's new in version 3</span></span>
<span data-ttu-id="db9c7-117">Версия 3 пакета SDK службы поиска Azure для .NET предназначена для последней общедоступной версии интерфейса REST API службы поиска Azure, в частности версии 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="db9c7-117">Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="db9c7-118">Это дает возможность использовать различные новые функции службы поиска Azure из приложений для .NET, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="db9c7-118">This makes it possible to use many new features of Azure Search from a .NET application, including the following:</span></span>

* [<span data-ttu-id="db9c7-119">Пользовательские анализаторы</span><span class="sxs-lookup"><span data-stu-id="db9c7-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="db9c7-120">поддержка индексатора [хранилища BLOB-объектов Azure](search-howto-indexing-azure-blob-storage.md) и [хранилища таблиц Azure](search-howto-indexing-azure-tables.md);</span><span class="sxs-lookup"><span data-stu-id="db9c7-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="db9c7-121">настройка индексатора посредством [сопоставления полей](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="db9c7-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="db9c7-122">поддержка тегов eTag, обеспечивающих безопасное одновременное обновление определений индекса, индексаторов и источников данных;</span><span class="sxs-lookup"><span data-stu-id="db9c7-122">ETags support to enable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="db9c7-123">поддержка декларативного создания определений полей индекса через дополнение класса модели и с помощью нового класса `FieldBuilder`;</span><span class="sxs-lookup"><span data-stu-id="db9c7-123">Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.</span></span>
* <span data-ttu-id="db9c7-124">поддержка .NET Core и .NET Portable Profile 111.</span><span class="sxs-lookup"><span data-stu-id="db9c7-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="db9c7-125">Действия по обновлению</span><span class="sxs-lookup"><span data-stu-id="db9c7-125">Steps to upgrade</span></span>
<span data-ttu-id="db9c7-126">Прежде всего обновите справочник NuGet для `Microsoft.Azure.Search` , воспользовавшись консолью диспетчера пакетов NuGet или щелкнув правой кнопкой мыши ссылки проекта и выбрав "Управление пакетами NuGet" в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db9c7-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="db9c7-127">После того как NuGet загрузит новые пакеты и их зависимости, перестройте проект.</span><span class="sxs-lookup"><span data-stu-id="db9c7-127">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="db9c7-128">Сборка может быть выполнена успешно — в зависимости от того, как структурирован ваш код.</span><span class="sxs-lookup"><span data-stu-id="db9c7-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="db9c7-129">Если она выполнена, то теперь все готово.</span><span class="sxs-lookup"><span data-stu-id="db9c7-129">If so, you're ready to go!</span></span>

<span data-ttu-id="db9c7-130">В противном случае отобразится сообщение об ошибке сборки следующего вида.</span><span class="sxs-lookup"><span data-stu-id="db9c7-130">If your build fails, you should see a build error like the following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' to 'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="db9c7-131">Далее необходимо устранить эту ошибку сборки.</span><span class="sxs-lookup"><span data-stu-id="db9c7-131">The next step is to fix this build error.</span></span> <span data-ttu-id="db9c7-132">Сведения о причинах ошибки и способах ее устранения см. в разделе [Критические изменения в версии 3](#ListOfChanges).</span><span class="sxs-lookup"><span data-stu-id="db9c7-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.</span></span>

<span data-ttu-id="db9c7-133">Могут появиться дополнительные предупреждения о сборке, связанные с устаревшими методами или свойствами.</span><span class="sxs-lookup"><span data-stu-id="db9c7-133">You may see additional build warnings related to obsolete methods or properties.</span></span> <span data-ttu-id="db9c7-134">В предупреждениях будет указано, что следует использовать вместо устаревшей функции.</span><span class="sxs-lookup"><span data-stu-id="db9c7-134">The warnings will include instructions on what to use instead of the deprecated feature.</span></span> <span data-ttu-id="db9c7-135">Например, если приложение использует `IndexingParameters.Base64EncodeKeys`, то отобразится предупреждение `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-135">For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="db9c7-136">После устранения ошибки сборки при необходимости можно внести изменения в приложение, чтобы воспользоваться преимуществами новых функциональных возможностей.</span><span class="sxs-lookup"><span data-stu-id="db9c7-136">Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span> <span data-ttu-id="db9c7-137">Новые возможности в пакете SDK описаны в разделе [Новые возможности в версии 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="db9c7-137">New features in the SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="db9c7-138">Критические изменения в версии 3</span><span class="sxs-lookup"><span data-stu-id="db9c7-138">Breaking changes in version 3</span></span>
<span data-ttu-id="db9c7-139">В версии 3 содержится небольшое количество критических изменений, для которых может потребоваться изменение кода и выполнение повторной сборки приложения.</span><span class="sxs-lookup"><span data-stu-id="db9c7-139">There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="db9c7-140">Тип возвращаемого значения Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="db9c7-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="db9c7-141">Метод `Indexes.GetClient` имеет новый тип возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="db9c7-141">The `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="db9c7-142">Раньше он возвращал `SearchIndexClient`, но в версии 2.0-preview значение было изменено на `ISearchIndexClient`, и это изменение переносится в версию 3.</span><span class="sxs-lookup"><span data-stu-id="db9c7-142">Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3.</span></span> <span data-ttu-id="db9c7-143">Это необходимо для поддержки клиентов, которые желают макетировать метод `GetClient` для модульных тестов, возвращая реализацию макета `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-143">This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="db9c7-144">Пример</span><span class="sxs-lookup"><span data-stu-id="db9c7-144">Example</span></span>
<span data-ttu-id="db9c7-145">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="db9c7-146">Можно изменить его на следующий для устранения ошибок сборки:</span><span class="sxs-lookup"><span data-stu-id="db9c7-146">You can change it to this to fix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-to-strings"></a><span data-ttu-id="db9c7-147">Типы AnalyzerName, DataType и другие больше не преобразуются в строки неявным образом</span><span class="sxs-lookup"><span data-stu-id="db9c7-147">AnalyzerName, DataType, and others are no longer implicitly convertible to strings</span></span>
<span data-ttu-id="db9c7-148">В пакете SDK службы поиска Azure для .NET существует много типов, которые являются производными от `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-148">There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="db9c7-149">Ранее все они неявно преобразовывались в тип `string`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-149">Previously these types were all implicitly convertible to type `string`.</span></span> <span data-ttu-id="db9c7-150">Однако в реализации `Object.Equals` была обнаружена ошибка для этих классов, и для исправления данной ошибки потребовалось отключить неявное преобразование.</span><span class="sxs-lookup"><span data-stu-id="db9c7-150">However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion.</span></span> <span data-ttu-id="db9c7-151">При этом явное преобразование в тип `string` по-прежнему доступно.</span><span class="sxs-lookup"><span data-stu-id="db9c7-151">Explicit conversion to `string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="db9c7-152">Пример</span><span class="sxs-lookup"><span data-stu-id="db9c7-152">Example</span></span>
<span data-ttu-id="db9c7-153">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-153">If your code looks like this:</span></span>

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

<span data-ttu-id="db9c7-154">Можно изменить его на следующий для устранения ошибок сборки:</span><span class="sxs-lookup"><span data-stu-id="db9c7-154">You can change it to this to fix any build errors:</span></span>

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

### <a name="removed-obsolete-members"></a><span data-ttu-id="db9c7-155">Удалены устаревшие члены</span><span class="sxs-lookup"><span data-stu-id="db9c7-155">Removed obsolete members</span></span>

<span data-ttu-id="db9c7-156">Вы можете столкнуться с ошибками сборки, связанными с методами или свойствами, которые были отмечены в версии 2.0-preview как устаревшие, а в версии 3 были удалены.</span><span class="sxs-lookup"><span data-stu-id="db9c7-156">You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="db9c7-157">При возникновении таких ошибок воспользуйтесь описанными ниже способами их устранения.</span><span class="sxs-lookup"><span data-stu-id="db9c7-157">If you encounter such errors, here is how to resolve them:</span></span>

- <span data-ttu-id="db9c7-158">Если вы использовали конструктор `ScoringParameter(string name, string value)`, то вместо него воспользуйтесь этим: `ScoringParameter(string name, IEnumerable<string> values)`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="db9c7-159">Если вы использовали свойство `ScoringParameter.Value`, то вместо него воспользуйтесь свойством `ScoringParameter.Values` или методом `ToString`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-159">If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.</span></span>
- <span data-ttu-id="db9c7-160">Если вы использовали свойство `SearchRequestOptions.RequestId`, то вместо него воспользуйтесь свойством `ClientRequestId`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-160">If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="db9c7-161">Удалены функции предварительной версии</span><span class="sxs-lookup"><span data-stu-id="db9c7-161">Removed preview features</span></span>

<span data-ttu-id="db9c7-162">При обновлении с версии 2.0-preview до версии 3 учитывайте, что поддержка анализа JSON и CSV для индексаторов больших двоичных объектов была удалена, так как эта функция все еще находится на стадии предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="db9c7-162">If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="db9c7-163">В частности, удалены следующие методы класса `IndexingParametersExtensions`:</span><span class="sxs-lookup"><span data-stu-id="db9c7-163">Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="db9c7-164">Если ваше приложение имеет жесткую зависимость от этих функций, то вы не сможете обновить пакет SDK службы поиска Azure для .NET до версии 3.</span><span class="sxs-lookup"><span data-stu-id="db9c7-164">If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK.</span></span> <span data-ttu-id="db9c7-165">Вы можете и далее использовать версию 2.0-preview.</span><span class="sxs-lookup"><span data-stu-id="db9c7-165">You can continue to use version 2.0-preview.</span></span> <span data-ttu-id="db9c7-166">Однако необходимо учитывать, что **использовать предварительные версии пакетов SDK в рабочих приложениях не рекомендуется**.</span><span class="sxs-lookup"><span data-stu-id="db9c7-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="db9c7-167">Предварительные версии функций предназначены исключительно для оценки и могут изменяться.</span><span class="sxs-lookup"><span data-stu-id="db9c7-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="db9c7-168">Заключение</span><span class="sxs-lookup"><span data-stu-id="db9c7-168">Conclusion</span></span>
<span data-ttu-id="db9c7-169">Если вам нужны дополнительные сведения об использовании пакета SDK для .NET для Поиска Azure, то ознакомьтесь с нашим недавно обновленным [пошаговым руководством](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="db9c7-169">If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="db9c7-170">Будем рады вашим отзывам о пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="db9c7-170">We welcome your feedback on the SDK.</span></span> <span data-ttu-id="db9c7-171">Если вы столкнулись с проблемами, то всегда можете обратиться за помощью на [форуме по Поиску Azure на сайте MSDN](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="db9c7-171">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="db9c7-172">При обнаружении ошибки можно зарегистрировать проблему в [репозитории GitHub пакета SDK .NET для Azure](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="db9c7-172">If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="db9c7-173">Добавьте в название вашей проблемы префикс "пакет SDK для поиска:".</span><span class="sxs-lookup"><span data-stu-id="db9c7-173">Make sure to prefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="db9c7-174">Благодарим вас за использование поиска Azure!</span><span class="sxs-lookup"><span data-stu-id="db9c7-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-to-upgrade-to-version-11"></a><span data-ttu-id="db9c7-175">Приложение. Инструкции по обновлению до версии 1.1</span><span class="sxs-lookup"><span data-stu-id="db9c7-175">Appendix: Steps to upgrade to version 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="db9c7-176">Этот раздел относится только к пользователям версии 1.0.2-preview пакета SDK службы поиска Azure для .NET и более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="db9c7-176">This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="db9c7-177">Прежде всего обновите справочник NuGet для `Microsoft.Azure.Search` , воспользовавшись консолью диспетчера пакетов NuGet или щелкнув правой кнопкой мыши ссылки проекта и выбрав "Управление пакетами NuGet" в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="db9c7-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="db9c7-178">После того как NuGet загрузит новые пакеты и их зависимости, перестройте проект.</span><span class="sxs-lookup"><span data-stu-id="db9c7-178">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="db9c7-179">Если ранее вы пользовались предварительной версией 1.0.0, 1.0.1 или 1.0.2, построение будет выполнено успешно.</span><span class="sxs-lookup"><span data-stu-id="db9c7-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!</span></span>

<span data-ttu-id="db9c7-180">Если ранее вы пользовались предварительной версией 0.13.0 или более ранней, вы должны увидеть примерно такие ошибки построения:</span><span class="sxs-lookup"><span data-stu-id="db9c7-180">If you were previously using version 0.13.0-preview or older, you should see build errors like the following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: The type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="db9c7-181">Далее необходимо устранить ошибки построения одну за другой.</span><span class="sxs-lookup"><span data-stu-id="db9c7-181">The next step is to fix the build errors one by one.</span></span> <span data-ttu-id="db9c7-182">Большинство требует изменения некоторых имен классов и методов, которые были переименованы в пакете SDK.</span><span class="sxs-lookup"><span data-stu-id="db9c7-182">Most will require changing some class and method names that have been renamed in the SDK.</span></span> <span data-ttu-id="db9c7-183">[Список критических изменений в версии 1.1](#ListOfChangesV1) содержит список этих изменений имен.</span><span class="sxs-lookup"><span data-stu-id="db9c7-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="db9c7-184">Если вы используете настраиваемые классы для моделирования документов и эти классы имеют свойства примитивных типов, не допускающие нулевого значения (например `int` или `bool` в C#), в версии пакета SDK 1.1 существует исправление ошибки, которое следует иметь в виду.</span><span class="sxs-lookup"><span data-stu-id="db9c7-184">If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware.</span></span> <span data-ttu-id="db9c7-185">Дополнительные сведения см. в разделе [Исправления в версии 1.1](#BugFixesV1).</span><span class="sxs-lookup"><span data-stu-id="db9c7-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="db9c7-186">Наконец, после устранения ошибки сборки при необходимости можно внести изменения в приложение, чтобы воспользоваться преимуществами новых функциональных возможностей.</span><span class="sxs-lookup"><span data-stu-id="db9c7-186">Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="db9c7-187">Список критических изменений в версии 1.1</span><span class="sxs-lookup"><span data-stu-id="db9c7-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="db9c7-188">Следующий список упорядочен по вероятности того, повлияет ли изменение на код приложения.</span><span class="sxs-lookup"><span data-stu-id="db9c7-188">The following list is ordered by the likelihood that the change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="db9c7-189">Изменения IndexBatch и IndexAction</span><span class="sxs-lookup"><span data-stu-id="db9c7-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="db9c7-190">`IndexBatch.Create` был переименован в `IndexBatch.New` и больше не имеет аргумента `params`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-190">`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="db9c7-191">Можно использовать `IndexBatch.New` для пакетов, сочетающих в себе различные типы действий (слияние, удаление и т. д.).</span><span class="sxs-lookup"><span data-stu-id="db9c7-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="db9c7-192">Кроме того, существуют новые статические методы для создания пакетов, в которых все действия одинаковы: `Delete`, `Merge`, `MergeOrUpload` и `Upload`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-192">In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="db9c7-193">`IndexAction` больше не имеет открытых конструкторов, и его свойства теперь являются неизменяемыми.</span><span class="sxs-lookup"><span data-stu-id="db9c7-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="db9c7-194">Следует использовать новые статические методы для создания действий для различных целей: `Delete`, `Merge`, `MergeOrUpload` и `Upload`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-194">You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="db9c7-195">`IndexAction.Create` был удален.</span><span class="sxs-lookup"><span data-stu-id="db9c7-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="db9c7-196">Если используется перегрузка, которая принимает только документ, обязательно используйте вместо нее `Upload` .</span><span class="sxs-lookup"><span data-stu-id="db9c7-196">If you used the overload that takes only a document, make sure to use `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="db9c7-197">Пример</span><span class="sxs-lookup"><span data-stu-id="db9c7-197">Example</span></span>
<span data-ttu-id="db9c7-198">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="db9c7-199">Можно изменить его на следующий для устранения ошибок сборки:</span><span class="sxs-lookup"><span data-stu-id="db9c7-199">You can change it to this to fix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="db9c7-200">Если требуется, можно упростить его так:</span><span class="sxs-lookup"><span data-stu-id="db9c7-200">If you want, you can further simplify it to this:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="db9c7-201">Изменения IndexBatchException</span><span class="sxs-lookup"><span data-stu-id="db9c7-201">IndexBatchException changes</span></span>
<span data-ttu-id="db9c7-202">Свойство `IndexBatchException.IndexResponse` было переименовано в `IndexingResults`, и теперь его тип `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-202">The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="db9c7-203">Пример</span><span class="sxs-lookup"><span data-stu-id="db9c7-203">Example</span></span>
<span data-ttu-id="db9c7-204">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="db9c7-205">Можно изменить его на следующий для устранения ошибок сборки:</span><span class="sxs-lookup"><span data-stu-id="db9c7-205">You can change it to this to fix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="db9c7-206">Изменение метода операции</span><span class="sxs-lookup"><span data-stu-id="db9c7-206">Operation method changes</span></span>
<span data-ttu-id="db9c7-207">Каждая операция в пакете SDK для .NET для поиска Azure представляется как набор перегрузок метода для синхронных и асинхронных вызовов.</span><span class="sxs-lookup"><span data-stu-id="db9c7-207">Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="db9c7-208">В версии 1.1 были изменены подписи и разложение этих перегрузок метода.</span><span class="sxs-lookup"><span data-stu-id="db9c7-208">The signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="db9c7-209">Например, операция "Получить статистику индекса" в более старых версиях пакета SDK предоставляла эти подписи:</span><span class="sxs-lookup"><span data-stu-id="db9c7-209">For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:</span></span>

<span data-ttu-id="db9c7-210">В `IIndexOperations`добавьте:</span><span class="sxs-lookup"><span data-stu-id="db9c7-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="db9c7-211">В `IndexOperationsExtensions`добавьте:</span><span class="sxs-lookup"><span data-stu-id="db9c7-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="db9c7-212">Подписи метода для той же операции в версии 1.1 выглядят следующим образом.</span><span class="sxs-lookup"><span data-stu-id="db9c7-212">The method signatures for the same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="db9c7-213">В `IIndexesOperations`добавьте:</span><span class="sxs-lookup"><span data-stu-id="db9c7-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="db9c7-214">В `IndexesOperationsExtensions`добавьте:</span><span class="sxs-lookup"><span data-stu-id="db9c7-214">In `IndexesOperationsExtensions`:</span></span>

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

<span data-ttu-id="db9c7-215">Начиная с версии 1.1, пакет SDK для .NET для поиска Azure распределяет методы операции иначе:</span><span class="sxs-lookup"><span data-stu-id="db9c7-215">Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="db9c7-216">Необязательные параметры теперь моделируются как параметры по умолчанию, а не как дополнительные перегрузки метода.</span><span class="sxs-lookup"><span data-stu-id="db9c7-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="db9c7-217">Это уменьшает количество перегрузок метода, порой радикально.</span><span class="sxs-lookup"><span data-stu-id="db9c7-217">This reduces the number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="db9c7-218">Методы расширения теперь скрывают много лишних сведений HTTP от вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="db9c7-218">The extension methods now hide a lot of the extraneous details of HTTP from the caller.</span></span> <span data-ttu-id="db9c7-219">Например, более старые версии пакета SDK возвращали объект ответа с кодом состояния HTTP, который часто не нужно проверять, так как методы операции создают исключение `CloudException` для любого кода состояния, который указывает на ошибку.</span><span class="sxs-lookup"><span data-stu-id="db9c7-219">For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="db9c7-220">Новые методы расширения просто возвращают объекты модели, что устраняет необходимость развертывать их в коде.</span><span class="sxs-lookup"><span data-stu-id="db9c7-220">The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.</span></span>
* <span data-ttu-id="db9c7-221">И наоборот, основные интерфейсы теперь демонстрируют методы, которые предоставляют более полный контроль на уровне HTTP при необходимости.</span><span class="sxs-lookup"><span data-stu-id="db9c7-221">Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it.</span></span> <span data-ttu-id="db9c7-222">Теперь можно передавать пользовательские заголовки HTTP для добавления в запросы, и новый возвращаемый тип. Теперь можно передавать пользовательские заголовки HTTP для добавления в запросы, и новый возвращаемый тип `AzureOperationResponse<T>` предоставляет прямой доступ к `HttpRequestMessage` и `HttpResponseMessage` для операции.</span><span class="sxs-lookup"><span data-stu-id="db9c7-222">You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation.</span></span> <span data-ttu-id="db9c7-223">`AzureOperationResponse` определяется в пространстве имен `Microsoft.Rest.Azure` и заменяет `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-223">`AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="db9c7-224">Изменения в параметрах оценки</span><span class="sxs-lookup"><span data-stu-id="db9c7-224">ScoringParameters changes</span></span>
<span data-ttu-id="db9c7-225">В последнюю версию пакета SDK был добавлен класс `ScoringParameter` для упрощения передачи параметров профилям оценки в поисковом запросе.</span><span class="sxs-lookup"><span data-stu-id="db9c7-225">A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query.</span></span> <span data-ttu-id="db9c7-226">Ранее свойство `ScoringProfiles` класса `SearchParameters` имело тип `IList<string>`. Теперь оно имеет тип `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-226">Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="db9c7-227">Пример</span><span class="sxs-lookup"><span data-stu-id="db9c7-227">Example</span></span>
<span data-ttu-id="db9c7-228">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="db9c7-229">Можно изменить его на следующий для устранения ошибок сборки:</span><span class="sxs-lookup"><span data-stu-id="db9c7-229">You can change it to this to fix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="db9c7-230">Изменение классов модели</span><span class="sxs-lookup"><span data-stu-id="db9c7-230">Model class changes</span></span>
<span data-ttu-id="db9c7-231">Из-за изменений подписи, описанных в разделе [Изменение метода операции](#OperationMethodChanges), многие классы в пространстве имен `Microsoft.Azure.Search.Models` были переименованы или удалены.</span><span class="sxs-lookup"><span data-stu-id="db9c7-231">Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="db9c7-232">Например:</span><span class="sxs-lookup"><span data-stu-id="db9c7-232">For example:</span></span>

* <span data-ttu-id="db9c7-233">`IndexDefinitionResponse` был заменен на `AzureOperationResponse<Index>`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="db9c7-234">`DocumentSearchResponse` был переименован в `DocumentSearchResult`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-234">`DocumentSearchResponse` has been renamed to `DocumentSearchResult`</span></span>
* <span data-ttu-id="db9c7-235">`IndexResult` был переименован в `IndexingResult`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-235">`IndexResult` has been renamed to `IndexingResult`</span></span>
* <span data-ttu-id="db9c7-236">`Documents.Count()` теперь возвращает `long` с количеством документов вместо `DocumentCountResponse`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-236">`Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="db9c7-237">`IndexGetStatisticsResponse` был переименован в `IndexGetStatisticsResult`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-237">`IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="db9c7-238">`IndexListResponse` был переименован в `IndexListResult`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-238">`IndexListResponse` has been renamed to `IndexListResult`</span></span>

<span data-ttu-id="db9c7-239">Подводя итог, классы, производные от `OperationResponse`, которые существовали только для оборачивания объектов модели, были удалены.</span><span class="sxs-lookup"><span data-stu-id="db9c7-239">To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed.</span></span> <span data-ttu-id="db9c7-240">В остальных классах суффикс изменен с `Response` на `Result`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-240">The remaining classes have had their suffix changed from `Response` to `Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="db9c7-241">Пример</span><span class="sxs-lookup"><span data-stu-id="db9c7-241">Example</span></span>
<span data-ttu-id="db9c7-242">Если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-242">If your code looks like this:</span></span>

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

<span data-ttu-id="db9c7-243">Можно изменить его на следующий для устранения ошибок сборки:</span><span class="sxs-lookup"><span data-stu-id="db9c7-243">You can change it to this to fix any build errors:</span></span>

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

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="db9c7-244">Классы ответа и IEnumerable</span><span class="sxs-lookup"><span data-stu-id="db9c7-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="db9c7-245">Дополнительное изменение, которое может повлиять на код, состоит в том, что классы ответов, содержащие коллекции, больше не реализуют `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="db9c7-246">Вместо этого вы можете получать прямой доступ к свойству коллекции.</span><span class="sxs-lookup"><span data-stu-id="db9c7-246">Instead, you can access the collection property directly.</span></span> <span data-ttu-id="db9c7-247">Например, если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="db9c7-248">Можно изменить его на следующий для устранения ошибок сборки:</span><span class="sxs-lookup"><span data-stu-id="db9c7-248">You can change it to this to fix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="db9c7-249">Исключение, касающееся веб-приложений</span><span class="sxs-lookup"><span data-stu-id="db9c7-249">Special case for web applications</span></span>
<span data-ttu-id="db9c7-250">Если у вас есть веб-приложение, которое сериализует `DocumentSearchResponse` непосредственно для отправки результатов поиска в браузер, необходимо будет внести изменения в код, иначе результаты не будут сериализованы правильно.</span><span class="sxs-lookup"><span data-stu-id="db9c7-250">If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly.</span></span> <span data-ttu-id="db9c7-251">Например, если код выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="db9c7-252">Его можно изменить путем получения свойства `.Results` для ответа поиска, чтобы исправить отрисовку результата поиска.</span><span class="sxs-lookup"><span data-stu-id="db9c7-252">You can change it by getting the `.Results` property of the search response to fix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="db9c7-253">Вам придется найти такие случаи в коде самостоятельно. **Компилятор не предупредит вас**, так как `JsonResult.Data` имеет тип `object`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-253">You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="db9c7-254">Изменения CloudException</span><span class="sxs-lookup"><span data-stu-id="db9c7-254">CloudException changes</span></span>
<span data-ttu-id="db9c7-255">Класс `CloudException` перемещен из пространства имен `Hyak.Common` в пространство имен `Microsoft.Rest.Azure`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-255">The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="db9c7-256">Кроме того, его свойство `Error` было изменено на `Body`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-256">Also, its `Error` property has been renamed to `Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="db9c7-257">Изменения SearchServiceClient и SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="db9c7-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="db9c7-258">Тип свойства `Credentials` был изменен с `SearchCredentials` на базовый класс `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-258">The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="db9c7-259">Если необходимо получить доступ к `SearchCredentials` из `SearchIndexClient` или `SearchServiceClient`, используйте новое свойство `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-259">If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.</span></span>

<span data-ttu-id="db9c7-260">В более старых версиях пакета SDK у `SearchServiceClient` и `SearchIndexClient` были конструкторы, которые принимали параметр `HttpClient`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-260">In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="db9c7-261">Они были заменены конструкторами, принимающими `HttpClientHandler` и массив объектов `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="db9c7-262">При необходимости это упрощает установку пользовательских обработчиков для предварительной обработки HTTP-запросов.</span><span class="sxs-lookup"><span data-stu-id="db9c7-262">This makes it easier to install custom handlers to pre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="db9c7-263">Наконец, изменились конструкторы, которые принимали `Uri` и `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-263">Finally, the constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="db9c7-264">Например, если у вас есть код, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="db9c7-265">Можно изменить его на следующий для устранения ошибок сборки:</span><span class="sxs-lookup"><span data-stu-id="db9c7-265">You can change it to this to fix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="db9c7-266">Также обратите внимание, что тип параметра учетных данных изменился на `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-266">Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`.</span></span> <span data-ttu-id="db9c7-267">Это вряд ли повлияет на код, так как `SearchCredentials` является производным от `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-267">This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="db9c7-268">Передача идентификатора запроса</span><span class="sxs-lookup"><span data-stu-id="db9c7-268">Passing a request ID</span></span>
<span data-ttu-id="db9c7-269">В более старых версиях пакета SDK можно было задать идентификатор запроса в `SearchServiceClient` или `SearchIndexClient`, и он включался в каждый запрос к REST API.</span><span class="sxs-lookup"><span data-stu-id="db9c7-269">In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API.</span></span> <span data-ttu-id="db9c7-270">Это полезно для устранения неполадок в службе поиска, если необходимо обратиться в службу поддержки.</span><span class="sxs-lookup"><span data-stu-id="db9c7-270">This is useful for troubleshooting issues with your search service if you need to contact support.</span></span> <span data-ttu-id="db9c7-271">Однако более полезно присвоить уникальный идентификатор запроса для каждой операции, а не использовать тот же идентификатор для всех операций.</span><span class="sxs-lookup"><span data-stu-id="db9c7-271">However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations.</span></span> <span data-ttu-id="db9c7-272">По этой причине методы `SetClientRequestId` из `SearchServiceClient` и `SearchIndexClient` были удалены.</span><span class="sxs-lookup"><span data-stu-id="db9c7-272">For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="db9c7-273">Вместо этого вы можете передать идентификатор запроса для каждого метода операции через необязательный параметр `SearchRequestOptions` .</span><span class="sxs-lookup"><span data-stu-id="db9c7-273">Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="db9c7-274">В будущем выпуске пакета SDK мы добавим новый механизм для глобальной настройки идентификатора запроса на объектах клиента, который согласован с подходом, используемым другим пакетом SDK Azure.</span><span class="sxs-lookup"><span data-stu-id="db9c7-274">In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="db9c7-275">Пример</span><span class="sxs-lookup"><span data-stu-id="db9c7-275">Example</span></span>
<span data-ttu-id="db9c7-276">Если у вас есть код, который выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="db9c7-277">Можно изменить его на следующий для устранения ошибок сборки:</span><span class="sxs-lookup"><span data-stu-id="db9c7-277">You can change it to this to fix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="db9c7-278">Изменение имени интерфейса</span><span class="sxs-lookup"><span data-stu-id="db9c7-278">Interface name changes</span></span>
<span data-ttu-id="db9c7-279">Имена интерфейсов группы операций изменены, чтобы согласовать их с соответствующими именами свойств:</span><span class="sxs-lookup"><span data-stu-id="db9c7-279">The operation group interface names have all changed to be consistent with their corresponding property names:</span></span>

* <span data-ttu-id="db9c7-280">Тип `ISearchServiceClient.Indexes` был переименован из `IIndexOperations` в `IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-280">The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.</span></span>
* <span data-ttu-id="db9c7-281">Тип `ISearchServiceClient.Indexers` был переименован из `IIndexerOperations` в `IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-281">The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.</span></span>
* <span data-ttu-id="db9c7-282">Тип `ISearchServiceClient.DataSources` был переименован из `IDataSourceOperations` в `IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-282">The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.</span></span>
* <span data-ttu-id="db9c7-283">Тип `ISearchIndexClient.Documents` был переименован из `IDocumentOperations` в `IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-283">The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.</span></span>

<span data-ttu-id="db9c7-284">Это изменение вряд ли повлияет на код, если вы не создали макеты этих интерфейсов для тестирования.</span><span class="sxs-lookup"><span data-stu-id="db9c7-284">This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="db9c7-285">Исправления в версии 1.1</span><span class="sxs-lookup"><span data-stu-id="db9c7-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="db9c7-286">В более старых версиях пакета SDK для .NET для поиска Azure была ошибка, связанная с сериализацией классов пользовательской модели.</span><span class="sxs-lookup"><span data-stu-id="db9c7-286">There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes.</span></span> <span data-ttu-id="db9c7-287">Ошибка могла произойти, если вы создавали класс пользовательской модели со свойством типа значения, не допускающего нуля.</span><span class="sxs-lookup"><span data-stu-id="db9c7-287">The bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-to-reproduce"></a><span data-ttu-id="db9c7-288">Шаги для воспроизведения</span><span class="sxs-lookup"><span data-stu-id="db9c7-288">Steps to reproduce</span></span>
<span data-ttu-id="db9c7-289">Создайте класс пользовательской модели со свойством типа значения, не допускающего нуля.</span><span class="sxs-lookup"><span data-stu-id="db9c7-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="db9c7-290">Например, добавьте открытое свойство `UnitCount` типа `int` вместо `int?`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="db9c7-291">При индексировании документа со значением по умолчанию этого типа (например 0 для `int`) поле будет иметь значение NULL в Поиске Azure.</span><span class="sxs-lookup"><span data-stu-id="db9c7-291">If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search.</span></span> <span data-ttu-id="db9c7-292">Если впоследствии выполняется поиск этого документа, вызов `Search` выдаст `JsonSerializationException` с сообщением о том, что невозможно преобразовать `null` в `int`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-292">If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.</span></span>

<span data-ttu-id="db9c7-293">Кроме того, фильтры могут не работать, как ожидалось, поскольку в индекс был записано значение null вместо ожидаемого значения.</span><span class="sxs-lookup"><span data-stu-id="db9c7-293">Also, filters may not work as expected since null was written to the index instead of the intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="db9c7-294">Сведения об исправлении</span><span class="sxs-lookup"><span data-stu-id="db9c7-294">Fix details</span></span>
<span data-ttu-id="db9c7-295">Эта проблема устранена в пакете SDK версии 1.1.</span><span class="sxs-lookup"><span data-stu-id="db9c7-295">We have fixed this issue in version 1.1 of the SDK.</span></span> <span data-ttu-id="db9c7-296">Теперь, если имеется такой класс модели:</span><span class="sxs-lookup"><span data-stu-id="db9c7-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="db9c7-297">и вы устанавливаете для `IntValue` значение 0, это значение теперь правильно сериализуется как 0 по сети и сохраняется как 0 в индексе.</span><span class="sxs-lookup"><span data-stu-id="db9c7-297">and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index.</span></span> <span data-ttu-id="db9c7-298">Циклы обработки также работают ожидаемым образом.</span><span class="sxs-lookup"><span data-stu-id="db9c7-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="db9c7-299">Существует одна потенциальная проблема, которую следует учитывать при таком подходе: при использовании типа модели со свойством, не допускающим значения NULL, необходимо **гарантировать** , что документы в индексе не будут содержать значение NULL для соответствующего поля.</span><span class="sxs-lookup"><span data-stu-id="db9c7-299">There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="db9c7-300">Ни пакет SDK, ни API REST поиска Azure не поможет вам это обеспечить.</span><span class="sxs-lookup"><span data-stu-id="db9c7-300">Neither the SDK nor the Azure Search REST API will help you to enforce this.</span></span>

<span data-ttu-id="db9c7-301">Это не просто гипотетическое соображение. Представьте себе ситуацию, когда вы добавляете новое поле в существующий индекс с типом `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="db9c7-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="db9c7-302">После обновления определения индекса все документы будут иметь значение null для этого нового поля (поскольку все типы допускают значение NULL в службе поиска Azure).</span><span class="sxs-lookup"><span data-stu-id="db9c7-302">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="db9c7-303">Если затем для этого поля вы используете класс модели со свойством `int`, не допускающим нулевое значение, при попытке получения документов вы получите `JsonSerializationException` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db9c7-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="db9c7-304">По этой причине по-прежнему рекомендуется использовать типы, допускающие значения NULL, в классах модели.</span><span class="sxs-lookup"><span data-stu-id="db9c7-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="db9c7-305">Дополнительные сведения по этой ошибке и исправлению см. в разделе об [этой проблеме на GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="db9c7-305">For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

