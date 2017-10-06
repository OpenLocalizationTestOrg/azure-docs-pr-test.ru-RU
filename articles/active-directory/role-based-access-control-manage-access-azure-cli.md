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
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a>Управление на основе ролей управления доступом с hello Azure интерфейс командной строки
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Интерфейс командной строки Azure](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)


Управление доступом на основе ролей (RBAC) можно использовать в hello портал Azure и API диспетчера ресурсов Azure toomanage доступа tooyour подписка и ресурсы на уровне детально. С помощью этой функции можно предоставить доступ для пользователей, группы или субъекты-службы Active Directory путем назначения некоторых ролей toothem на определенную область.

Прежде чем использовать hello Azure командной строки (CLI) toomanage RBAC, необходимо иметь hello следующие предварительные требования:

* Интерфейс командной строки Azure версии 0.8.8 или более поздней. последнюю версию tooinstall hello и связывание его с подпиской Azure. в разделе [Установка и настройка hello Azure CLI](../cli-install-nodejs.md).
* Azure Resource Manager в Azure CLI. Go слишком[использование hello Azure CLI с hello диспетчера ресурсов](../xplat-cli-azure-resource-manager.md) для получения дополнительных сведений.

## <a name="list-roles"></a>Вывод списка ролей
### <a name="list-all-available-roles"></a>Вывод списка всех доступных ролей
toolist всем доступным ролям, используйте:

        azure role list

Hello примере показан список hello *всем доступным ролям*.

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Снимок экрана: командная строка RBAC Azure — список ролей Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a>Вывод списка действий роли
действия hello toolist роли, используйте:

    azure role show "<role name>"

Hello пример hello действия hello *участника* и *участника виртуальной машины* ролей.

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Снимок экрана: командная строка RBAC Azure — отображение ролей Azure](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a>Вывод списка доступа
### <a name="list-role-assignments-effective-on-a-resource-group"></a>Вывод списка назначений ролей, действующих в группе ресурсов
toolist hello назначения ролей, которые находятся в группе ресурсов, используйте:

    azure role assignment list --resource-group <resource group name>

Hello пример hello назначения ролей в hello *pharma sales-projecforcast* группы.

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Снимок экрана: командная строка RBAC Azure — список назначений ролей Azure по группам](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a>Список назначений ролей для пользователя
Используйте toolist hello назначения ролей для определенных пользователей и назначения hello, которые назначаются группам tooa пользователя:

    azure role assignment list --signInName <user email>

Также можно просмотреть назначения ролей, которые наследуются от групп, изменив hello команды:

    azure role assignment list --expandPrincipalGroups --signInName <user email>

Hello пример hello назначения ролей, которые предоставляются toohello  *sameert@aaddemo.com*  пользователя. Сюда входят роли, назначаемые непосредственно toohello пользователей и ролей, которые наследуются от групп.

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Снимок экрана: командная строка RBAC Azure — список назначений ролей Azure по пользователям](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a>Предоставление доступа
toogrant доступа после определения роли hello, что требуется tooassign использовать:

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a>Назначение роли toogroup в области видимости hello подписки
tooassign группу tooa ролей в области hello подписки, используйте:

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Hello следующий пример назначает hello *чтения* роли слишком*команды Анна Кох* в hello *подписки* области.

![Снимок экрана: командная строка RBAC Azure — создание назначений ролей Azure по группам](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Назначение роли приложения tooan в области видимости hello подписки
tooassign приложении tooan роли на уровне подписки hello, используйте:

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Hello следующий код предоставляет hello *участника* tooan роли *Azure AD* приложение hello выбранной подписки.

 ![Командная строка RBAC Azure — создание назначений ролей Azure по приложениям](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Назначить пользователя роли tooa в области группы ресурсов hello
tooassign tooa роли пользователя в области группы ресурсов hello, используйте:

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

Hello следующий код предоставляет hello *участника виртуальной машины* роли слишком *samert@aaddemo.com*  пользователя на hello *Pharma Sales-ProjectForcast* область группы ресурсов.

![Снимок экрана: командная строка RBAC Azure — создание назначений ролей Azure по пользователям](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Назначение роли tooa группы в области видимости ресурса hello
tooassign группу tooa ролей в области видимости ресурса hello, используйте:

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

Hello следующий код предоставляет hello *участника виртуальной машины* tooan роли *Azure AD* на *подсети*.

![Снимок экрана: командная строка RBAC Azure — создание назначений ролей Azure по группам](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a>Запрет доступа
Используйте tooremove назначение ролей.

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

Hello следующий пример удаляет hello *участника виртуальной машины* назначение роли hello  *sammert@aaddemo.com*  пользователя на hello *Pharma Sales-ProjectForcast* Группа ресурсов.
Затем пример Hello удаляет hello назначение ролей из группы в подписке hello.

![Снимок экрана: командная строка RBAC Azure — удаление назначений ролей Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a>Создание настраиваемой роли
Используйте toocreate пользовательской роли:

    azure role create --inputfile <file path>

Hello следующий пример создает пользовательскую роль вызывается *оператор виртуальной машины*. Предоставляет пользовательской роли, считываемых доступа tooall *Microsoft.Compute*, *хранилища Майкрософт*, и *Microsoft.Network* поставщиков и предоставляет доступ к ресурсам toostart, перезапуска и мониторинга виртуальных машин. Эту настраиваемую роль можно использовать в двух подписках. В этом примере в качестве входных данных используется JSON-файл.

![Снимок экрана: JSON — определение пользовательской роли](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![Снимок экрана: командная строка RBAC Azure — создание ролей Azure](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a>Изменение настраиваемой роли
toomodify пользовательской роли, сначала использовать hello `azure role show` команды tooretrieve определения роли. Во-вторых внести необходимые изменения toohello hello роли-файл определения. Наконец, используйте `azure role set` toosave hello изменения определения роли.

    azure role set --inputfile <file path>

Hello следующий пример добавляет hello *Microsoft.Insights/diagnosticSettings/* toohello операции **действия**и подписки Azure toohello **AssignableScopes**пользовательские роли виртуальной машины оператор hello.

![Снимок экрана: JSON — изменение определения пользовательской роли](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Снимок экрана: командная строка RBAC Azure — настройка ролей Azure](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a>Удаление настраиваемой роли
toodelete пользовательской роли, сначала использовать hello `azure role show` команда hello toodetermine **идентификатор** hello роли. Затем с помощью hello `azure role delete` роли hello toodelete команду, указав hello **идентификатор**.

Hello следующий пример удаляет hello *оператор виртуальной машины* пользовательской роли.

![Снимок экрана: командная строка RBAC Azure — удаление ролей Azure](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a>Вывод списка настраиваемых ролей
toolist hello ролей, доступных для назначения в области, используйте hello `azure role list` команды.

Hello следующую команду список всех ролей, доступных для назначения в подписке hello выбран.

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Снимок экрана: командная строка RBAC Azure — список ролей Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

В следующем примере hello, hello *оператор виртуальной машины* пользовательской роли не предусмотрена в hello *Production4* подписки, так как ее нет в hello  **AssignableScopes** hello роли.

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Снимок экрана: командная строка RBAC Azure — список пользовательских ролей Azure](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

