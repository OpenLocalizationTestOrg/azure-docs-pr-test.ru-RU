---
title: "aaaQuickstart - кластера с помощью Docker Swarm Azure для Linux | Документы Microsoft"
description: "Быстро Узнайте toocreate с помощью Docker Swarm кластера для Linux с контейнерами в службе контейнера Azure с hello Azure CLI."
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
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a><span data-ttu-id="8b981-103">Развертывание кластера Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="8b981-103">Deploy Docker Swarm cluster</span></span>

<span data-ttu-id="8b981-104">В этом кратком руководстве кластера с помощью Docker Swarm развертывается hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8b981-104">In this quick start, a Docker Swarm cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="8b981-105">Контейнер несколькими приложение, состоящее из веб-сервер и экземпляр Redis затем развертывается и запускается на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="8b981-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="8b981-106">После завершения приложения hello доступна через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="8b981-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="8b981-107">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="8b981-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="8b981-108">Краткого руководства требует, что вы используете версию Azure CLI hello 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="8b981-108">This quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8b981-109">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="8b981-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8b981-110">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8b981-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="8b981-111">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="8b981-111">Create a resource group</span></span>

<span data-ttu-id="8b981-112">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="8b981-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="8b981-113">Группа ресурсов Azure — это логическая группа, в которой выполняется развертывание и администрирование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="8b981-113">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="8b981-114">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westus* расположение.</span><span class="sxs-lookup"><span data-stu-id="8b981-114">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="8b981-115">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8b981-115">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="8b981-116">Создание кластера Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="8b981-116">Create Docker Swarm cluster</span></span>

<span data-ttu-id="8b981-117">Создание кластера с помощью Docker Swarm в контейнере службы Azure с hello [создать acs az](/cli/azure/acs#create) команды.</span><span class="sxs-lookup"><span data-stu-id="8b981-117">Create a Docker Swarm cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="8b981-118">Hello следующий пример создает кластер с именем *mySwarmCluster* с Linux в один главный узел и три узла агента Linux.</span><span class="sxs-lookup"><span data-stu-id="8b981-118">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="8b981-119">Через несколько минут hello команда завершается и возвращает в формате json сведения о кластере hello.</span><span class="sxs-lookup"><span data-stu-id="8b981-119">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="8b981-120">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="8b981-120">Connect toohello cluster</span></span>

<span data-ttu-id="8b981-121">В этом кратком руководстве требуется hello IP-адрес главного помощью Docker Swarm hello и пул агентов hello Docker.</span><span class="sxs-lookup"><span data-stu-id="8b981-121">Throughout this quick start, you need hello IP address of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="8b981-122">Выполните следующие команды tooreturn hello оба IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="8b981-122">Run hello following command tooreturn both IP addresses.</span></span>


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

<span data-ttu-id="8b981-123">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8b981-123">Output:</span></span>

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

<span data-ttu-id="8b981-124">Создайте главный группу мелких объектов toohello туннеля SSH.</span><span class="sxs-lookup"><span data-stu-id="8b981-124">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="8b981-125">Замените `IPAddress` hello IP-адрес главного hello группу мелких объектов.</span><span class="sxs-lookup"><span data-stu-id="8b981-125">Replace `IPAddress` with hello IP address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

<span data-ttu-id="8b981-126">Набор hello `DOCKER_HOST` переменной среды.</span><span class="sxs-lookup"><span data-stu-id="8b981-126">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="8b981-127">Это позволяет toorun команды docker с помощью Docker Swarm hello без имени hello toospecify hello узла.</span><span class="sxs-lookup"><span data-stu-id="8b981-127">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="8b981-128">Теперь вы находитесь службы Docker готов toorun на hello с помощью Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="8b981-128">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="8b981-129">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="8b981-129">Run hello application</span></span>

<span data-ttu-id="8b981-130">Создайте файл с именем `docker-compose.yaml` и hello копировать содержимое в него.</span><span class="sxs-lookup"><span data-stu-id="8b981-130">Create a file named `docker-compose.yaml` and copy hello following content into it.</span></span>

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

<span data-ttu-id="8b981-131">Запустите hello, следующая команда toocreate hello Azure голос службы.</span><span class="sxs-lookup"><span data-stu-id="8b981-131">Run hello following command toocreate hello Azure Vote service.</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="8b981-132">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="8b981-132">Output:</span></span>

```bash
Creating network "user_default" with hello default driver
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

## <a name="test-hello-application"></a><span data-ttu-id="8b981-133">Тестирование приложения hello</span><span class="sxs-lookup"><span data-stu-id="8b981-133">Test hello application</span></span>

<span data-ttu-id="8b981-134">Обзор toohello IP-адрес tootest пула агента группу мелких объектов hello out приложения hello Azure голос.</span><span class="sxs-lookup"><span data-stu-id="8b981-134">Browse toohello IP address of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![Изображение просмотра tooAzure голоса](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="8b981-136">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="8b981-136">Delete cluster</span></span>
<span data-ttu-id="8b981-137">Когда кластер hello не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, контейнер службы и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="8b981-137">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="8b981-138">Получение кода hello</span><span class="sxs-lookup"><span data-stu-id="8b981-138">Get hello code</span></span>

<span data-ttu-id="8b981-139">В этом кратком руководстве образы контейнеров предварительно созданной были используется toocreate службу Docker.</span><span class="sxs-lookup"><span data-stu-id="8b981-139">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="8b981-140">Hello связанные код приложения, Dockerfile, и создать файл доступны на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b981-140">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="8b981-141">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="8b981-141">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="8b981-142">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8b981-142">Next steps</span></span>

<span data-ttu-id="8b981-143">В этом кратком руководстве развертывания кластера с помощью Docker Swarm и развернуты tooit приложение несколькими контейнера.</span><span class="sxs-lookup"><span data-stu-id="8b981-143">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="8b981-144">toolearn об интеграции с Visual Studio Team Services Docker горячего по-прежнему toohello CI или компакт-диска с помощью Docker Swarm и VSTS.</span><span class="sxs-lookup"><span data-stu-id="8b981-144">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8b981-145">Непрерывная интеграция и доставка с помощью Docker Swarm и VSTS</span><span class="sxs-lookup"><span data-stu-id="8b981-145">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)