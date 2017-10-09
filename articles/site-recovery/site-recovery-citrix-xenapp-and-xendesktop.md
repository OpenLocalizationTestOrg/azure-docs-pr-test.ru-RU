---
title: "aaaReplicate развертывании многоуровневого Citrix XenDesktop и XenApp с помощью Azure Site Recovery | Документы Microsoft"
description: "В этой статье описывается как tooprotect и восстановление развертывания Citrix XenDesktop и XenApp с помощью Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: ponatara
manager: abhemraj
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: ponatara
ms.openlocfilehash: c4ea9f95f91c585cdcf9d776b02c0967f4c16ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-citrix-xenapp-and-xendesktop-deployment-using-azure-site-recovery"></a><span data-ttu-id="db502-103">Репликация многоуровневого развертывания Citrix XenApp и XenApp с помощью Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="db502-103">Replicate a multi-tier Citrix XenApp and XenDesktop deployment using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="db502-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="db502-104">Overview</span></span>

<span data-ttu-id="db502-105">Citrix XenDesktop — это решение виртуализации рабочего стола, которое предоставляет рабочие столы и приложения в виде ondemand tooany пользователя службы, в любом месте.</span><span class="sxs-lookup"><span data-stu-id="db502-105">Citrix XenDesktop is a desktop virtualization solution that delivers desktops and applications as an ondemand service tooany user, anywhere.</span></span> <span data-ttu-id="db502-106">С помощью технологии доставки FlexCast XenDesktop можно быстро и безопасно предоставлять приложения и toousers рабочие столы.</span><span class="sxs-lookup"><span data-stu-id="db502-106">With FlexCast delivery technology, XenDesktop can quickly and securely deliver applications and desktops toousers.</span></span>
<span data-ttu-id="db502-107">Сейчас Citrix XenApp не предоставляет возможности аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="db502-107">Today, Citrix XenApp does not provide any disaster recovery capabilities.</span></span>

<span data-ttu-id="db502-108">Это решение хорошо аварийного восстановления, следует разрешить моделирования планов восстановления вокруг hello выше архитектур сложных приложений и также имеют hello возможность tooadd настроенные действия toohandle для сопоставлений между различными уровнями таким образом обеспечивая одним щелчком, что снимок решения в событии hello аварии начальные tooa снижение RTO.</span><span class="sxs-lookup"><span data-stu-id="db502-108">A good disaster recovery solution, should allow modeling of recovery plans around hello above complex application architectures and also have hello ability tooadd customized steps toohandle application mappings between various tiers hence providing a single-click sure shot solution in hello event of a disaster leading tooa lower RTO.</span></span>

<span data-ttu-id="db502-109">Этот документ содержит пошаговое руководство для создания решения аварийного восстановления для локальных развертываний Citrix XenApp на платформах Hyper-V и VMware vSphere.</span><span class="sxs-lookup"><span data-stu-id="db502-109">This document provides a step-by-step guidance for building a disaster recovery solution for your on-premises Citrix XenApp deployments on Hyper-V and VMware vSphere platforms.</span></span> <span data-ttu-id="db502-110">В этом документе также описывается как tooperform тестовой отработки отказа (аварийного восстановления) и tooAzure внеплановой отработки отказа с использованием планов восстановления, hello поддерживаемые конфигурации и необходимые компоненты.</span><span class="sxs-lookup"><span data-stu-id="db502-110">This document also describes how tooperform a test failover(disaster recovery drill) and unplanned failover tooAzure using recovery plans, hello supported configurations and prerequisites.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="db502-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="db502-111">Prerequisites</span></span>

<span data-ttu-id="db502-112">Прежде чем начать, убедитесь, что вы понимаете следующие hello:</span><span class="sxs-lookup"><span data-stu-id="db502-112">Before you start, make sure you understand hello following:</span></span>

1. [<span data-ttu-id="db502-113">Репликация tooAzure виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="db502-113">Replicating a virtual machine tooAzure</span></span>](site-recovery-vmware-to-azure.md)
1. <span data-ttu-id="db502-114">Как слишком[проектирования сети восстановления](site-recovery-network-design.md)</span><span class="sxs-lookup"><span data-stu-id="db502-114">How too[design a recovery network](site-recovery-network-design.md)</span></span>
1. [<span data-ttu-id="db502-115">Выполнив tooAzure теста отработки отказа</span><span class="sxs-lookup"><span data-stu-id="db502-115">Doing a test failover tooAzure</span></span>](site-recovery-test-failover-to-azure.md)
1. [<span data-ttu-id="db502-116">Выполнив tooAzure отработки отказа</span><span class="sxs-lookup"><span data-stu-id="db502-116">Doing a failover tooAzure</span></span>](site-recovery-failover.md)
1. <span data-ttu-id="db502-117">Как слишком[репликации контроллера домена](site-recovery-active-directory.md)</span><span class="sxs-lookup"><span data-stu-id="db502-117">How too[replicate a domain controller](site-recovery-active-directory.md)</span></span>
1. <span data-ttu-id="db502-118">Как слишком[репликации SQL Server](site-recovery-sql.md)</span><span class="sxs-lookup"><span data-stu-id="db502-118">How too[replicate SQL Server](site-recovery-sql.md)</span></span>

## <a name="deployment-patterns"></a><span data-ttu-id="db502-119">Модели развертывания</span><span class="sxs-lookup"><span data-stu-id="db502-119">Deployment patterns</span></span>

<span data-ttu-id="db502-120">Citrix XenApp и XenDesktop фермы обычно имеет hello после развертывания шаблона.</span><span class="sxs-lookup"><span data-stu-id="db502-120">A Citrix XenApp and XenDesktop farm typically has hello following deployment pattern:</span></span>

<span data-ttu-id="db502-121">**Модель развертывания**</span><span class="sxs-lookup"><span data-stu-id="db502-121">**Deployment pattern**</span></span>

<span data-ttu-id="db502-122">Развертывание Citrix XenApp и XenDesktop с помощью DNS-сервера AD, сервера базы данных SQL, контролера доставки Citrix, сервера StoreFront, XenApp Master (VDA), сервера лицензирования Citrix XenApp</span><span class="sxs-lookup"><span data-stu-id="db502-122">Citrix XenApp and XenDesktop deployment with AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server</span></span>

![Модель развертывания 1](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-deployment.png)


## <a name="site-recovery-support"></a><span data-ttu-id="db502-124">Поддержка Site Recovery</span><span class="sxs-lookup"><span data-stu-id="db502-124">Site Recovery support</span></span>

<span data-ttu-id="db502-125">В целях hello в этой статье управляет Citrix развертывания на виртуальных машинах VMware vSphere 6.0 / System Center VMM 2012 R2 были используется toosetup аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="db502-125">For hello purpose of this article, Citrix deployments on VMware virtual machines managed by vSphere 6.0 / System Center VMM 2012 R2 were used toosetup DR.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="db502-126">Исходный и целевой объект</span><span class="sxs-lookup"><span data-stu-id="db502-126">Source and target</span></span>

<span data-ttu-id="db502-127">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="db502-127">**Scenario**</span></span> | <span data-ttu-id="db502-128">**tooa вторичного сайта**</span><span class="sxs-lookup"><span data-stu-id="db502-128">**tooa secondary site**</span></span> | <span data-ttu-id="db502-129">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="db502-129">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="db502-130">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="db502-130">**Hyper-V**</span></span> | <span data-ttu-id="db502-131">За пределами области</span><span class="sxs-lookup"><span data-stu-id="db502-131">Not in scope</span></span> | <span data-ttu-id="db502-132">Да</span><span class="sxs-lookup"><span data-stu-id="db502-132">Yes</span></span>
<span data-ttu-id="db502-133">**VMware**</span><span class="sxs-lookup"><span data-stu-id="db502-133">**VMware**</span></span> | <span data-ttu-id="db502-134">За пределами области</span><span class="sxs-lookup"><span data-stu-id="db502-134">Not in scope</span></span> | <span data-ttu-id="db502-135">Да</span><span class="sxs-lookup"><span data-stu-id="db502-135">Yes</span></span>
<span data-ttu-id="db502-136">**Физический сервер**</span><span class="sxs-lookup"><span data-stu-id="db502-136">**Physical server**</span></span> | <span data-ttu-id="db502-137">За пределами области</span><span class="sxs-lookup"><span data-stu-id="db502-137">Not in scope</span></span> | <span data-ttu-id="db502-138">Да</span><span class="sxs-lookup"><span data-stu-id="db502-138">Yes</span></span>

### <a name="versions"></a><span data-ttu-id="db502-139">Версии</span><span class="sxs-lookup"><span data-stu-id="db502-139">Versions</span></span>
<span data-ttu-id="db502-140">Клиенты могут развертывать компоненты XenApp в качестве физических серверов или виртуальных машин под управлением Hyper-V или VMware.</span><span class="sxs-lookup"><span data-stu-id="db502-140">Customers can deploy XenApp components as Virtual Machines running on Hyper-V or VMware or as Physical Servers.</span></span> <span data-ttu-id="db502-141">Azure Site Recovery можно защитить tooAzure обоих развертываний физическими и виртуальными.</span><span class="sxs-lookup"><span data-stu-id="db502-141">Azure Site Recovery can protect both physical and virtual deployments tooAzure.</span></span>
<span data-ttu-id="db502-142">Поскольку XenApp 7,7 или более поздней версии поддерживаются в Azure, только для развертываний с этих версий возможен переход tooAzure для аварийного восстановления или миграции.</span><span class="sxs-lookup"><span data-stu-id="db502-142">Since XenApp 7.7 or later is supported in Azure, only deployments with these versions can be failed over tooAzure for Disaster Recovery or migration.</span></span>

### <a name="things-tookeep-in-mind"></a><span data-ttu-id="db502-143">Действия tookeep помнить</span><span class="sxs-lookup"><span data-stu-id="db502-143">Things tookeep in mind</span></span>

1. <span data-ttu-id="db502-144">Защита и восстановление локальных развертываний с помощью toodeliver машины ОС Server XenApp опубликованных приложений и XenApp опубликованных рабочих столов поддерживается.</span><span class="sxs-lookup"><span data-stu-id="db502-144">Protection and recovery of on-premises deployments using Server OS machines toodeliver XenApp published apps and XenApp published desktops is supported.</span></span>

2. <span data-ttu-id="db502-145">Защита и восстановление для локальных развертываний с помощью рабочего стола toodeliver машины ОС СТОЛОВ для виртуальных рабочих столов клиента, включая Windows 10 не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="db502-145">Protection and recovery of on-premises deployments using desktop OS machines toodeliver Desktop VDI for client virtual desktops, including Windows 10, is not supported.</span></span> <span data-ttu-id="db502-146">Это происходит потому ASR не поддерживает восстановление hello машин с рабочего стола OS'es.</span><span class="sxs-lookup"><span data-stu-id="db502-146">This is because ASR does not support hello recovery of machines with desktop OS’es.</span></span>  <span data-ttu-id="db502-147">Кроме того, лицензирование некоторых особенностей виртуального рабочего стола клиента (например,</span><span class="sxs-lookup"><span data-stu-id="db502-147">Also, some client virtual desktop flavours (eg.</span></span> <span data-ttu-id="db502-148">Windows 7) еще не поддерживается в Azure.</span><span class="sxs-lookup"><span data-stu-id="db502-148">Windows 7) are not yet supported for licensing in Azure.</span></span> <span data-ttu-id="db502-149">Дополнительные сведения о лицензировании рабочих столов клиента и сервера в Azure см. [здесь](https://azure.microsoft.com/pricing/licensing-faq/).</span><span class="sxs-lookup"><span data-stu-id="db502-149">[Learn More](https://azure.microsoft.com/pricing/licensing-faq/) about licensing for client/server desktops in Azure.</span></span>

3.  <span data-ttu-id="db502-150">С помощью Azure Site Recovery нельзя выполнить репликацию и защиту имеющихся локальных клонов MCS или PVS.</span><span class="sxs-lookup"><span data-stu-id="db502-150">Azure Site Recovery cannot replicate and protect existing on-premises MCS or PVS clones.</span></span>
<span data-ttu-id="db502-151">Необходимо toorecreate клонированного с помощью надежного обмена Сообщениями Azure подготовки из контроллера доставки.</span><span class="sxs-lookup"><span data-stu-id="db502-151">You need toorecreate these clones using Azure RM provisioning from Delivery controller.</span></span>

4. <span data-ttu-id="db502-152">NetScaler невозможно защитить с помощью Azure Site Recovery, так как NetScaler, основана на FreeBSD и Azure Site Recovery, не поддерживает защиту ОС FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="db502-152">NetScaler cannot be protected using Azure Site Recovery as NetScaler is based on FreeBSD and Azure Site Recovery does not support protection of FreeBSD OS.</span></span> <span data-ttu-id="db502-153">Будет необходимо toodeploy и настроить новое устройство NetScaler из рынок Azure после отработки отказа tooAzure.</span><span class="sxs-lookup"><span data-stu-id="db502-153">You would need toodeploy and configure a new NetScaler appliance from Azure Market place after failover tooAzure.</span></span>


## <a name="replicating-virtual-machines"></a><span data-ttu-id="db502-154">Репликация виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="db502-154">Replicating virtual machines</span></span>

<span data-ttu-id="db502-155">следующие компоненты hello развертывания Citrix XenApp Hello должны toobe защищенных tooenable репликации и восстановления.</span><span class="sxs-lookup"><span data-stu-id="db502-155">hello following components of hello Citrix XenApp deployment need toobe protected tooenable replication and recovery.</span></span>

* <span data-ttu-id="db502-156">DNS-сервер AD;</span><span class="sxs-lookup"><span data-stu-id="db502-156">Protection of AD DNS server</span></span>
* <span data-ttu-id="db502-157">сервер базы данных SQL;</span><span class="sxs-lookup"><span data-stu-id="db502-157">Protection of SQL database server</span></span>
* <span data-ttu-id="db502-158">контроллер доставки Citrix;</span><span class="sxs-lookup"><span data-stu-id="db502-158">Protection of Citrix Delivery Controller</span></span>
* <span data-ttu-id="db502-159">защита сервера StoreFront;</span><span class="sxs-lookup"><span data-stu-id="db502-159">Protection of StoreFront server.</span></span>
* <span data-ttu-id="db502-160">защита XenApp Master (VDA);</span><span class="sxs-lookup"><span data-stu-id="db502-160">Protection of XenApp Master (VDA)</span></span>
* <span data-ttu-id="db502-161">защита сервера лицензирования Citrix XenApp.</span><span class="sxs-lookup"><span data-stu-id="db502-161">Protection of Citrix XenApp License Server</span></span>


<span data-ttu-id="db502-162">**Репликация DNS-сервера AD**</span><span class="sxs-lookup"><span data-stu-id="db502-162">**AD DNS server replication**</span></span>

<span data-ttu-id="db502-163">См. слишком[защиты Active Directory и DNS с помощью Azure Site Recovery](site-recovery-active-directory.md) на руководство по репликации и настройка контроллера домена в Azure.</span><span class="sxs-lookup"><span data-stu-id="db502-163">Please refer too[Protect Active Directory and DNS with Azure Site Recovery](site-recovery-active-directory.md) on guidance for replicating and configuring a domain controller in Azure.</span></span>

<span data-ttu-id="db502-164">**Репликация сервера базы данных SQL**</span><span class="sxs-lookup"><span data-stu-id="db502-164">**SQL database Server replication**</span></span>

<span data-ttu-id="db502-165">См. слишком[защиты SQL Server с помощью аварийного восстановления SQL Server и Azure Site Recovery](site-recovery-sql.md) подробное техническое руководство по hello рекомендуется использовать параметры для защиты серверов SQL Server.</span><span class="sxs-lookup"><span data-stu-id="db502-165">Please refer too[Protect SQL Server with SQL Server disaster recovery and Azure Site Recovery](site-recovery-sql.md) for detailed technical guidance on hello recommended options for protecting SQL servers.</span></span>

<span data-ttu-id="db502-166">Выполните [в этом руководстве](site-recovery-vmware-to-azure.md) репликации toostart hello tooAzure виртуальных машин других компонентов.</span><span class="sxs-lookup"><span data-stu-id="db502-166">Follow [this guidance](site-recovery-vmware-to-azure.md) toostart replicating hello other component virtual machines tooAzure.</span></span>

![Защита компонентов XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-enablereplication.png)

<span data-ttu-id="db502-168">**Параметры вычислений и сети**</span><span class="sxs-lookup"><span data-stu-id="db502-168">**Compute and Network Settings**</span></span>

<span data-ttu-id="db502-169">После защищенных машин hello вычислений hello (отображает состояние как «Protected» в группе репликации элементов), и параметры сети требуется настроить toobe.</span><span class="sxs-lookup"><span data-stu-id="db502-169">After hello machines are protected (status shows as “Protected” under Replicated Items), hello Compute and Network settings need toobe configured.</span></span>
<span data-ttu-id="db502-170">В вычисления и сеть > вычислений свойства, можно указать имя и целевой размер виртуальной Машины Azure hello.</span><span class="sxs-lookup"><span data-stu-id="db502-170">In Compute and Network > Compute properties, you can specify hello Azure VM name and target size.</span></span>
<span data-ttu-id="db502-171">Если вам нужно, измените toocomply имя hello требованиям Azure.</span><span class="sxs-lookup"><span data-stu-id="db502-171">Modify hello name toocomply with Azure requirements if you need to.</span></span> <span data-ttu-id="db502-172">Кроме того, можно просматривать и добавлять сведения о hello целевой сети, подсети и IP-адрес, который будет назначен toohello виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="db502-172">You can also view and add information about hello target network, subnet, and IP address that will be assigned toohello Azure VM.</span></span>

<span data-ttu-id="db502-173">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="db502-173">Note hello following:</span></span>

* <span data-ttu-id="db502-174">Можно задать hello конечный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="db502-174">You can set hello target IP address.</span></span> <span data-ttu-id="db502-175">Если вы не укажете, при сбое машины hello будет использовать DHCP.</span><span class="sxs-lookup"><span data-stu-id="db502-175">If you don't provide an address, hello failed over machine will use DHCP.</span></span> <span data-ttu-id="db502-176">Если адрес, который недоступен в отработки отказа, отработка отказа hello не сработает.</span><span class="sxs-lookup"><span data-stu-id="db502-176">If you set an address that isn't available at failover, hello failover won't work.</span></span> <span data-ttu-id="db502-177">Здравствуйте, одинаковый целевой IP-адрес можно использовать для тестовой отработки отказа, если доступен адрес hello в hello тестовой отработки отказа сети.</span><span class="sxs-lookup"><span data-stu-id="db502-177">hello same target IP address can be used for test failover if hello address is available in hello test failover network.</span></span>

* <span data-ttu-id="db502-178">Для hello AD или DNS-сервера сохраняя hello локального адреса определяет hello же адрес как hello DNS-сервер для hello Azure виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="db502-178">For hello AD/DNS server, retaining hello on-premises address lets you specify hello same address as hello DNS server for hello Azure Virtual network.</span></span>

<span data-ttu-id="db502-179">Hello число сетевых адаптеров определяется размер hello, указываемые для hello целевой виртуальной машине, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="db502-179">hello number of network adapters is dictated by hello size you specify for hello target virtual machine, as follows:</span></span>

*   <span data-ttu-id="db502-180">Если hello количество сетевых адаптеров на исходном компьютере hello меньше или равно toohello число адаптеров разрешено hello целевой машине размером, а затем целевой hello будут иметь одинаковое число адаптеров как источник hello hello.</span><span class="sxs-lookup"><span data-stu-id="db502-180">If hello number of network adapters on hello source machine is less than or equal toohello number of adapters allowed for hello target machine size, then hello target will have hello same number of adapters as hello source.</span></span>
*   <span data-ttu-id="db502-181">Если hello число адаптеров для hello исходной виртуальной машины превышает допустимое hello для hello целевого размера, а затем максимальный размер целевой hello будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="db502-181">If hello number of adapters for hello source virtual machine exceeds hello number allowed for hello target size then hello target size maximum will be used.</span></span>
* <span data-ttu-id="db502-182">Например если исходная машина имеет два сетевых адаптера, hello целевой машине размер поддерживает четыре hello целевой компьютер будет иметь два адаптера.</span><span class="sxs-lookup"><span data-stu-id="db502-182">For example, if a source machine has two network adapters and hello target machine size supports four, hello target machine will have two adapters.</span></span> <span data-ttu-id="db502-183">Если hello исходный компьютер имеет два адаптера, но hello поддерживаемые целевой размер поддерживает только один hello целевой компьютер будет только один адаптер.</span><span class="sxs-lookup"><span data-stu-id="db502-183">If hello source machine has two adapters but hello supported target size only supports one then hello target machine will have only one adapter.</span></span>
*   <span data-ttu-id="db502-184">Если виртуальная машина hello имеет несколько сетевых адаптеров все они подключатся toohello одной сети.</span><span class="sxs-lookup"><span data-stu-id="db502-184">If hello virtual machine has multiple network adapters they will all connect toohello same network.</span></span>
*   <span data-ttu-id="db502-185">Если hello виртуальной машины с несколькими сетевыми адаптерами, hello первый отображаются в списке hello становится hello по умолчанию сетевой адаптер в виртуальной машине Azure hello.</span><span class="sxs-lookup"><span data-stu-id="db502-185">If hello virtual machine has multiple network adapters, then hello first one shown in hello list becomes hello Default network adapter in hello Azure virtual machine.</span></span>


## <a name="creating-a-recovery-plan"></a><span data-ttu-id="db502-186">Создание плана восстановления</span><span class="sxs-lookup"><span data-stu-id="db502-186">Creating a recovery plan</span></span>

<span data-ttu-id="db502-187">После включения репликации для виртуальных машин компонент XenApp hello hello следующим шагом является toocreate план восстановления.</span><span class="sxs-lookup"><span data-stu-id="db502-187">After replication is enabled for hello XenApp component VMs, hello next step is toocreate a recovery plan.</span></span>
<span data-ttu-id="db502-188">Группы плана восстановления объединяют виртуальные машины с аналогичными требованиями для выполнения отработки отказа и восстановления.</span><span class="sxs-lookup"><span data-stu-id="db502-188">A recovery plan groups together virtual machines with similar requirements for failover and recovery.</span></span>  

<span data-ttu-id="db502-189">**Действия toocreate плана восстановления**</span><span class="sxs-lookup"><span data-stu-id="db502-189">**Steps toocreate a recovery plan**</span></span>

1. <span data-ttu-id="db502-190">Добавление hello XenApp компонент виртуальных машин в план восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="db502-190">Add hello XenApp component virtual machines in hello Recovery Plan.</span></span>
2. <span data-ttu-id="db502-191">Выберите "Планы восстановления" > + Recovery Plan (Добавить план восстановления).</span><span class="sxs-lookup"><span data-stu-id="db502-191">Click Recovery Plans -> + Recovery Plan.</span></span> <span data-ttu-id="db502-192">Укажите имя для плана восстановления hello интуитивно понятными.</span><span class="sxs-lookup"><span data-stu-id="db502-192">Provide an intuitive name for hello recovery plan.</span></span>
3. <span data-ttu-id="db502-193">Для виртуальных машин VMware в качестве источника выберите сервер обработки VMware, в качестве целевого объекта — Microsoft Azure, а в качестве модели развертывания — диспетчер ресурсов и щелкните "Выбор элементов".</span><span class="sxs-lookup"><span data-stu-id="db502-193">For VMware virtual machines: Select source as VMware process server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items.</span></span>
4. <span data-ttu-id="db502-194">Для виртуальных машин Hyper-V: выберите источник, что и сервер VMM, целевых как Microsoft Azure и модель развертывания как диспетчер ресурсов и щелкнуть выбора элементов и выберите hello XenApp развертывания виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="db502-194">For Hyper-V virtual machines: Select source as VMM server, target as Microsoft Azure, and deployment model as Resource Manager and click on Select items and then select hello XenApp deployment VMs.</span></span>

### <a name="adding-virtual-machines-toofailover-groups"></a><span data-ttu-id="db502-195">Добавление групп toofailover виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="db502-195">Adding virtual machines toofailover groups</span></span>

<span data-ttu-id="db502-196">Планы восстановления может быть tooadd настраиваемые группы перехода на другой ресурс для запуска конкретного заказа, скриптов или ручных действий.</span><span class="sxs-lookup"><span data-stu-id="db502-196">Recovery plans can be customized tooadd failover groups for specific startup order, scripts or manual actions.</span></span> <span data-ttu-id="db502-197">следующие группы Hello должны плана восстановления добавлены toohello toobe.</span><span class="sxs-lookup"><span data-stu-id="db502-197">hello following groups need toobe added toohello recovery plan.</span></span>

1. <span data-ttu-id="db502-198">1 группа отработки отказа: DNS-сервер AD.</span><span class="sxs-lookup"><span data-stu-id="db502-198">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="db502-199">2 группа отработки отказа: виртуальные машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="db502-199">Failover Group2: SQL Server VMs</span></span>
2. <span data-ttu-id="db502-200">3 группа отработки отказа: виртуальная машина с образом VDA Master.</span><span class="sxs-lookup"><span data-stu-id="db502-200">Failover Group3: VDA Master Image VM</span></span>
3. <span data-ttu-id="db502-201">4 группа отработки отказа: контроллер доставки и виртуальные машины сервера StoreFront.</span><span class="sxs-lookup"><span data-stu-id="db502-201">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>


### <a name="adding-scripts-toohello-recovery-plan"></a><span data-ttu-id="db502-202">Добавление плана восстановления toohello сценариев</span><span class="sxs-lookup"><span data-stu-id="db502-202">Adding scripts toohello recovery plan</span></span>

<span data-ttu-id="db502-203">Скрипты могут выполняться до или после определенной группы в плане восстановления.</span><span class="sxs-lookup"><span data-stu-id="db502-203">Scripts can be run before or after a specific group in a recovery plan.</span></span> <span data-ttu-id="db502-204">Выполняемые вручную действия могут быть также включены и выполняться во время отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="db502-204">Manual actions can be also be included and performed during failover.</span></span>

<span data-ttu-id="db502-205">план восстановления, настроенные Hello выглядит следующим образом hello ниже.</span><span class="sxs-lookup"><span data-stu-id="db502-205">hello customized recovery plan looks like hello below:</span></span>

1. <span data-ttu-id="db502-206">1 группа отработки отказа: DNS-сервер AD.</span><span class="sxs-lookup"><span data-stu-id="db502-206">Failover Group1: AD DNS</span></span>
2. <span data-ttu-id="db502-207">2 группа отработки отказа: виртуальные машины SQL Server.</span><span class="sxs-lookup"><span data-stu-id="db502-207">Failover Group2: SQL Server VMs</span></span>
3. <span data-ttu-id="db502-208">3 группа отработки отказа: виртуальная машина с образом VDA Master.</span><span class="sxs-lookup"><span data-stu-id="db502-208">Failover Group3: VDA Master Image VM</span></span>

   >[!NOTE]     
   ><span data-ttu-id="db502-209">Шаги 4, 6 и 7, содержащий действия вручную или сценария, применимые tooonly XenApp локальной > среде с несколькими Подключениями и просмотры Страниц каталогами.</span><span class="sxs-lookup"><span data-stu-id="db502-209">Steps 4, 6 and 7 containing manual or script actions are applicable tooonly an on-premises XenApp >environment with MCS/PVS catalogs.</span></span>

4. <span data-ttu-id="db502-210">Действие вручную или скрипт группа 3: hello master VDA ВМ завершение работы ВМ VDA Master при переключении tooAzure будет находиться в состоянии выполнения.</span><span class="sxs-lookup"><span data-stu-id="db502-210">Group 3 Manual or script action: Shutdown master VDA VM hello Master VDA VM when failed over tooAzure will be in a running state.</span></span> <span data-ttu-id="db502-211">toocreate с помощью размещения Azure ARM новые каталоги MCS, образец hello VDA ВМ — необходимые toobe остановлена (de выделенной) состояние.</span><span class="sxs-lookup"><span data-stu-id="db502-211">toocreate new MCS catalogs using Azure ARM hosting, hello master VDA VM is required toobe in Stopped (de allocated) state.</span></span> <span data-ttu-id="db502-212">Здравствуйте, завершение работы виртуальной Машины с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="db502-212">Shutdown hello VM from Azure Portal.</span></span>

5. <span data-ttu-id="db502-213">4 группа отработки отказа: контроллер доставки и виртуальные машины сервера StoreFront.</span><span class="sxs-lookup"><span data-stu-id="db502-213">Failover Group4: Delivery Controller and StoreFront server VMs</span></span>
6. <span data-ttu-id="db502-214">Группа 3. Действие вручную или действие скрипта. Вариант 1:</span><span class="sxs-lookup"><span data-stu-id="db502-214">Group3 manual or script action 1:</span></span>

    <span data-ttu-id="db502-215">***Добавление подключения к узлу Azure RM***</span><span class="sxs-lookup"><span data-stu-id="db502-215">***Add Azure RM host connection***</span></span>

    <span data-ttu-id="db502-216">Создайте подключение к узлу Azure ARM tooprovision машины контроллера доставки новых MCS каталогов в Azure.</span><span class="sxs-lookup"><span data-stu-id="db502-216">Create Azure ARM host connection in Delivery Controller machine tooprovision new MCS catalogs in Azure.</span></span> <span data-ttu-id="db502-217">Выполните шаги hello, как описано в этом [статьи](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span><span class="sxs-lookup"><span data-stu-id="db502-217">Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/07/21/connecting-to-azure-resource-manager-in-xenapp-xendesktop/).</span></span>

7. <span data-ttu-id="db502-218">Группа 3. Действие вручную или действие скрипта. Вариант 2:</span><span class="sxs-lookup"><span data-stu-id="db502-218">Group3 manual or script action 2:</span></span>

    <span data-ttu-id="db502-219">***Повторное создание каталогов MCS в Azure***</span><span class="sxs-lookup"><span data-stu-id="db502-219">***Re-create MCS Catalogs in Azure***</span></span>

    <span data-ttu-id="db502-220">существующие клоны MCS или просмотры Страниц на первичном сайте hello Hello не будет реплицированных tooAzure.</span><span class="sxs-lookup"><span data-stu-id="db502-220">hello existing MCS or PVS clones on hello primary site will not be replicated tooAzure.</span></span> <span data-ttu-id="db502-221">Необходимо toorecreate клонированного с помощью hello реплицированные master VDA и Azure ARM подготовки из контроллера доставки. Выполните шаги hello, как описано в этом [статьи](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS каталоги в Azure.</span><span class="sxs-lookup"><span data-stu-id="db502-221">You need toorecreate these clones using hello replicated master VDA and Azure ARM provisioning from Delivery controller.Follow hello steps as explained in this [article](https://www.citrix.com/blogs/2016/09/12/using-xenapp-xendesktop-in-azure-resource-manager/) toocreate MCS catalogs in Azure.</span></span>

![План восстановления для компонентов XenApp](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-recoveryplan.png)


   >[!NOTE]
   ><span data-ttu-id="db502-223">Можно использовать скрипты в [расположение](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS с помощью нового IP-адресов hello отработку отказа hello > виртуальных машин или tooattach при необходимости подсистему балансировки нагрузки на hello отработку отказа виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="db502-223">You can use scripts at [location](https://github.com/Azure/azure-quickstart-templates/blob/>master/asr-automation-recovery/scripts) tooupdate hello DNS with hello new IPs of hello failed over >virtual machines or tooattach a load balancer on hello failed over virtual machine, if needed.</span></span>


## <a name="doing-a-test-failover"></a><span data-ttu-id="db502-224">Тестовая отработка отказа</span><span class="sxs-lookup"><span data-stu-id="db502-224">Doing a test failover</span></span>

<span data-ttu-id="db502-225">Выполните [в этом руководстве](site-recovery-test-failover-to-azure.md) toodo тестовой отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="db502-225">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

![План восстановления](./media/site-recovery-citrix-xenapp-and-xendesktop/citrix-tfo.png)


## <a name="doing-a-failover"></a><span data-ttu-id="db502-227">Отработка отказа</span><span class="sxs-lookup"><span data-stu-id="db502-227">Doing a failover</span></span>

<span data-ttu-id="db502-228">При выполнении отработки отказа используйте [это руководство](site-recovery-failover.md).</span><span class="sxs-lookup"><span data-stu-id="db502-228">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db502-229">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="db502-229">Next steps</span></span>

<span data-ttu-id="db502-230">Дополнительные сведения о репликации развертываний Citrix XenApp и XenDesktop см. в [этом техническом документе](https://aka.ms/citrix-xenapp-xendesktop-with-asr).</span><span class="sxs-lookup"><span data-stu-id="db502-230">You can [learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about replicating Citrix XenApp and XenDesktop deployments  in this white paper.</span></span> <span data-ttu-id="db502-231">Просмотрите рекомендации hello слишком[репликацию других приложений](site-recovery-workload.md) с помощью Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="db502-231">Look at hello guidance too[replicate other applications](site-recovery-workload.md) using Site Recovery.</span></span>
