---
title: "aaaLinux вычислений виртуальных машин в кластере HPC Pack | Документы Microsoft"
description: "Узнайте, как toocreate используйте HPC Pack кластер в Azure для Linux высокопроизводительных вычислительных систем (HPC) рабочих нагрузок"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 4d080fdd-5ffe-4f54-a78d-4c818f6eb3fb
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/12/2016
ms.author: danlep
ms.openlocfilehash: 9ed20d6cd69a6472a00666caf8965e9d022698a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-linux-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="538bf-103">Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure</span><span class="sxs-lookup"><span data-stu-id="538bf-103">Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="538bf-104">В этой статье описывается, как настроить в Azure [кластер пакета Microsoft HPC](https://technet.microsoft.com/library/cc514029.aspx), содержащий головной узел под управлением Windows Server и несколько вычислительных узлов под управлением поддерживаемого дистрибутива Linux.</span><span class="sxs-lookup"><span data-stu-id="538bf-104">Set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029.aspx) cluster in Azure that contains a head node running Windows Server and several compute nodes running a supported Linux distribution.</span></span> <span data-ttu-id="538bf-105">Просмотр данных toomove параметры среди узлов hello Linux и Windows hello головного узла кластера hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-105">Explore options toomove data among hello Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="538bf-106">Узнайте, как toosubmit Linux HPC заданий toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="538bf-106">Learn how toosubmit Linux HPC jobs toohello cluster.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="538bf-107">На высоком уровне hello следующей диаграмме показан кластер HPC Pack hello создания и работы с.</span><span class="sxs-lookup"><span data-stu-id="538bf-107">At a high level, hello following diagram shows hello HPC Pack cluster you create and work with.</span></span>

![Кластер пакета HPC с узлами Linux][scenario]

<span data-ttu-id="538bf-109">Для других параметров toorun Linux HPC рабочих нагрузок в Azure, в разделе [технические ресурсы для пакета и высокопроизводительных вычислительных систем](../../../batch/big-compute-resources.md).</span><span class="sxs-lookup"><span data-stu-id="538bf-109">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/big-compute-resources.md).</span></span>

## <a name="deploy-an-hpc-pack-cluster-with-linux-compute-nodes"></a><span data-ttu-id="538bf-110">Развертывание кластера пакета HPC с вычислительными узлами Linux</span><span class="sxs-lookup"><span data-stu-id="538bf-110">Deploy an HPC Pack cluster with Linux compute nodes</span></span>
<span data-ttu-id="538bf-111">В этой статье показано два варианта toodeploy кластере HPC Pack в Azure с Linux вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="538bf-111">This article shows you two options toodeploy an HPC Pack cluster in Azure with Linux compute nodes.</span></span> <span data-ttu-id="538bf-112">Оба метода используют образа Marketplace из Windows Server и головного узла HPC Pack toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-112">Both methods use a Marketplace image of Windows Server with HPC Pack toocreate hello head node.</span></span> 

* <span data-ttu-id="538bf-113">**Шаблон диспетчера ресурсов Azure** -использовать шаблон из hello Azure Marketplace или шаблон начало работы от сообщества hello, создания tooautomate hello кластера в модели развертывания диспетчера ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-113">**Azure Resource Manager template** - Use a template from hello Azure Marketplace, or a quickstart template from hello community, tooautomate creation of hello cluster in hello Resource Manager deployment model.</span></span> <span data-ttu-id="538bf-114">Здравствуйте, например, [кластера HPC Pack для рабочих нагрузок Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) шаблона в hello Azure Marketplace создается полная инфраструктура кластера HPC Pack для Linux HPC рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="538bf-114">For example, hello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace creates a complete HPC Pack cluster infrastructure for Linux HPC workloads.</span></span>
* <span data-ttu-id="538bf-115">**Сценарий PowerShell** -hello используйте [скрипт развертывания IaaS пакета Microsoft HPC](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate развертывания для завершения создания кластера в hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="538bf-115">**PowerShell script** - Use hello [Microsoft HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) (**New-HpcIaaSCluster.ps1**) tooautomate a complete cluster deployment in hello classic deployment model.</span></span> <span data-ttu-id="538bf-116">Этот скрипт Azure PowerShell использует образ виртуальной Машины HPC Pack в hello Azure Marketplace для быстрого развертывания и предоставляет широкий набор параметров toodeploy конфигурации вычислительные узлы Linux.</span><span class="sxs-lookup"><span data-stu-id="538bf-116">This Azure PowerShell script uses an HPC Pack VM image in hello Azure Marketplace for fast deployment and provides a comprehensive set of configuration parameters toodeploy Linux compute nodes.</span></span>

<span data-ttu-id="538bf-117">Дополнительные сведения о вариантах развертывания кластера HPC Pack в Azure см. в разделе [параметры toocreate и управлять кластером высокопроизводительных вычислительных систем (HPC) в Azure с пакетом Microsoft HPC](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="538bf-117">For more information about HPC Pack cluster deployment options in Azure, see [Options toocreate and manage a high-performance computing (HPC) cluster in Azure with Microsoft HPC Pack](../hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="538bf-118">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="538bf-118">Prerequisites</span></span>
* <span data-ttu-id="538bf-119">**Подписка Azure** -подписки можно использовать в любом hello Azure Global или Azure China.</span><span class="sxs-lookup"><span data-stu-id="538bf-119">**Azure subscription** - You can use a subscription in either hello Azure Global or Azure China service.</span></span> <span data-ttu-id="538bf-120">Если ее нет, можно создать [бесплатную учетную запись](https://azure.microsoft.com/pricing/free-trial/) всего за несколько минут.</span><span class="sxs-lookup"><span data-stu-id="538bf-120">If you don't have an account, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="538bf-121">**Квота ядер** -может потребоваться tooincrease hello квоту ядер, особенно в том случае, если выбрать toodeploy несколько узлов кластера с несколькими ядрами размеры виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="538bf-121">**Cores quota** - You might need tooincrease hello quota of cores, especially if you choose toodeploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="538bf-122">tooincrease квоту, откройте запрос поддержки сети клиента бесплатно.</span><span class="sxs-lookup"><span data-stu-id="538bf-122">tooincrease a quota, open an online customer support request at no charge.</span></span>
* <span data-ttu-id="538bf-123">**Дистрибутивы Linux** -в настоящее время HPC Pack поддерживает hello следующие дистрибутивы Linux для вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="538bf-123">**Linux distributions** - Currently HPC Pack supports hello following Linux distributions for compute nodes.</span></span> <span data-ttu-id="538bf-124">Можно использовать версии этих дистрибутивов, доступные в Marketplace, или создать собственные.</span><span class="sxs-lookup"><span data-stu-id="538bf-124">You can use Marketplace versions of these distributions where available, or supply your own.</span></span>
  
  * <span data-ttu-id="538bf-125">**Выпуски на основе CentOS**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span><span class="sxs-lookup"><span data-stu-id="538bf-125">**CentOS-based**: 6.5, 6.6, 6.7, 7.0, 7.1, 7.2, 6.5 HPC, 7.1 HPC</span></span>
  * <span data-ttu-id="538bf-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span><span class="sxs-lookup"><span data-stu-id="538bf-126">**Red Hat Enterprise Linux**: 6.7, 6.8, 7.2</span></span>
  * <span data-ttu-id="538bf-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 для HPC, SLES 12 для HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="538bf-127">**SUSE Linux Enterprise Server**: SLES 12, SLES 12 (Premium), SLES 12 SP1, SLES 12 SP1 (Premium), SLES 12 for HPC, SLES 12 for HPC (Premium)</span></span>
  * <span data-ttu-id="538bf-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="538bf-128">**Ubuntu Server**: 14.04 LTS, 16.04 LTS</span></span>
    
    > [!TIP]
    > <span data-ttu-id="538bf-129">сети Azure RDMA hello toouse с помощью одного из размеров виртуальных Машин hello функцией RDMA, укажите образ SUSE Linux Enterprise Server 12 HPC или на основе CentOS HPC из hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="538bf-129">toouse hello Azure RDMA network with one of hello RDMA-capable VM sizes, specify a SUSE Linux Enterprise Server 12 HPC or CentOS-based HPC image from hello Azure Marketplace.</span></span> <span data-ttu-id="538bf-130">Дополнительные сведения см. в статье [Размеры виртуальных машин Linux, оптимизированных для HPC](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="538bf-130">For more information, see [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

<span data-ttu-id="538bf-131">Предварительные условия toodeploy hello кластера с помощью скрипта развертывания IaaS пакета HPC hello:</span><span class="sxs-lookup"><span data-stu-id="538bf-131">Additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="538bf-132">**Клиентский компьютер** -необходим сценарий развертывания клиента на основе Windows компьютера toorun hello кластера.</span><span class="sxs-lookup"><span data-stu-id="538bf-132">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="538bf-133">**Azure PowerShell** - [установите и настройте Azure PowerShell](/powershell/azure/overview) (версии 0.8.10 или более поздней) на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="538bf-133">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="538bf-134">**Скрипт развертывания IaaS пакета HPC** — Загрузите и распакуйте hello последнюю версию скрипта hello из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="538bf-134">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="538bf-135">Проверьте версию hello hello сценария, введя `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="538bf-135">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="538bf-136">Эта статья основана на версии 4.4.1 или более поздней hello сценария.</span><span class="sxs-lookup"><span data-stu-id="538bf-136">This article is based on version 4.4.1 or later of hello script.</span></span>

### <a name="deployment-option-1-use-a-resource-manager-template"></a><span data-ttu-id="538bf-137">Вариант развертывания 1.</span><span class="sxs-lookup"><span data-stu-id="538bf-137">Deployment option 1.</span></span> <span data-ttu-id="538bf-138">Использование шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="538bf-138">Use a Resource Manager template</span></span>
1. <span data-ttu-id="538bf-139">Go toohello [кластера HPC Pack для рабочих нагрузок Linux](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) шаблона в hello Azure Marketplace и нажмите кнопку **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="538bf-139">Go toohello [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) template in hello Azure Marketplace, and click **Deploy**.</span></span>
2. <span data-ttu-id="538bf-140">В hello портал Azure просмотрите hello данные, а затем нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="538bf-140">In hello Azure portal, review hello information and then click **Create**.</span></span>
   
    ![Создание на портале][portal]
3. <span data-ttu-id="538bf-142">На hello **основы** колонки, введите имя кластера hello, который также имена hello ВМ головного узла.</span><span class="sxs-lookup"><span data-stu-id="538bf-142">On hello **Basics** blade, enter a name for hello cluster, which also names hello head node VM.</span></span> <span data-ttu-id="538bf-143">Можно выбрать существующую группу ресурсов или создать группу для развертывания hello в расположении, которое является доступной tooyou.</span><span class="sxs-lookup"><span data-stu-id="538bf-143">You can choose an existing resource group or create a group for hello deployment in a location that's available tooyou.</span></span> <span data-ttu-id="538bf-144">Hello расположение влияет на доступность hello некоторые размеры виртуальной Машины и другим службам Azure (см. [продукты, доступные по регионам](https://azure.microsoft.com/regions/services/)).</span><span class="sxs-lookup"><span data-stu-id="538bf-144">hello location affects hello availability of certain VM sizes and other Azure services (see [Products available by region](https://azure.microsoft.com/regions/services/)).</span></span>
4. <span data-ttu-id="538bf-145">На hello **головной узел параметры** колонке первого развертывания можно принять параметры по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-145">On hello **Head node settings** blade, for a first deployment, you can generally accept hello default settings.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="538bf-146">Hello **URL-адрес сценария после конфигурации** — необязательный параметр toospecify общедоступным сценарий Windows PowerShell, вы хотите toorun на ВМ головного узла hello после ее запуска.</span><span class="sxs-lookup"><span data-stu-id="538bf-146">hello **Post-configuration script URL** is an optional setting toospecify a publicly available Windows PowerShell script that you want toorun on hello head node VM after it is running.</span></span> 
   > 
   > 
5. <span data-ttu-id="538bf-147">На hello **вычислить параметры узла** колонке выберите шаблон именования для узлов hello, hello число и размер узлов hello и hello toodeploy распространения Linux.</span><span class="sxs-lookup"><span data-stu-id="538bf-147">On hello **Compute node settings** blade, select a naming pattern for hello nodes, hello number and size of hello nodes, and hello Linux distribution toodeploy.</span></span>
6. <span data-ttu-id="538bf-148">На hello **параметры инфраструктуры** колонки, введите имена для hello виртуальной сети и Active Directory домена, домена и учетные данные администратора виртуальной Машины и шаблон именования для учетных записей хранения hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-148">On hello **Infrastructure settings** blade, enter names for hello virtual network and Active Directory domain, domain and VM administrator credentials, and a naming pattern for hello storage accounts.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="538bf-149">Пакет HPC использует пользователей кластера tooauthenticate домена Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-149">HPC Pack uses hello Active Directory domain tooauthenticate cluster users.</span></span> 
   > 
   > 
7. <span data-ttu-id="538bf-150">После запуска hello проверочные тесты и просмотрите hello условия использования, нажмите кнопку **покупки**.</span><span class="sxs-lookup"><span data-stu-id="538bf-150">After hello validation tests run and you review hello terms of use, click **Purchase**.</span></span>

### <a name="deployment-option-2-use-hello-iaas-deployment-script"></a><span data-ttu-id="538bf-151">Вариант развертывания 2.</span><span class="sxs-lookup"><span data-stu-id="538bf-151">Deployment option 2.</span></span> <span data-ttu-id="538bf-152">Использование скрипта развертывания IaaS hello</span><span class="sxs-lookup"><span data-stu-id="538bf-152">Use hello IaaS deployment script</span></span>
<span data-ttu-id="538bf-153">Ниже перечислены предварительные условия toodeploy hello кластера с помощью скрипта развертывания IaaS пакета HPC hello:</span><span class="sxs-lookup"><span data-stu-id="538bf-153">Following are additional prerequisites toodeploy hello cluster by using hello HPC Pack IaaS deployment script:</span></span>

* <span data-ttu-id="538bf-154">**Клиентский компьютер** -необходим сценарий развертывания клиента на основе Windows компьютера toorun hello кластера.</span><span class="sxs-lookup"><span data-stu-id="538bf-154">**Client computer** - You need a Windows-based client computer toorun hello cluster deployment script.</span></span>
* <span data-ttu-id="538bf-155">**Azure PowerShell** - [установите и настройте Azure PowerShell](/powershell/azure/overview) (версии 0.8.10 или более поздней) на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="538bf-155">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="538bf-156">**Скрипт развертывания IaaS пакета HPC** — Загрузите и распакуйте hello последнюю версию скрипта hello из hello [центра загрузки Майкрософт](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="538bf-156">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="538bf-157">Проверьте версию hello hello сценария, введя `.\New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="538bf-157">You can check hello version of hello script by running `.\New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="538bf-158">Эта статья основана на версии 4.4.1 или более поздней hello сценария.</span><span class="sxs-lookup"><span data-stu-id="538bf-158">This article is based on version 4.4.1 or later of hello script.</span></span>

<span data-ttu-id="538bf-159">**XML-файл конфигурации**</span><span class="sxs-lookup"><span data-stu-id="538bf-159">**XML configuration file**</span></span>

<span data-ttu-id="538bf-160">Hello скрипт развертывания IaaS пакета HPC использует в качестве кластера HPC hello toodescribe входного XML-файла конфигурации.</span><span class="sxs-lookup"><span data-stu-id="538bf-160">hello HPC Pack IaaS deployment script uses an XML configuration file as input toodescribe hello  HPC cluster.</span></span> <span data-ttu-id="538bf-161">Hello следующий образец файла конфигурации указывает небольшой кластере, состоящем из головного узла HPC Pack и два размер A7 CentOS 7.0 Linux вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="538bf-161">hello following sample configuration file specifies a small cluster consisting of an HPC Pack head node and two size A7 CentOS 7.0 Linux compute nodes.</span></span> 

<span data-ttu-id="538bf-162">При необходимости для вашей среды и конфигурации кластера требуемой, измените файл hello и сохраните его с именем, например HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="538bf-162">Modify hello file as needed for your environment and desired cluster configuration, and save it with a name such as HPCDemoConfig.xml.</span></span> <span data-ttu-id="538bf-163">Например необходимо toosupply имя своей подписки и имя учетной записи хранилища с уникальным и имя облачной службы.</span><span class="sxs-lookup"><span data-stu-id="538bf-163">For example, you need toosupply your subscription name and a unique storage account name and cloud service name.</span></span> <span data-ttu-id="538bf-164">Кроме того может потребоваться, поддерживаемый toochoose другого образа Linux для hello вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="538bf-164">Additionally, you might want toochoose a different supported Linux image for hello compute nodes.</span></span> <span data-ttu-id="538bf-165">Дополнительные сведения об элементах hello в файле конфигурации hello см. в разделе файла Manual.rtf hello в папке скрипта hello и [создание кластера HPC с помощью скрипта развертывания IaaS пакета HPC hello](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="538bf-165">For more information about hello elements in hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>centos7rdmavnetje</VNetName>
    <SubnetName>CentOS7RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS7RDMA-HN</VMName>
    <ServiceName>centos7rdma-je</ServiceName>
  <VMSize>ExtraLarge</VMSize>
  <EnableRESTAPI />
  <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS7RDMA-LN%1%</VMNamePattern>
    <ServiceName>centos7rdma-je</ServiceName>
    <VMSize>A7</VMSize>
    <NodeCount>2</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="538bf-166">**hello toorun скрипт развертывания IaaS пакета HPC**</span><span class="sxs-lookup"><span data-stu-id="538bf-166">**toorun hello HPC Pack IaaS deployment script**</span></span>

1. <span data-ttu-id="538bf-167">Откройте Windows PowerShell на клиентском компьютере hello с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="538bf-167">Open Windows PowerShell on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="538bf-168">Изменение каталога toohello папку, где hello сценария установки (E:\IaaSClusterScript в этом примере).</span><span class="sxs-lookup"><span data-stu-id="538bf-168">Change directory toohello folder where hello script is installed (E:\IaaSClusterScript in this example).</span></span>
   
    ```powershell
    cd E:\IaaSClusterScript
    ```
3. <span data-ttu-id="538bf-169">Запустите следующие кластера HPC Pack hello toodeploy команда hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-169">Run hello following command toodeploy hello HPC Pack cluster.</span></span> <span data-ttu-id="538bf-170">В этом примере предполагается, что этот файл конфигурации hello находится в E:\HPCDemoConfig.xml</span><span class="sxs-lookup"><span data-stu-id="538bf-170">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml</span></span>
   
    ```powershell
    .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
    ```
   
    <span data-ttu-id="538bf-171">а.</span><span class="sxs-lookup"><span data-stu-id="538bf-171">a.</span></span> <span data-ttu-id="538bf-172">Поскольку hello **AdminPassword** не указан в hello предшествующий команды, не запрошенные tooenter hello пароль для пользователя *MyAdminName*.</span><span class="sxs-lookup"><span data-stu-id="538bf-172">Because hello **AdminPassword** is not specified in hello preceding command, you are prompted tooenter hello password for user *MyAdminName*.</span></span>
   
    <span data-ttu-id="538bf-173">b.</span><span class="sxs-lookup"><span data-stu-id="538bf-173">b.</span></span> <span data-ttu-id="538bf-174">затем скрипт Hello запускает файл конфигурации toovalidate hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-174">hello script then starts toovalidate hello configuration file.</span></span> <span data-ttu-id="538bf-175">Он может занять tooseveral минут в зависимости от сетевого подключения hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-175">It can take up tooseveral minutes depending on hello network connection.</span></span>
   
    ![Проверка][validate]
   
    <span data-ttu-id="538bf-177">c.</span><span class="sxs-lookup"><span data-stu-id="538bf-177">c.</span></span> <span data-ttu-id="538bf-178">После проверки передачи, скрипт hello перечисляет toocreate ресурсы кластера hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-178">After validations pass, hello script lists hello cluster resources toocreate.</span></span> <span data-ttu-id="538bf-179">Введите *Y* toocontinue.</span><span class="sxs-lookup"><span data-stu-id="538bf-179">Enter *Y* toocontinue.</span></span>
   
    ![Ресурсы][resources]
   
    <span data-ttu-id="538bf-181">d.</span><span class="sxs-lookup"><span data-stu-id="538bf-181">d.</span></span> <span data-ttu-id="538bf-182">Hello сценарий запускает кластера HPC Pack toodeploy hello и завершения конфигурации hello без дальнейшего действия вручную.</span><span class="sxs-lookup"><span data-stu-id="538bf-182">hello script starts toodeploy hello HPC Pack cluster and completes hello configuration without further manual steps.</span></span> <span data-ttu-id="538bf-183">Hello скрипт может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="538bf-183">hello script can run for several minutes.</span></span>
   
    ![Развернуть][deploy]
   
   > [!NOTE]
   > <span data-ttu-id="538bf-185">В этом примере hello скрипт создает файл журнала автоматически с момента hello **- файл журнала** параметр не указан.</span><span class="sxs-lookup"><span data-stu-id="538bf-185">In this example, hello script generates a log file automatically since hello **-LogFile** parameter isn't specified.</span></span> <span data-ttu-id="538bf-186">журналы Hello не записываются в режиме реального времени, но будут собраны в конце hello hello проверки и развертывания hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-186">hello logs aren't written in real time, but are collected at hello end of hello validation and hello deployment.</span></span> <span data-ttu-id="538bf-187">При остановке процесса PowerShell hello во время выполнения скрипта hello некоторые журналы будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="538bf-187">If hello PowerShell process is stopped while hello script is running, some logs are lost.</span></span>
   > 
   > 

## <a name="connect-toohello-head-node"></a><span data-ttu-id="538bf-188">Подключение toohello головного узла</span><span class="sxs-lookup"><span data-stu-id="538bf-188">Connect toohello head node</span></span>
<span data-ttu-id="538bf-189">После развертывания кластера HPC Pack hello в Azure, [подключитесь с удаленного рабочего стола](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello головного узла виртуальной Машины с помощью учетных данных домена, указанный при развертывании кластера hello "hello" (например, *hpc\\ clusteradmin*).</span><span class="sxs-lookup"><span data-stu-id="538bf-189">After you deploy hello HPC Pack cluster in Azure, [connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, *hpc\\clusteradmin*).</span></span> <span data-ttu-id="538bf-190">Управление hello кластера из головного узла hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-190">You manage hello cluster from hello head node.</span></span>

<span data-ttu-id="538bf-191">На головном узле hello запустите диспетчер кластеров HPC toocheck hello состояние кластера HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-191">On hello head node, start HPC Cluster Manager toocheck hello status of hello HPC Pack cluster.</span></span> <span data-ttu-id="538bf-192">Можно управлять и отслеживать Linux вычислительные узлы hello так же, как работать с Windows вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="538bf-192">You can manage and monitor Linux compute nodes hello same way you work with Windows compute nodes.</span></span> <span data-ttu-id="538bf-193">Например, отобразятся узлы Linux hello, перечисленных в **управление ресурсами** (эти узлы развертываются с hello **LinuxNode** шаблона).</span><span class="sxs-lookup"><span data-stu-id="538bf-193">For example, you see hello Linux nodes listed in **Resource Management** (these nodes are deployed with hello **LinuxNode** template).</span></span>

![Управление узлами][management]

<span data-ttu-id="538bf-195">Также отобразятся узлы Linux hello в hello **тепловой карты** представления.</span><span class="sxs-lookup"><span data-stu-id="538bf-195">You also see hello Linux nodes in hello **Heat Map** view.</span></span>

![Тепловая карта][heatmap]

## <a name="how-toomove-data-in-a-cluster-with-linux-nodes"></a><span data-ttu-id="538bf-197">Как toomove данных в кластере с узлами Linux</span><span class="sxs-lookup"><span data-stu-id="538bf-197">How toomove data in a cluster with Linux nodes</span></span>
<span data-ttu-id="538bf-198">У вас есть несколько вариантов toomove данных узлах Linux, а Windows hello головного узла кластера hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-198">You have several choices toomove data among Linux nodes and hello Windows head node of hello cluster.</span></span> <span data-ttu-id="538bf-199">Ниже приведены три распространенных методов, более подробно в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-199">Here are three common methods, described in more detail in hello following sections:</span></span>

* <span data-ttu-id="538bf-200">**Файл Azure** -предоставляет файлы управляемых toostore данных общей папки SMB файла в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="538bf-200">**Azure File** - Exposes a managed SMB file share toostore data files in Azure storage.</span></span> <span data-ttu-id="538bf-201">Windows узлы и узлы Linux можно подключить Azure файловый ресурс как к диску или папке на hello же время, даже если они развернуты в разных виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="538bf-201">Windows nodes and Linux nodes can mount an Azure File share as a drive or folder at hello same time, even if they're deployed in different virtual networks.</span></span>
* <span data-ttu-id="538bf-202">**Головной узел SMB совместно использовать** -подключение стандартных общую папку Windows hello головного узла на узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="538bf-202">**Head node SMB share** - Mounts a standard Windows shared folder of hello head node on Linux nodes.</span></span>
* <span data-ttu-id="538bf-203">**Сервер NFS головного узла** — предоставляет решение для обмена файлами для смешанной среды Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="538bf-203">**Head node NFS server**  - Provides a file-sharing solution for a mixed Windows and Linux environment.</span></span>

### <a name="azure-file-storage"></a><span data-ttu-id="538bf-204">Хранилище файлов Azure</span><span class="sxs-lookup"><span data-stu-id="538bf-204">Azure File storage</span></span>
<span data-ttu-id="538bf-205">Hello [файла Azure](https://azure.microsoft.com/services/storage/files/) служба предоставляет общие файловые ресурсы с помощью стандартного протокола SMB 2.1 hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-205">hello [Azure File](https://azure.microsoft.com/services/storage/files/) service exposes file shares using hello standard SMB 2.1 protocol.</span></span> <span data-ttu-id="538bf-206">Виртуальные машины Azure и облачных служб можно совместно использовать данные файлов между компонентами приложения с помощью монтируемых хранилищ и локальных приложений можно обращаться из файла данных в общей папке hello API-Интерфейс хранилища файлов.</span><span class="sxs-lookup"><span data-stu-id="538bf-206">Azure VMs and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share through hello File storage API.</span></span> 

<span data-ttu-id="538bf-207">Подробное описание шагов toocreate совместного использования файлов Azure, а затем подключите его на головном узле hello, см. [приступить к работе с хранилищем Windows Azure файл](../../../storage/files/storage-how-to-use-files-windows.md).</span><span class="sxs-lookup"><span data-stu-id="538bf-207">For detailed steps toocreate an Azure File share and mount it on hello head node, see [Get started with Azure File storage on Windows](../../../storage/files/storage-how-to-use-files-windows.md).</span></span> <span data-ttu-id="538bf-208">в разделе toomount hello Azure общей папки на узлах Linux hello, [как toouse хранилища Azure File с Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="538bf-208">toomount hello Azure File share on hello Linux nodes, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="538bf-209">tooset сохранение подключения в разделе [tooMicrosoft Persisting соединений файлов Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span><span class="sxs-lookup"><span data-stu-id="538bf-209">tooset up persisting connections, see [Persisting connections tooMicrosoft Azure Files](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx).</span></span>

<span data-ttu-id="538bf-210">В следующем примере hello создайте Azure файловый ресурс в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="538bf-210">In hello following example, create an Azure File share on a storage account.</span></span> <span data-ttu-id="538bf-211">toomount hello делиться на hello головного узла, откройте командную строку и введите следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="538bf-211">toomount hello share on hello head node, open a Command Prompt and enter hello following commands:</span></span>

```command
cmdkey /add:allvhdsje.file.core.windows.net /user:allvhdsje /pass:<storageaccountkey>

net use Z: \\allvhdje.file.core.windows.net\rdma /persistent:yes
```

<span data-ttu-id="538bf-212">В этом примере allvhdsje — это имя учетной записи хранилища, storageaccountkey является ключ учетной записи хранилища и rdma — hello Azure имя общей папки.</span><span class="sxs-lookup"><span data-stu-id="538bf-212">In this example, allvhdsje is your storage account name, storageaccountkey is your storage account key, and rdma is hello Azure File share name.</span></span> <span data-ttu-id="538bf-213">Hello Azure общей папки на головном узле hello подключается как Z:.</span><span class="sxs-lookup"><span data-stu-id="538bf-213">hello Azure File share is mounted as Z: on hello head node.</span></span>

<span data-ttu-id="538bf-214">toomount hello Azure общей папки на узлах Linux, запустите **clusrun** на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-214">toomount hello Azure File share on Linux nodes, run a **clusrun** command on hello head node.</span></span> <span data-ttu-id="538bf-215">**[ClusRun](https://technet.microsoft.com/library/cc947685.aspx)**  является полезным toocarry средство HPC Pack административные задачи на нескольких узлах.</span><span class="sxs-lookup"><span data-stu-id="538bf-215">**[Clusrun](https://technet.microsoft.com/library/cc947685.aspx)** is a useful HPC Pack tool toocarry out administrative tasks on multiple nodes.</span></span> <span data-ttu-id="538bf-216">(См. также раздел [Clusrun для узлов Linux](#Clusrun-for-Linux-nodes) в этой статье.)</span><span class="sxs-lookup"><span data-stu-id="538bf-216">(See also [Clusrun for Linux nodes](#Clusrun-for-Linux-nodes) in this article.)</span></span>

<span data-ttu-id="538bf-217">Откройте окно Windows PowerShell и введите следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="538bf-217">Open a Windows PowerShell window and enter hello following commands:</span></span>

```powershell
clusrun /nodegroup:LinuxNodes mkdir -p /rdma

clusrun /nodegroup:LinuxNodes mount -t cifs //allvhdsje.file.core.windows.net/rdma /rdma -o vers=2.1`,username=allvhdsje`,password=<storageaccountkey>'`,dir_mode=0777`,file_mode=0777
```

<span data-ttu-id="538bf-218">Hello первая команда создает папку с именем /rdma на всех узлах в группе LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-218">hello first command creates a folder named /rdma on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="538bf-219">Вторая команда Hello подключает hello allvhdsjw.file.core.windows.net/rdma общую папку файлов Azure на папку /rdma hello с dir и файл too777 набор битов режима.</span><span class="sxs-lookup"><span data-stu-id="538bf-219">hello second command mounts hello Azure File share allvhdsjw.file.core.windows.net/rdma onto hello /rdma folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="538bf-220">Вторая команда hello allvhdsje — это имя учетной записи хранилища и storageaccountkey является ключ учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="538bf-220">In hello second command, allvhdsje is your storage account name and storageaccountkey is your storage account key.</span></span>

> [!NOTE]
> <span data-ttu-id="538bf-221">Hello "\\`" символа в hello вторая команда является escape-символа для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="538bf-221">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="538bf-222">«\\`, «означает, что hello»,» (запятая) является частью команды hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-222">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="head-node-share"></a><span data-ttu-id="538bf-223">Общая папка головного узла</span><span class="sxs-lookup"><span data-stu-id="538bf-223">Head node share</span></span>
<span data-ttu-id="538bf-224">Кроме того подключите общей папки hello головного узла на узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="538bf-224">Alternatively, mount a shared folder of hello head node on Linux nodes.</span></span> <span data-ttu-id="538bf-225">Hello простейший способ tooshare файлов предоставляет общую папку, но hello головного узла и всех узлах Linux должны быть развернуты в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="538bf-225">A share provides hello simplest way tooshare files, but hello head node and all Linux nodes must be deployed in hello same virtual network.</span></span> <span data-ttu-id="538bf-226">Ниже приведены шаги, hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-226">Here are hello steps.</span></span>

1. <span data-ttu-id="538bf-227">Создайте папку на головном узле hello и предоставить к нему tooEveryone с разрешениями чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="538bf-227">Create a folder on hello head node and share it tooEveryone with Read/Write permissions.</span></span> <span data-ttu-id="538bf-228">Например, общий ресурс D:\OpenFOAM на hello головного узла в качестве \\CentOS7RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="538bf-228">For example, share D:\OpenFOAM on hello head node as \\CentOS7RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="538bf-229">Здесь CentOS7RDMA HN — имя узла hello hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="538bf-229">Here CentOS7RDMA-HN is hello hostname of hello head node.</span></span>
   
    ![Разрешения общих папок][fileshareperms]
   
    ![Общий доступ к файлам][filesharing]
2. <span data-ttu-id="538bf-232">Откройте окно Windows PowerShell и выполните следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="538bf-232">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS7RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="538bf-233">Hello первая команда создает папку с именем /openfoam на всех узлах в группе LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-233">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="538bf-234">Вторая команда Hello подключает //CentOS7RDMA-HN/OpenFOAM hello общие папки на папку hello с dir и файл too777 набор битов режима.</span><span class="sxs-lookup"><span data-stu-id="538bf-234">hello second command mounts hello shared folder //CentOS7RDMA-HN/OpenFOAM onto hello folder with dir and file mode bits set too777.</span></span> <span data-ttu-id="538bf-235">Hello имя пользователя и пароль в команде hello должно быть hello пользователя и пароль для пользователя кластера на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-235">hello username and password in hello command should be hello username and password of a cluster user on hello head node.</span></span> <span data-ttu-id="538bf-236">(См. раздел [Добавление и удаление пользователей кластера](https://technet.microsoft.com/library/ff919330.aspx).)</span><span class="sxs-lookup"><span data-stu-id="538bf-236">(See [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).)</span></span>

> [!NOTE]
> <span data-ttu-id="538bf-237">Hello "\\`" символа в hello вторая команда является escape-символа для PowerShell.</span><span class="sxs-lookup"><span data-stu-id="538bf-237">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="538bf-238">«\\`, «означает, что hello»,» (запятая) является частью команды hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-238">“\\`,” means that hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

### <a name="nfs-server"></a><span data-ttu-id="538bf-239">Сервер NFS</span><span class="sxs-lookup"><span data-stu-id="538bf-239">NFS server</span></span>
<span data-ttu-id="538bf-240">Hello службы для NFS позволяет tooshare и перенос файлов между компьютерами под управлением операционной системы Windows Server 2012 hello, с помощью протокола SMB hello и компьютеров под управлением Linux, с помощью протокола NFS hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-240">hello NFS service enables you tooshare and migrate files between computers running hello Windows Server 2012 operating system using hello SMB protocol and Linux-based computers using hello NFS protocol.</span></span> <span data-ttu-id="538bf-241">Hello NFS-сервер и все остальные узлы имеют toobe, развернутых в hello одной виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="538bf-241">hello NFS server and all other nodes have toobe deployed in hello same virtual network.</span></span> <span data-ttu-id="538bf-242">Он обеспечивает большую совместимость с узлами Linux, чем общая папка SMB.</span><span class="sxs-lookup"><span data-stu-id="538bf-242">It provides better compatibility with Linux nodes compared with an SMB share.</span></span> <span data-ttu-id="538bf-243">Например, он поддерживает ссылки на файлы.</span><span class="sxs-lookup"><span data-stu-id="538bf-243">For example, it supports file links.</span></span>

1. <span data-ttu-id="538bf-244">tooinstall и настройке NFS-сервер, следуйте указаниям hello [сервера для системы сетевой общей папке первый-законченный](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span><span class="sxs-lookup"><span data-stu-id="538bf-244">tooinstall and set up an NFS server, follow hello steps in [Server for Network File System First Share End-to-End](http://blogs.technet.com/b/filecab/archive/2012/10/08/server-for-network-file-system-first-share-end-to-end.aspx).</span></span>
   
    <span data-ttu-id="538bf-245">Например можно создайте с именем nfs и hello следующие свойства общего ресурса NFS:</span><span class="sxs-lookup"><span data-stu-id="538bf-245">For example, create an NFS share named nfs with hello following properties:</span></span>
   
    ![Авторизация NFS][nfsauth]
   
    ![Разрешения общих папок NFS][nfsshare]
   
    ![Разрешения NTFS NFS][nfsperm]
   
    ![Свойства управления NFS][nfsmanage]
2. <span data-ttu-id="538bf-250">Откройте окно Windows PowerShell и выполните следующие команды hello:</span><span class="sxs-lookup"><span data-stu-id="538bf-250">Open a Windows PowerShell window and run hello following commands:</span></span>
   
    ```powershell
    clusrun /nodegroup:LinuxNodes mkdir -p /nfsshare
   
    clusrun /nodegroup:LinuxNodes mount CentOS7RDMA-HN:/nfs /nfsshared
    ```
   
   <span data-ttu-id="538bf-251">Hello первая команда создает папку с именем /nfsshared на всех узлах в группе LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-251">hello first command creates a folder named /nfsshared on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="538bf-252">Hello вторая команда подключение hello NFS совместно использовать CentOS7RDMA HN: / nfs на hello папки.</span><span class="sxs-lookup"><span data-stu-id="538bf-252">hello second command mounts hello NFS share CentOS7RDMA-HN:/nfs onto hello folder.</span></span> <span data-ttu-id="538bf-253">Здесь CentOS7RDMA HN: / nfs — hello удаленный путь общего ресурса NFS.</span><span class="sxs-lookup"><span data-stu-id="538bf-253">Here CentOS7RDMA-HN:/nfs is hello remote path of your NFS share.</span></span>

## <a name="how-toosubmit-jobs"></a><span data-ttu-id="538bf-254">Как toosubmit заданий</span><span class="sxs-lookup"><span data-stu-id="538bf-254">How toosubmit jobs</span></span>
<span data-ttu-id="538bf-255">Существует несколько способов кластера HPC Pack toohello toosubmit заданий:</span><span class="sxs-lookup"><span data-stu-id="538bf-255">There are several ways toosubmit jobs toohello HPC Pack cluster:</span></span>

* <span data-ttu-id="538bf-256">Пользовательский интерфейс диспетчера кластеров HPC или диспетчера заданий HPC</span><span class="sxs-lookup"><span data-stu-id="538bf-256">HPC Cluster Manager or HPC Job Manager GUI</span></span>
* <span data-ttu-id="538bf-257">Веб-портал HPC</span><span class="sxs-lookup"><span data-stu-id="538bf-257">HPC web portal</span></span>
* <span data-ttu-id="538bf-258">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="538bf-258">REST API</span></span>

<span data-ttu-id="538bf-259">Задание отправки toohello кластера в Azure с помощью средства графического интерфейса пользователя пакета HPC и веб-портал HPC hello hello таким же как и для вычислительных узлов Windows.</span><span class="sxs-lookup"><span data-stu-id="538bf-259">Job submission toohello cluster in Azure via HPC Pack GUI tools and hello HPC web portal are hello same as for Windows compute nodes.</span></span> <span data-ttu-id="538bf-260">В разделе [диспетчера заданий HPC Pack](https://technet.microsoft.com/library/ff919691.aspx) и [как toosubmit заданий на локальном компьютере клиента](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="538bf-260">See [HPC Pack Job Manager](https://technet.microsoft.com/library/ff919691.aspx) and [How toosubmit jobs from an on-premises client computer](../../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="538bf-261">задания toosubmit через REST API hello ссылаться слишком[Создание и отправка заданий с помощью hello REST API в пакете Microsoft HPC](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span><span class="sxs-lookup"><span data-stu-id="538bf-261">toosubmit jobs via hello REST API, refer too[Creating and Submitting Jobs by Using hello REST API in Microsoft HPC Pack](http://social.technet.microsoft.com/wiki/contents/articles/7737.creating-and-submitting-jobs-by-using-the-rest-api-in-microsoft-hpc-pack-windows-hpc-server.aspx).</span></span> <span data-ttu-id="538bf-262">toosubmit задания из клиента Linux, также см. Образец hello Python toohello [пакет SDK HPC](https://www.microsoft.com/download/details.aspx?id=47756).</span><span class="sxs-lookup"><span data-stu-id="538bf-262">toosubmit jobs from a Linux client, also refer toohello Python sample in hello [HPC Pack SDK](https://www.microsoft.com/download/details.aspx?id=47756).</span></span>

## <a name="clusrun-for-linux-nodes"></a><span data-ttu-id="538bf-263">Clusrun для узлов Linux</span><span class="sxs-lookup"><span data-stu-id="538bf-263">Clusrun for Linux nodes</span></span>
<span data-ttu-id="538bf-264">Hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) средство может стать команд используется tooexecute на узлах Linux через командную строку или в диспетчере кластера HPC.</span><span class="sxs-lookup"><span data-stu-id="538bf-264">hello HPC Pack [clusrun](https://technet.microsoft.com/library/cc947685.aspx) tool can be used tooexecute commands on Linux nodes either through a Command Prompt or HPC Cluster Manager.</span></span> <span data-ttu-id="538bf-265">Ниже приводится несколько простых примеров.</span><span class="sxs-lookup"><span data-stu-id="538bf-265">Following are some basic examples.</span></span>

* <span data-ttu-id="538bf-266">Показать текущие имена пользователей на всех узлах в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-266">Show current user names on all nodes in hello cluster.</span></span>
  
    ```command
    clusrun whoami
    ```
* <span data-ttu-id="538bf-267">Установка hello **gdb** средства отладки с **yum** на всех узлах hello linuxnodes группировать и затем перезапустить узлы hello через 10 минут.</span><span class="sxs-lookup"><span data-stu-id="538bf-267">Install hello **gdb** debugger tool with **yum** on all nodes in hello linuxnodes group and then restart hello nodes after 10 minutes.</span></span>
  
    ```command
    clusrun /nodegroup:linuxnodes yum install gdb –y; shutdown –r 10
    ```
* <span data-ttu-id="538bf-268">Создать сценарий оболочки, отображение каждого числа от 1 до 10 в течение одной секунды на каждом узле Linux в кластере hello, запустите его и Показать выходные данные от узлов hello немедленно.</span><span class="sxs-lookup"><span data-stu-id="538bf-268">Create a shell script displaying each number 1 through 10 for one second on each Linux node in hello cluster, run it, and show output from hello nodes immediately.</span></span>
  
    ```command
    clusrun /interleaved /nodegroup:linuxnodes echo \"for i in {1..10}; do echo \\\"\$i\\\"; sleep 1; done\" ^> script.sh; chmod +x script.sh; ./script.sh
    ```

> [!NOTE]
> <span data-ttu-id="538bf-269">Может потребоваться toouse некоторые escape-символы в **clusrun** команд.</span><span class="sxs-lookup"><span data-stu-id="538bf-269">You might need toouse certain escape characters in **clusrun** commands.</span></span> <span data-ttu-id="538bf-270">Как показано в следующем примере используется ^ в командной строке tooescape hello» > «символ.</span><span class="sxs-lookup"><span data-stu-id="538bf-270">As shown in this example, use ^ in a Command Prompt tooescape hello ">" symbol.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="538bf-271">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="538bf-271">Next steps</span></span>
* <span data-ttu-id="538bf-272">Попробуйте вертикальное масштабирование hello кластера tooa большим числом узлов, или под управлением Linux рабочей нагрузки в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="538bf-272">Try scaling up hello cluster tooa larger number of nodes, or try running a Linux workload on hello cluster.</span></span> <span data-ttu-id="538bf-273">Пример см. в статье [Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure](hpcpack-cluster-namd.md).</span><span class="sxs-lookup"><span data-stu-id="538bf-273">For an example, see [Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure](hpcpack-cluster-namd.md).</span></span>
* <span data-ttu-id="538bf-274">Повторите кластер с [ВМ с поддержкой RDMA, большим объемом вычислений](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun рабочих нагрузок MPI.</span><span class="sxs-lookup"><span data-stu-id="538bf-274">Try a cluster with [RDMA-capable, compute-intensive VMs](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toorun MPI workloads.</span></span> <span data-ttu-id="538bf-275">С примером можно ознакомиться в статье [Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC](hpcpack-cluster-openfoam.md).</span><span class="sxs-lookup"><span data-stu-id="538bf-275">For an example, see [Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure](hpcpack-cluster-openfoam.md).</span></span>
* <span data-ttu-id="538bf-276">Если вы заинтересованы в работе с Linux узлов в кластере HPC Pack в локальной среде, см. раздел hello [TechNet рекомендации](https://technet.microsoft.com/library/mt595803.aspx).</span><span class="sxs-lookup"><span data-stu-id="538bf-276">If you are interested in working with Linux nodes in an on-premises HPC Pack cluster, see hello [TechNet guidance](https://technet.microsoft.com/library/mt595803.aspx).</span></span>

<!--Image references-->
[scenario]:media/hpcpack-cluster/scenario.png
[portal]:media/hpcpack-cluster/portal.png
[validate]:media/hpcpack-cluster/validate.png
[resources]:media/hpcpack-cluster/resources.png
[deploy]:media/hpcpack-cluster/deploy.png
[management]:media/hpcpack-cluster/management.png
[heatmap]:media/hpcpack-cluster/heatmap.png
[fileshareperms]:media/hpcpack-cluster/fileshare1.png
[filesharing]:media/hpcpack-cluster/fileshare2.png
[nfsauth]:media/hpcpack-cluster/nfsauth.png
[nfsshare]:media/hpcpack-cluster/nfsshare.png
[nfsperm]:media/hpcpack-cluster/nfsperm.png
[nfsmanage]:media/hpcpack-cluster/nfsmanage.png
