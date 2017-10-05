---
title: "Экземпляр отказоустойчивого кластера SQL Server на виртуальных машинах Azure | Документация Майкрософт"
description: "В этой статье объясняется, как создать экземпляр отказоустойчивого кластера SQL Server на виртуальных машинах Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 9fc761b1-21ad-4d79-bebc-a2f094ec214d
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 439353b7d22fb7376049ea8e1433a8d5840d3e0f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="96347-103">Настройка экземпляра отказоустойчивого кластера SQL Server на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="96347-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="96347-104">В этой статье объясняется, как создать экземпляр отказоустойчивого кластера SQL Server на виртуальных машинах Azure в модели Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="96347-104">This article explains how to create a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="96347-105">В этом решении [локальные дисковые пространства Windows Server 2016 Datacenter Edition \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) используются в качестве программной виртуальной сети SAN, синхронизирующей хранилище (диски с данными) между узлами (виртуальные машины Azure) в кластере Windows.</span><span class="sxs-lookup"><span data-stu-id="96347-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes the storage (data disks) between the nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="96347-106">S2D — это новшество в Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="96347-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="96347-107">На следующей схеме показано полное решение на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="96347-107">The following diagram shows the complete solution on Azure virtual machines:</span></span>

![Группа доступности](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="96347-109">На предыдущей схеме показано следующее:</span><span class="sxs-lookup"><span data-stu-id="96347-109">The preceding diagram shows:</span></span>

- <span data-ttu-id="96347-110">Две виртуальные машины Azure в отказоустойчивом кластере Windows.</span><span class="sxs-lookup"><span data-stu-id="96347-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="96347-111">Когда виртуальная машина находится в отказоустойчивом кластере, она также называется *узлом кластера* или просто *узлом*.</span><span class="sxs-lookup"><span data-stu-id="96347-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="96347-112">В каждой виртуальной машине есть два или больше дисков данных.</span><span class="sxs-lookup"><span data-stu-id="96347-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="96347-113">S2D синхронизирует данные на диске данных и представляет синхронизированное хранилище в качестве пула носителей.</span><span class="sxs-lookup"><span data-stu-id="96347-113">S2D synchronizes the data on the data disk and presents the synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="96347-114">Пул носителей представляет общий том кластера (CSV) для отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-114">The storage pool presents a cluster shared volume (CSV) to the failover cluster.</span></span>
- <span data-ttu-id="96347-115">Роль экземпляра кластера SQL Server FCI использует CSV для дисков данных.</span><span class="sxs-lookup"><span data-stu-id="96347-115">The SQL Server FCI cluster role uses the CSV for the data drives.</span></span>
- <span data-ttu-id="96347-116">Azure Load Balancer для хранения IP-адреса для экземпляра отказоустойчивого кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-116">An Azure load balancer to hold the IP address for the SQL Server FCI.</span></span>
- <span data-ttu-id="96347-117">В группе доступности Azure хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="96347-117">An Azure availability set holds all the resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="96347-118">Все ресурсы Azure, представленные на схеме, находятся в одной и той же группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="96347-118">All Azure resources are in the diagram are in the same resource group.</span></span>

<span data-ttu-id="96347-119">[Дополнительные сведения о \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) см. в статье Локальные дисковые пространства в Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="96347-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="96347-120">S2D поддерживает два типа архитектуры — конвергентную и гиперконвергентную.</span><span class="sxs-lookup"><span data-stu-id="96347-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="96347-121">В этом документе используется гиперконвергентная архитектура.</span><span class="sxs-lookup"><span data-stu-id="96347-121">The architecture in this document is hyper-converged.</span></span> <span data-ttu-id="96347-122">Гиперконвергентная инфраструктура размещает хранилище на тех же серверах, на которых размещено кластеризованное приложение.</span><span class="sxs-lookup"><span data-stu-id="96347-122">A hyper-converged infrastructure places the storage on the same servers that host the clustered application.</span></span> <span data-ttu-id="96347-123">В этой архитектуре хранилище находится на каждом узле экземпляра отказоустойчивого кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-123">In this architecture, the storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="96347-124">Пример шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="96347-124">Example Azure template</span></span>

<span data-ttu-id="96347-125">На основе шаблона в Azure можно создать полное решение.</span><span class="sxs-lookup"><span data-stu-id="96347-125">You can create the entire solution in Azure from a template.</span></span> <span data-ttu-id="96347-126">Пример шаблона доступен в [шаблонах быстрого запуска Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad) на GitHub.</span><span class="sxs-lookup"><span data-stu-id="96347-126">An example of a template is available in the GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="96347-127">Этот пример не предназначен или протестирован для какой-либо конкретной рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="96347-128">Вы можете запустить шаблон, чтобы создать экземпляр отказоустойчивого кластера SQL Server с хранилищем S2D, подключенным к вашему домену.</span><span class="sxs-lookup"><span data-stu-id="96347-128">You can run the template to create a SQL Server FCI with S2D storage connected to your domain.</span></span> <span data-ttu-id="96347-129">Шаблон можно оценить и изменить в соответствии со своими потребностями.</span><span class="sxs-lookup"><span data-stu-id="96347-129">You can evaluate the template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="96347-130">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="96347-130">Before you begin</span></span>

<span data-ttu-id="96347-131">Прежде чем продолжить, необходимо разобраться с некоторыми моментами и настроить несколько компонентов.</span><span class="sxs-lookup"><span data-stu-id="96347-131">There are a few things you need to know and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-to-know"></a><span data-ttu-id="96347-132">Необходимые знания</span><span class="sxs-lookup"><span data-stu-id="96347-132">What to know</span></span>
<span data-ttu-id="96347-133">Вам необходимо иметь представление о следующих технологиях:</span><span class="sxs-lookup"><span data-stu-id="96347-133">You should have an operational understanding of the following technologies:</span></span>

- <span data-ttu-id="96347-134">[технологии кластера под управлением Windows](http://technet.microsoft.com/library/hh831579.aspx);</span><span class="sxs-lookup"><span data-stu-id="96347-134">[Windows cluster technologies](http://technet.microsoft.com/library/hh831579.aspx)</span></span>
-  <span data-ttu-id="96347-135">[экземпляры отказоустойчивого кластера SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="96347-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="96347-136">Вам также необходимо иметь общее представление о следующих технологиях:</span><span class="sxs-lookup"><span data-stu-id="96347-136">Also, you should have a general understanding of the following technologies:</span></span>

- <span data-ttu-id="96347-137">[гиперконвергентное решение, использующее локальные дисковые пространства в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct);</span><span class="sxs-lookup"><span data-stu-id="96347-137">[Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)</span></span>
- <span data-ttu-id="96347-138">[группы ресурсов Azure](../../../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="96347-138">[Azure resource groups](../../../azure-resource-manager/resource-group-portal.md)</span></span>

### <a name="what-to-have"></a><span data-ttu-id="96347-139">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="96347-139">What to have</span></span>

<span data-ttu-id="96347-140">Перед выполнением инструкций, приведенных в данной статье, вам необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="96347-140">Before following the instructions in this article, you should already have:</span></span>

- <span data-ttu-id="96347-141">подписка Microsoft Azure;</span><span class="sxs-lookup"><span data-stu-id="96347-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="96347-142">домен Windows на виртуальных машинах Azure;</span><span class="sxs-lookup"><span data-stu-id="96347-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="96347-143">учетная запись с разрешением на создание объектов в виртуальной машине Azure;</span><span class="sxs-lookup"><span data-stu-id="96347-143">An account with permission to create objects in the Azure virtual machine.</span></span>
- <span data-ttu-id="96347-144">виртуальная сеть и подсеть Azure с достаточным пространством IP-адресов для следующих компонентов:</span><span class="sxs-lookup"><span data-stu-id="96347-144">An Azure virtual network and subnet with sufficient IP address space for the following components:</span></span>
   - <span data-ttu-id="96347-145">обе виртуальные машины;</span><span class="sxs-lookup"><span data-stu-id="96347-145">Both virtual machines.</span></span>
   - <span data-ttu-id="96347-146">IP-адрес отказоустойчивого кластера;</span><span class="sxs-lookup"><span data-stu-id="96347-146">The failover cluster IP address.</span></span>
   - <span data-ttu-id="96347-147">IP-адрес для каждого экземпляра отказоустойчивого кластера;</span><span class="sxs-lookup"><span data-stu-id="96347-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="96347-148">служба DNS, настроенная в сети Azure, указывающей на контроллеры домена.</span><span class="sxs-lookup"><span data-stu-id="96347-148">DNS configured on the Azure Network, pointing to the domain controllers.</span></span>

<span data-ttu-id="96347-149">После выполнения этих предварительных требований можно продолжить создание отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="96347-150">Сначала нужно создать виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="96347-150">The first step is to create the virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="96347-151">Шаг 1. Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="96347-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="96347-152">Войдите на [портал Azure](http://portal.azure.com) с использованием своей подписки.</span><span class="sxs-lookup"><span data-stu-id="96347-152">Log in to the [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="96347-153">[Создайте группу доступности Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="96347-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="96347-154">Группа доступности группирует виртуальные машины в доменах сбоя и доменах обновления.</span><span class="sxs-lookup"><span data-stu-id="96347-154">The availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="96347-155">Она позволяет гарантировать, что на ваше приложение не повлияют отдельные неисправные точки, такие как сетевой коммутатор или блок питания стойки серверов.</span><span class="sxs-lookup"><span data-stu-id="96347-155">The availability set makes sure that your application is not affected by single points of failure, like the network switch or the power unit of a rack of servers.</span></span>

   <span data-ttu-id="96347-156">Если вы не создали группу ресурсов для виртуальных машин, сделайте это во время создания группы доступности Azure.</span><span class="sxs-lookup"><span data-stu-id="96347-156">If you have not created the resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="96347-157">Если вы используете портал Azure для создания группы доступности, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="96347-157">If you're using the Azure portal to create the availability set, do the following steps:</span></span>

   - <span data-ttu-id="96347-158">На портале Azure щелкните **+**, чтобы открыть Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="96347-158">In the Azure portal, click **+** to open the Azure Marketplace.</span></span> <span data-ttu-id="96347-159">Найдите **Группа доступности**.</span><span class="sxs-lookup"><span data-stu-id="96347-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="96347-160">Выберите **Группа доступности**.</span><span class="sxs-lookup"><span data-stu-id="96347-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="96347-161">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="96347-161">Click **Create**.</span></span>
   - <span data-ttu-id="96347-162">В колонке **Создание группы доступности** установите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="96347-162">On the **Create availability set** blade, set the following values:</span></span>
      - <span data-ttu-id="96347-163">**Имя.** Имя группы доступности.</span><span class="sxs-lookup"><span data-stu-id="96347-163">**Name**: A name for the availability set.</span></span>
      - <span data-ttu-id="96347-164">**Подписка.** Ваша подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="96347-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="96347-165">**Группа ресурсов.** Если вы хотите использовать имеющуюся группу, выберите **Использовать существующий** и выберите группу из раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="96347-165">**Resource group**: If you want to use an existing group, click **Use existing** and select the group from the drop-down list.</span></span> <span data-ttu-id="96347-166">В противном случае выберите **Создать** и введите имя для группы.</span><span class="sxs-lookup"><span data-stu-id="96347-166">Otherwise choose **Create New** and type a name for the group.</span></span>
      - <span data-ttu-id="96347-167">**Расположение.** Задайте расположение, в котором вы планируете создать виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="96347-167">**Location**: Set the location where you plan to create your virtual machines.</span></span>
      - <span data-ttu-id="96347-168">**Домены сбоя.** Используйте значение по умолчанию (3).</span><span class="sxs-lookup"><span data-stu-id="96347-168">**Fault domains**: Use the default (3).</span></span>
      - <span data-ttu-id="96347-169">**Домены обновления.** Используйте значение по умолчанию (5).</span><span class="sxs-lookup"><span data-stu-id="96347-169">**Update domains**: Use the default (5).</span></span>
   - <span data-ttu-id="96347-170">Щелкните **Создать**, чтобы создать группу доступности.</span><span class="sxs-lookup"><span data-stu-id="96347-170">Click **Create** to create the availability set.</span></span>

1. <span data-ttu-id="96347-171">Создайте виртуальные машины в группе доступности.</span><span class="sxs-lookup"><span data-stu-id="96347-171">Create the virtual machines in the availability set.</span></span>

   <span data-ttu-id="96347-172">Подготовьте две виртуальные машины SQL Server в группе доступности Azure.</span><span class="sxs-lookup"><span data-stu-id="96347-172">Provision two SQL Server virtual machines in the Azure availability set.</span></span> <span data-ttu-id="96347-173">Инструкции см. в статье [Подготовка виртуальной машины SQL Server на портале Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="96347-173">For instructions, see [Provision a SQL Server virtual machine in the Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="96347-174">Разместите обе виртуальные машины:</span><span class="sxs-lookup"><span data-stu-id="96347-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="96347-175">в той же группе ресурсов Azure, что и группа доступности;</span><span class="sxs-lookup"><span data-stu-id="96347-175">In the same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="96347-176">в той же сети, что и контроллер домена;</span><span class="sxs-lookup"><span data-stu-id="96347-176">On the same network as your domain controller.</span></span>
   - <span data-ttu-id="96347-177">в подсети с достаточным пространством IP-адресов для обеих виртуальных машин и всех экземпляров отказоустойчивого кластера, которые со временем могут использоваться в этом кластере;</span><span class="sxs-lookup"><span data-stu-id="96347-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="96347-178">в группе доступности Azure.</span><span class="sxs-lookup"><span data-stu-id="96347-178">In the Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="96347-179">После создания виртуальной машины установить или изменить группу доступности невозможно.</span><span class="sxs-lookup"><span data-stu-id="96347-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="96347-180">Выберите образ из Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="96347-180">Choose an image from the Azure Marketplace.</span></span> <span data-ttu-id="96347-181">Вы можете использовать образ Marketplace с образом, который включает Windows Server и SQL Server или просто Windows Server.</span><span class="sxs-lookup"><span data-stu-id="96347-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just the Windows Server.</span></span> <span data-ttu-id="96347-182">Дополнительные сведения см. в статье [Приступая к работе с SQL Server в виртуальных машинах Azure](../../virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="96347-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="96347-183">Официальные образы SQL Server в коллекции Azure содержат установленный экземпляр SQL Server, а также программное обеспечение для установки SQL Server и необходимый ключ.</span><span class="sxs-lookup"><span data-stu-id="96347-183">The official SQL Server images in the Azure Gallery include an installed SQL Server instance, plus the SQL Server installation software, and the required key.</span></span>

   <span data-ttu-id="96347-184">Выберите необходимый образ в соответствии с желаемым способом оплаты за лицензию SQL Server:</span><span class="sxs-lookup"><span data-stu-id="96347-184">Choose the right image according to how you want to pay for the SQL Server license:</span></span>

   - <span data-ttu-id="96347-185">**Лицензирование с оплатой по мере использования.** Поминутная оплата этих образов доступна в таких лицензиях SQL Server:</span><span class="sxs-lookup"><span data-stu-id="96347-185">**Pay per usage licensing**: The per-minute cost of these images includes the SQL Server licensing:</span></span>
      - <span data-ttu-id="96347-186">**SQL Server 2016 Enterprise на базе Windows Server Datacenter 2016**;</span><span class="sxs-lookup"><span data-stu-id="96347-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="96347-187">**SQL Server 2016 Standard на базе Windows Server Datacenter 2016**;</span><span class="sxs-lookup"><span data-stu-id="96347-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="96347-188">**SQL Server 2016 Developer на базе Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="96347-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="96347-189">**BYOL (с использованием собственной лицензии)**:</span><span class="sxs-lookup"><span data-stu-id="96347-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="96347-190">**{BYOL} SQL Server 2016 Enterprise на базе Windows Server Datacenter 2016**;</span><span class="sxs-lookup"><span data-stu-id="96347-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="96347-191">**{BYOL} SQL Server 2016 Standard на базе Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="96347-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="96347-192">После создания виртуальной машины удалите предварительно установленный автономный экземпляр SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-192">After you create the virtual machine, remove the pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="96347-193">Вы будете использовать предварительно установленный носитель SQL Server для создания экземпляра отказоустойчивого кластера SQL Server после настройки отказоустойчивого кластера и S2D.</span><span class="sxs-lookup"><span data-stu-id="96347-193">You will use the pre-installed SQL Server media to create the SQL Server FCI after you configure the failover cluster and S2D.</span></span>

   <span data-ttu-id="96347-194">Кроме того, можно использовать образы Azure Marketplace только с операционной системой.</span><span class="sxs-lookup"><span data-stu-id="96347-194">Alternatively, you can use Azure Marketplace images with just the operating system.</span></span> <span data-ttu-id="96347-195">Выберите образ **Windows Server 2016 Datacenter** и установите экземпляр отказоустойчивого кластера SQL Server после настройки отказоустойчивого кластера и S2D.</span><span class="sxs-lookup"><span data-stu-id="96347-195">Choose a **Windows Server 2016 Datacenter** image and install the SQL Server FCI after you configure the failover cluster and S2D.</span></span> <span data-ttu-id="96347-196">Этот образ не содержит установочный носитель SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="96347-197">Поместите установочный носитель в расположении, где будет выполняться установка SQL Server для каждого сервера.</span><span class="sxs-lookup"><span data-stu-id="96347-197">Place the installation media in a location where you can run the SQL Server installation for each server.</span></span>

1. <span data-ttu-id="96347-198">После создания виртуальных машин в Azure подключитесь к каждой виртуальной машине с помощью протокола удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="96347-198">After Azure creates your virtual machines, connect to each virtual machine with RDP.</span></span>

   <span data-ttu-id="96347-199">При первом подключении к виртуальной машине с помощью протокола удаленного рабочего стола компьютер запрашивает, должен ли этот компьютер быть доступным в сети.</span><span class="sxs-lookup"><span data-stu-id="96347-199">When you first connect to a virtual machine with RDP, the computer asks if you want to allow this PC to be discoverable on the network.</span></span> <span data-ttu-id="96347-200">Щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="96347-200">Click **Yes**.</span></span>

1. <span data-ttu-id="96347-201">Если вы используете один из образов виртуальных машин на основе SQL Server, удалите экземпляр SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-201">If you are using one of the SQL Server-based virtual machine images, remove the SQL Server instance.</span></span>

   - <span data-ttu-id="96347-202">В разделе **Программы и компоненты** правой кнопкой мыши щелкните **Microsoft SQL Server 2016 (64-разрядная версия)** и выберите **Удалить/Изменить**.</span><span class="sxs-lookup"><span data-stu-id="96347-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="96347-203">Нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="96347-203">Click **Remove**.</span></span>
   - <span data-ttu-id="96347-204">Выберите экземпляр по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="96347-204">Select the default instance.</span></span>
   - <span data-ttu-id="96347-205">Удалите все компоненты в разделе **Службы ядра СУБД**.</span><span class="sxs-lookup"><span data-stu-id="96347-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="96347-206">Не удаляйте компоненты в разделе **Общие компоненты**.</span><span class="sxs-lookup"><span data-stu-id="96347-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="96347-207">См. следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="96347-207">See the following picture:</span></span>

      ![Удаление компонентов](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="96347-209">Нажмите кнопку **Далее**, а затем — кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="96347-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="96347-210"><a name="ports"></a>Откройте порты брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="96347-210"><a name="ports"></a>Open the firewall ports.</span></span>

   <span data-ttu-id="96347-211">На каждой виртуальной машине откройте следующие порты в брандмауэре Windows.</span><span class="sxs-lookup"><span data-stu-id="96347-211">On each virtual machine, open the following ports on the Windows Firewall.</span></span>

   | <span data-ttu-id="96347-212">Назначение</span><span class="sxs-lookup"><span data-stu-id="96347-212">Purpose</span></span> | <span data-ttu-id="96347-213">TCP-порт</span><span class="sxs-lookup"><span data-stu-id="96347-213">TCP Port</span></span> | <span data-ttu-id="96347-214">Примечания</span><span class="sxs-lookup"><span data-stu-id="96347-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="96347-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="96347-215">SQL Server</span></span> | <span data-ttu-id="96347-216">1433</span><span class="sxs-lookup"><span data-stu-id="96347-216">1433</span></span> | <span data-ttu-id="96347-217">Обычный порт для экземпляров SQL Server по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="96347-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="96347-218">Если используется образ из коллекции, этот порт будет автоматически открыт.</span><span class="sxs-lookup"><span data-stu-id="96347-218">If you used an image from the gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="96347-219">Проверка работоспособности</span><span class="sxs-lookup"><span data-stu-id="96347-219">Health probe</span></span> | <span data-ttu-id="96347-220">59999</span><span class="sxs-lookup"><span data-stu-id="96347-220">59999</span></span> | <span data-ttu-id="96347-221">Любой открытый TCP-порт.</span><span class="sxs-lookup"><span data-stu-id="96347-221">Any open TCP port.</span></span> <span data-ttu-id="96347-222">Позже настройте [проверку работоспособности](#probe) балансировщика нагрузки и кластер для использования этого порта.</span><span class="sxs-lookup"><span data-stu-id="96347-222">In a later step, configure the load balancer [health probe](#probe) and the cluster to use this port.</span></span>  

1. <span data-ttu-id="96347-223">Добавьте хранилище в виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="96347-223">Add storage to the virtual machine.</span></span> <span data-ttu-id="96347-224">Дополнительные сведения см. в статье [Хранилище класса "Премиум": высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="96347-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="96347-225">Для обеих виртуальных машин необходимо по крайней мере два диска данных.</span><span class="sxs-lookup"><span data-stu-id="96347-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="96347-226">Присоедините диски в формате RAW — диски, не отформатированные в NTFS.</span><span class="sxs-lookup"><span data-stu-id="96347-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="96347-227">Если присоединить диски, отформатированные в NTFS, S2D можно включить только без проверки допустимости диска.</span><span class="sxs-lookup"><span data-stu-id="96347-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="96347-228">Присоедините как минимум два хранилища класса Premium (диски SSD) к каждой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="96347-228">Attach a minimum of two Premium Storage (SSD disks) to each VM.</span></span> <span data-ttu-id="96347-229">Мы рекомендуем по крайней мере диски P30 (1 ТБ).</span><span class="sxs-lookup"><span data-stu-id="96347-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="96347-230">Для кэширования узла задайте значение **Только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="96347-230">Set host caching to **Read-only**.</span></span>

   <span data-ttu-id="96347-231">Емкость хранилища, используемого в рабочих средах, зависит от рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-231">The storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="96347-232">Значения, описанные в этой статье, предназначены для демонстрации и тестирования.</span><span class="sxs-lookup"><span data-stu-id="96347-232">The values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="96347-233">[Добавьте виртуальные машины в имеющийся домен](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="96347-233">[Add the virtual machines to your pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="96347-234">После создания и настройки виртуальных машин можно настроить отказоустойчивый кластер.</span><span class="sxs-lookup"><span data-stu-id="96347-234">After the virtual machines are created and configured, you can configure the failover cluster.</span></span>

## <a name="step-2-configure-the-windows-failover-cluster-with-s2d"></a><span data-ttu-id="96347-235">Шаг 2. Настройка отказоустойчивого кластера Windows с S2D</span><span class="sxs-lookup"><span data-stu-id="96347-235">Step 2: Configure the Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="96347-236">Следующим шагом является настройка отказоустойчивого кластера с S2D.</span><span class="sxs-lookup"><span data-stu-id="96347-236">The next step is to configure the failover cluster with S2D.</span></span> <span data-ttu-id="96347-237">На этом шаге вам предстоит выполнить дополнительные действия:</span><span class="sxs-lookup"><span data-stu-id="96347-237">In this step, you will do the following substeps:</span></span>

1. <span data-ttu-id="96347-238">Добавление компонента отказоустойчивой кластеризации Windows.</span><span class="sxs-lookup"><span data-stu-id="96347-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="96347-239">Проверка кластера</span><span class="sxs-lookup"><span data-stu-id="96347-239">Validate the cluster</span></span>
1. <span data-ttu-id="96347-240">Создание отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-240">Create the failover cluster</span></span>
1. <span data-ttu-id="96347-241">Создание облака-свидетеля.</span><span class="sxs-lookup"><span data-stu-id="96347-241">Create the cloud witness</span></span>
1. <span data-ttu-id="96347-242">Добавление хранилища.</span><span class="sxs-lookup"><span data-stu-id="96347-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="96347-243">Добавление компонента отказоустойчивой кластеризации Windows</span><span class="sxs-lookup"><span data-stu-id="96347-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="96347-244">Чтобы начать, подключитесь к первой виртуальной машине с помощью протокола удаленного рабочего стола, используя учетную запись домена, которая является участником локальной группы администраторов, а также имеет разрешения на создание объектов в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="96347-244">To begin, connect to the first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions to create objects in Active Directory.</span></span> <span data-ttu-id="96347-245">Используйте эту учетную запись для остальной части конфигурации.</span><span class="sxs-lookup"><span data-stu-id="96347-245">Use this account for the rest of the configuration.</span></span>

1. <span data-ttu-id="96347-246">[Добавьте компонент отказоустойчивой кластеризации для каждой виртуальной машины](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="96347-246">[Add Failover Clustering feature to each virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="96347-247">Чтобы установить компонент отказоустойчивой кластеризации из пользовательского интерфейса, сделайте следующее на обеих виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="96347-247">To install Failover Clustering feature from the UI, do the following steps on both virtual machines.</span></span>
   - <span data-ttu-id="96347-248">В **диспетчере серверов** выберите **Управление**, а затем — **Добавить роли и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="96347-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="96347-249">В **мастере добавления ролей и компонентов** нажимайте кнопку **Далее**, пока не откроется раздел **Выбор компонентов**.</span><span class="sxs-lookup"><span data-stu-id="96347-249">In **Add Roles and Features Wizard**, click **Next** until you get to **Select Features**.</span></span>
   - <span data-ttu-id="96347-250">В разделе **Выбор компонентов** выберите **Отказоустойчивая кластеризация**.</span><span class="sxs-lookup"><span data-stu-id="96347-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="96347-251">Включите все необходимые компоненты и средства управления.</span><span class="sxs-lookup"><span data-stu-id="96347-251">Include all required features and the management tools.</span></span> <span data-ttu-id="96347-252">Щелкните **Добавить компоненты**.</span><span class="sxs-lookup"><span data-stu-id="96347-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="96347-253">Чтобы установить компоненты, нажмите кнопку **Далее**, а затем — **Готово**.</span><span class="sxs-lookup"><span data-stu-id="96347-253">Click **Next** and then click **Finish** to install the features.</span></span>

   <span data-ttu-id="96347-254">Чтобы установить компонент отказоустойчивой кластеризации с помощью PowerShell, запустите следующий скрипт из сеанса PowerShell администратора на одной из виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="96347-254">To install the Failover Clustering feature with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="96347-255">Для справки в следующих шагах используются инструкции, приведенные на шаге 3 в статье [Гиперконвергентное решение с использованием локальных дисковых пространств в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="96347-255">For reference, the next steps follow the instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-the-cluster"></a><span data-ttu-id="96347-256">Проверка кластера</span><span class="sxs-lookup"><span data-stu-id="96347-256">Validate the cluster</span></span>

<span data-ttu-id="96347-257">В этом руководстве используются инструкции, приведенные в разделе о [проверке кластера](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="96347-257">This guide refers to instructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="96347-258">Проверьте кластер в пользовательском интерфейсе или с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96347-258">Validate the cluster in the UI or with PowerShell.</span></span>

<span data-ttu-id="96347-259">Чтобы проверить работу кластера с помощью пользовательского интерфейса, сделайте следующее на одной из виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="96347-259">To validate the cluster with the UI, do the following steps from one of the virtual machines.</span></span>

1. <span data-ttu-id="96347-260">В **диспетчере серверов** выберите **Сервис**, а затем — **Диспетчер отказоустойчивости кластеров**.</span><span class="sxs-lookup"><span data-stu-id="96347-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="96347-261">В **диспетчере отказоустойчивости кластеров** выберите **Действие**, а затем щелкните **Проверить конфигурацию...**.</span><span class="sxs-lookup"><span data-stu-id="96347-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="96347-262">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="96347-262">Click **Next**.</span></span>
1. <span data-ttu-id="96347-263">На вкладке **Выбор серверов или кластера** введите имена обеих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="96347-263">On **Select Servers or a Cluster**, type the name of both virtual machines.</span></span>
1. <span data-ttu-id="96347-264">На вкладке **Параметры тестирования** выберите **Выполнять только выбранные тесты**.</span><span class="sxs-lookup"><span data-stu-id="96347-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="96347-265">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="96347-265">Click **Next**.</span></span>
1. <span data-ttu-id="96347-266">На вкладке **Выбор тестов** выберите все тесты, кроме **Хранилище**.</span><span class="sxs-lookup"><span data-stu-id="96347-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="96347-267">См. следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="96347-267">See the following picture:</span></span>

   ![Проверка тестов](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="96347-269">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="96347-269">Click **Next**.</span></span>
1. <span data-ttu-id="96347-270">На вкладке **Подтверждение** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="96347-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="96347-271">**Мастер проверки конфигурации** выполняет проверочные тесты.</span><span class="sxs-lookup"><span data-stu-id="96347-271">The **Validate a Configuration Wizard** runs the validation tests.</span></span>

<span data-ttu-id="96347-272">Чтобы проверить кластер с помощью PowerShell, запустите следующий скрипт из сеанса PowerShell администратора на одной из виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="96347-272">To validate the cluster with PowerShell, run the following script from an administrator PowerShell session on one of the virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="96347-273">После проверки кластера создайте отказоустойчивый кластер.</span><span class="sxs-lookup"><span data-stu-id="96347-273">After you validate the cluster, create the failover cluster.</span></span>

### <a name="create-the-failover-cluster"></a><span data-ttu-id="96347-274">Создание отказоустойчивого кластера</span><span class="sxs-lookup"><span data-stu-id="96347-274">Create the failover cluster</span></span>

<span data-ttu-id="96347-275">В этом руководстве используются инструкции, приведенные в разделе [Создание отказоустойчивого кластера](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="96347-275">This guide refers to [Create the failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="96347-276">Для создания отказоустойчивого кластера требуется следующее.</span><span class="sxs-lookup"><span data-stu-id="96347-276">To create the failover cluster, you need:</span></span>
- <span data-ttu-id="96347-277">Имена виртуальных машин, которые становятся узлами кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-277">The names of the virtual machines that become the cluster nodes.</span></span>
- <span data-ttu-id="96347-278">Имя отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-278">A name for the failover cluster</span></span>
- <span data-ttu-id="96347-279">IP-адрес отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-279">An IP address for the failover cluster.</span></span> <span data-ttu-id="96347-280">Вы можете использовать IP-адрес, который не используется в той же виртуальной сети и подсети Azure, где расположены узлы кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-280">You can use an IP address that is not used on the same Azure virtual network and subnet as the cluster nodes.</span></span>

<span data-ttu-id="96347-281">Приведенная ниже команда PowerShell создает отказоустойчивый кластер.</span><span class="sxs-lookup"><span data-stu-id="96347-281">The following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="96347-282">Обновите скрипт, введя имена узлов (имена виртуальных машин) и доступный IP-адрес из виртуальной сети Azure:</span><span class="sxs-lookup"><span data-stu-id="96347-282">Update the script with the names of the nodes (the virtual machine names) and an available IP address from the Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="96347-283">Создание облака-свидетеля</span><span class="sxs-lookup"><span data-stu-id="96347-283">Create a cloud witness</span></span>

<span data-ttu-id="96347-284">Облако-свидетель является новым типом свидетеля кворума кластера, хранящегося в Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="96347-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="96347-285">Это устраняет необходимость в отдельной виртуальной машине, используемой для размещения файлового ресурса-свидетеля.</span><span class="sxs-lookup"><span data-stu-id="96347-285">This removes the need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="96347-286">[Создайте облако-свидетель для отказоустойчивого кластера](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="96347-286">[Create a cloud witness for the failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="96347-287">Создайте контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="96347-287">Create a blob container.</span></span>

1. <span data-ttu-id="96347-288">Сохраните ключи доступа и URL-адрес контейнера.</span><span class="sxs-lookup"><span data-stu-id="96347-288">Save the access keys and the container URL.</span></span>

1. <span data-ttu-id="96347-289">Настройте свидетель кворума отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-289">Configure the failover cluster cluster quorum witness.</span></span> <span data-ttu-id="96347-290">См. подраздел [Настройка облака-свидетеля в качестве свидетеля кворума].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="96347-290">See, [Configure the quorum witness in the user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in the UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="96347-291">Добавление хранилища</span><span class="sxs-lookup"><span data-stu-id="96347-291">Add storage</span></span>

<span data-ttu-id="96347-292">Диски для S2D должны быть пустыми и не содержать разделов или других данных.</span><span class="sxs-lookup"><span data-stu-id="96347-292">The disks for S2D need to be empty and without partitions or other data.</span></span> <span data-ttu-id="96347-293">Чтобы очистить диски, выполните [действия, описанные в этом руководстве](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="96347-293">To clean disks follow [the steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="96347-294">[Включите локальные дисковые пространства \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="96347-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="96347-295">Следующий скрипт PowerShell включает локальные дисковые пространства.</span><span class="sxs-lookup"><span data-stu-id="96347-295">The following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="96347-296">В **диспетчере отказоустойчивости кластеров** теперь отображается пул носителей.</span><span class="sxs-lookup"><span data-stu-id="96347-296">In **Failover Cluster Manager**, you can now see the storage pool.</span></span>

1. <span data-ttu-id="96347-297">[Создайте том](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="96347-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="96347-298">Одна из функций S2D — автоматическое создание пула носителей при включении.</span><span class="sxs-lookup"><span data-stu-id="96347-298">One of the features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="96347-299">Теперь можно создать том.</span><span class="sxs-lookup"><span data-stu-id="96347-299">You are now ready to create a volume.</span></span> <span data-ttu-id="96347-300">Командлет PowerShell `New-Volume` автоматизирует процесс создания тома, включая форматирование, добавление в кластер и создание общего тома кластера (CSV).</span><span class="sxs-lookup"><span data-stu-id="96347-300">The PowerShell commandlet `New-Volume` automates the volume creation process, including formatting, adding to the cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="96347-301">В следующем примере создается CSV емкостью 800 ГБ.</span><span class="sxs-lookup"><span data-stu-id="96347-301">The following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="96347-302">После выполнения этой команды том емкостью 800 ГБ подключается как ресурс кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="96347-303">Том находится в папке `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="96347-303">The volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="96347-304">На следующем снимке экрана показан общий том кластера с S2D.</span><span class="sxs-lookup"><span data-stu-id="96347-304">The following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="96347-306">Шаг 3. Тестирование отработки отказа отказоустойчивого кластера</span><span class="sxs-lookup"><span data-stu-id="96347-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="96347-307">В диспетчере отказоустойчивости кластеров убедитесь, что можете переместить ресурс хранилища в другой узел кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-307">In Failover Cluster Manager, verify that you can move the storage resource to the other cluster node.</span></span> <span data-ttu-id="96347-308">Если вы можете подключиться к отказоустойчивому кластеру с помощью **диспетчера отказоустойчивости кластеров** и перемещать хранилище с одного узла на другой, можно приступать к настройке экземпляра отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-308">If you can connect to the failover cluster with **Failover Cluster Manager** and move the storage from one node to the other, you are ready to configure the FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="96347-309">Шаг 4. Создание экземпляра отказоустойчивого кластера SQL Server</span><span class="sxs-lookup"><span data-stu-id="96347-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="96347-310">После настройки отказоустойчивого кластера и всех компонентов кластера, включая хранилище, можно создать экземпляр отказоустойчивого кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-310">After you have configured the failover cluster and all cluster components including storage, you can create the SQL Server FCI.</span></span>

1. <span data-ttu-id="96347-311">Подключитесь к первой виртуальной машине Azure с помощью RDP.</span><span class="sxs-lookup"><span data-stu-id="96347-311">Connect to the first virtual machine with RDP.</span></span>

1. <span data-ttu-id="96347-312">В **диспетчере отказоустойчивости кластеров** убедитесь, что все основные ресурсы кластера находятся на первой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="96347-312">In **Failover Cluster Manager**, make sure all cluster core resources are on the first virtual machine.</span></span> <span data-ttu-id="96347-313">При необходимости переместите все ресурсы на эту виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="96347-313">If necessary, move all resources to this virtual machine.</span></span>

1. <span data-ttu-id="96347-314">Найдите установочный носитель.</span><span class="sxs-lookup"><span data-stu-id="96347-314">Locate the installation media.</span></span> <span data-ttu-id="96347-315">Если на виртуальной машине используется один из образов Azure Marketplace, носитель находится в папке `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="96347-315">If the virtual machine uses one of the Azure Marketplace images, the media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="96347-316">Щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="96347-316">Click **Setup**.</span></span>

1. <span data-ttu-id="96347-317">В диалоговом окне **Центр установки SQL Server** выберите **Установка**.</span><span class="sxs-lookup"><span data-stu-id="96347-317">In the **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="96347-318">Щелкните **Новая установка отказоустойчивого кластера SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="96347-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="96347-319">Следуйте указаниям мастера, чтобы установить экземпляр отказоустойчивого кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-319">Follow the instructions in the wizard to install the SQL Server FCI.</span></span>

   <span data-ttu-id="96347-320">Каталоги данных экземпляра отказоустойчивого кластера должны находиться в кластеризованном хранилище.</span><span class="sxs-lookup"><span data-stu-id="96347-320">The FCI data directories need to be on clustered storage.</span></span> <span data-ttu-id="96347-321">В случае с S2D это не общий диск, а точка подключения к тому на каждом сервере.</span><span class="sxs-lookup"><span data-stu-id="96347-321">With S2D, it's not a shared disk, but a mount point to a volume on each server.</span></span> <span data-ttu-id="96347-322">S2D синхронизирует том между обоими узлами.</span><span class="sxs-lookup"><span data-stu-id="96347-322">S2D synchronizes the volume between both nodes.</span></span> <span data-ttu-id="96347-323">Том предоставляется в кластере в качестве общего тома кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-323">The volume is presented to the cluster as a cluster shared volume.</span></span> <span data-ttu-id="96347-324">Используйте точки подключения CSV для каталогов данных.</span><span class="sxs-lookup"><span data-stu-id="96347-324">Use the CSV mount point for the data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="96347-326">После завершения работы мастера программа установки установит экземпляр отказоустойчивого кластера SQL Server на первом узле.</span><span class="sxs-lookup"><span data-stu-id="96347-326">After you complete the wizard, Setup will install a SQL Server FCI on the first node.</span></span>

1. <span data-ttu-id="96347-327">После успешной установки экземпляра отказоустойчивого кластера на первом узле подключитесь ко второму узлу с помощью протокола удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="96347-327">After Setup successfully installs the FCI on the first node, connect to the second node with RDP.</span></span>

1. <span data-ttu-id="96347-328">Откройте диалоговое окно **Центр установки SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="96347-328">Open the **SQL Server Installation Center**.</span></span> <span data-ttu-id="96347-329">Щелкните **Установка**.</span><span class="sxs-lookup"><span data-stu-id="96347-329">Click **Installation**.</span></span>

1. <span data-ttu-id="96347-330">Выберите **Добавление узла в отказоустойчивый кластер SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="96347-330">Click **Add node to a SQL Server failover cluster**.</span></span> <span data-ttu-id="96347-331">Следуйте указаниям мастера, чтобы установить сервер SQL и добавить его в экземпляр отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-331">Follow the instructions in the wizard to install SQL server and add this server to the FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="96347-332">При использовании образа коллекции Azure Marketplace с SQL Server средства SQL Server включаются в образ.</span><span class="sxs-lookup"><span data-stu-id="96347-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with the image.</span></span> <span data-ttu-id="96347-333">Если вы не использовали этот образ, установите средства SQL Server отдельно.</span><span class="sxs-lookup"><span data-stu-id="96347-333">If you did not use this image, install the SQL Server tools separately.</span></span> <span data-ttu-id="96347-334">См. сведения в статье [Скачивание SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="96347-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="96347-335">Шаг 5.Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="96347-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="96347-336">На виртуальных машинах Azure кластеры используют балансировщик нагрузки для хранения IP-адреса, который должен находиться на одном узле кластера в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="96347-336">On Azure virtual machines, clusters use a load balancer to hold an IP address that needs to be on one cluster node at a time.</span></span> <span data-ttu-id="96347-337">В этом решении балансировщик нагрузки используется для хранения IP-адреса для экземпляра отказоустойчивого кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-337">In this solution, the load balancer holds the IP address for the SQL Server FCI.</span></span>

<span data-ttu-id="96347-338">[Создайте и настройте балансировщик нагрузки Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="96347-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-the-load-balancer-in-the-azure-portal"></a><span data-ttu-id="96347-339">Создание балансировщика нагрузки на портале Azure</span><span class="sxs-lookup"><span data-stu-id="96347-339">Create the load balancer in the Azure portal</span></span>

<span data-ttu-id="96347-340">Создание балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="96347-340">To create the load balancer:</span></span>

1. <span data-ttu-id="96347-341">На портале Azure перейдите в группу ресурсов с виртуальными машинами.</span><span class="sxs-lookup"><span data-stu-id="96347-341">In the Azure portal, go to the Resource Group with the virtual machines.</span></span>

1. <span data-ttu-id="96347-342">Щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="96347-342">Click **+ Add**.</span></span> <span data-ttu-id="96347-343">В Marketplace найдите **Балансировщик нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="96347-343">Search the Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="96347-344">Щелкните **Балансировщик нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="96347-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="96347-345">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="96347-345">Click **Create**.</span></span>

1. <span data-ttu-id="96347-346">Настройте для балансировщика нагрузки следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="96347-346">Configure the load balancer with:</span></span>

   - <span data-ttu-id="96347-347">**Имя.** Имя, определяющее балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-347">**Name**: A name that identifies the load balancer.</span></span>
   - <span data-ttu-id="96347-348">**Тип.** Балансировщик нагрузки может быть открытым или закрытым.</span><span class="sxs-lookup"><span data-stu-id="96347-348">**Type**: The load balancer can be either public or private.</span></span> <span data-ttu-id="96347-349">Доступ к закрытому балансировщику нагрузки может осуществляться в пределах одной и той же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="96347-349">A private load balancer can be accessed from within the same VNET.</span></span> <span data-ttu-id="96347-350">Большинство приложений Azure могут использовать закрытый балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="96347-351">Если приложению требуется доступ к SQL Server непосредственно через Интернет, используйте открытый балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-351">If your application needs access to SQL Server directly over the Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="96347-352">**Виртуальная сеть.** Виртуальная сеть, в которой находятся виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="96347-352">**Virtual Network**: The same network as the virtual machines.</span></span>
   - <span data-ttu-id="96347-353">**Подсеть.** Подсеть, в которой находятся виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="96347-353">**Subnet**: The same subnet as the virtual machines.</span></span>
   - <span data-ttu-id="96347-354">**Частный IP-адрес.** IP-адрес, назначенный сетевому ресурсу кластера SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="96347-354">**Private IP address**: The same IP address that you assigned to the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="96347-355">**Подписка.** Ваша подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="96347-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="96347-356">**Группа ресурсов.** Используйте ту же группу ресурсов, которая используется для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="96347-356">**Resource Group**: Use the same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="96347-357">**Расположение.** Используйте то же расположение Azure, что используется для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="96347-357">**Location**: Use the same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="96347-358">См. следующий рисунок.</span><span class="sxs-lookup"><span data-stu-id="96347-358">See the following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-the-load-balancer-backend-pool"></a><span data-ttu-id="96347-360">Настройка серверного пула балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="96347-360">Configure the load balancer backend pool</span></span>

1. <span data-ttu-id="96347-361">Вернитесь в группу ресурсов Azure с виртуальными машинами и найдите новый балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-361">Return to the Azure Resource Group with the virtual machines and locate the new load balancer.</span></span> <span data-ttu-id="96347-362">Может потребоваться обновить представление в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="96347-362">You may have to refresh the view on the Resource Group.</span></span> <span data-ttu-id="96347-363">Щелкните балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-363">Click the load balancer.</span></span>

1. <span data-ttu-id="96347-364">В колонке балансировщика нагрузки щелкните **Серверные пулы**.</span><span class="sxs-lookup"><span data-stu-id="96347-364">On the load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="96347-365">Щелкните **+ Добавить**, чтобы добавить серверный пул.</span><span class="sxs-lookup"><span data-stu-id="96347-365">Click **+ Add** to add a backend pool.</span></span>

1. <span data-ttu-id="96347-366">Введите имя для серверного пула.</span><span class="sxs-lookup"><span data-stu-id="96347-366">Type a name for the backend pool.</span></span>

1. <span data-ttu-id="96347-367">Щелкните **Добавить виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="96347-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="96347-368">В колонке **Выбор виртуальных машин** щелкните **Выберите группу доступности**.</span><span class="sxs-lookup"><span data-stu-id="96347-368">On the **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="96347-369">Выберите группу доступности, в которою вы поместили виртуальные машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-369">Choose the availability set that you placed the SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="96347-370">В колонке **Выбор виртуальных машин** щелкните **Выберите виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="96347-370">On the **Choose virtual machines** blade, click **Choose the virtual machines**.</span></span>

   <span data-ttu-id="96347-371">Портал Azure должен выглядеть, как показано на следующем рисунке.</span><span class="sxs-lookup"><span data-stu-id="96347-371">Your Azure portal should look like the following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="96347-373">В колонке **Выберите виртуальные машины** щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="96347-373">Click **Select** on the **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="96347-374">Нажмите **ОК** дважды.</span><span class="sxs-lookup"><span data-stu-id="96347-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="96347-375">Настройка пробы работоспособности балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="96347-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="96347-376">В колонке балансировщика нагрузки щелкните **Health probes** (Пробы работоспособности).</span><span class="sxs-lookup"><span data-stu-id="96347-376">On the load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="96347-377">Щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="96347-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="96347-378">В колонке **Add health probe** (Добавить проверку работоспособности) <a name="probe"></a>задайте параметры проверки работоспособности:</span><span class="sxs-lookup"><span data-stu-id="96347-378">On the **Add health probe** blade, <a name="probe"></a>Set the health probe parameters:</span></span>

   - <span data-ttu-id="96347-379">**Имя.** Имя для проверки работоспособности.</span><span class="sxs-lookup"><span data-stu-id="96347-379">**Name**: A name for the health probe.</span></span>
   - <span data-ttu-id="96347-380">**Протокол.** TCP.</span><span class="sxs-lookup"><span data-stu-id="96347-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="96347-381">**Порт.** Задайте значение доступного порта TCP.</span><span class="sxs-lookup"><span data-stu-id="96347-381">**Port**: Set to an available TCP port.</span></span> <span data-ttu-id="96347-382">Для этого порта требуется открытый порт брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="96347-382">This port requires an open firewall port.</span></span> <span data-ttu-id="96347-383">Используйте [тот же порт,](#ports) который вы задали для проверки работоспособности в брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="96347-383">Use the [same port](#ports) you set for the health probe at the firewall.</span></span>
   - <span data-ttu-id="96347-384">**Интервал.** 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="96347-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="96347-385">**Порог состояния неработоспособности.** 2 последовательных сбоя.</span><span class="sxs-lookup"><span data-stu-id="96347-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="96347-386">Нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="96347-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="96347-387">Задание правил балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="96347-387">Set load balancing rules</span></span>

1. <span data-ttu-id="96347-388">В колонке балансировщика нагрузки щелкните **Правила балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="96347-388">On the load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="96347-389">Щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="96347-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="96347-390">Настройте следующие параметры балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-390">Set the load balancing rules parameters:</span></span>

   - <span data-ttu-id="96347-391">**Имя.** Имя для правил балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-391">**Name**: A name for the load balancing rules.</span></span>
   - <span data-ttu-id="96347-392">**Frontend IP address** (Интерфейсный IP-адрес). Используйте IP-адрес для сетевого ресурса кластера SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="96347-392">**Frontend IP address**: Use the IP address for the SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="96347-393">**Порт.** TCP-порт экземпляра отказоустойчивого кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-393">**Port**: Set for the SQL Server FCI TCP port.</span></span> <span data-ttu-id="96347-394">Порт экземпляра по умолчанию — 1433.</span><span class="sxs-lookup"><span data-stu-id="96347-394">The default instance port is 1433.</span></span>
   - <span data-ttu-id="96347-395">**Внутренний порт.** Для этого значения используется тот же порт, что и для значения **Порт** при включении параметра **Плавающий IP-адрес (direct server return)**.</span><span class="sxs-lookup"><span data-stu-id="96347-395">**Backend port**: This value uses the same port as the **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="96347-396">**Серверный пул.** Используйте имя серверного пула, настроенного ранее.</span><span class="sxs-lookup"><span data-stu-id="96347-396">**Backend pool**: Use the backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="96347-397">**Health probe** (Проверка работоспособности). Используйте проверку работоспособности, настроенную ранее.</span><span class="sxs-lookup"><span data-stu-id="96347-397">**Health probe**: Use the health probe that you configured earlier.</span></span>
   - <span data-ttu-id="96347-398">**Сохранение сеанса.** Нет.</span><span class="sxs-lookup"><span data-stu-id="96347-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="96347-399">**Время ожидания простоя (в минутах)**: 4.</span><span class="sxs-lookup"><span data-stu-id="96347-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="96347-400">**Плавающий IP-адрес (direct server return).** Включено.</span><span class="sxs-lookup"><span data-stu-id="96347-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="96347-401">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="96347-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="96347-402">Шаг 6. Настройка кластера для проверки</span><span class="sxs-lookup"><span data-stu-id="96347-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="96347-403">Задайте параметр порта проверки кластера в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96347-403">Set the cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="96347-404">Чтобы задать параметр порта проверки кластера, обновите переменные в следующем скрипте из своей среды.</span><span class="sxs-lookup"><span data-stu-id="96347-404">To set the cluster probe port parameter, update variables in the following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name).
   $IPResourceName = "IP Address Resource Name" # the IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # the IP Address of the Internal Load Balancer (ILB). This is the static IP address for the load balancer you configured in the Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="96347-405">Шаг 7. Проверка отработки отказа экземпляра отказоустойчивого кластера</span><span class="sxs-lookup"><span data-stu-id="96347-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="96347-406">Проверьте отработку отказа экземпляра отказоустойчивого кластера, чтобы проверить функциональные возможности кластера.</span><span class="sxs-lookup"><span data-stu-id="96347-406">Test failover of the FCI to validate cluster functionality.</span></span> <span data-ttu-id="96347-407">Сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="96347-407">Do the following steps:</span></span>

1. <span data-ttu-id="96347-408">Подключитесь к одному из узлов кластера SQL Server FCI с помощью протокола удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="96347-408">Connect to one of the SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="96347-409">Откройте **диспетчер отказоустойчивости кластеров**.</span><span class="sxs-lookup"><span data-stu-id="96347-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="96347-410">Щелкните **Роли**.</span><span class="sxs-lookup"><span data-stu-id="96347-410">Click **Roles**.</span></span> <span data-ttu-id="96347-411">Обратите внимание, какой узел является владельцем роли SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="96347-411">Notice which node owns the SQL Server FCI role.</span></span>

1. <span data-ttu-id="96347-412">Щелкните правой кнопкой мыши роль SQL Server FCI.</span><span class="sxs-lookup"><span data-stu-id="96347-412">Right-click the SQL Server FCI role.</span></span>

1. <span data-ttu-id="96347-413">Щелкните **Переместить** и выберите **Лучший из возможных узлов**.</span><span class="sxs-lookup"><span data-stu-id="96347-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="96347-414">В **диспетчере отказоустойчивости кластеров** отобразится роль, и ее ресурсы перейдут в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="96347-414">**Failover Cluster Manager** shows the role and its resources go offline.</span></span> <span data-ttu-id="96347-415">Затем ресурсы переместятся и станут доступными на другом узле.</span><span class="sxs-lookup"><span data-stu-id="96347-415">The resources then move and come online on the other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="96347-416">Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="96347-416">Test connectivity</span></span>

<span data-ttu-id="96347-417">Чтобы проверить подключение, войдите на другую виртуальную машину в той же виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="96347-417">To test connectivity, log in to another virtual machine in the same virtual network.</span></span> <span data-ttu-id="96347-418">Откройте **SQL Server Management Studio** и подключитесь к экземпляру отказоустойчивого кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="96347-418">Open **SQL Server Management Studio** and connect to the SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="96347-419">При необходимости можно [скачать SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="96347-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="96347-420">Ограничения</span><span class="sxs-lookup"><span data-stu-id="96347-420">Limitations</span></span>
<span data-ttu-id="96347-421">На виртуальных машинах Azure координатор распределенных транзакций не поддерживается в экземпляре отказоустойчивого кластера, так как RPC-порт не поддерживается в балансировщике нагрузки.</span><span class="sxs-lookup"><span data-stu-id="96347-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because the RPC port is not supported by the load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="96347-422">См. также</span><span class="sxs-lookup"><span data-stu-id="96347-422">See Also</span></span>

<span data-ttu-id="96347-423">[Deploy a two-node S2D SOFS for UPD storage in Azure](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment) (Развертывание S2D SOFS с двумя узлами для хранилища UPD в Azure).</span><span class="sxs-lookup"><span data-stu-id="96347-423">[Setup S2D with remote desktop (Azure)](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)</span></span>

<span data-ttu-id="96347-424">[Гиперконвергентное решение с использованием локальных дисковых пространств в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="96347-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

<span data-ttu-id="96347-425">[Локальные дисковые пространства в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="96347-425">[Storage Space Direct Overview](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)</span></span>

<span data-ttu-id="96347-426">[SQL Server 2016 now supports Windows Server 2016 Storage Spaces Direct](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/) (SQL Server 2016 теперь поддерживает локальные дисковые пространства Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="96347-426">[SQL Server support for S2D](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)</span></span>
