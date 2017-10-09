---
title: "размеры виртуальных Машин Linux aaaAzure - HPC | Документы Microsoft"
description: "Список hello различные размеры, доступные для высокопроизводительных вычислительных систем виртуальных машин в Azure Linux."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a>Размеры виртуальных машин Linux, оптимизированных для HPC

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>Экземпляры с поддержкой RDMA
Подмножество hello экземпляров с большим объемом вычислений (H16r, H16mr, A8 и A9) возможностей сетевой интерфейс для подключения к удаленной памяти прямой доступ (RDMA). Этот интерфейс является Кроме размеры виртуальных Машин доступен tooother интерфейс стандартной сети Azure toohello. 
  
Этот интерфейс позволяет hello функцией RDMA экземпляры toocommunicate сети InfiniBand, работая на скорость FDR H16r и H16mr виртуальной машины и скорости QDR для виртуальных машин A8 и A9. Эти возможности RDMA может значительно повысить hello масштабируемость и производительность приложений интерфейса передачи сообщений (MPI).

Ниже приведены требования для сети Azure RDMA hello tooaccess функцией RDMA виртуальных машин Linux:
 
* **Распределения** — необходимо развернуть виртуальные машины с поддержкой RDMA SUSE Linux Enterprise Server (SLES) или программного обеспечения Wave незаконных (прежнее название — OpenLogic) на основе CentOS HPC изображений в hello Azure Marketplace. Hello следующих Marketplace образов поддержки подключения RDMA:
  
    * SLES 12 SP1 для HPC или SLES 12 SP1 для HPC (Premium)
    
    * 7.3 HPC на основе CentOS, 7.1 HPC на основе CentOS, 6.8 HPC на основе CentOS или 6.5 HPC на основе CentOS  
 
        > [!NOTE]
        > Для виртуальных машин серии H рекомендуем использовать образ SLES 12 SP1 для HPC или 7.1 (или более позднюю версию) HPC на основе CentOS.
        >
        > На изображениях HPC на основе CentOS hello, обновления ядра отключены в hello **yum** файла конфигурации. Это происходит потому hello драйверы Linux RDMA распространяемых в виде пакета RPM и обновления драйверов может не работать, если обновляется hello ядра.
        > 
        > 
* **MPI** : Intel MPI Library 5.x
  
    В зависимости от образа Marketplace hello выбирать, отдельные лицензирования, установки, или настройки Intel MPI будет требоваться, следующим образом: 
  
  * **SP1 SLES 12 для образа HPC** -пакеты Intel MPI распространяется на hello виртуальной Машины. Установите, запустив hello следующую команду:

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **Образы HPC на основе CentOS** — здесь уже установлена библиотека Intel MPI 5.1.  
    
    Дополнительные системные конфигурации — необходимые toorun заданий MPI в кластеризованных виртуальных машин. Например, в кластере виртуальных машин, необходимо tooestablish доверия между hello вычислительных узлов. Типичные параметры в разделе [настройки приложений MPI Linux RDMA toorun кластера](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="network-topology-considerations"></a>Аспекты топологии сети
* На виртуальных машинах Linux с поддержкой RDMA интерфейс Eth1 зарезервирован для сетевого трафика RDMA. Не изменяйте параметры Eth1 или любые сведения в файле конфигурации hello ссылается toothis сети. Eth0 зарезервирован для обычного сетевого трафика Azure.

* В Azure не поддерживается IP через InfiniBand (IB). Поддерживается только RDMA через IB.

## <a name="using-hpc-pack"></a>Использование пакета HPC
[Пакет HPC](https://technet.microsoft.com/library/jj899572.aspx), корпорации Майкрософт свободного HPC заданиями и кластером решение по управлению, один из вариантов для вас экземпляров вычислений hello toouse с Linux. последние версии Hello HPC Pack поддерживает несколько дистрибутивов Linux, toorun на вычислительных узлов, развернутые в виртуальных машинах Azure, под управлением Windows Server головного узла. С поддержкой RDMA Linux вычислительных узлов под управлением Intel MPI пакет HPC можно планирование и запуск приложений Linux MPI доступа к сети RDMA hello. Ознакомьтесь со статьей [Начало работы с вычислительными узлами Linux в кластере пакета HPC в Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="other-sizes"></a>Остальные размеры
- [Универсальные](sizes-general.md)
- [Оптимизированные для вычислений](sizes-compute.md)
- [Оптимизированные для памяти](sizes-memory.md)
- [Оптимизированные для хранилища](sizes-storage.md)
- [GPU](../windows/sizes-gpu.md)


## <a name="next-steps"></a>Дальнейшие действия

- tooget запущена, развертывание и использование размера большим объемом вычислений с RDMA в Linux, см. [настройки приложений MPI toorun кластеров Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

- Узнайте больше о том, как с помощью [единиц вычислений Azure (ACU)](acu.md) сравнить производительность вычислений для различных номеров SKU Azure.




