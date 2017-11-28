---
title: "Краткое руководство: кластер Azure Docker CE для Linux | Документация Майкрософт"
description: "Из этого краткого руководства вы узнаете, как создать кластер Docker CE для контейнеров Linux в службе контейнеров Azure при помощи Azure CLI."
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 7b8336e3865e7032e3ee0d5e4ee712bcb95aa4b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="d029d-103">Развертывание кластера Docker CE</span><span class="sxs-lookup"><span data-stu-id="d029d-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="d029d-104">В этом кратком руководстве объясняется, как развернуть кластер Docker CE с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d029d-104">In this quick start, a Docker CE cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="d029d-105">Затем в кластере будет развернуто и запущено многоконтейнерное приложение, состоящее из веб-интерфейса и экземпляра Redis.</span><span class="sxs-lookup"><span data-stu-id="d029d-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="d029d-106">По завершении приложение будет доступно через Интернет.</span><span class="sxs-lookup"><span data-stu-id="d029d-106">Once completed, the application is accessible over the internet.</span></span>

<span data-ttu-id="d029d-107">Выпуск Docker CE в службе контейнеров Azure находится на стадии предварительной версии и **его не следует использовать для рабочих нагрузок в рабочей среде**.</span><span class="sxs-lookup"><span data-stu-id="d029d-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="d029d-108">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="d029d-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="d029d-109">Если вы решили установить и использовать CLI локально, для выполнения инструкций в этом руководстве вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="d029d-109">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d029d-110">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="d029d-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="d029d-111">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d029d-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="d029d-112">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="d029d-112">Create a resource group</span></span>

<span data-ttu-id="d029d-113">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="d029d-113">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d029d-114">Группа ресурсов Azure — это логическая группа, в которой выполняется развертывание и администрирование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="d029d-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="d029d-115">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *ukwest*.</span><span class="sxs-lookup"><span data-stu-id="d029d-115">The following example creates a resource group named *myResourceGroup* in the *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="d029d-116">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d029d-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="d029d-117">Создание кластера Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="d029d-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="d029d-118">Создайте кластер Docker CE в службе контейнеров Azure с помощью команды [az acs create](/cli/azure/acs#create).</span><span class="sxs-lookup"><span data-stu-id="d029d-118">Create a Docker CE cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="d029d-119">В следующем примере создается кластер *mySwarmCluster* с одним главным узлом Linux и тремя узлами агентов Linux.</span><span class="sxs-lookup"><span data-stu-id="d029d-119">The following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="d029d-120">Через несколько минут выполнение команды завершается, и отображаются сведения о кластере в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="d029d-120">After several minutes, the command completes and returns json formatted information about the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="d029d-121">Подключение к кластеру</span><span class="sxs-lookup"><span data-stu-id="d029d-121">Connect to the cluster</span></span>

<span data-ttu-id="d029d-122">В этом кратком руководстве необходимо полное доменное имя (FQDN) главного узла Docker Swarm и пула агента Docker.</span><span class="sxs-lookup"><span data-stu-id="d029d-122">Throughout this quick start, you need the FQDN of both the Docker Swarm master and the Docker agent pool.</span></span> <span data-ttu-id="d029d-123">Выполните следующую команду для получения полных доменных имен примера и агента.</span><span class="sxs-lookup"><span data-stu-id="d029d-123">Run the following command to return both the master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="d029d-124">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d029d-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="d029d-125">Создайте туннель SSH для главного узла Swarm.</span><span class="sxs-lookup"><span data-stu-id="d029d-125">Create an SSH tunnel to the Swarm master.</span></span> <span data-ttu-id="d029d-126">Замените `MasterFQDN` адресом полного доменного имени главного узла Swarm.</span><span class="sxs-lookup"><span data-stu-id="d029d-126">Replace `MasterFQDN` with the FQDN address of the Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="d029d-127">Установите переменную среды `DOCKER_HOST`.</span><span class="sxs-lookup"><span data-stu-id="d029d-127">Set the `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="d029d-128">Так вы сможете выполнять команды Docker с Docker Swarm без указания имени узла.</span><span class="sxs-lookup"><span data-stu-id="d029d-128">This allows you to run docker commands against the Docker Swarm without having to specify the name of the host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="d029d-129">Теперь вы готовы к запуску служб Docker с помощью Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="d029d-129">You are now ready to run Docker services on the Docker Swarm.</span></span>


## <a name="run-the-application"></a><span data-ttu-id="d029d-130">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="d029d-130">Run the application</span></span>

<span data-ttu-id="d029d-131">Создайте файл с именем `azure-vote.yaml` и скопируйте в него следующее содержимое.</span><span class="sxs-lookup"><span data-stu-id="d029d-131">Create a file named `azure-vote.yaml` and copy the following content into it.</span></span>


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

<span data-ttu-id="d029d-132">Выполните команду [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/), чтобы создать службу Azure для голосования.</span><span class="sxs-lookup"><span data-stu-id="d029d-132">Run the [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command to create the Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="d029d-133">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d029d-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="d029d-134">Используйте команду [docker ps стека](https://docs.docker.com/engine/reference/commandline/stack_ps/) для развертывания приложения.</span><span class="sxs-lookup"><span data-stu-id="d029d-134">Use the [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command to return the deployment status of the application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="d029d-135">Как только `CURRENT STATE` каждой службы приобретет значение `Running`, приложение будет готово.</span><span class="sxs-lookup"><span data-stu-id="d029d-135">Once the `CURRENT STATE` of each service is `Running`, the application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-the-application"></a><span data-ttu-id="d029d-136">Тестирование приложения</span><span class="sxs-lookup"><span data-stu-id="d029d-136">Test the application</span></span>

<span data-ttu-id="d029d-137">Перейдите к полному доменному имени пула агентов Swarm, чтобы проверить приложение Azure для голосования.</span><span class="sxs-lookup"><span data-stu-id="d029d-137">Browse to the FQDN of the Swarm agent pool to test out the Azure Vote application.</span></span>

![Изображение перехода к приложению Azure для голосования](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="d029d-139">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="d029d-139">Delete cluster</span></span>
<span data-ttu-id="d029d-140">Чтобы удалить ненужные кластер, группу ресурсов, службу контейнеров и все связанные с ней ресурсы, выполните команду [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="d029d-140">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="d029d-141">Получение кода</span><span class="sxs-lookup"><span data-stu-id="d029d-141">Get the code</span></span>

<span data-ttu-id="d029d-142">В этом кратком руководстве для создания службы Docker используются предварительно созданные образы контейнеров.</span><span class="sxs-lookup"><span data-stu-id="d029d-142">In this quick start, pre-created container images have been used to create a Docker service.</span></span> <span data-ttu-id="d029d-143">Связанный с приложением код, Dockerfile и файл Compose доступны на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="d029d-143">The related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="d029d-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="d029d-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="d029d-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d029d-145">Next steps</span></span>

<span data-ttu-id="d029d-146">В этом кратком руководстве мы развернули кластер Docker Swarm, а затем развернули в нем многоконтейнерное приложение.</span><span class="sxs-lookup"><span data-stu-id="d029d-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application to it.</span></span>

<span data-ttu-id="d029d-147">Чтобы получить дополнительные сведения об интеграции Docker Swarm с Visual Studio Team Services, используйте CI или CD с помощью Docker Swarm и VSTS.</span><span class="sxs-lookup"><span data-stu-id="d029d-147">To learn about integrating Docker warm with Visual Studio Team Services, continue to the CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d029d-148">Непрерывная интеграция и доставка с помощью Docker Swarm и VSTS</span><span class="sxs-lookup"><span data-stu-id="d029d-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)