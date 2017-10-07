---
title: "ключ хранилища ключей aaaRestore и секретный код для шифрования виртуальных машин с помощью службы архивации Azure | Документы Microsoft"
description: "Дополнительные сведения о том, как в хранилище ключей toorestore ключ и секрет в службе архивации Azure с помощью PowerShell"
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="67b10-103">Восстановление ключа и секрета в хранилище ключей для зашифрованных виртуальных машин с помощью службы архивации Azure</span><span class="sxs-lookup"><span data-stu-id="67b10-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="67b10-104">В данной статье рассмотрен с помощью резервного копирования виртуальных Машин Azure tooperform восстановления зашифрованных виртуальных машин Azure, если ключ и секрет, не существует в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="67b10-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="67b10-105">Эти шаги можно использовать также в том случае, если необходимо, чтобы toomaintain отдельную копию ключа шифрования (клавиша) и секрет (ключ шифрования BitLocker) для hello восстановления виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="67b10-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67b10-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="67b10-106">Prerequisites</span></span>
* <span data-ttu-id="67b10-107">**Резервная копия зашифрованных виртуальных машин** — выполнять резервное копирование зашифрованных виртуальных машин Azure нужно с помощью службы архивации Azure.</span><span class="sxs-lookup"><span data-stu-id="67b10-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="67b10-108">См. в статье hello [управлять резервное копирование и восстановление виртуальных машин Azure с помощью PowerShell](backup-azure-vms-automation.md) для получения сведений об способ toobackup шифрования виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="67b10-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="67b10-109">**Настройка хранилища ключей Azure** — убедитесь, что хранилище ключей toowhich ключи и секреты необходимость toobe восстановления уже существует.</span><span class="sxs-lookup"><span data-stu-id="67b10-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="67b10-110">См. в статье hello [Приступая к работе с хранилищем ключей Azure](../key-vault/key-vault-get-started.md) сведения об управлении хранилищем ключей.</span><span class="sxs-lookup"><span data-stu-id="67b10-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="67b10-111">**Восстановление диска** — убедитесь, что запущено задание восстановления дисков для зашифрованной виртуальной машины с помощью [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="67b10-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="67b10-112">Это, поскольку это задание создает JSON-файла в вашей учетной записи хранилища, содержащий ключи и секретные коды для toobe ВМ hello зашифрованные восстановлена.</span><span class="sxs-lookup"><span data-stu-id="67b10-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="67b10-113">Получение ключа и секрета из службы Azure Backup</span><span class="sxs-lookup"><span data-stu-id="67b10-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="67b10-114">После восстановления работоспособности диска hello зашифрованных виртуальной Машины, убедитесь, что:</span><span class="sxs-lookup"><span data-stu-id="67b10-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="67b10-115">сведения о заданиях восстановления диска, заполняется $details, как упоминалось в [действия раздела диски восстановления hello, PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="67b10-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="67b10-116">Виртуальная машина должны быть созданы из восстановленные диски только **после восстановленной tookey хранилище ключей и секрет**.</span><span class="sxs-lookup"><span data-stu-id="67b10-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="67b10-117">Запрос hello восстановить свойства диска для сведений о задании hello.</span><span class="sxs-lookup"><span data-stu-id="67b10-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="67b10-118">Задать контекст хранилища Azure hello и восстановите файл конфигурации JSON, содержащий ключ и секретные сведения для зашифрованных виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="67b10-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="67b10-119">Ключ восстановления</span><span class="sxs-lookup"><span data-stu-id="67b10-119">Restore key</span></span>
<span data-ttu-id="67b10-120">После hello JSON-файл создается в путь назначения hello, упомянутых выше, создайте файл большой двоичный объект ключа из hello JSON и канала toorestore ключа командлет tooput hello ключ (ключ обмена Ключами) обратно в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="67b10-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="67b10-121">Восстановление секрета</span><span class="sxs-lookup"><span data-stu-id="67b10-121">Restore secret</span></span>
<span data-ttu-id="67b10-122">Используйте файл JSON hello созданной выше tooget секретное имя и значение и канала tooset секретный командлет tooput hello секрет (BEK) в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="67b10-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="67b10-123">**Воспользуйтесь этими командлетами, если виртуальная машина зашифрована с помощью BEK и KEK.**</span><span class="sxs-lookup"><span data-stu-id="67b10-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="67b10-124">Если ВМ **зашифрован только с помощью BEK**, создайте файл секретный BLOB-объектов из hello JSON и канала toorestore секретный командлет tooput hello секрет (BEK) в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="67b10-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="67b10-125">Можно получить значение для $secretname ссылаются выходные данные toohello $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl и используя текста после секреты / например секретный выходной URL-адрес — https://keyvaultname.vault.azure.net/secrets/ Имя B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 и секретный — B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="67b10-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="67b10-126">Значение тега hello DiskEncryptionKeyFileName совпадает с именем секрета.</span><span class="sxs-lookup"><span data-stu-id="67b10-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="67b10-127">Создание виртуальной машины на основе восстановленного диска</span><span class="sxs-lookup"><span data-stu-id="67b10-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="67b10-128">Необходимо создать резервные копии зашифрованных виртуальной Машины с помощью резервной копии виртуальной Машины Azure, hello командлеты PowerShell вышеупомянутых справки необходимо восстановить ключ и хранилища ключей секретный toohello назад.</span><span class="sxs-lookup"><span data-stu-id="67b10-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="67b10-129">После их восстановления, см. в статье hello [управлять резервное копирование и восстановление виртуальных машин Azure с помощью PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate шифрование виртуальных машин из восстановленной диска, ключ и секрет.</span><span class="sxs-lookup"><span data-stu-id="67b10-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="67b10-130">Устаревший подход</span><span class="sxs-lookup"><span data-stu-id="67b10-130">Legacy approach</span></span>
<span data-ttu-id="67b10-131">упомянутые выше подход Hello будет работать для всех точек восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="67b10-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="67b10-132">Однако hello более старый подход получения ключа и секретные сведения из точки восстановления будет действителен для более ранней, чем 11 июля 2017 г. для виртуальных машин, зашифрованные с помощью BEK и KEK точек восстановления.</span><span class="sxs-lookup"><span data-stu-id="67b10-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="67b10-133">После выполнения задания восстановления диска для зашифрованной виртуальной машины с помощью [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm) убедитесь, что переменная $rp заполняется допустимым значением.</span><span class="sxs-lookup"><span data-stu-id="67b10-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="67b10-134">Ключ восстановления</span><span class="sxs-lookup"><span data-stu-id="67b10-134">Restore key</span></span>
<span data-ttu-id="67b10-135">Используйте следующие командлеты tooget ключ (ключ обмена Ключами) сведения из точки восстановления hello и передать его tooput ключа командлет toorestore его обратно в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="67b10-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="67b10-136">Восстановление секрета</span><span class="sxs-lookup"><span data-stu-id="67b10-136">Restore secret</span></span>
<span data-ttu-id="67b10-137">Используйте следующие командлеты tooget секрет (BEK) сведения из точки восстановления hello и передать его tooput секретный командлет tooset его обратно в хранилище ключей hello.</span><span class="sxs-lookup"><span data-stu-id="67b10-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="67b10-138">Значение для $secretname можно получить с помощью ссылки на выходные данные toohello $rp1. KeyAndSecretDetails.SecretUrl и с помощью текста после секреты / например секретный выходной URL-адрес является https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 и секретное имя B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="67b10-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="67b10-139">Значение тега hello DiskEncryptionKeyFileName совпадает с именем секрета.</span><span class="sxs-lookup"><span data-stu-id="67b10-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="67b10-140">Значение для DiskEncryptionKeyEncryptionKeyURL можно получить из хранилища ключей после восстановления разделы hello и с помощью [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) командлета</span><span class="sxs-lookup"><span data-stu-id="67b10-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="67b10-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="67b10-141">Next steps</span></span>
<span data-ttu-id="67b10-142">После восстановления ключа и секретный задней tookey хранилища, см. в статье hello [управлять резервное копирование и восстановление виртуальных машин Azure с помощью PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate шифрование виртуальных машин из восстановленной диска, раздела и секрет.</span><span class="sxs-lookup"><span data-stu-id="67b10-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>
