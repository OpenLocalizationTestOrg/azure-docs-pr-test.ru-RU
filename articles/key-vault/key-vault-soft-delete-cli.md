---
ms.assetid: 
title: "Хранилище ключей aaaAzure — как мягкий toouse удалить с CLI"
description: "Примеры использования обратимого удаления с фрагментами кода для интерфейса командной строки."
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="fb8b2-103">Как toouse хранилище ключей soft-delete с CLI</span><span class="sxs-lookup"><span data-stu-id="fb8b2-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="fb8b2-104">Функция обратимого удаления в Azure Key Vault позволяет восстанавливать удаленные хранилища и объекты хранилищ.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="fb8b2-105">В частности адреса soft-delete hello следующие сценарии:</span><span class="sxs-lookup"><span data-stu-id="fb8b2-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="fb8b2-106">Поддержка восстанавливаемого удаления хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="fb8b2-107">Поддержка восстанавливаемого удаления объектов хранилища ключей (например, ключей, секретов и сертификатов).</span><span class="sxs-lookup"><span data-stu-id="fb8b2-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb8b2-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fb8b2-108">Prerequisites</span></span>

- <span data-ttu-id="fb8b2-109">Azure CLI 2.0. Если в вашей среде этот инструмент не установлен, ознакомьтесь с разделом [Управление Key Vault с помощью интерфейса командной строки 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="fb8b2-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="fb8b2-110">Дополнительная информация об использовании интерфейса командной строки с Key Vault приведена в [справочнике по Azure CLI 2.0 для Key Vault](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="fb8b2-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="fb8b2-111">Необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="fb8b2-111">Required permissions</span></span>

<span data-ttu-id="fb8b2-112">Операции Key Vault контролируются отдельно, посредством разрешений управления доступом на основе ролей (RBAC). Это осуществляется следующим образом.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="fb8b2-113">Операция</span><span class="sxs-lookup"><span data-stu-id="fb8b2-113">Operation</span></span> | <span data-ttu-id="fb8b2-114">Описание</span><span class="sxs-lookup"><span data-stu-id="fb8b2-114">Description</span></span> | <span data-ttu-id="fb8b2-115">Разрешение пользователя</span><span class="sxs-lookup"><span data-stu-id="fb8b2-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="fb8b2-116">список</span><span class="sxs-lookup"><span data-stu-id="fb8b2-116">List</span></span>|<span data-ttu-id="fb8b2-117">Выводит список удаленных хранилищ ключей.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="fb8b2-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="fb8b2-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="fb8b2-119">Recover</span><span class="sxs-lookup"><span data-stu-id="fb8b2-119">Recover</span></span>|<span data-ttu-id="fb8b2-120">Восстанавливает удаленное хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="fb8b2-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="fb8b2-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="fb8b2-122">Purge</span><span class="sxs-lookup"><span data-stu-id="fb8b2-122">Purge</span></span>|<span data-ttu-id="fb8b2-123">Окончательно удаляет удаленное хранилище ключей и все его содержимое.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="fb8b2-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="fb8b2-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="fb8b2-125">Дополнительные сведения о разрешениях и управлении доступом см. в разделе [Защита хранилища ключей](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="fb8b2-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="fb8b2-126">Включение обратимого удаления</span><span class="sxs-lookup"><span data-stu-id="fb8b2-126">Enabling soft-delete</span></span>

<span data-ttu-id="fb8b2-127">возможности toorecover toobe удаленные хранилища ключей или объектов, хранящихся в ключе хранилище, необходимо сначала включить soft-delete для этого хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="fb8b2-128">Существующее хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-128">Existing key vault</span></span>

<span data-ttu-id="fb8b2-129">Включите обратимое удаление для существующего хранилища ключей ContosoVault следующим образом.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="fb8b2-130">В настоящее время необходимые записи toouse диспетчера ресурсов Azure ресурсов обработки toodirectly hello *enableSoftDelete* toohello свойство ресурса хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="fb8b2-131">Новое хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-131">New key vault</span></span>

<span data-ttu-id="fb8b2-132">Выполняется Включение soft-delete для нового хранилища ключей во время создания, добавив флаг enable soft-delete hello tooyour создать команду.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="fb8b2-133">Проверка включения обратимого удаления</span><span class="sxs-lookup"><span data-stu-id="fb8b2-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="fb8b2-134">tooverify с soft-delete включено, в хранилище ключей выполнения hello *Показать* команды и найдите hello, «Мягкое удалить включен?»</span><span class="sxs-lookup"><span data-stu-id="fb8b2-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="fb8b2-135">и его значение (true или false).</span><span class="sxs-lookup"><span data-stu-id="fb8b2-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="fb8b2-136">Удаление хранилища ключей, защищенного с помощью обратимого удаления</span><span class="sxs-lookup"><span data-stu-id="fb8b2-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="fb8b2-137">Hello команда toodelete (или удалить) хранилища ключей остается hello подобны, но изменения его поведения в зависимости от того, включена ли soft-delete или нет.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="fb8b2-138">При выполнении предыдущей команды hello для хранилища ключей, у которого нет soft-delete включено будут окончательно удалены этому хранилищу ключей и все ее содержимое без параметров для восстановления.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="fb8b2-139">Как обратимое удаление защищает хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="fb8b2-140">Если обратимое удаление включено:</span><span class="sxs-lookup"><span data-stu-id="fb8b2-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="fb8b2-141">При удалении хранилища ключей, удаляется из соответствующей группы ресурсов и поместить в зарезервированному пространству имен, которое можно только связанные с расположением hello, где он был создан.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="fb8b2-142">Объекты в удаленный ключ хранилища, таких как ключи, секреты и сертификатов, недоступен и остаются, а их содержащего хранилища ключей находится в состоянии hello удален.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="fb8b2-143">Hello DNS-имя для хранилища ключей в удаленном состоянии сохраняется, поэтому не удается создать новое хранилище ключей с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="fb8b2-144">Можно просмотреть хранилищ ключей удаленном состоянии, связанные с подпиской, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fb8b2-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="fb8b2-145">Hello *идентификатор ресурса* в hello вывода относится toohello исходный идентификатор ресурса хранилища.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="fb8b2-146">Так как это хранилище ключей теперь находится в удаленном состоянии, ресурс с таким идентификатором ресурса не существует.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="fb8b2-147">Hello *идентификатор* поле может быть ресурсов hello tooidentify используется при восстановлении или удаления.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="fb8b2-148">Hello *запланированные даты очистки* поле указывает, когда хранилище hello будут окончательно удалены (удаление), если действие не выполняется для этого удаленного хранилища.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="fb8b2-149">hello toocalculate периода, который применяется для хранения по умолчанию Hello *запланированные даты очистки*, составляет 90 дней.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="fb8b2-150">Восстановление хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-150">Recovering a key vault</span></span>

<span data-ttu-id="fb8b2-151">toorecover хранилища ключей, необходимо указать имя хранилища ключей toospecify hello, группу ресурсов и расположение.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="fb8b2-152">Примечание hello расположение и hello группа ресурсов hello удалить хранилище ключей, так как необходимые для процесса восстановления хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="fb8b2-153">При восстановлении хранилища ключей hello результатом является новый ресурс с идентификатором hello хранилища ключей исходного ресурса.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="fb8b2-154">При удалении группы ресурсов hello которых было hello хранилища ключей, перед восстановлением hello хранилища ключей должны создаваться новую группу ресурсов с таким же именем.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="fb8b2-155">Объекты хранилища ключей и обратимое удаление</span><span class="sxs-lookup"><span data-stu-id="fb8b2-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="fb8b2-156">Ниже описывается удаление ключа ContosoFirstKey в хранилище ключей ContosoVault, в котором включено обратимое удаление.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="fb8b2-157">Если в хранилище ключей включено обратимое удаление, то удаленный ключ отображается как удаленный, за исключением случаев, когда вы явным образом выводите список удаленных ключей или извлекаете их.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="fb8b2-158">За исключением перечислении удаленный ключ, он или очистка его не удастся большинства операций по ключу в состоянии hello удален.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="fb8b2-159">Например toorequest toolist удалены ключей в хранилище ключей, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fb8b2-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="fb8b2-160">Переходное состояние</span><span class="sxs-lookup"><span data-stu-id="fb8b2-160">Transition state</span></span> 

<span data-ttu-id="fb8b2-161">При удалении ключа в хранилище ключей с soft-delete включено займет несколько секунд, чтобы переход toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="fb8b2-162">Во время это переходное состояние может показаться, что разделу hello не в состоянии active hello или удалить hello.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="fb8b2-163">Эта команда выведет список всех удаленных ключей в хранилище ключей ContosoVault.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="fb8b2-164">Использование обратимого удаления с объектами хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="fb8b2-165">Точно так же, как и в хранилищах ключей, удаленный ключ, секрет или сертификат останется в состоянии удаления для копирования too90 дней, если не восстановить ее или очистить его.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="fb8b2-166">ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-166">Keys</span></span>

<span data-ttu-id="fb8b2-167">toorecover удаленный ключ:</span><span class="sxs-lookup"><span data-stu-id="fb8b2-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="fb8b2-168">toopermanently удалить раздел:</span><span class="sxs-lookup"><span data-stu-id="fb8b2-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="fb8b2-169">Очистка ключа приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="fb8b2-170">Hello **восстановить** и **очистки** действия имеют свои собственные разрешения, связанные политики доступа хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="fb8b2-171">Для пользователя или службы основной toobe может tooexecute **восстановить** или **очистки** действия, они должны иметь hello соответствующие разрешения для этого объекта (ключа или секрета) в политике доступа hello хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="fb8b2-172">По умолчанию hello **очистки** разрешение не добавляется в политику доступа tooa хранилища ключей при hello «all» ярлык — используется toogrant все tooa пользовательские разрешения.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="fb8b2-173">Необходимо явно предоставить разрешение на **очистку**.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="fb8b2-174">Здравствуйте, например, следующая команда предоставляет user@contoso.com tooperform разрешение несколько операции с ключами в *ContosoVault* включая **очистки**.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="fb8b2-175">Настройка политики доступа хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="fb8b2-176">Если у вас есть хранилище ключей, в котором только что было включено обратимое удаление, то у вас может не быть разрешений на **восстановление** и **очистку**.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="fb8b2-177">Секреты</span><span class="sxs-lookup"><span data-stu-id="fb8b2-177">Secrets</span></span>

<span data-ttu-id="fb8b2-178">Как и в случае ключей, для операций с секретами в хранилище ключей используются собственные команды.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="fb8b2-179">Следующие, — это hello команды для удаления, список, восстановление и очистка секретные данные.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="fb8b2-180">Удаление секрета SQLPassword.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="fb8b2-181">Вывод списка всех удаленных секретов в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="fb8b2-182">Восстановите секрет в состоянии hello удалены:</span><span class="sxs-lookup"><span data-stu-id="fb8b2-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="fb8b2-183">Очистка секрета в удаленном состоянии.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="fb8b2-184">Очистка секрета приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="fb8b2-185">Очистка и хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="fb8b2-186">Объекты хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="fb8b2-186">Key vault objects</span></span>

<span data-ttu-id="fb8b2-187">Очистка ключа, секрета или сертификата приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="fb8b2-188">хранилище ключей Hello, содержит объект удален hello Однако останутся без изменений, как и другие объекты в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="fb8b2-189">Хранилища ключей в роли контейнеров</span><span class="sxs-lookup"><span data-stu-id="fb8b2-189">Key vaults as containers</span></span>
<span data-ttu-id="fb8b2-190">При очистке хранилища ключей все его содержимое, включая ключи, секреты и сертификаты, удаляется без возможности восстановления.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="fb8b2-191">toopurge хранилища ключей, использовать hello `az keyvault purge` команды.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="fb8b2-192">Можно найти расположение hello ключа хранилища с удаленных вашей подписки с помощью команды hello `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="fb8b2-193">Очистка хранилища ключей приведет к его окончательному удалению, то есть восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="fb8b2-194">Необходимые разрешения на очистку</span><span class="sxs-lookup"><span data-stu-id="fb8b2-194">Purge permissions required</span></span>
- <span data-ttu-id="fb8b2-195">toopurge удаленные хранилища ключей, таким образом, что хранилище hello и все ее содержимое, окончательно удаляются, hello пользователь должен tooperform разрешение RBAC *Microsoft.KeyVault/locations/deletedVaults/purge/action* операции.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="fb8b2-196">ключ toolist hello удален, хранилище hello пользователь должен tooperform разрешение RBAC *Microsoft.KeyVault/deletedVaults/read* разрешение.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="fb8b2-197">По умолчанию администратор подписки имеет эти разрешения.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="fb8b2-198">Очистка по расписанию</span><span class="sxs-lookup"><span data-stu-id="fb8b2-198">Scheduled purge</span></span>

<span data-ttu-id="fb8b2-199">Перечисление объектов удаленного хранилища ключей показывает во время toobe schedled, удаленные с хранилищем ключей.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="fb8b2-200">Hello *запланированные даты очистки* поле указывает, когда объект хранилища ключей будут окончательно удалены, если никакие действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="fb8b2-201">По умолчанию срок хранения hello объекта удаленного хранилища ключей составляет 90 дней.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="fb8b2-202">После очистки объекта хранилища, активированной значением его поля *Scheduled Purge Date* (Запланированная дата очистки), этот объект будет окончательно удален.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="fb8b2-203">Восстановить его будет невозможно.</span><span class="sxs-lookup"><span data-stu-id="fb8b2-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="fb8b2-204">Другие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="fb8b2-204">Other resources</span></span>

- <span data-ttu-id="fb8b2-205">Обзор функции обратимого удаления Key Vault см. в разделе [Общие сведения об обратимом удалении в Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="fb8b2-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="fb8b2-206">Общие сведения об использовании Azure Key Vault см. в разделе [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb8b2-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

