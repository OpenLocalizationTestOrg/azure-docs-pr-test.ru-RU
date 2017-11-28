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
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a><span data-ttu-id="91630-103">Настройка частного IP-адреса для виртуальной машины с помощью hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="91630-103">Configure private IP addresses for a virtual machine using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="91630-104">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="91630-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="91630-105">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="91630-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="91630-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="91630-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="91630-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -CLI нашей поколения для модели развертывания управления hello ресурсов</span><span class="sxs-lookup"><span data-stu-id="91630-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="91630-108">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="91630-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="91630-109">Вы также можете [управление статический частный IP-адрес в hello классической модели развертывания](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="91630-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="91630-110">приведенную ниже команду Azure CLI Образец Hello ожидать простой среде уже создан.</span><span class="sxs-lookup"><span data-stu-id="91630-110">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="91630-111">Если требуется toorun hello команд, отображаемых в этом документе, вначале построить hello тестовой среды, описанные в [создании виртуальной сети](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="91630-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="91630-112">Как toospecify статических частных IP-адресов при создании виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="91630-112">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="91630-113">toocreate Виртуальную машину с именем *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet* с статических частного IP-адреса *192.168.1.101*, выполните следующие действия hello.</span><span class="sxs-lookup"><span data-stu-id="91630-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="91630-114">Если ранее не пользовались Azure CLI, см. раздел [Установка и настройка hello Azure CLI](../cli-install-nodejs.md) и следуйте инструкциям hello toohello точку, где выбирается учетная запись Azure и подписки.</span><span class="sxs-lookup"><span data-stu-id="91630-114">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="91630-115">Запустите hello **azure конфигурации режима** tooswitch tooResource Manager режим команд, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="91630-115">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="91630-116">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91630-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="91630-117">Запустите hello **создать сеть azure public-ip** toocreate общедоступный IP-адрес для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="91630-117">Run hello **azure network public-ip create** toocreate a public IP for hello VM.</span></span> <span data-ttu-id="91630-118">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="91630-118">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="91630-119">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91630-119">Expected output:</span></span>
   
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
   
   * <span data-ttu-id="91630-120">**-g (или --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="91630-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="91630-121">Имя hello ресурсов группы hello общедоступный IP-адрес будет создаваться в.</span><span class="sxs-lookup"><span data-stu-id="91630-121">Name of hello resource group hello public IP will be created in.</span></span>
   * <span data-ttu-id="91630-122">**-n (или --name)**.</span><span class="sxs-lookup"><span data-stu-id="91630-122">**-n (or --name)**.</span></span> <span data-ttu-id="91630-123">Имя hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="91630-123">Name of hello public IP.</span></span>
   * <span data-ttu-id="91630-124">**-l (или --location)**.</span><span class="sxs-lookup"><span data-stu-id="91630-124">**-l (or --location)**.</span></span> <span data-ttu-id="91630-125">Регион Azure, где будут создаваться hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="91630-125">Azure region where hello public IP will be created.</span></span> <span data-ttu-id="91630-126">В данном случае это — *centralus*.</span><span class="sxs-lookup"><span data-stu-id="91630-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="91630-127">Запуска hello **сетевого адаптера сети azure создать** команда toocreate сетевой Адаптер с статический частных IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="91630-127">Run hello **azure network nic create** command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="91630-128">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="91630-128">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="91630-129">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91630-129">Expected output:</span></span>
   
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
   
   * <span data-ttu-id="91630-130">**-a (или --private-ip-address)**.</span><span class="sxs-lookup"><span data-stu-id="91630-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="91630-131">Статический частный IP-адрес для hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="91630-131">Static private IP address for hello NIC.</span></span>
   * <span data-ttu-id="91630-132">**-m (или --subnet-vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="91630-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="91630-133">Имя виртуальной сети, где будут создаваться hello Сетевых hello.</span><span class="sxs-lookup"><span data-stu-id="91630-133">Name of hello VNet where hello NIC will be created.</span></span>
   * <span data-ttu-id="91630-134">**-k (или --subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="91630-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="91630-135">Имя подсети hello, где будут создаваться hello сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="91630-135">Name of hello subnet where hello NIC will be created.</span></span>
5. <span data-ttu-id="91630-136">Запустите hello **создания виртуальной машины azure** команда toocreate hello созданную виртуальную Машину с помощью hello общедоступного IP-адреса и сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="91630-136">Run hello **azure vm create** command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="91630-137">Список Hello отображаться после вывода hello объясняется hello параметров, используемых.</span><span class="sxs-lookup"><span data-stu-id="91630-137">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="91630-138">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91630-138">Expected output:</span></span>
   
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
   
   * <span data-ttu-id="91630-139">**-y (или --os-type)**.</span><span class="sxs-lookup"><span data-stu-id="91630-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="91630-140">Тип операционной системы для виртуальной Машины, hello либо *Windows* или *Linux*.</span><span class="sxs-lookup"><span data-stu-id="91630-140">Type of operating system for hello VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="91630-141">**-f (или --nic-name)**.</span><span class="sxs-lookup"><span data-stu-id="91630-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="91630-142">Имя hello hello сетевого Адаптера виртуальной Машины будет использовать.</span><span class="sxs-lookup"><span data-stu-id="91630-142">Name of hello NIC hello VM will use.</span></span>
   * <span data-ttu-id="91630-143">**-i (или --public-ip-name)**.</span><span class="sxs-lookup"><span data-stu-id="91630-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="91630-144">Имя hello открытый IP hello виртуальная машина будет использовать.</span><span class="sxs-lookup"><span data-stu-id="91630-144">Name of hello public IP hello VM will use.</span></span>
   * <span data-ttu-id="91630-145">**-F (или --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="91630-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="91630-146">Имя виртуальной сети, где будут создаваться hello ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="91630-146">Name of hello VNet where hello VM will be created.</span></span>
   * <span data-ttu-id="91630-147">**-j (или --vnet-subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="91630-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="91630-148">Имя подсети hello, где будут создаваться hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="91630-148">Name of hello subnet where hello VM will be created.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="91630-149">Как статических частных IP-tooretrieve адресов сведения для виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="91630-149">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="91630-150">tooview hello статических частного IP-адреса сведения для hello создания ВМ с hello-сценарий, приведенный выше, запустите следующую команду Azure CLI hello и просмотрите значения hello для *метод alloc частный IP-адрес* и *частный IP-адрес*:</span><span class="sxs-lookup"><span data-stu-id="91630-150">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="91630-151">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91630-151">Expected output:</span></span>

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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="91630-152">Как tooremove статических частных IP-адресов из виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="91630-152">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="91630-153">Статический частный IP-адрес нельзя удалить из сетевой карты с использованием Azure CLI для диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="91630-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="91630-154">Необходимо создать новый сетевой Адаптер, использующий динамических IP-адресов, удалите hello предыдущих сетевой Адаптер из виртуальной Машины hello, а затем добавьте новый hello toohello сетевого Адаптера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="91630-154">You must create a new NIC that uses a dynamic IP, remove hello previous NIC from hello VM, and then add hello new NIC toohello VM.</span></span> <span data-ttu-id="91630-155">toochange hello сетевого Адаптера для hello виртуальной Машины используется int eh выше команды, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="91630-155">toochange hello NIC for hello VM used int eh commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="91630-156">Запустите hello **сетевого адаптера сети azure создать** команды toocreate новый сетевой Адаптер, с помощью динамического выделения IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="91630-156">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="91630-157">Обратите внимание на то, каким образом не требуется toospecify hello IP-адрес этого времени.</span><span class="sxs-lookup"><span data-stu-id="91630-157">Notice how you do not need toospecify hello IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="91630-158">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91630-158">Expected output:</span></span>
   
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
2. <span data-ttu-id="91630-159">Запустите hello **набор виртуальных машин azure** команда toochange hello сетевой Адаптер, используемый hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="91630-159">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="91630-160">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91630-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="91630-161">Если было, запустите hello **удалить сетевого адаптера сети azure** команды toodelete, старый hello сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="91630-161">If wanted, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="91630-162">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91630-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="91630-163">Как tooadd статический частных IP-адрес решения tooan существующей виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="91630-163">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="91630-164">tooadd статические частного IP адрес toohello сетевой Адаптер, используемый виртуальной машиной, созданной выше сценария hello выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="91630-164">tooadd a static private IP address toohello NIC used by teh VM created using hello script above, run hello following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="91630-165">Ожидаемые выходные данные:</span><span class="sxs-lookup"><span data-stu-id="91630-165">Expected output:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="91630-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="91630-166">Next steps</span></span>
* <span data-ttu-id="91630-167">Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="91630-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="91630-168">Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="91630-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="91630-169">Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="91630-169">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

