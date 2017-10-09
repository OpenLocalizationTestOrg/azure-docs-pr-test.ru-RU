---
title: "aaaAzure контейнер реестра репозиториев | Документы Microsoft"
description: "Как toouse репозиториями реестра контейнера Azure для Docker images"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: cristyg
ms.openlocfilehash: 448fb812f537c9502041ce5fb372b0681a9dac4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-private-docker-container-registry-using-hello-azure-powershell"></a>Создание частного реестра контейнера Docker, с помощью hello Azure PowerShell
Использование команд в [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/overview) toocreate реестре контейнеров и управлять его параметрами с компьютера Windows. Можно также создать и управлять контейнера реестры с помощью hello [портал Azure](container-registry-get-started-portal.md), hello [Azure CLI](container-registry-get-started-azure-cli.md), или программным путем с контейнер реестра hello [API-интерфейса REST](https://go.microsoft.com/fwlink/p/?linkid=834376).


* Сведения и основные понятия, в разделе [Здравствуйте, Обзор](container-registry-intro.md)
* Полный список поддерживаемых командлетов см. в разделе [Командлеты управления реестром контейнеров Azure](https://docs.microsoft.com/en-us/powershell/module/azurerm.containerregistry/).


## <a name="prerequisites"></a>Предварительные требования
* **Azure PowerShell**: tooinstall и приступить к работе с Azure PowerShell см. в разделе hello [инструкции по установке](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). Войдите в tooyour подписки Azure, выполнив `Login-AzureRMAccount`. Дополнительные сведения см. в статье [Начало работы с Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azurep).
* **Группа ресурсов.** Перед созданием реестра контейнеров создайте [группу ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups) или используйте имеющуюся. Убедитесь, что группа ресурсов hello в место, где будет hello реестра контейнера службы [доступных](https://azure.microsoft.com/regions/services/). toocreate группу ресурсов с помощью Azure PowerShell, в разделе [hello Справочник PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps#create-a-resource-group).
* **Учетная запись хранения** (необязательно): создание стандартной Azure [учетной записи хранилища](../storage/common/storage-introduction.md) реестр контейнера hello tooback hello местоположения. Если не указать учетную запись хранилища при создании реестр с помощью `New-AzureRMContainerRegistry`, hello команда создает ее автоматически. toocreate хранилища учетной записи с помощью PowerShell см. в разделе [hello Справочник PowerShell](https://docs.microsoft.com/en-us/powershell/module/azure/new-azurestorageaccount). Хранилище класса Premium сейчас не поддерживается.
* **Субъект-служба (необязательно).** Если реестр создан с помощью PowerShell, по умолчанию доступ к нему не предоставляется. В зависимости от потребностей можно назначить существующий реестр tooa основной службы Azure Active Directory или создать и назначить новый. Кроме того можно включить учетную запись пользователя admin hello реестра. Hello разделах данной статьи. Дополнительные сведения о доступе к реестра см. в разделе [аутентификация с помощью реестра контейнера hello](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Создание реестра контейнеров
Запустите hello `New-AzureRMContainerRegistry` toocreate команда реестра контейнера.

> [!TIP]
> При создании реестра укажите глобально уникальное доменное имя верхнего уровня, содержащее только буквы и цифры. Имя реестра Hello в примерах hello `MyRegistry`, но заменить собственным уникальное имя.
>
>

Здравствуйте, следующая команда использует hello минимальные параметры toocreate контейнер реестра `MyRegistry` в группе ресурсов hello `MyResourceGroup` в hello местоположение в США:

```PowerShell
$Registry = New-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

* `-StorageAccountName` является необязательным. Если не указано, учетную запись хранения создается с именем, содержащим имя реестра hello и отметка времени в hello указал группу ресурсов.

## <a name="assign-a-service-principal"></a>Назначение субъекта-службы
Использовать команды PowerShell tooassign Azure Active Directory [участника-службы](../azure-resource-manager/resource-group-authenticate-service-principal.md) tooa реестра. Hello участника-службы в этих примерах назначается роль владельца hello, но можно назначить [других ролей](../active-directory/role-based-access-control-configure.md) Если требуется.

### <a name="create-a-service-principal"></a>Создание субъекта-службы
В hello следующую команду создается новый участника службы. Укажите надежный пароль для hello `-Password` параметра.

```PowerShell
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName ApplicationDisplayName -Password "MyPassword"
```

### <a name="assign-a-new-or-existing-service-principal"></a>Назначение нового или существующего субъекта-службы
Можно назначить нового или существующего участника tooa реестра службы. tooassign его владельца роли доступа toohello реестра, запустите команду аналогичные toohello, следующий пример:

```PowerShell
New-AzureRMRoleAssignment -RoleDefinitionName Owner -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Registry.Id
```

##<a name="sign-in-toohello-registry-with-hello-service-principal"></a>Войдите в реестре toohello с субъектом-службой hello
После назначения реестр toohello основной службы hello, можно выполнить вход с помощью hello следующую команду:

```PowerShell
docker login -u $ServicePrincipal.ApplicationId -p myPassword
```

## <a name="manage-admin-credentials"></a>Управление учетными данными администратора
Учетная запись администратора автоматически создается для каждого реестра контейнеров, но по умолчанию она отключена. Hello ниже примерах команд PowerShell toomanage hello учетные данные администратора для реестра контейнера.

### <a name="obtain-admin-user-credentials"></a>Получение учетных данных пользователя с правами администратора
```PowerShell
Get-AzureRMContainerRegistryCredential -ResourceGroupName "MyResourceGroup" -Name "MyRegistry"
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Включение пользователя с правами администратора для имеющегося реестра
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -EnableAdminUser
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Отключение пользователя с правами администратора для имеющегося реестра
```PowerShell
Update-AzureRMContainerRegistry -ResourceGroupName "MyResourceGroup" -Name "MyRegistry" -DisableAdminUser
```

## <a name="next-steps"></a>Дальнейшие действия
* [Принудительная первый образ с помощью hello Docker CLI](container-registry-get-started-docker-cli.md)
