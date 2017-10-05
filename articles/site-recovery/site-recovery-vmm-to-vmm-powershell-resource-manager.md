---
title: "Репликация виртуальных машин Hyper-V из VMM на вторичный сайт с помощью PowerShell (Azure Resource Manager) | Документация Майкрософт"
description: "Описывается, как развернуть Azure Site Recovery, чтобы управлять репликацией, отработкой отказа и восстановлением виртуальных машин Hyper-V в облаках VMM на вторичный сайт VMM с помощью PowerShell (Resource Manager)."
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
ms.openlocfilehash: 5a6e00877b0a2b139d5322f610c1901ad76a710f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-to-a-secondary-vmm-site-using-powershell-resource-manager"></a><span data-ttu-id="eedf4-103">Репликация виртуальных машин Hyper-V из облаков VMM на вторичный сайт VMM с помощью PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="eedf4-103">Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eedf4-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="eedf4-104">Azure Portal</span></span>](site-recovery-vmm-to-vmm.md)
> * [<span data-ttu-id="eedf4-105">Классический портал</span><span class="sxs-lookup"><span data-stu-id="eedf4-105">Classic Portal</span></span>](site-recovery-vmm-to-vmm-classic.md)
> * [<span data-ttu-id="eedf4-106">PowerShell — Resource Manager</span><span class="sxs-lookup"><span data-stu-id="eedf4-106">PowerShell - Resource Manager</span></span>](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

<span data-ttu-id="eedf4-107">Вас приветствует служба Azure Site Recovery!</span><span class="sxs-lookup"><span data-stu-id="eedf4-107">Welcome to Azure Site Recovery!</span></span> <span data-ttu-id="eedf4-108">Эта статья поможет вам выполнить репликацию локальных виртуальных машин Hyper-V, управляемых в облаках System Center Virtual Machine Manager (VMM), на дополнительный сайт.</span><span class="sxs-lookup"><span data-stu-id="eedf4-108">Use this article if you want to replicate on-premises Hyper-V  virtual machines managed in System Center Virtual Machine Manager (VMM) clouds to a secondary site.</span></span>

<span data-ttu-id="eedf4-109">В этой статье показано, как использовать PowerShell для автоматизации распространенных задач, которые необходимо выполнять при настройке Azure Site Recovery для репликации виртуальных машин Hyper-V из облаков VMM System Center в облака VMM System Center на вторичном сайте.</span><span class="sxs-lookup"><span data-stu-id="eedf4-109">This article shows you how to use PowerShell to automate common tasks you need to perform when you set up Azure Site Recovery to replicate Hyper-V virtual machines in System Center VMM clouds to System Center VMM clouds in secondary site.</span></span>

<span data-ttu-id="eedf4-110">В этой статье рассматриваются необходимые условия для реализации сценария, а также описываются следующие действия.</span><span class="sxs-lookup"><span data-stu-id="eedf4-110">The article includes prerequisites for the scenario, and shows you</span></span>

* <span data-ttu-id="eedf4-111">Настройка хранилища служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="eedf4-111">How to set up a Recovery Services Vault</span></span>
* <span data-ttu-id="eedf4-112">Установка на исходном и целевом серверах VMM поставщика Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="eedf4-112">Install the Azure Site Recovery Provider on the source VMM server and the target VMM server</span></span>
* <span data-ttu-id="eedf4-113">Регистрация серверов VMM в хранилище.</span><span class="sxs-lookup"><span data-stu-id="eedf4-113">Register the VMM server(s) in the vault</span></span>
* <span data-ttu-id="eedf4-114">Настройка политики репликации для облака VMM.</span><span class="sxs-lookup"><span data-stu-id="eedf4-114">Configure replication policy for the VMM Cloud.</span></span> <span data-ttu-id="eedf4-115">Параметры репликации в политике будут применены ко всем защищенным виртуальным машинам.</span><span class="sxs-lookup"><span data-stu-id="eedf4-115">The replication settings in the policy will be applied to all protected virtual machines</span></span>
* <span data-ttu-id="eedf4-116">Включение защиты виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="eedf4-116">Enable protection for the virtual machines.</span></span>
* <span data-ttu-id="eedf4-117">Тестирование отработки отказа виртуальных машин по отдельности или по плану восстановления, позволяющее убедиться в том, что все работает ожидаемым образом.</span><span class="sxs-lookup"><span data-stu-id="eedf4-117">Test the failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>
* <span data-ttu-id="eedf4-118">Выполнение плановой или внеплановой отработки отказа виртуальных машин по отдельности или по плану восстановления, позволяющее убедиться в том, что все работает ожидаемым образом.</span><span class="sxs-lookup"><span data-stu-id="eedf4-118">Perform a planned or an unplanned failover of VMs individually or as part of a recovery plan to make sure everything is working as expected.</span></span>

<span data-ttu-id="eedf4-119">Если у вас возникают проблемы, опубликуйте свои вопросы на [форуме по Azure Recovery Services](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="eedf4-119">If you run into problems setting up this scenario, post your questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

> [!NOTE]
> <span data-ttu-id="eedf4-120">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Azure Resource Manager и классическая модель](../azure-resource-manager/resource-manager-deployment-model.md) .</span><span class="sxs-lookup"><span data-stu-id="eedf4-120">Azure has two different [deployment models](../azure-resource-manager/resource-manager-deployment-model.md) for creating and working with resources: Azure Resource Manager and classic.</span></span> <span data-ttu-id="eedf4-121">Кроме того, Azure предоставляет два портала — классический портал Azure, поддерживающий классическую модель развертывания, и портал Azure, поддерживающий обе модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="eedf4-121">Azure also has two portals – the Azure classic portal that supports the classic deployment model, and the Azure portal with support for both deployment models.</span></span> <span data-ttu-id="eedf4-122">В этой статье описывается модель развертывания с использованием менеджера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="eedf4-122">This article covers the Resource Manager deployment model.</span></span>
>
>

## <a name="on-premises-prerequisites"></a><span data-ttu-id="eedf4-123">Предварительные требования для локальной среды</span><span class="sxs-lookup"><span data-stu-id="eedf4-123">On-premises prerequisites</span></span>
<span data-ttu-id="eedf4-124">Вот что потребуется на первичных и вторичных локальных сайтах для развертывания этого сценария.</span><span class="sxs-lookup"><span data-stu-id="eedf4-124">Here's what you'll need in the primary and secondary on-premises sites to deploy this scenario:</span></span>

| <span data-ttu-id="eedf4-125">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="eedf4-125">**Prerequisites**</span></span> | <span data-ttu-id="eedf4-126">**Дополнительные сведения**</span><span class="sxs-lookup"><span data-stu-id="eedf4-126">**Details**</span></span> |
| --- | --- |
| <span data-ttu-id="eedf4-127">**VMM**</span><span class="sxs-lookup"><span data-stu-id="eedf4-127">**VMM**</span></span> |<span data-ttu-id="eedf4-128">Рекомендуется развернуть по серверу VMM на первичном и вторичном сайтах.</span><span class="sxs-lookup"><span data-stu-id="eedf4-128">We recommend you deploy a VMM server in the primary site and a VMM server in the secondary site.</span></span><br/><br/> <span data-ttu-id="eedf4-129">Вы можете также [выполнять репликацию между облаками на отдельном сервере VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span><span class="sxs-lookup"><span data-stu-id="eedf4-129">You can also [replicate between clouds on a single VMM server](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment).</span></span> <span data-ttu-id="eedf4-130">Для этого вам потребуется, чтобы на сервере VMM было настроено по крайней мере два облака.</span><span class="sxs-lookup"><span data-stu-id="eedf4-130">To do this you'll need at least two clouds configured on the VMM server.</span></span><br/><br/> <span data-ttu-id="eedf4-131">На серверах VMM должен выполняться как минимум System Center 2012 с пакетом обновления 1 (SP1) с последними обновлениями.</span><span class="sxs-lookup"><span data-stu-id="eedf4-131">VMM servers should be running at least System Center 2012 SP1 with the latest updates.</span></span><br/><br/> <span data-ttu-id="eedf4-132">Для каждого сервера VMM должно быть настроено одно или несколько облаков, и для каждого облака должен быть задан профиль загрузки Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="eedf4-132">Each VMM server must have at one or more clouds configured and all clouds must have the Hyper-V Capacity profile set.</span></span> <br/><br/><span data-ttu-id="eedf4-133">Облака должны содержать одну или несколько групп узлов VMM.</span><span class="sxs-lookup"><span data-stu-id="eedf4-133">Clouds must contain one or more VMM host groups.</span></span><br/><br/><span data-ttu-id="eedf4-134">Дополнительные сведения о настройке облаков VMM см. в разделах [Настройка структуры облака VMM](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric) и [Пошаговое руководство. Создание частных облаков с помощью VMM в System Center 2012 с пакетом обновления 1](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span><span class="sxs-lookup"><span data-stu-id="eedf4-134">Learn more about setting up VMM clouds in [Configuring the VMM cloud fabric](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric), and [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx).</span></span><br/><br/> <span data-ttu-id="eedf4-135">Серверы VMM должны иметь доступ к Интернету.</span><span class="sxs-lookup"><span data-stu-id="eedf4-135">VMM servers should have internet access.</span></span> |
| <span data-ttu-id="eedf4-136">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="eedf4-136">**Hyper-V**</span></span> |<span data-ttu-id="eedf4-137">Серверы Hyper-V должны работать под управлением Windows Server 2012 (или более поздних версий) с ролью Hyper-V и установленными последними обновлениями.</span><span class="sxs-lookup"><span data-stu-id="eedf4-137">Hyper-V servers must be running at least Windows Server 2012 with the Hyper-V role and have the latest updates installed.</span></span><br/><br/> <span data-ttu-id="eedf4-138">Сервер Hyper-V должен содержать одну или несколько виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="eedf4-138">A Hyper-V server should contain one or more VMs.</span></span><br/><br/>  <span data-ttu-id="eedf4-139">Серверы узлов Hyper-V должны быть размещены в первичном и вторичном облаках VMM.</span><span class="sxs-lookup"><span data-stu-id="eedf4-139">Hyper-V host servers should be located in host groups in the primary and secondary VMM clouds.</span></span><br/><br/> <span data-ttu-id="eedf4-140">Если вы используете Hyper-V в кластере на платформе Windows Server 2012 R2, то необходимо установить [обновление 2961977](https://support.microsoft.com/kb/2961977).</span><span class="sxs-lookup"><span data-stu-id="eedf4-140">If you're running Hyper-V in a cluster on Windows Server 2012 R2 you should install [update 2961977](https://support.microsoft.com/kb/2961977)</span></span><br/><br/> <span data-ttu-id="eedf4-141">Если вы используете Hyper-V в кластере на платформе Windows Server 2012, то учтите, что брокер кластера не создается автоматически при использовании кластера на основе статических IP-адресов.</span><span class="sxs-lookup"><span data-stu-id="eedf4-141">If you're running Hyper-V in a cluster on Windows Server 2012 note that cluster broker isn't created automatically if you have a static IP address-based cluster.</span></span> <span data-ttu-id="eedf4-142">Вам потребуется настроить брокер кластера вручную.</span><span class="sxs-lookup"><span data-stu-id="eedf4-142">You'll need to configure the cluster broker manually.</span></span> <span data-ttu-id="eedf4-143">[Подробная информация](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span><span class="sxs-lookup"><span data-stu-id="eedf4-143">[Read more](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).</span></span> |
| <span data-ttu-id="eedf4-144">**Поставщик**</span><span class="sxs-lookup"><span data-stu-id="eedf4-144">**Provider**</span></span> |<span data-ttu-id="eedf4-145">Во время развертывания службы Site Recovery установите на серверы VMM поставщик Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="eedf4-145">During Site Recovery deployment you install the Azure Site Recovery Provider on VMM servers.</span></span> <span data-ttu-id="eedf4-146">Поставщик обменивается данными со службой Site Recovery через порт HTTPS 443 для управления репликацией.</span><span class="sxs-lookup"><span data-stu-id="eedf4-146">The Provider communicates with Site Recovery over HTTPS 443 to orchestrate replication.</span></span> <span data-ttu-id="eedf4-147">Репликация данных осуществляется между сервером-источником и сервером-приемником Hyper-V через локальную сеть или VPN-подключение.</span><span class="sxs-lookup"><span data-stu-id="eedf4-147">Data replication occurs between the primary and secondary Hyper-V servers over the LAN or a VPN connection.</span></span><br/><br/> <span data-ttu-id="eedf4-148">Поставщику, запущенному на сервере VMM, нужен доступ к следующим URL-адресам: *.hypervrecoverymanager.windowsazure.com, *.accesscontrol.windows.net, *.backup.windowsazure.com, *.blob.core.windows.net, *.store.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="eedf4-148">The Provider running on the VMM server needs access to these URLs: *.hypervrecoverymanager.windowsazure.com; *.accesscontrol.windows.net; *.backup.windowsazure.com; *.blob.core.windows.net; *.store.core.windows.net.</span></span><br/><br/> <span data-ttu-id="eedf4-149">Кроме того, разрешите в брандмауэре обмен данными между серверами VMM и [диапазонами IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) , а также разрешите использовать протокол HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="eedf4-149">In addition allow firewall communication from the VMM servers to the [Azure datacenter IP ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653) and allow the HTTPS (443) protocol.</span></span> |

### <a name="network-mapping-prerequisites"></a><span data-ttu-id="eedf4-150">Предварительные требования сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="eedf4-150">Network mapping prerequisites</span></span>
<span data-ttu-id="eedf4-151">При сетевом сопоставлении сопоставляются сети виртуальных машин VMM первичного и вторичного серверов VMM. Вот для чего это делается:</span><span class="sxs-lookup"><span data-stu-id="eedf4-151">Network mapping maps between VMM VM networks on the primary and secondary VMM servers to:</span></span>

* <span data-ttu-id="eedf4-152">Оптимальное размещение виртуальных машин реплик на вторичных узлах Hyper-V после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="eedf4-152">Optimally place replica VMs on secondary Hyper-V hosts after failover.</span></span>
* <span data-ttu-id="eedf4-153">Подключение виртуальных машин реплик к соответствующим сетям виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="eedf4-153">Connect replica VMs to appropriate VM networks.</span></span>
* <span data-ttu-id="eedf4-154">Если не настроить сетевое сопоставление, виртуальные машины реплик не будут подключены к каким-либо сетям после отработки отказа.</span><span class="sxs-lookup"><span data-stu-id="eedf4-154">If you don't configure network mapping replica VMs won't be connected to any network after failover.</span></span>
* <span data-ttu-id="eedf4-155">Вот что понадобится, если вы хотите настроить сетевое сопоставление во время развертывания службы Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="eedf4-155">If you want to set up network mapping during Site Recovery deployment here's what you'll need:</span></span>

  * <span data-ttu-id="eedf4-156">Виртуальные машины на сервере узла Hyper-V должны быть подключены к сети виртуальных машин VMM.</span><span class="sxs-lookup"><span data-stu-id="eedf4-156">Make sure that VMs on the source Hyper-V host server are connected to a VMM VM network.</span></span> <span data-ttu-id="eedf4-157">Эта сеть должна быть подключена к логической сети, которая связана с облаком.</span><span class="sxs-lookup"><span data-stu-id="eedf4-157">That network should be linked to a logical network that is associated with the cloud.</span></span>
  * <span data-ttu-id="eedf4-158">Проверьте, настроена соответствующая сеть виртуальной машины для вторичного облака, которое будет использоваться для восстановления.</span><span class="sxs-lookup"><span data-stu-id="eedf4-158">Verify that the secondary cloud that you'll use for recovery has a corresponding VM network configured.</span></span> <span data-ttu-id="eedf4-159">Эта сеть виртуальной машины должна быть связана с логической сетью, которая связана с вторичным облаком.</span><span class="sxs-lookup"><span data-stu-id="eedf4-159">That VM network should be linked to a logical network that's associated with the secondary cloud.</span></span>

<span data-ttu-id="eedf4-160">Узнайте больше о настройке сетей VMM в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="eedf4-160">Learn more about configuring VMM networks in the below articles</span></span>

* [<span data-ttu-id="eedf4-161">Настройка логических сетей в VMM</span><span class="sxs-lookup"><span data-stu-id="eedf4-161">How to configure logical networks in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386307)
* [<span data-ttu-id="eedf4-162">Настройка сетей виртуальных машин и шлюзов в VMM</span><span class="sxs-lookup"><span data-stu-id="eedf4-162">How to configure VM networks and gateways in VMM</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=386308)

<span data-ttu-id="eedf4-163">[Узнайте больше](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) о принципе действия сетевого сопоставления.</span><span class="sxs-lookup"><span data-stu-id="eedf4-163">[Learn more](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) about how network mapping works.</span></span>

### <a name="powershell-prerequisites"></a><span data-ttu-id="eedf4-164">Необходимые компоненты PowerShell</span><span class="sxs-lookup"><span data-stu-id="eedf4-164">PowerShell prerequisites</span></span>
<span data-ttu-id="eedf4-165">Перед началом работы убедитесь, что среда Azure PowerShell готова к работе.</span><span class="sxs-lookup"><span data-stu-id="eedf4-165">Make sure you have Azure PowerShell ready to go.</span></span> <span data-ttu-id="eedf4-166">Если вы уже используете PowerShell, необходимо выполнить обновление до версии 0.8.10 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="eedf4-166">If you are already using PowerShell, you'll need to upgrade to version 0.8.10 or later.</span></span> <span data-ttu-id="eedf4-167">Дополнительные сведения о настройке PowerShell см. в статье [Установка и настройка Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="eedf4-167">For information about setting up PowerShell, see the [Guide to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="eedf4-168">После установки и настройки PowerShell все доступные командлеты для службы можно просмотреть [здесь](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eedf4-168">Once you have set up and configured PowerShell, you can view all of the available cmdlets for the service [here](/powershell/azure/overview).</span></span>

<span data-ttu-id="eedf4-169">Дополнительные сведения об использовании командлетов, например о типовой обработке значений параметров, входных и выходных параметров в Azure PowerShell, приведены в статье [Начало работы с командлетами Azure](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="eedf4-169">To learn about tips that can help you use the cmdlets, such as how parameter values, inputs, and outputs are typically handled in Azure PowerShell, see the [Guide to get Started with Azure Cmdlets](/powershell/azure/get-started-azureps).</span></span>

## <a name="step-1-set-the-subscription"></a><span data-ttu-id="eedf4-170">Шаг 1. Настройка подписки</span><span class="sxs-lookup"><span data-stu-id="eedf4-170">Step 1: Set the subscription</span></span>
1. <span data-ttu-id="eedf4-171">В Azure Powershell войдите в свою учетную запись Azure с помощью следующих командлетов:</span><span class="sxs-lookup"><span data-stu-id="eedf4-171">From Azure powershell, login to your Azure account: using the following cmdlets</span></span>

        $UserName = "<user@live.com>"
        $Password = "<password>"
        $SecurePassword = ConvertTo-SecureString -AsPlainText $Password -Force
        $Cred = New-Object System.Management.Automation.PSCredential -ArgumentList $UserName, $SecurePassword
        Login-AzureRmAccount #-Credential $Cred
2. <span data-ttu-id="eedf4-172">Получите список своих подписок.</span><span class="sxs-lookup"><span data-stu-id="eedf4-172">Get a list of your subscriptions.</span></span> <span data-ttu-id="eedf4-173">При этом также отобразится список идентификаторов subscriptionID для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="eedf4-173">This will also list the subscriptionIDs for each of the subscriptions.</span></span> <span data-ttu-id="eedf4-174">Запишите идентификатор subscriptionID подписки, в которой хотите создать хранилище служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="eedf4-174">Note down the subscriptionID of the subscription in which you wish to create the recovery services vault</span></span>    

        Get-AzureRmSubscription
3. <span data-ttu-id="eedf4-175">Задайте подписку, в которой будет создано хранилище служб восстановления, указав идентификатор подписки.</span><span class="sxs-lookup"><span data-stu-id="eedf4-175">Set the subscription in which the recovery services vault is to be created by mentioning the subscription ID</span></span>

        Set-AzureRmContext –SubscriptionID <subscriptionId>

## <a name="step-2-create-a-recovery-services-vault"></a><span data-ttu-id="eedf4-176">Шаг 2. Создание хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="eedf4-176">Step 2: Create a Recovery Services vault</span></span>
1. <span data-ttu-id="eedf4-177">Если у вас еще нет группы ресурсов Azure Resource Manager, создайте ее.</span><span class="sxs-lookup"><span data-stu-id="eedf4-177">Create an Azure Resource Manager resource group if you don't have one already</span></span>

        New-AzureRmResourceGroup -Name #ResourceGroupName -Location #location
2. <span data-ttu-id="eedf4-178">Создайте новое хранилище служб восстановления и сохраните созданный объект хранилища ASR в переменной, которая будет использоваться далее.</span><span class="sxs-lookup"><span data-stu-id="eedf4-178">Create a new Recovery Services vault and save the created ASR vault object in a variable (will be used later).</span></span> <span data-ttu-id="eedf4-179">Объект хранилища ASR также можно получить после создания с помощью командлета Get-AzureRMRecoveryServicesVault:-</span><span class="sxs-lookup"><span data-stu-id="eedf4-179">You can also retrieve the ASR vault object post creation using the Get-AzureRMRecoveryServicesVault cmdlet:-</span></span>

        $vault = New-AzureRmRecoveryServicesVault -Name #vaultname -ResouceGroupName #ResourceGroupName -Location #location

## <a name="step-3-set-the-recovery-services-vault-context"></a><span data-ttu-id="eedf4-180">Шаг 3. Настройка контекста для хранилища служб восстановления</span><span class="sxs-lookup"><span data-stu-id="eedf4-180">Step 3: Set the Recovery Services Vault context</span></span>
1. <span data-ttu-id="eedf4-181">Если хранилище уже создано, выполните следующую команду, чтобы получить его.</span><span class="sxs-lookup"><span data-stu-id="eedf4-181">If you have a vault already created, run the below command to get the vault.</span></span>

       $vault = Get-AzureRmRecoveryServicesVault -Name #vaultname
2. <span data-ttu-id="eedf4-182">Задайте контекст хранилища, выполнив указанную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="eedf4-182">Set the vault context by running the below command.</span></span>

       Set-AzureRmSiteRecoveryVaultSettings -ARSVault $vault

## <a name="step-4-install-the-azure-site-recovery-provider"></a><span data-ttu-id="eedf4-183">Шаг 4. Установка поставщика Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="eedf4-183">Step 4: Install the Azure Site Recovery Provider</span></span>
1. <span data-ttu-id="eedf4-184">На компьютере с VMM создайте каталог, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eedf4-184">On the VMM machine, create a directory by running the following command:</span></span>

       New-Item c:\ASR -type directory
2. <span data-ttu-id="eedf4-185">Распакуйте файлы с помощью загруженного поставщика, выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eedf4-185">Extract the files using the downloaded provider by running the following command</span></span>

       pushd C:\ASR\
       .\AzureSiteRecoveryProvider.exe /x:. /q
3. <span data-ttu-id="eedf4-186">Используйте следующую команду для установки провайдера:</span><span class="sxs-lookup"><span data-stu-id="eedf4-186">Install the provider using the following commands:</span></span>

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

   <span data-ttu-id="eedf4-187">Дождитесь завершения процесса установки.</span><span class="sxs-lookup"><span data-stu-id="eedf4-187">Wait for the installation to finish.</span></span>
4. <span data-ttu-id="eedf4-188">Зарегистрируйте сервер в хранилище, используя следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eedf4-188">Register the server in the vault using the following command:</span></span>

       $BinPath = $env:SystemDrive+"\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin"
       pushd $BinPath
       $encryptionFilePath = "C:\temp\".\DRConfigurator.exe /r /Credentials $VaultSettingFilePath /vmmfriendlyname $env:COMPUTERNAME /dataencryptionenabled $encryptionFilePath /startvmmservice

## <a name="step-5-create-and-associate-a-replication-policy"></a><span data-ttu-id="eedf4-189">Шаг 5. Создание и связывание политики репликации</span><span class="sxs-lookup"><span data-stu-id="eedf4-189">Step 5: Create and associate a replication policy</span></span>
1. <span data-ttu-id="eedf4-190">Создайте политику репликации Hyper-V 2012 R2, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="eedf4-190">Create a Hyper-V 2012 R2 replication policy by running the following command:</span></span>

        $ReplicationFrequencyInSeconds = "300";        #options are 30,300,900
        $PolicyName = “replicapolicy”
        $RepProvider = HyperVReplica2012R2
        $Recoverypoints = 24                    #specify the number of hours to retain recovery pints
        $AppConsistentSnapshotFrequency = 4 #specify the frequency (in hours) at which app consistent snapshots are taken
        $AuthMode = "Kerberos"  #options are "Kerberos" or "Certificate"
        $AuthPort = "8083"  #specify the port number that will be used for replication traffic on Hyper-V hosts
        $InitialRepMethod = "Online" #options are "Online" or "Offline"

        $policyresult = New-AzureRmSiteRecoveryPolicy -Name $policyname -ReplicationProvider $RepProvider -ReplicationFrequencyInSeconds $Replicationfrequencyinseconds -RecoveryPoints $recoverypoints -ApplicationConsistentSnapshotFrequencyInHours $AppConsistentSnapshotFrequency -Authentication $AuthMode -ReplicationPort $AuthPort -ReplicationMethod $InitialRepMethod

    > [!NOTE]
    > <span data-ttu-id="eedf4-191">Облако VMM может содержать узлы Hyper-V под управлением разных версий Windows Server (как уже упоминалось в предварительных требованиях к Hyper-V), но политика репликации зависит от версии ОС.</span><span class="sxs-lookup"><span data-stu-id="eedf4-191">The VMM cloud can contain Hyper-V hosts running different versions of Windows Server (as mentioned in the Hyper-V prerequisites), but the replication policy is OS version specific.</span></span> <span data-ttu-id="eedf4-192">Если вы используете узлы с разными версиями операционных систем, то создайте отдельные политики репликации для каждого типа версии ОС.</span><span class="sxs-lookup"><span data-stu-id="eedf4-192">If you have different hosts running on different operating system versions, then create separate replication policies for each type of OS version.</span></span> <span data-ttu-id="eedf4-193">Пример. Если у вас есть пять узлов с Windows Server 2012 и три с Windows Server 2012 R2, то создайте две политики репликации — по одной для каждого типа версии ОС.</span><span class="sxs-lookup"><span data-stu-id="eedf4-193">For eg: If you have five hosts running on Windows Servers 2012 and three on Windows Server 2012 R2, create two replication polices – one for each type of operating system versions.</span></span>

1. <span data-ttu-id="eedf4-194">Получите первичный контейнер защиты (основного облака VMM) и контейнер защиты для восстановления (облако VMM восстановления), выполнив следующие команды.</span><span class="sxs-lookup"><span data-stu-id="eedf4-194">Get the primary protection container (primary VMM Cloud) and recovery protection container (recovery VMM Cloud) by running the following commands:</span></span>

       $PrimaryCloud = "testprimarycloud"
       $primaryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloud;  

       $RecoveryCloud = "testrecoverycloud"
       $recoveryprotectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $RecoveryCloud;  
2. <span data-ttu-id="eedf4-195">Получите политику, созданную на шаге 1, указав ее понятное имя.</span><span class="sxs-lookup"><span data-stu-id="eedf4-195">Retrieve the policy you created in step 1 using the friendly name of the policy</span></span>

       $policy = Get-AzureRmSiteRecoveryPolicy -FriendlyName $policyname
3. <span data-ttu-id="eedf4-196">Запустите связывание контейнера защиты (облака VMM) с политикой репликации.</span><span class="sxs-lookup"><span data-stu-id="eedf4-196">Start the association of the protection container (VMM Cloud) with the replication policy:</span></span>

       $associationJob  = Start-AzureRmSiteRecoveryPolicyAssociationJob -Policy     $Policy -PrimaryProtectionContainer $primaryprotectionContainer -RecoveryProtectionContainer $recoveryprotectionContainer
4. <span data-ttu-id="eedf4-197">Дождитесь завершения задания связывания политики.</span><span class="sxs-lookup"><span data-stu-id="eedf4-197">Wait for the policy association job to complete.</span></span> <span data-ttu-id="eedf4-198">Проверить, завершено ли это задание, можно с помощью следующего фрагмента кода PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eedf4-198">You can check if the job has completed using the following PowerShell snippet.</span></span>

       $job = Get-AzureRmSiteRecoveryJob -Job $associationJob

       if($job -eq $null -or $job.StateDescription -ne "Completed")
       {
         $isJobLeftForProcessing = $true;
       }

   <span data-ttu-id="eedf4-199">После завершения обработки задания выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eedf4-199">After the job has finished processing, run the following command:</span></span>

       if($isJobLeftForProcessing)
       {
         Start-Sleep -Seconds 60
       }
       }While($isJobLeftForProcessing)

<span data-ttu-id="eedf4-200">Для проверки выполнения операции выполните действия, описанные в разделе [Мониторинг активности](#monitor).</span><span class="sxs-lookup"><span data-stu-id="eedf4-200">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

## <a name="step-6-configure-network-mapping"></a><span data-ttu-id="eedf4-201">Шаг 6. Настройка сетевого сопоставления</span><span class="sxs-lookup"><span data-stu-id="eedf4-201">Step 6: Configure network mapping</span></span>
1. <span data-ttu-id="eedf4-202">Первая команда возвращает серверы для текущего хранилища Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="eedf4-202">The first command gets servers for the current Azure Site Recovery vault.</span></span> <span data-ttu-id="eedf4-203">Команда сохраняет серверы Microsoft Azure Site Recovery в массиве $Servers.</span><span class="sxs-lookup"><span data-stu-id="eedf4-203">The command stores the Microsoft Azure Site Recovery servers in the $Servers array variable.</span></span>

        $Servers = Get-AzureRmSiteRecoveryServer
2. <span data-ttu-id="eedf4-204">Приведенные ниже команды получают сеть Site Recovery для исходного и целевого серверов VMM.</span><span class="sxs-lookup"><span data-stu-id="eedf4-204">The below commands get the site recovery network for the source VMM server and the target VMM server.</span></span>

        $PrimaryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[0]        

        $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]

    > [!NOTE]
    > <span data-ttu-id="eedf4-205">Исходный сервер VMM может быть первым или вторым в массиве серверов.</span><span class="sxs-lookup"><span data-stu-id="eedf4-205">The source VMM server can be the first one or the second one in the servers array.</span></span> <span data-ttu-id="eedf4-206">Проверьте имена серверов VMM и получите соответствующие сети.</span><span class="sxs-lookup"><span data-stu-id="eedf4-206">Check the names of the VMM servers and get the networks appropriately</span></span>


1. <span data-ttu-id="eedf4-207">Последний командлет создает сопоставление между основной сетью и сетью восстановления.</span><span class="sxs-lookup"><span data-stu-id="eedf4-207">The final cmdlet creates a mapping between the primary network and the recovery network.</span></span> <span data-ttu-id="eedf4-208">Этот командлет указывает основную сеть в качестве первого элемента $PrimaryNetworks, а сеть восстановления — в качестве первого элемента $RecoveryNetworks.</span><span class="sxs-lookup"><span data-stu-id="eedf4-208">The cmdlet specifies the primary network as the first element of $PrimaryNetworks and the recovery network as the first element of $RecoveryNetworks.</span></span>

        New-AzureRmSiteRecoveryNetworkMapping -PrimaryNetwork $PrimaryNetworks[0] -RecoveryNetwork $RecoveryNetworks[0]

## <a name="step-7-configure-storage-mapping"></a><span data-ttu-id="eedf4-209">Шаг 7. Настройка сопоставления хранилищ</span><span class="sxs-lookup"><span data-stu-id="eedf4-209">Step 7: Configure storage mapping</span></span>
1. <span data-ttu-id="eedf4-210">Приведенная ниже команда получает список классификаций хранилищ в переменную $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="eedf4-210">The below command gets the list of storage classifications into $storageclassifications variable.</span></span>

        $storageclassifications = Get-AzureRmSiteRecoveryStorageClassification
2. <span data-ttu-id="eedf4-211">Следующие команды получают классификацию источников в переменную $SourceClassification, а классификацию целей — в переменную $TargetClassification.</span><span class="sxs-lookup"><span data-stu-id="eedf4-211">The below commands get the source classification into $SourceClassificaion variable and target classification into $TargetClassification variable.</span></span>

        $SourceClassificaion = $storageclassifications[0]

        $TargetClassification = $storageclassifications[1]

    > [!NOTE]
    > <span data-ttu-id="eedf4-212">Классификации источников и целей могут быть любым элементом в массиве.</span><span class="sxs-lookup"><span data-stu-id="eedf4-212">The source and target classifications can be any element in the array.</span></span> <span data-ttu-id="eedf4-213">Обратитесь к выходным данным приведенной ниже команды, чтобы определить индекс классификаций источников и целей в массиве $storageclassifications.</span><span class="sxs-lookup"><span data-stu-id="eedf4-213">Refer to the output of the below command to figure the index of source and target classifications in $storageclassifications array.</span></span>

    > <span data-ttu-id="eedf4-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span><span class="sxs-lookup"><span data-stu-id="eedf4-214">Get-AzureRmSiteRecoveryStorageClassification | Select-Object -Property FriendlyName, Id | Format-Table</span></span>


1. <span data-ttu-id="eedf4-215">Приведенный ниже командлет создает сопоставление между классификациями источников и целей.</span><span class="sxs-lookup"><span data-stu-id="eedf4-215">The below cmdlet creates a mapping between the source classification and the target classification.</span></span>

        New-AzureRmSiteRecoveryStorageClassificationMapping -PrimaryStorageClassification $SourceClassificaion -RecoveryStorageClassification $TargetClassification

## <a name="step-8-enable-protection-for-virtual-machines"></a><span data-ttu-id="eedf4-216">Шаг 8. Включение защиты для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="eedf4-216">Step 8: Enable protection for virtual machines</span></span>
<span data-ttu-id="eedf4-217">После успешной настройки серверов, облаков и сетей можно включить защиту для виртуальных машин в облаке.</span><span class="sxs-lookup"><span data-stu-id="eedf4-217">After the servers, clouds and networks are configured correctly, you can enable protection for virtual machines in the cloud.</span></span>

1. <span data-ttu-id="eedf4-218">Чтобы включить защиту, выполните следующую команду для получения контейнера защиты:</span><span class="sxs-lookup"><span data-stu-id="eedf4-218">To enable protection, run the following command to get the protection container:</span></span>

          $PrimaryProtectionContainer = Get-AzureRmSiteRecoveryProtectionContainer -friendlyName $PrimaryCloudName
2. <span data-ttu-id="eedf4-219">Получите объект защиты (виртуальную машину), выполнив следующую команду:</span><span class="sxs-lookup"><span data-stu-id="eedf4-219">Get the protection entity (VM) by running the following command:</span></span>

           $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -friendlyName $VMName -ProtectionContainer $PrimaryProtectionContainer
3. <span data-ttu-id="eedf4-220">Включите репликацию для виртуальной машины, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="eedf4-220">Enable replication for the VM by running the following command:</span></span>

          $jobResult = Set-AzureRmSiteRecoveryProtectionEntity -ProtectionEntity $protectionentity -Protection Enable -Policy $policy

## <a name="test-your-deployment"></a><span data-ttu-id="eedf4-221">Выполните тестирование развертывания</span><span class="sxs-lookup"><span data-stu-id="eedf4-221">Test your deployment</span></span>
<span data-ttu-id="eedf4-222">Чтобы протестировать развертывание, можно запустить тестовую отработку отказа для отдельной виртуальной машины или создать план восстановления, состоящий из нескольких виртуальных машин, и запустить тестовую отработку отказа плана.</span><span class="sxs-lookup"><span data-stu-id="eedf4-222">To test your deployment you can run a test failover for a single virtual machine, or create a recovery plan consisting of multiple virtual machines and run a test failover for the plan.</span></span> <span data-ttu-id="eedf4-223">Тестовая обработка отказа имитирует механизм отработки отказа и восстановления в изолированной сети.</span><span class="sxs-lookup"><span data-stu-id="eedf4-223">Test failover simulates your failover and recovery mechanism in an isolated network.</span></span>

> [!NOTE]
> <span data-ttu-id="eedf4-224">Можно создать план восстановления для приложения на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="eedf4-224">You can create a recovery plan for your application in Azure portal.</span></span>
>
>

<span data-ttu-id="eedf4-225">Для проверки выполнения операции выполните действия, описанные в разделе [Мониторинг активности](#monitor).</span><span class="sxs-lookup"><span data-stu-id="eedf4-225">To check the completion of the operation, follow the steps in [Monitor Activity](#monitor).</span></span>

### <a name="run-a-test-failover"></a><span data-ttu-id="eedf4-226">Запуск тестовой отработки отказа</span><span class="sxs-lookup"><span data-stu-id="eedf4-226">Run a test failover</span></span>
1. <span data-ttu-id="eedf4-227">Выполните приведенные ниже командлеты, чтобы получить сеть виртуальных машин, отработку отказа виртуальных машин в которую вы хотите проверить.</span><span class="sxs-lookup"><span data-stu-id="eedf4-227">Run the below cmdlets to get the VM network to which you want to test failover your VMs to.</span></span>

       $Servers = Get-AzureRmSiteRecoveryServer
       $RecoveryNetworks = Get-AzureRmSiteRecoveryNetwork -Server $Servers[1]
2. <span data-ttu-id="eedf4-228">Выполните тестовую отработку отказа виртуальной машины следующим образом.</span><span class="sxs-lookup"><span data-stu-id="eedf4-228">Perform a test failover of a VM by doing the following:</span></span>

       $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -FriendlyName $VMName -ProtectionContainer $PrimaryprotectionContainer

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity -VMNetwork $RecoveryNetworks[1]
3. <span data-ttu-id="eedf4-229">Выполните тестовую отработку отказа по плану восстановления следующим образом.</span><span class="sxs-lookup"><span data-stu-id="eedf4-229">Perform a test failover of a recovery plan by doing the following:</span></span>

       $recoveryplanname = "test-recovery-plan"

       $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

       $jobIDResult =  Start-AzureRmSiteRecoveryTestFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan -VMNetwork $RecoveryNetworks[1]

### <a name="run-a-planned-failover"></a><span data-ttu-id="eedf4-230">Запуск запланированной отработки отказа</span><span class="sxs-lookup"><span data-stu-id="eedf4-230">Run a planned failover</span></span>
1. <span data-ttu-id="eedf4-231">Выполните плановую отработку отказа виртуальной машины следующим образом.</span><span class="sxs-lookup"><span data-stu-id="eedf4-231">Perform a planned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity
2. <span data-ttu-id="eedf4-232">Выполните плановую отработку отказа по плану восстановления следующим образом.</span><span class="sxs-lookup"><span data-stu-id="eedf4-232">Perform a planned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryPlannedFailoverJob -Direction PrimaryToRecovery -Recoveryplan $recoveryplan

### <a name="run-an-unplanned-failover"></a><span data-ttu-id="eedf4-233">Запуск незапланированной отработки отказа</span><span class="sxs-lookup"><span data-stu-id="eedf4-233">Run an unplanned failover</span></span>
1. <span data-ttu-id="eedf4-234">Выполните внеплановую отработку отказа виртуальной машины следующим образом.</span><span class="sxs-lookup"><span data-stu-id="eedf4-234">Perform an unplanned failover of a VM by doing the following:</span></span>

        $protectionEntity = Get-AzureRmSiteRecoveryProtectionEntity -Name $VMName -ProtectionContainer $PrimaryprotectionContainer

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

<span data-ttu-id="eedf4-235">2. Выполните внеплановую отработку отказа по плану восстановления следующим образом.</span><span class="sxs-lookup"><span data-stu-id="eedf4-235">2.Perform an unplanned failover of a recovery plan by doing the following:</span></span>

        $recoveryplanname = "test-recovery-plan"

        $recoveryplan = Get-AzureRmSiteRecoveryRecoveryPlan -FriendlyName $recoveryplanname

        $jobIDResult =  Start-AzureRmSiteRecoveryUnPlannedFailoverJob -Direction PrimaryToRecovery -ProtectionEntity $protectionEntity

## <span data-ttu-id="eedf4-236"><a name=monitor></a> Мониторинг активности</span><span class="sxs-lookup"><span data-stu-id="eedf4-236"><a name=monitor></a> Monitor Activity</span></span>
<span data-ttu-id="eedf4-237">Используйте следующие команды для мониторинга активности.</span><span class="sxs-lookup"><span data-stu-id="eedf4-237">Use the following commands to monitor the activity.</span></span> <span data-ttu-id="eedf4-238">Обратите внимание, что между обработкой заданий необходимы паузы для ожидания завершения обработки.</span><span class="sxs-lookup"><span data-stu-id="eedf4-238">Note that you have to wait in between jobs for the processing to finish.</span></span>

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



## <a name="next-steps"></a><span data-ttu-id="eedf4-239">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eedf4-239">Next steps</span></span>
<span data-ttu-id="eedf4-240">[Узнайте больше](/powershell/module/azurerm.recoveryservices.backup/#recovery) об использовании командлетов PowerShell инструмента Azure Resource Manager для службы Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="eedf4-240">[Read more](/powershell/module/azurerm.recoveryservices.backup/#recovery) about Azure Site Recovery with Azure Resource Manager PowerShell cmdlets.</span></span>
