---
title: "aaaAzure контейнер реестра репозиториев | Документы Microsoft"
description: "Как toouse репозиториями реестра контейнера Azure для Docker images"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a><span data-ttu-id="c2509-103">Создание частного реестра контейнера Docker, с помощью hello Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2509-103">Create a private Docker container registry using hello Azure PowerShell</span></span>
<span data-ttu-id="c2509-104">Использование команд в [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate реестре контейнеров и управлять его параметрами с компьютера Windows.</span><span class="sxs-lookup"><span data-stu-id="c2509-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="c2509-105">Можно также создать и управлять контейнера реестры с помощью hello [портал Azure](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), или программным путем с контейнер реестра hello [API-интерфейса REST](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="c2509-105">You can also create and manage container registries using hello [Azure portal](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with hello Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="c2509-106">Сведения и основные понятия, в разделе [Здравствуйте, Обзор](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="c2509-106">For background and concepts, see [hello overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="c2509-107">Полный список поддерживаемых командлетов см. в разделе [Командлеты управления реестром контейнеров Azure](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="c2509-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c2509-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2509-108">Prerequisites</span></span>
* <span data-ttu-id="c2509-109">**Azure PowerShell**: tooinstall и приступить к работе с Azure PowerShell см. в разделе hello [инструкции по установке](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c2509-109">**Azure PowerShell**: tooinstall and get started with Azure PowerShell, see hello [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="c2509-110">Войдите в tooyour подписки Azure, выполнив `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="c2509-110">Log in tooyour Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="c2509-111">Дополнительные сведения см. в статье [Начало работы с Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="c2509-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="c2509-112">**Группа ресурсов.** Перед созданием реестра контейнеров создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или используйте имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="c2509-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="c2509-113">Убедитесь, что группа ресурсов hello в место, где будет hello реестра контейнера службы [доступных](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="c2509-113">Make sure hello resource group is in a location where hello Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="c2509-114">toocreate группу ресурсов с помощью Azure PowerShell, в разделе [hello Справочник PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="c2509-114">toocreate a resource group using Azure PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="c2509-115">**Учетная запись хранения** (необязательно): создание стандартной Azure [учетной записи хранилища](../storage/common/storage-introduction.md) реестр контейнера hello tooback hello местоположения.</span><span class="sxs-lookup"><span data-stu-id="c2509-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) tooback hello container registry in hello same location.</span></span> <span data-ttu-id="c2509-116">Если не указать учетную запись хранилища при создании реестр с помощью `New-AzureRMContainerRegistry`, hello команда создает ее автоматически.</span><span class="sxs-lookup"><span data-stu-id="c2509-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, hello command creates one for you.</span></span> <span data-ttu-id="c2509-117">toocreate хранилища учетной записи с помощью PowerShell см. в разделе [hello Справочник PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="c2509-117">toocreate a storage account using PowerShell, see [hello PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="c2509-118">Хранилище класса Premium сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="c2509-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="c2509-119">**Субъект-служба (необязательно).** Если реестр создан с помощью PowerShell, по умолчанию доступ к нему не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="c2509-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="c2509-120">В зависимости от потребностей можно назначить существующий реестр tooa основной службы Azure Active Directory или создать и назначить новый.</span><span class="sxs-lookup"><span data-stu-id="c2509-120">Depending on your needs, you can assign an existing Azure Active Directory service principal tooa registry or create and assign a new one.</span></span> <span data-ttu-id="c2509-121">Кроме того можно включить учетную запись пользователя admin hello реестра.</span><span class="sxs-lookup"><span data-stu-id="c2509-121">Alternatively, you can enable hello registry's admin user account.</span></span> <span data-ttu-id="c2509-122">Hello разделах данной статьи.</span><span class="sxs-lookup"><span data-stu-id="c2509-122">See hello sections later in this article.</span></span> <span data-ttu-id="c2509-123">Дополнительные сведения о доступе к реестра см. в разделе [аутентификация с помощью реестра контейнера hello](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="c2509-123">For more information about registry access, see [Authenticate with hello container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="c2509-124">Создание реестра контейнеров</span><span class="sxs-lookup"><span data-stu-id="c2509-124">Create a container registry</span></span>
<span data-ttu-id="c2509-125">Запустите hello `New-AzureRMContainerRegistry` toocreate команда реестра контейнера.</span><span class="sxs-lookup"><span data-stu-id="c2509-125">Run hello `New-AzureRMContainerRegistry` command toocreate a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="c2509-126">При создании реестра укажите глобально уникальное доменное имя верхнего уровня, содержащее только буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="c2509-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="c2509-127">Имя реестра Hello в примерах hello `MyRegistry`, но заменить собственным уникальное имя.</span><span class="sxs-lookup"><span data-stu-id="c2509-127">hello registry name in hello examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="c2509-128">Здравствуйте, следующая команда использует hello минимальные параметры toocreate контейнер реестра `MyRegistry` в группе ресурсов hello `MyResourceGroup` в hello местоположение в США:</span><span class="sxs-lookup"><span data-stu-id="c2509-128">hello following command uses hello minimal parameters toocreate container registry `MyRegistry` in hello resource group `MyResourceGroup` in hello South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="c2509-129">`-StorageAccountName` является необязательным.</span><span class="sxs-lookup"><span data-stu-id="c2509-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="c2509-130">Если не указано, учетную запись хранения создается с именем, содержащим имя реестра hello и отметка времени в hello указал группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c2509-130">If not specified, a storage account is created with a name consisting of hello registry name and a timestamp in hello specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="c2509-131">Назначение субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="c2509-131">Assign a service principal</span></span>
<span data-ttu-id="c2509-132">Использовать команды PowerShell tooassign Azure Active Directory [участника-службы](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa реестра.</span><span class="sxs-lookup"><span data-stu-id="c2509-132">Use PowerShell commands tooassign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa registry.</span></span> <span data-ttu-id="c2509-133">Hello участника-службы в этих примерах назначается роль владельца hello, но можно назначить [других ролей](../active-directory/role-based-access-control-configure.md) Если требуется.</span><span class="sxs-lookup"><span data-stu-id="c2509-133">hello service principal in these examples is assigned hello Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="c2509-134">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="c2509-134">Create a service principal</span></span>
<span data-ttu-id="c2509-135">В hello следующую команду создается новый участника службы.</span><span class="sxs-lookup"><span data-stu-id="c2509-135">In hello following command, a new service principal is created.</span></span> <span data-ttu-id="c2509-136">Укажите надежный пароль для hello `-Password` параметра.</span><span class="sxs-lookup"><span data-stu-id="c2509-136">Specify a strong password with hello `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="c2509-137">Назначение нового или существующего субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="c2509-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="c2509-138">Можно назначить нового или существующего участника tooa реестра службы.</span><span class="sxs-lookup"><span data-stu-id="c2509-138">You can assign a new or an existing service principal tooa registry.</span></span> <span data-ttu-id="c2509-139">tooassign его владельца роли доступа toohello реестра, запустите команду аналогичные toohello, следующий пример:</span><span class="sxs-lookup"><span data-stu-id="c2509-139">tooassign it Owner role access toohello registry, run a command similar toohello following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a><span data-ttu-id="c2509-140">Войдите в реестре toohello с субъектом-службой hello</span><span class="sxs-lookup"><span data-stu-id="c2509-140">Sign in toohello registry with hello service principal</span></span>
<span data-ttu-id="c2509-141">После назначения реестр toohello основной службы hello, можно выполнить вход с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="c2509-141">After assigning hello service principal toohello registry, you can sign in using hello following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="c2509-142">Управление учетными данными администратора</span><span class="sxs-lookup"><span data-stu-id="c2509-142">Manage admin credentials</span></span>
<span data-ttu-id="c2509-143">Учетная запись администратора автоматически создается для каждого реестра контейнеров, но по умолчанию она отключена.</span><span class="sxs-lookup"><span data-stu-id="c2509-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="c2509-144">Hello ниже примерах команд PowerShell toomanage hello учетные данные администратора для реестра контейнера.</span><span class="sxs-lookup"><span data-stu-id="c2509-144">hello following examples show PowerShell commands toomanage hello admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="c2509-145">Получение учетных данных пользователя с правами администратора</span><span class="sxs-lookup"><span data-stu-id="c2509-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="c2509-146">Включение пользователя с правами администратора для имеющегося реестра</span><span class="sxs-lookup"><span data-stu-id="c2509-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="c2509-147">Отключение пользователя с правами администратора для имеющегося реестра</span><span class="sxs-lookup"><span data-stu-id="c2509-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="c2509-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2509-148">Next steps</span></span>
* [<span data-ttu-id="c2509-149">Принудительная первый образ с помощью hello Docker CLI</span><span class="sxs-lookup"><span data-stu-id="c2509-149">Push your first image using hello Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
