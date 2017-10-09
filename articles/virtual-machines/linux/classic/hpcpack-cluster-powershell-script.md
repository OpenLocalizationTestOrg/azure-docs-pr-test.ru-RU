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
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Создать кластер высокопроизводительных вычислительных систем (HPC) Linux с помощью скрипта развертывания IaaS пакета HPC hello
Запустите hello IaaS пакета HPC развертывания PowerShell скрипт toodeploy завершения кластера HPC Pack 2012 R2 для Linux рабочих нагрузок в виртуальных машинах Azure. Hello кластер состоит из присоединенных к Active Directory головного узла под управлением Windows Server с пакетом Microsoft HPC и вычислительных узлов, которые работают в одном из hello дистрибутивы Linux, поддерживаемых пакетом HPC. Toodeploy кластере HPC Pack в Windows Azure для рабочих нагрузок см [Создайте кластер Windows HPC с hello скрипт развертывания IaaS пакета HPC](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Можно также использовать toodeploy шаблона диспетчера ресурсов Azure кластере HPC Pack. Например, см. статью [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/) (Создание кластера HPC с вычислительными узлами Linux).

> [!IMPORTANT] 
> Hello сценарий PowerShell, описанных в этом разделе создается кластер Microsoft HPC Pack 2012 R2 в Azure с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.
> Кроме того сценарий hello, описанных в этой статье не поддерживает 2016 пакета HPC.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>Пример файла конфигурации
Hello следующий файл конфигурации создает контроллер домена и леса доменов и развертывает кластере HPC Pack, имеющего один головной узел с локальными базами данных и 10 вычислительных узлах Linux. Все hello облачные службы создаются непосредственно в месте hello Восточная Азия. Hello Linux вычислительные узлы создаются в два облачные службы и две учетные записи хранения (то есть *MyLnxCN-0001* для *MyLnxCN-0005* в *MyLnxCNService01* и *mylnxstorage01*, и *MyLnxCN-0006* для *MyLnxCN 0010* в *MyLnxCNService02* и *mylnxstorage02* ). Hello вычислительные узлы создаются из образа Linux OpenLogic CentOS версии 7.0. 

Подставьте собственные значения для имени подписки и hello имена учетной записи и службы.

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
## <a name="troubleshooting"></a>Устранение неполадок
* **Ошибка "Виртуальная сеть не существует"**. При выполнении toodeploy скрипт развертывания IaaS пакета HPC hello несколько кластеров в Azure одновременно в рамках одной подписки, одно или несколько развертываний может завершиться с ошибкой hello» виртуальной сети *VNet\_имя* не существует».
  Если эта ошибка возникает, снова запустите скрипт hello hello Сбой развертывания.
* **Проблемы доступа к hello Интернету из виртуальной сети Azure hello**. Если создание кластера HPC Pack с нового контроллера домена с помощью скрипта развертывания hello или повышения головного узла ВМ контроллера toodomain вручную, могут возникнуть проблемы с подключением hello виртуальных машин в виртуальной сети Azure hello toohello Интернет. Это может произойти, если сервер пересылки DNS-сервер автоматически настраивается на контроллере домена hello и неправильного разрешения этого DNS-сервера пересылки.
  
    toowork этой проблемы войдите на контроллер домена toohello и либо удалите параметр конфигурации сервера пересылки hello, или настройте допустимый сервер пересылки DNS-сервера. toodo это, в диспетчере серверов щелкните **средства** > **DNS** tooopen диспетчер DNS, а затем дважды щелкните **серверов пересылки**.

## <a name="next-steps"></a>Дальнейшие действия
* В разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](hpcpack-cluster.md) сведения о поддерживаемых дистрибутивах Linux перемещение данных и отправки задания кластера HPC Pack tooan с Linux вычислительных узлов.
* Руководства, с помощью скрипта hello toocreate кластера и выполните Linux HPC рабочей нагрузки см.:
  * [Запуск NAMD с пакетом Microsoft HPC на вычислительных узлах Linux в Azure](hpcpack-cluster-namd.md)
  * [Выполнение заданий OpenFoam в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC](hpcpack-cluster-openfoam.md)
  * [Выполнение заданий STAR-CCM+ в кластере Linux RDMA в Azure с помощью пакета Microsoft HPC](hpcpack-cluster-starccm.md)

