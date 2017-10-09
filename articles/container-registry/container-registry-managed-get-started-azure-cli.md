---
title: "aaaCreate частного реестра контейнера Docker - Azure CLI | Документы Microsoft"
description: "Начать создание и управление ими частных реестрах контейнера Docker с hello Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: 2cadf42db0681a09c95486510f1e65c6f87c5280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-cli"></a><span data-ttu-id="0bf6a-103">Создание управляемого контейнера реестра, с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0bf6a-103">Create a managed container registry using hello Azure CLI</span></span>

<span data-ttu-id="0bf6a-104">Реестр контейнеров Azure — это управляемая служба реестра контейнеров Docker, используемая для хранения частных образов контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="0bf6a-105">В этом руководстве рассматривается создание экземпляра управляемого реестра контейнера Azure с помощью hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-105">This guide details creating a managed Azure Container Registry instance using hello Azure CLI.</span></span>

<span data-ttu-id="0bf6a-106">Управляемые реестры контейнеров Azure находятся на стадии предварительной версии и не доступны во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0bf6a-107">Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0bf6a-108">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0bf6a-109">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0bf6a-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="0bf6a-110">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="0bf6a-110">Create a resource group</span></span>

<span data-ttu-id="0bf6a-111">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="0bf6a-112">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="0bf6a-113">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *westcentralus* расположение.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-113">hello following example creates a resource group named *myResourceGroup* in hello *westcentralus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-container-registry"></a><span data-ttu-id="0bf6a-114">Создание реестра контейнеров</span><span class="sxs-lookup"><span data-stu-id="0bf6a-114">Create a container registry</span></span>

<span data-ttu-id="0bf6a-115">Создание экземпляра контроля доступа с помощью hello [создать az acr](/cli/azure/acr#create) команды.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-115">Create an ACR instance using hello [az acr create](/cli/azure/acr#create) command.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf6a-116">При создании реестра укажите глобально уникальное доменное имя верхнего уровня, содержащее только буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-116">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span>

 <span data-ttu-id="0bf6a-117">Имя реестра Hello в примере hello *myContainerRegistry1*, подставьте собственные уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-117">hello registry name in hello example is *myContainerRegistry1*, substitute a unique name of your own.</span></span>

```azurecli
az acr create --name myContainerRegistry1 --resource-group myResourceGroup --sku Managed_Standard
```

<span data-ttu-id="0bf6a-118">При создании реестра hello hello выводится примерно следующее toohello:</span><span class="sxs-lookup"><span data-stu-id="0bf6a-118">When hello registry is created, hello output is similar toohello following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-29T04:50:28.607134+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry1",
  "location": "westcentralus",
  "loginServer": "mycontainerregistry1.azurecr.io",
  "name": "myContainerRegistry1",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Managed_Standard",
    "tier": "Managed"
  },
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="0bf6a-119">Войдите в экземпляр tooACR</span><span class="sxs-lookup"><span data-stu-id="0bf6a-119">Log in tooACR instance</span></span>

<span data-ttu-id="0bf6a-120">Перед принудительной отправки и извлекать образы контейнеров, необходимо войти в экземпляр toohello контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-120">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> <span data-ttu-id="0bf6a-121">toodo таким образом, используйте hello [входа acr az](/cli/azure/acr#login) команды.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-121">toodo so, use hello [az acr login](/cli/azure/acr#login) command.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

<span data-ttu-id="0bf6a-122">Команда Hello возвращает сообщение «Успешно выполнен вход» после завершения.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-122">hello command returns a 'Login Succeeded' message once completed.</span></span>

## <a name="use-azure-container-registry"></a><span data-ttu-id="0bf6a-123">Использование реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="0bf6a-123">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="0bf6a-124">Список образов контейнеров</span><span class="sxs-lookup"><span data-stu-id="0bf6a-124">List container images</span></span>

<span data-ttu-id="0bf6a-125">Используйте hello `az acr` CLI команды tooquery hello изображения и теги в репозитории.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-125">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="0bf6a-126">В настоящее время реестре контейнеров не поддерживает hello `docker search` tooquery команды для изображений и теги.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-126">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="0bf6a-127">Вывод списка репозиториев</span><span class="sxs-lookup"><span data-stu-id="0bf6a-127">List repositories</span></span>

<span data-ttu-id="0bf6a-128">Hello следующий пример формирует список репозиториев hello в реестре, в формате JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="0bf6a-128">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="0bf6a-129">Вывод списка тегов</span><span class="sxs-lookup"><span data-stu-id="0bf6a-129">List tags</span></span>

<span data-ttu-id="0bf6a-130">Hello следующий пример отображает список тегов hello на hello **образцы/nginx** репозитория, в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="0bf6a-130">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="0bf6a-131">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0bf6a-131">Next steps</span></span>

<span data-ttu-id="0bf6a-132">В этом кратком руководстве вы создали экземпляр управляемого реестра контейнера Azure, используя hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0bf6a-132">In this quick start, you've created a managed Azure Container Registry instance using hello Azure CLI.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0bf6a-133">Принудительная первый образ с помощью hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="0bf6a-133">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
