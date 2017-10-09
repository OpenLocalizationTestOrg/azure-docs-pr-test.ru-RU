---
title: "Группы доступности сервера - виртуальных машинах Azure — аварийного восстановления aaaSQL | Документы Microsoft"
description: "В этой статье объясняется, как группировать tooconfigure доступности SQL Server на виртуальных машинах Azure с репликой в разных регионах."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 388c464e-a16e-4c9d-a0d5-bb7cf5974689
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: df6238dc61c5a56879c75c9bf7314c618f43c0ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="2d2e2-103">Настройка группы доступности AlwaysOn на виртуальных машинах Azure в разных регионах</span><span class="sxs-lookup"><span data-stu-id="2d2e2-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="2d2e2-104">В этой статье объясняется, как tooconfigure доступности SQL Server Always On группы реплики на виртуальных машинах Azure в удаленном расположении Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-104">This article explains how tooconfigure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="2d2e2-105">Используйте этот конфигурации toosupport аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-105">Use this configuration toosupport disaster recovery.</span></span>

<span data-ttu-id="2d2e2-106">Эта статья относится tooAzure виртуальные машины в режим диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-106">This article applies tooAzure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="2d2e2-107">Hello иллюстрации показан общий развертывания группы доступности на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-107">hello following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="2d2e2-109">В таком развертывании все виртуальные машины находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="2d2e2-110">Hello реплики группы доступности могут иметь синхронной фиксации с автоматическим переходом на SQL-1 и SQL 2.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-110">hello availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="2d2e2-111">toobuild этой архитектуре см [шаблон группы доступности или учебника](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-111">toobuild this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="2d2e2-112">Эта архитектура является уязвимым toodowntime Если hello регион Azure становится недоступной.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-112">This architecture is vulnerable toodowntime if hello Azure region becomes inaccessible.</span></span> <span data-ttu-id="2d2e2-113">tooovercome этой уязвимости, добавить реплику в другом регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-113">tooovercome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="2d2e2-114">Hello следующей схеме показано как выглядит новая архитектура hello.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-114">hello following diagram shows how hello new architecture would look:</span></span>

   ![Аварийное восстановление группы доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="2d2e2-116">Hello предыдущей схеме показаны новые виртуальная машина с именем SQL-3.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-116">hello preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="2d2e2-117">SQL-3 находится в другом регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="2d2e2-118">SQL-3 добавляется toohello отказоустойчивого кластера Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-118">SQL-3 is added toohello Windows Server Failover Cluster.</span></span> <span data-ttu-id="2d2e2-119">На SQL-3 можно разместить реплику группы доступности.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="2d2e2-120">И, наконец Обратите внимание, что этой hello регион Azure для SQL-3 имеет новую подсистему балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-120">Finally, notice that hello Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="2d2e2-121">Группы доступности Azure является обязательным, если Здравствуйте, более чем одна виртуальная машина находится в одном регионе.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-121">An Azure availability set is required when more than one virtual machine is in hello same region.</span></span> <span data-ttu-id="2d2e2-122">Если только одна виртуальная машина находится в регионе hello, группа доступности hello не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-122">If only one virtual machine is in hello region, then hello availability set is not required.</span></span> <span data-ttu-id="2d2e2-123">Поместить виртуальную машину в группу доступности можно только во время создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="2d2e2-124">Если hello виртуальная машина уже находится в наборе доступности, можно добавить виртуальную машину для более поздней версии дополнительную реплику.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-124">If hello virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="2d2e2-125">В этой архитектуре реплики hello в удаленном регионе hello обычно настраивается с помощью режима доступности асинхронной фиксации и отработка отказа вручную.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-125">In this architecture, hello replica in hello remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="2d2e2-126">Если реплики группы доступности находятся на виртуальных машинах Azure в разных регионах Azure, то для каждого региона требуется:</span><span class="sxs-lookup"><span data-stu-id="2d2e2-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="2d2e2-127">шлюз виртуальной сети;</span><span class="sxs-lookup"><span data-stu-id="2d2e2-127">A virtual network gateway</span></span>
* <span data-ttu-id="2d2e2-128">подключение к шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-128">A virtual network gateway connection</span></span>

<span data-ttu-id="2d2e2-129">Hello следующая диаграмма показывает взаимодействие hello сети между центрами обработки данных.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-129">hello following diagram shows how hello networks communicate between data centers.</span></span>

   ![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="2d2e2-131">Эта архитектура влечет за собой оплату исходящего трафика для данных, реплицируемых между регионами Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="2d2e2-132">Ознакомьтесь с разделом [Сведения о стоимости пропускной способности](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="2d2e2-133">Создание удаленной реплики</span><span class="sxs-lookup"><span data-stu-id="2d2e2-133">Create remote replica</span></span>

<span data-ttu-id="2d2e2-134">реплики в удаленном центре обработки данных, toocreate hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2d2e2-134">toocreate a replica in a remote data center, do hello following steps:</span></span>

1. <span data-ttu-id="2d2e2-135">[Создание виртуальной сети в новой области hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-135">[Create a virtual network in hello new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="2d2e2-136">[Настройка подключения виртуальной сети для виртуальной сети с помощью портала Azure hello](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-136">[Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="2d2e2-137">В некоторых случаях возможно подключение к виртуальной сети для виртуальной сети hello toocreate toouse PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-137">In some cases, you may have toouse PowerShell toocreate hello VNet-to-VNet connection.</span></span> <span data-ttu-id="2d2e2-138">Например при использовании различных учетных записях Azure невозможно настроить соединение hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-138">For example, if you use different Azure accounts you cannot configure hello connection in hello portal.</span></span> <span data-ttu-id="2d2e2-139">В этом разделе, [VNet к VNet Настройка соединения с помощью портала Azure "hello"](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-139">In this case see, [Configure a VNet-to-VNet connection using hello Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="2d2e2-140">[Создание контроллера домена в новой области hello](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-140">[Create a domain controller in hello new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="2d2e2-141">Этот контроллер домена обеспечивает проверку подлинности, если не доступен контроллер домена hello в первичном сайте hello.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-141">This domain controller provides authentication if hello domain controller in hello primary site is not available.</span></span>

1. <span data-ttu-id="2d2e2-142">[Создание виртуальной машины SQL Server в новой области hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-142">[Create a SQL Server virtual machine in hello new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="2d2e2-143">[Создайте балансировки нагрузки Azure в сети hello в новой области hello](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-143">[Create an Azure load balancer in hello network on hello new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="2d2e2-144">Эта подсистема балансировки нагрузки должна:</span><span class="sxs-lookup"><span data-stu-id="2d2e2-144">This load balancer must:</span></span>

   - <span data-ttu-id="2d2e2-145">В hello одной сети и подсети как hello новой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-145">Be in hello same network and subnet as hello new virtual machine.</span></span>
   - <span data-ttu-id="2d2e2-146">Иметь статический IP-адрес для прослушивателя группы доступности hello.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-146">Have a static IP address for hello availability group listener.</span></span>
   - <span data-ttu-id="2d2e2-147">Включить пул серверной части, состоящий из только для виртуальных машин hello в hello же регионе, которые hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-147">Include a backend pool consisting of only hello virtual machines in hello same region as hello load balancer.</span></span>
   - <span data-ttu-id="2d2e2-148">Используйте IP-адрес определенного toohello пробы TCP порт.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-148">Use a TCP port probe specific toohello IP address.</span></span>
   - <span data-ttu-id="2d2e2-149">У определенного toohello правила SQL Server hello балансировки нагрузки одного региона.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-149">Have a load balancing rule specific toohello SQL Server in hello same region.</span></span>  

1. <span data-ttu-id="2d2e2-150">[Добавить toohello функции отказоустойчивой кластеризации SQL Server, новый](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-150">[Add Failover Clustering feature toohello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="2d2e2-151">[Присоединение hello новому домену toohello SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-151">[Join hello new SQL Server toohello domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="2d2e2-152">[Задать учетную запись домена hello новый SQL Server toouse учетной записи для службы](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-152">[Set hello new SQL Server service account toouse a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="2d2e2-153">[Добавить новый toohello SQL Server hello отказоустойчивого кластера Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-153">[Add hello new SQL Server toohello Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="2d2e2-154">Создайте ресурс IP-адреса в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-154">Create an IP address resource on hello cluster.</span></span>

   <span data-ttu-id="2d2e2-155">Можно создать ресурс IP-адреса hello в диспетчере отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-155">You can create hello IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="2d2e2-156">Щелкните правой кнопкой мыши роль группы доступности hello, щелкните **добавить ресурс**, **дополнительные ресурсы**и нажмите кнопку **IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-156">Right-click hello availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![Создание IP-адреса](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="2d2e2-158">Настройте этот IP-адрес следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="2d2e2-159">Использование сети hello из hello удаленном центре обработки данных.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-159">Use hello network from hello remote data center.</span></span>
   - <span data-ttu-id="2d2e2-160">Назначьте hello IP-адрес из hello новую подсистему балансировки нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-160">Assign hello IP address from hello new Azure load balancer.</span></span> 

1. <span data-ttu-id="2d2e2-161">Здравствуйте, новый SQL Server в диспетчере конфигурации SQL Server на [включить группы доступности AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-161">On hello new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="2d2e2-162">[Порты брандмауэра откройте hello нового SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-162">[Open firewall ports on hello new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="2d2e2-163">Hello номера портов, необходимо tooopen зависят от среды.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-163">hello port numbers you need tooopen depend on your environment.</span></span> <span data-ttu-id="2d2e2-164">Открытые порты для зеркального отображения конечной точки и Azure hello загрузить зонда работоспособности подсистемы балансировки.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-164">Open ports for hello mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="2d2e2-165">[Добавить группу доступности toohello реплики на hello нового SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-165">[Add a replica toohello availability group on hello new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="2d2e2-166">Для реплики в удаленном регионе Azure настройте асинхронную репликацию с ручной отработкой отказа.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="2d2e2-167">Добавьте hello ресурс IP-адреса в качестве зависимости для кластера (сетевое имя) точки доступа клиента прослушивателя hello.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-167">Add hello IP address resource as a dependency for hello listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="2d2e2-168">Hello следующем снимке экрана показан правильно настроенный ресурс IP-адреса кластера:</span><span class="sxs-lookup"><span data-stu-id="2d2e2-168">hello following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="2d2e2-170">Группа ресурсов кластера Hello включает оба IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-170">hello cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="2d2e2-171">Оба IP-адреса являются зависимости для точки доступа клиента hello прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-171">Both IP addresses are dependencies for hello listener client access point.</span></span> <span data-ttu-id="2d2e2-172">Используйте hello **или** оператор в конфигурации зависимостей hello кластера.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-172">Use hello **OR** operator in hello cluster dependency configuration.</span></span>

1. <span data-ttu-id="2d2e2-173">[Задайте параметры кластера hello в PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-173">[Set hello cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="2d2e2-174">Запустите сценарий PowerShell hello с hello кластера сетевое имя, IP-адрес и порт пробы, настроенные в подсистеме балансировки нагрузки hello в новой области hello.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-174">Run hello PowerShell script with hello cluster network name, IP address, and probe port that you configured on hello load balancer in hello new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster name for hello network in hello new region (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "<IPResourceName>" # hello cluster name for hello new IP Address resource.
   $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB) in hello new region. This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <nnnnn> # hello probe port you set on hello ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="2d2e2-175">Настройка подключения для нескольких подсетей</span><span class="sxs-lookup"><span data-stu-id="2d2e2-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="2d2e2-176">реплика Hello в hello удаленном центре обработки данных является частью группы доступности hello, но он находится в другой подсети.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-176">hello replica in hello remote data center is part of hello availability group but it is in a different subnet.</span></span> <span data-ttu-id="2d2e2-177">Если эта реплика становится первичной репликой hello, может произойти истечение времени ожидания соединения приложения.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-177">If this replica becomes hello primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="2d2e2-178">Такое поведение является hello такой же, как в развертывании с несколькими подсетями группы доступности в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-178">This behavior is hello same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="2d2e2-179">tooallow подключений из клиентских приложений, обновите hello клиентское подключение или настроить кэширование на ресурсу сетевого имени кластера hello разрешение имен.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-179">tooallow connections from client applications, either update hello client connection or configure name resolution caching on hello cluster network name resource.</span></span>

<span data-ttu-id="2d2e2-180">Желательно, обновите tooset строки подключения клиента hello `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-180">Preferably, update hello client connection strings tooset `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="2d2e2-181">Ознакомьтесь с разделом [Соединение с помощью MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="2d2e2-182">Если невозможно изменить строки подключения hello, можно настроить кэширование разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-182">If you cannot modify hello connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="2d2e2-183">Ознакомьтесь с разделом [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/) (Время ожидания подключения в группе доступности с несколькими подсетями).</span><span class="sxs-lookup"><span data-stu-id="2d2e2-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-tooremote-region"></a><span data-ttu-id="2d2e2-184">При сбое tooremote области</span><span class="sxs-lookup"><span data-stu-id="2d2e2-184">Fail over tooremote region</span></span>

<span data-ttu-id="2d2e2-185">tootest прослушивателя подключения toohello удаленной области, можно выполнить переход hello реплики toohello удаленной области.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-185">tootest listener connectivity toohello remote region, you can fail over hello replica toohello remote region.</span></span> <span data-ttu-id="2d2e2-186">Хотя hello реплики является асинхронным, переход на другой ресурс происходит потеря данных toopotential уязвимым.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-186">While hello replica is asynchronous, failover is vulnerable toopotential data loss.</span></span> <span data-ttu-id="2d2e2-187">toofail над без потери данных, изменить toosynchronous режим доступности hello и установить режим tooautomatic hello отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-187">toofail over without data loss, change hello availability mode toosynchronous and set hello failover mode tooautomatic.</span></span> <span data-ttu-id="2d2e2-188">Используйте следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-188">Use hello following steps:</span></span>

1. <span data-ttu-id="2d2e2-189">В **обозревателя объектов**, подключитесь toohello экземпляр SQL Server, на котором размещена первичная реплика hello.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-189">In **Object Explorer**, connect toohello instance of SQL Server that hosts hello primary replica.</span></span>
1. <span data-ttu-id="2d2e2-190">Выберите **Группы доступности AlwaysOn** > **Группы доступности**, щелкните правой кнопкой мыши группу доступности и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="2d2e2-191">На hello **Общие** в разделе **реплик доступности**, набор hello вторичной реплики в hello DR сайт toouse **синхронная фиксация** режима доступности и **Автоматическое** режим отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-191">On hello **General** page, under **Availability Replicas**, set hello secondary replica in hello DR site toouse **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="2d2e2-192">Если вторичная реплика в одном узле первичную реплику для обеспечения высокой доступности, задайте эту реплику слишком**Asynchronous Commit** и **вручную**.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica too**Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="2d2e2-193">Нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-193">Click OK.</span></span>
1. <span data-ttu-id="2d2e2-194">В **обозревателя объектов**, щелкните правой кнопкой мыши группу доступности hello и нажмите кнопку **Показать панель мониторинга**.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-194">In **Object Explorer**, right-click hello availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="2d2e2-195">На панели мониторинга hello, убедитесь, что hello синхронизировать реплики на сайте hello аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-195">On hello dashboard, verify that hello replica on hello DR site is synchronized.</span></span>
1. <span data-ttu-id="2d2e2-196">В **обозревателя объектов**, щелкните правой кнопкой мыши группу доступности hello и нажмите кнопку **отработки отказа...** . Управление входящим SQL Server открывает toofail мастер с сервером SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-196">In **Object Explorer**, right-click hello availability group, and click **Failover...**. SQL Server Management Studios opens a wizard toofail over SQL Server.</span></span>  
1. <span data-ttu-id="2d2e2-197">Нажмите кнопку **Далее**и экземпляр SQL Server выберите hello в сайте hello аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-197">Click **Next**, and select hello SQL Server instance in hello DR site.</span></span> <span data-ttu-id="2d2e2-198">Нажмите **Далее** еще раз.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-198">Click **Next** again.</span></span>
1. <span data-ttu-id="2d2e2-199">Подключите toohello экземпляр SQL Server на сайте hello аварийного восстановления и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-199">Connect toohello SQL Server instance in hello DR site and click **Next**.</span></span>
1. <span data-ttu-id="2d2e2-200">На hello **Сводка** , проверьте параметры hello и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-200">On hello **Summary** page, verify hello settings and click **Finish**.</span></span>

<span data-ttu-id="2d2e2-201">После тестирования подключения, переместите hello первичная реплика задней tooyour первичных данных по центру и изменять настройки tootheir назад режим доступности hello обычной работы.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-201">After testing connectivity, move hello primary replica back tooyour primary data center and set hello availability mode back tootheir normal operating settings.</span></span> <span data-ttu-id="2d2e2-202">Hello следующей таблице показаны hello обычные параметры функционирования hello архитектуры, описанные в этом документе.</span><span class="sxs-lookup"><span data-stu-id="2d2e2-202">hello following table shows hello normal operational settings for hello architecture described in this document:</span></span>

| <span data-ttu-id="2d2e2-203">Расположение</span><span class="sxs-lookup"><span data-stu-id="2d2e2-203">Location</span></span> | <span data-ttu-id="2d2e2-204">Экземпляр сервера</span><span class="sxs-lookup"><span data-stu-id="2d2e2-204">Server Instance</span></span> | <span data-ttu-id="2d2e2-205">Роль</span><span class="sxs-lookup"><span data-stu-id="2d2e2-205">Role</span></span> | <span data-ttu-id="2d2e2-206">Режим доступности</span><span class="sxs-lookup"><span data-stu-id="2d2e2-206">Availability Mode</span></span> | <span data-ttu-id="2d2e2-207">Режим отработки отказа</span><span class="sxs-lookup"><span data-stu-id="2d2e2-207">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="2d2e2-208">Основной центр обработки данных</span><span class="sxs-lookup"><span data-stu-id="2d2e2-208">Primary data center</span></span> | <span data-ttu-id="2d2e2-209">SQL-1</span><span class="sxs-lookup"><span data-stu-id="2d2e2-209">SQL-1</span></span> | <span data-ttu-id="2d2e2-210">Первичная</span><span class="sxs-lookup"><span data-stu-id="2d2e2-210">Primary</span></span> | <span data-ttu-id="2d2e2-211">Синхронный</span><span class="sxs-lookup"><span data-stu-id="2d2e2-211">Synchronous</span></span> | <span data-ttu-id="2d2e2-212">Автоматический</span><span class="sxs-lookup"><span data-stu-id="2d2e2-212">Automatic</span></span>
| <span data-ttu-id="2d2e2-213">Основной центр обработки данных</span><span class="sxs-lookup"><span data-stu-id="2d2e2-213">Primary data center</span></span> | <span data-ttu-id="2d2e2-214">SQL-2</span><span class="sxs-lookup"><span data-stu-id="2d2e2-214">SQL-2</span></span> | <span data-ttu-id="2d2e2-215">Вторичная</span><span class="sxs-lookup"><span data-stu-id="2d2e2-215">Secondary</span></span> | <span data-ttu-id="2d2e2-216">Синхронный</span><span class="sxs-lookup"><span data-stu-id="2d2e2-216">Synchronous</span></span> | <span data-ttu-id="2d2e2-217">Автоматический</span><span class="sxs-lookup"><span data-stu-id="2d2e2-217">Automatic</span></span>
| <span data-ttu-id="2d2e2-218">Дополнительный или удаленный центр обработки данных</span><span class="sxs-lookup"><span data-stu-id="2d2e2-218">Secondary or remote data center</span></span> | <span data-ttu-id="2d2e2-219">SQL-3</span><span class="sxs-lookup"><span data-stu-id="2d2e2-219">SQL-3</span></span> | <span data-ttu-id="2d2e2-220">Вторичная</span><span class="sxs-lookup"><span data-stu-id="2d2e2-220">Secondary</span></span> | <span data-ttu-id="2d2e2-221">Асинхронный</span><span class="sxs-lookup"><span data-stu-id="2d2e2-221">Asynchronous</span></span> | <span data-ttu-id="2d2e2-222">Руководство</span><span class="sxs-lookup"><span data-stu-id="2d2e2-222">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="2d2e2-223">Дополнительные сведения о плановой и принудительной отработке отказа вручную</span><span class="sxs-lookup"><span data-stu-id="2d2e2-223">More information about planned and forced manual failover</span></span>

<span data-ttu-id="2d2e2-224">Дополнительные сведения см. в разделе hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="2d2e2-224">For more information, see hello following topics:</span></span>

- [<span data-ttu-id="2d2e2-225">Выполнение запланированного перехода на другой ресурс вручную для группы доступности (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="2d2e2-225">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="2d2e2-226">Выполнение принудительного перехода на другой ресурс вручную для группы доступности (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="2d2e2-226">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="2d2e2-227">Ссылки на дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="2d2e2-227">Additional Links</span></span>

* [<span data-ttu-id="2d2e2-228">Группы доступности Always On</span><span class="sxs-lookup"><span data-stu-id="2d2e2-228">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="2d2e2-229">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="2d2e2-229">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="2d2e2-230">Подсистемы Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="2d2e2-230">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="2d2e2-231">Группы доступности Azure</span><span class="sxs-lookup"><span data-stu-id="2d2e2-231">Azure Availability Sets</span></span>](../manage-availability.md)
