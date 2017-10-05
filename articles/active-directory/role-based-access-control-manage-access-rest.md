---
title: "Управление доступом на основе ролей с помощью REST в Azure AD | Документация Майкрософт"
description: "Управление доступом на основе ролей с помощью интерфейса REST API"
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
ms.openlocfilehash: a5c19fd87ce1ae3e199bf1dfc8cf82f5653baac2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="b377e-103">Управление доступом на основе ролей с помощью REST API</span><span class="sxs-lookup"><span data-stu-id="b377e-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b377e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b377e-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="b377e-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="b377e-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="b377e-106">ИНТЕРФЕЙС REST API</span><span class="sxs-lookup"><span data-stu-id="b377e-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="b377e-107">Функция управления доступом на основе ролей (RBAC) на портале Azure и в API Azure Resource Manager помогает очень точно управлять доступом к подписке и ресурсам.</span><span class="sxs-lookup"><span data-stu-id="b377e-107">Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="b377e-108">С ее помощью вы можете предоставлять доступ пользователям, группам и субъектам-службам Active Directory, назначая им роли с определенной областью.</span><span class="sxs-lookup"><span data-stu-id="b377e-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="b377e-109">Вывод списка всех назначений ролей</span><span class="sxs-lookup"><span data-stu-id="b377e-109">List all role assignments</span></span>
<span data-ttu-id="b377e-110">Здесь описывается вывод списка всех назначений ролей в указанной области и внутренних областях.</span><span class="sxs-lookup"><span data-stu-id="b377e-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="b377e-111">Чтобы вывести список назначений ролей, требуется доступ к операции `Microsoft.Authorization/roleAssignments/read` в этой области.</span><span class="sxs-lookup"><span data-stu-id="b377e-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="b377e-112">Доступ к этой операции предоставляется всем встроенным ролям.</span><span class="sxs-lookup"><span data-stu-id="b377e-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="b377e-113">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b377e-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b377e-114">Запрос</span><span class="sxs-lookup"><span data-stu-id="b377e-114">Request</span></span>
<span data-ttu-id="b377e-115">Используйте метод **GET** со следующим универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="b377e-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="b377e-116">Чтобы настроить запрос, замените следующий текст в URI указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="b377e-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b377e-117">Замените *{scope}* областью, для которой требуется вывести список назначений ролей.</span><span class="sxs-lookup"><span data-stu-id="b377e-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="b377e-118">В следующих примерах показано, как указать область для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="b377e-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b377e-119">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="b377e-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b377e-120">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b377e-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b377e-121">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b377e-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b377e-122">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b377e-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="b377e-123">Замените *{filter}* условием, по которому требуется отфильтровать список назначений ролей.</span><span class="sxs-lookup"><span data-stu-id="b377e-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="b377e-124">Вывод списка назначений ролей только для определенной области без учета внутренних областей: `atScope()`</span><span class="sxs-lookup"><span data-stu-id="b377e-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="b377e-125">Вывод списка назначений ролей для определенного пользователя, группы или приложения: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="b377e-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="b377e-126">Вывод списка назначений ролей для определенного пользователя, включая роли, унаследованные от групп | `assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="b377e-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="b377e-127">Ответ</span><span class="sxs-lookup"><span data-stu-id="b377e-127">Response</span></span>
<span data-ttu-id="b377e-128">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="b377e-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="b377e-129">Получение сведений о назначении роли</span><span class="sxs-lookup"><span data-stu-id="b377e-129">Get information about a role assignment</span></span>
<span data-ttu-id="b377e-130">Здесь описывается получение сведений о назначении роли, указанной с помощью идентификатора.</span><span class="sxs-lookup"><span data-stu-id="b377e-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="b377e-131">Чтобы получить сведения о назначении роли, требуется доступ к операции `Microsoft.Authorization/roleAssignments/read`.</span><span class="sxs-lookup"><span data-stu-id="b377e-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="b377e-132">Доступ к этой операции предоставляется всем встроенным ролям.</span><span class="sxs-lookup"><span data-stu-id="b377e-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="b377e-133">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b377e-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b377e-134">Запрос</span><span class="sxs-lookup"><span data-stu-id="b377e-134">Request</span></span>
<span data-ttu-id="b377e-135">Используйте метод **GET** со следующим универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="b377e-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="b377e-136">Чтобы настроить запрос, замените следующий текст в URI указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="b377e-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b377e-137">Замените *{scope}* областью, для которой требуется вывести список назначений ролей.</span><span class="sxs-lookup"><span data-stu-id="b377e-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="b377e-138">В следующих примерах показано, как указать область для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="b377e-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b377e-139">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="b377e-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b377e-140">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b377e-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b377e-141">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b377e-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b377e-142">Замените *{role-assignment-id}* идентификатором GUID для назначения роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="b377e-143">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b377e-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b377e-144">Ответ</span><span class="sxs-lookup"><span data-stu-id="b377e-144">Response</span></span>
<span data-ttu-id="b377e-145">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="b377e-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="b377e-146">Создание назначения роли</span><span class="sxs-lookup"><span data-stu-id="b377e-146">Create a Role Assignment</span></span>
<span data-ttu-id="b377e-147">Здесь описывается создание назначения роли в указанной области для определенного субъекта, назначающего роль.</span><span class="sxs-lookup"><span data-stu-id="b377e-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="b377e-148">Чтобы создать назначение роли, требуется доступ к операции `Microsoft.Authorization/roleAssignments/write`.</span><span class="sxs-lookup"><span data-stu-id="b377e-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="b377e-149">Из встроенных ролей эту операцию могут выполнять только *владелец* и *администратор доступа пользователей*.</span><span class="sxs-lookup"><span data-stu-id="b377e-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b377e-150">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b377e-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b377e-151">Запрос</span><span class="sxs-lookup"><span data-stu-id="b377e-151">Request</span></span>
<span data-ttu-id="b377e-152">Используйте метод **PUT** со следующим универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="b377e-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="b377e-153">Чтобы настроить запрос, замените следующий текст в URI указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="b377e-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b377e-154">Замените *{scope}* областью, для которой требуется создать назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="b377e-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="b377e-155">При создании назначения роли в родительской области все дочерние области также его наследуют.</span><span class="sxs-lookup"><span data-stu-id="b377e-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="b377e-156">В следующих примерах показано, как указать область для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="b377e-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b377e-157">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="b377e-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b377e-158">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b377e-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="b377e-159">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b377e-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b377e-160">Замените *{role-assignment-id}* новым идентификатором GUID, который станет GUID нового назначения роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="b377e-161">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b377e-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="b377e-162">В тексте запроса введите значения в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="b377e-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="b377e-163">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b377e-163">Element Name</span></span> | <span data-ttu-id="b377e-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b377e-164">Required</span></span> | <span data-ttu-id="b377e-165">Тип</span><span class="sxs-lookup"><span data-stu-id="b377e-165">Type</span></span> | <span data-ttu-id="b377e-166">Описание</span><span class="sxs-lookup"><span data-stu-id="b377e-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b377e-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="b377e-167">roleDefinitionId</span></span> |<span data-ttu-id="b377e-168">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-168">Yes</span></span> |<span data-ttu-id="b377e-169">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-169">String</span></span> |<span data-ttu-id="b377e-170">Идентификатор роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-170">The identifier of the role.</span></span> <span data-ttu-id="b377e-171">Он указывается в формате `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="b377e-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="b377e-172">principalId</span><span class="sxs-lookup"><span data-stu-id="b377e-172">principalId</span></span> |<span data-ttu-id="b377e-173">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-173">Yes</span></span> |<span data-ttu-id="b377e-174">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-174">String</span></span> |<span data-ttu-id="b377e-175">ObjectId субъекта Azure AD (пользователя, группы или субъекта-службы), которому назначается роль.</span><span class="sxs-lookup"><span data-stu-id="b377e-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="b377e-176">Ответ</span><span class="sxs-lookup"><span data-stu-id="b377e-176">Response</span></span>
<span data-ttu-id="b377e-177">Код состояния: 201.</span><span class="sxs-lookup"><span data-stu-id="b377e-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="b377e-178">Удаление назначения ролей</span><span class="sxs-lookup"><span data-stu-id="b377e-178">Delete a Role Assignment</span></span>
<span data-ttu-id="b377e-179">Здесь описывается удаление назначения роли в указанной области.</span><span class="sxs-lookup"><span data-stu-id="b377e-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="b377e-180">Чтобы удалить назначение роли, требуется доступ к операции `Microsoft.Authorization/roleAssignments/delete`.</span><span class="sxs-lookup"><span data-stu-id="b377e-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="b377e-181">Из встроенных ролей эту операцию могут выполнять только *владелец* и *администратор доступа пользователей*.</span><span class="sxs-lookup"><span data-stu-id="b377e-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b377e-182">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b377e-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b377e-183">Запрос</span><span class="sxs-lookup"><span data-stu-id="b377e-183">Request</span></span>
<span data-ttu-id="b377e-184">Используйте метод **DELETE** со следующим универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="b377e-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="b377e-185">Чтобы настроить запрос, замените следующий текст в URI указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="b377e-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b377e-186">Замените *{scope}* областью, для которой требуется создать назначения ролей.</span><span class="sxs-lookup"><span data-stu-id="b377e-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="b377e-187">В следующих примерах показано, как указать область для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="b377e-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b377e-188">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="b377e-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b377e-189">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b377e-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b377e-190">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b377e-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b377e-191">Замените *{role-assignment-id}* идентификатором GUID для назначения роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="b377e-192">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b377e-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b377e-193">Ответ</span><span class="sxs-lookup"><span data-stu-id="b377e-193">Response</span></span>
<span data-ttu-id="b377e-194">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="b377e-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="b377e-195">Вывод списка всех ролей</span><span class="sxs-lookup"><span data-stu-id="b377e-195">List all Roles</span></span>
<span data-ttu-id="b377e-196">Здесь описывается вывод списка всех ролей, которые доступны для назначения в указанной области.</span><span class="sxs-lookup"><span data-stu-id="b377e-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="b377e-197">Для вывода списка ролей требуется доступ к операции `Microsoft.Authorization/roleDefinitions/read` в этой области.</span><span class="sxs-lookup"><span data-stu-id="b377e-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="b377e-198">Доступ к этой операции предоставляется всем встроенным ролям.</span><span class="sxs-lookup"><span data-stu-id="b377e-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="b377e-199">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b377e-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b377e-200">Запрос</span><span class="sxs-lookup"><span data-stu-id="b377e-200">Request</span></span>
<span data-ttu-id="b377e-201">Используйте метод **GET** со следующим универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="b377e-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="b377e-202">Чтобы настроить запрос, замените следующий текст в URI указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="b377e-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b377e-203">Замените *{scope}* областью, для которой требуется вывести список ролей.</span><span class="sxs-lookup"><span data-stu-id="b377e-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="b377e-204">В следующих примерах показано, как указать область для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="b377e-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b377e-205">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="b377e-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b377e-206">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b377e-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b377e-207">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b377e-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b377e-208">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b377e-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="b377e-209">Замените *{filter}* условием, по которому требуется отфильтровать список ролей.</span><span class="sxs-lookup"><span data-stu-id="b377e-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="b377e-210">Вывод списка ролей, доступных для назначения в указанной области и любой из ее дочерних областей: `atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="b377e-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="b377e-211">Поиск с помощью точного отображаемого имени роли: `roleName%20eq%20'{role-display-name}'`</span><span class="sxs-lookup"><span data-stu-id="b377e-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="b377e-212">Используйте точное отображаемое имя роли в формате URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="b377e-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="b377e-213">Например, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="b377e-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="b377e-214">Ответ</span><span class="sxs-lookup"><span data-stu-id="b377e-214">Response</span></span>
<span data-ttu-id="b377e-215">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="b377e-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="get-information-about-a-role"></a><span data-ttu-id="b377e-216">Получение сведений о роли</span><span class="sxs-lookup"><span data-stu-id="b377e-216">Get information about a Role</span></span>
<span data-ttu-id="b377e-217">Здесь описывается получение сведений о роли, указанной с помощью идентификатора определения роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="b377e-218">Чтобы получить сведения о роли с помощью ее отображаемого имени, ознакомьтесь с разделом [Вывод списка всех ролей](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="b377e-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="b377e-219">Чтобы получить сведения о роли, требуется доступ к операции `Microsoft.Authorization/roleDefinitions/read`.</span><span class="sxs-lookup"><span data-stu-id="b377e-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="b377e-220">Доступ к этой операции предоставляется всем встроенным ролям.</span><span class="sxs-lookup"><span data-stu-id="b377e-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="b377e-221">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b377e-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b377e-222">Запрос</span><span class="sxs-lookup"><span data-stu-id="b377e-222">Request</span></span>
<span data-ttu-id="b377e-223">Используйте метод **GET** со следующим универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="b377e-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b377e-224">Чтобы настроить запрос, замените следующий текст в URI указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="b377e-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b377e-225">Замените *{scope}* областью, для которой требуется вывести список назначений ролей.</span><span class="sxs-lookup"><span data-stu-id="b377e-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="b377e-226">В следующих примерах показано, как указать область для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="b377e-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b377e-227">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="b377e-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b377e-228">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b377e-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b377e-229">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b377e-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b377e-230">Замените *{role-definition-id}* идентификатором GUID для определения роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="b377e-231">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b377e-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b377e-232">Ответ</span><span class="sxs-lookup"><span data-stu-id="b377e-232">Response</span></span>
<span data-ttu-id="b377e-233">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="b377e-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="create-a-custom-role"></a><span data-ttu-id="b377e-234">Создание настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="b377e-234">Create a Custom Role</span></span>
<span data-ttu-id="b377e-235">Здесь описывается создание настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-235">Create a custom role.</span></span>

<span data-ttu-id="b377e-236">Чтобы создать настраиваемую роль, требуется доступ к операции `Microsoft.Authorization/roleDefinitions/write` во всех областях `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="b377e-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="b377e-237">Из встроенных ролей эту операцию могут выполнять только *владелец* и *администратор доступа пользователей*.</span><span class="sxs-lookup"><span data-stu-id="b377e-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b377e-238">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b377e-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b377e-239">Запрос</span><span class="sxs-lookup"><span data-stu-id="b377e-239">Request</span></span>
<span data-ttu-id="b377e-240">Используйте метод **PUT** со следующим универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="b377e-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b377e-241">Чтобы настроить запрос, замените следующий текст в URI указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="b377e-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b377e-242">Замените *{scope}* первой областью *AssignableScope* для настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="b377e-243">В следующих примерах показано, как указать область для различных уровней.</span><span class="sxs-lookup"><span data-stu-id="b377e-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="b377e-244">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="b377e-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b377e-245">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b377e-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b377e-246">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b377e-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b377e-247">Замените *{role-definition-id}* новым идентификатором GUID, который станет GUID новой настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="b377e-248">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b377e-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="b377e-249">В тексте запроса введите значения в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="b377e-249">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="b377e-250">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b377e-250">Element Name</span></span> | <span data-ttu-id="b377e-251">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b377e-251">Required</span></span> | <span data-ttu-id="b377e-252">Тип</span><span class="sxs-lookup"><span data-stu-id="b377e-252">Type</span></span> | <span data-ttu-id="b377e-253">Описание</span><span class="sxs-lookup"><span data-stu-id="b377e-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b377e-254">name</span><span class="sxs-lookup"><span data-stu-id="b377e-254">name</span></span> |<span data-ttu-id="b377e-255">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-255">Yes</span></span> |<span data-ttu-id="b377e-256">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-256">String</span></span> |<span data-ttu-id="b377e-257">Идентификатор GUID настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="b377e-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="b377e-258">properties.roleName</span></span> |<span data-ttu-id="b377e-259">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-259">Yes</span></span> |<span data-ttu-id="b377e-260">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-260">String</span></span> |<span data-ttu-id="b377e-261">Отображаемое имя настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-261">Display name of the custom role.</span></span> <span data-ttu-id="b377e-262">Не может быть более 128 символов в длину.</span><span class="sxs-lookup"><span data-stu-id="b377e-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="b377e-263">properties.description</span><span class="sxs-lookup"><span data-stu-id="b377e-263">properties.description</span></span> |<span data-ttu-id="b377e-264">Нет</span><span class="sxs-lookup"><span data-stu-id="b377e-264">No</span></span> |<span data-ttu-id="b377e-265">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-265">String</span></span> |<span data-ttu-id="b377e-266">Описание настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-266">Description of the custom role.</span></span> <span data-ttu-id="b377e-267">Не может быть более 1024 символов в длину.</span><span class="sxs-lookup"><span data-stu-id="b377e-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="b377e-268">properties.type</span><span class="sxs-lookup"><span data-stu-id="b377e-268">properties.type</span></span> |<span data-ttu-id="b377e-269">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-269">Yes</span></span> |<span data-ttu-id="b377e-270">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-270">String</span></span> |<span data-ttu-id="b377e-271">Укажите значение CustomRole.</span><span class="sxs-lookup"><span data-stu-id="b377e-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="b377e-272">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="b377e-272">properties.permissions.actions</span></span> |<span data-ttu-id="b377e-273">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-273">Yes</span></span> |<span data-ttu-id="b377e-274">String[]</span><span class="sxs-lookup"><span data-stu-id="b377e-274">String[]</span></span> |<span data-ttu-id="b377e-275">Массив строк действий, определяющих операции, к которым предоставляет доступ настраиваемая роль.</span><span class="sxs-lookup"><span data-stu-id="b377e-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="b377e-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="b377e-276">properties.permissions.notActions</span></span> |<span data-ttu-id="b377e-277">Нет</span><span class="sxs-lookup"><span data-stu-id="b377e-277">No</span></span> |<span data-ttu-id="b377e-278">String[]</span><span class="sxs-lookup"><span data-stu-id="b377e-278">String[]</span></span> |<span data-ttu-id="b377e-279">Массив строк действий, определяющих операции, исключаемые из списка операций, к которым предоставляет доступ настраиваемая роль.</span><span class="sxs-lookup"><span data-stu-id="b377e-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="b377e-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="b377e-280">properties.assignableScopes</span></span> |<span data-ttu-id="b377e-281">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-281">Yes</span></span> |<span data-ttu-id="b377e-282">String[]</span><span class="sxs-lookup"><span data-stu-id="b377e-282">String[]</span></span> |<span data-ttu-id="b377e-283">Массив областей, в которых можно использовать настраиваемую роль.</span><span class="sxs-lookup"><span data-stu-id="b377e-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="b377e-284">Ответ</span><span class="sxs-lookup"><span data-stu-id="b377e-284">Response</span></span>
<span data-ttu-id="b377e-285">Код состояния: 201.</span><span class="sxs-lookup"><span data-stu-id="b377e-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="b377e-286">Обновление настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="b377e-286">Update a Custom Role</span></span>
<span data-ttu-id="b377e-287">Здесь описывается изменение настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-287">Modify a custom role.</span></span>

<span data-ttu-id="b377e-288">Чтобы изменить настраиваемую роль, требуется доступ к операции `Microsoft.Authorization/roleDefinitions/write` во всех областях `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="b377e-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="b377e-289">Из встроенных ролей эту операцию могут выполнять только *владелец* и *администратор доступа пользователей*.</span><span class="sxs-lookup"><span data-stu-id="b377e-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b377e-290">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b377e-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b377e-291">Запрос</span><span class="sxs-lookup"><span data-stu-id="b377e-291">Request</span></span>
<span data-ttu-id="b377e-292">Используйте метод **PUT** со следующим универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="b377e-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b377e-293">Чтобы настроить запрос, замените следующий текст в URI указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="b377e-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b377e-294">Замените *{scope}* первой областью *AssignableScope* для настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="b377e-295">В следующих примерах показано, как указать область для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="b377e-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b377e-296">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="b377e-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b377e-297">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b377e-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b377e-298">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b377e-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b377e-299">Замените *{role-definition-id}* идентификатором GUID настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="b377e-300">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b377e-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="b377e-301">В тексте запроса введите значения в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="b377e-301">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="b377e-302">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="b377e-302">Element Name</span></span> | <span data-ttu-id="b377e-303">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b377e-303">Required</span></span> | <span data-ttu-id="b377e-304">Тип</span><span class="sxs-lookup"><span data-stu-id="b377e-304">Type</span></span> | <span data-ttu-id="b377e-305">Описание</span><span class="sxs-lookup"><span data-stu-id="b377e-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b377e-306">name</span><span class="sxs-lookup"><span data-stu-id="b377e-306">name</span></span> |<span data-ttu-id="b377e-307">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-307">Yes</span></span> |<span data-ttu-id="b377e-308">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-308">String</span></span> |<span data-ttu-id="b377e-309">Идентификатор GUID настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="b377e-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="b377e-310">properties.roleName</span></span> |<span data-ttu-id="b377e-311">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-311">Yes</span></span> |<span data-ttu-id="b377e-312">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-312">String</span></span> |<span data-ttu-id="b377e-313">Отображаемое имя обновленной настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="b377e-314">properties.description</span><span class="sxs-lookup"><span data-stu-id="b377e-314">properties.description</span></span> |<span data-ttu-id="b377e-315">Нет</span><span class="sxs-lookup"><span data-stu-id="b377e-315">No</span></span> |<span data-ttu-id="b377e-316">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-316">String</span></span> |<span data-ttu-id="b377e-317">Описание обновленной настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="b377e-318">properties.type</span><span class="sxs-lookup"><span data-stu-id="b377e-318">properties.type</span></span> |<span data-ttu-id="b377e-319">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-319">Yes</span></span> |<span data-ttu-id="b377e-320">Строка</span><span class="sxs-lookup"><span data-stu-id="b377e-320">String</span></span> |<span data-ttu-id="b377e-321">Укажите значение CustomRole.</span><span class="sxs-lookup"><span data-stu-id="b377e-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="b377e-322">properties.permissions.actions</span><span class="sxs-lookup"><span data-stu-id="b377e-322">properties.permissions.actions</span></span> |<span data-ttu-id="b377e-323">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-323">Yes</span></span> |<span data-ttu-id="b377e-324">String[]</span><span class="sxs-lookup"><span data-stu-id="b377e-324">String[]</span></span> |<span data-ttu-id="b377e-325">Массив строк действий, определяющих операции, к которым предоставляет доступ обновленная настраиваемая роль.</span><span class="sxs-lookup"><span data-stu-id="b377e-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="b377e-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="b377e-326">properties.permissions.notActions</span></span> |<span data-ttu-id="b377e-327">Нет</span><span class="sxs-lookup"><span data-stu-id="b377e-327">No</span></span> |<span data-ttu-id="b377e-328">String[]</span><span class="sxs-lookup"><span data-stu-id="b377e-328">String[]</span></span> |<span data-ttu-id="b377e-329">Массив строк действий, определяющих операции, исключаемых из списка операций, к которым предоставляет доступ обновленная настраиваемая роль.</span><span class="sxs-lookup"><span data-stu-id="b377e-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="b377e-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="b377e-330">properties.assignableScopes</span></span> |<span data-ttu-id="b377e-331">Да</span><span class="sxs-lookup"><span data-stu-id="b377e-331">Yes</span></span> |<span data-ttu-id="b377e-332">String[]</span><span class="sxs-lookup"><span data-stu-id="b377e-332">String[]</span></span> |<span data-ttu-id="b377e-333">Массив областей, в которых можно использовать обновленную настраиваемую роль.</span><span class="sxs-lookup"><span data-stu-id="b377e-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="b377e-334">Ответ</span><span class="sxs-lookup"><span data-stu-id="b377e-334">Response</span></span>
<span data-ttu-id="b377e-335">Код состояния: 201.</span><span class="sxs-lookup"><span data-stu-id="b377e-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="b377e-336">Удаление настраиваемой роли</span><span class="sxs-lookup"><span data-stu-id="b377e-336">Delete a Custom Role</span></span>
<span data-ttu-id="b377e-337">Здесь описывается удаление настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-337">Delete a custom role.</span></span>

<span data-ttu-id="b377e-338">Чтобы удалить настраиваемую роль, требуется доступ к операции `Microsoft.Authorization/roleDefinitions/delete` во всех областях `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="b377e-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="b377e-339">Из встроенных ролей эту операцию могут выполнять только *владелец* и *администратор доступа пользователей*.</span><span class="sxs-lookup"><span data-stu-id="b377e-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="b377e-340">Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b377e-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="b377e-341">Запрос</span><span class="sxs-lookup"><span data-stu-id="b377e-341">Request</span></span>
<span data-ttu-id="b377e-342">Используйте метод **DELETE** со следующим универсальным кодом ресурса (URI).</span><span class="sxs-lookup"><span data-stu-id="b377e-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="b377e-343">Чтобы настроить запрос, замените следующий текст в URI указанными значениями.</span><span class="sxs-lookup"><span data-stu-id="b377e-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="b377e-344">Замените *{scope}* областью, в которой требуется удалить определение роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="b377e-345">В следующих примерах показано, как указать область для различных уровней:</span><span class="sxs-lookup"><span data-stu-id="b377e-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="b377e-346">Subscription: /subscriptions/{ИД_подписки}</span><span class="sxs-lookup"><span data-stu-id="b377e-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="b377e-347">Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="b377e-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="b377e-348">Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="b377e-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="b377e-349">Замените *{role-definition-id}* идентификатором GUID для определения настраиваемой роли.</span><span class="sxs-lookup"><span data-stu-id="b377e-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="b377e-350">Замените *{api-version}* значением 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="b377e-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="b377e-351">Ответ</span><span class="sxs-lookup"><span data-stu-id="b377e-351">Response</span></span>
<span data-ttu-id="b377e-352">Код состояния: 200.</span><span class="sxs-lookup"><span data-stu-id="b377e-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b377e-353">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b377e-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
