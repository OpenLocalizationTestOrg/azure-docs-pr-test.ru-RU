---
title: "aaaUse PowerShell tooback копировании и восстановлении приложений служб приложений"
description: "Узнайте, как toouse PowerShell tooback копировании и восстановлении приложения в службе приложений Azure"
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>Использование PowerShell tooback и восстановление приложения служб приложений
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [REST API](../app-service-web/websites-csm-backup.md)
> 
> 

Узнайте, как Azure PowerShell tooback toouse копировании и восстановлении [приложения служб приложений](https://azure.microsoft.com/services/app-service/web/). Дополнительные сведения о резервных копиях веб-приложений, включая требования и ограничения, см. в статье [Резервное копирование веб-приложений в службе приложений Azure](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Предварительные требования
toouse PowerShell toomanage резервных копий приложения необходимо hello следующие:

* **URL-адрес SAS** , разрешает чтение и контейнер хранилища Azure tooan доступ для записи. В разделе [основные сведения о модели SAS hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md) объяснение URL-адреса SAS. С примерами управления службой хранилища Azure с помощью PowerShell можно ознакомиться в статье [Использование Azure PowerShell со службой хранилища Azure](../storage/common/storage-powershell-guide-full.md).
* **Строка подключения базы данных** Если tooback копии базы данных вместе с веб-приложения.

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>Как командлеты резервного копирования toogenerate toouse URL-адрес SAS с веб-приложения hello
Подписанный URL-адрес можно создать с помощью PowerShell. Ниже приведен пример как toogenerate один, который может использоваться с командлетами hello рассматриваемые в данной статье.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Установка Azure PowerShell 1.3.2 или более поздней версии
Инструкции по установке и использованию Azure PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).

## <a name="create-a-backup"></a>Создание резервной копии
Используйте командлет New-AzureRmWebAppBackup hello toocreate резервной копии веб-приложения.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Он создает резервную копию, имя которой присваивается автоматически. Если вы хотите tooprovide имя для резервного копирования, используйте hello BackupName необязательный параметр.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude базы данных в резервной копии hello, сначала создайте с помощью командлета New-AzureRmWebAppDatabaseBackupSetting hello параметр резервного копирования базы данных, а затем указать, что установка значения в hello баз данных параметр командлета New-AzureRmWebAppBackup hello. параметр базы данных Hello принимает массив параметров базы данных, позволяя tooback более чем одной базы данных.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Получение резервных копий
командлет Get-AzureRmWebAppBackupList Hello возвращает массив всех резервных копий для веб-приложения. Необходимо указать имя веб-приложения hello hello и ее группа ресурсов.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

tooget заданной резервной копии с помощью командлета Get-AzureRmWebAppBackup hello.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

Можно также передать объект web app в hello командлетов управления резервным копированием для удобства.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Планирование автоматического резервного копирования
Можно запланировать toohappen резервные копии автоматически с заданным интервалом. tooconfigure расписания резервного копирования, с помощью командлета hello AzureRmWebAppBackupConfiguration редактирования. Этот командлет принимает несколько параметров.

* **Имя** - hello имя веб-приложения hello.
* **ResourceGroupName** — hello имя hello ресурсов группы содержащего hello веб-приложения.
* **Slot** — необязательный параметр. Имя слота приложения hello web Hello.
* **StorageAccountUrl** -hello URL-адрес SAS для контейнера хранилища Azure hello использовать резервные копии toostore hello.
* **FrequencyInterval** -как часто hello резервные копии должны вноситься числовое значение. Принимаются только положительные целые числа.
* **FrequencyUnit** -единица времени для частоты hello резервные копии следует сделать. Допустимые варианты: Hour (часы) и Day (дни).
* **RetentionPeriodInDays** — количество дней, hello автоматического резервного копирования следует сохранить, прежде чем они будут автоматически удалены.
* **StartTime** — необязательный параметр. Hello время начала автоматической архивации hello. Если это поле имеет значение NULL, то архивация начинается немедленно. Принимаются значения в формате DateTime.
* **Databases** — необязательный параметр. Массив DatabaseBackupSettings для hello toobackup баз данных.
* **KeepAtLeastOneBackup** — необязательный параметр. Введите это Если одной резервной копии следует всегда хранить в hello учетной записи хранилища, независимо от того, насколько стара он является.

Ниже приведен пример того, как toouse этого командлета.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget hello текущее расписание резервного копирования, используйте командлет Get-AzureRmWebAppBackupConfiguration hello. Это может быть полезно для изменения уже настроенного графика.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Восстановление веб-приложения из резервной копии
toorestore веб-приложения из резервной копии, используйте командлет hello AzureRmWebAppBackup восстановления. Самый простой способ toouse Hello этого командлета является toopipe в резервной копии объекта, полученного из командлета Get-AzureRmWebAppBackup hello или командлет Get-AzureRmWebAppBackupList.

После резервного копирования объекта, его можно передать в командлет Restore-AzureRmWebAppBackup hello. Укажите, следует присвоить toooverwrite содержимое веб-приложения hello с hello содержимое резервной копии hello параметр tooindicate hello перезаписи коммутатора. Если резервная копия hello содержит базы данных, также восстанавливаются этих баз данных.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Ниже приведен пример как toouse hello AzureRmWebAppBackup восстановления путем указания всех параметров hello.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>удаление резервной копии;
toodelete резервной копии с помощью командлета Remove-AzureRmWebAppBackup hello. Эта функция удаляет hello резервной копии из вашей учетной записи хранилища. Укажите имя приложения, ее группа ресурсов и идентификатор hello hello резервного копирования требуется toodelete.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

Можно также передать объект резервного копирования в toodelete командлет Remove-AzureRmWebAppBackup hello его.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
