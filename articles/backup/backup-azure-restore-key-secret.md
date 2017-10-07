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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Восстановление ключа и секрета в хранилище ключей для зашифрованных виртуальных машин с помощью службы архивации Azure
В данной статье рассмотрен с помощью резервного копирования виртуальных Машин Azure tooperform восстановления зашифрованных виртуальных машин Azure, если ключ и секрет, не существует в хранилище ключей hello. Эти шаги можно использовать также в том случае, если необходимо, чтобы toomaintain отдельную копию ключа шифрования (клавиша) и секрет (ключ шифрования BitLocker) для hello восстановления виртуальной Машины.

## <a name="prerequisites"></a>Предварительные требования
* **Резервная копия зашифрованных виртуальных машин** — выполнять резервное копирование зашифрованных виртуальных машин Azure нужно с помощью службы архивации Azure. См. в статье hello [управлять резервное копирование и восстановление виртуальных машин Azure с помощью PowerShell](backup-azure-vms-automation.md) для получения сведений об способ toobackup шифрования виртуальных машинах Azure.
* **Настройка хранилища ключей Azure** — убедитесь, что хранилище ключей toowhich ключи и секреты необходимость toobe восстановления уже существует. См. в статье hello [Приступая к работе с хранилищем ключей Azure](../key-vault/key-vault-get-started.md) сведения об управлении хранилищем ключей.
* **Восстановление диска** — убедитесь, что запущено задание восстановления дисков для зашифрованной виртуальной машины с помощью [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm). Это, поскольку это задание создает JSON-файла в вашей учетной записи хранилища, содержащий ключи и секретные коды для toobe ВМ hello зашифрованные восстановлена.

## <a name="get-key-and-secret-from-azure-backup"></a>Получение ключа и секрета из службы Azure Backup

> [!NOTE]
> После восстановления работоспособности диска hello зашифрованных виртуальной Машины, убедитесь, что:
> 1. сведения о заданиях восстановления диска, заполняется $details, как упоминалось в [действия раздела диски восстановления hello, PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. Виртуальная машина должны быть созданы из восстановленные диски только **после восстановленной tookey хранилище ключей и секрет**.
>
>

Запрос hello восстановить свойства диска для сведений о задании hello.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Задать контекст хранилища Azure hello и восстановите файл конфигурации JSON, содержащий ключ и секретные сведения для зашифрованных виртуальной Машины.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>Ключ восстановления
После hello JSON-файл создается в путь назначения hello, упомянутых выше, создайте файл большой двоичный объект ключа из hello JSON и канала toorestore ключа командлет tooput hello ключ (ключ обмена Ключами) обратно в хранилище ключей hello.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>Восстановление секрета
Используйте файл JSON hello созданной выше tooget секретное имя и значение и канала tooset секретный командлет tooput hello секрет (BEK) в хранилище ключей hello. **Воспользуйтесь этими командлетами, если виртуальная машина зашифрована с помощью BEK и KEK.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

Если ВМ **зашифрован только с помощью BEK**, создайте файл секретный BLOB-объектов из hello JSON и канала toorestore секретный командлет tooput hello секрет (BEK) в хранилище ключей hello.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. Можно получить значение для $secretname ссылаются выходные данные toohello $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl и используя текста после секреты / например секретный выходной URL-адрес — https://keyvaultname.vault.azure.net/secrets/ Имя B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 и секретный — B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Значение тега hello DiskEncryptionKeyFileName совпадает с именем секрета.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>Создание виртуальной машины на основе восстановленного диска
Необходимо создать резервные копии зашифрованных виртуальной Машины с помощью резервной копии виртуальной Машины Azure, hello командлеты PowerShell вышеупомянутых справки необходимо восстановить ключ и хранилища ключей секретный toohello назад. После их восстановления, см. в статье hello [управлять резервное копирование и восстановление виртуальных машин Azure с помощью PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate шифрование виртуальных машин из восстановленной диска, ключ и секрет.

## <a name="legacy-approach"></a>Устаревший подход
упомянутые выше подход Hello будет работать для всех точек восстановления hello. Однако hello более старый подход получения ключа и секретные сведения из точки восстановления будет действителен для более ранней, чем 11 июля 2017 г. для виртуальных машин, зашифрованные с помощью BEK и KEK точек восстановления. После выполнения задания восстановления диска для зашифрованной виртуальной машины с помощью [PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm) убедитесь, что переменная $rp заполняется допустимым значением.

### <a name="restore-key"></a>Ключ восстановления
Используйте следующие командлеты tooget ключ (ключ обмена Ключами) сведения из точки восстановления hello и передать его tooput ключа командлет toorestore его обратно в хранилище ключей hello.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>Восстановление секрета
Используйте следующие командлеты tooget секрет (BEK) сведения из точки восстановления hello и передать его tooput секретный командлет tooset его обратно в хранилище ключей hello.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. Значение для $secretname можно получить с помощью ссылки на выходные данные toohello $rp1. KeyAndSecretDetails.SecretUrl и с помощью текста после секреты / например секретный выходной URL-адрес является https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 и секретное имя B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Значение тега hello DiskEncryptionKeyFileName совпадает с именем секрета.
> 3. Значение для DiskEncryptionKeyEncryptionKeyURL можно получить из хранилища ключей после восстановления разделы hello и с помощью [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) командлета
>
>

## <a name="next-steps"></a>Дальнейшие действия
После восстановления ключа и секретный задней tookey хранилища, см. в статье hello [управлять резервное копирование и восстановление виртуальных машин Azure с помощью PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate шифрование виртуальных машин из восстановленной диска, раздела и секрет.
