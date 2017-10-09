---
title: "Управление доступом на основе aaaRole с REST - Azure AD | Документы Microsoft"
description: "Управление доступом на основе ролей с hello REST API"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="8a43f-103">Управление на основе ролей управления доступом с помощью API-интерфейса REST hello</span><span class="sxs-lookup"><span data-stu-id="8a43f-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8a43f-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8a43f-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="8a43f-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="8a43f-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="8a43f-106">REST API</span><span class="sxs-lookup"><span data-stu-id="8a43f-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="8a43f-107">На основе ролей управления доступом (RBAC) в hello портал Azure и API диспетчера ресурсов Azure помогает управлять доступа tooyour подписка и ресурсы на уровне детально.</span><span class="sxs-lookup"><span data-stu-id="8a43f-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="8a43f-108">С помощью этой функции можно предоставить доступ для пользователей, группы или субъекты-службы Active Directory путем назначения некоторых ролей toothem на определенную область.</span><span class="sxs-lookup"><span data-stu-id="8a43f-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="8a43f-109">Вывод списка всех назначений ролей</span><span class="sxs-lookup"><span data-stu-id="8a43f-109">List all role assignments</span></span>
<span data-ttu-id="8a43f-110">Все назначения ролей hello в указанный hello списки области и subscopes.</span><span class="sxs-lookup"><span data-stu-id="8a43f-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="8a43f-111">toolist назначения ролей, необходимо иметь доступ слишком`Microsoft.Authorization/roleAssignments/read` операцию в область hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="8a43f-112">Все встроенные роли hello предоставляются toothis операции доступа.</span><span class="sxs-lookup"><span data-stu-id="8a43f-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="8a43f-113">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a43f-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8a43f-114">Запрос</span><span class="sxs-lookup"><span data-stu-id="8a43f-114">Request</span></span>
<span data-ttu-id="8a43f-115">Используйте hello **получить** метод с hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="8a43f-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="8a43f-116">В рамках hello URI создайте hello после замены toocustomize запрос:</span><span class="sxs-lookup"><span data-stu-id="8a43f-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="8a43f-117">Замените *{scope}* с областью видимости hello, для которого вы хотите toolist hello назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="8a43f-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="8a43f-118">Привет, следующие примеры показывают, как toospecify hello области для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="8a43f-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="8a43f-119">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="8a43f-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8a43f-120">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8a43f-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8a43f-121">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8a43f-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8a43f-122">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8a43f-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="8a43f-123">Замените *{filter}* с условием hello обратиться в список назначения роли hello toofilter tooapply:</span><span class="sxs-lookup"><span data-stu-id="8a43f-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="8a43f-124">Список назначений ролей для hello только указаны области, не включая hello назначений ролей на subscopes:`atScope()`</span><span class="sxs-lookup"><span data-stu-id="8a43f-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="8a43f-125">Вывод списка назначений ролей для определенного пользователя, группы или приложения: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="8a43f-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="8a43f-126">Вывод списка назначений ролей для определенного пользователя, включая роли, унаследованные от групп | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="8a43f-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="8a43f-127">Ответ</span><span class="sxs-lookup"><span data-stu-id="8a43f-127">Response</span></span>
<span data-ttu-id="8a43f-128">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="8a43f-128">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="8a43f-129">Получение сведений о назначении роли</span><span class="sxs-lookup"><span data-stu-id="8a43f-129">Get information about a role assignment</span></span>
<span data-ttu-id="8a43f-130">Возвращает сведения о назначении одной роли, указанной идентификатором назначения роли hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="8a43f-131">tooget сведения о назначении роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleAssignments/read` операции.</span><span class="sxs-lookup"><span data-stu-id="8a43f-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="8a43f-132">Все встроенные роли hello предоставляются toothis операции доступа.</span><span class="sxs-lookup"><span data-stu-id="8a43f-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="8a43f-133">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a43f-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8a43f-134">Запрос</span><span class="sxs-lookup"><span data-stu-id="8a43f-134">Request</span></span>
<span data-ttu-id="8a43f-135">Используйте hello **получить** метод с hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="8a43f-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="8a43f-136">В рамках hello URI создайте hello после замены toocustomize запрос:</span><span class="sxs-lookup"><span data-stu-id="8a43f-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="8a43f-137">Замените *{scope}* с областью видимости hello, для которого вы хотите toolist hello назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="8a43f-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="8a43f-138">Привет, следующие примеры показывают, как toospecify hello области для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="8a43f-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="8a43f-139">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="8a43f-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8a43f-140">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8a43f-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8a43f-141">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8a43f-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8a43f-142">Замените *{идентификатор роли назначения}* с идентификатором GUID hello hello назначение ролей.</span><span class="sxs-lookup"><span data-stu-id="8a43f-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="8a43f-143">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8a43f-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="8a43f-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="8a43f-144">Response</span></span>
<span data-ttu-id="8a43f-145">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="8a43f-145">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a><span data-ttu-id="8a43f-146">Создание назначения роли</span><span class="sxs-lookup"><span data-stu-id="8a43f-146">Create a Role Assignment</span></span>
<span data-ttu-id="8a43f-147">Создание роли назначения на hello указан области для hello указанного участника предоставление hello указанной роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="8a43f-148">toocreate назначение ролей, необходимо иметь доступ слишком`Microsoft.Authorization/roleAssignments/write` операции.</span><span class="sxs-lookup"><span data-stu-id="8a43f-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="8a43f-149">Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа.</span><span class="sxs-lookup"><span data-stu-id="8a43f-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="8a43f-150">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a43f-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8a43f-151">Запрос</span><span class="sxs-lookup"><span data-stu-id="8a43f-151">Request</span></span>
<span data-ttu-id="8a43f-152">Используйте hello **ПОМЕСТИТЬ** метод с hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="8a43f-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="8a43f-153">В рамках hello URI создайте hello после замены toocustomize запрос:</span><span class="sxs-lookup"><span data-stu-id="8a43f-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="8a43f-154">Замените *{scope}* с областью видимости hello, с которой вы хотите toocreate hello назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="8a43f-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="8a43f-155">При создании назначения ролей в родительской области, все дочерние области наследуют hello же назначение ролей.</span><span class="sxs-lookup"><span data-stu-id="8a43f-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="8a43f-156">Привет, следующие примеры показывают, как toospecify hello области для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="8a43f-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="8a43f-157">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="8a43f-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8a43f-158">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8a43f-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="8a43f-159">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8a43f-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8a43f-160">Замените *{идентификатор роли назначения}* нового идентификатора GUID, которая становится идентификатор GUID hello hello создать назначение ролей.</span><span class="sxs-lookup"><span data-stu-id="8a43f-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="8a43f-161">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8a43f-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="8a43f-162">Для текста запроса hello укажите значения hello в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="8a43f-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="8a43f-163">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="8a43f-163">Element Name</span></span> | <span data-ttu-id="8a43f-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8a43f-164">Required</span></span> | <span data-ttu-id="8a43f-165">Тип</span><span class="sxs-lookup"><span data-stu-id="8a43f-165">Type</span></span> | <span data-ttu-id="8a43f-166">Описание</span><span class="sxs-lookup"><span data-stu-id="8a43f-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8a43f-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="8a43f-167">roleDefinitionId</span></span> |<span data-ttu-id="8a43f-168">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-168">Yes</span></span> |<span data-ttu-id="8a43f-169">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-169">String</span></span> |<span data-ttu-id="8a43f-170">Идентификатор Hello hello роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-170">hello identifier of hello role.</span></span> <span data-ttu-id="8a43f-171">Hello идентификатора hello выглядит следующим образом:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="8a43f-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="8a43f-172">principalId</span><span class="sxs-lookup"><span data-stu-id="8a43f-172">principalId</span></span> |<span data-ttu-id="8a43f-173">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-173">Yes</span></span> |<span data-ttu-id="8a43f-174">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-174">String</span></span> |<span data-ttu-id="8a43f-175">objectId hello Azure AD участника (пользователя, группы или субъекта-службы) назначена роль toowhich hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="8a43f-176">Ответ</span><span class="sxs-lookup"><span data-stu-id="8a43f-176">Response</span></span>
<span data-ttu-id="8a43f-177">Код состояния: 201.</span><span class="sxs-lookup"><span data-stu-id="8a43f-177">Status code: 201</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a><span data-ttu-id="8a43f-178">Удаление назначения ролей</span><span class="sxs-lookup"><span data-stu-id="8a43f-178">Delete a Role Assignment</span></span>
<span data-ttu-id="8a43f-179">Удалить назначение роли в hello указана область.</span><span class="sxs-lookup"><span data-stu-id="8a43f-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="8a43f-180">toodelete назначение ролей, необходимо иметь доступ toohello `Microsoft.Authorization/roleAssignments/delete` операции.</span><span class="sxs-lookup"><span data-stu-id="8a43f-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="8a43f-181">Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа.</span><span class="sxs-lookup"><span data-stu-id="8a43f-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="8a43f-182">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a43f-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8a43f-183">Запрос</span><span class="sxs-lookup"><span data-stu-id="8a43f-183">Request</span></span>
<span data-ttu-id="8a43f-184">Используйте hello **удалить** метод с hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="8a43f-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="8a43f-185">В рамках hello URI создайте hello после замены toocustomize запрос:</span><span class="sxs-lookup"><span data-stu-id="8a43f-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="8a43f-186">Замените *{scope}* с областью видимости hello, с которой вы хотите toocreate hello назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="8a43f-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="8a43f-187">Привет, следующие примеры показывают, как toospecify hello области для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="8a43f-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="8a43f-188">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="8a43f-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8a43f-189">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8a43f-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8a43f-190">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8a43f-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8a43f-191">Замените *{идентификатор роли назначения}* с идентификатором назначения роли hello GUID.</span><span class="sxs-lookup"><span data-stu-id="8a43f-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="8a43f-192">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8a43f-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="8a43f-193">Ответ</span><span class="sxs-lookup"><span data-stu-id="8a43f-193">Response</span></span>
<span data-ttu-id="8a43f-194">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="8a43f-194">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a><span data-ttu-id="8a43f-195">Вывод списка всех ролей</span><span class="sxs-lookup"><span data-stu-id="8a43f-195">List all Roles</span></span>
<span data-ttu-id="8a43f-196">Список всех ролей hello, доступных для назначения на указанный hello области.</span><span class="sxs-lookup"><span data-stu-id="8a43f-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="8a43f-197">toolist ролей, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/read` операцию в область hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="8a43f-198">Все встроенные роли hello предоставляются toothis операции доступа.</span><span class="sxs-lookup"><span data-stu-id="8a43f-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="8a43f-199">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a43f-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8a43f-200">Запрос</span><span class="sxs-lookup"><span data-stu-id="8a43f-200">Request</span></span>
<span data-ttu-id="8a43f-201">Используйте hello **получить** метод с hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="8a43f-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="8a43f-202">В рамках hello URI создайте hello после замены toocustomize запрос:</span><span class="sxs-lookup"><span data-stu-id="8a43f-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="8a43f-203">Замените *{scope}* с областью видимости hello, для которого вы хотите toolist hello ролей.</span><span class="sxs-lookup"><span data-stu-id="8a43f-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="8a43f-204">Привет, следующие примеры показывают, как toospecify hello области для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="8a43f-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="8a43f-205">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="8a43f-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8a43f-206">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8a43f-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8a43f-207">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8a43f-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8a43f-208">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8a43f-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="8a43f-209">Замените *{filter}* с условием hello, что вы хотите tooapply toofilter hello список ролей:</span><span class="sxs-lookup"><span data-stu-id="8a43f-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="8a43f-210">Список ролей, доступных для назначения на hello указаны области, а также все ее дочерние области:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="8a43f-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="8a43f-211">Поиск с помощью точного отображаемого имени роли: `roleName%20eq%20'{role-display-name}'`</span><span class="sxs-lookup"><span data-stu-id="8a43f-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="8a43f-212">Используйте форму URL-кодированием hello hello точное отображаемое имя роли hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="8a43f-213">Например, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="8a43f-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="8a43f-214">Ответ</span><span class="sxs-lookup"><span data-stu-id="8a43f-214">Response</span></span>
<span data-ttu-id="8a43f-215">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="8a43f-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a><span data-ttu-id="8a43f-216">Получение сведений о роли</span><span class="sxs-lookup"><span data-stu-id="8a43f-216">Get information about a Role</span></span>
<span data-ttu-id="8a43f-217">Возвращает сведения об одной роли, заданные hello идентификатор определения роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="8a43f-218">tooget сведения об одной роли с помощью его отображаемое имя. в разделе [списка всех ролей](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="8a43f-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="8a43f-219">tooget сведения о роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/read` операции.</span><span class="sxs-lookup"><span data-stu-id="8a43f-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="8a43f-220">Все встроенные роли hello предоставляются toothis операции доступа.</span><span class="sxs-lookup"><span data-stu-id="8a43f-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="8a43f-221">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a43f-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8a43f-222">Запрос</span><span class="sxs-lookup"><span data-stu-id="8a43f-222">Request</span></span>
<span data-ttu-id="8a43f-223">Используйте hello **получить** метод с hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="8a43f-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="8a43f-224">В рамках hello URI создайте hello после замены toocustomize запрос:</span><span class="sxs-lookup"><span data-stu-id="8a43f-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="8a43f-225">Замените *{scope}* с областью видимости hello, для которого вы хотите toolist hello назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="8a43f-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="8a43f-226">Привет, следующие примеры показывают, как toospecify hello области для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="8a43f-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="8a43f-227">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="8a43f-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8a43f-228">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8a43f-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8a43f-229">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8a43f-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8a43f-230">Замените *{role-definition-id}* с идентификатором GUID hello hello определения роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="8a43f-231">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8a43f-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="8a43f-232">Ответ</span><span class="sxs-lookup"><span data-stu-id="8a43f-232">Response</span></span>
<span data-ttu-id="8a43f-233">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="8a43f-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a><span data-ttu-id="8a43f-234">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="8a43f-234">Create a Custom Role</span></span>
<span data-ttu-id="8a43f-235">Здесь описывается создание настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-235">Create a custom role.</span></span>

<span data-ttu-id="8a43f-236">toocreate пользовательской роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/write` операцию для всех hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="8a43f-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="8a43f-237">Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа.</span><span class="sxs-lookup"><span data-stu-id="8a43f-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="8a43f-238">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a43f-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8a43f-239">Запрос</span><span class="sxs-lookup"><span data-stu-id="8a43f-239">Request</span></span>
<span data-ttu-id="8a43f-240">Используйте hello **ПОМЕСТИТЬ** метод с hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="8a43f-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="8a43f-241">В рамках hello URI создайте hello после замены toocustomize запрос:</span><span class="sxs-lookup"><span data-stu-id="8a43f-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="8a43f-242">Замените *{scope}* с hello первый *AssignableScope* hello пользовательские роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="8a43f-243">Привет, следующие примеры показывают, как toospecify hello области для различных уровней.</span><span class="sxs-lookup"><span data-stu-id="8a43f-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="8a43f-244">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="8a43f-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8a43f-245">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8a43f-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8a43f-246">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8a43f-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8a43f-247">Замените *{role-definition-id}* нового идентификатора GUID, которая становится hello идентификатор GUID для новой настраиваемой роли hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="8a43f-248">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8a43f-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="8a43f-249">Для текста запроса hello укажите значения hello в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="8a43f-249">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="8a43f-250">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="8a43f-250">Element Name</span></span> | <span data-ttu-id="8a43f-251">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8a43f-251">Required</span></span> | <span data-ttu-id="8a43f-252">Тип</span><span class="sxs-lookup"><span data-stu-id="8a43f-252">Type</span></span> | <span data-ttu-id="8a43f-253">Описание</span><span class="sxs-lookup"><span data-stu-id="8a43f-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8a43f-254">name</span><span class="sxs-lookup"><span data-stu-id="8a43f-254">name</span></span> |<span data-ttu-id="8a43f-255">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-255">Yes</span></span> |<span data-ttu-id="8a43f-256">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-256">String</span></span> |<span data-ttu-id="8a43f-257">Идентификатор GUID пользовательской роли hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="8a43f-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="8a43f-258">properties.roleName</span></span> |<span data-ttu-id="8a43f-259">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-259">Yes</span></span> |<span data-ttu-id="8a43f-260">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-260">String</span></span> |<span data-ttu-id="8a43f-261">Отображаемое имя пользовательской роли hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-261">Display name of hello custom role.</span></span> <span data-ttu-id="8a43f-262">Не может быть более 128 символов в длину.</span><span class="sxs-lookup"><span data-stu-id="8a43f-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="8a43f-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="8a43f-263">properties.description</span></span> |<span data-ttu-id="8a43f-264">Нет</span><span class="sxs-lookup"><span data-stu-id="8a43f-264">No</span></span> |<span data-ttu-id="8a43f-265">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-265">String</span></span> |<span data-ttu-id="8a43f-266">Описание hello пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-266">Description of hello custom role.</span></span> <span data-ttu-id="8a43f-267">Не может быть более 1024 символов в длину.</span><span class="sxs-lookup"><span data-stu-id="8a43f-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="8a43f-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="8a43f-268">properties.type</span></span> |<span data-ttu-id="8a43f-269">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-269">Yes</span></span> |<span data-ttu-id="8a43f-270">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-270">String</span></span> |<span data-ttu-id="8a43f-271">Значение слишком «CustomRole».</span><span class="sxs-lookup"><span data-stu-id="8a43f-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="8a43f-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="8a43f-272">properties.permissions.actions</span></span> |<span data-ttu-id="8a43f-273">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-273">Yes</span></span> |<span data-ttu-id="8a43f-274">String[]</span><span class="sxs-lookup"><span data-stu-id="8a43f-274">String[]</span></span> |<span data-ttu-id="8a43f-275">Массив действий строк, указав hello операции, предоставляемые пользовательской роли hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="8a43f-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="8a43f-276">properties.permissions.notActions</span></span> |<span data-ttu-id="8a43f-277">Нет</span><span class="sxs-lookup"><span data-stu-id="8a43f-277">No</span></span> |<span data-ttu-id="8a43f-278">String[]</span><span class="sxs-lookup"><span data-stu-id="8a43f-278">String[]</span></span> |<span data-ttu-id="8a43f-279">Массив строк действий, указав hello tooexclude операций из операции hello, предоставленные hello пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="8a43f-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="8a43f-280">properties.assignableScopes</span></span> |<span data-ttu-id="8a43f-281">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-281">Yes</span></span> |<span data-ttu-id="8a43f-282">String[]</span><span class="sxs-lookup"><span data-stu-id="8a43f-282">String[]</span></span> |<span data-ttu-id="8a43f-283">Массив областей, в какие hello используются пользовательские роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="8a43f-284">Ответ</span><span class="sxs-lookup"><span data-stu-id="8a43f-284">Response</span></span>
<span data-ttu-id="8a43f-285">Код состояния: 201.</span><span class="sxs-lookup"><span data-stu-id="8a43f-285">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a><span data-ttu-id="8a43f-286">Обновление настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="8a43f-286">Update a Custom Role</span></span>
<span data-ttu-id="8a43f-287">Здесь описывается изменение настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-287">Modify a custom role.</span></span>

<span data-ttu-id="8a43f-288">toomodify пользовательской роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/write` операцию для всех hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="8a43f-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="8a43f-289">Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа.</span><span class="sxs-lookup"><span data-stu-id="8a43f-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="8a43f-290">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a43f-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8a43f-291">Запрос</span><span class="sxs-lookup"><span data-stu-id="8a43f-291">Request</span></span>
<span data-ttu-id="8a43f-292">Используйте hello **ПОМЕСТИТЬ** метод с hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="8a43f-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="8a43f-293">В рамках hello URI создайте hello после замены toocustomize запрос:</span><span class="sxs-lookup"><span data-stu-id="8a43f-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="8a43f-294">Замените *{scope}* с hello первый *AssignableScope* hello пользовательские роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="8a43f-295">Привет, следующие примеры показывают, как toospecify hello области для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="8a43f-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="8a43f-296">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="8a43f-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8a43f-297">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8a43f-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8a43f-298">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8a43f-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8a43f-299">Замените *{role-definition-id}* с идентификатором GUID hello hello пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="8a43f-300">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8a43f-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="8a43f-301">Для текста запроса hello укажите значения hello в hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="8a43f-301">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="8a43f-302">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="8a43f-302">Element Name</span></span> | <span data-ttu-id="8a43f-303">Обязательно</span><span class="sxs-lookup"><span data-stu-id="8a43f-303">Required</span></span> | <span data-ttu-id="8a43f-304">Тип</span><span class="sxs-lookup"><span data-stu-id="8a43f-304">Type</span></span> | <span data-ttu-id="8a43f-305">Описание</span><span class="sxs-lookup"><span data-stu-id="8a43f-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8a43f-306">name</span><span class="sxs-lookup"><span data-stu-id="8a43f-306">name</span></span> |<span data-ttu-id="8a43f-307">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-307">Yes</span></span> |<span data-ttu-id="8a43f-308">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-308">String</span></span> |<span data-ttu-id="8a43f-309">Идентификатор GUID пользовательской роли hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="8a43f-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="8a43f-310">properties.roleName</span></span> |<span data-ttu-id="8a43f-311">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-311">Yes</span></span> |<span data-ttu-id="8a43f-312">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-312">String</span></span> |<span data-ttu-id="8a43f-313">Отображаемое имя hello обновление пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="8a43f-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="8a43f-314">properties.description</span></span> |<span data-ttu-id="8a43f-315">Нет</span><span class="sxs-lookup"><span data-stu-id="8a43f-315">No</span></span> |<span data-ttu-id="8a43f-316">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-316">String</span></span> |<span data-ttu-id="8a43f-317">Описание hello обновить пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="8a43f-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="8a43f-318">properties.type</span></span> |<span data-ttu-id="8a43f-319">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-319">Yes</span></span> |<span data-ttu-id="8a43f-320">Строка</span><span class="sxs-lookup"><span data-stu-id="8a43f-320">String</span></span> |<span data-ttu-id="8a43f-321">Значение слишком «CustomRole».</span><span class="sxs-lookup"><span data-stu-id="8a43f-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="8a43f-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="8a43f-322">properties.permissions.actions</span></span> |<span data-ttu-id="8a43f-323">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-323">Yes</span></span> |<span data-ttu-id="8a43f-324">String[]</span><span class="sxs-lookup"><span data-stu-id="8a43f-324">String[]</span></span> |<span data-ttu-id="8a43f-325">Массив строк действий, указав hello операций toowhich hello обновить пользовательскую роль предоставляет доступ.</span><span class="sxs-lookup"><span data-stu-id="8a43f-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="8a43f-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="8a43f-326">properties.permissions.notActions</span></span> |<span data-ttu-id="8a43f-327">Нет</span><span class="sxs-lookup"><span data-stu-id="8a43f-327">No</span></span> |<span data-ttu-id="8a43f-328">String[]</span><span class="sxs-lookup"><span data-stu-id="8a43f-328">String[]</span></span> |<span data-ttu-id="8a43f-329">Массив действий строк, указав tooexclude операций hello от операций hello какие hello обновлены предоставляет пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="8a43f-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="8a43f-330">properties.assignableScopes</span></span> |<span data-ttu-id="8a43f-331">Да</span><span class="sxs-lookup"><span data-stu-id="8a43f-331">Yes</span></span> |<span data-ttu-id="8a43f-332">String[]</span><span class="sxs-lookup"><span data-stu-id="8a43f-332">String[]</span></span> |<span data-ttu-id="8a43f-333">Массив областей, в какие hello можно использовать обновленный пользовательской роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="8a43f-334">Ответ</span><span class="sxs-lookup"><span data-stu-id="8a43f-334">Response</span></span>
<span data-ttu-id="8a43f-335">Код состояния: 201.</span><span class="sxs-lookup"><span data-stu-id="8a43f-335">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a><span data-ttu-id="8a43f-336">Удаление настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="8a43f-336">Delete a Custom Role</span></span>
<span data-ttu-id="8a43f-337">Здесь описывается удаление настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="8a43f-337">Delete a custom role.</span></span>

<span data-ttu-id="8a43f-338">toodelete пользовательской роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/delete` операцию для всех hello `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="8a43f-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="8a43f-339">Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа.</span><span class="sxs-lookup"><span data-stu-id="8a43f-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="8a43f-340">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8a43f-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8a43f-341">Запрос</span><span class="sxs-lookup"><span data-stu-id="8a43f-341">Request</span></span>
<span data-ttu-id="8a43f-342">Используйте hello **удалить** метод с hello, следующий URI:</span><span class="sxs-lookup"><span data-stu-id="8a43f-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="8a43f-343">В рамках hello URI создайте hello после замены toocustomize запрос:</span><span class="sxs-lookup"><span data-stu-id="8a43f-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="8a43f-344">Замените *{scope}* с областью видимости hello, с которой вы хотите определения роли toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="8a43f-345">Привет, следующие примеры показывают, как toospecify hello области для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="8a43f-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="8a43f-346">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="8a43f-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8a43f-347">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8a43f-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8a43f-348">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8a43f-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8a43f-349">Замените *{role-definition-id}* с идентификатором hello GUID роли определение пользовательской роли hello.</span><span class="sxs-lookup"><span data-stu-id="8a43f-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="8a43f-350">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8a43f-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="8a43f-351">Ответ</span><span class="sxs-lookup"><span data-stu-id="8a43f-351">Response</span></span>
<span data-ttu-id="8a43f-352">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="8a43f-352">Status code: 200</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a><span data-ttu-id="8a43f-353">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8a43f-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
