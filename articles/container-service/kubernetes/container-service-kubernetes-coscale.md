---
title: "aaaMonitor Kubernetes Azure кластер с CoScale | Документы Microsoft"
description: "Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="d1d5b-103">Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью CoScale</span><span class="sxs-lookup"><span data-stu-id="d1d5b-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="d1d5b-104">В этой статье мы покажем, как toodeploy hello [CoScale](https://www.coscale.com/) toomonitor агента, все узлы и контейнеры в вашей Kubernetes кластера в службе контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="d1d5b-105">Для работы с этой конфигурацией вам понадобится учетная запись с CoScale.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="d1d5b-106">Сведения о CoScale</span><span class="sxs-lookup"><span data-stu-id="d1d5b-106">About CoScale</span></span> 

<span data-ttu-id="d1d5b-107">CoScale представляет собой платформу для мониторинга, собирающую метрики и события из всех контейнеров на нескольких платформах оркестрации.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="d1d5b-108">CoScale обеспечивает комплексный мониторинг для сред Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="d1d5b-109">Он предоставляет визуализации и анализа для всех слоев в стек hello: hello ОС, Kubernetes, Docker и приложения, работающие на контейнеры.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="d1d5b-110">CoScale предоставляет несколько встроенных панелей мониторинга и он имеет операторы tooallow обнаружение аномалий встроенные и проблем инфраструктуры и приложений toofind разработчикам быстро.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![Пользовательский интерфейс CoScale](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="d1d5b-112">Как показано в этой статье, можно установить агенты на toorun кластера Kubernetes CoScale как решение SaaS.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="d1d5b-113">Если требуется tookeep данных на месте, CoScale также доступна для локальной установки.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d1d5b-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d1d5b-114">Prerequisites</span></span>

<span data-ttu-id="d1d5b-115">Необходимо сначала слишком[создать учетную запись CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="d1d5b-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="d1d5b-116">В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d1d5b-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="d1d5b-117">Также предполагается, что имеется hello `az` Azure CLI и `kubectl` установлены инструменты.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="d1d5b-118">Можно проверить при наличии hello `az` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="d1d5b-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="d1d5b-119">Если у вас нет hello `az` средство установки приведены инструкции по [здесь](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d1d5b-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="d1d5b-120">Можно проверить при наличии hello `kubectl` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="d1d5b-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="d1d5b-121">Если средство `kubectl` не установлено, выполните команду:</span><span class="sxs-lookup"><span data-stu-id="d1d5b-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="d1d5b-122">Установка агента CoScale hello с DaemonSet</span><span class="sxs-lookup"><span data-stu-id="d1d5b-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="d1d5b-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) , используемые Kubernetes toorun один экземпляр контейнера на каждом узле в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="d1d5b-124">Они идеально подходит для выполнения агентов мониторинга, например агент CoScale hello.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="d1d5b-125">После входа в tooCoScale go toohello [агент страница](https://app.coscale.com/) tooinstall CoScale агенты на кластер с помощью DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="d1d5b-126">Hello CoScale пользовательского интерфейса предоставляет toocreate действия интерактивная конфигурации агента и начать наблюдение за полный Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![Конфигурация агента CoScale](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="d1d5b-128">агент hello toostart hello кластере, выполните команду предоставленный hello:</span><span class="sxs-lookup"><span data-stu-id="d1d5b-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Запуск агента CoScale hello](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="d1d5b-130">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="d1d5b-130">That's it!</span></span> <span data-ttu-id="d1d5b-131">После hello агенты запущены и работают, вы увидите данные в консоли hello через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="d1d5b-132">Посетите hello [агент страница](https://app.coscale.com/) toosee сводку по кластеру, выполнять дополнительные действия по настройке и в разделе панелей мониторинга, например hello **Kubernetes кластера Обзор**.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Основные сведения о кластере Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="d1d5b-134">агент CoScale Hello автоматически развертываются на новых компьютерах в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="d1d5b-135">Hello агента автоматически обновляется при выпуске новой версии.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d1d5b-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d1d5b-136">Next steps</span></span>

<span data-ttu-id="d1d5b-137">В разделе hello [CoScale документации](http://docs.coscale.com/) и [блог](https://www.coscale.com/blog) для получения дополнительных сведения о CoScale мониторинг решений.</span><span class="sxs-lookup"><span data-stu-id="d1d5b-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

