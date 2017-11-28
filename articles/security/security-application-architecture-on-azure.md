---
title: "aaaIntegrate безопасности в Azure архитектур | Документы Microsoft"
description: " В этой статье помогут понять hello архитектуры приложения и служб для Azure toomake его проще toointegrate безопасности в разработке и реализации. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 4f2d9386-bda3-4ec8-8b1a-cd0c11242ffc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: cfca8a1a2766f72bc3340c4e3df0019eb8b5a1e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-on-azure"></a><span data-ttu-id="1eee6-103">Архитектура приложения в Azure</span><span class="sxs-lookup"><span data-stu-id="1eee6-103">Application architecture on Azure</span></span>
<span data-ttu-id="1eee6-104">toohelp защиты вашей облачных решений на базе Microsoft Azure важно надежный фундамент архитектуры.</span><span class="sxs-lookup"><span data-stu-id="1eee6-104">toohelp secure your cloud-based solutions on Microsoft Azure, a strong architectural foundation is critical.</span></span> <span data-ttu-id="1eee6-105">Глубокое понимание архитектуры приложений и служб обеспечит серьезные преимущества архитекторам, проектировщикам и разработчикам программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="1eee6-105">Architects, designers, and implementers all benefit from a strong knowledge of application and services architecture.</span></span> <span data-ttu-id="1eee6-106">Эти базовые знания помогают понять все компоненты hello облачных решений и сделать его проще toointegrate безопасности всех аспектов проектирования и реализации.</span><span class="sxs-lookup"><span data-stu-id="1eee6-106">This foundational knowledge helps you understand all hello components of your cloud-based solutions and make it easier toointegrate security into all aspects of your design and implementation.</span></span>

<span data-ttu-id="1eee6-107">Мы имеют hello следующие toohelp можно с помощью архитектуры исследования и схемы:</span><span class="sxs-lookup"><span data-stu-id="1eee6-107">We have hello following toohelp you with your architectural investigations and designs:</span></span>

* <span data-ttu-id="1eee6-108">инфографика по архитектурам;</span><span class="sxs-lookup"><span data-stu-id="1eee6-108">Architectural infographics</span></span>
* <span data-ttu-id="1eee6-109">проекты архитектуры;</span><span class="sxs-lookup"><span data-stu-id="1eee6-109">Architectural blueprints</span></span>
* <span data-ttu-id="1eee6-110">облачный и корпоративный набор символов;</span><span class="sxs-lookup"><span data-stu-id="1eee6-110">Cloud and enterprise symbol set</span></span>
* <span data-ttu-id="1eee6-111">шаблон трехмерных проектов Visio.</span><span class="sxs-lookup"><span data-stu-id="1eee6-111">3D blueprint Visio template</span></span>

## <a name="architectural-infographics"></a><span data-ttu-id="1eee6-112">инфографика по архитектурам;</span><span class="sxs-lookup"><span data-stu-id="1eee6-112">Architectural infographics</span></span>
<span data-ttu-id="1eee6-113">Корпорация Майкрософт опубликовала несколько постеров и инфографических материалов на тему проектирования архитектуры.</span><span class="sxs-lookup"><span data-stu-id="1eee6-113">Microsoft publishes several architectural related posters/infographics.</span></span> <span data-ttu-id="1eee6-114">К ним относятся следующие:</span><span class="sxs-lookup"><span data-stu-id="1eee6-114">They include:</span></span>

* [<span data-ttu-id="1eee6-115">Building Real-World Cloud Applications</span><span class="sxs-lookup"><span data-stu-id="1eee6-115">Building Real-World Cloud Applications</span></span>](https://azure.microsoft.com/documentation/infographics/building-real-world-cloud-apps/)
* [<span data-ttu-id="1eee6-116">Scaling with Cloud Services</span><span class="sxs-lookup"><span data-stu-id="1eee6-116">Scaling with Cloud Services</span></span>](https://azure.microsoft.com/documentation/infographics/cloud-services/)

## <a name="architectural-blueprints"></a><span data-ttu-id="1eee6-117">проекты архитектуры;</span><span class="sxs-lookup"><span data-stu-id="1eee6-117">Architectural blueprints</span></span>
<span data-ttu-id="1eee6-118">Корпорация Майкрософт публикует набор высокого уровня [архитектурных чертежей](http://aka.ms/azblueprints) отображаются как toobuild определенных типов систем, использующих продукты Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1eee6-118">Microsoft publishes a set of high-level [architectural blueprints](http://aka.ms/azblueprints) showing how toobuild specific types of systems using Microsoft products.</span></span>
<span data-ttu-id="1eee6-119">Каждый проект содержит:</span><span class="sxs-lookup"><span data-stu-id="1eee6-119">Each blueprint includes a:</span></span>

* <span data-ttu-id="1eee6-120">двухмерный файл на основе Visio 2003, который можно скачать и изменить;</span><span class="sxs-lookup"><span data-stu-id="1eee6-120">Flat 2D Visio 2003-based file that you can download and modify</span></span>
* <span data-ttu-id="1eee6-121">Цветные объемной перспективы PDF файла toointroduce hello чертежом сборки technical аудитории</span><span class="sxs-lookup"><span data-stu-id="1eee6-121">Colorful 3D perspective PDF file toointroduce hello blueprint tooless technical audiences</span></span>
* <span data-ttu-id="1eee6-122">Видео, которое проведет вас через hello 3D версии</span><span class="sxs-lookup"><span data-stu-id="1eee6-122">Video that walks through hello 3D version</span></span>

## <a name="cloud-and-enterprise-symbol-set"></a><span data-ttu-id="1eee6-123">облачный и корпоративный набор символов;</span><span class="sxs-lookup"><span data-stu-id="1eee6-123">Cloud and enterprise symbol set</span></span>
<span data-ttu-id="1eee6-124">[Просмотр hello Visio и обучающие видео символы](http://aka.ms/CnESymbolsVideo) и затем [загрузить набор облака и корпоративного символа hello](http://aka.ms/CnESymbols) toohelp создания технических материалов, которые описывают Azure, Windows Server, SQL Server и многое другое.</span><span class="sxs-lookup"><span data-stu-id="1eee6-124">[View hello Visio and symbols training video](http://aka.ms/CnESymbolsVideo) and then [download hello Cloud and Enterprise Symbol set](http://aka.ms/CnESymbols) toohelp create technical materials that describe Azure, Windows Server, SQL Server and more.</span></span> <span data-ttu-id="1eee6-125">Символы hello в схемах архитектуры, учебные материалы, презентации, таблицы, плакатов, технические документы и даже сторонних книг можно использовать, если серий книги hello люди toouse продуктов корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="1eee6-125">You can use hello symbols in architecture diagrams, training materials, presentations, datasheets, infographics, whitepapers, and even third party books if hello book trains people toouse Microsoft products.</span></span> <span data-ttu-id="1eee6-126">Однако они не предназначены для применения в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="1eee6-126">However, they are not meant for use in user interfaces.</span></span>

## <a name="3d-blueprint-visio-template"></a><span data-ttu-id="1eee6-127">шаблон трехмерных проектов Visio.</span><span class="sxs-lookup"><span data-stu-id="1eee6-127">3D blueprint Visio template</span></span>
<span data-ttu-id="1eee6-128">Здравствуйте 3D версии hello [проекты архитектуры Майкрософт](http://aka.ms/azblueprints) изначально были созданы с помощью средства сторонних производителей.</span><span class="sxs-lookup"><span data-stu-id="1eee6-128">hello 3D versions of hello [Microsoft Architecture Blueprints](http://aka.ms/azblueprints) were initially created in a non-Microsoft tool.</span></span> <span data-ttu-id="1eee6-129">Новый шаблон для Visio 2013 (и более поздних версий) был выпущен 5 августа 2015 года для [аттестационного курса по архитектуре Майкрософт, распространяемого на сайте EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span><span class="sxs-lookup"><span data-stu-id="1eee6-129">A new Visio 2013 (and later) template shipped on August 5, 2015 as part of a [Microsoft Architecture certification course distributed on EDX.ORG](https://docs.microsoft.com/azure/architecture/#microsoft-architecture-certification-course).</span></span>

<span data-ttu-id="1eee6-130">шаблон Hello также доступен вне hello курса.</span><span class="sxs-lookup"><span data-stu-id="1eee6-130">hello template is also available outside hello course.</span></span>

* <span data-ttu-id="1eee6-131">[Просмотреть видео обучения hello](http://aka.ms/3dBlueprintTemplateVideo) первым, чтобы знать, что можно делать</span><span class="sxs-lookup"><span data-stu-id="1eee6-131">[View hello training video](http://aka.ms/3dBlueprintTemplateVideo) first so you know what it can do</span></span>
* <span data-ttu-id="1eee6-132">Загрузите hello [Microsoft 3d шаблоне Visio план](http://aka.ms/3DBlueprintTemplate)</span><span class="sxs-lookup"><span data-stu-id="1eee6-132">Download hello [Microsoft 3d Blueprint Visio Template](http://aka.ms/3DBlueprintTemplate)</span></span>
* <span data-ttu-id="1eee6-133">Загрузите hello [облака и корпоративного символы](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse 3D шаблоном hello</span><span class="sxs-lookup"><span data-stu-id="1eee6-133">Download hello [Cloud and Enterprise Symbols](https://docs.microsoft.com/azure/architecture/#drawing-symbol-and-icon-sets) toouse with hello 3D template</span></span>
