---
title: "aaaQuickstart - Azure Kubernetes кластера для Windows | Документы Microsoft"
description: "Быстро Узнайте toocreate Kubernetes кластера для контейнеров Windows в службе контейнера Azure с hello Azure CLI."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="33f21-103">Кластер Azure Kubernetes для Windows | Документация Майкрософт</span><span class="sxs-lookup"><span data-stu-id="33f21-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="33f21-104">Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.</span><span class="sxs-lookup"><span data-stu-id="33f21-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="33f21-105">В этом руководстве рассматривается использование hello Azure CLI toodeploy [Kubernetes](https://kubernetes.io/docs/home/) кластер в [контейнера службы Azure](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="33f21-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="33f21-106">После развертывания кластера hello tooit соединены hello Kubernetes `kubectl` средство командной строки и развертывание первого контейнера Windows.</span><span class="sxs-lookup"><span data-stu-id="33f21-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="33f21-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="33f21-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="33f21-108">Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="33f21-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="33f21-109">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="33f21-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="33f21-110">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="33f21-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="33f21-111">Поддержка контейнеров Windows для Kubernetes в Службе контейнеров Azure реализована в режиме предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="33f21-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="33f21-112">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="33f21-112">Create a resource group</span></span>

<span data-ttu-id="33f21-113">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="33f21-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="33f21-114">Группа ресурсов Azure — это логическая группа, в которой выполняется развертывание и администрирование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="33f21-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="33f21-115">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="33f21-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="33f21-116">Создание кластера Kubernetes</span><span class="sxs-lookup"><span data-stu-id="33f21-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="33f21-117">Создание кластера Kubernetes в контейнере службы Azure с hello [создать acs az](/cli/azure/acs#create) команды.</span><span class="sxs-lookup"><span data-stu-id="33f21-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="33f21-118">Hello следующий пример создает кластер с именем *myK8sCluster* с Linux в один главный узел с двумя узлами агент Windows.</span><span class="sxs-lookup"><span data-stu-id="33f21-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="33f21-119">В этом примере создается SSH master Linux toohello tooconnect необходимые ключи.</span><span class="sxs-lookup"><span data-stu-id="33f21-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="33f21-120">В этом примере используется *azureuser* имени пользователя с правами администратора и *myPassword12* hello паролем на узлах Windows hello.</span><span class="sxs-lookup"><span data-stu-id="33f21-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="33f21-121">Обновите эти значения toosomething соответствующие tooyour среду.</span><span class="sxs-lookup"><span data-stu-id="33f21-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="33f21-122">Через несколько минут завершения команды hello и отображаются сведения о развертывании.</span><span class="sxs-lookup"><span data-stu-id="33f21-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="33f21-123">Установка kubectl</span><span class="sxs-lookup"><span data-stu-id="33f21-123">Install kubectl</span></span>

<span data-ttu-id="33f21-124">tooconnect toohello Kubernetes кластера с клиентского компьютера, используйте [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), клиент командной строки Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="33f21-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="33f21-125">Если вы используете Azure CloudShell, установка `kubectl` уже выполнена.</span><span class="sxs-lookup"><span data-stu-id="33f21-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="33f21-126">Если требуется, чтобы tooinstall его локально, можно использовать hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) команды.</span><span class="sxs-lookup"><span data-stu-id="33f21-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="33f21-127">Здравствуйте, следующий пример устанавливает Azure CLI `kubectl` tooyour системы.</span><span class="sxs-lookup"><span data-stu-id="33f21-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="33f21-128">В Windows запустите следующую команду от имени администратора:</span><span class="sxs-lookup"><span data-stu-id="33f21-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="33f21-129">Подключение с помощью kubectl</span><span class="sxs-lookup"><span data-stu-id="33f21-129">Connect with kubectl</span></span>

<span data-ttu-id="33f21-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes кластера, запустите hello [az kubernetes get-учетные данные acs](/cli/azure/acs/kubernetes#get-credentials) команды.</span><span class="sxs-lookup"><span data-stu-id="33f21-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="33f21-131">Hello следующем примере загружаются hello конфигурации кластера для кластера Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="33f21-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="33f21-132">tooverify hello подключения кластера tooyour с компьютера, попробуйте запустить:</span><span class="sxs-lookup"><span data-stu-id="33f21-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="33f21-133">`kubectl`список узлов hello master и агента.</span><span class="sxs-lookup"><span data-stu-id="33f21-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="33f21-134">Развертывание контейнера Windows IIS</span><span class="sxs-lookup"><span data-stu-id="33f21-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="33f21-135">Можно запустить контейнер Docker внутри группы контейнеров Kubernetes (объект *pod*), которая содержит один или несколько контейнеров.</span><span class="sxs-lookup"><span data-stu-id="33f21-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="33f21-136">Этот простой пример использует toospecify файл JSON контейнер Microsoft Internet Information Server (IIS), а затем создает с помощью hello pod hello `kubctl apply` команды.</span><span class="sxs-lookup"><span data-stu-id="33f21-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="33f21-137">Создание локального файла с именем `iis.json` и копирования hello после текста.</span><span class="sxs-lookup"><span data-stu-id="33f21-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="33f21-138">Этот файл сообщением о Kubernetes toorun IIS в Windows Server 2016 Nano Server с помощью образа из общего контейнера [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="33f21-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="33f21-139">контейнер Hello использует порт 80, но изначально доступен только в рамках сети кластера hello.</span><span class="sxs-lookup"><span data-stu-id="33f21-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="33f21-140">toostart hello pod, тип:</span><span class="sxs-lookup"><span data-stu-id="33f21-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="33f21-141">Развертывание tootrack hello, тип:</span><span class="sxs-lookup"><span data-stu-id="33f21-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="33f21-142">При развертывании hello pod, находится в состоянии hello `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="33f21-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="33f21-143">Он может занять несколько минут для hello tooenter контейнера hello `Running` состояния.</span><span class="sxs-lookup"><span data-stu-id="33f21-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="33f21-144">Представление hello страницу приветствия IIS</span><span class="sxs-lookup"><span data-stu-id="33f21-144">View hello IIS welcome page</span></span>

<span data-ttu-id="33f21-145">tooexpose hello world toohello pod с общедоступный IP-адрес, тип hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="33f21-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="33f21-146">С помощью этой команды Kubernetes создает службу и [правило подсистемы балансировки нагрузки Azure](container-service-kubernetes-load-balancing.md) с общедоступный IP-адрес для службы hello.</span><span class="sxs-lookup"><span data-stu-id="33f21-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="33f21-147">Выполните следующие команды toosee hello состояние службы hello hello.</span><span class="sxs-lookup"><span data-stu-id="33f21-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="33f21-148">Изначально hello IP-адрес выглядит как `pending`.</span><span class="sxs-lookup"><span data-stu-id="33f21-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="33f21-149">Через несколько минут hello внешний IP-адрес hello `iis` pod имеет значение:</span><span class="sxs-lookup"><span data-stu-id="33f21-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="33f21-150">Можно использовать веб-браузере choice toosee hello по умолчанию службы IIS страницу приветствия во внешний IP-адрес hello:</span><span class="sxs-lookup"><span data-stu-id="33f21-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![Изображение просмотра tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="33f21-152">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="33f21-152">Delete cluster</span></span>
<span data-ttu-id="33f21-153">Когда кластер hello не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, контейнер службы и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="33f21-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="33f21-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="33f21-154">Next steps</span></span>

<span data-ttu-id="33f21-155">В этом кратком руководстве описано, как развертывать подключенный к `kubectl` кластер Kubernetes и группу контейнеров с контейнером IIS.</span><span class="sxs-lookup"><span data-stu-id="33f21-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="33f21-156">toolearn Дополнительные сведения о службе Azure контейнера, продолжить работу с учебником Kubernetes toohello.</span><span class="sxs-lookup"><span data-stu-id="33f21-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="33f21-157">[Create container images to be used with Azure Container Service](container-service-tutorial-kubernetes-prepare-app.md) (Создание образов контейнеров для использования со Службой контейнеров Azure)</span><span class="sxs-lookup"><span data-stu-id="33f21-157">[Manage an ACS Kubernetes cluster](container-service-tutorial-kubernetes-prepare-app.md)</span></span>
