---
title: "aaaDeploy и управлять резервными копиями для развертывания диспетчера ресурсов виртуальных машин с помощью PowerShell | Документы Microsoft"
description: "Использование PowerShell toodeploy и управление ими резервных копий в Azure для развертывания диспетчера ресурсов виртуальных машин"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 68606e4f-536d-4eac-9f80-8a198ea94d52
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/28/2017
ms.author: markgal;trinadhk
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486fb3ae1902403fe6bf303df57244b76677ab17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermrecoveryservicesbackup-cmdlets-tooback-up-virtual-machines"></a>Использовать tooback командлеты AzureRM.RecoveryServices.Backup копирование виртуальных машин
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов](backup-azure-vms-automation.md)
> * [Классический](backup-azure-vms-classic-automation.md)
>
>

В этой статье показано, как хранилище tooback командлеты Azure PowerShell toouse копирование и восстановление из службы восстановления Azure виртуальной машины (VM). Хранилище служб восстановления — ресурс диспетчера ресурсов Azure и tooprotect используемых данных и средств в службах архивации Azure и Azure Site Recovery. Можно использовать tooprotect хранилище служб восстановления Azure Service Manager развернутые виртуальные машины и виртуальные машины на развертывания диспетчера ресурсов Azure.

> [!NOTE]
> В Azure предусмотрены две модели развертывания, позволяющие создавать ресурсы и работать с ними: [модель Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). Эта статья предназначена для использования с виртуальными машинами, созданных с помощью модели hello диспетчера ресурсов.
>
>

В этой статье описывается с помощью PowerShell tooprotect виртуальной Машины и восстановление данных из точки восстановления.

## <a name="concepts"></a>Основные понятия
Если вы не знакомы с hello службы архивации Azure, общие сведения о службе hello извлечь [возможности резервного копирования Azure?](backup-introduction-to-azure-backup.md) Прежде чем начать, убедитесь, что охватывают hello essentials о toowork hello предварительных требований с помощью Azure Backup и hello ограничения текущее решение резервного копирования hello виртуальной Машины.

toouse PowerShell по сути, это необходимые toounderstand hello иерархия объектов и откуда toostart.

![Иерархия объектов служб восстановления](./media/backup-azure-vms-arm-automation/recovery-services-object-hierarchy.png)

hello tooview Справочник по командлетам AzureRm.RecoveryServices.Backup PowerShell, в разделе hello [архивации Azure — командлеты служб восстановления](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup) в hello библиотека Azure.

## <a name="setup-and-registration"></a>Настройка и регистрация
toobegin:

1. [Загрузка последней версии PowerShell hello](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) (hello Минимальная требуемая версия —: 1.4.0)
2. Находите hello доступных командлетов Azure PowerShell резервного копирования с помощью hello следующую команду:

```
PS C:\> Get-Command *azurermrecoveryservices*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmRecoveryServicesBackupItem           1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Disable-AzureRmRecoveryServicesBackupProtection    1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Enable-AzureRmRecoveryServicesBackupProtection     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupContainer         1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupItem              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJob               1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupJobDetails        1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupManagementServer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRMRecoveryServicesBackupRecoveryPoint     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupRetentionPolic... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesBackupSchedulePolicy... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Get-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Get-AzureRmRecoveryServicesVaultSettingsFile       1.4.0      AzureRM.RecoveryServices
Cmdlet          New-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          New-AzureRmRecoveryServicesVault                   1.4.0      AzureRM.RecoveryServices
Cmdlet          Remove-AzureRmRecoveryServicesProtectionPolicy     1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Remove-AzureRmRecoveryServicesVault                1.4.0      AzureRM.RecoveryServices
Cmdlet          Restore-AzureRMRecoveryServicesBackupItem          1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesBackupProperties        1.4.0      AzureRM.RecoveryServices
Cmdlet          Set-AzureRmRecoveryServicesBackupProtectionPolicy  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Set-AzureRmRecoveryServicesVaultContext            1.4.0      AzureRM.RecoveryServices
Cmdlet          Stop-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupContainer  1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Unregister-AzureRmRecoveryServicesBackupManagem... 1.4.0      AzureRM.RecoveryServices.Backup
Cmdlet          Wait-AzureRmRecoveryServicesBackupJob              1.4.0      AzureRM.RecoveryServices.Backup
```


с помощью PowerShell можно автоматизировать Hello следующие задачи:

* Создание хранилища служб восстановления
* Резервное копирование виртуальных машин Azure
* активация задания архивации;
* наблюдение за выполнением задания архивации;
* Восстановление виртуальной машины Azure

## <a name="create-a-recovery-services-vault"></a>Создание хранилища служб восстановления
Привет, следующие шаги, чтобы привести по созданию хранилище служб восстановления. Хранилище служб восстановления отличается от хранилища службы архивации.

1. При использовании резервного копирования Azure для hello первый раз, необходимо использовать hello  **[регистра AzureRmResourceProvider](http://docs.microsoft.com/powershell/module/azurerm.resources/register-azurermresourceprovider)**  поставщика службы восстановления Azure hello tooregister командлетов с вашей подпиской.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hello хранилище служб восстановления является ресурса диспетчера ресурсов, поэтому вам необходимо tooplace его в группе ресурсов. Можно использовать существующую группу ресурсов или создайте группу ресурсов с hello  **[New AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresourcegroup)**  командлета. При создании группы ресурсов, укажите hello имя и расположение для группы ресурсов hello.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Используйте hello  **[New AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault)**  hello toocreate командлет хранилище служб восстановления. Убедитесь, что toospecify hello одинаковое расположение для hello хранилище, которое использовалось для группы ресурсов hello.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Укажите тип hello toouse избыточности хранилища; можно использовать [локально избыточное хранилище (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) или [географически избыточное хранилище (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello следующий пример демонстрирует hello - BackupStorageRedundancy для testvault был установлен tooGeoRedundant.

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testvault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -Vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

   > [!TIP]
   > Многие командлеты службы архивации Azure в качестве входных данных необходим объект хранилища служб восстановления hello. По этой причине — это объект хранилища служб восстановления резервной копии удобный toostore hello в переменной.
   >
   >

## <a name="view-hello-vaults-in-a-subscription"></a>Представление hello хранилища в подписке
Используйте  **[Get AzureRmRecoveryServicesVault](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/get-azurermrecoveryservicesvault)**  tooview hello список всех хранилищ в текущей подписке hello. Можно использовать этот toocheck команд, созданного новое хранилище, или toosee hello хранилищ, доступных в подписке hello.

Запустите команду Get-AzureRmRecoveryServicesVault tooview hello всех хранилищ в подписке hello. Hello пример hello сведений, отображаемых для каждого хранилища.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="back-up-azure-vms"></a>Резервное копирование виртуальных машин Azure
Используйте хранилище служб восстановления tooprotect виртуальные машины. Перед установкой защиты hello hello в контексте хранилища (тип данных, защищенных в хранилище hello hello) и проверьте политику защиты hello. Политика защиты Hello — hello планирование запуска заданий резервного копирования hello и длительность хранения каждого резервного копирования моментального снимка.

### <a name="set-vault-context"></a>Задание контекста хранилища
Прежде чем включать защиту на виртуальной Машине, используйте  **[набор AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset hello хранилище контекста. После установки контекста хранилище hello, оно применяется tooall последующими командлетами. Hello следующий пример устанавливает hello хранилище контекст для хранилища hello *testvault*.

```
PS C:\> Get-AzureRmRecoveryServicesVault -Name "testvault" | Set-AzureRmRecoveryServicesVaultContext
```

### <a name="create-a-protection-policy"></a>Создание политики защиты
Создаваемое хранилище служб восстановления поставляется с политиками защиты и хранения по умолчанию. Политика защиты по умолчанию Hello триггеры задания резервного копирования каждый день в указанное время. политики хранения по умолчанию Hello хранит hello ежедневных точки восстановления в течение 30 дней. Можно использовать по умолчанию hello tooquickly политики защиты виртуальной Машины и изменение политики hello позже с помощью различных сведений.

Используйте  **[Get AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupprotectionpolicy)**  tooview политики защиты hello в хранилище hello. Можно использовать этот командлет tooget определенной политике или tooview hello политики, связанные с типом рабочей нагрузки. Следующий пример Hello получает политики для типа рабочей нагрузки, AzureVM.

```
PS C:\> Get-AzureRmRecoveryServicesBackupProtectionPolicy -WorkloadType "AzureVM"
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
DefaultPolicy        AzureVM            AzureVM              4/14/2016 5:00:00 PM
```

> [!NOTE]
> часовой пояс Hello поля BackupTime hello в PowerShell — в формате UTC. Тем не менее если в hello портал Azure показано время резервного копирования hello, hello при скорректированное tooyour местном часовом поясе.
>
>

Политика защиты архивации связана по крайней мере с одной политикой хранения. Политика хранения определяет продолжительность хранения точки восстановления до ее удаления. Используйте  **[Get AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupretentionpolicyobject)**  политики хранения по умолчанию hello tooview.  Аналогично можно использовать  **[Get AzureRmRecoveryServicesBackupSchedulePolicyObject](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupschedulepolicyobject)**  tooobtain hello по умолчанию расписание политики. Hello  **[New AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  командлет создает объект PowerShell, который содержит сведения о политике резервного копирования. Hello расписание и хранения объектов политики используются как входные данные toohello  **[New AzureRmRecoveryServicesBackupProtectionPolicy](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy)**  командлета. Hello следующий пример сохраняет расписание hello и политика хранения hello в переменных. пример Hello использует эти переменные toodefine hello параметры при создании политики защиты, *NewPolicy*.

```
PS C:\> $schPol = Get-AzureRmRecoveryServicesBackupSchedulePolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> New-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy" -WorkloadType "AzureVM" -RetentionPolicy $retPol -SchedulePolicy $schPol
Name                 WorkloadType       BackupManagementType BackupTime                DaysOfWeek
----                 ------------       -------------------- ----------                ----------
NewPolicy           AzureVM            AzureVM              4/24/2016 1:30:00 AM
```


### <a name="enable-protection"></a>Включить защиту
После определения политики резервного копирования защиты hello по-прежнему необходимо включить hello политики для элемента. Используйте  **[Enable AzureRmRecoveryServicesBackupProtection](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/enable-azurermrecoveryservicesbackupprotection)**  tooenable защиты. Включение защиты требуется два объекта - элемент hello и политики hello. После hello политики связан с хранилищем hello, во время hello, определенные в расписание политики hello активации рабочего процесса резервного копирования hello.

После защиты включает пример hello элемента, V2VM, с помощью политики hello NewPolicy Hello. tooenable hello защиту для виртуальных машин диспетчера ресурсов без шифрования

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

tooenable hello защиты на шифрование виртуальных машин (шифрование с помощью BEK и KEK), необходимо toogive hello Azure Backup service разрешение tooread ключи и секретные данные из хранилища ключей.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToKeys backup,get,list -PermissionsToSecrets get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

tooenable hello защиты на шифрование виртуальных машин (шифрование только с помощью BEK), необходимо toogive hello Azure Backup service разрешение tooread секретов из хранилища ключей.

```
PS C:\> Set-AzureRmKeyVaultAccessPolicy -VaultName "KeyVaultName" -ResourceGroupName "RGNameOfKeyVault" -PermissionsToSecrets backup,get,list -ServicePrincipalName 262044b1-e2ce-469f-a196-69ab7ada62d3
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V2VM" -ResourceGroupName "RGName1"
```

> [!NOTE]
> При использовании облако Azure для государственных hello, затем использовать ff281ffe-705c-4f53-9f37-a40e6f2c68f3 hello значение для параметра hello **- ServicePrincipalName** в [Set-AzureRmKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) командлета .
>
>

Классические виртуальные машины

```
PS C:\> $pol=Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Enable-AzureRmRecoveryServicesBackupProtection -Policy $pol -Name "V1VM" -ServiceName "ServiceName1"
```

### <a name="modify-a-protection-policy"></a>Изменение политики защиты
Политика защиты hello toomodify, используйте [AzureRmRecoveryServicesBackupProtectionPolicy набор](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/set-azurermrecoveryservicesbackupprotectionpolicy) hello toomodify SchedulePolicy или RetentionPolicy объектов.

Hello следующий пример изменяет количество дней too365 хранения точки восстановления hello.

```
PS C:\> $retPol = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType "AzureVM"
PS C:\> $retPol.DailySchedule.DurationCountInDays = 365
PS C:\> $pol= Get-AzureRmRecoveryServicesBackupProtectionPolicy -Name "NewPolicy"
PS C:\> Set-AzureRmRecoveryServicesBackupProtectionPolicy -Policy $pol  -RetentionPolicy $RetPol
```

## <a name="trigger-a-backup"></a>Активация архивации
Можно использовать  **[резервного копирования AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/backup-azurermrecoveryservicesbackupitem)**  tootrigger задания резервного копирования. Если это hello начальной резервной копии, это полное резервное копирование. При последующем выполнении архивации резервная копия будет добавочной. Быть убедиться, что toouse  **[набор AzureRmRecoveryServicesVaultContext](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)**  tooset контекст хранилища hello перед тем как запускать задание резервного копирования hello. Следующий пример Hello предполагается, что был задан контекст хранилища.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer -ContainerType "AzureVM" -Status "Registered" -FriendlyName "V2VM"
PS C:\> $item = Get-AzureRmRecoveryServicesBackupItem -Container $namedContainer -WorkloadType "AzureVM"
PS C:\> $job = Backup-AzureRmRecoveryServicesBackupItem -Item $item
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM              Backup               InProgress            4/23/2016 5:00:30 PM                       cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

> [!NOTE]
> часовой пояс Hello hello StartTime и EndTime полей в PowerShell — в формате UTC. Тем не менее если в hello портал Azure показано время hello, hello при скорректированное tooyour местном часовом поясе.
>
>

## <a name="monitoring-a-backup-job"></a>Наблюдение за выполнением задания резервного копирования
Длительные операции, например задания резервного копирования можно отслеживать без использования hello портал Azure. состояние hello tooget выполняющиеся задания, используйте hello  **[Get AzureRmRecoveryservicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjob)**  командлета. Этот командлет возвращает hello заданий резервного копирования для конкретного хранилища и хранилище, указан в контексте хранилища hello. Hello следующий пример возвращает hello состояние выполняющегося задания как массив и сохраняет состояние hello в hello $joblist переменной.

```
PS C:\> $joblist = Get-AzureRmRecoveryservicesBackupJob –Status "InProgress"
PS C:\> $joblist[0]
WorkloadName     Operation            Status               StartTime                 EndTime                   JobID
------------     ---------            ------               ---------                 -------                   ----------
V2VM             Backup               InProgress            4/23/2016 5:00:30 PM           cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Вместо опроса эти задания для завершения — которая представляет требуется дополнительный код - использовать hello  **[ожидания AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  командлета. Этот командлет приостанавливает работу hello, до завершения задания hello или hello указано, что достигнуто значение тайм-аута.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $joblist[0] -Timeout 43200
```

## <a name="restore-an-azure-vm"></a>Восстановление виртуальной машины Azure
Отсутствует ключевое различие между hello восстановление виртуальной Машины с помощью портала Azure hello и восстановление виртуальной Машины с помощью PowerShell. С помощью PowerShell hello операция восстановления завершена, создав hello диски и сведения о конфигурации из точки восстановления hello.

> [!NOTE]
> Операция восстановления Hello не создает виртуальную машину.
>
>

toocreate виртуальной машины с диска, см. раздел hello [hello Создание виртуальной Машины из хранимых дисков](backup-azure-vms-automation.md#create-a-vm-from-stored-disks). приведены основные шаги Hello toorestore ВМ Azure.

* Выберите hello виртуальной Машины
* Выбор точки восстановления
* Восстановление дисков hello
* Создание виртуальной Машины hello из хранимых дисков

Hello на рисунке показана иерархия hello объекта из hello RecoveryServicesVault вниз toohello BackupRecoveryPoint.

![Иерархия объектов служб восстановления с BackupContainer](./media/backup-azure-vms-arm-automation/backuprecoverypoint-only.png)

toorestore резервных копий данных, определите hello резервную копию элемента и точки восстановления hello, содержащий данные на момент hello. Используйте hello  **[восстановления AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toohello пользовательской учетной записи в хранилище данных toorestore командлета из hello.

### <a name="select-hello-vm"></a>Выберите hello виртуальной Машины
tooget hello PowerShell объект, определяющий hello справа резервное копирование элемента, запустите из контейнера hello в хранилище hello и постепенно вниз по иерархии объектов hello. tooselect hello контейнера, представляющий hello виртуальной Машины, используйте hello  **[Get AzureRmRecoveryServicesBackupContainer](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)**  командлета и передать этот toohello  **[ Get-AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)**  командлета.

```
PS C:\> $namedContainer = Get-AzureRmRecoveryServicesBackupContainer  -ContainerType "AzureVM" –Status "Registered" -FriendlyName "V2VM"
PS C:\> $backupitem = Get-AzureRmRecoveryServicesBackupItem –Container $namedContainer  –WorkloadType "AzureVM"
```

### <a name="choose-a-recovery-point"></a>Выбор точки восстановления
Используйте hello  **[Get AzureRmRecoveryServicesBackupRecoveryPoint](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)**  toolist командлет се точки восстановления для архивации элемента hello. Выберите toorestore точки восстановления hello. Если вы не уверены, какие toouse точки восстановления, это toochoose хорошей практикой hello последней RecoveryPointType = AppConsistent пункт в списке hello.

В следующий скрипт hello, hello переменной, **$rp**, представляет собой массив из точки восстановления для hello выбранных резервное копирование элемента из hello за последние семь дней. время с последней точки восстановления hello с индексом 0 Hello массива сортируются в обратном порядке. Используйте обычный массив PowerShell индексирования точки восстановления toopick hello. В примере hello $rp [0] выбирает hello последней точки восстановления.

```
PS C:\> $startDate = (Get-Date).AddDays(-7)
PS C:\> $endDate = Get-Date
PS C:\> $rp = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $backupitem -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
PS C:\> $rp[0]
RecoveryPointAdditionalInfo :
SourceVMStorageType         : NormalStorage
Name                        : 15260861925810
ItemName                    : VM;iaasvmcontainer;RGName1;V2VM
RecoveryPointId             : /subscriptions/XX/resourceGroups/ RGName1/providers/Microsoft.RecoveryServices/vaults/testvault/backupFabrics/Azure/protectionContainers/IaasVMContainer;iaasvmcontainer;RGName1;V2VM/protectedItems/VM;iaasvmcontainer; RGName1;V2VM/recoveryPoints/15260861925810
RecoveryPointType           : AppConsistent
RecoveryPointTime           : 4/23/2016 5:02:04 PM
WorkloadType                : AzureVM
ContainerName               : IaasVMContainer;iaasvmcontainer; RGName1;V2VM
ContainerType               : AzureVM
BackupManagementType        : AzureVM
```



### <a name="restore-hello-disks"></a>Восстановление дисков hello
Используйте hello  **[восстановления AzureRmRecoveryServicesBackupItem](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/restore-azurermrecoveryservicesbackupitem)**  toorestore командлет элемент резервного копирования данных и конфигурации tooa точек восстановления. После идентификации точки восстановления используется в качестве hello значения для hello **- RecoveryPoint** параметра. В предыдущем примере кода hello **$rp [0]** было toouse точки восстановления hello. В следующий пример кода hello **$rp [0]** — hello toouse точки восстановления для восстановления диска hello.

toorestore hello диски и сведения о конфигурации:

```
PS C:\> $restorejob = Restore-AzureRmRecoveryServicesBackupItem -RecoveryPoint $rp[0] -StorageAccountName "DestAccount" -StorageAccountResourceGroupName "DestRG"
PS C:\> $restorejob
WorkloadName     Operation          Status               StartTime                 EndTime            JobID
------------     ---------          ------               ---------                 -------          ----------
V2VM              Restore           InProgress           4/23/2016 5:00:30 PM                        cf4b3ef5-2fac-4c8e-a215-d2eba4124f27
```

Используйте hello  **[ожидания AzureRmRecoveryServicesBackupJob](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/wait-azurermrecoveryservicesbackupjob)**  toowait командлет для задания toocomplete hello восстановления.

```
PS C:\> Wait-AzureRmRecoveryServicesBackupJob -Job $restorejob -Timeout 43200
```

После завершения задания восстановления hello использовать hello  **[Get AzureRmRecoveryServicesBackupJobDetails](https://docs.microsoft.com/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupjobdetails)**  командлет tooget hello и подробные сведения о hello операции восстановления. Hello JobDetails свойство имеет hello toorebuild необходимые сведения hello виртуальной Машины.

```
PS C:\> $restorejob = Get-AzureRmRecoveryServicesBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmRecoveryServicesBackupJobDetails -Job $restorejob
```

После восстановления дисков hello перехода toohello Далее раздел toocreate hello виртуальной Машины.

## <a name="create-a-vm-from-restored-disks"></a>Создание виртуальной машины с восстановленного диска
После восстановления дисков hello, выполните эти шаги toocreate и настроить hello виртуальную машину с диска.

> [!NOTE]
> toocreate шифрования виртуальные машины с восстановленные диски, роли Azure должен иметь действие hello tooperform разрешения, **Microsoft.KeyVault/vaults/deploy/action**. Если у роли нет этого разрешения, создайте пользовательскую роль с этим действием. Дополнительные сведения см. в разделе [Пользовательские роли в Azure RBAC](../active-directory/role-based-access-control-custom-roles.md).
>
>

1. Запрос hello восстановить свойства диска для сведений о задании hello.

  ```
  PS C:\> $properties = $details.properties
  PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
  PS C:\> $containerName = $properties["Config Blob Container Name"]
  PS C:\> $blobName = $properties["Config Blob Name"]
  ```

2. Задать контекст хранилища Azure hello и восстановите файл конфигурации JSON hello.

    ```
    PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName "testvault"
    PS C:\> $destination_path = "C:\vmconfig.json"
    PS C:\> Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path
    PS C:\> $obj = ((Get-Content -Path $destination_path -Raw -Encoding Unicode)).TrimEnd([char]0x00) | ConvertFrom-Json
    ```

3. Используйте hello файл конфигурации JSON toocreate конфигурацию виртуальной Машины hello.

    ```
   PS C:\> $vm = New-AzureRmVMConfig -VMSize $obj.'properties.hardwareProfile'.vmSize -VMName "testrestore"
    ```

4. Присоедините диск hello ОС и дисков данных. В зависимости от конфигурации hello виртуальных машин щелкните hello соответствующую ссылку tooview соответствующих командлетов: 
    - [Неуправляемые, без шифрования виртуальные машины](#non-managed-non-encrypted-vms)
    - [Неуправляемые, зашифрованный виртуальных машин (BEK)](#non-managed-encrypted-vms-bek-only)
    - [Виртуальные машины неуправляемые, зашифрованный (BEK и Ключами)](#non-managed-encrypted-vms-bek-and-kek)
    - [Управляемые без шифрования виртуальные машины](#managed-non-encrypted-vms)
    - [Виртуальные машины управляемых, зашифрованный (BEK и Ключами)](#managed-encrypted-vms-bek-and-kek)
    
    #### <a name="non-managed-non-encrypted-vms"></a>Неуправляемые незашифрованные виртуальные машины

    Используйте следующий пример для виртуальных машин под управлением, незашифрованные hello.

    ```
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.StorageProfile'.osDisk.vhd.Uri -CreateOption "Attach"
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.StorageProfile'.OsDisk.OsType
    PS C:\> foreach($dd in $obj.'properties.StorageProfile'.DataDisks)
    {
    $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="non-managed-encrypted-vms-bek-only"></a>Неуправляемые зашифрованные виртуальные машины (только BEK)

    Для неуправляемых, зашифрованный ВМ (шифрование только с помощью BEK) необходимо toorestore hello toohello секретного ключа хранилища для присоединения дисков. Дополнительные сведения см. в разделе статьи hello [восстановление зашифрованных виртуальной машине из точки восстановления в Azure Backup](backup-azure-restore-key-secret.md). Следующий образец Hello показан способ tooattach ОС и дисков данных для шифрования виртуальных машин.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="non-managed-encrypted-vms-bek-and-kek"></a>Неуправляемые зашифрованные виртуальные машины (BEK и KEK)

    Для неуправляемых, зашифрованный ВМ (шифрование с помощью BEK и Ключами) требуется ключ toorestore hello и toohello секрета хранилища ключей для присоединения дисков. Дополнительные сведения см. в разделе статьи hello [восстановление зашифрованных виртуальной машине из точки восстановления в Azure Backup](backup-azure-restore-key-secret.md). Следующий образец Hello показан способ tooattach ОС и дисков данных для шифрования виртуальных машин.

    ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -Name "osdisk" -VhdUri $obj.'properties.storageProfile'.osDisk.vhd.uri -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> $vm.StorageProfile.OsDisk.OsType = $obj.'properties.storageProfile'.osDisk.osType
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $vm = Add-AzureRmVMDataDisk -VM $vm -Name "datadisk1" -VhdUri $dd.vhd.Uri -DiskSizeInGB 127 -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

    #### <a name="managed-non-encrypted-vms"></a>Управляемые незашифрованные виртуальные машины

    Для управляемых незашифрованные виртуальных машин будет необходимо управлять toocreate диска из хранилища больших двоичных объектов, а затем подключите диски hello. Подробные сведения см. в статье hello, [присоединения tooa диска данных виртуальной Машины Windows с помощью PowerShell](../virtual-machines/windows/attach-disk-ps.md). Привет, следующий пример кода показывает, как tooattach hello диски данных для управляемых виртуальных машин без шифрования.

    ```
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
    }
    ```

    #### <a name="managed-encrypted-vms-bek-and-kek"></a>Управляемые зашифрованные виртуальные машины (BEK и KEK)

    Для управляемых зашифрованные виртуальных машин (шифрование с помощью BEK и Ключами) будет требуется toocreate управляемых дисков из хранилища больших двоичных объектов, а затем подключите диски hello. Подробные сведения см. в статье hello, [присоединения tooa диска данных виртуальной Машины Windows с помощью PowerShell](../virtual-machines/windows/attach-disk-ps.md). Hello следующем образце кода показано, как tooattach hello диски с данными для виртуальных машин, управляемых зашифрованные.

     ```
    PS C:\> $dekUrl = "https://ContosoKeyVault.vault.azure.net:443/secrets/ContosoSecret007/xx000000xx0849999f3xx30000003163"
    PS C:\> $kekUrl = "https://ContosoKeyVault.vault.azure.net:443/keys/ContosoKey007/x9xxx00000x0000x9b9949999xx0x006"
    PS C:\> $keyVaultId = "/subscriptions/abcdedf007-4xyz-1a2b-0000-12a2b345675c/resourceGroups/ContosoRG108/providers/Microsoft.KeyVault/vaults/ContosoKeyVault"
    PS C:\> $storageType = "StandardLRS"
    PS C:\> $osDiskName = $vm.Name + "_osdisk"
    PS C:\> $osVhdUri = $obj.'properties.storageProfile'.osDisk.vhd.uri
    PS C:\> $diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $osVhdUri
    PS C:\> $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk $diskConfig -ResourceGroupName "test"
    PS C:\> Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -DiskEncryptionKeyUrl $dekUrl -DiskEncryptionKeyVaultId $keyVaultId -KeyEncryptionKeyUrl $kekUrl -KeyEncryptionKeyVaultId $keyVaultId -CreateOption "Attach" -Windows
    PS C:\> foreach($dd in $obj.'properties.storageProfile'.dataDisks)
     {
     $dataDiskName = $vm.Name + $dd.name ;
     $dataVhdUri = $dd.vhd.uri ;
     $dataDiskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location "West US" -CreateOption Import -SourceUri $dataVhdUri ;
     $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk $dataDiskConfig -ResourceGroupName "test" ;
     Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -ManagedDiskId $dataDisk2.Id -Lun $dd.Lun -CreateOption "Attach"
     }
    ```

5. Чтобы задайте параметры сети hello.

    ```
    PS C:\> $nicName="p1234"
    PS C:\> $pip = New-AzureRmPublicIpAddress -Name $nicName -ResourceGroupName "test" -Location "WestUS" -AllocationMethod Dynamic
    PS C:\> $vnet = Get-AzureRmVirtualNetwork -Name "testvNET" -ResourceGroupName "test"
    PS C:\> $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName "test" -Location "WestUS" -SubnetId $vnet.Subnets[$subnetindex].Id -PublicIpAddressId $pip.Id
    PS C:\> $vm=Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    ```
6. Создайте виртуальную машину hello.

    ```    
    PS C:\> New-AzureRmVM -ResourceGroupName "test" -Location "WestUS" -VM $vm
    ```

## <a name="next-steps"></a>Дальнейшие действия
Если вы предпочитаете toouse PowerShell tooengage с ресурсами Azure, см статью PowerShell hello, [развертывание и управление резервного копирования для Windows Server](backup-client-automation.md). Если вы управляете операции резервного копирования DPM, см. в статье hello [развертывание и управление резервным копированием для DPM](backup-dpm-automation.md). Обе эти статьи имеют две версии — для развертывания с помощью Resource Manager и для классической модели развертывания.  
