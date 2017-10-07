---
title: "tooback PowerShell aaaUse копии Windows Server tooAzure | Документы Microsoft"
description: "Узнайте, как toodeploy и управление резервным копированием Azure с помощью PowerShell"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>Развертывание и управление ими tooAzure резервного копирования для клиента Windows Server и Windows с помощью PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [Классический](backup-client-automation-classic.md)
>
>

В этой статье показано, как toouse PowerShell для настройки резервного копирования Azure на Windows Server или на клиенте Windows и управление резервного копирования и восстановления.

## <a name="install-azure-powershell"></a>Установка Azure PowerShell
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Эта статья посвящена hello диспетчера ресурсов Azure (ARM) и hello MS Online Backup PowerShell командлеты, позволяющие toouse хранилище служб восстановления в группе ресурсов.

Версия Azure PowerShell 1.0 была выпущена в октябре 2015 г. В этом выпуске успешно hello 0.9.8 выпуска и приводящими существенные изменения, особенно в шаблон именования hello hello командлетов. 1.0 выполните командлеты hello шаблону именования {глагол}-AzureRm {существительное}; в то время как hello 0.9.8 имена не включают **Rm** (например, New-AzureRmResourceGroup вместо New AzureResourceGroup). При использовании Azure PowerShell 0.9.8, необходимо сначала включить режим диспетчера ресурсов hello, запустив hello **AzureResourceManager Switch-AzureMode** команды. Эта команда не требуется в версии 1.0 и более поздних версиях.

Если требуется toouse в сценарии, написанные для среды hello 0.9.8, hello 1.0 или более поздней версии среды следует тщательно обновления и тестировать сценарии hello в тестовой среде перед их использованием в рабочей среде tooavoid непредвиденного влияния.

[Загрузка последней версии PowerShell hello](https://github.com/Azure/azure-powershell/releases) (Минимальная требуемая версия —: 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a>Создание хранилища служб восстановления
Привет, следующие шаги, чтобы привести по созданию хранилище служб восстановления. Хранилище служб восстановления отличается от хранилища службы архивации.

1. При использовании резервного копирования Azure для hello первый раз, необходимо использовать hello **AzureRMResourceProvider регистра** поставщика службы восстановления Azure hello tooregister командлетов с вашей подпиской.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. Hello хранилище служб восстановления это ARM ресурс, поэтому требуется tooplace его в группе ресурсов. Вы можете выбрать существующую группу ресурсов или создать новую. При создании новой группы ресурсов, укажите hello имя и расположение для группы ресурсов hello.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. Используйте hello **New AzureRmRecoveryServicesVault** командлет toocreate hello новое хранилище. Убедитесь, что toospecify hello одинаковое расположение для hello хранилище, которое использовалось для группы ресурсов hello.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. Укажите тип hello toouse избыточности хранилища; можно использовать [локально избыточное хранилище (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) или [географически избыточное хранилище (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Hello следующий пример демонстрирует hello - BackupStorageRedundancy для testVault был установлен tooGeoRedundant.

   > [!TIP]
   > Многие командлеты службы архивации Azure в качестве входных данных необходим объект хранилища служб восстановления hello. По этой причине — это объект хранилища служб восстановления резервной копии удобный toostore hello в переменной.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a>Представление hello хранилища в подписке
Используйте **Get AzureRmRecoveryServicesVault** tooview hello список всех хранилищ в текущей подписке hello. Можно использовать этот toocheck команды создания нового хранилища или toosee какие хранилищами доступны в подписке hello.

Выполните команду hello **Get AzureRmRecoveryServicesVault**, и перечислены все хранилища в подписке hello.

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


## <a name="installing-hello-azure-backup-agent"></a>Установка агента Azure Backup hello
Перед установкой агента Azure Backup hello загружены и на приветствия Windows Server необходимо toohave hello установщика. Можно получить последнюю версию установщика hello hello hello [центра загрузки Майкрософт](http://aka.ms/azurebackup_agent) или хранилище служб восстановления hello страницы панели мониторинга. Сохранить hello установщика tooan легкодоступном месте как * C:\Downloads\*.

Кроме того используйте загрузчик программы hello tooget PowerShell:
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

tooinstall агент hello, запустите следующую команду в консоли PowerShell с повышенными hello:

```
PS C:\> MARSAgentInstaller.exe /q
```

При этом устанавливаются hello агента со всеми параметрами по умолчанию hello. Установка Hello занимает несколько минут в фоновом режиме hello. Если вы не укажете hello */nu* параметр, а затем hello **центра обновления Windows** окно в конце hello hello toocheck установки обновлений. После установки агент hello будет отображаться в списке установленных программ hello.

toosee hello список установленных программ, перейдите в слишком**панели управления** > **программы** > **программы и компоненты**.

![Агент установлен](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Параметры установки
toosee, Здравствуйте, все параметры, доступные через hello командной строки, выполните следующую команду hello.

```
PS C:\> MARSAgentInstaller.exe /?
```

Hello доступны следующие параметры.

| Параметр | Сведения | значение по умолчанию |
| --- | --- | --- |
| /q |Позволяет выполнить тихую установку. |- |
| /p:"расположение" |Путь toohello папку для установки агента Azure Backup hello. |C:\Program Files\Microsoft Azure Recovery Services Agent |
| /s:"расположение" |Путь toohello для папки кэша hello Azure Backup agent. |C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch |
| /m |Участие в tooMicrosoft обновления |- |
| /nu |Позволяет отказаться от проверки наличия обновлений после завершения установки. |- |
| /d |Удаляет агент служб восстановления Microsoft Azure. |- |
| /ph |Адрес узла прокси-сервера. |- |
| /po |Номер порта узла прокси-сервера. |- |
| /pu |Имя пользователя узла прокси-сервера. |- |
| /pw |Пароль прокси-сервера. |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a>Регистрация Windows Server или Windows клиентского компьютера tooa хранилище служб восстановления
После создания хранилище служб восстановления hello, загрузите последнюю версию агента hello и учетные данные хранилища hello и сохранить его в удобном месте, например C:\Downloads.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

На приветствия Windows Server или клиентский компьютер Windows, запустите hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) командлет tooregister hello машины с хранилищем hello.
Этот и другие командлеты, используемые для резервного копирования, являются модуль MSONLINE hello какие hello установщика агента Mars добавляется как часть процесса установки hello. 

Установка агента Hello не обновляет hello $Env: PSModulePath переменной. Это означает, что автоматическая загрузка модуля завершается ошибкой. tooresolve это можно сделать hello следующее:

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

Кроме того можно вручную загрузить модуль hello в скрипте следующим образом:

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

После загрузки командлеты оперативной архивации hello регистрации hello учетные данные хранилища:


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> Не используйте файл учетных данных хранилища hello toospecify относительные пути. Необходимо указать абсолютный путь в качестве входного toohello командлета.
>
>

## <a name="networking-settings"></a>Параметры сети
Если подключение hello hello Windows компьютера toohello является Интернет через прокси-сервер, параметры прокси-сервера hello также можно указать toohello агента. В нашем случае прокси-сервер не используется, поэтому мы явным образом удаляем все данные прокси-сервера.

Использование пропускной способности также можно управлять с помощью параметров hello ```work hour bandwidth``` и ```non-work hour bandwidth``` для заданного набора дней недели hello.

Задания параметров прокси-сервера и пропускной способности hello осуществляется с помощью hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) командлета:

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>Параметры шифрования
tooAzure Hello резервного копирования данных, отправляемых резервной копии является зашифрованным tooprotect hello конфиденциальность данных hello. Парольная фраза для шифрования Hello — hello «password» toodecrypt hello данные во время восстановления hello.

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> Обновление сведений парольную фразу hello надежным и безопасным, после ее установки. Не быть может toorestore данные из Azure без этой парольной фразы.
>
>

## <a name="back-up-files-and-folders"></a>Резервное копирование файлов и папок
Для политики определены все резервные копии из серверов и клиентов Windows tooAzure резервного копирования. Hello политики состоит из трех частей:

1. Объект **расписание резервного копирования** , указывающий, когда архивы toobe выполнены и синхронизируются с hello службой.
2. Объект **расписание хранения** , указывающее, как долго точки восстановления tooretain hello в Azure.
3. **Указания включения/исключения файлов** — определяет, для каких элементов следует создавать резервные копии.

Поскольку мы будем использовать автоматическое резервное копирование данных, в этой статье предполагается, что заданных настроек нет. Мы сначала необходимо создать новую политику резервного копирования, с помощью hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) командлета.

```
PS C:\> $newpolicy = New-OBPolicy
```

В это время hello политики является пустым и другие командлеты, необходимые toodefine какие элементы будут включены или исключены, при резервные копии выполняются и Здравствуйте, где будут храниться резервные копии.

### <a name="configuring-hello-backup-schedule"></a>Настройка расписания резервного копирования hello
Здравствуйте, сначала hello состоит из трех частей политики — расписание архивации hello, которое создается с помощью hello [New OBSchedule](https://technet.microsoft.com/library/hh770401) командлета. расписание резервного копирования Hello определяет, когда архивы toobe копии. При создании расписания необходимые toospecify 2 входных параметров.

* **Дни недели hello** следует запускать эту резервную копию hello. Можно запустить задание резервного копирования hello только один день, или каждый день недели hello или любую комбинацию между ними.
* **Время суток hello** когда должно выполняться резервное копирование hello. Определяется too3 разное время суток hello, когда будут создаваться hello резервного копирования.

Например, политику резервного копирования можно настроить таким образом, чтобы соответствующее задание выполнялось в 16:00 каждые субботу и воскресенье.

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

расписание резервного копирования Hello требуется toobe, связанных с политикой, но это можно сделать с помощью hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) командлета.

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>Настройка политики хранения
Политика хранения Hello определяет продолжительность восстановления сохраняются точки, созданные из задания резервного копирования. При создании новой политики хранения с помощью hello [New OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) командлета, можно указать hello, сколько дней hello точки восстановления резервной копии должны toobe сохранило резервного копирования Azure. пример Hello задана политика сохранения 7 дней.

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

Hello политика хранения должна быть связана hello основной политики с помощью командлета hello [OBRetentionPolicy набор](https://technet.microsoft.com/library/hh770405):

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a>Включение и исключение файлов toobe резервного копирования
```OBFileSpec``` Объект определяет hello файлы toobe включен и исключен из резервной копии. Это набор правил, что область out hello защищенных файлов и папок на компьютере. Можно создать любое количество правил включения или исключения файлов и связать их с политикой. При создании нового объекта OBFileSpec, можно сделать следующее:

* Укажите hello файлов и папок toobe включены
* Укажите hello файлов и папок toobe исключены
* Укажите рекурсивные резервного копирования данных в папке (или) ли следует копировать только hello верхнего уровня файлы в указанной папке hello вверх.

Hello последний достигается с помощью флага - нерекурсивных hello в команде New-OBFileSpec hello.

В следующем примере hello мы резервное копирование тома C: и D: и исключить hello двоичных файлов операционной системы в папке Windows hello и любые временные папки. toodo, поэтому мы создадим две спецификации файла с помощью hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) командлет - для включения и исключения. После создания спецификации файла hello они связаны hello политики с помощью hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) командлета.

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a>Применение политики hello
Теперь hello объекта политики завершена и имеет связанное расписание резервного копирования, политика хранения и список включения и исключения файлов. Эта политика теперь могут быть зафиксированы для toouse резервного копирования Azure. Перед установкой hello вновь созданные политики убедитесь, что нет существующие политики резервного копирования, связанных с сервером hello с помощью hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) командлета. Удаление политики hello выдаст запрос на подтверждение. Подтверждение hello tooskip использовать hello ```-Confirm:$false``` флаг с командлетом hello.

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

Слишком большой объем выделяемой объект политики hello выполняется с помощью hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) командлета. При этом также будет запрашиваться соответствующее подтверждение. Подтверждение hello tooskip использовать hello ```-Confirm:$false``` флаг с командлетом hello.

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

Вы можете просмотреть сведения hello hello существующие политики резервного копирования с помощью hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) командлета. Можно выполнять детализацию дальше с помощью hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) командлет расписание резервного копирования hello и hello [Get OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) командлета для политики хранения hello

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a>Выполнение нерегламентированного резервного копирования
После настройки политики резервного копирования резервных копий hello будет выполняться по расписанию hello. Резервное копирование ad-hoc запуска можно также с помощью hello [OBBackup начала](https://technet.microsoft.com/library/hh770426) командлета:

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a>Восстановление данных из службы архивации Azure
Этот раздел поможет выполнить шаги hello для автоматического восстановления данных из резервной копии Azure. Это включает в себя таким образом hello следующие шаги:

1. Выберите исходный том hello
2. Выберите резервного копирования toorestore точки
3. Выберите элемент toorestore
4. Инициирующий процесс восстановления hello

### <a name="picking-hello-source-volume"></a>Комплектации hello исходного тома
В порядке toorestore элемент из резервного копирования Azure необходимо сначала tooidentify hello источник элемента hello. Поскольку команды hello выполнении в контексте сервера или клиента Windows hello, hello машины уже определен. Hello следующим шагом в определение исходного hello — tooidentify hello том, содержащий его. Список томов или источников резервного копирования с этого компьютера можно получить, выполнив hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) командлета. Эта команда возвращает массив всех источников hello, полученные с сервера и клиента.

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-toorestore"></a>Выбрав какие toorestore точки резервного копирования
Получить список точек резервного копирования, выполнив hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) командлет с соответствующими параметрами. В нашем примере мы выберем hello последней резервной копии точки для исходного тома hello *D:* и использовать его toorecover определенного файла.

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
Hello объекта ```$rps``` является массивом точек резервного копирования. Hello первый элемент является последней точки hello и n-й элемент hello — самая старая точка hello. Последняя точка toochoose hello, мы будем использовать ```$rps[0]```.

### <a name="choosing-an-item-toorestore"></a>Выбор элемента toorestore
использовать tooidentify hello точное файл или папка toorestore, рекурсивно hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) командлета. Иерархии папок hello этот способ можно просматривать только с помощью hello ```Get-OBRecoverableItem```.

В этом примере, если мы хотим файл hello toorestore *finances.xls* мы ссылаться, используя hello объекта ```$filesFolders[1]```.

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

Можно также выполнить поиск toorestore элементов с помощью hello ```Get-OBRecoverableItem``` командлета. В нашем примере toosearch для *finances.xls* удалось получить дескриптор файла hello, запустив следующую команду:

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>Запуск процесса восстановления hello
процесс восстановления tootrigger hello, необходимо сначала параметры восстановления toospecify hello. Это можно сделать с помощью hello [New OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) командлета. Например, предположим, что файлы hello toorestore мы хотим слишком*C:\temp*. Также предположим, что мы хотим tooskip существующие файлы в папку назначения hello *C:\temp*. toocreate такой вариант восстановления, используйте hello следующую команду:

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

Теперь запускать hello процесса восстановления с помощью hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) на выбранных hello ```$item``` из вывода hello hello ```Get-OBRecoverableItem``` командлета:

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>Удаление агента Azure Backup hello
Удаление агента Azure Backup hello можно сделать с помощью hello следующую команду:

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

При удалении hello двоичные файлы агента с компьютера hello имеет некоторые последствия tooconsider:

* Удаляет фильтр файлов hello из машины hello и остановить отслеживание изменений.
* Все данные политики удаляется с компьютера hello, но сведения о политике hello продолжается toobe хранятся в службе hello.
* Удаляются все расписания резервного копирования, и последующие операции резервного копирования больше не выполняются.

Однако hello данные хранятся в Azure остается и сохраняются согласно установки политики хранения hello вами. Предыдущие точки восстановления автоматически рассматриваются как устаревшие.

## <a name="remote-management"></a>Удаленное управление
Все управление hello вокруг hello Azure Backup agent, политики и источников данных может быть выполнена удаленно с помощью PowerShell. Привет, удаленное управление компьютеру toobe правильно подготовлен.

По умолчанию служба удаленного управления Windows hello настроена на запуск вручную. Тип запуска Hello должен быть установлен слишком*автоматического* и hello служба должна быть запущена. tooverify, hello служба WinRM запущена, значение свойства Status hello hello должно быть *под управлением*.

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

Для удаленного взаимодействия необходимо настроить PowerShell.

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

машины Hello теперь можно управлять удаленно — начиная с установки hello hello агента. Например следующий скрипт hello копирует hello агента toohello удаленный компьютер и устанавливает его.

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительная информация о службе архивации Azure для сервера или клиента Windows

* [Введение tooAzure резервной копии](backup-introduction-to-azure-backup.md)
* [Резервное копирование серверов Windows](backup-configure-vault.md)
