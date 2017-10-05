---
title: "Экземпляры контейнеров Azure и оркестрация контейнеров"
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
ms.openlocfilehash: cbb558a92d565759c8dc7d2693960955eb053b0a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-container-instances-and-container-orchestrators"></a><span data-ttu-id="cb483-103">Экземпляры контейнеров Azure и оркестраторы контейнеров</span><span class="sxs-lookup"><span data-stu-id="cb483-103">Azure Container Instances and container orchestrators</span></span>

<span data-ttu-id="cb483-104">Благодаря небольшому размеру и ориентации приложения контейнеры хорошо подходят для эластичных сред доставки и архитектур на основе микрослужб.</span><span class="sxs-lookup"><span data-stu-id="cb483-104">Because of their small size and application orientation, containers are well suited for agile delivery environments and microservice-based architectures.</span></span> <span data-ttu-id="cb483-105">Задача автоматизации большого числа контейнеров, управления ими, а также способом их взаимодействия называется *оркестрацией*.</span><span class="sxs-lookup"><span data-stu-id="cb483-105">The task of automating and managing a large number of containers and how they interact is known as *orchestration*.</span></span> <span data-ttu-id="cb483-106">В число популярных оркестраторов контейнеров входят Kubernetes, DC/OS и Docker Swarm, каждый из которых доступен в [службе контейнеров Azure](https://docs.microsoft.com/azure/container-service/).</span><span class="sxs-lookup"><span data-stu-id="cb483-106">Popular container orchestrators include Kubernetes, DC/OS, and Docker Swarm, all of which are available in the [Azure Container Service](https://docs.microsoft.com/azure/container-service/).</span></span>

<span data-ttu-id="cb483-107">Экземпляры контейнеров Azure предоставляют некоторые основные функции планирования платформ оркестрации, однако они не охватывают службы более высокого значения, которые предоставляют эти платформы, и могут их дополнять.</span><span class="sxs-lookup"><span data-stu-id="cb483-107">Azure Container Instances provides some of the basic scheduling capabilities of orchestration platforms, but it does not cover the higher-value services that those platforms provide and can in fact be complementary with them.</span></span> <span data-ttu-id="cb483-108">В этой статье описывается область, которую обрабатывают экземпляры контейнеров Azure, и как она взаимодействует с полной оркестрацией контейнера.</span><span class="sxs-lookup"><span data-stu-id="cb483-108">This article describes the scope of what Azure Container Instances handles and how full container orchestrators might interact with it.</span></span>

## <a name="traditional-orchestration"></a><span data-ttu-id="cb483-109">Традиционная оркестрация</span><span class="sxs-lookup"><span data-stu-id="cb483-109">Traditional orchestration</span></span>

<span data-ttu-id="cb483-110">Стандартное определение оркестрации включает в себя следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="cb483-110">The standard definition of orchestration includes the following tasks:</span></span>

- <span data-ttu-id="cb483-111">**Планирование.** Получив образ контейнера и запрос ресурса, найдите подходящий компьютер для запуска контейнера.</span><span class="sxs-lookup"><span data-stu-id="cb483-111">**Scheduling**: Given a container image and a resource request, find a suitable machine on which to run the container.</span></span>
- <span data-ttu-id="cb483-112">**Сходство/удаление сходства.** Укажите, что контейнеры должны выполняться рядом друг с другом (для повышения производительности) или на достаточном расстоянии друг от друга (для увеличения доступности).</span><span class="sxs-lookup"><span data-stu-id="cb483-112">**Affinity/Anti-affinity**: Specify that a set of containers should run nearby each other (for performance) or sufficiently far apart (for availability).</span></span>
- <span data-ttu-id="cb483-113">**Мониторинг работоспособности.** Проверьте наличие ошибок в контейнере и автоматически перенесите их устранение.</span><span class="sxs-lookup"><span data-stu-id="cb483-113">**Health monitoring**: Watch for container failures and automatically reschedule them.</span></span>
- <span data-ttu-id="cb483-114">**Отработка отказа.** Отслеживайте процессы, которые выполняются на каждом компьютере, и перенесите контейнеры из неисправных компьютеров в работоспособные узлы.</span><span class="sxs-lookup"><span data-stu-id="cb483-114">**Failover**: Keep track of what is running on each machine and reschedule containers from failed machines to healthy nodes.</span></span>
- <span data-ttu-id="cb483-115">**Масштабирование.** Добавьте или удалите экземпляры контейнеров в соответствии с требованиями вручную или автоматически.</span><span class="sxs-lookup"><span data-stu-id="cb483-115">**Scaling**: Add or remove container instances to match demand, either manually or automatically.</span></span>
- <span data-ttu-id="cb483-116">**Сеть.** Укажите наложенную сеть для координации контейнеров, взаимодействующих в нескольких хост-компьютерах.</span><span class="sxs-lookup"><span data-stu-id="cb483-116">**Networking**: Provide an overlay network for coordinating containers to communicate across multiple host machines.</span></span>
- <span data-ttu-id="cb483-117">**Обнаружение служб.** Позвольте контейнерам автоматически находить друг друга, даже когда они перемещаются между хост-компьютерами и их IP-адреса изменяются.</span><span class="sxs-lookup"><span data-stu-id="cb483-117">**Service discovery**: Enable containers to locate each other automatically even as they move between host machines and change IP addresses.</span></span>
- <span data-ttu-id="cb483-118">**Координирование обновлений приложений.** Управляйте обновлениями контейнера, чтобы избежать простоя приложения, и выполняйте откат, если что-то пошло не так.</span><span class="sxs-lookup"><span data-stu-id="cb483-118">**Coordinated application upgrades**: Manage container upgrades to avoid application down time and enable rollback if something goes wrong.</span></span>

## <a name="orchestration-with-azure-container-instances-a-layered-approach"></a><span data-ttu-id="cb483-119">Оркестрация с помощью экземпляров контейнеров Azure: многоуровневый подход</span><span class="sxs-lookup"><span data-stu-id="cb483-119">Orchestration with Azure Container Instances: A layered approach</span></span>

<span data-ttu-id="cb483-120">Экземпляры контейнеров Azure позволяют применять многоуровневый подход для выполнения оркестрации, предоставляя все возможности планирования и управления, необходимые для запуска одного контейнера. Они также позволяют использовать платформы оркестратора, чтобы управлять многоконтейнерными задачами на их базе.</span><span class="sxs-lookup"><span data-stu-id="cb483-120">Azure Container Instances enables a layered approach to orchestration, providing all of the scheduling and management capabilities required to run a single container, while allowing orchestrator platforms to manage multi-container tasks on top of it.</span></span>

<span data-ttu-id="cb483-121">Так как вся базовая инфраструктура для экземпляров контейнеров управляется с помощью Azure, платформе оркестратора не нужно самостоятельно искать подходящий хост-компьютер для запуска одного контейнера.</span><span class="sxs-lookup"><span data-stu-id="cb483-121">Because all of the underlying infrastructure for Container Instances is managed by Azure, an orchestrator platform does not need to concern itself with finding an appropriate host machine on which to run a single container.</span></span> <span data-ttu-id="cb483-122">Благодаря гибкости облака один контейнер всегда будет доступным.</span><span class="sxs-lookup"><span data-stu-id="cb483-122">The elasticity of the cloud ensures that one is always available.</span></span> <span data-ttu-id="cb483-123">Вместо этого оркестратор может сосредоточиться на задачах, которые упрощают разработку архитектуры нескольких контейнеров, включая масштабирование и скоординированные обновления.</span><span class="sxs-lookup"><span data-stu-id="cb483-123">Instead, the orchestrator can focus on the tasks that simplify the development of multi-container architectures, including scaling and coordinated upgrades.</span></span>



## <a name="potential-scenarios"></a><span data-ttu-id="cb483-124">Возможные сценарии</span><span class="sxs-lookup"><span data-stu-id="cb483-124">Potential scenarios</span></span>

<span data-ttu-id="cb483-125">Хотя интеграция оркестратора с экземплярами контейнеров Azure еще только на начальной стадии, мы ожидаем возникновения нескольких различных сред.</span><span class="sxs-lookup"><span data-stu-id="cb483-125">While orchestrator integration with Azure Container Instances is still nascent, we anticipate that a few different environments may emerge:</span></span>

### <a name="orchestration-of-container-instances-exclusively"></a><span data-ttu-id="cb483-126">Монопольная оркестрация экземпляров контейнера</span><span class="sxs-lookup"><span data-stu-id="cb483-126">Orchestration of Container Instances exclusively</span></span>

<span data-ttu-id="cb483-127">Так как они позволяют быстро начать работу и оплачиваются по секундам, среда, которая основывается исключительно на экземплярах контейнеров Azure, предоставляет самый быстрый способ приступить к работе и обрабатывать крайне изменчивые рабочие нагрузки.</span><span class="sxs-lookup"><span data-stu-id="cb483-127">Because they start quickly and bill by the second, an environment based exclusively on Azure Container Instances offers the fastest way to get started and to deal with highly variable workloads.</span></span>

### <a name="combination-of-container-instances-and-containers-in-virtual-machines"></a><span data-ttu-id="cb483-128">Сочетание экземпляров контейнеров и контейнеров в виртуальных машинах</span><span class="sxs-lookup"><span data-stu-id="cb483-128">Combination of Container Instances and Containers in Virtual Machines</span></span>

<span data-ttu-id="cb483-129">Для длительных и стабильных рабочих нагрузок оркестрация контейнеров в кластере выделенных виртуальных машин обычно будет дешевле, чем выполнение тех же контейнеров с помощью экземпляров контейнеров.</span><span class="sxs-lookup"><span data-stu-id="cb483-129">For long-running, stable workloads, orchestrating containers in a cluster of dedicated virtual machines will typically be cheaper than running the same containers with Container Instances.</span></span> <span data-ttu-id="cb483-130">Однако экземпляры контейнеров предлагают эффективное решение для быстрого развертывания и сжатия общей емкости для обработки непредвиденных или кратковременных пиковых нагрузок в использовании.</span><span class="sxs-lookup"><span data-stu-id="cb483-130">However, Container Instances offer a great solution for quickly expanding and contracting your overall capacity to deal with unexpected or short-lived spikes in usage.</span></span> <span data-ttu-id="cb483-131">Вместо масштабирования количества виртуальных машин в кластере и развертывания дополнительных контейнеров на этих компьютерах оркестратор может просто составить расписание для добавления контейнеров с помощью экземпляров контейнеров и удалить их, когда они больше не требуются.</span><span class="sxs-lookup"><span data-stu-id="cb483-131">Rather than scaling out the number of virtual machines in your cluster, then deploying additional containers onto those machines, the orchestrator can simply schedule the additional containers using Container Instances and delete them when they're no longer needed.</span></span>

## <a name="sample-implementation-azure-container-instances-connector-for-kubernetes"></a><span data-ttu-id="cb483-132">Пример реализации: соединитель экземпляров контейнеров Azure для Kubernetes</span><span class="sxs-lookup"><span data-stu-id="cb483-132">Sample implementation: Azure Container Instances Connector for Kubernetes</span></span>

<span data-ttu-id="cb483-133">Чтобы показать, как можно интегрировать платформы оркестрации контейнеров с экземплярами контейнеров Azure, мы приступили к созданию [примера соединителя для Kubernetes][aci-connector-k8s].</span><span class="sxs-lookup"><span data-stu-id="cb483-133">To demonstrate how container orchestration platforms can integrate with Azure Container Instances, we have started building a [sample connector for Kubernetes][aci-connector-k8s].</span></span> 

<span data-ttu-id="cb483-134">Соединитель для Kubernetes имитирует [kubelet][kubelet-doc], выполняя регистрацию в качестве узла с неограниченной емкостью, а также подготавливает создание модулей [pod][pod-doc] в качестве групп контейнеров в экземплярах контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="cb483-134">The connector for Kubernetes mimics the [kubelet][kubelet-doc] by registering as a node with unlimited capacity and dispatching the creation of [pods][pod-doc] as container groups in Azure Container Instances.</span></span> 

<!-- ![ACI Connector for Kubernetes][aci-connector-k8s-gif] -->

<span data-ttu-id="cb483-135">Вы можете создать соединители для других оркестраторов, которые аналогичным образом интегрируются с примитивами платформы, чтобы сочетать возможности API оркестратора со скоростью и простотой управления контейнерами в экземплярах контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="cb483-135">Connectors for other orchestrators could be built that similarly integrated with platform primitives to combine the power of the orchestrator API with the speed and simplicity of managing containers in Azure Container Instances.</span></span>

> [!WARNING]
> <span data-ttu-id="cb483-136">Соединитель ACI для Kubernetes является *экспериментальным* и не должен использоваться в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="cb483-136">The ACI connector for Kubernetes is *experimental* and should not be used in production.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb483-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb483-137">Next steps</span></span>

<span data-ttu-id="cb483-138">Создайте свой первый контейнер с использованием экземпляров контейнеров Azure, используя [краткое руководство](container-instances-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="cb483-138">Create your first container with Azure Container Instances using the [quick start guide](container-instances-quickstart.md).</span></span>

<!-- IMAGES -->
[aci-connector-k8s-gif]: ./media/container-instances-orchestrator-relationship/aci-connector-k8s.gif

<!-- LINKS -->
[aci-connector-k8s]: https://github.com/azure/aci-connector-k8s
[kubelet-doc]: https://kubernetes.io/docs/admin/kubelet/
[pod-doc]: https://kubernetes.io/docs/concepts/workloads/pods/pod/