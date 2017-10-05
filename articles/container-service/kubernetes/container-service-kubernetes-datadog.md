---
title: "Мониторинг кластера Kubernetes в Azure с помощью DataDog | Документация Майкрософт"
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
ms.openlocfilehash: 40b34457447a8f80d8cdf77579750e0c42df22d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="b040c-103">Мониторинг кластера службы контейнеров Azure с помощью Datadog</span><span class="sxs-lookup"><span data-stu-id="b040c-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b040c-104">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b040c-104">Prerequisites</span></span>
<span data-ttu-id="b040c-105">В этом пошаговом руководстве предполагается, что вы [создали кластер Kubernetes с помощью службы контейнеров Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="b040c-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="b040c-106">Также предполагается, что у вас установлен интерфейс командной строки Azure `az` и инструменты `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="b040c-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="b040c-107">Чтобы проверить наличие средства `az`, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="b040c-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="b040c-108">Если средство `az` не установлено, следуйте инструкциям, приведенным [здесь](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="b040c-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="b040c-109">Чтобы проверить наличие средства `kubectl`, выполните такую команду:</span><span class="sxs-lookup"><span data-stu-id="b040c-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="b040c-110">Если средство `kubectl` не установлено, выполните команду:</span><span class="sxs-lookup"><span data-stu-id="b040c-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="b040c-111">Datadog</span><span class="sxs-lookup"><span data-stu-id="b040c-111">DataDog</span></span>
<span data-ttu-id="b040c-112">Datadog представляет собой службу мониторинга, которая собирает данные мониторинга из контейнеров в кластере службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="b040c-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="b040c-113">Datadog имеет панель мониторинга интеграции с Docker, в которой вы можете увидеть некоторые метрики своих контейнеров.</span><span class="sxs-lookup"><span data-stu-id="b040c-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="b040c-114">Метрики контейнеров собраны в несколько групп: ЦП, память, сеть и ввод-вывод.</span><span class="sxs-lookup"><span data-stu-id="b040c-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="b040c-115">Datadog разделяет метрики по контейнерам и образам.</span><span class="sxs-lookup"><span data-stu-id="b040c-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="b040c-116">Необходимо сначала [создать учетную запись](https://www.datadoghq.com/lpg/).</span><span class="sxs-lookup"><span data-stu-id="b040c-116">You first need to [create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-the-datadog-agent-with-a-daemonset"></a><span data-ttu-id="b040c-117">Установка агента DataDog с помощью DaemonSet</span><span class="sxs-lookup"><span data-stu-id="b040c-117">Installing the Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="b040c-118">Kubernetes использует наборы DaemonSet для выполнения отдельного экземпляра контейнера на каждом узле в кластере.</span><span class="sxs-lookup"><span data-stu-id="b040c-118">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="b040c-119">Они идеально подходят для выполнения агентов мониторинга.</span><span class="sxs-lookup"><span data-stu-id="b040c-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="b040c-120">После входа в DataDog можно следовать [инструкциям к DataDog](https://app.datadoghq.com/account/settings#agent/kubernetes), чтобы установить на кластер агенты DataDog с помощью DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="b040c-120">Once you have logged into Datadog, you can follow the [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) to install Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="b040c-121">Заключение</span><span class="sxs-lookup"><span data-stu-id="b040c-121">Conclusion</span></span>
<span data-ttu-id="b040c-122">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="b040c-122">That's it!</span></span> <span data-ttu-id="b040c-123">Через несколько минут после того, как агенты будут запущены и начнут работать, вы увидите данные в консоли.</span><span class="sxs-lookup"><span data-stu-id="b040c-123">Once the agents are up and running you should see data in the console in a few minutes.</span></span> <span data-ttu-id="b040c-124">Вы можете посетить интегрированную [панель мониторинга Kubernetes](https://app.datadoghq.com/screen/integration/kubernetes), чтобы просмотреть сводку по кластеру.</span><span class="sxs-lookup"><span data-stu-id="b040c-124">You can visit the integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) to see a summary of your cluster.</span></span>
