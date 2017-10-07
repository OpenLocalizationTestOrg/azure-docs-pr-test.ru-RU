---
title: "aaaCreate пользовательских ролей в RBAC Azure. | Документы Microsoft"
description: "Узнайте, как пользовательские роли toodefine с контроля доступа для более точного управления удостоверениями в вашей подписке Azure."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>Создание пользовательских ролей для управления доступом на основе ролей в Azure
Создайте пользовательскую роль в управления доступом Azure Role-Based (RBAC), если ни один из встроенных ролей hello соответствует потребностям специальный доступ. Можно создать настраиваемые роли с помощью [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [интерфейса командной строки Azure](role-based-access-control-manage-access-azure-cli.md) (CLI) и hello [API-интерфейса REST](role-based-access-control-manage-access-rest.md). Так же, как и встроенные роли можно назначить toousers пользовательские роли, группы и приложения в подписке, группы ресурсов и ресурсов областей. Пользовательские роли хранятся в клиенте Azure AD и могут использоваться несколькими подписками.

Каждый клиент можно создать пользовательские роли too2000. 

Hello ниже приведен пример пользовательской роли для мониторинга и перезапуска виртуальных машин.

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a>Действия
Hello **действия** свойства пользовательской роли указывает hello Azure операций toowhich hello роль предоставляет доступ. Это коллекция строк операций, которые определяют защищенные действия поставщиков ресурсов Azure. Формат hello выполните операцию строки `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Операции строк, которые содержат подстановочные знаки (\*) предоставить доступ tooall операций, которые сопоставляют строку hello операции. например

* `*/read`предоставляет доступ к tooread операции для всех типов ресурсов для всех поставщиков ресурсов Azure.
* `Microsoft.Compute/*`предоставляет доступ к tooall операции для всех типов ресурсов в поставщике ресурсов Microsoft.Compute hello.
* `Microsoft.Network/*/read`предоставляет доступ к tooread операции для всех типов ресурсов в поставщике ресурсов Microsoft.Network hello Azure.
* `Microsoft.Compute/virtualMachines/*`предоставляет доступ к операции tooall виртуальных машин и его дочерние типы ресурсов.
* `Microsoft.Web/sites/restart/Action`предоставляет доступ к toorestart веб-сайтов.

Используйте `Get-AzureRmProviderOperation` (в PowerShell) или `azure provider operations show` (в Azure CLI) toolist операций поставщиков ресурсов Azure. Можно также использовать эти tooverify команд, что операция строка является допустимой и строки операции tooexpand подстановочный знак.

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Снимок экрана PowerShell: Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Снимок экрана Azure CLI: azure provider operations show "Microsoft.Compute/virtualMachines/\*/action" ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
Используйте hello **NotActions** свойства, если набор операций, что вы хотите tooallow hello проще определить, исключив ограниченные операции. Hello доступа, предоставляемого пользовательской роли вычисляется путем вычитания hello **NotActions** операций из hello **действия** операций.

> [!NOTE]
> Если пользователю назначена роль, исключающей операции в **NotActions**и назначается как вторая роль, предоставляющую доступ toohello же операция, пользователь hello допускается tooperform этой операции. **NotActions** не deny правила — это просто toocreate удобный способ набор разрешенных операций при определенных операций требуется toobe исключен.
>
>

## <a name="assignablescopes"></a>AssignableScopes
Hello **AssignableScopes** свойства пользовательской роли hello указывает области hello (подписки, группы ресурсов или ресурсов), в течение которого hello пользовательской роли доступна для назначения. Hello пользовательской роли можно сделать доступными для назначения в hello подписки или групп ресурсов, которые требуют, а не пользователя помехи взаимодействия для оставшихся hello hello подписок или групп ресурсов.

Примеры допустимых назначаемых областей:

* «/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e», «/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624» - делает доступными для назначения роли hello в две подписки.
* «/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e» - делает доступными для назначения роли hello в одной подписке.
* «/ подписок или c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups сеть» - делает hello роли, назначаемые только в группе ресурсов сети hello.

> [!NOTE]
> Необходимо использовать по крайней мере одну подписку, группу ресурсов или идентификатор ресурса.
>
>

## <a name="custom-roles-access-control"></a>Контроль доступа к пользовательским ролям
Hello **AssignableScopes** свойства пользовательской роли hello также управляет, кто может просматривать, изменения и удаления роли hello.

* Кто может создавать пользовательские роли?
    Создавать пользовательские роли для использования в подписках, группах ресурсов и отдельных ресурсах могут владельцы (и администраторы доступа пользователей) этих областей.
    Hello Создание роли hello пользователю возможности tooperform toobe `Microsoft.Authorization/roleDefinition/write` операцию для всех hello **AssignableScopes** hello роли.
* Кто может изменять пользовательские роли?
    Изменять пользовательские роли для использования в подписках, группах ресурсов и отдельных ресурсах могут владельцы (и администраторы доступа пользователей) этих областей. Пользователи должны hello может tooperform toobe `Microsoft.Authorization/roleDefinition/write` операцию для всех hello **AssignableScopes** пользовательские роли.
* Кто может просматривать пользовательские роли?
    Все стандартные роли Azure RBAC позволяют просматривать список ролей, доступных для назначения. Пользователи, которые можно выполнять hello `Microsoft.Authorization/roleDefinition/read` операции на уровне области можно просмотреть hello RBAC ролей, доступных для назначения в этой области.

## <a name="see-also"></a>См. также
* [Управление доступом на основе ролей](role-based-access-control-configure.md): Приступая к работе с RBAC в hello портал Azure.
* Узнайте, как доступ к toomanage с:
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [Интерфейс командной строки Azure](role-based-access-control-manage-access-azure-cli.md)
  * [REST API](role-based-access-control-manage-access-rest.md)
* [Встроенные роли](role-based-access-built-in-roles.md): получение сведений о ролях hello, которые поставляются в RBAC.
