---
title: "aaaMonitor Azure Kubernetes кластер с Datadog | Документы Microsoft"
description: "Мониторинг кластера Kubernetes в Службе контейнеров Azure с помощью DataDog."
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="46ee6-103">Мониторинг кластера службы контейнеров Azure с помощью Datadog</span><span class="sxs-lookup"><span data-stu-id="46ee6-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46ee6-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="46ee6-104">Prerequisites</span></span>
<span data-ttu-id="46ee6-105">В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="46ee6-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="46ee6-106">Также предполагается, что имеется hello `az` Azure cli и `kubectl` установлены инструменты.</span><span class="sxs-lookup"><span data-stu-id="46ee6-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="46ee6-107">Можно проверить при наличии hello `az` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="46ee6-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="46ee6-108">Если у вас нет hello `az` средство установки приведены инструкции по [здесь](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="46ee6-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="46ee6-109">Можно проверить при наличии hello `kubectl` установить, запустив средство:</span><span class="sxs-lookup"><span data-stu-id="46ee6-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="46ee6-110">Если средство `kubectl` не установлено, выполните команду:</span><span class="sxs-lookup"><span data-stu-id="46ee6-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="46ee6-111">Datadog</span><span class="sxs-lookup"><span data-stu-id="46ee6-111">DataDog</span></span>
<span data-ttu-id="46ee6-112">Datadog представляет собой службу мониторинга, которая собирает данные мониторинга из контейнеров в кластере службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="46ee6-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="46ee6-113">Datadog имеет панель мониторинга интеграции с Docker, в которой вы можете увидеть некоторые метрики своих контейнеров.</span><span class="sxs-lookup"><span data-stu-id="46ee6-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="46ee6-114">Метрики контейнеров собраны в несколько групп: ЦП, память, сеть и ввод-вывод.</span><span class="sxs-lookup"><span data-stu-id="46ee6-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="46ee6-115">Datadog разделяет метрики по контейнерам и образам.</span><span class="sxs-lookup"><span data-stu-id="46ee6-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="46ee6-116">Необходимо сначала слишком[создать учетную запись](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="46ee6-116">You first need too[create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a><span data-ttu-id="46ee6-117">Установка агента Datadog hello с DaemonSet</span><span class="sxs-lookup"><span data-stu-id="46ee6-117">Installing hello Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="46ee6-118">DaemonSets используются Kubernetes toorun один экземпляр контейнера на каждом узле в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="46ee6-118">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="46ee6-119">Они идеально подходят для выполнения агентов мониторинга.</span><span class="sxs-lookup"><span data-stu-id="46ee6-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="46ee6-120">После входа в Datadog, можно выполнить hello [инструкции Datadog](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog агенты на кластер с помощью DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="46ee6-120">Once you have logged into Datadog, you can follow hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="46ee6-121">Заключение</span><span class="sxs-lookup"><span data-stu-id="46ee6-121">Conclusion</span></span>
<span data-ttu-id="46ee6-122">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="46ee6-122">That's it!</span></span> <span data-ttu-id="46ee6-123">Когда агенты hello функционируют, и под управлением, вы увидите данные в консоли hello через несколько минут.</span><span class="sxs-lookup"><span data-stu-id="46ee6-123">Once hello agents are up and running you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="46ee6-124">Посетите hello интеграции [kubernetes мониторинга](https://app.datadoghq.com/screen/integration/kubernetes) toosee Сводка кластера.</span><span class="sxs-lookup"><span data-stu-id="46ee6-124">You can visit hello integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee a summary of your cluster.</span></span>
