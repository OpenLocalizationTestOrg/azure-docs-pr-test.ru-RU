---
title: "aaaCreate частного реестра Docker - портал Azure | Документы Microsoft"
description: "Начать создание и управление ими частных реестрах контейнера Docker с hello портал Azure"
services: container-registry
documentationcenter: 
author: neilpeterson
manager: timlt
editor: na
tags: 
keywords: 
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: nepeters
ms.custom: na
ms.openlocfilehash: cf3ce0dcf3036d0e9cd1eaf01721deccb00248d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-container-registry-using-hello-azure-portal"></a><span data-ttu-id="816cb-103">Создание управляемого контейнера реестра, с помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="816cb-103">Create a managed container registry using hello Azure portal</span></span>

<span data-ttu-id="816cb-104">Реестр контейнеров Azure — это управляемая служба реестра контейнеров Docker, используемая для хранения частных образов контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="816cb-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="816cb-105">В этом руководстве рассматривается создание экземпляра управляемого реестра контейнера Azure с помощью портала Azure hello.</span><span class="sxs-lookup"><span data-stu-id="816cb-105">This guide details creating a managed Azure Container Registry instance using hello Azure portal.</span></span>

<span data-ttu-id="816cb-106">Управляемые реестры контейнеров Azure находятся на стадии предварительной версии и не доступны во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="816cb-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="816cb-107">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="816cb-107">Log in tooAzure</span></span>

<span data-ttu-id="816cb-108">Войдите в систему toohello портал Azure по адресу http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="816cb-108">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="816cb-109">Создание реестра контейнеров</span><span class="sxs-lookup"><span data-stu-id="816cb-109">Create a container registry</span></span>

1. <span data-ttu-id="816cb-110">Нажмите кнопку hello **New** кнопка найдена в верхнем левом углу hello hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="816cb-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="816cb-111">Поиск hello marketplace для **контейнер Azure реестра** и выберите его.</span><span class="sxs-lookup"><span data-stu-id="816cb-111">Search hello marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="816cb-112">Нажмите кнопку **создать** которого открывается колонка создания ACR hello.</span><span class="sxs-lookup"><span data-stu-id="816cb-112">Click **Create** which will open hello ACR creation blade.</span></span>

    ![Параметры реестра контейнеров](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="816cb-114">В hello **реестра контейнера Azure** колонки, введите следующую информацию hello.</span><span class="sxs-lookup"><span data-stu-id="816cb-114">In hello **Azure Container Registry** blade, enter hello following information.</span></span> <span data-ttu-id="816cb-115">Закончив, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="816cb-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="816cb-116">а.</span><span class="sxs-lookup"><span data-stu-id="816cb-116">a.</span></span> <span data-ttu-id="816cb-117">**Имя реестра** — глобальное уникальное доменное имя верхнего уровня для определенного реестра.</span><span class="sxs-lookup"><span data-stu-id="816cb-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="816cb-118">В этом примере — имя реестра hello *myAzureContainerRegistry1*, но заменить собственным уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="816cb-118">In this example, hello registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="816cb-119">Hello имя может содержать только буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="816cb-119">hello name can contain only letters and numbers.</span></span>

    <span data-ttu-id="816cb-120">b.</span><span class="sxs-lookup"><span data-stu-id="816cb-120">b.</span></span> <span data-ttu-id="816cb-121">**Группа ресурсов**: выберите существующую [группы ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или имя типа hello новую.</span><span class="sxs-lookup"><span data-stu-id="816cb-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span>

    <span data-ttu-id="816cb-122">c.</span><span class="sxs-lookup"><span data-stu-id="816cb-122">c.</span></span> <span data-ttu-id="816cb-123">**Расположение**: Выбор расположения центра обработки данных Azure, где hello службы [доступных](https://azure.microsoft.com/regions/services/), такие как **центральных штатах юга США**.</span><span class="sxs-lookup"><span data-stu-id="816cb-123">**Location**: Select an Azure datacenter location where hello service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="816cb-124">d.</span><span class="sxs-lookup"><span data-stu-id="816cb-124">d.</span></span> <span data-ttu-id="816cb-125">**Пользователю с правами администратора**: следует включить в реестре hello tooaccess пользователя администратора.</span><span class="sxs-lookup"><span data-stu-id="816cb-125">**Admin user**: If you want, enable an admin user tooaccess hello registry.</span></span> <span data-ttu-id="816cb-126">Можно изменить этот параметр после создания hello реестра.</span><span class="sxs-lookup"><span data-stu-id="816cb-126">You can change this setting after creating hello registry.</span></span>

    <span data-ttu-id="816cb-127">д.</span><span class="sxs-lookup"><span data-stu-id="816cb-127">e.</span></span> <span data-ttu-id="816cb-128">**Использование управляемых реестра**: выберите «Да» toohave ACR автоматически Управление хранилищем реестра hello, использование веб-перехватчиков и использование проверки подлинности AAD.</span><span class="sxs-lookup"><span data-stu-id="816cb-128">**Use managed registry**: Select yes toohave ACR automatically manage hello registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="816cb-129">f.</span><span class="sxs-lookup"><span data-stu-id="816cb-129">f.</span></span> <span data-ttu-id="816cb-130">**Ценовая категория.** Выберите ценовую категорию. См. дополнительные сведения о ценах на ACR.</span><span class="sxs-lookup"><span data-stu-id="816cb-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-tooacr-instance"></a><span data-ttu-id="816cb-131">Войдите в экземпляр tooACR</span><span class="sxs-lookup"><span data-stu-id="816cb-131">Log in tooACR instance</span></span>

<span data-ttu-id="816cb-132">Перед принудительной отправки и извлекать образы контейнеров, необходимо войти в экземпляр toohello контроля доступа.</span><span class="sxs-lookup"><span data-stu-id="816cb-132">Before pushing and pulling container images, you must log in toohello ACR instance.</span></span> 

<span data-ttu-id="816cb-133">Таким образом, toodo используйте hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="816cb-133">toodo so, use hello Azure CLI 2.0.</span></span> <span data-ttu-id="816cb-134">Во-первых, при необходимости войдите в Azure, с помощью hello [входа az](/cli/azure/#login) команды.</span><span class="sxs-lookup"><span data-stu-id="816cb-134">First, if needed, log into Azure using hello [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="816cb-135">Затем используйте hello [входа acr az](/cli/azure/acr#login) toolog команды в toohello реестра контейнера Azure.</span><span class="sxs-lookup"><span data-stu-id="816cb-135">Next, use hello [az acr login](/cli/azure/acr#login) command toolog in toohello Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="816cb-136">Использование реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="816cb-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="816cb-137">Список образов контейнеров</span><span class="sxs-lookup"><span data-stu-id="816cb-137">List container images</span></span>

<span data-ttu-id="816cb-138">Используйте hello `az acr` CLI команды tooquery hello изображения и теги в репозитории.</span><span class="sxs-lookup"><span data-stu-id="816cb-138">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="816cb-139">В настоящее время реестре контейнеров не поддерживает hello `docker search` tooquery команды для изображений и теги.</span><span class="sxs-lookup"><span data-stu-id="816cb-139">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="816cb-140">Вывод списка репозиториев</span><span class="sxs-lookup"><span data-stu-id="816cb-140">List repositories</span></span>

<span data-ttu-id="816cb-141">Hello следующий пример формирует список репозиториев hello в реестре, в формате JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="816cb-141">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="816cb-142">Вывод списка тегов</span><span class="sxs-lookup"><span data-stu-id="816cb-142">List tags</span></span>

<span data-ttu-id="816cb-143">Hello следующий пример отображает список тегов hello на hello **образцы/nginx** репозитория, в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="816cb-143">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="816cb-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="816cb-144">Next steps</span></span>

<span data-ttu-id="816cb-145">В этом кратком руководстве вы создали экземпляр управляемого реестра контейнера Azure, используя hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="816cb-145">In this quick start, you've created a managed Azure Container Registry instance using hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="816cb-146">Принудительная первый образ с помощью hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="816cb-146">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
