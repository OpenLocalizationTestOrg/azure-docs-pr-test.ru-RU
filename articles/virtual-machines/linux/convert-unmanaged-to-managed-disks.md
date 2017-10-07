---
title: "aaaConvert виртуальной машины Linux в Azure из неуправляемого диски toomanaged - управляемых дисков Azure | Документы Microsoft"
description: "Как диски tooconvert из toomanaged неуправляемые дисков виртуальной Машины Linux с помощью Azure CLI 2.0 в модели развертывания диспетчера ресурсов hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Преобразовать виртуальную машину Linux с неуправляемой дисков toomanaged дисков

При наличии существующих Linux виртуальных машин (ВМ), использующие неуправляемые диски можно преобразовать диски toouse управляемых виртуальных машин hello через hello [управляемых дисков Azure](../windows/managed-disks-overview.md) службы. Этот процесс преобразует диска hello операционной системы и все подключенные диски данных.

В этой статье показано, как tooconvert виртуальных машин с помощью hello Azure CLI. Если необходима tooinstall или обновить ее, см. раздел [установить CLI Azure 2.0](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Перед началом работы

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Преобразование одноэкземплярных виртуальных машин
В этом разделе описывается, как диски toomanaged в tooconvert экземпляра ВМ Azure из неуправляемого. (Если виртуальные машины в наборе доступности, см. следующий раздел hello.) Можно использовать этот процесс tooconvert hello виртуальных машин из дисков toopremium управляемых дисков неуправляемого premium (SSD) или стандарт (HDD) неуправляемого дисков toostandard управляемых дисков.

1. Освободить hello виртуальной Машины с помощью [ВМ az deallocate](/cli/azure/vm#deallocate). Hello следующий пример отменяет выделение hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Преобразовать диски toomanaged hello ВМ с помощью [преобразование виртуальной машины az](/cli/azure/vm#convert). После процесса преобразует Hello hello виртуальной Машины с именем `myVM`, включая диск hello ОС и дисков данных:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Запустите hello виртуальной Машины после hello преобразования toomanaged диски с помощью [запуска виртуальной машины az](/cli/azure/vm#start). Следующий пример запускает Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Преобразование виртуальных машин в группе доступности

Если hello ВМ, которые вы хотите tooconvert toomanaged диски находятся в наборе доступности, необходимо сначала управляемый набор tooa tooconvert hello доступности группы доступности.

Все виртуальные машины в наборе доступности hello должна освобождаться перед преобразованием набора доступности hello. Все диски виртуальных машин toomanaged после доступности hello назначила себя tooconvert план был преобразованный tooa управляемые группы доступности. Затем запустите все виртуальные машины hello и продолжить работу в обычном режиме.

1. Выведите список всех виртуальных машин в группе доступности, выполнив команду [az vm availability-set list](/cli/azure/vm/availability-set#list). Hello следующий пример отображает список всех виртуальных машин в набор доступности hello `myAvailabilitySet` в группе ресурсов hello с именем `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Освободить все hello виртуальные машины с помощью [ВМ az deallocate](/cli/azure/vm#deallocate). Hello следующий пример отменяет выделение hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Преобразовать hello доступности с помощью [преобразовать группу доступности виртуальной машины az](/cli/azure/vm/availability-set#convert). Hello следующий пример преобразует набор именованных доступности hello `myAvailabilitySet` в группе ресурсов hello с именем `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Преобразовать все диски toomanaged ВМ hello, используя [преобразование виртуальной машины az](/cli/azure/vm#convert). После процесса преобразует Hello hello виртуальной Машины с именем `myVM`, включая диск hello ОС и дисков данных:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Запустить все виртуальные машины hello после hello преобразования toomanaged диски с помощью [запуска виртуальной машины az](/cli/azure/vm#start). Следующий пример запускает Hello hello виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о возможностях хранения данных доступны в [обзоре Управляемых дисков Azure](../windows/managed-disks-overview.md).
