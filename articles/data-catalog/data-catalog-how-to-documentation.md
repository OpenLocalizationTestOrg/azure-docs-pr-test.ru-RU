---
title: "Источники данных toodocument aaaHow | Документы Microsoft"
description: "Выделение как tooarticle как toodocument ресурсов данных в каталоге данных Azure."
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
ms.openlocfilehash: 4e46838d91ab4d0c0bc569ac526a0c729134bb10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="a77bb-103">Создание документации по источникам данных</span><span class="sxs-lookup"><span data-stu-id="a77bb-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="a77bb-104">Введение</span><span class="sxs-lookup"><span data-stu-id="a77bb-104">Introduction</span></span>
<span data-ttu-id="a77bb-105">**Каталог данных Microsoft Azure** — это полностью управляемая облачная служба, выполняющая функции систем регистрации и обнаружения корпоративных источников данных.</span><span class="sxs-lookup"><span data-stu-id="a77bb-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="a77bb-106">Другими словами **каталога данных Azure** все сводится к помогает обнаруживать, людям *понять*и использовать источники данных и помогает организациям tooget несколько значений из существующих данных.</span><span class="sxs-lookup"><span data-stu-id="a77bb-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations tooget more value from their existing data.</span></span>

<span data-ttu-id="a77bb-107">При регистрации источника данных с **каталога данных Azure**, его метаданные копируются и службой hello, но История hello не ограничивается не существует.</span><span class="sxs-lookup"><span data-stu-id="a77bb-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span> <span data-ttu-id="a77bb-108">**Каталог данных Azure** также позволяет пользователям tooprovide собственные полную документацию, описывающую использования hello и типичные сценарии для источника данных hello.</span><span class="sxs-lookup"><span data-stu-id="a77bb-108">**Azure Data Catalog** also allows users tooprovide their own complete documentation that can describe hello usage and common scenarios for hello data source.</span></span>

<span data-ttu-id="a77bb-109">В [как источники данных tooannotate](data-catalog-how-to-annotate.md), вы узнаете, что специалисты, которые знать hello источника данных можно аннотировать с тегами и описание.</span><span class="sxs-lookup"><span data-stu-id="a77bb-109">In [How tooannotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know hello data source can annotate it with tags and a description.</span></span> <span data-ttu-id="a77bb-110">Hello **каталога данных Azure** портал включает редактор форматированного текста, чтобы пользователи полностью выполнять Документирование ресурсов данных и контейнеры.</span><span class="sxs-lookup"><span data-stu-id="a77bb-110">hello **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="a77bb-111">Редактор Hello содержит абзаца форматирования, такие как заголовки, форматирование текста, маркированные списки, нумерованные списки и таблицы.</span><span class="sxs-lookup"><span data-stu-id="a77bb-111">hello editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="a77bb-112">Теги и описания прекрасно подходят для простых заметок.</span><span class="sxs-lookup"><span data-stu-id="a77bb-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="a77bb-113">Тем не менее потребители данных toohelp лучше понять использование hello источника данных и бизнес-сценариев для источника данных, специалист может содержать полные, подробных документацию.</span><span class="sxs-lookup"><span data-stu-id="a77bb-113">However, toohelp data consumers better understand hello use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="a77bb-114">Это легко toodocument источника данных.</span><span class="sxs-lookup"><span data-stu-id="a77bb-114">It's easy toodocument a data source.</span></span> <span data-ttu-id="a77bb-115">Выберите ресурс данных или контейнер и щелкните **Документация**.</span><span class="sxs-lookup"><span data-stu-id="a77bb-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="a77bb-116">Создание документации по ресурсам данных</span><span class="sxs-lookup"><span data-stu-id="a77bb-116">Documenting data assets</span></span>
<span data-ttu-id="a77bb-117">Здравствуйте, преимущество **каталога данных Azure** документации позволяет toouse данные каталога как toocreate репозитории содержимого полные описания ресурсов данных.</span><span class="sxs-lookup"><span data-stu-id="a77bb-117">hello benefit of **Azure Data Catalog** documentation allows you toouse your Data Catalog as a content repository toocreate a complete narrative of your data assets.</span></span> <span data-ttu-id="a77bb-118">Можно изучать подробные описания контейнеров и таблиц.</span><span class="sxs-lookup"><span data-stu-id="a77bb-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="a77bb-119">Если уже имеется содержимое в другой репозиторий содержимого, например, SharePoint или общей папки, можно добавить toohello активов документации ссылки tooreference это существующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="a77bb-119">If you already have content in another content repository, such as SharePoint or a file share, you can add toohello asset documentation links tooreference this existing content.</span></span> <span data-ttu-id="a77bb-120">Эта возможность облегчает поиск существующих документов.</span><span class="sxs-lookup"><span data-stu-id="a77bb-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="a77bb-121">Документация не включена в индекс поиска.</span><span class="sxs-lookup"><span data-stu-id="a77bb-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="a77bb-122">Hello уровень документации может находиться в диапазоне от описания характеристик hello и значение данных активов контейнера tooa подробное описание схемы таблицы в контейнере.</span><span class="sxs-lookup"><span data-stu-id="a77bb-122">hello level of documentation can range from describing hello characteristics and value of a data asset container tooa detailed description of table schema within a container.</span></span> <span data-ttu-id="a77bb-123">уровень Hello документации, предоставленной должны управляться потребностям бизнеса.</span><span class="sxs-lookup"><span data-stu-id="a77bb-123">hello level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="a77bb-124">Создание документации по ресурсам данных сопряжено с такими основными преимуществами и недостатками.</span><span class="sxs-lookup"><span data-stu-id="a77bb-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="a77bb-125">Документ является контейнером: все содержимое hello в одном месте, но возможно отсутствие необходимости сведения для пользователей toomake обоснованное решение.</span><span class="sxs-lookup"><span data-stu-id="a77bb-125">Document just a container: All hello content is in one place, but might lack necessary details for users toomake an informed decision.</span></span>
* <span data-ttu-id="a77bb-126">Документ только таблиц hello: содержимого конкретных toothat объект, однако у пользователей есть несколько расположений для документов.</span><span class="sxs-lookup"><span data-stu-id="a77bb-126">Document just hello tables: Content is specific toothat object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="a77bb-127">Документов контейнеров и таблиц: наиболее комплексный подход, но может внести дополнительные обслуживания hello документов.</span><span class="sxs-lookup"><span data-stu-id="a77bb-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of hello documents.</span></span>

## <a name="summary"></a><span data-ttu-id="a77bb-128">Сводка</span><span class="sxs-lookup"><span data-stu-id="a77bb-128">Summary</span></span>
<span data-ttu-id="a77bb-129">Создавая документацию по источникам данных с помощью **каталога данных Azure** , можно описать свои ресурсы данных максимально подробно.</span><span class="sxs-lookup"><span data-stu-id="a77bb-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="a77bb-130">С помощью ссылки, можно связать toocontent, хранящихся в существующего содержимого репозитория, где собраны вместе на существующих документов и ресурсов данных.</span><span class="sxs-lookup"><span data-stu-id="a77bb-130">By using links, you can link toocontent stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="a77bb-131">А ваши пользователи, обнаружив определенные ресурсы данных, могут пользоваться полным набором документации.</span><span class="sxs-lookup"><span data-stu-id="a77bb-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
