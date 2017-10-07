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
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Автоматическая архивация SQL Server на виртуальных машинах Azure (классическая модель)
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [Классический](../classic/sql-automated-backup.md)
> 
> 

Автоматическое резервное копирование автоматически настраивает [tooMicrosoft управляемого резервного копирования Azure](https://msdn.microsoft.com/library/dn449496.aspx) для всех существующих и новых баз данных на виртуальной Машине Azure под управлением SQL Server 2014 Standard или Enterprise. Это позволяет tooconfigure регулярные резервные копии, использовать устойчивые Azure BLOB-объекта хранилища. Автоматическая архивация зависит от hello [расширения агента SQL Server IaaS](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. tooview hello диспетчера ресурсов версию этой статьи в разделе [автоматического резервного копирования для SQL Server в диспетчере ресурсов Azure виртуальные машины](../sql/virtual-machines-windows-sql-automated-backup.md).

## <a name="prerequisites"></a>Предварительные требования
toouse автоматическое резервное копирование, примите во внимание следующие предварительные требования hello.

**Операционная система**

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**Версия/выпуск SQL Server**

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> Автоматическая архивация пока не поддерживает SQL Server 2016.
> 
> 

**Конфигурация базы данных**

* Целевые базы данных должна использовать модель полного восстановления hello.

**Azure PowerShell**

* [Установка последних команд Azure PowerShell hello](/powershell/azure/overview).

**Расширение IaaS для SQL Server**

* [Установка расширения SQL Server IaaS hello](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>данных
Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического резервного копирования. Для классических виртуальных машин необходимо использовать PowerShell tooconfigure эти параметры.

| Настройка | Диапазон (по умолчанию) | Описание |
| --- | --- | --- |
| **Автоматическая архивация** |Включено/отключено (отключено) |Включает или отключает автоматическую архивацию для виртуальной машины Azure под управлением SQL Server 2014 Standard или Enterprise. |
| **Срок хранения** |1–30 дней (30 дней) |Hello количество дней tooretain резервной копии. |
| **Учетная запись хранения** |Учетная запись хранения Azure (hello учетной записи хранения создана для hello указанной виртуальной Машины) |Toouse учетной записи хранилища Azure для хранения файлов автоматического резервного копирования в хранилище больших двоичных объектов. Контейнер создается в этом toostore расположение всех файлов резервных копий. файл резервной копии Hello соглашение об именах включает hello Дата, время и имя компьютера. |
| **Шифрование** |Включено/отключено (отключено) |Включает или отключает шифрование. При включении шифрования сертификатов hello, резервного копирования используется toorestore hello расположены в hello указать учетную запись хранения hello используя же контейнер automaticbackup hello же соглашение об именовании. При изменении пароля hello, новый сертификат создается с этим паролем, но Здравствуй, старый сертификат остается toorestore предыдущих резервных копий. |
| **Пароль** |Текст пароля (нет) |Пароль для ключей шифрования. Требуется, только если шифрование включено. В порядке toorestore зашифрованной резервной копии, необходимо иметь правильный пароль hello и связанные сертификата, который был использован в hello время, когда была создана резервная копия hello. | **Архивация системных баз данных** | Включено/отключено (отключено) | Полная архивация Master, Model и MSDB |
| **Настройка расписания архивации баз данных** | Ручная или автоматическая (автоматическая) | Выберите **автоматизирован** tooautomatically воспользоваться полной резервной копии журналов и основании рост журнала. Выберите **вручную** toospecify hello расписание для полной и резервные копии журналов. |

## <a name="configuration-with-powershell"></a>Настройка с помощью PowerShell
В следующем примере PowerShell hello автоматического резервного копирования настраивается для существующей виртуальной Машине SQL Server 2014. Hello **New AzureVMSqlServerAutoBackupConfig** команда настраивает hello параметры автоматического резервного копирования toostore, резервных копий в учетной записи хранилища Azure hello, указанных в переменной hello $storageaccount. Эти резервные копии будут храниться в течение 10 дней. Hello **AzureVMSqlServerExtension набор** hello обновления указанной виртуальной Машине Azure с помощью этих параметров команды.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello.

шифрование tooenable изменить hello предыдущего сценария toopass hello параметра EnableEncryption с паролем (защищенной строки) для параметра CertificatePassword hello. Hello следующий сценарий включает параметры автоматической архивации hello в предыдущем примере hello и добавляет шифрование.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

автоматическое резервное копирование toodisable выполнения hello же сценарий, не hello **-включить** toohello параметр **New AzureVMSqlServerAutoBackupConfig**. Как и установка, может занять несколько минут toodisable автоматическое резервное копирование.

> [!NOTE]
> Отключение и удаление hello агента IaaS SQL Server не удаляет hello ранее настроенные параметры управляемого резервного копирования. Прежде чем отключить или удалить hello агента IaaS SQL Server, следует отключить автоматическое резервное копирование.
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
Автоматическая архивация настраивает управляемое резервное копирование на виртуальных машинах Azure. Поэтому важно слишком[документации hello управляемого резервного копирования](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello влияние и поведение.

Можно найти созданием резервных копий и восстановление руководство по SQL Server на виртуальных машинах Azure в разделе hello: [резервное копирование и восстановление для SQL Server в виртуальных машинах Azure](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](../classic/sql-server-agent-extension.md).

Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

