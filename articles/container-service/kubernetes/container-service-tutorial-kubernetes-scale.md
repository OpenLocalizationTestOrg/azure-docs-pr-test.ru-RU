---
title: "Руководство по Службе контейнеров Azure: масштабирование приложения | Документация Майкрософт"
description: "Руководство по Службе контейнеров Azure: масштабирование приложения"
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
ms.openlocfilehash: 62e70e34d06f5220734ff85c70a0c9b475f9579b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="5c06b-104">Масштабирование pod и инфраструктуры Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5c06b-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="5c06b-105">Если вы выполнили инструкции в руководствах, то у вас имеется работающий кластер Kubernetes в Службе контейнеров Azure и вы развернули в нем приложение Vote Azure.</span><span class="sxs-lookup"><span data-stu-id="5c06b-105">If you've been following the tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed the Azure Voting app.</span></span> 

<span data-ttu-id="5c06b-106">В этом руководстве (часть 5 из 7) описывается масштабирование pod, содержащихся в приложении, и их автомасштабирование.</span><span class="sxs-lookup"><span data-stu-id="5c06b-106">In this tutorial, part five of seven, you scale out the pods in the app and try pod autoscaling.</span></span> <span data-ttu-id="5c06b-107">Вы также узнаете, как масштабировать количество узлов агентов виртуальной машины Azure, чтобы менять емкость кластера для размещения рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="5c06b-107">You also learn how to scale the number of Azure VM agent nodes to change the cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="5c06b-108">Вам предстоят следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="5c06b-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5c06b-109">масштабирование pod Kubernetes вручную;</span><span class="sxs-lookup"><span data-stu-id="5c06b-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="5c06b-110">настройка автомасштабирования pod, в которых выполняется интерфейсная часть приложения;</span><span class="sxs-lookup"><span data-stu-id="5c06b-110">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="5c06b-111">масштабирование узлов агентов Kubernetes в Azure.</span><span class="sxs-lookup"><span data-stu-id="5c06b-111">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="5c06b-112">В последующих руководствах выполняется обновление приложения Vote Azure, а также настройка Operations Management Suite для отслеживания кластера Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5c06b-112">In subsequent tutorials, the Azure Vote application is updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5c06b-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="5c06b-113">Before you begin</span></span>

<span data-ttu-id="5c06b-114">В предыдущих руководствах приложение было упаковано в образ контейнера, этот образ был передан в реестр контейнеров Azure и был создан кластер Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5c06b-114">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="5c06b-115">Затем приложение было запущено в кластере Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5c06b-115">The application was then run on the Kubernetes cluster.</span></span> <span data-ttu-id="5c06b-116">Если вы не выполнили эти действия, то можете ознакомиться со статьей [Создание образов контейнеров для использования со службой контейнеров Azure](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="5c06b-116">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="5c06b-117">Для этого руководства как минимум необходим кластер Kubernetes с выполняющимся приложением.</span><span class="sxs-lookup"><span data-stu-id="5c06b-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="5c06b-118">Масштабирование pod вручную</span><span class="sxs-lookup"><span data-stu-id="5c06b-118">Manually scale pods</span></span>

<span data-ttu-id="5c06b-119">К настоящему моменту было развернуто по отдельной реплике внешнего приложения Vote Azure и экземпляра Redis.</span><span class="sxs-lookup"><span data-stu-id="5c06b-119">Thus far, the Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="5c06b-120">Чтобы проверить это, выполните команду [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="5c06b-120">To verify, run the [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="5c06b-121">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5c06b-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="5c06b-122">Вручную измените число pod в развертывании `azure-vote-front`, выполнив команду [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale).</span><span class="sxs-lookup"><span data-stu-id="5c06b-122">Manually change the number of pods in the `azure-vote-front` deployment using the [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="5c06b-123">В этом примере их число увеличивается до 5.</span><span class="sxs-lookup"><span data-stu-id="5c06b-123">This example increases the number to 5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="5c06b-124">Выполните команду [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get), чтобы убедиться, что Kubernetes создает новые pod.</span><span class="sxs-lookup"><span data-stu-id="5c06b-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) to verify that Kubernetes is creating the pods.</span></span> <span data-ttu-id="5c06b-125">Дополнительные pod будут запущены примерно через минуту.</span><span class="sxs-lookup"><span data-stu-id="5c06b-125">After a minute or so, the additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="5c06b-126">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5c06b-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="5c06b-127">Автомасштабирование pod</span><span class="sxs-lookup"><span data-stu-id="5c06b-127">Autoscale pods</span></span>

<span data-ttu-id="5c06b-128">Kubernetes поддерживает [горизонтальное автомасштабирование pod](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) для изменения числа pod в развертывании в зависимости от использования ЦП или других выбранных метрик.</span><span class="sxs-lookup"><span data-stu-id="5c06b-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="5c06b-129">Чтобы использовать инструмент автомасштабирования, для ваших pod необходимо определить запросы и лимиты ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="5c06b-129">To use the autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="5c06b-130">В развертывании `azure-vote-front` каждый контейнер внешнего приложения запрашивает 0,25 ресурсов ЦП с лимитом в 0,5 ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="5c06b-130">In the `azure-vote-front` deployment, the front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="5c06b-131">Параметры имеют следующий вид.</span><span class="sxs-lookup"><span data-stu-id="5c06b-131">The settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="5c06b-132">В следующем примере используется команда [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) для автомасштабирования числа модулей в развертывании `azure-vote-front`.</span><span class="sxs-lookup"><span data-stu-id="5c06b-132">The following example uses the [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command to autoscale the number of pods in the `azure-vote-front` deployment.</span></span> <span data-ttu-id="5c06b-133">Если использование ЦП превышает 50 %, то инструмент автомасштабирования увеличивает число pod максимум до 10.</span><span class="sxs-lookup"><span data-stu-id="5c06b-133">Here, if CPU utilization exceeds 50%, the autoscaler increases the pods to a maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="5c06b-134">Выполните следующую команду, чтобы просмотреть состояние инструмента автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="5c06b-134">To see the status of the autoscaler, run the following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="5c06b-135">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="5c06b-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="5c06b-136">Через несколько минут минимальной нагрузки на приложение Vote Azure число реплик pod автоматически уменьшится до 3.</span><span class="sxs-lookup"><span data-stu-id="5c06b-136">After a few minutes, with minimal load on the Azure Vote app, the number of pod replicas decreases automatically to 3.</span></span>

## <a name="scale-the-agents"></a><span data-ttu-id="5c06b-137">Масштабирование агентов</span><span class="sxs-lookup"><span data-stu-id="5c06b-137">Scale the agents</span></span>

<span data-ttu-id="5c06b-138">Если вы создали кластер Kubernetes с помощью команд по умолчанию в предыдущем руководстве, то у него три узла агентов.</span><span class="sxs-lookup"><span data-stu-id="5c06b-138">If you created your Kubernetes cluster using default commands in the previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="5c06b-139">Если вы планируете увеличение или уменьшение рабочих нагрузок контейнеров в кластере, то можете соответствующим образом изменить число агентов вручную.</span><span class="sxs-lookup"><span data-stu-id="5c06b-139">You can adjust the number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="5c06b-140">Выполните команду [az acs scale](/cli/azure/acs#scale), указав количество агентов с помощью параметра `--new-agent-count`.</span><span class="sxs-lookup"><span data-stu-id="5c06b-140">Use the [az acs scale](/cli/azure/acs#scale) command, and specify the number of agents with the `--new-agent-count` parameter.</span></span>

<span data-ttu-id="5c06b-141">В следующем примере в кластере Kubernetes *myK8sCluster* число узлов агентов увеличивается до 4.</span><span class="sxs-lookup"><span data-stu-id="5c06b-141">The following example increases the number of agent nodes to 4 in the Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="5c06b-142">Для выполнения этой команды требуется несколько минут.</span><span class="sxs-lookup"><span data-stu-id="5c06b-142">The command takes a couple of minutes to complete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="5c06b-143">Выходные данные команды содержат число узлов агентов в значении `agentPoolProfiles:count`.</span><span class="sxs-lookup"><span data-stu-id="5c06b-143">The command output shows the number of agent nodes in the value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="5c06b-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5c06b-144">Next steps</span></span>

<span data-ttu-id="5c06b-145">В этом руководстве вы использовали различные возможности масштабирования кластера Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5c06b-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="5c06b-146">Были рассмотрены такие задачи:</span><span class="sxs-lookup"><span data-stu-id="5c06b-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5c06b-147">масштабирование pod Kubernetes вручную;</span><span class="sxs-lookup"><span data-stu-id="5c06b-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="5c06b-148">настройка автомасштабирования pod, в которых выполняется интерфейсная часть приложения;</span><span class="sxs-lookup"><span data-stu-id="5c06b-148">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="5c06b-149">масштабирование узлов агентов Kubernetes в Azure.</span><span class="sxs-lookup"><span data-stu-id="5c06b-149">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="5c06b-150">Перейдите к следующему руководству, чтобы узнать об обновлении приложения в Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="5c06b-150">Advance to the next tutorial to learn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5c06b-151">Обновление приложения в Kubernetes</span><span class="sxs-lookup"><span data-stu-id="5c06b-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

