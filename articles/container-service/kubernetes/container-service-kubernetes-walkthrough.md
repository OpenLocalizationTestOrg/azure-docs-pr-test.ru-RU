---
title: "aaaQuickstart - кластера Azure Kubernetes для Linux | Документы Microsoft"
description: "Быстро Узнайте toocreate кластер Kubernetes для Linux с контейнерами в службе контейнера Azure с hello Azure CLI."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="fd83b-103">Развертывание кластера Kubernetes для контейнеров Linux</span><span class="sxs-lookup"><span data-stu-id="fd83b-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="fd83b-104">В этом кратком руководстве кластера Kubernetes развертывается hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fd83b-104">In this quick start, a Kubernetes cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="fd83b-105">Контейнер несколькими приложение, состоящее из веб-сервер и экземпляр Redis затем развертывается и запускается на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="fd83b-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="fd83b-106">После завершения приложения hello доступна через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="fd83b-106">Once completed, hello application is accessible over hello internet.</span></span> 

<span data-ttu-id="fd83b-107">Пример приложения Hello, используемые в этом документе записывается в Python.</span><span class="sxs-lookup"><span data-stu-id="fd83b-107">hello example application used in this document is written in Python.</span></span> <span data-ttu-id="fd83b-108">Основные понятия Hello и этапы, описанные здесь может быть используется toodeploy любого контейнера изображения в качестве Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="fd83b-108">hello concepts and steps detailed here can be used toodeploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="fd83b-109">Hello кода, Dockerfile и предварительно созданный проект toothis связанные файлы манифеста Kubernetes доступны на [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="fd83b-109">hello code, Dockerfile, and pre-created Kubernetes manifest files related toothis project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Изображение просмотра tooAzure голоса](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="fd83b-111">В этом кратком руководстве предполагается, основные понятия Kubernetes см. подробные сведения о Kubernetes hello [Kubernetes документации]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="fd83b-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="fd83b-112">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="fd83b-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="fd83b-113">Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="fd83b-113">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="fd83b-114">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="fd83b-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="fd83b-115">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="fd83b-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="fd83b-116">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="fd83b-116">Create a resource group</span></span>

<span data-ttu-id="fd83b-117">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="fd83b-117">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="fd83b-118">Группа ресурсов Azure — это логическая группа, в которой выполняется развертывание и администрирование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="fd83b-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="fd83b-119">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westeurope* расположение.</span><span class="sxs-lookup"><span data-stu-id="fd83b-119">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="fd83b-120">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fd83b-120">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="fd83b-121">Создание кластера Kubernetes</span><span class="sxs-lookup"><span data-stu-id="fd83b-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="fd83b-122">Создание кластера Kubernetes в контейнере службы Azure с hello [создать acs az](/cli/azure/acs#create) команды.</span><span class="sxs-lookup"><span data-stu-id="fd83b-122">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="fd83b-123">Hello следующий пример создает кластер с именем *myK8sCluster* с Linux в один главный узел и три узла агента Linux.</span><span class="sxs-lookup"><span data-stu-id="fd83b-123">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="fd83b-124">Через несколько минут hello команда завершается и возвращает в формате json сведения о кластере hello.</span><span class="sxs-lookup"><span data-stu-id="fd83b-124">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span> 

## <a name="connect-toohello-cluster"></a><span data-ttu-id="fd83b-125">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="fd83b-125">Connect toohello cluster</span></span>

<span data-ttu-id="fd83b-126">использовать кластер Kubernetes toomanage [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), клиент командной строки Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="fd83b-126">toomanage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="fd83b-127">Если вы используете Azure CloudShell, клиент kubectl уже установлен.</span><span class="sxs-lookup"><span data-stu-id="fd83b-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="fd83b-128">Если требуется, чтобы tooinstall его локально, можно использовать hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) команды.</span><span class="sxs-lookup"><span data-stu-id="fd83b-128">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="fd83b-129">tooconfigure kubectl tooconnect tooyour Kubernetes кластера, запустите hello [az kubernetes get-учетные данные acs](/cli/azure/acs/kubernetes#get-credentials) команды.</span><span class="sxs-lookup"><span data-stu-id="fd83b-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="fd83b-130">На этом этапе загрузки учетных данных и настраивает hello Kubernetes CLI toouse их.</span><span class="sxs-lookup"><span data-stu-id="fd83b-130">This step downloads credentials and configures hello Kubernetes CLI toouse them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="fd83b-131">tooyour tooverify hello подключения кластера, используйте hello [kubectl получить](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooreturn команда список узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="fd83b-131">tooverify hello connection tooyour cluster, use hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command tooreturn a list of hello cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="fd83b-132">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fd83b-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a><span data-ttu-id="fd83b-133">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="fd83b-133">Run hello application</span></span>

<span data-ttu-id="fd83b-134">Файл манифеста Kubernetes определяет требуемое состояние для hello кластера, включая то, что должна быть запущена образы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="fd83b-134">A Kubernetes manifest file defines a desired state for hello cluster, including what container images should be running.</span></span> <span data-ttu-id="fd83b-135">Например манифест представляет используется toocreate все объекты, необходимые toorun hello приложения Azure голос.</span><span class="sxs-lookup"><span data-stu-id="fd83b-135">For this example, a manifest is used toocreate all objects needed toorun hello Azure Vote application.</span></span> 

<span data-ttu-id="fd83b-136">Создайте файл с именем `azure-vote.yml` и скопируйте в него следующие YAML hello.</span><span class="sxs-lookup"><span data-stu-id="fd83b-136">Create a file named `azure-vote.yml` and copy into it hello following YAML.</span></span> <span data-ttu-id="fd83b-137">Если вы работаете в Azure Cloud Shell, этот файл можно создать с помощью Vi или Nano, как при работе в виртуальной или физической системе.</span><span class="sxs-lookup"><span data-stu-id="fd83b-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="fd83b-138">Используйте hello [kubectl создания](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) команды toorun приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fd83b-138">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="fd83b-139">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="fd83b-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a><span data-ttu-id="fd83b-140">Тестирование приложения hello</span><span class="sxs-lookup"><span data-stu-id="fd83b-140">Test hello application</span></span>

<span data-ttu-id="fd83b-141">При запуске приложения hello [Kubernetes службы](https://kubernetes.io/docs/concepts/services-networking/service/) создается hello, предоставляет toohello внешнего интерфейса приложения Интернета.</span><span class="sxs-lookup"><span data-stu-id="fd83b-141">As hello application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes hello application front end toohello internet.</span></span> <span data-ttu-id="fd83b-142">Этот процесс может занять несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="fd83b-142">This process can take a few minutes toocomplete.</span></span> 

<span data-ttu-id="fd83b-143">toomonitor о ходе выполнения, используйте hello [kubectl получить службу](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) с hello `--watch` аргумент.</span><span class="sxs-lookup"><span data-stu-id="fd83b-143">toomonitor progress, use hello [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="fd83b-144">Здравствуйте, изначально **внешний IP-** для hello *azure голос передней панели* службы отображается как *ожидающие*.</span><span class="sxs-lookup"><span data-stu-id="fd83b-144">Initially hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="fd83b-145">После hello внешний IP-адрес отличается от *ожидающие* tooan *IP-адрес*, используйте `CTRL-C` toostop hello kubectl Контрольные значения процесса.</span><span class="sxs-lookup"><span data-stu-id="fd83b-145">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="fd83b-146">Теперь можно выполнять поиск toohello внешние IP адрес toosee hello голос приложения Azure.</span><span class="sxs-lookup"><span data-stu-id="fd83b-146">You can now browse toohello external IP address toosee hello Azure Vote App.</span></span>

![Изображение просмотра tooAzure голоса](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="fd83b-148">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="fd83b-148">Delete cluster</span></span>
<span data-ttu-id="fd83b-149">Когда кластер hello не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, контейнер службы и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fd83b-149">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="fd83b-150">Получение кода hello</span><span class="sxs-lookup"><span data-stu-id="fd83b-150">Get hello code</span></span>

<span data-ttu-id="fd83b-151">В этом кратком руководстве образы контейнеров предварительно созданной были используется toocreate Kubernetes развертывания.</span><span class="sxs-lookup"><span data-stu-id="fd83b-151">In this quick start, pre-created container images have been used toocreate a Kubernetes deployment.</span></span> <span data-ttu-id="fd83b-152">Hello связанные код приложения, Dockerfile, и файл манифеста Kubernetes доступны на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="fd83b-152">hello related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="fd83b-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="fd83b-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="fd83b-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd83b-154">Next steps</span></span>

<span data-ttu-id="fd83b-155">В этом кратком руководстве развертывания кластера Kubernetes и развернуты tooit приложение несколькими контейнера.</span><span class="sxs-lookup"><span data-stu-id="fd83b-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application tooit.</span></span> 

<span data-ttu-id="fd83b-156">toolearn Дополнительные сведения о службе Azure контейнера и пошагового полный пример toodeployment, продолжить работу с учебником кластера Kubernetes toohello.</span><span class="sxs-lookup"><span data-stu-id="fd83b-156">toolearn more about Azure Container Service, and walk through a complete code toodeployment example, continue toohello Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="fd83b-157">[Create container images to be used with Azure Container Service](./container-service-tutorial-kubernetes-prepare-app.md) (Создание образов контейнеров для использования со Службой контейнеров Azure)</span><span class="sxs-lookup"><span data-stu-id="fd83b-157">[Manage an ACS Kubernetes cluster](./container-service-tutorial-kubernetes-prepare-app.md)</span></span>
