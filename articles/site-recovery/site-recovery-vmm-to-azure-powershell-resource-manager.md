---
title: "виртуальные машины aaaReplicate Hyper-V в облаках VMM с помощью Azure Site Recovery и PowerShell (диспетчера ресурсов) | Документы Microsoft"
description: "Репликация виртуальных машин Hyper-V в облаках VMM с помощью Azure Site Recovery и PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a>Реплицировать виртуальные машины Hyper-V в tooAzure облака VMM, с помощью PowerShell и диспетчера ресурсов Azure
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

включает описание необходимых условий для сценария hello Hello статьи, а также демонстрируется

* Как tooset копирование хранилище служб восстановления
* Установка поставщика Azure Site Recovery hello на исходном сервере VMM hello
* Зарегистрируйте сервер hello в хранилище hello, добавьте учетную запись хранилища Azure
* Установка агента служб восстановления Azure hello на серверах узлов Hyper-V
* Настройте параметры защиты для облака VMM, которые будут применяться tooall защищенные виртуальные машины
* Включение защиты для таких виртуальных машин.
* Протестируйте toomake сбое hello убедиться, что все работает должным образом.

Если возникли проблемы с установкой этого сценария опубликовать вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью модели развертывания диспетчера ресурсов hello.
>
>

## <a name="before-you-start"></a>Перед началом работы
Убедитесь, что выполнены следующие предварительные требования.

### <a name="azure-prerequisites"></a>Предварительные требования Azure
* Вам потребуется учетная запись [Microsoft Azure](https://azure.microsoft.com/) . Если у вас ее нет, воспользуйтесь [бесплатной учетной записью](https://azure.microsoft.com/free). Кроме того, вы можете прочесть об hello [ценообразования Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).
* Вам потребуется подписка CSP при out сценарий hello репликации tooa CSP подписки. Дополнительные сведения о программе CSP hello в [как tooenroll в программе CSP hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).
* Вам потребуется реплицируемые данные tooAzure toostore учетная запись Azure v2 хранилища (диспетчера ресурсов). Hello учетная запись должна включена георепликация. Он должен быть в hello же регионе, что hello службы Azure Site Recovery и быть связан с hello одной подписки или подписки CSP hello. toolearn Дополнительные сведения о настройке хранилища Azure в разделе hello [tooMicrosoft введение хранилища Azure](../storage/common/storage-introduction.md) для ссылки.
* Необходимо убедиться, что виртуальные машины, которые вы хотите tooprotect соответствовать hello toomake [предварительные требования виртуальной машины Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

> [!NOTE]
> В настоящее через Powershell доступны только операции уровня виртуальной машины. Скоро будет включена поддержка операций на уровне плана восстановления.  Теперь не ограниченной tooperforming отказов только по «защищенных виртуальных Машин», а не на уровне плана восстановления.
>
>

### <a name="vmm-prerequisites"></a>Предварительные требования VMM
* Вам потребуется сервер VMM под управлением System Center 2012 R2.
* На любом сервере VMM, содержащем виртуальные машины, необходимо вернуть tooprotect должен работать под управлением hello поставщика Azure Site Recovery. При установке hello развертывания Azure Site Recovery.
* Необходимо по крайней мере одно облако на сервер VMM требуется tooprotect hello. облако Hello должен содержать:
  * одну или несколько групп узлов VMM;
  * Один или несколько серверов или кластеров узлов Hyper-V в каждой группе узлов.
  * Один или несколько виртуальных машин на сервере Hyper-V источника hello.
* Дополнительные сведения о настройке облаков VMM
  * Дополнительные сведения о частных облаках VMM в [новые возможности частного облака с System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) и [облака VMM 2012 и hello](http://go.microsoft.com/fwlink/?LinkId=324956).
  * Дополнительные сведения о [hello Настройка VMM облако структуры](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)
  * После того как все элементы структуры облака будут готовы, ознакомьтесь с дополнительными сведениями о создании частных облаков в разделах [Создание частного облака в VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) и [Пошаговое руководство: создание частных облаков с VMM System Center 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkId=324954).

### <a name="hyper-v-prerequisites"></a>Предварительные требования Hyper-V
* Hello серверы узла Hyper-V должны работать под управлением **Windows Server 2012** с ролью Hyper-V или **Microsoft Hyper-V Server 2012** и иметь hello установлены последние обновления.
* Если Hyper-V выполняется в кластере, учтите, что брокер кластера не создается автоматически при использовании кластера на основе статических IP-адресов. Брокер кластера hello tooconfigure вам потребуется вручную. Для
* Инструкции см. в разделе [как tooConfigure брокера реплики Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).
* Любой сервер узла Hyper-V или кластера, для которого требуется защита toomanage должны включаться в облаке VMM.

### <a name="network-mapping-prerequisites"></a>Предварительные требования сетевого сопоставления
При защите виртуальных машин в Azure, hello сопоставление сетей hello сетями виртуальных машин на исходном сервере VMM hello и целевой сети Azure tooenable hello следующее:

* Все машины, которые отработки отказа на hello же может подключиться tooeach других, независимо от используемого плана восстановления, находящиеся в сеть.
* Если сетевой шлюз настроен hello целевой сети Azure, виртуальные машины могут подключаться tooother локальных виртуальных машин.
* Если не настроить сетевое сопоставление, только hello виртуальной машины, отработка отказа в hello же плана восстановления будут другие возможности tooconnect tooeach после tooAzure отработку отказа.

Если требуется, чтобы toodeploy сетевого сопоставления необходимо иметь hello следующее:

* виртуальные машины Hello требуется tooprotect на исходном сервере VMM hello должно быть tooa подключенной сети виртуальной Машины. Сеть должна быть связанной tooa логической сети, связанной с облаком hello.
* Сеть Azure toowhich реплицировать виртуальные машины могут подключаться после отработки отказа. Будет предложено выбрать этой сети во время отработки отказа hello. сеть Hello должны находиться в hello же регионе, что подписки Azure Site Recovery.

Дополнительные сведения о сетевом сопоставлении см. в следующих статьях.

* [Как tooconfigure логических сетей в VMM](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [Как tooconfigure ВМ сетей и шлюзов в VMM](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [Как tooconfigure и мониторинг виртуальных сетей в Azure](https://azure.microsoft.com/documentation/services/virtual-network/)

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
1. Если у вас еще нет группы ресурсов в Azure Resource Manager, создайте ее.

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. Создайте новое хранилище служб восстановления и сохраните hello, созданном объекте хранилища ASR в переменной (будет использоваться позднее). Вы также можете получить hello ASR хранилища объекта post создания с помощью командлета Get-AzureRMRecoveryServicesVault hello:-

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Шаг 3: Установка контекста hello хранилище служб восстановления

Задайте контекст хранилища hello, выполнив hello ниже команду.

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

## <a name="step-5-create-an-azure-storage-account"></a>Шаг 5. Создание учетной записи хранения Azure

При отсутствии учетной записи хранилища Azure, создание учетной записи включена георепликация в hello в том же геообъекте hello хранилище, выполнив следующую команду hello:

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

Обратите внимание, что учетная запись хранения hello должна быть в hello же регионе, что служба восстановления сайтов Azure hello и связанные с hello одной подписке.

## <a name="step-6-install-hello-azure-recovery-services-agent"></a>Шаг 6: Установите агент служб восстановления Azure hello
1. Скачать агент служб восстановления Azure hello в [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) и установить его на каждом сервере узла Hyper-V, расположенных в hello VMM облаков, вы хотите tooprotect.
2. Выполните следующую команду на всех узлах VMM hello.

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a>Шаг 7. Настройка параметров защиты облачных систем
1. Создайте политику репликации tooAzure, выполнив следующую команду hello:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. Получите контейнер защиты, выполнив следующие команды hello:

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. Получите сведения о tooa политики hello переменную, с помощью задания hello, который был создан и отметить hello политики понятное имя:

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. Запустите hello сопоставление контейнера защиты hello с политикой репликации hello:

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. После завершения задания hello, выполните следующую команду hello:

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. После завершения обработки задания hello, выполните следующую команду hello:

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).

## <a name="step-8-configure-network-mapping"></a>Шаг 8. Настройка сетевого сопоставления
Перед началом сопоставления сетей убедитесь, что виртуальные машины на исходном сервере VMM hello tooa подключенной сети виртуальной Машины. Кроме того, создайте одну или несколько виртуальных сетей Azure.

Дополнительные сведения о как toocreate в виртуальной сети с помощью диспетчера ресурсов Azure и PowerShell в [Создание виртуальной сети через VPN-подключения сеть сеть, с помощью диспетчера ресурсов Azure и PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

Обратите внимание, что несколько сетей виртуальной машины может быть сопоставленных tooa одной сетью Azure. Если hello целевая сеть содержит несколько подсетей, и одна из этих подсетей имеет hello находится совпадает с именем подсети, на какие hello исходной виртуальной машины, а затем hello реплики виртуальной машины будет подключенных toothat целевой подсети после отработки отказа. Если никакой целевой подсети с совпадающим именем, hello виртуальная машина будет подключенных toohello первой подсети в сети hello.

1. Первая команда Hello возвращает серверов для hello текущее хранилище Azure Site Recovery. Hello команда сохраняет серверы Microsoft Azure Site Recovery hello в переменной hello $Servers массива.

        $Servers = Get-AzureRmSiteRecoveryServer
2. Вторая команда Hello возвращает hello сети восстановления сайта для первого сервера hello в массиве hello $Servers. Команда Hello сохраняет сетей hello в hello $Networks переменной.

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. Третья команда Hello получает виртуальные сети Azure, а затем это значение в переменной hello $AzureVmNetworks.

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. Hello окончательного создает сопоставление между первичной и сетями виртуальной машины Azure hello hello. командлет Hello указывает hello основной сети как первый элемент $Networks hello. командлет Hello указывает сеть виртуальной машины как первого элемента $AzureVmNetworks hello.

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a>Шаг 9. Включение защиты для виртуальных машин
После надлежащей настройки серверов hello, облаков и сетей, можно включить защиту для виртуальных машин в облаке hello.

 Обратите внимание hello следующие:

* Виртуальные машины должны соответствовать требованиям, предъявляемым Azure. Проверьте эти [предварительные условия и поддержка](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) в руководстве по планированию hello.
* tooenable защиты, hello операционной системы и свойства диска операционной системы необходимо задать для виртуальной машины hello. При создании виртуальной машины в VMM с помощью шаблона виртуальной машины можно задать свойство hello. Можно также задать эти свойства для существующих виртуальных машин на hello **Общие** и **конфигурация оборудования** вкладки свойств виртуальной машины hello. Если не установить эти свойства в VMM вы будете может tooconfigure их на портале Azure Site Recovery hello.

1. Защита tooenable выполнения hello следующая команда контейнера защиты tooget hello:

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. Получите сущность защиты hello (VM), выполнив следующую команду hello:

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. Включите hello аварийного восстановления для hello виртуальной Машины, выполнив следующую команду hello:

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a>Выполните тестирование развертывания
tootest тест можно выполнять развертывание отработку отказа для одной виртуальной машины или создайте план восстановления, состоящий из нескольких виртуальных машин, выполните тест отработки отказа для плана hello. Тестовая обработка отказа имитирует механизм отработки отказа и восстановления в изолированной сети. Обратите внимание на следующее.

* Tooconnect toohello виртуальной машины в Azure с помощью удаленного рабочего стола, после отработки отказа hello, включите подключение к удаленному рабочему столу на виртуальной машине hello перед запуском тестовой отработки отказа hello.
* После отработки отказа будут использоваться открытый IP адрес tooconnect toohello виртуальной машины в Azure с помощью удаленного рабочего стола. Если требуется toodo это, убедитесь, что нет политик домена, запретить подключения tooa виртуальной машины, с помощью общедоступного адреса.

toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).

### <a name="run-a-test-failover"></a>Запуск тестовой отработки отказа
- Запустите тестовую отработку отказа hello, выполнив hello следующую команду:

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a>Запуск запланированной отработки отказа
- Запустите hello Запланированный переход на другой ресурс, выполнив следующую команду hello:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a>Запуск незапланированной отработки отказа
- Запуск hello внеплановой отработки отказа, выполнив следующую команду hello:

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

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
