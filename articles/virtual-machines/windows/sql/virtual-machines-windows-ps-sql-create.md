---
title: "aaaCreate виртуальной машины с SQL Server в Azure PowerShell (диспетчера ресурсов) | Документы Microsoft"
description: "Содержит описание действий и сценарии PowerShell для создания виртуальной машины Azure на основе образа из коллекции образов виртуальных машин SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Подготовка виртуальной машины SQL Server к работе с помощью Azure PowerShell (в Resource Manager)
> [!div class="op_single_selector"]
> * [Портал](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Обзор
В этом учебнике показано, как hello в одной виртуальной машине Azure с помощью toocreate **диспетчера ресурсов Azure** развертывания модели с помощью командлетов Azure PowerShell. В этом учебнике мы создадим одной виртуальной машины с помощью одного диска из образа в коллекции SQL hello. Мы создадим новые поставщики для hello хранилища, сети и вычислительных ресурсов, которые будут использоваться виртуальной машиной hello. Вы можете использовать существующие поставщики для любых из этих ресурсов.

Если требуется hello базовую версию этого раздела, см. раздел [подготовки виртуальной машины SQL Server с помощью Azure PowerShell Classic](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Предварительные требования
Для работы с этим руководством вам потребуется:

* Учетная запись Azure и подписка (еще до начала). Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](https://azure.microsoft.com/pricing/free-trial/).
* [Azure PowerShell](/powershell/azure/overview)1.4.0 или более поздней версии (в этом учебнике использовалась версия 1.5.0).
  * tooretrieve версию, тип **Azure Get-Module - ListAvailable**.

## <a name="configure-your-subscription"></a>Настройка подписки
Откройте Windows PowerShell и установить tooyour доступа учетной записи Azure, выполнив следующий командлет hello. Откроется экран tooenter имя входа учетные данные. Используйте hello же электронной почты и пароль, использовать toosign в toohello портал Azure.

    Add-AzureRmAccount

После успешного входа в некоторые сведения можно просмотреть на экране, которая включает в себя SubscriptionId hello, с которой вы выполнили вход. Это hello подписки, в которой hello ресурсы в этом учебнике будет создан, если вы не изменили tooa другую подписку. При наличии нескольких SubscriptionIds, выполните следующий командлет tooreturn hello список всех вашей SubscriptionIds:

    Get-AzureRmSubscription

tooanother toochange SubscriptionID, запустите следующий командлет с вашей требуемой SubscriptionId hello.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Определение переменных образа
toosimplify удобство использования и понимание hello выполнить сценарий из этого учебника, начнем, определив несколько переменных. Изменить значения параметров hello, при необходимости, но Учтите, что именования ограничения связанные tooname длины и специальные символы при изменении значений hello.

### <a name="location-and-resource-group"></a>Расположение и группа ресурсов
Используйте две переменные toodefine hello данных региона и hello группа ресурсов, в который будут созданы другие ресурсы для виртуальной машины hello hello.

При желании изменить, а затем выполните следующие командлеты tooinitialize hello эти переменные.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Свойства хранилища
Используйте следующие переменные toodefine hello учетной записи и hello тип хранения для toobe хранилища, используемый виртуальной машиной hello hello.

При желании изменить, а затем выполните следующий командлет tooinitialize hello эти переменные. Обратите внимание, что в этом примере используется [хранилище уровня "Премиум"](../../../storage/common/storage-premium-storage.md), которое рекомендуется для рабочих нагрузок в рабочей среде. Дополнительные сведения об этом руководстве, а также другие рекомендации см. в статье [Рекомендации по оптимизации производительности SQL Server в виртуальных машинах Azure](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Свойства сети
Используйте следующие переменные toodefine hello сетевого интерфейса, способ распределения hello TCP/IP, hello виртуальной сети имя, hello виртуальной подсети, hello диапазон IP-адресов для виртуальной сети hello, hello диапазон IP-адресов для подсети hello и hello hello toobe имя метки общедоступные сети hello hello виртуальной машине.

При желании изменить, а затем выполните следующий командлет tooinitialize hello эти переменные.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Свойства виртуальной машины
Используйте следующие имя виртуальной машины hello toodefine переменные, имя компьютера hello, размер виртуальной машины hello и hello имя диска операционной системы для виртуальной машины hello hello.

При желании изменить, а затем выполните следующий командлет tooinitialize hello эти переменные.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Свойства образа
Используйте следующие переменные toodefine hello изображения toouse для виртуальной машины hello hello. В этом примере используется образ SQL Server 2016 Enterprise hello.

При желании изменить, а затем выполните следующий командлет tooinitialize hello эти переменные.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Обратите внимание, что можно получить полный список предложений образа SQL Server с помощью команды Get-AzureRmVMImageOffer hello.

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

И вы увидите hello номера SKU для предложения с помощью команды Get-AzureRmVMImageSku hello. Hello следующая команда показывает все номера SKU для hello **SQL2014SP1 WS2012R2** предлагают.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Создание группы ресурсов
С помощью модели развертывания диспетчера ресурсов hello hello первый объект, который вы создаете — hello группы ресурсов. Мы будем использовать hello [New AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate командлет группе ресурсов Azure и его ресурсы с ресурсом hello группы имя и расположение определяется hello переменные, которые ранее инициализирован.

Выполните следующий командлет toocreate hello новой группы ресурсов.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Создайте учетную запись хранения.
Hello виртуальной машине требуется ресурсы хранения для диска операционной системы hello и hello данных SQL Server и файлов журнала. Для упрощения мы создадим один диск для всех ресурсов. Можно подключить дополнительные диски, позднее с помощью hello [диска Azure добавить](/powershell/module/azure/add-azuredisk) командлета в порядок tooplace данных SQL Server и файлы журнала на выделенные диски. Мы будем использовать hello [New AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) toocreate командлет стандартное хранилище учетную запись в новой группы ресурсов и hello имя учетной записи хранения, имя Sku хранения и места, определенного с помощью переменных hello, которую ранее инициализирован.

Выполните следующий командлет toocreate hello учетной записи хранения.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Создание сетевых ресурсов
Hello виртуальной машины необходимо указать число сетевых ресурсов для подключения к сети.

* Каждой виртуальной машине требуется виртуальная сеть.
* Для виртуальной сети следует определить по крайней мере одну подсеть.
* Для сетевого интерфейса следует определить общедоступный или частный IP-адрес.

### <a name="create-a-virtual-network-subnet-configuration"></a>Создание конфигурации подсети в виртуальной сети
Сначала мы создадим конфигурацию подсети для нашей виртуальной сети. В этом руководстве мы создадим подсеть по умолчанию с помощью hello [New AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) командлета. Мы создадим нашей конфигурации подсети виртуальной сети с hello подсети имя и адрес префикс, определенный с помощью hello переменные, которые ранее инициализирован.

> [!NOTE]
> Можно определить дополнительные свойства конфигурации подсети виртуальной сети hello, с помощью этого командлета, но они выходят за рамки данного учебника hello.
>
>

Выполните следующий командлет toocreate hello конфигурацию виртуальной подсети.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Создать виртуальную сеть
После этого мы создадим нашей виртуальной сети, с помощью hello [New AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) командлета. Мы создадим нашей виртуальной сети в новую группу ресурсов, с именем hello, расположение и адрес префикс, определенный с использованием hello переменные, которые ранее инициализирован и конфигурация hello подсети, определенные в предыдущем шаге hello.

Выполните следующий командлет toocreate hello виртуальной сети.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Создать общедоступный IP-адрес hello
Теперь, когда у нас есть определенные виртуальной сети, нужно tooconfigure IP-адрес для подключения к toohello виртуальной машины. В этом учебнике мы создадим общедоступный IP-адрес, с помощью динамических IP-адресов, адресация toosupport подключение к Интернету. Мы будем использовать hello [New AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) командлет toocreate hello общедоступный IP-адрес в prevously Создание группы ресурсов hello и с именем hello, расположение, способ распределения и определяются с помощью hello метка DNS-имени домена переменные, которые ранее инициализирован.

> [!NOTE]
> Можно определить дополнительные свойства hello общедоступный IP-адрес с помощью этого командлета, но это вне области hello начальной учебника. Можно также создать частный адрес или адрес со статическим адресом, но также они выходят за рамки данного учебника hello.
>
>

Выполните следующий командлет toocreate hello открытый IP-адреса.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Создание сетевого интерфейса hello
Мы стали готовы toocreate hello сетевого интерфейса, который будет использовать наши виртуальной машины. Мы будем использовать hello [New AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) ранее определенные командлет toocreate нашей сетевого интерфейса в группе ресурсов hello, созданного ранее и с hello, местоположение, подсеть и общедоступный IP-адрес.

Выполните следующий командлет toocreate hello сетевого интерфейса.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Настройка объекта виртуальной машины
Теперь, когда у нас есть ресурсы хранилища и сети, определенные, не готов toodefine вычислительных ресурсов для виртуальной машины hello. В этом руководстве мы hello размер виртуальной машины, а также различные свойства операционной системы, укажите hello сетевого интерфейса, который мы создали ранее, определить хранилище больших двоичных объектов и укажите hello диска операционной системы.

### <a name="create-hello-vm-object"></a>Создание hello объекта виртуальной Машины
Начнем с указанием размера виртуальной машины hello. В этом руководстве мы указываем DS13. Мы будем использовать hello [New AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) toocreate командлет объект можно настроить виртуальную машину с именем hello и размер, определенный с помощью hello переменные, которые ранее инициализирован.

Выполните следующий объект виртуальной машины hello toocreate командлета hello.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>Создайте учетные данные объекта toohold hello имя и пароль для учетной записи локального администратора hello
Прежде чем мы можно задать свойства hello операционной системы для виртуальной машины hello, нужны toosupply hello учетные данные для учетной записи локального администратора hello виде защищенной строки. tooaccomplish это, мы будем использовать hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) командлета.

Выполните следующий командлет hello и в окне запроса учетных данных Windows PowerShell hello введите hello toouse имя и пароль для учетной записи локального администратора hello в виртуальной машине Windows hello.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Задать свойства hello операционной системы для виртуальной машины hello
Теперь мы все свойства операционной системы готов tooset hello виртуальной машины. Мы будем использовать hello [набор AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) командлет tooset hello тип операционной системы Windows, требует hello [агент виртуальной машины](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe установлен, укажите, что hello включает автоматически обновление и задайте имя виртуальной машины hello, имя компьютера hello и hello учетные данные, используя hello переменные, которые ранее инициализирован.

Выполнение hello следующие свойства командлет tooset hello операционной системы для виртуальной машины.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Добавление hello сетевой интерфейс toohello виртуальной машины
Далее мы добавим hello сетевого интерфейса, созданного ранее toohello виртуальной машины. Мы будем использовать hello [AzureRmVMNetworkInterface добавить](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) командлет tooadd hello сетевого интерфейса с помощью hello переменной сетевого интерфейса, определенного ранее.

Выполнение hello, выполнив командлет tooset hello сетевого интерфейса для виртуальной машины.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Задать место хранения большого двоичного объекта hello hello toobe диск, используемый виртуальной машиной hello
Затем мы определим место хранения большого двоичного объекта hello hello toobe диск, используемый виртуальной машиной hello hello переменных, определенных вами ранее.

Выполните следующие места хранения больших двоичных объектов hello tooset командлет hello.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Задайте свойства диска для виртуальной машины hello hello операционной системы
Далее мы установим hello операционной системы свойства диска для виртуальной машины hello. Мы будем использовать hello [AzureRmVMOSDisk набор](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify командлета, hello операционной системы для виртуальной машины hello поступит из образа, кэширование только tooread tooset (так как SQL Server устанавливается на hello общий диск) и определения имя виртуальной машины Hello и диск операционной системы hello, определяются с помощью hello переменные, которые было определено ранее.

Выполнение hello следующие свойства командлет tooset hello операционной системы диска для виртуальной машины.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Укажите образ платформы hello для hello виртуальной машины
Наш последний шаг настройки — образ платформы hello toospecify для нашей виртуальной машины. В этом руководстве мы используем hello последний образ SQL Server 2016 CTP. Мы будем использовать hello [AzureRmVMSourceImage набор](/powershell/module/azurerm.compute/set-azurermvmsourceimage) toouse командлет этот образ в соответствии с определением hello переменных, определенных вами ранее.

Выполнение hello, выполнив командлет образа платформы hello toospecify для виртуальной машины.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Создать виртуальную Машину SQL hello
Теперь, после завершения действия по настройке hello, все готово toocreate hello виртуальной машины. Мы будем использовать hello [New AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) командлет toocreate hello виртуальной машины с помощью hello переменные, которые мы определили.

Выполните следующий командлет toocreate hello виртуальной машины.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

создается виртуальная машина Hello. Обратите внимание, что стандартная учетная запись хранения создается для Диагностика загрузки поскольку hello указана учетная запись хранения для диска виртуальной машины hello — учетная запись хранения premium.

Этот компьютер теперь можно просмотреть в toosee портала Azure hello [его общедоступный IP-адрес и его полное доменное имя](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Пример сценария
Hello следующий скрипт содержит hello полный скрипт PowerShell для этого учебника. Он предполагает, что уже toouse подписки Azure приветствия программы установки с hello **добавить AzureRmAccount** и **AzureRmSubscription выберите** команд.

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>Дальнейшие действия
После создания виртуальной машины hello их готовности tooconnect toohello виртуальной машины с помощью подключения удаленного рабочего СТОЛА и установки. Дополнительные сведения см. в разделе [подключения виртуальной машины SQL Server в Azure (диспетчера ресурсов) tooa](virtual-machines-windows-sql-connect.md).

