---
title: "aaaRun ЗВЕЗДА-CCM + с пакетом HPC на виртуальных машинах Linux | Документы Microsoft"
description: "Развертывание кластера Microsoft HPC в Azure и запуск задания STAR-CCM+ на нескольких вычислительных узлах Linux в сети RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="d2a7d-103">Выполнение заданий STAR-CCM+ в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="d2a7d-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="d2a7d-104">В этой статье показано, как кластера toodeploy пакета Microsoft HPC в Azure и выполнения [ЗВЕЗДА приложения adapco CD-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) задания на нескольких вычислительных узлов Linux, которые связаны между собой с InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d2a7d-105">Пакет Microsoft HPC предоставляет возможности toorun разнообразные крупномасштабных HPC и параллельных приложений, включая приложения MPI, в кластерах из виртуальных машин Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="d2a7d-106">Пакет HPC также поддерживает приложения высокопроизводительных вычислений для Linux на виртуальных вычислительных узлах Linux, развернутых в кластере HPC.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="d2a7d-107">Введение toousing Linux вычислительных узлов с помощью пакета HPC, см. в разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="d2a7d-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="d2a7d-108">Настройка кластера пакета HPC</span><span class="sxs-lookup"><span data-stu-id="d2a7d-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="d2a7d-109">Загрузите скрипты развертывания IaaS пакета HPC hello из hello [центра загрузки](https://www.microsoft.com/en-us/download/details.aspx?id=44949) и извлеките их локально.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="d2a7d-110">В системе должен быть установлен компонент Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="d2a7d-111">Если PowerShell на локальном компьютере не настроен, прочтите статью hello [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d2a7d-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d2a7d-112">На момент написания этой статьи hello образы Linux hello из hello Azure Marketplace (который содержит драйверы hello InfiniBand в Azure) — для SLES 12, CentOS версии 6.5 и CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="d2a7d-113">Эта статья основана на использовании hello SLES 12.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="d2a7d-114">Имя hello tooretrieve все образы Linux, которые поддерживают HPC в hello Marketplace, выполните следующую команду PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="d2a7d-115">Результатом Hello список hello расположение, в котором эти изображения доступны и hello имя образа (**ImageName**) toobe, используемый в шаблон развертывания hello позже.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="d2a7d-116">Перед развертыванием кластера hello toobuild имеется файл шаблона развертывания пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="d2a7d-117">Так как мы целевой кластер небольшой, hello головной узел будет hello контроллера домена и размещения локальной базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="d2a7d-118">Hello следующий шаблон будет развертывания головного узла, создайте XML-файл с именем **MyCluster.xml**и замените значения hello **SubscriptionId**, **StorageAccount**,  **Расположение**, **VMName**, и **ServiceName** с вашими.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="d2a7d-119">Запустите Создание hello головной узел, выполнив команду PowerShell hello в командную строку с повышенными привилегиями:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="d2a7d-120">Через 20 минут too30 hello головной узел должен быть готов.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="d2a7d-121">Tooit можно подключиться из hello портал Azure, щелкнув hello **Connect** значок hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="d2a7d-122">В конечном итоге возможно toofix hello DNS-сервер пересылки.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="d2a7d-123">toodo таким образом, запустите диспетчер DNS.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="d2a7d-124">Имя сервера правой кнопкой мыши hello в диспетчере DNS, выберите **свойства**, а затем нажмите кнопку hello **серверов пересылки** вкладку.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="d2a7d-125">Нажмите кнопку hello **изменить** tooremove серверы пересылки, а затем нажмите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="d2a7d-126">Убедитесь в том, что hello **использовать корневые ссылки, если нет серверов пересылки доступны** флажок установлен и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="d2a7d-127">Настройка вычислительных узлов Linux</span><span class="sxs-lookup"><span data-stu-id="d2a7d-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="d2a7d-128">Развертывание вычислительных узлов hello Linux с помощью hello того же шаблона развертывания, вы использовали toocreate hello головного узла.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="d2a7d-129">Копирование файла hello **MyCluster.xml** из головного узла toohello локального компьютера, а также обновление hello **NodeCount** тег с hello число узлов, которое следует toodeploy (< = 20).</span><span class="sxs-lookup"><span data-stu-id="d2a7d-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="d2a7d-130">Быть внимательны toohave достаточное количество доступных ядер Azure квоты, так как каждого экземпляра A9 будет занимать 16 ядер в подписке.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="d2a7d-131">Экземпляры A8 (8 ядер) можно использовать вместо A9, если требуется больше виртуальных машин в hello toouse же бюджет.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="d2a7d-132">На головном узле hello скопируйте скрипты развертывания IaaS пакета HPC hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="d2a7d-133">Выполните следующие команды Azure PowerShell в командную строку hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="d2a7d-134">Запустите **Add-AzureAccount** tooconnect tooyour подписки Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="d2a7d-135">Если у вас несколько подписок, запустите **Get-AzureSubscription** toolist их.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="d2a7d-136">Задать подписку по умолчанию, выполнив hello **xxxx Select-AzureSubscription - SubscriptionName-по умолчанию** команды.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="d2a7d-137">Запустите **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart развертывание Linux вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![Развертывание головного узла][hndeploy]

<span data-ttu-id="d2a7d-139">Откройте средство диспетчера кластеров HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="d2a7d-140">Через несколько минут вычислительные узлы Linux станут периодически появляться в списке вычислительных узлов кластера.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="d2a7d-141">Режимом hello классического развертывания ВМ IaaS создаются последовательно.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="d2a7d-142">Поэтому если важно hello количество узлов, получение все развертывания может занять значительное время.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Узлы Linux в диспетчере кластера пакета HPC][clustermanager]

<span data-ttu-id="d2a7d-144">Теперь, когда все узлы в кластере hello доступны и запущены, существуют параметры toomake дополнительную инфраструктуру.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="d2a7d-145">Настройка общей папки Azure для узлов Windows и Linux</span><span class="sxs-lookup"><span data-stu-id="d2a7d-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="d2a7d-146">Можно использовать скрипты toostore службы файлов Azure hello, пакеты приложений и файлов данных.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="d2a7d-147">Служба файлов Azure предоставляет возможности CIFS на базе хранилища BLOB-объектов Azure как постоянного хранилища.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="d2a7d-148">Имейте в виду, это не самым эффективным решением hello, но он hello один простой и не требует выделенных виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="d2a7d-149">Создать общий ресурс файла Azure в соответствии с инструкциями hello в статье hello [приступить к работе с хранилищем Windows Azure файл](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="d2a7d-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="d2a7d-150">Оставьте hello имя вашей учетной записи хранилища, как **saname**, имя общей папки hello как **sharename**и ключ учетной записи хранения hello как **sakey**.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="d2a7d-151">Подключите hello Azure общей папки на головном узле hello</span><span class="sxs-lookup"><span data-stu-id="d2a7d-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="d2a7d-152">Откройте окно командной строки с повышенными привилегиями и выполните следующие команды toostore hello и учетные данные в хранилище локального компьютера hello hello:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="d2a7d-153">Затем toomount hello Azure общую папку, запустите:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="d2a7d-154">Подключите hello Azure общей папки на вычислительных узлах Linux</span><span class="sxs-lookup"><span data-stu-id="d2a7d-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="d2a7d-155">Один полезным инструментом, который поставляется с пакетом HPC — средство clusrun hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="d2a7d-156">Это средство командной строки toorun hello, же команды можно использовать одновременно на нескольких вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="d2a7d-157">В нашем случае он использовал toomount hello Azure общую папку и ее сохранения toosurvive после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="d2a7d-158">В командную строку на головном узле hello выполните следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="d2a7d-159">каталог подключения hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="d2a7d-160">toomount hello Azure общей папки:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="d2a7d-161">общий ресурс подключения hello toopersist:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="d2a7d-162">Установка STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="d2a7d-162">Install STAR-CCM+</span></span>
<span data-ttu-id="d2a7d-163">Экземпляры виртуальной машины Azure A8 и A9 обеспечивают поддержку InfiniBand и возможности RDMA.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="d2a7d-164">драйверы ядра Hello, обеспечивающие эти возможности доступны для Windows Server 2012 R2, SUSE 12, CentOS версии 6.5 и CentOS 7.1 изображений в hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="d2a7d-165">Microsoft MPI и Intel MPI (выпуск 5.x) — это два MPI библиотеки hello, поддерживающие драйверы в Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="d2a7d-166">В состав пакета STAR-CCM+ CD-adapco (11.x и более поздней версии) входит библиотека Intel MPI версии 5.x, что обеспечивает поддержку InfiniBand для Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="d2a7d-167">Получить hello Linux64 ЗВЕЗДА-CCM + пакета из hello [приложения adapco компакт-диска портал](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="d2a7d-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="d2a7d-168">В нашем случае мы использовали версию 11.02.010 в режиме смешанной точности.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="d2a7d-169">На головном узле hello в hello **/hpcdata** файла Azure совместного использования, создайте сценарий с именем **setupstarccm.sh** с hello после содержимого.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="d2a7d-170">Этот сценарий будет выполняться каждый tooset узел вычислений копирование ЗВЕЗДА-CCM + локально.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="d2a7d-171">Пример сценария setupstarcm.sh</span><span class="sxs-lookup"><span data-stu-id="d2a7d-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="d2a7d-172">Теперь tooset копирование ЗВЕЗДА-CCM + в вашей системе Linux вычислительных узлов, откройте командную строку с повышенными привилегиями и выполните hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="d2a7d-173">Пока выполняется команда hello, hello ЦП можно отслеживать с помощью hello тепловой карты диспетчера кластеров служб.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="d2a7d-174">Через несколько минут все узлы будут настроены должным образом.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="d2a7d-175">Запуск заданий STAR-CCM+</span><span class="sxs-lookup"><span data-stu-id="d2a7d-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="d2a7d-176">Пакет HPC используется для его возможности планировщика заданий в порядке toorun ЗВЕЗДА-CCM + заданий.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="d2a7d-177">toodo таким образом, требуется hello поддержки несколько скриптов, используемых toostart hello задания и выполняемые ЗВЕЗДА-CCM +.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="d2a7d-178">Hello входных данных хранится на hello Azure общей папки, первый для простоты.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="d2a7d-179">Следующий сценарий PowerShell Hello — используется tooqueue ЗВЕЗДЫ-CCM + задания.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="d2a7d-180">Он принимает три аргумента:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-180">It takes three arguments:</span></span>

* <span data-ttu-id="d2a7d-181">Имя модели Hello</span><span class="sxs-lookup"><span data-stu-id="d2a7d-181">hello model name</span></span>
* <span data-ttu-id="d2a7d-182">число Hello используется toobe узлов</span><span class="sxs-lookup"><span data-stu-id="d2a7d-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="d2a7d-183">Hello количество ядер на каждый узел, toobe используется</span><span class="sxs-lookup"><span data-stu-id="d2a7d-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="d2a7d-184">Поскольку ЗВЕЗДА-CCM + можно заполнить hello пропускной способности памяти, это обычно лучше toouse меньше ядра на вычислительные узлы и добавить новые узлы.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="d2a7d-185">Hello точное число ядер на узел будет зависеть от семейство процессоров hello и скорость взаимосвязь hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="d2a7d-186">узлы Hello выделяются исключительно для задания hello и не может совместно использоваться другими заданиями.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="d2a7d-187">Hello задание не запускается как задание MPI напрямую.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="d2a7d-188">Hello **runstarccm.sh** запускает сценарий запуска MPI hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="d2a7d-189">Hello входных данных модели и hello **runstarccm.sh** сценарий хранятся в hello **/hpcdata** общего ресурса, который был подключен ранее.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="d2a7d-190">Файлы журналов именуются с ИД задания hello и хранятся в hello **/hpcdata папки**, вместе с hello ЗВЕЗДА-CCM + выходные файлы.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="d2a7d-191">Пример сценария SubmitStarccmJob.ps1</span><span class="sxs-lookup"><span data-stu-id="d2a7d-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="d2a7d-192">Замените **runner.java** предпочтительным средством запуска моделей Java и кодом ведения журнала STAR-CCM+.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="d2a7d-193">Пример сценария runstarccm.sh</span><span class="sxs-lookup"><span data-stu-id="d2a7d-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="d2a7d-194">В рамках теста мы использовали маркер лицензии увеличения мощности по требованию.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="d2a7d-195">Для этого токена у вас есть tooset hello **$CDLMD_LICENSE_FILE** переменной среды слишком **1999@flex.cd-adapco.com**  и ключ hello в hello **- podkey** параметр hello командной строки .</span><span class="sxs-lookup"><span data-stu-id="d2a7d-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="d2a7d-196">После некоторых инициализации hello сценарий извлекает--из hello **$CCP_NODES_CORES** переменные среды, HPC Pack — hello список узлов toobuild использует hostfile, который hello запуска MPI.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="d2a7d-197">Этот hostfile будет содержать список имен узлов вычислений, используемые для задания hello, по одному имени на строку hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="d2a7d-198">Формат Hello **$CCP_NODES_CORES** имеет следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="d2a7d-199">Описание</span><span class="sxs-lookup"><span data-stu-id="d2a7d-199">Where:</span></span>

* <span data-ttu-id="d2a7d-200">`<Number of nodes>`— количество узлов, выделенных toothis задания hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="d2a7d-201">`<Name of node_n_...>`— Имя каждого узла, выделенное задание toothis hello.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="d2a7d-202">`<Cores of node_n_...>`— hello количество ядер на узле hello выделенной toothis задания.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="d2a7d-203">Здравствуйте, количество ядер (**$NBCORES**) — это также вычисляемый на основе hello количество узлов (**$NBNODES**) и hello количество ядер на узел (передается в качестве параметра **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="d2a7d-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="d2a7d-204">Для доступа к параметрам MPI hello, hello, которые используются с Intel MPI в Azure:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="d2a7d-205">`-mpi intel`toospecify Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="d2a7d-206">`-fabric UDAPL`команды toouse InfiniBand в Azure.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="d2a7d-207">`-cpubind bandwidth,v`пропускная способность toooptimize для MPI с ЗВЕЗДА-CCM +.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="d2a7d-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI работы с Azure InfiniBand и tooset hello необходимое количество ядер на узел.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="d2a7d-209">`-batch`toostart ЗВЕЗДА-CCM + в пакетном режиме без пользовательского интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="d2a7d-210">И, наконец toostart задания, убедитесь, что узлы доступны и запущены и находятся в оперативном режиме в диспетчере кластеров.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="d2a7d-211">В командной строке PowerShell выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="d2a7d-212">Остановка узлов</span><span class="sxs-lookup"><span data-stu-id="d2a7d-212">Stop nodes</span></span>
<span data-ttu-id="d2a7d-213">Позднее после завершения тестов, можно использовать следующие toostop команд HPC Pack PowerShell hello и запуска узлов:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="d2a7d-214">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2a7d-214">Next steps</span></span>
<span data-ttu-id="d2a7d-215">Попробуйте запустить другие рабочие нагрузки Linux.</span><span class="sxs-lookup"><span data-stu-id="d2a7d-215">Try running other Linux workloads.</span></span> <span data-ttu-id="d2a7d-216">Например, ознакомьтесь со следующими статьями:</span><span class="sxs-lookup"><span data-stu-id="d2a7d-216">For example, see:</span></span>

* [<span data-ttu-id="d2a7d-217">Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="d2a7d-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="d2a7d-218">Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="d2a7d-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
