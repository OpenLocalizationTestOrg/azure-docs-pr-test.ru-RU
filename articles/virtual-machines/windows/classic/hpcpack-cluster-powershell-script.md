---
title: "кластер Windows HPC toodeploy aaaPowerShell сценарий | Документы Microsoft"
description: "Запустить сценарий PowerShell toodeploy кластера Windows HPC Pack 2012 R2 в виртуальных машинах Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="50a6a-103">Создать кластер высокопроизводительных вычислительных систем (HPC) Windows с помощью скрипта развертывания IaaS пакета HPC hello</span><span class="sxs-lookup"><span data-stu-id="50a6a-103">Create a Windows high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="50a6a-104">Запустите сценарий PowerShell toodeploy для hello IaaS пакета HPC развертывания завершения кластера HPC Pack 2012 R2 для рабочих нагрузок Windows на виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="50a6a-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="50a6a-105">Hello кластер состоит из присоединенных к Active Directory головного узла под управлением Windows Server с пакетом Microsoft HPC и дополнительные окна вычислительные ресурсы, которые вы задаете.</span><span class="sxs-lookup"><span data-stu-id="50a6a-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="50a6a-106">Если для рабочих нагрузок Linux toodeploy кластере HPC Pack в Azure, см. [создание кластера Linux HPC с hello скрипт развертывания IaaS пакета HPC](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="50a6a-106">If you want toodeploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with hello HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="50a6a-107">Можно также использовать toodeploy шаблона диспетчера ресурсов Azure кластере HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="50a6a-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="50a6a-108">Примеры см. в статьях [Создание кластера HPC](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) и [Создание кластера HPC с помощью пользовательского образа вычислительного узла](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span><span class="sxs-lookup"><span data-stu-id="50a6a-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="50a6a-109">Hello сценарий PowerShell, описанных в этом разделе создается кластер Microsoft HPC Pack 2012 R2 в Azure с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="50a6a-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="50a6a-110">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="50a6a-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="50a6a-111">Кроме того сценарий hello, описанных в этой статье не поддерживает 2016 пакета HPC.</span><span class="sxs-lookup"><span data-stu-id="50a6a-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="50a6a-112">Примеры файлов конфигурации</span><span class="sxs-lookup"><span data-stu-id="50a6a-112">Example configuration files</span></span>
<span data-ttu-id="50a6a-113">В hello следующие примеры подставьте собственные значения для вашей подписки с идентификатором или именем и hello имена учетной записи и службы.</span><span class="sxs-lookup"><span data-stu-id="50a6a-113">In hello following examples, substitute your own values for your subscription Id or name and hello account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="50a6a-114">Пример 1</span><span class="sxs-lookup"><span data-stu-id="50a6a-114">Example 1</span></span>
<span data-ttu-id="50a6a-115">Hello следующий файл конфигурации развертывает кластере HPC Pack с головной узел с локальными базами данных и пять вычислительных узлов под управлением операционной системы Windows Server 2012 R2 hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-115">hello following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="50a6a-116">Все hello облачные службы создаются непосредственно в hello расположение Запад США.</span><span class="sxs-lookup"><span data-stu-id="50a6a-116">All hello cloud services are created directly in hello West US location.</span></span> <span data-ttu-id="50a6a-117">Hello головной узел выступает как контроллер домена в лесу домена hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-117">hello head node acts as domain controller of hello domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="50a6a-118">Пример 2</span><span class="sxs-lookup"><span data-stu-id="50a6a-118">Example 2</span></span>
<span data-ttu-id="50a6a-119">Следующий файл конфигурации Hello развертывает кластере HPC Pack в существующем лесу домена.</span><span class="sxs-lookup"><span data-stu-id="50a6a-119">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="50a6a-120">Hello кластере имеется 1 головной узел с локальными базами данных и 12 вычислительных узлов с hello применяется расширение BGInfo виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="50a6a-120">hello cluster has 1 head node with local databases and 12 compute nodes with hello BGInfo VM extension applied.</span></span>
<span data-ttu-id="50a6a-121">Автоматическая установка обновлений Windows отключена для hello все виртуальные машины в лесу домена hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-121">Automatic installation of Windows updates is disabled for all hello VMs in hello domain forest.</span></span> <span data-ttu-id="50a6a-122">Все hello облачные службы создаются непосредственно в расположении Восточная Азия.</span><span class="sxs-lookup"><span data-stu-id="50a6a-122">All hello cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="50a6a-123">Hello вычислительные узлы создаются в трех облачных служб и три учетные записи хранения: *MyHPCCN-0001* слишком*MyHPCCN-0005* в *MyHPCCNService01* и  *mycnstorage01*; *С MyHPCCN-0006* слишком*MyHPCCN0010* в *MyHPCCNService02* и *mycnstorage02*; и  *MyHPCCN-0011* слишком*MyHPCCN-0012* в *MyHPCCNService03* и *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="50a6a-123">hello compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* too*MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* too*MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* too*MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="50a6a-124">Hello вычислительные узлы создаются из существующего собственного образа, записанного с вычислительного узла.</span><span class="sxs-lookup"><span data-stu-id="50a6a-124">hello compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="50a6a-125">Hello автоматически увеличиваться и уменьшаться по умолчанию включена служба расширение и уменьшение интервалов.</span><span class="sxs-lookup"><span data-stu-id="50a6a-125">hello auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="50a6a-126">Пример 3</span><span class="sxs-lookup"><span data-stu-id="50a6a-126">Example 3</span></span>
<span data-ttu-id="50a6a-127">Следующий файл конфигурации Hello развертывает кластере HPC Pack в существующем лесу домена.</span><span class="sxs-lookup"><span data-stu-id="50a6a-127">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="50a6a-128">Hello кластера содержит один головной узел, один сервер базы данных с диска данных объемом 500 ГБ, два узла брокера под управлением операционной системы Windows Server 2012 R2 hello и пять вычислительных узлов под управлением операционной системы Windows Server 2012 R2 hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-128">hello cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running hello Windows Server 2012 R2 operating system, and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="50a6a-129">Здравствуйте, облачная служба MyHPCCNService создается в территориальной группе hello *MyIBAffinityGroup*, и hello другие облачные службы создаются в территориальной группе hello *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="50a6a-129">hello cloud service MyHPCCNService is created in hello affinity group *MyIBAffinityGroup*, and hello other cloud services are created in hello affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="50a6a-130">Hello API REST планировщика заданий HPC и веб-портал HPC на головном узле hello включены.</span><span class="sxs-lookup"><span data-stu-id="50a6a-130">hello HPC Job Scheduler REST API and HPC web portal are enabled on hello head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="50a6a-131">Пример 4</span><span class="sxs-lookup"><span data-stu-id="50a6a-131">Example 4</span></span>
<span data-ttu-id="50a6a-132">Следующий файл конфигурации Hello развертывает кластере HPC Pack в существующем лесу домена.</span><span class="sxs-lookup"><span data-stu-id="50a6a-132">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="50a6a-133">Hello кластере имеется два головной узел с локальными базами данных, создаются два шаблона узла Azure и для шаблона узла Azure создаются три узла Azure среднего размера *именем AzureTemplate1*.</span><span class="sxs-lookup"><span data-stu-id="50a6a-133">hello cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="50a6a-134">Файл скрипта выполняется на головном узле hello после настройки головного узла hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-134">A script file runs on hello head node after hello head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="50a6a-135">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="50a6a-135">Troubleshooting</span></span>
* <span data-ttu-id="50a6a-136">**Ошибка «Виртуальная сеть не существует»** -при запуске сценария toodeploy hello несколько кластеров в Azure одновременно в рамках одной подписки, одно или несколько развертываний может завершиться с ошибкой hello» виртуальной сети *виртуальной сети\_имя* не существует».</span><span class="sxs-lookup"><span data-stu-id="50a6a-136">**“VNet doesn’t exist” error** - If you run hello script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="50a6a-137">Если эта ошибка возникает, запустите сценарий hello снова для hello Сбой развертывания.</span><span class="sxs-lookup"><span data-stu-id="50a6a-137">If this error occurs, run hello script again for hello failed deployment.</span></span>
* <span data-ttu-id="50a6a-138">**Проблемы доступа к hello Интернету из виртуальной сети Azure hello** — при создании кластера с помощью нового контроллера домена с помощью скрипта развертывания hello, или вы вручную повысить роль контроллера toodomain ВМ головного узла, могут возникнуть проблемы подключение виртуальных машин hello toohello Интернет.</span><span class="sxs-lookup"><span data-stu-id="50a6a-138">**Problem accessing hello Internet from hello Azure virtual network** - If you create a cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs toohello Internet.</span></span> <span data-ttu-id="50a6a-139">Это может происходить, если сервер пересылки DNS-сервер автоматически настраивается на контроллере домена hello и неправильного разрешения этого DNS-сервера пересылки.</span><span class="sxs-lookup"><span data-stu-id="50a6a-139">This problem can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="50a6a-140">toowork этой проблемы войдите на контроллер домена toohello и либо удалите параметр конфигурации сервера пересылки hello, или настройте допустимый сервер пересылки DNS-сервера.</span><span class="sxs-lookup"><span data-stu-id="50a6a-140">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="50a6a-141">tooconfigure этот параметр в диспетчере серверов щелкните **средства** >
    **DNS** tooopen диспетчер DNS, а затем дважды щелкните **серверов пересылки**.</span><span class="sxs-lookup"><span data-stu-id="50a6a-141">tooconfigure this setting, in Server Manager click **Tools** >
    **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="50a6a-142">**Проблема с доступом к сети RDMA из виртуальных машин с большим объемом вычислений** — Если добавление вычислений в Windows Server или узлов брокера размера виртуальных машин с помощью функцией RDMA, таких как A8 или A9, могут возникнуть проблемы с подключением эти сети приложений RDMA toohello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="50a6a-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs toohello RDMA application network.</span></span> <span data-ttu-id="50a6a-143">Одна из причин, эта проблема возникает — если hello расширение HpcVmDrivers установлен неправильно при добавлении виртуальных машин hello toohello кластера.</span><span class="sxs-lookup"><span data-stu-id="50a6a-143">One reason this problem occurs is if hello HpcVmDrivers extension is not properly installed when hello VMs are added toohello cluster.</span></span> <span data-ttu-id="50a6a-144">Например расширение могло остаться в установке состояния hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-144">For example, the extension might be stuck in hello installing state.</span></span>
  
    <span data-ttu-id="50a6a-145">toowork этой проблемы, первый состояния флажка hello hello расширения в виртуальных машинах hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-145">toowork around this problem, first check hello state of hello extension in hello VMs.</span></span> <span data-ttu-id="50a6a-146">Если расширение hello установлен неправильно, попробуйте удалить hello узлы из кластера HPC hello и затем снова добавьте узлы hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-146">If hello extension is not properly installed, try removing hello nodes from hello HPC cluster and then add hello nodes again.</span></span> <span data-ttu-id="50a6a-147">Например можно добавить виртуальные машины вычислительных узлов, запустив скрипт Add-HpcIaaSNode.ps1 hello на головном узле hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-147">For example, you can add compute node VMs by running hello Add-HpcIaaSNode.ps1 script on hello head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50a6a-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="50a6a-148">Next steps</span></span>
* <span data-ttu-id="50a6a-149">Запустите тестовую рабочую нагрузку на кластере hello.</span><span class="sxs-lookup"><span data-stu-id="50a6a-149">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="50a6a-150">Пример см. в разделе hello HPC Pack [руководство по началу работы](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="50a6a-150">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="50a6a-151">Hello учебника tooscript кластерное развертывание и запуск HPC рабочей нагрузки, см. в разделе [Приступая к работе с кластере HPC Pack в Azure toorun Excel и SOA рабочих нагрузок](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50a6a-151">For a tutorial tooscript hello cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="50a6a-152">Повторите toostart средства пакета HPC, остановить, добавления и удаления вычислительных узлов в кластере, создаваемые вами.</span><span class="sxs-lookup"><span data-stu-id="50a6a-152">Try HPC Pack's tools toostart, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="50a6a-153">См. статью [Управление числом и доступностью вычислительных узлов в кластере пакета HPC в Azure](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="50a6a-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="50a6a-154">tooget установка кластера toohello toosubmit заданий с локального компьютера в разделе [кластера HPC отправки задания из локального компьютера tooan пакета HPC в Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="50a6a-154">tooget set up toosubmit jobs toohello cluster from a local computer, see [Submit HPC jobs from an on-premises computer tooan HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

