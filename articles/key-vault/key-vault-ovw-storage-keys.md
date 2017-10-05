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
# <a name="azure-key-vault-storage-account-keys"></a>Ключи учетной записи хранения Azure Key Vault

До появления ключей учетной записи хранения Azure Key Vault разработчикам приходилось управлять ключами учетной записи хранения Azure (ASA) и сменять их вручную или с помощью внешних средств автоматизации. Сейчас ключи учетной записи хранения Key Vault реализованы в качестве [секретов Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) для проверки подлинности с помощью учетной записи хранения Azure. 

Функция ключа ASA управляет сменой секретов и устраняет необходимость прямого контакта с ключом ASA за счет использования подписанных URL-адресов (SAS). 

Дополнительные сведения об учетных записях хранения Azure см. в статье [Об учетных записях хранения Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Поддержка интерфейсов

Функция ключей учетной записи хранения Azure изначально доступна через интерфейсы REST, .NET, C# и PowerShell. Дополнительные сведения см. в разделе [Документация по хранилищу ключей](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Поведение ключей учетной записи хранения

### <a name="what-key-vault-manages"></a>Чем управляет Key Vault

Служба Key Vault выполняет несколько внутренних функций управления от вашего имени, если вы используете ключи учетной записи хранения.

1. Служба хранилища Azure Key Vault управляет ключами учетной записи хранения Azure (ASA). 
    - На внутреннем уровне Azure Key Vault может выводить список (синхронизировать) ключи с помощью учетной записи хранения Azure.  
    - Azure Key Vault периодически повторно создает (сменяет) ключи. 
    - Значения ключей никогда не возвращаются в ответе вызывающему объекту. 
    - Azure Key Vault управляет ключами как учетных записей хранения, так и классических учетных записей хранения. 
2. Azure Key Vault позволяет владельцу хранилища или объекта создавать определения SAS (учетной записи или службы). 
    - Значение SAS, созданное с помощью определения SAS, возвращается в качестве секрета через путь универсального кода ресурса (URI) REST. Дополнительные сведения см. в статье [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations) (Операции с учетными записями хранения Azure Key Vault).

### <a name="naming-guidance"></a>Рекомендации по именованию

Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и строчных букв.  
 
Имя определения SAS должно быть 1–102 символа в длину и содержать только символы 0–9, a–z, A–Z.

## <a name="developer-experience"></a>Возможности для разработчика 

### <a name="before-azure-key-vault-storage-keys"></a>До появления ключей Azure Key Vault 

Разработчикам приходилось применять следующие методы, чтобы получить доступ к хранилищу Azure с помощью ключа учетной записи хранения. 
 
 ```
//create storage account using connection string containing account name 
// and the storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>После появления ключей Azure Key Vault 

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
 
 ### <a name="developer-best-practices"></a>Рекомендации разработчикам 

- Разрешите только Key Vault управлять ключами ASA. Не пытайтесь управлять ими самостоятельно. Это повлияет на процессы Key Vault. 
- Ключи ASA не должны управляться более чем одним объектом Key Vault. 
- Если необходимо вручную повторно создать ключи ASA, рекомендуем делать это через Key Vault. 

## <a name="getting-started"></a>Приступая к работе

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Настройка разрешений для управления доступом на основе ролей (RBAC)

Для Key Vault необходимы разрешения для *вывода списка* и *повторного создания* ключей учетной записи хранения. Настройте эти разрешения, выполнив следующие действия:

- Получите ObjectId хранилища Key Vault: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Присвойте идентификатору Azure Key Vault роль оператора учетной записи хранения: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Для классической учетной записи задайте для параметра роли значение *Classic Storage Account Key Operator Service Role* (Роль службы оператора ключей классических учетных записей хранения).

### <a name="storage-account-onboarding"></a>Подключение учетной записи хранения 

Пример: владелец объекта Key Vault добавляет объект учетной записи хранилища в Azure Key Vault, чтобы подключить учетную запись хранения.

Во время подключения Key Vault проверяет, что удостоверение подключаемой учетной записи имеет разрешения на *перечисление* и *повторное создание* ключей хранилища. Чтобы проверить эти разрешения, Key Vault получает токен OBO (от имени) от службы аутентификации, указывает Azure Resource Manager в качестве целевой аудитории, а затем обращается к службе хранилища Azure для *получения списка*. Если *вызов списка* завершается неудачно, создание объекта Key Vault завершается ошибкой с кодом состояния HTTP *Запрещено*. Ключи, указанные таким способом, кэшируются с помощью хранилища сущностей хранилища ключей. 

Key Vault необходимо убедиться, что идентификатор имеет разрешения на *повторное создание*, прежде чем предоставить ему права на повторное создание ключей. Чтобы убедиться, что идентификатор (через токен OBO), а также основной идентификатор Key Vault имеют следующие разрешения:

- Key Vault выводит список разрешений RBAC в ресурсе учетной записи хранения.
- Key Vault проверяет ответ через сопоставление регулярных выражений для определения действий и их отсутствия. 

Некоторые поддерживаемые примеры вы можете найти в разделе [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault — управляемая система хранения ключей учетных записей).

Если удостоверение не имеет разрешение на *повторное создание* или основное удостоверение Key Vault не имеет разрешение на *перечисление* или *повторное создание*, тогда запрос на подключение завершается ошибкой с соответствующим кодом и сообщением. 

Маркер OBO будет работать только при использовании основных, собственных клиентских приложений PowerShell или CLI.

## <a name="other-applications"></a>Другие приложения

- Маркеры SAS, созданные с помощью ключей учетной записи хранения Key Vault, предоставляют более точный контроль доступа к учетной записи хранения Azure. Дополнительные сведения см. в статье [Использование подписанных URL-адресов (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>См. также

- [Сведения о ключах, секретах и сертификатах](https://docs.microsoft.com/rest/api/keyvault/)
- [Официальный блог команды разработчиков Azure Key Vault](https://blogs.technet.microsoft.com/kv/)
