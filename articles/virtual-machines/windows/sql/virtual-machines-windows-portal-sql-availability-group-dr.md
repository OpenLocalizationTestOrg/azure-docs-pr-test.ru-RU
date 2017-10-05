---
title: "Группы доступности SQL Server, виртуальные машины Azure и аварийное восстановление | Документация Майкрософт"
description: "В этой статье описывается, как настроить группу доступности SQL Server на виртуальных машинах Azure с репликой, расположенной в другом регионе."
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
ms.openlocfilehash: 1ce90cf4bae66bfd6387a2698fd9b1ba7fc64595
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="configure-an-always-on-availability-group-on-azure-virtual-machines-in-different-regions"></a><span data-ttu-id="e1ade-103">Настройка группы доступности AlwaysOn на виртуальных машинах Azure в разных регионах</span><span class="sxs-lookup"><span data-stu-id="e1ade-103">Configure an Always On availability group on Azure virtual machines in different regions</span></span>

<span data-ttu-id="e1ade-104">В этой статье описывается, как настроить группу доступности AlwaysOn SQL Server на виртуальных машинах Azure в удаленном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ade-104">This article explains how to configure a SQL Server Always On availability group replica on Azure virtual machines in a remote Azure location.</span></span> <span data-ttu-id="e1ade-105">Эту конфигурацию можно использовать для поддержки аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="e1ade-105">Use this configuration to support disaster recovery.</span></span>

<span data-ttu-id="e1ade-106">Данная статья относится к виртуальным машинам Azure в режиме Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e1ade-106">This article applies to Azure Virtual Machines in Resource Manager mode.</span></span>

<span data-ttu-id="e1ade-107">На следующем рисунке показано типичное развертывание группы доступности на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ade-107">The following image shows a common deployment of an availability group on Azure virtual machines:</span></span>

   ![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic.png)

<span data-ttu-id="e1ade-109">В таком развертывании все виртуальные машины находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ade-109">In this deployment, all virtual machines are in one Azure region.</span></span> <span data-ttu-id="e1ade-110">Реплики группы доступности могут использовать синхронную фиксацию с автоматической отработкой отказа на SQL-1 и SQL-2.</span><span class="sxs-lookup"><span data-stu-id="e1ade-110">The availability group replicas can have synchronous commit with automatic failover on SQL-1 and SQL-2.</span></span> <span data-ttu-id="e1ade-111">Для создания этой архитектуры ознакомьтесь с [шаблоном группы доступности или соответствующим руководством](virtual-machines-windows-portal-sql-availability-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e1ade-111">To build this architecture, see [Availability Group template or tutorial](virtual-machines-windows-portal-sql-availability-group-overview.md).</span></span>

<span data-ttu-id="e1ade-112">Данная архитектура подвержена простоям в случаях, когда регион Azure становится недоступным.</span><span class="sxs-lookup"><span data-stu-id="e1ade-112">This architecture is vulnerable to downtime if the Azure region becomes inaccessible.</span></span> <span data-ttu-id="e1ade-113">Чтобы устранить эту уязвимость, добавьте реплику в другой регион Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ade-113">To overcome this vulnerability, add a replica in a different Azure region.</span></span> <span data-ttu-id="e1ade-114">На следующей схеме показано, как будет выглядеть новая архитектура.</span><span class="sxs-lookup"><span data-stu-id="e1ade-114">The following diagram shows how the new architecture would look:</span></span>

   ![Аварийное восстановление группы доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/00-availability-group-basic-dr.png)

<span data-ttu-id="e1ade-116">На предыдущей схеме показана новая виртуальная машина с именем SQL-3.</span><span class="sxs-lookup"><span data-stu-id="e1ade-116">The preceding diagram shows a new virtual machine called SQL-3.</span></span> <span data-ttu-id="e1ade-117">SQL-3 находится в другом регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ade-117">SQL-3 is in a different Azure region.</span></span> <span data-ttu-id="e1ade-118">Она добавлена в отказоустойчивый кластер Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e1ade-118">SQL-3 is added to the Windows Server Failover Cluster.</span></span> <span data-ttu-id="e1ade-119">На SQL-3 можно разместить реплику группы доступности.</span><span class="sxs-lookup"><span data-stu-id="e1ade-119">SQL-3 can host an availability group replica.</span></span> <span data-ttu-id="e1ade-120">Наконец, обратите внимание, что для региона Azure виртуальной машины SQL-3 используется новая подсистема Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e1ade-120">Finally, notice that the Azure region for SQL-3 has a new Azure load balancer.</span></span>

>[!NOTE]
> <span data-ttu-id="e1ade-121">Группа доступности Azure нужна, если в одном регионе размещено более одной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e1ade-121">An Azure availability set is required when more than one virtual machine is in the same region.</span></span> <span data-ttu-id="e1ade-122">Если в регионе находится только одна виртуальная машина, то использовать группу доступности не обязательно.</span><span class="sxs-lookup"><span data-stu-id="e1ade-122">If only one virtual machine is in the region, then the availability set is not required.</span></span> <span data-ttu-id="e1ade-123">Поместить виртуальную машину в группу доступности можно только во время создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e1ade-123">You can only place a virtual machine in an availability set at creation time.</span></span> <span data-ttu-id="e1ade-124">Если в группе доступности уже есть виртуальная машина, то позже в нее можно будет добавить виртуальную машину для размещения дополнительной реплики.</span><span class="sxs-lookup"><span data-stu-id="e1ade-124">If the virtual machine is already in an availability set, you can add a virtual machine for an additional replica later.</span></span>

<span data-ttu-id="e1ade-125">В данной архитектуре для реплики в удаленном регионе обычно настраивается режим доступности с асинхронной фиксацией и режим ручной отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e1ade-125">In this architecture, the replica in the remote region is normally configured with asynchronous commit availability mode and manual failover mode.</span></span>

<span data-ttu-id="e1ade-126">Если реплики группы доступности находятся на виртуальных машинах Azure в разных регионах Azure, то для каждого региона требуется:</span><span class="sxs-lookup"><span data-stu-id="e1ade-126">When availability group replicas are on Azure virtual machines in different Azure regions, each region requires:</span></span>

* <span data-ttu-id="e1ade-127">шлюз виртуальной сети;</span><span class="sxs-lookup"><span data-stu-id="e1ade-127">A virtual network gateway</span></span>
* <span data-ttu-id="e1ade-128">подключение к шлюзу виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e1ade-128">A virtual network gateway connection</span></span>

<span data-ttu-id="e1ade-129">На следующей схеме показано взаимодействие сетей между центрами обработки данных.</span><span class="sxs-lookup"><span data-stu-id="e1ade-129">The following diagram shows how the networks communicate between data centers.</span></span>

   ![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/01-vpngateway-example.png)

>[!IMPORTANT]
><span data-ttu-id="e1ade-131">Эта архитектура влечет за собой оплату исходящего трафика для данных, реплицируемых между регионами Azure.</span><span class="sxs-lookup"><span data-stu-id="e1ade-131">This architecture incurs outbound data charges for data replicated between Azure regions.</span></span> <span data-ttu-id="e1ade-132">Ознакомьтесь с разделом [Сведения о стоимости пропускной способности](http://azure.microsoft.com/pricing/details/bandwidth/).</span><span class="sxs-lookup"><span data-stu-id="e1ade-132">See [Bandwidth Pricing](http://azure.microsoft.com/pricing/details/bandwidth/).</span></span>  

## <a name="create-remote-replica"></a><span data-ttu-id="e1ade-133">Создание удаленной реплики</span><span class="sxs-lookup"><span data-stu-id="e1ade-133">Create remote replica</span></span>

<span data-ttu-id="e1ade-134">Чтобы создать реплику в удаленном центре обработки данных, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e1ade-134">To create a replica in a remote data center, do the following steps:</span></span>

1. <span data-ttu-id="e1ade-135">[Создайте виртуальную сеть в новом регионе](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="e1ade-135">[Create a virtual network in the new region](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

1. <span data-ttu-id="e1ade-136">[Настройте подключение между виртуальными сетями на портале Azure](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e1ade-136">[Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span></span>

   >[!NOTE]
   ><span data-ttu-id="e1ade-137">В некоторых случаях для создания подключения между виртуальными сетями может потребоваться использовать PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e1ade-137">In some cases, you may have to use PowerShell to create the VNet-to-VNet connection.</span></span> <span data-ttu-id="e1ade-138">Например, при использовании разных учетных записей Azure подключение невозможно настроить на портале.</span><span class="sxs-lookup"><span data-stu-id="e1ade-138">For example, if you use different Azure accounts you cannot configure the connection in the portal.</span></span> <span data-ttu-id="e1ade-139">В этом случае ознакомьтесь с разделом [Настройка подключения между виртуальными сетями на портале Azure](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e1ade-139">In this case see, [Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

1. <span data-ttu-id="e1ade-140">[Создайте контроллер домена в новом регионе](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="e1ade-140">[Create a domain controller in the new region](../../../active-directory/active-directory-new-forest-virtual-machine.md).</span></span>

   <span data-ttu-id="e1ade-141">Этот контроллер домена обеспечивает аутентификацию в случае, если контроллер домена на первичном сайте недоступен.</span><span class="sxs-lookup"><span data-stu-id="e1ade-141">This domain controller provides authentication if the domain controller in the primary site is not available.</span></span>

1. <span data-ttu-id="e1ade-142">[Создайте виртуальную машину SQL Server в новом регионе](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e1ade-142">[Create a SQL Server virtual machine in the new region](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

1. <span data-ttu-id="e1ade-143">[Создайте Azure Load Balancer в сети в новом регионе](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="e1ade-143">[Create an Azure load balancer in the network on the new region](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

   <span data-ttu-id="e1ade-144">Эта подсистема балансировки нагрузки должна:</span><span class="sxs-lookup"><span data-stu-id="e1ade-144">This load balancer must:</span></span>

   - <span data-ttu-id="e1ade-145">находиться в той же сети и подсети, что и новая виртуальная машина;</span><span class="sxs-lookup"><span data-stu-id="e1ade-145">Be in the same network and subnet as the new virtual machine.</span></span>
   - <span data-ttu-id="e1ade-146">использовать статический IP-адрес для прослушивателя группы доступности;</span><span class="sxs-lookup"><span data-stu-id="e1ade-146">Have a static IP address for the availability group listener.</span></span>
   - <span data-ttu-id="e1ade-147">включать в себя внутренний пул, состоящий только из виртуальных машин, размещенных в том же регионе, что и подсистема балансировки нагрузки;</span><span class="sxs-lookup"><span data-stu-id="e1ade-147">Include a backend pool consisting of only the virtual machines in the same region as the load balancer.</span></span>
   - <span data-ttu-id="e1ade-148">использовать пробу TCP-порта для IP-адреса;</span><span class="sxs-lookup"><span data-stu-id="e1ade-148">Use a TCP port probe specific to the IP address.</span></span>
   - <span data-ttu-id="e1ade-149">использовать правило балансировки нагрузки для SQL Server в том же регионе.</span><span class="sxs-lookup"><span data-stu-id="e1ade-149">Have a load balancing rule specific to the SQL Server in the same region.</span></span>  

1. <span data-ttu-id="e1ade-150">[Добавьте компонент отказоустойчивой кластеризации на новый сервер SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="e1ade-150">[Add Failover Clustering feature to the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

1. <span data-ttu-id="e1ade-151">[Присоедините новый сервер SQL Server к домену](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="e1ade-151">[Join the new SQL Server to the domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

1. <span data-ttu-id="e1ade-152">[Настройте новую учетную запись службы SQL Server для использования доменной учетной записи](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span><span class="sxs-lookup"><span data-stu-id="e1ade-152">[Set the new SQL Server service account to use a domain account](virtual-machines-windows-portal-sql-availability-group-prereq.md#setServiceAccount).</span></span>

1. <span data-ttu-id="e1ade-153">[Добавьте новый сервер SQL Server в отказоустойчивый кластер Windows Server](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span><span class="sxs-lookup"><span data-stu-id="e1ade-153">[Add the new SQL Server to the Windows Server Failover Cluster](virtual-machines-windows-portal-sql-availability-group-tutorial.md#addNode).</span></span>

1. <span data-ttu-id="e1ade-154">Создайте ресурс IP-адреса в кластере.</span><span class="sxs-lookup"><span data-stu-id="e1ade-154">Create an IP address resource on the cluster.</span></span>

   <span data-ttu-id="e1ade-155">Для этого можно использовать диспетчер отказоустойчивости кластеров.</span><span class="sxs-lookup"><span data-stu-id="e1ade-155">You can create the IP address resource in Failover Cluster Manager.</span></span> <span data-ttu-id="e1ade-156">Щелкните правой кнопкой мыши роль группы доступности и выберите **Добавить ресурс**, **Дополнительные ресурсы**, затем щелкните **IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="e1ade-156">Right-click the availability group role, click **Add Resource**, **More Resources**, and click **IP Address**.</span></span>

   ![Создание IP-адреса](./media/virtual-machines-windows-portal-sql-availability-group-dr/20-add-ip-resource.png)

   <span data-ttu-id="e1ade-158">Настройте этот IP-адрес следующим образом.</span><span class="sxs-lookup"><span data-stu-id="e1ade-158">Configure this IP address as follows:</span></span>

   - <span data-ttu-id="e1ade-159">Используйте сеть удаленного центра обработки данных.</span><span class="sxs-lookup"><span data-stu-id="e1ade-159">Use the network from the remote data center.</span></span>
   - <span data-ttu-id="e1ade-160">Назначьте IP-адрес из новой подсистемы Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e1ade-160">Assign the IP address from the new Azure load balancer.</span></span> 

1. <span data-ttu-id="e1ade-161">[Включите группы доступности AlwaysOn](http://msdn.microsoft.com/library/ff878259.aspx) на новом сервере SQL Server с помощью диспетчера конфигурации SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e1ade-161">On the new SQL Server in SQL Server Configuration Manager, [enable Always On Availability Groups](http://msdn.microsoft.com/library/ff878259.aspx).</span></span>

1. <span data-ttu-id="e1ade-162">[Откройте порты брандмауэра на новом сервере SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span><span class="sxs-lookup"><span data-stu-id="e1ade-162">[Open firewall ports on the new SQL Server](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).</span></span>

   <span data-ttu-id="e1ade-163">Номера портов, которые необходимо открыть, зависят от вашей среды.</span><span class="sxs-lookup"><span data-stu-id="e1ade-163">The port numbers you need to open depend on your environment.</span></span> <span data-ttu-id="e1ade-164">Откройте порты для конечной точки зеркального отображения и пробы работоспособности Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="e1ade-164">Open ports for the mirroring endpoint and Azure load balancer health probe.</span></span>

1. <span data-ttu-id="e1ade-165">[Добавьте реплику в группу доступности на новом сервере SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1ade-165">[Add a replica to the availability group on the new SQL Server](http://msdn.microsoft.com/library/hh213239.aspx).</span></span>

   <span data-ttu-id="e1ade-166">Для реплики в удаленном регионе Azure настройте асинхронную репликацию с ручной отработкой отказа.</span><span class="sxs-lookup"><span data-stu-id="e1ade-166">For a replica in a remote Azure region, set it for asynchronous replication with manual failover.</span></span>  

1. <span data-ttu-id="e1ade-167">Добавьте ресурс IP-адреса в качестве зависимости для кластера (сетевое имя) точки доступа клиента прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="e1ade-167">Add the IP address resource as a dependency for the listener client access point (network name) cluster.</span></span>

   <span data-ttu-id="e1ade-168">На следующем рисунке показан правильно настроенного ресурс IP-адреса кластера.</span><span class="sxs-lookup"><span data-stu-id="e1ade-168">The following screenshot shows a properly configured IP address cluster resource:</span></span>

   ![Группа доступности](./media/virtual-machines-windows-portal-sql-availability-group-dr/50-configure-dependency-multiple-ip.png)

   >[!IMPORTANT]
   ><span data-ttu-id="e1ade-170">Группа ресурсов кластера включает в себя оба IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="e1ade-170">The cluster resource group includes both IP addresses.</span></span> <span data-ttu-id="e1ade-171">Оба IP-адреса являются зависимостями для точки доступа клиента прослушивателя.</span><span class="sxs-lookup"><span data-stu-id="e1ade-171">Both IP addresses are dependencies for the listener client access point.</span></span> <span data-ttu-id="e1ade-172">Используйте оператор **OR** в конфигурации зависимостей кластера.</span><span class="sxs-lookup"><span data-stu-id="e1ade-172">Use the **OR** operator in the cluster dependency configuration.</span></span>

1. <span data-ttu-id="e1ade-173">[Настройте параметры кластера в PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span><span class="sxs-lookup"><span data-stu-id="e1ade-173">[Set the cluster parameters in PowerShell](virtual-machines-windows-portal-sql-availability-group-tutorial.md#setparam).</span></span>

<span data-ttu-id="e1ade-174">Выполните сценарий PowerShell с сетевым именем кластера, IP-адресом и портом пробы, настроенными для подсистемы балансировки нагрузки в новом регионе.</span><span class="sxs-lookup"><span data-stu-id="e1ade-174">Run the PowerShell script with the cluster network name, IP address, and probe port that you configured on the load balancer in the new region.</span></span>

   ```PowerShell
   $ClusterNetworkName = "<MyClusterNetworkName>" # The cluster name for the network in the new region (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "<IPResourceName>" # The cluster name for the new IP Address resource.
   $ILBIP = “<n.n.n.n>” # The IP Address of the Internal Load Balancer (ILB) in the new region. This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <nnnnn> # The probe port you set on the ILB.

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```

## <a name="set-connection-for-multiple-subnets"></a><span data-ttu-id="e1ade-175">Настройка подключения для нескольких подсетей</span><span class="sxs-lookup"><span data-stu-id="e1ade-175">Set connection for multiple subnets</span></span>

<span data-ttu-id="e1ade-176">Реплика в удаленном центре обработки данных входит в группу доступности, но находится в другой подсети.</span><span class="sxs-lookup"><span data-stu-id="e1ade-176">The replica in the remote data center is part of the availability group but it is in a different subnet.</span></span> <span data-ttu-id="e1ade-177">Если это реплика станет первичной, то возможно превышение времени ожидания подключения к приложению.</span><span class="sxs-lookup"><span data-stu-id="e1ade-177">If this replica becomes the primary replica, application connection time-outs may occur.</span></span> <span data-ttu-id="e1ade-178">Точно так же работает локальная группа доступности в развертывании с несколькими подсетями.</span><span class="sxs-lookup"><span data-stu-id="e1ade-178">This behavior is the same as an on-premises availability group in a multi-subnet deployment.</span></span> <span data-ttu-id="e1ade-179">Чтобы разрешить подключения из клиентских приложений, либо измените подключение клиента, либо настройте кэширование разрешения имен для ресурса сетевого имени кластера.</span><span class="sxs-lookup"><span data-stu-id="e1ade-179">To allow connections from client applications, either update the client connection or configure name resolution caching on the cluster network name resource.</span></span>

<span data-ttu-id="e1ade-180">Желательно изменить строки подключения клиента, чтобы задать `MultiSubnetFailover=Yes`.</span><span class="sxs-lookup"><span data-stu-id="e1ade-180">Preferably, update the client connection strings to set `MultiSubnetFailover=Yes`.</span></span> <span data-ttu-id="e1ade-181">Ознакомьтесь с разделом [Соединение с помощью MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="e1ade-181">See [Connecting With MultiSubnetFailover](http://msdn.microsoft.com/library/gg471494#Anchor_0).</span></span>

<span data-ttu-id="e1ade-182">Если вам не удается изменить строки подключения, можно настроить кэширование разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="e1ade-182">If you cannot modify the connection strings, you can configure name resolution caching.</span></span> <span data-ttu-id="e1ade-183">Ознакомьтесь с разделом [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/) (Время ожидания подключения в группе доступности с несколькими подсетями).</span><span class="sxs-lookup"><span data-stu-id="e1ade-183">See [Connection Timeouts in Multi-subnet Availability Group](http://blogs.msdn.microsoft.com/alwaysonpro/2014/06/03/connection-timeouts-in-multi-subnet-availability-group/).</span></span>

## <a name="fail-over-to-remote-region"></a><span data-ttu-id="e1ade-184">Отработка отказа в удаленный регион</span><span class="sxs-lookup"><span data-stu-id="e1ade-184">Fail over to remote region</span></span>

<span data-ttu-id="e1ade-185">Чтобы проверить возможность подключения прослушивателя к удаленному региону, можно отработать отказ реплики в удаленный регион.</span><span class="sxs-lookup"><span data-stu-id="e1ade-185">To test listener connectivity to the remote region, you can fail over the replica to the remote region.</span></span> <span data-ttu-id="e1ade-186">Если реплика является асинхронной, то отработка отказа может привести к потере данных.</span><span class="sxs-lookup"><span data-stu-id="e1ade-186">While the replica is asynchronous, failover is vulnerable to potential data loss.</span></span> <span data-ttu-id="e1ade-187">Чтобы отработать отказ без потери данных, измените режим доступности на синхронный и задайте автоматический режим отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e1ade-187">To fail over without data loss, change the availability mode to synchronous and set the failover mode to automatic.</span></span> <span data-ttu-id="e1ade-188">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e1ade-188">Use the following steps:</span></span>

1. <span data-ttu-id="e1ade-189">В **обозревателе объектов** подключитесь к экземпляру SQL Server, на котором размещена первичная реплика.</span><span class="sxs-lookup"><span data-stu-id="e1ade-189">In **Object Explorer**, connect to the instance of SQL Server that hosts the primary replica.</span></span>
1. <span data-ttu-id="e1ade-190">Выберите **Группы доступности AlwaysOn** > **Группы доступности**, щелкните правой кнопкой мыши группу доступности и выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="e1ade-190">Under **AlwaysOn Availability Groups**, **Availability Groups**, right-click your availability group and click **Properties**.</span></span>
1. <span data-ttu-id="e1ade-191">На странице **Общие** в разделе **Реплики доступности** задайте для вторичной реплики на узле аварийного восстановления режим доступности **Синхронная фиксация** и **автоматический** режим отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e1ade-191">On the **General** page, under **Availability Replicas**, set the secondary replica in the DR site to use **Synchronous Commit** availability mode and **Automatic** failover mode.</span></span>
1. <span data-ttu-id="e1ade-192">Если вторичная реплика находится на том же узле, что и первичная реплика, для обеспечения высокого уровня доступности, то задайте для нее режимы **Асинхронная фиксация** и **Ручной**.</span><span class="sxs-lookup"><span data-stu-id="e1ade-192">If you have a secondary replica in same site as your primary replica for high availability, set this replica to **Asynchronous Commit** and **Manual**.</span></span>
1. <span data-ttu-id="e1ade-193">Нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="e1ade-193">Click OK.</span></span>
1. <span data-ttu-id="e1ade-194">В **обозревателе объектов** щелкните правой кнопкой мыши группу доступности и выберите **Show Dashboard** (Показать панель мониторинга).</span><span class="sxs-lookup"><span data-stu-id="e1ade-194">In **Object Explorer**, right-click the availability group, and click **Show Dashboard**.</span></span>
1. <span data-ttu-id="e1ade-195">На панели мониторинга убедитесь, что реплика на сайте аварийного восстановления синхронизирована.</span><span class="sxs-lookup"><span data-stu-id="e1ade-195">On the dashboard, verify that the replica on the DR site is synchronized.</span></span>
1. <span data-ttu-id="e1ade-196">В **обозревателе объектов** щелкните правой кнопкой мыши группу доступности и выберите **Отработка отказа…**.</span><span class="sxs-lookup"><span data-stu-id="e1ade-196">In **Object Explorer**, right-click the availability group, and click **Failover...**.</span></span> <span data-ttu-id="e1ade-197">В SQL Server Management Studio откроется мастер для отработки отказа SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e1ade-197">SQL Server Management Studios opens a wizard to fail over SQL Server.</span></span>  
1. <span data-ttu-id="e1ade-198">Щелкните **Далее** и выберите экземпляр SQL Server на сайте аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="e1ade-198">Click **Next**, and select the SQL Server instance in the DR site.</span></span> <span data-ttu-id="e1ade-199">Нажмите **Далее** еще раз.</span><span class="sxs-lookup"><span data-stu-id="e1ade-199">Click **Next** again.</span></span>
1. <span data-ttu-id="e1ade-200">Подключитесь к экземпляру SQL Server на сайте аварийного восстановления и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e1ade-200">Connect to the SQL Server instance in the DR site and click **Next**.</span></span>
1. <span data-ttu-id="e1ade-201">Проверьте параметры на странице **Сводка**, а затем нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="e1ade-201">On the **Summary** page, verify the settings and click **Finish**.</span></span>

<span data-ttu-id="e1ade-202">После проверки подключения верните первичную реплику в основной центр обработки данных и восстановите обычные рабочие параметры режима доступности.</span><span class="sxs-lookup"><span data-stu-id="e1ade-202">After testing connectivity, move the primary replica back to your primary data center and set the availability mode back to their normal operating settings.</span></span> <span data-ttu-id="e1ade-203">В таблице ниже приведены обычные рабочие параметры для архитектуры, описанной в этом документе.</span><span class="sxs-lookup"><span data-stu-id="e1ade-203">The following table shows the normal operational settings for the architecture described in this document:</span></span>

| <span data-ttu-id="e1ade-204">Расположение</span><span class="sxs-lookup"><span data-stu-id="e1ade-204">Location</span></span> | <span data-ttu-id="e1ade-205">Экземпляр сервера</span><span class="sxs-lookup"><span data-stu-id="e1ade-205">Server Instance</span></span> | <span data-ttu-id="e1ade-206">Роль</span><span class="sxs-lookup"><span data-stu-id="e1ade-206">Role</span></span> | <span data-ttu-id="e1ade-207">Режим доступности</span><span class="sxs-lookup"><span data-stu-id="e1ade-207">Availability Mode</span></span> | <span data-ttu-id="e1ade-208">Режим отработки отказа</span><span class="sxs-lookup"><span data-stu-id="e1ade-208">Failover Mode</span></span>
| ----- | ----- | ----- | ----- | -----
| <span data-ttu-id="e1ade-209">Основной центр обработки данных</span><span class="sxs-lookup"><span data-stu-id="e1ade-209">Primary data center</span></span> | <span data-ttu-id="e1ade-210">SQL-1</span><span class="sxs-lookup"><span data-stu-id="e1ade-210">SQL-1</span></span> | <span data-ttu-id="e1ade-211">Первичная</span><span class="sxs-lookup"><span data-stu-id="e1ade-211">Primary</span></span> | <span data-ttu-id="e1ade-212">Синхронный</span><span class="sxs-lookup"><span data-stu-id="e1ade-212">Synchronous</span></span> | <span data-ttu-id="e1ade-213">Автоматический</span><span class="sxs-lookup"><span data-stu-id="e1ade-213">Automatic</span></span>
| <span data-ttu-id="e1ade-214">Основной центр обработки данных</span><span class="sxs-lookup"><span data-stu-id="e1ade-214">Primary data center</span></span> | <span data-ttu-id="e1ade-215">SQL-2</span><span class="sxs-lookup"><span data-stu-id="e1ade-215">SQL-2</span></span> | <span data-ttu-id="e1ade-216">Вторичная</span><span class="sxs-lookup"><span data-stu-id="e1ade-216">Secondary</span></span> | <span data-ttu-id="e1ade-217">Синхронный</span><span class="sxs-lookup"><span data-stu-id="e1ade-217">Synchronous</span></span> | <span data-ttu-id="e1ade-218">Автоматический</span><span class="sxs-lookup"><span data-stu-id="e1ade-218">Automatic</span></span>
| <span data-ttu-id="e1ade-219">Дополнительный или удаленный центр обработки данных</span><span class="sxs-lookup"><span data-stu-id="e1ade-219">Secondary or remote data center</span></span> | <span data-ttu-id="e1ade-220">SQL-3</span><span class="sxs-lookup"><span data-stu-id="e1ade-220">SQL-3</span></span> | <span data-ttu-id="e1ade-221">Вторичная</span><span class="sxs-lookup"><span data-stu-id="e1ade-221">Secondary</span></span> | <span data-ttu-id="e1ade-222">Асинхронный</span><span class="sxs-lookup"><span data-stu-id="e1ade-222">Asynchronous</span></span> | <span data-ttu-id="e1ade-223">Руководство</span><span class="sxs-lookup"><span data-stu-id="e1ade-223">Manual</span></span>


### <a name="more-information-about-planned-and-forced-manual-failover"></a><span data-ttu-id="e1ade-224">Дополнительные сведения о плановой и принудительной отработке отказа вручную</span><span class="sxs-lookup"><span data-stu-id="e1ade-224">More information about planned and forced manual failover</span></span>

<span data-ttu-id="e1ade-225">Дополнительные сведения см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="e1ade-225">For more information, see the following topics:</span></span>

- [<span data-ttu-id="e1ade-226">Выполнение запланированного перехода на другой ресурс вручную для группы доступности (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="e1ade-226">Perform a Planned Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/hh231018.aspx)
- [<span data-ttu-id="e1ade-227">Выполнение принудительного перехода на другой ресурс вручную для группы доступности (SQL Server)</span><span class="sxs-lookup"><span data-stu-id="e1ade-227">Perform a Forced Manual Failover of an Availability Group (SQL Server)</span></span>](http://msdn.microsoft.com/library/ff877957.aspx)

## <a name="additional-links"></a><span data-ttu-id="e1ade-228">Ссылки на дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e1ade-228">Additional Links</span></span>

* [<span data-ttu-id="e1ade-229">Группы доступности Always On</span><span class="sxs-lookup"><span data-stu-id="e1ade-229">Always On Availability Groups</span></span>](http://msdn.microsoft.com/library/hh510230.aspx)
* [<span data-ttu-id="e1ade-230">Виртуальные машины Azure</span><span class="sxs-lookup"><span data-stu-id="e1ade-230">Azure Virtual Machines</span></span>](http://docs.microsoft.com/azure/virtual-machines/windows/)
* [<span data-ttu-id="e1ade-231">Подсистемы Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e1ade-231">Azure Load Balancers</span></span>](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer)
* [<span data-ttu-id="e1ade-232">Группы доступности Azure</span><span class="sxs-lookup"><span data-stu-id="e1ade-232">Azure Availability Sets</span></span>](../manage-availability.md)
