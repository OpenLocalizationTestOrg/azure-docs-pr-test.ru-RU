---
title: "aaaManage Azure решений с помощью PowerShell | Документы Microsoft"
description: "Используете Azure PowerShell и диспетчера ресурсов toomanage ресурсы."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>Управление ресурсами с помощью Azure PowerShell и Resource Manager
> [!div class="op_single_selector"]
> * [Портал](resource-group-portal.md)
> * [Интерфейс командной строки Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
>
>

В этой статье вы узнаете, как toomanage решений с помощью Azure PowerShell и диспетчера ресурсов Azure. Если вы не знакомы с Resource Manager, то см. статью [Общие сведения о диспетчере ресурсов Azure](resource-group-overview.md). Этот раздел посвящен задачам управления. Вы сможете выполнять следующие задачи:

1. Создание группы ресурсов
2. Добавить группу ресурсов toohello ресурсов
3. Добавить ресурс toohello тег
4. Запрос ресурсов на основе имен или значений тегов
5. Применение и удаление блокировку ресурса hello
6. Удаление группы ресурсов

В этой статье не отображается как toodeploy подписки tooyour шаблона диспетчера ресурсов. Эти сведения см. в статье [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md) (Развертывание ресурсов с использованием шаблонов Resource Manager и Azure PowerShell).

## <a name="get-started-with-azure-powershell"></a>Начало работы с Azure PowerShell

Если вы не установили Azure PowerShell, см. раздел [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

Если установлены в прошлом hello Azure PowerShell, но не его обновил недавно, рекомендуется установить последнюю версию hello. Вы можете обновить версию hello через hello метод, который используется tooinstall его. Например если вы использовали hello Web Platform Installer, повторный запуск и найти обновление.

использование вашей версии hello модуля ресурсы Azure toocheck hello следующий командлет:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Этот раздел был обновлен для версии 3.3.0. При наличии более ранней версии работы могут не соответствовать hello, описанного в этом разделе. Документацию о командлетах hello в этой версии см. в разделе [AzureRM.Resources модуль](/powershell/module/azurerm.resources).

## <a name="log-in-tooyour-azure-account"></a>Войдите в tooyour учетная запись Azure
Прежде чем начать работу над решением, необходимо войти в tooyour учетной записи.

toolog в tooyour учетная запись Azure, используйте hello **AzureRmAccount входа** командлета.

```powershell
Login-AzureRmAccount
```

Hello командлет запросит hello учетные данные входа для учетной записи Azure. После входа в систему, он загружает параметры учетной записи, таким образом, они будут доступны tooAzure PowerShell.

Hello командлет возвращает информацию о вашей учетной записи и hello toouse подписки для задач hello.

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

Если у вас есть несколько подписок, можно переключиться tooa другую подписку. Во-первых давайте посмотрим, все подписки hello для вашей учетной записи.

```powershell
Get-AzureRmSubscription
```

Отобразятся включенные и отключенные подписки.

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

tooswitch tooa другую подписку, укажите имя подписки hello с hello **AzureRmContext набор** командлета.

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>Создание группы ресурсов
Перед развертыванием tooyour подписки на все ресурсы, необходимо создать группу ресурсов, который будет содержать ресурсы hello.

использовать toocreate группу ресурсов hello **New AzureRmResourceGroup** командлета. Команда Hello использует hello **имя** toospecify параметра имя группы ресурсов hello и hello **расположение** toospecify параметр его расположение.

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

Вывод Hello имеет hello следующий формат:

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

Группа ресурсов tooretrieve hello позже, используйте hello, выполнив командлет:

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget все Здравствуйте групп ресурсов в подписке, не указано имя:

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>Добавить группы ресурсов tooa ресурсов
tooadd toohello ресурсов группы ресурсов, можно использовать hello **New-AzureRmResource** командлета или командлета, toohello определенного типа ресурсов создается (как **New AzureRmStorageAccount**). Может оказаться проще toouse командлета, так как он включает параметры для hello свойства, необходимые для нового ресурса hello tooa определенного типа ресурсов. toouse **New-AzureRmResource**, необходимо знать все tooset hello свойства без необходимости вводить их.

Однако добавление ресурса с помощью командлетов может ввести в заблуждение будущих поскольку hello новый ресурс не существует в шаблоне диспетчера ресурсов. Корпорация Майкрософт рекомендует определение hello инфраструктуры Azure решения в шаблона диспетчера ресурсов. Шаблоны позволяют tooreliably и повторно развернуть решение. В этом примере учетная запись хранения создается с помощью командлета PowerShell, но затем создается шаблон из группы ресурсов.

Привет, выполнив командлет создает учетную запись хранилища. Вместо использования имени hello, показано в примере hello, укажите уникальное имя для учетной записи хранения hello. Имя Hello должен находиться в диапазоне от 3 до 24 символов и содержать только строчные буквы и цифры. При использовании имени hello, показано в примере hello, сообщение об ошибке, поскольку это имя уже используется.

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

Если вам требуется tooretrieve этот ресурс позже, используйте hello, выполнив командлет:

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>Добавление тега

Теги позволяют tooorganize ресурсы в соответствии с toodifferent свойства. Например, может иметь несколько ресурсов в разных группах ресурсов, принадлежащих toohello же отдела. Можно применить отдел тег и значение toothose ресурсов toomark их как принадлежащий toohello одной категории. Также можно пометить, в какой среде используется ресурс — рабочей или тестовой. В этом разделе применяются теги tooonly один ресурс, но в вашей среде скорее всего, имеет смысл, tooapply теги tooall свои ресурсы.

Привет, выполнив командлет применяется два учетной записи хранилища tooyour теги:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

Теги обновляются как один объект. tooadd ресурс tooa тег, который уже включает теги, сначала получить существующие теги hello. Добавьте hello новый тег toohello объект, содержащий существующие теги hello и повторно применить все hello теги toohello ресурсов.

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>Поиск ресурсов

Используйте hello **Find-AzureRmResource** командлет tooretrieve ресурсы для поиска различных условий.

* tooget ресурсов по имени, предоставляют hello **ResourceNameContains** параметр:

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget все ресурсы hello в группе ресурсов обеспечивают hello **ResourceGroupNameContains** параметр:

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget все ресурсы hello имя тега и значением, обеспечивают hello **TagName** и **TagValue** параметры:

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* ресурсы hello tooall с определенного типа ресурсов, обеспечивают hello **ResourceType** параметр:

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>Блокировка ресурса

Когда требуется toomake убедитесь, что важный ресурс не удаляется случайно или изменены, применение toohello ресурса блокировки. Можно указать параметр **CanNotDelete** или **ReadOnly**.

блокировки управления toocreate или delete, необходимо иметь доступ слишком`Microsoft.Authorization/*` или `Microsoft.Authorization/locks/*` действия. Hello встроенных ролей эти действия предоставляются только владелец и администратор доступа пользователя.

tooapply блокировку, используйте следующий командлет hello:

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Hello ресурс блокировки в предшествующих пример hello нельзя удалить, пока блокировка hello удаляется. tooremove блокировку, используйте:

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Дополнительные сведения об установке блокировок см. в статье [Блокировка ресурсов с помощью диспетчера ресурсов Azure](resource-group-lock-resources.md).

## <a name="remove-resources-or-resource-group"></a>Удаление ресурсов или группы ресурсов
Ресурс или группу ресурсов можно удалить. При удалении группы ресурсов, также удалить все ресурсы hello в пределах этой группы ресурсов.

* ресурс из группы ресурсов hello, используйте hello toodelete **Remove-AzureRmResource** командлета. Этот командлет удаляет hello ресурсов, но не удаляет группу ресурсов hello.

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete группу ресурсов и его ресурсы используют hello **AzureRmResourceGroup удаление** командлета.

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

Для обоих командлетов предлагают tooconfirm нужно tooremove hello ресурс или группу ресурсов. Если операция hello успешно удаляет hello ресурс или группа ресурсов, он возвращает **True**.

## <a name="run-resource-manager-scripts-with-azure-automation"></a>Выполнение сценариев Resource Manager со службой автоматизации Azure

В этом разделе показано, как tooperform основных операций на ресурсы с помощью Azure PowerShell. Для более сложных сценариев управления обычно требуется toocreate сценария и повторно использовать этот скрипт, при необходимости, или по расписанию. [Служба автоматизации Azure](../automation/automation-intro.md) предоставляет способ для вас tooautomate распространенные сценарии, управляющие решений Azure.

Hello следующих разделах показано, как выполнять задачи управления toouse автоматизации Azure, диспетчер ресурсов и PowerShell tooeffectively:

- Сведения о создании модулей Runbook см. в статье [Мой первый модуль Runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).
- Сведения о работе с галереями сценариев см. в статье [Коллекции модулей Runbook и других модулей для службы автоматизации Azure](../automation/automation-runbook-gallery.md).
- Модули Runbook, запускать и останавливать виртуальные машины, в разделе [сценарий автоматизации Azure: toocreate формата JSON с помощью тегов расписание для включения и выключения виртуальной Машины Azure](../automation/automation-scenario-start-stop-vm-wjson-tags.md).
- Сведения о модулях Runbook, запускающих и останавливающих виртуальные машины в нерабочее время, см. в статье [Решение для запуска и остановки виртуальных машин в нерабочее время [предварительная версия] в службе автоматизации](../automation/automation-solution-vm-management.md).

## <a name="next-steps"></a>Дальнейшие действия
* в разделе toolearn о создании шаблонов диспетчера ресурсов [разработки шаблоны Azure Resource Manager](resource-group-authoring-templates.md).
* в разделе toolearn о развертывании шаблонов, [развернуть приложение с помощью шаблона Azure Resource Manager](resource-group-template-deploy.md).
* Можно переместить существующие ресурсы tooa новую группу ресурсов. Примеры см. в разделе [tooNew перемещение ресурсов группы ресурсов или подписку](resource-group-move-resources.md).
* Для получения рекомендаций по как предприятия могут использовать диспетчер ресурсов tooeffectively управление подписками см. в разделе [корпоративные функции формирования шаблонов - управление конкретные подписки](resource-manager-subscription-governance.md).

