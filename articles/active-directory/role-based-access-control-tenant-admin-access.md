---
title: "Администратор aaaTenant повышение прав доступа - Azure AD | Документы Microsoft"
description: "В этом разделе описываются hello, встроенных в роли для управления доступом на основе ролей (RBAC)."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="524f8-103">Повышение прав доступа администратором клиентов с помощью управления доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="524f8-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="524f8-104">Управление доступом на основе ролей позволяет администраторам клиентов временно повысить права доступа, чтобы предоставить больше разрешений, чем обычно.</span><span class="sxs-lookup"><span data-stu-id="524f8-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="524f8-105">Администратор клиента может повысить себе toohello роли Администратор доступа пользователя, если это требуется.</span><span class="sxs-lookup"><span data-stu-id="524f8-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="524f8-106">Эта роль предоставляет hello себе или другим toogrant разрешения администратора для клиента роли hello область «/».</span><span class="sxs-lookup"><span data-stu-id="524f8-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="524f8-107">Эта функция важна, так как она допускает hello клиента администратора toosee все hello подписок, которые существуют в организации.</span><span class="sxs-lookup"><span data-stu-id="524f8-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="524f8-108">Он также позволяет для автоматизации приложений (например, выставление счетов и аудит) tooaccess все подписки hello и обеспечить точное представление состояния hello hello организации для выставления счетов или средства управления.</span><span class="sxs-lookup"><span data-stu-id="524f8-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="524f8-109">Как toouse elevateAccess toogive клиента доступа</span><span class="sxs-lookup"><span data-stu-id="524f8-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="524f8-110">базовый процесс Hello работает с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="524f8-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="524f8-111">С помощью REST, вызовите *elevateAccess*, какие предоставляет вам Здравствуйте, администратор доступа пользователя роли на «/» области.</span><span class="sxs-lookup"><span data-stu-id="524f8-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="524f8-112">Создание [назначение ролей](/rest/api/authorization/roleassignments) tooassign любой роли в любой области.</span><span class="sxs-lookup"><span data-stu-id="524f8-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="524f8-113">Следующий пример Hello показано назначение свойства hello hello роль модуля чтения в «/» области:</span><span class="sxs-lookup"><span data-stu-id="524f8-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. <span data-ttu-id="524f8-114">Являясь администратором доступа пользователей, можно также удалять назначения роли для области "/".</span><span class="sxs-lookup"><span data-stu-id="524f8-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="524f8-115">Отзовите привилегии администратора доступа пользователей, пока они не понадобятся вновь.</span><span class="sxs-lookup"><span data-stu-id="524f8-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="524f8-116">Как tooundo hello elevateAccess действие</span><span class="sxs-lookup"><span data-stu-id="524f8-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="524f8-117">При вызове *elevateAccess* создать назначение ролей для текущего пользователя, поэтому toorevoke те права доступа вы должны toodelete hello назначения.</span><span class="sxs-lookup"><span data-stu-id="524f8-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="524f8-118">Вызовите [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) где roleName = hello toodetermine администратор доступа пользователя имя GUID роли пользователя администратора hello.</span><span class="sxs-lookup"><span data-stu-id="524f8-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="524f8-119">Hello ответ должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="524f8-119">hello response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    <span data-ttu-id="524f8-120">Сохранить hello GUID из hello *имя* параметра в данном случае **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="524f8-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="524f8-121">Вызовите [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), где principalId — ваш ObjectId.</span><span class="sxs-lookup"><span data-stu-id="524f8-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="524f8-122">Перечисляет все назначения, в клиенте hello.</span><span class="sxs-lookup"><span data-stu-id="524f8-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="524f8-123">Найти для одного hello которых hello область «/» и заканчивается RoleDefinitionId hello роли hello имя идентификатором GUID, найденным в шаге 1.</span><span class="sxs-lookup"><span data-stu-id="524f8-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="524f8-124">Назначение ролей Hello должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="524f8-124">hello role assignment should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    <span data-ttu-id="524f8-125">Снова, сохраните hello GUID из hello *имя* параметра в данном случае **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="524f8-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="524f8-126">Наконец, вызовите [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) где roleAssignmentId = hello имя идентификатора GUID, определенным на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="524f8-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="524f8-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="524f8-127">Next steps</span></span>

- <span data-ttu-id="524f8-128">Узнайте больше об [управлении доступом на основе ролей с помощью REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="524f8-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="524f8-129">[Управление назначениями доступа](role-based-access-control-manage-assignments.md) в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="524f8-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
