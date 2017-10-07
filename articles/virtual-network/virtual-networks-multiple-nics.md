---
title: "aaaCreate виртуальной Машины (классические) с несколькими сетевыми адаптерами, с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate и настройка виртуальных машин с несколькими сетевыми адаптерами, с помощью PowerShell."
services: virtual-network, virtual-machines
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a1a3952c-2dcc-4977-bd7a-52d623c1fb07
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 8ef35bd4cfd7e6a527080f1cfc541275ca86f5e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics"></a><span data-ttu-id="d7662-103">Создание виртуальных машин (классическая модель) с несколькими сетевыми интерфейсами</span><span class="sxs-lookup"><span data-stu-id="d7662-103">Create a VM (Classic) with multiple NICs</span></span>
<span data-ttu-id="d7662-104">Можно создавать виртуальные машины (ВМ) в Azure и присоединить несколько tooeach сетевых интерфейсов (NIC) виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d7662-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="d7662-105">Это необходимо для целого ряда сетевых устройств (например, в составе решений для доставки приложений и оптимизации работы глобальной сети).</span><span class="sxs-lookup"><span data-stu-id="d7662-105">Multiple NICs are a requirement for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span> <span data-ttu-id="d7662-106">Кроме того, поддержка нескольких сетевых интерфейсов обеспечивает изоляцию трафика между ними.</span><span class="sxs-lookup"><span data-stu-id="d7662-106">Multiple NICs also provide isolation of traffic between NICs.</span></span>

![Несколько сетевых адаптеров на виртуальной машине](./media/virtual-networks-multiple-nics/IC757773.png)

<span data-ttu-id="d7662-108">Рисунок отображает Hello виртуальной Машины с тремя сетевыми адаптерами, подключить tooa другой подсети.</span><span class="sxs-lookup"><span data-stu-id="d7662-108">hello figure shows a VM with three NICs, each connected tooa different subnet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7662-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d7662-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d7662-110">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="d7662-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="d7662-111">Для большинства новых развертываний мы рекомендуем использовать модель развертывания с помощью Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7662-111">Microsoft recommends that most new deployments use Resource Manager.</span></span>

* <span data-ttu-id="d7662-112">С выходом в Интернет виртуального IP-адреса (классического развертывания) поддерживается только на сетевом адаптере hello «default».</span><span class="sxs-lookup"><span data-stu-id="d7662-112">Internet-facing VIP (classic deployments) is only supported on hello "default" NIC.</span></span> <span data-ttu-id="d7662-113">Имеется только один виртуальный IP-адрес toohello IP-адрес сетевого адаптера. по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="d7662-113">There is only one VIP toohello IP of hello default NIC.</span></span>
* <span data-ttu-id="d7662-114">В настоящее время для виртуальных машин с несколькими сетевыми картами не поддерживаются общедоступные IP-адреса уровня экземпляра (LPIP) (классические развертывания).</span><span class="sxs-lookup"><span data-stu-id="d7662-114">At this time, Instance Level Public IP (LPIP) addresses (classic deployments) are not supported for multi NIC VMs.</span></span>
* <span data-ttu-id="d7662-115">Здравствуйте, порядок сетевых адаптеров hello в внутри hello виртуальной Машины будет произвольным и может изменяться при обновлениях инфраструктуры Azure.</span><span class="sxs-lookup"><span data-stu-id="d7662-115">hello order of hello NICs from inside hello VM will be random, and could also change across Azure infrastructure updates.</span></span> <span data-ttu-id="d7662-116">Здравствуйте, IP-адресов, но hello соответствующие ethernet MAC адреса остаются одинаковыми hello.</span><span class="sxs-lookup"><span data-stu-id="d7662-116">However, hello IP addresses, and hello corresponding ethernet MAC addresses will remain hello same.</span></span> <span data-ttu-id="d7662-117">Например, предположим, **Eth1** имеет IP-адрес 10.1.0.100 и MAC-адрес 00-0D-3A-B0-39-0D; после обновления инфраструктуры Azure и перезагрузки, он может быть изменен слишком**Eth2**, но hello IP- и MAC связывания будет остаются одинаковыми hello.</span><span class="sxs-lookup"><span data-stu-id="d7662-117">For example, assume **Eth1** has IP address 10.1.0.100 and MAC address 00-0D-3A-B0-39-0D; after an Azure infrastructure update and reboot, it could be changed too**Eth2**, but hello IP and MAC pairing will remain hello same.</span></span> <span data-ttu-id="d7662-118">Если перезагрузка инициирована клиентом, hello порядок сетевого Адаптера останется таким же hello.</span><span class="sxs-lookup"><span data-stu-id="d7662-118">When a restart is customer-initiated, hello NIC order will remain hello same.</span></span>
* <span data-ttu-id="d7662-119">Hello адрес для каждого сетевого Адаптера на каждой виртуальной Машине должен быть расположен в подсети, несколько сетевых адаптеров на одной виртуальной Машине можно каждой назначен Здравствуйте, адреса, которые находятся в одной подсети.</span><span class="sxs-lookup"><span data-stu-id="d7662-119">hello address for each NIC on each VM must be located in a subnet, multiple NICs on a single VM can each be assigned addresses that are in hello same subnet.</span></span>
* <span data-ttu-id="d7662-120">Hello размер виртуальной Машины определяет hello количество сетевых Адаптеров, которые можно создать для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d7662-120">hello VM size determines hello number of NICS that you can create for a VM.</span></span> <span data-ttu-id="d7662-121">Справочник по hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) виртуальной Машины размеров toodetermine статей, какое количество сетевых Адаптеров, размер каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d7662-121">Reference hello [Windows Server](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VM sizes articles toodetermine how many NICS each VM size supports.</span></span> 

## <a name="network-security-groups-nsgs"></a><span data-ttu-id="d7662-122">Группы безопасности сети (NSG)</span><span class="sxs-lookup"><span data-stu-id="d7662-122">Network Security Groups (NSGs)</span></span>
<span data-ttu-id="d7662-123">В развертывании диспетчера ресурсов любая сетевая карта на виртуальной машине может быть связана с группой безопасности сети (NSG), включая сетевые карты на виртуальных машинах с поддержкой нескольких сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="d7662-123">In a Resource Manager deployment, any NIC on a VM may be associated with a Network Security Group (NSG), including any NICs on a VM that has multiple NICs enabled.</span></span> <span data-ttu-id="d7662-124">Если сетевой Адаптер, назначается адрес в одной подсети, в котором hello подсети связан с NSG, затем hello в подсети hello NSG также применяются правила toothat сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="d7662-124">If a NIC is assigned an address within a subnet where hello subnet is associated with an NSG, then hello rules in hello subnet’s NSG also apply toothat NIC.</span></span> <span data-ttu-id="d7662-125">В подсетях tooassociating сложения с Nsg можно также связать сетевой Адаптер с NSG.</span><span class="sxs-lookup"><span data-stu-id="d7662-125">In addition tooassociating subnets with NSGs, you can also associate a NIC with an NSG.</span></span>

<span data-ttu-id="d7662-126">Если подсеть связан с NSG, а сетевой Адаптер в этой подсети по отдельности, связанные с NSG, hello связанные правила NSG применяются в **потока порядок** toohello направление hello трафика, передаваемого в соответствии с Hello сетевого Адаптера:</span><span class="sxs-lookup"><span data-stu-id="d7662-126">If a subnet is associated with an NSG, and a NIC within that subnet is individually associated with an NSG, hello associated NSG rules are applied in **flow order** according toohello direction of hello traffic being passed into or out of hello NIC:</span></span>

* <span data-ttu-id="d7662-127">**Входящий трафик** которого целевым является hello сетевого Адаптера в вопрос сначала проходит через hello подсети, вызывающих срабатывание правил NSG hello подсети, до передачи в hello сетевого Адаптера, а затем вызывающих срабатывание правил NSG hello сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="d7662-127">**Incoming traffic** whose destination is hello NIC in question flows first through hello subnet, triggering hello subnet’s NSG rules, before passing into hello NIC, then triggering hello NIC’s NSG rules.</span></span>
* <span data-ttu-id="d7662-128">**Исходящий трафик** , источником которого является hello сетевого Адаптера в вопросе потоков первым обслужен из hello сетевого Адаптера, вызывающих срабатывание правил NSG hello сетевой Адаптер, перед обрабатываемым hello подсети, а затем вызывающих срабатывание правил NSG hello подсети.</span><span class="sxs-lookup"><span data-stu-id="d7662-128">**Outgoing traffic** whose source is hello NIC in question flows first out from hello NIC, triggering hello NIC’s NSG rules, before passing through hello subnet, then triggering hello subnet’s NSG rules.</span></span>

<span data-ttu-id="d7662-129">Дополнительные сведения о [сетевых групп безопасности](virtual-networks-nsg.md) и как они применяются на основании toosubnets ассоциации, виртуальные машины и сетевых адаптеров...</span><span class="sxs-lookup"><span data-stu-id="d7662-129">Learn more about [Network Security Groups](virtual-networks-nsg.md) and how they are applied based on associations toosubnets, VMs, and NICs..</span></span>

## <a name="how-tooconfigure-a-multi-nic-vm-in-a-classic-deployment"></a><span data-ttu-id="d7662-130">Как tooConfigure нескольких сетевых Адаптеров виртуальной Машины, в классическом развертывании</span><span class="sxs-lookup"><span data-stu-id="d7662-130">How tooConfigure a multi NIC VM in a classic deployment</span></span>
<span data-ttu-id="d7662-131">Приведенные ниже инструкции Hello служит для создания нескольких виртуальных Машин NIC с тремя сетевыми адаптерами: сетевой Адаптер по умолчанию и два дополнительных сетевых адаптера.</span><span class="sxs-lookup"><span data-stu-id="d7662-131">hello instructions below will help you create a multi NIC VM containing 3 NICs: a default NIC and two additional NICs.</span></span> <span data-ttu-id="d7662-132">действия по настройке Hello создаст виртуальной Машины, который будет настроен в соответствии с toohello службы фрагменте файла конфигурации ниже:</span><span class="sxs-lookup"><span data-stu-id="d7662-132">hello configuration steps will create a VM that will be configured according toohello service configuration file fragment below:</span></span>

    <VirtualNetworkSite name="MultiNIC-VNet" Location="North Europe">
    <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
    … Skip over hello remainder section …
    </VirtualNetworkSite>


<span data-ttu-id="d7662-133">Необходимо, чтобы следующие необходимые компоненты перед попыткой команды PowerShell toorun hello в примере hello hello.</span><span class="sxs-lookup"><span data-stu-id="d7662-133">You need hello following prerequisites before trying toorun hello PowerShell commands in hello example.</span></span>

* <span data-ttu-id="d7662-134">Подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="d7662-134">An Azure subscription.</span></span>
* <span data-ttu-id="d7662-135">Настроенная виртуальная сеть.</span><span class="sxs-lookup"><span data-stu-id="d7662-135">A configured virtual network.</span></span> <span data-ttu-id="d7662-136">Дополнительные сведения о виртуальных сетях см. в [этой статье](virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d7662-136">See [Virtual Network Overview](virtual-networks-overview.md) for more information about VNets.</span></span>
* <span data-ttu-id="d7662-137">последнюю версию Azure PowerShell Hello загружаются и устанавливаются.</span><span class="sxs-lookup"><span data-stu-id="d7662-137">hello latest version of Azure PowerShell downloaded and installed.</span></span> <span data-ttu-id="d7662-138">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d7662-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d7662-139">toocreate виртуальной Машины с несколькими сетевыми адаптерами, полный hello следующие шаги путем ввода каждой команды в одном сеансе PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d7662-139">toocreate a VM with multiple NICs, complete hello following steps by entering each command within a single PowerShell session:</span></span>

1. <span data-ttu-id="d7662-140">Выберите образ виртуальной машины в коллекции образов Azure.</span><span class="sxs-lookup"><span data-stu-id="d7662-140">Select a VM image from Azure VM image gallery.</span></span> <span data-ttu-id="d7662-141">Обратите внимание на то, что образы часто меняются, а их доступность зависит от региона.</span><span class="sxs-lookup"><span data-stu-id="d7662-141">Note that images change frequently and are available by region.</span></span> <span data-ttu-id="d7662-142">Hello изображения, указанного в приведенном ниже примере hello может изменить или может в вашем регионе, поэтому будьте внимательны и toospecify hello образа необходимо.</span><span class="sxs-lookup"><span data-stu-id="d7662-142">hello image specified in hello example below may change or might not be in your region, so be sure toospecify hello image you need.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    -ImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201410.01-en.us-127GB.vhd"
    ```

2. <span data-ttu-id="d7662-143">Создайте конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d7662-143">Create a VM configuration.</span></span>

    ```powershell
    $vm = New-AzureVMConfig -Name "MultiNicVM" -InstanceSize "ExtraLarge" `
    -Image $image.ImageName –AvailabilitySetName "MyAVSet"
    ```

3. <span data-ttu-id="d7662-144">Создайте имя входа администратора по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="d7662-144">Create hello default administrator login.</span></span>

    ```powershell
    Add-AzureProvisioningConfig –VM $vm -Windows -AdminUserName "<YourAdminUID>" `
    -Password "<YourAdminPassword>"
    ```

4. <span data-ttu-id="d7662-145">Добавьте конфигурацию виртуальной Машины toohello дополнительные сетевые адаптеры.</span><span class="sxs-lookup"><span data-stu-id="d7662-145">Add additional NICs toohello VM configuration.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name "Ethernet1" `
    -SubnetName "Midtier" -StaticVNetIPAddress "10.1.1.111" -VM $vm
    Add-AzureNetworkInterfaceConfig -Name "Ethernet2" `
    -SubnetName "Backend" -StaticVNetIPAddress "10.1.2.222" -VM $vm
    ```

5. <span data-ttu-id="d7662-146">Укажите подсеть hello и IP-адрес для сетевого адаптера. по умолчанию hello</span><span class="sxs-lookup"><span data-stu-id="d7662-146">Specify hello subnet and IP address for hello default NIC.</span></span>

    ```powershell
    Set-AzureSubnet -SubnetNames "Frontend" -VM $vm
    Set-AzureStaticVNetIP -IPAddress "10.1.0.100" -VM $vm
    ```

6. <span data-ttu-id="d7662-147">Создайте hello виртуальной Машины в виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d7662-147">Create hello VM in your virtual network.</span></span>

    ```powershell
    New-AzureVM -ServiceName "MultiNIC-CS" –VNetName "MultiNIC-VNet" –VMs $vm
    ```

    > [!NOTE]
    > <span data-ttu-id="d7662-148">Hello виртуальную сеть, указанные здесь должен уже существовать (согласно hello необходимые компоненты).</span><span class="sxs-lookup"><span data-stu-id="d7662-148">hello VNet that you specify here must already exist (as mentioned in hello prerequisites).</span></span> <span data-ttu-id="d7662-149">пример Hello указывает виртуальную сеть с именем **MultiNIC-VNet**.</span><span class="sxs-lookup"><span data-stu-id="d7662-149">hello example below specifies a virtual network named **MultiNIC-VNet**.</span></span>
    >

## <a name="limitations"></a><span data-ttu-id="d7662-150">Ограничения</span><span class="sxs-lookup"><span data-stu-id="d7662-150">Limitations</span></span>
<span data-ttu-id="d7662-151">Hello следующие ограничения применяются при использовании нескольких сетевых адаптеров:</span><span class="sxs-lookup"><span data-stu-id="d7662-151">hello following limitations are applicable when using multiple NICs:</span></span>

* <span data-ttu-id="d7662-152">Виртуальные машины с несколькими сетевыми интерфейсами должны создаваться в виртуальных сетях Azure.</span><span class="sxs-lookup"><span data-stu-id="d7662-152">VMs with multiple NICs must be created in Azure virtual networks (VNets).</span></span> <span data-ttu-id="d7662-153">Для виртуальных машин без поддержки виртуальной сети нельзя настроить несколько сетевых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="d7662-153">Non-VNet VMs cannot be configured with multiple NICs.</span></span>
* <span data-ttu-id="d7662-154">Все виртуальные машины в группе доступности набор toouse необходимость несколько сетевых адаптеров или одного сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="d7662-154">All VMs in an availability set need toouse either multiple NICs or a single NIC.</span></span> <span data-ttu-id="d7662-155">В группе доступности нельзя одновременно использовать виртуальные машины с несколькими сетевыми интерфейсами и виртуальные машины с одним сетевым интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="d7662-155">There cannot be a mixture of multiple NIC VMs and single NIC VMs within an availability set.</span></span> <span data-ttu-id="d7662-156">Те же правила действуют для виртуальных машин в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="d7662-156">Same rules apply for VMs in a cloud service.</span></span> <span data-ttu-id="d7662-157">Несколько сетевых Адаптеров виртуальных машин, они не являются обязательными toohave hello одинаковое число сетевых адаптеров, при условии, что каждый из них имеет по крайней мере два.</span><span class="sxs-lookup"><span data-stu-id="d7662-157">For multiple NIC VMs, they aren't required toohave hello same number of NICs, as long as they each have at least two.</span></span>
* <span data-ttu-id="d7662-158">Чтобы настроить несколько сетевых интерфейсов для развернутой виртуальной машины с одним сетевым интерфейсом (и наоборот), необходимо удалить, а затем повторно создать эту виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="d7662-158">A VM with a single NIC cannot be configured with multi NICs (and vice-versa) once it is deployed, without deleting and re-creating it.</span></span>

## <a name="secondary-nics-access-tooother-subnets"></a><span data-ttu-id="d7662-159">Подсети tooother доступа вторичных сетевых адаптеров</span><span class="sxs-lookup"><span data-stu-id="d7662-159">Secondary NICs access tooother subnets</span></span>
<span data-ttu-id="d7662-160">По умолчанию вторичных сетевых адаптеров не будет настроен шлюз по умолчанию, из-за toowhich hello трафику на hello вторичных сетевых адаптеров будет ограниченной toobe внутри hello одной подсети.</span><span class="sxs-lookup"><span data-stu-id="d7662-160">By default secondary NICs will not be configured with a default gateway, due toowhich hello traffic flow on hello secondary NICs will be limited toobe within hello same subnet.</span></span> <span data-ttu-id="d7662-161">Hello нужные tooenable вторичных сетевых адаптеров tootalk собственные подсеть извне, им нужно будет tooadd запись в hello таблицы tooconfigure hello шлюз маршрутизации как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="d7662-161">If hello users want tooenable secondary NICs tootalk outside their own subnet, they will need tooadd an entry in hello routing table tooconfigure hello gateway as described below.</span></span>

> [!NOTE]
> <span data-ttu-id="d7662-162">Для виртуальных машин, созданных до июля 2015 года, шлюз по умолчанию может быть настроен для всех сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="d7662-162">VMs created before July 2015 may have a default gateway configured for all NICs.</span></span> <span data-ttu-id="d7662-163">шлюз по умолчанию Hello для вторичных сетевых адаптеров не будут удалены только виртуальные машины после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="d7662-163">hello default gateway for secondary NICs will not be removed until these VMs are rebooted.</span></span> <span data-ttu-id="d7662-164">В операционных системах, использующих hello слабого узла модели маршрутизации, например в Linux подключение к Интернету может нарушить работу, если hello входящего и исходящего трафика используют разные сетевые адаптеры.</span><span class="sxs-lookup"><span data-stu-id="d7662-164">In Operating systems that use hello weak host routing model, such as Linux, Internet connectivity can break if hello ingress and egress traffic use different NICs.</span></span>
> 

### <a name="configure-windows-vms"></a><span data-ttu-id="d7662-165">Настройка виртуальных машин Windows</span><span class="sxs-lookup"><span data-stu-id="d7662-165">Configure Windows VMs</span></span>
<span data-ttu-id="d7662-166">Предположим, что у вас есть виртуальная машина Windows с двумя сетевыми картами со следующими адресами:</span><span class="sxs-lookup"><span data-stu-id="d7662-166">Suppose that you have a Windows VM with two NICs as follows:</span></span>

* <span data-ttu-id="d7662-167">IP-адрес основной сетевой карты: 192.168.1.4;</span><span class="sxs-lookup"><span data-stu-id="d7662-167">Primary NIC IP address: 192.168.1.4</span></span>
* <span data-ttu-id="d7662-168">IP-адрес дополнительной сетевой карты: 192.168.2.5.</span><span class="sxs-lookup"><span data-stu-id="d7662-168">Secondary NIC IP address: 192.168.2.5</span></span>

<span data-ttu-id="d7662-169">Hello таблицу маршрутизации IPv4 для этой виртуальной Машины будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d7662-169">hello IPv4 route table for this VM would look like this:</span></span>

    IPv4 Route Table
    ===========================================================================
    Active Routes:
    Network Destination        Netmask          Gateway       Interface  Metric
              0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
            127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
            127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
      127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        168.63.129.16  255.255.255.255      192.168.1.1      192.168.1.4      6
          192.168.1.0    255.255.255.0         On-link       192.168.1.4    261
          192.168.1.4  255.255.255.255         On-link       192.168.1.4    261
        192.168.1.255  255.255.255.255         On-link       192.168.1.4    261
          192.168.2.0    255.255.255.0         On-link       192.168.2.5    261
          192.168.2.5  255.255.255.255         On-link       192.168.2.5    261
        192.168.2.255  255.255.255.255         On-link       192.168.2.5    261
            224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
            224.0.0.0        240.0.0.0         On-link       192.168.1.4    261
            224.0.0.0        240.0.0.0         On-link       192.168.2.5    261
      255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
      255.255.255.255  255.255.255.255         On-link       192.168.1.4    261
      255.255.255.255  255.255.255.255         On-link       192.168.2.5    261
    ===========================================================================

<span data-ttu-id="d7662-170">Обратите внимание, что этот маршрут по умолчанию hello (0.0.0.0) — только доступные toohello первичный сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="d7662-170">Notice that hello default route (0.0.0.0) is only available toohello primary NIC.</span></span> <span data-ttu-id="d7662-171">Не будет возможности tooaccess ресурсам за пределами hello подсеть для получателей hello сетевого Адаптера, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="d7662-171">You will not be able tooaccess resources outside hello subnet for hello secondary NIC, as seen below:</span></span>

    C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5

    Pinging 192.168.1.7 from 192.165.2.5 with 32 bytes of data:
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.
    PING: transmit failed. General failure.

<span data-ttu-id="d7662-172">tooadd Маршрутизация по умолчанию hello дополнительный сетевой Адаптер, выполните следующие действия hello:</span><span class="sxs-lookup"><span data-stu-id="d7662-172">tooadd a default route on hello secondary NIC, follow hello steps below:</span></span>

1. <span data-ttu-id="d7662-173">Из командной строки выполните команду hello ниже tooidentify hello порядковый номер для hello дополнительный сетевой Адаптер:</span><span class="sxs-lookup"><span data-stu-id="d7662-173">From a command prompt, run hello command below tooidentify hello index number for hello secondary NIC:</span></span>
   
        C:\Users\Administrator>route print
        ===========================================================================
        Interface List
         29...00 15 17 d9 b1 6d ......Microsoft Virtual Machine Bus Network Adapter #16
         27...00 15 17 d9 b1 41 ......Microsoft Virtual Machine Bus Network Adapter #14
          1...........................Software Loopback Interface 1
         14...00 00 00 00 00 00 00 e0 Teredo Tunneling Pseudo-Interface
         20...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
        ===========================================================================
2. <span data-ttu-id="d7662-174">Обратите внимание, hello вторую запись в таблице hello, с индексом, 27 (в данном примере).</span><span class="sxs-lookup"><span data-stu-id="d7662-174">Notice hello second entry in hello table, with an index of 27 (in this example).</span></span>
3. <span data-ttu-id="d7662-175">Запустите из командной строки hello, hello **добавить маршрут** команды, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d7662-175">From hello command prompt, run hello **route add** command as shown below.</span></span> <span data-ttu-id="d7662-176">В этом примере вы указываете 192.168.2.1 как шлюз по умолчанию hello для hello дополнительный сетевой Адаптер:</span><span class="sxs-lookup"><span data-stu-id="d7662-176">In this example, you are specifying 192.168.2.1 as hello default gateway for hello secondary NIC:</span></span>
   
        route ADD -p 0.0.0.0 MASK 0.0.0.0 192.168.2.1 METRIC 5000 IF 27
4. <span data-ttu-id="d7662-177">подключение tootest вернуться toohello командную строку и повторите tooping из другой подсети hello дополнительный сетевой Адаптер как int показано eh приведенном ниже примере:</span><span class="sxs-lookup"><span data-stu-id="d7662-177">tootest connectivity, go back toohello command prompt and try tooping a different subnet from hello secondary NIC as shown int eh example below:</span></span>
   
        C:\Users\Administrator>ping 192.168.1.7 -S 192.165.2.5
   
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
        Reply from 192.168.1.7: bytes=32 time=2ms TTL=128
        Reply from 192.168.1.7: bytes=32 time<1ms TTL=128
5. <span data-ttu-id="d7662-178">Можно также проверить ваш hello toocheck таблицы маршрутов добавления маршрута, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="d7662-178">You can also check your route table toocheck hello newly added route, as shown below:</span></span>
   
        C:\Users\Administrator>route print
   
        ...
   
        IPv4 Route Table
        ===========================================================================
        Active Routes:
        Network Destination        Netmask          Gateway       Interface  Metric
                  0.0.0.0          0.0.0.0      192.168.1.1      192.168.1.4      5
                  0.0.0.0          0.0.0.0      192.168.2.1      192.168.2.5   5005
                127.0.0.0        255.0.0.0         On-link         127.0.0.1    306

### <a name="configure-linux-vms"></a><span data-ttu-id="d7662-179">Настройка виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="d7662-179">Configure Linux VMs</span></span>
<span data-ttu-id="d7662-180">Для виртуальных машин Linux, поскольку слабого маршрутизации, использует поведение по умолчанию hello рекомендуется, hello вторичных сетевых адаптеров являются ограниченными tootraffic потоков только в пределах hello одной подсети.</span><span class="sxs-lookup"><span data-stu-id="d7662-180">For Linux VMs, since hello default behavior uses weak host routing, we recommend that hello secondary NICs are restricted tootraffic flows only within hello same subnet.</span></span> <span data-ttu-id="d7662-181">Однако если некоторые сценарии требуют подключения за пределами подсети hello, пользователи должны включить tooensure маршрутизации на основе политик, Здравствуйте, входящего и исходящего трафика использует hello одного сетевого адаптера.</span><span class="sxs-lookup"><span data-stu-id="d7662-181">However if certain scenarios demand connectivity outside hello subnet, users should enable policy based routing tooensure that hello ingress and egress traffic uses hello same NIC.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7662-182">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7662-182">Next steps</span></span>
* <span data-ttu-id="d7662-183">Развертывание [виртуальных машин с несколькими сетевыми картами в сценарии 2-уровневого приложения в развертывании диспетчера ресурсов](virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="d7662-183">Deploy [MultiNIC VMs in a 2-tier application scenario in a Resource Manager deployment](virtual-network-deploy-multinic-arm-template.md).</span></span>
* <span data-ttu-id="d7662-184">Развертывание [виртуальных машин с несколькими сетевыми картами в сценарии 2-уровневого приложения в классическом развертывании](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d7662-184">Deploy [MultiNIC VMs in a 2-tier application scenario in a classic deployment](virtual-network-deploy-multinic-classic-ps.md).</span></span>

