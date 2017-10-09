---
title: "aaaReplicate виртуальных машин Hyper-V с помощью PowerShell и диспетчера ресурсов Azure | Документы Microsoft"
description: "Автоматизация hello репликации tooAzure виртуальных машин Hyper-V с помощью PowerShell и диспетчера ресурсов Azure в Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: abhiag
editor: 
ms.assetid: 05e0d76e-c3f5-4845-8052-094019b6d102
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: 4fb15ce2e9ad54f1dd6f54ff769eb912aa4b0272
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-by-using-powershell-and-azure-resource-manager"></a>Репликация между локальными виртуальными машинами Hyper-V и Azure с помощью PowerShell и Azure Resource Manager
> [!div class="op_single_selector"]
> * [Портал Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell — Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Классический портал](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

## <a name="overview"></a>Обзор
Azure Site Recovery поддерживает tooyour бизнес-непрерывности и аварийного восстановления стратегии, управляя операциями репликации, отработки отказа и восстановления виртуальных машин в различных вариантов развертывания. Полный список сценариев развертывания см. в разделе hello [Обзор Azure Site Recovery](site-recovery-overview.md).

Azure PowerShell — это модуль, предоставляет toomanage командлеты Azure через Windows PowerShell. Он может работать с двумя типами модулей: hello Azure профиля модуля или hello модуль диспетчера ресурсов Azure.

Командлеты PowerShell для службы Site Recovery, доступные в Azure PowerShell для диспетчера ресурсов Azure, позволяют обеспечить защиту и выполнить восстановление серверов в Azure.

В этой статье описывается как toouse Windows PowerShell, вместе с Azure Resource Manager, tooconfigure toodeploy Site Recovery и управлять tooAzure защиты сервера. пример Hello, используемые в этой статье показано, как tooprotect, отработки отказа и восстановления виртуальных машин на tooAzure узла Hyper-V, с помощью Azure PowerShell с помощью диспетчера ресурсов Azure.

> [!NOTE]
> Hello командлеты PowerShell восстановления сайта в настоящее время позволяют hello tooconfigure следующие: один tooanother сайта диспетчера виртуальных машин, tooAzure сайта диспетчера виртуальных машин и tooAzure узла Hyper-V.
>
>

Не требуется toobe toouse expert PowerShell в этой статье, но вам нужен toounderstand hello основные понятия, например модули, командлеты и сеансов. Дополнительные сведения о Windows PowerShell можно найти в разделе [Начало работы с Windows PowerShell](http://technet.microsoft.com/library/hh857337.aspx).

Дополнительные сведения см. также в статье [Использование Azure PowerShell с Azure Resource Manager](../powershell-azure-resource-manager.md).

> [!NOTE]
> Партнеры корпорации Майкрософт, которые являются частью программы hello поставщика облачных решений (CSP) можно настроить и управлять защиты серверов, клиентов; tootheir клиентов соответствующих CSP подписки (клиента).
>
>

## <a name="before-you-start"></a>Перед началом работы
Убедитесь, что выполнены следующие предварительные требования.

* Учетная запись [Microsoft Azure](https://azure.microsoft.com/) . Начните с [бесплатной пробной версии](https://azure.microsoft.com/pricing/free-trial/). Также вы можете ознакомиться с [расценками на использование менеджера Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
* Azure PowerShell 1.0. Дополнительные сведения об этом выпуске и как tooinstall, в разделе [Azure PowerShell 1.0.](https://azure.microsoft.com/)
* Hello [AzureRM.SiteRecovery](https://www.powershellgallery.com/packages/AzureRM.SiteRecovery/) и [AzureRM.RecoveryServices](https://www.powershellgallery.com/packages/AzureRM.RecoveryServices/) модулей. Можно получить последние версии этих модулей hello hello [коллекции PowerShell](https://www.powershellgallery.com/)

В этой статье показано, как toouse Azure Powershell с tooconfigure диспетчера ресурсов Azure и управление ими защиты серверов. пример Hello, используемые в этой статье показано, как tooprotect виртуальной машины, работающей на узле Hyper-V, tooAzure. Hello следующие необходимые условия — пример определенного toothis. Более широкий набор требований для hello различные сценарии восстановления сайта, см. документации toohello относится toothat сценария.

* Узел Hyper-V под управлением Windows Server 2012 R2 или Microsoft Hyper-V Server 2012 R2, содержащий одну или несколько виртуальных машин.
* Серверы Hyper-V подключен toohello Интернет, напрямую или через прокси-сервер.
* Hello требуется tooprotect виртуальные машины должны соответствовать [требования виртуальной машины](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="step-1-sign-in-tooyour-azure-account"></a>Шаг 1: Войдите в учетную запись Azure tooyour
1. Откройте консоль PowerShell и выполнения этой команды toosign в tooyour учетная запись Azure. командлет Hello вызов веб-страницы, которое предложит ввести учетные данные учетной записи.

        Login-AzureRmAccount

    Кроме того, также может включать учетные данные учетной записи toohello параметр `Login-AzureRmAccount` командлет с помощью hello `-Credential` параметра.

    Если партнер CSP работе от имени клиента, укажите hello клиента как клиента, с помощью имени основного домена tenantID или клиента.

        Login-AzureRmAccount -Tenant "fabrikam.com"
2. Учетной записи может иметь несколько подписок, следует связывать hello подписку toouse с учетной записью hello.

        Select-AzureRmSubscription -SubscriptionName $SubscriptionName
3. Убедитесь, что подписки зарегистрированных toouse hello Azure поставщиков для служб восстановления и восстановления сайта с помощью hello, следующие команды:

   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices`
   * `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`

   В выходные данные этих команд, если hello hello **RegistrationState** задано слишком**зарегистрированные**, можно продолжить tooStep 2. В противном случае необходимо зарегистрировать поставщик отсутствует hello в вашей подписке.

   tooregister hello поставщика Azure Site Recovery и службы восстановления, запустите hello, следующие команды:

       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.SiteRecovery
       Register-AzureRmResourceProvider -ProviderNamespace Microsoft.RecoveryServices

   Убедитесь, что поставщики hello успешно зарегистрирован с помощью следующих команд hello: `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.RecoveryServices` и `Get-AzureRmResourceProvider -ProviderNamespace  Microsoft.SiteRecovery`.

## <a name="step-2-set-up-hello-recovery-services-vault"></a>Шаг 2: Настройка hello в хранилище службы восстановления
1. Создайте группу ресурсов диспетчера ресурсов Azure, в котором будет создание хранилища hello, или используйте существующую группу ресурсов. Можно создать новую группу ресурсов с помощью hello следующую команду:

        New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Geo  

    где hello $ResourceGroupName переменной содержит hello имя группы ресурсов hello требуется toocreate и hello $Geo переменная содержит hello Azure регион, в какую группу ресурсов hello toocreate (например, «Юг Бразилии»).

    Список групп ресурсов в подписке можно получить с помощью hello `Get-AzureRmResourceGroup` командлета.
2. Создайте хранилище служб восстановления Azure следующим образом:

        $vault = New-AzureRmRecoveryServicesVault -Name <string> -ResourceGroupName <string> -Location <string>

    Список существующих хранилищ можно получить с помощью hello `Get-AzureRmRecoveryServicesVault` командлета.

> [!NOTE]
> Если вы хотите tooperform операции восстановления сайта хранилищ, созданные с помощью классического портала hello или модуля Azure Service Management PowerShell hello, список таких хранилищ можно получить с помощью hello `Get-AzureRmSiteRecoveryVault` командлета. Для каждой новой операции рекомендуется создавать отдельное хранилище служб восстановления. Hello хранилищ Site Recovery, ранее созданную поддерживаются, но у вас нет новейших функций hello.
>
>

## <a name="step-3-set-hello-recovery-services-vault-context"></a>Шаг 3: Настройка hello контекст хранилища служб восстановления
1. Задайте контекст хранилища hello, выполнив hello следующую команду:

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-create-a-hyper-v-site-and-generate-a-new-vault-registration-key-for-hello-site"></a>Шаг 4: Создание узла Hyper-V и создание нового ключа регистрации хранилища для узла hello.
1. Создайте сайт Hyper-V следующим образом:

        $sitename = "MySite"                #Specify site friendly name
        New-AzureRmSiteRecoverySite -Name $sitename

    Этот командлет запускает узел hello toocreate задания Site Recovery и возвращает объект задания Site Recovery. Дождитесь toocomplete задания hello и убедитесь в успешном завершении задания hello.

    Можно получить объект задания hello и тем самым проверьте hello текущее состояние задания hello, с помощью командлета Get-AzureRmSiteRecoveryJob hello.
2. Создать и скачать ключ регистрации для сайта hello следующим образом:

        $SiteIdentifier = Get-AzureRmSiteRecoverySite -Name $sitename | Select -ExpandProperty SiteIdentifier
        Get-AzureRmRecoveryServicesVaultSettingsFile -Vault $vault -SiteIdentifier $SiteIdentifier -SiteFriendlyName $sitename -Path $Path

    Копировать hello загружаются узла ключа toohello Hyper-V. Вам также потребуется hello ключа tooregister hello Hyper-V узла toohello сайт.

## <a name="step-5-install-hello-azure-site-recovery-provider-and-azure-recovery-services-agent-on-your-hyper-v-host"></a>Шаг 5: Установка поставщика Azure Site Recovery hello и агента служб восстановления Azure на узле Hyper-V
1. Загрузить установщик hello hello последнюю версию поставщика hello из [Microsoft](https://aka.ms/downloaddra).
2. Установщик выполнения hello на узле Hyper-V и в конце hello hello установки по-прежнему toohello этап регистрации.
3. При появлении запроса предоставляют hello скачать ключ регистрации узла и выполнить регистрацию узла toohello hello Hyper-V.
4. Убедитесь, что зарегистрированные toohello сайта, на которых размещены hello Hyper-V с помощью hello следующую команду:

        $server =  Get-AzureRmSiteRecoveryServer -FriendlyName $server-friendlyname

## <a name="step-6-create-a-replication-policy-and-associate-it-with-hello-protection-container"></a>Шаг 6: Создайте политику репликации и связать его с контейнера защиты hello
1. Создайте политику репликации, выполнив следующую команду:

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points
        $storageaccountID = Get-AzureRmStorageAccount -Name "mystorea" -ResourceGroupName "MyRG" | Select -ExpandProperty Id

        $PolicyResult = New-AzureRmSiteRecoveryPolicy -Name $PolicyName -ReplicationProvider “HyperVReplicaAzure” -ReplicationFrequencyInSeconds $ReplicationFrequencyInSeconds  -RecoveryPoints $Recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId $storageaccountID

    Проверка hello вернул tooensure задания успешное создание политики репликации hello.

   > [!IMPORTANT]
   > Hello указанную учетную запись хранения должна быть в hello же регионе Azure, что ваше хранилище служб восстановления и должно быть включена георепликация.
   >
   > * Если hello восстановления учетной записи хранения имеет тип хранилища Azure (классические), переход на другой ресурс hello защищенных машин восстановить hello машины tooAzure IaaS (классические).
   > * Hello указана учетная запись хранения для восстановления типа хранилища Azure (Azure Resource Manager), переход на другой ресурс hello защищены машины восстановить hello машины tooAzure IaaS (диспетчера ресурсов Azure).
   >
   >
2. Получите hello защиты соответствующий toohello узел контейнера, следующим образом:

        $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer
3. Запустите hello сопоставление контейнера защиты hello с политикой репликации hello, как показано ниже:

     $Policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $PolicyName   $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy $Policy -PrimaryProtectionContainer $protectionContainer.

   Дождитесь toocomplete задания ассоциации hello и убедитесь, что он успешно завершено.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Шаг 7. Включение защиты для виртуальных машин
1. Получите hello защиты сущности соответствующего toohello виртуальной Машины требуется tooprotect, как показано ниже:

        $VMFriendlyName = "Fabrikam-app"                    #Name of hello VM
        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName
2. Защищать hello виртуальной машины, как показано ниже:

        $Ostype = "Windows"                                 # "Windows" or "Linux"
        $DRjob = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionEntity -Policy $Policy -Protection Enable -RecoveryAzureStorageAccountId $storageaccountID  -OS $OStype -OSDiskName $protectionEntity.Disks[0].Name

   > [!IMPORTANT]
   > Hello указанную учетную запись хранения должна быть в hello же регионе Azure, что ваше хранилище служб восстановления и должно быть включена георепликация.
   >
   > * Если hello восстановления учетной записи хранения имеет тип хранилища Azure (классические), переход на другой ресурс hello защищенных машин восстановить hello машины tooAzure IaaS (классические).
   > * Hello указана учетная запись хранения для восстановления типа хранилища Azure (Azure Resource Manager), переход на другой ресурс hello защищены машины восстановить hello машины tooAzure IaaS (диспетчера ресурсов Azure).
   >
   > Если hello ВМ, вы защищаете имеет более одного диска вложенного tooit, укажите hello диска операционной системы с помощью hello *OSDiskName* параметра.
   >
   >
3. Дождитесь tooreach виртуальных машин hello защищенное состояние после начальной репликации hello. Это может занять некоторое время, в зависимости от таких факторов, как объем hello toobe данные реплицируются и hello tooAzure вышестоящего пропускную способность. Состояние задания Hello и StateDescription следующим образом, обновляются при hello достижения в защищенное состояние виртуальной Машины.

        PS C:\> $DRjob = Get-AzureRmSiteRecoveryJob -Job $DRjob

        PS C:\> $DRjob | Select-Object -ExpandProperty State
        Succeeded

        PS C:\> $DRjob | Select-Object -ExpandProperty StateDescription
        Completed
4. Обновите свойства восстановления, например hello размера роли виртуальной Машины и отработки отказа tooupon карты интерфейса сети hello сети Azure tooattach hello виртуальной машины.

        PS C:\> $nw1 = Get-AzureRmVirtualNetwork -Name "FailoverNw" -ResourceGroupName "MyRG"

        PS C:\> $VMFriendlyName = "Fabrikam-App"

        PS C:\> $VM = Get-AzureRmSiteRecoveryVM -ProtectionContainer $protectionContainer -FriendlyName $VMFriendlyName

        PS C:\> $UpdateJob = Set-AzureRmSiteRecoveryVM -VirtualMachine $VM -PrimaryNic $VM.NicDetailsList[0].NicId -RecoveryNetworkId $nw1.Id -RecoveryNicSubnetName $nw1.Subnets[0].Name

        PS C:\> $UpdateJob = Get-AzureRmSiteRecoveryJob -Job $UpdateJob

        PS C:\> $UpdateJob

        Name             : b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        ID               : /Subscriptions/a731825f-4bf2-4f81-a611-c331b272206e/resourceGroups/MyRG/providers/Microsoft.RecoveryServices/vault
                           s/MyVault/replicationJobs/b8a647e0-2cb9-40d1-84c4-d0169919e2c5
        Type             : Microsoft.RecoveryServices/vaults/replicationJobs
        JobType          : UpdateVmProperties
        DisplayName      : Update hello virtual machine
        ClientRequestId  : 805a22a3-be86-441c-9da8-f32685673112-2015-12-10 17:55:51Z-P
        State            : Succeeded
        StateDescription : Completed
        StartTime        : 10-12-2015 17:55:53 +00:00
        EndTime          : 10-12-2015 17:55:54 +00:00
        TargetObjectId   : 289682c6-c5e6-42dc-a1d2-5f9621f78ae6
        TargetObjectType : ProtectionEntity
        TargetObjectName : Fabrikam-App
        AllowedActions   : {Restart}
        Tasks            : {UpdateVmPropertiesTask}
        Errors           : {}



## <a name="step-8-run-a-test-failover"></a>Шаг 8. Запуск тестовой отработки отказа
1. Запустите задание тестовой отработки отказа, выполнив следующую команду:

        $nw = Get-AzureRmVirtualNetwork -Name "TestFailoverNw" -ResourceGroupName "MyRG" #Specify Azure vnet name and resource group

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMFriendlyName -ProtectionContainer $protectionContainer

        $TFjob = Start-AzureRmSiteRecoveryTestFailoverJob -ProtectionEntity $protectionEntity -Direction PrimaryToRecovery -AzureVMNetworkId $nw.Id
2. Проверьте теста hello создания виртуальной Машины в Azure. (hello теста отработки отказа Задание приостановлено, после создания hello тестовой виртуальной Машине в Azure. Hello завершения задания по очистке дефекты hello создан при возобновлении задания hello, как показано в следующем шаге hello.)
3. Полный hello тестирования отработки отказа следующим образом:

        $TFjob = Resume-AzureRmSiteRecoveryJob -Job $TFjob

## <a name="next-steps"></a>Дальнейшие действия
[Узнайте больше](https://msdn.microsoft.com/library/azure/mt637930.aspx) о командлетах PowerShell инструмента Azure Resource Manager для службы Azure Site Recovery.
