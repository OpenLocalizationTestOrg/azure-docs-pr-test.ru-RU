---
title: "Учебник контейнера службы aaaAzure - развертывание кластера | Документы Microsoft"
description: "Руководство по Службе контейнеров Azure: развертывание кластера"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="d279f-104">Развертывание кластера Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="d279f-104">Deploy a Kubernetes cluster in Azure Container Service</span></span>

<span data-ttu-id="d279f-105">Kubernetes предоставляет распределенную платформу для контейнерных приложений.</span><span class="sxs-lookup"><span data-stu-id="d279f-105">Kubernetes provides a distributed platform for containerized applications.</span></span> <span data-ttu-id="d279f-106">Служба контейнеров Azure упрощает и убыстряет подготовку кластера Kubernetes для использования в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d279f-106">With Azure Container Service, provisioning of a production ready Kubernetes cluster is simple and quick.</span></span> <span data-ttu-id="d279f-107">В этом руководстве (часть 3 из 7) развертывается кластер Kubernetes службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="d279f-107">In this tutorial, part 3 of 7, an Azure Container Service Kubernetes cluster is deployed.</span></span> <span data-ttu-id="d279f-108">В частности, рассматриваются такие шаги:</span><span class="sxs-lookup"><span data-stu-id="d279f-108">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d279f-109">развертывание кластера ACS Kubernetes;</span><span class="sxs-lookup"><span data-stu-id="d279f-109">Deploying a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="d279f-110">Установка hello Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="d279f-110">Installation of hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="d279f-111">настройка kubectl.</span><span class="sxs-lookup"><span data-stu-id="d279f-111">Configuration of kubectl</span></span>

<span data-ttu-id="d279f-112">В последующих учебники hello Azure голос приложение развертывания кластера toohello, масштабирования, обновления и Operations Management Suite является настроенным toomonitor hello Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="d279f-112">In subsequent tutorials, hello Azure Vote application is deployed toohello cluster, scaled, updated, and Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d279f-113">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="d279f-113">Before you begin</span></span>

<span data-ttu-id="d279f-114">В предыдущих учебниках образ контейнера был создан и загружен экземпляр tooan реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="d279f-114">In previous tutorials, a container image was created and uploaded tooan Azure Container Registry instance.</span></span> <span data-ttu-id="d279f-115">Если вы не были выполнены следующие действия и хотите toofollow вдоль, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="d279f-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span>

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="d279f-116">Создание кластера Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d279f-116">Create Kubernetes cluster</span></span>

<span data-ttu-id="d279f-117">В hello [с предыдущим учебником](./container-service-tutorial-kubernetes-prepare-acr.md), группу ресурсов с именем *myResourceGroup* был создан.</span><span class="sxs-lookup"><span data-stu-id="d279f-117">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-acr.md), a resource group named *myResourceGroup* was created.</span></span> <span data-ttu-id="d279f-118">Если вы этого не сделали, создайте эту группу ресурсов сейчас.</span><span class="sxs-lookup"><span data-stu-id="d279f-118">If you have not done so, create this resource group now.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="d279f-119">Создание кластера Kubernetes в контейнере службы Azure с hello [создать acs az](/cli/azure/acs#create) команды.</span><span class="sxs-lookup"><span data-stu-id="d279f-119">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="d279f-120">Hello следующий пример создает кластер с именем *myK8sCluster* с Linux в один главный узел и три узла агента Linux.</span><span class="sxs-lookup"><span data-stu-id="d279f-120">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

<span data-ttu-id="d279f-121">Через несколько минут выполнения команды hello и в формате json возвращает сведения о развертывании hello ACS.</span><span class="sxs-lookup"><span data-stu-id="d279f-121">After several minutes, hello command completes, and returns json formatted information about hello ACS deployment.</span></span>

## <a name="install-hello-kubectl-cli"></a><span data-ttu-id="d279f-122">Установка hello kubectl CLI</span><span class="sxs-lookup"><span data-stu-id="d279f-122">Install hello kubectl CLI</span></span>

<span data-ttu-id="d279f-123">tooconnect toohello Kubernetes кластера с клиентского компьютера, используйте [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), клиент командной строки Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="d279f-123">tooconnect toohello Kubernetes cluster from your client computer, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="d279f-124">Если вы используете Azure CloudShell, установка `kubectl` уже выполнена.</span><span class="sxs-lookup"><span data-stu-id="d279f-124">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="d279f-125">Если требуется, чтобы tooinstall его локально, использовать hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) команды.</span><span class="sxs-lookup"><span data-stu-id="d279f-125">If you want tooinstall it locally, use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="d279f-126">Если выполняется macOS или Linux, может потребоваться toorun с sudo.</span><span class="sxs-lookup"><span data-stu-id="d279f-126">If running in Linux or macOS, you may need toorun with sudo.</span></span> <span data-ttu-id="d279f-127">В Windows убедитесь, что оболочка запущена от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="d279f-127">On Windows, ensure your shell has been run as administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli 
```

<span data-ttu-id="d279f-128">В Windows, — установка по умолчанию hello *c:\program files (x86)\kubectl.exe*.</span><span class="sxs-lookup"><span data-stu-id="d279f-128">On Windows, hello default installation is *c:\program files (x86)\kubectl.exe*.</span></span> <span data-ttu-id="d279f-129">Может потребоваться tooadd этот путь к файлу toohello Windows.</span><span class="sxs-lookup"><span data-stu-id="d279f-129">You may need tooadd this file toohello Windows path.</span></span> 

## <a name="connect-with-kubectl"></a><span data-ttu-id="d279f-130">Подключение с помощью kubectl</span><span class="sxs-lookup"><span data-stu-id="d279f-130">Connect with kubectl</span></span>

<span data-ttu-id="d279f-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes кластера, запустите hello [az kubernetes get-учетные данные acs](/cli/azure/acs/kubernetes#get-credentials) команды.</span><span class="sxs-lookup"><span data-stu-id="d279f-131">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

<span data-ttu-id="d279f-132">tooverify hello подключения tooyour кластера, запустите hello [kubectl получения узлов](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) команды.</span><span class="sxs-lookup"><span data-stu-id="d279f-132">tooverify hello connection tooyour cluster, run hello [kubectl get nodes](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="d279f-133">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d279f-133">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

<span data-ttu-id="d279f-134">По завершении руководства вы получите кластер ACS Kubernetes, готовый к обработке рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="d279f-134">At tutorial completion, you have an ACS Kubernetes cluster ready for workloads.</span></span> <span data-ttu-id="d279f-135">В последующих учебники приложение несколькими контейнера — развернутой toothis кластер, горизонтального масштабирования, обновления и отслеживаться.</span><span class="sxs-lookup"><span data-stu-id="d279f-135">In subsequent tutorials, a multi-container application is deployed toothis cluster, scaled out, updated, and monitored.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d279f-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d279f-136">Next steps</span></span>

<span data-ttu-id="d279f-137">В этом руководстве был развернут кластер Kubernetes Службы контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="d279f-137">In this tutorial, an Azure Container Service Kubernetes cluster was deployed.</span></span> <span data-ttu-id="d279f-138">Привет, следующие шаги были выполнены:</span><span class="sxs-lookup"><span data-stu-id="d279f-138">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d279f-139">развертывание кластера ACS Kubernetes;</span><span class="sxs-lookup"><span data-stu-id="d279f-139">Deployed a Kubernetes ACS cluster</span></span>
> * <span data-ttu-id="d279f-140">Установленные hello Kubernetes CLI (kubectl)</span><span class="sxs-lookup"><span data-stu-id="d279f-140">Installed hello Kubernetes CLI (kubectl)</span></span>
> * <span data-ttu-id="d279f-141">настройка kubectl.</span><span class="sxs-lookup"><span data-stu-id="d279f-141">Configured kubectl</span></span>

<span data-ttu-id="d279f-142">Переместить следующий учебник toolearn toohello о запуске приложения на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="d279f-142">Advance toohello next tutorial toolearn about running application on hello cluster.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d279f-143">Запуск приложений в Kubernetes</span><span class="sxs-lookup"><span data-stu-id="d279f-143">Deploy application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-deploy-application.md)
