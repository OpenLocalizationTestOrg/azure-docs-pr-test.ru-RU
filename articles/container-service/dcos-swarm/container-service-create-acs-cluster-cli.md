---
title: "aaaDeploy кластер контейнера Docker - Azure CLI | Документы Microsoft"
description: "Развертывание решений Kubernetes, DC/OS или Docker Swarm в службе контейнеров Azure с помощью Azure CLI 2.0"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a><span data-ttu-id="e5fff-103">Развертывания с помощью Azure CLI 2.0 hello решения по размещению контейнера Docker</span><span class="sxs-lookup"><span data-stu-id="e5fff-103">Deploy a Docker container hosting solution using hello Azure CLI 2.0</span></span>

<span data-ttu-id="e5fff-104">Используйте hello `az acs` команды в toocreate hello Azure CLI 2.0 кластеров и управление ими в службе контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fff-104">Use hello `az acs` commands in hello Azure CLI 2.0 toocreate and manage clusters in Azure Container Service.</span></span> <span data-ttu-id="e5fff-105">Можно также развернуть кластер контейнера службы Azure с помощью hello [портал Azure](container-service-deployment.md) или hello API-интерфейсы службы контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fff-105">You can also deploy an Azure Container Service cluster by using hello [Azure portal](container-service-deployment.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="e5fff-106">Для получения справки по `az acs` команд, передайте hello `-h` параметр tooany команды.</span><span class="sxs-lookup"><span data-stu-id="e5fff-106">For help on `az acs` commands, pass hello `-h` parameter tooany command.</span></span> <span data-ttu-id="e5fff-107">Например, `az acs create -h`.</span><span class="sxs-lookup"><span data-stu-id="e5fff-107">For example: `az acs create -h`.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="e5fff-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e5fff-108">Prerequisites</span></span>
<span data-ttu-id="e5fff-109">toocreate кластера контейнера службы Azure с помощью hello Azure CLI 2.0, необходимо:</span><span class="sxs-lookup"><span data-stu-id="e5fff-109">toocreate an Azure Container Service cluster using hello Azure CLI 2.0, you must:</span></span>
* <span data-ttu-id="e5fff-110">учетная запись Azure ([получите бесплатную пробную версию](https://azure.microsoft.com/pricing/free-trial/));</span><span class="sxs-lookup"><span data-stu-id="e5fff-110">have an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/))</span></span>
* <span data-ttu-id="e5fff-111">установки и настройки hello [Azure CLI 2.0](/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="e5fff-111">have installed and set up hello [Azure CLI 2.0](/cli/azure/install-az-cli2)</span></span>

## <a name="get-started"></a><span data-ttu-id="e5fff-112">Начало работы</span><span class="sxs-lookup"><span data-stu-id="e5fff-112">Get started</span></span> 
### <a name="log-in-tooyour-account"></a><span data-ttu-id="e5fff-113">Войдите в учетную запись tooyour</span><span class="sxs-lookup"><span data-stu-id="e5fff-113">Log in tooyour account</span></span>
```azurecli
az login 
```

<span data-ttu-id="e5fff-114">Выполните hello toolog запросы в интерактивном режиме.</span><span class="sxs-lookup"><span data-stu-id="e5fff-114">Follow hello prompts toolog in interactively.</span></span> <span data-ttu-id="e5fff-115">Другие методы toolog в, в разделе [Приступая к работе с Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e5fff-115">For other methods toolog in, see [Get started with Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).</span></span>

### <a name="set-your-azure-subscription"></a><span data-ttu-id="e5fff-116">Настройка подписки Azure</span><span class="sxs-lookup"><span data-stu-id="e5fff-116">Set your Azure subscription</span></span>

<span data-ttu-id="e5fff-117">Если у вас есть несколько подписок Azure, установите подписку по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="e5fff-117">If you have more than one Azure subscription, set hello default subscription.</span></span> <span data-ttu-id="e5fff-118">Например:</span><span class="sxs-lookup"><span data-stu-id="e5fff-118">For example:</span></span>

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a><span data-ttu-id="e5fff-119">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e5fff-119">Create a resource group</span></span>
<span data-ttu-id="e5fff-120">Мы рекомендуем создать группу ресурсов для каждого кластера.</span><span class="sxs-lookup"><span data-stu-id="e5fff-120">We recommend that you create a resource group for every cluster.</span></span> <span data-ttu-id="e5fff-121">Укажите регион Azure, в котором [доступна](https://azure.microsoft.com/en-us/regions/services/) Служба контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fff-121">Specify an Azure region in which Azure Container Service is [available](https://azure.microsoft.com/en-us/regions/services/).</span></span> <span data-ttu-id="e5fff-122">Например:</span><span class="sxs-lookup"><span data-stu-id="e5fff-122">For example:</span></span>

```azurecli
az group create -n acsrg1 -l "westus"
```
<span data-ttu-id="e5fff-123">Выходные данные выглядят аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="e5fff-123">Output is similar toohello following:</span></span>

![Создание группы ресурсов](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a><span data-ttu-id="e5fff-125">Создание кластера Службы контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e5fff-125">Create an Azure Container Service cluster</span></span>

<span data-ttu-id="e5fff-126">toocreate кластер, используйте `az acs create`.</span><span class="sxs-lookup"><span data-stu-id="e5fff-126">toocreate a cluster, use `az acs create`.</span></span>
<span data-ttu-id="e5fff-127">Имя кластера hello и hello hello группы ресурсов, созданных в предыдущем шаге hello — обязательные параметры.</span><span class="sxs-lookup"><span data-stu-id="e5fff-127">A name for hello cluster and hello name of hello resource group created in hello previous step are mandatory parameters.</span></span> 

<span data-ttu-id="e5fff-128">Другие входные данные, установите toodefault значения (см. следующий экран приветствия) Если не переопределены с помощью их соответствующими параметрами.</span><span class="sxs-lookup"><span data-stu-id="e5fff-128">Other inputs are set toodefault values (see hello following screen) unless overwritten using their respective switches.</span></span> <span data-ttu-id="e5fff-129">Например по умолчанию tooDC/OS задается hello orchestrator.</span><span class="sxs-lookup"><span data-stu-id="e5fff-129">For example, hello orchestrator is set by default tooDC/OS.</span></span> <span data-ttu-id="e5fff-130">И если не указано, создается на имя кластера hello основе префикса имени DNS.</span><span class="sxs-lookup"><span data-stu-id="e5fff-130">And if you don't specify one, a DNS name prefix is created based on hello cluster name.</span></span>

![Использование az acs create](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a><span data-ttu-id="e5fff-132">Быстрое выполнение `acs create` с использованием значений по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e5fff-132">Quick `acs create` using defaults</span></span>
<span data-ttu-id="e5fff-133">При наличии файла открытого ключа SSH-RSA `id_rsa.pub` в расположении по умолчанию hello (или создана для [OS X и Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) или [Windows](../../virtual-machines/linux/ssh-from-windows.md)), используйте команду hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e5fff-133">If you have an SSH RSA public key file `id_rsa.pub` in hello default location (or created one for [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md)), use a command like hello following:</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
<span data-ttu-id="e5fff-134">Если у вас нет открытого ключа SSH, используйте вторую команду.</span><span class="sxs-lookup"><span data-stu-id="e5fff-134">If you don't have an SSH public key, use this second command.</span></span> <span data-ttu-id="e5fff-135">Эта команда с hello `--generate-ssh-keys` коммутатора создаст ее.</span><span class="sxs-lookup"><span data-stu-id="e5fff-135">This command with hello `--generate-ssh-keys` switch creates one for you.</span></span>

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

<span data-ttu-id="e5fff-136">После выполнения команды hello, подождите около 10 минут для создания toobe кластера hello.</span><span class="sxs-lookup"><span data-stu-id="e5fff-136">After you enter hello command, wait for about 10 minutes for hello cluster toobe created.</span></span> <span data-ttu-id="e5fff-137">выходные данные команды Hello включает полные доменные имена (FQDN) главного hello и узлы агентов и SSH команда tooconnect toohello первый образец.</span><span class="sxs-lookup"><span data-stu-id="e5fff-137">hello command output includes fully qualified domain names (FQDNs) of hello master and agent nodes and an SSH command tooconnect toohello first master.</span></span> <span data-ttu-id="e5fff-138">Ниже приведены сокращенные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="e5fff-138">Here is abbreviated output:</span></span>

![Изображение создания ACS](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> <span data-ttu-id="e5fff-140">Hello [Пошаговое руководство Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md) показано, как toouse `az acs create` с toocreate значения по умолчанию Kubernetes кластера.</span><span class="sxs-lookup"><span data-stu-id="e5fff-140">hello [Kubernetes walkthrough](../kubernetes/container-service-kubernetes-walkthrough.md) shows how toouse `az acs create` with default values toocreate a Kubernetes cluster.</span></span>
>

## <a name="manage-acs-clusters"></a><span data-ttu-id="e5fff-141">Управление кластерами ACS</span><span class="sxs-lookup"><span data-stu-id="e5fff-141">Manage ACS clusters</span></span>

<span data-ttu-id="e5fff-142">Использование дополнительных `az acs` команды toomanage кластера.</span><span class="sxs-lookup"><span data-stu-id="e5fff-142">Use additional `az acs` commands toomanage your cluster.</span></span> <span data-ttu-id="e5fff-143">Ниже приведены некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="e5fff-143">Here are some examples.</span></span>

### <a name="list-clusters-under-a-subscription"></a><span data-ttu-id="e5fff-144">Получение списка кластеров в рамках подписки</span><span class="sxs-lookup"><span data-stu-id="e5fff-144">List clusters under a subscription</span></span>

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a><span data-ttu-id="e5fff-145">Получение списка кластеров в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="e5fff-145">List clusters in a resource group</span></span>

```azurecli
az acs list -g acsrg1 --output table
```

![acs list](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a><span data-ttu-id="e5fff-147">Отображение сведений о кластере службы контейнеров</span><span class="sxs-lookup"><span data-stu-id="e5fff-147">Display details of a container service cluster</span></span>

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![acs show](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a><span data-ttu-id="e5fff-149">Масштаб hello кластера</span><span class="sxs-lookup"><span data-stu-id="e5fff-149">Scale hello cluster</span></span>
<span data-ttu-id="e5fff-150">Увеличение и уменьшение масштабирования узлов агента разрешено.</span><span class="sxs-lookup"><span data-stu-id="e5fff-150">Both scaling in and scaling out of agent nodes are allowed.</span></span> <span data-ttu-id="e5fff-151">Здравствуйте, параметр `new-agent-count` hello новое число агентов в кластере hello ACS.</span><span class="sxs-lookup"><span data-stu-id="e5fff-151">hello parameter `new-agent-count` is hello new number of agents in hello ACS cluster.</span></span>

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![acs scale](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a><span data-ttu-id="e5fff-153">Удаление кластера службы контейнеров</span><span class="sxs-lookup"><span data-stu-id="e5fff-153">Delete a container service cluster</span></span>
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
<span data-ttu-id="e5fff-154">Эта команда удаляет все ресурсы (сеть и хранилище), созданные при создании контейнера службы hello.</span><span class="sxs-lookup"><span data-stu-id="e5fff-154">This command does not delete all resources (network and storage) created while creating hello container service.</span></span> <span data-ttu-id="e5fff-155">toodelete все ресурсы легко, рекомендуется развертывание каждого кластера в группу различных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e5fff-155">toodelete all resources easily, it is recommended you deploy each cluster in a distinct resource group.</span></span> <span data-ttu-id="e5fff-156">Затем удалите группу ресурсов hello при hello кластер больше не требуется.</span><span class="sxs-lookup"><span data-stu-id="e5fff-156">Then, delete hello resource group when hello cluster is no longer required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5fff-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5fff-157">Next steps</span></span>
<span data-ttu-id="e5fff-158">Теперь, когда у вас есть работающий кластер, выберите ссылки ниже, чтобы узнать о возможностях подключения и управления.</span><span class="sxs-lookup"><span data-stu-id="e5fff-158">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="e5fff-159">Подключите кластер tooan контейнера службы Azure</span><span class="sxs-lookup"><span data-stu-id="e5fff-159">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="e5fff-160">Работа со службой контейнеров Azure и DC/OS</span><span class="sxs-lookup"><span data-stu-id="e5fff-160">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="e5fff-161">Работа со службой контейнеров Azure и Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="e5fff-161">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="e5fff-162">Работа со службой контейнеров Azure и Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e5fff-162">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)