---
title: "aaaQuickstart - кластера CE Docker в Azure для Linux | Документы Microsoft"
description: "Быстро Узнайте toocreate кластер Docker CE для Linux с контейнерами в службе контейнера Azure с hello Azure CLI."
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
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a><span data-ttu-id="f6289-103">Развертывание кластера Docker CE</span><span class="sxs-lookup"><span data-stu-id="f6289-103">Deploy Docker CE cluster</span></span>

<span data-ttu-id="f6289-104">В этом кратком руководстве развернут кластер Docker CE с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f6289-104">In this quick start, a Docker CE cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="f6289-105">Контейнер несколькими приложение, состоящее из веб-сервер и экземпляр Redis затем развертывается и запускается на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="f6289-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="f6289-106">После завершения приложения hello доступна через Интернет hello.</span><span class="sxs-lookup"><span data-stu-id="f6289-106">Once completed, hello application is accessible over hello internet.</span></span>

<span data-ttu-id="f6289-107">Выпуск Docker CE в службе контейнеров Azure находится на стадии предварительной версии и **его не следует использовать для рабочих нагрузок в рабочей среде**.</span><span class="sxs-lookup"><span data-stu-id="f6289-107">Docker CE on Azure Container Service is in preview and **should not be used for production workloads**.</span></span>

<span data-ttu-id="f6289-108">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="f6289-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="f6289-109">Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f6289-109">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f6289-110">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="f6289-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f6289-111">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f6289-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="f6289-112">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="f6289-112">Create a resource group</span></span>

<span data-ttu-id="f6289-113">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="f6289-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f6289-114">Группа ресурсов Azure — это логическая группа, в которой выполняется развертывание и администрирование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="f6289-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="f6289-115">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *ukwest* расположение.</span><span class="sxs-lookup"><span data-stu-id="f6289-115">hello following example creates a resource group named *myResourceGroup* in hello *ukwest* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

<span data-ttu-id="f6289-116">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="f6289-116">Output:</span></span>

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

## <a name="create-docker-swarm-cluster"></a><span data-ttu-id="f6289-117">Создание кластера Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="f6289-117">Create Docker Swarm cluster</span></span>

<span data-ttu-id="f6289-118">Создайте кластер Docker CE в контейнере службы Azure с hello [создать acs az](/cli/azure/acs#create) команды.</span><span class="sxs-lookup"><span data-stu-id="f6289-118">Create a Docker CE cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="f6289-119">Hello следующий пример создает кластер с именем *mySwarmCluster* с Linux в один главный узел и три узла агента Linux.</span><span class="sxs-lookup"><span data-stu-id="f6289-119">hello following example creates a cluster named *mySwarmCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

<span data-ttu-id="f6289-120">Через несколько минут hello команда завершается и возвращает в формате json сведения о кластере hello.</span><span class="sxs-lookup"><span data-stu-id="f6289-120">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="f6289-121">Подключите кластер toohello</span><span class="sxs-lookup"><span data-stu-id="f6289-121">Connect toohello cluster</span></span>

<span data-ttu-id="f6289-122">В этом кратком руководстве необходимо полное доменное имя главного помощью Docker Swarm hello и пул агентов Docker hello hello.</span><span class="sxs-lookup"><span data-stu-id="f6289-122">Throughout this quick start, you need hello FQDN of both hello Docker Swarm master and hello Docker agent pool.</span></span> <span data-ttu-id="f6289-123">Выполните следующую команду, tooreturn оба hello master и агента полных доменных имен hello.</span><span class="sxs-lookup"><span data-stu-id="f6289-123">Run hello following command tooreturn both hello master and agent FQDNs.</span></span>


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

<span data-ttu-id="f6289-124">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="f6289-124">Output:</span></span>

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

<span data-ttu-id="f6289-125">Создайте главный группу мелких объектов toohello туннеля SSH.</span><span class="sxs-lookup"><span data-stu-id="f6289-125">Create an SSH tunnel toohello Swarm master.</span></span> <span data-ttu-id="f6289-126">Замените `MasterFQDN` с hello адрес полного доменного ИМЕНИ базы данных master hello группу мелких объектов.</span><span class="sxs-lookup"><span data-stu-id="f6289-126">Replace `MasterFQDN` with hello FQDN address of hello Swarm master.</span></span>

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

<span data-ttu-id="f6289-127">Набор hello `DOCKER_HOST` переменной среды.</span><span class="sxs-lookup"><span data-stu-id="f6289-127">Set hello `DOCKER_HOST` environment variable.</span></span> <span data-ttu-id="f6289-128">Это позволяет toorun команды docker с помощью Docker Swarm hello без имени hello toospecify hello узла.</span><span class="sxs-lookup"><span data-stu-id="f6289-128">This allows you toorun docker commands against hello Docker Swarm without having toospecify hello name of hello host.</span></span>

```bash
export DOCKER_HOST=localhost:2374
```

<span data-ttu-id="f6289-129">Теперь вы находитесь службы Docker готов toorun на hello с помощью Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="f6289-129">You are now ready toorun Docker services on hello Docker Swarm.</span></span>


## <a name="run-hello-application"></a><span data-ttu-id="f6289-130">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="f6289-130">Run hello application</span></span>

<span data-ttu-id="f6289-131">Создайте файл с именем `azure-vote.yaml` и hello копировать содержимое в него.</span><span class="sxs-lookup"><span data-stu-id="f6289-131">Create a file named `azure-vote.yaml` and copy hello following content into it.</span></span>


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

<span data-ttu-id="f6289-132">Запустите hello [развертывание стека docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) команды toocreate hello Azure голос службы.</span><span class="sxs-lookup"><span data-stu-id="f6289-132">Run hello [docker stack deploy](https://docs.docker.com/engine/reference/commandline/stack_deploy/) command toocreate hello Azure Vote service.</span></span>

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

<span data-ttu-id="f6289-133">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="f6289-133">Output:</span></span>

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

<span data-ttu-id="f6289-134">Используйте hello [docker ps стека](https://docs.docker.com/engine/reference/commandline/stack_ps/) команды tooreturn hello состояние развертывания приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f6289-134">Use hello [docker stack ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) command tooreturn hello deployment status of hello application.</span></span>

```bash
docker stack ps azure-vote
```

<span data-ttu-id="f6289-135">Здравствуйте, один раз `CURRENT STATE` каждой службы является `Running`, приложение hello готов.</span><span class="sxs-lookup"><span data-stu-id="f6289-135">Once hello `CURRENT STATE` of each service is `Running`, hello application is ready.</span></span>

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a><span data-ttu-id="f6289-136">Тестирование приложения hello</span><span class="sxs-lookup"><span data-stu-id="f6289-136">Test hello application</span></span>

<span data-ttu-id="f6289-137">Обзор toohello tootest пула агента hello группу мелких объектов ожидания hello приложения Azure голос полное доменное имя.</span><span class="sxs-lookup"><span data-stu-id="f6289-137">Browse toohello FQDN of hello Swarm agent pool tootest out hello Azure Vote application.</span></span>

![Изображение просмотра tooAzure голоса](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a><span data-ttu-id="f6289-139">Удаление кластера</span><span class="sxs-lookup"><span data-stu-id="f6289-139">Delete cluster</span></span>
<span data-ttu-id="f6289-140">Когда кластер hello не нужны, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, контейнер службы и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="f6289-140">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="f6289-141">Получение кода hello</span><span class="sxs-lookup"><span data-stu-id="f6289-141">Get hello code</span></span>

<span data-ttu-id="f6289-142">В этом кратком руководстве образы контейнеров предварительно созданной были используется toocreate службу Docker.</span><span class="sxs-lookup"><span data-stu-id="f6289-142">In this quick start, pre-created container images have been used toocreate a Docker service.</span></span> <span data-ttu-id="f6289-143">Hello связанные код приложения, Dockerfile, и создать файл доступны на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="f6289-143">hello related application code, Dockerfile, and Compose file are available on GitHub.</span></span>

[<span data-ttu-id="f6289-144">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="f6289-144">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="f6289-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f6289-145">Next steps</span></span>

<span data-ttu-id="f6289-146">В этом кратком руководстве развертывания кластера с помощью Docker Swarm и развернуты tooit приложение несколькими контейнера.</span><span class="sxs-lookup"><span data-stu-id="f6289-146">In this quick start, you deployed a Docker Swarm cluster and deployed a multi-container application tooit.</span></span>

<span data-ttu-id="f6289-147">toolearn об интеграции с Visual Studio Team Services Docker горячего по-прежнему toohello CI или компакт-диска с помощью Docker Swarm и VSTS.</span><span class="sxs-lookup"><span data-stu-id="f6289-147">toolearn about integrating Docker warm with Visual Studio Team Services, continue toohello CI/CD with Docker Swarm and VSTS.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6289-148">Непрерывная интеграция и доставка с помощью Docker Swarm и VSTS</span><span class="sxs-lookup"><span data-stu-id="f6289-148">CI/CD with Docker Swarm and VSTS</span></span>](./container-service-docker-swarm-setup-ci-cd.md)