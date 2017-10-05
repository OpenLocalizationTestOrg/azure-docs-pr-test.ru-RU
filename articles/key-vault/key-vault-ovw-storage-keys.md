---
ms.assetid: 
title: "Ключи учетной записи хранения Azure Key Vault"
description: "Ключи учетной записи хранения обеспечивают простую интеграцию между Azure Key Vault и доступом по ключу к учетной записи хранения Azure."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: 3148088c88236c64e089fd25c98eb8ac7cdcbfea
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="31e8d-103">Ключи учетной записи хранения Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="31e8d-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="31e8d-104">До появления ключей учетной записи хранения Azure Key Vault разработчикам приходилось управлять ключами учетной записи хранения Azure (ASA) и сменять их вручную или с помощью внешних средств автоматизации.</span><span class="sxs-lookup"><span data-stu-id="31e8d-104">Before Azure Key Vault Storage Account Keys, developers had to manage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="31e8d-105">Сейчас ключи учетной записи хранения Key Vault реализованы в качестве [секретов Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) для проверки подлинности с помощью учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="31e8d-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="31e8d-106">Функция ключа ASA управляет сменой секретов и устраняет необходимость прямого контакта с ключом ASA за счет использования подписанных URL-адресов (SAS).</span><span class="sxs-lookup"><span data-stu-id="31e8d-106">The ASA key feature manages secret rotation for you and removes the need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="31e8d-107">Дополнительные сведения об учетных записях хранения Azure см. в статье [Об учетных записях хранения Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="31e8d-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="31e8d-108">Поддержка интерфейсов</span><span class="sxs-lookup"><span data-stu-id="31e8d-108">Supporting interfaces</span></span>

<span data-ttu-id="31e8d-109">Функция ключей учетной записи хранения Azure изначально доступна через интерфейсы REST, .NET, C# и PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31e8d-109">The Azure Storage Account keys feature is initially available through the REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="31e8d-110">Дополнительные сведения см. в разделе [Документация по хранилищу ключей](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="31e8d-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="31e8d-111">Поведение ключей учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="31e8d-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="31e8d-112">Чем управляет Key Vault</span><span class="sxs-lookup"><span data-stu-id="31e8d-112">What Key Vault manages</span></span>

<span data-ttu-id="31e8d-113">Служба Key Vault выполняет несколько внутренних функций управления от вашего имени, если вы используете ключи учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="31e8d-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="31e8d-114">Служба хранилища Azure Key Vault управляет ключами учетной записи хранения Azure (ASA).</span><span class="sxs-lookup"><span data-stu-id="31e8d-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="31e8d-115">На внутреннем уровне Azure Key Vault может выводить список (синхронизировать) ключи с помощью учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="31e8d-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="31e8d-116">Azure Key Vault периодически повторно создает (сменяет) ключи.</span><span class="sxs-lookup"><span data-stu-id="31e8d-116">Azure Key Vault regenerates (rotates) the keys periodically.</span></span> 
    - <span data-ttu-id="31e8d-117">Значения ключей никогда не возвращаются в ответе вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="31e8d-117">Key values are never returned in response to caller.</span></span> 
    - <span data-ttu-id="31e8d-118">Azure Key Vault управляет ключами как учетных записей хранения, так и классических учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="31e8d-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="31e8d-119">Azure Key Vault позволяет владельцу хранилища или объекта создавать определения SAS (учетной записи или службы).</span><span class="sxs-lookup"><span data-stu-id="31e8d-119">Azure Key Vault allows you, the vault/object owner, to create SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="31e8d-120">Значение SAS, созданное с помощью определения SAS, возвращается в качестве секрета через путь универсального кода ресурса (URI) REST.</span><span class="sxs-lookup"><span data-stu-id="31e8d-120">The SAS value, created using SAS definition, is returned as a secret via the REST URI path.</span></span> <span data-ttu-id="31e8d-121">Дополнительные сведения см. в статье [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations) (Операции с учетными записями хранения Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="31e8d-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="31e8d-122">Рекомендации по именованию</span><span class="sxs-lookup"><span data-stu-id="31e8d-122">Naming guidance</span></span>

<span data-ttu-id="31e8d-123">Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и строчных букв.</span><span class="sxs-lookup"><span data-stu-id="31e8d-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="31e8d-124">Имя определения SAS должно быть 1–102 символа в длину и содержать только символы 0–9, a–z, A–Z.</span><span class="sxs-lookup"><span data-stu-id="31e8d-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="31e8d-125">Возможности для разработчика</span><span class="sxs-lookup"><span data-stu-id="31e8d-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="31e8d-126">До появления ключей Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="31e8d-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="31e8d-127">Разработчикам приходилось применять следующие методы, чтобы получить доступ к хранилищу Azure с помощью ключа учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="31e8d-127">Developers used to need to do the following practices with a storage account key to get access to Azure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="31e8d-128">После появления ключей Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="31e8d-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure to set storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command to get Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using the SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and the Blob storage endpoint to create a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about to expire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="31e8d-129">Рекомендации разработчикам</span><span class="sxs-lookup"><span data-stu-id="31e8d-129">Developer best practices</span></span> 

- <span data-ttu-id="31e8d-130">Разрешите только Key Vault управлять ключами ASA.</span><span class="sxs-lookup"><span data-stu-id="31e8d-130">Only allow Key Vault to manage your ASA keys.</span></span> <span data-ttu-id="31e8d-131">Не пытайтесь управлять ими самостоятельно. Это повлияет на процессы Key Vault.</span><span class="sxs-lookup"><span data-stu-id="31e8d-131">Do not attempt to manage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="31e8d-132">Ключи ASA не должны управляться более чем одним объектом Key Vault.</span><span class="sxs-lookup"><span data-stu-id="31e8d-132">Do not allow ASA keys to be managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="31e8d-133">Если необходимо вручную повторно создать ключи ASA, рекомендуем делать это через Key Vault.</span><span class="sxs-lookup"><span data-stu-id="31e8d-133">If you need to manually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="31e8d-134">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="31e8d-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="31e8d-135">Настройка разрешений для управления доступом на основе ролей (RBAC)</span><span class="sxs-lookup"><span data-stu-id="31e8d-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="31e8d-136">Для Key Vault необходимы разрешения для *вывода списка* и *повторного создания* ключей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="31e8d-136">Key Vault needs permissions to *list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="31e8d-137">Настройте эти разрешения, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="31e8d-137">Set up these permissions using the following steps:</span></span>

- <span data-ttu-id="31e8d-138">Получите ObjectId хранилища Key Vault:</span><span class="sxs-lookup"><span data-stu-id="31e8d-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="31e8d-139">Присвойте идентификатору Azure Key Vault роль оператора учетной записи хранения:</span><span class="sxs-lookup"><span data-stu-id="31e8d-139">Assign Storage Key Operator role to Azure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="31e8d-140">Для классической учетной записи задайте для параметра роли значение *Classic Storage Account Key Operator Service Role* (Роль службы оператора ключей классических учетных записей хранения).</span><span class="sxs-lookup"><span data-stu-id="31e8d-140">For a classic account type, set the role parameter to *"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="31e8d-141">Подключение учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="31e8d-141">Storage account onboarding</span></span> 

<span data-ttu-id="31e8d-142">Пример: владелец объекта Key Vault добавляет объект учетной записи хранилища в Azure Key Vault, чтобы подключить учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="31e8d-142">Example: As a Key Vault object owner you add a storage account object to your Azure Key Vault to onboard a storage account.</span></span>

<span data-ttu-id="31e8d-143">Во время подключения Key Vault проверяет, что удостоверение подключаемой учетной записи имеет разрешения на *перечисление* и *повторное создание* ключей хранилища.</span><span class="sxs-lookup"><span data-stu-id="31e8d-143">During onboarding, Key Vault needs to verify that the identity of the onboarding account has permissions to *list* and to *regenerate* storage keys.</span></span> <span data-ttu-id="31e8d-144">Чтобы проверить эти разрешения, Key Vault получает токен OBO (от имени) от службы аутентификации, указывает Azure Resource Manager в качестве целевой аудитории, а затем обращается к службе хранилища Azure для *получения списка*.</span><span class="sxs-lookup"><span data-stu-id="31e8d-144">In order to verify these permissions, Key Vault gets an OBO (On Behalf Of) token from the authentication service, audience set to Azure Resource Manager, and makes a *list* key call to the Azure Storage service.</span></span> <span data-ttu-id="31e8d-145">Если *вызов списка* завершается неудачно, создание объекта Key Vault завершается ошибкой с кодом состояния HTTP *Запрещено*.</span><span class="sxs-lookup"><span data-stu-id="31e8d-145">If the *list* call fails, the Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="31e8d-146">Ключи, указанные таким способом, кэшируются с помощью хранилища сущностей хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="31e8d-146">The keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="31e8d-147">Key Vault необходимо убедиться, что идентификатор имеет разрешения на *повторное создание*, прежде чем предоставить ему права на повторное создание ключей.</span><span class="sxs-lookup"><span data-stu-id="31e8d-147">Key Vault must verify that the identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="31e8d-148">Чтобы убедиться, что идентификатор (через токен OBO), а также основной идентификатор Key Vault имеют следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="31e8d-148">To verify that the identity, via OBO token, as well as the Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="31e8d-149">Key Vault выводит список разрешений RBAC в ресурсе учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="31e8d-149">Key Vault lists RBAC permissions on the storage account resource.</span></span>
- <span data-ttu-id="31e8d-150">Key Vault проверяет ответ через сопоставление регулярных выражений для определения действий и их отсутствия.</span><span class="sxs-lookup"><span data-stu-id="31e8d-150">Key Vault validates the response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="31e8d-151">Некоторые поддерживаемые примеры вы можете найти в разделе [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault — управляемая система хранения ключей учетных записей).</span><span class="sxs-lookup"><span data-stu-id="31e8d-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="31e8d-152">Если удостоверение не имеет разрешение на *повторное создание* или основное удостоверение Key Vault не имеет разрешение на *перечисление* или *повторное создание*, тогда запрос на подключение завершается ошибкой с соответствующим кодом и сообщением.</span><span class="sxs-lookup"><span data-stu-id="31e8d-152">If the identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then the onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="31e8d-153">Маркер OBO будет работать только при использовании основных, собственных клиентских приложений PowerShell или CLI.</span><span class="sxs-lookup"><span data-stu-id="31e8d-153">The OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="31e8d-154">Другие приложения</span><span class="sxs-lookup"><span data-stu-id="31e8d-154">Other applications</span></span>

- <span data-ttu-id="31e8d-155">Маркеры SAS, созданные с помощью ключей учетной записи хранения Key Vault, предоставляют более точный контроль доступа к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="31e8d-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access to an Azure storage account.</span></span> <span data-ttu-id="31e8d-156">Дополнительные сведения см. в статье [Использование подписанных URL-адресов (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="31e8d-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="31e8d-157">См. также</span><span class="sxs-lookup"><span data-stu-id="31e8d-157">See also</span></span>

- [<span data-ttu-id="31e8d-158">Сведения о ключах, секретах и сертификатах</span><span class="sxs-lookup"><span data-stu-id="31e8d-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="31e8d-159">Официальный блог команды разработчиков Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="31e8d-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
