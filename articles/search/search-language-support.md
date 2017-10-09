---
title: "aaaAzure поиска многоязыковой | Документы Microsoft"
description: "Служба поиска Azure поддерживает 56 языков — для этого используются языковые анализаторы Lucene и технология Майкрософт для обработки естественных языков."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="1b1ea-103">Создание индекса для многоязычных документов в поиске Azure</span><span class="sxs-lookup"><span data-stu-id="1b1ea-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="1b1ea-104">Портал</span><span class="sxs-lookup"><span data-stu-id="1b1ea-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="1b1ea-105">REST</span><span class="sxs-lookup"><span data-stu-id="1b1ea-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="1b1ea-106">.NET</span><span class="sxs-lookup"><span data-stu-id="1b1ea-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="1b1ea-107">Unleashing hello языковых анализаторов является так же легко, как свойство один параметр для поиска поля в определение индекса hello.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="1b1ea-108">Теперь можно выполнить этот шаг в портал hello.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="1b1ea-109">Ниже приведены снимки экрана приветствия колонках портала Azure для службы поиска Azure, позволяют пользователям toodefine схему индекса.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="1b1ea-110">В этой колонке пользователи могут создавать все поля hello и задать свойство анализатора hello для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b1ea-111">Можно задать только анализатора языка во время определения поля, как в при при создании нового индекса hello основание, или при добавлении нового поля tooan существующий индекс.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="1b1ea-112">Убедитесь, что полностью указывать все атрибуты, включая hello анализатора, при создании поля hello.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="1b1ea-113">Не быть может tooedit атрибутами hello или изменить тип анализатора hello после сохранения изменений.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="1b1ea-114">Добавление определения нового поля</span><span class="sxs-lookup"><span data-stu-id="1b1ea-114">Define a new field definition</span></span>
1. <span data-ttu-id="1b1ea-115">Войдите в toohello [портал Azure](https://portal.azure.com) и Привет открыть колонку службы поиска службы.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="1b1ea-116">Нажмите кнопку **добавить индекс** в hello командной строке вверху hello toostart панели мониторинга службы hello новый индекс или откройте существующий индекс tooset анализатора на новые поля, которые вы добавляете tooan существующий индекс.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="1b1ea-117">Появится колонки полей Hello, содержащее параметры для определения схемы hello hello индекса, в том числе вкладку анализатора hello используется для выбора анализатора языка.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="1b1ea-118">В полях запустите определение поля, указание имени и типа данных hello и задания атрибутов toomark hello поле как полный текст для поиска, в результаты поиска, можно использовать в структурах навигации аспекта, извлекаемые сортируемого и т. д.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="1b1ea-119">Прежде чем продолжить toohello следующее поле, откройте hello **анализатора** вкладки.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="1b1ea-120">![][1]
*tooselect анализатора, откройте вкладку анализатора hello в колонке поля hello*</span><span class="sxs-lookup"><span data-stu-id="1b1ea-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="1b1ea-121">Выбор анализатора</span><span class="sxs-lookup"><span data-stu-id="1b1ea-121">Choose an analyzer</span></span>
1. <span data-ttu-id="1b1ea-122">Прокрутите toofind hello поле, которое вы определяете.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="1b1ea-123">Если еще не помечен как поле hello как с возможностью поиска, нажмите кнопку toomark теперь флажок hello его как **доступный**.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="1b1ea-124">Выберите hello анализатора области toodisplay hello список доступных анализаторов.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="1b1ea-125">Выберите анализатор hello требуется toouse.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="1b1ea-126">![][2]
*Выберите один из hello Поддерживаемые анализаторы для каждого поля*</span><span class="sxs-lookup"><span data-stu-id="1b1ea-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="1b1ea-127">По умолчанию все поддерживающие поиск поля используют hello [Lucene стандартный анализатор](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) которого не зависит от языка.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="1b1ea-128">tooview hello полный список поддерживаемых анализаторов см. в разделе [языковая поддержка в поиске Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b1ea-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="1b1ea-129">Выбрав hello анализатора языка для поля, он будет использоваться при каждом запросе индексирования и поиска для этого поля.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="1b1ea-130">При выдаче запроса от нескольких полей с помощью различных анализаторов hello запрос будет обрабатываться независимо друг от друга hello правой анализаторы для каждого поля.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="1b1ea-131">Многие веб- и мобильных приложений обслуживает пользователей земного шара hello, с использованием различных языков.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="1b1ea-132">Это возможно toodefine индекса для сценария, как в данном путем создания поля для каждого поддерживаемого языка.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="1b1ea-133">![][3]
*Определение индекса с полем описания для каждого поддерживаемого языка*</span><span class="sxs-lookup"><span data-stu-id="1b1ea-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="1b1ea-134">Если известны языка hello hello агента, выполнение запроса, запрос поиска может быть tooa с областью конкретного поля, с помощью hello **searchFields** параметр запроса.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="1b1ea-135">Hello следующий запрос будет выполняться только для описания hello в польского языка:</span><span class="sxs-lookup"><span data-stu-id="1b1ea-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="1b1ea-136">Можно запросить индекс из портала hello, с помощью **обозреватель поиска** toopaste в toohello аналогичные запроса, которое показано выше.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="1b1ea-137">Поиск в обозревателе можно получить на панели команд hello в колонке службы hello.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="1b1ea-138">В разделе [запросить индекс поиска Azure на портале hello](search-explorer.md) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="1b1ea-139">Иногда hello языка hello агента, выполнение запроса не известно, в какой вариантов hello запрос может быть произведен от всех полей одновременно.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="1b1ea-140">При необходимости можно сделать какой-то язык предпочтительным, воспользовавшись [профилями оценки](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b1ea-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="1b1ea-141">В следующем примере hello совпадений, обнаруженных в описании hello на английском языке оцененные выше относительный toomatches в польский и французского языков:</span><span class="sxs-lookup"><span data-stu-id="1b1ea-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="1b1ea-142">Если вы разработчик .NET, обратите внимание, что можно настроить с помощью hello анализаторы языка [пакет SDK Azure Search .NET](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="1b1ea-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="1b1ea-143">последний выпуск Hello включает поддержку анализаторы языка Microsoft hello также.</span><span class="sxs-lookup"><span data-stu-id="1b1ea-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
