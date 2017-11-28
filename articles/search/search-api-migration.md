---
title: "aaaUpgrading toohello API REST службы поиска Azure версии 2016-09-01 | Документы Microsoft"
description: "Обновление toohello API REST службы поиска Azure версии 2016-09-01"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="72cdc-103">Обновление toohello API REST службы поиска Azure версии 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="72cdc-103">Upgrading toohello Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="72cdc-104">Если вы используете версию 2015-02-28 или 2015-02-28-Preview из hello [API REST службы поиска Azure](https://msdn.microsoft.com/library/azure/dn798935.aspx), эта статья поможет вам обновить приложения toouse hello Далее общедоступной API версии, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="72cdc-104">If you're using version 2015-02-28 or 2015-02-28-Preview of hello [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application toouse hello next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="72cdc-105">Версии 2016-09-01 из API-интерфейса REST hello содержит некоторые изменения из более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="72cdc-105">Version 2016-09-01 of hello REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="72cdc-106">Эти отличия в основном обратно совместимы, поэтому изменение кода потребует минимальных усилий в зависимости от версии, которая использовался ранее.</span><span class="sxs-lookup"><span data-stu-id="72cdc-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="72cdc-107">В разделе [tooupgrade действия](#UpgradeSteps) инструкции toochange новой версии API код toouse hello.</span><span class="sxs-lookup"><span data-stu-id="72cdc-107">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="72cdc-108">Экземпляр службы поиска Azure поддерживает несколько версий API-Интерфейс REST, включая hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="72cdc-108">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="72cdc-109">Вы можете продолжить toouse версии, когда он больше не hello последнюю версию, но рекомендуется перейти к toouse кода hello последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="72cdc-109">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="72cdc-110">Новые возможности в версии 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="72cdc-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="72cdc-111">Версии 2016-09-01 — второй общедоступной версии hello hello API REST службы поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="72cdc-111">Version 2016-09-01 is hello second generally available release of hello Azure Search Service REST API.</span></span> <span data-ttu-id="72cdc-112">Новые возможности в этой версии API:</span><span class="sxs-lookup"><span data-stu-id="72cdc-112">New features in this API version include:</span></span>

* <span data-ttu-id="72cdc-113">[Пользовательские анализаторы](https://aka.ms/customanalyzers), которая разрешает tootake контроль над процессом hello преобразования текста в токены индексируемых и с возможностью поиска.</span><span class="sxs-lookup"><span data-stu-id="72cdc-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you tootake control over hello process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="72cdc-114">[Хранилище больших двоичных объектов Azure](search-howto-indexing-azure-blob-storage.md) и [табличного хранилища Azure](search-howto-indexing-azure-tables.md) индексаторы, которые позволяют вам tooeasily импортировать данные из хранилища Azure в поиске Azure, по расписанию или по требованию.</span><span class="sxs-lookup"><span data-stu-id="72cdc-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you tooeasily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="72cdc-115">[Поля сопоставления](search-indexer-field-mappings.md), которая разрешает toocustomize как индексаторов в поиске Azure для импорта данных.</span><span class="sxs-lookup"><span data-stu-id="72cdc-115">[Field mappings](search-indexer-field-mappings.md), which allow you toocustomize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="72cdc-116">Теги eTag, разрешающих tooupdate hello определений индексов, индексаторов и источников данных в режиме параллелизма.</span><span class="sxs-lookup"><span data-stu-id="72cdc-116">ETags, which allow you tooupdate hello definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="72cdc-117">Tooupgrade действия</span><span class="sxs-lookup"><span data-stu-id="72cdc-117">Steps tooupgrade</span></span>
<span data-ttu-id="72cdc-118">При обновлении с версии 2015-02-28, скорее всего, будут toomake tooyour любого изменения кода, кроме номера версии toochange hello.</span><span class="sxs-lookup"><span data-stu-id="72cdc-118">If you are upgrading from version 2015-02-28, you probably won't have toomake any changes tooyour code, other than toochange hello version number.</span></span> <span data-ttu-id="72cdc-119">Hello только ситуации, в которых может потребоваться toochange кода, когда:</span><span class="sxs-lookup"><span data-stu-id="72cdc-119">hello only situations in which you may need toochange code are when:</span></span>

* <span data-ttu-id="72cdc-120">Код завершается ошибкой, если в ответе API возвращаются нераспознанные свойства.</span><span class="sxs-lookup"><span data-stu-id="72cdc-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="72cdc-121">По умолчанию приложение должно игнорировать свойства, которые не распознаются.</span><span class="sxs-lookup"><span data-stu-id="72cdc-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="72cdc-122">Код сохраняет запросы API-интерфейса и пытается tooresend их toohello новой версии API.</span><span class="sxs-lookup"><span data-stu-id="72cdc-122">Your code persists API requests and tries tooresend them toohello new API version.</span></span> <span data-ttu-id="72cdc-123">Например, это может произойти, если приложение сохраняет токены продолжения, возвращенный API поиска hello (Дополнительные сведения см. по `@search.nextPageParameters` в hello [Справочник по API поиска](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="72cdc-123">For example, this might happen if your application persists continuation tokens returned from hello Search API (for more information, look for `@search.nextPageParameters` in hello [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="72cdc-124">Если любой из этих ситуаций применить tooyou, затем может потребоваться toochange код соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="72cdc-124">If either of these situations apply tooyou, then you may need toochange your code accordingly.</span></span> <span data-ttu-id="72cdc-125">В противном случае никаких изменений не требуется Если не требуется, чтобы с помощью hello toostart [новые функции](#WhatsNew) версии 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="72cdc-125">Otherwise, no changes should be necessary unless you want toostart using hello [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="72cdc-126">При обновлении с версии 2015-02-28-Preview hello выше также применяется, но также следует иметь в виду, что некоторые функции предварительной версии не доступны в версии 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="72cdc-126">If you are upgrading from version 2015-02-28-Preview, hello above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="72cdc-127">Поддержка индексатора хранилища BLOB-объектов Azure для CSV-файлов и больших двоичных объектов, содержащих массивы JSON.</span><span class="sxs-lookup"><span data-stu-id="72cdc-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="72cdc-128">синонимы;</span><span class="sxs-lookup"><span data-stu-id="72cdc-128">Synonyms</span></span>
* <span data-ttu-id="72cdc-129">Запросы "Скорее всего".</span><span class="sxs-lookup"><span data-stu-id="72cdc-129">"More like this" queries</span></span>

<span data-ttu-id="72cdc-130">Если ваш код использует эти функции, нельзя будет tooupgrade too2016-09-01 без удаления их использования.</span><span class="sxs-lookup"><span data-stu-id="72cdc-130">If your code uses these features, you will not be able tooupgrade too2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72cdc-131">Помните, что предварительные версии API предназначены для тестирования и ознакомления. Они не должны использоваться в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="72cdc-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="72cdc-132">Заключение</span><span class="sxs-lookup"><span data-stu-id="72cdc-132">Conclusion</span></span>
<span data-ttu-id="72cdc-133">Если требуются дополнительные сведения об использовании hello API REST службы поиска Azure, см. раздел hello недавно обновленного [Справочник по API](https://msdn.microsoft.com/library/azure/dn798935.aspx) на сайте MSDN.</span><span class="sxs-lookup"><span data-stu-id="72cdc-133">If you need more details on using hello Azure Search Service REST API, see hello recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="72cdc-134">Будем рады вашим отзывам о службе поиска Azure.</span><span class="sxs-lookup"><span data-stu-id="72cdc-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="72cdc-135">Если возникли проблемы, вы бесплатно tooask нам для получения справки по hello [форум MSDN поиска Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) или [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="72cdc-135">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="72cdc-136">Если вы требуете вопрос о Azure поиск на сайте StackOverflow, убедитесь, что tootag с `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="72cdc-136">If you're asking a question about Azure Search on StackOverflow, make sure tootag it with `azure-search`.</span></span>

<span data-ttu-id="72cdc-137">Благодарим вас за использование поиска Azure!</span><span class="sxs-lookup"><span data-stu-id="72cdc-137">Thank you for using Azure Search!</span></span>

