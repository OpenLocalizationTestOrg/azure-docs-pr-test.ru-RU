---
title: "сценарий aaaPowerShell toodeploy кластера Linux HPC | Документы Microsoft"
description: "Запустите сценарий PowerShell toodeploy кластеров Linux HPC Pack 2012 R2 в виртуальных машинах Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="fa7ef-103">Создать кластер высокопроизводительных вычислительных систем (HPC) Linux с помощью скрипта развертывания IaaS пакета HPC hello</span><span class="sxs-lookup"><span data-stu-id="fa7ef-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="fa7ef-104">Запустите hello IaaS пакета HPC развертывания PowerShell скрипт toodeploy завершения кластера HPC Pack 2012 R2 для Linux рабочих нагрузок в виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="fa7ef-105">Hello кластер состоит из присоединенных к Active Directory головного узла под управлением Windows Server с пакетом Microsoft HPC и вычислительных узлов, которые работают в одном из hello дистрибутивы Linux, поддерживаемых пакетом HPC.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="fa7ef-106">Toodeploy кластере HPC Pack в Windows Azure для рабочих нагрузок см [Создайте кластер Windows HPC с hello скрипт развертывания IaaS пакета HPC](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa7ef-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="fa7ef-107">Можно также использовать toodeploy шаблона диспетчера ресурсов Azure кластере HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="fa7ef-108">Например, см. статью [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/) (Создание кластера HPC с вычислительными узлами Linux).</span><span class="sxs-lookup"><span data-stu-id="fa7ef-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="fa7ef-109">Hello сценарий PowerShell, описанных в этом разделе создается кластер Microsoft HPC Pack 2012 R2 в Azure с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="fa7ef-110">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="fa7ef-111">Кроме того сценарий hello, описанных в этой статье не поддерживает 2016 пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="fa7ef-112">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="fa7ef-112">Example configuration file</span></span>
<span data-ttu-id="fa7ef-113">Hello следующий файл конфигурации создает контроллер домена и леса доменов и развертывает кластере HPC Pack, имеющего один головной узел с локальными базами данных и 10 вычислительных узлах Linux.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="fa7ef-114">Все hello облачные службы создаются непосредственно в месте hello Восточная Азия.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="fa7ef-115">Hello Linux вычислительные узлы создаются в два облачные службы и две учетные записи хранения (то есть *MyLnxCN-0001* для *MyLnxCN-0005* в *MyLnxCNService01* и *mylnxstorage01*, и *MyLnxCN-0006* для *MyLnxCN 0010* в *MyLnxCNService02* и *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="fa7ef-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="fa7ef-116">Hello вычислительные узлы создаются из образа Linux OpenLogic CentOS версии 7.0.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="fa7ef-117">Подставьте собственные значения для имени подписки и hello имена учетной записи и службы.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="fa7ef-118">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="fa7ef-118">Troubleshooting</span></span>
* <span data-ttu-id="fa7ef-119">**Ошибка "Виртуальная сеть не существует"**.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="fa7ef-120">При выполнении toodeploy скрипт развертывания IaaS пакета HPC hello несколько кластеров в Azure одновременно в рамках одной подписки, одно или несколько развертываний может завершиться с ошибкой hello» виртуальной сети *VNet\_имя* не существует».</span><span class="sxs-lookup"><span data-stu-id="fa7ef-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="fa7ef-121">Если эта ошибка возникает, снова запустите скрипт hello hello Сбой развертывания.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="fa7ef-122">**Проблемы доступа к hello Интернету из виртуальной сети Azure hello**.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="fa7ef-123">Если создание кластера HPC Pack с нового контроллера домена с помощью скрипта развертывания hello или повышения головного узла ВМ контроллера toodomain вручную, могут возникнуть проблемы с подключением hello виртуальных машин в виртуальной сети Azure hello toohello Интернет.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="fa7ef-124">Это может произойти, если сервер пересылки DNS-сервер автоматически настраивается на контроллере домена hello и неправильного разрешения этого DNS-сервера пересылки.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="fa7ef-125">toowork этой проблемы войдите на контроллер домена toohello и либо удалите параметр конфигурации сервера пересылки hello, или настройте допустимый сервер пересылки DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="fa7ef-126">toodo это, в диспетчере серверов щелкните **средства** > **DNS** tooopen диспетчер DNS, а затем дважды щелкните **серверов пересылки**.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa7ef-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa7ef-127">Next steps</span></span>
* <span data-ttu-id="fa7ef-128">В разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md) сведения о поддерживаемых дистрибутивах Linux перемещение данных и отправки задания кластера HPC Pack tooan с Linux вычислительных узлов.</span><span class="sxs-lookup"><span data-stu-id="fa7ef-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="fa7ef-129">Руководства, с помощью скрипта hello toocreate кластера и выполните Linux HPC рабочей нагрузки см.:</span><span class="sxs-lookup"><span data-stu-id="fa7ef-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="fa7ef-130">Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="fa7ef-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="fa7ef-131">Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="fa7ef-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="fa7ef-132">Выполнение заданий STAR-CCM+ в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="fa7ef-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

