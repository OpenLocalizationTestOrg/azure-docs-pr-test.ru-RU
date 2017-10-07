---
title: "aaaAutomated резервного копирования для SQL Server виртуальной машины (классические) | Документы Microsoft"
description: "Описывается функция hello автоматического резервного копирования для SQL Server в виртуальных машинах Azure с помощью диспетчера ресурсов. "
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
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="b0b4d-103">Автоматическая архивация SQL Server на виртуальных машинах Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="b0b4d-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0b4d-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="b0b4d-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="b0b4d-105">Классический</span><span class="sxs-lookup"><span data-stu-id="b0b4d-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="b0b4d-106">Автоматическое резервное копирование автоматически настраивает [tooMicrosoft управляемого резервного копирования Azure](https://msdn.microsoft.com/library/dn449496.aspx) для всех существующих и новых баз данных на виртуальной Машине Azure под управлением SQL Server 2014 Standard или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-106">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="b0b4d-107">Это позволяет tooconfigure регулярные резервные копии, использовать устойчивые Azure BLOB-объекта хранилища.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-107">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="b0b4d-108">Автоматическая архивация зависит от hello [расширения агента SQL Server IaaS](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0b4d-108">Automated Backup depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="b0b4d-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b0b4d-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b0b4d-110">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b0b4d-111">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b0b4d-112">tooview hello диспетчера ресурсов версию этой статьи в разделе [автоматического резервного копирования для SQL Server в диспетчере ресурсов Azure виртуальные машины](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="b0b4d-112">tooview hello Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0b4d-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b0b4d-113">Prerequisites</span></span>
<span data-ttu-id="b0b4d-114">toouse автоматическое резервное копирование, примите во внимание следующие предварительные требования hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-114">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="b0b4d-115">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-115">**Operating System**:</span></span>

* <span data-ttu-id="b0b4d-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b0b4d-116">Windows Server 2012</span></span>
* <span data-ttu-id="b0b4d-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b0b4d-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="b0b4d-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b0b4d-118">Windows Server 2016</span></span>

<span data-ttu-id="b0b4d-119">**Версия/выпуск SQL Server**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="b0b4d-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="b0b4d-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="b0b4d-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="b0b4d-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="b0b4d-122">Автоматическая архивация пока не поддерживает SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="b0b4d-123">**Конфигурация базы данных**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-123">**Database configuration**:</span></span>

* <span data-ttu-id="b0b4d-124">Целевые базы данных должна использовать модель полного восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-124">Target databases must use hello full recovery model.</span></span>

<span data-ttu-id="b0b4d-125">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="b0b4d-126">[Установка последних команд Azure PowerShell hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b0b4d-126">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="b0b4d-127">**Расширение IaaS для SQL Server**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="b0b4d-128">[Установка расширения SQL Server IaaS hello](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b0b4d-128">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="b0b4d-129">данных</span><span class="sxs-lookup"><span data-stu-id="b0b4d-129">Settings</span></span>
<span data-ttu-id="b0b4d-130">Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-130">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="b0b4d-131">Для классических виртуальных машин необходимо использовать PowerShell tooconfigure эти параметры.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-131">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="b0b4d-132">Настройка</span><span class="sxs-lookup"><span data-stu-id="b0b4d-132">Setting</span></span> | <span data-ttu-id="b0b4d-133">Диапазон (по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="b0b4d-133">Range (Default)</span></span> | <span data-ttu-id="b0b4d-134">Описание</span><span class="sxs-lookup"><span data-stu-id="b0b4d-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b0b4d-135">**Автоматическая архивация**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-135">**Automated Backup**</span></span> |<span data-ttu-id="b0b4d-136">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="b0b4d-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="b0b4d-137">Включает или отключает автоматическую архивацию для виртуальной машины Azure под управлением SQL Server 2014 Standard или Enterprise.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="b0b4d-138">**Срок хранения**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-138">**Retention Period**</span></span> |<span data-ttu-id="b0b4d-139">1–30 дней (30 дней)</span><span class="sxs-lookup"><span data-stu-id="b0b4d-139">1-30 days (30 days)</span></span> |<span data-ttu-id="b0b4d-140">Hello количество дней tooretain резервной копии.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-140">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="b0b4d-141">**Учетная запись хранения**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-141">**Storage Account**</span></span> |<span data-ttu-id="b0b4d-142">Учетная запись хранения Azure (hello учетной записи хранения создана для hello указанной виртуальной Машины)</span><span class="sxs-lookup"><span data-stu-id="b0b4d-142">Azure storage account (hello storage account created for hello specified VM)</span></span> |<span data-ttu-id="b0b4d-143">Toouse учетной записи хранилища Azure для хранения файлов автоматического резервного копирования в хранилище больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-143">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="b0b4d-144">Контейнер создается в этом toostore расположение всех файлов резервных копий.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-144">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="b0b4d-145">файл резервной копии Hello соглашение об именах включает hello Дата, время и имя компьютера.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-145">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="b0b4d-146">**Шифрование**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-146">**Encryption**</span></span> |<span data-ttu-id="b0b4d-147">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="b0b4d-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="b0b4d-148">Включает или отключает шифрование.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-148">Enables or disables encryption.</span></span> <span data-ttu-id="b0b4d-149">При включении шифрования сертификатов hello, резервного копирования используется toorestore hello расположены в hello указать учетную запись хранения hello используя же контейнер automaticbackup hello же соглашение об именовании.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-149">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same automaticbackup container using hello same naming convention.</span></span> <span data-ttu-id="b0b4d-150">При изменении пароля hello, новый сертификат создается с этим паролем, но Здравствуй, старый сертификат остается toorestore предыдущих резервных копий.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-150">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="b0b4d-151">**Пароль**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-151">**Password**</span></span> |<span data-ttu-id="b0b4d-152">Текст пароля (нет)</span><span class="sxs-lookup"><span data-stu-id="b0b4d-152">Password text (None)</span></span> |<span data-ttu-id="b0b4d-153">Пароль для ключей шифрования.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-153">A password for encryption keys.</span></span> <span data-ttu-id="b0b4d-154">Требуется, только если шифрование включено.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="b0b4d-155">В порядке toorestore зашифрованной резервной копии, необходимо иметь правильный пароль hello и связанные сертификата, который был использован в hello время, когда была создана резервная копия hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-155">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> | <span data-ttu-id="b0b4d-156">**Архивация системных баз данных**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-156">**Backup system databases**</span></span> | <span data-ttu-id="b0b4d-157">Включено/отключено (отключено)</span><span class="sxs-lookup"><span data-stu-id="b0b4d-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="b0b4d-158">Полная архивация Master, Model и MSDB</span><span class="sxs-lookup"><span data-stu-id="b0b4d-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="b0b4d-159">**Настройка расписания архивации баз данных**</span><span class="sxs-lookup"><span data-stu-id="b0b4d-159">**Configure backup schedule**</span></span> | <span data-ttu-id="b0b4d-160">Ручная или автоматическая (автоматическая)</span><span class="sxs-lookup"><span data-stu-id="b0b4d-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="b0b4d-161">Выберите **автоматизирован** tooautomatically воспользоваться полной резервной копии журналов и основании рост журнала.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-161">Select **Automated** tooautomatically take full and log backups based on log growth.</span></span> <span data-ttu-id="b0b4d-162">Выберите **вручную** toospecify hello расписание для полной и резервные копии журналов.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-162">Select **Manual** toospecify hello schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="b0b4d-163">Настройка с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0b4d-163">Configuration with PowerShell</span></span>
<span data-ttu-id="b0b4d-164">В следующем примере PowerShell hello автоматического резервного копирования настраивается для существующей виртуальной Машине SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-164">In hello following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="b0b4d-165">Hello **New AzureVMSqlServerAutoBackupConfig** команда настраивает hello параметры автоматического резервного копирования toostore, резервных копий в учетной записи хранилища Azure hello, указанных в переменной hello $storageaccount.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-165">hello **New-AzureVMSqlServerAutoBackupConfig** command configures hello Automated Backup settings toostore backups in hello Azure storage account specified by hello $storageaccount variable.</span></span> <span data-ttu-id="b0b4d-166">Эти резервные копии будут храниться в течение 10 дней.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="b0b4d-167">Hello **AzureVMSqlServerExtension набор** hello обновления указанной виртуальной Машине Azure с помощью этих параметров команды.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-167">hello **Set-AzureVMSqlServerExtension** command updates hello specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="b0b4d-168">Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-168">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="b0b4d-169">шифрование tooenable изменить hello предыдущего сценария toopass hello параметра EnableEncryption с паролем (защищенной строки) для параметра CertificatePassword hello.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-169">tooenable encryption, modify hello previous script toopass hello EnableEncryption parameter along with a password (secure string) for hello CertificatePassword parameter.</span></span> <span data-ttu-id="b0b4d-170">Hello следующий сценарий включает параметры автоматической архивации hello в предыдущем примере hello и добавляет шифрование.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-170">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="b0b4d-171">автоматическое резервное копирование toodisable выполнения hello же сценарий, не hello **-включить** toohello параметр **New AzureVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-171">toodisable automatic backup, run hello same script without hello **-Enable** parameter toohello **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="b0b4d-172">Как и установка, может занять несколько минут toodisable автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-172">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="b0b4d-173">Отключение и удаление hello агента IaaS SQL Server не удаляет hello ранее настроенные параметры управляемого резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-173">Disabling and uninstalling hello SQL Server IaaS Agent does not remove hello previously configured Managed Backup settings.</span></span> <span data-ttu-id="b0b4d-174">Прежде чем отключить или удалить hello агента IaaS SQL Server, следует отключить автоматическое резервное копирование.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-174">You should disable Automated Backup before disabling or uninstalling hello SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b0b4d-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b0b4d-175">Next steps</span></span>
<span data-ttu-id="b0b4d-176">Автоматическая архивация настраивает управляемое резервное копирование на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="b0b4d-177">Поэтому важно слишком[документации hello управляемого резервного копирования](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello влияние и поведение.</span><span class="sxs-lookup"><span data-stu-id="b0b4d-177">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="b0b4d-178">Можно найти созданием резервных копий и восстановление руководство по SQL Server на виртуальных машинах Azure в разделе hello: [резервное копирование и восстановление для SQL Server в виртуальных машинах Azure](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b0b4d-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="b0b4d-179">Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="b0b4d-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="b0b4d-180">Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b0b4d-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

