---
title: "Репозитории реестра контейнеров Azure | Документация Майкрософт"
description: "Использование репозиториев реестра контейнеров Azure для образов Docker"
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
ms.openlocfilehash: 1e5d5ea5b1ec121fe008abc48178b1d58f540ce1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-private-docker-container-registry-using-the-azure-powershell"></a><span data-ttu-id="43769-103">Создание частного реестра контейнеров Docker с помощью Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="43769-103">Create a private Docker container registry using the Azure PowerShell</span></span>
<span data-ttu-id="43769-104">Команды в [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) позволяют создать реестр контейнеров и управлять его параметрами с компьютера Windows.</span><span class="sxs-lookup"><span data-stu-id="43769-104">Use commands in [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) to create a container registry and manage its settings from your Windows computer.</span></span> <span data-ttu-id="43769-105">Кроме того, эти действия можно выполнять на [портале Azure](container-registry-get-started-portal.md), в [интерфейсе командной строки Azure](container-registry-get-started-azure-cli.md) или программными средствами с помощью [API REST](https://go.microsoft.com/fwlink/p/?linkid=834376) реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="43769-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md), the [Azure CLI](container-registry-get-started-azure-cli.md), or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="43769-106">Общие сведения и основные понятия см. в статье [Общие сведения о службе реестра контейнеров Azure](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="43769-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="43769-107">Полный список поддерживаемых командлетов см. в разделе [Командлеты управления реестром контейнеров Azure](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span><span class="sxs-lookup"><span data-stu-id="43769-107">For a full list of supported cmdlets, see [Azure Container Registry Management Cmdlets](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="43769-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="43769-108">Prerequisites</span></span>
* <span data-ttu-id="43769-109">**Azure PowerShell.** Инструкции по установке и началу работы с Azure PowerShell см. [здесь](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="43769-109">**Azure PowerShell**: To install and get started with Azure PowerShell, see the [installation instructions](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="43769-110">Войдите в свою подписку Azure, выполнив команду `Login-AzureRMAccount`.</span><span class="sxs-lookup"><span data-stu-id="43769-110">Log in to your Azure subscription by running `Login-AzureRMAccount`.</span></span> <span data-ttu-id="43769-111">Дополнительные сведения см. в статье [Начало работы с Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span><span class="sxs-lookup"><span data-stu-id="43769-111">For more information, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).</span></span>
* <span data-ttu-id="43769-112">**Группа ресурсов.** Перед созданием реестра контейнеров создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или используйте имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="43769-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="43769-113">Группа ресурсов должна находиться в расположении, где [доступна](https://azure.microsoft.com/regions/services/) служба реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="43769-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="43769-114">Сведения о создании группы ресурсов с помощью Azure PowerShell см. в [справочнике по PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span><span class="sxs-lookup"><span data-stu-id="43769-114">To create a resource group using Azure PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).</span></span>
* <span data-ttu-id="43769-115">**Учетная запись хранения (необязательно).** Создайте стандартную [учетную запись хранения](../storage/common/storage-introduction.md) Azure для хранения сведений реестра контейнеров в том же расположении.</span><span class="sxs-lookup"><span data-stu-id="43769-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/common/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="43769-116">Учетную запись хранения (если она не задана при создании реестра) можно создать с помощью команды `New-AzureRMContainerRegistry`.</span><span class="sxs-lookup"><span data-stu-id="43769-116">If you don't specify a storage account when creating a registry with `New-AzureRMContainerRegistry`, the command creates one for you.</span></span> <span data-ttu-id="43769-117">Сведения о создании учетной записи хранения с помощью Azure PowerShell см. в [справочнике по PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span><span class="sxs-lookup"><span data-stu-id="43769-117">To create a storage account using PowerShell, see [the PowerShell reference](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount).</span></span> <span data-ttu-id="43769-118">Хранилище класса Premium сейчас не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="43769-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="43769-119">**Субъект-служба (необязательно).** Если реестр создан с помощью PowerShell, по умолчанию доступ к нему не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="43769-119">**Service principal** (optional): When you create a registry with PowerShell, by default it is not set up for access.</span></span> <span data-ttu-id="43769-120">В зависимости от ваших требований можно назначить для реестра существующий субъект-службу Azure Active Directory или создать и назначить новый.</span><span class="sxs-lookup"><span data-stu-id="43769-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry or create and assign a new one.</span></span> <span data-ttu-id="43769-121">Кроме того, можно включить учетную запись администратора реестра.</span><span class="sxs-lookup"><span data-stu-id="43769-121">Alternatively, you can enable the registry's admin user account.</span></span> <span data-ttu-id="43769-122">См. следующие разделы этой статьи.</span><span class="sxs-lookup"><span data-stu-id="43769-122">See the sections later in this article.</span></span> <span data-ttu-id="43769-123">Дополнительные сведения о доступе к реестру см. в статье [Authenticate with the container registry](container-registry-authentication.md) (Проверка подлинности с помощью реестра контейнеров).</span><span class="sxs-lookup"><span data-stu-id="43769-123">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="43769-124">Создание реестра контейнеров</span><span class="sxs-lookup"><span data-stu-id="43769-124">Create a container registry</span></span>
<span data-ttu-id="43769-125">Чтобы создать реестр контейнеров, выполните команду `New-AzureRMContainerRegistry`.</span><span class="sxs-lookup"><span data-stu-id="43769-125">Run the `New-AzureRMContainerRegistry` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="43769-126">При создании реестра укажите глобально уникальное доменное имя верхнего уровня, содержащее только буквы и цифры.</span><span class="sxs-lookup"><span data-stu-id="43769-126">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="43769-127">В примерах в качестве имени реестра используется имя `MyRegistry`, но его нужно заменить собственным.</span><span class="sxs-lookup"><span data-stu-id="43769-127">The registry name in the examples is `MyRegistry`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="43769-128">Следующая команда создает реестр контейнеров `MyRegistry` в группе ресурсов `MyResourceGroup` в юго-центральном регионе США. При этом используются минимальные параметры.</span><span class="sxs-lookup"><span data-stu-id="43769-128">The following command uses the minimal parameters to create container registry `MyRegistry` in the resource group `MyResourceGroup` in the South Central US location:</span></span>

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* <span data-ttu-id="43769-129">`-StorageAccountName` является необязательным.</span><span class="sxs-lookup"><span data-stu-id="43769-129">`-StorageAccountName` is optional.</span></span> <span data-ttu-id="43769-130">Если это не определено, учетная запись хранения создается с именем, состоящим из имени реестра и метки времени в указанной группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="43769-130">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="43769-131">Назначение субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="43769-131">Assign a service principal</span></span>
<span data-ttu-id="43769-132">Команды PowerShell позволяют назначать [субъект-службу](../azure-resource-manager/resource-group-authenticate-service-principal.md) Azure Active Directory для реестра.</span><span class="sxs-lookup"><span data-stu-id="43769-132">Use PowerShell commands to assign an Azure Active Directory [service principal](../azure-resource-manager/resource-group-authenticate-service-principal.md) to a registry.</span></span> <span data-ttu-id="43769-133">В этих примерах субъект-служба имеет роль владельца, но при необходимости можно назначить [другие роли](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="43769-133">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal"></a><span data-ttu-id="43769-134">Создание субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="43769-134">Create a service principal</span></span>
<span data-ttu-id="43769-135">С помощью следующей команды создается новый субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="43769-135">In the following command, a new service principal is created.</span></span> <span data-ttu-id="43769-136">Укажите надежный пароль с помощью параметра `-Password`.</span><span class="sxs-lookup"><span data-stu-id="43769-136">Specify a strong password with the `-Password` parameter.</span></span>

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a><span data-ttu-id="43769-137">Назначение нового или существующего субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="43769-137">Assign a new or existing service principal</span></span>
<span data-ttu-id="43769-138">Реестру можно назначить новый или существующий субъект-службу.</span><span class="sxs-lookup"><span data-stu-id="43769-138">You can assign a new or an existing service principal to a registry.</span></span> <span data-ttu-id="43769-139">Чтобы назначить ему роль владельца для доступа к реестру, выполните команду, аналогичную следующей.</span><span class="sxs-lookup"><span data-stu-id="43769-139">To assign it Owner role access to the registry, run a command similar to the following example:</span></span>

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-to-the-registry-with-the-service-principal"></a><span data-ttu-id="43769-140">Вход в реестр с помощью субъекта-службы</span><span class="sxs-lookup"><span data-stu-id="43769-140">Sign in to the registry with the service principal</span></span>
<span data-ttu-id="43769-141">После назначения реестру субъекта-службы можно войти в реестр с помощью следующей команды:</span><span class="sxs-lookup"><span data-stu-id="43769-141">After assigning the service principal to the registry, you can sign in using the following command:</span></span>

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a><span data-ttu-id="43769-142">Управление учетными данными администратора</span><span class="sxs-lookup"><span data-stu-id="43769-142">Manage admin credentials</span></span>
<span data-ttu-id="43769-143">Учетная запись администратора автоматически создается для каждого реестра контейнеров, но по умолчанию она отключена.</span><span class="sxs-lookup"><span data-stu-id="43769-143">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="43769-144">В следующих примерах показаны команды PowerShell, с помощью которых можно управлять учетными данными администратора для реестра контейнеров.</span><span class="sxs-lookup"><span data-stu-id="43769-144">The following examples show PowerShell commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="43769-145">Получение учетных данных пользователя с правами администратора</span><span class="sxs-lookup"><span data-stu-id="43769-145">Obtain admin user credentials</span></span>
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="43769-146">Включение пользователя с правами администратора для имеющегося реестра</span><span class="sxs-lookup"><span data-stu-id="43769-146">Enable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="43769-147">Отключение пользователя с правами администратора для имеющегося реестра</span><span class="sxs-lookup"><span data-stu-id="43769-147">Disable admin user for an existing registry</span></span>
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a><span data-ttu-id="43769-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43769-148">Next steps</span></span>
* [<span data-ttu-id="43769-149">Отправка первого образа с помощью интерфейса командной строки Docker</span><span class="sxs-lookup"><span data-stu-id="43769-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)
