---
title: "Учебник контейнера службы aaaAzure - масштаб приложения | Документы Microsoft"
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
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="620e5-104">Масштабирование pod и инфраструктуры Kubernetes</span><span class="sxs-lookup"><span data-stu-id="620e5-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="620e5-105">Если вы смотрел hello учебники, имеется действующее Kubernetes кластера в службе контейнера Azure, и вы развернули приложение Azure голосования hello.</span><span class="sxs-lookup"><span data-stu-id="620e5-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="620e5-106">В этом учебнике, часть 5, 7, горизонтальное масштабирование hello модулей в приложение hello и повторите pod автоматического масштабирования.</span><span class="sxs-lookup"><span data-stu-id="620e5-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="620e5-107">Вы также узнаете, как количество hello tooscale toochange узлы агента ВМ Azure hello кластера емкость для размещения рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="620e5-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="620e5-108">Вам предстоят следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="620e5-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="620e5-109">масштабирование pod Kubernetes вручную;</span><span class="sxs-lookup"><span data-stu-id="620e5-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="620e5-110">Настройка модулей автомасштабирования выполнение внешнего интерфейса приложения hello</span><span class="sxs-lookup"><span data-stu-id="620e5-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="620e5-111">Масштабирование узлы Azure агентов Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="620e5-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="620e5-112">В последующих учебники hello Azure голос приложение обновляется, и Operations Management Suite настроили кластер Kubernetes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="620e5-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="620e5-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="620e5-113">Before you begin</span></span>

<span data-ttu-id="620e5-114">В предыдущих учебниках приложение было упаковано в образ контейнера, tooAzure реестра контейнера и создания кластера Kubernetes загружены этот образ.</span><span class="sxs-lookup"><span data-stu-id="620e5-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="620e5-115">приложение Hello затем была запущена на кластере Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="620e5-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="620e5-116">Если вы не были выполнены следующие действия и хотите toofollow вдоль, возвращают toohello [учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="620e5-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="620e5-117">Для этого руководства как минимум необходим кластер Kubernetes с выполняющимся приложением.</span><span class="sxs-lookup"><span data-stu-id="620e5-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="620e5-118">Масштабирование pod вручную</span><span class="sxs-lookup"><span data-stu-id="620e5-118">Manually scale pods</span></span>

<span data-ttu-id="620e5-119">До сих hello Azure голос переднего плана и экземпляр Redis были развернуты, каждый с одной реплики.</span><span class="sxs-lookup"><span data-stu-id="620e5-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="620e5-120">tooverify, запустите hello [kubectl получить](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) команды.</span><span class="sxs-lookup"><span data-stu-id="620e5-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="620e5-121">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="620e5-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="620e5-122">Вручную измените hello количество модулей в hello `azure-vote-front` развертывания с помощью hello [kubectl шкалы](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) команды.</span><span class="sxs-lookup"><span data-stu-id="620e5-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="620e5-123">В этом примере увеличивается число too5 hello.</span><span class="sxs-lookup"><span data-stu-id="620e5-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="620e5-124">Запустите [kubectl получить модулей](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify, Kubernetes создает hello модулей.</span><span class="sxs-lookup"><span data-stu-id="620e5-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="620e5-125">Прошествии минуты под управлением hello дополнительных модулей:</span><span class="sxs-lookup"><span data-stu-id="620e5-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="620e5-126">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="620e5-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="620e5-127">Автомасштабирование pod</span><span class="sxs-lookup"><span data-stu-id="620e5-127">Autoscale pods</span></span>

<span data-ttu-id="620e5-128">Поддерживает Kubernetes [автоматическое масштабирование горизонтальной pod](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello число модулей в развертывании в зависимости от загрузки ЦП или другой выбор метрик.</span><span class="sxs-lookup"><span data-stu-id="620e5-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="620e5-129">toouse hello autoscaler, ваш модулей должен иметь ЦП запросы и заданных пределов.</span><span class="sxs-lookup"><span data-stu-id="620e5-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="620e5-130">В hello `azure-vote-front` развертывания, Процессор запросов 0,25 контейнера переднего плана, ограничение на число 0,5 hello ЦП.</span><span class="sxs-lookup"><span data-stu-id="620e5-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="620e5-131">Параметры Hello иметь вид:</span><span class="sxs-lookup"><span data-stu-id="620e5-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="620e5-132">Hello следующий пример использует hello [автомасштабирования kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) команды tooautoscale hello число модулей в hello `azure-vote-front` развертывания.</span><span class="sxs-lookup"><span data-stu-id="620e5-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="620e5-133">Здесь Если загрузка ЦП превышает 50%, hello autoscaler увеличивает hello модулей tooa более 10.</span><span class="sxs-lookup"><span data-stu-id="620e5-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="620e5-134">состояние hello toosee autoscaler hello, запустите hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="620e5-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="620e5-135">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="620e5-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="620e5-136">Через несколько минут с минимальной нагрузкой на приложение hello Azure голос число hello pod реплик, которые автоматически уменьшается too3.</span><span class="sxs-lookup"><span data-stu-id="620e5-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="620e5-137">Агенты hello шкалы</span><span class="sxs-lookup"><span data-stu-id="620e5-137">Scale hello agents</span></span>

<span data-ttu-id="620e5-138">Если вы создали Kubernetes кластер с помощью команды по умолчанию в предыдущем учебнике hello, он имеет три узла агента.</span><span class="sxs-lookup"><span data-stu-id="620e5-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="620e5-139">При планировании большее или меньшее количество рабочих нагрузок контейнера в кластере hello число агентов можно настроить вручную.</span><span class="sxs-lookup"><span data-stu-id="620e5-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="620e5-140">Используйте hello [масштабировать acs az](/cli/azure/acs#scale) команду и укажите номер hello агентов hello `--new-agent-count` параметра.</span><span class="sxs-lookup"><span data-stu-id="620e5-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="620e5-141">Hello следующем примере увеличивается число hello агента too4 узлов в кластере Kubernetes hello с именем *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="620e5-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="620e5-142">Команда Hello занимает несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="620e5-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="620e5-143">Hello выходные данные команды отображаются номер hello агента узлы в значение hello `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="620e5-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="620e5-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="620e5-144">Next steps</span></span>

<span data-ttu-id="620e5-145">В этом руководстве вы использовали различные возможности масштабирования кластера Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="620e5-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="620e5-146">Были рассмотрены такие задачи:</span><span class="sxs-lookup"><span data-stu-id="620e5-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="620e5-147">масштабирование pod Kubernetes вручную;</span><span class="sxs-lookup"><span data-stu-id="620e5-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="620e5-148">Настройка модулей автомасштабирования выполнение внешнего интерфейса приложения hello</span><span class="sxs-lookup"><span data-stu-id="620e5-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="620e5-149">Масштабирование узлы Azure агентов Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="620e5-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="620e5-150">Переместить следующий учебник toolearn toohello об обновлении приложения в Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="620e5-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="620e5-151">Обновление приложения в Kubernetes</span><span class="sxs-lookup"><span data-stu-id="620e5-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

