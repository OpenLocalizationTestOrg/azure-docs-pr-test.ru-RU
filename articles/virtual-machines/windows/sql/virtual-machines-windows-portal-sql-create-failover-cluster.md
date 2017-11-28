---
title: "aaaSQL Server FCI - виртуальных машинах Azure | Документы Microsoft"
description: "В этой статье объясняется, каким образом toocreate отказоустойчивого кластера SQL Server экземпляра на виртуальных машинах Azure."
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
ms.openlocfilehash: bee3b27805c5f6cc02a43b25d480c129c254cb90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sql-server-failover-cluster-instance-on-azure-virtual-machines"></a><span data-ttu-id="e690b-103">Настройка экземпляра отказоустойчивого кластера SQL Server на виртуальных машинах Azure</span><span class="sxs-lookup"><span data-stu-id="e690b-103">Configure SQL Server Failover Cluster Instance on Azure Virtual Machines</span></span>

<span data-ttu-id="e690b-104">В этой статье объясняется, как toocreate SQL Server отказоустойчивого кластера экземпляра (FCI) на виртуальных машинах Azure в модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e690b-104">This article explains how toocreate a SQL Server Failover Cluster Instance (FCI) on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="e690b-105">Это решение использует [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\) ](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) как программный виртуальную сеть SAN, синхронизирующего hello хранения (диски с данными) между узлами hello (виртуальные машины Azure) в Кластер Windows.</span><span class="sxs-lookup"><span data-stu-id="e690b-105">This solution uses [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) as a software-based virtual SAN that synchronizes hello storage (data disks) between hello nodes (Azure VMs) in a Windows Cluster.</span></span> <span data-ttu-id="e690b-106">S2D — это новшество в Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e690b-106">S2D is new in Windows Server 2016.</span></span>

<span data-ttu-id="e690b-107">Hello следующей схеме показано законченное решение hello на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="e690b-107">hello following diagram shows hello complete solution on Azure virtual machines:</span></span>

![Группа доступности](./media/virtual-machines-windows-portal-sql-create-failover-cluster/00-sql-fci-s2d-complete-solution.png)

<span data-ttu-id="e690b-109">Hello предшествующий диаграмме показано:</span><span class="sxs-lookup"><span data-stu-id="e690b-109">hello preceding diagram shows:</span></span>

- <span data-ttu-id="e690b-110">Две виртуальные машины Azure в отказоустойчивом кластере Windows.</span><span class="sxs-lookup"><span data-stu-id="e690b-110">Two Azure virtual machines in a Windows Failover Cluster.</span></span> <span data-ttu-id="e690b-111">Когда виртуальная машина находится в отказоустойчивом кластере, она также называется *узлом кластера* или просто *узлом*.</span><span class="sxs-lookup"><span data-stu-id="e690b-111">When a virtual machine is in a failover cluster it is also called a *cluster node*, or *nodes*.</span></span>
- <span data-ttu-id="e690b-112">В каждой виртуальной машине есть два или больше дисков данных.</span><span class="sxs-lookup"><span data-stu-id="e690b-112">Each virtual machine has two or more data disks.</span></span>
- <span data-ttu-id="e690b-113">S2D синхронизирует hello данные на диске данных hello и представляется hello синхронизации хранилища в качестве пула носителей.</span><span class="sxs-lookup"><span data-stu-id="e690b-113">S2D synchronizes hello data on hello data disk and presents hello synchronized storage as a storage pool.</span></span>
- <span data-ttu-id="e690b-114">пул носителей Hello представляется toohello отказоустойчивого кластера общего тома (CSV) кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-114">hello storage pool presents a cluster shared volume (CSV) toohello failover cluster.</span></span>
- <span data-ttu-id="e690b-115">роли кластера Hello отказоустойчивого Кластера SQL Server использует hello CSV для дисков с данными hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-115">hello SQL Server FCI cluster role uses hello CSV for hello data drives.</span></span>
- <span data-ttu-id="e690b-116">Нагрузки Azure балансировки toohold hello IP-адрес для hello отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-116">An Azure load balancer toohold hello IP address for hello SQL Server FCI.</span></span>
- <span data-ttu-id="e690b-117">Группы доступности Azure хранит все ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-117">An Azure availability set holds all hello resources.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e690b-118">Все ресурсы Azure, в диаграмме hello в hello одну группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e690b-118">All Azure resources are in hello diagram are in hello same resource group.</span></span>

<span data-ttu-id="e690b-119">[Дополнительные сведения о \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview) см. в статье Локальные дисковые пространства в Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e690b-119">For details about S2D, see [Windows Server 2016 Datacenter edition Storage Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span></span>

<span data-ttu-id="e690b-120">S2D поддерживает два типа архитектуры — конвергентную и гиперконвергентную.</span><span class="sxs-lookup"><span data-stu-id="e690b-120">S2D supports two types of architectures - converged and hyper-converged.</span></span> <span data-ttu-id="e690b-121">Архитектура Hello в этом документе гиперконвергентных.</span><span class="sxs-lookup"><span data-stu-id="e690b-121">hello architecture in this document is hyper-converged.</span></span> <span data-ttu-id="e690b-122">Хранилища hello местах инфраструктуры гиперконвергентных на hello серверы, ведущее приложение hello кластеризованным.</span><span class="sxs-lookup"><span data-stu-id="e690b-122">A hyper-converged infrastructure places hello storage on hello same servers that host hello clustered application.</span></span> <span data-ttu-id="e690b-123">В этой архитектуре hello хранятся на каждом узле отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-123">In this architecture, hello storage is on each SQL Server FCI node.</span></span>

### <a name="example-azure-template"></a><span data-ttu-id="e690b-124">Пример шаблона Azure</span><span class="sxs-lookup"><span data-stu-id="e690b-124">Example Azure template</span></span>

<span data-ttu-id="e690b-125">Всего решения hello в Azure можно создать на основе шаблона.</span><span class="sxs-lookup"><span data-stu-id="e690b-125">You can create hello entire solution in Azure from a template.</span></span> <span data-ttu-id="e690b-126">Пример шаблона доступен в hello GitHub [шаблоны быстрый запуск Azure](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span><span class="sxs-lookup"><span data-stu-id="e690b-126">An example of a template is available in hello GitHub [Azure Quickstart Templates](https://github.com/MSBrett/azure-quickstart-templates/tree/master/sql-server-2016-fci-existing-vnet-and-ad).</span></span> <span data-ttu-id="e690b-127">Этот пример не предназначен или протестирован для какой-либо конкретной рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e690b-127">This example is not designed or tested for any specific workload.</span></span> <span data-ttu-id="e690b-128">Можно запустить toocreate шаблона hello отказоустойчивого Кластера SQL Server с доменом подключенных tooyour S2D хранилища.</span><span class="sxs-lookup"><span data-stu-id="e690b-128">You can run hello template toocreate a SQL Server FCI with S2D storage connected tooyour domain.</span></span> <span data-ttu-id="e690b-129">Можно оценить hello шаблон и измените его при необходимости.</span><span class="sxs-lookup"><span data-stu-id="e690b-129">You can evaluate hello template, and modify it for your purposes.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e690b-130">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e690b-130">Before you begin</span></span>

<span data-ttu-id="e690b-131">Существует несколько моментов, которые необходимо tooknow и несколько факторов, которые необходимы в месте перед продолжением работы.</span><span class="sxs-lookup"><span data-stu-id="e690b-131">There are a few things you need tooknow and a couple of things that you need in place before you proceed.</span></span>

### <a name="what-tooknow"></a><span data-ttu-id="e690b-132">Какие tooknow</span><span class="sxs-lookup"><span data-stu-id="e690b-132">What tooknow</span></span>
<span data-ttu-id="e690b-133">Должно быть оперативной понимание hello следующие технологии:</span><span class="sxs-lookup"><span data-stu-id="e690b-133">You should have an operational understanding of hello following technologies:</span></span>

- <span data-ttu-id="e690b-134">[технологии кластера под управлением Windows](http://technet.microsoft.com/library/hh831579.aspx);</span><span class="sxs-lookup"><span data-stu-id="e690b-134">[Windows cluster technologies](http://technet.microsoft.com/library/hh831579.aspx)</span></span>
-  <span data-ttu-id="e690b-135">[экземпляры отказоустойчивого кластера SQL Server](http://msdn.microsoft.com/library/ms189134.aspx).</span><span class="sxs-lookup"><span data-stu-id="e690b-135">[SQL Server Failover Cluster Instances](http://msdn.microsoft.com/library/ms189134.aspx).</span></span>

<span data-ttu-id="e690b-136">Кроме того должен иметь общее представление о hello следующие технологии:</span><span class="sxs-lookup"><span data-stu-id="e690b-136">Also, you should have a general understanding of hello following technologies:</span></span>

- <span data-ttu-id="e690b-137">[гиперконвергентное решение, использующее локальные дисковые пространства в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct);</span><span class="sxs-lookup"><span data-stu-id="e690b-137">[Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct)</span></span>
- <span data-ttu-id="e690b-138">[группы ресурсов Azure](../../../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e690b-138">[Azure resource groups](../../../azure-resource-manager/resource-group-portal.md)</span></span>

### <a name="what-toohave"></a><span data-ttu-id="e690b-139">Какие toohave</span><span class="sxs-lookup"><span data-stu-id="e690b-139">What toohave</span></span>

<span data-ttu-id="e690b-140">Перед выполнением инструкции hello в этой статье, необходимо иметь:</span><span class="sxs-lookup"><span data-stu-id="e690b-140">Before following hello instructions in this article, you should already have:</span></span>

- <span data-ttu-id="e690b-141">подписка Microsoft Azure;</span><span class="sxs-lookup"><span data-stu-id="e690b-141">A Microsoft Azure subscription.</span></span>
- <span data-ttu-id="e690b-142">домен Windows на виртуальных машинах Azure;</span><span class="sxs-lookup"><span data-stu-id="e690b-142">A Windows domain on Azure virtual machines.</span></span>
- <span data-ttu-id="e690b-143">Учетная запись с объектами toocreate разрешений в hello виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="e690b-143">An account with permission toocreate objects in hello Azure virtual machine.</span></span>
- <span data-ttu-id="e690b-144">Виртуальная сеть Azure и подсеть с достаточно пространство IP-адресов для hello следующие компоненты:</span><span class="sxs-lookup"><span data-stu-id="e690b-144">An Azure virtual network and subnet with sufficient IP address space for hello following components:</span></span>
   - <span data-ttu-id="e690b-145">обе виртуальные машины;</span><span class="sxs-lookup"><span data-stu-id="e690b-145">Both virtual machines.</span></span>
   - <span data-ttu-id="e690b-146">IP-адрес кластера отработки отказа Hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-146">hello failover cluster IP address.</span></span>
   - <span data-ttu-id="e690b-147">IP-адрес для каждого экземпляра отказоустойчивого кластера;</span><span class="sxs-lookup"><span data-stu-id="e690b-147">An IP address for each FCI.</span></span>
- <span data-ttu-id="e690b-148">Служба DNS настроена на hello сети Azure, указывающий toohello контроллеров домена.</span><span class="sxs-lookup"><span data-stu-id="e690b-148">DNS configured on hello Azure Network, pointing toohello domain controllers.</span></span>

<span data-ttu-id="e690b-149">После выполнения этих предварительных требований можно продолжить создание отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-149">With these prerequisites in place, you can proceed with building your failover cluster.</span></span> <span data-ttu-id="e690b-150">Hello первым шагом является toocreate hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e690b-150">hello first step is toocreate hello virtual machines.</span></span>

## <a name="step-1-create-virtual-machines"></a><span data-ttu-id="e690b-151">Шаг 1. Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e690b-151">Step 1: Create virtual machines</span></span>

1. <span data-ttu-id="e690b-152">Войдите в toohello [портал Azure](http://portal.azure.com) с вашей подпиской.</span><span class="sxs-lookup"><span data-stu-id="e690b-152">Log in toohello [Azure portal](http://portal.azure.com) with your subscription.</span></span>

1. <span data-ttu-id="e690b-153">[Создайте группу доступности Azure](../tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="e690b-153">[Create an Azure availability set](../tutorial-availability-sets.md).</span></span>

   <span data-ttu-id="e690b-154">доступность Hello задать группы виртуальных машин в доменах сбоя и домены обновления.</span><span class="sxs-lookup"><span data-stu-id="e690b-154">hello availability set groups virtual machines across fault domains and update domains.</span></span> <span data-ttu-id="e690b-155">набор доступности Hello гарантирует, что ваше приложение не повлияют единственных точек отказа, таких как hello сетевой коммутатор или блок питания стойки серверов hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-155">hello availability set makes sure that your application is not affected by single points of failure, like hello network switch or hello power unit of a rack of servers.</span></span>

   <span data-ttu-id="e690b-156">Если вы не создали hello группы ресурсов для виртуальных машин, только при создании группы доступности Azure.</span><span class="sxs-lookup"><span data-stu-id="e690b-156">If you have not created hello resource group for your virtual machines, do it when you create an Azure availability set.</span></span> <span data-ttu-id="e690b-157">Если вы используете группы доступности hello Azure портала toocreate hello, hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e690b-157">If you're using hello Azure portal toocreate hello availability set, do hello following steps:</span></span>

   - <span data-ttu-id="e690b-158">В hello портал Azure, щелкните  **+**  tooopen hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e690b-158">In hello Azure portal, click **+** tooopen hello Azure Marketplace.</span></span> <span data-ttu-id="e690b-159">Найдите **Группа доступности**.</span><span class="sxs-lookup"><span data-stu-id="e690b-159">Search for **Availability set**.</span></span>
   - <span data-ttu-id="e690b-160">Выберите **Группа доступности**.</span><span class="sxs-lookup"><span data-stu-id="e690b-160">Click **Availability set**.</span></span>
   - <span data-ttu-id="e690b-161">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e690b-161">Click **Create**.</span></span>
   - <span data-ttu-id="e690b-162">На hello **создать набор доступности** колонке hello набор следующие значения:</span><span class="sxs-lookup"><span data-stu-id="e690b-162">On hello **Create availability set** blade, set hello following values:</span></span>
      - <span data-ttu-id="e690b-163">**Имя**: имя набора доступности hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-163">**Name**: A name for hello availability set.</span></span>
      - <span data-ttu-id="e690b-164">**Подписка.** Ваша подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="e690b-164">**Subscription**: Your Azure subscription.</span></span>
      - <span data-ttu-id="e690b-165">**Группа ресурсов**: toouse существующую группу, нажмите кнопку **использовать существующие** и hello выберите группу из раскрывающегося списка hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-165">**Resource group**: If you want toouse an existing group, click **Use existing** and select hello group from hello drop-down list.</span></span> <span data-ttu-id="e690b-166">В противном случае выберите **создать новый** и введите имя для группы hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-166">Otherwise choose **Create New** and type a name for hello group.</span></span>
      - <span data-ttu-id="e690b-167">**Расположение**: задать hello расположение, где toocreate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e690b-167">**Location**: Set hello location where you plan toocreate your virtual machines.</span></span>
      - <span data-ttu-id="e690b-168">**Домены отказоустойчивости**: использовать значение по умолчанию hello (3).</span><span class="sxs-lookup"><span data-stu-id="e690b-168">**Fault domains**: Use hello default (3).</span></span>
      - <span data-ttu-id="e690b-169">**Домены обновления**: использовать значение по умолчанию hello (5).</span><span class="sxs-lookup"><span data-stu-id="e690b-169">**Update domains**: Use hello default (5).</span></span>
   - <span data-ttu-id="e690b-170">Нажмите кнопку **создать** набор доступности toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-170">Click **Create** toocreate hello availability set.</span></span>

1. <span data-ttu-id="e690b-171">Создание виртуальных машин hello в набор доступности hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-171">Create hello virtual machines in hello availability set.</span></span>

   <span data-ttu-id="e690b-172">Подготовить два виртуальных машин SQL Server в наборе доступности Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-172">Provision two SQL Server virtual machines in hello Azure availability set.</span></span> <span data-ttu-id="e690b-173">Инструкции см. в разделе [подготовки виртуальной машины SQL Server в Azure portal hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e690b-173">For instructions, see [Provision a SQL Server virtual machine in hello Azure portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

   <span data-ttu-id="e690b-174">Разместите обе виртуальные машины:</span><span class="sxs-lookup"><span data-stu-id="e690b-174">Place both virtual machines:</span></span>

   - <span data-ttu-id="e690b-175">В hello одной группе ресурсов Azure, задайте доступности находится в.</span><span class="sxs-lookup"><span data-stu-id="e690b-175">In hello same Azure resource group that your availability set is in.</span></span>
   - <span data-ttu-id="e690b-176">На hello сетевых как контроллер домена.</span><span class="sxs-lookup"><span data-stu-id="e690b-176">On hello same network as your domain controller.</span></span>
   - <span data-ttu-id="e690b-177">в подсети с достаточным пространством IP-адресов для обеих виртуальных машин и всех экземпляров отказоустойчивого кластера, которые со временем могут использоваться в этом кластере;</span><span class="sxs-lookup"><span data-stu-id="e690b-177">On a subnet with sufficient IP address space for both virtual machines, and all FCIs that you may eventually use on this cluster.</span></span>
   - <span data-ttu-id="e690b-178">В наборе доступности Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-178">In hello Azure availability set.</span></span>   

      >[!IMPORTANT]
      ><span data-ttu-id="e690b-179">После создания виртуальной машины установить или изменить группу доступности невозможно.</span><span class="sxs-lookup"><span data-stu-id="e690b-179">You cannot set or change availability set after a virtual machine has been created.</span></span>

   <span data-ttu-id="e690b-180">Выбор изображения из hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e690b-180">Choose an image from hello Azure Marketplace.</span></span> <span data-ttu-id="e690b-181">Можно использовать Marketplace включает образ с, Windows Server и SQL Server или просто hello Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-181">You can use a Marketplace image with that includes Windows Server and SQL Server, or just hello Windows Server.</span></span> <span data-ttu-id="e690b-182">Дополнительные сведения см. в статье [Приступая к работе с SQL Server в виртуальных машинах Azure](../../virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e690b-182">For details, see [Overview of SQL Server on Azure Virtual Machines](../../virtual-machines-windows-sql-server-iaas-overview.md)</span></span>

   <span data-ttu-id="e690b-183">Hello официальный образов SQL Server в коллекции Azure hello включают установленного экземпляра SQL Server, а также программное обеспечение для установки SQL Server hello и требуемый раздел hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-183">hello official SQL Server images in hello Azure Gallery include an installed SQL Server instance, plus hello SQL Server installation software, and hello required key.</span></span>

   <span data-ttu-id="e690b-184">Выберите правом изображении hello в соответствии с нужным toohow toopay hello лицензии SQL Server:</span><span class="sxs-lookup"><span data-stu-id="e690b-184">Choose hello right image according toohow you want toopay for hello SQL Server license:</span></span>

   - <span data-ttu-id="e690b-185">**Оплата за использование лицензирования**: hello / мин стоимость этих образов включает hello лицензирования SQL Server:</span><span class="sxs-lookup"><span data-stu-id="e690b-185">**Pay per usage licensing**: hello per-minute cost of these images includes hello SQL Server licensing:</span></span>
      - <span data-ttu-id="e690b-186">**SQL Server 2016 Enterprise на базе Windows Server Datacenter 2016**;</span><span class="sxs-lookup"><span data-stu-id="e690b-186">**SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="e690b-187">**SQL Server 2016 Standard на базе Windows Server Datacenter 2016**;</span><span class="sxs-lookup"><span data-stu-id="e690b-187">**SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="e690b-188">**SQL Server 2016 Developer на базе Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="e690b-188">**SQL Server 2016 Developer on Windows Server Datacenter 2016**</span></span>

   - <span data-ttu-id="e690b-189">**BYOL (с использованием собственной лицензии)**:</span><span class="sxs-lookup"><span data-stu-id="e690b-189">**Bring-your-own-license (BYOL)**</span></span>

      - <span data-ttu-id="e690b-190">**{BYOL} SQL Server 2016 Enterprise на базе Windows Server Datacenter 2016**;</span><span class="sxs-lookup"><span data-stu-id="e690b-190">**{BYOL} SQL Server 2016 Enterprise on Windows Server Datacenter 2016**</span></span>
      - <span data-ttu-id="e690b-191">**{BYOL} SQL Server 2016 Standard на базе Windows Server Datacenter 2016**.</span><span class="sxs-lookup"><span data-stu-id="e690b-191">**{BYOL} SQL Server 2016 Standard on Windows Server Datacenter 2016**</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="e690b-192">После создания виртуальной машины hello, удалите hello предустановленных автономным экземпляром SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-192">After you create hello virtual machine, remove hello pre-installed standalone SQL Server instance.</span></span> <span data-ttu-id="e690b-193">После настройки hello отказоустойчивого кластера и S2D будет использоваться hello предварительно установить SQL Server носителя toocreate hello отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-193">You will use hello pre-installed SQL Server media toocreate hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span>

   <span data-ttu-id="e690b-194">Кроме того можно использовать образы Azure Marketplace просто hello операционную систему.</span><span class="sxs-lookup"><span data-stu-id="e690b-194">Alternatively, you can use Azure Marketplace images with just hello operating system.</span></span> <span data-ttu-id="e690b-195">Выберите **Windows Server 2016 Datacenter** и образов установки hello отказоустойчивого Кластера SQL Server после настройки hello отказоустойчивого кластера и S2D.</span><span class="sxs-lookup"><span data-stu-id="e690b-195">Choose a **Windows Server 2016 Datacenter** image and install hello SQL Server FCI after you configure hello failover cluster and S2D.</span></span> <span data-ttu-id="e690b-196">Этот образ не содержит установочный носитель SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-196">This image does not contain SQL Server installation media.</span></span> <span data-ttu-id="e690b-197">Поместите hello установочного носителя в расположении, где выполняется установка SQL Server hello для каждого сервера.</span><span class="sxs-lookup"><span data-stu-id="e690b-197">Place hello installation media in a location where you can run hello SQL Server installation for each server.</span></span>

1. <span data-ttu-id="e690b-198">После Azure создает виртуальные машины, подключите tooeach виртуальную машину с помощью протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="e690b-198">After Azure creates your virtual machines, connect tooeach virtual machine with RDP.</span></span>

   <span data-ttu-id="e690b-199">При первом подключении tooa виртуальной машины с помощью протокола удаленного рабочего СТОЛА, компьютер hello запросом tooallow этот ПК toobe обнаружения сети hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-199">When you first connect tooa virtual machine with RDP, hello computer asks if you want tooallow this PC toobe discoverable on hello network.</span></span> <span data-ttu-id="e690b-200">Щелкните **Да**.</span><span class="sxs-lookup"><span data-stu-id="e690b-200">Click **Yes**.</span></span>

1. <span data-ttu-id="e690b-201">При использовании одного из образов hello виртуальной машины под управлением SQL Server, удалите hello экземпляр SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-201">If you are using one of hello SQL Server-based virtual machine images, remove hello SQL Server instance.</span></span>

   - <span data-ttu-id="e690b-202">В разделе **Программы и компоненты** правой кнопкой мыши щелкните **Microsoft SQL Server 2016 (64-разрядная версия)** и выберите **Удалить/Изменить**.</span><span class="sxs-lookup"><span data-stu-id="e690b-202">In **Programs and Features**, right-click **Microsoft SQL Server 2016 (64-bit)** and click **Uninstall/Change**.</span></span>
   - <span data-ttu-id="e690b-203">Нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="e690b-203">Click **Remove**.</span></span>
   - <span data-ttu-id="e690b-204">Выберите экземпляр по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-204">Select hello default instance.</span></span>
   - <span data-ttu-id="e690b-205">Удалите все компоненты в разделе **Службы ядра СУБД**.</span><span class="sxs-lookup"><span data-stu-id="e690b-205">Remove all features under **Database Engine Services**.</span></span> <span data-ttu-id="e690b-206">Не удаляйте компоненты в разделе **Общие компоненты**.</span><span class="sxs-lookup"><span data-stu-id="e690b-206">Do not remove **Shared Features**.</span></span> <span data-ttu-id="e690b-207">См. следующий рисунок hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-207">See hello following picture:</span></span>

      ![Удаление компонентов](./media/virtual-machines-windows-portal-sql-create-failover-cluster/03-remove-features.png)

   - <span data-ttu-id="e690b-209">Нажмите кнопку **Далее**, а затем — кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="e690b-209">Click **Next**, and then click **Remove**.</span></span>

1. <span data-ttu-id="e690b-210"><a name="ports"></a>Открыть порты брандмауэра hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-210"><a name="ports"></a>Open hello firewall ports.</span></span>

   <span data-ttu-id="e690b-211">На каждой виртуальной машине откройте следующие порты в брандмауэре Windows hello hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-211">On each virtual machine, open hello following ports on hello Windows Firewall.</span></span>

   | <span data-ttu-id="e690b-212">Назначение</span><span class="sxs-lookup"><span data-stu-id="e690b-212">Purpose</span></span> | <span data-ttu-id="e690b-213">TCP-порт</span><span class="sxs-lookup"><span data-stu-id="e690b-213">TCP Port</span></span> | <span data-ttu-id="e690b-214">Примечания</span><span class="sxs-lookup"><span data-stu-id="e690b-214">Notes</span></span>
   | ------ | ------ | ------
   | <span data-ttu-id="e690b-215">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e690b-215">SQL Server</span></span> | <span data-ttu-id="e690b-216">1433</span><span class="sxs-lookup"><span data-stu-id="e690b-216">1433</span></span> | <span data-ttu-id="e690b-217">Обычный порт для экземпляров SQL Server по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e690b-217">Normal port for default instances of SQL Server.</span></span> <span data-ttu-id="e690b-218">Если использовать образ из коллекции hello, этот порт будет автоматически открыт.</span><span class="sxs-lookup"><span data-stu-id="e690b-218">If you used an image from hello gallery, this port is automatically opened.</span></span>
   | <span data-ttu-id="e690b-219">Проверка работоспособности</span><span class="sxs-lookup"><span data-stu-id="e690b-219">Health probe</span></span> | <span data-ttu-id="e690b-220">59999</span><span class="sxs-lookup"><span data-stu-id="e690b-220">59999</span></span> | <span data-ttu-id="e690b-221">Любой открытый TCP-порт.</span><span class="sxs-lookup"><span data-stu-id="e690b-221">Any open TCP port.</span></span> <span data-ttu-id="e690b-222">На более позднем этапе настройки балансировки нагрузки hello [проверки работоспособности](#probe) и hello кластера toouse этот порт.</span><span class="sxs-lookup"><span data-stu-id="e690b-222">In a later step, configure hello load balancer [health probe](#probe) and hello cluster toouse this port.</span></span>  

1. <span data-ttu-id="e690b-223">Добавление хранилища toohello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e690b-223">Add storage toohello virtual machine.</span></span> <span data-ttu-id="e690b-224">Дополнительные сведения см. в статье [Хранилище класса "Премиум": высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../../storage/common/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e690b-224">For detailed information, see [add storage](../../../storage/common/storage-premium-storage.md).</span></span>

   <span data-ttu-id="e690b-225">Для обеих виртуальных машин необходимо по крайней мере два диска данных.</span><span class="sxs-lookup"><span data-stu-id="e690b-225">Both virtual machines need at least two data disks.</span></span>

   <span data-ttu-id="e690b-226">Присоедините диски в формате RAW — диски, не отформатированные в NTFS.</span><span class="sxs-lookup"><span data-stu-id="e690b-226">Attach raw disks - not NTFS formatted disks.</span></span>
      >[!NOTE]
      ><span data-ttu-id="e690b-227">Если присоединить диски, отформатированные в NTFS, S2D можно включить только без проверки допустимости диска.</span><span class="sxs-lookup"><span data-stu-id="e690b-227">If you attach NTFS-formatted disks, you can only enable S2D with no disk eligibility check.</span></span>  

   <span data-ttu-id="e690b-228">Присоедините как минимум два tooeach хранилище Premium (SSD-дисков) виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e690b-228">Attach a minimum of two Premium Storage (SSD disks) tooeach VM.</span></span> <span data-ttu-id="e690b-229">Мы рекомендуем по крайней мере диски P30 (1 ТБ).</span><span class="sxs-lookup"><span data-stu-id="e690b-229">We recommend at least P30 (1 TB) disks.</span></span>

   <span data-ttu-id="e690b-230">Набор узлов, кэширование слишком**только для чтения**.</span><span class="sxs-lookup"><span data-stu-id="e690b-230">Set host caching too**Read-only**.</span></span>

   <span data-ttu-id="e690b-231">Hello емкость хранилища, используемого в рабочей среде зависит от рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e690b-231">hello storage capacity you use in production environments depends on your workload.</span></span> <span data-ttu-id="e690b-232">Hello значений, описанных в этой статье предназначены для демонстрации и тестирования.</span><span class="sxs-lookup"><span data-stu-id="e690b-232">hello values described in this article are for demonstration and testing.</span></span>

1. <span data-ttu-id="e690b-233">[Добавить существующий домен hello виртуальные машины tooyour](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span><span class="sxs-lookup"><span data-stu-id="e690b-233">[Add hello virtual machines tooyour pre-existing domain](virtual-machines-windows-portal-sql-availability-group-prereq.md#joinDomain).</span></span>

<span data-ttu-id="e690b-234">После создания и настройки hello виртуальных машин можно настроить hello отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-234">After hello virtual machines are created and configured, you can configure hello failover cluster.</span></span>

## <a name="step-2-configure-hello-windows-failover-cluster-with-s2d"></a><span data-ttu-id="e690b-235">Шаг 2: Настройка отказоустойчивого кластера Windows hello с S2D</span><span class="sxs-lookup"><span data-stu-id="e690b-235">Step 2: Configure hello Windows Failover Cluster with S2D</span></span>

<span data-ttu-id="e690b-236">Hello следующим шагом является tooconfigure hello отказоустойчивый кластер с S2D.</span><span class="sxs-lookup"><span data-stu-id="e690b-236">hello next step is tooconfigure hello failover cluster with S2D.</span></span> <span data-ttu-id="e690b-237">На этом шаге будет выполнять hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="e690b-237">In this step, you will do hello following substeps:</span></span>

1. <span data-ttu-id="e690b-238">Добавление компонента отказоустойчивой кластеризации Windows.</span><span class="sxs-lookup"><span data-stu-id="e690b-238">Add Windows Failover Clustering feature</span></span>
1. <span data-ttu-id="e690b-239">Проверка кластера hello</span><span class="sxs-lookup"><span data-stu-id="e690b-239">Validate hello cluster</span></span>
1. <span data-ttu-id="e690b-240">Создание отказоустойчивого кластера hello</span><span class="sxs-lookup"><span data-stu-id="e690b-240">Create hello failover cluster</span></span>
1. <span data-ttu-id="e690b-241">Создание следящий сервер облака hello</span><span class="sxs-lookup"><span data-stu-id="e690b-241">Create hello cloud witness</span></span>
1. <span data-ttu-id="e690b-242">Добавление хранилища.</span><span class="sxs-lookup"><span data-stu-id="e690b-242">Add storage</span></span>

### <a name="add-windows-failover-clustering-feature"></a><span data-ttu-id="e690b-243">Добавление компонента отказоустойчивой кластеризации Windows.</span><span class="sxs-lookup"><span data-stu-id="e690b-243">Add Windows Failover Clustering feature</span></span>

1. <span data-ttu-id="e690b-244">toobegin, подключение toohello первую виртуальную машину с помощью протокола удаленного рабочего СТОЛА, используя учетную запись домена, которая является членом локальной группы администраторов и не имеет разрешения toocreate объектов в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e690b-244">toobegin, connect toohello first virtual machine with RDP using a domain account that is a member of local administrators, and has permissions toocreate objects in Active Directory.</span></span> <span data-ttu-id="e690b-245">Используйте эту учетную запись для hello остальной конфигурацией hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-245">Use this account for hello rest of hello configuration.</span></span>

1. <span data-ttu-id="e690b-246">[Добавить виртуальную машину отказоустойчивой кластеризации для компонентов tooeach](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span><span class="sxs-lookup"><span data-stu-id="e690b-246">[Add Failover Clustering feature tooeach virtual machine](virtual-machines-windows-portal-sql-availability-group-prereq.md#add-failover-clustering-features-to-both-sql-server-vms).</span></span>

   <span data-ttu-id="e690b-247">Средство отказоустойчивости кластеров tooinstall из пользовательского интерфейса, hello hello инструкциям на обеих виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e690b-247">tooinstall Failover Clustering feature from hello UI, do hello following steps on both virtual machines.</span></span>
   - <span data-ttu-id="e690b-248">В **диспетчере серверов** выберите **Управление**, а затем — **Добавить роли и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="e690b-248">In **Server Manager**, click **Manage**, and then click **Add Roles and Features**.</span></span>
   - <span data-ttu-id="e690b-249">В **мастера добавления ролей и компонентов**, нажмите кнопку **Далее** пока не будет получен слишком**Выбор компонентов**.</span><span class="sxs-lookup"><span data-stu-id="e690b-249">In **Add Roles and Features Wizard**, click **Next** until you get too**Select Features**.</span></span>
   - <span data-ttu-id="e690b-250">В разделе **Выбор компонентов** выберите **Отказоустойчивая кластеризация**.</span><span class="sxs-lookup"><span data-stu-id="e690b-250">In **Select Features**, click **Failover Clustering**.</span></span> <span data-ttu-id="e690b-251">Включить все необходимые компоненты и средства управления hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-251">Include all required features and hello management tools.</span></span> <span data-ttu-id="e690b-252">Щелкните **Добавить компоненты**.</span><span class="sxs-lookup"><span data-stu-id="e690b-252">Click **Add Features**.</span></span>
   - <span data-ttu-id="e690b-253">Нажмите кнопку **Далее** и нажмите кнопку **Готово** tooinstall функции hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-253">Click **Next** and then click **Finish** tooinstall hello features.</span></span>

   <span data-ttu-id="e690b-254">tooinstall hello отказоустойчивой кластеризации с помощью PowerShell, запустите следующий скрипт из сеанса PowerShell администратора на одной из виртуальных машин hello hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-254">tooinstall hello Failover Clustering feature with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   $nodes = ("<node1>","<node2>")
   Invoke-Command  $nodes {Install-WindowsFeature Failover-Clustering -IncludeAllSubFeature -IncludeManagementTools}
   ```

<span data-ttu-id="e690b-255">Справочник, дальнейшие действия hello следовать инструкциям hello в шаге 3 [схождения Hyper решения, с помощью дисковых пространств в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="e690b-255">For reference, hello next steps follow hello instructions under Step 3 of [Hyper-converged solution using Storage Spaces Direct in Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-3-configure-storage-spaces-direct).</span></span>

### <a name="validate-hello-cluster"></a><span data-ttu-id="e690b-256">Проверка кластера hello</span><span class="sxs-lookup"><span data-stu-id="e690b-256">Validate hello cluster</span></span>

<span data-ttu-id="e690b-257">В этом руководстве tooinstructions под [проверки кластера](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span><span class="sxs-lookup"><span data-stu-id="e690b-257">This guide refers tooinstructions under [validate cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-31-run-cluster-validation).</span></span>

<span data-ttu-id="e690b-258">Проверка кластера hello hello пользовательского интерфейса или с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e690b-258">Validate hello cluster in hello UI or with PowerShell.</span></span>

<span data-ttu-id="e690b-259">toovalidate hello кластера с помощью пользовательского интерфейса, hello hello, выполнив действия из одной из виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-259">toovalidate hello cluster with hello UI, do hello following steps from one of hello virtual machines.</span></span>

1. <span data-ttu-id="e690b-260">В **диспетчере серверов** выберите **Сервис**, а затем — **Диспетчер отказоустойчивости кластеров**.</span><span class="sxs-lookup"><span data-stu-id="e690b-260">In **Server Manager**, click **Tools**, then click **Failover Cluster Manager**.</span></span>
1. <span data-ttu-id="e690b-261">В **диспетчере отказоустойчивости кластеров** выберите **Действие**, а затем щелкните **Проверить конфигурацию...**.</span><span class="sxs-lookup"><span data-stu-id="e690b-261">In **Failover Cluster Manager**, click **Action**, then click **Validate Configuration...**.</span></span>
1. <span data-ttu-id="e690b-262">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e690b-262">Click **Next**.</span></span>
1. <span data-ttu-id="e690b-263">На **Выбор серверов или кластера**, имя типа hello обе виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e690b-263">On **Select Servers or a Cluster**, type hello name of both virtual machines.</span></span>
1. <span data-ttu-id="e690b-264">На вкладке **Параметры тестирования** выберите **Выполнять только выбранные тесты**.</span><span class="sxs-lookup"><span data-stu-id="e690b-264">On **Testing options**, choose **Run only tests I select**.</span></span> <span data-ttu-id="e690b-265">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e690b-265">Click **Next**.</span></span>
1. <span data-ttu-id="e690b-266">На вкладке **Выбор тестов** выберите все тесты, кроме **Хранилище**.</span><span class="sxs-lookup"><span data-stu-id="e690b-266">On **Test selection**, include all tests except **Storage**.</span></span> <span data-ttu-id="e690b-267">См. следующий рисунок hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-267">See hello following picture:</span></span>

   ![Проверка тестов](./media/virtual-machines-windows-portal-sql-create-failover-cluster/10-validate-cluster-test.png)

1. <span data-ttu-id="e690b-269">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e690b-269">Click **Next**.</span></span>
1. <span data-ttu-id="e690b-270">На вкладке **Подтверждение** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="e690b-270">On **Confirmation**, click **Next**.</span></span>

<span data-ttu-id="e690b-271">Hello **мастер проверки конфигурации** запусков hello проверочные тесты.</span><span class="sxs-lookup"><span data-stu-id="e690b-271">hello **Validate a Configuration Wizard** runs hello validation tests.</span></span>

<span data-ttu-id="e690b-272">toovalidate hello кластера с помощью PowerShell, запустите следующий скрипт из сеанса PowerShell администратора на одной из виртуальных машин hello hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-272">toovalidate hello cluster with PowerShell, run hello following script from an administrator PowerShell session on one of hello virtual machines.</span></span>

   ```PowerShell
   Test-Cluster –Node ("<node1>","<node2>") –Include "Storage Spaces Direct", "Inventory", "Network", "System Configuration"
   ```

<span data-ttu-id="e690b-273">После проверки кластера hello, создайте отказоустойчивый кластер hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-273">After you validate hello cluster, create hello failover cluster.</span></span>

### <a name="create-hello-failover-cluster"></a><span data-ttu-id="e690b-274">Создание отказоустойчивого кластера hello</span><span class="sxs-lookup"><span data-stu-id="e690b-274">Create hello failover cluster</span></span>

<span data-ttu-id="e690b-275">В этом руководстве, слишком[создать hello отказоустойчивого кластера](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span><span class="sxs-lookup"><span data-stu-id="e690b-275">This guide refers too[Create hello failover cluster](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-32-create-a-cluster).</span></span>

<span data-ttu-id="e690b-276">toocreate hello отказоустойчивый кластер, необходимо:</span><span class="sxs-lookup"><span data-stu-id="e690b-276">toocreate hello failover cluster, you need:</span></span>
- <span data-ttu-id="e690b-277">имена Hello hello виртуальных машин, которые становятся hello узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-277">hello names of hello virtual machines that become hello cluster nodes.</span></span>
- <span data-ttu-id="e690b-278">Имя для hello отказоустойчивого кластера</span><span class="sxs-lookup"><span data-stu-id="e690b-278">A name for hello failover cluster</span></span>
- <span data-ttu-id="e690b-279">IP-адрес для hello отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-279">An IP address for hello failover cluster.</span></span> <span data-ttu-id="e690b-280">Можно использовать IP-адрес, который не используется на hello одной виртуальной сети Azure и подсеть, как hello узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-280">You can use an IP address that is not used on hello same Azure virtual network and subnet as hello cluster nodes.</span></span>

<span data-ttu-id="e690b-281">Привет, следуя PowerShell создается отказоустойчивый кластер.</span><span class="sxs-lookup"><span data-stu-id="e690b-281">hello following PowerShell creates a failover cluster.</span></span> <span data-ttu-id="e690b-282">Обновление hello скрипт с hello имена узлов hello (приветствия имен виртуальных машин) и доступные IP-адрес из hello виртуальной сети Azure:</span><span class="sxs-lookup"><span data-stu-id="e690b-282">Update hello script with hello names of hello nodes (hello virtual machine names) and an available IP address from hello Azure VNET:</span></span>

```PowerShell
New-Cluster -Name <FailoverCluster-Name> -Node ("<node1>","<node2>") –StaticAddress <n.n.n.n> -NoStorage
```   

### <a name="create-a-cloud-witness"></a><span data-ttu-id="e690b-283">Создание облака-свидетеля</span><span class="sxs-lookup"><span data-stu-id="e690b-283">Create a cloud witness</span></span>

<span data-ttu-id="e690b-284">Облако-свидетель является новым типом свидетеля кворума кластера, хранящегося в Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="e690b-284">Cloud Witness is a new type of cluster quorum witness stored in an Azure Storage Blob.</span></span> <span data-ttu-id="e690b-285">Эта функция удаляет необходимость hello отдельной виртуальной машины, размещение общей папке следящего сервера.</span><span class="sxs-lookup"><span data-stu-id="e690b-285">This removes hello need of a separate VM hosting a witness share.</span></span>

1. <span data-ttu-id="e690b-286">[Создание облачных следящего сервера для hello отказоустойчивого кластера](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span><span class="sxs-lookup"><span data-stu-id="e690b-286">[Create a cloud witness for hello failover cluster](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness).</span></span>

1. <span data-ttu-id="e690b-287">Создайте контейнер больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="e690b-287">Create a blob container.</span></span>

1. <span data-ttu-id="e690b-288">Сохраните ключи доступа hello и URL-адрес контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-288">Save hello access keys and hello container URL.</span></span>

1. <span data-ttu-id="e690b-289">Настройка следящего сервера кворума кластера hello отказоустойчивого кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-289">Configure hello failover cluster cluster quorum witness.</span></span> <span data-ttu-id="e690b-290">В разделе, [Настройка свидетеля кворума hello в пользовательском интерфейсе hello]. (http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) в hello пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e690b-290">See, [Configure hello quorum witness in hello user interface].(http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness#to-configure-cloud-witness-as-a-quorum-witness) in hello UI.</span></span>

### <a name="add-storage"></a><span data-ttu-id="e690b-291">Добавление хранилища.</span><span class="sxs-lookup"><span data-stu-id="e690b-291">Add storage</span></span>

<span data-ttu-id="e690b-292">Hello дисков для S2D должны toobe пустой и без секций или других данных.</span><span class="sxs-lookup"><span data-stu-id="e690b-292">hello disks for S2D need toobe empty and without partitions or other data.</span></span> <span data-ttu-id="e690b-293">Выполните дисков tooclean [hello шаги данного руководства](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span><span class="sxs-lookup"><span data-stu-id="e690b-293">tooclean disks follow [hello steps in this guide](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-34-clean-disks).</span></span>

1. <span data-ttu-id="e690b-294">[Включите локальные дисковые пространства \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="e690b-294">[Enable Store Spaces Direct \(S2D\)](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-35-enable-storage-spaces-direct).</span></span>

   <span data-ttu-id="e690b-295">Привет, следуя PowerShell позволяет дисковые пространства прямого подключения.</span><span class="sxs-lookup"><span data-stu-id="e690b-295">hello following PowerShell enables storage spaces direct.</span></span>  

   ```PowerShell
   Enable-ClusterS2D
   ```

   <span data-ttu-id="e690b-296">В **Диспетчер отказоустойчивости кластеров**, теперь можно увидеть hello пула носителей.</span><span class="sxs-lookup"><span data-stu-id="e690b-296">In **Failover Cluster Manager**, you can now see hello storage pool.</span></span>

1. <span data-ttu-id="e690b-297">[Создайте том](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span><span class="sxs-lookup"><span data-stu-id="e690b-297">[Create a volume](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct#step-36-create-volumes).</span></span>

   <span data-ttu-id="e690b-298">Одной из функций hello S2D является, он автоматически создается пул носителей при его включении.</span><span class="sxs-lookup"><span data-stu-id="e690b-298">One of hello features of S2D is that it automatically creates a storage pool when you enable it.</span></span> <span data-ttu-id="e690b-299">Теперь вы находитесь готов toocreate тома.</span><span class="sxs-lookup"><span data-stu-id="e690b-299">You are now ready toocreate a volume.</span></span> <span data-ttu-id="e690b-300">Здравствуйте, командлет PowerShell `New-Volume` автоматизирует процесс создания тома hello, включая форматирование, добавление toohello кластера и создание общий том кластера (CSV).</span><span class="sxs-lookup"><span data-stu-id="e690b-300">hello PowerShell commandlet `New-Volume` automates hello volume creation process, including formatting, adding toohello cluster, and creating a cluster shared volume (CSV).</span></span> <span data-ttu-id="e690b-301">Следующий пример Hello создает 800 ГБ CSV.</span><span class="sxs-lookup"><span data-stu-id="e690b-301">hello following example creates an 800 gigabyte (GB) CSV.</span></span>

   ```PowerShell
   New-Volume -StoragePoolFriendlyName S2D* -FriendlyName VDisk01 -FileSystem CSVFS_REFS -Size 800GB
   ```   

   <span data-ttu-id="e690b-302">После выполнения этой команды том емкостью 800 ГБ подключается как ресурс кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-302">After this command completes, an 800 GB volume is mounted as a cluster resource.</span></span> <span data-ttu-id="e690b-303">том Hello в `C:\ClusterStorage\Volume1\`.</span><span class="sxs-lookup"><span data-stu-id="e690b-303">hello volume is at `C:\ClusterStorage\Volume1\`.</span></span>

   <span data-ttu-id="e690b-304">Привет, следующая схема показывает общий том кластера с S2D:</span><span class="sxs-lookup"><span data-stu-id="e690b-304">hello following diagram shows a cluster shared volume with S2D:</span></span>

   ![ClusterSharedVolume](./media/virtual-machines-windows-portal-sql-create-failover-cluster/15-cluster-shared-volume.png)

## <a name="step-3-test-failover-cluster-failover"></a><span data-ttu-id="e690b-306">Шаг 3. Тестирование отработки отказа отказоустойчивого кластера</span><span class="sxs-lookup"><span data-stu-id="e690b-306">Step 3: Test failover cluster failover</span></span>

<span data-ttu-id="e690b-307">В диспетчере отказоустойчивости кластеров, убедитесь, что можно переместить toohello ресурсов хранилища hello другой узел кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-307">In Failover Cluster Manager, verify that you can move hello storage resource toohello other cluster node.</span></span> <span data-ttu-id="e690b-308">Если вы можете подключиться toohello отказоустойчивый кластер с **Диспетчер отказоустойчивости кластеров** и переместить хранилище hello из одного узла toohello других, вы готовы tooconfigure hello отказоустойчивого Кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-308">If you can connect toohello failover cluster with **Failover Cluster Manager** and move hello storage from one node toohello other, you are ready tooconfigure hello FCI.</span></span>

## <a name="step-4-create-sql-server-fci"></a><span data-ttu-id="e690b-309">Шаг 4. Создание экземпляра отказоустойчивого кластера SQL Server</span><span class="sxs-lookup"><span data-stu-id="e690b-309">Step 4: Create SQL Server FCI</span></span>

<span data-ttu-id="e690b-310">После настройки hello отказоустойчивого кластера и все компоненты кластера, включая хранилище можно создать hello отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-310">After you have configured hello failover cluster and all cluster components including storage, you can create hello SQL Server FCI.</span></span>

1. <span data-ttu-id="e690b-311">Первая виртуальная машина toohello подключитесь с помощью протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="e690b-311">Connect toohello first virtual machine with RDP.</span></span>

1. <span data-ttu-id="e690b-312">В **Диспетчер отказоустойчивости кластеров**, убедитесь, что все основные ресурсы кластера на первой виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-312">In **Failover Cluster Manager**, make sure all cluster core resources are on hello first virtual machine.</span></span> <span data-ttu-id="e690b-313">При необходимости переместите все ресурсы toothis виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="e690b-313">If necessary, move all resources toothis virtual machine.</span></span>

1. <span data-ttu-id="e690b-314">Найдите hello установочного носителя.</span><span class="sxs-lookup"><span data-stu-id="e690b-314">Locate hello installation media.</span></span> <span data-ttu-id="e690b-315">Если виртуальная машина hello использует одно из изображений hello Azure Marketplace, hello мультимедиа находится в `C:\SQLServer_<version number>_Full`.</span><span class="sxs-lookup"><span data-stu-id="e690b-315">If hello virtual machine uses one of hello Azure Marketplace images, hello media is located at `C:\SQLServer_<version number>_Full`.</span></span> <span data-ttu-id="e690b-316">Щелкните **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="e690b-316">Click **Setup**.</span></span>

1. <span data-ttu-id="e690b-317">В hello **центр установки SQL Server**, нажмите кнопку **установки**.</span><span class="sxs-lookup"><span data-stu-id="e690b-317">In hello **SQL Server Installation Center**, click **Installation**.</span></span>

1. <span data-ttu-id="e690b-318">Щелкните **Новая установка отказоустойчивого кластера SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e690b-318">Click **New SQL Server failover cluster installation**.</span></span> <span data-ttu-id="e690b-319">Следуйте инструкциям hello приветствия мастера tooinstall hello отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-319">Follow hello instructions in hello wizard tooinstall hello SQL Server FCI.</span></span>

   <span data-ttu-id="e690b-320">каталоги данных Hello отказоустойчивого Кластера должны toobe на кластерных хранилищ.</span><span class="sxs-lookup"><span data-stu-id="e690b-320">hello FCI data directories need toobe on clustered storage.</span></span> <span data-ttu-id="e690b-321">С S2D он не общий диск, но tooa точки подключения тома на каждом сервере.</span><span class="sxs-lookup"><span data-stu-id="e690b-321">With S2D, it's not a shared disk, but a mount point tooa volume on each server.</span></span> <span data-ttu-id="e690b-322">S2D синхронизирует тома hello между обоих узлов.</span><span class="sxs-lookup"><span data-stu-id="e690b-322">S2D synchronizes hello volume between both nodes.</span></span> <span data-ttu-id="e690b-323">Hello тома выводится toohello кластера как общий том кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-323">hello volume is presented toohello cluster as a cluster shared volume.</span></span> <span data-ttu-id="e690b-324">Используйте точку подключения CSV hello каталогов данных hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-324">Use hello CSV mount point for hello data directories.</span></span>

   ![DataDirectories](./media/virtual-machines-windows-portal-sql-create-failover-cluster/20-data-dicrectories.png)

1. <span data-ttu-id="e690b-326">После завершения мастера hello, программа установки установит отказоустойчивого Кластера SQL Server на первом узле hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-326">After you complete hello wizard, Setup will install a SQL Server FCI on hello first node.</span></span>

1. <span data-ttu-id="e690b-327">После успешного Установка hello отказоустойчивого Кластера на первом узле hello, подключиться toohello второго узла с помощью протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="e690b-327">After Setup successfully installs hello FCI on hello first node, connect toohello second node with RDP.</span></span>

1. <span data-ttu-id="e690b-328">Откройте hello **центр установки SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e690b-328">Open hello **SQL Server Installation Center**.</span></span> <span data-ttu-id="e690b-329">Щелкните **Установка**.</span><span class="sxs-lookup"><span data-stu-id="e690b-329">Click **Installation**.</span></span>

1. <span data-ttu-id="e690b-330">Нажмите кнопку **отказоустойчивого кластера SQL Server tooa добавить узел**.</span><span class="sxs-lookup"><span data-stu-id="e690b-330">Click **Add node tooa SQL Server failover cluster**.</span></span> <span data-ttu-id="e690b-331">Следуйте инструкциям hello приветствия мастера tooinstall SQL server и добавьте этот сервер toohello отказоустойчивого Кластера.</span><span class="sxs-lookup"><span data-stu-id="e690b-331">Follow hello instructions in hello wizard tooinstall SQL server and add this server toohello FCI.</span></span>

   >[!NOTE]
   ><span data-ttu-id="e690b-332">При использовании образа коллекции Azure Marketplace с SQL Server средств SQL Server были включены с помощью образа hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-332">If you used an Azure Marketplace gallery image with SQL Server, SQL Server tools were included with hello image.</span></span> <span data-ttu-id="e690b-333">Если вы не использовали этот образ, установите средства SQL Server hello отдельно.</span><span class="sxs-lookup"><span data-stu-id="e690b-333">If you did not use this image, install hello SQL Server tools separately.</span></span> <span data-ttu-id="e690b-334">См. сведения в статье [Скачивание SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="e690b-334">See [Download SQL Server Management Studio (SSMS)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="step-5-create-azure-load-balancer"></a><span data-ttu-id="e690b-335">Шаг 5.Создание Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e690b-335">Step 5: Create Azure load balancer</span></span>

<span data-ttu-id="e690b-336">На виртуальных машинах Azure кластеров с помощью toohold подсистемы балансировки нагрузки IP-адрес, который должен toobe на одном узле кластера одновременно.</span><span class="sxs-lookup"><span data-stu-id="e690b-336">On Azure virtual machines, clusters use a load balancer toohold an IP address that needs toobe on one cluster node at a time.</span></span> <span data-ttu-id="e690b-337">В этом решении балансировки нагрузки hello содержит hello IP-адрес для hello отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-337">In this solution, hello load balancer holds hello IP address for hello SQL Server FCI.</span></span>

<span data-ttu-id="e690b-338">[Создайте и настройте балансировщик нагрузки Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span><span class="sxs-lookup"><span data-stu-id="e690b-338">[Create and configure an Azure load balancer](virtual-machines-windows-portal-sql-availability-group-tutorial.md#configure-internal-load-balancer).</span></span>

### <a name="create-hello-load-balancer-in-hello-azure-portal"></a><span data-ttu-id="e690b-339">Создание hello балансировки нагрузки в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="e690b-339">Create hello load balancer in hello Azure portal</span></span>

<span data-ttu-id="e690b-340">Подсистема балансировки нагрузки hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="e690b-340">toocreate hello load balancer:</span></span>

1. <span data-ttu-id="e690b-341">В hello портал Azure перейдите toohello группы ресурсов с виртуальными машинами hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-341">In hello Azure portal, go toohello Resource Group with hello virtual machines.</span></span>

1. <span data-ttu-id="e690b-342">Щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e690b-342">Click **+ Add**.</span></span> <span data-ttu-id="e690b-343">Поиск hello Marketplace для **балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="e690b-343">Search hello Marketplace for **Load Balancer**.</span></span> <span data-ttu-id="e690b-344">Щелкните **Балансировщик нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="e690b-344">Click **Load Balancer**.</span></span>

1. <span data-ttu-id="e690b-345">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e690b-345">Click **Create**.</span></span>

1. <span data-ttu-id="e690b-346">Настройка балансировки нагрузки hello с:</span><span class="sxs-lookup"><span data-stu-id="e690b-346">Configure hello load balancer with:</span></span>

   - <span data-ttu-id="e690b-347">**Имя**: имя, идентифицирующее hello подсистемы балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e690b-347">**Name**: A name that identifies hello load balancer.</span></span>
   - <span data-ttu-id="e690b-348">**Тип**: hello балансировки нагрузки может быть открытой или закрытой.</span><span class="sxs-lookup"><span data-stu-id="e690b-348">**Type**: hello load balancer can be either public or private.</span></span> <span data-ttu-id="e690b-349">Балансировщик нагрузки закрытый может осуществляться в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e690b-349">A private load balancer can be accessed from within hello same VNET.</span></span> <span data-ttu-id="e690b-350">Большинство приложений Azure могут использовать закрытый балансировщик нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e690b-350">Most Azure applications can use a private load balancer.</span></span> <span data-ttu-id="e690b-351">Если приложению доступа tooSQL сервер непосредственно через Интернет hello используется внешняя Подсистема балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e690b-351">If your application needs access tooSQL Server directly over hello Internet, use a public load balancer.</span></span>
   - <span data-ttu-id="e690b-352">**Виртуальная сеть**: hello сетевых как hello виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e690b-352">**Virtual Network**: hello same network as hello virtual machines.</span></span>
   - <span data-ttu-id="e690b-353">**Подсети**: hello подсети hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e690b-353">**Subnet**: hello same subnet as hello virtual machines.</span></span>
   - <span data-ttu-id="e690b-354">**Частный IP-адрес**: hello же IP-адрес, назначенный ресурсу сетевого кластера toohello отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-354">**Private IP address**: hello same IP address that you assigned toohello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="e690b-355">**Подписка.** Ваша подписка Azure.</span><span class="sxs-lookup"><span data-stu-id="e690b-355">**subscription**: Your Azure subscription.</span></span>
   - <span data-ttu-id="e690b-356">**Группа ресурсов**: используйте hello же группе ресурсов, что виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e690b-356">**Resource Group**: Use hello same resource group as your virtual machines.</span></span>
   - <span data-ttu-id="e690b-357">**Расположение**: используйте hello же расположению Azure, виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="e690b-357">**Location**: Use hello same Azure location as your virtual machines.</span></span>
   <span data-ttu-id="e690b-358">См. следующий рисунок hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-358">See hello following picture:</span></span>

   ![CreateLoadBalancer](./media/virtual-machines-windows-portal-sql-create-failover-cluster/30-load-balancer-create.png)

### <a name="configure-hello-load-balancer-backend-pool"></a><span data-ttu-id="e690b-360">Настройка внутреннего пула подсистемы балансировки нагрузки hello</span><span class="sxs-lookup"><span data-stu-id="e690b-360">Configure hello load balancer backend pool</span></span>

1. <span data-ttu-id="e690b-361">Возвращает toohello группы ресурсов Azure с виртуальными машинами hello и найдите hello новую подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e690b-361">Return toohello Azure Resource Group with hello virtual machines and locate hello new load balancer.</span></span> <span data-ttu-id="e690b-362">Может иметь вид hello toorefresh на hello группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="e690b-362">You may have toorefresh hello view on hello Resource Group.</span></span> <span data-ttu-id="e690b-363">Выберите hello подсистему балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="e690b-363">Click hello load balancer.</span></span>

1. <span data-ttu-id="e690b-364">В колонке подсистемы балансировки нагрузки hello, нажмите кнопку **внутренние пулы**.</span><span class="sxs-lookup"><span data-stu-id="e690b-364">On hello load balancer blade, click **Backend pools**.</span></span>

1. <span data-ttu-id="e690b-365">Нажмите кнопку **+ добавить** tooadd внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="e690b-365">Click **+ Add** tooadd a backend pool.</span></span>

1. <span data-ttu-id="e690b-366">Введите имя для hello внутренний пул.</span><span class="sxs-lookup"><span data-stu-id="e690b-366">Type a name for hello backend pool.</span></span>

1. <span data-ttu-id="e690b-367">Щелкните **Добавить виртуальную машину**.</span><span class="sxs-lookup"><span data-stu-id="e690b-367">Click **Add a virtual machine**.</span></span>

1. <span data-ttu-id="e690b-368">На hello **выберите виртуальные машины** колонка, щелкните **выберите группу доступности**.</span><span class="sxs-lookup"><span data-stu-id="e690b-368">On hello **Choose virtual machines** blade, click **Choose an availability set**.</span></span>

1. <span data-ttu-id="e690b-369">Выберите группу доступности hello помещен hello виртуальных машин SQL Server в.</span><span class="sxs-lookup"><span data-stu-id="e690b-369">Choose hello availability set that you placed hello SQL Server virtual machines in.</span></span>

1. <span data-ttu-id="e690b-370">На hello **выберите виртуальные машины** колонка, щелкните **выберите виртуальные машины hello**.</span><span class="sxs-lookup"><span data-stu-id="e690b-370">On hello **Choose virtual machines** blade, click **Choose hello virtual machines**.</span></span>

   <span data-ttu-id="e690b-371">Портал Azure должно иметь вид hello следующий рисунок:</span><span class="sxs-lookup"><span data-stu-id="e690b-371">Your Azure portal should look like hello following picture:</span></span>

   ![CreateLoadBalancerBackEnd](./media/virtual-machines-windows-portal-sql-create-failover-cluster/33-load-balancer-back-end.png)

1. <span data-ttu-id="e690b-373">Нажмите кнопку **выберите** на hello **выберите виртуальные машины** колонку.</span><span class="sxs-lookup"><span data-stu-id="e690b-373">Click **Select** on hello **Choose virtual machines** blade.</span></span>

1. <span data-ttu-id="e690b-374">Нажмите **ОК** дважды.</span><span class="sxs-lookup"><span data-stu-id="e690b-374">Click **OK** twice.</span></span>

### <a name="configure-a-load-balancer-health-probe"></a><span data-ttu-id="e690b-375">Настройка пробы работоспособности балансировщика нагрузки</span><span class="sxs-lookup"><span data-stu-id="e690b-375">Configure a load balancer health probe</span></span>

1. <span data-ttu-id="e690b-376">В колонке подсистемы балансировки нагрузки hello, нажмите кнопку **зонды работоспособности**.</span><span class="sxs-lookup"><span data-stu-id="e690b-376">On hello load balancer blade, click **Health probes**.</span></span>

1. <span data-ttu-id="e690b-377">Щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e690b-377">Click **+ Add**.</span></span>

1. <span data-ttu-id="e690b-378">На hello **проверки работоспособности добавить** колонке <a name="probe"> </a>задать параметры проверки работоспособности hello:</span><span class="sxs-lookup"><span data-stu-id="e690b-378">On hello **Add health probe** blade, <a name="probe"></a>Set hello health probe parameters:</span></span>

   - <span data-ttu-id="e690b-379">**Имя**: имя для проверки работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-379">**Name**: A name for hello health probe.</span></span>
   - <span data-ttu-id="e690b-380">**Протокол.** TCP.</span><span class="sxs-lookup"><span data-stu-id="e690b-380">**Protocol**: TCP.</span></span>
   - <span data-ttu-id="e690b-381">**Порт**: задать tooan доступный TCP-порт.</span><span class="sxs-lookup"><span data-stu-id="e690b-381">**Port**: Set tooan available TCP port.</span></span> <span data-ttu-id="e690b-382">Для этого порта требуется открытый порт брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="e690b-382">This port requires an open firewall port.</span></span> <span data-ttu-id="e690b-383">Используйте hello [тот же порт](#ports) , задаваемое для проверки работоспособности hello на брандмауэре hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-383">Use hello [same port](#ports) you set for hello health probe at hello firewall.</span></span>
   - <span data-ttu-id="e690b-384">**Интервал.** 5 секунд.</span><span class="sxs-lookup"><span data-stu-id="e690b-384">**Interval**: 5 Seconds.</span></span>
   - <span data-ttu-id="e690b-385">**Порог состояния неработоспособности.** 2 последовательных сбоя.</span><span class="sxs-lookup"><span data-stu-id="e690b-385">**Unhealthy threshold**: 2 consecutive failures.</span></span>

1. <span data-ttu-id="e690b-386">Нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="e690b-386">Click OK.</span></span>

### <a name="set-load-balancing-rules"></a><span data-ttu-id="e690b-387">Задание правил балансировки нагрузки</span><span class="sxs-lookup"><span data-stu-id="e690b-387">Set load balancing rules</span></span>

1. <span data-ttu-id="e690b-388">В колонке подсистемы балансировки нагрузки hello, нажмите кнопку **правила подсистемы балансировки нагрузки**.</span><span class="sxs-lookup"><span data-stu-id="e690b-388">On hello load balancer blade, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="e690b-389">Щелкните **+ Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e690b-389">Click **+ Add**.</span></span>

1. <span data-ttu-id="e690b-390">Задайте параметры правила балансировки нагрузки hello:</span><span class="sxs-lookup"><span data-stu-id="e690b-390">Set hello load balancing rules parameters:</span></span>

   - <span data-ttu-id="e690b-391">**Имя**: имя для правила подсистемы балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-391">**Name**: A name for hello load balancing rules.</span></span>
   - <span data-ttu-id="e690b-392">**Интерфейсный IP-адрес**: использовать hello IP-адрес для hello ресурса сети кластера для отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-392">**Frontend IP address**: Use hello IP address for hello SQL Server FCI cluster network resource.</span></span>
   - <span data-ttu-id="e690b-393">**Порт**: задать для hello порт TCP отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-393">**Port**: Set for hello SQL Server FCI TCP port.</span></span> <span data-ttu-id="e690b-394">порт экземпляра по умолчанию Hello: 1433.</span><span class="sxs-lookup"><span data-stu-id="e690b-394">hello default instance port is 1433.</span></span>
   - <span data-ttu-id="e690b-395">**Внутренний порт**: hello же порт использует это значение в качестве hello **порт** значение при включении **плавающий IP-адрес (прямой возврат сервера)**.</span><span class="sxs-lookup"><span data-stu-id="e690b-395">**Backend port**: This value uses hello same port as hello **Port** value when you enable **Floating IP (direct server return)**.</span></span>
   - <span data-ttu-id="e690b-396">**Внутренний пул**: имя пула внутренних hello использование ранее.</span><span class="sxs-lookup"><span data-stu-id="e690b-396">**Backend pool**: Use hello backend pool name that you configured earlier.</span></span>
   - <span data-ttu-id="e690b-397">**Проверка работоспособности**: проверка работоспособности hello использование ранее.</span><span class="sxs-lookup"><span data-stu-id="e690b-397">**Health probe**: Use hello health probe that you configured earlier.</span></span>
   - <span data-ttu-id="e690b-398">**Сохранение сеанса.** Нет.</span><span class="sxs-lookup"><span data-stu-id="e690b-398">**Session persistence**: None.</span></span>
   - <span data-ttu-id="e690b-399">**Время ожидания простоя (в минутах)**: 4.</span><span class="sxs-lookup"><span data-stu-id="e690b-399">**Idle timeout (minutes)**: 4.</span></span>
   - <span data-ttu-id="e690b-400">**Плавающий IP-адрес (direct server return).** Включено.</span><span class="sxs-lookup"><span data-stu-id="e690b-400">**Floating IP (direct server return)**: Enabled</span></span>

1. <span data-ttu-id="e690b-401">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e690b-401">Click **OK**.</span></span>

## <a name="step-6-configure-cluster-for-probe"></a><span data-ttu-id="e690b-402">Шаг 6. Настройка кластера для проверки</span><span class="sxs-lookup"><span data-stu-id="e690b-402">Step 6: Configure cluster for probe</span></span>

<span data-ttu-id="e690b-403">Параметр hello кластера пробы порт в PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e690b-403">Set hello cluster probe port parameter in PowerShell.</span></span>

<span data-ttu-id="e690b-404">tooset Здравствуйте параметр port проверки кластера, обновить переменные в hello следующий скрипт из среды.</span><span class="sxs-lookup"><span data-stu-id="e690b-404">tooset hello cluster probe port parameter, update variables in hello following script from your environment.</span></span>

  ```PowerShell
   $ClusterNetworkName = "<Cluster Network Name>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name).
   $IPResourceName = "IP Address Resource Name" # hello IP Address cluster resource name.
   $ILBIP = "<10.0.0.x>" # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
   [int]$ProbePort = <59999>

   Import-Module FailoverClusters

   Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
   ```


## <a name="step-7-test-fci-failover"></a><span data-ttu-id="e690b-405">Шаг 7. Проверка отработки отказа экземпляра отказоустойчивого кластера</span><span class="sxs-lookup"><span data-stu-id="e690b-405">Step 7: Test FCI failover</span></span>

<span data-ttu-id="e690b-406">Тестовая отработка отказа FCI toovalidate кластера функции hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-406">Test failover of hello FCI toovalidate cluster functionality.</span></span> <span data-ttu-id="e690b-407">Здравствуйте, следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e690b-407">Do hello following steps:</span></span>

1. <span data-ttu-id="e690b-408">Подключитесь tooone узлов кластера hello отказоустойчивого Кластера SQL Server с помощью протокола удаленного рабочего СТОЛА.</span><span class="sxs-lookup"><span data-stu-id="e690b-408">Connect tooone of hello SQL Server FCI cluster nodes with RDP.</span></span>

1. <span data-ttu-id="e690b-409">Откройте **диспетчер отказоустойчивости кластеров**.</span><span class="sxs-lookup"><span data-stu-id="e690b-409">Open **Failover Cluster Manager**.</span></span> <span data-ttu-id="e690b-410">Щелкните **Роли**.</span><span class="sxs-lookup"><span data-stu-id="e690b-410">Click **Roles**.</span></span> <span data-ttu-id="e690b-411">Обратите внимание, какой из узлов является владельцем роли hello отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-411">Notice which node owns hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="e690b-412">Щелкните правой кнопкой мыши роль hello отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-412">Right-click hello SQL Server FCI role.</span></span>

1. <span data-ttu-id="e690b-413">Щелкните **Переместить** и выберите **Лучший из возможных узлов**.</span><span class="sxs-lookup"><span data-stu-id="e690b-413">Click **Move** and click **Best Possible Node**.</span></span>

<span data-ttu-id="e690b-414">**Диспетчер отказоустойчивости кластеров** показано hello роли и его ресурсы переходят в автономный режим.</span><span class="sxs-lookup"><span data-stu-id="e690b-414">**Failover Cluster Manager** shows hello role and its resources go offline.</span></span> <span data-ttu-id="e690b-415">Hello ресурсы затем переместите и переходит в оперативный режим Здравствуйте, на другой узел.</span><span class="sxs-lookup"><span data-stu-id="e690b-415">hello resources then move and come online on hello other node.</span></span>

### <a name="test-connectivity"></a><span data-ttu-id="e690b-416">Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="e690b-416">Test connectivity</span></span>

<span data-ttu-id="e690b-417">возможность подключения tootest журнала tooanother виртуальной машине в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="e690b-417">tootest connectivity, log in tooanother virtual machine in hello same virtual network.</span></span> <span data-ttu-id="e690b-418">Откройте **SQL Server Management Studio** и подключите toohello имя отказоустойчивого Кластера SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e690b-418">Open **SQL Server Management Studio** and connect toohello SQL Server FCI name.</span></span>

>[!NOTE]
><span data-ttu-id="e690b-419">При необходимости можно [скачать SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="e690b-419">If necessary, you can [download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

## <a name="limitations"></a><span data-ttu-id="e690b-420">Ограничения</span><span class="sxs-lookup"><span data-stu-id="e690b-420">Limitations</span></span>
<span data-ttu-id="e690b-421">На виртуальных машинах Azure координатора распределенных транзакций (DTC) не поддерживается на отказоустойчивые кластеры, поскольку hello порта RPC не поддерживается подсистемой балансировки нагрузки hello.</span><span class="sxs-lookup"><span data-stu-id="e690b-421">On Azure virtual machines, Microsoft Distributed Transaction Coordinator (DTC) is not supported on FCIs because hello RPC port is not supported by hello load balancer.</span></span>

## <a name="see-also"></a><span data-ttu-id="e690b-422">См. также</span><span class="sxs-lookup"><span data-stu-id="e690b-422">See Also</span></span>

<span data-ttu-id="e690b-423">[Deploy a two-node S2D SOFS for UPD storage in Azure](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment) (Развертывание S2D SOFS с двумя узлами для хранилища UPD в Azure).</span><span class="sxs-lookup"><span data-stu-id="e690b-423">[Setup S2D with remote desktop (Azure)](http://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-storage-spaces-direct-deployment)</span></span>

<span data-ttu-id="e690b-424">[Гиперконвергентное решение с использованием локальных дисковых пространств в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span><span class="sxs-lookup"><span data-stu-id="e690b-424">[Hyper-converged solution with storage spaces direct](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct).</span></span>

<span data-ttu-id="e690b-425">[Локальные дисковые пространства в Windows Server 2016](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview).</span><span class="sxs-lookup"><span data-stu-id="e690b-425">[Storage Space Direct Overview](http://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)</span></span>

<span data-ttu-id="e690b-426">[SQL Server 2016 now supports Windows Server 2016 Storage Spaces Direct](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/) (SQL Server 2016 теперь поддерживает локальные дисковые пространства Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="e690b-426">[SQL Server support for S2D](https://blogs.technet.microsoft.com/dataplatforminsider/2016/09/27/sql-server-2016-now-supports-windows-server-2016-storage-spaces-direct/)</span></span>
