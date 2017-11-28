---
title: "Руководство по службе контейнеров Azure — мониторинг Kubernetes | Документация Майкрософт"
description: "Руководство по службе контейнеров Azure — мониторинг Kubernetes с помощью Microsoft Operations Management Suite (OMS)"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: f4d09973ada8e3cd0ff2b00d20aca979e834cd7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="f9f7f-104">Мониторинг кластера Kubernetes с помощью Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="f9f7f-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="f9f7f-105">Мониторинг кластера Kubernetes и контейнеров крайне важен, особенно в том случае, если вы управляете масштабируемым рабочим кластером с несколькими приложениями.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="f9f7f-106">Вы можете воспользоваться преимуществами нескольких решений для мониторинга Kubernetes от корпорации Майкрософт или других поставщиков.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="f9f7f-107">В этом руководстве выполняется мониторинг кластера Kubernetes с помощью решения "Контейнеры" в [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md). Это облачное решение Майкрософт для управления ИТ-средой.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-107">In this tutorial, you monitor your Kubernetes cluster by using the Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="f9f7f-108">(Решение "Контейнеры" OMS находится в предварительной версии.)</span><span class="sxs-lookup"><span data-stu-id="f9f7f-108">(The OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="f9f7f-109">В этом руководстве, (часть 7 из 7) рассматриваются следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="f9f7f-109">This tutorial, part seven of seven, covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9f7f-110">Получение параметров рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="f9f7f-111">Настройка агентов OMS на узлах Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-111">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="f9f7f-112">Доступ к данным мониторинга на портале OMS или на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-112">Access monitoring information in the OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f9f7f-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="f9f7f-113">Before you begin</span></span>

<span data-ttu-id="f9f7f-114">В предыдущих руководствах приложение было упаковано в образы контейнеров, образы были отправлены в реестр контейнеров Azure и был создан кластер Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-114">In previous tutorials, an application was packaged into container images, these images uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="f9f7f-115">Если вы не выполнили эти действия, вы можете ознакомиться со статьей [Создание образов контейнеров для использования со службой контейнеров Azure](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="f9f7f-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="f9f7f-116">Для этого руководства требуется по крайней мере кластер Kubernetes с узлами агентов Linux и учетная запись OMS.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="f9f7f-117">При необходимости зарегистрируйтесь для получения [бесплатной пробной версии OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="f9f7f-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="f9f7f-118">Получение параметров рабочей области</span><span class="sxs-lookup"><span data-stu-id="f9f7f-118">Get Workspace settings</span></span>

<span data-ttu-id="f9f7f-119">На [портале OMS](https://mms.microsoft.com) последовательно выберите **Параметры** > **Подключенные источники** > **Серверы Linux**.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-119">When you can access the [OMS portal](https://mms.microsoft.com), go to **Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="f9f7f-120">Здесь можно найти *идентификатор рабочей области*, а также основной и дополнительный *ключ рабочей области*.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-120">There, you can find the *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="f9f7f-121">Запишите эти значения, так как они понадобятся для настройки агентов OMS в кластере.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-121">Take note of these values, which you need to set up OMS agents on the cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="f9f7f-122">Настройка агентов OMS</span><span class="sxs-lookup"><span data-stu-id="f9f7f-122">Set up OMS agents</span></span>

<span data-ttu-id="f9f7f-123">Ниже приведен файл YAML для настройки агентов OMS на узлах кластера Linux.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-123">Here is a YAML file to set up OMS agents on the Linux cluster nodes.</span></span> <span data-ttu-id="f9f7f-124">Он создает [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) Kubernetes, который запускает идентичный модуль на каждом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="f9f7f-125">Ресурс DaemonSet идеально подходит для развертывания агента мониторинга.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-125">The DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="f9f7f-126">Сохраните следующий текст в файл с именем `oms-daemonset.yaml` и замените значения заполнителей *myWorkspaceID* и *myWorkspaceKey* на идентификатор и ключ рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-126">Save the following text to a file named `oms-daemonset.yaml`, and replace the placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="f9f7f-127">(В рабочей среде можно закодировать эти значения в виде секретов.)</span><span class="sxs-lookup"><span data-stu-id="f9f7f-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="f9f7f-128">Создайте DaemonSet с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="f9f7f-128">Create the DaemonSet with the following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="f9f7f-129">Чтобы убедиться, что DaemonSet был создан, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f9f7f-129">To see that the DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="f9f7f-130">Результат аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="f9f7f-130">Output is similar to the following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="f9f7f-131">Через несколько минут после запуска агентов OMS начнет принимать и обрабатывать данные.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-131">After the agents are running, it takes several minutes for OMS to ingest and process the data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="f9f7f-132">Доступ к данным мониторинга</span><span class="sxs-lookup"><span data-stu-id="f9f7f-132">Access monitoring data</span></span>

<span data-ttu-id="f9f7f-133">Просматривать и анализировать данные мониторинга контейнера OMS можно с помощью [решения "Контейнер"](../../log-analytics/log-analytics-containers.md) на портале Azure или на портале OMS.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-133">View and analyze the OMS container monitoring data with the [Container solution](../../log-analytics/log-analytics-containers.md) in either the OMS portal or the Azure portal.</span></span> 

<span data-ttu-id="f9f7f-134">Для установки решения "Контейнер" с помощью [портала OMS](https://mms.microsoft.com) перейдите в **Коллекция решений**.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-134">To install the Container solution using the [OMS portal](https://mms.microsoft.com), go to **Solutions Gallery**.</span></span> <span data-ttu-id="f9f7f-135">Затем добавьте **решение "Контейнер"**.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-135">Then add **Container Solution**.</span></span> <span data-ttu-id="f9f7f-136">Кроме того, можно добавить решение "Контейнеры" из [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="f9f7f-136">Alternatively, add the Containers solution from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="f9f7f-137">На портале OMS найдите плитку сводки **Контейнеры** на панели мониторинга OMS.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-137">In the OMS portal, look for a **Containers** summary tile on the OMS dashboard.</span></span> <span data-ttu-id="f9f7f-138">Щелкните плитку, чтобы просмотреть дополнительные сведения, в том числе события контейнера, ошибки, состояние, список образов, использование ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-138">Click the tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="f9f7f-139">Более детализированные сведения можно получить, щелкнув строку на одной из плиток или выполнив [поиск по журналам](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="f9f7f-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Панель мониторинга "Контейнеры" на портале OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="f9f7f-141">На портале Azure перейдите к **Log Analytics** и выберите имя рабочей области.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-141">Similarly, in the Azure portal, go to **Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="f9f7f-142">Чтобы увидеть плитку сводки **Контейнеры**, щелкните **Решения** > **Контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-142">To see the **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="f9f7f-143">Чтобы просмотреть сведения, щелкните плитку.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-143">To see details, click the tile.</span></span>

<span data-ttu-id="f9f7f-144">Подробные сведения о создании запросов и анализе данных мониторинга см. в [документации по Log Analytics](../../log-analytics/index.md).</span><span class="sxs-lookup"><span data-stu-id="f9f7f-144">See the [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9f7f-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9f7f-145">Next steps</span></span>

<span data-ttu-id="f9f7f-146">В этом руководстве вы выполнили мониторинг кластера Kubernetes с помощью OMS,</span><span class="sxs-lookup"><span data-stu-id="f9f7f-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="f9f7f-147">в частности такие задачи:</span><span class="sxs-lookup"><span data-stu-id="f9f7f-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f9f7f-148">Получение параметров рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="f9f7f-149">Настройка агентов OMS на узлах Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-149">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="f9f7f-150">Доступ к данным мониторинга на портале OMS или на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-150">Access monitoring information in the OMS portal or Azure portal</span></span>


<span data-ttu-id="f9f7f-151">Чтобы увидеть предварительно созданные примеры сценариев для службы контейнеров, перейдите по ссылке ниже.</span><span class="sxs-lookup"><span data-stu-id="f9f7f-151">Follow this link to see pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9f7f-152">Примеры Azure CLI для службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="f9f7f-152">Azure Container Service script samples</span></span>](cli-samples.md)
