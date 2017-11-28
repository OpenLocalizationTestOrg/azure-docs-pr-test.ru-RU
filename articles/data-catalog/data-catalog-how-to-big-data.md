---
title: "toowork aaaHow с источниками данных «большие данные» | Документы Microsoft"
description: "Как tooarticle выделения шаблоны с помощью каталога данных Azure с источниками данных «большие данные», включая хранилища больших двоичных объектов, Озера данных Azure и Hadoop HDFS."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="2351c-103">Как источники toowork с большими данными в каталоге данных Azure</span><span class="sxs-lookup"><span data-stu-id="2351c-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="2351c-104">Введение</span><span class="sxs-lookup"><span data-stu-id="2351c-104">Introduction</span></span>
<span data-ttu-id="2351c-105">**Каталог данных Microsoft Azure** — это полностью управляемая облачная служба, выполняющая функции систем регистрации и обнаружения корпоративных источников данных.</span><span class="sxs-lookup"><span data-stu-id="2351c-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="2351c-106">Все дело помогает пользователям обнаруживать, понять и использовать источники данных и помогает организациям tooget дополнительные значения из своих существующих источников данных, включая большие наборы данных.</span><span class="sxs-lookup"><span data-stu-id="2351c-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="2351c-107">**Каталог данных Azure** поддерживает hello регистрации BLOB-хранилище больших двоичных объектов и каталоги, а также Hadoop HDFS-файлов и каталогов.</span><span class="sxs-lookup"><span data-stu-id="2351c-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="2351c-108">Hello полуструктурированные характер этих источников данных предоставляет большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="2351c-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="2351c-109">Однако tooget hello максимальную пользу из их с регистрации **каталога данных Azure**, пользователям необходимо учитывать, как организованы hello источников данных.</span><span class="sxs-lookup"><span data-stu-id="2351c-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="2351c-110">Каталоги как логические наборы данных</span><span class="sxs-lookup"><span data-stu-id="2351c-110">Directories as logical data sets</span></span>
<span data-ttu-id="2351c-111">Распространенный подход для организации источников данных большого размера — tootreat каталоги как логические наборы данных.</span><span class="sxs-lookup"><span data-stu-id="2351c-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="2351c-112">Каталоги верхнего уровня, используемых toodefine набор данных, когда подпапки секции, и определить hello файлы, содержащиеся в них самих данных hello.</span><span class="sxs-lookup"><span data-stu-id="2351c-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="2351c-113">Пример такого подхода:</span><span class="sxs-lookup"><span data-stu-id="2351c-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="2351c-114">В этом примере vehicle_maintenance_events и location_tracking_events представляют логические наборы данных.</span><span class="sxs-lookup"><span data-stu-id="2351c-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="2351c-115">Каждая из этих папок содержит файлы данных, разделенные на вложенные папки по году и месяцу.</span><span class="sxs-lookup"><span data-stu-id="2351c-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="2351c-116">Каждая из вложенных папок может содержать сотни и тысячи файлов.</span><span class="sxs-lookup"><span data-stu-id="2351c-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="2351c-117">При таком подходе регистрация отдельных файлов в **каталоге данных Azure** не имеет смысла.</span><span class="sxs-lookup"><span data-stu-id="2351c-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="2351c-118">Вместо этого зарегистрируйте hello каталоги, которые представляют Привет наборы данных, которые быть toohello может применяться пользователями, работа с данными hello.</span><span class="sxs-lookup"><span data-stu-id="2351c-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="2351c-119">Справочные файлы данных</span><span class="sxs-lookup"><span data-stu-id="2351c-119">Reference data files</span></span>
<span data-ttu-id="2351c-120">Дополнительный шаблон — наборы данных ссылок toostore как отдельные файлы.</span><span class="sxs-lookup"><span data-stu-id="2351c-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="2351c-121">Эти наборы данных могут рассматриваться как hello «небольшое» части большие наборы данных и часто являются аналогичные toodimensions в модель аналитических данных.</span><span class="sxs-lookup"><span data-stu-id="2351c-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="2351c-122">Справочник по файлы данных содержат записи, используемые tooprovide контекст для массового hello hello файлов данных, хранимых в другом месте в хранилище данных большого размера hello.</span><span class="sxs-lookup"><span data-stu-id="2351c-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="2351c-123">Пример такого подхода:</span><span class="sxs-lookup"><span data-stu-id="2351c-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="2351c-124">Работая специалист по анализу данных или аналитик hello содержит данные в hello большего размера структуры каталогов, hello данные в этих файлах ссылки могут быть используется tooprovide более подробные сведения для сущностей, которые являются называется tooonly по имени или Идентификатору в hello больший объем данных набор.</span><span class="sxs-lookup"><span data-stu-id="2351c-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="2351c-125">В этом шаблоне имеет смысл tooregister hello отдельных эталонных данных файлов с **каталога данных Azure**.</span><span class="sxs-lookup"><span data-stu-id="2351c-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="2351c-126">Каждый файл представляет набор данных и может быть аннотирован и обнаружен независимо от других файлов.</span><span class="sxs-lookup"><span data-stu-id="2351c-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="2351c-127">Альтернативные подходы</span><span class="sxs-lookup"><span data-stu-id="2351c-127">Alternate patterns</span></span>
<span data-ttu-id="2351c-128">Hello шаблонов, описанных в предшествующих раздел hello являются только два возможных способа хранилище большие наборы данных могут быть организованы, но каждая реализация отличается.</span><span class="sxs-lookup"><span data-stu-id="2351c-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="2351c-129">Независимо от того, как структурированы источникам данных, при регистрации источников данных большого размера с **каталога данных Azure**, сосредоточиться на регистрация hello файлы и каталоги, которые представляют Привет наборы данных, которые имеют значение tooothers в вашей организация.</span><span class="sxs-lookup"><span data-stu-id="2351c-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="2351c-130">Регистрация всех файлов и каталогов может загромождать hello каталога, что затрудняет для пользователей toofind необходимые условия.</span><span class="sxs-lookup"><span data-stu-id="2351c-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="2351c-131">Сводка</span><span class="sxs-lookup"><span data-stu-id="2351c-131">Summary</span></span>
<span data-ttu-id="2351c-132">Регистрация источников данных с **каталога данных Azure** делает их проще toodiscover и понять.</span><span class="sxs-lookup"><span data-stu-id="2351c-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="2351c-133">Регистрация и аннотирование hello больших данных файлов и каталогов, которые представляют собой логические наборы данных, можно помочь пользователям находить и использовать hello источников данных большого размера, которые им необходимы.</span><span class="sxs-lookup"><span data-stu-id="2351c-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>
