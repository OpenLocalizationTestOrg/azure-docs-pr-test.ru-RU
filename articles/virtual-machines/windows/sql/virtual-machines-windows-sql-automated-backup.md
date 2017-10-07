---
title: "aaaAutomated резервного копирования для SQL Server 2014 виртуальных машин Azure | Документы Microsoft"
description: "Описывается функция hello автоматического резервного копирования для SQL Server 2014 работающих виртуальных машин в Azure. Эта статья содержит определенные tooVMs, с помощью диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a>Автоматическая архивация для виртуальных машин SQL Server 2014 (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Автоматическое резервное копирование автоматически настраивает [tooMicrosoft управляемого резервного копирования Azure](https://msdn.microsoft.com/library/dn449496.aspx) для всех существующих и новых баз данных на виртуальной Машине Azure под управлением SQL Server 2014 Standard или Enterprise. Это позволяет tooconfigure регулярные резервные копии, использовать устойчивые Azure BLOB-объекта хранилища. Автоматическая архивация зависит от hello [расширения агента SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Предварительные требования
toouse автоматическое резервное копирование, примите во внимание следующие предварительные требования hello.

**Операционная система**

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

**Версия/выпуск SQL Server**

- SQL Server 2014 Standard
- SQL Server 2014 Enterprise

> [!IMPORTANT]
> Автоматическая архивация работает с SQL Server 2014. При использовании SQL Server 2016 можно использовать автоматическое резервное копирование v2 tooback копии баз данных. Дополнительную информацию см. в статье [Автоматическая архивация версии 2 для виртуальных машин SQL Server 2016 в Azure](virtual-machines-windows-sql-automated-backup-v2.md).

**Конфигурация базы данных**

- Целевые базы данных должна использовать модель полного восстановления hello. Дополнительные сведения о влиянии hello hello модель полного восстановления резервных копий см. в разделе [hello резервного копирования в модели полного восстановления](https://technet.microsoft.com/library/ms190217.aspx).
- Целевые базы данных должен быть на экземпляре SQL Server по умолчанию hello. Hello расширения IaaS SQL Server не поддерживает именованные экземпляры.

**Модель развертывания Azure**

- Диспетчер ресурсов

**Azure PowerShell**

- [Установка последних команд Azure PowerShell hello](/powershell/azure/overview) при планировании tooconfigure автоматическое резервное копирование с помощью PowerShell.

> [!NOTE]
> Автоматическая архивация зависит от расширения агента SQL Server IaaS hello. В текущей коллекции образов виртуальных машин SQL это расширение присутствует по умолчанию. Дополнительные сведения см. в статье [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md) (Расширение агента SQL Server IaaS).

## <a name="settings"></a>данных

Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического резервного копирования. Hello фактические шаги настройки отличаются в зависимости от того, используются ли hello портал Azure или команд Windows PowerShell для Azure.

| Настройка | Диапазон (по умолчанию) | Описание |
| --- | --- | --- |
| **Автоматическая архивация** | Включено/отключено (отключено) | Включает или отключает автоматическую архивацию для виртуальной машины Azure под управлением SQL Server 2014 Standard или Enterprise. |
| **Срок хранения** | 1–30 дней (30 дней) | Hello количество дней tooretain резервной копии. |
| **Учетная запись хранения** | Учетная запись хранения Azure. | Toouse учетной записи хранилища Azure для хранения файлов автоматического резервного копирования в хранилище больших двоичных объектов. Контейнер создается в этом toostore расположение всех файлов резервных копий. файл резервной копии Hello соглашение об именах включает hello Дата, время и имя компьютера. |
| **Шифрование** | Включено/отключено (отключено) | Включает или отключает шифрование. При включено шифрование, сертификаты, используемые toorestore hello hello-резервной копии находятся в hello указан учетную запись хранилища в hello же `automaticbackup` контейнер с помощью hello же соглашение об именовании. При изменении пароля hello, новый сертификат создается с этим паролем, но Здравствуй, старый сертификат остается toorestore предыдущих резервных копий. |
| **Пароль** | Текст пароля | Пароль для ключей шифрования. Требуется, только если шифрование включено. В порядке toorestore зашифрованной резервной копии, необходимо иметь правильный пароль hello и связанные сертификата, который был использован в hello время, когда была создана резервная копия hello. |

## <a name="configuration-in-hello-portal"></a>Конфигурация в hello портала

Во время инициализации или для существующих виртуальных машинах SQL Server 2014 можно использовать hello Azure портала tooconfigure автоматическое резервное копирование.

### <a name="new-vms"></a>Новые виртуальные машины

При создании новой виртуальной машины 2014 SQL Server в модели развертывания диспетчера ресурсов hello, используйте hello Azure портала tooconfigure автоматическое резервное копирование.

В hello **параметры SQL Server** колонке выберите **автоматическое резервное копирование**. Hello следующие Azure портала снимке экрана показано hello **автоматическое резервное копирование SQL** колонку.

![Настройка автоматической архивации SQL на портале Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

Контекст, в разделе hello полный на [подготовку виртуальной машины SQL Server в Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Существующие виртуальные машины

Выберите существующую виртуальную машину SQL Server. Затем выберите hello **конфигурации SQL Server** раздел hello **параметры** колонку.

![Автоматизированная архивация SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

В hello **конфигурации SQL Server** колонка, щелкните hello **изменить** кнопку в hello автоматического резервного копирования раздела.

![Настройка автоматизированной архивации SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

По завершении нажмите кнопку hello **ОК** кнопку внизу hello hello **конфигурации SQL Server** toosave колонке изменения.

При включении автоматического резервного копирования для hello первый раз Azure настраивает hello агента SQL Server IaaS в фоновом режиме hello. В течение этого времени hello Azure портала может показывать, что автоматическая архивация настроена. Подождите несколько минут для hello агента toobe установлены, настроены. После этого hello Azure портале будут отображаться новые параметры hello.

> [!NOTE]
> Можно также настроить автоматизированную архивацию с помощью шаблона. Чтобы получить дополнительные сведения, ознакомьтесь с [шаблоном быстрого запуска Azure для автоматизированной архивации](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).

## <a name="configuration-with-powershell"></a>Настройка с помощью PowerShell

Можно использовать PowerShell tooconfigure автоматическое резервное копирование. Предварительно необходимо выполнить следующее.

- [Загрузите и установите последнюю версию Azure PowerShell hello](http://aka.ms/webpi-azps).
- Откройте компонент Windows PowerShell и свяжите его со своей учетной записью. Это можно сделать с помощью инструкции hello в hello [настроить подписку](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) раздел hello подготовки раздела.

### <a name="install-hello-sql-iaas-extension"></a>Установка расширения SQL IaaS hello
При подготовке виртуальной машины SQL Server из портала Azure hello hello расширения IaaS SQL Server должны быть уже настроены. Можно определить, если оно устанавливается для виртуальной Машины путем вызова **Get AzureRmVM** и проверив hello **расширения** свойство.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

Если установлен hello расширения агента IaaS SQL Server, вы увидите, что оно указано как «SqlIaaSAgent» или «SQLIaaSExtension». **ProvisioningState** для расширения hello также должен быть «Succeeded».

Если он не установлен или не удалось подготовить toobe, его можно установить с hello следующую команду. В дополнение toohello ВМ имя и группе ресурсов, необходимо также указать область hello (**$region**), расположенных в ВМ.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <a id="verifysettings"></a> Проверка текущих параметров

Если вы включили автоматическое резервное копирование во время подготовки, можно использовать PowerShell toocheck текущей конфигурации. Запустите hello **Get AzureRmVMSqlServerExtension** команды и изучить hello **AutoBackupSettings** свойства:

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

Вы должны получить аналогичные toohello следующие выходные данные:

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

Если выходных данных показано, что **включить** задано слишком**False**, то у вас есть tooenable автоматическое резервное копирование. Hello хорошие новости — Включение и настройка автоматического резервного копирования в hello таким же образом. Hello следующем разделе для получения этих сведений.

> [!NOTE] 
> Проверьте параметры hello сразу же после внесения изменений, возможно, вы получите обратно hello старые значения конфигурации. Подождите несколько минут и проверить параметры hello снова toomake том, что изменения были применены.

### <a name="configure-automated-backup"></a>Настройка автоматической архивации
PowerShell tooenable автоматическое резервное копирование, а также toomodify можно использовать его параметров и поведения в любое время.

Во-первых выберите или создайте учетную запись хранения hello файлов резервных копий. Hello следующий скрипт выбирает учетную запись хранения или создает ее, если она не существует.

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> Служба автоматической архивации не поддерживает хранение резервных копий в хранилище уровня "Премиум", но может создавать резервные копии дисков виртуальных машин, которые используют хранилище уровня "Премиум".

Затем с помощью hello **New AzureRmVMSqlServerAutoBackupConfig** команды tooenable и настроить автоматическое резервное копирование параметров hello toostore-резервные копии в hello учетной записи хранилища Azure. В этом примере hello копии создаются toobe сохраняются в течение 10 дней. Здравствуйте, вторая команда **AzureRmVMSqlServerExtension набор**, hello обновления указано ВМ Azure с помощью этих параметров.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello.

> [!NOTE]
> Существуют другие параметры для **New AzureRmVMSqlServerAutoBackupConfig** , применяемые только tooSQL Server 2016 и v2 автоматического резервного копирования. SQL Server 2014 не поддерживает следующие параметры hello: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, и **LogBackupFrequencyInMinutes**. При попытке tooconfigure эти параметры на виртуальной машине SQL Server 2014, не содержит ошибок, но параметры hello не применяется. Если требуется toouse эти параметры на виртуальной машине SQL Server 2016, см. раздел [v2 автоматического резервного копирования для SQL Server 2016 виртуальных машин Azure](virtual-machines-windows-sql-automated-backup-v2.md).

шифрование tooenable изменить hello предыдущего сценария toopass hello **EnableEncryption** параметра вместе с паролем (защищенной строки) для hello **CertificatePassword** параметра. Hello следующий сценарий включает параметры автоматической архивации hello в предыдущем примере hello и добавляет шифрование.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

параметры применяются, tooconfirm [Проверка конфигурации автоматического резервного копирования hello](#verifysettings).

### <a name="disable-automated-backup"></a>Отключение автоматической архивации

Автоматическое резервное копирование, выполнения hello же сценарий, не hello toodisable **-включить** toohello параметр **New AzureRmVMSqlServerAutoBackupConfig** команды. Здравствуйте, отсутствие hello **-включить** функции hello toodisable команда hello параметров сигналы. Как и установка, может занять несколько минут toodisable автоматическое резервное копирование.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>Пример сценария

Hello следующий скрипт предоставляет набор переменных, можно настроить tooenable и настройки автоматического резервного копирования для виртуальной Машины. В вашем случае может потребоваться toocustomize hello скрипт на основе требований. Например можно иметь toomake изменения, если требуется, чтобы toodisable hello резервное копирование системных баз данных или включить шифрование.

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Дальнейшие действия

Автоматическая архивация настраивает управляемое резервное копирование на виртуальных машинах Azure. Поэтому важно слишком[документации hello управляемого резервного копирования](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello влияние и поведение.

Можно найти созданием резервных копий и восстановление руководство по SQL Server на виртуальных машинах Azure в разделе hello: [резервное копирование и восстановление для SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-backup-recovery.md).

Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).

