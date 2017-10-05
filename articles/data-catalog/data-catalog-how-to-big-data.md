---
title: "Как работать с источниками больших данных | Документация Майкрософт"
description: "Статья, описывающая подходы к использованию каталога данных Azure при работе с источниками больших данных, в том числе с хранилищем BLOB-объектов Azure, озером данных Azure и Hadoop HDFS."
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
ms.openlocfilehash: 001d80ce42f0e87276e59d70dffb75eb561d96cd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-work-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="11700-103">Работа с источниками больших данных в каталоге данных Azure</span><span class="sxs-lookup"><span data-stu-id="11700-103">How to work with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="11700-104">Введение</span><span class="sxs-lookup"><span data-stu-id="11700-104">Introduction</span></span>
<span data-ttu-id="11700-105">**Каталог данных Microsoft Azure** — это полностью управляемая облачная служба, выполняющая функции систем регистрации и обнаружения корпоративных источников данных.</span><span class="sxs-lookup"><span data-stu-id="11700-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="11700-106">Он помогает пользователям обнаруживать, оценивать и использовать источники данных, повышая ценность источников информации, в том числе источников больших данных, для организаций.</span><span class="sxs-lookup"><span data-stu-id="11700-106">It is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="11700-107">**Каталог данных Azure** поддерживает регистрацию больших двоичных объектов и каталогов хранилища BLOB-объектов Azure, а также файлов и каталогов Hadoop HDFS.</span><span class="sxs-lookup"><span data-stu-id="11700-107">**Azure Data Catalog** supports the registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="11700-108">Эти источники данных являются частично структурированными, что обеспечивает большую гибкость.</span><span class="sxs-lookup"><span data-stu-id="11700-108">The semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="11700-109">Однако это также означает, что для получения максимальной пользы от регистрации источников в **каталоге данных Azure** пользователям необходимо понимать и учитывать их структуру.</span><span class="sxs-lookup"><span data-stu-id="11700-109">However, to get the most value from registering them with **Azure Data Catalog**, users must consider how the data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="11700-110">Каталоги как логические наборы данных</span><span class="sxs-lookup"><span data-stu-id="11700-110">Directories as logical data sets</span></span>
<span data-ttu-id="11700-111">Наиболее общий подход к организации источников больших данных — использование каталогов в качестве логических наборов данных.</span><span class="sxs-lookup"><span data-stu-id="11700-111">A common pattern for organizing big data sources is to treat directories as logical data sets.</span></span> <span data-ttu-id="11700-112">Каталоги верхнего уровня определяют наборы данных, вложенные папки определяют разделы, а файлы в них хранят сами данные.</span><span class="sxs-lookup"><span data-stu-id="11700-112">Top-level directories are used to define a data set, while subfolders define partitions, and the files they contain store the data itself.</span></span>

<span data-ttu-id="11700-113">Пример такого подхода:</span><span class="sxs-lookup"><span data-stu-id="11700-113">An example of this pattern might be:</span></span>

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

<span data-ttu-id="11700-114">В этом примере vehicle_maintenance_events и location_tracking_events представляют логические наборы данных.</span><span class="sxs-lookup"><span data-stu-id="11700-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="11700-115">Каждая из этих папок содержит файлы данных, разделенные на вложенные папки по году и месяцу.</span><span class="sxs-lookup"><span data-stu-id="11700-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="11700-116">Каждая из вложенных папок может содержать сотни и тысячи файлов.</span><span class="sxs-lookup"><span data-stu-id="11700-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="11700-117">При таком подходе регистрация отдельных файлов в **каталоге данных Azure** не имеет смысла.</span><span class="sxs-lookup"><span data-stu-id="11700-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="11700-118">Вместо этого следует регистрировать каталоги, представляющие наборы данных, которые будут полезны пользователям, работающим с данными.</span><span class="sxs-lookup"><span data-stu-id="11700-118">Instead, register the directories that represent the data sets that be meaningful to the users working with the data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="11700-119">Справочные файлы данных</span><span class="sxs-lookup"><span data-stu-id="11700-119">Reference data files</span></span>
<span data-ttu-id="11700-120">Другой подход представляет собой хранение справочных наборов данных в качестве отдельных файлов.</span><span class="sxs-lookup"><span data-stu-id="11700-120">A complementary pattern is to store reference data sets as individual files.</span></span> <span data-ttu-id="11700-121">Эти наборы данных можно рассматривать как малую часть больших данных. Они зачастую напоминают измерения в аналитической модели данных.</span><span class="sxs-lookup"><span data-stu-id="11700-121">These data sets may be thought of as the 'small' side of big data, and are often similar to dimensions in an analytical data model.</span></span> <span data-ttu-id="11700-122">Справочные файлы данных содержат записи, используемые в качестве контекста для основного массива файлов в хранилище больших данных.</span><span class="sxs-lookup"><span data-stu-id="11700-122">Reference data files contain records that are used to provide context for the bulk of the data files stored elsewhere in the big data store.</span></span>

<span data-ttu-id="11700-123">Пример такого подхода:</span><span class="sxs-lookup"><span data-stu-id="11700-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="11700-124">Специалисту по анализу и обработке данных, который работает с данными в каталогах со сложной структурой, данные в справочных файлах могут помочь получить более подробную информацию о сущностях, которые упоминаются в больших наборах данных только по имени или идентификатору.</span><span class="sxs-lookup"><span data-stu-id="11700-124">When an analyst or data scientist is working with the data contained in the larger directory structures, the data in these reference files can be used to provide more detailed information for entities that are referred to only by name or ID in the larger data set.</span></span>

<span data-ttu-id="11700-125">В этом случае имеет смысл зарегистрировать в **каталоге данных Azure** отдельные справочные файлы данных.</span><span class="sxs-lookup"><span data-stu-id="11700-125">In this pattern, it makes sense to register the individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="11700-126">Каждый файл представляет набор данных и может быть аннотирован и обнаружен независимо от других файлов.</span><span class="sxs-lookup"><span data-stu-id="11700-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="11700-127">Альтернативные подходы</span><span class="sxs-lookup"><span data-stu-id="11700-127">Alternate patterns</span></span>
<span data-ttu-id="11700-128">В подразделе выше описаны два возможных способа упорядочения больших объемов данных в хранилище, однако их реализация отличается в каждом конкретном случае.</span><span class="sxs-lookup"><span data-stu-id="11700-128">The patterns described in the preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="11700-129">Независимо от структуры источников больших данных регистрировать в **каталоге данных Azure** следует те файлы и папки, представляющие наборы данных, которые будут полезны другим пользователям в организации.</span><span class="sxs-lookup"><span data-stu-id="11700-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering the files and directories that represent the data sets that are of value to others within your organization.</span></span> <span data-ttu-id="11700-130">Регистрация всех файлов и папок может перегрузить каталог и затруднить поиск нужных данных.</span><span class="sxs-lookup"><span data-stu-id="11700-130">Registering all files and directories can clutter the catalog, making it harder for users to find what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="11700-131">Сводка</span><span class="sxs-lookup"><span data-stu-id="11700-131">Summary</span></span>
<span data-ttu-id="11700-132">Регистрация источников данных в **каталоге данных Azure** упрощает их поиск и интерпретацию.</span><span class="sxs-lookup"><span data-stu-id="11700-132">Registering data sources with **Azure Data Catalog** makes them easier to discover and understand.</span></span> <span data-ttu-id="11700-133">Регистрация и аннотирование файлов и каталогов, содержащих большие объемы данных и представляющих логические наборы данных, помогают пользователям находить и использовать необходимую информацию в источниках больших данных.</span><span class="sxs-lookup"><span data-stu-id="11700-133">By registering and annotating the big data files and directories that represent logical data sets, you can help users find and use the big data sources they need.</span></span>
