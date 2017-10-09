---
title: "aaaAutomated v2 резервного копирования для SQL Server 2016 виртуальных машин Azure | Документы Microsoft"
description: "Описывается функция hello автоматического резервного копирования для SQL Server 2016 работающих виртуальных машин в Azure. Эта статья содержит определенные tooVMs, с помощью диспетчера ресурсов hello."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>Автоматическая архивация версии 2 для виртуальных машин SQL Server 2016 в Azure (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Автоматическая настройка автоматического резервного копирования v2 [tooMicrosoft управляемого резервного копирования Azure](https://msdn.microsoft.com/library/dn449496.aspx) для всех существующих и новых баз данных на виртуальной Машине Azure под управлением SQL Server 2016 Standard, Enterprise или Developer. Это позволяет tooconfigure регулярные резервные копии, использовать устойчивые Azure BLOB-объекта хранилища. Автоматическое резервное копирование v2 зависит от hello [расширения агента SQL Server IaaS](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Предварительные требования
toouse v2 автоматического резервного копирования, просмотрите hello следующие предварительные требования:

**Операционная система**

- Windows Server 2012 R2
- Windows Server 2016

**Версия/выпуск SQL Server**

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer.

> [!IMPORTANT]
> Автоматическая архивация версии 2 работает с SQL Server 2016. При использовании SQL Server 2014 можно использовать автоматическое резервное копирование v1 tooback копии баз данных. Дополнительную информацию см. в статье [Автоматическая архивация для виртуальных машин SQL Server 2014 в Azure](virtual-machines-windows-sql-automated-backup.md).

**Конфигурация базы данных**

- Целевые базы данных должна использовать модель полного восстановления hello. Дополнительные сведения о влиянии hello hello модель полного восстановления резервных копий см. в разделе [hello резервного копирования в модели полного восстановления](https://technet.microsoft.com/library/ms190217.aspx).
- Системные базы данных имеют toouse модель полного восстановления. Тем не менее если требуется toobe резервных копий журнала для модели или базы данных MSDB, необходимо использовать модель полного восстановления.
- Целевые базы данных должен быть на экземпляре SQL Server по умолчанию hello. Hello расширения IaaS SQL Server не поддерживает именованные экземпляры.

**Модель развертывания Azure**

- Диспетчер ресурсов

> [!NOTE]
> Автоматическая архивация зависит hello **расширения агента SQL Server IaaS**. В текущей коллекции образов виртуальных машин SQL это расширение присутствует по умолчанию. Дополнительные сведения см. в статье [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md) (Расширение агента SQL Server IaaS).

## <a name="settings"></a>данных
Hello следующей таблице описаны параметры hello, которые могут быть настроены для автоматического резервного копирования v2. Hello фактические шаги настройки отличаются в зависимости от того, используются ли hello портал Azure или команд Windows PowerShell для Azure.

### <a name="basic-settings"></a>Основные параметры

| Настройка | Диапазон (по умолчанию) | Описание |
| --- | --- | --- |
| **Автоматическая архивация** | Включено/отключено (отключено) | Включает или отключает автоматическую архивацию для виртуальной машины Azure под управлением SQL Server 2016 Standard или SQL Server 2016 Enterprise. |
| **Срок хранения** | 1–30 дней (30 дней) | количество резервных копий tooretain дней Hello. |
| **Учетная запись хранения** | Учетная запись хранения Azure. | Toouse учетной записи хранилища Azure для хранения файлов автоматического резервного копирования в хранилище больших двоичных объектов. Контейнер создается в этом toostore расположение всех файлов резервных копий. файл резервной копии Hello соглашение об именах включает hello даты, времени и идентификатор GUID базы данных. |
| **Шифрование** |Включено/отключено (отключено) | Включает или отключает шифрование. При включено шифрование, сертификаты, используемые toorestore hello hello-резервной копии находятся в hello указан учетную запись хранилища в hello же **automaticbackup** контейнер с помощью hello же соглашение об именовании. При изменении пароля hello, новый сертификат создается с этим паролем, но Здравствуй, старый сертификат остается toorestore предыдущих резервных копий. |
| **Пароль** |Текст пароля | Пароль для ключей шифрования. Требуется, только если шифрование включено. В порядке toorestore зашифрованной резервной копии, необходимо иметь правильный пароль hello и связанные сертификата, который был использован в hello время, когда была создана резервная копия hello. |

### <a name="advanced-settings"></a>Дополнительные параметры

| Настройка | Диапазон (по умолчанию) | Описание |
| --- | --- | --- |
| **System Database Backups** (Архивация системных баз данных) | Включено/отключено (отключено) | При включении этой функции также выполнить резервное копирование hello системных баз данных: Master, MSDB и Model. Убедитесь, они находятся в режиме полного восстановления Если выполнены toobe резервных копий журнала для hello MSDB и базы данных модели. Резервные копии журналов для базы данных Master не создаются. Кроме того, не создаются и резервные копии базы данных TempDB. |
| **Расписание архивации** | Ручная или автоматическая (автоматическая) | По умолчанию hello расписание резервного копирования будет автоматически определен на основе рост журнала hello. Вручную расписание резервного копирования позволяет hello пользователя toospecify hello временное окно резервного копирования. В этом случае резервное копирование только занимает место во hello указаны частоты и во время hello временное окно конкретный день. |
| **Full backup frequency** (Частота полной архивации) | Ежедневно или еженедельно | Частота создания полных резервных копий. В обоих случаях во время следующего запланированного времени периода hello начнется полные резервные копии. Если выбрана еженедельная архивация, то она может охватывать несколько дней, пока не будут успешно созданы резервные копии всех баз данных. |
| **Full backup start time** (Время начала полной архивации) | 00:00–23:00 (01:00) | Время начала полной архивации в заданный день. |
| **Full backup time window** (Временное окно полной архивации) | 1–23 ч (1 ч) | Продолжительность периода времени hello заданного дня, во время которого разрешено выполнение полного резервного копирования. |
| **Log backup frequency** (Частота создания резервных копий журналов) | 5–60 мин (60 мин) | Частота создания резервных копий журналов. |

## <a name="understanding-full-backup-frequency"></a>Основные сведения о частоте полной архивации
Это важные toounderstand hello различие между ежедневно и еженедельно полные резервные копии. Для этого мы рассмотрим два примера сценария.

### <a name="scenario-1-weekly-backups"></a>Сценарий 1. Еженедельные резервные копии
У вас есть виртуальная машина SQL Server, которая содержит несколько очень больших баз данных.

Понедельник включить автоматическое резервное копирование v2 с hello следующие параметры:

- "Расписание архивации": **Ручное**;
- "Full backup frequency" (Частота полной архивации): **Еженедельная**;
- "Full backup start time" (Время начала полной архивации): **01:00**;
- "Full backup time window" (Временное окно полной архивации): **1 ч**.

Таким образом, чтобы hello следующей доступной резервной копии, вторник в 13: 00 для 1 час. В это время служба автоматической архивации начнет по очереди архивировать ваши базы данных. В этом сценарии базы данных обладают достаточной будет выполнена, полные резервные копии для баз данных, hello Первая пара. Однако через час не все базы данных hello не созданы резервные копии.

В этом случае автоматическое резервное копирование начнется резервное копирование hello оставшихся баз данных hello следующего дня, среда, в 13: 00 для 1 час. Если не все базы данных не созданы резервные копии в это время, он попытается подключиться снова hello следующий день в hello же время. Это будет продолжаться, пока все базы данных не будут заархивированы.

Как только наступит следующий вторник, служба автоматической архивации снова начнет создавать резервные копии всех баз данных.

Этот сценарий показывает, что автоматическое резервное копирование будет работать только в пределах hello указанного интервала времени, и каждой базы данных будут создаваться резервные копии один раз в неделю. Это также показывает, что возможна для toospan резервные копии нескольких дней в hello случае когда нет возможности toocomplete все резервные копии в течение одного дня.

### <a name="scenario-2-daily-backups"></a>Сценарий 2. Ежедневные резервные копии
У вас есть виртуальная машина SQL Server, которая содержит несколько очень больших баз данных.

Понедельник включить автоматическое резервное копирование v2 с hello следующие параметры:

- "Расписание архивации": "Ручное";
- "Full backup frequency" (Частота полной архивации): "Ежедневная";
- "Full backup start time" (Время начала полной архивации): "22:00";
- "Full backup time window" (Временное окно полной архивации): "6 ч".

Таким образом, чтобы hello следующей доступной резервной копии, понедельник в 22: 00 на 6 часов. В это время служба автоматической архивации начнет по очереди архивировать ваши базы данных.

Затем во вторник в 22:00 снова начнется 6-часовая полная архивация всех баз данных.

> [!IMPORTANT]
> При планировании ежедневного резервного копирования, рекомендуется запланировать tooensure широкий времени окна, скопированы все базы данных в течение этого времени. Это особенно важно в случае hello, при наличии большого объема данных tooback вверх.

## <a name="configuration-in-hello-portal"></a>Конфигурация в hello портала

Можно использовать v2 автоматического резервного копирования Azure портала tooconfigure hello во время инициализации или для существующих виртуальных машинах SQL Server 2016.

### <a name="new-vms"></a>Новые виртуальные машины

Используйте автоматическое резервное копирование v2 hello Azure портала tooconfigure при создании новой виртуальной машины 2016 SQL Server в модели развертывания диспетчера ресурсов hello. 

В hello **параметры SQL Server** колонке выберите **автоматическое резервное копирование**. Hello следующие Azure портала снимке экрана показано hello **автоматическое резервное копирование SQL** колонку.

![Настройка автоматической архивации SQL на портале Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> По умолчанию автоматическая архивация версии 2 отключена.

Контекст, в разделе hello полный на [подготовку виртуальной машины SQL Server в Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Существующие виртуальные машины

Выберите существующую виртуальную машину SQL Server. Затем выберите hello **конфигурации SQL Server** раздел hello **параметры** колонку.

![Автоматизированная архивация SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

В hello **конфигурации SQL Server** колонка, щелкните hello **изменить** кнопку в hello автоматического резервного копирования раздела.

![Настройка автоматизированной архивации SQL для существующих виртуальных машин](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

По завершении нажмите кнопку hello **ОК** кнопку внизу hello hello **конфигурации SQL Server** toosave колонке изменения.

При включении автоматического резервного копирования для hello первый раз Azure настраивает hello агента SQL Server IaaS в фоновом режиме hello. В течение этого времени hello Azure портала может показывать, что автоматическая архивация настроена. Подождите несколько минут для hello агента toobe установлены, настроены. После этого hello Azure портале будут отображаться новые параметры hello.

## <a name="configuration-with-powershell"></a>Настройка с помощью PowerShell

Можно использовать PowerShell tooconfigure v2 автоматического резервного копирования. Предварительно необходимо выполнить следующее.

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
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

Если выходных данных показано, что **включить** задано слишком**False**, то у вас есть tooenable автоматическое резервное копирование. Hello хорошие новости — Включение и настройка автоматического резервного копирования в hello таким же образом. Hello следующем разделе для получения этих сведений.

> [!NOTE] 
> Проверьте параметры hello сразу же после внесения изменений, возможно, вы получите обратно hello старые значения конфигурации. Подождите несколько минут и проверить параметры hello снова toomake том, что изменения были применены.

### <a name="configure-automated-backup-v2"></a>Настройка автоматической архивации версии 2
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

Затем с помощью hello **New AzureRmVMSqlServerAutoBackupConfig** команды tooenable и настройка резервного копирования toostore параметры hello v2 автоматического резервного копирования в учетную запись хранилища Azure hello. В этом примере hello копии создаются toobe сохраняются в течение 10 дней. Архивация системных баз данных включена. Полная архивация выполняется раз в неделю, и для нее выделяется 2-часовое временное окно, начинающееся в 20:00. Резервные копии журналов создаются каждые 30 минут. Здравствуйте, вторая команда **AzureRmVMSqlServerExtension набор**, hello обновления указано ВМ Azure с помощью этих параметров.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

Он может занять несколько минут tooinstall и настроить агент SQL Server IaaS hello. 

шифрование tooenable изменить hello предыдущего сценария toopass hello **EnableEncryption** параметра вместе с паролем (защищенной строки) для hello **CertificatePassword** параметра. Hello следующий сценарий включает параметры автоматической архивации hello в предыдущем примере hello и добавляет шифрование.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

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
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

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
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Дальнейшие действия
Служба автоматической архивации версии 2 позволяет настроить управляемую архивацию на виртуальных машинах Azure. Поэтому важно слишком[документации hello управляемого резервного копирования](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello влияние и поведение.

Можно найти созданием резервных копий и восстановление руководство по SQL Server на виртуальных машинах Azure в разделе hello: [резервное копирование и восстановление для SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-backup-recovery.md).

Сведения о других доступных задачах автоматизации см. в разделе [Расширение агента IaaS для SQL Server](virtual-machines-windows-sql-server-agent-extension.md).

Дополнительные сведения о запуске SQL Server на виртуальных машинах Azure см. в [обзоре использования SQL Server на виртуальных машинах Azure](virtual-machines-windows-sql-server-iaas-overview.md).

