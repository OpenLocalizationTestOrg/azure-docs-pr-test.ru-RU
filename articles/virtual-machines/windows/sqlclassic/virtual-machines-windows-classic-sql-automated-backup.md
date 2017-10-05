---
title: "Автоматизированная архивация для виртуальных машин SQL Server (классическая модель) | Документация Майкрософт"
description: "Описание функции автоматической архивации для SQL Server на виртуальных машинах Azure с использованием модели развертывания Resource Manager. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: f7664291c2f45c422d52f682d08dbb67ab32b099
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="ac40f-103">Автоматическая архивация SQL Server на виртуальных машинах Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="ac40f-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac40f-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="ac40f-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="ac40f-105">Классический</span><span class="sxs-lookup"><span data-stu-id="ac40f-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="ac40f-106">Служба автоматической архивации автоматически настраивает [управляемое резервное копирование на портал Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) для всех существующих и новых баз данных на виртуальной машине Azure c SQL Server 2014 Standard или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ac40f-106">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="ac40f-107">Это позволяет настроить регулярную архивацию базы данных с использованием надежного хранилища больших двоичных объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ac40f-107">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="ac40f-108">Автоматическая архивация зависит от [Расширения агента IaaS для SQL Server](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac40f-108">Automated Backup depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ac40f-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ac40f-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ac40f-110">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ac40f-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ac40f-111">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ac40f-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ac40f-112">Версию этой статьи для Resource Manager см. в статье [Автоматическая архивация SQL Server на виртуальных машинах Azure (Resource Manager)](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ac40f-112">To view the Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac40f-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ac40f-113">Prerequisites</span></span>
<span data-ttu-id="ac40f-114">Для использования автоматической архивации необходимо выполнить следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="ac40f-114">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="ac40f-115">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="ac40f-115">**Operating System**:</span></span>

* <span data-ttu-id="ac40f-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ac40f-116">Windows Server 2012</span></span>
* <span data-ttu-id="ac40f-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ac40f-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="ac40f-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ac40f-118">Windows Server 2016</span></span>

<span data-ttu-id="ac40f-119">**Версия/выпуск SQL Server**</span><span class="sxs-lookup"><span data-stu-id="ac40f-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="ac40f-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="ac40f-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="ac40f-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="ac40f-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="ac40f-122">Автоматическая архивация пока не поддерживает SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="ac40f-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="ac40f-123">**Конфигурация базы данных**</span><span class="sxs-lookup"><span data-stu-id="ac40f-123">**Database configuration**:</span></span>

* <span data-ttu-id="ac40f-124">В конечных базах данных должна использоваться модель полного восстановления.</span><span class="sxs-lookup"><span data-stu-id="ac40f-124">Target databases must use the full recovery model.</span></span>

<span data-ttu-id="ac40f-125">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ac40f-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="ac40f-126">[Установите последнюю версию команд Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ac40f-126">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="ac40f-127">**Расширение IaaS для SQL Server**</span><span class="sxs-lookup"><span data-stu-id="ac40f-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="ac40f-128">[Установите расширение IaaS для SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ac40f-128">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="ac40f-129">Параметры</span><span class="sxs-lookup"><span data-stu-id="ac40f-129">Settings</span></span>
<span data-ttu-id="ac40f-130">В приведенной ниже таблице описаны параметры настройки автоматической архивации.</span><span class="sxs-lookup"><span data-stu-id="ac40f-130">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="ac40f-131">Для виртуальных машин, развернутых с использованием классической модели, эти параметры необходимо настроить с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac40f-131">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="ac40f-132">Настройка</span><span class="sxs-lookup"><span data-stu-id="ac40f-132">Setting</span></span> | <span data-ttu-id="ac40f-133">Диапазон (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ac40f-133">Range (Default)</span></span> | <span data-ttu-id="ac40f-134">Описание</span><span class="sxs-lookup"><span data-stu-id="ac40f-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ac40f-135">**Автоматическая архивация**</span><span class="sxs-lookup"><span data-stu-id="ac40f-135">**Automated Backup**</span></span> |<span data-ttu-id="ac40f-136">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="ac40f-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="ac40f-137">Включает или отключает автоматическую архивацию для виртуальной машины Azure под управлением SQL Server 2014 Standard или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ac40f-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="ac40f-138">**Срок хранения**</span><span class="sxs-lookup"><span data-stu-id="ac40f-138">**Retention Period**</span></span> |<span data-ttu-id="ac40f-139">1–30 дней (30 дней)</span><span class="sxs-lookup"><span data-stu-id="ac40f-139">1-30 days (30 days)</span></span> |<span data-ttu-id="ac40f-140">Число дней хранения резервной копии.</span><span class="sxs-lookup"><span data-stu-id="ac40f-140">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="ac40f-141">**Учетная запись хранения**</span><span class="sxs-lookup"><span data-stu-id="ac40f-141">**Storage Account**</span></span> |<span data-ttu-id="ac40f-142">Учетная запись хранения Azure (учетная запись хранения, созданная для указанной виртуальной машины)</span><span class="sxs-lookup"><span data-stu-id="ac40f-142">Azure storage account (the storage account created for the specified VM)</span></span> |<span data-ttu-id="ac40f-143">Учетная запись хранения Azure для хранения файлов автоматической архивации в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="ac40f-143">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="ac40f-144">Там же создается контейнер для хранения всех файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="ac40f-144">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="ac40f-145">Имя файла резервной копии содержит дату, время и имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="ac40f-145">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="ac40f-146">**Шифрование**</span><span class="sxs-lookup"><span data-stu-id="ac40f-146">**Encryption**</span></span> |<span data-ttu-id="ac40f-147">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="ac40f-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="ac40f-148">Включает или отключает шифрование.</span><span class="sxs-lookup"><span data-stu-id="ac40f-148">Enables or disables encryption.</span></span> <span data-ttu-id="ac40f-149">Если шифрование включено, сертификаты, используемые для восстановления резервной копии, сохраняются в указанной учетной записи хранения в том же контейнере automaticbackup с использованием того же принципа именования файлов.</span><span class="sxs-lookup"><span data-stu-id="ac40f-149">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same automaticbackup container using the same naming convention.</span></span> <span data-ttu-id="ac40f-150">При изменении пароля создается новый сертификат; при этом старый сертификат сохраняется для восстановления предыдущих резервных копий.</span><span class="sxs-lookup"><span data-stu-id="ac40f-150">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="ac40f-151">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="ac40f-151">**Password**</span></span> |<span data-ttu-id="ac40f-152">Текст пароля (нет)</span><span class="sxs-lookup"><span data-stu-id="ac40f-152">Password text (None)</span></span> |<span data-ttu-id="ac40f-153">Пароль для ключей шифрования.</span><span class="sxs-lookup"><span data-stu-id="ac40f-153">A password for encryption keys.</span></span> <span data-ttu-id="ac40f-154">Требуется, только если шифрование включено.</span><span class="sxs-lookup"><span data-stu-id="ac40f-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="ac40f-155">Для восстановления зашифрованной резервной копии требуется правильный пароль и соответствующий сертификат, который использовался при создании резервной копии.</span><span class="sxs-lookup"><span data-stu-id="ac40f-155">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> | <span data-ttu-id="ac40f-156">**Архивация системных баз данных**</span><span class="sxs-lookup"><span data-stu-id="ac40f-156">**Backup system databases**</span></span> | <span data-ttu-id="ac40f-157">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="ac40f-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="ac40f-158">Полная архивация Master, Model и MSDB</span><span class="sxs-lookup"><span data-stu-id="ac40f-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="ac40f-159">**Настройка расписания архивации баз данных**</span><span class="sxs-lookup"><span data-stu-id="ac40f-159">**Configure backup schedule**</span></span> | <span data-ttu-id="ac40f-160">Ручная или автоматическая (автоматическая)</span><span class="sxs-lookup"><span data-stu-id="ac40f-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="ac40f-161">Выберите **Автоматическая**, чтобы включить автоматическое создание полных резервных копий и резервных копий журналов в зависимости от размера журнала.</span><span class="sxs-lookup"><span data-stu-id="ac40f-161">Select **Automated** to automatically take full and log backups based on log growth.</span></span> <span data-ttu-id="ac40f-162">Выберите **Ручная**, чтобы задать расписание для создания полных резервных копий и резервных копий журналов.</span><span class="sxs-lookup"><span data-stu-id="ac40f-162">Select **Manual** to specify the schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="ac40f-163">Настройка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac40f-163">Configuration with PowerShell</span></span>
<span data-ttu-id="ac40f-164">В следующем примере с использованием PowerShell автоматическая архивация настраивается для существующей виртуальной машины SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="ac40f-164">In the following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="ac40f-165">Команда **AzureVMSqlServerAutoBackupConfig** настраивает параметры автоматической архивации для хранения резервных копий в учетной записи хранения Azure, указанной в переменной $storageaccount.</span><span class="sxs-lookup"><span data-stu-id="ac40f-165">The **New-AzureVMSqlServerAutoBackupConfig** command configures the Automated Backup settings to store backups in the Azure storage account specified by the $storageaccount variable.</span></span> <span data-ttu-id="ac40f-166">Эти резервные копии будут храниться в течение 10 дней.</span><span class="sxs-lookup"><span data-stu-id="ac40f-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="ac40f-167">Команда **AzureVMSqlServerExtension** обновляет указанную виртуальную машину Azure в соответствии с заданными параметрами.</span><span class="sxs-lookup"><span data-stu-id="ac40f-167">The **Set-AzureVMSqlServerExtension** command updates the specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="ac40f-168">Установка и настройка агента SQL Server IaaS занимают несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ac40f-168">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="ac40f-169">Чтобы включить шифрование, измените предыдущий скрипт таким образом, чтобы он передавал параметр EnableEncryption вместе с паролем (защищенной строкой) для параметра CertificatePassword.</span><span class="sxs-lookup"><span data-stu-id="ac40f-169">To enable encryption, modify the previous script to pass the EnableEncryption parameter along with a password (secure string) for the CertificatePassword parameter.</span></span> <span data-ttu-id="ac40f-170">Следующий скрипт активирует параметры автоматической архивации их предыдущего примера и добавляет шифрование.</span><span class="sxs-lookup"><span data-stu-id="ac40f-170">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="ac40f-171">Чтобы отключить автоматическую архивацию, выполните тот же сценарий без параметра **-Enable** в командлете **New-AzureVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="ac40f-171">To disable automatic backup, run the same script without the **-Enable** parameter to the **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="ac40f-172">Как и установка, отключение автоматической архивации занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="ac40f-172">As with installation, it can take several minutes to disable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="ac40f-173">При отключении и удалении агента SQL Server IaaS не удаляются настроенные ранее параметры управляемого резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="ac40f-173">Disabling and uninstalling the SQL Server IaaS Agent does not remove the previously configured Managed Backup settings.</span></span> <span data-ttu-id="ac40f-174">Перед отключением и удалением агента SQL Server IaaS необходимо отключить автоматическую архивацию.</span><span class="sxs-lookup"><span data-stu-id="ac40f-174">You should disable Automated Backup before disabling or uninstalling the SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ac40f-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac40f-175">Next steps</span></span>
<span data-ttu-id="ac40f-176">Автоматическая архивация настраивает управляемое резервное копирование на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="ac40f-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="ac40f-177">В связи с этим важно изучить [документацию по управляемой архивации](https://msdn.microsoft.com/library/dn449496.aspx) и понять, как она работает.</span><span class="sxs-lookup"><span data-stu-id="ac40f-177">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="ac40f-178">Дополнительные сведения об архивации и восстановлении SQL Server на виртуальных машинах Azure см. в статье [Архивация и восстановление SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac40f-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="ac40f-179">Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ac40f-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="ac40f-180">Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac40f-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

