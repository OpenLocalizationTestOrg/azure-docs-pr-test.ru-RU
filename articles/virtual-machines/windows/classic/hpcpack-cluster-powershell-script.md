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
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Создать кластер высокопроизводительных вычислительных систем (HPC) Windows с помощью скрипта развертывания IaaS пакета HPC hello
Запустите сценарий PowerShell toodeploy для hello IaaS пакета HPC развертывания завершения кластера HPC Pack 2012 R2 для рабочих нагрузок Windows на виртуальных машинах Azure. Hello кластер состоит из присоединенных к Active Directory головного узла под управлением Windows Server с пакетом Microsoft HPC и дополнительные окна вычислительные ресурсы, которые вы задаете. Если для рабочих нагрузок Linux toodeploy кластере HPC Pack в Azure, см. [создание кластера Linux HPC с hello скрипт развертывания IaaS пакета HPC](../../linux/classic/hpcpack-cluster-powershell-script.md). Можно также использовать toodeploy шаблона диспетчера ресурсов Azure кластере HPC Pack. Примеры см. в статьях [Создание кластера HPC](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) и [Создание кластера HPC с помощью пользовательского образа вычислительного узла](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).

> [!IMPORTANT] 
> Hello сценарий PowerShell, описанных в этом разделе создается кластер Microsoft HPC Pack 2012 R2 в Azure с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.
> Кроме того сценарий hello, описанных в этой статье не поддерживает 2016 пакета HPC.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a>Примеры файлов конфигурации
В hello следующие примеры подставьте собственные значения для вашей подписки с идентификатором или именем и hello имена учетной записи и службы.

### <a name="example-1"></a>Пример 1
Hello следующий файл конфигурации развертывает кластере HPC Pack с головной узел с локальными базами данных и пять вычислительных узлов под управлением операционной системы Windows Server 2012 R2 hello. Все hello облачные службы создаются непосредственно в hello расположение Запад США. Hello головной узел выступает как контроллер домена в лесу домена hello.

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

### <a name="example-2"></a>Пример 2
Следующий файл конфигурации Hello развертывает кластере HPC Pack в существующем лесу домена. Hello кластере имеется 1 головной узел с локальными базами данных и 12 вычислительных узлов с hello применяется расширение BGInfo виртуальной Машины.
Автоматическая установка обновлений Windows отключена для hello все виртуальные машины в лесу домена hello. Все hello облачные службы создаются непосредственно в расположении Восточная Азия. Hello вычислительные узлы создаются в трех облачных служб и три учетные записи хранения: *MyHPCCN-0001* слишком*MyHPCCN-0005* в *MyHPCCNService01* и  *mycnstorage01*; *С MyHPCCN-0006* слишком*MyHPCCN0010* в *MyHPCCNService02* и *mycnstorage02*; и  *MyHPCCN-0011* слишком*MyHPCCN-0012* в *MyHPCCNService03* и *mycnstorage03*). Hello вычислительные узлы создаются из существующего собственного образа, записанного с вычислительного узла. Hello автоматически увеличиваться и уменьшаться по умолчанию включена служба расширение и уменьшение интервалов.

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

### <a name="example-3"></a>Пример 3
Следующий файл конфигурации Hello развертывает кластере HPC Pack в существующем лесу домена. Hello кластера содержит один головной узел, один сервер базы данных с диска данных объемом 500 ГБ, два узла брокера под управлением операционной системы Windows Server 2012 R2 hello и пять вычислительных узлов под управлением операционной системы Windows Server 2012 R2 hello. Здравствуйте, облачная служба MyHPCCNService создается в территориальной группе hello *MyIBAffinityGroup*, и hello другие облачные службы создаются в территориальной группе hello *MyAffinityGroup*. Hello API REST планировщика заданий HPC и веб-портал HPC на головном узле hello включены.

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



### <a name="example-4"></a>Пример 4
Следующий файл конфигурации Hello развертывает кластере HPC Pack в существующем лесу домена. Hello кластере имеется два головной узел с локальными базами данных, создаются два шаблона узла Azure и для шаблона узла Azure создаются три узла Azure среднего размера *именем AzureTemplate1*. Файл скрипта выполняется на головном узле hello после настройки головного узла hello.

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

## <a name="troubleshooting"></a>Устранение неполадок
* **Ошибка «Виртуальная сеть не существует»** -при запуске сценария toodeploy hello несколько кластеров в Azure одновременно в рамках одной подписки, одно или несколько развертываний может завершиться с ошибкой hello» виртуальной сети *виртуальной сети\_имя* не существует».
  Если эта ошибка возникает, запустите сценарий hello снова для hello Сбой развертывания.
* **Проблемы доступа к hello Интернету из виртуальной сети Azure hello** — при создании кластера с помощью нового контроллера домена с помощью скрипта развертывания hello, или вы вручную повысить роль контроллера toodomain ВМ головного узла, могут возникнуть проблемы подключение виртуальных машин hello toohello Интернет. Это может происходить, если сервер пересылки DNS-сервер автоматически настраивается на контроллере домена hello и неправильного разрешения этого DNS-сервера пересылки.
  
    toowork этой проблемы войдите на контроллер домена toohello и либо удалите параметр конфигурации сервера пересылки hello, или настройте допустимый сервер пересылки DNS-сервера. tooconfigure этот параметр в диспетчере серверов щелкните **средства** >
    **DNS** tooopen диспетчер DNS, а затем дважды щелкните **серверов пересылки**.
* **Проблема с доступом к сети RDMA из виртуальных машин с большим объемом вычислений** — Если добавление вычислений в Windows Server или узлов брокера размера виртуальных машин с помощью функцией RDMA, таких как A8 или A9, могут возникнуть проблемы с подключением эти сети приложений RDMA toohello виртуальных машин. Одна из причин, эта проблема возникает — если hello расширение HpcVmDrivers установлен неправильно при добавлении виртуальных машин hello toohello кластера. Например расширение могло остаться в установке состояния hello.
  
    toowork этой проблемы, первый состояния флажка hello hello расширения в виртуальных машинах hello. Если расширение hello установлен неправильно, попробуйте удалить hello узлы из кластера HPC hello и затем снова добавьте узлы hello. Например можно добавить виртуальные машины вычислительных узлов, запустив скрипт Add-HpcIaaSNode.ps1 hello на головном узле hello.

## <a name="next-steps"></a>Дальнейшие действия
* Запустите тестовую рабочую нагрузку на кластере hello. Пример см. в разделе hello HPC Pack [руководство по началу работы](https://technet.microsoft.com/library/jj884144).
* Hello учебника tooscript кластерное развертывание и запуск HPC рабочей нагрузки, см. в разделе [Приступая к работе с кластере HPC Pack в Azure toorun Excel и SOA рабочих нагрузок](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Повторите toostart средства пакета HPC, остановить, добавления и удаления вычислительных узлов в кластере, создаваемые вами. См. статью [Управление числом и доступностью вычислительных узлов в кластере пакета HPC в Azure](hpcpack-cluster-node-manage.md).
* tooget установка кластера toohello toosubmit заданий с локального компьютера в разделе [кластера HPC отправки задания из локального компьютера tooan пакета HPC в Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

