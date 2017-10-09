---
title: "aaaAbout вычислений виртуальных машин с Linux | Документы Microsoft"
description: "Справочные сведения и рекомендации по использованию hello H-series и A8, A9, A10 и A11 вычислений размеры виртуальных машин Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>Сведения об экземплярах серии H и серии A для ресурсоемких вычислений для Linux
Вот основные сведения и некоторые рекомендации по использованию hello Azure H ряд новых и hello предыдущих размеров A8, A9, A10 и A11, также известный как *вычислений* экземпляров. Эта статья посвящена применению этих размеров на виртуальных машинах Linux. Сведения в этой статье можно также использовать для [виртуальных машин Windows](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Основные характеристики, сведения о дисках и объеме памяти см. в статье [Размеры виртуальных машин в Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>Доступа к сети RDMA toohello
Можно создать кластеры с поддержкой RDMA виртуальных машин Linux, выполните одну из следующих поддерживаемых дистрибутивах Linux HPC и поддерживаемых преимущества tootake реализации MPI сети Azure RDMA hello hello. В разделе [настройки приложений MPI toorun кластеров Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) для параметров развертывания и шаги настройки образца.

* **Распределения** — необходимо развернуть виртуальные машины с поддержкой RDMA SUSE Linux Enterprise Server (SLES) или программного обеспечения Wave незаконных (прежнее название — OpenLogic) на основе CentOS HPC изображений в hello Azure Marketplace. Hello следующих Marketplace образов поддержки подключения RDMA:
  
    * SLES 12 SP1 для HPC, SLES 12 SP1 для HPC (Premium)
    
    * 7.1 HPC на основе CentOS, 6.5 HPC на основе CentOS.  
 
        > [!NOTE]
        > Для виртуальных машин серии H рекомендуем использовать образ SLES 12 SP1 для HPC или 7.1 HPC на основе CentOS.
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
    
    Дополнительные системные конфигурации — необходимые toorun заданий MPI в кластеризованных виртуальных машин. Например, в кластере виртуальных машин, необходимо tooestablish доверия между hello вычислительных узлов. Типичные параметры в разделе [настройки приложений MPI toorun кластеров Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>Рекомендации по использованию пакета HPC и Linux
[Пакет HPC](https://technet.microsoft.com/library/jj899572.aspx), свободного HPC заданиями и кластером решении для управления Майкрософт, предоставляет один вариант toouse hello вычислений экземпляры с Linux. последние версии Hello HPC Pack поддерживает несколько дистрибутивов Linux, toorun на вычислительных узлов, развернутые в виртуальных машинах Azure, под управлением Windows Server головного узла. С поддержкой RDMA Linux вычислительных узлов под управлением Intel MPI пакет HPC можно планирование и запуск приложений Linux MPI доступа к сети RDMA hello. tooget работы см. в разделе [Приступая к работе с Linux вычислительных узлов в кластере HPC Pack в Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Аспекты топологии сети
* На виртуальных машинах Linux с поддержкой RDMA интерфейс Eth1 зарезервирован для сетевого трафика RDMA. Не изменяйте параметры Eth1 или любые сведения в файле конфигурации hello ссылается toothis сети. Eth0 зарезервирован для обычного сетевого трафика Azure.
* В Azure не поддерживается IP через InfiniBand (IB). Поддерживается только RDMA через IB.



## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о доступности и расценках размеров hello большим объемом вычислений см [ценах — виртуальные машины](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Сведения о дисках и объеме памяти см. в статье [Размеры виртуальных машин в Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* tooget запущена, развертывание и использование размера большим объемом вычислений с RDMA в Linux, см. [настройки приложений MPI toorun кластеров Linux RDMA](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

