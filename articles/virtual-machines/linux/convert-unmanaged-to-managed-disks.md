---
title: "Управляемые диски Azure. Преобразование виртуальной машины Linux с неуправляемыми дисками в Azure для использования управляемых дисков | Документация Майкрософт"
description: "Переключение виртуальной машины Linux, развернутой в рамках модели Resource Manager, с неуправляемых дисков на управляемые диски с помощью Azure CLI 2.0."
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
ms.openlocfilehash: 94f8e3330fb2d6547811315fcfdb8ced338e0247
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-to-managed-disks"></a>Переключение виртуальной машины Linux с неуправляемых дисков на управляемые диски

При наличии виртуальных машин Linux, использующих неуправляемые диски, их можно преобразовать для использования управляемых дисков с помощью службы [Управляемые диски Azure](../windows/managed-disks-overview.md). При этом преобразуются диск операционной системы и все подключенные диски данных.

В этой статье показано, как преобразовать виртуальные машины с помощью Azure CLI. Если вам установить или обновить Azure CLI, ознакомьтесь со статьей [Установка Azure CLI 2.0](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Перед началом работы

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Преобразование одноэкземплярных виртуальных машин
В этом разделе описывается, как преобразовать одноэкземплярные виртуальные машины Azure с неуправляемыми дисками, чтобы они могли использовать Управляемые диски. (Если виртуальные машины находятся в группе доступности, ознакомьтесь со следующим разделом.) Этот процесс позволяет переключить виртуальные машины с неуправляемых дисков уровня "Премиум" (SSD) на управляемые диски уровня "Премиум" или с неуправляемых дисков уровня "Стандартный" (жесткие диски) на управляемые диски уровня "Стандартный".

1. Отмените выделение виртуальной машины с помощью команды [az vm deallocate](/cli/azure/vm#deallocate). В следующем примере освобождается виртуальная машина `myVM`, входящая в группу ресурсов `myResourceGroup`.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Преобразуйте виртуальную машину для использования управляемых дисков, выполнив команду [az vm convert](/cli/azure/vm#convert). Приведенный ниже процесс преобразовывает виртуальную машину `myVM`, включая ее диск ОС и все диски данных.

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. После преобразования запустите виртуальную машину командой [az vm start](/cli/azure/vm#start). В следующем примере запускается виртуальная машина `myVM` в группе ресурсов `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Преобразование виртуальных машин в группе доступности

Если виртуальные машины, которые вы хотите преобразовать для использования управляемых дисков, входят в группу доступности, то необходимо сначала преобразовать эту группу доступности в управляемую группу доступности.

Перед преобразованием группы доступности нужно освободить все виртуальные машины в этой группе. Запланируйте преобразование всех виртуальных машин для использования управляемых дисков после того, как содержащая их группа доступности будет преобразована в управляемую группу доступности. Затем можно будет запустить все виртуальные машины и продолжить работу в обычном режиме.

1. Выведите список всех виртуальных машин в группе доступности, выполнив команду [az vm availability-set list](/cli/azure/vm/availability-set#list). В следующем примере выводится список виртуальных машин в группе доступности `myAvailabilitySet` в группе ресурсов `myResourceGroup`.

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Отмените выделение всех виртуальных машин командой [az vm deallocate](/cli/azure/vm#deallocate). В следующем примере освобождается виртуальная машина `myVM`, входящая в группу ресурсов `myResourceGroup`.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Преобразуйте группу доступности с помощью команды [az vm availability-set convert](/cli/azure/vm/availability-set#convert). В следующем примере преобразовывается группа доступности `myAvailabilitySet` в группе ресурсов `myResourceGroup`.

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Преобразуйте все виртуальные машины для использования управляемых дисков с помощью команды [az vm convert](/cli/azure/vm#convert). Приведенный ниже процесс преобразовывает виртуальную машину `myVM`, включая ее диск ОС и все диски данных.

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. После преобразования запустите все виртуальные машины с помощью команды [az vm start](/cli/azure/vm#start). В следующем примере запускается виртуальная машина `myVM` в группе ресурсов `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о возможностях хранения данных доступны в [обзоре Управляемых дисков Azure](../windows/managed-disks-overview.md).
