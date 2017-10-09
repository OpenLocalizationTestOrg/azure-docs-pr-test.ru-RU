---
title: "Работа по сети для репликации VMware tooAzure aaaPlan | Документы Microsoft"
description: "В этой статье описывается планирование требуется при репликации виртуальных машин VMware tooAzure сети"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5578a0b4-0352-41c3-9cce-56beb17a4d97
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 2b4f385c768cc7f5e98abae0afb8258b00f3724f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-plan-networking-for-vmware-tooazure-replication"></a><span data-ttu-id="22468-103">Шаг 4: Планирование сети для репликации tooAzure VMware</span><span class="sxs-lookup"><span data-stu-id="22468-103">Step 4: Plan networking for VMware tooAzure replication</span></span>

<span data-ttu-id="22468-104">Это статье кратко рассматриваются вопросы планирования при репликации локальных виртуальных машин VMware tooAzure с помощью hello сети [Azure Site Recovery](site-recovery-overview.md) службы.</span><span class="sxs-lookup"><span data-stu-id="22468-104">This article summarizes network planning considerations when replicating on-premises VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="22468-105">Отправлять все комментарии hello нижней части этой статьи, или задать вопросы в hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="22468-105">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="connect-tooreplica-vms"></a><span data-ttu-id="22468-106">Подключить виртуальные машины tooreplica</span><span class="sxs-lookup"><span data-stu-id="22468-106">Connect tooreplica VMs</span></span>

<span data-ttu-id="22468-107">При планировании репликации и стратегия отработки отказа, является одним из ключевых вопроса hello как toohello tooconnect виртуальной Машины Azure после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="22468-107">When planning your replication and failover strategy, one of hello key questions is how tooconnect toohello Azure VM after failover.</span></span> <span data-ttu-id="22468-108">При разработке сетевой стратегии для виртуальных машин реплик Azure существует несколько вариантов:</span><span class="sxs-lookup"><span data-stu-id="22468-108">There are a couple of choices when designing your network strategy for replica Azure VMs:</span></span>

- <span data-ttu-id="22468-109">**Использовать другой IP-адрес**: можно выбрать toouse диапазоном IP-адресов для сети виртуальной Машины Azure реплицированных hello.</span><span class="sxs-lookup"><span data-stu-id="22468-109">**Use different IP address**: You can select toouse a different IP address range for hello replicated Azure VM network.</span></span> <span data-ttu-id="22468-110">В этот сценарий hello виртуальная машина получит новый IP-адрес после отработки отказа и требуется обновление DNS.</span><span class="sxs-lookup"><span data-stu-id="22468-110">In this scenario hello VM gets a new IP address after failover, and a DNS update is required.</span></span>
- <span data-ttu-id="22468-111">**Сохраняет же IP-адрес**: может потребоваться toouse hello же диапазон IP-адресов, что основного локального узла, для hello сети Azure после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="22468-111">**Retain same IP address**: You might want toouse hello same IP address range as that in your primary on-premises site, for hello Azure network after failover.</span></span> <span data-ttu-id="22468-112">Сохранение hello одинаковые IP-адреса упрощает hello восстановления за счет уменьшения проблемы, связанные с сети после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="22468-112">Keeping hello same IP addresses simplifies hello recovery by reducing network related issues after failover.</span></span> <span data-ttu-id="22468-113">Тем не менее при выполнении репликации tooAzure, необходимо будет tooupdate маршруты с нового расположения hello hello IP-адресов после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="22468-113">However, when you're replicating tooAzure, you will need tooupdate routes with hello new location of hello IP addresses after failover.</span></span> 


## <a name="retain-ip-addresses"></a><span data-ttu-id="22468-114">Использование тех же IP-адресов</span><span class="sxs-lookup"><span data-stu-id="22468-114">Retain IP addresses</span></span>

<span data-ttu-id="22468-115">Site Recovery предоставляет hello возможность tooretain фиксированных IP-адресов при отработке отказа tooAzure с отработки отказа в подсети.</span><span class="sxs-lookup"><span data-stu-id="22468-115">Site Recovery provides hello capability tooretain fixed IP addresses when failing over tooAzure, with a subnet failover.</span></span>

<span data-ttu-id="22468-116">При отработке отказа в подсети отдельно взятая подсеть присутствует на сайте 1 или 2, но никогда на обоих сайтах одновременно.</span><span class="sxs-lookup"><span data-stu-id="22468-116">With subnet failover, a specific subnet is present at Site 1 or Site 2, but never at both sites simultaneously.</span></span> <span data-ttu-id="22468-117">В порядке toomaintain hello пространство IP-адресов в событии hello перехода на другой ресурс программным образом упорядочить для hello маршрутизатора инфраструктуры toomove из одного узла tooanother hello подсетей.</span><span class="sxs-lookup"><span data-stu-id="22468-117">In order toomaintain hello IP address space in hello event of a failover, you programmatically arrange for hello router infrastructure toomove hello subnets from one site tooanother.</span></span> <span data-ttu-id="22468-118">Во время отработки отказа hello подсетей для перемещения hello связанные защищенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="22468-118">During failover, hello subnets move with hello associated protected VMs.</span></span> <span data-ttu-id="22468-119">Основным недостатком Hello: в случае сбоя hello иметь toomove hello всей подсети.</span><span class="sxs-lookup"><span data-stu-id="22468-119">hello main drawback is that in hello event of a failure, you have toomove hello whole subnet.</span></span>


### <a name="failover-example"></a><span data-ttu-id="22468-120">Пример отработки отказа</span><span class="sxs-lookup"><span data-stu-id="22468-120">Failover example</span></span>

<span data-ttu-id="22468-121">Давайте рассмотрим пример tooAzure перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="22468-121">Let's look at an example for failover tooAzure.</span></span>

- <span data-ttu-id="22468-122">Вымышленная компания, банк Woodgrove, имеет локальную инфраструктуру, в которой размещены ее бизнес-приложения.</span><span class="sxs-lookup"><span data-stu-id="22468-122">A ficticious company, Woodgrove Bank, has an on-premises infrastructure hosting their business apps.</span></span> <span data-ttu-id="22468-123">Ее мобильные приложения размещены в Azure.</span><span class="sxs-lookup"><span data-stu-id="22468-123">Their mobile applications are hosted on Azure.</span></span>
- <span data-ttu-id="22468-124">Связь между виртуальными машинами банка Woodgrove в Azure и локальных серверов обеспечивается соединение сеть сеть (VPN) между hello локальной сети edge и hello виртуальной сети Azure.</span><span class="sxs-lookup"><span data-stu-id="22468-124">Connectivity between Woodgrove Bank VMs in Azure and on-premises servers is provided by a site-to-site (VPN) connection between hello on-premises edge network and hello Azure virtual network.</span></span>
- <span data-ttu-id="22468-125">Это VPN означает, что hello компании виртуальной сети в Azure в виде расширения их в локальной сети.</span><span class="sxs-lookup"><span data-stu-id="22468-125">This VPN means that hello company's virtual network in Azure appears as an extension of their on-premises network.</span></span>
- <span data-ttu-id="22468-126">Woodgrove хочет toouse Site Recovery tooreplicate локальных рабочих нагрузок tooAzure.</span><span class="sxs-lookup"><span data-stu-id="22468-126">Woodgrove wants toouse Site Recovery tooreplicate on-premises workloads tooAzure.</span></span>
 - <span data-ttu-id="22468-127">Woodgrove имеет toodeal с приложениями и конфигурации, которые зависят от жестко IP-адресов и поэтому tooretain IP-адреса для своих приложений после отработки отказа tooAzure.</span><span class="sxs-lookup"><span data-stu-id="22468-127">Woodgrove has toodeal with applications and configurations which depend on hard-coded IP addresses, and thus need tooretain IP addresses for their applications after failover tooAzure.</span></span>
 - <span data-ttu-id="22468-128">Woodgrove назначил IP-адреса из диапазона 172.16.1.0/24, 172.16.2.0/24 tooits ресурсов в Azure.</span><span class="sxs-lookup"><span data-stu-id="22468-128">Woodgrove has assigned IP addresses from range 172.16.1.0/24, 172.16.2.0/24 tooits resources running in Azure.</span></span>


<span data-ttu-id="22468-129">Для банка Woodgrove toobe может tooreplicate tooAzure его виртуальные МАШИНЫ во время сохранения hello IP-адресов Вот какие hello компании toodo:</span><span class="sxs-lookup"><span data-stu-id="22468-129">For Woodgrove toobe able tooreplicate its VMS tooAzure while retaining hello IP addresses, here's what hello company needs toodo:</span></span>

1. <span data-ttu-id="22468-130">Создайте виртуальную сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="22468-130">Create an Azure virtual network.</span></span> <span data-ttu-id="22468-131">Расширение hello в локальной сети, необходимо, чтобы приложения могут выполнять отработку отказа без проблем.</span><span class="sxs-lookup"><span data-stu-id="22468-131">It should be an extension of hello on-premises network, so that applications can fail over seamlessly.</span></span>
2. <span data-ttu-id="22468-132">Azure позволяет вам tooadd сеть сеть VPN-подключение, кроме toopoint сеть toohello виртуальных сетей, созданные в Azure.</span><span class="sxs-lookup"><span data-stu-id="22468-132">Azure allows you tooadd site-to-site VPN connectivity, in addition toopoint-to-site connectivity toohello virtual networks created in Azure.</span></span>
3. <span data-ttu-id="22468-133">При настройке подключения hello сайт сайт, в hello Azure сети, может осуществлять маршрутизацию трафика toohello локально (локальная сеть) только в том случае, если диапазон IP-адресов hello отличается от диапазона IP-адресов hello в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="22468-133">When setting up hello site-to-site connection, in hello Azure network, you can route traffic toohello on-premises location (local-network) only if hello IP address range is different from hello on-premises IP address range.</span></span>
    - <span data-ttu-id="22468-134">Это связано с тем, что Azure не поддерживает растянутые подсети.</span><span class="sxs-lookup"><span data-stu-id="22468-134">This is because Azure doesn’t support stretched subnets.</span></span> <span data-ttu-id="22468-135">Поэтому при наличии подсети 192.168.1.0/24 локальной 192.168.1.0/24 локальной сети нельзя добавить в hello сети Azure.</span><span class="sxs-lookup"><span data-stu-id="22468-135">So if you have subnet 192.168.1.0/24 on-premises, you can’t add a local-network 192.168.1.0/24 in hello Azure network.</span></span>
    - <span data-ttu-id="22468-136">Ожидается, так как Azure не знает, что отсутствуют активные ВМ в подсети hello и подсети hello создается только для аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="22468-136">This is expected because Azure doesn’t know that there are no active VMs in hello subnet, and that hello subnet is being created for disaster recovery only.</span></span>
    - <span data-ttu-id="22468-137">toobe может toocorrectly маршрутизацию сетевого трафика за пределами Azure hello подсетей в сети hello и hello локальной сети должен конфликтуют.</span><span class="sxs-lookup"><span data-stu-id="22468-137">toobe able toocorrectly route network traffic out of an Azure network hello subnets in hello network and hello local-network mustn't conflict.</span></span>

![Перед выполнением отработки отказа подсети](./media/site-recovery-network-design/network-design7.png)

### <a name="before-failover"></a><span data-ttu-id="22468-139">Перед выполнением отработки отказа</span><span class="sxs-lookup"><span data-stu-id="22468-139">Before failover</span></span>

1. <span data-ttu-id="22468-140">Создайте дополнительную сеть (например, сеть восстановления).</span><span class="sxs-lookup"><span data-stu-id="22468-140">Create an additional network (for example Recovery Network).</span></span> <span data-ttu-id="22468-141">Это сеть hello в которой отработку отказа виртуальных машин были созданы.</span><span class="sxs-lookup"><span data-stu-id="22468-141">This is hello network in which failed over VMs are created.</span></span>
2. <span data-ttu-id="22468-142">tooensure, hello IP-адрес для виртуальной Машины сохраняется после отработки отказа, в свойствах виртуальной Машины hello > **Настройка**, укажите hello же IP-адресов, hello виртуальной Машины используется локальная и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="22468-142">tooensure that hello IP address for a VM is retained after a failover, in hello VM properties > **Configure**, specify hello same IP address that hello VM has on-premises, and click **Save**.</span></span>
3. <span data-ttu-id="22468-143">При переключении hello ВМ Azure Site Recovery будет назначать hello, предоставляемые tooit IP адрес.</span><span class="sxs-lookup"><span data-stu-id="22468-143">When hello VM is failed over, Azure Site Recovery will assign hello provided IP address tooit.</span></span>

    ![Свойства сети](./media/site-recovery-network-design/network-design8.png)

4. <span data-ttu-id="22468-145">После отработки отказа триггер срабатывает и hello виртуальные машины создаются в Azure с hello требуется IP-адрес, можно подключиться при помощи сети toohello [tooVnet подключения виртуальной сети](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="22468-145">After failover is trigger is triggered, and hello VMs are created in Azure with hello required IP address, you can connect toohello network using a [Vnet tooVnet connection](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span> <span data-ttu-id="22468-146">Это действие можно выполнить с помощью сценария.</span><span class="sxs-lookup"><span data-stu-id="22468-146">This action can be scripted.</span></span>
5. <span data-ttu-id="22468-147">Маршруты необходимо соответствующим образом изменены, toobe tooreflect tooAzure теперь перемещен, 192.168.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="22468-147">Routes need toobe appropriately modified, tooreflect that 192.168.1.0/24 has now moved tooAzure.</span></span>

    ![После выполнения отработки отказа подсети](./media/site-recovery-network-design/network-design9.png)

### <a name="after-failover"></a><span data-ttu-id="22468-149">После выполнения отработки отказа</span><span class="sxs-lookup"><span data-stu-id="22468-149">After failover</span></span>

<span data-ttu-id="22468-150">Если у вас нет сети Azure, как показано на рисунке выше, то после отработки отказа можно создать VPN-подключение типа "сайт — сайт" между основным сайтом и сетью Azure.</span><span class="sxs-lookup"><span data-stu-id="22468-150">If you don't have an Azure network as illustrated above, you can create a site-to-site VPN connection between your primary site and Azure, after failover.</span></span>

## <a name="change-ip-addresses"></a><span data-ttu-id="22468-151">Изменение IP-адресов</span><span class="sxs-lookup"><span data-stu-id="22468-151">Change IP addresses</span></span>

<span data-ttu-id="22468-152">Это [блога](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) объясняет, как tooset копирование hello Azure сетевой инфраструктуры, когда нет необходимости использовать tooretain IP адресов после перехода на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="22468-152">This [blog post](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) explains how tooset up hello Azure networking infrastructure when you don't need tooretain IP addresses after failover.</span></span> <span data-ttu-id="22468-153">Он начинается с описание приложения, осуществляет как tooset сеть в локальной, так и в Azure и заканчиваются сведения о выполнении переход на другой ресурс.</span><span class="sxs-lookup"><span data-stu-id="22468-153">It starts with an application description, looks at how tooset up networking on-premises and in Azure, and concludes with information about running failovers.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="22468-154">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22468-154">Next steps</span></span>

<span data-ttu-id="22468-155">Go слишком[шаг 5: Подготовка Azure](vmware-walkthrough-prepare-azure.md)</span><span class="sxs-lookup"><span data-stu-id="22468-155">Go too[Step 5: Prepare Azure](vmware-walkthrough-prepare-azure.md)</span></span>
