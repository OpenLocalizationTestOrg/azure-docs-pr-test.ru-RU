---
title: "aaaManage хранилище ключей Azure стека с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toomanage хранилище ключей Azure стека с помощью PowerShell."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 37adddf8da02766559f4d61134a9d5ce47377da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-in-azure-stack-using-powershell"></a><span data-ttu-id="8f0e4-103">Управление хранилищем ключей Azure стека с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f0e4-103">Manage Key Vault in Azure Stack using PowerShell</span></span>

<span data-ttu-id="8f0e4-104">Эта статья поможет вам получить toocreate работы и управление хранилищем ключей Azure стека с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-104">This article helps you get started toocreate and manage Key Vault in Azure Stack by using PowerShell.</span></span> <span data-ttu-id="8f0e4-105">командлеты PowerShell ключ хранилища Hello, описанных в этой статье доступны как часть hello Azure PowerShell SDK.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-105">hello Key Vault PowerShell cmdlets described in this article are available as a part of hello Azure PowerShell SDK.</span></span> <span data-ttu-id="8f0e4-106">Hello следующих разделах описаны командлеты PowerShell hello, которые требуется toocreate хранилища, хранения и управлять криптографические ключи и секретные данные, а также разрешают операции tooinvoke пользователи или приложения в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-106">hello following sections describe hello PowerShell cmdlets that are required toocreate a vault, store, and manage cryptographic keys and secrets as well as authorize users or applications tooinvoke operations in hello vault.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8f0e4-107">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8f0e4-107">Prerequisites</span></span>
* [<span data-ttu-id="8f0e4-108">Установка PowerShell Azure стека.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-108">Install PowerShell for Azure Stack.</span></span>](azure-stack-powershell-install.md)  
* <span data-ttu-id="8f0e4-109">Администраторов облака Azure стек должен иметь [создать предложение](azure-stack-create-offer.md) , включающего службы хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-109">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="8f0e4-110">Пользователи должны [подписаться предложение tooan](azure-stack-subscribe-plan-provision-vm.md) , включающего службы хранилища ключей hello.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-110">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span> 
* [<span data-ttu-id="8f0e4-111">Настройка среды PowerShell hello Azure стека пользователя</span><span class="sxs-lookup"><span data-stu-id="8f0e4-111">Configure hello Azure Stack user's PowerShell environment</span></span>](azure-stack-powershell-configure-user.md)

## <a name="enable-your-tenant-subscription-for-vault-operations"></a><span data-ttu-id="8f0e4-112">Включите вашу подписку клиента для операций хранилища</span><span class="sxs-lookup"><span data-stu-id="8f0e4-112">Enable your tenant subscription for vault operations</span></span>

<span data-ttu-id="8f0e4-113">Прежде чем можно выполнять все операции с хранилищем ключей, необходимо tooensure которой включены подписки клиента операций в хранилище.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-113">Before you can issue any operations against a key vault, you need tooensure that your tenant subscription is enabled for vault operations.</span></span> <span data-ttu-id="8f0e4-114">tooverify запуска hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="8f0e4-114">tooverify, run hello following command:</span></span>

```PowerShell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault | ft -Autosize
```
<span data-ttu-id="8f0e4-115">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="8f0e4-115">**Output**</span></span>

<span data-ttu-id="8f0e4-116">Если подписки включены предупреждения об операциях хранилища, hello выходных данных отображается «RegistrationState» равно «Зарегистрированные» для всех типов ресурсов хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-116">If your subscription is enabled for vault operations, hello output shows “RegistrationState” equals “Registered” for all resource types of a key vault.</span></span>

![Состояние регистрации](media/azure-stack-kv-manage-powershell/image1.png)

<span data-ttu-id="8f0e4-118">Если это не так hello, вызовите hello, следующая команда tooregister службы хранилища ключей hello в подписке:</span><span class="sxs-lookup"><span data-stu-id="8f0e4-118">If that’s not hello case, invoke hello following command tooregister hello Key Vault service in your subscription:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.KeyVault
```

<span data-ttu-id="8f0e4-119">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="8f0e4-119">**Output**</span></span>

<span data-ttu-id="8f0e4-120">При успешном выполнении регистрации hello hello следующие выходные данные возвращаются в:</span><span class="sxs-lookup"><span data-stu-id="8f0e4-120">If hello registration is successful, hello following output is returned:</span></span>

![Регистрация](media/azure-stack-kv-manage-powershell/image2.png)

<span data-ttu-id="8f0e4-122">Hello следующих разделах предполагается, что служба хранилища ключей зарегистрирована в рамках подписки пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-122">hello following sections assume Key Vault service is registered within hello user subscription.</span></span> <span data-ttu-id="8f0e4-123">При вызове команды хранилища ключей, если возникли ошибка - «hello подписки не зарегистрированного toouse пространством имен "Microsoft.KeyVault», убедитесь, что имеется [включен поставщика ресурсов хранилища ключей hello](#enable-your-tenant-subscription-for-vault-operations) согласно инструкциям, приведенным Приведенные выше.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-123">When invoking key vault commands, if you get an error- "hello subscription is not registered toouse namespace ‘Microsoft.KeyVault" then, confirm that you have [enabled hello Key Vault resource provider](#enable-your-tenant-subscription-for-vault-operations) as per instructions mentioned earlier.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="8f0e4-124">Создайте хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-124">Create a key vault</span></span> 

<span data-ttu-id="8f0e4-125">Прежде чем создавать хранилища ключей, создайте группу ресурсов, чтобы все хранилища ключей, касающиеся ресурсы находятся в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-125">Before you create a key vault, create a resource group so that all key vault related resources exist in a resource group.</span></span> <span data-ttu-id="8f0e4-126">Используйте hello, следующая команда toocreate новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-126">Use hello following command toocreate a new resource group:</span></span>

```PowerShell
New-AzureRmResourceGroup -Name “VaultRG” -Location local -verbose -Force

```

<span data-ttu-id="8f0e4-127">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="8f0e4-127">**Output**</span></span>

![Создание группы ресурсов](media/azure-stack-kv-manage-powershell/image3.png)

<span data-ttu-id="8f0e4-129">Теперь воспользуйтесь hello **New AzureRMKeyVault** toocreate команда хранилища ключей в группе ресурсов hello, которое было создано ранее.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-129">Now, use hello **New-AzureRMKeyVault** command toocreate a key vault in hello resource group that you created earlier.</span></span> <span data-ttu-id="8f0e4-130">Эта команда считывает три имя группы ресурсов обязательные параметры, имя хранилища ключей и географическое расположение.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-130">This command reads three mandatory parameters- resource group name, key vault name, and geographic location.</span></span> 

<span data-ttu-id="8f0e4-131">Выполните следующие команды toocreate hello хранилища ключей:</span><span class="sxs-lookup"><span data-stu-id="8f0e4-131">Run hello following command toocreate a key vault:</span></span>

```PowerShell
New-AzureRmKeyVault -VaultName “Vault01” -ResourceGroupName “VaultRG” -Location local -verbose
```
<span data-ttu-id="8f0e4-132">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="8f0e4-132">**Output**</span></span>

![новый кв](media/azure-stack-kv-manage-powershell/image4.png)

<span data-ttu-id="8f0e4-134">выходные данные этой команды Hello отображает свойства hello hello хранилища ключей, который вы создали.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-134">hello output of this command shows hello properties of hello key vault that you created.</span></span> <span data-ttu-id="8f0e4-135">Когда приложение получает доступ к этому хранилищу, он использует hello **URI хранилища** свойства, показанного в выходных данных hello.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-135">When an application accesses this vault, it uses hello **Vault URI** property shown in hello output.</span></span> <span data-ttu-id="8f0e4-136">Например, здесь хранилище hello URI является **https://vault01.vault.local.azurestack.external**.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-136">For example, hello vault URI here is **https://vault01.vault.local.azurestack.external**.</span></span> <span data-ttu-id="8f0e4-137">Приложений, взаимодействующих с этим хранилищем ключей через REST API необходимо использовать этот URI.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-137">Applications interacting with this key vault through REST API must use this URI.</span></span>

<span data-ttu-id="8f0e4-138">В развертывании на основе служб федерации Active Directory при создании хранилища ключей с помощью PowerShell, может появиться предупреждение об ошибке «политика доступа не установлена.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-138">In ADFS-based deployments, when you create a key vault by using PowerShell, you might receive a warning that says "Access policy is not set.</span></span> <span data-ttu-id="8f0e4-139">Не пользователя или приложения имеет toouse разрешение доступа к этим хранилищем».</span><span class="sxs-lookup"><span data-stu-id="8f0e4-139">No user or application has access permission toouse this vault".</span></span> <span data-ttu-id="8f0e4-140">tooresolve эту проблему, задайте политику доступа для hello хранилища с помощью hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) команды:</span><span class="sxs-lookup"><span data-stu-id="8f0e4-140">tooresolve this issue, set an access policy for hello vault by using hello [Set-AzureRmKeyVaultAccessPolicy](azure-stack-kv-manage-powershell.md#authorize-an-application-to-use-a-key-or-secret) command:</span></span>

```PowerShell
# Obtain hello security identifier(SID) of hello active directory user
$adUser = Get-ADUser -Filter "Name -eq '{Active directory user name}'"
$objectSID = $adUser.SID.Value 

#Set hello key vault access policy
Set-AzureRmKeyVaultAccessPolicy -VaultName "{key vault name}" -ResourceGroupName "{resource group name}" -ObjectId "{object SID}" -PermissionsToKeys {permissionsToKeys} -PermissionsToSecrets {permissionsToSecrets} -BypassObjectIdValidation 
```

## <a name="manage-keys-and-secrets"></a><span data-ttu-id="8f0e4-141">Управление ключами и секретов</span><span class="sxs-lookup"><span data-stu-id="8f0e4-141">Manage keys and secrets</span></span>

<span data-ttu-id="8f0e4-142">После создания хранилища, используйте следующие шаги toocreate hello и управление ими ключи и секретные данные в хранилище hello.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-142">After creating a vault, use hello following steps toocreate and manage keys and secrets within hello vault.</span></span>

### <a name="create-a-key"></a><span data-ttu-id="8f0e4-143">Создание ключа</span><span class="sxs-lookup"><span data-stu-id="8f0e4-143">Create a key</span></span>

<span data-ttu-id="8f0e4-144">Используйте hello **Add-AzureKeyVaultKey** команды toocreate или импортируйте программное обеспечение защищенного ключа в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-144">Use hello **Add-AzureKeyVaultKey** command toocreate or import a software protected key in a key vault.</span></span> 

```PowerShell
Add-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01” -verbose -Destination Software
```
<span data-ttu-id="8f0e4-145">Hello **назначения** используется параметр toospecify разделу hello — защищенного программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-145">hello **Destination** parameter is used toospecify that hello key is software protected.</span></span> <span data-ttu-id="8f0e4-146">Если ключ hello успешно создана, hello команда выводит hello подробные сведения о hello ключ создан.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-146">When hello key is successfully created, hello command outputs hello details of hello created key.</span></span>

<span data-ttu-id="8f0e4-147">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="8f0e4-147">**Output**</span></span>

![Новый ключ](media/azure-stack-kv-manage-powershell/image5.png)

<span data-ttu-id="8f0e4-149">Теперь можно создать ссылку hello ключ создан с помощью URI-адрес.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-149">You can now reference hello created key by using its URI.</span></span> <span data-ttu-id="8f0e4-150">Если при создании или импорте ключ, который имеет совпадает с именем существующего ключа, со значениями hello, заданные в новый ключ hello обновляется hello исходного ключа.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-150">If you create or import a key that has same name as an existing key, hello original key is updated with hello values that are specified in hello new key.</span></span>  <span data-ttu-id="8f0e4-151">Доступ к предыдущей версии hello с помощью конкретной версии hello URI hello ключа.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-151">You can access hello previous version by using hello version-specific URI of hello key.</span></span> <span data-ttu-id="8f0e4-152">Например,</span><span class="sxs-lookup"><span data-stu-id="8f0e4-152">For example,</span></span> 

* <span data-ttu-id="8f0e4-153">Используйте **https://vault10.vault.local.azurestack.external:443, ключи/key01** tooalways получить текущую версию hello</span><span class="sxs-lookup"><span data-stu-id="8f0e4-153">Use **https://vault10.vault.local.azurestack.external:443/keys/key01** tooalways get hello current version</span></span>  
* <span data-ttu-id="8f0e4-154">Используйте **https://vault010.vault.local.azurestack.external:443/ключи/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget этой конкретной версии</span><span class="sxs-lookup"><span data-stu-id="8f0e4-154">Use **https://vault010.vault.local.azurestack.external:443/keys/key01/d0b36ee2e3d14e9f967b8b6b1d38938a** tooget this specific version</span></span>

### <a name="get-a-key"></a><span data-ttu-id="8f0e4-155">Получить ключ</span><span class="sxs-lookup"><span data-stu-id="8f0e4-155">Get a key</span></span>

<span data-ttu-id="8f0e4-156">Используйте hello **Get-AzureKeyVaultKey** команды tooread ключ и сведения о нем.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-156">Use hello **Get-AzureKeyVaultKey** command tooread a key and its details.</span></span>

```PowerShell
Get-AzureKeyVaultKey -VaultName “Vault01” -Name “Key01”
```

### <a name="create-a-secret"></a><span data-ttu-id="8f0e4-157">Создание секрета</span><span class="sxs-lookup"><span data-stu-id="8f0e4-157">Create a secret</span></span>

<span data-ttu-id="8f0e4-158">Используйте hello **AzureKeyVaultSecret набор** команду toocreate или обновление секрета в хранилище.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-158">Use hello **Set-AzureKeyVaultSecret** command toocreate or update a secret in a vault.</span></span> <span data-ttu-id="8f0e4-159">Секрет создается в том случае, если он еще не существует, а новая версия секрета hello создается в том случае, если он уже существует.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-159">A secret is created if it doesn’t already exist, and a new version of hello secret is created if it already exists.</span></span>

```PowerShell
$secretvalue = ConvertTo-SecureString “User@123” -AsPlainText -Force
Set-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01” -SecretValue $secretvalue
```

<span data-ttu-id="8f0e4-160">**Выходные данные**</span><span class="sxs-lookup"><span data-stu-id="8f0e4-160">**Output**</span></span>

![Создание секрета](media/azure-stack-kv-manage-powershell/image6.png)

### <a name="get-a-secret"></a><span data-ttu-id="8f0e4-162">Получить секрет</span><span class="sxs-lookup"><span data-stu-id="8f0e4-162">Get a secret</span></span>

<span data-ttu-id="8f0e4-163">Используйте hello **Get AzureKeyVaultSecret** tooread команда секрет в хранилище ключей.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-163">Use hello **Get-AzureKeyVaultSecret** command tooread a secret in a key vault.</span></span> <span data-ttu-id="8f0e4-164">Эта команда может возвращать все или некоторые версии секрета.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-164">This command can return all or specific versions of a secret.</span></span> 

```PowerShell
Get-AzureKeyVaultSecret -VaultName “Vault01” -Name “Secret01”
```

<span data-ttu-id="8f0e4-165">После создания ключи и секретные коды, вы можете разрешить внешние приложения toouse их.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-165">After creating keys and secrets, you can authorize external applications toouse them.</span></span>

## <a name="authorize-an-application-toouse-a-key-or-secret"></a><span data-ttu-id="8f0e4-166">Авторизовать приложение toouse ключа или секрета</span><span class="sxs-lookup"><span data-stu-id="8f0e4-166">Authorize an application toouse a key or secret</span></span>

<span data-ttu-id="8f0e4-167">tooauthorize приложения tooaccess ключа или секрета в hello ключа хранилища, используйте hello **Set-AzureRmKeyVaultAccessPolicy** команды.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-167">tooauthorize an application tooaccess a key or secret in hello key vault, use hello **Set-AzureRmKeyVaultAccessPolicy** command.</span></span>
<span data-ttu-id="8f0e4-168">Например если имя хранилища — ContosoKeyVault и hello приложения вы хотите tooauthorize имеет идентификатор клиента 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-168">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a Client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed.</span></span> <span data-ttu-id="8f0e4-169">Выполните следующие команды tooauthorize hello приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8f0e4-169">Run hello following command tooauthorize hello application.</span></span> <span data-ttu-id="8f0e4-170">Кроме того, можно указать hello **PermissionsToKeys** параметр tooset разрешения для пользователя, приложения или группы безопасности:</span><span class="sxs-lookup"><span data-stu-id="8f0e4-170">Optionally, you can specify hello **PermissionsToKeys** parameter tooset permissions for a user, application, or a security group:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed -PermissionsToKeys decrypt,sign
```

<span data-ttu-id="8f0e4-171">Если требуется tooauthorize этой же tooread секреты приложения в хранилище, выполните следующий командлет hello:</span><span class="sxs-lookup"><span data-stu-id="8f0e4-171">If you want tooauthorize that same application tooread secrets in your vault, run hello following cmdlet:</span></span>

```PowerShell
Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -ServicePrincipalName 8f8c4bbd-485b-45fd-98f7-ec6300 -PermissionsToKeys Get
```

## <a name="next-steps"></a><span data-ttu-id="8f0e4-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8f0e4-172">Next Steps</span></span>
* [<span data-ttu-id="8f0e4-173">Развертывание виртуальной Машины с помощью пароля, хранящихся в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="8f0e4-173">Deploy a VM with password stored in a Key Vault</span></span>](azure-stack-kv-deploy-vm-with-secret.md)  
* [<span data-ttu-id="8f0e4-174">Развертывание виртуальной Машины с сертификатом, который хранится в хранилище ключей</span><span class="sxs-lookup"><span data-stu-id="8f0e4-174">Deploy a VM with certificate stored in Key Vault</span></span>](azure-stack-kv-push-secret-into-vm.md) 
