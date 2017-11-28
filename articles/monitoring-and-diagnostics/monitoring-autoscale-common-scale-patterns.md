---
title: "aaaOverview общих шаблонов автомасштабирования | Документы Microsoft"
description: "Узнайте, что некоторые распространенные шаблоны tooauto hello масштабировать ресурс в Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="4ccaf-103">Обзор общих шаблонов автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="4ccaf-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="4ccaf-104">В этой статье описаны некоторые распространенные шаблоны tooscale hello ресурс в Azure.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-104">This article describes some of hello common patterns tooscale your resource in Azure.</span></span>

<span data-ttu-id="4ccaf-105">Автоматическое масштабирование Azure монитор применяется только tooVirtual задает масштаб компьютера (VMSS), облачные службы, планах службы приложений и среды службы приложений.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="4ccaf-106">Начало работы</span><span class="sxs-lookup"><span data-stu-id="4ccaf-106">Lets get started</span></span>

<span data-ttu-id="4ccaf-107">В данной статье предполагается, что вы знакомы с автомасштабированием.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="4ccaf-108">Вы можете [получить ресурс работы здесь tooscale][1].</span><span class="sxs-lookup"><span data-stu-id="4ccaf-108">You can [get started here tooscale your resource][1].</span></span> <span data-ttu-id="4ccaf-109">Hello ниже приведены некоторые распространенные шаблоны шкалы hello.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-109">hello following are some of hello common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="4ccaf-110">Масштабирование на основе использования ЦП</span><span class="sxs-lookup"><span data-stu-id="4ccaf-110">Scale based on CPU</span></span>

<span data-ttu-id="4ccaf-111">У вас есть веб-приложение (VMSS или роль облачной службы). Кроме того:</span><span class="sxs-lookup"><span data-stu-id="4ccaf-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="4ccaf-112">Вы хотите tooscale out/шкалы, в зависимости от ЦП.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-112">You want tooscale out/scale in based on CPU.</span></span>
- <span data-ttu-id="4ccaf-113">Кроме того, требуется tooensure имеется минимальное число экземпляров.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-113">Additionally, you want tooensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="4ccaf-114">Кроме того требуется tooensure, toohello максимального количества экземпляров, которыми можно масштабировать до.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-114">Also, you want tooensure that you set a maximum limit toohello number of instances you can scale to.</span></span>

![Масштабирование на основе использования ЦП][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="4ccaf-116">Масштабирование в рабочие и выходные дни</span><span class="sxs-lookup"><span data-stu-id="4ccaf-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="4ccaf-117">У вас есть веб-приложение (VMSS или роль облачной службы). Кроме того:</span><span class="sxs-lookup"><span data-stu-id="4ccaf-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="4ccaf-118">требуется 3 экземпляра по умолчанию (в рабочие дни);</span><span class="sxs-lookup"><span data-stu-id="4ccaf-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="4ccaf-119">Трафик не нужна в выходные и таким образом вы хотите tooscale работу экземпляра too1 на выходные дни.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-119">You don't expect traffic on weekends and hence you want tooscale down too1 instance on weekends.</span></span>

![Масштабирование в рабочие и выходные дни][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="4ccaf-121">Масштабирование в праздничные дни</span><span class="sxs-lookup"><span data-stu-id="4ccaf-121">Scale differently during holidays</span></span>

<span data-ttu-id="4ccaf-122">У вас есть веб-приложение (VMSS или роль облачной службы). Кроме того:</span><span class="sxs-lookup"><span data-stu-id="4ccaf-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="4ccaf-123">Вы хотите tooscale вверх или вниз по умолчанию, основанное на ЦП</span><span class="sxs-lookup"><span data-stu-id="4ccaf-123">You want tooscale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="4ccaf-124">Однако во время праздников (или в определенные дни, которые важны для бизнеса) необходимо toooverride hello значения по умолчанию и имеют больший объем в вашем распоряжении.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-124">However, during holiday season (or specific days that are important for your business) you want toooverride hello defaults and have more capacity at your disposal.</span></span>

![Масштабирование в праздничные дни][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="4ccaf-126">Масштабирование на основе пользовательской метрики</span><span class="sxs-lookup"><span data-stu-id="4ccaf-126">Scale based on custom metric</span></span>

<span data-ttu-id="4ccaf-127">У вас есть веб-интерфейса и уровня API, который взаимодействует с серверной hello.</span><span class="sxs-lookup"><span data-stu-id="4ccaf-127">You have a web front end and a API tier that communicates with hello backend.</span></span> 

- <span data-ttu-id="4ccaf-128">Требуется tooscale hello API уровня на основе пользовательских событий в hello внешнего интерфейса (пример: требуется, чтобы процесс извлечения на основе hello числа элементов в корзину hello tooscale)</span><span class="sxs-lookup"><span data-stu-id="4ccaf-128">You want tooscale hello API tier based on custom events in hello front end (example: You want tooscale your checkout process based on hello number of items in hello shopping cart)</span></span>

![Масштабирование на основе пользовательской метрики][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png