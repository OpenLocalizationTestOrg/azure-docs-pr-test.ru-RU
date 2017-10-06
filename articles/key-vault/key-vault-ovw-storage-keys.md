---
ms.assetid: 
title: "aaaAzure ключи учетной записи хранилища ключей"
description: "Ключи учетной записи хранения укажите прозрачный интеграцию хранилища ключей Azure и доступ к ключу на основе tooAzure учетной записи хранилища."
ms.topic: article
services: key-vault
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/25/2017
ms.openlocfilehash: becdf97798a08164c48d3a7a14aea6ca54085c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-storage-account-keys"></a><span data-ttu-id="110d9-103">Ключи учетной записи хранения Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="110d9-103">Azure Key Vault Storage Account Keys</span></span>

<span data-ttu-id="110d9-104">Перед ключи учетной записи хранения хранилище ключей Azure разработчики имели toomanage свои собственные ключи учетной записи хранилища Azure (ASA) и повернуть их вручную или с помощью внешних автоматизации.</span><span class="sxs-lookup"><span data-stu-id="110d9-104">Before Azure Key Vault Storage Account Keys, developers had toomanage their own Azure Storage Account (ASA) keys and rotate them manually or through an external automation.</span></span> <span data-ttu-id="110d9-105">Сейчас ключи учетной записи хранения Key Vault реализованы в качестве [секретов Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) для проверки подлинности с помощью учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="110d9-105">Now, Key Vault Storage Account Keys are implemented as [Key Vault secrets](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) for authenticating with an Azure Storage Account.</span></span> 

<span data-ttu-id="110d9-106">ключевой особенностью ASA Hello управляет секретный поворота и удаляет hello потребность прямой связи с ключом ASA путем предоставления общего доступа подписи (SAS) как метод.</span><span class="sxs-lookup"><span data-stu-id="110d9-106">hello ASA key feature manages secret rotation for you and removes hello need for your direct contact with an ASA key by offering Shared Access Signatures (SAS) as a method.</span></span> 

<span data-ttu-id="110d9-107">Дополнительные сведения об учетных записях хранения Azure см. в статье [Об учетных записях хранения Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="110d9-107">For more general information on Azure Storage Accounts, see [About Azure storage accounts](https://docs.microsoft.com/azure/storage/storage-create-storage-account).</span></span>

## <a name="supporting-interfaces"></a><span data-ttu-id="110d9-108">Поддержка интерфейсов</span><span class="sxs-lookup"><span data-stu-id="110d9-108">Supporting interfaces</span></span>

<span data-ttu-id="110d9-109">Hello функция ключи учетной записи хранилища Azure изначально доступна через hello REST, .NET или C# и PowerShell интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="110d9-109">hello Azure Storage Account keys feature is initially available through hello REST, .NET/C# and PowerShell interfaces.</span></span> <span data-ttu-id="110d9-110">Дополнительные сведения см. в разделе [Документация по хранилищу ключей](https://docs.microsoft.com/azure/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="110d9-110">For more information, see [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).</span></span>


## <a name="storage-account-keys-behavior"></a><span data-ttu-id="110d9-111">Поведение ключей учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="110d9-111">Storage account keys behavior</span></span>

### <a name="what-key-vault-manages"></a><span data-ttu-id="110d9-112">Чем управляет Key Vault</span><span class="sxs-lookup"><span data-stu-id="110d9-112">What Key Vault manages</span></span>

<span data-ttu-id="110d9-113">Служба Key Vault выполняет несколько внутренних функций управления от вашего имени, если вы используете ключи учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="110d9-113">Key Vault performs several internal management functions on your behalf when you use Storage Account Keys.</span></span>

1. <span data-ttu-id="110d9-114">Служба хранилища Azure Key Vault управляет ключами учетной записи хранения Azure (ASA).</span><span class="sxs-lookup"><span data-stu-id="110d9-114">Azure Key Vault manages keys of an Azure Storage Account (ASA).</span></span> 
    - <span data-ttu-id="110d9-115">На внутреннем уровне Azure Key Vault может выводить список (синхронизировать) ключи с помощью учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="110d9-115">Internally, Azure Key Vault can list (sync) keys with an Azure Storage Account.</span></span>  
    - <span data-ttu-id="110d9-116">Повторно создает хранилище ключей Azure (поворот) периодически ключи hello.</span><span class="sxs-lookup"><span data-stu-id="110d9-116">Azure Key Vault regenerates (rotates) hello keys periodically.</span></span> 
    - <span data-ttu-id="110d9-117">Ключевые значения никогда не возвращаются в toocaller ответа.</span><span class="sxs-lookup"><span data-stu-id="110d9-117">Key values are never returned in response toocaller.</span></span> 
    - <span data-ttu-id="110d9-118">Azure Key Vault управляет ключами как учетных записей хранения, так и классических учетных записей хранения.</span><span class="sxs-lookup"><span data-stu-id="110d9-118">Azure Key Vault manages keys of both Storage Accounts and Classic Storage Accounts.</span></span> 
2. <span data-ttu-id="110d9-119">Хранилище ключей Azure позволяет вы, владелец объекта или хранилище hello, определения toocreate SAS (учетной записи или служба SAS).</span><span class="sxs-lookup"><span data-stu-id="110d9-119">Azure Key Vault allows you, hello vault/object owner, toocreate SAS (account or service SAS) definitions.</span></span> 
    - <span data-ttu-id="110d9-120">Hello значение SAS с помощью определения SAS, возвращается как секрет по пути REST URI hello.</span><span class="sxs-lookup"><span data-stu-id="110d9-120">hello SAS value, created using SAS definition, is returned as a secret via hello REST URI path.</span></span> <span data-ttu-id="110d9-121">Дополнительные сведения см. в статье [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations) (Операции с учетными записями хранения Azure Key Vault).</span><span class="sxs-lookup"><span data-stu-id="110d9-121">For more information, see [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations).</span></span>

### <a name="naming-guidance"></a><span data-ttu-id="110d9-122">Рекомендации по именованию</span><span class="sxs-lookup"><span data-stu-id="110d9-122">Naming guidance</span></span>

<span data-ttu-id="110d9-123">Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и строчных букв.</span><span class="sxs-lookup"><span data-stu-id="110d9-123">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>  
 
<span data-ttu-id="110d9-124">Имя определения SAS должно быть 1–102 символа в длину и содержать только символы 0–9, a–z, A–Z.</span><span class="sxs-lookup"><span data-stu-id="110d9-124">A SAS definition name must be 1-102 characters in length containing only 0-9, a-z, A-Z.</span></span>

## <a name="developer-experience"></a><span data-ttu-id="110d9-125">Возможности для разработчика</span><span class="sxs-lookup"><span data-stu-id="110d9-125">Developer experience</span></span> 

### <a name="before-azure-key-vault-storage-keys"></a><span data-ttu-id="110d9-126">До появления ключей Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="110d9-126">Before Azure Key Vault Storage Keys</span></span> 

<span data-ttu-id="110d9-127">Разработчики использовали hello toodo tooneed методы с tooAzure хранилище tooget ключа доступа хранилища учетной записи.</span><span class="sxs-lookup"><span data-stu-id="110d9-127">Developers used tooneed toodo hello following practices with a storage account key tooget access tooAzure storage.</span></span> 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a><span data-ttu-id="110d9-128">После появления ключей Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="110d9-128">After Azure Key Vault Storage Keys</span></span> 

```
//Please make sure tooset storage permissions appropriately on your key vault
Set-AzureRmKeyVaultAccessPolicy -VaultName 'yourVault' -ObjectId yourObjectId -PermissionsToStorage all

//Use PowerShell command tooget Secret URI 

Set-AzureKeyVaultManagedStorageSasDefinition -Service Blob -ResourceType Container,Service -VaultName yourKV  
-AccountName msak01 -Name blobsas1 -Protocol HttpsOnly -ValidityPeriod ([System.Timespan]::FromDays(1)) -Permission Read,List

//Get SAS token from Key Vault

var secret = await kv.GetSecretAsync("SecretUri");

// Create new storage credentials using hello SAS token. 

var accountSasCredential = new StorageCredentials(secret.Value); 

// Use credentials and hello Blob storage endpoint toocreate a new Blob service client. 

var accountWithSas = new CloudStorageAccount(accountSasCredential, new Uri ("https://myaccount.blob.core.windows.net/"), null, null, null); 

var blobClientWithSas = accountWithSas.CreateCloudBlobClient(); 
 
// If SAS token is about tooexpire then Get sasToken again from Key Vault and update it.

accountSasCredential.UpdateSASToken(sasToken);

  ```
 
 ### <a name="developer-best-practices"></a><span data-ttu-id="110d9-129">Рекомендации разработчикам</span><span class="sxs-lookup"><span data-stu-id="110d9-129">Developer best practices</span></span> 

- <span data-ttu-id="110d9-130">Разрешить toomanage хранилище ключей только ключи ASA.</span><span class="sxs-lookup"><span data-stu-id="110d9-130">Only allow Key Vault toomanage your ASA keys.</span></span> <span data-ttu-id="110d9-131">Не пытайтесь toomanage их самостоятельно, взаимодействовать с процессами хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="110d9-131">Do not attempt toomanage them yourself, you will interfere with Key Vault's processes.</span></span> 
- <span data-ttu-id="110d9-132">Не разрешать ASA ключи toobe под управлением более одного объекта в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="110d9-132">Do not allow ASA keys toobe managed by more than one Key Vault object.</span></span> 
- <span data-ttu-id="110d9-133">Если вам требуется toomanually повторно создать ключи ASA, рекомендуется восстановить их помощью хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="110d9-133">If you need toomanually regenerate your ASA keys, we recommend that you regenerate them via Key Vault.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="110d9-134">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="110d9-134">Getting started</span></span>

### <a name="setup-for-role-based-access-control-rbac-permissions"></a><span data-ttu-id="110d9-135">Настройка разрешений для управления доступом на основе ролей (RBAC)</span><span class="sxs-lookup"><span data-stu-id="110d9-135">Setup for role-based access control (RBAC) permissions</span></span>

<span data-ttu-id="110d9-136">Хранилище ключей требуются разрешения слишком*списка* и *повторно создать* ключи для учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="110d9-136">Key Vault needs permissions too*list* and *regenerate* keys for a storage account.</span></span> <span data-ttu-id="110d9-137">Настроить эти разрешения с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="110d9-137">Set up these permissions using hello following steps:</span></span>

- <span data-ttu-id="110d9-138">Получите ObjectId хранилища Key Vault:</span><span class="sxs-lookup"><span data-stu-id="110d9-138">Get ObjectId of Key Vault:</span></span> 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- <span data-ttu-id="110d9-139">Назначьте роль оператора Key хранилища tooAzure ключ хранилища удостоверений:</span><span class="sxs-lookup"><span data-stu-id="110d9-139">Assign Storage Key Operator role tooAzure Key Vault Identity:</span></span> 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > <span data-ttu-id="110d9-140">Для типа классический учетной записи, установите параметр роли hello слишком*«Классический хранилища учетной записи ключа оператор службы роли»*.</span><span class="sxs-lookup"><span data-stu-id="110d9-140">For a classic account type, set hello role parameter too*"Classic Storage Account Key Operator Service Role"*.</span></span>

### <a name="storage-account-onboarding"></a><span data-ttu-id="110d9-141">Подключение учетной записи хранения</span><span class="sxs-lookup"><span data-stu-id="110d9-141">Storage account onboarding</span></span> 

<span data-ttu-id="110d9-142">Пример: Как владелец объекта хранилища ключей, добавьте хранилища учетной записи хранилища ключей Azure tooonboard объекта tooyour учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="110d9-142">Example: As a Key Vault object owner you add a storage account object tooyour Azure Key Vault tooonboard a storage account.</span></span>

<span data-ttu-id="110d9-143">Во время адаптации, хранилище ключей требуется hello удостоверение учетной записи адаптации hello имеет разрешения слишком tooverify*списка* и слишком*повторно создать* хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="110d9-143">During onboarding, Key Vault needs tooverify that hello identity of hello onboarding account has permissions too*list* and too*regenerate* storage keys.</span></span> <span data-ttu-id="110d9-144">В заказ tooverify эти разрешения, хранилище ключей возвращает OBO (по имени из) токен из службы проверки подлинности hello, аудитории задать tooAzure диспетчера ресурсов и делает *списка* ключа службой хранилища Azure toohello вызова.</span><span class="sxs-lookup"><span data-stu-id="110d9-144">In order tooverify these permissions, Key Vault gets an OBO (On Behalf Of) token from hello authentication service, audience set tooAzure Resource Manager, and makes a *list* key call toohello Azure Storage service.</span></span> <span data-ttu-id="110d9-145">Если hello *списка* вызов завершается ошибкой, Здравствуйте, происходит сбой создания объекта с кодом состояния HTTP из хранилища ключей *запрещено*.</span><span class="sxs-lookup"><span data-stu-id="110d9-145">If hello *list* call fails, hello Key Vault object creation fails with a HTTP status code of *Forbidden*.</span></span> <span data-ttu-id="110d9-146">разделы Hello, указанные таким образом кэшируются с хранилищем хранилища ключей сущности.</span><span class="sxs-lookup"><span data-stu-id="110d9-146">hello keys listed in this fashion are cached with your key vault entity storage.</span></span> 

<span data-ttu-id="110d9-147">Хранилище ключей должно убедитесь, что удостоверение hello имеет *повторно создать* разрешения, прежде чем он может стать владельцем повторное создание ключей.</span><span class="sxs-lookup"><span data-stu-id="110d9-147">Key Vault must verify that hello identity has *regenerate* permissions before it can take ownership of regenerating your keys.</span></span> <span data-ttu-id="110d9-148">tooverify hello удостоверение через маркер OBO, а также hello удостоверение стороны хранилище ключей имеет следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="110d9-148">tooverify that hello identity, via OBO token, as well as hello Key Vault first party identity has these permissions:</span></span>

- <span data-ttu-id="110d9-149">Хранилище ключей список разрешений RBAC на ресурс учетной записи хранения hello.</span><span class="sxs-lookup"><span data-stu-id="110d9-149">Key Vault lists RBAC permissions on hello storage account resource.</span></span>
- <span data-ttu-id="110d9-150">Хранилище ключей проверяет hello ответу с помощью действий, а не действия сопоставление регулярных выражений.</span><span class="sxs-lookup"><span data-stu-id="110d9-150">Key Vault validates hello response via regular expression matching of actions and non-actions.</span></span> 

<span data-ttu-id="110d9-151">Некоторые поддерживаемые примеры вы можете найти в разделе [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault — управляемая система хранения ключей учетных записей).</span><span class="sxs-lookup"><span data-stu-id="110d9-151">Find some supporting examples at [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167).</span></span>

<span data-ttu-id="110d9-152">Если удостоверение hello не имеет *повторно создать* разрешений или если удостоверение стороны хранилища ключей не *списка* или *повторно создать* разрешений, а затем адаптации hello запрос завершается неудачно, возвращая соответствующий код ошибки и сообщения.</span><span class="sxs-lookup"><span data-stu-id="110d9-152">If hello identity does not have *regenerate* permissions or if Key Vault's first party identity doesn’t have *list* or *regenerate* permission, then hello onboarding request fails returning an appropriate error code and message.</span></span> 

<span data-ttu-id="110d9-153">токен OBO Hello будет работать только при использовании в основном, собственные клиентские приложения, PowerShell или интерфейс командной строки.</span><span class="sxs-lookup"><span data-stu-id="110d9-153">hello OBO token will only work when you use first-party, native client applications of either PowerShell or CLI.</span></span>

## <a name="other-applications"></a><span data-ttu-id="110d9-154">Другие приложения</span><span class="sxs-lookup"><span data-stu-id="110d9-154">Other applications</span></span>

- <span data-ttu-id="110d9-155">Маркеры SAS, создано с помощью ключа учетной записи хранилища ключей, предоставляют еще больше tooan управляемый доступ к ресурсам учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="110d9-155">SAS tokens, constructed using Key Vault storage account keys, provide even more controlled access tooan Azure storage account.</span></span> <span data-ttu-id="110d9-156">Дополнительные сведения см. в статье [Использование подписанных URL-адресов (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span><span class="sxs-lookup"><span data-stu-id="110d9-156">For more information, see [Using shared access signatures](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).</span></span>

## <a name="see-also"></a><span data-ttu-id="110d9-157">См. также</span><span class="sxs-lookup"><span data-stu-id="110d9-157">See also</span></span>

- [<span data-ttu-id="110d9-158">Сведения о ключах, секретах и сертификатах</span><span class="sxs-lookup"><span data-stu-id="110d9-158">About keys, secrets, and certificates</span></span>](https://docs.microsoft.com/rest/api/keyvault/)
- [<span data-ttu-id="110d9-159">Официальный блог команды разработчиков Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="110d9-159">Key Vault Team Blog</span></span>](https://blogs.technet.microsoft.com/kv/)
