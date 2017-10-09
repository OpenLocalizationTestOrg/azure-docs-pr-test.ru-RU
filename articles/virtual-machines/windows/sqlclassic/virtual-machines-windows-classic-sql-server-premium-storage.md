---
title: "aaaUse хранилища Azure Premium с SQL Server | Документы Microsoft"
description: "В этой статье использует ресурсы, созданные с помощью hello классической модели развертывания и дает рекомендации по использованию хранилища Azure Premium с SQL Server, работающий на виртуальных машинах Azure."
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a>Использование хранилища Azure Premium Storage с SQL Server на виртуальных машинах
## <a name="overview"></a>Обзор
[Хранилище Azure Premium](../../../storage/common/storage-premium-storage.md) hello следующего поколения хранилище, обеспечивающее малая задержка и высокая пропускная способность ввода-ВЫВОДА. Данное хранилище лучше справляется с интенсивными нагрузками ввода-вывода, как, например, SQL Server на [виртуальных машинах](https://azure.microsoft.com/services/virtual-machines/)IaaS.

> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../azure-resource-manager/resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.

В этой статье приведены планированию и рекомендации по переносу виртуальной машины под управлением SQL Server toouse хранилище Premium. Она включает описание этапов работы с инфраструктурой Azure (сеть, хранилище) и гостевой виртуальной машиной Windows. пример Hello в hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) показано полное комплексное tooend миграции как улучшить toomove больше виртуальных машин tootake преимуществами локальной SSD-хранилище с помощью PowerShell.

Это важные toounderstand процедура конца в конец hello используя хранилища Azure Premium с SQL Server на виртуальных машинах IAAS. А именно:

* Идентификация hello предварительные требования toouse хранилище Premium.
* Примеры развертывания SQL Server в IaaS tooPremium хранилища для нового развертывания.
* Примеры миграции существующих развернутых служб — как отдельных серверов, так и развернутых служб, использующих группы доступности AlwaysOn SQL.
* Возможные подходы при миграции.
* Пример полной конца в конец действия Azure, Windows и SQL Server для миграции hello существующую реализацию Always On.

Более детальные дополнительные сведения о сервере SQL Server в виртуальных машинах Azure содержатся в статье [SQL Server в виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

**Автор:** Дэниэл Сол (Daniel Sol) **Технические рецензенты:** Луис Карлос Варгас Херринг (Luis Carlos Vargas Herring), Санджай Мишра (Sanjay Mishra), Правин Митал (Pravin Mital), Юрген Томас (Juergen Thomas), Гонсало Руис (Gonzalo Ruiz).

## <a name="prerequisites-for-premium-storage"></a>Необходимые условия для использования хранилища Premium Storage
Существует несколько предварительных условий для использования Premium Storage.

### <a name="machine-size"></a>Размер машины
Для использования хранилища Premium вам потребуется серии toouse DS виртуальные машины (VM). Если ранее не пользовались серии DS машин в облачной службе до, необходимо удалить существующие ВМ hello, исключить hello присоединенные диски и затем создать новую облачную службу, прежде чем повторно создавать виртуальную Машину в качестве доменных служб Active Directory роли размера hello. Дополнительные сведения о размерах виртуальных машин см. в статье [Размеры виртуальных машин и облачных служб для Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="cloud-services"></a>Облачные службы
Виртуальные машины DS* можно использовать с хранилищем Premium Storage, только если они были созданы в новой облачной службе. При использовании SQL Server Always On в Azure, hello всегда на прослушиватель будет ссылаться toohello Azure внутренний или внешний IP-адрес подсистемы балансировки нагрузки адрес, связанный с облачной службой. В этой статье основное внимание уделено toomigrate, сохраняя доступность в этом сценарии.

> [!NOTE]
> Серии DS * необходимо hello первой виртуальной Машины, развернутой toohello новой облачной службы.
>
>

### <a name="regional-vnets"></a>Региональные виртуальные сети
Для доменных служб Active Directory * виртуальных машин, необходимо настроить hello виртуальной сети (VNET) размещение ваш язык toobe виртуальных машин. Этот «может быть расширен» hello виртуальной сети является tooallow hello больше виртуальных машин toobe подготовлены в других кластерах и разрешить связь между ними. В следующий снимок экрана приветствия hello выделенное расположение показывает региональных виртуальных сетей, в то время как первый результат hello показывает «узких» виртуальной сети.

![RegionalVNET][1]

Можно вызвать tooa toomigrate службу поддержки Майкрософт региональной виртуальной сети, корпорация Майкрософт будут внесены изменения, то toocomplete hello миграции tooregional виртуальных сетей, изменив hello территориальная группа в конфигурации сети hello. Экспортировать hello конфигурации сети в PowerShell, а затем замените hello **AffinityGroup** свойство в hello **VirtualNetworkSite** элемент с **расположение** свойство. Укажите `Location = XXXX`, где `XXXX` регион Azure. Затем импортируйте новую конфигурацию hello.

Например учитывая hello следующая конфигурация виртуальной сети:

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

toomove этот tooa региональной виртуальной сети в Западной Европе изменить toohello конфигурации hello следующие:

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a>учетные записи хранения;
Вам потребуется toocreate новой учетной записи хранения, настроенной для хранения Premium. Обратите внимание, что использование hello хранилища Premium задается в учетной записи хранилища hello не для отдельных виртуальных жестких дисков, однако при использовании ВМ серии DS * можно присоединить виртуальные жесткие ДИСКИ из Premium и стандартное хранилище учетных записей. Это можно использовать, если tooplace hello виртуального жесткого диска операционной системы на toohello учетной записи хранения Premium не требуется.

следующие Hello **New AzureStorageAccountPowerShell** с hello «Premium_LRS» **тип** создает учетную запись хранения Premium:

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a>Настройки кэша виртуальных жестких дисков
Hello основное различие между созданием диски, которые являются частью учетной записи хранения Premium — параметр кэша диска hello. Для дисков томов данных SQL Server рекомендуется использовать**кэширование чтения**. Тома журналов транзакций, параметр кэша диска hello следует установить слишком "**нет**". Это отличается от hello рекомендаций для учетных записей стандартного хранилища.

После присоединения виртуальных жестких дисков hello hello в кэше не могут быть изменены. Будет необходимо toodetach и заново присоединить hello виртуального жесткого диска с помощью параметра обновленным кэшем.

### <a name="windows-storage-spaces"></a>Дисковое пространство Windows
Можно использовать [дисковые пространства Windows](https://technet.microsoft.com/library/hh831739.aspx) так же предыдущих стандартное хранилище, это позволит вам toomigrate виртуальной Машины, которая уже использует дисковые пространства. пример Hello в [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (шаг 9 и далее) демонстрирует hello tooextract кода Powershell и Импорт виртуальной Машины с помощью нескольких подключенных виртуальных жестких дисков.

Пулы носителей использовались в пропускной способности tooenhance учетной записи хранилища Azure, Standard и уменьшить задержку. Возможно, вам интересно будет попробовать пулы носителей в Premium Storage для новых развертываний, однако они создают дополнительные сложности при настройке хранилища.

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a>Как toofind виртуальные диски Azure сопоставить toostorage пулы
Как рекомендации параметр отдельного кэша для подключенных виртуальных жестких дисков, вы можете toocopy hello виртуальные жесткие диски tooa учетной записи хранения Premium. Тем не менее при повторном присоединении их новой серии DS toohello виртуальной Машины, может потребоваться параметры кэша tooalter hello. Это проще приветствия tooapply хранилище Premium рекомендуемые параметры кэша, при наличии отдельных виртуальных жестких дисков для hello SQL данных файлов и журнала файлов (а не один виртуальный жесткий ДИСК, содержащий оба).

> [!NOTE]
> Если у вас есть файлы данных и журналов SQL Server на hello одном томе, выбрать параметр кэширования hello зависит от hello шаблоны доступа к операции ввода-ВЫВОДА для базы данных рабочих нагрузок. Только тестирование может показать, какой параметр кэширования лучше всего подходит для данного сценария.
>
>

Однако при использовании Windows дискового пространства, который состоит из нескольких виртуальных жестких дисков, необходимо будет toolook в вашей исходной tooidentify скрипты, связанные VHD, в какие конкретного пула таким образом можно затем задать параметры кэша hello соответствующим образом для каждого диска.

Если нет исходного доступных tooshow сценария вы сопоставляющие виртуальные жесткие диски toohello пула носителей, можно использовать после действия toodetermine hello диска и хранилища пула сопоставления hello.

Для каждого диска используйте следующие шаги hello:

1. Получение списка дисков присоединенного tooVM с hello **Get-AzureVM** команды:

    Get-AzureVM -ServiceName <servicename> -Name <vmname> | Get-AzureDataDisk
2. Обратите внимание, hello Diskname и LUN.

    ![DisknameAndLUN][2]
3. Удаленный рабочий стол в hello виртуальной Машины. Затем перейдите слишком**Управление компьютером** | **диспетчер устройств** | **дисков**. Просмотрите свойства hello каждого hello «Microsoft виртуальных дисков»

    ![VirtualDiskProperties][3]
4. Hello здесь номер LUN является номер LUN toohello ссылки, указываемые при присоединении toohello hello виртуального жесткого диска виртуальной Машины.
5. Для hello «Виртуальный диск Microsoft» go toohello **сведения** на вкладке выберите hello **свойство** списка, перейдите в слишком**раздел реестра**. В hello **значение**, Примечание hello **смещение**, который является 0002 в следующий снимок экрана приветствия. Hello 0002 обозначает hello PhysicalDisk2 hello ссылки пула носителей.

    ![VirtualDiskPropertyDetails][4]
6. Для каждого пула носителей выгрузите hello связанные диски:

    Get-StoragePool -FriendlyName AMS1pooldata | Get-PhysicalDisk

    ![GetStoragePool][5]

Теперь вы можете использовать этот tooassociate сведения присоединенных дисков tooPhysical виртуальные жесткие диски в пулы носителей.

После сопоставления дисков tooPhysical виртуальные жесткие диски в пулы носителей можно отсоединить и скопировать tooa учетной записи хранения Premium присоедините их с правильный кэш hello задание. См. в разделе Пример hello в hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), шаги 8 – 12. Следующие действия показывают, как tooextract VHD ВМ присоединенного диска tooa CSV файл конфигурации, скопируйте VHD hello, изменить настройки кэша диска hello и наконец повторного развертывания виртуальной Машины hello как серии DS виртуальной Машины с hello все подключенные диски.

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a>Пропускная способность хранилища виртуальной машины и хранилища VHD
Hello производительность хранилища зависит hello размер виртуальной Машины DS * указан и hello размер виртуального жесткого диска. виртуальные машины Hello имели разные ограничения по производительности для hello количество виртуальных жестких дисков, которые можно подключить и максимальная пропускная способность (МБ/с), они будут поддерживать hello. Номера hello используемой пропускной способности, см. [виртуальной машины размеры и облачных служб для Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Повышенная производительность диска достигается при увеличении размеров диска. Это следует учитывать при планировании миграции. Дополнительные сведения [см hello таблицы для операций ввода-ВЫВОДА и типы дисков](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).

Наконец, следует помнить, что виртуальные машины имеют различную максимальную пропускную способность, которую они будут поддерживать для всех подключенных дисков. В условиях высокой нагрузки может перегрузке hello максимальное число дисковых пропускную способность, доступную для заданного размера роли виртуальной Машины. Например Standard_DS14 будет поддерживать too512MB в секунду; Таким образом с помощью трех дисков P30 удалось перегрузке пропускную способность диска hello hello виртуальной Машины. Однако в этом примере удалось превышен предел пропускной способности hello в зависимости от сочетание hello чтения и записи операций ввода-вывода.

## <a name="new-deployments"></a>Новые развертывания
Hello следующих двух разделах показано, как можно развернуть виртуальные машины SQL Server tooPremium хранилища. Как упоминалось ранее, вам не обязательно диска ОС hello tooplace на хранилище Premium. Вы можете toodo это если планируется tooplace любой рабочей нагрузки, большим объемом операций ввода-ВЫВОДА на hello виртуального жесткого диска операционной системы.

Hello в первом примере показано использование существующих образов коллекции Azure. Hello во втором примере показано, как изображения toouse пользовательских виртуальных Машин, у вас есть учетная запись хранения Standard.

> [!NOTE]
> В этих примерах предполагается, что вы уже создали региональную виртуальную сеть.
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a>Создание новой виртуальной машины с хранилищем Premium Storage с помощью образа из Коллекции
Hello приведенном ниже примере показано, как tooplace hello виртуального жесткого диска операционной системы на хранилище premium и подключить виртуальные жесткие диски для хранения Premium. Тем не менее можно также разместить диска ОС hello в стандартном хранилище учетной записи и затем подключить виртуальные жесткие диски, которые находятся в учетной записи хранения Premium. Мы продемонстрируем оба сценария.

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a>Шаг 1. Создайте учетную запись хранения Premium
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a>Шаг 2. Создайте новую облачную службу
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a>Шаг 3. Зарезервируйте VIP облачной службы (необязательно)
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a>Шаг 4. Создайте контейнер виртуальных машин
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a>Шаг 5. Разместите виртуальный жесткий диск операционной системы в хранилище Standard или Premium 
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a>Шаг 6. Создайте виртуальную машину
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a>Создать новый toouse ВМ хранилища Premium с помощью пользовательского образа
В этом сценарии показана ситуация, где у вас есть существующие настраиваемые образы, хранящиеся в учетной записи хранения Standard. Как уже упоминалось, следует ли tooplace hello виртуального жесткого диска операционной системы на хранилище Premium, вам потребуется toocopy hello образ, который существует в hello Стандартная учетная запись хранения и передачи tooa хранилище Premium, прежде чем можно будет использовать. Если у вас есть образ в локальной среде, можно также использовать этот метод toocopy, прямо toohello учетной записи хранения Premium.

#### <a name="step-1-create-storage-account"></a>Шаг 1. Создайте учетную запись хранения
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a>Шаг 2. Создайте облачную службу
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a>Шаг 3. Используйте существующий образ
Вы можете использовать существующий образ. Вы также можете [взять образ имеющегося компьютера](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Созданием образа компьютера hello Примечание не имеет toobe DS * машины. После получения изображений hello hello следующие шаги Показать как toocopy его toohello учетной записи хранения Premium с hello **AzureStorageBlobCopy начала** командлетов PowerShell для.

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a>Шаг 4. Скопируйте BLOB-объект между учетными записями хранения
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a>Шаг 5. Регулярно проверяйте состояние копирования:
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a>Шаг 6: Добавление образа диска tooAzure диск хранилища в подписке
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> Вы можете обнаружить, несмотря на то, что отчеты о состоянии hello как успех, по-прежнему получение аренды ошибка диска. В этом случае подождите около 10 минут.
>
>

#### <a name="step-7--build-hello-vm"></a>Шаг 7: Построение hello виртуальной Машины
Здесь вы создаете hello виртуальной Машины из образа и присоединения два виртуальных жестких дисков хранилища Premium:

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a>Существующие развернутые службы, не использующие группы доступности AlwaysOn
> [!NOTE]
> Для существующих развертываний сначала узнать hello [необходимые компоненты](#prerequisites-for-premium-storage) этого раздела.
>
>

Существуют различные рекомендации относительно развертывания SQL Server — как без использования групп доступности AlwaysOn, так и с их использованием. Если вы не используете Always On и иметь существующий изолированный экземпляр SQL Server, вы можете обновить tooPremium хранилища с помощью облачной службы и хранилища учетной записи. Рассмотрим следующие варианты hello.

* **Создать новую виртуальную машину SQL Server**. Вы можете создать новую виртуальную машину сервера SQL Server, использующую учетную запись хранения Premium, согласно описанию в пункте «Новые развертывания». Затем выполните резервное копирование и восстановление конфигурации сервера SQL Server и баз данных пользователя. Hello приложения потребуется обновить toobe tooreference hello нового SQL Server при доступе внутренне или внешне. Вы должны были toocopy всех объектов «за пределы базы данных» как если бы вы занимались миграции (SxS) SQL Server на одном компьютере. Это относится к таким объектам как имена входа, сертификаты и связанные серверы.
* **Миграция существующей виртуальной машины SQL Server**. Для этого потребуется, отключая hello виртуальной Машине SQL Server, а затем передавая его новой облачной службы tooa, которая включает копирование всех его вложенных toohello VHD учетной записи хранения Premium. При hello виртуальная машина переходит в оперативный режим, имя узла сервера hello как перед будет ссылки на приложение hello. Имейте в виду, что влияет на размер hello hello существующий диск hello характеристики производительности. Например 400 ГБ дискового возвращает округленное tooa P20. Если вы знаете, не требуется, производительность диска, может повторно создать виртуальную Машину в качестве виртуальной Машины серии DS hello и подключить виртуальные жесткие диски спецификация размера и производительности hello, требуемую для хранения Premium. Затем можно отсоединить и заново присоединить hello файлы баз данных SQL Server.

> [!NOTE]
> При копирования дисков VHD hello, следует иметь в виду hello размера, в зависимости от размера hello означает тип диска хранилища Premium они подразделяются, определяет спецификации производительности диска. Размер Azure будет округление вверх toohello ближайшего диск, поэтому при наличии 400 ГБ дискового, это будет округляться tooa P20. В зависимости от требований операции ввода-ВЫВОДА существующего объекта hello виртуального жесткого диска операционной системы может не потребоваться toomigrate этот tooa учетной записи хранения Premium.
>
>

Если SQL Server осуществляется извне, hello облачной службы VIP изменится. Вы также будете иметь tooupdate конечных точек, списки управления доступом и DNS параметров.

## <a name="existing-deployments-that-use-always-on-availability-groups"></a>Существующие развернутые службы, использующие группы доступности AlwaysOn
> [!NOTE]
> Для существующих развертываний сначала узнать hello [необходимые компоненты](#prerequisites-for-premium-storage) этого раздела.
>
>

В начале этого раздела мы рассмотрим, как AlwaysOn взаимодействует с сетью Azure. Затем мы произойдет сбой миграции в сценариях tootwo: где которое должно пройти некоторое время простоя миграций и миграций, где необходимо достичь минимальным временем простоя.

Локальные группы доступности AlwaysOn сервера SQL Server используют прослушиватель локально, при этом он регистрирует виртуальное имя DNS и IP-адрес, который разделяется между одним или несколькими серверами SQL. При подключении клиентов они маршрутизируются через hello прослушивателя IP toohello основного сервера SQL Server. Это сервер hello, которому принадлежит hello всегда на IP-ресурс в это время.

![DeploymentsUseAlways On][6]

В Microsoft Azure может иметь tooa только один IP-адрес сетевого Адаптера на hello виртуальной Машины, в заказ tooachieve Здравствуйте же уровень абстракции как локальной, Azure использует hello IP-адрес, назначенный toohello внутренний или внешний подсистемы балансировки нагрузки (ILB/ELB). Hello IP-ресурс, с которым между серверами hello задано toohello же IP-адрес как hello ILB/ELB. Он опубликован в hello DNS и клиентский трафик передается через hello ILB/ELB toohello основной реплику SQL Server. Hello ILB/ELB знает, что SQL Server является первичным, поскольку он использует зонды tooprobe hello всегда на IP-ресурс. В предыдущем примере hello он проверяет каждый узел, содержащий конечную точку ссылается hello ELB/ILB, какое значение отвечает является hello основного сервера SQL Server.

> [!NOTE]
> Hello ILB и ELB оба назначаются tooa определенной Azure облачной службы, поэтому любой миграции в облако в Azure скорее всего повлечет за приветствия, приведет к изменению IP подсистемы балансировки нагрузки.
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a>Миграция развернутых служб AlwaysOn, допускающая некоторое время простоя
Имеются две стратегии toomigrate Always On развертывания, которая позволяет некоторое время простоя:

1. **Добавьте дополнительные tooan вторичных реплик в существующих всегда на кластер**
2. **Перенос tooa новый всегда на кластер**

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a>1. Добавьте дополнительные вторичные реплики tooan существующий всегда на кластер
Одной из стратегий является tooadd toohello дополнительные базы данных-получатели группы доступности AlwaysOn. Требуется tooadd их в новой облачной службы и добавьте прослушиватель hello hello новый нагрузки балансировки IP-адрес.

##### <a name="points-of-downtime"></a>Точки простоя:
* Проверка кластера.
* Тестирование отработки отказа AlwaysOn для новых вторичных реплик.

При использовании пулов хранения Windows в рамках hello виртуальной Машины более высокую пропускную способность ввода-ВЫВОДА, то они будут отключены во время полной проверки кластера. При добавлении кластера узлов toohello, Hello проверочный тест является обязательным. время Hello toorun hello теста может меняться, поэтому следует проверить это в вашей репрезентативной тестовой среды tooget приблизительное время сколько времени это займет.

Когда выполняется переход на другой ресурс вручную и хаоса тестирование hello вновь добавлены функции высокой доступности AlwaysOn tooensure узлы должным образом необходимо выполнить подготовку.

![DeploymentUseAlways On2][7]

> [!NOTE]
> Следует остановить все экземпляры SQL Server, где используются пулы носителей hello перед hello проверка выполняется.
>
> ##### <a name="high-level-steps"></a>Пошаговые действия
>

1. Создайте два новых сервера SQL в новой облачной службе с присоединенным хранилищем Premium.
2. Скопируйте ПОЛНЫЕ резервные копии и восстановите их с помощью **NORECOVERY**.
3. Скопируйте зависимые объекты «не из базы данных пользователя», например имена входа и т. д.
4. Создайте новую внутреннюю подсистему балансировки нагрузки (ILB) или используйте внешнюю подсистему балансировки нагрузки (ELB), а затем настройте конечные точки с балансировкой нагрузки на обоих новых узлах.

   > [!NOTE]
   > Убедитесь, что все узлы имеют hello правильной конфигурации конечной точки, прежде чем продолжить
   >
   >
5. Остановите toohello доступ пользователя или приложения SQL Server (если используются пулы носителей).
6. Остановите службы ядра SQL Server на всех узлах (если используются пулы носителей).
7. Добавить новые узлы toocluster и запустить полную проверку.
8. Если проверка прошла успешно, запустите все службы SQL Server.
9. Выполните резервное копирование журналов транзакций и восстановление баз данных пользователя.
10. Добавление новых узлов в группы доступности AlwaysOn hello и поместите репликации в **синхронной**.
11. Добавить IP-адрес hello адрес ресурса hello новой облачной службы ILB/ELB через PowerShell для AlwaysOn на основании hello несколькими сайтами примера в hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage). В кластерах Windows установите hello **возможных владельцев** из hello **IP-адрес** toohello новые узлы ресурсов старого. Обратитесь к разделу «Добавление ресурса IP-адреса в одной подсети» hello hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
12. Переход на другой ресурс tooone hello новых узлов.
13. Внесите hello новых узлов партнеров автоматического перехода на другой ресурс и тестовые отработки отказа.
14. Удалите исходные узлы из группы доступности.

##### <a name="advantages"></a>Преимущества
* Новые серверы SQL можно проверить (SQL Server и приложений) перед добавлением на tooAlways.
* Можно изменить размер виртуальной Машины hello и настроить hello хранилища tooyour точные требования. Однако было бы полезно tookeep все пути к файлам SQL hello hello таким же.
* Можно управлять начала передачи hello toohello резервные копии БД hello вторичных реплик. Это отличается от использования Azure **AzureStorageBlobCopy начала** toocopy командлетов для виртуальных жестких дисков, так как это асинхронную копию.

##### <a name="disadvantages"></a>Недостатки
* При использовании пулов хранения Windows, происходит во время hello полной проверки кластеров для hello новые дополнительные узлы кластера простой.
* В зависимости от версии SQL Server hello и hello существующих число вторичных реплик, может не быть может tooadd несколько вторичных реплик, не удаляя существующих баз данных-получателей.
* Может быть много времени передачи данных SQL при настройке баз данных-получателей hello.
* В случае параллельной работы новых машин это может повлечь дополнительные расходы при миграции.

#### <a name="2-migrate-tooa-new-always-on-cluster"></a>2. Перенос tooa новый всегда на кластер
Другая стратегия — toocreate совершенно новый всегда на кластере с совершенно новые узлы в новой облачной службы, а затем перенаправления hello клиентов toouse его.

##### <a name="points-of-downtime"></a>Точки простоя
Нет простоев при переносе приложений и пользователей toohello Always On прослушиватель. зависит от времени простоя Hello.

* Hello время toodatabases резервные копии журнала транзакций toorestore на новых серверах.
* Hello время, затраченное tooupdate клиентских приложений toouse Always On прослушиватель.

##### <a name="advantages"></a>Преимущества
* Можно проверить hello реальной производственной среде, SQL Server, и изменения сборки операционной системы.
* У вас есть hello параметр toocustomize hello хранилище и toopotentially уменьшить размер виртуальной Машины. Это может способствовать снижению затрат.
* Во время этого процесса можно обновить сборку или версию SQL Server. Можно также обновить hello операционной системы.
* Здравствуйте, предыдущие всегда на кластер может выступать в качестве целевой сплошной отката.

##### <a name="disadvantages"></a>Недостатки
* Требуется toochange hello DNS-имя прослушивателя hello, если требуются оба кластера Always On, работающими одновременно. Это добавляет администрирования нагрузку во время миграции hello строк клиентского приложения должен содержать hello новое имя прослушивателя.
* Необходимо реализовать механизм синхронизации между двух сред tookeep hello их как закрыть как возможные toominimize hello финальная синхронизация требований перед миграцией.
* Во время миграции будет добавлен затрат, при наличии hello новой среды выполнения.

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a>Миграция развернутых служб AlwaysOn для минимального времени простоя
Существуют две стратегии миграции развернутых служб AlwaysOn для минимального времени простоя:

1. **Использование существующей вторичной реплики: один узел**
2. **Использование существующей вторичной реплики (реплик): несколько узлов**

#### <a name="1-utilize-an-existing-secondary-single-site"></a>1. Использование существующей вторичной реплики: один узел
Стратегия минимальным временем простоя tootake вторичной существующее облако и удалить ее из hello текущего облачной службы. Затем скопируйте hello виртуальные жесткие диски toohello новой Premium учетной записи хранилища и создать hello виртуальной Машины в новой облачной службе hello. Затем обновите прослушивателя hello в кластеризации и переход на другой ресурс.

##### <a name="points-of-downtime"></a>Точки простоя
* Нет времени простоя при обновлении конечной точки с балансировкой нагрузки hello hello конечный узел.
* Повторное подключение вашего клиента может задерживаться в зависимости от конфигурации клиента/DNS.
* Нет дополнительных время простоя при выборе tootake hello всегда на кластере группы вне сети tooswap out hello IP-адресов. Этого можно избежать с помощью или зависимостей и возможных владельцев для hello добавлен ресурс IP-адреса. Обратитесь к разделу «Добавление ресурса IP-адреса в одной подсети» hello hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).

> [!NOTE]
> При необходимости hello toopartake добавленный узел в качестве всегда на переход на другой ресурс партнера необходимо tooadd конечная точка Azure с toohello ссылки, задать нагрузки балансировки. При запуске hello **Add-AzureEndpoint** команды toodo, текущего подключения tooremain открыть, но новый прослушиватель toohello подключения не будет возможности toobe установлено, пока не был обновлен hello подсистемы балансировки нагрузки. При тестировании это замеченный toolast 90-120секунд, это следует проверить.
>
>

##### <a name="advantages"></a>Преимущества
* Дополнительные затраты при миграции не возникают.
* Миграция один к одному.
* Меньший уровень сложности.
* Позволяет увеличить операции ввода-вывода из SKU хранилища Premium. Если hello диски отсоединения от hello виртуальной Машины и скопировать toohello новой облачной службе сторонний средство можно размер виртуального жесткого диска используется tooincrease hello, предоставляющий выше пропускной способности. Для увеличения размера виртуального жесткого диска ознакомьтесь с комментариями на [форуме](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).

##### <a name="disadvantages"></a>Недостатки
* Возникают временные потери в высокой доступности и аварийном восстановлении во время миграции.
* Как это миграции 1:1, будет иметь toouse минимальный размер виртуальной Машины, который будет поддерживать ваш номер виртуальных жестких дисков, не будет возможности toodownsize виртуальных машин.
* Этот сценарий будет использовать hello Azure **AzureStorageBlobCopy начала** командлет, который является асинхронным. Соглашение об уровне обслуживания после завершения копирования отсутствует. время Hello hello копий зависит, тогда это зависит от ожидания в очереди, к которой он также зависит от объема hello tootransfer данных. Hello время копирования увеличивается, если происходит передача hello tooanother центр обработки данных Azure, поддерживающий хранение Premium в другой области. При наличии только 2 узлов, рассмотрите возможности по устранению рисков в случае копирования hello требуется больше времени, чем при тестировании. Сюда могут входить следующие идеи hello.
  * Добавьте временный сторонних узел SQL Server для обеспечения высокой ДОСТУПНОСТИ перед миграцией hello согласованный простоев.
  * Выполните миграцию hello за пределами Azure запланированного обслуживания.
  * Убедиться, что кворум кластера настроен правильно.  

##### <a name="high-level-steps"></a>Пошаговые действия
В этом документе не демонстрирует завершения tooend пример, однако hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) предоставляет сведения, которые можно использовать tooperform это.

![MinimalDowntime][8]

* Конфигурация диска сбора и удалить узел hello (не удаляйте подключенных виртуальных жестких дисков).
* Создайте учетную запись хранения Premium и скопируйте виртуальные жесткие диски из hello Стандартная учетная запись хранения
* Создать новую облачную службу и повторно развернуть hello SQL2 виртуальной Машины в этой облачной службе. Создать hello виртуальной Машины с помощью hello копируется исходный виртуальный жесткий ДИСК операционной системы и присоединение hello копирования виртуальных жестких дисков.
* Настройте ILB/ELB и добавьте конечные точки.
* Обновите прослушиватель одним из следующих способов:
  * Получение группы AlwaysOn hello вне сети и обновление hello всегда в прослушиватель, с новой ILB / ELB IP-адрес.
  * Или добавление hello ресурс IP-адреса из новой облачной службы ILB/ELB через PowerShell в кластеризации Windows. Затем набор hello возможных владельцев ресурса toohello hello IP-адрес узла, SQL2 миграцию и настроить его как или зависимость в hello сетевое имя. Обратитесь к разделу «Добавление ресурса IP-адреса в одной подсети» hello hello [приложение](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
* Проверка DNS-клиенты toohello конфигурации и распространение.
* Перенесите виртуальную машину SQL1 и выполните шаги 2—4.
* При использовании 5ii действия, затем добавьте SQL1 как возможного владельца для hello добавить ресурс IP-адреса
* Проверьте отработку отказа.

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a>2) Использование существующей вторичной реплики (реплик): несколько узлов
При наличии узлов в более одного центра обработки данных Azure (DC), или у вас гибридная среда, можно использовать конфигурации Always On в это время простоя toominimize среды.

Hello подход является toochange hello Always On синхронизации tooSynchronous hello в локальной или дополнительный контроллер домена в Azure, а затем перехода на другой ресурс по toothat SQL Server. Затем скопируйте VHD hello tooa учетной записи хранения Premium и повторного развертывания hello машины в новой облачной службы. Обновите прослушивателя hello и затем восстановить после сбоя.

##### <a name="points-of-downtime"></a>Точки простоя
время простоя Hello состоит из hello время toofailover toohello альтернативой контроллера домена и обратно. Время простоя также зависит от конфигурации клиента/DNS: повторное подключение вашего клиента может задерживаться.
Рассмотрим следующий пример конфигурации AlwaysOn в гибридной hello.

![MultiSite1][9]

##### <a name="advantages"></a>Преимущества
* Можно использовать существующую инфраструктуру.
* У вас есть hello параметр обновления toopre hello хранилища Azure hello DC аварийного восстановления Azure сначала.
* можно перенастроить Hello хранилища Azure для аварийного восстановления контроллера домена.
* Во время миграции выполняются как минимум два перехода на другой ресурс, не считая тестовых переходов.
* Не требуется toomove данных SQL Server с помощью резервного копирования и восстановления.

##### <a name="disadvantages"></a>Недостатки
* В зависимости от tooSQL доступа клиента сервер может возникнуть увеличивают задержку при в приложении toohello альтернативный контроллер домена работает SQL Server.
* может занять длительное время копирования Hello tooPremium хранилища виртуальных жестких дисков. Это может повлиять на решение о ли tookeep hello узел в hello группы доступности. Следует считать это когда журнала вычислительных операций, выполняемых загружает во время миграции hello фактором является обязательным, поскольку hello первичного узла будет иметь tookeep hello нереплицированные транзакции в журнале транзакций. Это может привести к значительному увеличению размера журнала.
* Этот сценарий будет использовать hello Azure **AzureStorageBlobCopy начала** командлет, который является асинхронным. Соглашение об уровне обслуживания после завершения отсутствует. Hello время hello копий зависит, тогда это зависит от ожидания в очереди, он также зависит от объема hello tootransfer данных. Таким образом, достаточно одного узла в 2-й центре обработки данных, в случае, если копия hello требуется больше времени, чем при тестировании необходимо принять меры по устранению рисков. Сюда могут входить следующие идеи hello.
  * Добавьте временный второй узел SQL для обеспечения высокой ДОСТУПНОСТИ перед миграцией hello согласованный простоев.
  * Выполните миграцию hello за пределами Azure запланированного обслуживания.
  * Убедиться, что кворум кластера настроен правильно.

Этот сценарий предполагает документированы установки и знать, как hello хранения сопоставляется в порядке toomake изменения параметров кэша оптимальной диска.

##### <a name="high-level-steps"></a>Пошаговые действия
![Multisite2][10]

* Делает hello локальной / альтернативные hello Azure контроллер домена первичного сервера SQL и сделать его hello других автоматического перехода на другой ресурс партнера (AFP).
* Сбор данных о конфигурации дисков SQL2 и удалить узел hello (не удаляйте подключенных виртуальных жестких дисков).
* Создайте учетную запись хранения Premium и скопируйте виртуальные жесткие диски из hello Стандартная учетная запись хранения.
* Создать новую облачную службу и создайте hello SQL2 ВМ с его дисков хранилища вознаграждения.
* Настройте ILB/ELB и добавьте конечные точки.
* Обновление hello всегда в прослушиватель, с новой ILB / ELB IP адрес и тестирования перехода на другой ресурс.
* Проверьте конфигурацию DNS hello.
* Изменить AFP tooSQL2 hello и перенести SQL1 и выполните шаги 2 – 5.
* Проверьте отработку отказа.
* Перейдите назад tooSQL1 hello AFP и SQL2

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a>Приложение: Миграция tooPremium многосайтового всегда на кластера хранилища
Hello оставшейся части этого раздела предоставляет подробный пример преобразования с несколькими сайтами Always On tooPremium хранения данных кластера. Также преобразует hello прослушивателя с помощью балансировки нагрузки внутренней tooan подсистемы балансировки нагрузки (ILB).

### <a name="environment"></a>Среда
* Windows 2k12 / SQL 2k12
* 1 файл БД на SP 
* 2 x пулы носителей на каждом узле

![Приложение1][11]

### <a name="vm"></a>ВМ:
В этом примере мы будем toodemonstrate переход от tooILB ELB. ELB обладал перед ILB, поэтому в следующем примере показано, как toothis tooswitch во время hello миграции.

![Приложение2][12]

### <a name="pre-steps-connect-toosubscription"></a>Действия по предварительной подключения tooSubscription
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a>Шаг 1. Создайте новую учетную запись хранения и облачную службу
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a>Шаг 2: Увеличьте hello разрешенных ошибок на ресурсы<Optional>
На некоторые ресурсы, принадлежащие tooyour группы доступности AlwaysOn существуют ограничения на количество сбоев, которые могут возникнуть в течение которых служба кластеров hello попытается группы ресурсов toorestart hello. Рекомендуется хотя проходу с этой процедурой, так как при отсутствии вручную отработки отказа перехода на другой ресурс и триггер, завершение работы компьютеров может получить ограничения закрыть toothis увеличить.

Она бы быть hello сбоя оправданным toodouble скидка, toodo это в диспетчере отказоустойчивости кластеров, go toohello свойства hello Always On группы ресурсов:

![Приложение3][13]

Измените hello too6 максимум сбоев.

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a>Шаг 3. Добавление ресурса IP-адреса для группы кластера <Optional>
Если у вас есть только один IP-адрес для hello группы кластера и подсети выровненных toohello облака, учтите, что, если вы случайно перевод в автономный режим все узлы кластера в облаке hello что сети затем hello IP-ресурс кластера и сетевое имя кластера не будет возможности toocome Онлайн. В hello события объекта, это приведет к тому обновляет tooother ресурсы кластера.

#### <a name="step-4-dns-configuration"></a>Шаг 4. Настройка DNS
плавный переход зависит от того, каким образом производится DNS tooimplement загруженные и обновлены.
При установке Always On, он создает группу ресурсов кластера Windows, при открытии диспетчера отказоустойчивости кластеров, вы увидите, как минимум, он будет иметь три ресурса, hello два hello документа относится tooare:

* Имя виртуальной сети (VNN) — это hello DNS-имя, клиент подключения toowhen Желательное tooconnect tooSQL серверах с помощью Always On.
* Ресурс IP-адреса — это IP-адрес, связанный с виртуальной сети hello hello и может иметь несколько в многосайтовой конфигурации будет иметь IP-адрес каждого сайта и подсеть.

При подключении tooSQL Server, драйвер SQL Server Client hello будет извлечь hello записей DNS, связанных с прослушивателем hello и повторите tooconnect tooeach всегда на связанные IP-адрес, ниже обсуждаются некоторые факторы, которые могут повлиять на это.

Hello число параллельных записей DNS, которые связаны с именем прослушивателя hello зависит не только от hello число связанных IP-адреса, но hello "RegisterAllIpProviders'setting в отказоустойчивой кластеризации для hello ресурсов всегда ON имя виртуальной сети.

При развертывании Always On в Azure hello toocreate различных этапов прослушивателя и IP-адресов, у вас есть toomanually Настройка too1 «RegisterAllIpProviders» hello, это разные tooan локального Always On развертывания где оно уже установлено too1.

Если «RegisterAllIpProviders» равно 0, то вы увидите только в DNS запись DNS, связанную с hello прослушиватель:

![Приложение4][14]

Если RegisterAllIpProviders равен 1:

![Приложение5][15]

Приведенный ниже код Hello будет дампа out hello параметры виртуальной сети и установите ее, выполните Примечание для hello изменения tootake эффекта, вам потребуется tootake hello VNN автономный режим и включить его обратно в оперативный режим, этот ведения hello прослушивателя вне сети может вызвать клиент подключения перебоев в работе.

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

На более позднем этапе миграции необходимо будет tooupdate hello Always On прослушиватель с обновление IP-адреса, который будет ссылаться на подсистему балансировки нагрузки, это будет включать в себя удаление IP-адрес ресурса и добавление. После обновления hello IP необходимо tooensure hello новый IP-адрес уже был обновлен в зоне DNS, и что hello клиенты обновляют их локального кэша DNS.

Если клиенты находятся в разных сегментах и ссылаться на другой DNS-сервер, необходимо tooconsider как обстоят дела передачи зоны DNS в ходе миграции hello как hello приложение подключиться будет ограничен времени, по крайней мере hello время передачи зоны все новые IP-адресов для прослушивателя hello. Находясь в рамках здесь ограничения времени, следует обсудить и проверить принудительное Добавочная архивация с помощью команд Windows, а также поместить hello DNS tooa записей узла снизить время tooLive (TTL), чтобы обновлять клиенты hello. Дополнительные сведения см. в статье [Добавочные передачи зоны](https://technet.microsoft.com/library/cc958973.aspx) и [Start-DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).

По умолчанию hello срок ЖИЗНИ для записи DNS, которая связана с hello прослушивателя в Always On в Azure составляет 1200 секунд. Вы можете tooreduce это при работе в рамках ограничения времени во время обновления клиентов миграции tooensure hello их DNS с hello обновить IP-адрес для прослушивателя hello. Можно просматривать и изменить конфигурацию hello записи конфигурации hello объекта hello виртуальной сети:

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

Обратите внимание, нижний hello hello «HostRecordTTL» будет выполняться большего объема трафика DNS.

##### <a name="client-application-settings"></a>Параметры клиентского приложения
Если Здравствуйте, поддерживаемых приложением SQL клиента .net 4.5 SQLClient, то можно использовать "MULTISUBNETFAILOVER = TRUE" ключевое слово, рекомендуется применять, так как она позволяет быстрее tooSQL соединения группы доступности AlwaysOn во время отработки отказа toobe. Перечисление всех IP-адресов, связанных с hello Always On прослушивателя в параллельном режиме и выполняется более интенсивная скорости повтора подключения TCP во время отработки отказа.

Дополнительные сведения о hello параметры, приведенные выше, см. в разделе [MultiSubnetFailover ключевое слово и связанные компоненты](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover). Ознакомьтесь также со статьей [Поддержка SqlClient для высокого уровня доступности и аварийного восстановления](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).

#### <a name="step-5-cluster-quorum-settings"></a>Шаг 5. Параметры кворума кластера
Как будет toobe снятия хотя бы один сервер SQL вниз одновременно, следует изменять приветствия кворума кластера, при 2 узлов с помощью файла общей папке следящего сервера (FSW), следует задать большинство узлов tooallow кворума hello и использовать динамические голосования, и это tooallow для постоянные tooremain один узел.

    Set-ClusterQuorum -NodeMajority  

Дополнительные сведения об управлении и настройке кворума кластера hello см. в разделе [Здравствуйте кворума в отказоустойчивом кластере Windows Server 2012, настройке и управлении](https://technet.microsoft.com/library/jj612870.aspx).

#### <a name="step-6-extract-existing-endpoints-and-acls"></a>Шаг 6. Извлеките существующие конечные точки и списки управления доступом
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

Сохраните эти tooa текстовый файл.

#### <a name="step-7-change-failover-partners-and-replication-modes"></a>Шаг 7. Измените партнеров перехода на другой ресурс и режимы репликации
При наличии более чем 2 серверами SQL можно следует изменить hello отработки отказа другой базы данных-получателя в другой контроллер домена или локальной too'Synchronous и сделать ее автоматического участника отработки отказа (AFP), поэтому поддержания высокого уровня ДОСТУПНОСТИ в процессе внесения изменений. Это можно сделать через TSQL или изменить при помощи SSMS:

![Приложение6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a>Шаг 8. Удалите дополнительную виртуальную машину из облачной службы
Следует планирования toomigrate дополнительного узла облака во-первых, если в данный момент первичной, необходимо запустить отработку отказа вручную.

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a>Шаг 9. Измените параметры кэширования диска в файле CSV и сохраните
Для томов с данными они должны устанавливаться tooREADONLY.

Для тома журнала Отслеживания этих должно быть равно tooNONE.

![Приложение7][17]

#### <a name="step-10-copy-vhds"></a>Шаг 10. Скопируйте виртуальные жесткие диски
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



Можно проверить состояние копирования hello toohello VHD hello учетной записи хранения Premium:

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Приложение8][18]

Подождите, пока все они будут успешно сохранены.

Информация об отдельных больших двоичных объектах.

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a>Шаг 11. Зарегистрируйте диск ОС
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a>Шаг 12. Импортируйте вторичную реплику в новую облачную службу
Hello кода ниже также использует hello добавлен параметр здесь вы можете импортировать машины hello и использовать hello retainable виртуальных IP-адресов.

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a>Шаг 13. Создайте ILB в новой облачной службе, добавьте конечные точки с балансировкой нагрузки и списки управления доступом
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a>Шаг 14. Обновите AlwaysOn
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Приложение9][19]

Теперь можно Удалите старые облачную службу hello IP-адрес.

![Приложение10][20]

#### <a name="step-15-dns-update-check"></a>Шаг 15. Проверка обновлений DNS
Теперь необходимо проверить DNS-серверов в сети клиента SQL Server и убедитесь, что кластеризации добавил hello запись дополнительный узел для hello добавить IP-адрес. Если эти DNS-серверы не обновлялись, можно воспользоваться режимом вынужденного передачи зоны DNS и убедитесь, что hello клиентов в подсети отсутствует, может tooresolve tooboth всегда на IP-адреса, поэтому нет необходимости toowait для автоматической репликации DNS.

#### <a name="step-16-reconfigure-always-on"></a>Шаг 16. Перенастройте AlwaysOn 
На этом этапе дождитесь hello получателей, этот узел, который был перенесенных toofully повторную синхронизацию с локальным узлом hello и переключение toosynchronous узел репликации и сделать его hello AFP.  

#### <a name="step-17-migrate-second-node"></a>Шаг 17. Перенесите второй узел
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a>Шаг 18. Измените параметры кэширования диска в файле CSV и сохраните
Для томов с данными они должны устанавливаться tooREADONLY.

Для тома журнала Отслеживания этих должно быть равно tooNONE.

![Приложение11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a>Шаг 19. Создайте новую независимую учетную запись хранения для дополнительного узла
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a>Шаг 20. Скопируйте виртуальные жесткие диски
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


Можно проверить состояние копирования hello виртуального жесткого диска для всех виртуальных жестких дисков: ForEach ($disk в $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. DiskLabel $diskName = $disk. DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Приложение12][22]

Подождите, пока все они будут успешно сохранены.

Информация об отдельных больших двоичных объектах.

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a>Шаг 21. Зарегистрируйте диск ОС
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a>Шаг 22. Добавьте конечные точки с балансировкой нагрузки и списки управления доступом
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a>Шаг 23. Проверьте отработку отказа
Теперь должен сообщить hello перенесенных узел синхронизации с локальным hello всегда на узел, поместите его в режиме репликации toosynchronous и подождите, пока он не будет синхронизирована. Затем отработку отказа из локальной toohello первый узел миграция, который является hello AFP. После, работал, изменение hello последнего переноса AFP toohello узла.

Следует тестовые отработки отказа между всеми узлами и запустить на то, что ожидается хаоса тесты, которые tooensure переход на другой ресурс может использоваться в качестве и своевременно манор.

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a>Шаг 24. Верните исходные параметры кворума кластера, DNS TTL, параметры перехода на другой ресурс и параметры синхронизации
##### <a name="adding-ip-address-resource-on-same-subnet"></a>Добавление ресурса IP-адреса в одной подсети
Если только двух серверов SQL Server и хотите toomigrate их новых tooa облачной службы, но, чтобы tookeep их на Здравствуйте одной подсети, можно избежать создания прослушивателя hello автономного toodelete всегда hello исходный IP-адрес и добавить новый IP-адрес hello. Если вы переносите hello виртуальные машины tooanother подсети, он не потребуется toodo как сеть дополнительных кластера, которая будет ссылаться в этой подсети.

После возможно восстановление hello миграции получателя и были добавлены в hello новый ресурс IP-адрес для новой облачной службе hello до перехода на другой ресурс hello существующий первичный, следует выполните следующие действия в пределах hello Диспетчер отказоустойчивости кластеров:

tooadd IP-адрес в разделе hello [приложение](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), шаг 14.

1. Hello текущий ресурс IP-адреса, измените too'Existing возможного владельца hello основного сервера SQL Server ", в примере hello ниже «dansqlams4»:

    ![Приложение13][23]
2. Hello новый ресурс IP-адреса, измените too'Migrated hello возможного владельца сервера-получателя SQL ", в примере hello ниже «dansqlams5»:

    ![Приложение14][24]
3. После этого вы можете отработки отказа, когда последний узел hello переносится hello возможных владельцев следует изменять, этот узел добавляется в качестве возможного владельца:

    ![Приложение15][25]

## <a name="additional-resources"></a>Дополнительные ресурсы
* [Хранилище Azure Premium](../../../storage/common/storage-premium-storage.md)
* [Виртуальные машины](https://azure.microsoft.com/services/virtual-machines/)
* [SQL Server в виртуальных машинах Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png
