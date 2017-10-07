---
title: "aaaHow tooresize виртуальная машина Linux с hello Azure CLI 2.0 | Документы Microsoft"
description: "Как tooscale вверх или масштаб работу виртуальной машины Linux, изменив hello размер виртуальной Машины."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>Изменение размера виртуальной машины Linux с помощью CLI 2.0

После подготовки виртуальной машины (VM) можно масштабировать hello ВМ вверх или вниз, изменив hello [размер виртуальной Машины][vm-sizes]. В некоторых случаях необходимо сначала отменить hello виртуальной Машины. Требуется toodeallocate hello виртуальной Машины, если размер недоступен в кластере hello оборудования, на котором размещается виртуальная машина hello требуемого hello. В этой статье указаны как tooresize a виртуальная машина Linux с hello Azure CLI 2.0. Можно также выполнить следующие действия с hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="resize-a-vm"></a>Изменение размера виртуальной машины
tooresize виртуальной Машины необходимо hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

1. Изменяет размер hello просмотреть список доступных виртуальных Машин на кластере оборудования hello размещения hello виртуальной Машины с [az виртуальной машины-vm-resize параметры списка](/cli/azure/vm#list-vm-resize-options). Hello следующий пример отображает список размеров виртуальной Машины для виртуальной Машины с именем hello `myVM` в группе ресурсов hello `myResourceGroup` области:
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. По желанию hello указан размер виртуальной Машины, изменение размера hello виртуальной Машины с [изменить размер виртуальной машины az](/cli/azure/vm#resize). Следующий пример изменяет размер Hello hello виртуальной Машины с именем `myVM` toohello `Standard_DS3_v2` размер:
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    Hello ВМ перезапускается во время этого процесса. После перезапуска hello сопоставляются существующей операционной системы и дисков данных. Все устройства hello временный диск будет потеряно.

3. При желании hello не указан размер виртуальной Машины необходимо toofirst deallocate hello виртуальной Машины с [ВМ az deallocate](/cli/azure/vm#deallocate). Этот процесс позволяет toothen ВМ hello использоваться размер tooany размер доступной, hello поддерживает области и их запуска. Hello следующее deallocate, масштабировать и затем запустить Виртуальную машину с именем hello `myVM` в группе ресурсов hello с именем `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > Освобождение hello виртуальной Машины также освобождает любой динамических IP-адресов, назначенных toohello виртуальной Машины. Hello ОС и диски с данными не затрагиваются.

## <a name="next-steps"></a>Дальнейшие действия
Для дополнительной масштабируемости запустите несколько экземпляров виртуальных машин и разверните их. Дополнительные сведения см. в статье [Автоматическое масштабирование машин Linux в наборе масштабирования виртуальных машин][scale-set]. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
