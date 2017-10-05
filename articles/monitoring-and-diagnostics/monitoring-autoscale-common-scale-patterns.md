---
title: "Обзор общих шаблонов автомасштабирования | Документация Майкрософт"
description: "Ознакомьтесь с некоторыми общими шаблонами для автомасштабирования ресурсов в Azure."
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
ms.openlocfilehash: fce51546e041c8989d813c3935e058c52b38ba77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-common-autoscale-patterns"></a><span data-ttu-id="db64c-103">Обзор общих шаблонов автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="db64c-103">Overview of common autoscale patterns</span></span>
<span data-ttu-id="db64c-104">В этой статье описаны некоторые общие шаблоны для масштабирования ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="db64c-104">This article describes some of the common patterns to scale your resource in Azure.</span></span>

<span data-ttu-id="db64c-105">Автомасштабирование Azure Monitor используется только с масштабируемыми наборами виртуальных машин, облачными службами, а также с планами и средами службы приложений.</span><span class="sxs-lookup"><span data-stu-id="db64c-105">Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="db64c-106">Начало работы</span><span class="sxs-lookup"><span data-stu-id="db64c-106">Lets get started</span></span>

<span data-ttu-id="db64c-107">В данной статье предполагается, что вы знакомы с автомасштабированием.</span><span class="sxs-lookup"><span data-stu-id="db64c-107">This article assumes that you are familiar with auto scale.</span></span> <span data-ttu-id="db64c-108">Сведения по началу работы с автомасштабированием ресурсов см. [здесь][1].</span><span class="sxs-lookup"><span data-stu-id="db64c-108">You can [get started here to scale your resource][1].</span></span> <span data-ttu-id="db64c-109">Далее приведены некоторые общие шаблоны масштабирования.</span><span class="sxs-lookup"><span data-stu-id="db64c-109">The following are some of the common scale patterns.</span></span>

## <a name="scale-based-on-cpu"></a><span data-ttu-id="db64c-110">Масштабирование на основе использования ЦП</span><span class="sxs-lookup"><span data-stu-id="db64c-110">Scale based on CPU</span></span>

<span data-ttu-id="db64c-111">У вас есть веб-приложение (VMSS или роль облачной службы). Кроме того:</span><span class="sxs-lookup"><span data-stu-id="db64c-111">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="db64c-112">вы хотите выполнять развертывание и свертывание на основе использования ЦП;</span><span class="sxs-lookup"><span data-stu-id="db64c-112">You want to scale out/scale in based on CPU.</span></span>
- <span data-ttu-id="db64c-113">вы хотите иметь минимальное количество экземпляров;</span><span class="sxs-lookup"><span data-stu-id="db64c-113">Additionally, you want to ensure there is a minimum number of instances.</span></span> 
- <span data-ttu-id="db64c-114">при этом нужно задать максимальное ограничение на количество экземпляров, которые можно развернуть.</span><span class="sxs-lookup"><span data-stu-id="db64c-114">Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.</span></span>

![Масштабирование на основе использования ЦП][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a><span data-ttu-id="db64c-116">Масштабирование в рабочие и выходные дни</span><span class="sxs-lookup"><span data-stu-id="db64c-116">Scale differently on weekdays vs weekends</span></span>

<span data-ttu-id="db64c-117">У вас есть веб-приложение (VMSS или роль облачной службы). Кроме того:</span><span class="sxs-lookup"><span data-stu-id="db64c-117">You have a web app (/VMSS/cloud service role) and</span></span>

- <span data-ttu-id="db64c-118">требуется 3 экземпляра по умолчанию (в рабочие дни);</span><span class="sxs-lookup"><span data-stu-id="db64c-118">You want 3 instances by default (on weekdays)</span></span>
- <span data-ttu-id="db64c-119">трафик в выходные дни не ожидается, поэтому необходимо уменьшить масштаб до 1 экземпляра.</span><span class="sxs-lookup"><span data-stu-id="db64c-119">You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.</span></span>

![Масштабирование в рабочие и выходные дни][3]

## <a name="scale-differently-during-holidays"></a><span data-ttu-id="db64c-121">Масштабирование в праздничные дни</span><span class="sxs-lookup"><span data-stu-id="db64c-121">Scale differently during holidays</span></span>

<span data-ttu-id="db64c-122">У вас есть веб-приложение (VMSS или роль облачной службы). Кроме того:</span><span class="sxs-lookup"><span data-stu-id="db64c-122">You have a web app (/VMSS/cloud service role) and</span></span> 

- <span data-ttu-id="db64c-123">необходимо увеличивать и уменьшать масштаб на основе использования ЦП по умолчанию;</span><span class="sxs-lookup"><span data-stu-id="db64c-123">You want to scale up/down based on CPU usage by default</span></span>
- <span data-ttu-id="db64c-124">однако во время праздников (или в определенные дни, которые важны для бизнеса) вы хотите переопределить значения по умолчанию и увеличить емкость.</span><span class="sxs-lookup"><span data-stu-id="db64c-124">However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.</span></span>

![Масштабирование в праздничные дни][4]

## <a name="scale-based-on-custom-metric"></a><span data-ttu-id="db64c-126">Масштабирование на основе пользовательской метрики</span><span class="sxs-lookup"><span data-stu-id="db64c-126">Scale based on custom metric</span></span>

<span data-ttu-id="db64c-127">У вас есть веб-интерфейс и уровень API, который взаимодействует с серверной частью.</span><span class="sxs-lookup"><span data-stu-id="db64c-127">You have a web front end and a API tier that communicates with the backend.</span></span> 

- <span data-ttu-id="db64c-128">Необходимо масштабировать уровень API на основе пользовательских событий во внешнем интерфейсе (например, масштабировать процесс оформления заказов и оплаты на основе количества элементов в корзине).</span><span class="sxs-lookup"><span data-stu-id="db64c-128">You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)</span></span>

![Масштабирование на основе пользовательской метрики][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png