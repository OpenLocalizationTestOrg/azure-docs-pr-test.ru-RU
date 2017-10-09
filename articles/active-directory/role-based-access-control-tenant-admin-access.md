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
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Повышение прав доступа администратором клиентов с помощью управления доступом на основе ролей

Управление доступом на основе ролей позволяет администраторам клиентов временно повысить права доступа, чтобы предоставить больше разрешений, чем обычно. Администратор клиента может повысить себе toohello роли Администратор доступа пользователя, если это требуется. Эта роль предоставляет hello себе или другим toogrant разрешения администратора для клиента роли hello область «/».

Эта функция важна, так как она допускает hello клиента администратора toosee все hello подписок, которые существуют в организации. Он также позволяет для автоматизации приложений (например, выставление счетов и аудит) tooaccess все подписки hello и обеспечить точное представление состояния hello hello организации для выставления счетов или средства управления.  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Как toouse elevateAccess toogive клиента доступа

базовый процесс Hello работает с hello следующие шаги:

1. С помощью REST, вызовите *elevateAccess*, какие предоставляет вам Здравствуйте, администратор доступа пользователя роли на «/» области.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Создание [назначение ролей](/rest/api/authorization/roleassignments) tooassign любой роли в любой области. Следующий пример Hello показано назначение свойства hello hello роль модуля чтения в «/» области:

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

3. Являясь администратором доступа пользователей, можно также удалять назначения роли для области "/".

4. Отзовите привилегии администратора доступа пользователей, пока они не понадобятся вновь.


## <a name="how-tooundo-hello-elevateaccess-action"></a>Как tooundo hello elevateAccess действие

При вызове *elevateAccess* создать назначение ролей для текущего пользователя, поэтому toorevoke те права доступа вы должны toodelete hello назначения.

1.  Вызовите [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) где roleName = hello toodetermine администратор доступа пользователя имя GUID роли пользователя администратора hello. Hello ответ должен выглядеть следующим образом:

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

    Сохранить hello GUID из hello *имя* параметра в данном случае **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Вызовите [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get), где principalId — ваш ObjectId. Перечисляет все назначения, в клиенте hello. Найти для одного hello которых hello область «/» и заканчивается RoleDefinitionId hello роли hello имя идентификатором GUID, найденным в шаге 1. Назначение ролей Hello должен выглядеть следующим образом:

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

    Снова, сохраните hello GUID из hello *имя* параметра в данном случае **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

3. Наконец, вызовите [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) где roleAssignmentId = hello имя идентификатора GUID, определенным на шаге 2.

## <a name="next-steps"></a>Дальнейшие действия

- Узнайте больше об [управлении доступом на основе ролей с помощью REST](role-based-access-control-manage-access-rest.md).

- [Управление назначениями доступа](role-based-access-control-manage-assignments.md) в hello портал Azure
