---
title: "Учебник экземпляры контейнером aaaAzure - Подготовка реестра контейнера Azure | Документы Microsoft"
description: "Руководство по службе \"Экземпляры контейнеров Azure\". Подготовка реестра контейнеров Azure"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a><span data-ttu-id="e914c-104">Развертывание реестра контейнеров Azure и его использование</span><span class="sxs-lookup"><span data-stu-id="e914c-104">Deploy and use Azure Container Registry</span></span>

<span data-ttu-id="e914c-105">Это вторая часть руководства, состоящего из трех частей.</span><span class="sxs-lookup"><span data-stu-id="e914c-105">This is part two of a three-part tutorial.</span></span> <span data-ttu-id="e914c-106">В hello [ранее](./container-instances-tutorial-prepare-app.md), был создан образ контейнера простого веб-приложения, написанные на [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="e914c-106">In hello [previous step](./container-instances-tutorial-prepare-app.md), a container image was created for a simple web application written in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="e914c-107">В этом учебнике это изображение помещается tooan реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="e914c-107">In this tutorial, this image is pushed tooan Azure Container Registry.</span></span> <span data-ttu-id="e914c-108">Если вы не создали hello образ контейнера, возвращают слишком[учебник 1 – Создание образа контейнера](./container-instances-tutorial-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="e914c-108">If you have not created hello container image, return too[Tutorial 1 – Create container image](./container-instances-tutorial-prepare-app.md).</span></span> 

<span data-ttu-id="e914c-109">Hello реестра контейнера Azure является Azure, частного реестра образов контейнера Docker.</span><span class="sxs-lookup"><span data-stu-id="e914c-109">hello Azure Container Registry is an Azure-based, private registry, for Docker container images.</span></span> <span data-ttu-id="e914c-110">Этот учебник Пошаговое руководство по развертыванию экземпляра реестра контейнера Azure и опубликуйте tooit образа контейнера.</span><span class="sxs-lookup"><span data-stu-id="e914c-110">This tutorial walks through deploying an Azure Container Registry instance, and pushing a container image tooit.</span></span> <span data-ttu-id="e914c-111">В частности, рассматриваются такие шаги:</span><span class="sxs-lookup"><span data-stu-id="e914c-111">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e914c-112">Развертывание экземпляра реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e914c-112">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="e914c-113">Добавление тегов к образу контейнера для помещения в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e914c-113">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="e914c-114">Отправка изображения tooAzure реестра контейнера</span><span class="sxs-lookup"><span data-stu-id="e914c-114">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="e914c-115">В последующих учебники развертывание hello контейнера из вашего частного реестра tooAzure экземпляры контейнером.</span><span class="sxs-lookup"><span data-stu-id="e914c-115">In subsequent tutorials, you deploy hello container from your private registry tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e914c-116">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e914c-116">Before you begin</span></span>

<span data-ttu-id="e914c-117">Что вы используете версию Azure CLI hello 2.0.4 упражнений этого учебника нужен или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e914c-117">This tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e914c-118">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="e914c-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e914c-119">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e914c-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="e914c-120">Развертывание реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e914c-120">Deploy Azure Container Registry</span></span>

<span data-ttu-id="e914c-121">При развертывании реестра контейнеров Azure сначала необходимо создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e914c-121">When deploying an Azure Container Registry, you first need a resource group.</span></span> <span data-ttu-id="e914c-122">Группа ресурсов Azure — это логическая коллекция, в которой выполняется развертывание и администрирование ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="e914c-122">An Azure resource group is a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="e914c-123">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e914c-123">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e914c-124">В этом примере имя группы ресурсов *myResourceGroup* создается в hello *eastus* области.</span><span class="sxs-lookup"><span data-stu-id="e914c-124">In this example, a resource group named *myResourceGroup* is created in hello *eastus* region.</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e914c-125">Создайте в реестре контейнера Azure с hello [создать az acr](/cli/azure/acr#create) команды.</span><span class="sxs-lookup"><span data-stu-id="e914c-125">Create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> <span data-ttu-id="e914c-126">Имя контейнера реестра Hello **должно быть уникальным**.</span><span class="sxs-lookup"><span data-stu-id="e914c-126">hello name of a Container Registry **must be unique**.</span></span> <span data-ttu-id="e914c-127">В следующем примере hello, мы используем имя hello *mycontainerregistry082*.</span><span class="sxs-lookup"><span data-stu-id="e914c-127">In hello following example, we use hello name *mycontainerregistry082*.</span></span>

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

<span data-ttu-id="e914c-128">На протяжении hello конца данного учебника мы используем `<acrname>` как заполнитель для hello контейнер реестра с выбранным именем.</span><span class="sxs-lookup"><span data-stu-id="e914c-128">Throughout hello rest of this tutorial, we use `<acrname>` as a placeholder for hello container registry name that you chose.</span></span>

## <a name="container-registry-login"></a><span data-ttu-id="e914c-129">Вход в реестр контейнеров</span><span class="sxs-lookup"><span data-stu-id="e914c-129">Container registry login</span></span>

<span data-ttu-id="e914c-130">Необходимо войти в экземпляре ACR tooyour до отправки tooit изображения.</span><span class="sxs-lookup"><span data-stu-id="e914c-130">You must log in tooyour ACR instance before pushing images tooit.</span></span> <span data-ttu-id="e914c-131">Используйте hello [входа acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) команды toocomplete hello операции.</span><span class="sxs-lookup"><span data-stu-id="e914c-131">Use hello [az acr login](https://docs.microsoft.com/en-us/cli/azure/acr#login) command toocomplete hello operation.</span></span> <span data-ttu-id="e914c-132">Необходимо tooprovide hello уникальное имя, заданное реестра toohello контейнера, при его создании.</span><span class="sxs-lookup"><span data-stu-id="e914c-132">You need tooprovide hello unique name given toohello container registry when it was created.</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="e914c-133">Команда Hello возвращает сообщение «Успешно выполнен вход» после завершения.</span><span class="sxs-lookup"><span data-stu-id="e914c-133">hello command returns a 'Login Succeeded’ message once completed.</span></span>

## <a name="tag-container-image"></a><span data-ttu-id="e914c-134">Добавление тега к образу контейнера</span><span class="sxs-lookup"><span data-stu-id="e914c-134">Tag container image</span></span>

<span data-ttu-id="e914c-135">toodeploy образ контейнера из частного реестра hello образ нуждается toobe тегом hello `loginServer` имя реестра hello.</span><span class="sxs-lookup"><span data-stu-id="e914c-135">toodeploy a container image from a private registry, hello image needs toobe tagged with hello `loginServer` name of hello registry.</span></span>

<span data-ttu-id="e914c-136">список текущего изображения, используйте hello toosee `docker images` команды.</span><span class="sxs-lookup"><span data-stu-id="e914c-136">toosee a list of current images, use hello `docker images` command.</span></span>

```bash
docker images
```

<span data-ttu-id="e914c-137">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e914c-137">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

<span data-ttu-id="e914c-138">hello loginServer tooget имя, запустите следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="e914c-138">tooget hello loginServer name, run hello following command.</span></span>

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

<span data-ttu-id="e914c-139">Тег hello *aci учебника приложений* изображение с loginServer hello hello контейнер реестра.</span><span class="sxs-lookup"><span data-stu-id="e914c-139">Tag hello *aci-tutorial-app* image with hello loginServer of hello container registry.</span></span> <span data-ttu-id="e914c-140">Кроме того, добавьте `:v1` toohello конец hello имя образа.</span><span class="sxs-lookup"><span data-stu-id="e914c-140">Also, add `:v1` toohello end of hello image name.</span></span> <span data-ttu-id="e914c-141">Этот тег указывает номер версии образа hello.</span><span class="sxs-lookup"><span data-stu-id="e914c-141">This tag indicates hello image version number.</span></span>

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

<span data-ttu-id="e914c-142">После тегов, выполните `docker images` tooverify hello операции.</span><span class="sxs-lookup"><span data-stu-id="e914c-142">Once tagged, run `docker images` tooverify hello operation.</span></span>

```bash
docker images
```

<span data-ttu-id="e914c-143">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e914c-143">Output:</span></span>

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a><span data-ttu-id="e914c-144">Принудительная tooAzure образ контейнера реестра</span><span class="sxs-lookup"><span data-stu-id="e914c-144">Push image tooAzure Container Registry</span></span>

<span data-ttu-id="e914c-145">Принудительная hello *aci учебника приложения* toohello реестра образов.</span><span class="sxs-lookup"><span data-stu-id="e914c-145">Push hello *aci-tutorial-app* image toohello registry.</span></span>

<span data-ttu-id="e914c-146">Используя следующий пример hello, замените имя loginServer реестра контейнера hello loginServer hello из среды.</span><span class="sxs-lookup"><span data-stu-id="e914c-146">Using hello following example, replace hello container registry loginServer name with hello loginServer from your environment.</span></span>

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a><span data-ttu-id="e914c-147">Получение списка образов в реестре контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e914c-147">List images in Azure Container Registry</span></span>

<span data-ttu-id="e914c-148">tooreturn список образов, которые передаются реестра tooyour контейнера Azure, пользователь hello [списка репозитория acr az](/cli/azure/acr/repository#list) команды.</span><span class="sxs-lookup"><span data-stu-id="e914c-148">tooreturn a list of images that have been pushed tooyour Azure Container registry, user hello [az acr repository list](/cli/azure/acr/repository#list) command.</span></span> <span data-ttu-id="e914c-149">Обновление hello команды с именем реестра hello контейнера.</span><span class="sxs-lookup"><span data-stu-id="e914c-149">Update hello command with hello container registry name.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="e914c-150">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e914c-150">Output:</span></span>

```azurecli
Result
----------------
aci-tutorial-app
```

<span data-ttu-id="e914c-151">А затем toosee hello тегов для определенного образа, используйте hello [acr репозитория az show теги](/cli/azure/acr/repository#show-tags) команды.</span><span class="sxs-lookup"><span data-stu-id="e914c-151">And then toosee hello tags for a specific image, use hello [az acr repository show-tags](/cli/azure/acr/repository#show-tags) command.</span></span>

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

<span data-ttu-id="e914c-152">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="e914c-152">Output:</span></span>

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a><span data-ttu-id="e914c-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e914c-153">Next steps</span></span>

<span data-ttu-id="e914c-154">В этом учебнике в реестре контейнера Azure был подготовлен для использования с экземплярами Azure контейнера и занесен hello образ контейнера.</span><span class="sxs-lookup"><span data-stu-id="e914c-154">In this tutorial, an Azure Container Registry was prepared for use with Azure Container Instances, and hello container image was pushed.</span></span> <span data-ttu-id="e914c-155">Привет, следующие шаги были выполнены:</span><span class="sxs-lookup"><span data-stu-id="e914c-155">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e914c-156">Развертывание экземпляра реестра контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e914c-156">Deploying an Azure Container Registry instance</span></span>
> * <span data-ttu-id="e914c-157">Добавление тегов к образу контейнера для помещения в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e914c-157">Tagging container image for Azure Container Registry</span></span>
> * <span data-ttu-id="e914c-158">Отправка изображения tooAzure реестра контейнера</span><span class="sxs-lookup"><span data-stu-id="e914c-158">Uploading image tooAzure Container Registry</span></span>

<span data-ttu-id="e914c-159">Переместить Далее учебника toolearn toohello о развертывании tooAzure hello контейнера, с помощью экземпляров контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="e914c-159">Advance toohello next tutorial toolearn about deploying hello container tooAzure using Azure Container Instances.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e914c-160">Развертывание контейнеров tooAzure экземпляры контейнером</span><span class="sxs-lookup"><span data-stu-id="e914c-160">Deploy containers tooAzure Container Instances</span></span>](./container-instances-tutorial-deploy-app.md)
