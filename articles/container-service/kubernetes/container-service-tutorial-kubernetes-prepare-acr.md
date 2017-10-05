---
title: "Руководство по службе контейнеров Azure — подготовка ACR | Документация Майкрософт"
description: "Руководство по службе контейнеров Azure — подготовка ACR"
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
ms.openlocfilehash: 3e1f7617bf2fc52ee4c15598f51a46276f4dc57d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="050d1-104">Развертывание реестра контейнеров Azure и его использование</span><span class="sxs-lookup"><span data-stu-id="050d1-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="050d1-105">Реестр контейнеров Azure (ACR) является частным реестром на базе Azure для образов контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="050d1-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="050d1-106">В этом руководстве (здесь представлена вторая его часть из семи) рассматриваются основные шаги для развертывания экземпляра реестра контейнеров Azure и отправки в него образов контейнеров.</span><span class="sxs-lookup"><span data-stu-id="050d1-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image to it.</span></span> <span data-ttu-id="050d1-107">В частности, рассматриваются такие шаги:</span><span class="sxs-lookup"><span data-stu-id="050d1-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="050d1-108">развертывание экземпляра реестра контейнеров Azure (ACR);</span><span class="sxs-lookup"><span data-stu-id="050d1-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="050d1-109">добавление тегов к образу контейнера для ACR;</span><span class="sxs-lookup"><span data-stu-id="050d1-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="050d1-110">отправка образа в ACR.</span><span class="sxs-lookup"><span data-stu-id="050d1-110">Uploading the image to ACR</span></span>

<span data-ttu-id="050d1-111">В последующих руководствах данный экземпляр ACR интегрируется с кластером Kubernetes службы контейнеров Azure для безопасного выполнения образов контейнеров.</span><span class="sxs-lookup"><span data-stu-id="050d1-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="050d1-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="050d1-112">Before you begin</span></span>

<span data-ttu-id="050d1-113">В [предыдущей части руководства](./container-service-tutorial-kubernetes-prepare-app.md) мы создали образ контейнера для простого приложения Azure для голосования.</span><span class="sxs-lookup"><span data-stu-id="050d1-113">In the [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="050d1-114">Теперь мы поместим этот образ в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="050d1-114">In this tutorial, this image is pushed to an Azure Container Registry.</span></span> <span data-ttu-id="050d1-115">Если вы еще не создали образ приложения Azure для голосования, выполните инструкции из статьи [Create container images to be used with Azure Container Service](./container-service-tutorial-kubernetes-prepare-app.md) (Создание образов контейнеров с помощью службы контейнеров Azure).</span><span class="sxs-lookup"><span data-stu-id="050d1-115">If you have not created the Azure Voting app image, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="050d1-116">Описанные здесь шаги подходят для любого образа контейнера.</span><span class="sxs-lookup"><span data-stu-id="050d1-116">Alternatively, the steps detailed here work with any container image.</span></span>

<span data-ttu-id="050d1-117">Для этого руководства требуется Azure CLI версии 2.0.4 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="050d1-117">This tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="050d1-118">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="050d1-118">Run `az --version` to find the version.</span></span> <span data-ttu-id="050d1-119">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="050d1-119">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="050d1-120">Развертывание реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="050d1-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="050d1-121">При развертывании реестра контейнеров Azure сначала необходимо создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="050d1-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="050d1-122">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="050d1-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="050d1-123">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="050d1-123">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="050d1-124">В этом примере создается группа ресурсов с именем *myResourceGroup* в регионе *westeurope*.</span><span class="sxs-lookup"><span data-stu-id="050d1-124">In this example, a resource group named *myResourceGroup* is created in the *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="050d1-125">Создайте реестр контейнеров Azure с помощью команды[az acr create](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="050d1-125">Create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="050d1-126">Имя контейнера реестра **должно быть уникальным**.</span><span class="sxs-lookup"><span data-stu-id="050d1-126">The name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="050d1-127">В остальной части этого руководства acrname будет заменять в примерах имя контейнера реестра.</span><span class="sxs-lookup"><span data-stu-id="050d1-127">Throughout the rest of this tutorial, we use "acrname" as a placeholder for the container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="050d1-128">Вход в реестр контейнеров</span><span class="sxs-lookup"><span data-stu-id="050d1-128">Container registry login</span></span>

<span data-ttu-id="050d1-129">Войдите в свой экземпляр ACR, прежде чем отправлять в него образы.</span><span class="sxs-lookup"><span data-stu-id="050d1-129">You must log in to your ACR instance before pushing images to it.</span></span> <span data-ttu-id="050d1-130">Используйте команду [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login), чтобы выполнить операцию.</span><span class="sxs-lookup"><span data-stu-id="050d1-130">Use the [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command to complete the operation.</span></span> <span data-ttu-id="050d1-131">Укажите уникальное имя реестра контейнеров, заданное для него при создании.</span><span class="sxs-lookup"><span data-stu-id="050d1-131">You need to provide the unique name given to the container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="050d1-132">После выполнения эта команда возвращает сообщение Login Succeeded (Вход выполнен).</span><span class="sxs-lookup"><span data-stu-id="050d1-132">The command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="050d1-133">Присвоение тегов образам контейнеров</span><span class="sxs-lookup"><span data-stu-id="050d1-133">Tag container images</span></span>

<span data-ttu-id="050d1-134">Каждый образ контейнера должен иметь тег с именем сервера входа (loginServer), указанным для реестра.</span><span class="sxs-lookup"><span data-stu-id="050d1-134">Each container image needs to be tagged with the loginServer name of the registry.</span></span> <span data-ttu-id="050d1-135">Данный тег используется для маршрутизации при отправке образов контейнеров в реестр образов.</span><span class="sxs-lookup"><span data-stu-id="050d1-135">This tag is used for routing when pushing container images to an image registry.</span></span>

<span data-ttu-id="050d1-136">Чтобы просмотреть список сохраненных образов, используйте команду [docker images](https://docs.docker.com/engine/reference/commandline/images/).</span><span class="sxs-lookup"><span data-stu-id="050d1-136">To see a list of current images, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="050d1-137">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="050d1-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="050d1-138">Чтобы получить имя loginServer, выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="050d1-138">To get the loginServer name, run the following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="050d1-139">Теперь пометьте образ *azure-vote-front* с помощью тега loginServer реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="050d1-139">Now, tag the *azure-vote-front* image with the loginServer of the container registry.</span></span> <span data-ttu-id="050d1-140">Кроме того, добавьте `:redis-v1` в конец имени образа.</span><span class="sxs-lookup"><span data-stu-id="050d1-140">Also, add `:redis-v1` to the end of the image name.</span></span> <span data-ttu-id="050d1-141">Этот тег обозначает номер версии образа.</span><span class="sxs-lookup"><span data-stu-id="050d1-141">This tag indicates the image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="050d1-142">Добавив все нужные теги, выполните команду [docker images] (https://docs.docker.com/engine/reference/commandline/images/), чтобы проверить правильность работы.</span><span class="sxs-lookup"><span data-stu-id="050d1-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) to verify the operation.</span></span>

```bash
docker images
```

<span data-ttu-id="050d1-143">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="050d1-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-to-registry"></a><span data-ttu-id="050d1-144">Отправка образов в реестр</span><span class="sxs-lookup"><span data-stu-id="050d1-144">Push images to registry</span></span>

<span data-ttu-id="050d1-145">Отправьте образ *azure-vote-front* в реестр.</span><span class="sxs-lookup"><span data-stu-id="050d1-145">Push the *azure-vote-front* image to the registry.</span></span> 

<span data-ttu-id="050d1-146">Используйте следующий пример, заменив в нем имя loginServer ACR именем loginServer своей среды.</span><span class="sxs-lookup"><span data-stu-id="050d1-146">Using the following example, replace the ACR loginServer name with the loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="050d1-147">Для завершения операции требуется несколько минут.</span><span class="sxs-lookup"><span data-stu-id="050d1-147">This takes a couple of minutes to complete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="050d1-148">Перечисление образов в реестре</span><span class="sxs-lookup"><span data-stu-id="050d1-148">List images in registry</span></span>

<span data-ttu-id="050d1-149">Чтобы получить список образов, отправленных в реестр контейнеров Azure, выполните команду [az acr repository list](/cli/azure/acr/repository#list).</span><span class="sxs-lookup"><span data-stu-id="050d1-149">To return a list of images that have been pushed to your Azure Container registry, user the [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="050d1-150">Укажите в команде имя нужного экземпляра ACR.</span><span class="sxs-lookup"><span data-stu-id="050d1-150">Update the command with the ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="050d1-151">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="050d1-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="050d1-152">Чтобы увидеть теги для конкретного образа, используйте команду [az acr repository show-tags](/cli/azure/acr/repository#show-tags).</span><span class="sxs-lookup"><span data-stu-id="050d1-152">And then to see the tags for a specific image, use the [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="050d1-153">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="050d1-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="050d1-154">По завершении работы с этим руководством образ контейнера будет сохранен в частном экземпляре реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="050d1-154">At tutorial completion, the container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="050d1-155">В следующих частях руководства мы развернем этот образ из ACR в кластер Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="050d1-155">This image is deployed from ACR to a Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="050d1-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="050d1-156">Next steps</span></span>

<span data-ttu-id="050d1-157">В этом руководстве вы подготовили реестр контейнеров Azure для использования в кластере Kubernetes ACS.</span><span class="sxs-lookup"><span data-stu-id="050d1-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="050d1-158">Были выполнены следующие действия:</span><span class="sxs-lookup"><span data-stu-id="050d1-158">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="050d1-159">развертывание экземпляра реестра контейнеров Azure;</span><span class="sxs-lookup"><span data-stu-id="050d1-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="050d1-160">добавление тегов к образу контейнера для ACR;</span><span class="sxs-lookup"><span data-stu-id="050d1-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="050d1-161">отправка образа в ACR.</span><span class="sxs-lookup"><span data-stu-id="050d1-161">Uploaded the image to ACR</span></span>

<span data-ttu-id="050d1-162">Перейдите к следующему руководству, чтобы ознакомиться с развертыванием кластера Kubernetes в Azure.</span><span class="sxs-lookup"><span data-stu-id="050d1-162">Advance to the next tutorial to learn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="050d1-163">Развертывание кластера Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="050d1-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)