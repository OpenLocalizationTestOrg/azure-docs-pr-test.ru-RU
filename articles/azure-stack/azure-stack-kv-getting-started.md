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
# <a name="getting-started-with-key-vault"></a><span data-ttu-id="aed24-103">Приступая к работе с хранилищем ключей</span><span class="sxs-lookup"><span data-stu-id="aed24-103">Getting started with Key Vault</span></span>
<span data-ttu-id="aed24-104">В этом разделе описаны шаги hello toocreate хранилища, управлять ключи и секретные коды а также разрешают операции tooinvoke пользователи или приложения в хранилище hello Azure стека.</span><span class="sxs-lookup"><span data-stu-id="aed24-104">This section describes hello steps toocreate a vault, manage keys and secrets as well as authorize users or applications tooinvoke operations in hello vault in Azure Stack.</span></span> <span data-ttu-id="aed24-105">Hello следующие шаги предполагают подписки клиента существует и KeyVault служба зарегистрирована в этой подписке.</span><span class="sxs-lookup"><span data-stu-id="aed24-105">hello following steps assume a tenant subscription exists and KeyVault service is registered within that subscription.</span></span> <span data-ttu-id="aed24-106">Все команды пример hello основаны на hello KeyVault командлетов, доступных в рамках hello Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="aed24-106">All hello example commands are based on hello KeyVault cmdlets available as part of hello Azure PowerShell SDK.</span></span>

## <a name="enabling-hello-tenant-subscription-for-vault-operations"></a><span data-ttu-id="aed24-107">Включение подписки клиента hello для операций хранилища</span><span class="sxs-lookup"><span data-stu-id="aed24-107">Enabling hello tenant subscription for Vault operations</span></span>
<span data-ttu-id="aed24-108">Перед можно выполнять операции с любое хранилище, необходимо tooensure которой включены подписки операций в хранилище.</span><span class="sxs-lookup"><span data-stu-id="aed24-108">Before you can issue operations against any vault, you need tooensure that your subscription is enabled for vault operations.</span></span> <span data-ttu-id="aed24-109">Вы можете подтвердить, выполнив следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="aed24-109">You can confirm that by issuing hello following PowerShell command:</span></span>

    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -AutoSize

<span data-ttu-id="aed24-110">выходные данные Hello hello выше команду следует сообщать «Зарегистрировано» для hello «Registration» состояние каждой строки.</span><span class="sxs-lookup"><span data-stu-id="aed24-110">hello output of hello above command should report “Registered” for hello “Registration” state of every row.</span></span>

    ProviderNamespace RegistrationState ResourceTypes Locations
    Microsoft.KeyVault Registered {operations} {local}
    Microsoft.KeyVault Registered {vaults} {local}
    Microsoft.KeyVault Registered {vaults/secrets} {local}


 <span data-ttu-id="aed24-111">Если это не так hello, следует вызвать hello, следующая команда tooregister hello KeyVault службы в подписке:</span><span class="sxs-lookup"><span data-stu-id="aed24-111">If that’s not hello case, you should invoke hello following command tooregister hello KeyVault service within your subscription:</span></span>

    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault

<span data-ttu-id="aed24-112">И следующих hello hello выходные данные команды hello:</span><span class="sxs-lookup"><span data-stu-id="aed24-112">And hello folowing is hello output of hello command:</span></span>

    ProviderNamespace : Microsoft.KeyVault
    RegistrationState : Registered
    ResourceTypes : {operations, vaults, vaults/secrets}
    Locations : {local}


> [!NOTE]
> <span data-ttu-id="aed24-113">Если появляется ошибка hello: «*hello подписка не зарегистрирована в хранилище ключей Azure*» при вызове командлетов KeyVault, подтвердите включен поставщик ресурсов KeyVault hello по приведенным выше инструкциям.</span><span class="sxs-lookup"><span data-stu-id="aed24-113">If you get hello error: "*hello subscription is not registered with Azure Key Vault*" when invoking KeyVault cmdlets, please confirm you have enabled hello KeyVault resource provider per instructions above.</span></span>
> 
> 

## <a name="creating-a-hardened-container-a-vault-in-azure-stack-toostore-and-manage-cryptographic-keys-and-secrets"></a><span data-ttu-id="aed24-114">Создание жесткой контейнера (хранилище) в стек Azure toostore и управления ими криптографических ключей и</span><span class="sxs-lookup"><span data-stu-id="aed24-114">Creating a hardened container (a vault) in Azure Stack toostore and manage cryptographic keys and secrets</span></span>
<span data-ttu-id="aed24-115">Порядок toocreate хранилище клиента необходимо сначала создать группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="aed24-115">In order toocreate a Vault, a tenant should first create a resource group.</span></span> <span data-ttu-id="aed24-116">Hello следующие команды PowerShell создают группу ресурсов, а затем хранилище в этой группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="aed24-116">hello following PowerShell commands create a resource group and then a Vault in that Resource Group.</span></span> <span data-ttu-id="aed24-117">пример Hello также включает hello стандартные выходные данные этого командлета.</span><span class="sxs-lookup"><span data-stu-id="aed24-117">hello example also includes hello typical output from that cmdlet.</span></span>

### <a name="creating-a-resource-group"></a><span data-ttu-id="aed24-118">Создание группы ресурсов:</span><span class="sxs-lookup"><span data-stu-id="aed24-118">Creating a resource group:</span></span>
    New-AzureRmResourceGroup -Name vaultrg010 -Location local -Verbose -Force

<span data-ttu-id="aed24-119">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="aed24-119">Output:</span></span>

    VERBOSE: Performing hello operation "Replacing resource group ..." on target "".
    VERBOSE: 12:52:51 PM - Created resource group 'vaultrg010' in location 'local'
    ResourceGroupName : vaultrg010
    Location : local
    ProvisioningState : Succeeded
    Tags :
    ResourceId : /subscriptions/fa881715-3802-42cc-a54e-a06adf61584d/resourceGroups/vaultrg010


### <a name="creating-a-vault"></a><span data-ttu-id="aed24-120">Создание хранилища:</span><span class="sxs-lookup"><span data-stu-id="aed24-120">Creating a vault:</span></span>
    New-AzureRmKeyVault -VaultName vault010 -ResourceGroupName vaultrg010 -Location local -Verbose

<span data-ttu-id="aed24-121">Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="aed24-121">Output:</span></span>

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

<span data-ttu-id="aed24-122">выходные данные командлета Hello приведены свойства ключа хранилища hello, которое вы только что создали.</span><span class="sxs-lookup"><span data-stu-id="aed24-122">hello output of this cmdlet shows properties of hello key vault that you’ve just created.</span></span> <span data-ttu-id="aed24-123">Hello двух наиболее важных свойств:</span><span class="sxs-lookup"><span data-stu-id="aed24-123">hello two most important properties are:</span></span>

* <span data-ttu-id="aed24-124">**Имя хранилища**: В примере hello это **vault010**.</span><span class="sxs-lookup"><span data-stu-id="aed24-124">**Vault Name**: In hello example, this is **vault010**.</span></span> <span data-ttu-id="aed24-125">Вы будете использовать это имя для выполнения других командлетов хранилища ключей;</span><span class="sxs-lookup"><span data-stu-id="aed24-125">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="aed24-126">**Код URI хранилища**: пример hello это https://vault010.vault.local.azurestack.global.</span><span class="sxs-lookup"><span data-stu-id="aed24-126">**Vault URI**: In hello example, this is https://vault010.vault.local.azurestack.global.</span></span> <span data-ttu-id="aed24-127">Необходимо, чтобы приложения, использующие ваше хранилище через REST API, использовали этот URI.</span><span class="sxs-lookup"><span data-stu-id="aed24-127">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="aed24-128">Учетная запись Azure — теперь авторизованным tooperform все операции в этот ключ в хранилище.</span><span class="sxs-lookup"><span data-stu-id="aed24-128">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="aed24-129">Пока что это недоступно для других учетных записей.</span><span class="sxs-lookup"><span data-stu-id="aed24-129">As yet, nobody else is.</span></span>

## <a name="operating-on-keys-and-secrets"></a><span data-ttu-id="aed24-130">Ключи и секретные данные</span><span class="sxs-lookup"><span data-stu-id="aed24-130">Operating on Keys and Secrets</span></span>
<span data-ttu-id="aed24-131">После создания хранилища, выполните hello ниже шаги toocreate управление ключи и секретные коды:</span><span class="sxs-lookup"><span data-stu-id="aed24-131">After creating a vault, follow hello below steps toocreate manage keys and secrets:</span></span>

### <a name="creating-a-key"></a><span data-ttu-id="aed24-132">Создание ключа</span><span class="sxs-lookup"><span data-stu-id="aed24-132">Creating a key</span></span>
<span data-ttu-id="aed24-133">В заказ toocreate ключа, используйте hello **Add-AzureKeyVaultKey** в приведенном ниже примере hello.</span><span class="sxs-lookup"><span data-stu-id="aed24-133">In order toocreate a key, use hello **Add-AzureKeyVaultKey** per hello example below.</span></span> <span data-ttu-id="aed24-134">После успешного создания ключа hello командлет выдаст hello, новые сведения о ключе.</span><span class="sxs-lookup"><span data-stu-id="aed24-134">After successful key creation, hello cmdlet will output hello newly created key details.</span></span>

    Add-AzureKeyVaultKey -VaultName \$vaultName -Name\$keyVaultKeyName -Verbose -Destination Software

<span data-ttu-id="aed24-135">Hello ниже приведен вывод hello hello *Add-AzureKeyVaultKey* командлета:</span><span class="sxs-lookup"><span data-stu-id="aed24-135">hello following is hello output of hello *Add-AzureKeyVaultKey* cmdlet:</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

<span data-ttu-id="aed24-136">Теперь можно ссылаться на этот ключ, созданные или переданные tooAzure хранилище ключей с помощью URI-адрес.</span><span class="sxs-lookup"><span data-stu-id="aed24-136">You can now reference this key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="aed24-137">Используйте **https://vault010.vault.local.azurestack.global:443, ключи/keyVaultKeyName001** tooalways получить текущую версию hello; и использовать **https://vault010.vault.local.azurestack.global:443/ключи / keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** tooget этой конкретной версии.</span><span class="sxs-lookup"><span data-stu-id="aed24-137">Use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001** tooalways get hello current version; and use **https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff** tooget this specific version.</span></span>

### <a name="retrieving-a-key"></a><span data-ttu-id="aed24-138">Получение ключа</span><span class="sxs-lookup"><span data-stu-id="aed24-138">Retrieving a key</span></span>
<span data-ttu-id="aed24-139">Используйте hello **Get-AzureKeyVaultKey** tooretrieve Здравствуйте, ключ и сведения о нем в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="aed24-139">Use hello **Get-AzureKeyVaultKey** tooretrieve a key and its details per hello following example:</span></span>

    Get-AzureKeyVaultKey -VaultName vault010 -Name keyVaultKeyName001

<span data-ttu-id="aed24-140">Вот hello выходные данные Get-AzureKeyVaultKey Hello</span><span class="sxs-lookup"><span data-stu-id="aed24-140">hello following is hello output of Get-AzureKeyVaultKey</span></span>

    Attributes : Microsoft.Azure.Commands.KeyVault.Models.KeyAttributes
    Key : {"kid":"https://vault010.vault.local.azurestack.global/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff","kty":"RSA","key\_ops":\["encrypt"
    ,"decrypt","sign","verify","wrapKey","unwrapKey"\],"n":"nDkcBQCyyLnXtbwFMnXOWzPDqWKiyjf0G3QTxvuN\_MansEn9X-91q4\_WFmRBCd5zWBqz671iuZO\_D4r0P25
    Fe2lAq\_3T1gATVNGR7LTEU9W5h8AoY10bmt4e0y66Jn2vUV-UTCz4\_vtKSKoiuNXHFR\_tGZ-6YX-frqKIiC8pbE4Qvz1x-c7E-eM\_Cpu87koL95n-Hl3wQRQRPXEPRR6gcHR5E74D1
    gLEFCWKySTo4nXtLoeBMNK5QYEBZIAS61ACbR4czjHn6ty-tZeVTc7hyK\_UO2EbJovQIAhyayfq018uNtCBzjjkqJKnY34kviVCPoTQqOdpHa0FHrloe5FeIw","e":"AQAB"}
    VaultName : vault010
    Name : keyVaultKeyName001
    Version : 86062b02b10342688f3b0b3713e343ff
    Id : https://vault010.vault.local.azurestack.global:443/keys/keyVaultKeyName001/86062b02b10342688f3b0b3713e343ff

### <a name="setting-a-secret"></a><span data-ttu-id="aed24-141">Задание секрета</span><span class="sxs-lookup"><span data-stu-id="aed24-141">Setting a secret</span></span>
    $secretvalue = ConvertTo-SecureString 'User@123' -AsPlainText -Force
    Set-AzureKeyVaultSecret -Name MySecret-VaultName vault010 -SecretValue $secretvalue

<span data-ttu-id="aed24-142">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="aed24-142">Output</span></span>

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

### <a name="retrieving-a-secret"></a><span data-ttu-id="aed24-143">Получение секрета</span><span class="sxs-lookup"><span data-stu-id="aed24-143">Retrieving a secret</span></span>
    Get-AzureKeyVaultSecret -VaultName vault010

<span data-ttu-id="aed24-144">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="aed24-144">Output</span></span>

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

<span data-ttu-id="aed24-145">Теперь хранилища ключей и ключа или секрета готова для toouse приложений.</span><span class="sxs-lookup"><span data-stu-id="aed24-145">Now, your key vault and key or secret is ready for applications toouse.</span></span>
<span data-ttu-id="aed24-146">Toouse приложений необходимо авторизовать их.</span><span class="sxs-lookup"><span data-stu-id="aed24-146">You must authorize applications toouse them.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="aed24-147">Авторизовать hello приложения toouse hello ключа или секрета</span><span class="sxs-lookup"><span data-stu-id="aed24-147">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="aed24-148">tooaccess приложения hello tooauthorize hello ключа или секрета в хранилище hello, используйте hello Set -**AzureRmKeyVaultAccessPolicy** командлета.</span><span class="sxs-lookup"><span data-stu-id="aed24-148">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello Set-**AzureRmKeyVaultAccessPolicy** cmdlet.</span></span>

<span data-ttu-id="aed24-149">Например, если имя хранилища — *ContosoKeyVault* и hello приложение имеет tooauthorize *идентификатор клиента* из *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*и вы хотите toodecrypt приложения hello tooauthorize и войдите с ключами в хранилище, выполните следующие hello:</span><span class="sxs-lookup"><span data-stu-id="aed24-149">For example, if your vault name is *ContosoKeyVault* and hello application you want tooauthorize has a *Client ID* of *8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed*, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, run hello following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign

<span data-ttu-id="aed24-150">Tooauthorize этой же tooread секреты приложения в хранилище, выполните следующие hello:</span><span class="sxs-lookup"><span data-stu-id="aed24-150">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToSecrets Get


## <a name="next-steps"></a><span data-ttu-id="aed24-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="aed24-151">Next steps</span></span>
[<span data-ttu-id="aed24-152">Развертывание виртуальной машины с помощью пароля из хранилища ключей</span><span class="sxs-lookup"><span data-stu-id="aed24-152">Deploy a VM with a Key Vault password</span></span>](azure-stack-kv-deploy-vm-with-secret.md)

[<span data-ttu-id="aed24-153">Развертывание виртуальной Машины с помощью хранилища ключей сертификата</span><span class="sxs-lookup"><span data-stu-id="aed24-153">Deploy a VM with a Key Vault certificate</span></span>](azure-stack-kv-push-secret-into-vm.md)

