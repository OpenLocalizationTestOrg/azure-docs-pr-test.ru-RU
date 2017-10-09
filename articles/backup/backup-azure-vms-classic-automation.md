---
title: "aaaDeploy и управление резервным копированием для виртуальных машин Azure с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toodeploy и управление резервным копированием Azure с помощью PowerShell."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>Использовать tooback командлеты AzureRM.Backup копирование виртуальных машин
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](backup-azure-vms-automation.md)
> * [Классический](backup-azure-vms-classic-automation.md)
>
>

В этой статье показано, как toouse Azure PowerShell для резервного копирования и восстановления виртуальных машин Azure. В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: модель Resource Manager и классическая модель. В этой статье описан с помощью tooback модели развертывания классический hello копирование данных tooa резервное хранилище. Если вы не создали резервное хранилище в вашей подписке, см. раздел hello диспетчера ресурсов версию этой статьи [tooback AzureRM.RecoveryServices.Backup используйте командлеты копирование виртуальных машин](backup-azure-vms-automation.md). Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

> [!IMPORTANT]
> Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии. Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md). Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб.<br/> После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ. **К 1 ноября 2017 года**:
>- Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.
>- Вы не будет возможности tooaccess данные резервной копии hello классического портала. Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.
>

## <a name="concepts"></a>Основные понятия
Эта статья содержит сведения о конкретных toohello командлеты PowerShell tooback копии виртуальных машин. Чтобы изучить вводные сведения о защите виртуальных машин Azure, ознакомьтесь с разделом [Планирование инфраструктуры резервного копирования виртуальных машин в Azure](backup-azure-vms-introduction.md).

> [!NOTE]
> Прежде чем начать, познакомьтесь hello [необходимые компоненты](backup-azure-vms-prepare.md) необходимые toowork с резервного копирования Azure и hello [ограничения](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) из текущего решения резервного копирования hello виртуальной Машины.
>
>

toouse PowerShell, по сути, принимают момент иерархии hello toounderstand объектов и откуда toostart.

![Иерархия объектов](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

Hello два самых важных потока включения защиты для виртуальной Машины, а восстановление данных из точки восстановления. Hello посвящена эта статья является toohelp, вы становитесь детальное представление о работе с tooenable командлеты PowerShell hello эти два сценария.

## <a name="setup-and-registration"></a>Настройка и регистрация
toobegin:

1. [Скачайте последнюю версию PowerShell](https://github.com/Azure/azure-powershell/releases) (минимальная требуемая версия — 1.0.0)
2. Находите hello доступных командлетов Azure PowerShell резервного копирования с помощью hello следующую команду:

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

Hello следующие программы установки и регистрации задачи можно автоматизировать с помощью PowerShell:

* создать хранилище архивации;
* Регистрация виртуальных машин hello hello службы архивации Azure

### <a name="create-a-backup-vault"></a>создать хранилище архивации;
> [!WARNING]
> Для клиентов, использующих Azure Backup для hello первый раз необходимо использовать с вашей подпиской поставщика toobe tooregister hello Azure Backup. Это можно сделать, выполнив следующую команду hello: Register AzureRmResourceProvider - ProviderNamespace «Microsoft.Backup»
>
>

Можно создать новое хранилище резервных копий с помощью hello **New AzureRmBackupVault** командлета. резервное хранилище Hello является ресурс ARM, поэтому вам необходимо tooplace его в группе ресурсов. В консоли Azure PowerShell с повышенными привилегиями выполните hello, следующие команды:

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Можно получить список всех резервных хранилищ hello в данной подписке с помощью hello **Get AzureRmBackupVault** командлета.

> [!NOTE]
> — Это удобный toostore hello резервного хранилища объект в переменную. Hello объекта хранилища, необходимое в качестве входных данных для многих командлеты службы архивации Azure.
>
>

### <a name="registering-hello-vms"></a>Регистрация виртуальных машин hello
Hello первым шагом к настройке резервного копирования с помощью службы архивации Azure является tooregister компьютер или ВМ с Azure резервного хранилища. Hello **AzureRmBackupContainer регистра** командлет принимает входные данные для hello виртуальной машины Azure IaaS и регистрирует его с указанным хранилищем hello. Операция register Hello связывает hello виртуальной машины Azure с резервным хранилищем hello и отслеживает hello ВМ жизненного цикла резервного копирования hello.

Регистрация ВМ с hello службы архивации Azure создает объект верхнего уровня контейнера. Контейнер обычно содержит несколько элементов, которые можно архивировать, но в случае hello виртуальных машин будет только один элемент резервного копирования для контейнера hello.

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>Виртуальные машины службы архивации Azure
### <a name="create-a-protection-policy"></a>Создание политики защиты
Это не обязательное toocreate новую резервную копию toostart защиты политики виртуальных машин. хранилище Hello поставляется с «политика по умолчанию», можно использовать tooquickly включить защиту и затем hello правой сведения изменены позже. Список политик hello, доступных в хранилище hello можно получить с помощью hello **Get AzureRmBackupProtectionPolicy** командлета:

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> часовой пояс Hello поля BackupTime hello в PowerShell — в формате UTC. Тем не менее при отображении hello время резервного копирования в hello портал Azure, часовой пояс hello является выровненных tooyour local system вместе со смещением hello UTC.
>
>

Политика резервного копирования связана по крайней мере с одной политикой хранения. Политика хранения Hello определяет, как долго точки восстановления хранится в службе архивации Azure. Hello **New AzureRmBackupRetentionPolicy** командлет создает объекты PowerShell, которые содержат сведения о политике хранения. Эти объекты политики хранения используются как входные данные toohello *New AzureRmBackupProtectionPolicy* командлета, или непосредственно с hello *Enable AzureRmBackupProtection* командлета.

Политики резервного копирования определяет, когда и как часто hello выполняется резервное копирование элемента. Hello **New AzureRmBackupProtectionPolicy** командлет создает объект PowerShell, который содержит сведения о политике резервного копирования. Hello политику резервного копирования используется в качестве входного toohello *Enable AzureRmBackupProtection* командлета.

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>Включить защиту
Включение защиты включает в себя два объекта - hello элемента и hello политики и оба toohello toobelong необходимость же хранилища. После hello политики связан с элементом hello, рабочий процесс резервного копирования hello включится на определенное расписание hello.

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>Начальное резервное копирование
расписание резервного копирования Hello позаботится сделать hello полной первоначальной копии элемента hello и добавочного копирования hello для hello последующие резервные копии. Однако если требуется tooforce hello начальной резервной копии toohappen в определенное время или даже немедленно используйте hello **AzureRmBackupItem резервного копирования** командлета:

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> Здравствуйте, часовой пояс hello StartTime и EndTime поля, показанные в PowerShell — в формате UTC. При отображении hello аналогичные сведения в hello портал Azure, часовой пояс hello то, выровненные tooyour локальные системные часы.
>
>

### <a name="monitoring-a-backup-job"></a>Наблюдение за выполнением задания резервного копирования
Большинство длительных операций службы архивации Azure моделируются в виде задания. Это позволяет легко tootrack выполняется без необходимости tookeep hello Azure откройте портал в любое время.

Последнее состояние tooget hello выполняющиеся задания, используйте hello **Get AzureRmBackupJob** командлета.

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

Вместо опроса эти задания для завершения — то есть ненужные, дополнительный код - это проще hello toouse **AzureRmBackupJob ожидания** командлета. При использовании в скрипте hello командлет приостанавливает hello выполнения до завершения задания hello или hello указано, что достигнуто значение тайм-аута.

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>Восстановление виртуальной машины Azure
В порядке toorestore резервных копий данных необходимо tooidentify hello архивных элементов и точки восстановления hello, содержащий данные на момент hello. Эта информация является tooinitiate командлет предоставленного toohello восстановление AzureRmBackupItem восстановления данных из учетной записи клиента toohello hello хранилища.

### <a name="select-hello-vm"></a>Выберите hello виртуальной Машины
tooget hello PowerShell объект, определяющий Здравствуйте элемент право резервного копирования, вы должны toostart из hello контейнера в хранилище hello и постепенно вниз по иерархии объектов. tooselect hello контейнера, представляющий hello виртуальной Машины, используйте hello **Get AzureRmBackupContainer** командлета и передать этот toohello **Get AzureRmBackupItem** командлета.

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>Выбор точки восстановления
Теперь можно получить список всех точек восстановления hello hello резервное копирование элемента с помощью hello **Get AzureRmBackupRecoveryPoint** командлет и выберите toorestore точки восстановления hello. Обычно пользователи выбирается hello последней *AppConsistent* указывают в списке hello.

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

переменная приветствия ```$rp``` является массивом точек восстановления для hello выбран элемент резервного копирования, сортируются в обратном порядке времени — hello последняя точка восстановления находится по индексу 0. Используйте обычный массив PowerShell индексирования точки восстановления toopick hello. Например: ```$rp[0]``` выберет hello последней точки восстановления.

### <a name="restoring-disks"></a>Восстановление дисков
Отсутствует ключевое различие между операциями восстановления hello сделать hello портал Azure и Azure PowerShell. С помощью PowerShell операция восстановления hello останавливается на восстановление из точки восстановления hello hello диски и сведения о конфигурации. Она не создает виртуальную машину.

> [!WARNING]
> Hello AzureRmBackupItem восстановления не создает виртуальную Машину. Восстанавливает только диски hello toohello указана учетная запись хранения. Это не является hello такое же поведение, будет наблюдаться в hello портал Azure.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

Можно получить сведения hello hello операции восстановления, используя hello **Get AzureRmBackupJobDetails** командлета, после завершения задания восстановления hello. Hello *ErrorDetails* свойство будет hello сведения о необходимости toorebuild hello виртуальной Машины.

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>Построение hello виртуальной Машины
Построение hello виртуальной Машины из hello восстановить диски можно сделать с помощью старых командлетов Azure Service Management PowerShell hello, hello новых шаблонов диспетчера ресурсов Azure, или даже при использовании hello портал Azure. В краткий пример, будет показано, как tooget существует, с помощью командлетов для управления службой Azure hello.

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

Дополнительные сведения о том, как toobuild ВМ с hello восстановления дисков, узнайте, как hello следующие командлеты:

* [Add-AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [New-AzureVMConfig](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [New-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>Примеры кода
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1. Получить состояние завершения hello задания дополнительных задач
состояние завершения hello tootrack отдельных вложенных задач, можно использовать hello **Get AzureRmBackupJobDetails** командлета:

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2. Создание ежедневного или еженедельного отчета для задач резервного копирования
Администраторы обычно требуется, какие задания резервного копирования выполнялись в hello последние 24 часа, tooknow hello состояние этих заданий резервного копирования. Кроме того, hello объем передаваемых данных позволяет администраторам tooestimate способ их ежемесячное использование данных. Приведенный ниже сценарий Hello hello необработанные данные извлекаются из службы архивации Azure hello и отображает hello сведения в консоли PowerShell hello.

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

Tooadd построения диаграмм возможности вывода отчета toothis следует узнать из блога TechNet hello [построения диаграмм с помощью PowerShell](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>Дальнейшие действия
Если вы предпочитаете PowerShell tooengage с ресурсами Azure, ознакомиться с hello статье PowerShell для защиты Windows Server [развертывание и управление резервного копирования для Windows Server](backup-client-automation-classic.md). Доступна и другая статья, посвященная тому, как использовать PowerShell для управления службой архивации DPM: [Развертывание службы архивации для DPM и управление ею](backup-dpm-automation-classic.md). Обе эти статьи имеют две версии — для развертывания с помощью Resource Manager и для классической модели развертывания.
