---
title: "aaaReplicate приложения (Azure tooAzure) | Документы Microsoft"
description: "В этой статье описывается, как tooset репликацию виртуальных машин выполняется в одном регионе Azure слишком другую область в Azure."
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a><span data-ttu-id="128e2-103">Реплицировать виртуальные машины Azure tooanother регион Azure</span><span class="sxs-lookup"><span data-stu-id="128e2-103">Replicate Azure virtual machines tooanother Azure region</span></span>



>[!NOTE]
>
> <span data-ttu-id="128e2-104">Репликация Azure Site Recovery для виртуальных машин Azure сейчас доступна в предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="128e2-104">Site Recovery replication for Azure virtual machines is currently in preview.</span></span>

<span data-ttu-id="128e2-105">В этой статье описывается, как tooset репликацию виртуальных машин выполняется в один регион Azure tooanother регион Azure.</span><span class="sxs-lookup"><span data-stu-id="128e2-105">This article describes how tooset up replication of virtual machines running in one Azure region tooanother Azure region.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="128e2-106">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="128e2-106">Prerequisites</span></span>

* <span data-ttu-id="128e2-107">Hello предполагается, что уже известно о Site Recovery и хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="128e2-107">hello article assumes that you already know about Site Recovery and Recovery Services Vault.</span></span> <span data-ttu-id="128e2-108">Необходимо toohave созданные предварительной «Хранилище служб восстановления».</span><span class="sxs-lookup"><span data-stu-id="128e2-108">You need toohave a 'Recovery services vault' pre created.</span></span>

    >[!NOTE]
    >
    > <span data-ttu-id="128e2-109">Рекомендуется создать hello «Хранилище служб восстановления» в hello место хранения вашей tooreplicate виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="128e2-109">It is recommended that you create hello 'Recovery services vault' in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="128e2-110">Например, если целевое расположение — "Центральная часть США", создайте хранилище в этом регионе.</span><span class="sxs-lookup"><span data-stu-id="128e2-110">For example, if your target location is 'Central US', create vault in 'Central US'.</span></span>

* <span data-ttu-id="128e2-111">При использовании правил группы безопасности сети (NSG) или подключение к Интернету toooutbound доступ в toocontrol прокси-сервера брандмауэра на виртуальных машинах Azure hello, убедитесь, что требуется, вы белого списка hello URL-адреса или IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="128e2-111">If you are using Network Security Groups (NSG) rules or firewall proxy toocontrol access toooutbound internet connectivity on hello Azure VMs, ensure that you whitelist hello required URLs or IPs.</span></span> <span data-ttu-id="128e2-112">См. слишком[документ руководства по сети](./site-recovery-azure-to-azure-networking-guidance.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="128e2-112">Refer too[Networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md) for more details.</span></span>

* <span data-ttu-id="128e2-113">Если у вас есть подключение ExpressRoute или VPN-подключение между локальной и hello исходное местоположение в Azure, выполните [рекомендации по восстановлению сайта для ExpressRoute Azure tooon организациями и конфигурацию виртуальной частной сети](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) документа.</span><span class="sxs-lookup"><span data-stu-id="128e2-113">If you have an ExpressRoute or a VPN connection between on-premises and hello source location in Azure, follow [Site Recovery Considerations for Azure tooon-premises ExpressRoute / VPN configuration](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) document.</span></span>

* <span data-ttu-id="128e2-114">Учетная запись пользователя Azure должен toohave определенных [разрешений](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable репликацию виртуальной машины Azure.</span><span class="sxs-lookup"><span data-stu-id="128e2-114">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>

* <span data-ttu-id="128e2-115">Ваша подписка Azure должен быть включен toocreate виртуальные машины в целевом расположении hello требуется toouse как область аварийного восстановления.</span><span class="sxs-lookup"><span data-stu-id="128e2-115">Your Azure subscription should be enabled toocreate VMs in hello target location you want toouse as DR region.</span></span> <span data-ttu-id="128e2-116">Вы можете обратиться поддержки tooenable hello необходимые квоты.</span><span class="sxs-lookup"><span data-stu-id="128e2-116">You can contact support tooenable hello required quota.</span></span>

## <a name="enable-replication-from-azure-site-recovery-vault"></a><span data-ttu-id="128e2-117">Включение репликации из хранилища Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="128e2-117">Enable replication from Azure Site Recovery vault</span></span>
<span data-ttu-id="128e2-118">В этом примере мы выполнит репликацию виртуальных машин, работающих в toohello расположение Azure «Восточная Азия» hello "Юго-Восточная Азия" расположение.</span><span class="sxs-lookup"><span data-stu-id="128e2-118">For this illustration, we will replicate VMs running  in hello ‘East Asia’ Azure location toohello ‘South East Asia’ location.</span></span> <span data-ttu-id="128e2-119">Ниже приведены шаги Hello.</span><span class="sxs-lookup"><span data-stu-id="128e2-119">hello steps are as follows:</span></span>

 <span data-ttu-id="128e2-120">Нажмите кнопку **+ реплицировать** в репликации tooenable hello хранилище для виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="128e2-120">Click **+Replicate** in hello vault tooenable replication for hello virtual machines.</span></span>

1. <span data-ttu-id="128e2-121">**Источник:** он ссылается точка происхождения hello машин в этом случае toohello **Azure**.</span><span class="sxs-lookup"><span data-stu-id="128e2-121">**Source:** It refers toohello point of origin of hello machines which in this case is **Azure**.</span></span>

2. <span data-ttu-id="128e2-122">**Исходное местоположение:** это hello регион Azure, с которого осуществляется tooprotect виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="128e2-122">**Source location:** It is hello Azure region from where you want tooprotect your virtual machines.</span></span> <span data-ttu-id="128e2-123">На этом рисунке hello источник будет «Восточная Азия»</span><span class="sxs-lookup"><span data-stu-id="128e2-123">For this illustration, hello source location will be 'East Asia'</span></span>

3. <span data-ttu-id="128e2-124">**Модель развертывания:** он ссылается модель развертывания Azure toohello hello исходных компьютеров.</span><span class="sxs-lookup"><span data-stu-id="128e2-124">**Deployment model:** It refers toohello Azure deployment model of hello source machines.</span></span> <span data-ttu-id="128e2-125">Можно выбрать либо классическом или диспетчер ресурсов и машин, принадлежащих конкретной модели toohello будут указаны для защиты в следующем шаге hello.</span><span class="sxs-lookup"><span data-stu-id="128e2-125">You can select either classic or resource manager and machines belonging toohello specific model will be listed for protection in hello next step.</span></span>

      >[!NOTE]
      >
      > <span data-ttu-id="128e2-126">Классическую виртуальную машину можно реплицировать или восстанавливать только как классическую виртуальную машину,</span><span class="sxs-lookup"><span data-stu-id="128e2-126">You can only replicate a classic virtual machine and recover it as a classic virtual machine.</span></span> <span data-ttu-id="128e2-127">ее нельзя восстановить в качестве виртуальной машины диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="128e2-127">You cannot recover it as a Resource Manager virtual machine.</span></span>

4. <span data-ttu-id="128e2-128">**Группа ресурсов:** его, toowhich группы ресурсов hello, принадлежат исходные виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="128e2-128">**Resource Group:** It’s hello resource group toowhich your source virtual machines belong.</span></span> <span data-ttu-id="128e2-129">Для защиты в следующем шаге hello будут перечислены все hello виртуальных машин в группе hello выбранной группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="128e2-129">All hello VMs under hello selected resource group will be listed for protection in hello next step.</span></span>

    ![Включение репликации](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

<span data-ttu-id="128e2-131">В **виртуальных машин > выберите виртуальные машины**щелкните и выберите каждый компьютер, tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="128e2-131">In **Virtual Machines > Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="128e2-132">Можно выбрать только те компьютеры, для которых можно включить репликацию.</span><span class="sxs-lookup"><span data-stu-id="128e2-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="128e2-133">Затем нажмите кнопку ОК.</span><span class="sxs-lookup"><span data-stu-id="128e2-133">Then click OK.</span></span>
    <span data-ttu-id="128e2-134">![Включение репликации](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span><span class="sxs-lookup"><span data-stu-id="128e2-134">![Enable replication](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)</span></span>


<span data-ttu-id="128e2-135">В разделе "Параметры" можно настроить свойства целевого веб-сайта.</span><span class="sxs-lookup"><span data-stu-id="128e2-135">Under Settings section you can configure target site properties</span></span>

1. <span data-ttu-id="128e2-136">**Целевое расположение:** hello там, где исходные данные виртуальных машин будут реплицированы.</span><span class="sxs-lookup"><span data-stu-id="128e2-136">**Target Location:**  This is hello location where your source virtual machine data will be replicated.</span></span> <span data-ttu-id="128e2-137">В зависимости от расположения выбранной машины Site Recovery предоставляет hello список регионов подходящий конечный объект.</span><span class="sxs-lookup"><span data-stu-id="128e2-137">Depending upon your selected machines location, Site Recovery will provide you hello list of suitable target regions.</span></span>

    > [!TIP]
    > <span data-ttu-id="128e2-138">Рекомендуется tookeep целевое расположение хранилища же на момент восстановления служб.</span><span class="sxs-lookup"><span data-stu-id="128e2-138">It is recommended tookeep target location same as of your recovery services vault.</span></span>

2. <span data-ttu-id="128e2-139">**Целевая группа ресурсов:** это hello ресурсов группы toowhich будет принадлежать все реплицированные виртуальные машины. По умолчанию ASR создаст новую группу ресурсов в целевой области hello с именем, имеющим суффикс «asr».</span><span class="sxs-lookup"><span data-stu-id="128e2-139">**Target resource group :** It is hello resource group toowhich all your replicated virtual machines will belong.By default ASR will create a new resource group in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="128e2-140">В случае, если группы ресурсов, созданные ASR уже существует, он будет использоваться повторно. Вы также можете toocustomize его, как показано в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="128e2-140">In case resource group created by ASR already exist, it will be reused.You can also choose toocustomize it as shown in hello section below.</span></span>    
3. <span data-ttu-id="128e2-141">**Целевая виртуальная сеть:** по умолчанию ASR создаст новую виртуальную сеть в целевой области hello с именем, имеющим суффикс «asr».</span><span class="sxs-lookup"><span data-stu-id="128e2-141">**Target Virtual Network:** By default, ASR will create a new virtual network in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="128e2-142">Это будет сопоставленных tooyour Исходная сеть и будет использоваться для будущих защиту.</span><span class="sxs-lookup"><span data-stu-id="128e2-142">This will be mapped tooyour source network and will be used for any future protection.</span></span>

    > [!NOTE]
    > <span data-ttu-id="128e2-143">[Проверьте сведения о сетевых](site-recovery-network-mapping-azure-to-azure.md) tooknow Дополнительные сведения о сопоставлении сетей.</span><span class="sxs-lookup"><span data-stu-id="128e2-143">[Check networking details](site-recovery-network-mapping-azure-to-azure.md) tooknow more about network mapping.</span></span>

4. <span data-ttu-id="128e2-144">**Использовать учетные записи хранения:** по умолчанию, ASR создаст hello новой целевой учетной записи хранения которой копирует конфигурацию хранилища исходной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="128e2-144">**Target Storage accounts:** By default, ASR will create hello new target storage account mimicking your source VM storage configuration.</span></span> <span data-ttu-id="128e2-145">Если учетная запись хранения, создаваемая ASR, уже имеется, она будет использоваться повторно.</span><span class="sxs-lookup"><span data-stu-id="128e2-145">In case storage account created by ASR already exist, it will be reused.</span></span>

5. <span data-ttu-id="128e2-146">**Кэширование учетных записей хранения:** ASR необходима учетная запись дополнительного хранилища, именем хранилища кэша в области источника hello.</span><span class="sxs-lookup"><span data-stu-id="128e2-146">**Cache Storage accounts:** ASR needs extra storage account called cache storage in hello source region.</span></span> <span data-ttu-id="128e2-147">Здравствуйте, все изменения отслеживаются и отправленные учетной записи хранилища toocache перед репликацией этих toohello целевое расположение исходных виртуальных проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="128e2-147">All hello changes happening on hello source VMs are tracked and sent toocache storage account before replicating those toohello target location.</span></span>

6. <span data-ttu-id="128e2-148">**Группа доступности:** по умолчанию, ASR создаст новый доступности в целевой области hello с именем, имеющим суффикс «asr».</span><span class="sxs-lookup"><span data-stu-id="128e2-148">**Availability set :** By default, ASR will create a new availability set in hello target region with name having "asr" suffix.</span></span> <span data-ttu-id="128e2-149">Если группа доступности, создаваемая ASR, уже имеется, она будет использоваться повторно.</span><span class="sxs-lookup"><span data-stu-id="128e2-149">In case availability set created by ASR already exist, it will be reused.</span></span>

7.  <span data-ttu-id="128e2-150">**Политика репликации:** он определяет параметры hello для восстановления точки хранения журнала и приложения согласованный моментальный снимок интервал.</span><span class="sxs-lookup"><span data-stu-id="128e2-150">**Replication Policy:** It defines hello settings for recovery point retention history and app consistent snapshot frequency.</span></span> <span data-ttu-id="128e2-151">По умолчанию ASR создаст политику репликации с параметрами по умолчанию "24 часа" для хранения точки восстановления и "60 минут" — для периодичности создания моментальных снимков, совместимых с приложениями.</span><span class="sxs-lookup"><span data-stu-id="128e2-151">By default, ASR will create a new replication policy with default settings of ‘24 hours’ for recovery point retention and ’60 minutes’ for app consistent snapshot frequency.</span></span>

    ![Включение репликации](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a><span data-ttu-id="128e2-153">Настройка целевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="128e2-153">Customize target resources</span></span>

<span data-ttu-id="128e2-154">В случае, если требуется, чтобы по умолчанию hello toochange, используемые ASR, можно изменить параметры hello в зависимости от потребностей.</span><span class="sxs-lookup"><span data-stu-id="128e2-154">In case you want toochange hello defaults used by ASR, you can change hello settings based on your needs.</span></span>

1. <span data-ttu-id="128e2-155">**Настройка:** нажмите кнопку toochange hello по умолчанию, используемые ASR.</span><span class="sxs-lookup"><span data-stu-id="128e2-155">**Customize:** Click it toochange hello defaults used by ASR.</span></span>

2. <span data-ttu-id="128e2-156">**Целевая группа ресурсов:** hello группы ресурсов можно выбрать из списка всех групп ресурсов hello, существующих в целевом расположении hello в рамках подписки hello hello.</span><span class="sxs-lookup"><span data-stu-id="128e2-156">**Target resource group :**  You can select hello resource group from hello list of all hello resource groups existing in hello target location within hello subscription.</span></span>

3. <span data-ttu-id="128e2-157">**Целевая виртуальная сеть:** hello список всех hello виртуальной сети можно найти в целевом расположении hello.</span><span class="sxs-lookup"><span data-stu-id="128e2-157">**Target Virtual Network:** You can find hello list of all hello virtual network in hello target location.</span></span>

4. <span data-ttu-id="128e2-158">**Группа доступности:** можно добавить только доступность наборы параметров toohello виртуальных машин, которые являются частью доступности в исходной области.</span><span class="sxs-lookup"><span data-stu-id="128e2-158">**Availability set :** You can only add availability sets settings toohello virtual machines which are a part of availability in source region.</span></span>

5. <span data-ttu-id="128e2-159">**Target Storage accounts** (Целевые учетные записи хранения):</span><span class="sxs-lookup"><span data-stu-id="128e2-159">**Target Storage accounts:**</span></span>

<span data-ttu-id="128e2-160">![Включение репликации](./media/site-recovery-replicate-azure-to-azure/customize.PNG). Щелкните **Create target resource** (Создать целевой ресурс) и включите репликацию.</span><span class="sxs-lookup"><span data-stu-id="128e2-160">![Enable replication](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Click on **Create target resource** and Enable Replication</span></span>


<span data-ttu-id="128e2-161">После защищенных виртуальных машин можно проверить состояние работоспособности виртуальных машин в группе hello **реплицируются элементов**</span><span class="sxs-lookup"><span data-stu-id="128e2-161">Once virtual machines are protected you can check hello status of VMs health under **Replicated items**</span></span>

>[!NOTE]
><span data-ttu-id="128e2-162">Во время hello время начальной репликации удалось вероятность того, что состояние принимает toorefresh времени, и вы не видите выполняется некоторое время.</span><span class="sxs-lookup"><span data-stu-id="128e2-162">During hello time of initial replication there could a possibility that status takes time toorefresh and you don't see progress for some time.</span></span> <span data-ttu-id="128e2-163">Можно щелкнуть кнопку обновления hello над hello hello колонке tooget hello последнее состояние.</span><span class="sxs-lookup"><span data-stu-id="128e2-163">You can click hello Refresh button on hello top of hello blade tooget hello latest status.</span></span>
>

![Включение репликации](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a><span data-ttu-id="128e2-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="128e2-165">Next steps</span></span>
- <span data-ttu-id="128e2-166">Дополнительные сведения о выполнении тестовой отработки отказа см. в [этой статье](site-recovery-test-failover-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="128e2-166">[Learn more](site-recovery-test-failover-to-azure.md) about running a test failover.</span></span>
- <span data-ttu-id="128e2-167">[Дополнительные сведения](site-recovery-failover.md) о различных типов отработки отказа и как toorun их.</span><span class="sxs-lookup"><span data-stu-id="128e2-167">[Learn more](site-recovery-failover.md) about different types of failovers, and how toorun them.</span></span>
- <span data-ttu-id="128e2-168">Дополнительные сведения о [с использованием планов восстановления](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="128e2-168">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
- <span data-ttu-id="128e2-169">Дополнительные сведения о повторной защите виртуальных машин Azure после отработки отказа см.в статье [Повторное включение защиты виртуальных машин, восстанавливаемых из Azure на локальный сайт](site-recovery-how-to-reprotect.md).</span><span class="sxs-lookup"><span data-stu-id="128e2-169">Learn more about [reprotecting Azure  VMs](site-recovery-how-to-reprotect.md) after failover.</span></span>
