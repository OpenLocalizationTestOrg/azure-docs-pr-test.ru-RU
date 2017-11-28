---
title: "Повышение прав доступа администратором клиентов в Azure AD | Документация Майкрософт"
description: "В этом разделе описаны встроенные роли для управления доступом на основе ролей (RBAC)."
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
ms.openlocfilehash: bf64a92b359a6f68d84fa5ee17eda64ed6371990
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="6e23c-103">Повышение прав доступа администратором клиентов с помощью управления доступом на основе ролей</span><span class="sxs-lookup"><span data-stu-id="6e23c-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="6e23c-104">Управление доступом на основе ролей позволяет администраторам клиентов временно повысить права доступа, чтобы предоставить больше разрешений, чем обычно.</span><span class="sxs-lookup"><span data-stu-id="6e23c-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="6e23c-105">При необходимости администратор клиентов может повысить свои права до роли администратора доступа пользователей.</span><span class="sxs-lookup"><span data-stu-id="6e23c-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="6e23c-106">Эта роль позволяет администратору клиентов предоставить себе или другим пользователям роли в области "/".</span><span class="sxs-lookup"><span data-stu-id="6e23c-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="6e23c-107">Эта возможность важна, так как она позволяет администратору клиентов видеть все подписки, которые существуют в организации.</span><span class="sxs-lookup"><span data-stu-id="6e23c-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="6e23c-108">Она также позволяет приложениям службы автоматизации (например, приложениям для выставления счетов и аудита) обращаться ко всем подпискам и обеспечивать точное представление о состоянии организации с точки зрения выставления счетов или управления ресурсами.</span><span class="sxs-lookup"><span data-stu-id="6e23c-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization for billing or asset management.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="6e23c-109">Как использовать elevateAccess для предоставления доступа клиентам</span><span class="sxs-lookup"><span data-stu-id="6e23c-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="6e23c-110">Базовый процесс состоит из приведенных ниже действий.</span><span class="sxs-lookup"><span data-stu-id="6e23c-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="6e23c-111">С помощью REST вызовите действие *elevateAccess*, который предоставляет вам роль администратора доступа пользователей в области "/".</span><span class="sxs-lookup"><span data-stu-id="6e23c-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="6e23c-112">Создание [назначение роли](/rest/api/authorization/roleassignments), чтобы назначить любую роль в любой области.</span><span class="sxs-lookup"><span data-stu-id="6e23c-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="6e23c-113">В следующем примере показаны свойства для назначения роли "Читатель" для области "/".</span><span class="sxs-lookup"><span data-stu-id="6e23c-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="6e23c-114">Являясь администратором доступа пользователей, можно также удалять назначения роли для области "/".</span><span class="sxs-lookup"><span data-stu-id="6e23c-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="6e23c-115">Отзовите привилегии администратора доступа пользователей, пока они не понадобятся вновь.</span><span class="sxs-lookup"><span data-stu-id="6e23c-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="6e23c-116">Как отменить действие elevateAccess</span><span class="sxs-lookup"><span data-stu-id="6e23c-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="6e23c-117">При вызове *elevateAccess* для вас создается назначение роли. Поэтому, чтобы отозвать эти привилегии, необходимо удалить назначение.</span><span class="sxs-lookup"><span data-stu-id="6e23c-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="6e23c-118">Вызовите [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get), где roleName — администратор доступа пользователей, чтобы определить GUID параметра name роли администратор доступа пользователей.</span><span class="sxs-lookup"><span data-stu-id="6e23c-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="6e23c-119">Результат должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="6e23c-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
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

    <span data-ttu-id="6e23c-120">Сохраните GUID из параметра *name*, в данном случае это **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="6e23c-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="6e23c-121">Вызовите [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), где principalId — ваш ObjectId.</span><span class="sxs-lookup"><span data-stu-id="6e23c-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="6e23c-122">Буден выведен список всех назначений в клиенте.</span><span class="sxs-lookup"><span data-stu-id="6e23c-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="6e23c-123">Найдите назначение, у которого задана область "/" и RoleDefinitionId заканчивается значением GUID из параметра name роли, найденным на шаге 1.</span><span class="sxs-lookup"><span data-stu-id="6e23c-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="6e23c-124">Назначение роли должно выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="6e23c-124">The role assignment should look like this:</span></span>

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

    <span data-ttu-id="6e23c-125">Опять же, сохраните GUID из параметра *name*. В данном случае это **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="6e23c-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="6e23c-126">Наконец, вызовите [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById), где roleAssignmentId — GUID из параметра name роли, найденный на шаге 2.</span><span class="sxs-lookup"><span data-stu-id="6e23c-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e23c-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e23c-127">Next steps</span></span>

- <span data-ttu-id="6e23c-128">Узнайте больше об [управлении доступом на основе ролей с помощью REST](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="6e23c-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="6e23c-129">Изучите [управление правами доступа](role-based-access-control-manage-assignments.md) на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6e23c-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
