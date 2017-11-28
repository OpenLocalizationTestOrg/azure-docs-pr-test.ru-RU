---
title: "виртуальные машины aaaReplicate Hyper-V в облаках VMM с помощью Azure Site Recovery и PowerShell (диспетчера ресурсов) | Документы Microsoft"
description: "Репликация виртуальных машин Hyper-V в облаках VMM с помощью Azure Site Recovery и PowerShell"
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: raynew
ms.assetid: 6ac509ad-5024-43d8-b621-d8fec019b9a9
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: rajanaki
ms.openlocfilehash: b0f641de4e10a600ead415ceb9bd488fb4d1659d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-powershell-and-azure-resource-manager"></a><span data-ttu-id="e499b-103">Реплицировать виртуальные машины Hyper-V в tooAzure облака VMM, с помощью PowerShell и диспетчера ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="e499b-103">Replicate Hyper-V virtual machines in VMM clouds tooAzure using PowerShell and Azure Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e499b-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="e499b-104">Azure Portal</span></span>](site-recovery-vmm-to-azure.md)
> * [<span data-ttu-id="e499b-105">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e499b-105">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [<span data-ttu-id="e499b-106">Классический портал</span><span class="sxs-lookup"><span data-stu-id="e499b-106">Classic Portal</span></span>](site-recovery-vmm-to-azure-classic.md)
> * [<span data-ttu-id="e499b-107">PowerShell — классическая модель</span><span class="sxs-lookup"><span data-stu-id="e499b-107">PowerShell - Classic</span></span>](site-recovery-deploy-with-powershell.md)
>
>

## <a name="overview"></a><span data-ttu-id="e499b-108">Обзор</span><span class="sxs-lookup"><span data-stu-id="e499b-108">Overview</span></span>
<span data-ttu-id="e499b-109">Azure Site Recovery поддерживает tooyour бизнес-непрерывности и аварийного восстановления (BCDR) стратегии, управляя операциями репликации, отработки отказа и восстановления виртуальных машин в различных вариантов развертывания.</span><span class="sxs-lookup"><span data-stu-id="e499b-109">Azure Site Recovery contributes tooyour business continuity and disaster recovery (BCDR) strategy by orchestrating replication, failover and recovery of virtual machines in a number of deployment scenarios.</span></span> <span data-ttu-id="e499b-110">Полный список развертывания сценариев. в разделе hello [Обзор Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e499b-110">For a full list of deployment scenarios see hello [Azure Site Recovery overview](site-recovery-overview.md).</span></span>

<span data-ttu-id="e499b-111">В этой статье показано, как toouse PowerShell tooautomate общие задачи должны tooperform при настройке виртуальных машин Hyper-V Azure Site Recovery tooreplicate в хранилище tooAzure облаков System Center VMM.</span><span class="sxs-lookup"><span data-stu-id="e499b-111">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooAzure storage.</span></span>

<span data-ttu-id="e499b-112">включает описание необходимых условий для сценария hello Hello статьи, а также демонстрируется</span><span class="sxs-lookup"><span data-stu-id="e499b-112">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="e499b-113">Как tooset копирование хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="e499b-113">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="e499b-114">Установка поставщика Azure Site Recovery hello на исходном сервере VMM hello</span><span class="sxs-lookup"><span data-stu-id="e499b-114">Install hello Azure Site Recovery Provider on hello source VMM server</span></span>
* <span data-ttu-id="e499b-115">Зарегистрируйте сервер hello в хранилище hello, добавьте учетную запись хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="e499b-115">Register hello server in hello vault, add an Azure storage account</span></span>
* <span data-ttu-id="e499b-116">Установка агента служб восстановления Azure hello на серверах узлов Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e499b-116">Install hello Azure Recovery Services agent on Hyper-V host servers</span></span>
* <span data-ttu-id="e499b-117">Настройте параметры защиты для облака VMM, которые будут применяться tooall защищенные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="e499b-117">Configure protection settings for VMM clouds, that will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="e499b-118">Включение защиты для таких виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e499b-118">Enable protection for those virtual machines.</span></span>
* <span data-ttu-id="e499b-119">Протестируйте toomake сбое hello убедиться, что все работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="e499b-119">Test hello fail-over toomake sure everything's working as expected.</span></span>

<span data-ttu-id="e499b-120">Если возникли проблемы с установкой этого сценария опубликовать вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="e499b-120">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="e499b-121">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e499b-121">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e499b-122">В этой статье описан с помощью модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-122">This article covers using hello Resource Manager deployment model.</span></span>
>
>

## <a name="before-you-start"></a><span data-ttu-id="e499b-123">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="e499b-123">Before you start</span></span>
<span data-ttu-id="e499b-124">Убедитесь, что выполнены следующие предварительные требования.</span><span class="sxs-lookup"><span data-stu-id="e499b-124">Make sure you have these prerequisites in place:</span></span>

### <a name="azure-prerequisites"></a><span data-ttu-id="e499b-125">Предварительные требования Azure</span><span class="sxs-lookup"><span data-stu-id="e499b-125">Azure prerequisites</span></span>
* <span data-ttu-id="e499b-126">Вам потребуется учетная запись [Microsoft Azure](https://azure.microsoft.com/) .</span><span class="sxs-lookup"><span data-stu-id="e499b-126">You'll need a [Microsoft Azure](https://azure.microsoft.com/) account.</span></span> <span data-ttu-id="e499b-127">Если у вас ее нет, воспользуйтесь [бесплатной учетной записью](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="e499b-127">If you don't have one, start with a [free account](https://azure.microsoft.com/free).</span></span> <span data-ttu-id="e499b-128">Кроме того, вы можете прочесть об hello [ценообразования Azure Site Recovery Manager](https://azure.microsoft.com/pricing/details/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="e499b-128">In addition, you can read about hello [Azure Site Recovery Manager pricing](https://azure.microsoft.com/pricing/details/site-recovery/).</span></span>
* <span data-ttu-id="e499b-129">Вам потребуется подписка CSP при out сценарий hello репликации tooa CSP подписки.</span><span class="sxs-lookup"><span data-stu-id="e499b-129">You'll need a CSP subscription if you are trying out hello replication tooa CSP subscription scenario.</span></span> <span data-ttu-id="e499b-130">Дополнительные сведения о программе CSP hello в [как tooenroll в программе CSP hello](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span><span class="sxs-lookup"><span data-stu-id="e499b-130">Learn more about hello CSP program in [how tooenroll in hello CSP program](https://msdn.microsoft.com/library/partnercenter/mt156995.aspx).</span></span>
* <span data-ttu-id="e499b-131">Вам потребуется реплицируемые данные tooAzure toostore учетная запись Azure v2 хранилища (диспетчера ресурсов).</span><span class="sxs-lookup"><span data-stu-id="e499b-131">You'll need an Azure v2 storage (Resource Manager) account toostore data replicated tooAzure.</span></span> <span data-ttu-id="e499b-132">Hello учетная запись должна включена георепликация.</span><span class="sxs-lookup"><span data-stu-id="e499b-132">hello account needs geo-replication enabled.</span></span> <span data-ttu-id="e499b-133">Он должен быть в hello же регионе, что hello службы Azure Site Recovery и быть связан с hello одной подписки или подписки CSP hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-133">It should be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription or hello CSP subscription.</span></span> <span data-ttu-id="e499b-134">toolearn Дополнительные сведения о настройке хранилища Azure в разделе hello [tooMicrosoft введение хранилища Azure](../storage/common/storage-introduction.md) для ссылки.</span><span class="sxs-lookup"><span data-stu-id="e499b-134">toolearn more about setting up Azure storage, see hello [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md) for reference.</span></span>
* <span data-ttu-id="e499b-135">Необходимо убедиться, что виртуальные машины, которые вы хотите tooprotect соответствовать hello toomake [предварительные требования виртуальной машины Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="e499b-135">You'll need toomake sure that virtual machines you want tooprotect comply with hello [Azure virtual machine prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>

> [!NOTE]
> <span data-ttu-id="e499b-136">В настоящее через Powershell доступны только операции уровня виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="e499b-136">Currently, only VM level operations are possible through Powershell.</span></span> <span data-ttu-id="e499b-137">Скоро будет включена поддержка операций на уровне плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="e499b-137">Support for recovery plan level operations will be made soon.</span></span>  <span data-ttu-id="e499b-138">Теперь не ограниченной tooperforming отказов только по «защищенных виртуальных Машин», а не на уровне плана восстановления.</span><span class="sxs-lookup"><span data-stu-id="e499b-138">For now, you are limited tooperforming fail-overs only at a ‘protected VM’ granularity and not at a Recovery Plan level.</span></span>
>
>

### <a name="vmm-prerequisites"></a><span data-ttu-id="e499b-139">Предварительные требования VMM</span><span class="sxs-lookup"><span data-stu-id="e499b-139">VMM prerequisites</span></span>
* <span data-ttu-id="e499b-140">Вам потребуется сервер VMM под управлением System Center 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e499b-140">You'll need VMM server running on System Center 2012 R2.</span></span>
* <span data-ttu-id="e499b-141">На любом сервере VMM, содержащем виртуальные машины, необходимо вернуть tooprotect должен работать под управлением hello поставщика Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e499b-141">Any VMM server containing virtual machines you want tooprotect must be running hello Azure Site Recovery Provider.</span></span> <span data-ttu-id="e499b-142">При установке hello развертывания Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e499b-142">This is installed during hello Azure Site Recovery deployment.</span></span>
* <span data-ttu-id="e499b-143">Необходимо по крайней мере одно облако на сервер VMM требуется tooprotect hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-143">You'll need at least one cloud on hello VMM server you want tooprotect.</span></span> <span data-ttu-id="e499b-144">облако Hello должен содержать:</span><span class="sxs-lookup"><span data-stu-id="e499b-144">hello cloud should contain:</span></span>
  * <span data-ttu-id="e499b-145">одну или несколько групп узлов VMM;</span><span class="sxs-lookup"><span data-stu-id="e499b-145">One or more VMM host groups.</span></span>
  * <span data-ttu-id="e499b-146">Один или несколько серверов или кластеров узлов Hyper-V в каждой группе узлов.</span><span class="sxs-lookup"><span data-stu-id="e499b-146">One or more Hyper-V host servers or clusters in each host group.</span></span>
  * <span data-ttu-id="e499b-147">Один или несколько виртуальных машин на сервере Hyper-V источника hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-147">One or more virtual machines on hello source Hyper-V server.</span></span>
* <span data-ttu-id="e499b-148">Дополнительные сведения о настройке облаков VMM</span><span class="sxs-lookup"><span data-stu-id="e499b-148">Learn more about setting up VMM clouds:</span></span>
  * <span data-ttu-id="e499b-149">Дополнительные сведения о частных облаках VMM в [новые возможности частного облака с System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) и [облака VMM 2012 и hello](http://go.microsoft.com/fwlink/?LinkId=324956).</span><span class="sxs-lookup"><span data-stu-id="e499b-149">Read more about private VMM clouds in [What’s New in Private Cloud with System Center 2012 R2 VMM](http://go.microsoft.com/fwlink/?LinkId=324952) and in [VMM 2012 and hello clouds](http://go.microsoft.com/fwlink/?LinkId=324956).</span></span>
  * <span data-ttu-id="e499b-150">Дополнительные сведения о [hello Настройка VMM облако структуры](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span><span class="sxs-lookup"><span data-stu-id="e499b-150">Learn about [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric)</span></span>
  * <span data-ttu-id="e499b-151">После того как все элементы структуры облака будут готовы, ознакомьтесь с дополнительными сведениями о создании частных облаков в разделах [Создание частного облака в VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) и [Пошаговое руководство: создание частных облаков с VMM System Center 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span><span class="sxs-lookup"><span data-stu-id="e499b-151">After your cloud fabric elements are in place learn about creating private clouds in [Creating a private cloud in VMM](http://go.microsoft.com/fwlink/p/?LinkId=324953) and in [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://go.microsoft.com/fwlink/p/?LinkId=324954).</span></span>

### <a name="hyper-v-prerequisites"></a><span data-ttu-id="e499b-152">Предварительные требования Hyper-V</span><span class="sxs-lookup"><span data-stu-id="e499b-152">Hyper-V prerequisites</span></span>
* <span data-ttu-id="e499b-153">Hello серверы узла Hyper-V должны работать под управлением **Windows Server 2012** с ролью Hyper-V или **Microsoft Hyper-V Server 2012** и иметь hello установлены последние обновления.</span><span class="sxs-lookup"><span data-stu-id="e499b-153">hello host Hyper-V servers must be running at least **Windows Server 2012** with Hyper-V role or **Microsoft Hyper-V Server 2012** and have hello latest updates installed.</span></span>
* <span data-ttu-id="e499b-154">Если Hyper-V выполняется в кластере, учтите, что брокер кластера не создается автоматически при использовании кластера на основе статических IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="e499b-154">If you're running Hyper-V in a cluster note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="e499b-155">Брокер кластера hello tooconfigure вам потребуется вручную.</span><span class="sxs-lookup"><span data-stu-id="e499b-155">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="e499b-156">Для</span><span class="sxs-lookup"><span data-stu-id="e499b-156">For</span></span>
* <span data-ttu-id="e499b-157">Инструкции см. в разделе [как tooConfigure брокера реплики Hyper-V](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span><span class="sxs-lookup"><span data-stu-id="e499b-157">For instructions see [How tooConfigure Hyper-V Replica Broker](http://blogs.technet.com/b/haroldwong/archive/2013/03/27/server-virtualization-series-hyper-v-replica-broker-explained-part-15-of-20-by-yung-chou.aspx).</span></span>
* <span data-ttu-id="e499b-158">Любой сервер узла Hyper-V или кластера, для которого требуется защита toomanage должны включаться в облаке VMM.</span><span class="sxs-lookup"><span data-stu-id="e499b-158">Any Hyper-V host server or cluster for which you want toomanage protection must be included in a VMM cloud.</span></span>

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="e499b-159">Предварительные требования сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="e499b-159">Network mapping prerequisites</span></span>
<span data-ttu-id="e499b-160">При защите виртуальных машин в Azure, hello сопоставление сетей hello сетями виртуальных машин на исходном сервере VMM hello и целевой сети Azure tooenable hello следующее:</span><span class="sxs-lookup"><span data-stu-id="e499b-160">When you protect virtual machines in Azure, hello network mapping  maps hello virtual machine networks on hello source VMM server and target Azure networks tooenable hello following:</span></span>

* <span data-ttu-id="e499b-161">Все машины, которые отработки отказа на hello же может подключиться tooeach других, независимо от используемого плана восстановления, находящиеся в сеть.</span><span class="sxs-lookup"><span data-stu-id="e499b-161">All machines which fail over on hello same network can connect tooeach other, irrespective of which recovery plan they are in.</span></span>
* <span data-ttu-id="e499b-162">Если сетевой шлюз настроен hello целевой сети Azure, виртуальные машины могут подключаться tooother локальных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="e499b-162">If a network gateway is setup on hello target Azure network, virtual machines can connect tooother on-premises virtual machines.</span></span>
* <span data-ttu-id="e499b-163">Если не настроить сетевое сопоставление, только hello виртуальной машины, отработка отказа в hello же плана восстановления будут другие возможности tooconnect tooeach после tooAzure отработку отказа.</span><span class="sxs-lookup"><span data-stu-id="e499b-163">If you don’t configure network mapping, only hello virtual machines that fail over in hello same recovery plan will be able tooconnect tooeach other after fail-over tooAzure.</span></span>

<span data-ttu-id="e499b-164">Если требуется, чтобы toodeploy сетевого сопоставления необходимо иметь hello следующее:</span><span class="sxs-lookup"><span data-stu-id="e499b-164">If you want toodeploy network mapping you'll need hello following:</span></span>

* <span data-ttu-id="e499b-165">виртуальные машины Hello требуется tooprotect на исходном сервере VMM hello должно быть tooa подключенной сети виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e499b-165">hello virtual machines you want tooprotect on hello source VMM server should be connected tooa VM network.</span></span> <span data-ttu-id="e499b-166">Сеть должна быть связанной tooa логической сети, связанной с облаком hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-166">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
* <span data-ttu-id="e499b-167">Сеть Azure toowhich реплицировать виртуальные машины могут подключаться после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e499b-167">An Azure network toowhich replicated virtual machines can connect after fail-over.</span></span> <span data-ttu-id="e499b-168">Будет предложено выбрать этой сети во время отработки отказа hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-168">You'll select this network at hello time of fail-over.</span></span> <span data-ttu-id="e499b-169">сеть Hello должны находиться в hello же регионе, что подписки Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e499b-169">hello network should be in hello same region as your Azure Site Recovery subscription.</span></span>

<span data-ttu-id="e499b-170">Дополнительные сведения о сетевом сопоставлении см. в следующих статьях.</span><span class="sxs-lookup"><span data-stu-id="e499b-170">Learn more about network mapping in</span></span>

* [<span data-ttu-id="e499b-171">Как tooconfigure логических сетей в VMM</span><span class="sxs-lookup"><span data-stu-id="e499b-171">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="e499b-172">Как tooconfigure ВМ сетей и шлюзов в VMM</span><span class="sxs-lookup"><span data-stu-id="e499b-172">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)
* [<span data-ttu-id="e499b-173">Как tooconfigure и мониторинг виртуальных сетей в Azure</span><span class="sxs-lookup"><span data-stu-id="e499b-173">How tooconfigure and monitor virtual networks in Azure</span></span>](https://azure.microsoft.com/documentation/services/virtual-network/)

### <a name="powershell-prerequisites"></a><span data-ttu-id="e499b-174">Необходимые компоненты PowerShell</span><span class="sxs-lookup"><span data-stu-id="e499b-174">PowerShell prerequisites</span></span>
<span data-ttu-id="e499b-175">Убедитесь, что у вас есть toogo готовности Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e499b-175">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="e499b-176">Если вы уже используете PowerShell, вам потребуется tooupgrade tooversion 0.8.10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="e499b-176">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="e499b-177">Сведения о настройке PowerShell см. в разделе hello [проводят tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="e499b-177">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="e499b-178">После установки и настройки PowerShell вы можете просматривать все hello доступных командлетов для службы hello [здесь](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e499b-178">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="e499b-179">toolearn советы, помогающие использовать командлеты hello, например как значения параметров, входы и выходы обычно обрабатываются в Azure PowerShell, в разделе hello [руководство по работе с командлетами Azure tooget](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="e499b-179">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="e499b-180">Шаг 1: Задайте подписку hello</span><span class="sxs-lookup"><span data-stu-id="e499b-180">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="e499b-181">Из Azure powershell, tooyour входа учетной записи Azure: с помощью следующих командлетов hello</span><span class="sxs-lookup"><span data-stu-id="e499b-181">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="e499b-182">Получите список своих подписок.</span><span class="sxs-lookup"><span data-stu-id="e499b-182">Get a list of your subscriptions.</span></span> <span data-ttu-id="e499b-183">Выводит также список hello subscriptionIDs для каждой из подписок hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-183">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="e499b-184">Запишите subscriptionID hello hello подписки, в котором вы хотите хранилище служб восстановления toocreate hello</span><span class="sxs-lookup"><span data-stu-id="e499b-184">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>

        Get-AzureRmSubscription
3. <span data-ttu-id="e499b-185">Задать hello подписки, в какие hello хранилище служб восстановления является toobe созданные упомянуть hello идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="e499b-185">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="e499b-186">Шаг 2. Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="e499b-186">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="e499b-187">Если у вас еще нет группы ресурсов в Azure Resource Manager, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="e499b-187">Create a resource group  in Azure Resource Manager if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="e499b-188">Создайте новое хранилище служб восстановления и сохраните hello, созданном объекте хранилища ASR в переменной (будет использоваться позднее).</span><span class="sxs-lookup"><span data-stu-id="e499b-188">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="e499b-189">Вы также можете получить hello ASR хранилища объекта post создания с помощью командлета Get-AzureRMRecoveryServicesVault hello:-</span><span class="sxs-lookup"><span data-stu-id="e499b-189">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="e499b-190">Шаг 3: Установка контекста hello хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="e499b-190">Step 3: Set hello Recovery Services Vault context</span></span>

<span data-ttu-id="e499b-191">Задайте контекст хранилища hello, выполнив hello ниже команду.</span><span class="sxs-lookup"><span data-stu-id="e499b-191">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="e499b-192">Шаг 4: Установка поставщика Azure Site Recovery hello</span><span class="sxs-lookup"><span data-stu-id="e499b-192">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="e499b-193">На виртуальной машине VMM hello создайте каталог, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-193">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="e499b-194">Извлеките файлы hello, с помощью поставщика загружаются hello, выполнив следующую команду hello</span><span class="sxs-lookup"><span data-stu-id="e499b-194">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="e499b-195">Установите поставщик hello, с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e499b-195">Install hello provider using hello following commands:</span></span>

       .\SetupDr.exe /i
       $installationRegPath = "hklm:\software\Microsoft\Microsoft System Center Virtual Machine Manager Server\DRAdapter"
       do
       {
         $isNotInstalled = $true;
         if(Test-Path $installationRegPath)
         {
           $isNotInstalled = $false;
         }
       }While($isNotInstalled)

   <span data-ttu-id="e499b-196">Дождитесь установки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-196">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="e499b-197">Зарегистрируйте сервер hello в хранилище hello, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e499b-197">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-an-azure-storage-account"></a><span data-ttu-id="e499b-198">Шаг 5. Создание учетной записи хранения Azure</span><span class="sxs-lookup"><span data-stu-id="e499b-198">Step 5: Create an Azure storage account</span></span>

<span data-ttu-id="e499b-199">При отсутствии учетной записи хранилища Azure, создание учетной записи включена георепликация в hello в том же геообъекте hello хранилище, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-199">If you don't have an Azure storage account, create a geo-replication enabled account in hello same geo as hello vault by running hello following command:</span></span>

        $StorageAccountName = "teststorageacc1"    #StorageAccountname
        $StorageAccountGeo  = "Southeast Asia"     
        $ResourceGroupName =  “myRG”             #ResourceGroupName
        $RecoveryStorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Type “StandardGRS” -Location $StorageAccountGeo

<span data-ttu-id="e499b-200">Обратите внимание, что учетная запись хранения hello должна быть в hello же регионе, что служба восстановления сайтов Azure hello и связанные с hello одной подписке.</span><span class="sxs-lookup"><span data-stu-id="e499b-200">Note that hello storage account must be in hello same region as hello Azure Site Recovery service, and be associated with hello same subscription.</span></span>

## <a name="step-6-install-hello-azure-recovery-services-agent"></a><span data-ttu-id="e499b-201">Шаг 6: Установите агент служб восстановления Azure hello</span><span class="sxs-lookup"><span data-stu-id="e499b-201">Step 6: Install hello Azure Recovery Services Agent</span></span>
1. <span data-ttu-id="e499b-202">Скачать агент служб восстановления Azure hello в [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) и установить его на каждом сервере узла Hyper-V, расположенных в hello VMM облаков, вы хотите tooprotect.</span><span class="sxs-lookup"><span data-stu-id="e499b-202">Download hello Azure Recovery Services agent at [http://aka.ms/latestmarsagent](http://aka.ms/latestmarsagent) and install it on each Hyper-V host server located in hello VMM clouds you want tooprotect.</span></span>
2. <span data-ttu-id="e499b-203">Выполните следующую команду на всех узлах VMM hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-203">Run hello following command on all VMM hosts:</span></span>

       marsagentinstaller.exe /q /nu

## <a name="step-7-configure-cloud-protection-settings"></a><span data-ttu-id="e499b-204">Шаг 7. Настройка параметров защиты облачных систем</span><span class="sxs-lookup"><span data-stu-id="e499b-204">Step 7: Configure cloud protection settings</span></span>
1. <span data-ttu-id="e499b-205">Создайте политику репликации tooAzure, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-205">Create a replication policy tooAzure by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $Recoverypoints = 6                    #specify hello number of recovery points

        $policryresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider HyperVReplicaAzure -ReplicationFrequencyInSeconds $replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours 1 -RecoveryAzureStorageAccountId "/subscriptions/q1345667/resourceGroups/test/providers/Microsoft.Storage/storageAccounts/teststorageacc1"

1. <span data-ttu-id="e499b-206">Получите контейнер защиты, выполнив следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-206">Get a protection container by running hello following commands:</span></span>

       $PrimaryCloud = "testcloud"
       $protectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  
2. <span data-ttu-id="e499b-207">Получите сведения о tooa политики hello переменную, с помощью задания hello, который был создан и отметить hello политики понятное имя:</span><span class="sxs-lookup"><span data-stu-id="e499b-207">Get hello policy details tooa variable using hello job that was created and mentioning hello friendly policy name:</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="e499b-208">Запустите hello сопоставление контейнера защиты hello с политикой репликации hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-208">Start hello association of hello protection container with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $protectionContainer  
4. <span data-ttu-id="e499b-209">После завершения задания hello, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-209">After hello job has finished, run hello following command:</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }
5. <span data-ttu-id="e499b-210">После завершения обработки задания hello, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-210">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="e499b-211">toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).</span><span class="sxs-lookup"><span data-stu-id="e499b-211">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-8-configure-network-mapping"></a><span data-ttu-id="e499b-212">Шаг 8. Настройка сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="e499b-212">Step 8: Configure network mapping</span></span>
<span data-ttu-id="e499b-213">Перед началом сопоставления сетей убедитесь, что виртуальные машины на исходном сервере VMM hello tooa подключенной сети виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="e499b-213">Before you begin network mapping verify that virtual machines on hello source VMM server are connected tooa VM network.</span></span> <span data-ttu-id="e499b-214">Кроме того, создайте одну или несколько виртуальных сетей Azure.</span><span class="sxs-lookup"><span data-stu-id="e499b-214">In addition, create one or more Azure virtual networks.</span></span>

<span data-ttu-id="e499b-215">Дополнительные сведения о как toocreate в виртуальной сети с помощью диспетчера ресурсов Azure и PowerShell в [Создание виртуальной сети через VPN-подключения сеть сеть, с помощью диспетчера ресурсов Azure и PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e499b-215">Learn more about how toocreate a virtual network using Azure Resource Manager and PowerShell, in [Create a virtual network with a site-to-site VPN connection using Azure Resource Manager and PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)</span></span>

<span data-ttu-id="e499b-216">Обратите внимание, что несколько сетей виртуальной машины может быть сопоставленных tooa одной сетью Azure.</span><span class="sxs-lookup"><span data-stu-id="e499b-216">Note that multiple Virtual Machine networks can be mapped tooa single Azure network.</span></span> <span data-ttu-id="e499b-217">Если hello целевая сеть содержит несколько подсетей, и одна из этих подсетей имеет hello находится совпадает с именем подсети, на какие hello исходной виртуальной машины, а затем hello реплики виртуальной машины будет подключенных toothat целевой подсети после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="e499b-217">If hello target network has multiple subnets and one of those subnets has hello same name as subnet on which hello source virtual machine is located, then hello replica virtual machine will be connected toothat target subnet after fail-over.</span></span> <span data-ttu-id="e499b-218">Если никакой целевой подсети с совпадающим именем, hello виртуальная машина будет подключенных toohello первой подсети в сети hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-218">If there is no target subnet with a matching name, hello virtual machine will be connected toohello first subnet in hello network.</span></span>

1. <span data-ttu-id="e499b-219">Первая команда Hello возвращает серверов для hello текущее хранилище Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e499b-219">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="e499b-220">Hello команда сохраняет серверы Microsoft Azure Site Recovery hello в переменной hello $Servers массива.</span><span class="sxs-lookup"><span data-stu-id="e499b-220">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="e499b-221">Вторая команда Hello возвращает hello сети восстановления сайта для первого сервера hello в массиве hello $Servers.</span><span class="sxs-lookup"><span data-stu-id="e499b-221">hello second command gets hello site recovery network for hello first server in hello $Servers array.</span></span> <span data-ttu-id="e499b-222">Команда Hello сохраняет сетей hello в hello $Networks переменной.</span><span class="sxs-lookup"><span data-stu-id="e499b-222">hello command stores hello networks in hello $Networks variable.</span></span>

        $Networks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]

1. <span data-ttu-id="e499b-223">Третья команда Hello получает виртуальные сети Azure, а затем это значение в переменной hello $AzureVmNetworks.</span><span class="sxs-lookup"><span data-stu-id="e499b-223">hello third command gets Azure virtual networks, and then that value in hello $AzureVmNetworks variable.</span></span>

        $AzureVmNetworks =  Get-AzureRmVirtualNetwork
2. <span data-ttu-id="e499b-224">Hello окончательного создает сопоставление между первичной и сетями виртуальной машины Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-224">hello final cmdlet creates a mapping between hello primary network and hello Azure virtual machine network.</span></span> <span data-ttu-id="e499b-225">командлет Hello указывает hello основной сети как первый элемент $Networks hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-225">hello cmdlet specifies hello primary network as hello first element of $Networks.</span></span> <span data-ttu-id="e499b-226">командлет Hello указывает сеть виртуальной машины как первого элемента $AzureVmNetworks hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-226">hello cmdlet specifies a virtual machine network as hello first element of $AzureVmNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $Networks[0] -AzureVMNetworkId $AzureVmNetworks[0]

## <a name="step-9-enable-protection-for-virtual-machines"></a><span data-ttu-id="e499b-227">Шаг 9. Включение защиты для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="e499b-227">Step 9: Enable protection for virtual machines</span></span>
<span data-ttu-id="e499b-228">После надлежащей настройки серверов hello, облаков и сетей, можно включить защиту для виртуальных машин в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-228">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

 <span data-ttu-id="e499b-229">Обратите внимание hello следующие:</span><span class="sxs-lookup"><span data-stu-id="e499b-229">Note hello following:</span></span>

* <span data-ttu-id="e499b-230">Виртуальные машины должны соответствовать требованиям, предъявляемым Azure.</span><span class="sxs-lookup"><span data-stu-id="e499b-230">Virtual machines must meet Azure requirements.</span></span> <span data-ttu-id="e499b-231">Проверьте эти [предварительные условия и поддержка](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) в руководстве по планированию hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-231">Check these in [Prerequisites and Support](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) in hello planning guide.</span></span>
* <span data-ttu-id="e499b-232">tooenable защиты, hello операционной системы и свойства диска операционной системы необходимо задать для виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-232">tooenable protection, hello operating system and operating system disk properties must be set for hello virtual machine.</span></span> <span data-ttu-id="e499b-233">При создании виртуальной машины в VMM с помощью шаблона виртуальной машины можно задать свойство hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-233">When you create a virtual machine in VMM using a virtual machine template you can set hello property.</span></span> <span data-ttu-id="e499b-234">Можно также задать эти свойства для существующих виртуальных машин на hello **Общие** и **конфигурация оборудования** вкладки свойств виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-234">You can also set these properties for existing virtual machines on hello **General** and **Hardware Configuration** tabs of hello virtual machine properties.</span></span> <span data-ttu-id="e499b-235">Если не установить эти свойства в VMM вы будете может tooconfigure их на портале Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-235">If you don't set these properties in VMM you'll be able tooconfigure them in hello Azure Site Recovery portal.</span></span>

1. <span data-ttu-id="e499b-236">Защита tooenable выполнения hello следующая команда контейнера защиты tooget hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-236">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $ProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $CloudName
2. <span data-ttu-id="e499b-237">Получите сущность защиты hello (VM), выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-237">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $protectionContainer
3. <span data-ttu-id="e499b-238">Включите hello аварийного восстановления для hello виртуальной Машины, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-238">Enable hello DR for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable –Force -Policy $policy -RecoveryAzureStorageAccountId  $storageID "/subscriptions/217653172865hcvkchgvd/resourceGroups/rajanirgps/providers/Microsoft.Storage/storageAccounts/teststorageacc1

## <a name="test-your-deployment"></a><span data-ttu-id="e499b-239">Выполните тестирование развертывания</span><span class="sxs-lookup"><span data-stu-id="e499b-239">Test your deployment</span></span>
<span data-ttu-id="e499b-240">tootest тест можно выполнять развертывание отработку отказа для одной виртуальной машины или создайте план восстановления, состоящий из нескольких виртуальных машин, выполните тест отработки отказа для плана hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-240">tootest your deployment you can run a test fail-over for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test fail-over for hello plan.</span></span> <span data-ttu-id="e499b-241">Тестовая обработка отказа имитирует механизм отработки отказа и восстановления в изолированной сети.</span><span class="sxs-lookup"><span data-stu-id="e499b-241">Test fail-over simulates your fail-over and recovery mechanism in an isolated network.</span></span> <span data-ttu-id="e499b-242">Обратите внимание на следующее.</span><span class="sxs-lookup"><span data-stu-id="e499b-242">Note that:</span></span>

* <span data-ttu-id="e499b-243">Tooconnect toohello виртуальной машины в Azure с помощью удаленного рабочего стола, после отработки отказа hello, включите подключение к удаленному рабочему столу на виртуальной машине hello перед запуском тестовой отработки отказа hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-243">If you want tooconnect toohello virtual machine in Azure using Remote Desktop after hello fail-over, enable Remote Desktop Connection on hello virtual machine before you run hello test failover.</span></span>
* <span data-ttu-id="e499b-244">После отработки отказа будут использоваться открытый IP адрес tooconnect toohello виртуальной машины в Azure с помощью удаленного рабочего стола.</span><span class="sxs-lookup"><span data-stu-id="e499b-244">After fail-over, you'll use a public IP address tooconnect toohello virtual machine in Azure using Remote Desktop.</span></span> <span data-ttu-id="e499b-245">Если требуется toodo это, убедитесь, что нет политик домена, запретить подключения tooa виртуальной машины, с помощью общедоступного адреса.</span><span class="sxs-lookup"><span data-stu-id="e499b-245">If you want toodo this, ensure you don't have any domain policies that prevent you from connecting tooa virtual machine using a public address.</span></span>

<span data-ttu-id="e499b-246">toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).</span><span class="sxs-lookup"><span data-stu-id="e499b-246">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="e499b-247">Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="e499b-247">Run a test failover</span></span>
- <span data-ttu-id="e499b-248">Запустите тестовую отработку отказа hello, выполнив hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="e499b-248">Start hello test failover by running hello following command:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-a-planned-failover"></a><span data-ttu-id="e499b-249">Запуск запланированной отработки отказа</span><span class="sxs-lookup"><span data-stu-id="e499b-249">Run a planned failover</span></span>
- <span data-ttu-id="e499b-250">Запустите hello Запланированный переход на другой ресурс, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-250">Start hello planned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="e499b-251">Запуск незапланированной отработки отказа</span><span class="sxs-lookup"><span data-stu-id="e499b-251">Run an unplanned failover</span></span>
- <span data-ttu-id="e499b-252">Запуск hello внеплановой отработки отказа, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="e499b-252">Start hello unplanned failover by running hello following command:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $protectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -AzureVMNetworkId <string>  

## <span data-ttu-id="e499b-253"><a name=monitor></a> Мониторинг активности</span><span class="sxs-lookup"><span data-stu-id="e499b-253"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="e499b-254">Используйте следующие команды toomonitor hello действие hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-254">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="e499b-255">Обратите внимание, что на toowait между задания для обработки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="e499b-255">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

    Do
    {
        $job = Get-AzureSiteRecoveryJob -Id $associationJob.JobId;
        Write-Host "Job State:{0}, StateDescription:{1}" -f Job.State, $job.StateDescription;
        if($job -eq $null -or $job.StateDescription -ne "Completed")
        {
            $isJobLeftForProcessing = $true;
        }

    if($isJobLeftForProcessing)
        {
            Start-Sleep -Seconds 60
        }
    }While($isJobLeftForProcessing)



## <a name="next-steps"></a><span data-ttu-id="e499b-256">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e499b-256">Next steps</span></span>
<span data-ttu-id="e499b-257">[Узнайте больше](/powershell/module/azurerm.recoveryservices.backup/#recovery) об использовании командлетов PowerShell инструмента Azure Resource Manager для службы Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e499b-257">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
