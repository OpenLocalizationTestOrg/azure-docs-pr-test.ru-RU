---
title: "aaaExpand виртуальных жестких дисков на виртуальной Машине Linux в Azure | Документы Microsoft"
description: "Узнайте, как tooexpand виртуальных жестких дисков на виртуальной Машине Linux с hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>Как tooexpand виртуальных жестких дисков на виртуальной Машине Linux с hello Azure CLI
размер виртуального жесткого диска по умолчанию Hello hello операционной системы (ОС) обычно составляет 30 ГБ на виртуальной машине (VM) Linux в Azure. Вы можете [добавить диски данных](add-disk.md) tooprovide для дополнительного пространства хранилища, но вы также можете tooexpand существующий диск данных. В этой статье указаны как tooexpand управление диски для виртуальной Машины Linux с hello Azure CLI 2.0. Можно также развернуть диск ОС hello неуправляемого с hello [Azure CLI 1.0](expand-disks-nodejs.md).

> [!WARNING]
> Всегда проверяйте, созданы ли резервные копии данных, прежде чем выполнять операции по изменению размера диска. Дополнительные сведения см. в статье [Архивация виртуальных машин Linux в Azure](tutorial-backup-vms.md).

## <a name="expand-disk"></a>Расширение диска
Убедитесь, что hello последней [Azure CLI 2.0](/cli/azure/install-az-cli2) установлен и войти в систему с учетной записью Azure tooan [входа az](/cli/azure/#login).

Для этой статьи потребуется существующая виртуальная машина в Azure с хотя бы одним подключенным и подготовленным диском данных. Если у вас нет виртуальной машины, которую можно использовать, см. раздел [о создании и подготовке виртуальной машины с дисками данных](tutorial-manage-disks.md#create-and-attach-disks).

В hello следующим примерам, замените имена параметров примере собственные значения. Примеры имен параметров: *myResourceGroup* и *myVM*.

1. Невозможно выполнить операции для виртуальных жестких дисков с hello виртуальной Машины под управлением. Отмените подготовку виртуальной машины, выполнив команду [az vm deallocate](/cli/azure/vm#deallocate). Hello следующий пример отменяет выделение hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`не освобождает hello вычислительных ресурсов. toorelease вычислительных ресурсов, используйте `az vm deallocate`. Hello виртуальная машина должна быть освобождена tooexpand hello виртуального жесткого диска.

2. Просмотрите список управляемых дисков в группе ресурсов, выполнив команду [az disk list](/cli/azure/disk#list). Hello следующий пример отображает список управляемых дисков в группе ресурсов hello с именем *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Разверните hello диска с [обновление диска az](/cli/azure/disk#update). Hello следующий пример расширяет hello управляемого диска с именем *myDataDisk* toobe *200*ГБ:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > При развертывании управляемого диска hello обновить размер — сопоставленных toohello ближайший размер управляемого диска. Таблицы размеров свободного управляемого hello и уровней, см. [Azure диски Обзор управляемых - цены и выставление счетов](../windows/managed-disks-overview.md#pricing-and-billing).

3. Запустите виртуальную машину, выполнив команду [az vm start](/cli/azure/vm#start). Следующий пример запускает Hello hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. Tooyour SSH виртуальных Машин с соответствующими учетными данными hello. Можно получить hello общедоступный IP-адрес виртуальной Машины с [Показать ВМ az](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. toouse hello развернуто диска, раздел hello tooexpand и файловой системы.

    а. Если уже подключен, отключите hello диска:

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Используйте `parted` tooview сведения на диске и размер раздела hello:

    ```bash
    sudo parted /dev/sdc
    ```

    Просмотр сведений о hello существующего раздела макета с `print`. Hello выходных данных примерно toohello следующий пример, который показывает, что базовый диск hello имеет размер в ГБ 215:

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. Разверните секцию hello с `resizepart`. Введите номер секции hello, *1*и размер для новой секции hello:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, введите`quit`

5. С секцией hello изменения размеров, проверки согласованности секции hello с `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Теперь измените размер hello файловой системы с `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. Подключения hello секции toohello требуемого расположения, такие как `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. диск ОС hello tooverify был изменен, используйте `df -h`. Следующий пример выходных данных Hello показывает hello диска с данными, */dev/sdc1*, теперь составляет 200 ГБ:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Дальнейшие действия
Если требуется дополнительное хранилище, вы также [добавить tooa дисков данных виртуальной Машины с Linux](add-disk.md). Дополнительные сведения о шифровании диска см. в разделе [шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI](encrypt-disks.md).
