---
title: "aaaReplicate виртуальных машин Hyper-V в VMM tooa вторичного сайта с помощью PowerShell (диспетчера ресурсов Azure) | Документы Microsoft"
description: "Описывает, каким образом tooa с помощью PowerShell (диспетчера ресурсов) вторичный сайт VMM облаков toodeploy Azure Site Recovery tooorchestrate репликации, отработки отказа и восстановления виртуальных машин Hyper-V в VMM"
services: site-recovery
documentationcenter: 
author: sujaytalasila
manager: rochakm
editor: raynew
ms.assetid: 9d38e9c3-217c-4e44-830c-575e9a4141f2
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: a769dcc68d66c18b9dc47539071f4d0e0f1db70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="87200-103">Реплицировать виртуальные машины Hyper-V в VMM облаков tooa вторичный сайт VMM с помощью PowerShell (диспетчера ресурсов)</span><span class="sxs-lookup"><span data-stu-id="87200-103">Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="87200-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="87200-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="87200-105">Классический портал</span><span class="sxs-lookup"><span data-stu-id="87200-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="87200-106">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="87200-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="87200-107">Вас приветствует tooAzure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="87200-107">Welcome tooAzure Site Recovery!</span></span> <span data-ttu-id="87200-108">В этой статье следует используйте, если необходимо, чтобы tooreplicate локальных виртуальных машин Hyper-V управляются в облаках диспетчера виртуальных машин System Center (VMM): tooa вторичного сайта.</span><span class="sxs-lookup"><span data-stu-id="87200-108">Use this article if you want tooreplicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds tooa secondary site.</span></span>

<span data-ttu-id="87200-109">В этой статье показано, как toouse PowerShell tooautomate общие задачи должны tooperform при настройке Azure Site Recovery tooreplicate Hyper-V виртуальных машин в облаках VMM System Center VMM облаков центра tooSystem вторичном сайте.</span><span class="sxs-lookup"><span data-stu-id="87200-109">This article shows you how toouse PowerShell tooautomate common tasks you need tooperform when you set up Azure Site Recovery tooreplicate Hyper-V virtual machines in System Center VMM clouds tooSystem Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="87200-110">включает описание необходимых условий для сценария hello Hello статьи, а также демонстрируется</span><span class="sxs-lookup"><span data-stu-id="87200-110">hello article includes prerequisites for hello scenario, and shows you</span></span>

* <span data-ttu-id="87200-111">Как tooset копирование хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="87200-111">How tooset up a Recovery Services Vault</span></span>
* <span data-ttu-id="87200-112">Установите hello поставщика Azure Site Recovery на исходном сервере VMM hello и целевой сервер VMM hello</span><span class="sxs-lookup"><span data-stu-id="87200-112">Install hello Azure Site Recovery Provider on hello source VMM server and hello target VMM server</span></span>
* <span data-ttu-id="87200-113">Зарегистрируйте серверы VMM hello в хранилище hello</span><span class="sxs-lookup"><span data-stu-id="87200-113">Register hello VMM server(s) in hello vault</span></span>
* <span data-ttu-id="87200-114">Настройте политику репликации для облака VMM hello.</span><span class="sxs-lookup"><span data-stu-id="87200-114">Configure replication policy for hello VMM Cloud.</span></span> <span data-ttu-id="87200-115">параметры репликации Hello hello политики будет применен tooall защищенные виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="87200-115">hello replication settings in hello policy will be applied tooall protected virtual machines</span></span>
* <span data-ttu-id="87200-116">Включите защиту для виртуальных машин hello.</span><span class="sxs-lookup"><span data-stu-id="87200-116">Enable protection for hello virtual machines.</span></span>
* <span data-ttu-id="87200-117">Тестовая отработка отказа hello виртуальных машин, отдельно или как часть toomake для плана восстановления, убедиться, что все работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="87200-117">Test hello failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>
* <span data-ttu-id="87200-118">Выполнение плановой или незапланированной отработки отказа виртуальных машин по отдельности или в составе toomake для плана восстановления, убедиться, что все работает должным образом.</span><span class="sxs-lookup"><span data-stu-id="87200-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan toomake sure everything is working as expected.</span></span>

<span data-ttu-id="87200-119">Если возникли проблемы с установкой этого сценария опубликовать вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="87200-119">If you run into problems setting up this scenario, post your questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="87200-120">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md) .</span><span class="sxs-lookup"><span data-stu-id="87200-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="87200-121">Azure также содержит два портала — hello классический портал Azure, поддерживающий hello классической модели развертывания и hello портал Azure с поддержкой обе модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="87200-121">Azure also has two portals – hello Azure classic portal that supports hello classic deployment model, and hello Azure portal with support for both deployment models.</span></span> <span data-ttu-id="87200-122">В этой статье рассматриваются hello модели развертывания диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="87200-122">This article covers hello Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="87200-123">Предварительные требования для локальной среды</span><span class="sxs-lookup"><span data-stu-id="87200-123">On-premises prerequisites</span></span>
<span data-ttu-id="87200-124">Вот что вам понадобится в hello первичного и вторичного локальных сайтов toodeploy этот сценарий:</span><span class="sxs-lookup"><span data-stu-id="87200-124">Here's what you'll need in hello primary and secondary on-premises sites toodeploy this scenario:</span></span>

| <span data-ttu-id="87200-125">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="87200-125">**Prerequisites**</span></span> | <span data-ttu-id="87200-126">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="87200-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="87200-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="87200-127">**VMM**</span></span> |<span data-ttu-id="87200-128">Мы рекомендуем развернуть сервер VMM в первичном сайте hello и сервера VMM на вторичном сайте hello.</span><span class="sxs-lookup"><span data-stu-id="87200-128">We recommend you deploy a VMM server in hello primary site and a VMM server in hello secondary site.</span></span><br/><br/> <span data-ttu-id="87200-129">Вы можете также [выполнять репликацию между облаками на отдельном сервере VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="87200-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="87200-130">toodo это необходимо по крайней мере два облака, настроенные на сервере VMM hello.</span><span class="sxs-lookup"><span data-stu-id="87200-130">toodo this you'll need at least two clouds configured on hello VMM server.</span></span><br/><br/> <span data-ttu-id="87200-131">Серверы VMM должен работать под управлением System Center 2012 SP1 с последними обновлениями hello.</span><span class="sxs-lookup"><span data-stu-id="87200-131">VMM servers should be running at least System Center 2012 SP1 with hello latest updates.</span></span><br/><br/> <span data-ttu-id="87200-132">Каждый сервер VMM, должна иметь на один или несколько облаков настроен и все должен иметь набор профилей hello емкости Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="87200-132">Each VMM server must have at one or more clouds configured and all clouds must have hello Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="87200-133">Облака должны содержать одну или несколько групп узлов VMM.</span><span class="sxs-lookup"><span data-stu-id="87200-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="87200-134">Дополнительные сведения о настройке облаков VMM в [hello Настройка VMM облако структуры](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), и [Пошаговое руководство: создание частных облаков с помощью System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="87200-134">Learn more about setting up VMM clouds in [Configuring hello VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="87200-135">Серверы VMM должны иметь доступ к Интернету.</span><span class="sxs-lookup"><span data-stu-id="87200-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="87200-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="87200-136">**Hyper-V**</span></span> |<span data-ttu-id="87200-137">Серверы Hyper-V должны работать под управлением Windows Server 2012 с ролью Hyper-V hello и иметь hello установлены последние обновления.</span><span class="sxs-lookup"><span data-stu-id="87200-137">Hyper-V servers must be running at least Windows Server 2012 with hello Hyper-V role and have hello latest updates installed.</span></span><br/><br/> <span data-ttu-id="87200-138">Сервер Hyper-V должен содержать одну или несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="87200-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="87200-139">Серверы узла Hyper-V должны находиться в группах узлов в hello Первичное и вторичное облака VMM.</span><span class="sxs-lookup"><span data-stu-id="87200-139">Hyper-V host servers should be located in host groups in hello primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="87200-140">Если вы используете Hyper-V в кластере на платформе Windows Server 2012 R2, то необходимо установить [обновление 2961977](https://support.microsoft.com/kb/2961977).</span><span class="sxs-lookup"><span data-stu-id="87200-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="87200-141">Если вы используете Hyper-V в кластере на платформе Windows Server 2012, то учтите, что брокер кластера не создается автоматически при использовании кластера на основе статических IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="87200-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="87200-142">Брокер кластера hello tooconfigure вам потребуется вручную.</span><span class="sxs-lookup"><span data-stu-id="87200-142">You'll need tooconfigure hello cluster broker manually.</span></span> <span data-ttu-id="87200-143">[Подробная информация](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="87200-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="87200-144">**Поставщик**</span><span class="sxs-lookup"><span data-stu-id="87200-144">**Provider**</span></span> |<span data-ttu-id="87200-145">Во время развертывания службы восстановления сайтов установите hello поставщика Azure Site Recovery на серверах VMM.</span><span class="sxs-lookup"><span data-stu-id="87200-145">During Site Recovery deployment you install hello Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="87200-146">Hello поставщик взаимодействует с Site Recovery через HTTPS 443 tooorchestrate репликации.</span><span class="sxs-lookup"><span data-stu-id="87200-146">hello Provider communicates with Site Recovery over HTTPS 443 tooorchestrate replication.</span></span> <span data-ttu-id="87200-147">Репликация данных между hello основной и дополнительный серверы Hyper-V через hello локальной сети или VPN-подключения.</span><span class="sxs-lookup"><span data-stu-id="87200-147">Data replication occurs between hello primary and secondary Hyper-V servers over hello LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="87200-148">Hello поставщик, запущенный на сервере VMM hello должен получить доступ к URL-адреса toothese: *. hypervrecoverymanager.windowsazure.com; *. accesscontrol.windows.net; *. backup.windowsazure.com; *. blob.core.windows.net; *. store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="87200-148">hello Provider running on hello VMM server needs access toothese URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="87200-149">Разрешить связь брандмауэра из toohello серверы VMM hello, кроме [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) и разрешить hello протокола HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="87200-149">In addition allow firewall communication from hello VMM servers toohello [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow hello HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="87200-150">Предварительные требования сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="87200-150">Network mapping prerequisites</span></span>
<span data-ttu-id="87200-151">Сети сопоставление между сетями виртуальных Машин VMM на hello первичных и вторичных серверов VMM для:</span><span class="sxs-lookup"><span data-stu-id="87200-151">Network mapping maps between VMM VM networks on hello primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="87200-152">Оптимальное размещение виртуальных машин реплик на вторичных узлах Hyper-V после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="87200-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="87200-153">Подключение сети виртуальных Машин tooappropriate виртуальные машины реплики.</span><span class="sxs-lookup"><span data-stu-id="87200-153">Connect replica VMs tooappropriate VM networks.</span></span>
* <span data-ttu-id="87200-154">Если не настроить сетевое сопоставление реплики виртуальных машин не будет tooany подключенной сети после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="87200-154">If you don't configure network mapping replica VMs won't be connected tooany network after failover.</span></span>
* <span data-ttu-id="87200-155">Если требуется, чтобы tooset сети сопоставления во время восстановления сайта здесь это вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="87200-155">If you want tooset up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="87200-156">Убедитесь tooa подключенной сети виртуальной Машины VMM виртуальные машины на исходном hello сервер узла Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="87200-156">Make sure that VMs on hello source Hyper-V host server are connected tooa VMM VM network.</span></span> <span data-ttu-id="87200-157">Сеть должна быть связанной tooa логической сети, связанной с облаком hello.</span><span class="sxs-lookup"><span data-stu-id="87200-157">That network should be linked tooa logical network that is associated with hello cloud.</span></span>
  * <span data-ttu-id="87200-158">Убедитесь, что hello вторичное облако, которое будет использоваться для восстановления настроена соответствующая сеть ВМ.</span><span class="sxs-lookup"><span data-stu-id="87200-158">Verify that hello secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="87200-159">Сеть виртуальной Машины должна была tooa связанной логической сети, связанной с hello вторичное облако.</span><span class="sxs-lookup"><span data-stu-id="87200-159">That VM network should be linked tooa logical network that's associated with hello secondary cloud.</span></span>

<span data-ttu-id="87200-160">Дополнительные сведения о настройке сетей в VMM в hello ниже статьи</span><span class="sxs-lookup"><span data-stu-id="87200-160">Learn more about configuring VMM networks in hello below articles</span></span>

* [<span data-ttu-id="87200-161">Как tooconfigure логических сетей в VMM</span><span class="sxs-lookup"><span data-stu-id="87200-161">How tooconfigure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="87200-162">Как tooconfigure ВМ сетей и шлюзов в VMM</span><span class="sxs-lookup"><span data-stu-id="87200-162">How tooconfigure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="87200-163">[Узнайте больше](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) о принципе действия сетевого сопоставления.</span><span class="sxs-lookup"><span data-stu-id="87200-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="87200-164">Необходимые компоненты PowerShell</span><span class="sxs-lookup"><span data-stu-id="87200-164">PowerShell prerequisites</span></span>
<span data-ttu-id="87200-165">Убедитесь, что у вас есть toogo готовности Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87200-165">Make sure you have Azure PowerShell ready toogo.</span></span> <span data-ttu-id="87200-166">Если вы уже используете PowerShell, вам потребуется tooupgrade tooversion 0.8.10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="87200-166">If you are already using PowerShell, you'll need tooupgrade tooversion 0.8.10 or later.</span></span> <span data-ttu-id="87200-167">Сведения о настройке PowerShell см. в разделе hello [проводят tooinstall и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="87200-167">For information about setting up PowerShell, see hello [Guide tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="87200-168">После установки и настройки PowerShell вы можете просматривать все hello доступных командлетов для службы hello [здесь](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="87200-168">Once you have set up and configured PowerShell, you can view all of hello available cmdlets for hello service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="87200-169">toolearn советы, помогающие использовать командлеты hello, например как значения параметров, входы и выходы обычно обрабатываются в Azure PowerShell, в разделе hello [руководство по работе с командлетами Azure tooget](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="87200-169">toolearn about tips that can help you use hello cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see hello [Guide tooget Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-hello-subscription"></a><span data-ttu-id="87200-170">Шаг 1: Задайте подписку hello</span><span class="sxs-lookup"><span data-stu-id="87200-170">Step 1: Set hello subscription</span></span>
1. <span data-ttu-id="87200-171">Из Azure powershell, tooyour входа учетной записи Azure: с помощью следующих командлетов hello</span><span class="sxs-lookup"><span data-stu-id="87200-171">From Azure powershell, login tooyour Azure account: using hello following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="87200-172">Получите список своих подписок.</span><span class="sxs-lookup"><span data-stu-id="87200-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="87200-173">Выводит также список hello subscriptionIDs для каждой из подписок hello.</span><span class="sxs-lookup"><span data-stu-id="87200-173">This will also list hello subscriptionIDs for each of hello subscriptions.</span></span> <span data-ttu-id="87200-174">Запишите subscriptionID hello hello подписки, в котором вы хотите хранилище служб восстановления toocreate hello</span><span class="sxs-lookup"><span data-stu-id="87200-174">Note down hello subscriptionID of hello subscription in which you wish toocreate hello recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="87200-175">Задать hello подписки, в какие hello хранилище служб восстановления является toobe созданные упомянуть hello идентификатор подписки</span><span class="sxs-lookup"><span data-stu-id="87200-175">Set hello subscription in which hello recovery services vault is toobe created by mentioning hello subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="87200-176">Шаг 2. Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="87200-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="87200-177">Если у вас еще нет группы ресурсов Azure Resource Manager, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="87200-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="87200-178">Создайте новое хранилище служб восстановления и сохраните hello, созданном объекте хранилища ASR в переменной (будет использоваться позднее).</span><span class="sxs-lookup"><span data-stu-id="87200-178">Create a new Recovery Services vault and save hello created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="87200-179">Вы также можете получить hello ASR хранилища объекта post создания с помощью командлета Get-AzureRMRecoveryServicesVault hello:-</span><span class="sxs-lookup"><span data-stu-id="87200-179">You can also retrieve hello ASR vault object post creation using hello Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-hello-recovery-services-vault-context"></a><span data-ttu-id="87200-180">Шаг 3: Установка контекста hello хранилище служб восстановления</span><span class="sxs-lookup"><span data-stu-id="87200-180">Step 3: Set hello Recovery Services Vault context</span></span>
1. <span data-ttu-id="87200-181">Если хранилище уже создан, запустите hello ниже команда tooget hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="87200-181">If you have a vault already created, run hello below command tooget hello vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="87200-182">Задайте контекст хранилища hello, выполнив hello ниже команду.</span><span class="sxs-lookup"><span data-stu-id="87200-182">Set hello vault context by running hello below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-hello-azure-site-recovery-provider"></a><span data-ttu-id="87200-183">Шаг 4: Установка поставщика Azure Site Recovery hello</span><span class="sxs-lookup"><span data-stu-id="87200-183">Step 4: Install hello Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="87200-184">На виртуальной машине VMM hello создайте каталог, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="87200-184">On hello VMM machine, create a directory by running hello following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="87200-185">Извлеките файлы hello, с помощью поставщика загружаются hello, выполнив следующую команду hello</span><span class="sxs-lookup"><span data-stu-id="87200-185">Extract hello files using hello downloaded provider by running hello following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="87200-186">Установите поставщик hello, с помощью hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="87200-186">Install hello provider using hello following commands:</span></span>

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

   <span data-ttu-id="87200-187">Дождитесь установки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="87200-187">Wait for hello installation toofinish.</span></span>
4. <span data-ttu-id="87200-188">Зарегистрируйте сервер hello в хранилище hello, с помощью hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="87200-188">Register hello server in hello vault using hello following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="87200-189">Шаг 5. Создание и связывание политики репликации</span><span class="sxs-lookup"><span data-stu-id="87200-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="87200-190">Создайте политику репликации Hyper-V 2012 R2, запустив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="87200-190">Create a Hyper-V 2012 R2 replication policy by running hello following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify hello number of hours tooretain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify hello frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify hello port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="87200-191">Hello облака VMM может содержать узлы Hyper-V под управлением других версий Windows Server (согласно hello требования Hyper-V), но политика репликации hello — версии операционной системы.</span><span class="sxs-lookup"><span data-stu-id="87200-191">hello VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in hello Hyper-V prerequisites), but hello replication policy is OS version specific.</span></span> <span data-ttu-id="87200-192">Если вы используете узлы с разными версиями операционных систем, то создайте отдельные политики репликации для каждого типа версии ОС.</span><span class="sxs-lookup"><span data-stu-id="87200-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="87200-193">Пример. Если у вас есть пять узлов с Windows Server 2012 и три с Windows Server 2012 R2, то создайте две политики репликации — по одной для каждого типа версии ОС.</span><span class="sxs-lookup"><span data-stu-id="87200-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="87200-194">Получите, выполнив следующие команды hello hello основную защиту (основное облако VMM) и восстановления защиты контейнер (восстановление облака VMM):</span><span class="sxs-lookup"><span data-stu-id="87200-194">Get hello primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running hello following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="87200-195">Получить политику hello, созданный на шаге 1, с помощью hello понятное имя политики hello</span><span class="sxs-lookup"><span data-stu-id="87200-195">Retrieve hello policy you created in step 1 using hello friendly name of hello policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="87200-196">Запуск сопоставления hello hello контейнера защиты (облака VMM) с политикой репликации hello:</span><span class="sxs-lookup"><span data-stu-id="87200-196">Start hello association of hello protection container (VMM Cloud) with hello replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="87200-197">Дождитесь toocomplete задания связи политики hello.</span><span class="sxs-lookup"><span data-stu-id="87200-197">Wait for hello policy association job toocomplete.</span></span> <span data-ttu-id="87200-198">Можно проверить, если hello задание завершено с помощью hello, следующий фрагмент команды PowerShell.</span><span class="sxs-lookup"><span data-stu-id="87200-198">You can check if hello job has completed using hello following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="87200-199">После завершения обработки задания hello, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="87200-199">After hello job has finished processing, run hello following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="87200-200">toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).</span><span class="sxs-lookup"><span data-stu-id="87200-200">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="87200-201">Шаг 6. Настройка сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="87200-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="87200-202">Первая команда Hello возвращает серверов для hello текущее хранилище Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="87200-202">hello first command gets servers for hello current Azure Site Recovery vault.</span></span> <span data-ttu-id="87200-203">Hello команда сохраняет серверы Microsoft Azure Site Recovery hello в переменной hello $Servers массива.</span><span class="sxs-lookup"><span data-stu-id="87200-203">hello command stores hello Microsoft Azure Site Recovery servers in hello $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="87200-204">Hello ниже команды получить hello сети восстановления сайта для hello исходный сервер VMM и hello целевой сервер VMM.</span><span class="sxs-lookup"><span data-stu-id="87200-204">hello below commands get hello site recovery network for hello source VMM server and hello target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="87200-205">Hello исходный сервер VMM может hello первый или hello второй массив серверов один в hello.</span><span class="sxs-lookup"><span data-stu-id="87200-205">hello source VMM server can be hello first one or hello second one in hello servers array.</span></span> <span data-ttu-id="87200-206">Проверьте имена hello серверов VMM hello и соответствующим образом получить hello сети</span><span class="sxs-lookup"><span data-stu-id="87200-206">Check hello names of hello VMM servers and get hello networks appropriately</span></span>


1. <span data-ttu-id="87200-207">Hello окончательного создает сопоставление между hello основной сети и сети восстановления hello.</span><span class="sxs-lookup"><span data-stu-id="87200-207">hello final cmdlet creates a mapping between hello primary network and hello recovery network.</span></span> <span data-ttu-id="87200-208">командлет Hello указывает hello основной сети как первый элемент $PrimaryNetworks и hello сети восстановления как первый элемент $RecoveryNetworks hello hello.</span><span class="sxs-lookup"><span data-stu-id="87200-208">hello cmdlet specifies hello primary network as hello first element of $PrimaryNetworks and hello recovery network as hello first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="87200-209">Шаг 7. Настройка сопоставления хранилищ</span><span class="sxs-lookup"><span data-stu-id="87200-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="87200-210">Hello ниже команда получает список hello классификации хранилища в переменную $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="87200-210">hello below command gets hello list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="87200-211">Классификация источников hello в переменную $SourceClassificaion и целевой классификации в переменную $TargetClassification, получить Hello ниже команды.</span><span class="sxs-lookup"><span data-stu-id="87200-211">hello below commands get hello source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="87200-212">Hello исходных и целевых классификаций может быть любой элемент в массиве hello.</span><span class="sxs-lookup"><span data-stu-id="87200-212">hello source and target classifications can be any element in hello array.</span></span> <span data-ttu-id="87200-213">См. выходные данные toohello hello ниже индекс hello toofigure команды исходных и целевых классификаций $storageclassifications массива.</span><span class="sxs-lookup"><span data-stu-id="87200-213">Refer toohello output of hello below command toofigure hello index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="87200-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="87200-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="87200-215">Hello ниже командлет создает сопоставление между hello классификации источника и целевой классификацией hello.</span><span class="sxs-lookup"><span data-stu-id="87200-215">hello below cmdlet creates a mapping between hello source classification and hello target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="87200-216">Шаг 8. Включение защиты для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="87200-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="87200-217">После надлежащей настройки серверов hello, облаков и сетей, можно включить защиту для виртуальных машин в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="87200-217">After hello servers, clouds and networks are configured correctly, you can enable protection for virtual machines in hello cloud.</span></span>

1. <span data-ttu-id="87200-218">Защита tooenable выполнения hello следующая команда контейнера защиты tooget hello:</span><span class="sxs-lookup"><span data-stu-id="87200-218">tooenable protection, run hello following command tooget hello protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="87200-219">Получите сущность защиты hello (VM), выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="87200-219">Get hello protection entity (VM) by running hello following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="87200-220">Включите репликацию для виртуальной Машины hello, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="87200-220">Enable replication for hello VM by running hello following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="87200-221">Выполните тестирование развертывания</span><span class="sxs-lookup"><span data-stu-id="87200-221">Test your deployment</span></span>
<span data-ttu-id="87200-222">Планирование развертывания можно запустить тестовую отработку отказа для одной виртуальной машины или создайте план восстановления, состоящий из нескольких виртуальных машин и запустите тестовую отработку отказа для hello tootest.</span><span class="sxs-lookup"><span data-stu-id="87200-222">tootest your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for hello plan.</span></span> <span data-ttu-id="87200-223">Тестовая обработка отказа имитирует механизм отработки отказа и восстановления в изолированной сети.</span><span class="sxs-lookup"><span data-stu-id="87200-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="87200-224">Можно создать план восстановления для приложения на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="87200-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="87200-225">toocheck hello завершения операции hello, следуйте указаниям hello [наблюдение за активностью](#monitor).</span><span class="sxs-lookup"><span data-stu-id="87200-225">toocheck hello completion of hello operation, follow hello steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="87200-226">Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="87200-226">Run a test failover</span></span>
1. <span data-ttu-id="87200-227">Запустите hello ниже командлеты tooget hello ВМ сети toowhich требуется tootest отработки отказа виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="87200-227">Run hello below cmdlets tooget hello VM network toowhich you want tootest failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="87200-228">Выполните тестовую отработку отказа виртуальной машины, выполнив следующие hello.</span><span class="sxs-lookup"><span data-stu-id="87200-228">Perform a test failover of a VM by doing hello following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="87200-229">Выполните тестовую отработку отказа плана восстановления, выполнив следующие hello.</span><span class="sxs-lookup"><span data-stu-id="87200-229">Perform a test failover of a recovery plan by doing hello following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="87200-230">Запуск запланированной отработки отказа</span><span class="sxs-lookup"><span data-stu-id="87200-230">Run a planned failover</span></span>
1. <span data-ttu-id="87200-231">Выполните Плановую отработку отказа виртуальной машины, выполнив следующие hello.</span><span class="sxs-lookup"><span data-stu-id="87200-231">Perform a planned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="87200-232">Выполните Плановую отработку отказа плана восстановления, выполнив следующие hello.</span><span class="sxs-lookup"><span data-stu-id="87200-232">Perform a planned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="87200-233">Запуск незапланированной отработки отказа</span><span class="sxs-lookup"><span data-stu-id="87200-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="87200-234">Выполните незапланированную отработку отказа виртуальной Машины, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="87200-234">Perform an unplanned failover of a VM by doing hello following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="87200-235">2. выполните незапланированной отработки отказа плана восстановления, выполнив следующие hello.</span><span class="sxs-lookup"><span data-stu-id="87200-235">2.Perform an unplanned failover of a recovery plan by doing hello following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="87200-236"><a name=monitor></a> Мониторинг активности</span><span class="sxs-lookup"><span data-stu-id="87200-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="87200-237">Используйте следующие команды toomonitor hello действие hello.</span><span class="sxs-lookup"><span data-stu-id="87200-237">Use hello following commands toomonitor hello activity.</span></span> <span data-ttu-id="87200-238">Обратите внимание, что на toowait между задания для обработки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="87200-238">Note that you have toowait in between jobs for hello processing toofinish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="87200-239">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="87200-239">Next steps</span></span>
<span data-ttu-id="87200-240">[Узнайте больше](/powershell/module/azurerm.recoveryservices.backup/#recovery) об использовании командлетов PowerShell инструмента Azure Resource Manager для службы Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="87200-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
