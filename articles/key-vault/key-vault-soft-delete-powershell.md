---
ms.assetid: 
title: "Хранилище ключей aaaAzure — как toouse soft удаление с помощью PowerShell"
description: "Примеры использования обратимого удаления с фрагментами кода для PowerShell."
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a>Как toouse хранилище ключей soft удаление с помощью PowerShell

Функция обратимого удаления в Azure Key Vault позволяет восстанавливать удаленные хранилища и объекты хранилищ. В частности адреса soft-delete hello следующие сценарии:

- Поддержка восстанавливаемого удаления хранилища ключей
- Поддержка восстанавливаемого удаления объектов хранилища ключей (например, ключей, секретов и сертификатов).

## <a name="prerequisites"></a>Предварительные требования

- Azure PowerShell 4.0.0 или более поздней версии — Если нет этом уже установки, установите Azure PowerShell и связать ее с подпиской Azure, см. раздел [как tooinstall и настройка Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview). 

>[!NOTE]
> Отсутствует файл устаревшей версией нашей форматирование вывода PowerShell ключ хранилища, который **может** загружаться в вашей среде вместо hello правильная версия. Мы планирование, что обновленная версия PowerShell toocontain hello необходимые исправления для hello форматирование выходных данных и обновит в это время в этом разделе. Здравствуйте текущее решение должно возникнуть проблема форматирования является:
> - Используйте hello следующем запросе, если вы не видите hello soft-delete включено свойство, описанное в этом разделе: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.


Дополнительные сведения о Key Vault для PowerShell см. в [справочнике по PowerShell для Azure Key Vault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

## <a name="required-permissions"></a>Необходимые разрешения

Операции Key Vault контролируются отдельно, посредством разрешений управления доступом на основе ролей (RBAC). Это осуществляется следующим образом.

| Операция | Описание | Разрешение пользователя |
|:--|:--|:--|
|список|Выводит список удаленных хранилищ ключей.|Microsoft.KeyVault/deletedVaults/read|
|Recover|Восстанавливает удаленное хранилище ключей.|Microsoft.KeyVault/vaults/write|
|Purge|Окончательно удаляет удаленное хранилище ключей и все его содержимое.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

Дополнительные сведения о разрешениях и управлении доступом см. в разделе [Защита хранилища ключей](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Включение обратимого удаления

возможности toorecover toobe удаленные хранилища ключей или объектов, хранящихся в ключе хранилище, необходимо сначала включить soft-delete для этого хранилища ключей.

### <a name="existing-key-vault"></a>Существующее хранилище ключей

Включите обратимое удаление для существующего хранилища ключей ContosoVault следующим образом. 

>[!NOTE]
>В настоящее время необходимые записи toouse диспетчера ресурсов Azure ресурсов обработки toodirectly hello *enableSoftDelete* toohello свойство ресурса хранилища ключей.

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>Новое хранилище ключей

Выполняется Включение soft-delete для нового хранилища ключей во время создания, добавив флаг enable soft-delete hello tooyour создать команду.

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>Проверка включения обратимого удаления

tooverify с soft-delete включено, в хранилище ключей выполнения hello *получить* команды и найдите hello, «Мягкое удалить включен?» и его значение (true или false).

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Удаление хранилища ключей, защищенного с помощью обратимого удаления

Hello команда toodelete (или удалить) хранилища ключей остается hello подобны, но изменения его поведения в зависимости от того, включена ли soft-delete или нет.

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
>При выполнении предыдущей команды hello для хранилища ключей, у которого нет soft-delete включено будут окончательно удалены этому хранилищу ключей и все ее содержимое без параметров для восстановления.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Как обратимое удаление защищает хранилище ключей

Если обратимое удаление включено:

- При удалении хранилища ключей, удаляется из соответствующей группы ресурсов и поместить в зарезервированному пространству имен, которое можно только связанные с расположением hello, где он был создан. 
- Объекты в удаленный ключ хранилища, таких как ключи, секреты и сертификатов, недоступен и остаются, а их содержащего хранилища ключей находится в состоянии hello удален. 
- Hello DNS-имя для хранилища ключей в удаленном состоянии сохраняется, поэтому не удается создать новое хранилище ключей с таким же именем.  

Можно просмотреть хранилищ ключей удаленном состоянии, связанные с подпиской, с помощью hello следующую команду:

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

Hello *идентификатор ресурса* в hello вывода относится toohello исходный идентификатор ресурса хранилища. Так как это хранилище ключей теперь находится в удаленном состоянии, ресурс с таким идентификатором ресурса не существует. Hello *идентификатор* поле может быть ресурсов hello tooidentify используется при восстановлении или удаления. Hello *запланированные даты очистки* поле указывает, когда хранилище hello будут окончательно удалены (удаление), если действие не выполняется для этого удаленного хранилища. hello toocalculate периода, который применяется для хранения по умолчанию Hello *запланированные даты очистки*, составляет 90 дней.

## <a name="recovering-a-key-vault"></a>Восстановление хранилища ключей

toorecover хранилища ключей, необходимо указать имя хранилища ключей toospecify hello, группу ресурсов и расположение. Примечание hello расположение и hello группа ресурсов hello удалить хранилище ключей, так как необходимые для процесса восстановления хранилища ключей.

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

При восстановлении хранилища ключей hello результатом является новый ресурс с идентификатором hello хранилища ключей исходного ресурса. При удалении группы ресурсов hello которых было hello хранилища ключей, перед восстановлением hello хранилища ключей должны создаваться новую группу ресурсов с таким же именем.

## <a name="key-vault-objects-and-soft-delete"></a>Объекты хранилища ключей и обратимое удаление

Ниже описывается удаление ключа ContosoFirstKey в хранилище ключей ContosoVault, в котором включено обратимое удаление.

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

Если в хранилище ключей включено обратимое удаление, то удаленный ключ отображается как удаленный, за исключением случаев, когда вы явным образом выводите список удаленных ключей или извлекаете их. За исключением перечислении удаленный ключ, он или очистка его не удастся большинства операций по ключу в состоянии hello удален. 

Например toorequest toolist удалены ключей в хранилище ключей, используйте hello следующую команду:

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>Переходное состояние 

При удалении ключа в хранилище ключей с soft-delete включено займет несколько секунд, чтобы переход toocomplete hello. Во время это переходное состояние может показаться, что разделу hello не в состоянии active hello или удалить hello. Эта команда выведет список всех удаленных ключей в хранилище ключей ContosoVault.

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Использование обратимого удаления с объектами хранилища ключей

Точно так же, как и в хранилищах ключей, удаленный ключ, секрет или сертификат останется в состоянии удаления для копирования too90 дней, если не восстановить ее или очистить его. 

#### <a name="keys"></a>ключей

toorecover удаленный ключ:

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

toopermanently удалить раздел:

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
>Очистка ключа приведет к его окончательному удалению, то есть восстановить его будет невозможно.

Hello **восстановить** и **очистки** действия имеют свои собственные разрешения, связанные политики доступа хранилища ключей. Для пользователя или службы основной toobe может tooexecute **восстановить** или **очистки** действия, они должны иметь hello соответствующие разрешения для этого объекта (ключа или секрета) в политике доступа hello хранилища ключей. По умолчанию hello **очистки** разрешение не добавляется в политику доступа tooa хранилища ключей при hello «all» ярлык — используется toogrant все tooa пользовательские разрешения. Необходимо явно предоставить разрешение на **очистку**. Здравствуйте, например, следующая команда предоставляет user@contoso.com tooperform разрешение несколько операции с ключами в *ContosoVault* включая **очистки**.

#### <a name="set-a-key-vault-access-policy"></a>Настройка политики доступа хранилища ключей

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> Если у вас есть хранилище ключей, в котором только что было включено обратимое удаление, то у вас может не быть разрешений на **восстановление** и **очистку**.

#### <a name="secrets"></a>Секреты

Как и в случае ключей, для операций с секретами в хранилище ключей используются собственные команды. Следующие, — это hello команды для удаления, список, восстановление и очистка секретные данные.

- Удаление секрета SQLPassword. 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- Вывод списка всех удаленных секретов в хранилище ключей. 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- Восстановите секрет в состоянии hello удалены: 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- Очистка секрета в удаленном состоянии. 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
>Очистка секрета приведет к его окончательному удалению, то есть восстановить его будет невозможно.

## <a name="purging-and-key-vaults"></a>Очистка и хранилище ключей

### <a name="key-vault-objects"></a>Объекты хранилища ключей

Очистка ключа, секрета или сертификата приведет к его окончательному удалению, то есть восстановить его будет невозможно. хранилище ключей Hello, содержит объект удален hello Однако останутся без изменений, как и другие объекты в хранилище ключей hello. 

### <a name="key-vaults-as-containers"></a>Хранилища ключей в роли контейнеров
При очистке хранилища ключей все его содержимое, включая ключи, секреты и сертификаты, удаляется без возможности восстановления. toopurge хранилища ключей, использовать hello `Remove-AzureRmKeyVault` команду с параметром hello `-InRemovedState` , указав расположение hello hello удалить хранилище ключей с hello `-Location location` аргумент. Можно найти расположение hello удаленного хранилища с помощью команды hello `Get-AzureRmKeyVault -InRemovedState`.

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
>Очистка хранилища ключей приведет к его окончательному удалению, то есть восстановить его будет невозможно.

### <a name="purge-permissions-required"></a>Необходимые разрешения на очистку
- toopurge удаленные хранилища ключей, таким образом, что хранилище hello и все ее содержимое, окончательно удаляются, hello пользователь должен tooperform разрешение RBAC *Microsoft.KeyVault/locations/deletedVaults/purge/action* операции. 
- ключ toolist hello удален, хранилище hello пользователь должен tooperform разрешение RBAC *Microsoft.KeyVault/deletedVaults/read* разрешение. 
- По умолчанию администратор подписки имеет эти разрешения. 

### <a name="scheduled-purge"></a>Очистка по расписанию

Перечисление объектов удаленного хранилища ключей показывает во время toobe schedled, удаленные с хранилищем ключей. Hello *запланированные даты очистки* поле указывает, когда объект хранилища ключей будут окончательно удалены, если никакие действия не выполняются. По умолчанию срок хранения hello объекта удаленного хранилища ключей составляет 90 дней.

>[!NOTE]
>После очистки объекта хранилища, активированной значением его поля *Scheduled Purge Date* (Запланированная дата очистки), этот объект будет окончательно удален. Восстановить его будет невозможно.

## <a name="other-resources"></a>Другие ресурсы:

- Обзор функции обратимого удаления Key Vault см. в разделе [Общие сведения об обратимом удалении в Azure Key Vault](key-vault-ovw-soft-delete.md).
- Общие сведения об использовании Azure Key Vault см. в разделе [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).

