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
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>Управление на основе ролей управления доступом с помощью API-интерфейса REST hello
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Интерфейс командной строки Azure](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

На основе ролей управления доступом (RBAC) в hello портал Azure и API диспетчера ресурсов Azure помогает управлять доступа tooyour подписка и ресурсы на уровне детально. С помощью этой функции можно предоставить доступ для пользователей, группы или субъекты-службы Active Directory путем назначения некоторых ролей toothem на определенную область.

## <a name="list-all-role-assignments"></a>Вывод списка всех назначений ролей
Все назначения ролей hello в указанный hello списки области и subscopes.

toolist назначения ролей, необходимо иметь доступ слишком`Microsoft.Authorization/roleAssignments/read` операцию в область hello. Все встроенные роли hello предоставляются toothis операции доступа. Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).

### <a name="request"></a>Запрос
Используйте hello **получить** метод с hello, следующий URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

В рамках hello URI создайте hello после замены toocustomize запрос:

1. Замените *{scope}* с областью видимости hello, для которого вы хотите toolist hello назначения ролей. Привет, следующие примеры показывают, как toospecify hello области для различных уровней:

   * Subscription: /subscriptions/{ИД_подписки}  
   * Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1  
   * Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Замените *{api-version}* значением 2015-07-01.
3. Замените *{filter}* с условием hello обратиться в список назначения роли hello toofilter tooapply:

   * Список назначений ролей для hello только указаны области, не включая hello назначений ролей на subscopes:`atScope()`    
   * Вывод списка назначений ролей для определенного пользователя, группы или приложения: `principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * Вывод списка назначений ролей для определенного пользователя, включая роли, унаследованные от групп | `assignedTo('{objectId of user}')`

### <a name="response"></a>Ответ
Код состояния: 200.

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

## <a name="get-information-about-a-role-assignment"></a>Получение сведений о назначении роли
Возвращает сведения о назначении одной роли, указанной идентификатором назначения роли hello.

tooget сведения о назначении роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleAssignments/read` операции. Все встроенные роли hello предоставляются toothis операции доступа. Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).

### <a name="request"></a>Запрос
Используйте hello **получить** метод с hello, следующий URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

В рамках hello URI создайте hello после замены toocustomize запрос:

1. Замените *{scope}* с областью видимости hello, для которого вы хотите toolist hello назначения ролей. Привет, следующие примеры показывают, как toospecify hello области для различных уровней:

   * Subscription: /subscriptions/{ИД_подписки}  
   * Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1  
   * Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Замените *{идентификатор роли назначения}* с идентификатором GUID hello hello назначение ролей.
3. Замените *{api-version}* значением 2015-07-01.

### <a name="response"></a>Ответ
Код состояния: 200.

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

## <a name="create-a-role-assignment"></a>Создание назначения роли
Создание роли назначения на hello указан области для hello указанного участника предоставление hello указанной роли.

toocreate назначение ролей, необходимо иметь доступ слишком`Microsoft.Authorization/roleAssignments/write` операции. Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа. Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).

### <a name="request"></a>Запрос
Используйте hello **ПОМЕСТИТЬ** метод с hello, следующий URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

В рамках hello URI создайте hello после замены toocustomize запрос:

1. Замените *{scope}* с областью видимости hello, с которой вы хотите toocreate hello назначения ролей. При создании назначения ролей в родительской области, все дочерние области наследуют hello же назначение ролей. Привет, следующие примеры показывают, как toospecify hello области для различных уровней:

   * Subscription: /subscriptions/{ИД_подписки}  
   * Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1   
   * Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Замените *{идентификатор роли назначения}* нового идентификатора GUID, которая становится идентификатор GUID hello hello создать назначение ролей.
3. Замените *{api-version}* значением 2015-07-01.

Для текста запроса hello укажите значения hello в hello следующий формат:

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| Имя элемента | Обязательно | Тип | Описание |
| --- | --- | --- | --- |
| roleDefinitionId |Да |Строка |Идентификатор Hello hello роли. Hello идентификатора hello выглядит следующим образом:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| principalId |Да |Строка |objectId hello Azure AD участника (пользователя, группы или субъекта-службы) назначена роль toowhich hello. |

### <a name="response"></a>Ответ
Код состояния: 201.

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

## <a name="delete-a-role-assignment"></a>Удаление назначения ролей
Удалить назначение роли в hello указана область.

toodelete назначение ролей, необходимо иметь доступ toohello `Microsoft.Authorization/roleAssignments/delete` операции. Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа. Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).

### <a name="request"></a>Запрос
Используйте hello **удалить** метод с hello, следующий URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

В рамках hello URI создайте hello после замены toocustomize запрос:

1. Замените *{scope}* с областью видимости hello, с которой вы хотите toocreate hello назначения ролей. Привет, следующие примеры показывают, как toospecify hello области для различных уровней:

   * Subscription: /subscriptions/{ИД_подписки}  
   * Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1  
   * Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Замените *{идентификатор роли назначения}* с идентификатором назначения роли hello GUID.
3. Замените *{api-version}* значением 2015-07-01.

### <a name="response"></a>Ответ
Код состояния: 200.

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

## <a name="list-all-roles"></a>Вывод списка всех ролей
Список всех ролей hello, доступных для назначения на указанный hello области.

toolist ролей, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/read` операцию в область hello. Все встроенные роли hello предоставляются toothis операции доступа. Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).

### <a name="request"></a>Запрос
Используйте hello **получить** метод с hello, следующий URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

В рамках hello URI создайте hello после замены toocustomize запрос:

1. Замените *{scope}* с областью видимости hello, для которого вы хотите toolist hello ролей. Привет, следующие примеры показывают, как toospecify hello области для различных уровней:

   * Subscription: /subscriptions/{ИД_подписки}  
   * Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1  
   * Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Замените *{api-version}* значением 2015-07-01.
3. Замените *{filter}* с условием hello, что вы хотите tooapply toofilter hello список ролей:

   * Список ролей, доступных для назначения на hello указаны области, а также все ее дочерние области:`atScopeAndBelow()`
   * Поиск с помощью точного отображаемого имени роли: `roleName%20eq%20'{role-display-name}'` Используйте форму URL-кодированием hello hello точное отображаемое имя роли hello. Например, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>Ответ
Код состояния: 200.

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

## <a name="get-information-about-a-role"></a>Получение сведений о роли
Возвращает сведения об одной роли, заданные hello идентификатор определения роли. tooget сведения об одной роли с помощью его отображаемое имя. в разделе [списка всех ролей](role-based-access-control-manage-access-rest.md#list-all-roles).

tooget сведения о роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/read` операции. Все встроенные роли hello предоставляются toothis операции доступа. Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).

### <a name="request"></a>Запрос
Используйте hello **получить** метод с hello, следующий URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

В рамках hello URI создайте hello после замены toocustomize запрос:

1. Замените *{scope}* с областью видимости hello, для которого вы хотите toolist hello назначения ролей. Привет, следующие примеры показывают, как toospecify hello области для различных уровней:

   * Subscription: /subscriptions/{ИД_подписки}  
   * Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1  
   * Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Замените *{role-definition-id}* с идентификатором GUID hello hello определения роли.
3. Замените *{api-version}* значением 2015-07-01.

### <a name="response"></a>Ответ
Код состояния: 200.

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

## <a name="create-a-custom-role"></a>Создание настраиваемой роли
Здесь описывается создание настраиваемой роли.

toocreate пользовательской роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/write` операцию для всех hello `AssignableScopes`. Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа. Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).

### <a name="request"></a>Запрос
Используйте hello **ПОМЕСТИТЬ** метод с hello, следующий URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

В рамках hello URI создайте hello после замены toocustomize запрос:

1. Замените *{scope}* с hello первый *AssignableScope* hello пользовательские роли. Привет, следующие примеры показывают, как toospecify hello области для различных уровней.

   * Subscription: /subscriptions/{ИД_подписки}  
   * Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1  
   * Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Замените *{role-definition-id}* нового идентификатора GUID, которая становится hello идентификатор GUID для новой настраиваемой роли hello.
3. Замените *{api-version}* значением 2015-07-01.

Для текста запроса hello укажите значения hello в hello следующий формат:

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

| Имя элемента | Обязательно | Тип | Описание |
| --- | --- | --- | --- |
| name |Да |Строка |Идентификатор GUID пользовательской роли hello. |
| properties.roleName |Да |Строка |Отображаемое имя пользовательской роли hello. Не может быть более 128 символов в длину. |
| properties.description |Нет |Строка |Описание hello пользовательской роли. Не может быть более 1024 символов в длину. |
| properties.type |Да |Строка |Значение слишком «CustomRole». |
| properties.permissions.actions |Да |String[] |Массив действий строк, указав hello операции, предоставляемые пользовательской роли hello. |
| properties.permissions.notActions |Нет |String[] |Массив строк действий, указав hello tooexclude операций из операции hello, предоставленные hello пользовательской роли. |
| properties.assignableScopes |Да |String[] |Массив областей, в какие hello используются пользовательские роли. |

### <a name="response"></a>Ответ
Код состояния: 201.

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

## <a name="update-a-custom-role"></a>Обновление настраиваемой роли
Здесь описывается изменение настраиваемой роли.

toomodify пользовательской роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/write` операцию для всех hello `AssignableScopes`. Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа. Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).

### <a name="request"></a>Запрос
Используйте hello **ПОМЕСТИТЬ** метод с hello, следующий URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

В рамках hello URI создайте hello после замены toocustomize запрос:

1. Замените *{scope}* с hello первый *AssignableScope* hello пользовательские роли. Привет, следующие примеры показывают, как toospecify hello области для различных уровней:

   * Subscription: /subscriptions/{ИД_подписки}  
   * Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1  
   * Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Замените *{role-definition-id}* с идентификатором GUID hello hello пользовательской роли.
3. Замените *{api-version}* значением 2015-07-01.

Для текста запроса hello укажите значения hello в hello следующий формат:

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

| Имя элемента | Обязательно | Тип | Описание |
| --- | --- | --- | --- |
| name |Да |Строка |Идентификатор GUID пользовательской роли hello. |
| properties.roleName |Да |Строка |Отображаемое имя hello обновление пользовательской роли. |
| properties.description |Нет |Строка |Описание hello обновить пользовательской роли. |
| properties.type |Да |Строка |Значение слишком «CustomRole». |
| properties.permissions.actions |Да |String[] |Массив строк действий, указав hello операций toowhich hello обновить пользовательскую роль предоставляет доступ. |
| properties.permissions.notActions |Нет |String[] |Массив действий строк, указав tooexclude операций hello от операций hello какие hello обновлены предоставляет пользовательской роли. |
| properties.assignableScopes |Да |String[] |Массив областей, в какие hello можно использовать обновленный пользовательской роли. |

### <a name="response"></a>Ответ
Код состояния: 201.

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

## <a name="delete-a-custom-role"></a>Удаление настраиваемой роли
Здесь описывается удаление настраиваемой роли.

toodelete пользовательской роли, необходимо иметь доступ слишком`Microsoft.Authorization/roleDefinitions/delete` операцию для всех hello `AssignableScopes`. Hello встроенных ролей, только *владельца* и *администратор доступа пользователя* предоставляются toothis операции доступа. Дополнительные сведения о назначениях ролей и управлении доступом к ресурсам Azure см. в статье [Использование назначений ролей для управления доступом к ресурсам в подписке Azure](role-based-access-control-configure.md).

### <a name="request"></a>Запрос
Используйте hello **удалить** метод с hello, следующий URI:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

В рамках hello URI создайте hello после замены toocustomize запрос:

1. Замените *{scope}* с областью видимости hello, с которой вы хотите определения роли toodelete hello. Привет, следующие примеры показывают, как toospecify hello области для различных уровней:

   * Subscription: /subscriptions/{ИД_подписки}  
   * Группа ресурсов: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1  
   * Ресурс: /subscriptions/{ИД_подписки}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Замените *{role-definition-id}* с идентификатором hello GUID роли определение пользовательской роли hello.
3. Замените *{api-version}* значением 2015-07-01.

### <a name="response"></a>Ответ
Код состояния: 200.

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

## <a name="next-steps"></a>Дальнейшие действия

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
