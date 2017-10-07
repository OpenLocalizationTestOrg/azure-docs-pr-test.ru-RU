---
title: "hello aaaDeploy службы мобильности восстановления сайта с помощью DSC службы автоматизации Azure | Документы Microsoft"
description: "Описывает, как развертывать tooautomatically Azure Automation DSC toouse службу hello Mobility восстановления сайта Azure и Azure агент для виртуальной Машины VMware и tooAzure репликации физического сервера"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>Развертывание службы мобильности hello с DSC службы автоматизации Azure для репликации виртуальной машины
В Operations Management Suite предоставляется комплексное решение для архивации и аварийного восстановления, которое можно использовать в плане обеспечения непрерывности бизнес-процессов.

Мы начали этот путь с Hyper-V, используя реплику Hyper-V. Но у нас есть развернутой toosupport разнородных установки, так как клиенты имеют несколько низкоуровневых оболочках и платформ в своих облаках.

При выполнении рабочих нагрузок VMware и физических серверов сегодня, сервер управления запускает все hello компонентов Azure Site Recovery в вашей среде toohandle hello связью и передачи данных репликации в Azure, когда Azure — место.

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>Развертывание службы hello Mobility восстановления сайта с помощью DSC службы автоматизации
Начнем с краткого разбора функций этого сервера управления.

сервер управления Hello выполняется несколько ролей сервера. Одна из них, *роль конфигурации*, координирует обмен данными и управляет процессами репликации и восстановления данных.

Кроме того, hello *процесс* роли действует как шлюз репликации. Эта роль передаются данные репликации из защищенного источника машин, выполняет оптимизацию для кэширования, сжатия и шифрования и отправляет его tooan учетной записи хранилища Azure. Одна из функций hello для hello процесс роли также установки toopush машин tooprotected службы мобильности hello и выполнить автоматическое обнаружение виртуальных машин VMware.

Если восстановление размещения из Azure, hello *главного целевого сервера* роль будет обрабатывать данные репликации hello в рамках этой операции.

Для машин, защищенных hello, мы полагаемся на hello *службы Mobility service*. Этот компонент является компьютер развернутой tooevery (виртуальной Машины VMware или физических серверов), будет tooreplicate tooAzure. Она фиксирует записи данных на компьютере hello и пересылает их toohello сервера управления (роль процесса).

При работе с непрерывность бизнес-процессов, это важно toounderstand рабочих нагрузок, инфраструктуры и компоненты hello. Можно затем требования hello для целевого времени восстановления (RTO) и целевую точку восстановления (RPO). В данном контексте hello службы Mobility service — tooensuring ключа, как и следовало ожидать защищенных рабочих нагрузок.

Как оптимальным образом можно обеспечить надежную защищенную конфигурацию, используя компоненты Operations Management Suite?

В этой статье приведен пример того, как можно использовать Azure Automation требуемого состояния (DSC), вместе с Site Recovery, tooensure:

* Служба мобильности Hello и агент ВМ Azure являются развернутой toohello компьютеров с Windows, которые должны tooprotect.
* Служба мобильности Hello и агент ВМ Azure всегда запускаются при Azure — целевым объектом репликации hello.

## <a name="prerequisites"></a>Предварительные требования
* В случае установки необходимых hello toostore репозитория
* Репозиторий toostore hello требуется парольная фраза tooregister с сервером управления hello

  > [!NOTE]
  > Для каждого сервера управления создается уникальная парольная фраза. Если вы собираетесь toodeploy несколько серверов управления, у вас есть tooensure, исправьте парольную фразу, хранится в файле passphrase.txt hello hello.
  >
  >
* Windows Management Framework (WMF) 5.0 установлено на компьютерах hello, что требуется tooenable для защиты (требование DSC службы автоматизации)

  > [!NOTE]
  > Если требуется, чтобы машины toouse DSC для Windows, имеющих установки WMF 4.0, см. раздел hello [использование DSC в отключенных средах](## Use DSC in disconnected environments).
  

Служба мобильности Hello может устанавливаться через командную строку hello и нескольких аргументов. Вот почему потребуется двоичные файлы hello toohave (после извлечения их из настройки программы установки) и сохранять их в том месте, где их можно получить с помощью конфигурации DSC.

## <a name="step-1-extract-binaries"></a>Шаг 1. Извлечение двоичных файлов
1. tooextract hello файлы, необходимые для программы установки, откройте toohello следующий каталог на сервере управления.

    **\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    В этой папке должен быть MSI-файл с таким именем.

    **Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**

    Используйте следующие команды tooextract hello установщика hello:

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. Выберите все файлы и отправлять их tooa сжатые ZIP-папки.

Теперь у вас есть hello двоичные файлы, необходимые настройки hello tooautomate hello службы Mobility service с помощью DSC службы автоматизации.

### <a name="passphrase"></a>Парольная фраза
Далее необходимо toodetermine место tooplace этот ZIP-папки. Можно использовать учетную запись хранилища Azure, как показано далее, toostore hello парольную фразу, необходимое для установки hello. затем регистрирует Hello агента с сервером управления hello в рамках процесса hello.

Парольная фраза Hello, полученный при развертывании сервера управления hello могут быть сохранены как passphrase.txt tooa текстовый файл.

Поместите ZIP-папки hello и парольная фраза hello выделенного контейнера в учетной записи хранилища Azure hello.

![Расположение папки](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

Если вы предпочитаете tookeep эти файлы в общей папке в сети, это можно сделать. Необходимо просто tooensure, hello DSC ресурс, который будет использоваться позже имеет доступ и может получить установки hello и парольную фразу.

## <a name="step-2-create-hello-dsc-configuration"></a>Шаг 2: Создание конфигурации hello DSC
Программа установки Hello зависит от WMF 5.0. Для компьютера toosuccessfully hello применить hello конфигурации с помощью DSC службы автоматизации, WMF 5.0 должен toobe присутствует.

Hello среде используется следующая конфигурация DSC пример hello:

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
Hello конфигурации будет выполнять hello следующее:

* переменные Hello сообщает о конфигурации hello где tooget hello двоичных файлов для службы мобильности hello и hello агент ВМ Azure, которой tooget hello парольной фразы, а toostore hello выходных данных.
* Hello конфигурации будут импортированы ресурсов xPSDesiredStateConfiguration DSC hello, чтобы можно было использовать `xRemoteFile` toodownload hello файлов из репозитория hello.
* Hello конфигурации создаст каталог место двоичные файлы toostore hello.
* ресурс archive Hello hello файлы будут извлечены из ZIP-папки hello.
* ресурс установки пакета Hello будет установлена служба Mobility hello из hello UNIFIEDAGENT. Exe-ФАЙЛ установщика hello определенных аргументов. (переменные hello, составляющие hello аргументы требуют toobe изменить tooreflect среды)
* Hello пакета ресурсов AzureAgent установить агент ВМ Azure hello, рекомендуется на каждой виртуальной Машине, запущенной в Azure. агент ВМ Azure Hello также упрощает toohello возможных tooadd расширения виртуальной Машины после отработки отказа.
* Hello ресурсы, служба будет убедитесь, что мобильных служб, связанных с hello и hello Azure они всегда работают.

Сохранить конфигурацию hello как **ASRMobilityService**.

> [!NOTE]
> Запомнить hello tooreplace CSIP в сервер управления фактическое hello tooreflect конфигурации для hello агент будет подключен и будет использовать правильную парольную фразу hello.
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>Шаг 3: Отправка tooAutomation DSC
Поскольку hello DSC настройки, сделанные будет импортировать требуемый модуль ресурсов DSC (xPSDesiredStateConfiguration), вам потребуется tooimport этот модуль в автоматизации перед отправкой конфигурации hello DSC.

Слишком Обзор входа в учетную запись автоматизации, tooyour**активы** > **модули**и нажмите кнопку **обзора коллекции**.

Здесь можно найти модуль hello и импортируйте его tooyour учетной записи.

![Импорт модуля](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

После завершения, go tooyour машины при наличии hello модули диспетчера ресурсов Azure и продолжить конфигурацию DSC только что созданный hello tooimport.

### <a name="import-cmdlets"></a>Импорт командлетов
В PowerShell войдите в tooyour подписки Azure. Изменения tooreflect командлеты hello среды и записывать данные учетной записи автоматизации в переменной.

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

Отправьте hello настройки tooAutomation DSC с помощью hello, выполнив командлет.

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>Компиляция конфигурации hello в DSC службы автоматизации
Далее необходимо toocompile hello конфигурации в DSC службы автоматизации, так, чтобы можно было начать tooit tooregister узлов. Для этого, выполнив следующий командлет hello:

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

Это может занять несколько минут, так как по сути вы развертываете hello конфигурации toohello размещенных DSC опрашивающей службы.

После компиляции hello конфигурации можно получить сведения о задании hello с помощью PowerShell (Get-AzureRmAutomationDscCompilationJob) или с помощью hello [портал Azure](https://portal.azure.com/).

![Получение задания](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

Теперь успешно опубликован и отправки вашего tooAutomation конфигурации DSC DSC.

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>Шаг 4: Встроенный машины tooAutomation DSC
> [!NOTE]
> Одним из hello необходимые условия для выполнения этого сценария является обновляются, компьютеры с Windows hello последнюю версию WMF. Можно загрузить и установить правильную версию hello для вашей платформы из hello [центра загрузки](https://www.microsoft.com/download/details.aspx?id=50395).
>
>

Теперь вы создадите metaconfig для DSC, что будет применять tooyour узлов. toosucceed с этим необходимо tooretrieve hello конечной точки URL-адрес и hello первичный ключ для выбранной учетной записи автоматизации в Azure. Можно найти эти значения в разделе **ключей** на hello **все параметры** колонке hello учетной записи автоматизации.

![Значения ключей](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

В этом примере имеется физический сервер Windows Server 2012 R2, требуется tooprotect с помощью Site Recovery.

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>Проверьте все ожидающие операции переименования файла в реестре hello
Прежде чем начать tooassociate hello server с конечной точкой hello DSC службы автоматизации, рекомендуется проверять наличие все ожидающие операции переименования файла в реестре hello. Они могут запретить hello установки завершить из-за tooa ожидается перезагрузка.

Выполните следующий командлет tooverify, это не ожидается перезагрузка сервера hello hello.

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
Это показывает пустым, имеется ли tooproceed ОК. Если нет, вы должны обработать перезагрузка сервера hello в течение периода обслуживания.

tooapply hello конфигурации на сервере hello запустите hello PowerShell интегрированная среда сценариев (ISE) и выполните следующий скрипт hello. Это по сути локальной конфигурации DSC, указать tooregister engine hello локального диспетчера конфигураций с hello службы DSC службы автоматизации и получить определенную конфигурацию hello (ASRMobilityService.localhost).

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

Эта конфигурация приведет к tooregister engine сам hello локального диспетчера конфигураций с DSC службы автоматизации. Также определяет работу hello ядра, что нужно делать при изменении конфигурации (ApplyAndAutoCorrect) и как его следует продолжить настройку hello, если требуется перезагрузка.

После запуска этого сценария hello узел должен начинаться tooregister с Automation DSC.

![Выполняется регистрация узла](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Если вернуться toohello портал Azure, вы увидите этот узел вновь зарегистрированного hello теперь отображается на портале hello.

![Зарегистрированный узел портала hello](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

На сервере hello можно выполнить следующий командлет tooverify, hello узел был зарегистрирован правильно PowerShell hello:

```powershell
Get-DscLocalConfigurationManager
```

После настройки hello извлеченные и примененные toohello сервера, это можно проверить, выполнив следующий командлет hello:

```powershell
Get-DscConfigurationStatus
```

Hello выходные данные показывают, что этот сервер hello успешно извлечено конфигурации:

![Выходные данные](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

Кроме того, программа установки службы Mobility hello имеет свой собственный журнал, в котором можно найти в *SystemDrive*\ProgramData\ASRSetupLogs.

Вот и все! Теперь успешно развернуты и зарегистрированы hello Mobility service на компьютере hello, требуется tooprotect с помощью Site Recovery. DSC будет убедитесь, что hello необходимые службы запущены всегда.

![Развертывание завершено успешно](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

После hello сервер управления обнаруживает hello успешному развертыванию, можно настроить защиту и включить репликацию на машине hello с помощью Site Recovery.

## <a name="use-dsc-in-disconnected-environments"></a>Использование DSC в отключенных средах
Если компьютеры не подключенных toohello Интернета, можно по-прежнему полагаться на DSC toodeploy и настроить службу Mobility hello на hello рабочих нагрузок, которые должны tooprotect.

Можно создать собственные опрашивающего сервера DSC в вашей среде tooessentially предоставляют hello такие же возможности, которые получаются из DSC службы автоматизации. То есть hello клиентов будет получать hello конфигурации (после его регистрации) конечной точки toohello DSC. Тем не менее другой вариант — toomanually принудительной hello DSC конфигурации tooyour машины, локально или удаленно.

Обратите внимание, что в этом примере добавленный параметр для имени компьютера hello. Hello удаленные файлы теперь находятся на удаленном ресурсе, который должен быть доступен, которые должны tooprotect машины hello. Hello конец скрипта hello вводит в действие hello конфигурации, а затем запускает tooapply hello DSC конфигурации toohello целевого компьютера.

### <a name="prerequisites"></a>Предварительные требования
Убедитесь, что установлен модуль PowerShell xPSDesiredStateConfiguration, hello. Для компьютеров Windows с установленным WMF 5.0 вы можете установить модуль xPSDesiredStateConfiguration hello, выполнив следующий командлет на целевых компьютерах hello hello:

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

Можно также загрузить и сохранить модуль hello на случай необходимости toodistribute его tooWindows машин, имеющих WMF 4.0. Выполните этот командлет на компьютере, на котором установлен компонент PowerShellGet (WMF 5.0).

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

Также для WMF 4.0, убедитесь, что hello [обновление Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) будет установлено на компьютерах hello.

Hello следующей конфигурации могут быть принудительно tooWindows машин, которые имеют WMF 5.0 и WMF 4.0:

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

Если tooinstantiate собственные опрашивающего сервера DSC на ваши возможности hello toomimic корпоративной сети, можно получить из DSC службы автоматизации, см. [Настройка опрашивающего веб-сервера DSC](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>Развертывание конфигурации DSC с помощью шаблона Azure Resource Manager (необязательно)
В этой статье основное внимание уделяется созданию собственного tooautomatically конфигурации DSC развертывать службы мобильности hello и hello агента ВМ Azure — и убедитесь, что они работают на компьютерах hello, которые должны tooprotect. У нас также есть шаблона Azure Resource Manager, которое будет выполнять развертывание этого DSC конфигурации tooa новую или существующую запись службы автоматизации Azure. Hello шаблон будет использовать ресурсы автоматизации toocreate входные параметры, содержащие переменные hello для вашей среды.

После развертывания шаблона hello, можно просто ссылаться toostep 4 в tooonboard этого руководства компьютеры.

Hello шаблонов будет выполнять hello следующее:

1. Использует имеющуюся или создаст учетную запись службы автоматизации.
2. Примет входные параметры для:
   * ASRRemoteFile--hello расположение, где были сохранены hello установки службы Mobility
   * ASRPassphrase--hello расположение, где сохранили файл passphrase.txt hello
   * ASRCSEndpoint--hello IP-адрес сервера управления
3. Импортируйте модуль PowerShell xPSDesiredStateConfiguration hello
4. Создание и компиляция конфигурации DSC hello

Все hello в предыдущих шагах, произойдет в правильном порядке hello, для возможности запуска адаптации компьютеры для защиты.

Hello шаблона с помощью инструкции по развертыванию, находится на [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).

Развертывание hello шаблона с помощью PowerShell:

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>Дальнейшие действия
После развертывания агентов службы мобильности hello, вы можете [включить репликацию](site-recovery-vmware-to-azure.md) для hello виртуальных машин.
