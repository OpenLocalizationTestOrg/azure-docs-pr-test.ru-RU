---
title: "tooAzure виртуальных машин Hyper-V aaaReplicate hello классическом портале с помощью PowerShell | Документы Microsoft"
description: "Автоматизация hello репликацию виртуальных машин Hyper-V в облаках VMM с помощью Site Recovery и PowerShell в классическом портале hello"
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: tysonn
ms.assetid: 9011f567-e0b4-4306-951a-b30da19f5db6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: d6847b46ac227209e6890de4ab603b23f827360f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-tooazure-with-powershell-in-hello-classic-portal"></a>Реплицировать tooAzure виртуальных машин Hyper-V с помощью PowerShell в классическом портале hello
> [!div class="op_single_selector"]
> * [Портал Azure](site-recovery-vmm-to-azure.md)
> * [PowerShell — Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Классический портал](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell — классическая модель](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a>Обзор
Azure Site Recovery поддерживает tooyour бизнес-непрерывности и аварийного восстановления (BCDR) стратегии, управляя операциями репликации, отработки отказа и восстановления виртуальных машин в различных вариантов развертывания. Полный список развертывания сценариев. в разделе hello [Обзор Azure Site Recovery](site-recovery-overview.md).

В этой статье показано, как toouse PowerShell tooautomate общие задачи должны tooperform при настройке виртуальных машин Hyper-V Azure Site Recovery tooreplicate в хранилище tooAzure облаков System Center VMM.

статья Hello содержит необходимые условия для сценария hello и показано, как установить tooset копирование в хранилище Site Recovery hello поставщика Azure Site Recovery на исходном сервере VMM hello, зарегистрируйте сервер hello в хранилище hello, добавьте учетную запись хранилища Azure, установите hello Azure Агент служб восстановления на серверах узлов Hyper-V, настройте параметры защиты для облаков VMM, будет применен tooall защищенные виртуальные машины, а затем включите защиту для этих виртуальных машин. После этого тестирования toomake отработки отказа hello, убедиться, что все работает должным образом.

Если возникли проблемы с установкой этого сценария опубликовать вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания.
>
>

## <a name="before-you-start"></a>Перед началом работы
Убедитесь, что выполнены следующие предварительные требования.

### <a name="azure-prerequisites"></a>Предварительные требования Azure
* Вам потребуется учетная запись [Microsoft Azure](https://azure.microsoft.com/) . Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/).
* Вам потребуется данные реплицируются toostore учетной записи хранилища Azure. Hello учетная запись должна включена георепликация. Он должен быть в hello же регионе, что хранилище Azure Site Recovery hello и связанные с hello одной подписке. См. [дополнительные сведения о службе хранилища Azure](../storage/common/storage-introduction.md).
* Необходимо убедиться, что, нужно tooprotect виртуальные машины соответствуют toomake [предварительные требования виртуальной машины Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

### <a name="vmm-prerequisites"></a>Предварительные требования VMM
* Вам потребуется сервер VMM под управлением System Center 2012 R2.
* Необходимо по крайней мере одно облако на сервер VMM требуется tooprotect hello. облако Hello должен содержать:
  * одну или несколько групп узлов VMM;
  * один или несколько серверов узлов или кластеров Hyper-V в каждой группе узлов;
  * Один или несколько виртуальных машин на сервере Hyper-V источника hello.

### <a name="hyper-v-prerequisites"></a>Предварительные требования Hyper-V
* Hello серверы узла Hyper-V должны работать под управлением **Windows Server 2012** с ролью Hyper-V или **Microsoft Hyper-V Server 2012** и иметь hello установлены последние обновления.
* Если Hyper-V выполняется в кластере, учтите, что брокер кластера не создается автоматически при использовании кластера на основе статических IP-адресов. Брокер кластера hello tooconfigure вам потребуется вручную. toodo это, в диспетчере сервера > Диспетчер отказоустойчивости кластеров, подключите toohello кластер, щелкните **настроить роль** и выберите **брокера реплики Hyper-V** в hello **выберите роль**экрана приветствия мастера высокой доступности.
* Любой сервер узла Hyper-V или кластера, для которого требуется защита toomanage должны включаться в облаке VMM.

### <a name="network-mapping-prerequisites"></a>Предварительные требования сетевого сопоставления
При защите виртуальных машин в Azure сетевое сопоставление сопоставление между сетями VM на исходном сервере VMM hello и целевой сетях Azure tooenable hello следующее:

* Все машины, которые отработки отказа на hello же может подключиться tooeach других, независимо от используемого плана восстановления, находящиеся в сеть.
* Если сетевой шлюз настроен hello целевой сети Azure, виртуальные машины могут подключаться tooother локальных виртуальных машин.
* Если не настроить сети сопоставление только виртуальные машины, которые выполняют отработку отказа в hello же плана восстановления будут другие возможности tooconnect tooeach после tooAzure перехода на другой ресурс.

Если требуется, чтобы toodeploy сетевого сопоставления необходимо иметь hello следующее:

* виртуальные машины Hello требуется tooprotect на исходном сервере VMM hello должно быть tooa подключенной сети виртуальной Машины. Сеть должна быть связанной tooa логической сети, связанной с облаком hello.
* Сеть Azure toowhich реплицировать виртуальные машины могут подключаться после отработки отказа. Будет предложено выбрать этой сети во время hello перехода на другой ресурс. сеть Hello должны находиться в hello же регионе, что подписки Azure Site Recovery.

### <a name="powershell-prerequisites"></a>Необходимые компоненты PowerShell
Убедитесь, что у вас есть toogo готовности Azure PowerShell. Если вы уже используете PowerShell, вам потребуется tooupgrade tooversion 0.8.10 или более поздней версии. Сведения о настройке PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs). После установки и настройки PowerShell вы можете просматривать все hello доступных командлетов для службы hello [здесь](/powershell/azure/overview).

toolearn советы, помогающие использовать командлеты hello, например как значения параметров, входы и выходы обычно обрабатываются в Azure PowerShell, в разделе [начало работы с командлетами Azure](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Шаг 1: Задайте подписку hello
В PowerShell выполните следующие командлеты.

```
$UserName = "<user@live.com>"
$Password = "<password>"
$AzureSubscriptionName = "prod_sub1"

$SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
$Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $securePassword
Add-AzureAccount -Credential $Cred;
$AzureSubscription = Select-AzureSubscription -SubscriptionName $AzureSubscriptionName

```

Замените hello элементы внутри hello «< >» свои данные.

## <a name="step-2-create-a-site-recovery-vault"></a>Шаг 2. Создание хранилища Site Recovery
В PowerShell замените элементы hello в «< >» hello свои данные и выполните следующие команды:

```

$VaultName = "<testvault123>"
$VaultGeo  = "<Southeast Asia>"
$OutputPathForSettingsFile = "<c:\>"

```


```
New-AzureSiteRecoveryVault -Location $VaultGeo -Name $VaultName;
$vault = Get-AzureSiteRecoveryVault -Name $VaultName;

```

## <a name="step-3-generate-a-vault-registration-key"></a>Шаг 3. Создание ключа регистрации хранилища
Создайте ключ регистрации в хранилище hello. После загрузки hello поставщика Azure Site Recovery и установите его на сервере VMM hello, используемой этим сервером VMM hello tooregister ключа в хранилище hello.

1. Получить файл параметр hello хранилища и задать контекст hello:

   ```

   $VaultName = "<testvault123>"
   $VaultGeo  = "<Southeast Asia>"
   $OutputPathForSettingsFile = "<c:\>"

   $VaultSetingsFile = Get-AzureSiteRecoveryVaultSettingsFile -Location $VaultGeo -Name $VaultName -Path $OutputPathForSettingsFile;

   ```
2. Задайте контекст хранилища hello, выполнив hello, следующие команды:

   ```

   $VaultSettingFilePath = $vaultSetingsFile.FilePath
   $VaultContext = Import-AzureSiteRecoveryVaultSettingsFile -Path $VaultSettingFilePath -ErrorAction Stop

   ```

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Шаг 4: Установка поставщика Azure Site Recovery hello
1. На виртуальной машине VMM hello создайте каталог, выполнив следующую команду hello:

   ```

   pushd C:\ASR\

   ```
2. Извлеките файлы hello, с помощью поставщика загружаются hello, выполнив следующую команду hello

   ```

   AzureSiteRecoveryProvider.exe /x:. /q

   ```
3. Установите поставщик hello, с помощью hello, следующие команды:

   ```

   .\SetupDr.exe /i

   ```

   ```

   $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
   do
   {
     $isNotInstalled = $true;
     if(Test-Path $installationRegPath)
     {
         $isNotInstalled = $false;
     }
   }While($isNotInstalled)

   ```

   Дождитесь установки toofinish hello.
4. Зарегистрируйте сервер hello в хранилище hello, с помощью hello следующую команду:

   ```

   $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
   pushd $BinPath
   $encryptionFilePath = "C:\temp\"
   .\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

   ```

## <a name="step-5-create-an-azure-storage-account"></a>Шаг 5. Создание учетной записи хранения Azure
Если у вас нет учетной записи Azure, создайте учетную запись с включенной репликацией geo, выполнив hello следующую команду:

```

$StorageAccountName = "teststorageacc1"
$StorageAccountGeo  = "Southeast Asia"

New-AzureStorageAccount -StorageAccountName $StorageAccountName -Label $StorageAccountName -Location $StorageAccountGeo;

```

Обратите внимание, что учетная запись хранения hello должна быть в hello же регионе, что служба восстановления сайтов Azure hello и связанные с hello одной подписке.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Шаг 6: Установите агент служб восстановления Azure hello
Hello портал Azure, установка агента служб восстановления Azure hello на каждом сервере узла Hyper-V, расположенных в облаках VMM hello требуется tooprotect.

Выполните следующую команду на всех узлах VMM hello.

```

marsagentinstaller.exe /q /nu

```


## <a name="step-7-configure-cloud-protection-settings"></a>Шаг 7. Настройка параметров защиты облачных систем
1. Создайте профиль tooAzure облачной защиты, выполнив следующую команду hello:

   ```

   $ReplicationFrequencyInSeconds = "300";
   $ProfileResult = New-AzureSiteRecoveryProtectionProfileObject -ReplicationProvider HyperVReplica -RecoveryAzureSubscription $AzureSubscriptionName -RecoveryAzureStorageAccount $StorageAccountName -ReplicationFrequencyInSeconds     $ReplicationFrequencyInSeconds;

   ```
2. Получите контейнер защиты, выполнив следующие команды hello:

   ```

   $PrimaryCloud = "testcloud"
   $protectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $PrimaryCloud;

   ```
3. Запустите hello сопоставление контейнера защиты hello с облаком hello:

   ```

   $associationJob = Start-AzureSiteRecoveryProtectionProfileAssociationJob -ProtectionProfile $profileResult -PrimaryProtectionContainer $protectionContainer;        

   ```
4. После завершения задания hello, выполните следующую команду hello:

        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
        $isJobLeftForProcessing = $true;
        }


1. После завершения обработки задания hello, выполните следующую команду hello:

        Do
        {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

        if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
        }While($isJobLeftForProcessing)



toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).

## <a name="step-8-configure-network-mapping"></a>Шаг 8. Настройка сетевого сопоставления
Перед началом сопоставления сетей убедитесь, что виртуальные машины на исходном сервере VMM hello tooa подключенной сети виртуальной Машины. Кроме того, создайте одну или несколько виртуальных сетей Azure. Обратите внимание, что несколько сетей виртуальной Машины может быть сопоставленных tooa одной сетью Azure.

Обратите внимание, что если hello целевая сеть содержит несколько подсетей, и одна из этих подсетей имеет hello находится совпадает с именем подсети, на какие hello исходной виртуальной машины, то hello реплики виртуальной машины после отработки отказа будет подключенных toothat целевой подсети. Если целевой подсети с совпадающим именем не существует, hello виртуальная машина будет подключенных toohello первой подсети в сети hello.

Первая команда Hello возвращает серверов для hello текущее хранилище Azure Site Recovery. Hello команда сохраняет серверы Microsoft Azure Site Recovery hello в переменной hello $Servers массива.

    $Servers = Get-AzureSiteRecoveryServer


Вторая команда Hello возвращает hello сети восстановления сайта для первого сервера hello в массиве hello $Servers. Команда Hello сохраняет сетей hello в hello $Networks переменной.

    $Networks = Get-AzureSiteRecoveryNetwork -Server $Servers[0]

Третья команда Hello возвращает подписками Azure с помощью командлета Get-AzureSubscription hello и затем сохраняет это значение в переменной hello $Subscriptions.

    $Subscriptions = Get-AzureSubscription



Четвертая команда Hello получает виртуальные сети Azure с помощью командлета Get-AzureVNetSite hello, а затем это значение в переменной hello $AzureVmNetworks.

    $AzureVmNetworks = Get-AzureVNetSite



Hello окончательного создает сопоставление между первичной и сетями виртуальной машины Azure hello hello. командлет Hello указывает hello основной сети как первый элемент $Networks hello. командлет Hello указывает сеть виртуальной машины как первого элемента hello $AzureVmNetworks с помощью его идентификатора. Команда Hello содержит идентификатор вашей подписки Azure.

    New-AzureSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureSubscriptionId $Subscriptions[0].SubscriptionId -AzureVMNetworkId $AzureVmNetworks[0].Id


## <a name="step-9-enable-protection-for-virtual-machines"></a>Шаг 9. Включение защиты для виртуальных машин
После надлежащей настройки серверов, облаков и сетей, можно включить защиту для виртуальных машин в облаке hello. Обратите внимание hello следующие:

Виртуальные машины должны соответствовать [предварительным требованиям к виртуальным машинам Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

tooenable защиты hello операционной системы и свойства диска операционной системы необходимо задать для виртуальной машины hello. При создании виртуальной машины в VMM с помощью шаблона виртуальной машины можно задать свойство hello. Можно также задать эти свойства для существующих виртуальных машин на hello **Общие** и **конфигурация оборудования** вкладки свойств виртуальной машины hello. Если не установить эти свойства в VMM вы будете может tooconfigure их на портале Azure Site Recovery hello.

1. Защита tooenable выполнения hello следующая команда контейнера защиты tooget hello:

     $ProtectionContainer = Get-AzureSiteRecoveryProtectionContainer -Name $CloudName
2. Получите сущность защиты hello (VM), выполнив следующую команду hello:

        $protectionEntity = Get-AzureSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer



1. Включите hello аварийного восстановления для hello виртуальной Машины, выполнив следующую команду hello:

        $jobResult = Set-AzureSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity     -Protection Enable -Force



## <a name="test-your-deployment"></a>Выполните тестирование развертывания
Планирование развертывания можно запустить тестовую отработку отказа для одной виртуальной машины или создайте план восстановления, состоящий из нескольких виртуальных машин и запустите тестовую отработку отказа для hello tootest. Тестовая обработка отказа имитирует механизм отработки отказа и восстановления в изолированной сети. Обратите внимание на следующее.

* Tooconnect toohello виртуальной машины в Azure с помощью удаленного рабочего стола, после отработки отказа hello, включите подключение к удаленному рабочему столу на виртуальной машине hello перед запуском тестовой отработки отказа hello.
* После отработки отказа будут использоваться открытый IP адрес tooconnect toohello виртуальной машины в Azure с помощью удаленного рабочего стола. Если требуется toodo это, убедитесь, что нет политик домена, запретить подключения tooa виртуальной машины, с помощью общедоступного адреса.

toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).

### <a name="create-a-recovery-plan"></a>Создайте план восстановления
1. Создание XML-файл в качестве шаблона для плана восстановления, используя данные hello ниже и сохраните его как «C:\RPTemplatePath.xml».
2. Измените узел RecoveryPlan hello идентификатор, имя, PrimaryServerId и SecondaryServerId.
3. Измените узел ProtectionEntity hello PrimaryProtectionEntityId (vmid из VMM).
4. Можно добавить дополнительные виртуальные машины, добавив дополнительные узлы ProtectionEntity.

        <#
        <?xml version="1.0" encoding="utf-16"?>
        <RecoveryPlan Id="d0323b26-5be2-471b-addc-0a8742796610" Name="rp-test"     PrimaryServerId="9350a530-d5af-435b-9f2b-b941b5d9fcd5"     SecondaryServerId="21a9403c-6ec1-44f2-b744-b4e50b792387" Description=""     Version="V2014_07">
          <Actions />
          <ActionGroups>
            <ShutdownAllActionGroup Id="ShutdownAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </ShutdownAllActionGroup>
            <FailoverAllActionGroup Id="FailoverAllActionGroup">
              <PreActionSequence />
              <PostActionSequence />
            </FailoverAllActionGroup>
            <BootActionGroup Id="DefaultActionGroup">
              <PreActionSequence />
              <PostActionSequence />
              <ProtectionEntity PrimaryProtectionEntityId="d4c8ce92-a613-4c63-9b03-    cf163cc36ef8" />
            </BootActionGroup>
          </ActionGroups>
          <ActionGroupSequence>
            <ActionGroup Id="ShutdownAllActionGroup" ActionId="ShutdownAllActionGroup"     Before="FailoverAllActionGroup" />
            <ActionGroup Id="FailoverAllActionGroup" ActionId="FailoverAllActionGroup"     After="ShutdownAllActionGroup" Before="DefaultActionGroup" />
            <ActionGroup Id="DefaultActionGroup" ActionId="DefaultActionGroup" After="FailoverAllActionGroup"/>
          </ActionGroupSequence>
        </RecoveryPlan>
        #>



1. Заполните данных hello в шаблоне hello.

        $TemplatePath = "C:\RPTemplatePath.xml";



1. Создайте hello RecoveryPlan:

        $RPCreationJob = New-AzureSiteRecoveryRecoveryPlan -File $TemplatePath -WaitForCompletion;

### <a name="run-a-test-failover"></a>Запуск тестовой отработки отказа
1. Получите объект RecoveryPlan hello, выполнив следующую команду hello:

     $RPObject = Get-AzureSiteRecoveryRecoveryPlan -Name $RPName;
2. Запустите тестовую отработку отказа hello, выполнив hello следующую команду:

        $jobIDResult = Start-AzureSiteRecoveryTestFailoverJob -RecoveryPlan $RPObject -Direction PrimaryToRecovery;


## <a name=monitor></a> Мониторинг активности
Используйте следующие команды toomonitor hello действие hello. Обратите внимание, что на toowait между задания для обработки toofinish hello.

    Do
    {
            $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
            Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
            if($job -eq $null -or $job.StateDescription -ne "Completed")
            {
                $isJobLeftForProcessing = $true;
            }

        if($isJobLeftForProcessing)
            {
                Start-Sleep -Seconds 60
            }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a>Дальнейшие действия
[Узнайте больше](/powershell/azure/overview) о командлетах PowerShell для Azure Site Recovery. </a>.
