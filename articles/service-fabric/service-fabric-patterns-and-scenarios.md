---
title: "Шаблоны и сценарии использования Azure Service Fabric | Документация Майкрософт"
description: "Практические рекомендации по применению проверенных шаблонов (с возможностью повторного использования) для проектирования, разработки и эксплуатации микрослужб в Service Fabric."
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
ms.openlocfilehash: fb2fa495758433e357722427b1c162420935955d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="service-fabric-patterns-and-scenarios"></a><span data-ttu-id="b7f9e-103">Шаблоны и сценарии использования Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b7f9e-103">Service Fabric patterns and scenarios</span></span>
<span data-ttu-id="b7f9e-104">Если вам требуется создать крупномасштабные микрослужбы с помощью Azure Service Fabric, воспользуйтесь опытом специалистов, которые разработали и создали эту платформу как услугу (PaaS).</span><span class="sxs-lookup"><span data-stu-id="b7f9e-104">If you’re looking at building large-scale microservices using Azure Service Fabric, learn from the experts who designed and built this platform as a service (PaaS).</span></span> <span data-ttu-id="b7f9e-105">Начните с правильной архитектуры, а затем узнайте, как оптимизировать ресурсы для приложения.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-105">Get started with proper architecture, and then learn how to optimize resources for your application.</span></span> <span data-ttu-id="b7f9e-106">Курс [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) (Шаблоны Service Fabric и практические рекомендации) содержит ответы на самые распространенные вопросы, задаваемые реальными пользователями о сценариях использования и областях применения Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-106">The [Service Fabric Patterns and Practices](https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344) course answers the questions most often asked by real-world customers about Service Fabric scenarios and application areas.</span></span>
 
<span data-ttu-id="b7f9e-107">Узнайте, как проектировать, разрабатывать и эксплуатировать микрослужбы в Service Fabric, применяя рекомендации и проверенные шаблоны с возможностью повторного использования.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-107">Find out how to design, develop, and operate your microservices on Service Fabric using best practices and proven, reusable patterns.</span></span> <span data-ttu-id="b7f9e-108">Получите общие сведения о Service Fabric, а затем подробнее изучите разделы, посвященные оптимизации и безопасности кластера, переносу устаревших приложений, масштабированию в Интернете вещей, размещению игровых ядер и другим темам.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-108">Get an overview of Service Fabric and then dive deep into topics that cover cluster optimization and security, migrating legacy apps, IoT at scale, hosting game engines, and more.</span></span> <span data-ttu-id="b7f9e-109">Рассмотрите процесс непрерывной доставки для различных рабочих нагрузок, а также узнайте полезные сведения о контейнерах и поддержке Linux.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-109">Look at continuous delivery for various workloads, and even get the details on Linux support and containers.</span></span> 

## <a name="introduction"></a><span data-ttu-id="b7f9e-110">Введение</span><span class="sxs-lookup"><span data-stu-id="b7f9e-110">Introduction</span></span>
<span data-ttu-id="b7f9e-111">Рекомендации и общие сведения о выборе между платформой как услугой (PaaS) и инфраструктурой как услугой (IaaS).</span><span class="sxs-lookup"><span data-stu-id="b7f9e-111">Explore best practices, and learn about choosing platform as a service (PaaS) over infrastructure as a service (IaaS).</span></span> <span data-ttu-id="b7f9e-112">Ознакомьтесь со следующими проверенными принципами проектирования приложений.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-112">Get the details on following proven application design principles.</span></span>

<table><tr><th><span data-ttu-id="b7f9e-113">Видео</span><span class="sxs-lookup"><span data-stu-id="b7f9e-113">Video</span></span></th><th><span data-ttu-id="b7f9e-114">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="b7f9e-114">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=N2KwbbSGD_6405167344">
<img src="./media/service-fabric-patterns-and-scenarios/intro.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="b7f9e-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Общие сведения о Service Fabric</a></span><span class="sxs-lookup"><span data-stu-id="b7f9e-115"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mudwqISGD_6005167344">Introduction to Service Fabric</a></span></span></td></tr>
</table>

## <a name="cluster-planning-and-management"></a><span data-ttu-id="b7f9e-116">Планирование кластера и управление им</span><span class="sxs-lookup"><span data-stu-id="b7f9e-116">Cluster planning and management</span></span>
<span data-ttu-id="b7f9e-117">Получите сведения о планировании ресурсов, оптимизации и безопасности кластера в контексте Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-117">Learn about capacity planning, cluster optimization, and cluster security, in this look at Azure Service Fabric.</span></span>

<table><tr><th><span data-ttu-id="b7f9e-118">Видео</span><span class="sxs-lookup"><span data-stu-id="b7f9e-118">Video</span></span></th><th><span data-ttu-id="b7f9e-119">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="b7f9e-119">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=cyDYZcSGD_2805167344">
<img src="./media/service-fabric-patterns-and-scenarios/cluster.png" WIDTH="360" HEIGHT="244">
</a></td><td> <span data-ttu-id="b7f9e-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Планирование кластера и управление им</a></span><span class="sxs-lookup"><span data-stu-id="b7f9e-120"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=E5B3nJSGD_805167344">Cluster Planning and Management</a></span></span></td></tr>
</table>

## <a name="hyper-scale-web"></a><span data-ttu-id="b7f9e-121">Гипермасштабируемые веб-службы</span><span class="sxs-lookup"><span data-stu-id="b7f9e-121">Hyper-scale web</span></span>
<span data-ttu-id="b7f9e-122">Ознакомьтесь с основными понятиями гипермасштабируемых веб-служб, включая доступность и надежность, гипермасштабирование и управление состоянием.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-122">Review concepts around hyper-scale web, including availability and reliability, hyper-scale, and state management.</span></span>

<table><tr><th><span data-ttu-id="b7f9e-123">Видео</span><span class="sxs-lookup"><span data-stu-id="b7f9e-123">Video</span></span></th><th><span data-ttu-id="b7f9e-124">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="b7f9e-124">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=NgldAdSGD_405167344">
<img src="./media/service-fabric-patterns-and-scenarios/hyperscaleweb.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="b7f9e-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Гипермасштабируемые веб-службы</a></span><span class="sxs-lookup"><span data-stu-id="b7f9e-125"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=CPMLBLSGD_7705167344">Hyper-scale web</a></span></span></td></tr>
</table>

## <a name="iot"></a><span data-ttu-id="b7f9e-126">Интернет вещей</span><span class="sxs-lookup"><span data-stu-id="b7f9e-126">IoT</span></span>
<span data-ttu-id="b7f9e-127">Ознакомьтесь с возможностями Интернета вещей в контексте Azure Service Fabric, включая конвейер Интернета вещей Azure, мультитенантность и масштабирование в Интернете вещей.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-127">Explore the Internet of Things (IoT) in the context of Azure Service Fabric, including the Azure IoT pipeline, multi-tenancy, and IoT at scale.</span></span>

<table><tr><th><span data-ttu-id="b7f9e-128">Видео</span><span class="sxs-lookup"><span data-stu-id="b7f9e-128">Video</span></span></th><th><span data-ttu-id="b7f9e-129">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="b7f9e-129">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=naFUVeSGD_1505167344">
<img src="./media/service-fabric-patterns-and-scenarios/iot.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="b7f9e-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Интернет вещей</a></span><span class="sxs-lookup"><span data-stu-id="b7f9e-130"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">IoT</a></span></span></td></tr>
</table>

## <a name="gaming"></a><span data-ttu-id="b7f9e-131">Игры</span><span class="sxs-lookup"><span data-stu-id="b7f9e-131">Gaming</span></span>
<span data-ttu-id="b7f9e-132">Рассмотрите пошаговые и интерактивные игры, а также узнайте о размещении существующих игровых ядер.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-132">Look at turn-based games, interactive games, and hosting existing game engines.</span></span>

<table><tr><th><span data-ttu-id="b7f9e-133">Видео</span><span class="sxs-lookup"><span data-stu-id="b7f9e-133">Video</span></span></th><th><span data-ttu-id="b7f9e-134">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="b7f9e-134">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=6wECzeSGD_3805167344">
<img src="./media/service-fabric-patterns-and-scenarios/gaming.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="b7f9e-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Игры</a></span><span class="sxs-lookup"><span data-stu-id="b7f9e-135"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=kfqFWMSGD_6205167344">Gaming</a></span></span></td></tr>
</table>

## <a name="continuous-delivery"></a><span data-ttu-id="b7f9e-136">Непрерывная доставка</span><span class="sxs-lookup"><span data-stu-id="b7f9e-136">Continuous delivery</span></span>
<span data-ttu-id="b7f9e-137">Ознакомьтесь с основными понятиями, такими как непрерывная интеграция и непрерывная доставка с помощью Visual Studio Team Services, рабочий процесс сборки/пакета/публикации, настройка в нескольких средах, а также пакет и общая папка службы.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-137">Explore concepts, including continuous integration/continuous delivery with Visual Studio Team Services, build/package/publish workflow, multi-environment setup, and service package/share.</span></span>

<table><tr><th><span data-ttu-id="b7f9e-138">Видео</span><span class="sxs-lookup"><span data-stu-id="b7f9e-138">Video</span></span></th><th><span data-ttu-id="b7f9e-139">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="b7f9e-139">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=78h5ofSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/cd.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="b7f9e-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Непрерывная доставка</a></span><span class="sxs-lookup"><span data-stu-id="b7f9e-140"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=VlENvOSGD_105167344">Continuous delivery</a></span></span></td></tr>
</table>

## <a name="migration"></a><span data-ttu-id="b7f9e-141">Миграция</span><span class="sxs-lookup"><span data-stu-id="b7f9e-141">Migration</span></span>
<span data-ttu-id="b7f9e-142">Сведения о переносе из облачной службы и о переносе устаревших приложений.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-142">Learn about migrating from a cloud service, in addition to migration of legacy apps.</span></span>

<table><tr><th><span data-ttu-id="b7f9e-143">Видео</span><span class="sxs-lookup"><span data-stu-id="b7f9e-143">Video</span></span></th><th><span data-ttu-id="b7f9e-144">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="b7f9e-144">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=hd1cMgSGD_5605167344">
<img src="./media/service-fabric-patterns-and-scenarios/migration.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="b7f9e-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Миграция</a></span><span class="sxs-lookup"><span data-stu-id="b7f9e-145"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=GQAq4QSGD_8305167344">Migration</a></span></span></td></tr>
</table>

## <a name="containers-and-linux-support"></a><span data-ttu-id="b7f9e-146">Контейнеры и поддержка Linux</span><span class="sxs-lookup"><span data-stu-id="b7f9e-146">Containers and Linux support</span></span>
<span data-ttu-id="b7f9e-147">Получите ответ на вопрос "Зачем нужны контейнеры?"</span><span class="sxs-lookup"><span data-stu-id="b7f9e-147">Get the answer to the question, "Why containers?"</span></span> <span data-ttu-id="b7f9e-148">Сведения о предварительных версиях функций контейнеров Windows, поддержки Linux и оркестрации контейнеров Linux.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-148">Learn about the preview for Windows containers, Linux supports, and Linux containers orchestration.</span></span> <span data-ttu-id="b7f9e-149">Узнайте, как выполнить перенос приложений .NET Core на Linux.</span><span class="sxs-lookup"><span data-stu-id="b7f9e-149">Plus, find out how to migrate .NET Core apps to Linux.</span></span>

<table><tr><th><span data-ttu-id="b7f9e-150">Видео</span><span class="sxs-lookup"><span data-stu-id="b7f9e-150">Video</span></span></th><th><span data-ttu-id="b7f9e-151">В формате PowerPoint</span><span class="sxs-lookup"><span data-stu-id="b7f9e-151">PowerPoint deck</span></span></th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=V1ERJhSGD_305167344">
<img src="./media/service-fabric-patterns-and-scenarios/containers.png" WIDTH="360" HEIGHT="244">
</a></td><td><span data-ttu-id="b7f9e-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Контейнеры и поддержка Linux</a></span><span class="sxs-lookup"><span data-stu-id="b7f9e-152"><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/service-fabric-patterns-and-practices-16925?l=mlYsZRSGD_2105167344">Containers and Linux support</a></span></span></td></tr>
</table>

## <a name="next-steps"></a><span data-ttu-id="b7f9e-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b7f9e-153">Next steps</span></span>
<span data-ttu-id="b7f9e-154">Теперь, когда вы изучили шаблоны и сценарии использования Service Fabric, узнайте больше о [создании кластеров и управлении ими](service-fabric-deploy-anywhere.md), [переносе приложений облачных служб в Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [настройке непрерывной доставки](service-fabric-set-up-continuous-integration.md) и [развертывании контейнеров](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b7f9e-154">Now that you've learned about Service Fabric patterns and scenarios, read more about how to [create and manage clusters](service-fabric-deploy-anywhere.md), [migrate Cloud Services apps to Service Fabric](service-fabric-cloud-services-migration-worker-role-stateless-service.md), [set up continuous delivery](service-fabric-set-up-continuous-integration.md), and [deploy containers](service-fabric-containers-overview.md).</span></span>
