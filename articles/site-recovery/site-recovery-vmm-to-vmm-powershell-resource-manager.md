---
title: "aaaReplicate виртуальных машин Hyper-V в VMM tooa вторичного сайта с помощью PowerShell (диспетчера ресурсов Azure) | Документы Microsoft"
description: "Описывает, каким образом tooa с помощью PowerShell (диспетчера ресурсов) вторичный сайт VMM облаков toodeploy Azure Site Recovery tooorchestrate репликации, отработки отказа и восстановления виртуальных машин Hyper-V в VMM"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a>Реплицировать виртуальные машины Hyper-V в VMM облаков tooa вторичный сайт VMM с помощью PowerShell (диспетчера ресурсов)
> [!div class="op_single_selector"]
> * [Портал Azure](site-recovery-vmm-to-vmm.md)
> * [Классический портал](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell — Resource Manager](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Вас приветствует tooAzure Site Recovery. В этой статье следует используйте, если необходимо, чтобы tooreplicate локальных виртуальных машин Hyper-V управляются в облаках диспетчера виртуальных машин System Center (VMM): tooa вторичного сайта.

В этой статье показано, как toouse PowerShell tooautomate общие задачи должны tooperform при настройке Azure Site Recovery tooreplicate Hyper-V виртуальных машин в облаках VMM System Center VMM облаков центра tooSystem вторичном сайте.

включает описание необходимых условий для сценария hello Hello статьи, а также демонстрируется

* Как tooset копирование хранилище служб восстановления
* Установите hello поставщика Azure Site Recovery на исходном сервере VMM hello и целевой сервер VMM hello
* Зарегистрируйте серверы VMM hello в хранилище hello
* Настройте политику репликации для облака VMM hello. параметры репликации Hello hello политики будет применен tooall защищенные виртуальные машины
* Включите защиту для виртуальных машин hello.
* Тестовая отработка отказа hello виртуальных машин, отдельно или как часть toomake для плана восстановления, убедиться, что все работает должным образом.
* Выполнение плановой или незапланированной отработки отказа виртуальных машин по отдельности или в составе toomake для плана восстановления, убедиться, что все работает должным образом.

Если возникли проблемы с установкой этого сценария опубликовать вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md) . Azure также содержит два портала — hello классический портал Azure, поддерживающий hello классической модели развертывания и hello портал Azure с поддержкой обе модели развертывания. В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.
>
>

## <a name="on-premises-prerequisites"></a>Предварительные требования для локальной среды
Вот что вам понадобится в hello первичного и вторичного локальных сайтов toodeploy этот сценарий:

| **Предварительные требования** | **Дополнительные сведения** |
| --- | --- |
| **VMM** |Мы рекомендуем развернуть сервер VMM в первичном сайте hello и сервера VMM на вторичном сайте hello.<br/><br/> Вы можете также [выполнять репликацию между облаками на отдельном сервере VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). toodo это необходимо по крайней мере два облака, настроенные на сервере VMM hello.<br/><br/> Серверы VMM должен работать под управлением System Center 2012 SP1 с последними обновлениями hello.<br/><br/> Каждый сервер VMM, должна иметь на один или несколько облаков настроен и все должен иметь набор профилей hello емкости Hyper-V. <br/><br/>Облака должны содержать одну или несколько групп узлов VMM.<br/><br/>Дополнительные сведения о настройке облаков VMM в [hello Настройка VMM облако структуры](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), и [Пошаговое руководство: создание частных облаков с помощью System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).<br/><br/> Серверы VMM должны иметь доступ к Интернету. |
| **Hyper-V** |Серверы Hyper-V должны работать под управлением Windows Server 2012 с ролью Hyper-V hello и иметь hello установлены последние обновления.<br/><br/> Сервер Hyper-V должен содержать одну или несколько виртуальных машин.<br/><br/>  Серверы узла Hyper-V должны находиться в группах узлов в hello Первичное и вторичное облака VMM.<br/><br/> Если вы используете Hyper-V в кластере на платформе Windows Server 2012 R2, то необходимо установить [обновление 2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Если вы используете Hyper-V в кластере на платформе Windows Server 2012, то учтите, что брокер кластера не создается автоматически при использовании кластера на основе статических IP-адресов. Брокер кластера hello tooconfigure вам потребуется вручную. [Подробная информация](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Поставщик** |Во время развертывания службы восстановления сайтов установите hello поставщика Azure Site Recovery на серверах VMM. Hello поставщик взаимодействует с Site Recovery через HTTPS 443 tooorchestrate репликации. Репликация данных между hello основной и дополнительный серверы Hyper-V через hello локальной сети или VPN-подключения.<br/><br/> Hello поставщик, запущенный на сервере VMM hello должен получить доступ к URL-адреса toothese: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.<br/><br/> Разрешить связь брандмауэра из toohello серверы VMM hello, кроме [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) и разрешить hello протокола HTTPS (443). |

### <a name="network-mapping-prerequisites"></a>Предварительные требования сетевого сопоставления
Сети сопоставление между сетями виртуальных Машин VMM на hello первичных и вторичных серверов VMM для:

* Оптимальное размещение виртуальных машин реплик на вторичных узлах Hyper-V после отработки отказа.
* Подключение сети виртуальных Машин tooappropriate виртуальные машины реплики.
* Если не настроить сетевое сопоставление реплики виртуальных машин не будет tooany подключенной сети после отработки отказа.
* Если требуется, чтобы tooset сети сопоставления во время восстановления сайта здесь это вам потребуется:

  * Убедитесь tooa подключенной сети виртуальной Машины VMM виртуальные машины на исходном hello сервер узла Hyper-V. Сеть должна быть связанной tooa логической сети, связанной с облаком hello.
  * Убедитесь, что hello вторичное облако, которое будет использоваться для восстановления настроена соответствующая сеть ВМ. Сеть виртуальной Машины должна была tooa связанной логической сети, связанной с hello вторичное облако.

Дополнительные сведения о настройке сетей в VMM в hello ниже статьи

* [Как tooconfigure логических сетей в VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Как tooconfigure ВМ сетей и шлюзов в VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)

[Узнайте больше](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) о принципе действия сетевого сопоставления.

### <a name="powershell-prerequisites"></a>Необходимые компоненты PowerShell
Убедитесь, что у вас есть toogo готовности Azure PowerShell. Если вы уже используете PowerShell, вам потребуется tooupgrade tooversion 0.8.10 или более поздней версии. Сведения о настройке PowerShell см. в разделе hello [проводят tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs). После установки и настройки PowerShell вы можете просматривать все hello доступных командлетов для службы hello [здесь](/powershell/azure/overview).

toolearn советы, помогающие использовать командлеты hello, например как значения параметров, входы и выходы обычно обрабатываются в Azure PowerShell, в разделе hello [руководство по работе с командлетами Azure tooget](/powershell/azure/get-started-azureps).

## <a name="step-1-set-hello-subscription"></a>Шаг 1: Задайте подписку hello
1. Из Azure powershell, tooyour входа учетной записи Azure: с помощью следующих командлетов hello

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. Получите список своих подписок. Выводит также список hello subscriptionIDs для каждой из подписок hello. Запишите subscriptionID hello hello подписки, в котором вы хотите хранилище служб восстановления toocreate hello    

        Get-AzureRmSubscription
3. Задать hello подписки, в какие hello хранилище служб восстановления является toobe созданные упомянуть hello идентификатор подписки

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a>Шаг 2. Создание хранилища служб восстановления
1. Если у вас еще нет группы ресурсов Azure Resource Manager, создайте ее.

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Создайте новое хранилище служб восстановления и сохраните hello, созданном объекте хранилища ASR в переменной (будет использоваться позднее). Вы также можете получить hello ASR хранилища объекта post создания с помощью командлета Get-AzureRMRecoveryServicesVault hello:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Шаг 3: Установка контекста hello хранилище служб восстановления
1. Если хранилище уже создан, запустите hello ниже команда tooget hello хранилища.

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. Задайте контекст хранилища hello, выполнив hello ниже команду.

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a>Шаг 4: Установка поставщика Azure Site Recovery hello
1. На виртуальной машине VMM hello создайте каталог, выполнив следующую команду hello:

       New-Item c:\ASR -type directory
2. Извлеките файлы hello, с помощью поставщика загружаются hello, выполнив следующую команду hello

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. Установите поставщик hello, с помощью hello, следующие команды:

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   Дождитесь установки toofinish hello.
4. Зарегистрируйте сервер hello в хранилище hello, с помощью hello следующую команду:

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a>Шаг 5. Создание и связывание политики репликации
1. Создайте политику репликации Hyper-V 2012 R2, запустив следующую команду hello.

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > Hello облака VMM может содержать узлы Hyper-V под управлением других версий Windows Server (согласно hello требования Hyper-V), но политика репликации hello — версии операционной системы. Если вы используете узлы с разными версиями операционных систем, то создайте отдельные политики репликации для каждого типа версии ОС. Пример. Если у вас есть пять узлов с Windows Server 2012 и три с Windows Server 2012 R2, то создайте две политики репликации — по одной для каждого типа версии ОС.

1. Получите, выполнив следующие команды hello hello основную защиту (основное облако VMM) и восстановления защиты контейнер (восстановление облака VMM):

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. Получить политику hello, созданный на шаге 1, с помощью hello понятное имя политики hello

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Запуск сопоставления hello hello контейнера защиты (облака VMM) с политикой репликации hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. Дождитесь toocomplete задания связи политики hello. Можно проверить, если hello задание завершено с помощью hello, следующий фрагмент команды PowerShell.

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   После завершения обработки задания hello, выполните следующую команду hello:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).

## <a name="step-6-configure-network-mapping"></a>Шаг 6. Настройка сетевого сопоставления
1. Первая команда Hello возвращает серверов для hello текущее хранилище Azure Site Recovery. Hello команда сохраняет серверы Microsoft Azure Site Recovery hello в переменной hello $Servers массива.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Hello ниже команды получить hello сети восстановления сайта для hello исходный сервер VMM и hello целевой сервер VMM.

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > Hello исходный сервер VMM может hello первый или hello второй массив серверов один в hello. Проверьте имена hello серверов VMM hello и соответствующим образом получить hello сети


1. Hello окончательного создает сопоставление между hello основной сети и сети восстановления hello. командлет Hello указывает hello основной сети как первый элемент $PrimaryNetworks и hello сети восстановления как первый элемент $RecoveryNetworks hello hello.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a>Шаг 7. Настройка сопоставления хранилищ
1. Hello ниже команда получает список hello классификации хранилища в переменную $storageclassifications.

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. Классификация источников hello в переменную $SourceClassificaion и целевой классификации в переменную $TargetClassification, получить Hello ниже команды.

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > Hello исходных и целевых классификаций может быть любой элемент в массиве hello. См. выходные данные toohello hello ниже индекс hello toofigure команды исходных и целевых классификаций $storageclassifications массива.

    > Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table


1. Hello ниже командлет создает сопоставление между hello классификации источника и целевой классификацией hello.

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a>Шаг 8. Включение защиты для виртуальных машин
После надлежащей настройки серверов hello, облаков и сетей, можно включить защиту для виртуальных машин в облаке hello.

1. Защита tooenable выполнения hello следующая команда контейнера защиты tooget hello:

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. Получите сущность защиты hello (VM), выполнив следующую команду hello:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. Включите репликацию для виртуальной Машины hello, выполнив следующую команду hello:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a>Выполните тестирование развертывания
Планирование развертывания можно запустить тестовую отработку отказа для одной виртуальной машины или создайте план восстановления, состоящий из нескольких виртуальных машин и запустите тестовую отработку отказа для hello tootest. Тестовая обработка отказа имитирует механизм отработки отказа и восстановления в изолированной сети.

> [!NOTE]
> Можно создать план восстановления для приложения на портале Azure.
>
>

toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).

### <a name="run-a-test-failover"></a>Запуск тестовой отработки отказа
1. Запустите hello ниже командлеты tooget hello ВМ сети toowhich требуется tootest отработки отказа виртуальные машины.

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. Выполните тестовую отработку отказа виртуальной машины, выполнив следующие hello.

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. Выполните тестовую отработку отказа плана восстановления, выполнив следующие hello.

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a>Запуск запланированной отработки отказа
1. Выполните Плановую отработку отказа виртуальной машины, выполнив следующие hello.

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. Выполните Плановую отработку отказа плана восстановления, выполнив следующие hello.

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a>Запуск незапланированной отработки отказа
1. Выполните незапланированную отработку отказа виртуальной Машины, выполнив hello ниже:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

2. выполните незапланированной отработки отказа плана восстановления, выполнив следующие hello.

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

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
[Узнайте больше](/powershell/module/azurerm.recoveryservices.backup/#recovery) об использовании командлетов PowerShell инструмента Azure Resource Manager для службы Azure Site Recovery.
