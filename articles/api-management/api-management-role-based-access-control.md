---
title: "aaaHow tooUse ролевого контроля доступа в службе управления API Azure | Документы Microsoft"
description: "Узнайте, как toouse hello встроенных ролей и создание пользовательских ролей в службе управления API Azure"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>Как tooUse ролевого управления доступом в службе управления API Azure
Управления API Azure зависит от управления доступом Azure Role-Based (RBAC) tooenable подробного управления доступом для службы управления API и сущностей (например, API, политики). В этой статье дается обзор hello встроенных и пользовательских ролей в службе управления API. Если для получения дополнительных сведений для управления доступом в hello портала Azure см. раздел [Приступая к управлению доступом в hello портал Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Встроенные роли
В настоящее время API управления предоставляет 3 встроенные роли и добавит в hello ближайшее будущее 2 Дополнительные роли. Эти роли можно назначать в различных областях, включая подписку, группу ресурсов и отдельный экземпляр управления API. Для экземпляра Если tooan пользователя на уровне группы ресурсов hello назначена роль «Чтения службы управления API Azure» hello, затем hello пользователь будет иметь доступ для чтения экземпляров управления API tooall внутри группы ресурсов hello. 

Hello ниже приводится краткое описание каждого из hello встроенных ролей. Вы можете назначить эти роли с помощью hello портала Azure или других средств, включая Azure [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [интерфейс командной строки](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), и [API-интерфейса REST](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Дополнительные сведения о том, как tooassign встроенные роли, в разделе [использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Роль          | Доступ на чтение<sup>[1]</sup> | Доступ на запись<sup>[2]</sup> | Создание, удаление и масштабирование служб, настройка VPN и личных доменов | Доступ к toolegacy Publsiher портала | Описание
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Azure API Management Service Contributor | ✓ | ✓  | ✓  | ✓ | Суперпользователь. Имеет полный служб управления tooAPI доступа CRUD и сущностей (например, API-интерфейсы, политики). Имеет доступ toohello прежних версий publisher портала. |
| Azure API Management Service Reader | ✓  | | || Имеет доступ только для чтения tooAPI управления службами и сущностей. |
| Azure API Management Service Operator | ✓ | | ✓ | | Может управлять службами управления API, но не может управлять сущностями.|
| Azure API Management Service Editor<sup>*</sup> | ✓ | ✓ | |  | Может управлять сущностями управления API, но не может управлять службами.|
| Azure API Management Content Manager<sup>*</sup> | ✓ | | | ✓ | Может управлять порталом разработчика. Tooservices доступ только для чтения и сущностей.|

<sup>[1] службы управления tooAPI доступ для чтения и сущностей (например, API, политики)</sup>

<sup>Службы управления tooAPI доступ для записи [2] и сущностей, за исключением следующих opeartions: 1) экземпляр создание, удаление и масштабирование настройки доменного имени (3) пользовательские конфигурации VPN (2)</sup>

<sup>\*Hello редактор службы роли будут доступны после мы Миграция всех пользовательского интерфейса администратора из hello существующего издателя портала toohello портал Azure. Hello роль диспетчера содержимого будут доступны после рефакторинга портал издателя hello tooonly содержать портал разработчиков hello toomanaging связанные функциональные возможности.</sup>  


## <a name="custom-roles"></a>Пользовательские роли
Если ни один из встроенных ролей hello удовлетворения конкретных потребностей, пользовательские роли может быть создан tooprovide более детального управления для сущностей API управления доступом. Например можно создать пользовательскую роль, которая имеет доступ только для чтения tooan службы управления API, но имеет определенный интерфейс API tooone доступ на запись только. Дополнительные сведения о пользовательских ролях см. toolearn [настраиваемые роли в Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

При создании пользовательской роли, это проще toostart с одним из встроенных ролей hello. Изменить tooadd атрибуты hello hello действий, NotActions или AssignableScopes, а затем сохранить hello в качестве новой роли. Hello следующий пример начинается с ролью «Чтения службы управления API Azure» hello и создает пользовательской роли, называется «Калькулятор редактором API». Hello пользовательской роли могут назначаться только tooa конкретного API таким образом будет только имеет доступ toothat API. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Просмотр видеообзора

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Дальнейшие действия

* Узнайте больше об управлении доступом на основе ролей в Azure.
  * [Приступая к управлению доступом в hello портал Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Использовать tooyour роли назначения toomanage доступ к ресурсам подписки Azure](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Пользовательские роли в Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
