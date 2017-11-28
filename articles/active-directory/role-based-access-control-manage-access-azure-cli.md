---
title: "на основе ролей ролей (RBAC) с помощью Azure CLI aaaManage | Документы Microsoft"
description: "Узнайте, как toomanage Role-Based ролей (RBAC) с помощью командной строки Azure hello интерфейс листинг роли и роли действия и путем назначения ролей toohello областей подписки и приложения."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="c8ac7-103">Управление на основе ролей управления доступом с hello Azure интерфейс командной строки</span><span class="sxs-lookup"><span data-stu-id="c8ac7-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8ac7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8ac7-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="c8ac7-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="c8ac7-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="c8ac7-106">REST API</span><span class="sxs-lookup"><span data-stu-id="c8ac7-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="c8ac7-107">Управление доступом на основе ролей (RBAC) можно использовать в hello портал Azure и API диспетчера ресурсов Azure toomanage доступа tooyour подписка и ресурсы на уровне детально.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="c8ac7-108">С помощью этой функции можно предоставить доступ для пользователей, группы или субъекты-службы Active Directory путем назначения некоторых ролей toothem на определенную область.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="c8ac7-109">Прежде чем использовать hello Azure командной строки (CLI) toomanage RBAC, необходимо иметь hello следующие предварительные требования:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="c8ac7-110">Интерфейс командной строки Azure версии 0.8.8 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="c8ac7-111">последнюю версию tooinstall hello и связывание его с подпиской Azure. в разделе [Установка и настройка hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c8ac7-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="c8ac7-112">Azure Resource Manager в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="c8ac7-113">Go слишком[использование hello Azure CLI с hello диспетчера ресурсов](../xplat-cli-azure-resource-manager.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="c8ac7-114">Вывод списка ролей</span><span class="sxs-lookup"><span data-stu-id="c8ac7-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="c8ac7-115">Вывод списка всех доступных ролей</span><span class="sxs-lookup"><span data-stu-id="c8ac7-115">List all available roles</span></span>
<span data-ttu-id="c8ac7-116">toolist всем доступным ролям, используйте:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="c8ac7-117">Hello примере показан список hello *всем доступным ролям*.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Снимок экрана: командная строка RBAC Azure — список ролей Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="c8ac7-119">Вывод списка действий роли</span><span class="sxs-lookup"><span data-stu-id="c8ac7-119">List actions of a role</span></span>
<span data-ttu-id="c8ac7-120">действия hello toolist роли, используйте:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="c8ac7-121">Hello пример hello действия hello *участника* и *участника виртуальной машины* ролей.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Снимок экрана: командная строка RBAC Azure — отображение ролей Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="c8ac7-123">Вывод списка доступа</span><span class="sxs-lookup"><span data-stu-id="c8ac7-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="c8ac7-124">Вывод списка назначений ролей, действующих в группе ресурсов</span><span class="sxs-lookup"><span data-stu-id="c8ac7-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="c8ac7-125">toolist hello назначения ролей, которые находятся в группе ресурсов, используйте:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="c8ac7-126">Hello пример hello назначения ролей в hello *pharma sales-projecforcast* группы.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Снимок экрана: командная строка RBAC Azure — список назначений ролей Azure по группам](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="c8ac7-128">Список назначений ролей для пользователя</span><span class="sxs-lookup"><span data-stu-id="c8ac7-128">List role assignments for a user</span></span>
<span data-ttu-id="c8ac7-129">Используйте toolist hello назначения ролей для определенных пользователей и назначения hello, которые назначаются группам tooa пользователя:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="c8ac7-130">Также можно просмотреть назначения ролей, которые наследуются от групп, изменив hello команды:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="c8ac7-131">Hello пример hello назначения ролей, которые предоставляются toohello  *sameert@aaddemo.com*  пользователя.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="c8ac7-132">Сюда входят роли, назначаемые непосредственно toohello пользователей и ролей, которые наследуются от групп.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Снимок экрана: командная строка RBAC Azure — список назначений ролей Azure по пользователям](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="c8ac7-134">Предоставление доступа</span><span class="sxs-lookup"><span data-stu-id="c8ac7-134">Grant access</span></span>
<span data-ttu-id="c8ac7-135">toogrant доступа после определения роли hello, что требуется tooassign использовать:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="c8ac7-136">Назначение роли toogroup в области видимости hello подписки</span><span class="sxs-lookup"><span data-stu-id="c8ac7-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="c8ac7-137">tooassign группу tooa ролей в области hello подписки, используйте:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="c8ac7-138">Hello следующий пример назначает hello *чтения* роли слишком*команды Анна Кох* в hello *подписки* области.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![Снимок экрана: командная строка RBAC Azure — создание назначений ролей Azure по группам](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="c8ac7-140">Назначение роли приложения tooan в области видимости hello подписки</span><span class="sxs-lookup"><span data-stu-id="c8ac7-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="c8ac7-141">tooassign приложении tooan роли на уровне подписки hello, используйте:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="c8ac7-142">Hello следующий код предоставляет hello *участника* tooan роли *Azure AD* приложение hello выбранной подписки.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![Командная строка RBAC Azure — создание назначений ролей Azure по приложениям](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="c8ac7-144">Назначить пользователя роли tooa в области группы ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="c8ac7-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="c8ac7-145">tooassign tooa роли пользователя в области группы ресурсов hello, используйте:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="c8ac7-146">Hello следующий код предоставляет hello *участника виртуальной машины* роли слишком *samert@aaddemo.com*  пользователя на hello *Pharma Sales-ProjectForcast* область группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![Снимок экрана: командная строка RBAC Azure — создание назначений ролей Azure по пользователям](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="c8ac7-148">Назначение роли tooa группы в области видимости ресурса hello</span><span class="sxs-lookup"><span data-stu-id="c8ac7-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="c8ac7-149">tooassign группу tooa ролей в области видимости ресурса hello, используйте:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="c8ac7-150">Hello следующий код предоставляет hello *участника виртуальной машины* tooan роли *Azure AD* на *подсети*.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![Снимок экрана: командная строка RBAC Azure — создание назначений ролей Azure по группам](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="c8ac7-152">Запрет доступа</span><span class="sxs-lookup"><span data-stu-id="c8ac7-152">Remove access</span></span>
<span data-ttu-id="c8ac7-153">Используйте tooremove назначение ролей.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="c8ac7-154">Hello следующий пример удаляет hello *участника виртуальной машины* назначение роли hello  *sammert@aaddemo.com*  пользователя на hello *Pharma Sales-ProjectForcast* Группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="c8ac7-155">Затем пример Hello удаляет hello назначение ролей из группы в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![Снимок экрана: командная строка RBAC Azure — удаление назначений ролей Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="c8ac7-157">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="c8ac7-157">Create a custom role</span></span>
<span data-ttu-id="c8ac7-158">Используйте toocreate пользовательской роли:</span><span class="sxs-lookup"><span data-stu-id="c8ac7-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="c8ac7-159">Hello следующий пример создает пользовательскую роль вызывается *оператор виртуальной машины*.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="c8ac7-160">Предоставляет пользовательской роли, считываемых доступа tooall *Microsoft.Compute*, *хранилища Майкрософт*, и *Microsoft.Network* поставщиков и предоставляет доступ к ресурсам toostart, перезапуска и мониторинга виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="c8ac7-161">Эту настраиваемую роль можно использовать в двух подписках.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="c8ac7-162">В этом примере в качестве входных данных используется JSON-файл.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-162">This example uses a JSON file as an input.</span></span>

![Снимок экрана: JSON — определение пользовательской роли](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Снимок экрана: командная строка RBAC Azure — создание ролей Azure](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="c8ac7-165">Изменение настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="c8ac7-165">Modify a custom role</span></span>
<span data-ttu-id="c8ac7-166">toomodify пользовательской роли, сначала использовать hello `azure role show` команды tooretrieve определения роли.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="c8ac7-167">Во-вторых внести необходимые изменения toohello hello роли-файл определения.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="c8ac7-168">Наконец, используйте `azure role set` toosave hello изменения определения роли.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="c8ac7-169">Hello следующий пример добавляет hello *Microsoft.Insights/diagnosticSettings/* toohello операции **действия**и подписки Azure toohello **AssignableScopes**пользовательские роли виртуальной машины оператор hello.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![Снимок экрана: JSON — изменение определения пользовательской роли](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Снимок экрана: командная строка RBAC Azure — настройка ролей Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="c8ac7-172">Удаление настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="c8ac7-172">Delete a custom role</span></span>
<span data-ttu-id="c8ac7-173">toodelete пользовательской роли, сначала использовать hello `azure role show` команда hello toodetermine **идентификатор** hello роли.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="c8ac7-174">Затем с помощью hello `azure role delete` роли hello toodelete команду, указав hello **идентификатор**.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="c8ac7-175">Hello следующий пример удаляет hello *оператор виртуальной машины* пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![Снимок экрана: командная строка RBAC Azure — удаление ролей Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="c8ac7-177">Вывод списка настраиваемых ролей</span><span class="sxs-lookup"><span data-stu-id="c8ac7-177">List custom roles</span></span>
<span data-ttu-id="c8ac7-178">toolist hello ролей, доступных для назначения в области, используйте hello `azure role list` команды.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="c8ac7-179">Hello следующую команду список всех ролей, доступных для назначения в подписке hello выбран.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Снимок экрана: командная строка RBAC Azure — список ролей Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="c8ac7-181">В следующем примере hello, hello *оператор виртуальной машины* пользовательской роли не предусмотрена в hello *Production4* подписки, так как ее нет в hello  **AssignableScopes** hello роли.</span><span class="sxs-lookup"><span data-stu-id="c8ac7-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Снимок экрана: командная строка RBAC Azure — список пользовательских ролей Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="c8ac7-183">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c8ac7-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

