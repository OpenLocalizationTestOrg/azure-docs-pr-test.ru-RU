---
title: "диск aaaExpand операционной системы на виртуальной Машине Linux с hello Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как tooexpand hello виртуального диска операционной системы (ОС) на виртуальной Машине Linux с помощью hello Azure CLI 1.0 и модели развертывания диспетчера ресурсов hello"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a>Расширить диск операционной системы на виртуальной Машине Linux с помощью hello Azure CLI с hello Azure CLI 1.0
размер виртуального жесткого диска по умолчанию Hello hello операционной системы (ОС) обычно составляет 30 ГБ на виртуальной машине (VM) Linux в Azure. Вы можете [добавить диски данных](add-disk.md) tooprovide для дополнительного пространства хранилища, но вы также можете tooexpand hello ОС диска. В этой статье указаны как диск tooexpand hello ОС для ВМ Linux с помощью неуправляемых диски с hello Azure CLI 1.0.

## <a name="cli-versions-toocomplete-hello-task"></a>Задача hello toocomplete версии CLI
Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.

- [Azure CLI 1.0](#prerequisites) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)
- [Azure CLI 2.0](expand-disks.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления

## <a name="prerequisites"></a>Предварительные требования
Требуется hello [последние Azure CLI 1.0](../../cli-install-nodejs.md) установлен и вход tooan [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/) использование режима диспетчера ресурсов hello следующим образом:

```azurecli
azure config mode arm
```

В hello следующим примерам, замените имена параметров примере собственные значения. Примеры имен параметров: *myResourceGroup* и *myVM*.

## <a name="expand-os-disk"></a>Расширение диска операционной системы

1. Невозможно выполнить операции для виртуальных жестких дисков с hello виртуальной Машины под управлением. Hello примере останавливается и освобождает Виртуальную машину с именем hello *myVM* в группе ресурсов hello с именем *myResourceGroup*:

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `azure vm stop`не освобождает hello вычислительных ресурсов. toorelease вычислительных ресурсов, используйте `azure vm deallocate`. Hello виртуальная машина должна быть освобождена tooexpand hello виртуального жесткого диска.

2. Изменить размер hello hello неуправляемого диска операционной системы, выполнив hello `azure vm set` команды. Следующий пример обновляет Hello hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup* toobe *50* ГБ:

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. Запустите виртуальную машину следующим образом:

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. Tooyour SSH виртуальных Машин с соответствующими учетными данными hello. диск ОС hello tooverify был изменен, используйте `df -h`. Hello следующий пример выходных данных показан основной раздел hello (*sda1/dev/*) теперь составляет 50 ГБ:

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a>Дальнейшие действия
Если требуется дополнительное хранилище, вы также [добавить tooa дисков данных виртуальной Машины с Linux](add-disk.md). Дополнительные сведения о шифровании диска см. в разделе [шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI](encrypt-disks.md).
