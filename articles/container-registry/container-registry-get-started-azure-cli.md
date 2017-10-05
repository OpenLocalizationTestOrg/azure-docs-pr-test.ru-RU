---
title: "Создание частного реестра контейнеров Docker с помощью Azure CLI | Документация Майкрософт"
description: "Приступите к созданию частных реестров контейнеров Docker и управлению ими с помощью Azure CLI 2.0"
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: cristyg
tags: 
keywords: 
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2875f4089231ed12a0312b2c2e077938440365c6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-cli-20"></a><span data-ttu-id="2511c-103">Создание частного реестра контейнеров Docker с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2511c-103">Create a private Docker container registry using the Azure CLI 2.0</span></span>
<span data-ttu-id="2511c-104">Команды в [Azure CLI 2.0](https://github.com/Azure/azure-cli) позволяют создать реестр контейнеров и управлять его параметрами на компьютере Linux, Mac или Windows.</span><span class="sxs-lookup"><span data-stu-id="2511c-104">Use commands in the [Azure CLI 2.0](https://github.com/Azure/azure-cli) to create a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="2511c-105">Кроме того, эти действия можно выполнять на [портале Azure](container-registry-get-started-portal.md) или программным образом с помощью [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376) реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="2511c-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="2511c-106">Общие сведения и основные понятия см. в статье [Общие сведения о службе реестра контейнеров Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="2511c-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="2511c-107">Чтобы получить справку по командам интерфейса командной строки для реестра контейнеров (команды `az acr`), добавьте в любую команду параметр `-h`.</span><span class="sxs-lookup"><span data-stu-id="2511c-107">For help on Container Registry CLI commands (`az acr` commands), pass the `-h` parameter to any command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2511c-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2511c-108">Prerequisites</span></span>
* <span data-ttu-id="2511c-109">**Azure CLI 2.0.** Инструкции по установке Azure CLI 2.0 и началу работы с ним см. [здесь](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2511c-109">**Azure CLI 2.0**: To install and get started with the CLI 2.0, see the [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="2511c-110">Войдите в свою подписку Azure, выполнив команду `az login`.</span><span class="sxs-lookup"><span data-stu-id="2511c-110">Log in to your Azure subscription by running `az login`.</span></span> <span data-ttu-id="2511c-111">Дополнительные сведения см. в статье [Get started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) (Приступая к работе с Azure CLI 2.0).</span><span class="sxs-lookup"><span data-stu-id="2511c-111">For more information, see [Get started with the CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="2511c-112">**Группа ресурсов.** Перед созданием реестра контейнеров создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или используйте имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="2511c-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="2511c-113">Группа ресурсов должна находиться в расположении, где [доступна](https://azure.microsoft.com/regions/services/) служба реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="2511c-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="2511c-114">Справочные материалы по созданию группы ресурсов с помощью CLI 2.0 см. [здесь](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="2511c-114">To create a resource group using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="2511c-115">**Учетная запись хранения (необязательно).** Создайте стандартную [учетную запись хранения](../storage/common/storage-introduction.md) Azure для хранения сведений реестра контейнеров в том же расположении.</span><span class="sxs-lookup"><span data-stu-id="2511c-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="2511c-116">Учетную запись хранения (если она не задана при создании реестра) можно создать с помощью команды `az acr create`.</span><span class="sxs-lookup"><span data-stu-id="2511c-116">If you don't specify a storage account when creating a registry with `az acr create`, the command creates one for you.</span></span> <span data-ttu-id="2511c-117">Справочные материалы по созданию учетной записи хранения с помощью CLI 2.0 см. [здесь](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="2511c-117">To create a storage account using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="2511c-118">Хранилище класса Premium сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="2511c-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="2511c-119">**Субъект-служба (необязательно).** Если реестр создан с помощью интерфейса командной строки, по умолчанию доступ к нему не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="2511c-119">**Service principal** (optional): When you create a registry with the CLI, by default it is not set up for access.</span></span> <span data-ttu-id="2511c-120">В зависимости от потребностей для реестра можно назначить имеющийся субъект-службу Azure Active Directory (или создать и назначить новый) или включить учетную запись пользователя с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="2511c-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry (or create and assign a new one), or enable the registry's admin user account.</span></span> <span data-ttu-id="2511c-121">См. следующие разделы этой статьи.</span><span class="sxs-lookup"><span data-stu-id="2511c-121">See the sections later in this article.</span></span> <span data-ttu-id="2511c-122">Дополнительные сведения о доступе к реестру см. в статье [Authenticate with the container registry](container-registry-authentication.md) (Проверка подлинности с помощью реестра контейнеров).</span><span class="sxs-lookup"><span data-stu-id="2511c-122">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="2511c-123">Создание реестра контейнеров</span><span class="sxs-lookup"><span data-stu-id="2511c-123">Create a container registry</span></span>
<span data-ttu-id="2511c-124">Чтобы создать реестр контейнеров, выполните команду `az acr create`.</span><span class="sxs-lookup"><span data-stu-id="2511c-124">Run the `az acr create` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="2511c-125">При создании реестра укажите глобально уникальное доменное имя верхнего уровня, содержащее только буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="2511c-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="2511c-126">В примерах в качестве имени реестра используется имя `myRegistry1`, но его нужно заменить собственным.</span><span class="sxs-lookup"><span data-stu-id="2511c-126">The registry name in the examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="2511c-127">Следующая команда создает реестр контейнеров `myRegistry1` в группе ресурсов `myResourceGroup`. При этом используются минимальные параметры и SKU *Базовый*.</span><span class="sxs-lookup"><span data-stu-id="2511c-127">The following command uses the minimal parameters to create container registry `myRegistry1` in the resource group `myResourceGroup`, and using the *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="2511c-128">`--storage-account-name` является необязательным.</span><span class="sxs-lookup"><span data-stu-id="2511c-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="2511c-129">Если это не определено, учетная запись хранения создается с именем, состоящим из имени реестра и метки времени в указанной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2511c-129">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

<span data-ttu-id="2511c-130">При создании реестра выходные данные выглядят так:</span><span class="sxs-lookup"><span data-stu-id="2511c-130">When the registry is created, the output is similar to the following:</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T18:36:29.124842+00:00",
  "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry
/registries/myRegistry1",
  "location": "southcentralus",
  "loginServer": "myregistry1.azurecr.io",
  "name": "myRegistry1",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "myregistry123456789"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}

```


<span data-ttu-id="2511c-131">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="2511c-131">Take special note:</span></span>

* <span data-ttu-id="2511c-132">`id` — идентификатор реестра в подписке, необходимый при назначении субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="2511c-132">`id` - Identifier for the registry in your subscription, which you need if you want to assign a service principal.</span></span>
* <span data-ttu-id="2511c-133">`loginServer` — полное доменное имя, которое необходимо указать для [входа в реестр](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="2511c-133">`loginServer` - The fully qualified name you specify to [log in to the registry](container-registry-authentication.md).</span></span> <span data-ttu-id="2511c-134">В рассматриваемом примере это `myregistry1.exp.azurecr.io` (все знаки в нижнем регистре).</span><span class="sxs-lookup"><span data-stu-id="2511c-134">In this example, the name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="2511c-135">Назначение субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="2511c-135">Assign a service principal</span></span>
<span data-ttu-id="2511c-136">Команды в интерфейсе командной строки 2.0 позволяют назначить субъект-службу Azure Active Directory для реестра.</span><span class="sxs-lookup"><span data-stu-id="2511c-136">Use CLI 2.0 commands to assign an Azure Active Directory service principal to a registry.</span></span> <span data-ttu-id="2511c-137">В этих примерах субъект-служба имеет роль владельца, но при необходимости можно назначить [другие роли](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="2511c-137">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-to-the-registry"></a><span data-ttu-id="2511c-138">Создание субъекта-службы и назначение доступа к реестру</span><span class="sxs-lookup"><span data-stu-id="2511c-138">Create a service principal and assign access to the registry</span></span>
<span data-ttu-id="2511c-139">Следующая команда назначает новому субъекту-службе роль владельца для доступа к идентификатору реестра, отправленному с помощью параметра `--scopes`.</span><span class="sxs-lookup"><span data-stu-id="2511c-139">In the following command, a new service principal is assigned Owner role access to the registry identifier passed with the `--scopes` parameter.</span></span> <span data-ttu-id="2511c-140">Укажите надежный пароль с помощью параметра `--password`.</span><span class="sxs-lookup"><span data-stu-id="2511c-140">Specify a strong password with the `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="2511c-141">Назначение имеющегося субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="2511c-141">Assign an existing service principal</span></span>
<span data-ttu-id="2511c-142">Если субъект-службы уже создан и ему необходимо назначить роль владельца для доступа к реестру, выполните команду, аналогичную следующей.</span><span class="sxs-lookup"><span data-stu-id="2511c-142">If you already have a service principal and want to assign it Owner role access to the registry, run a command similar to the following example.</span></span> <span data-ttu-id="2511c-143">Используйте параметр `--assignee`, чтобы передать идентификатор приложения субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="2511c-143">You pass the service principal app ID using the `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="2511c-144">Управление учетными данными администратора</span><span class="sxs-lookup"><span data-stu-id="2511c-144">Manage admin credentials</span></span>
<span data-ttu-id="2511c-145">Учетная запись администратора автоматически создается для каждого реестра контейнеров, но по умолчанию она отключена.</span><span class="sxs-lookup"><span data-stu-id="2511c-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="2511c-146">В приведенных ниже примерах показаны команды `az acr` интерфейса командной строки, используемые для управления учетными данными администратора для реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="2511c-146">The following examples show `az acr` CLI commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="2511c-147">Получение учетных данных пользователя с правами администратора</span><span class="sxs-lookup"><span data-stu-id="2511c-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="2511c-148">Включение пользователя с правами администратора для имеющегося реестра</span><span class="sxs-lookup"><span data-stu-id="2511c-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="2511c-149">Отключение пользователя с правами администратора для имеющегося реестра</span><span class="sxs-lookup"><span data-stu-id="2511c-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="2511c-150">Вывод списка образов и тегов</span><span class="sxs-lookup"><span data-stu-id="2511c-150">List images and tags</span></span>
<span data-ttu-id="2511c-151">Используйте команду `az acr` интерфейса командной строки, чтобы запросить образы и теги в репозитории.</span><span class="sxs-lookup"><span data-stu-id="2511c-151">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="2511c-152">В настоящее время реестр контейнеров не поддерживает команду `docker search`, используемую для запроса образов и тегов.</span><span class="sxs-lookup"><span data-stu-id="2511c-152">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="2511c-153">Вывод списка репозиториев</span><span class="sxs-lookup"><span data-stu-id="2511c-153">List repositories</span></span>
<span data-ttu-id="2511c-154">Следующий пример выводит список репозиториев реестра в формате JSON (нотация объектов JavaScript).</span><span class="sxs-lookup"><span data-stu-id="2511c-154">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="2511c-155">Вывод списка тегов</span><span class="sxs-lookup"><span data-stu-id="2511c-155">List tags</span></span>
<span data-ttu-id="2511c-156">Следующий пример выводит список тегов репозитория **samples/nginx** в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="2511c-156">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="2511c-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2511c-157">Next steps</span></span>
* [<span data-ttu-id="2511c-158">Отправка первого образа с помощью интерфейса командной строки Docker</span><span class="sxs-lookup"><span data-stu-id="2511c-158">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
