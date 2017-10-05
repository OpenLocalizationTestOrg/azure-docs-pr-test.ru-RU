---
title: "Краткое руководство: сеть кластера Azure Docker Swarm для Linux | Документация Майкрософт"
description: "Узнайте , как быстро создать кластер Docker Swarm для контейнеров Linux в Службе контейнеров Azure при помощи Azure CLI."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 1d10c347795227ed056a95d1bcd4aff82af7b876
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="a7771-103">Развертывание кластера Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a7771-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="a7771-104">В этом кратком руководстве объясняется, как развернуть кластер Docker Swarm с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a7771-104">In this quick start, a Docker Swarm cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="a7771-105">Затем в кластере будет развернуто и запущено многоконтейнерное приложение, состоящее из веб-интерфейса и экземпляра Redis.</span><span class="sxs-lookup"><span data-stu-id="a7771-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="a7771-106">По завершении приложение будет доступно через Интернет.</span><span class="sxs-lookup"><span data-stu-id="a7771-106">Once completed, the application is accessible over the internet.</span></span>

<span data-ttu-id="a7771-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="a7771-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="a7771-108">Для этого руководства требуется Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="a7771-108">This quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a7771-109">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="a7771-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="a7771-110">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a7771-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="a7771-111">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="a7771-111">Create a resource group</span></span>

<span data-ttu-id="a7771-112">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a7771-112">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="a7771-113">Группа ресурсов Azure — это логическая группа, в которой выполняется развертывание и администрирование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="a7771-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="a7771-114">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *westus*.</span><span class="sxs-lookup"><span data-stu-id="a7771-114">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="a7771-115">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a7771-115">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="a7771-116">Создание кластера Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="a7771-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="a7771-117">Создайте кластер Docker Swarm в Службе контейнеров Azure с помощью команды [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="a7771-117">Create a Docker Swarm cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="a7771-118">В следующем примере создается кластер *mySwarmCluster* с одним главным узлом Linux и тремя узлами агентов Linux.</span><span class="sxs-lookup"><span data-stu-id="a7771-118">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="a7771-119">Через несколько минут выполнение команды завершается, и отображаются сведения о кластере в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="a7771-119">After several minutes, the command completes and returns json formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="a7771-120">Подключение к кластеру</span><span class="sxs-lookup"><span data-stu-id="a7771-120">Connect to the cluster</span></span>

<span data-ttu-id="a7771-121">В этом кратком руководстве понадобится полное доменное имя (FQDN) образца Docker Swarm и пул агента Docker.</span><span class="sxs-lookup"><span data-stu-id="a7771-121">Throughout this quick start, you need the IP address of both the Docker Swarm master and the Docker agent pool.</span></span> <span data-ttu-id="a7771-122">Выполните следующую команду, чтобы вернуть оба IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="a7771-122">Run the following command to return both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="a7771-123">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a7771-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="a7771-124">Создайте туннель SSH для главного узла Swarm.</span><span class="sxs-lookup"><span data-stu-id="a7771-124">Create an SSH tunnel to the Swarm master.</span></span> <span data-ttu-id="a7771-125">Замените `IPAddress` IP-адресом главного узла Swarm.</span><span class="sxs-lookup"><span data-stu-id="a7771-125">Replace `IPAddress` with the IP address of the Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="a7771-126">Установите переменную среды `DOCKER_HOST`.</span><span class="sxs-lookup"><span data-stu-id="a7771-126">Set the `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="a7771-127">Так вы сможете выполнять команды Docker с Docker Swarm без указания имени узла.</span><span class="sxs-lookup"><span data-stu-id="a7771-127">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="a7771-128">Теперь вы готовы к запуску служб Docker с помощью Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="a7771-128">You are now ready to run Docker services on the Docker Swarm.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="a7771-129">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="a7771-129">Run the application</span></span>

<span data-ttu-id="a7771-130">Создайте файл с именем `docker-compose.yaml` и скопируйте в него следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="a7771-130">Create a file named `docker-compose.yaml` and copy the following content into it.</span></span>

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="a7771-131">Выполните следующую команду, чтобы создать службу Azure для голосования.</span><span class="sxs-lookup"><span data-stu-id="a7771-131">Run the following command to create the Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="a7771-132">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="a7771-132">Output:</span></span>

```bash
Creating network "user_default" with the default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-the-application"></a><span data-ttu-id="a7771-133">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="a7771-133">Test the application</span></span>

<span data-ttu-id="a7771-134">Перейдите по IP-адресу пула агентов Swarm, чтобы проверить приложение Azure для голосования.</span><span class="sxs-lookup"><span data-stu-id="a7771-134">Browse to the IP address of the Swarm agent pool to test out the Azure Vote application.</span></span>

![Изображение перехода к приложению Azure для голосования](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="a7771-136">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="a7771-136">Delete cluster</span></span>
<span data-ttu-id="a7771-137">Чтобы удалить ненужные кластер, группу ресурсов, службу контейнеров и все связанные с ней ресурсы, выполните команду [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="a7771-137">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="a7771-138">Получение кода</span><span class="sxs-lookup"><span data-stu-id="a7771-138">Get the code</span></span>

<span data-ttu-id="a7771-139">В этом кратком руководстве для создания службы Docker используются предварительно созданные образы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="a7771-139">In this quick start, pre-created container images have been used to create a Docker service.</span></span> <span data-ttu-id="a7771-140">Связанный с приложением код, Dockerfile и файл Compose доступны на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="a7771-140">The related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="a7771-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="a7771-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="a7771-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a7771-142">Next steps</span></span>

<span data-ttu-id="a7771-143">В этом кратком руководстве мы развернули кластер Docker Swarm, а затем развернули в нем многоконтейнерное приложение.</span><span class="sxs-lookup"><span data-stu-id="a7771-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="a7771-144">Чтобы получить дополнительные сведения об интеграции Docker Swarm с Visual Studio Team Services, используйте CI или CD с помощью Docker Swarm и VSTS.</span><span class="sxs-lookup"><span data-stu-id="a7771-144">To learn about integrating Docker warm with Visual Studio Team Services, continue to the CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7771-145">Непрерывная интеграция и доставка с помощью Docker Swarm и VSTS</span><span class="sxs-lookup"><span data-stu-id="a7771-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)