---
title: "aaaGetting к работе с хранилищем ключей Azure стека | Документы Microsoft"
description: "Начало работы с использованием хранилища ключей Azure стека"
services: azure-stack
documentationcenter: 
author: rlfmendes
manager: natmack
editor: 
ms.assetid: b973be33-2fc1-4ee6-976a-84ed270e7254
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: ricardom
ms.openlocfilehash: 66ae55291951ee0c673ba2b50ea4aecb3df19a88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-key-vault"></a>Приступая к работе с хранилищем ключей
В этом разделе описаны шаги hello toocreate хранилища, управлять ключи и секретные коды а также разрешают операции tooinvoke пользователи или приложения в хранилище hello Azure стека. Hello следующие шаги предполагают подписки клиента существует и KeyVault служба зарегистрирована в этой подписке. Все команды пример hello основаны на hello KeyVault командлетов, доступных в рамках hello Azure PowerShell SDK.

## <a name="enabling-hello-tenant-subscription-for-vault-operations"></a>Включение подписки клиента hello для операций хранилища
Перед можно выполнять операции с любое хранилище, необходимо tooensure которой включены подписки операций в хранилище. Вы можете подтвердить, выполнив следующую команду PowerShell hello:

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

выходные данные Hello hello выше команду следует сообщать «Зарегистрировано» для hello «Registration» состояние каждой строки.

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 Если это не так hello, следует вызвать hello, следующая команда tooregister hello KeyVault службы в подписке:

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

И следующих hello hello выходные данные команды hello:

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> Если появляется ошибка hello: «*hello подписка не зарегистрирована в хранилище ключей Azure*» при вызове командлетов KeyVault, подтвердите включен поставщик ресурсов KeyVault hello по приведенным выше инструкциям.
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-toostore-and-manage-cryptographic-keys-and-secrets"></a>Создание жесткой контейнера (хранилище) в стек Azure toostore и управления ими криптографических ключей и
Порядок toocreate хранилище клиента необходимо сначала создать группу ресурсов. Hello следующие команды PowerShell создают группу ресурсов, а затем хранилище в этой группе ресурсов. пример Hello также включает hello стандартные выходные данные этого командлета.

### <a name="creating-a-resource-group"></a>Создание группы ресурсов:
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

Выходные данные:

    VERBOSE: Performing hello operation "Replacing resource group ..." on target "".
    VERBOSE: 12:52:51 PM - Created resource group 'vaultrg010' in location 'local'
    ResourceGroupName : vaultrg010
    Location : local
    ProvisioningState : Succeeded
    Tags :
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010


### <a name="creating-a-vault"></a>Создание хранилища:
    New-AzureRmKeyVault -VaultName vault010 -ResourceGroupName vaultrg010 -Location local -Verbose

Выходные данные:

    VaultUri : https://vault010.vault.local.azurestack.global
    TenantId : 5454420b-2e38-4b9e-8b56-1712d321cf33
    TenantName : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Sku : Standard
    EnabledForDeployment : False
    EnabledForTemplateDeployment : False
    EnabledForDiskEncryption : False
    AccessPolicies : {5454420b-2e38-4b9e-8b56-1712d321cf33}
    AccessPoliciesText :
    Tenant ID : 5454420b-2e38-4b9e-8b56-1712d321cf33
    Object ID : ca342e90-f6aa-435b-a11c-dfe5ef0bfeeb
    Application ID :
    Display Name : Tenant Admin (tenantadmin1@msazurestack.onmicrosoft.com)
    Permissions tooKeys : get, create, delete, list, update, import, backup, restore
    Permissions tooSecrets : all
    OriginalVault : Microsoft.Azure.Management.KeyVault.Vault
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010/providers/Microsoft.KeyVault/vaults/vault010
    VaultName : vault010
    ResourceGroupName : vaultrg010
    Location : local
    Tags : {}
    TagsTable :

выходные данные командлета Hello приведены свойства ключа хранилища hello, которое вы только что создали. Hello двух наиболее важных свойств:

* **Имя хранилища**: В примере hello это **vault010**. Вы будете использовать это имя для выполнения других командлетов хранилища ключей;
* **Код URI хранилища**: пример hello это https://vault010.vault.local.azurestack.global. Необходимо, чтобы приложения, использующие ваше хранилище через REST API, использовали этот URI.

Учетная запись Azure — теперь авторизованным tooperform все операции в этот ключ в хранилище. Пока что это недоступно для других учетных записей.

## <a name="operating-on-keys-and-secrets"></a>Ключи и секретные данные
После создания хранилища, выполните hello ниже шаги toocreate управление ключи и секретные коды:

### <a name="creating-a-key"></a>Создание ключа
В заказ toocreate ключа, используйте hello **Add-AzureKeyVaultKey** в приведенном ниже примере hello. После успешного создания ключа hello командлет выдаст hello, новые сведения о ключе.

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

Hello ниже приведен вывод hello hello *Add-AzureKeyVaultKey* командлета:

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

Теперь можно ссылаться на этот ключ, созданные или переданные tooAzure хранилище ключей с помощью URI-адрес. Используйте **https://vault010.vault.local.azurestack.global:443, ключи/keyVaultKeyName001** tooalways получить текущую версию hello; и использовать **https://vault010.vault.local.azurestack.global:443/ключи / keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** tooget этой конкретной версии.

### <a name="retrieving-a-key"></a>Получение ключа
Используйте hello **Get-AzureKeyVaultKey** tooretrieve Здравствуйте, ключ и сведения о нем в следующем примере:

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

Вот hello выходные данные Get-AzureKeyVaultKey Hello

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

### <a name="setting-a-secret"></a>Задание секрета
    $secretvalue = ConvertTo-SecureString 'User@123' -AsPlainText -Force
    Set-AzureKeyVaultSecret -Name MySecret-VaultName vault010 -SecretValue $secretvalue

Выходные данные

    Vault Name : vault010
    Name : MySecret
    Version : 65a387f2ed4a416180e852b970846f5b
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret/65a387f2ed4a416180e852b970846f5b
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags : 

### <a name="retrieving-a-secret"></a>Получение секрета
    Get-AzureKeyVaultSecret -VaultName vault010

Выходные данные

    Vault Name : vault010
    Name : MySecret
    Version :
    Id : https://vault010.vault.local.azurestack.global:443/secrets/MySecret
    Enabled : True
    Expires :
    Not Before :
    Created : 8/17/2016 10:49:52 PM
    Updated : 8/17/2016 10:49:52 PM
    Content Type :
    Tags :

Теперь хранилища ключей и ключа или секрета готова для toouse приложений.
Toouse приложений необходимо авторизовать их.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Авторизовать hello приложения toouse hello ключа или секрета
tooaccess приложения hello tooauthorize hello ключа или секрета в хранилище hello, используйте hello Set -**AzureRmKeyVaultAccessPolicy** командлета.

Например, если имя хранилища — *ContosoKeyVault* и hello приложение имеет tooauthorize *идентификатор клиента* из *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*и вы хотите toodecrypt приложения hello tooauthorize и войдите с ключами в хранилище, выполните следующие hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

Tooauthorize этой же tooread секреты приложения в хранилище, выполните следующие hello:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a>Дальнейшие действия
[Развертывание виртуальной машины с помощью пароля из хранилища ключей](azure-stack-kv-deploy-vm-with-secret.md)

[Развертывание виртуальной Машины с помощью хранилища ключей сертификата](azure-stack-kv-push-secret-into-vm.md)

