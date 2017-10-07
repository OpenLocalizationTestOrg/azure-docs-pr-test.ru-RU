---
title: "aaaMultiple IP-адресов для виртуальных машин Azure — PowerShell | Документы Microsoft"
description: "Узнайте, как tooassign несколько IP-адресов tooa виртуальной машины с помощью PowerShell | Диспетчер ресурсов."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>Назначение нескольких IP-адресов toovirtual машин с помощью PowerShell

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

В этой статье объясняется, как toocreate виртуальной машины (VM) с помощью развертывания диспетчера ресурсов Azure hello модели с помощью PowerShell. Несколько IP-адресов нельзя назначить tooresources, созданные с помощью hello классической модели развертывания. Дополнительные сведения о моделях развертывания Azure, чтение hello toolearn [понять модели развертывания](../resource-manager-deployment-model.md) статьи.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Создание виртуальной машины с несколькими IP-адресами

Привет, описанных ниже объясняется, как toocreate пример виртуальной Машины с несколькими IP-адресов, как описано в сценарии hello. Измените имена переменных в соответствии с требованиями своей реализации.

1. Откройте окно командной строки PowerShell и завершения hello, оставшиеся шаги в этом разделе в одном сеансе PowerShell. Если у вас еще нет PowerShell устанавливается и настраивается, hello завершения шагов в hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.
2. Учетная запись входа tooyour с hello `login-azurermaccount` команды.
3. Замените *myResourceGroup* и *westus* именем и расположением по своему выбору. Создайте группу ресурсов. Группа ресурсов — это логический контейнер, в котором происходит развертывание ресурсов Azure и управление ими.

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. Создание виртуальной сети (VNet) и подсети в hello местоположения hello группа ресурсов:

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. Создайте группу безопасности сети (NSG) и правило. Hello NSG защищает hello виртуальной Машины с помощью правила входящего и исходящего трафика. В нашем случае создается правило для входящего трафика порта 3389, которое разрешает входящие подключения к удаленному рабочему столу.

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. Определение hello основной IP-конфигурации для hello сетевого адаптера. Изменение 10.0.0.4 tooa допустимый адрес в подсети hello, вы создали, если вы не использовали ранее определенное значение hello. Прежде чем назначать статический IP-адрес, рекомендуем сначала убедиться, что он не используется. Введите команду hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`. Если доступен адрес hello, hello выходные возвращает *True*. Если он недоступен, hello выходные возвращает *False* и список доступных адресов. 

    В следующие команды, hello **замените hello уникальное DNS имя toouse < замены с your уникальный name >.** Hello имя должно быть уникальным для общих IP-адресов внутри области Azure. Данный параметр является необязательным. Его можно удалить, если требуется только tooconnect toohello виртуальной Машины с помощью hello общедоступный IP-адрес.

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    При назначении нескольких tooa конфигурации IP сетевого Адаптера, один конфигурации должны быть назначены как hello *-основной*.

    > [!NOTE]
    > За общедоступные IP-адреса взимается номинальная плата. Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы. Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке. Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.

7. Определение hello дополнительный IP-конфигурации для hello сетевого адаптера. Конфигурации можно добавлять и удалять по мере необходимости. Каждой конфигурации IP должен быть назначен частный IP-адрес. Каждой конфигурации может быть назначен один необязательный общедоступный IP-адрес.

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. Создайте hello сетевой Адаптер и связать hello три IP конфигурации tooit:

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >Хотя все конфигурации будут назначены tooone сетевого Адаптера в этой статье, можно назначить сетевого Адаптера, подключенного tooevery toohello виртуальной Машины для нескольких IP конфигурации. как считывать toocreate виртуальной Машины с несколькими сетевыми картами toolearn hello [создания виртуальной Машины с несколькими сетевыми адаптерами](virtual-network-deploy-multinic-arm-ps.md) статьи.

9. Создайте hello виртуальной Машины, введя hello, следующие команды:

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. Добавить hello частного IP адресов toohello ВМ операционной системы, выполнив шаги hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи. Не добавляйте hello открытый IP адресов toohello операционной системы.

## <a name="add"></a>Добавьте IP адресов tooa виртуальной Машины

Можно добавить открытые и закрытые tooa адресов IP сетевого Адаптера, выполнив hello, описанных ниже. Hello примеры в следующих разделах hello предполагается, что вы уже виртуальной Машины с hello трех IP-конфигурации, описанной в hello [сценарий](#Scenario) в этой статье, но он не обязательно должен выполнить.

1. Откройте окно командной строки PowerShell и завершения hello, оставшиеся шаги в этом разделе в одном сеансе PowerShell. Если у вас еще нет PowerShell устанавливается и настраивается, hello завершения шагов в hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) статьи.
2. Изменить hello «значения» hello, следуя имя toohello $Variables hello сетевого Адаптера необходимо tooadd IP адрес tooand hello ресурсов группы и размещения hello сетевой Адаптер существует в:

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    Если вы не знаете имя hello hello требуется toochange сетевого Адаптера, введите следующие команды hello, а затем измените значения hello hello предыдущие переменные:

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. Создайте переменную и присвойте ему toohello существующего сетевого Адаптера, введя следующую команду hello:

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. В hello, следующие команды, измените *MyVNet* и *MySubnet* toohello имена hello виртуальной сети и подсети hello, подключен сетевой Адаптер. Введите hello команды tooretrieve hello виртуальной сети и подсети объектов hello подключения сетевого Адаптера:

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    Если вы не знаете hello виртуальную сеть или подсеть имя приветствия подключен сетевой Адаптер, введите следующую команду hello:
    ```powershell
    $MyNIC.IpConfigurations
    ```
    В выходных данных hello найдите toohello аналогичный текст, следующий пример выходных данных:
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    В данном выходе *MyVnet* — hello виртуальной сети и *MySubnet* — сетевой Адаптер подключен к hello подсети hello.

5. Выполните действия hello в одном из следующих разделах, в зависимости от требований hello.

    **Добавление частного IP-адреса**

    tooadd закрытый tooa адрес IP сетевого Адаптера, необходимо создать IP-адрес. Hello следующая команда создает конфигурации со статическим IP-адресом 10.0.0.7. При задании статического IP-адреса, он должен быть неиспользуемый адрес для подсети hello. Рекомендуется сначала протестировать tooensure адрес hello, она доступна, введя hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` команды. Если IP-адрес hello, hello output возвращает *True*. Если он недоступен, hello выходные возвращает *False*и список доступных адресов.

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    Вы можете создать любое количество конфигураций, указывая для них уникальные имена и уникальные частные IP-адреса (если используются статические IP-адреса).

    Добавьте hello частного IP адрес toohello операционной системы ВМ, выполнив действия hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи.

    **Добавление общедоступного IP-адреса**

    Общедоступный IP-адрес будет добавлен, связав общих ресурсов tooeither IP-адрес новой конфигурации IP или существующей конфигурации IP. Этапы hello в одном hello следующих разделах, сколько требуется.

    > [!NOTE]
    > За общедоступные IP-адреса взимается номинальная плата. Дополнительные сведения о IP-адресов цен, toolearn чтения hello [цены IP адрес](https://azure.microsoft.com/pricing/details/ip-addresses) страницы. Нет toohello предельное число общих IP-адресов, которые могут использоваться в подписке. Дополнительные об ограничениях hello, чтение hello toolearn [Azure ограничивает](../azure-subscription-service-limits.md#networking-limits) статьи.
    >

    - **Связать hello открытый конфигурацию IP-адреса ресурса tooa новый IP**
    
        Чтобы добавить общедоступный IP-адрес в новую IP-конфигурацию, необходимо добавить и частный IP-адрес, так как все IP-конфигурации должны иметь частный IP-адрес. В конфигурацию можно добавить имеющийся ресурс общедоступного IP-адреса или создать новый. toocreate новый, введите следующую команду hello:
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        toocreate новой конфигурации IP с статический частный IP-адрес и связанные hello *myPublicIp3* общедоступный IP-адрес адрес ресурса, введите следующую команду hello:

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **Связать hello открытый конфигурацию IP-адреса ресурса tooan существующие IP**

        Открытый ресурс IP-адреса можно только связанные tooan IP-конфигурации, уже не связан. Можно определить, имеет ли связанный общий IP-адрес IP-адрес, введя следующую команду hello.

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        Вы видите аналогичные toohello следующие выходные данные:

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        С момента hello **PublicIpAddress** столбца для *IpConfig 3* является пустым, не открытого ресурса IP-адреса является в настоящее время связаны tooit. Можно добавить существующие открытый IP адрес ресурса tooIpConfig-3, или введите hello, следующая команда toocreate один:

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        Введите следующую команду, общедоступный IP-адрес tooassociate hello адресов toohello существующие IP конфигурации ресурса с именем hello *IpConfig 3*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. Задайте hello Сетевых hello новой конфигурации IP, указав hello следующую команду:

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. Просмотр hello частных IP-адресов и hello открытый IP адрес ресурсы назначенного toohello hello сетевого Адаптера, введя следующую команду:

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. Добавьте hello частного IP адрес toohello операционной системы ВМ, выполнив действия hello для вашей операционной системы в hello [добавить IP-адресов операционной системы виртуальной Машины tooa](#os-config) этой статьи. Не добавляйте hello открытый IP адрес toohello операционной системы.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
