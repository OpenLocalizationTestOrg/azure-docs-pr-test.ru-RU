---
title: "aaaHow tooresize виртуальная машина Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Как tooscale вверх или масштаб работу виртуальной машины Linux, изменив hello размер виртуальной Машины."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>Изменение размера виртуальной машины Linux с помощью Azure CLI 1.0

## <a name="overview"></a>Обзор

После подготовки виртуальной машины (VM) можно масштабировать hello ВМ вверх или вниз, изменив hello [размер виртуальной Машины][vm-sizes]. В некоторых случаях необходимо сначала отменить hello виртуальной Машины. Это может произойти, если новый размер hello не доступен на кластере hello оборудования, на котором размещается виртуальная машина hello.

В этой статье показано, как tooresize в виртуальной Машине Linux с помощью hello [Azure CLI][azure-cli].

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#resize-a-linux-vm) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -нашей нового поколения CLI для модели развертывания hello ресурсов управления


## <a name="resize-a-linux-vm"></a>Изменение размера виртуальной машины Linux
tooresize виртуальную Машину, выполните hello следующие шаги.

1. Выполните следующую команду CLI hello. Эта команда выводит список размеров виртуальных Машин hello, доступные на кластере оборудования hello hello ВМ размещения.
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. При желании hello, указан размер запустите hello, следующая команда tooresize hello виртуальной Машины.
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    во время этого процесса будет перезапущена Hello виртуальной Машины. После перезапуска hello будут перераспределены существующей операционной системы и дисков данных. Все устройства hello временного диска будут потеряны.
   
    Используйте hello `--enable-boot-diagnostics` позволяет [загрузки диагностики][boot-diagnostics], toolog связанные toostartup любые ошибки.
3. В противном случае — если hello требуемого размера не указан, выполните следующие команды toodeallocate hello виртуальной Машины, ее размер, а затем перезапустите ВМ hello hello.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > Освобождение hello виртуальной Машины также освобождает любой динамических IP-адресов, назначенных toohello виртуальной Машины. Hello ОС и диски с данными не затрагиваются.
   > 
   > 

## <a name="next-steps"></a>Дальнейшие действия
Для дополнительной масштабируемости запустите несколько экземпляров виртуальных машин и разверните их. Дополнительные сведения см. в статье [Автоматическое масштабирование машин Linux в наборе масштабирования виртуальных машин][scale-set]. 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
