---
title: "aaaMicrosoft средства моделирования угроз - Azure | Документы Microsoft"
description: "Главная страница для hello Microsoft средства моделирования угроз, содержащий сведения о начале работы со средством hello, включая процесс моделирования угроз hello"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 923225a30c592ffdb1d254000451cfaac54a0e68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="6c14e-103">Средство моделирования угроз Microsoft</span><span class="sxs-lookup"><span data-stu-id="6c14e-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="6c14e-104">Hello средства моделирования угроз является ключевым элементом hello Microsoft Security Development Lifecycle (SDL).</span><span class="sxs-lookup"><span data-stu-id="6c14e-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="6c14e-105">Он позволяет программному обеспечению разработкой tooidentify и избежать потенциальных проблем безопасности рано, по мере относительно легко и экономически эффективная tooresolve.</span><span class="sxs-lookup"><span data-stu-id="6c14e-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="6c14e-106">В результате он значительно уменьшает общую стоимость разработки hello.</span><span class="sxs-lookup"><span data-stu-id="6c14e-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="6c14e-107">Кроме того мы разработали средство hello со специалистами незащищенной помните, упрощая моделирование угроз для всех разработчиков, предоставляя четкие инструкции по созданию и анализ модели угроз.</span><span class="sxs-lookup"><span data-stu-id="6c14e-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="6c14e-108">Средство Hello позволяет:</span><span class="sxs-lookup"><span data-stu-id="6c14e-108">hello tool enables anyone to:</span></span>

* <span data-ttu-id="6c14e-109">Обмен данными о hello разработки безопасности системы</span><span class="sxs-lookup"><span data-stu-id="6c14e-109">Communicate about hello security design of their systems</span></span>
* <span data-ttu-id="6c14e-110">Анализ этих решений на предмет потенциальных проблем безопасности с помощью проверенных методов.</span><span class="sxs-lookup"><span data-stu-id="6c14e-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="6c14e-111">Рекомендации по анализу проблем, связанных с безопасностью, и методы их устранения</span><span class="sxs-lookup"><span data-stu-id="6c14e-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="6c14e-112">Вот некоторые возможности средств и принципиально новые функциональные возможности, просто tooname некоторые из них:</span><span class="sxs-lookup"><span data-stu-id="6c14e-112">Here are some tooling capabilities and innovations, just tooname a few:</span></span>

* <span data-ttu-id="6c14e-113">**Автоматизация** — рекомендации и отзывы о создании модели.</span><span class="sxs-lookup"><span data-stu-id="6c14e-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="6c14e-114">**STRIDE по элементам** — интерактивный анализ угроз и их устранение.</span><span class="sxs-lookup"><span data-stu-id="6c14e-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="6c14e-115">**Отчетов:** действия безопасности и проверки в стадии проверки hello</span><span class="sxs-lookup"><span data-stu-id="6c14e-115">**Reporting:** Security activities and testing in hello verification phase</span></span>
* <span data-ttu-id="6c14e-116">**Уникальный методологии:** toobetter пользователей позволяет визуализировать и понять угроз</span><span class="sxs-lookup"><span data-stu-id="6c14e-116">**Unique Methodology:** Enables users toobetter visualize and understand threats</span></span>
* <span data-ttu-id="6c14e-117">**Спроектированное для разработчиков с упором на защиту программного обеспечения** — разные подходы по работе с активами или злоумышленниками.</span><span class="sxs-lookup"><span data-stu-id="6c14e-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="6c14e-118">Мы всегда ставим во главу угла программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="6c14e-118">We are centered on software.</span></span> <span data-ttu-id="6c14e-119">Мы опираемся на действия, знакомые всем разработчикам и архитекторам: рисование изображений при проектировании архитектуры программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="6c14e-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="6c14e-120">**Анализ проектирования основное внимание уделено:** hello термин «моделирование угроз» может ссылаться tooeither требований или метод анализа разработки.</span><span class="sxs-lookup"><span data-stu-id="6c14e-120">**Focused on Design Analysis:** hello term "threat modeling" can refer tooeither a requirements or a design analysis technique.</span></span> <span data-ttu-id="6c14e-121">В некоторых случаях он ссылается tooa сложные комбинации двух hello.</span><span class="sxs-lookup"><span data-stu-id="6c14e-121">Sometimes, it refers tooa complex blend of hello two.</span></span> <span data-ttu-id="6c14e-122">моделирования toothreat подход Microsoft SDL Hello методика анализа разработки с фокусом ввода</span><span class="sxs-lookup"><span data-stu-id="6c14e-122">hello Microsoft SDL approach toothreat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c14e-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6c14e-123">Next steps</span></span>

<span data-ttu-id="6c14e-124">в следующей таблице Hello содержит tooget важных ссылок, в которой была начата hello средства моделирования угроз:</span><span class="sxs-lookup"><span data-stu-id="6c14e-124">hello table below contains important links tooget you started with hello Threat Modeling Tool:</span></span>

| <span data-ttu-id="6c14e-125">Шаг</span><span class="sxs-lookup"><span data-stu-id="6c14e-125">Step</span></span>  | <span data-ttu-id="6c14e-126">Описание</span><span class="sxs-lookup"><span data-stu-id="6c14e-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="6c14e-127">**1**</span><span class="sxs-lookup"><span data-stu-id="6c14e-127">**1**</span></span> | [<span data-ttu-id="6c14e-128">Загрузите средства моделирования угроз hello</span><span class="sxs-lookup"><span data-stu-id="6c14e-128">Download hello Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="6c14e-129">**2**</span><span class="sxs-lookup"><span data-stu-id="6c14e-129">**2**</span></span> | [<span data-ttu-id="6c14e-130">Руководство по началу работы</span><span class="sxs-lookup"><span data-stu-id="6c14e-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="6c14e-131">**3**</span><span class="sxs-lookup"><span data-stu-id="6c14e-131">**3**</span></span> | [<span data-ttu-id="6c14e-132">Ознакомьтесь с возможностями hello</span><span class="sxs-lookup"><span data-stu-id="6c14e-132">Get familiar with hello features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="6c14e-133">**4**</span><span class="sxs-lookup"><span data-stu-id="6c14e-133">**4**</span></span> | [<span data-ttu-id="6c14e-134">Дополнительные сведения о категориях создаваемых угроз</span><span class="sxs-lookup"><span data-stu-id="6c14e-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="6c14e-135">**5**</span><span class="sxs-lookup"><span data-stu-id="6c14e-135">**5**</span></span> | [<span data-ttu-id="6c14e-136">Найти возможные способы устранения угрозы toogenerated</span><span class="sxs-lookup"><span data-stu-id="6c14e-136">Find mitigations toogenerated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="6c14e-137">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="6c14e-137">Resources</span></span>

<span data-ttu-id="6c14e-138">Ниже приведены несколько старых статей актуальны toothreat моделирования сегодня.</span><span class="sxs-lookup"><span data-stu-id="6c14e-138">Here are a few older articles still relevant toothreat modeling today:</span></span>

* [<span data-ttu-id="6c14e-139">Статья на важность угроз моделирования hello</span><span class="sxs-lookup"><span data-stu-id="6c14e-139">Article on hello Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="6c14e-140">Курс обучения по защищенным информационным системам</span><span class="sxs-lookup"><span data-stu-id="6c14e-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="6c14e-141">Ознакомьтесь с ресурсами, предоставленными разработчиками средства моделирования угроз:</span><span class="sxs-lookup"><span data-stu-id="6c14e-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="6c14e-142">Диспетчер угроз</span><span class="sxs-lookup"><span data-stu-id="6c14e-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="6c14e-143">Блог, посвященный решениям для обеспечения безопасности (автор — Симоне Курзи (Simone Curzi)</span><span class="sxs-lookup"><span data-stu-id="6c14e-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)