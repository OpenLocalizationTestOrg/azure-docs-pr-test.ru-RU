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
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="18697-103">Как toouse хранилище ключей soft удаление с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="18697-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="18697-104">Функция обратимого удаления в Azure Key Vault позволяет восстанавливать удаленные хранилища и объекты хранилищ.</span><span class="sxs-lookup"><span data-stu-id="18697-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="18697-105">В частности адреса soft-delete hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="18697-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="18697-106">Поддержка восстанавливаемого удаления хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="18697-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="18697-107">Поддержка восстанавливаемого удаления объектов хранилища ключей (например, ключей, секретов и сертификатов).</span><span class="sxs-lookup"><span data-stu-id="18697-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18697-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="18697-108">Prerequisites</span></span>

- <span data-ttu-id="18697-109">Azure PowerShell 4.0.0 или более поздней версии — Если нет этом уже установки, установите Azure PowerShell и связать ее с подпиской Azure, см. раздел [как tooinstall и настройка Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="18697-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="18697-110">Отсутствует файл устаревшей версией нашей форматирование вывода PowerShell ключ хранилища, который **может** загружаться в вашей среде вместо hello правильная версия.</span><span class="sxs-lookup"><span data-stu-id="18697-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="18697-111">Мы планирование, что обновленная версия PowerShell toocontain hello необходимые исправления для hello форматирование выходных данных и обновит в это время в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="18697-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="18697-112">Здравствуйте текущее решение должно возникнуть проблема форматирования является:</span><span class="sxs-lookup"><span data-stu-id="18697-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="18697-113">Используйте hello следующем запросе, если вы не видите hello soft-delete включено свойство, описанное в этом разделе: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="18697-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="18697-114">Дополнительные сведения о Key Vault для PowerShell см. в [справочнике по PowerShell для Azure Key Vault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="18697-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="18697-115">Необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="18697-115">Required permissions</span></span>

<span data-ttu-id="18697-116">Операции Key Vault контролируются отдельно, посредством разрешений управления доступом на основе ролей (RBAC). Это осуществляется следующим образом.</span><span class="sxs-lookup"><span data-stu-id="18697-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="18697-117">Операция</span><span class="sxs-lookup"><span data-stu-id="18697-117">Operation</span></span> | <span data-ttu-id="18697-118">Описание</span><span class="sxs-lookup"><span data-stu-id="18697-118">Description</span></span> | <span data-ttu-id="18697-119">Разрешение пользователя</span><span class="sxs-lookup"><span data-stu-id="18697-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="18697-120">список</span><span class="sxs-lookup"><span data-stu-id="18697-120">List</span></span>|<span data-ttu-id="18697-121">Выводит список удаленных хранилищ ключей.</span><span class="sxs-lookup"><span data-stu-id="18697-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="18697-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="18697-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="18697-123">Recover</span><span class="sxs-lookup"><span data-stu-id="18697-123">Recover</span></span>|<span data-ttu-id="18697-124">Восстанавливает удаленное хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="18697-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="18697-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="18697-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="18697-126">Purge</span><span class="sxs-lookup"><span data-stu-id="18697-126">Purge</span></span>|<span data-ttu-id="18697-127">Окончательно удаляет удаленное хранилище ключей и все его содержимое.</span><span class="sxs-lookup"><span data-stu-id="18697-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="18697-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="18697-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="18697-129">Дополнительные сведения о разрешениях и управлении доступом см. в разделе [Защита хранилища ключей](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="18697-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="18697-130">Включение обратимого удаления</span><span class="sxs-lookup"><span data-stu-id="18697-130">Enabling soft-delete</span></span>

<span data-ttu-id="18697-131">возможности toorecover toobe удаленные хранилища ключей или объектов, хранящихся в ключе хранилище, необходимо сначала включить soft-delete для этого хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="18697-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="18697-132">Существующее хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="18697-132">Existing key vault</span></span>

<span data-ttu-id="18697-133">Включите обратимое удаление для существующего хранилища ключей ContosoVault следующим образом.</span><span class="sxs-lookup"><span data-stu-id="18697-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="18697-134">В настоящее время необходимые записи toouse диспетчера ресурсов Azure ресурсов обработки toodirectly hello *enableSoftDelete* toohello свойство ресурса хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="18697-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="18697-135">Новое хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="18697-135">New key vault</span></span>

<span data-ttu-id="18697-136">Выполняется Включение soft-delete для нового хранилища ключей во время создания, добавив флаг enable soft-delete hello tooyour создать команду.</span><span class="sxs-lookup"><span data-stu-id="18697-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="18697-137">Проверка включения обратимого удаления</span><span class="sxs-lookup"><span data-stu-id="18697-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="18697-138">tooverify с soft-delete включено, в хранилище ключей выполнения hello *получить* команды и найдите hello, «Мягкое удалить включен?»</span><span class="sxs-lookup"><span data-stu-id="18697-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="18697-139">и его значение (true или false).</span><span class="sxs-lookup"><span data-stu-id="18697-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="18697-140">Удаление хранилища ключей, защищенного с помощью обратимого удаления</span><span class="sxs-lookup"><span data-stu-id="18697-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="18697-141">Hello команда toodelete (или удалить) хранилища ключей остается hello подобны, но изменения его поведения в зависимости от того, включена ли soft-delete или нет.</span><span class="sxs-lookup"><span data-stu-id="18697-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="18697-142">При выполнении предыдущей команды hello для хранилища ключей, у которого нет soft-delete включено будут окончательно удалены этому хранилищу ключей и все ее содержимое без параметров для восстановления.</span><span class="sxs-lookup"><span data-stu-id="18697-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="18697-143">Как обратимое удаление защищает хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="18697-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="18697-144">Если обратимое удаление включено:</span><span class="sxs-lookup"><span data-stu-id="18697-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="18697-145">При удалении хранилища ключей, удаляется из соответствующей группы ресурсов и поместить в зарезервированному пространству имен, которое можно только связанные с расположением hello, где он был создан.</span><span class="sxs-lookup"><span data-stu-id="18697-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="18697-146">Объекты в удаленный ключ хранилища, таких как ключи, секреты и сертификатов, недоступен и остаются, а их содержащего хранилища ключей находится в состоянии hello удален.</span><span class="sxs-lookup"><span data-stu-id="18697-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="18697-147">Hello DNS-имя для хранилища ключей в удаленном состоянии сохраняется, поэтому не удается создать новое хранилище ключей с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="18697-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="18697-148">Можно просмотреть хранилищ ключей удаленном состоянии, связанные с подпиской, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="18697-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

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

<span data-ttu-id="18697-149">Hello *идентификатор ресурса* в hello вывода относится toohello исходный идентификатор ресурса хранилища.</span><span class="sxs-lookup"><span data-stu-id="18697-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="18697-150">Так как это хранилище ключей теперь находится в удаленном состоянии, ресурс с таким идентификатором ресурса не существует.</span><span class="sxs-lookup"><span data-stu-id="18697-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="18697-151">Hello *идентификатор* поле может быть ресурсов hello tooidentify используется при восстановлении или удаления.</span><span class="sxs-lookup"><span data-stu-id="18697-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="18697-152">Hello *запланированные даты очистки* поле указывает, когда хранилище hello будут окончательно удалены (удаление), если действие не выполняется для этого удаленного хранилища.</span><span class="sxs-lookup"><span data-stu-id="18697-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="18697-153">hello toocalculate периода, который применяется для хранения по умолчанию Hello *запланированные даты очистки*, составляет 90 дней.</span><span class="sxs-lookup"><span data-stu-id="18697-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="18697-154">Восстановление хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="18697-154">Recovering a key vault</span></span>

<span data-ttu-id="18697-155">toorecover хранилища ключей, необходимо указать имя хранилища ключей toospecify hello, группу ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="18697-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="18697-156">Примечание hello расположение и hello группа ресурсов hello удалить хранилище ключей, так как необходимые для процесса восстановления хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="18697-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="18697-157">При восстановлении хранилища ключей hello результатом является новый ресурс с идентификатором hello хранилища ключей исходного ресурса.</span><span class="sxs-lookup"><span data-stu-id="18697-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="18697-158">При удалении группы ресурсов hello которых было hello хранилища ключей, перед восстановлением hello хранилища ключей должны создаваться новую группу ресурсов с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="18697-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="18697-159">Объекты хранилища ключей и обратимое удаление</span><span class="sxs-lookup"><span data-stu-id="18697-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="18697-160">Ниже описывается удаление ключа ContosoFirstKey в хранилище ключей ContosoVault, в котором включено обратимое удаление.</span><span class="sxs-lookup"><span data-stu-id="18697-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="18697-161">Если в хранилище ключей включено обратимое удаление, то удаленный ключ отображается как удаленный, за исключением случаев, когда вы явным образом выводите список удаленных ключей или извлекаете их.</span><span class="sxs-lookup"><span data-stu-id="18697-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="18697-162">За исключением перечислении удаленный ключ, он или очистка его не удастся большинства операций по ключу в состоянии hello удален.</span><span class="sxs-lookup"><span data-stu-id="18697-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="18697-163">Например toorequest toolist удалены ключей в хранилище ключей, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="18697-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="18697-164">Переходное состояние</span><span class="sxs-lookup"><span data-stu-id="18697-164">Transition state</span></span> 

<span data-ttu-id="18697-165">При удалении ключа в хранилище ключей с soft-delete включено займет несколько секунд, чтобы переход toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="18697-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="18697-166">Во время это переходное состояние может показаться, что разделу hello не в состоянии active hello или удалить hello.</span><span class="sxs-lookup"><span data-stu-id="18697-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="18697-167">Эта команда выведет список всех удаленных ключей в хранилище ключей ContosoVault.</span><span class="sxs-lookup"><span data-stu-id="18697-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="18697-168">Использование обратимого удаления с объектами хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="18697-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="18697-169">Точно так же, как и в хранилищах ключей, удаленный ключ, секрет или сертификат останется в состоянии удаления для копирования too90 дней, если не восстановить ее или очистить его.</span><span class="sxs-lookup"><span data-stu-id="18697-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="18697-170">ключей</span><span class="sxs-lookup"><span data-stu-id="18697-170">Keys</span></span>

<span data-ttu-id="18697-171">toorecover удаленный ключ:</span><span class="sxs-lookup"><span data-stu-id="18697-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="18697-172">toopermanently удалить раздел:</span><span class="sxs-lookup"><span data-stu-id="18697-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="18697-173">Очистка ключа приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="18697-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="18697-174">Hello **восстановить** и **очистки** действия имеют свои собственные разрешения, связанные политики доступа хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="18697-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="18697-175">Для пользователя или службы основной toobe может tooexecute **восстановить** или **очистки** действия, они должны иметь hello соответствующие разрешения для этого объекта (ключа или секрета) в политике доступа hello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="18697-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="18697-176">По умолчанию hello **очистки** разрешение не добавляется в политику доступа tooa хранилища ключей при hello «all» ярлык — используется toogrant все tooa пользовательские разрешения.</span><span class="sxs-lookup"><span data-stu-id="18697-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="18697-177">Необходимо явно предоставить разрешение на **очистку**.</span><span class="sxs-lookup"><span data-stu-id="18697-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="18697-178">Здравствуйте, например, следующая команда предоставляет user@contoso.com tooperform разрешение несколько операции с ключами в *ContosoVault* включая **очистки**.</span><span class="sxs-lookup"><span data-stu-id="18697-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="18697-179">Настройка политики доступа хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="18697-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="18697-180">Если у вас есть хранилище ключей, в котором только что было включено обратимое удаление, то у вас может не быть разрешений на **восстановление** и **очистку**.</span><span class="sxs-lookup"><span data-stu-id="18697-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="18697-181">Секреты</span><span class="sxs-lookup"><span data-stu-id="18697-181">Secrets</span></span>

<span data-ttu-id="18697-182">Как и в случае ключей, для операций с секретами в хранилище ключей используются собственные команды.</span><span class="sxs-lookup"><span data-stu-id="18697-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="18697-183">Следующие, — это hello команды для удаления, список, восстановление и очистка секретные данные.</span><span class="sxs-lookup"><span data-stu-id="18697-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="18697-184">Удаление секрета SQLPassword.</span><span class="sxs-lookup"><span data-stu-id="18697-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="18697-185">Вывод списка всех удаленных секретов в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="18697-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="18697-186">Восстановите секрет в состоянии hello удалены:</span><span class="sxs-lookup"><span data-stu-id="18697-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="18697-187">Очистка секрета в удаленном состоянии.</span><span class="sxs-lookup"><span data-stu-id="18697-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="18697-188">Очистка секрета приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="18697-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="18697-189">Очистка и хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="18697-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="18697-190">Объекты хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="18697-190">Key vault objects</span></span>

<span data-ttu-id="18697-191">Очистка ключа, секрета или сертификата приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="18697-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="18697-192">хранилище ключей Hello, содержит объект удален hello Однако останутся без изменений, как и другие объекты в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="18697-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="18697-193">Хранилища ключей в роли контейнеров</span><span class="sxs-lookup"><span data-stu-id="18697-193">Key vaults as containers</span></span>
<span data-ttu-id="18697-194">При очистке хранилища ключей все его содержимое, включая ключи, секреты и сертификаты, удаляется без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="18697-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="18697-195">toopurge хранилища ключей, использовать hello `Remove-AzureRmKeyVault` команду с параметром hello `-InRemovedState` , указав расположение hello hello удалить хранилище ключей с hello `-Location location` аргумент.</span><span class="sxs-lookup"><span data-stu-id="18697-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="18697-196">Можно найти расположение hello удаленного хранилища с помощью команды hello `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="18697-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="18697-197">Очистка хранилища ключей приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="18697-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="18697-198">Необходимые разрешения на очистку</span><span class="sxs-lookup"><span data-stu-id="18697-198">Purge permissions required</span></span>
- <span data-ttu-id="18697-199">toopurge удаленные хранилища ключей, таким образом, что хранилище hello и все ее содержимое, окончательно удаляются, hello пользователь должен tooperform разрешение RBAC *Microsoft.KeyVault/locations/deletedVaults/purge/action* операции.</span><span class="sxs-lookup"><span data-stu-id="18697-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="18697-200">ключ toolist hello удален, хранилище hello пользователь должен tooperform разрешение RBAC *Microsoft.KeyVault/deletedVaults/read* разрешение.</span><span class="sxs-lookup"><span data-stu-id="18697-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="18697-201">По умолчанию администратор подписки имеет эти разрешения.</span><span class="sxs-lookup"><span data-stu-id="18697-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="18697-202">Очистка по расписанию</span><span class="sxs-lookup"><span data-stu-id="18697-202">Scheduled purge</span></span>

<span data-ttu-id="18697-203">Перечисление объектов удаленного хранилища ключей показывает во время toobe schedled, удаленные с хранилищем ключей.</span><span class="sxs-lookup"><span data-stu-id="18697-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="18697-204">Hello *запланированные даты очистки* поле указывает, когда объект хранилища ключей будут окончательно удалены, если никакие действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="18697-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="18697-205">По умолчанию срок хранения hello объекта удаленного хранилища ключей составляет 90 дней.</span><span class="sxs-lookup"><span data-stu-id="18697-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="18697-206">После очистки объекта хранилища, активированной значением его поля *Scheduled Purge Date* (Запланированная дата очистки), этот объект будет окончательно удален.</span><span class="sxs-lookup"><span data-stu-id="18697-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="18697-207">Восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="18697-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="18697-208">Другие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="18697-208">Other resources</span></span>

- <span data-ttu-id="18697-209">Обзор функции обратимого удаления Key Vault см. в разделе [Общие сведения об обратимом удалении в Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="18697-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="18697-210">Общие сведения об использовании Azure Key Vault см. в разделе [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="18697-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

