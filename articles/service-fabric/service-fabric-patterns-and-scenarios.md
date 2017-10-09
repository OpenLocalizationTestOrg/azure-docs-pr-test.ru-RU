---
title: "aaaAzure Service Fabric шаблонов и сценариев | Документы Microsoft"
description: "Рекомендации и проверенные toodesign повторно используемых шаблонов разработки и работы вашей микрослужбами на Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: d5aa75ff-98b9-4573-a2e5-7f5ab288157a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 3811420eb53d9a49e490dd2e2e5319d8dea5629c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="7abf7-103">Шаблоны и сценарии использования Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7abf7-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="7abf7-104">Если вы рассматриваете возможность создания крупномасштабных микрослужбами, с помощью Azure Service Fabric, сведения из hello специалисты, которые разрабатываются и создаются эта платформа как услуга (PaaS).</span><span class="sxs-lookup"><span data-stu-id="7abf7-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from hello experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="7abf7-105">Приступая к работе с правильной архитектуры и затем Узнайте, как toooptimize ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="7abf7-105">Get started with proper architecture, and then learn how toooptimize resources for your application.</span></span> <span data-ttu-id="7abf7-106">Hello [Service Fabric шаблоны и методики](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) курс содержит ответы на вопросы hello, наиболее часто задаваемые реальных клиентами о Service Fabric сценариев и области приложения.</span><span class="sxs-lookup"><span data-stu-id="7abf7-106">hello [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers hello questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="7abf7-107">Узнайте, как toodesign, разработки и эксплуатации вашей микрослужбами на Service Fabric, с использованием рекомендаций и проверенные, многократно используемых шаблонов.</span><span class="sxs-lookup"><span data-stu-id="7abf7-107">Find out how toodesign, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="7abf7-108">Получите общие сведения о Service Fabric, а затем подробнее изучите разделы, посвященные оптимизации и безопасности кластера, переносу устаревших приложений, масштабированию в Интернете вещей, размещению игровых ядер и другим темам.</span><span class="sxs-lookup"><span data-stu-id="7abf7-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="7abf7-109">Посмотрите на непрерывной поставки для различных рабочих нагрузок и даже получить hello сведения о поддержке Linux и контейнеры.</span><span class="sxs-lookup"><span data-stu-id="7abf7-109">Look at continuous delivery for various workloads, and even get hello details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="7abf7-110">Введение</span><span class="sxs-lookup"><span data-stu-id="7abf7-110">Introduction</span></span>
<span data-ttu-id="7abf7-111">Рекомендации и общие сведения о выборе между платформой как услугой (PaaS) и инфраструктурой как услугой (IaaS).</span><span class="sxs-lookup"><span data-stu-id="7abf7-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="7abf7-112">Получение сведений о hello на следующие принципы разработки проверенные приложений.</span><span class="sxs-lookup"><span data-stu-id="7abf7-112">Get hello details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="7abf7-113">Видео</span><span class="sxs-lookup"><span data-stu-id="7abf7-113">Video</span></span></th><th><span data-ttu-id="7abf7-114">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7abf7-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7abf7-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Введение tooService структуры</a></span><span class="sxs-lookup"><span data-stu-id="7abf7-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction tooService Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="7abf7-116">Планирование кластера и управление им</span><span class="sxs-lookup"><span data-stu-id="7abf7-116">Cluster planning and management</span></span>
<span data-ttu-id="7abf7-117">Получите сведения о планировании ресурсов, оптимизации и безопасности кластера в контексте Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7abf7-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="7abf7-118">Видео</span><span class="sxs-lookup"><span data-stu-id="7abf7-118">Video</span></span></th><th><span data-ttu-id="7abf7-119">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7abf7-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="7abf7-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Планирование кластера и управление им</a></span><span class="sxs-lookup"><span data-stu-id="7abf7-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="7abf7-121">Гипермасштабируемые веб-службы</span><span class="sxs-lookup"><span data-stu-id="7abf7-121">Hyper-scale web</span></span>
<span data-ttu-id="7abf7-122">Ознакомьтесь с основными понятиями гипермасштабируемых веб-служб, включая доступность и надежность, гипермасштабирование и управление состоянием.</span><span class="sxs-lookup"><span data-stu-id="7abf7-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="7abf7-123">Видео</span><span class="sxs-lookup"><span data-stu-id="7abf7-123">Video</span></span></th><th><span data-ttu-id="7abf7-124">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7abf7-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7abf7-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Гипермасштабируемые веб-службы</a></span><span class="sxs-lookup"><span data-stu-id="7abf7-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="7abf7-126">Интернет вещей</span><span class="sxs-lookup"><span data-stu-id="7abf7-126">IoT</span></span>
<span data-ttu-id="7abf7-127">Изучите hello Интернета вещей (IoT) в контексте hello Azure Service Fabric, включая hello Azure IoT конвейера, поддержки нескольких клиентов и IoT в масштабе.</span><span class="sxs-lookup"><span data-stu-id="7abf7-127">Explore hello Internet of Things (IoT) in hello context of Azure Service Fabric, including hello Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="7abf7-128">Видео</span><span class="sxs-lookup"><span data-stu-id="7abf7-128">Video</span></span></th><th><span data-ttu-id="7abf7-129">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7abf7-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7abf7-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Интернет вещей</a></span><span class="sxs-lookup"><span data-stu-id="7abf7-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="7abf7-131">Игры</span><span class="sxs-lookup"><span data-stu-id="7abf7-131">Gaming</span></span>
<span data-ttu-id="7abf7-132">Рассмотрите пошаговые и интерактивные игры, а также узнайте о размещении существующих игровых ядер.</span><span class="sxs-lookup"><span data-stu-id="7abf7-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="7abf7-133">Видео</span><span class="sxs-lookup"><span data-stu-id="7abf7-133">Video</span></span></th><th><span data-ttu-id="7abf7-134">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7abf7-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7abf7-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Игры</a></span><span class="sxs-lookup"><span data-stu-id="7abf7-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="7abf7-136">Непрерывная доставка</span><span class="sxs-lookup"><span data-stu-id="7abf7-136">Continuous delivery</span></span>
<span data-ttu-id="7abf7-137">Ознакомьтесь с основными понятиями, такими как непрерывная интеграция и непрерывная доставка с помощью Visual Studio Team Services, рабочий процесс сборки/пакета/публикации, настройка в нескольких средах, а также пакет и общая папка службы.</span><span class="sxs-lookup"><span data-stu-id="7abf7-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="7abf7-138">Видео</span><span class="sxs-lookup"><span data-stu-id="7abf7-138">Video</span></span></th><th><span data-ttu-id="7abf7-139">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7abf7-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7abf7-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Непрерывная доставка</a></span><span class="sxs-lookup"><span data-stu-id="7abf7-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="7abf7-141">Миграция</span><span class="sxs-lookup"><span data-stu-id="7abf7-141">Migration</span></span>
<span data-ttu-id="7abf7-142">Дополнительные сведения о миграции из облачной службы, кроме toomigration прежних версий приложений.</span><span class="sxs-lookup"><span data-stu-id="7abf7-142">Learn about migrating from a cloud service, in addition toomigration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="7abf7-143">Видео</span><span class="sxs-lookup"><span data-stu-id="7abf7-143">Video</span></span></th><th><span data-ttu-id="7abf7-144">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7abf7-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7abf7-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Миграция</a></span><span class="sxs-lookup"><span data-stu-id="7abf7-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="7abf7-146">Контейнеры и поддержка Linux</span><span class="sxs-lookup"><span data-stu-id="7abf7-146">Containers and Linux support</span></span>
<span data-ttu-id="7abf7-147">Получить вопрос toohello ответов hello, «почему контейнеры?»</span><span class="sxs-lookup"><span data-stu-id="7abf7-147">Get hello answer toohello question, "Why containers?"</span></span> <span data-ttu-id="7abf7-148">Дополнительные сведения о предварительной версии hello для контейнеров Windows, Linux поддерживает и orchestration контейнеров Linux.</span><span class="sxs-lookup"><span data-stu-id="7abf7-148">Learn about hello preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="7abf7-149">Кроме того, узнайте, как приложения tooLinux toomigrate .NET Core.</span><span class="sxs-lookup"><span data-stu-id="7abf7-149">Plus, find out how toomigrate .NET Core apps tooLinux.</span></span>

<table><tr><th><span data-ttu-id="7abf7-150">Видео</span><span class="sxs-lookup"><span data-stu-id="7abf7-150">Video</span></span></th><th><span data-ttu-id="7abf7-151">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="7abf7-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="7abf7-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Контейнеры и поддержка Linux</a></span><span class="sxs-lookup"><span data-stu-id="7abf7-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="7abf7-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7abf7-153">Next steps</span></span>
<span data-ttu-id="7abf7-154">Теперь, когда вы узнали о Service Fabric шаблонов и сценариев, Дополнительные сведения о том, как слишком[создания кластеров и управление ими](service-fabric-deploy-anywhere.md), [перенос облачных служб приложений tooService структуры](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [Настройка непрерывной поставки](service-fabric-set-up-continuous-integration.md), и [развернуть контейнеры](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7abf7-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how too[create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps tooService Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
