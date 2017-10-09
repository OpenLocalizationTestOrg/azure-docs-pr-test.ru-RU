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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="e0d7d-103">Использование PowerShell tooback и восстановление приложения служб приложений</span><span class="sxs-lookup"><span data-stu-id="e0d7d-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0d7d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0d7d-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="e0d7d-105">REST API</span><span class="sxs-lookup"><span data-stu-id="e0d7d-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="e0d7d-106">Узнайте, как Azure PowerShell tooback toouse копировании и восстановлении [приложения служб приложений](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="e0d7d-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="e0d7d-107">Дополнительные сведения о резервных копиях веб-приложений, включая требования и ограничения, см. в статье [Резервное копирование веб-приложений в службе приложений Azure](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e0d7d-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0d7d-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e0d7d-108">Prerequisites</span></span>
<span data-ttu-id="e0d7d-109">toouse PowerShell toomanage резервных копий приложения необходимо hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e0d7d-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="e0d7d-110">**URL-адрес SAS** , разрешает чтение и контейнер хранилища Azure tooan доступ для записи.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="e0d7d-111">В разделе [основные сведения о модели SAS hello](../storage/common/storage-dotnet-shared-access-signature-part-1.md) объяснение URL-адреса SAS.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="e0d7d-112">С примерами управления службой хранилища Azure с помощью PowerShell можно ознакомиться в статье [Использование Azure PowerShell со службой хранилища Azure](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="e0d7d-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="e0d7d-113">**Строка подключения базы данных** Если tooback копии базы данных вместе с веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="e0d7d-114">Как командлеты резервного копирования toogenerate toouse URL-адрес SAS с веб-приложения hello</span><span class="sxs-lookup"><span data-stu-id="e0d7d-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="e0d7d-115">Подписанный URL-адрес можно создать с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="e0d7d-116">Ниже приведен пример как toogenerate один, который может использоваться с командлетами hello рассматриваемые в данной статье.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="e0d7d-117">Установка Azure PowerShell 1.3.2 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="e0d7d-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="e0d7d-118">Инструкции по установке и использованию Azure PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0d7d-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="e0d7d-119">Создание резервной копии</span><span class="sxs-lookup"><span data-stu-id="e0d7d-119">Create a backup</span></span>
<span data-ttu-id="e0d7d-120">Используйте командлет New-AzureRmWebAppBackup hello toocreate резервной копии веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="e0d7d-121">Он создает резервную копию, имя которой присваивается автоматически.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="e0d7d-122">Если вы хотите tooprovide имя для резервного копирования, используйте hello BackupName необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="e0d7d-123">tooinclude базы данных в резервной копии hello, сначала создайте с помощью командлета New-AzureRmWebAppDatabaseBackupSetting hello параметр резервного копирования базы данных, а затем указать, что установка значения в hello баз данных параметр командлета New-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="e0d7d-124">параметр базы данных Hello принимает массив параметров базы данных, позволяя tooback более чем одной базы данных.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="e0d7d-125">Получение резервных копий</span><span class="sxs-lookup"><span data-stu-id="e0d7d-125">Get backups</span></span>
<span data-ttu-id="e0d7d-126">командлет Get-AzureRmWebAppBackupList Hello возвращает массив всех резервных копий для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="e0d7d-127">Необходимо указать имя веб-приложения hello hello и ее группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="e0d7d-128">tooget заданной резервной копии с помощью командлета Get-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="e0d7d-129">Можно также передать объект web app в hello командлетов управления резервным копированием для удобства.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="e0d7d-130">Планирование автоматического резервного копирования</span><span class="sxs-lookup"><span data-stu-id="e0d7d-130">Schedule automatic backups</span></span>
<span data-ttu-id="e0d7d-131">Можно запланировать toohappen резервные копии автоматически с заданным интервалом.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="e0d7d-132">tooconfigure расписания резервного копирования, с помощью командлета hello AzureRmWebAppBackupConfiguration редактирования.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="e0d7d-133">Этот командлет принимает несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="e0d7d-134">**Имя** - hello имя веб-приложения hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="e0d7d-135">**ResourceGroupName** — hello имя hello ресурсов группы содержащего hello веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="e0d7d-136">**Slot** — необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-136">**Slot** - Optional.</span></span> <span data-ttu-id="e0d7d-137">Имя слота приложения hello web Hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="e0d7d-138">**StorageAccountUrl** -hello URL-адрес SAS для контейнера хранилища Azure hello использовать резервные копии toostore hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="e0d7d-139">**FrequencyInterval** -как часто hello резервные копии должны вноситься числовое значение.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="e0d7d-140">Принимаются только положительные целые числа.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-140">Must be a positive integer.</span></span>
* <span data-ttu-id="e0d7d-141">**FrequencyUnit** -единица времени для частоты hello резервные копии следует сделать.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="e0d7d-142">Допустимые варианты: Hour (часы) и Day (дни).</span><span class="sxs-lookup"><span data-stu-id="e0d7d-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="e0d7d-143">**RetentionPeriodInDays** — количество дней, hello автоматического резервного копирования следует сохранить, прежде чем они будут автоматически удалены.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="e0d7d-144">**StartTime** — необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-144">**StartTime** - Optional.</span></span> <span data-ttu-id="e0d7d-145">Hello время начала автоматической архивации hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="e0d7d-146">Если это поле имеет значение NULL, то архивация начинается немедленно.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="e0d7d-147">Принимаются значения в формате DateTime.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-147">Must be a DateTime.</span></span>
* <span data-ttu-id="e0d7d-148">**Databases** — необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-148">**Databases** - Optional.</span></span> <span data-ttu-id="e0d7d-149">Массив DatabaseBackupSettings для hello toobackup баз данных.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="e0d7d-150">**KeepAtLeastOneBackup** — необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="e0d7d-151">Введите это Если одной резервной копии следует всегда хранить в hello учетной записи хранилища, независимо от того, насколько стара он является.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="e0d7d-152">Ниже приведен пример того, как toouse этого командлета.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="e0d7d-153">tooget hello текущее расписание резервного копирования, используйте командлет Get-AzureRmWebAppBackupConfiguration hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="e0d7d-154">Это может быть полезно для изменения уже настроенного графика.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="e0d7d-155">Восстановление веб-приложения из резервной копии</span><span class="sxs-lookup"><span data-stu-id="e0d7d-155">Restore a web app from a backup</span></span>
<span data-ttu-id="e0d7d-156">toorestore веб-приложения из резервной копии, используйте командлет hello AzureRmWebAppBackup восстановления.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="e0d7d-157">Самый простой способ toouse Hello этого командлета является toopipe в резервной копии объекта, полученного из командлета Get-AzureRmWebAppBackup hello или командлет Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="e0d7d-158">После резервного копирования объекта, его можно передать в командлет Restore-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="e0d7d-159">Укажите, следует присвоить toooverwrite содержимое веб-приложения hello с hello содержимое резервной копии hello параметр tooindicate hello перезаписи коммутатора.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="e0d7d-160">Если резервная копия hello содержит базы данных, также восстанавливаются этих баз данных.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="e0d7d-161">Ниже приведен пример как toouse hello AzureRmWebAppBackup восстановления путем указания всех параметров hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="e0d7d-162">удаление резервной копии;</span><span class="sxs-lookup"><span data-stu-id="e0d7d-162">Delete a backup</span></span>
<span data-ttu-id="e0d7d-163">toodelete резервной копии с помощью командлета Remove-AzureRmWebAppBackup hello.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="e0d7d-164">Эта функция удаляет hello резервной копии из вашей учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="e0d7d-165">Укажите имя приложения, ее группа ресурсов и идентификатор hello hello резервного копирования требуется toodelete.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="e0d7d-166">Можно также передать объект резервного копирования в toodelete командлет Remove-AzureRmWebAppBackup hello его.</span><span class="sxs-lookup"><span data-stu-id="e0d7d-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
