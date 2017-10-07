---
title: "Экземпляры контейнером aaaAzure и Orchestration контейнера"
description: "Узнайте, как экземпляры контейнеров Azure взаимодействуют с оркестраторами контейнеров."
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 69a39edc6f14d885c1ac300990ed1399002ccfee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="fcdcf-103">Экземпляры контейнеров Azure и оркестраторы контейнеров</span><span class="sxs-lookup"><span data-stu-id="fcdcf-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="fcdcf-104">Благодаря небольшому размеру и ориентации приложения контейнеры хорошо подходят для эластичных сред доставки и архитектур на основе микрослужб.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="fcdcf-105">Задача Hello Автоматизация и управление большим числом контейнеров и их взаимодействие называется *orchestration*.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-105">hello task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="fcdcf-106">Популярные контейнера orchestrators включают Kubernetes, DC/OS и помощью Docker Swarm, которые доступны в hello [контейнера службы Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="fcdcf-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in hello [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="fcdcf-107">Экземпляры контейнером Azure предоставляет некоторые основные функции платформы orchestration планирования hello, но он не распространяется на службы высокое значение hello, этих платформ предоставляют и может быть фактически взаимодополняющие с ними.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-107">Azure Container Instances provides some of hello basic scheduling capabilities of orchestration platforms, but it does not cover hello higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="fcdcf-108">В этой статье описывается область hello экземпляры контейнером Azure обрабатывает и насколько orchestrators контейнер может взаимодействовать с ним.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-108">This article describes hello scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="fcdcf-109">Традиционная оркестрация</span><span class="sxs-lookup"><span data-stu-id="fcdcf-109">Traditional orchestration</span></span>

<span data-ttu-id="fcdcf-110">стандартное определение Hello orchestration включает hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="fcdcf-110">hello standard definition of orchestration includes hello following tasks:</span></span>

- <span data-ttu-id="fcdcf-111">**Планирование**: Получив образ контейнера и запрос на ресурс, найти подходящий машины, на каком контейнере toorun hello.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which toorun hello container.</span></span>
- <span data-ttu-id="fcdcf-112">**Сходство/удаление сходства.** Укажите, что контейнеры должны выполняться рядом друг с другом (для повышения производительности) или на достаточном расстоянии друг от друга (для увеличения доступности).</span><span class="sxs-lookup"><span data-stu-id="fcdcf-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="fcdcf-113">**Мониторинг работоспособности.** Проверьте наличие ошибок в контейнере и автоматически перенесите их устранение.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="fcdcf-114">**Переход на другой ресурс**: отслеживать то, что работает на каждом компьютере и контейнеры из узлов toohealthy машины не удалось изменить расписание.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines toohealthy nodes.</span></span>
- <span data-ttu-id="fcdcf-115">**Масштабирование**: Добавление или удаление запросу toomatch экземпляры контейнером, вручную или автоматически.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-115">**Scaling**: Add or remove container instances toomatch demand, either manually or automatically.</span></span>
- <span data-ttu-id="fcdcf-116">**Работа по сети**: предоставляют наложения сети координацию toocommunicate контейнеры между несколькими компьютерами узла.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-116">**Networking**: Provide an overlay network for coordinating containers toocommunicate across multiple host machines.</span></span>
- <span data-ttu-id="fcdcf-117">**Обнаружение службы**: toolocate контейнеры друг с другом автоматически включают даже при перемещении между компьютеров-узлов и изменить IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-117">**Service discovery**: Enable containers toolocate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="fcdcf-118">**Координация обновлений приложений**: управление приложением tooavoid контейнера обновления время простоя и возможность выполнить откат, если что-то пойдет не так.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-118">**Coordinated application upgrades**: Manage container upgrades tooavoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="fcdcf-119">Оркестрация с помощью экземпляров контейнеров Azure: многоуровневый подход</span><span class="sxs-lookup"><span data-stu-id="fcdcf-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="fcdcf-120">Azure экземпляры контейнером включает tooorchestration многоуровневый подход, предоставляя все планирования hello и возможности управления требуется toorun одного контейнера, обеспечив при этом orchestrator задачи несколькими контейнерами toomanage платформы на основе.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-120">Azure Container Instances enables a layered approach tooorchestration, providing all of hello scheduling and management capabilities required toorun a single container, while allowing orchestrator platforms toomanage multi-container tasks on top of it.</span></span>

<span data-ttu-id="fcdcf-121">Поскольку все hello базовой инфраструктуры для экземпляров контейнера управляется Azure, платформу orchestrator не нуждается в tooconcern сам поиска соответствующего хост-компьютера, на какие toorun один контейнер.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-121">Because all of hello underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need tooconcern itself with finding an appropriate host machine on which toorun a single container.</span></span> <span data-ttu-id="fcdcf-122">Hello гибкости облачных hello гарантирует, что том, что один доступна всегда.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-122">hello elasticity of hello cloud ensures that one is always available.</span></span> <span data-ttu-id="fcdcf-123">Вместо этого hello orchestrator позволяет сосредоточиться на hello задачи, которые упрощают разработку hello архитектур несколькими контейнера, включая масштабирование и скоординированное обновлений.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-123">Instead, hello orchestrator can focus on hello tasks that simplify hello development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="fcdcf-124">Возможные сценарии</span><span class="sxs-lookup"><span data-stu-id="fcdcf-124">Potential scenarios</span></span>

<span data-ttu-id="fcdcf-125">Хотя интеграция оркестратора с экземплярами контейнеров Azure еще только на начальной стадии, мы ожидаем возникновения нескольких различных сред.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="fcdcf-126">Монопольная оркестрация экземпляров контейнера</span><span class="sxs-lookup"><span data-stu-id="fcdcf-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="fcdcf-127">Так как они быстро приступить к работе и выставления счетов по hello во-вторых, исключительно на основе среды экземпляры контейнером Azure предлагает hello самый быстрый способ tooget работы и toodeal с высокой степенью переменной рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-127">Because they start quickly and bill by hello second, an environment based exclusively on Azure Container Instances offers hello fastest way tooget started and toodeal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="fcdcf-128">Сочетание экземпляров контейнеров и контейнеров в виртуальных машинах</span><span class="sxs-lookup"><span data-stu-id="fcdcf-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="fcdcf-129">Для долго выполняющихся стабильный рабочих нагрузок, управляя операциями контейнеры в кластере выделенных виртуальных машинах обычно будет дешевле, чем выполнение hello же контейнеры с экземпляры контейнером.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running hello same containers with Container Instances.</span></span> <span data-ttu-id="fcdcf-130">Однако экземпляры контейнером обеспечивает эффективное решение для быстрого развертывания и сжатием вашей toodeal общей емкости с неверным или кратковременных всплески в использовании.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity toodeal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="fcdcf-131">Вместо того чтобы масштабирование hello количество виртуальных машин в кластере, то развертывание дополнительные контейнеры на этих компьютерах, hello orchestrator можно просто запланировать hello дополнительные контейнеры с помощью экземпляров контейнера и удалить их, когда они не нужны.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-131">Rather than scaling out hello number of virtual machines in your cluster, then deploying additional containers onto those machines, hello orchestrator can simply schedule hello additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="fcdcf-132">Пример реализации: соединитель экземпляров контейнеров Azure для Kubernetes</span><span class="sxs-lookup"><span data-stu-id="fcdcf-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="fcdcf-133">toodemonstrate как контейнер orchestration платформы могут интегрироваться с Azure экземпляров контейнера, мы запустили построение [образец соединитель для Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="fcdcf-133">toodemonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="fcdcf-134">Здравствуйте соединитель для Kubernetes имитирует hello [kubelet] [ kubelet-doc] путем регистрации как узел с неограниченной емкости и диспетчеризации Создание hello [модулей] [ pod-doc] как контейнер группы в Azure экземпляры контейнером.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-134">hello connector for Kubernetes mimics hello [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching hello creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="fcdcf-135">Соединителей для других orchestrators может быть построена, аналогично интегрирован примитивы платформы toocombine мощность hello hello orchestrator API hello скорость и простота управления контейнерами в экземплярах контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives toocombine hello power of hello orchestrator API with hello speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="fcdcf-136">Здравствуйте ACI соединитель для Kubernetes *экспериментальный* и не должны использоваться в производственной среде.</span><span class="sxs-lookup"><span data-stu-id="fcdcf-136">hello ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcdcf-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fcdcf-137">Next steps</span></span>

<span data-ttu-id="fcdcf-138">Создание первого контейнера с экземплярами Azure контейнера, с помощью hello [краткого руководства по](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="fcdcf-138">Create your first container with Azure Container Instances using hello [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/