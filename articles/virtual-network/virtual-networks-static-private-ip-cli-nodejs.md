---
title: "aaaConfigure частных IP-адресов для виртуальных машин - Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов для виртуальных машин с помощью hello Azure командной строки (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a>Настройка частного IP-адреса для виртуальной машины с помощью hello Azure CLI 1.0


## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI 

Можно выполнить с помощью одного из следующих версий CLI hello задачу hello. 

- [Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -CLI нашей поколения для модели развертывания управления hello ресурсов 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello модели развертывания диспетчера ресурсов. Вы также можете [управление статический частный IP-адрес в hello классической модели развертывания](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан. Если требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, описанные в [создании виртуальной сети](virtual-networks-create-vnet-arm-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Как toospecify статических частных IP-адресов при создании виртуальной Машины
toocreate Виртуальную машину с именем *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet* с статических частного IP-адреса *192.168.1.101*, выполните следующие действия hello.

1. Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.
2. Запустите hello **azure конфигурации режима** tooswitch tooResource Manager режим команд, как показано ниже.
   
        azure config mode arm
   
    Ожидаемые выходные данные:
   
        info:    New mode is arm
3. Запустите hello **создать сеть azure public-ip** toocreate общедоступный IP-адрес для hello виртуальной Машины. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    Ожидаемые выходные данные:
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * **-g (или --resource-group)**. Имя hello ресурсов группы hello общедоступный IP-адрес будет создаваться в.
   * **-n (или --name)**. Имя hello общедоступный IP-адрес.
   * **-l (или --location)**. Регион Azure, где будут создаваться hello общедоступный IP-адрес. В данном случае это — *centralus*.
4. Запуска hello **сетевого адаптера сети azure создать** команда toocreate сетевой Адаптер с статический частных IP-адрес. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    Ожидаемые выходные данные:
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * **-a (или --private-ip-address)**. Статический частный IP-адрес для hello сетевого адаптера.
   * **-m (или --subnet-vnet-name)**. Имя виртуальной сети, где будут создаваться hello Сетевых hello.
   * **-k (или --subnet-name)**. Имя подсети hello, где будут создаваться hello сетевого Адаптера.
5. Запустите hello **создания виртуальной машины azure** команда toocreate hello созданную виртуальную Машину с помощью hello общедоступного IP-адреса и сетевого Адаптера. Список Hello отображаться после вывода hello объясняется hello параметров, используемых.
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    Ожидаемые выходные данные:
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * **-y (или --os-type)**. Тип операционной системы для виртуальной Машины, hello либо *Windows* или *Linux*.
   * **-f (или --nic-name)**. Имя hello hello сетевого Адаптера виртуальной Машины будет использовать.
   * **-i (или --public-ip-name)**. Имя hello открытый IP hello виртуальная машина будет использовать.
   * **-F (или --vnet-name)**. Имя виртуальной сети, где будут создаваться hello ВМ hello.
   * **-j (или --vnet-subnet-name)**. Имя подсети hello, где будут создаваться hello виртуальной Машины.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Как статических частных IP-tooretrieve адресов сведения для виртуальной Машины
tooview hello статических частного IP-адреса сведения для hello создания ВМ с hello-сценарий, приведенный выше, запустите следующую команду Azure CLI hello и просмотрите значения hello для *метод alloc частный IP-адрес* и *частный IP-адрес*:

    azure vm show -g TestRG -n DNS01

Ожидаемые выходные данные:

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Как tooremove статических частных IP-адресов из виртуальной Машины
Статический частный IP-адрес нельзя удалить из сетевой карты с использованием Azure CLI для диспетчера ресурсов. Необходимо создать новый сетевой Адаптер, использующий динамических IP-адресов, удалите hello предыдущих сетевой Адаптер из виртуальной Машины hello, а затем добавьте новый hello toohello сетевого Адаптера виртуальной Машины. toochange hello сетевого Адаптера для hello виртуальной Машины используется int eh выше команды, выполните следующие шаги hello.

1. Запустите hello **сетевого адаптера сети azure создать** команды toocreate новый сетевой Адаптер, с помощью динамического выделения IP-адресов. Обратите внимание на то, каким образом не требуется toospecify hello IP-адрес этого времени.
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. Запустите hello **набор виртуальных машин azure** команда toochange hello сетевой Адаптер, используемый hello виртуальной Машины.
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    Ожидаемые выходные данные:
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. Если было, запустите hello **удалить сетевого адаптера сети azure** команды toodelete, старый hello сетевого адаптера.
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    Ожидаемые выходные данные:
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Как tooadd статический частных IP-адрес решения tooan существующей виртуальной Машины
tooadd статические частного IP адрес toohello сетевой Адаптер, используемый виртуальной машиной, созданной выше сценария hello выполните hello следующую команду:

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

Ожидаемые выходные данные:

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .
* Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).

