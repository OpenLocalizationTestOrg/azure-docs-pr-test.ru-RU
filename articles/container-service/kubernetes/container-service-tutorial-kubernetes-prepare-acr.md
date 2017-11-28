---
title: "Учебник контейнера службы aaaAzure - Подготовка контроля доступа | Документы Microsoft"
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
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="eac42-104">Развертывание реестра контейнеров Azure и его использование</span><span class="sxs-lookup"><span data-stu-id="eac42-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="eac42-105">Реестр контейнеров Azure (ACR) является частным реестром на базе Azure для образов контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="eac42-105">Azure Container Registry (ACR) is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="eac42-106">Этот учебник, часть два из семи, пошаговое руководство по развертыванию экземпляра реестра контейнера Azure и опубликуйте tooit образа контейнера.</span><span class="sxs-lookup"><span data-stu-id="eac42-106">This tutorial, part two of seven, walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="eac42-107">В частности, рассматриваются такие шаги:</span><span class="sxs-lookup"><span data-stu-id="eac42-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eac42-108">развертывание экземпляра реестра контейнеров Azure (ACR);</span><span class="sxs-lookup"><span data-stu-id="eac42-108">Deploying an Azure Container Registry (ACR) instance</span></span>
> * <span data-ttu-id="eac42-109">добавление тегов к образу контейнера для ACR;</span><span class="sxs-lookup"><span data-stu-id="eac42-109">Tagging a container image for ACR</span></span>
> * <span data-ttu-id="eac42-110">Отправка изображения tooACR hello</span><span class="sxs-lookup"><span data-stu-id="eac42-110">Uploading hello image tooACR</span></span>

<span data-ttu-id="eac42-111">В последующих руководствах данный экземпляр ACR интегрируется с кластером Kubernetes службы контейнеров Azure для безопасного выполнения образов контейнеров.</span><span class="sxs-lookup"><span data-stu-id="eac42-111">In subsequent tutorials, this ACR instance is integrated with an Azure Container Service Kubernetes cluster, for securely running container images.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="eac42-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="eac42-112">Before you begin</span></span>

<span data-ttu-id="eac42-113">В hello [с предыдущим учебником](./container-service-tutorial-kubernetes-prepare-app.md), образ контейнера был создан для простого приложения Azure с правом голоса.</span><span class="sxs-lookup"><span data-stu-id="eac42-113">In hello [previous tutorial](./container-service-tutorial-kubernetes-prepare-app.md), a container image was created for a simple Azure Voting application.</span></span> <span data-ttu-id="eac42-114">В этом учебнике это изображение помещается tooan реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="eac42-114">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="eac42-115">Если вы не создали образа приложения Azure с правом голоса hello, возвращают слишком[учебник 1 – Создание образов контейнеров](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="eac42-115">If you have not created hello Azure Voting app image, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> <span data-ttu-id="eac42-116">Кроме того действия hello описанный здесь работают с любой образ контейнера.</span><span class="sxs-lookup"><span data-stu-id="eac42-116">Alternatively, hello steps detailed here work with any container image.</span></span>

<span data-ttu-id="eac42-117">Что вы используете версию Azure CLI hello 2.0.4 упражнений этого учебника нужен или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="eac42-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="eac42-118">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="eac42-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="eac42-119">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eac42-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="eac42-120">Развертывание реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="eac42-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="eac42-121">При развертывании реестра контейнеров Azure сначала необходимо создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eac42-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="eac42-122">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="eac42-122">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="eac42-123">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="eac42-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="eac42-124">В этом примере имя группы ресурсов *myResourceGroup* создается в hello *westeurope* области.</span><span class="sxs-lookup"><span data-stu-id="eac42-124">In this example, a resource group named *myResourceGroup* is created in hello *westeurope* region.</span></span>

```azurecli
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="eac42-125">Создайте в реестре контейнера Azure с hello [создать az acr](/cli/azure/acr#create) команды.</span><span class="sxs-lookup"><span data-stu-id="eac42-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="eac42-126">Имя контейнера реестра Hello **должно быть уникальным**.</span><span class="sxs-lookup"><span data-stu-id="eac42-126">hello name of a Container Registry **must be unique**.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

<span data-ttu-id="eac42-127">На протяжении hello конца данного учебника «acrname» используется как заполнитель для hello контейнер реестра с выбранным именем.</span><span class="sxs-lookup"><span data-stu-id="eac42-127">Throughout hello rest of this tutorial, we use "acrname" as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="eac42-128">Вход в реестр контейнеров</span><span class="sxs-lookup"><span data-stu-id="eac42-128">Container registry login</span></span>

<span data-ttu-id="eac42-129">Необходимо войти в экземпляре ACR tooyour до отправки tooit изображения.</span><span class="sxs-lookup"><span data-stu-id="eac42-129">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="eac42-130">Используйте hello [входа acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) команды toocomplete hello операции.</span><span class="sxs-lookup"><span data-stu-id="eac42-130">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="eac42-131">Необходимо tooprovide hello уникальное имя, заданное реестра toohello контейнера, при его создании.</span><span class="sxs-lookup"><span data-stu-id="eac42-131">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="eac42-132">Команда Hello возвращает сообщение «Успешно выполнен вход» после завершения.</span><span class="sxs-lookup"><span data-stu-id="eac42-132">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-images"></a><span data-ttu-id="eac42-133">Присвоение тегов образам контейнеров</span><span class="sxs-lookup"><span data-stu-id="eac42-133">Tag container images</span></span>

<span data-ttu-id="eac42-134">Каждый образ контейнера должен toobe тегом hello loginServer имя реестра hello.</span><span class="sxs-lookup"><span data-stu-id="eac42-134">Each container image needs toobe tagged with hello loginServer name of hello registry.</span></span> <span data-ttu-id="eac42-135">Данный тег используется для маршрутизации при принудительной установке реестра образов tooan образы контейнера.</span><span class="sxs-lookup"><span data-stu-id="eac42-135">This tag is used for routing when pushing container images tooan image registry.</span></span>

<span data-ttu-id="eac42-136">список текущего изображения, используйте hello toosee [образов docker](https://docs.docker.com/engine/reference/commandline/images/) команды.</span><span class="sxs-lookup"><span data-stu-id="eac42-136">toosee a list of current images, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command.</span></span>

```bash
docker images
```

<span data-ttu-id="eac42-137">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="eac42-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="eac42-138">hello loginServer tooget имя, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="eac42-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="eac42-139">Теперь hello тег *azure голос передней панели* изображение с loginServer hello hello контейнер реестра.</span><span class="sxs-lookup"><span data-stu-id="eac42-139">Now, tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="eac42-140">Кроме того, добавьте `:redis-v1` toohello конец hello имя образа.</span><span class="sxs-lookup"><span data-stu-id="eac42-140">Also, add `:redis-v1` toohello end of hello image name.</span></span> <span data-ttu-id="eac42-141">Этот тег указывает версию образа hello.</span><span class="sxs-lookup"><span data-stu-id="eac42-141">This tag indicates hello image version.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="eac42-142">После с тегами, выполните операцию hello tooverify (https://docs.docker.com/engine/reference/commandline/images/) [образов docker].</span><span class="sxs-lookup"><span data-stu-id="eac42-142">Once tagged, run [docker images] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="eac42-143">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="eac42-143">Output:</span></span>

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a><span data-ttu-id="eac42-144">Принудительная tooregistry изображений</span><span class="sxs-lookup"><span data-stu-id="eac42-144">Push images tooregistry</span></span>

<span data-ttu-id="eac42-145">Принудительная hello *azure голос передней панели* реестра toohello изображения.</span><span class="sxs-lookup"><span data-stu-id="eac42-145">Push hello *azure-vote-front* image toohello registry.</span></span> 

<span data-ttu-id="eac42-146">Используя следующий пример hello, замените имя loginServer ACR hello loginServer hello из среды.</span><span class="sxs-lookup"><span data-stu-id="eac42-146">Using hello following example, replace hello ACR loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

<span data-ttu-id="eac42-147">Это занимает несколько минут toocomplete.</span><span class="sxs-lookup"><span data-stu-id="eac42-147">This takes a couple of minutes toocomplete.</span></span>

## <a name="list-images-in-registry"></a><span data-ttu-id="eac42-148">Перечисление образов в реестре</span><span class="sxs-lookup"><span data-stu-id="eac42-148">List images in registry</span></span>

<span data-ttu-id="eac42-149">tooreturn список образов, которые передаются реестра tooyour контейнера Azure, пользователь hello [списка репозитория acr az](/cli/azure/acr/repository#list) команды.</span><span class="sxs-lookup"><span data-stu-id="eac42-149">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="eac42-150">Обновление hello команды с именем экземпляра ACR hello.</span><span class="sxs-lookup"><span data-stu-id="eac42-150">Update hello command with hello ACR instance name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="eac42-151">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="eac42-151">Output:</span></span>

```azurecli
Result
----------------
azure-vote-front
```

<span data-ttu-id="eac42-152">А затем toosee hello тегов для определенного образа, используйте hello [acr репозитория az show теги](/cli/azure/acr/repository#show-tags) команды.</span><span class="sxs-lookup"><span data-stu-id="eac42-152">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

<span data-ttu-id="eac42-153">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="eac42-153">Output:</span></span>

```azurecli
Result
--------
redis-v1
```

<span data-ttu-id="eac42-154">По завершении учебника образ контейнера hello хранилось в закрытого экземпляра реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="eac42-154">At tutorial completion, hello container image has been stored in a private Azure Container Registry instance.</span></span> <span data-ttu-id="eac42-155">Этот образ развертывается из кластера Kubernetes tooa контроля доступа в последующих учебники.</span><span class="sxs-lookup"><span data-stu-id="eac42-155">This image is deployed from ACR tooa Kubernetes cluster in subsequent tutorials.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eac42-156">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eac42-156">Next steps</span></span>

<span data-ttu-id="eac42-157">В этом руководстве вы подготовили реестр контейнеров Azure для использования в кластере Kubernetes ACS.</span><span class="sxs-lookup"><span data-stu-id="eac42-157">In this tutorial, an Azure Container Registry was prepared for use in an ACS Kubernetes cluster.</span></span> <span data-ttu-id="eac42-158">Привет, следующие шаги были выполнены:</span><span class="sxs-lookup"><span data-stu-id="eac42-158">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eac42-159">развертывание экземпляра реестра контейнеров Azure;</span><span class="sxs-lookup"><span data-stu-id="eac42-159">Deployed an Azure Container Registry instance</span></span>
> * <span data-ttu-id="eac42-160">добавление тегов к образу контейнера для ACR;</span><span class="sxs-lookup"><span data-stu-id="eac42-160">Tagged a container image for ACR</span></span>
> * <span data-ttu-id="eac42-161">Отправленный hello tooACR изображения</span><span class="sxs-lookup"><span data-stu-id="eac42-161">Uploaded hello image tooACR</span></span>

<span data-ttu-id="eac42-162">Переместить следующий учебник toolearn toohello о развертывании Kubernetes кластера в Azure.</span><span class="sxs-lookup"><span data-stu-id="eac42-162">Advance toohello next tutorial toolearn about deploying a Kubernetes cluster in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eac42-163">Развертывание кластера Kubernetes в службе контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="eac42-163">Deploy Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-deploy-cluster.md)