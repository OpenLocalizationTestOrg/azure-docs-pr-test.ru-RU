---
ms.assetid: 
title: "Как использовать обратимое удаление в Azure Key Vault с помощью интерфейса командной строки"
description: "Примеры использования обратимого удаления с фрагментами кода для интерфейса командной строки."
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 3ee2c5dfb99d734cde25894174466b8e49823c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-cli"></a><span data-ttu-id="f2c4b-103">Как использовать обратимое удаление в Key Vault с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="f2c4b-103">How to use Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="f2c4b-104">Функция обратимого удаления в Azure Key Vault позволяет восстанавливать удаленные хранилища и объекты хранилищ.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="f2c4b-105">В частности, обратимое удаление применяется в следующих сценариях:</span><span class="sxs-lookup"><span data-stu-id="f2c4b-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="f2c4b-106">Поддержка восстанавливаемого удаления хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="f2c4b-107">Поддержка восстанавливаемого удаления объектов хранилища ключей (например, ключей, секретов и сертификатов).</span><span class="sxs-lookup"><span data-stu-id="f2c4b-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2c4b-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f2c4b-108">Prerequisites</span></span>

- <span data-ttu-id="f2c4b-109">Azure CLI 2.0. Если в вашей среде этот инструмент не установлен, ознакомьтесь с разделом [Управление Key Vault с помощью интерфейса командной строки 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="f2c4b-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="f2c4b-110">Дополнительная информация об использовании интерфейса командной строки с Key Vault приведена в [справочнике по Azure CLI 2.0 для Key Vault](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="f2c4b-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="f2c4b-111">Необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="f2c4b-111">Required permissions</span></span>

<span data-ttu-id="f2c4b-112">Операции Key Vault контролируются отдельно, посредством разрешений управления доступом на основе ролей (RBAC). Это осуществляется следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="f2c4b-113">Операция</span><span class="sxs-lookup"><span data-stu-id="f2c4b-113">Operation</span></span> | <span data-ttu-id="f2c4b-114">Описание</span><span class="sxs-lookup"><span data-stu-id="f2c4b-114">Description</span></span> | <span data-ttu-id="f2c4b-115">Разрешение пользователя</span><span class="sxs-lookup"><span data-stu-id="f2c4b-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="f2c4b-116">список</span><span class="sxs-lookup"><span data-stu-id="f2c4b-116">List</span></span>|<span data-ttu-id="f2c4b-117">Выводит список удаленных хранилищ ключей.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="f2c4b-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="f2c4b-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="f2c4b-119">Recover</span><span class="sxs-lookup"><span data-stu-id="f2c4b-119">Recover</span></span>|<span data-ttu-id="f2c4b-120">Восстанавливает удаленное хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="f2c4b-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="f2c4b-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="f2c4b-122">Purge</span><span class="sxs-lookup"><span data-stu-id="f2c4b-122">Purge</span></span>|<span data-ttu-id="f2c4b-123">Окончательно удаляет удаленное хранилище ключей и все его содержимое.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="f2c4b-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="f2c4b-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="f2c4b-125">Дополнительные сведения о разрешениях и управлении доступом см. в разделе [Защита хранилища ключей](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f2c4b-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="f2c4b-126">Включение обратимого удаления</span><span class="sxs-lookup"><span data-stu-id="f2c4b-126">Enabling soft-delete</span></span>

<span data-ttu-id="f2c4b-127">Чтобы иметь возможность восстановить удаленное хранилище ключей или объекты, хранящиеся в хранилище ключей, для него необходимо сначала включить обратимое удаление.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-127">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="f2c4b-128">Существующее хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-128">Existing key vault</span></span>

<span data-ttu-id="f2c4b-129">Включите обратимое удаление для существующего хранилища ключей ContosoVault следующим образом.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="f2c4b-130">В настоящее время необходимо использовать операции с ресурсами Azure Resource Manager, чтобы записать свойство *enableSoftDelete* непосредственно в ресурс Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-130">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="f2c4b-131">Новое хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-131">New key vault</span></span>

<span data-ttu-id="f2c4b-132">Обратимое удаление для нового хранилища ключей включается во время создания путем добавления флага --enable-soft-delete в команду create.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-132">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="f2c4b-133">Проверка включения обратимого удаления</span><span class="sxs-lookup"><span data-stu-id="f2c4b-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="f2c4b-134">Чтобы проверить, включено ли обратимое удаление в хранилище ключей, выполните команду *show* и в выходных данных найдите атрибут "Soft Delete Enabled?"</span><span class="sxs-lookup"><span data-stu-id="f2c4b-134">To verify that a key vault has soft-delete enabled, run the *show* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="f2c4b-135">и его значение (true или false).</span><span class="sxs-lookup"><span data-stu-id="f2c4b-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="f2c4b-136">Удаление хранилища ключей, защищенного с помощью обратимого удаления</span><span class="sxs-lookup"><span data-stu-id="f2c4b-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="f2c4b-137">Команда для удаления хранилища ключей остается прежней, но в зависимости от того, включено ли обратимое удаление, меняется ее поведение.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-137">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="f2c4b-138">Если выполнить предыдущую команду для хранилища ключей, в котором не включено обратимое удаление, оно и его содержимое будут окончательно удалены без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-138">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="f2c4b-139">Как обратимое удаление защищает хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="f2c4b-140">Если обратимое удаление включено:</span><span class="sxs-lookup"><span data-stu-id="f2c4b-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="f2c4b-141">При удалении хранилище ключей удаляется из соответствующей группы ресурсов и помещается в зарезервированное пространство имен, которое связано только с расположением, в котором было создано.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="f2c4b-142">Объекты в удаленном хранилище ключей, такие как ключи, секреты и сертификаты, становятся недоступными и остаются таковыми, пока содержащее их хранилище ключей находится в удаленном состоянии.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="f2c4b-143">DNS-имя хранилища ключей в удаленном состоянии остается зарезервированным, поэтому не удастся создать новое хранилище ключей с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-143">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="f2c4b-144">Чтобы просмотреть хранилища ключей в удаленном состоянии, связанные с вашей подпиской, можно выполнить следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-144">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="f2c4b-145">*Идентификатор ресурса* в выходных данных — это исходный идентификатор ресурса данного хранилища.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-145">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="f2c4b-146">Так как это хранилище ключей теперь находится в удаленном состоянии, ресурс с таким идентификатором ресурса не существует.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="f2c4b-147">Поле *Id* (Идентификатор) поле может использоваться для определения ресурса при восстановлении или очистке.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-147">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="f2c4b-148">Поле *Scheduled Purge Date* (Запланированная дата очистки) указывает, когда хранилище будет окончательно удалено, если с ним не будет выполнено какое-либо действие.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-148">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="f2c4b-149">Срок хранения по умолчанию, используемый для вычисления *запланированной даты очистки*, составляет 90 дней.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-149">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="f2c4b-150">Восстановление хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-150">Recovering a key vault</span></span>

<span data-ttu-id="f2c4b-151">Чтобы восстановить хранилище ключей, необходимо указать его имя, группу ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-151">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="f2c4b-152">Запишите расположение и группу ресурсов удаленного хранилища ключей, так как их необходимо знать, чтобы осуществить восстановление.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-152">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="f2c4b-153">После восстановления хранилища ключей вы получите новый ресурс с исходным идентификатором ресурса хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-153">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="f2c4b-154">Если группа ресурсов, в которой находилось хранилище ключей, удалена, то перед восстановлением хранилища ключей нужно создать новую группу ресурсов с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-154">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="f2c4b-155">Объекты хранилища ключей и обратимое удаление</span><span class="sxs-lookup"><span data-stu-id="f2c4b-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="f2c4b-156">Ниже описывается удаление ключа ContosoFirstKey в хранилище ключей ContosoVault, в котором включено обратимое удаление.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="f2c4b-157">Если в хранилище ключей включено обратимое удаление, то удаленный ключ отображается как удаленный, за исключением случаев, когда вы явным образом выводите список удаленных ключей или извлекаете их.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="f2c4b-158">Большинство операций с ключом в удаленном состоянии завершится сбоем, кроме вывода списка удаленных ключей, восстановления этого ключа или его удаления.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-158">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="f2c4b-159">Например, чтобы запросить список удаленных ключей в хранилище ключей, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-159">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="f2c4b-160">Переходное состояние</span><span class="sxs-lookup"><span data-stu-id="f2c4b-160">Transition state</span></span> 

<span data-ttu-id="f2c4b-161">Удаление ключа в хранилище ключей, в котором включено обратимое удаление, может занять несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="f2c4b-162">Во время этого переходного состояния может создаться впечатление, что ключ не находится ни в активном, ни в удаленном состоянии.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-162">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="f2c4b-163">Эта команда выведет список всех удаленных ключей в хранилище ключей ContosoVault.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="f2c4b-164">Использование обратимого удаления с объектами хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="f2c4b-165">Как и хранилища ключей, удаленный ключ, секрет или сертификат останется в удаленном состоянии в течение 90 дней, если его не восстановить или не очистить.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="f2c4b-166">ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-166">Keys</span></span>

<span data-ttu-id="f2c4b-167">Восстановление удаленного ключа.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-167">To recover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="f2c4b-168">Окончательное удаление ключа.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-168">To permanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="f2c4b-169">Очистка ключа приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="f2c4b-170">Для действий **восстановления** и **очистки** в политике доступа хранилища ключей заданы собственные разрешения.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-170">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="f2c4b-171">Чтобы пользователь или субъект-служба могли выполнить **восстановление** или **очистку**, они должны иметь соответствующее разрешение для этого объекта (ключа или секрета) в политике доступа хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-171">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="f2c4b-172">По умолчанию разрешение на **очистку** не добавляется в политику доступа хранилища ключей, если для предоставления всех разрешений пользователю используется параметр "Все".</span><span class="sxs-lookup"><span data-stu-id="f2c4b-172">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="f2c4b-173">Необходимо явно предоставить разрешение на **очистку**.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="f2c4b-174">Например, приведенная ниже команда предоставляет разрешение user@contoso.com на выполнение нескольких операций с ключами в *ContosoVault*, включая **очистку**.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-174">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="f2c4b-175">Настройка политики доступа хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="f2c4b-176">Если у вас есть хранилище ключей, в котором только что было включено обратимое удаление, то у вас может не быть разрешений на **восстановление** и **очистку**.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="f2c4b-177">Секреты</span><span class="sxs-lookup"><span data-stu-id="f2c4b-177">Secrets</span></span>

<span data-ttu-id="f2c4b-178">Как и в случае ключей, для операций с секретами в хранилище ключей используются собственные команды.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="f2c4b-179">Ниже приведены команды для удаления, вывода списка, восстановления и очистки секретов.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-179">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="f2c4b-180">Удаление секрета SQLPassword.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="f2c4b-181">Вывод списка всех удаленных секретов в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="f2c4b-182">Восстановление секрета в удаленном состоянии.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-182">Recover a secret in the deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="f2c4b-183">Очистка секрета в удаленном состоянии.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="f2c4b-184">Очистка секрета приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="f2c4b-185">Очистка и хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="f2c4b-186">Объекты хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="f2c4b-186">Key vault objects</span></span>

<span data-ttu-id="f2c4b-187">Очистка ключа, секрета или сертификата приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="f2c4b-188">Однако содержащее его хранилище ключей останется без изменений, как и другие объекты, хранящиеся в нем.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-188">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="f2c4b-189">Хранилища ключей в роли контейнеров</span><span class="sxs-lookup"><span data-stu-id="f2c4b-189">Key vaults as containers</span></span>
<span data-ttu-id="f2c4b-190">При очистке хранилища ключей все его содержимое, включая ключи, секреты и сертификаты, удаляется без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="f2c4b-191">Для очистки хранилища ключей используйте команду `az keyvault purge`.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-191">To purge a key vault, use the `az keyvault purge` command.</span></span> <span data-ttu-id="f2c4b-192">Найти расположение удаленных хранилищ ключей для своей подписки можно с помощью команды `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-192">You can find the location your subscription's deleted key vaults using the command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="f2c4b-193">Очистка хранилища ключей приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="f2c4b-194">Необходимые разрешения на очистку</span><span class="sxs-lookup"><span data-stu-id="f2c4b-194">Purge permissions required</span></span>
- <span data-ttu-id="f2c4b-195">Чтобы очистить удаленное хранилище ключей, то есть окончательно удалить его вместе со всем содержимым, пользователю нужно разрешение RBAC на выполнение операции *Microsoft.KeyVault/locations/deletedVaults/purge/action*.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-195">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="f2c4b-196">Чтобы вывести список удаленных хранилищ ключей, пользователю нужно разрешение RBAC на выполнение операции *Microsoft.KeyVault/deletedVaults/read*.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-196">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="f2c4b-197">По умолчанию администратор подписки имеет эти разрешения.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="f2c4b-198">Очистка по расписанию</span><span class="sxs-lookup"><span data-stu-id="f2c4b-198">Scheduled purge</span></span>

<span data-ttu-id="f2c4b-199">При выводе списка объектов удаленного хранилища ключей отображается запланированное время их очистки службой Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-199">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="f2c4b-200">Поле *Scheduled Purge Date* (Запланированная дата очистки) указывает, когда объект хранилища ключей будет окончательно удален, если не предпринять какое-либо действие.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-200">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="f2c4b-201">По умолчанию срок хранения объекта удаленного хранилища ключей составляет 90 дней.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-201">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="f2c4b-202">После очистки объекта хранилища, активированной значением его поля *Scheduled Purge Date* (Запланированная дата очистки), этот объект будет окончательно удален.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="f2c4b-203">Восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="f2c4b-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="f2c4b-204">Другие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="f2c4b-204">Other resources</span></span>

- <span data-ttu-id="f2c4b-205">Обзор функции обратимого удаления Key Vault см. в разделе [Общие сведения об обратимом удалении в Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="f2c4b-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="f2c4b-206">Общие сведения об использовании Azure Key Vault см. в разделе [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f2c4b-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

