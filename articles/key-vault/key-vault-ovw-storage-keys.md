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
# <a name="azure-key-vault-storage-account-keys"></a>Ключи учетной записи хранения Azure Key Vault

Перед ключи учетной записи хранения хранилище ключей Azure разработчики имели toomanage свои собственные ключи учетной записи хранилища Azure (ASA) и повернуть их вручную или с помощью внешних автоматизации. Сейчас ключи учетной записи хранения Key Vault реализованы в качестве [секретов Key Vault](https://docs.microsoft.com/rest/api/keyvault/about-keys--secrets-and-certificates#BKMK_WorkingWithSecrets) для проверки подлинности с помощью учетной записи хранения Azure. 

ключевой особенностью ASA Hello управляет секретный поворота и удаляет hello потребность прямой связи с ключом ASA путем предоставления общего доступа подписи (SAS) как метод. 

Дополнительные сведения об учетных записях хранения Azure см. в статье [Об учетных записях хранения Azure](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

## <a name="supporting-interfaces"></a>Поддержка интерфейсов

Hello функция ключи учетной записи хранилища Azure изначально доступна через hello REST, .NET или C# и PowerShell интерфейсов. Дополнительные сведения см. в разделе [Документация по хранилищу ключей](https://docs.microsoft.com/azure/key-vault/).


## <a name="storage-account-keys-behavior"></a>Поведение ключей учетной записи хранения

### <a name="what-key-vault-manages"></a>Чем управляет Key Vault

Служба Key Vault выполняет несколько внутренних функций управления от вашего имени, если вы используете ключи учетной записи хранения.

1. Служба хранилища Azure Key Vault управляет ключами учетной записи хранения Azure (ASA). 
    - На внутреннем уровне Azure Key Vault может выводить список (синхронизировать) ключи с помощью учетной записи хранения Azure.  
    - Повторно создает хранилище ключей Azure (поворот) периодически ключи hello. 
    - Ключевые значения никогда не возвращаются в toocaller ответа. 
    - Azure Key Vault управляет ключами как учетных записей хранения, так и классических учетных записей хранения. 
2. Хранилище ключей Azure позволяет вы, владелец объекта или хранилище hello, определения toocreate SAS (учетной записи или служба SAS). 
    - Hello значение SAS с помощью определения SAS, возвращается как секрет по пути REST URI hello. Дополнительные сведения см. в статье [Azure Key Vault storage account operations](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations) (Операции с учетными записями хранения Azure Key Vault).

### <a name="naming-guidance"></a>Рекомендации по именованию

Имя учетной записи хранения должно содержать от 3 до 24 символов и состоять только из цифр и строчных букв.  
 
Имя определения SAS должно быть 1–102 символа в длину и содержать только символы 0–9, a–z, A–Z.

## <a name="developer-experience"></a>Возможности для разработчика 

### <a name="before-azure-key-vault-storage-keys"></a>До появления ключей Azure Key Vault 

Разработчики использовали hello toodo tooneed методы с tooAzure хранилище tooget ключа доступа хранилища учетной записи. 
 
 ```
//create storage account using connection string containing account name 
// and hello storage key 

var storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));
var blobClient = storageAccount.CreateCloudBlobClient();
 ```
 
### <a name="after-azure-key-vault-storage-keys"></a>После появления ключей Azure Key Vault 

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
 
 ### <a name="developer-best-practices"></a>Рекомендации разработчикам 

- Разрешить toomanage хранилище ключей только ключи ASA. Не пытайтесь toomanage их самостоятельно, взаимодействовать с процессами хранилища ключей. 
- Не разрешать ASA ключи toobe под управлением более одного объекта в хранилище ключей. 
- Если вам требуется toomanually повторно создать ключи ASA, рекомендуется восстановить их помощью хранилище ключей. 

## <a name="getting-started"></a>Приступая к работе

### <a name="setup-for-role-based-access-control-rbac-permissions"></a>Настройка разрешений для управления доступом на основе ролей (RBAC)

Хранилище ключей требуются разрешения слишком*списка* и *повторно создать* ключи для учетной записи хранилища. Настроить эти разрешения с помощью hello следующие шаги:

- Получите ObjectId хранилища Key Vault: 

    `Get-AzureRmADServicePrincipal -SearchString "AzureKeyVault"`

- Назначьте роль оператора Key хранилища tooAzure ключ хранилища удостоверений: 

    `New-AzureRmRoleAssignment -ObjectId <objectId of AzureKeyVault from previous command> -RoleDefinitionName 'Storage Account Key Operator Service Role' -Scope '<azure resource id of storage account>'`

    >[!NOTE]
    > Для типа классический учетной записи, установите параметр роли hello слишком*«Классический хранилища учетной записи ключа оператор службы роли»*.

### <a name="storage-account-onboarding"></a>Подключение учетной записи хранения 

Пример: Как владелец объекта хранилища ключей, добавьте хранилища учетной записи хранилища ключей Azure tooonboard объекта tooyour учетной записи хранилища.

Во время адаптации, хранилище ключей требуется hello удостоверение учетной записи адаптации hello имеет разрешения слишком tooverify*списка* и слишком*повторно создать* хранилища ключей. В заказ tooverify эти разрешения, хранилище ключей возвращает OBO (по имени из) токен из службы проверки подлинности hello, аудитории задать tooAzure диспетчера ресурсов и делает *списка* ключа службой хранилища Azure toohello вызова. Если hello *списка* вызов завершается ошибкой, Здравствуйте, происходит сбой создания объекта с кодом состояния HTTP из хранилища ключей *запрещено*. разделы Hello, указанные таким образом кэшируются с хранилищем хранилища ключей сущности. 

Хранилище ключей должно убедитесь, что удостоверение hello имеет *повторно создать* разрешения, прежде чем он может стать владельцем повторное создание ключей. tooverify hello удостоверение через маркер OBO, а также hello удостоверение стороны хранилище ключей имеет следующие разрешения:

- Хранилище ключей список разрешений RBAC на ресурс учетной записи хранения hello.
- Хранилище ключей проверяет hello ответу с помощью действий, а не действия сопоставление регулярных выражений. 

Некоторые поддерживаемые примеры вы можете найти в разделе [Key Vault - Managed Storage Account Keys Samples](https://github.com/Azure/azure-sdk-for-net/blob/psSdkJson6/src/SDKs/KeyVault/dataPlane/Microsoft.Azure.KeyVault.Samples/samples/HelloKeyVault/Program.cs#L167) (Key Vault — управляемая система хранения ключей учетных записей).

Если удостоверение hello не имеет *повторно создать* разрешений или если удостоверение стороны хранилища ключей не *списка* или *повторно создать* разрешений, а затем адаптации hello запрос завершается неудачно, возвращая соответствующий код ошибки и сообщения. 

токен OBO Hello будет работать только при использовании в основном, собственные клиентские приложения, PowerShell или интерфейс командной строки.

## <a name="other-applications"></a>Другие приложения

- Маркеры SAS, создано с помощью ключа учетной записи хранилища ключей, предоставляют еще больше tooan управляемый доступ к ресурсам учетной записи хранилища Azure. Дополнительные сведения см. в статье [Использование подписанных URL-адресов (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1).

## <a name="see-also"></a>См. также

- [Сведения о ключах, секретах и сертификатах](https://docs.microsoft.com/rest/api/keyvault/)
- [Официальный блог команды разработчиков Azure Key Vault](https://blogs.technet.microsoft.com/kv/)
