---
title: "Средство моделирования угроз Microsoft Azure | Документация Майкрософт"
description: "Главная страница средства моделирования угроз Майкрософт, содержащая сведения о начале работы с помощью средства, в том числе процесс моделирования угроз"
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
ms.openlocfilehash: 6e26b0af2a16a872c8e02b736e24019b47ed5780
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="a8486-103">Средство моделирования угроз Microsoft</span><span class="sxs-lookup"><span data-stu-id="a8486-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="a8486-104">Средство моделирования угроз — это основной элемент жизненного цикла разработки защищенных приложений (Майкрософт) (SDL)</span><span class="sxs-lookup"><span data-stu-id="a8486-104">The Threat Modeling Tool is a core element of the Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="a8486-105">Он позволяет архитекторам ПО на ранних этапах выявлять и устранять потенциальные проблемы, связанные с безопасностью, когда их еще можно относительно легко и без особых затрат устранить.</span><span class="sxs-lookup"><span data-stu-id="a8486-105">It allows software architects to identify and mitigate potential security issues early, when they are relatively easy and cost-effective to resolve.</span></span> <span data-ttu-id="a8486-106">В результате это средство значительно снижает стоимость разработки.</span><span class="sxs-lookup"><span data-stu-id="a8486-106">As a result, it greatly reduces the total cost of development.</span></span> <span data-ttu-id="a8486-107">Кроме того, при проектировании этого средства учитывались потребности специалистов, не связанных со сферой безопасности. С его помощью все разработчики могут легко моделировать угрозы благодаря четкому руководству по созданию и анализу моделей угроз.</span><span class="sxs-lookup"><span data-stu-id="a8486-107">Also, we designed the tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="a8486-108">Это средство предоставляет пользователям следующие возможности.</span><span class="sxs-lookup"><span data-stu-id="a8486-108">The tool enables anyone to:</span></span>

* <span data-ttu-id="a8486-109">Обмен данными о разработке решений для обеспечения безопасности своих систем.</span><span class="sxs-lookup"><span data-stu-id="a8486-109">Communicate about the security design of their systems</span></span>
* <span data-ttu-id="a8486-110">Анализ этих решений на предмет потенциальных проблем безопасности с помощью проверенных методов.</span><span class="sxs-lookup"><span data-stu-id="a8486-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="a8486-111">Рекомендации по анализу проблем, связанных с безопасностью, и методы их устранения</span><span class="sxs-lookup"><span data-stu-id="a8486-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="a8486-112">Ниже описаны некоторые из возможностей (включая инновационные) предлагаемого инструментария.</span><span class="sxs-lookup"><span data-stu-id="a8486-112">Here are some tooling capabilities and innovations, just to name a few:</span></span>

* <span data-ttu-id="a8486-113">**Автоматизация** — рекомендации и отзывы о создании модели.</span><span class="sxs-lookup"><span data-stu-id="a8486-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="a8486-114">**STRIDE по элементам** — интерактивный анализ угроз и их устранение.</span><span class="sxs-lookup"><span data-stu-id="a8486-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="a8486-115">**Отчеты** — действия по обеспечению безопасности и тестирование на этапе проверки.</span><span class="sxs-lookup"><span data-stu-id="a8486-115">**Reporting:** Security activities and testing in the verification phase</span></span>
* <span data-ttu-id="a8486-116">**Уникальные методы** — пользователи могут более эффективно визуализировать и оценивать угрозы.</span><span class="sxs-lookup"><span data-stu-id="a8486-116">**Unique Methodology:** Enables users to better visualize and understand threats</span></span>
* <span data-ttu-id="a8486-117">**Спроектированное для разработчиков с упором на защиту программного обеспечения** — разные подходы по работе с активами или злоумышленниками.</span><span class="sxs-lookup"><span data-stu-id="a8486-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="a8486-118">Мы всегда ставим во главу угла программное обеспечение.</span><span class="sxs-lookup"><span data-stu-id="a8486-118">We are centered on software.</span></span> <span data-ttu-id="a8486-119">Мы опираемся на действия, знакомые всем разработчикам и архитекторам: рисование изображений при проектировании архитектуры программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="a8486-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="a8486-120">**Фокус на анализе архитектуры** — термин "моделирование угроз" может означать как требования, так и методику анализа архитектуры.</span><span class="sxs-lookup"><span data-stu-id="a8486-120">**Focused on Design Analysis:** The term "threat modeling" can refer to either a requirements or a design analysis technique.</span></span> <span data-ttu-id="a8486-121">В некоторых случаях он обозначает сложную комбинацию этих двух компонентов.</span><span class="sxs-lookup"><span data-stu-id="a8486-121">Sometimes, it refers to a complex blend of the two.</span></span> <span data-ttu-id="a8486-122">Подход к моделированию угроз Microsoft SDL — это метод с фокусом на анализ архитектуры.</span><span class="sxs-lookup"><span data-stu-id="a8486-122">The Microsoft SDL approach to threat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8486-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8486-123">Next steps</span></span>

<span data-ttu-id="a8486-124">В таблице ниже перечислены важные ссылки, которые помогут вам приступить к работе со средством моделирования угроз:</span><span class="sxs-lookup"><span data-stu-id="a8486-124">The table below contains important links to get you started with the Threat Modeling Tool:</span></span>

| <span data-ttu-id="a8486-125">Шаг</span><span class="sxs-lookup"><span data-stu-id="a8486-125">Step</span></span>  | <span data-ttu-id="a8486-126">Описание</span><span class="sxs-lookup"><span data-stu-id="a8486-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="a8486-127">**1**</span><span class="sxs-lookup"><span data-stu-id="a8486-127">**1**</span></span> | [<span data-ttu-id="a8486-128">Скачивание средства моделирования угроз</span><span class="sxs-lookup"><span data-stu-id="a8486-128">Download the Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="a8486-129">**2**</span><span class="sxs-lookup"><span data-stu-id="a8486-129">**2**</span></span> | [<span data-ttu-id="a8486-130">Руководство по началу работы</span><span class="sxs-lookup"><span data-stu-id="a8486-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="a8486-131">**3**</span><span class="sxs-lookup"><span data-stu-id="a8486-131">**3**</span></span> | [<span data-ttu-id="a8486-132">Общие сведения об этих функциях</span><span class="sxs-lookup"><span data-stu-id="a8486-132">Get familiar with the features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="a8486-133">**4**</span><span class="sxs-lookup"><span data-stu-id="a8486-133">**4**</span></span> | [<span data-ttu-id="a8486-134">Дополнительные сведения о категориях создаваемых угроз</span><span class="sxs-lookup"><span data-stu-id="a8486-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="a8486-135">**5**</span><span class="sxs-lookup"><span data-stu-id="a8486-135">**5**</span></span> | [<span data-ttu-id="a8486-136">Поиск способов устранения рисков для созданных угроз</span><span class="sxs-lookup"><span data-stu-id="a8486-136">Find mitigations to generated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="a8486-137">Ресурсы</span><span class="sxs-lookup"><span data-stu-id="a8486-137">Resources</span></span>

<span data-ttu-id="a8486-138">Ниже приведены несколько старых статей, которые по-прежнему актуальны к моделированию угроз:</span><span class="sxs-lookup"><span data-stu-id="a8486-138">Here are a few older articles still relevant to threat modeling today:</span></span>

* [<span data-ttu-id="a8486-139">Статьи о важности моделирования угроз</span><span class="sxs-lookup"><span data-stu-id="a8486-139">Article on the Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="a8486-140">Курс обучения по защищенным информационным системам</span><span class="sxs-lookup"><span data-stu-id="a8486-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="a8486-141">Ознакомьтесь с ресурсами, предоставленными разработчиками средства моделирования угроз:</span><span class="sxs-lookup"><span data-stu-id="a8486-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="a8486-142">Диспетчер угроз</span><span class="sxs-lookup"><span data-stu-id="a8486-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="a8486-143">Блог, посвященный решениям для обеспечения безопасности (автор — Симоне Курзи (Simone Curzi)</span><span class="sxs-lookup"><span data-stu-id="a8486-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)