---
title: "Сценарий PowerShell для развертывания кластера HPC на основе Linux | Документация Майкрософт"
description: "Из этой статьи вы узнаете, как с помощью сценария PowerShell развернуть кластер пакета HPC 2012 R2 в Linux на виртуальной машине Azure."
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
ms.openlocfilehash: c15dc66718a855e22f8109448cb8c8a23787b9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="79205-103">Создание кластера высокопроизводительных вычислительных систем (HPC) Linux с помощью сценария развертывания пакета HPC в IaaS</span><span class="sxs-lookup"><span data-stu-id="79205-103">Create a Linux high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="79205-104">Выполните сценарий PowerShell для развертывания пакета HPC в IaaS, чтобы развернуть полный кластер HPC 2012 R2 для рабочих нагрузок Linux на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="79205-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="79205-105">Кластер состоит из присоединенного к Active Directory головного узла под управлением Windows Server и пакета Microsoft HPC, а также вычислительных узлов под управлением одного из дистрибутивов Linux с поддержкой пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="79205-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of the Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="79205-106">Если вы хотите развернуть кластер пакета HPC в Azure для рабочих нагрузок Windows, см. статью [Создание кластера для высокопроизводительных вычислений (HPC) Windows с помощью сценария развертывания пакета HPC в IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="79205-106">If you want to deploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="79205-107">Вы также можете использовать шаблон диспетчера ресурсов Azure для развертывания HPC-кластера.</span><span class="sxs-lookup"><span data-stu-id="79205-107">You can also use an Azure Resource Manager template to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="79205-108">Например, см. статью [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/) (Создание кластера HPC с вычислительными узлами Linux).</span><span class="sxs-lookup"><span data-stu-id="79205-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="79205-109">Сценарий PowerShell, описанный в этой статье, создает кластер пакета Microsoft HPC 2012 R2 в Azure с помощью классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="79205-109">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="79205-110">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="79205-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="79205-111">Кроме того сценарий, описанный в этой статье не поддерживает пакет HPC 2016.</span><span class="sxs-lookup"><span data-stu-id="79205-111">In addition, the script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="79205-112">Пример файла конфигурации</span><span class="sxs-lookup"><span data-stu-id="79205-112">Example configuration file</span></span>
<span data-ttu-id="79205-113">Следующий файл конфигурации создает контроллер домена и доменный лес, а также развертывает кластер пакета HPC с одним головным узлом с локальными базами данных и десятью вычислительными узлами под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="79205-113">The following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="79205-114">Все облачные службы создаются сразу в расположении East Asia (Восточная Азия).</span><span class="sxs-lookup"><span data-stu-id="79205-114">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="79205-115">Вычислительные узлы под управлением Linux создаются в двух облачных службах и двух учетных записях хранения (от *MyLnxCN-0001* до *MyLnxCN-0005* в *MyLnxCNService01* и *mylnxstorage01* и от *MyLnxCN-0006* до *MyLnxCN-0010* в *MyLnxCNService02* и *mylnxstorage02*).</span><span class="sxs-lookup"><span data-stu-id="79205-115">The Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="79205-116">Вычислительные узлы создаются из образа OpenLogic CentOS версии 7.0 для Linux.</span><span class="sxs-lookup"><span data-stu-id="79205-116">The compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="79205-117">Подставьте свои значения: имя вашей подписки и имена учетной записи и служб.</span><span class="sxs-lookup"><span data-stu-id="79205-117">Substitute your own values for your subscription name and the account and service names.</span></span>

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
## <a name="troubleshooting"></a><span data-ttu-id="79205-118">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="79205-118">Troubleshooting</span></span>
* <span data-ttu-id="79205-119">**Ошибка "Виртуальная сеть не существует"**.</span><span class="sxs-lookup"><span data-stu-id="79205-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="79205-120">Когда вы запускаете сценарий развертывания IaaS пакета HPC для одновременного развертывания нескольких кластеров в Azure в рамках одной подписки, для одного или нескольких развертываний может возникать ошибка "Виртуальная сеть *имя\_виртуальной_сети* не существует".</span><span class="sxs-lookup"><span data-stu-id="79205-120">If you run the HPC Pack IaaS deployment script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="79205-121">В случае возникновения этой ошибки повторно выполните сценарий для развертывания, завершившегося сбоем.</span><span class="sxs-lookup"><span data-stu-id="79205-121">If this error occurs, rerun the script for the failed deployment.</span></span>
* <span data-ttu-id="79205-122">**Проблема с доступом к Интернету из виртуальной сети Azure**.</span><span class="sxs-lookup"><span data-stu-id="79205-122">**Problem accessing the Internet from the Azure virtual network**.</span></span> <span data-ttu-id="79205-123">Если вы создаете кластер с новым контроллером домена с помощью сценария развертывания или назначаете виртуальную машину контроллером домена вручную, могут возникать проблемы при подключении виртуальных машин к Интернету.</span><span class="sxs-lookup"><span data-stu-id="79205-123">If you create an HPC Pack cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs in the Azure virtual network to the Internet.</span></span> <span data-ttu-id="79205-124">Проблема может возникать, когда DNS-сервер пересылки настраивается на контроллере домена автоматически и не выполняет разрешение адресов должным образом.</span><span class="sxs-lookup"><span data-stu-id="79205-124">This can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="79205-125">Чтобы решить эту проблему, войдите на контроллер домена и удалите настройки сервера пересылки или задайте допустимый DNS-сервер пересылки.</span><span class="sxs-lookup"><span data-stu-id="79205-125">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="79205-126">Для этого в диспетчере серверов щелкните **Сервис** > **DNS**, чтобы открыть диспетчер DNS, а затем дважды щелкните **Серверы пересылки**.</span><span class="sxs-lookup"><span data-stu-id="79205-126">To do this, in Server Manager click **Tools** > **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79205-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="79205-127">Next steps</span></span>
* <span data-ttu-id="79205-128">Сведения о поддерживаемых дистрибутивах Linux, перемещении данных и отправке заданий в кластер пакета HPC с помощью вычислительных узлов под управлением Linux см. в статье [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="79205-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs to an HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="79205-129">Чтобы научиться использовать сценарий для создания кластера и запуска рабочей нагрузки HPC в Linux, см. следующие руководства:</span><span class="sxs-lookup"><span data-stu-id="79205-129">For tutorials that use the script to create a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="79205-130">Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="79205-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="79205-131">Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="79205-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="79205-132">Выполнение заданий STAR-CCM+ в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC</span><span class="sxs-lookup"><span data-stu-id="79205-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

