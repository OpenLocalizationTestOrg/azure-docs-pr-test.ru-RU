---
title: "Служба архивации Azure: С помощью PowerShell tooback копирование рабочих нагрузок DPM | Документы Microsoft"
description: "Узнайте, как toodeploy и управление резервным копированием Azure для Data Protection Manager (DPM) с помощью PowerShell"
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>Развертывание и управление ими tooAzure резервного копирования для серверов Data Protection Manager (DPM), с помощью PowerShell
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Классический](backup-dpm-automation-classic.md)
>
>

В этой статье объясняется, как toouse PowerShell tooback копирование и восстановление данных DPM из резервного хранилища. Мы рекомендуем использовать хранилища служб восстановления для всех новых развертываний. Новый пользователь Azure Backup, с помощью статьи hello [развертывание и управление ими tooAzure данных Data Protection Manager с помощью PowerShell](backup-dpm-automation.md), поэтому при хранении данных в хранилище служб восстановления.

> [!IMPORTANT]
> Теперь можно обновить вашими хранилищами служб tooRecovery хранилища резервной копии. Дополнительные сведения см. в статье hello [обновление tooa хранилища резервной копии, в хранилище служб восстановления](backup-azure-upgrade-backup-to-recovery-services.md). Корпорация Майкрософт рекомендует tooupgrade вашей резервных хранилищ tooRecovery хранилищами служб. После 15 октября 2017 г. нельзя использовать PowerShell toocreate резервное копирование хранилищ. **К 1 ноября 2017 года**:
>- Все оставшиеся хранилища резервной копии будет автоматически обновленные tooRecovery хранилищами служб.
>- Вы не будет возможности tooaccess данные резервной копии hello классического портала. Вместо этого используйте hello Azure портала tooaccess резервного копирования данных в хранилищах службы восстановления.
>

## <a name="setting-up-hello-powershell-environment"></a>Настройка среды PowerShell hello
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Прежде чем использовать PowerShell toomanage из резервных копий с tooAzure Data Protection Manager, необходимо будет справа среде toohave hello в PowerShell. В начале сеанса PowerShell hello hello убедитесь, что запустить hello, следующая команда tooimport hello правой модули и позволяют командлеты DPM hello toocorrectly ссылку:

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>Настройка и регистрация
toobegin:

1. [Скачайте последнюю версию PowerShell](https://github.com/Azure/azure-powershell/releases) (минимальная требуемая версия — 1.0.0)
2. Включения командлетов резервного копирования Azure hello переключив слишком*AzureResourceManager* режиме с помощью hello **Switch-AzureMode** командлетов для:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Hello следующие программы установки и регистрации задачи можно автоматизировать с помощью PowerShell:

* создать хранилище архивации;
* Установка агента Azure Backup hello
* Регистрация hello службы архивации Azure
* Параметры сети
* Параметры шифрования

### <a name="create-a-backup-vault"></a>создать хранилище архивации;
> [!WARNING]
> Для клиентов, использующих Azure Backup для hello первый раз необходимо использовать с вашей подпиской поставщика toobe tooregister hello Azure Backup. Это можно сделать, выполнив следующую команду hello: Register AzureProvider - ProviderNamespace «Microsoft.Backup»
>
>

Можно создать новое хранилище резервных копий с помощью hello **New AzureRMBackupVault** командлетов для. резервное хранилище Hello является ресурс ARM, поэтому вам необходимо tooplace его в группе ресурсов. В консоли Azure PowerShell с повышенными привилегиями выполните hello, следующие команды:

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

Можно получить список всех резервных хранилищ hello в данной подписке с помощью hello **Get AzureRMBackupVault** командлетов для.

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>Установка агента Azure Backup hello на сервере DPM
Перед установкой агента Azure Backup hello загружены и на приветствия Windows Server необходимо toohave hello установщика. Можно получить последнюю версию установщика hello hello hello [центра загрузки Майкрософт](http://aka.ms/azurebackup_agent) или со страницы панели мониторинга резервного хранилища hello. Сохранить hello установщика tooan легкодоступном месте как * C:\Downloads\*.

агент hello tooinstall, запустите следующую команду в консоли PowerShell с повышенными hello **на сервере DPM hello**:

```
PS C:\> MARSAgentInstaller.exe /q
```

При этом устанавливаются hello агента со всеми параметрами по умолчанию hello. Установка Hello занимает несколько минут в фоновом режиме hello. Если вы не укажете hello */nu* hello параметр **центра обновления Windows** окно в конце hello hello toocheck установки обновлений.

Hello агент будет отображаться в списке установленных программ hello. toosee hello список установленных программ, перейдите в слишком**панели управления** > **программы** > **программы и компоненты**.

![Агент установлен](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a>Параметры установки
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

### <a name="registering-with-hello-azure-backup-service"></a>Регистрация hello службы архивации Azure
Прежде чем выполнять регистрацию с hello службы архивации Azure, необходимо tooensure, hello [необходимые компоненты](backup-azure-dpm-introduction.md) соблюдены. Необходимо следующее:

* Действующая подписка Azure
* Хранилище архивов

toodownload hello учетные данные хранилища, запустите hello **Get AzureBackupVaultCredentials** командлет в консоли Azure PowerShell и хранилище его в удобном расположении, например * C:\Downloads\*.

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

Регистрации hello машины с хранилищем hello осуществляется с помощью hello [DPMCloudRegistration начала](https://technet.microsoft.com/library/jj612787) командлета:

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

Регистрирует сервер DPM, с именем «TestingServer» hello хранилище Microsoft Azure с помощью hello указанное хранилище учетных данных.

> [!IMPORTANT]
> Не используйте файл учетных данных хранилища hello toospecify относительные пути. Необходимо указать абсолютный путь в качестве входного toohello командлета.
>
>

### <a name="initial-configuration-settings"></a>Исходные параметры конфигурации
После hello сервер DPM зарегистрирован hello резервное хранилище, он будет запускаться с параметрами по умолчанию подписки. Эти параметры подписки включают сетью, шифрования и hello промежуточной области. toobegin изменение hello подписки параметров необходимо toofirst справиться с hello существующие (по умолчанию), параметры с помощью hello [Get DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) командлета:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Локальный объект PowerShell toothis сделанных изменений, которые ```$setting``` и hello полный объект будет зафиксирована tooDPM и резервного копирования Azure toosave их с помощью hello [DPMCloudSubscriptionSetting набор](https://technet.microsoft.com/library/jj612791) командлета. Требуется toouse hello ```–Commit``` tooensure флаг, который hello изменения сохраняются. Параметры Hello не будет применяться и используемые резервного копирования Azure, пока не зафиксирована.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a>Сеть
Если подключение hello toohello машины hello DPM служба архивации Azure на hello Интернет через прокси-сервер, параметры прокси-сервера hello должны быть предоставлены для toosucceed резервных копий. Это делается с помощью hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` и hello ```ProxyPassword``` параметры с hello [DPMCloudSubscriptionSetting набор](https://technet.microsoft.com/library/jj612791) командлета. В нашем случае прокси-сервер не используется, поэтому мы явным образом удаляем все данные прокси-сервера.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

Пропускная способность также можно управлять с помощью параметров ```-WorkHourBandwidth``` и ```-NonWorkHourBandwidth``` для заданного набора дней недели hello. В данном случае мы не будем настраивать регулирование.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a>Настройка hello промежуточной области
Агент архивации Azure Hello, выполняется на сервере DPM hello должен временное хранилище для данных, восстанавливаемых из облака hello (локальную область промежуточного хранения). Настройка hello промежуточной области хранения с помощью hello [набор DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) командлета и hello ```-StagingAreaPath``` параметра.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

В приведенном выше примере hello, hello промежуточной области устанавливается слишком*C:\StagingArea* hello объекта PowerShell ```$setting```. Убедитесь, что hello указанная папка уже существует, иначе hello окончательная фиксация параметров подписки hello завершится ошибкой.

### <a name="encryption-settings"></a>Параметры шифрования
tooAzure Hello резервного копирования данных, отправляемых резервной копии является зашифрованным tooprotect hello конфиденциальность данных hello. Парольная фраза для шифрования Hello — hello «password» toodecrypt hello данные во время восстановления hello. Он tookeep важные безопасный этой информации и защиты после ее установки.

В следующем примере hello, hello первая команда преобразует строку hello ```passphrase123456789``` tooa безопасной строки и присваивает hello защищенной строки toohello переменную с именем ```$Passphrase```. Вторая команда Hello задает защищенную строку hello в ```$Passphrase``` как hello пароль для шифрования резервных копий.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Обновление сведений парольную фразу hello надежным и безопасным, после ее установки. Данные могут toorestore из Azure без этой парольной фразы не будет.
>
>

На этом этапе должны были внесены все необходимые hello изменения toohello ```$setting``` объекта. Не забывайте toocommit hello изменения.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>Защита данных tooAzure резервной копии
В этом разделе будет добавьте tooDPM производственного сервера и затем включите защиту hello toolocal DPM хранилища данных и затем tooAzure резервного копирования. В примерах hello мы покажем, как tooback копирования файлов и папок. Hello логику можно легко быть расширенные toobackup любой источник данных, поддерживаемых DPM. Все резервные копии DPM находятся под управлением группы защиты (ГЗ), которая состоит из четырех частей.

1. **Членов группы** приведен список все защищаемые объекты hello (также называется *Datasources* в DPM), которые должны tooprotect в hello одной группе защиты. Например можно tooprotect производственный виртуальных машин в одну группу защиты и баз данных SQL Server в другую группу защиты как они могут иметь различные требования для резервного копирования. Перед любой источник данных можно архивировать на рабочем сервере необходимо убедиться, что hello toomake агент DPM устанавливается на сервере hello и под управлением DPM. Выполните действия hello для [Установка hello агент DPM](https://technet.microsoft.com/library/bb870935.aspx) , связав ее toohello соответствующие сервера DPM.
2. **Метод защиты данных** указывает hello резервного расположения целей - ленту, диск и облака. В нашем примере мы будет защищать данные toohello локального диска и toohello облака.
3. Объект **расписание резервного копирования** , указывающий при архивы toobe выполнить и как часто hello данные должны быть синхронизированы между hello сервера DPM и hello рабочего сервера.
4. Объект **расписание хранения** , указывающее, как долго точки восстановления tooretain hello в Azure.

### <a name="creating-a-protection-group"></a>Создание группы защиты
Начните с создания новой группы защиты с помощью hello [New DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) командлета.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

Hello выше командлет будет создана группа защиты с именем *ProtectGroup01*. Можно изменять существующую группу защиты более поздней версии tooadd резервного копирования toohello облако Azure. Тем не менее toomake любые изменения toohello группа защиты — новые или существующие - мы должны tooget дескриптор на *изменяемой* объекта с помощью hello [Get DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) командлета.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>Добавление членов группы toohello группы защиты
Каждый агент DPM знает hello список источников данных на сервере hello, установленной на. tooadd toohello источник данных группы защиты, hello toofirst потребностей агент DPM Отправить список сервер DPM задней toohello hello источников данных. Одного или нескольких источников данных, а затем и добавлены toohello группы защиты. шаги, которые необходимы tooget Hello PowerShell достичь указаны:

1. Получить список всех серверов, управляемых с помощью DPM с помощью hello агент DPM.
2. Выберите определенный сервер.
3. Получить список всех источников данных на сервере hello.
4. Выберите один или несколько источников данных и добавить их toohello группы защиты

список серверов, на какие hello агента DPM установлена, а управляется hello сервер DPM Hello приобретается вместе с hello [Get DPMProductionServer](https://technet.microsoft.com/library/hh881600) командлета. В этом примере мы отфильтруем и настроим для резервного копирования только сервер с именем *productionserver01* .

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Теперь извлечь hello список источников данных на ```$server``` с помощью hello [Get DPMDatasource](https://technet.microsoft.com/library/hh881605) командлета. В этом примере мы фильтрации для тома hello * D:\* которой мы хотим tooconfigure для резервного копирования. Этот источник данных добавляется toohello группы защиты с помощью hello [DPMChildDatasource добавить](https://technet.microsoft.com/library/hh881732) командлета. Запомнить toouse hello *modifable* объект группы защиты ```$MPG``` toomake hello дополнения.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Повторите этот шаг столько раз, по мере необходимости, пока не будут добавлены все hello выбранной группы защиты toohello источники данных. Также можно только один источник данных и hello полный рабочий процесс для создания группы защиты hello и позднее добавить несколько источников данных toohello группы защиты.

### <a name="selecting-hello-data-protection-method"></a>Выбор метода защиты данных hello
После hello источники данных будут добавлены toohello группы защиты, hello следующим шагом является hello с помощью метода защиты hello toospecify [DPMProtectionType набор](https://technet.microsoft.com/library/hh881725) командлета. В этом примере hello группы защиты будет настроен для локального диска и резервное копирование в облако. Необходимо также toospecify hello datasource, необходимо с помощью hello toocloud tooprotect [DPMChildDatasource добавить](https://technet.microsoft.com/library/hh881732.aspx) командлет с флагом - сети.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Установка диапазона хранения hello
Задать политику хранения hello точки hello резервного копирования с помощью hello [DPMPolicyObjective набор](https://technet.microsoft.com/library/hh881762) командлета. Хотя может показаться нечетное tooset hello хранения перед расписание резервного копирования hello определен, с помощью hello ```Set-DPMPolicyObjective``` автоматически задает расписание резервного копирования по умолчанию, который затем может быть изменен. Он всегда расписание резервного копирования hello возможных tooset сначала и hello политики хранения после.

В следующем примере hello hello командлет задает параметры хранения hello для резервного копирования на диск. Это будет хранить архивы 10 дней и синхронизировать данные каждые 6 часов между hello рабочий сервер и сервер DPM hello. Hello ```SynchronizationFrequencyMinutes``` не определяет, как часто точки резервного копирования создается, но, как часто данные копируются toohello сервера DPM; это предотвращает чрезмерного увеличения размера резервного копирования.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

Для резервного копирования будет tooAzure (DPM называется toothese оперативного резервного копирования) hello диапазонов хранения можно настроить для [Долгосрочное хранение с использованием Деда отец ов схемы (GFS)](backup-azure-backup-cloud-as-tape.md). То есть можно определить политику объединенного хранения, включающую политики ежедневного, еженедельного, ежемесячного и ежегодного хранения. В этом примере мы массив, представляющий схему сложных хранения hello, нам нужно создать, а затем настройте hello диапазон хранения, с помощью hello [DPMPolicyObjective набор](https://technet.microsoft.com/library/hh881762) командлета.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>Расписание резервного копирования набор hello
DPM задает расписание резервного копирования по умолчанию автоматически при указании цели защиты hello, с помощью hello ```Set-DPMPolicyObjective``` командлета. расписания по умолчанию hello toochange, использовать hello [Get DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) командлет следуют hello [DPMPolicySchedule набор](https://technet.microsoft.com/library/hh881723) командлета.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

В приведенном выше примере hello ```$onlineSch``` является массивом с четырьмя элементами, содержащий hello существующее расписание оперативной защиты для hello группы защиты в схеме GFS hello:

1. ```$onlineSch[0]```будет содержать hello ежедневное расписание
2. ```$onlineSch[1]```будет содержать hello еженедельного расписания
3. ```$onlineSch[2]```будет содержать hello ежемесячного расписания
4. ```$onlineSch[3]```будет содержать hello годовой расписания

Поэтому если вам требуется toomodify hello Еженедельное расписание, toorefer toohello ```$onlineSch[1]```.

### <a name="initial-backup"></a>Начальное резервное копирование
При резервном копировании datasource для hello впервые, DPM требуется toocreate начальной реплики, которая создаст копию защищенных toobe datasource hello на томе реплики DPM. Это действие может быть запланированной на определенное время или можно запустить вручную, используя hello [набор DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) командлет с параметром hello ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>Изменение размера hello реплики DPM и тома точек восстановления
Можно также изменить размер тома реплики DPM, а также использование теневого копирования тома hello [DPMDatasourceDiskAllocation набор](https://technet.microsoft.com/library/hh881618.aspx) командлет как hello в следующем примере: Get-DatasourceDiskAllocation - Datasource $DS SET-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-вручную - ReplicaArea (2 ГБ) — ShadowCopyArea (2 ГБ)

### <a name="committing-hello-changes-toohello-protection-group"></a>Фиксация hello изменяет toohello группы защиты
Наконец hello изменения должны toobe, зафиксированные до DPM можно использовать резервную копию hello каждой новой конфигурации группы защиты hello. Это делается с помощью hello [DPMProtectionGroup набор](https://technet.microsoft.com/library/hh881758) командлета.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>Просматривать hello резервного копирования точки
Можно использовать hello [Get DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget командлет список всех точек восстановления для источника данных. В этом примере мы:

* извлечь все PGs hello на сервере DPM hello, который будет сохранен в виде массива```$PG```
* получить соответствующий toohello hello источников данных```$PG[0]```
* Получите все hello точки восстановления для источника данных.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Восстановление данных, защищенных в Azure
Восстановление данных представляет собой сочетание объектов ```RecoverableItem``` и ```RecoveryOption```. В предыдущем разделе hello нас есть список точек hello резервного копирования для источника данных.

В следующем примере hello демонстрируют, как toorestore Hyper-V виртуальной машины из резервного копирования Azure точками объединение резервного копирования с hello целевого объекта для восстановления. А именно:

* Создание параметра восстановления, используя hello [New DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) командлета.
* Извлечение hello массивом точек резервного копирования, с помощью hello ```Get-DPMRecoveryPoint``` командлета.
* Выбор резервного копирования toorestore точки из.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

Hello команды можно легко расширить для любого типа источника данных.

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о службе архивации Azure для DPM в разделе [tooDPM введение резервного копирования](backup-azure-dpm-introduction.md)
