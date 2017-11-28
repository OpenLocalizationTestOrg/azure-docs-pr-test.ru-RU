---
title: "aaaCreate частного реестра контейнера Docker - Azure CLI | Документы Microsoft"
description: "Начать создание и управление ими частных реестрах контейнера Docker с hello Azure CLI 2.0"
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
ms.openlocfilehash: f0d876a70b71a5e1bd564fbc9198f693dfe8a347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-cli-20"></a><span data-ttu-id="b8a4a-103">Создание частного реестра контейнера Docker, с помощью Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="b8a4a-103">Create a private Docker container registry using hello Azure CLI 2.0</span></span>
<span data-ttu-id="b8a4a-104">Использование команд в hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate реестре контейнеров и управлять его параметрами с компьютера Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-104">Use commands in hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) toocreate a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="b8a4a-105">Можно также создать и управлять контейнера реестры с помощью hello [портал Azure](container-registry-get-started-portal.md) или программным путем с контейнер реестра hello [API-интерфейса REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md) or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="b8a4a-106">Сведения и основные понятия, в разделе [Здравствуйте, Обзор](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="b8a4a-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="b8a4a-107">Для получения справки о командах CLI реестра контейнера (`az acr` команды), передать hello `-h` параметр tooany команды.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-107">For help on Container Registry CLI commands (`az acr` commands), pass hello `-h` parameter tooany command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b8a4a-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b8a4a-108">Prerequisites</span></span>
* <span data-ttu-id="b8a4a-109">**Azure CLI 2.0**: tooinstall и приступить к работе с hello CLI 2.0 см. в разделе hello [инструкции по установке](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-109">**Azure CLI 2.0**: tooinstall and get started with hello CLI 2.0, see hello [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="b8a4a-110">Войдите в tooyour подписки Azure, выполнив `az login`.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-110">Log in tooyour Azure subscription by running `az login`.</span></span> <span data-ttu-id="b8a4a-111">Дополнительные сведения см. в разделе [Приступая к работе с hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-111">For more information, see [Get started with hello CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="b8a4a-112">**Группа ресурсов.** Перед созданием реестра контейнеров создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или используйте имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="b8a4a-113">Убедитесь, что группа ресурсов hello в место, где будет hello реестра контейнера службы [доступных](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="b8a4a-114">группы ресурсов с помощью toocreate hello CLI версии 2.0, в разделе [hello CLI 2.0 ссылка](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-114">toocreate a resource group using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="b8a4a-115">**Учетная запись хранения** (необязательно): создание стандартной Azure [учетной записи хранилища](../storage/common/storage-introduction.md) реестр контейнера hello tooback hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="b8a4a-116">Если не указать учетную запись хранилища при создании реестр с помощью `az acr create`, hello команда создает ее автоматически.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-116">If you don't specify a storage account when creating a registry with `az acr create`, hello command creates one for you.</span></span> <span data-ttu-id="b8a4a-117">учетную запись хранилища, используя toocreate hello CLI 2.0 см. в разделе [hello CLI 2.0 ссылка](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-117">toocreate a storage account using hello CLI 2.0, see [hello CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="b8a4a-118">Хранилище класса Premium сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="b8a4a-119">**Субъект-служба** (необязательно): при создании файла реестра с hello CLI по умолчанию он не настроен для доступа.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-119">**Service principal** (optional): When you create a registry with hello CLI, by default it is not set up for access.</span></span> <span data-ttu-id="b8a4a-120">В зависимости от потребностей, можно назначить существующий реестр tooa основной службы Azure Active Directory (или создать и назначить новый), или включить учетную запись пользователя admin hello реестра.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry (or create and assign a new one), or enable hello registry's admin user account.</span></span> <span data-ttu-id="b8a4a-121">Hello разделах данной статьи.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-121">See hello sections later in this article.</span></span> <span data-ttu-id="b8a4a-122">Дополнительные сведения о доступе к реестра см. в разделе [аутентификация с помощью реестра контейнера hello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-122">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="b8a4a-123">Создание реестра контейнеров</span><span class="sxs-lookup"><span data-stu-id="b8a4a-123">Create a container registry</span></span>
<span data-ttu-id="b8a4a-124">Запустите hello `az acr create` toocreate команда реестра контейнера.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-124">Run hello `az acr create` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="b8a4a-125">При создании реестра укажите глобально уникальное доменное имя верхнего уровня, содержащее только буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="b8a4a-126">Имя реестра Hello в примерах hello `myRegistry1`, но заменить собственным уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-126">hello registry name in hello examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="b8a4a-127">Здравствуйте, следующая команда использует hello минимальные параметры toocreate контейнер реестра `myRegistry1` в группе ресурсов hello `myResourceGroup`и с помощью hello *основные* sku:</span><span class="sxs-lookup"><span data-stu-id="b8a4a-127">hello following command uses hello minimal parameters toocreate container registry `myRegistry1` in hello resource group `myResourceGroup`, and using hello *Basic* sku:</span></span>

```azurecli
az acr create --name myRegistry1 --resource-group myResourceGroup --sku Basic
```

* <span data-ttu-id="b8a4a-128">`--storage-account-name` является необязательным.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="b8a4a-129">Если не указано, учетную запись хранения создается с именем, содержащим имя реестра hello и отметка времени в hello указал группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-129">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

<span data-ttu-id="b8a4a-130">При создании реестра hello hello выводится примерно следующее toohello:</span><span class="sxs-lookup"><span data-stu-id="b8a4a-130">When hello registry is created, hello output is similar toohello following:</span></span>

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


<span data-ttu-id="b8a4a-131">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-131">Take special note:</span></span>

* <span data-ttu-id="b8a4a-132">`id`-Идентификатор для раздела реестра hello в вашей подписке, требуется, если вы хотите tooassign участника службы.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-132">`id` - Identifier for hello registry in your subscription, which you need if you want tooassign a service principal.</span></span>
* <span data-ttu-id="b8a4a-133">`loginServer`-Полное имя hello указании слишком[входа в реестре toohello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-133">`loginServer` - hello fully qualified name you specify too[log in toohello registry](container-registry-authentication.md).</span></span> <span data-ttu-id="b8a4a-134">В этом примере имеет имя hello `myregistry1.exp.azurecr.io` (прописными буквами).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-134">In this example, hello name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="b8a4a-135">Назначение субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="b8a4a-135">Assign a service principal</span></span>
<span data-ttu-id="b8a4a-136">С помощью команды CLI 2.0 tooassign реестр tooa основной службы Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-136">Use CLI 2.0 commands tooassign an Azure Active Directory service principal tooa registry.</span></span> <span data-ttu-id="b8a4a-137">Hello участника-службы в этих примерах назначается роль владельца hello, но можно назначить [других ролей](../active-directory/role-based-access-control-configure.md) Если требуется.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-137">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-toohello-registry"></a><span data-ttu-id="b8a4a-138">Создание участника службы и назначение доступа toohello реестра</span><span class="sxs-lookup"><span data-stu-id="b8a4a-138">Create a service principal and assign access toohello registry</span></span>
<span data-ttu-id="b8a4a-139">В hello следующую команду, субъекта-службы назначается идентификатор владельца роли доступа toohello реестра, переданный с hello `--scopes` параметра.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-139">In hello following command, a new service principal is assigned Owner role access toohello registry identifier passed with hello `--scopes` parameter.</span></span> <span data-ttu-id="b8a4a-140">Укажите надежный пароль для hello `--password` параметра.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-140">Specify a strong password with hello `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="b8a4a-141">Назначение имеющегося субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="b8a4a-141">Assign an existing service principal</span></span>
<span data-ttu-id="b8a4a-142">Если вы уже участника службы и хотите tooassign его владельца роли доступа toohello реестра, запустите команду аналогичные toohello, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-142">If you already have a service principal and want tooassign it Owner role access toohello registry, run a command similar toohello following example.</span></span> <span data-ttu-id="b8a4a-143">Передайте идентификатор основного приложения службы hello, с помощью hello `--assignee` параметр:</span><span class="sxs-lookup"><span data-stu-id="b8a4a-143">You pass hello service principal app ID using hello `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="b8a4a-144">Управление учетными данными администратора</span><span class="sxs-lookup"><span data-stu-id="b8a4a-144">Manage admin credentials</span></span>
<span data-ttu-id="b8a4a-145">Учетная запись администратора автоматически создается для каждого реестра контейнеров, но по умолчанию она отключена.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-145">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="b8a4a-146">Здравствуйте, следующие примеры `az acr` CLI команды toomanage hello учетные данные администратора для реестра контейнера.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-146">hello following examples show `az acr` CLI commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="b8a4a-147">Получение учетных данных пользователя с правами администратора</span><span class="sxs-lookup"><span data-stu-id="b8a4a-147">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="b8a4a-148">Включение пользователя с правами администратора для имеющегося реестра</span><span class="sxs-lookup"><span data-stu-id="b8a4a-148">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="b8a4a-149">Отключение пользователя с правами администратора для имеющегося реестра</span><span class="sxs-lookup"><span data-stu-id="b8a4a-149">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="b8a4a-150">Вывод списка образов и тегов</span><span class="sxs-lookup"><span data-stu-id="b8a4a-150">List images and tags</span></span>
<span data-ttu-id="b8a4a-151">Используйте hello `az acr` CLI команды tooquery hello изображения и теги в репозитории.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-151">Use hello `az acr` CLI commands tooquery hello images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="b8a4a-152">В настоящее время реестре контейнеров не поддерживает hello `docker search` tooquery команды для изображений и теги.</span><span class="sxs-lookup"><span data-stu-id="b8a4a-152">Currently, Container Registry does not support hello `docker search` command tooquery for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="b8a4a-153">Вывод списка репозиториев</span><span class="sxs-lookup"><span data-stu-id="b8a4a-153">List repositories</span></span>
<span data-ttu-id="b8a4a-154">Hello следующий пример формирует список репозиториев hello в реестре, в формате JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="b8a4a-154">hello following example lists hello repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="b8a4a-155">Вывод списка тегов</span><span class="sxs-lookup"><span data-stu-id="b8a4a-155">List tags</span></span>
<span data-ttu-id="b8a4a-156">Hello следующий пример отображает список тегов hello на hello **образцы/nginx** репозитория, в формате JSON:</span><span class="sxs-lookup"><span data-stu-id="b8a4a-156">hello following example lists hello tags on hello **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="b8a4a-157">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b8a4a-157">Next steps</span></span>
* [<span data-ttu-id="b8a4a-158">Принудительная первый образ с помощью hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="b8a4a-158">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
