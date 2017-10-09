---
title: "Учебник контейнера службы aaaAzure - монитор Kubernetes | Документы Microsoft"
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="702c2-104">Мониторинг кластера Kubernetes с помощью Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="702c2-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="702c2-105">Мониторинг кластера Kubernetes и контейнеров крайне важен, особенно в том случае, если вы управляете масштабируемым рабочим кластером с несколькими приложениями.</span><span class="sxs-lookup"><span data-stu-id="702c2-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="702c2-106">Вы можете воспользоваться преимуществами нескольких решений для мониторинга Kubernetes от корпорации Майкрософт или других поставщиков.</span><span class="sxs-lookup"><span data-stu-id="702c2-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="702c2-107">В этом учебнике отслеживать Kubernetes кластера с помощью решения контейнеры hello в [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Облачное решение управления ИТ корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="702c2-107">In this tutorial, you monitor your Kubernetes cluster by using hello Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="702c2-108">(hello решений OMS контейнеры находится в предварительной версии).</span><span class="sxs-lookup"><span data-stu-id="702c2-108">(hello OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="702c2-109">В этом учебнике, часть 7 семь, приведены hello следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="702c2-109">This tutorial, part seven of seven, covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="702c2-110">Получение параметров рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="702c2-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="702c2-111">Настроить агенты OMS на узлах Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="702c2-111">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="702c2-112">Доступ к данным мониторинга на портале OMS hello или портал Azure</span><span class="sxs-lookup"><span data-stu-id="702c2-112">Access monitoring information in hello OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="702c2-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="702c2-113">Before you begin</span></span>

<span data-ttu-id="702c2-114">В предыдущих учебниках приложение было упаковано в образах контейнеров, эти образы, отправленном tooAzure реестра контейнера и создан Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="702c2-114">In previous tutorials, an application was packaged into container images, these images uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="702c2-115">Если вы не были выполнены следующие действия и хотите toofollow вдоль, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="702c2-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="702c2-116">Для этого руководства требуется по крайней мере кластер Kubernetes с узлами агентов Linux и учетная запись OMS.</span><span class="sxs-lookup"><span data-stu-id="702c2-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="702c2-117">При необходимости зарегистрируйтесь для получения [бесплатной пробной версии OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="702c2-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="702c2-118">Получение параметров рабочей области</span><span class="sxs-lookup"><span data-stu-id="702c2-118">Get Workspace settings</span></span>

<span data-ttu-id="702c2-119">При доступе к hello [портал OMS](https://mms.microsoft.com), перейдите в слишком**параметры** > **подключенные источники** > **серверы Linux**.</span><span class="sxs-lookup"><span data-stu-id="702c2-119">When you can access hello [OMS portal](https://mms.microsoft.com), go too**Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="702c2-120">Здесь можно найти hello *идентификатор рабочей области* и основных или дополнительных *ключ рабочей области*.</span><span class="sxs-lookup"><span data-stu-id="702c2-120">There, you can find hello *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="702c2-121">Запишите эти значения, которые необходимо tooset копирование агенты OMS в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="702c2-121">Take note of these values, which you need tooset up OMS agents on hello cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="702c2-122">Настройка агентов OMS</span><span class="sxs-lookup"><span data-stu-id="702c2-122">Set up OMS agents</span></span>

<span data-ttu-id="702c2-123">Вот tooset файл YAML копирование OMS агенты на узлах кластера hello Linux.</span><span class="sxs-lookup"><span data-stu-id="702c2-123">Here is a YAML file tooset up OMS agents on hello Linux cluster nodes.</span></span> <span data-ttu-id="702c2-124">Он создает [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) Kubernetes, который запускает идентичный модуль на каждом узле кластера.</span><span class="sxs-lookup"><span data-stu-id="702c2-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="702c2-125">Hello ресурсов DaemonSet идеально подходит для развертывания агента мониторинга.</span><span class="sxs-lookup"><span data-stu-id="702c2-125">hello DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="702c2-126">Сохраните следующий текстовый файл tooa с именем hello `oms-daemonset.yaml`и замените значения заполнителей hello для *myWorkspaceID* и *myWorkspaceKey* с идентификатор рабочей области OMS и ключа.</span><span class="sxs-lookup"><span data-stu-id="702c2-126">Save hello following text tooa file named `oms-daemonset.yaml`, and replace hello placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="702c2-127">(В рабочей среде можно закодировать эти значения в виде секретов.)</span><span class="sxs-lookup"><span data-stu-id="702c2-127">(In production, you can encode these values as secrets.)</span></span>

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

<span data-ttu-id="702c2-128">Создайте hello DaemonSet с hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="702c2-128">Create hello DaemonSet with hello following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="702c2-129">выполните для этого hello создания DaemonSet toosee:</span><span class="sxs-lookup"><span data-stu-id="702c2-129">toosee that hello DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="702c2-130">Выходные данные выглядят аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="702c2-130">Output is similar toohello following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="702c2-131">После запуска агентов hello он занимает несколько минут для OMS tooingest и обрабатывающие данные hello.</span><span class="sxs-lookup"><span data-stu-id="702c2-131">After hello agents are running, it takes several minutes for OMS tooingest and process hello data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="702c2-132">Доступ к данным мониторинга</span><span class="sxs-lookup"><span data-stu-id="702c2-132">Access monitoring data</span></span>

<span data-ttu-id="702c2-133">Просматривать и анализировать данные мониторинга с hello контейнера OMS hello [решения контейнера](../../log-analytics/log-analytics-containers.md) в портал OMS hello или hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="702c2-133">View and analyze hello OMS container monitoring data with hello [Container solution](../../log-analytics/log-analytics-containers.md) in either hello OMS portal or hello Azure portal.</span></span> 

<span data-ttu-id="702c2-134">tooinstall hello контейнера решения с помощью hello [портал OMS](https://mms.microsoft.com), перейдите в слишком**коллекции решений**.</span><span class="sxs-lookup"><span data-stu-id="702c2-134">tooinstall hello Container solution using hello [OMS portal](https://mms.microsoft.com), go too**Solutions Gallery**.</span></span> <span data-ttu-id="702c2-135">Затем добавьте **решение "Контейнер"**.</span><span class="sxs-lookup"><span data-stu-id="702c2-135">Then add **Container Solution**.</span></span> <span data-ttu-id="702c2-136">Кроме того, добавить решение контейнеры hello из hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="702c2-136">Alternatively, add hello Containers solution from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="702c2-137">На портале OMS hello, искать **контейнеры** сводки плитки на панели мониторинга OMS hello.</span><span class="sxs-lookup"><span data-stu-id="702c2-137">In hello OMS portal, look for a **Containers** summary tile on hello OMS dashboard.</span></span> <span data-ttu-id="702c2-138">Щелкните плитку hello Дополнительные сведения, включая: события контейнера, ошибки, состояние, изображение инвентаризации и использования ЦП и памяти.</span><span class="sxs-lookup"><span data-stu-id="702c2-138">Click hello tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="702c2-139">Более детализированные сведения можно получить, щелкнув строку на одной из плиток или выполнив [поиск по журналам](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="702c2-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Панель мониторинга "Контейнеры" на портале OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="702c2-141">Аналогичным образом в hello портал Azure, перейдите слишком**анализа журналов** и выберите имя рабочей области.</span><span class="sxs-lookup"><span data-stu-id="702c2-141">Similarly, in hello Azure portal, go too**Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="702c2-142">toosee hello **контейнеры** Плитка сводки, щелкните **решения** > **контейнеры**.</span><span class="sxs-lookup"><span data-stu-id="702c2-142">toosee hello **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="702c2-143">сведения о toosee, щелкните плитку hello.</span><span class="sxs-lookup"><span data-stu-id="702c2-143">toosee details, click hello tile.</span></span>

<span data-ttu-id="702c2-144">В разделе hello [документации Azure Log Analytics](../../log-analytics/index.md) подробное руководство по запросу и анализ данных наблюдения.</span><span class="sxs-lookup"><span data-stu-id="702c2-144">See hello [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="702c2-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="702c2-145">Next steps</span></span>

<span data-ttu-id="702c2-146">В этом руководстве вы выполнили мониторинг кластера Kubernetes с помощью OMS,</span><span class="sxs-lookup"><span data-stu-id="702c2-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="702c2-147">в частности такие задачи:</span><span class="sxs-lookup"><span data-stu-id="702c2-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="702c2-148">Получение параметров рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="702c2-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="702c2-149">Настроить агенты OMS на узлах Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="702c2-149">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="702c2-150">Доступ к данным мониторинга на портале OMS hello или портал Azure</span><span class="sxs-lookup"><span data-stu-id="702c2-150">Access monitoring information in hello OMS portal or Azure portal</span></span>


<span data-ttu-id="702c2-151">Выполните этот toosee ссылку готовые примеры скриптов для службы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="702c2-151">Follow this link toosee pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="702c2-152">Примеры Azure CLI для службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="702c2-152">Azure Container Service script samples</span></span>](cli-samples.md)
