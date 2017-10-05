---
title: "Создание документации по источникам данных | Документация Майкрософт"
description: "Эта статья представляет собой практическое руководство, в котором объяснено, как создать документацию по ресурсам данных в каталоге данных Azure."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: ffe951f60afb57524568fe1ed3b3668d0088e124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="ff255-103">Создание документации по источникам данных</span><span class="sxs-lookup"><span data-stu-id="ff255-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="ff255-104">Введение</span><span class="sxs-lookup"><span data-stu-id="ff255-104">Introduction</span></span>
<span data-ttu-id="ff255-105">**Каталог данных Microsoft Azure** — это полностью управляемая облачная служба, выполняющая функции систем регистрации и обнаружения корпоративных источников данных.</span><span class="sxs-lookup"><span data-stu-id="ff255-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="ff255-106">Проще говоря, **каталог данных Azure** помогает пользователям находить, *оценивать*и использовать источники данных, что, в свою очередь, повышает для организаций ценность существующей информации.</span><span class="sxs-lookup"><span data-stu-id="ff255-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="ff255-107">Если источник данных зарегистрирован в **каталоге данных Azure**, его метаданные копируются и индексируются службой, но на этом работа с ними не заканчивается.</span><span class="sxs-lookup"><span data-stu-id="ff255-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="ff255-108">**Каталог данных Azure** позволяет пользователям также предоставлять их собственную полную документацию, в которой описаны использование и стандартные сценарии, предназначенные для источника данных.</span><span class="sxs-lookup"><span data-stu-id="ff255-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="ff255-109">Из статьи о [создании заметок к источникам данных](data-catalog-how-to-annotate.md)вы можете узнать, что специалисты, владеющие информацией об источнике данных, могут добавлять к нему теги и описания.</span><span class="sxs-lookup"><span data-stu-id="ff255-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="ff255-110">Портал **каталога данных Azure** содержит текстовый редактор, с помощью которого пользователи могут документировать ресурсы и контейнеры данных.</span><span class="sxs-lookup"><span data-stu-id="ff255-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="ff255-111">Редактор предусматривает возможности форматирования, включая работу с заголовками, маркированными списками, нумерованными списками и таблицами, а также форматированием текста.</span><span class="sxs-lookup"><span data-stu-id="ff255-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="ff255-112">Теги и описания прекрасно подходят для простых заметок.</span><span class="sxs-lookup"><span data-stu-id="ff255-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="ff255-113">Но чтобы пользователи могли соотнести бизнес-сценарии с имеющимися источниками данных, а также оценили возможности использования этих источников, специалисты могут предоставить исчерпывающую документацию.</span><span class="sxs-lookup"><span data-stu-id="ff255-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="ff255-114">Создать документацию по источнику данных легко.</span><span class="sxs-lookup"><span data-stu-id="ff255-114">It's easy to document a data source.</span></span> <span data-ttu-id="ff255-115">Выберите ресурс данных или контейнер и щелкните **Документация**.</span><span class="sxs-lookup"><span data-stu-id="ff255-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="ff255-116">Создание документации по ресурсам данных</span><span class="sxs-lookup"><span data-stu-id="ff255-116">Documenting data assets</span></span>
<span data-ttu-id="ff255-117">Вы можете использовать документацию **каталога данных Azure** в качестве репозитория содержимого, создавая с его помощью полное описание ресурсов данных.</span><span class="sxs-lookup"><span data-stu-id="ff255-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="ff255-118">Можно изучать подробные описания контейнеров и таблиц.</span><span class="sxs-lookup"><span data-stu-id="ff255-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="ff255-119">Если у вас уже есть содержимое в другом репозитории содержимого, например в SharePoint или общей папке, вы можете добавить ссылки на это содержимое в документацию по ресурсу.</span><span class="sxs-lookup"><span data-stu-id="ff255-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="ff255-120">Эта возможность облегчает поиск существующих документов.</span><span class="sxs-lookup"><span data-stu-id="ff255-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="ff255-121">Документация не включена в индекс поиска.</span><span class="sxs-lookup"><span data-stu-id="ff255-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="ff255-122">Уровень документации может быть разным: от описания характеристик и значений контейнера ресурса данных до подробного описания схемы таблицы, которую содержит контейнер.</span><span class="sxs-lookup"><span data-stu-id="ff255-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="ff255-123">Уровень документации следует выбирать с учетом ваших бизнес-потребностей.</span><span class="sxs-lookup"><span data-stu-id="ff255-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="ff255-124">Создание документации по ресурсам данных сопряжено с такими основными преимуществами и недостатками.</span><span class="sxs-lookup"><span data-stu-id="ff255-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="ff255-125">Документация только по контейнеру: все содержимое находится в одном расположении, но содержимое может быть недостаточно подробным, следовательно, некоторые пользователи не смогут принять обоснованные решения.</span><span class="sxs-lookup"><span data-stu-id="ff255-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="ff255-126">Документация только по таблицам: содержимое описывает конкретный объект, но документы находятся в нескольких расположениях.</span><span class="sxs-lookup"><span data-stu-id="ff255-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="ff255-127">Документация по контейнерам и таблицам: комплексный подход, который не исключает необходимость дополнительной работы с документами.</span><span class="sxs-lookup"><span data-stu-id="ff255-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="ff255-128">Сводка</span><span class="sxs-lookup"><span data-stu-id="ff255-128">Summary</span></span>
<span data-ttu-id="ff255-129">Создавая документацию по источникам данных с помощью **каталога данных Azure** , можно описать свои ресурсы данных максимально подробно.</span><span class="sxs-lookup"><span data-stu-id="ff255-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="ff255-130">Вы можете добавить ссылки на существующий репозиторий содержимого, чтобы использовать уже имеющиеся документы и ресурсы данных.</span><span class="sxs-lookup"><span data-stu-id="ff255-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="ff255-131">А ваши пользователи, обнаружив определенные ресурсы данных, могут пользоваться полным набором документации.</span><span class="sxs-lookup"><span data-stu-id="ff255-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
