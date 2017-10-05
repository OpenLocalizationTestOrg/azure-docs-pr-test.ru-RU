---
title: "Создание частного реестра Docker с помощью портала Azure | Документация Майкрософт"
description: "Приступите к созданию частных реестров контейнеров Docker и управлению ими с помощью портала Azure"
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
ms.openlocfilehash: 560aee42b0c5a61c37c594d7937f833ab7183d49
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-managed-container-registry-using-the-azure-portal"></a><span data-ttu-id="e5cec-103">Создание управляемого реестра контейнеров с помощью портала Azure</span><span class="sxs-lookup"><span data-stu-id="e5cec-103">Create a managed container registry using the Azure portal</span></span>

<span data-ttu-id="e5cec-104">Реестр контейнеров Azure — это управляемая служба реестра контейнеров Docker, используемая для хранения частных образов контейнеров Docker.</span><span class="sxs-lookup"><span data-stu-id="e5cec-104">Azure Container Registry is a managed Docker container registry service used for storing private Docker container images.</span></span> <span data-ttu-id="e5cec-105">В этом руководстве рассматривается создание экземпляра управляемого реестра контейнеров Azure с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="e5cec-105">This guide details creating a managed Azure Container Registry instance using the Azure portal.</span></span>

<span data-ttu-id="e5cec-106">Управляемые реестры контейнеров Azure находятся на стадии предварительной версии и не доступны во всех регионах.</span><span class="sxs-lookup"><span data-stu-id="e5cec-106">Managed Azure container registries are in preview and not available in all regions.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="e5cec-107">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="e5cec-107">Log in to Azure</span></span>

<span data-ttu-id="e5cec-108">Войдите на портал Azure по адресу http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="e5cec-108">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="e5cec-109">Создание реестра контейнеров</span><span class="sxs-lookup"><span data-stu-id="e5cec-109">Create a container registry</span></span>

1. <span data-ttu-id="e5cec-110">Щелкните **Создать** в верхнем левом углу портала Azure.</span><span class="sxs-lookup"><span data-stu-id="e5cec-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="e5cec-111">Найдите в Marketplace **реестр контейнеров Azure** и выберите его.</span><span class="sxs-lookup"><span data-stu-id="e5cec-111">Search the marketplace for **Azure container registry** and select it.</span></span>

3. <span data-ttu-id="e5cec-112">Щелкните **Создать**, после чего откроется колонка создания ACR.</span><span class="sxs-lookup"><span data-stu-id="e5cec-112">Click **Create** which will open the ACR creation blade.</span></span>

    ![Параметры реестра контейнеров](./media/container-registry-get-started-portal/managed-container-registry-settings.png)

4. <span data-ttu-id="e5cec-114">В колонке **Реестр контейнеров Azure** введите следующую информацию.</span><span class="sxs-lookup"><span data-stu-id="e5cec-114">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="e5cec-115">Закончив, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e5cec-115">Click **Create** when you are done.</span></span>

    <span data-ttu-id="e5cec-116">а.</span><span class="sxs-lookup"><span data-stu-id="e5cec-116">a.</span></span> <span data-ttu-id="e5cec-117">**Имя реестра** — глобальное уникальное доменное имя верхнего уровня для определенного реестра.</span><span class="sxs-lookup"><span data-stu-id="e5cec-117">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="e5cec-118">В этом примере в качестве имени реестра используется имя *myAzureContainerRegistry1*, но его нужно заменить собственным.</span><span class="sxs-lookup"><span data-stu-id="e5cec-118">In this example, the registry name is *myAzureContainerRegistry1*, but substitute a unique name of your own.</span></span> <span data-ttu-id="e5cec-119">Имя может содержать только буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="e5cec-119">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="e5cec-120">b.</span><span class="sxs-lookup"><span data-stu-id="e5cec-120">b.</span></span> <span data-ttu-id="e5cec-121">**Группа ресурсов.** Выберите имеющуюся [группу ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или укажите имя, чтобы создать новую.</span><span class="sxs-lookup"><span data-stu-id="e5cec-121">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="e5cec-122">c.</span><span class="sxs-lookup"><span data-stu-id="e5cec-122">c.</span></span> <span data-ttu-id="e5cec-123">**Расположение.** Выберите расположение центра обработки данных Azure, в котором [доступна](https://azure.microsoft.com/regions/services/) служба, например **юго-центральный регион США**.</span><span class="sxs-lookup"><span data-stu-id="e5cec-123">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="e5cec-124">г)</span><span class="sxs-lookup"><span data-stu-id="e5cec-124">d.</span></span> <span data-ttu-id="e5cec-125">**Пользователь-администратор.** При необходимости укажите пользователя с правами администратора для доступа к реестру.</span><span class="sxs-lookup"><span data-stu-id="e5cec-125">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="e5cec-126">Этот параметр можно изменить после создания реестра.</span><span class="sxs-lookup"><span data-stu-id="e5cec-126">You can change this setting after creating the registry.</span></span>

    <span data-ttu-id="e5cec-127">д.</span><span class="sxs-lookup"><span data-stu-id="e5cec-127">e.</span></span> <span data-ttu-id="e5cec-128">**Использование управляемого реестра.** Выберите "Да", чтобы ACR автоматически управлял хранилищем реестров, использовал веб-перехватчики и проверку подлинности AAD.</span><span class="sxs-lookup"><span data-stu-id="e5cec-128">**Use managed registry**: Select yes to have ACR automatically manage the registry storage, use webhooks, and use AAD authentication.</span></span>

    <span data-ttu-id="e5cec-129">Е.</span><span class="sxs-lookup"><span data-stu-id="e5cec-129">f.</span></span> <span data-ttu-id="e5cec-130">**Ценовая категория.** Выберите ценовую категорию. См. дополнительные сведения о ценах на ACR.</span><span class="sxs-lookup"><span data-stu-id="e5cec-130">**Pricing Tier**: Select a pricing tier, see here ACR pricing for more information.</span></span>

## <a name="log-in-to-acr-instance"></a><span data-ttu-id="e5cec-131">Вход в экземпляр ACR</span><span class="sxs-lookup"><span data-stu-id="e5cec-131">Log in to ACR instance</span></span>

<span data-ttu-id="e5cec-132">Перед отправкой и извлечением образов контейнеров необходимо войти в экземпляр ACR.</span><span class="sxs-lookup"><span data-stu-id="e5cec-132">Before pushing and pulling container images, you must log in to the ACR instance.</span></span> 

<span data-ttu-id="e5cec-133">Чтобы сделать это, используйте Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="e5cec-133">To do so, use the Azure CLI 2.0.</span></span> <span data-ttu-id="e5cec-134">Во-первых, при необходимости войдите в Azure с помощью команды [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e5cec-134">First, if needed, log into Azure using the [az login](/cli/azure/#login) command.</span></span> 

```azurecli
az login
```

<span data-ttu-id="e5cec-135">Затем используйте команду [az acr login](/cli/azure/acr#login), чтобы войти в реестр контейнеров Azure.</span><span class="sxs-lookup"><span data-stu-id="e5cec-135">Next, use the [az acr login](/cli/azure/acr#login) command to log in to the Azure Container Registry.</span></span>

```azurecli-interactive
az acr login --name myAzureContainerRegistry1
```

## <a name="use-azure-container-registry"></a><span data-ttu-id="e5cec-136">Использование реестра контейнеров Azure</span><span class="sxs-lookup"><span data-stu-id="e5cec-136">Use Azure Container Registry</span></span>

### <a name="list-container-images"></a><span data-ttu-id="e5cec-137">Список образов контейнеров</span><span class="sxs-lookup"><span data-stu-id="e5cec-137">List container images</span></span>

<span data-ttu-id="e5cec-138">Используйте команду `az acr` интерфейса командной строки, чтобы запросить образы и теги в репозитории.</span><span class="sxs-lookup"><span data-stu-id="e5cec-138">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="e5cec-139">В настоящее время реестр контейнеров не поддерживает команду `docker search`, используемую для запроса образов и тегов.</span><span class="sxs-lookup"><span data-stu-id="e5cec-139">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>

### <a name="list-repositories"></a><span data-ttu-id="e5cec-140">Вывод списка репозиториев</span><span class="sxs-lookup"><span data-stu-id="e5cec-140">List repositories</span></span>

<span data-ttu-id="e5cec-141">Следующий пример выводит список репозиториев реестра в формате JSON (нотация объектов JavaScript).</span><span class="sxs-lookup"><span data-stu-id="e5cec-141">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myContainerRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="e5cec-142">Вывод списка тегов</span><span class="sxs-lookup"><span data-stu-id="e5cec-142">List tags</span></span>

<span data-ttu-id="e5cec-143">Следующий пример выводит список тегов репозитория **samples/nginx** в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="e5cec-143">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myContainerRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="e5cec-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e5cec-144">Next steps</span></span>

<span data-ttu-id="e5cec-145">В этом кратком руководстве вы создали управляемый экземпляр реестра контейнеров Azure с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="e5cec-145">In this quick start, you've created a managed Azure Container Registry instance using the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5cec-146">Отправка первого образа с помощью интерфейса командной строки Docker</span><span class="sxs-lookup"><span data-stu-id="e5cec-146">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)