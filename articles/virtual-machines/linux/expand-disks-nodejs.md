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
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a><span data-ttu-id="6cfe2-103">Расширить диск операционной системы на виртуальной Машине Linux с помощью hello Azure CLI с hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6cfe2-103">Expand OS disk on a Linux VM using hello Azure CLI with hello Azure CLI 1.0</span></span>
<span data-ttu-id="6cfe2-104">размер виртуального жесткого диска по умолчанию Hello hello операционной системы (ОС) обычно составляет 30 ГБ на виртуальной машине (VM) Linux в Azure.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="6cfe2-105">Вы можете [добавить диски данных](add-disk.md) tooprovide для дополнительного пространства хранилища, но вы также можете tooexpand hello ОС диска.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand hello OS disk.</span></span> <span data-ttu-id="6cfe2-106">В этой статье указаны как диск tooexpand hello ОС для ВМ Linux с помощью неуправляемых диски с hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-106">This article details how tooexpand hello OS disk for a Linux VM using unmanaged disks with hello Azure CLI 1.0.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6cfe2-107">Задача hello toocomplete версии CLI</span><span class="sxs-lookup"><span data-stu-id="6cfe2-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="6cfe2-108">Можно выполнить с помощью одного из следующих версий CLI hello задачу hello.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="6cfe2-109">[Azure CLI 1.0](#prerequisites) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="6cfe2-109">[Azure CLI 1.0](#prerequisites) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="6cfe2-110">[Azure CLI 2.0](expand-disks.md) -нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="6cfe2-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6cfe2-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6cfe2-111">Prerequisites</span></span>
<span data-ttu-id="6cfe2-112">Требуется hello [последние Azure CLI 1.0](../../cli-install-nodejs.md) установлен и вход tooan [учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/) использование режима диспетчера ресурсов hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6cfe2-112">You need hello [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in tooan [Azure account](https://azure.microsoft.com/pricing/free-trial/) using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="6cfe2-113">В hello следующим примерам, замените имена параметров примере собственные значения.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-113">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="6cfe2-114">Примеры имен параметров: *myResourceGroup* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="6cfe2-115">Расширение диска операционной системы</span><span class="sxs-lookup"><span data-stu-id="6cfe2-115">Expand OS disk</span></span>

1. <span data-ttu-id="6cfe2-116">Невозможно выполнить операции для виртуальных жестких дисков с hello виртуальной Машины под управлением.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="6cfe2-117">Hello примере останавливается и освобождает Виртуальную машину с именем hello *myVM* в группе ресурсов hello с именем *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="6cfe2-117">hello following example stops and deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="6cfe2-118">`azure vm stop`не освобождает hello вычислительных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-118">`azure vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="6cfe2-119">toorelease вычислительных ресурсов, используйте `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-119">toorelease compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="6cfe2-120">Hello виртуальная машина должна быть освобождена tooexpand hello виртуального жесткого диска.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-120">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="6cfe2-121">Изменить размер hello hello неуправляемого диска операционной системы, выполнив hello `azure vm set` команды.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-121">Update hello size of hello unmanaged OS disk using hello `azure vm set` command.</span></span> <span data-ttu-id="6cfe2-122">Следующий пример обновляет Hello hello виртуальной Машины с именем *myVM* в группе ресурсов hello с именем *myResourceGroup* toobe *50* ГБ:</span><span class="sxs-lookup"><span data-stu-id="6cfe2-122">hello following example updates hello VM named *myVM* in hello resource group named *myResourceGroup* toobe *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="6cfe2-123">Запустите виртуальную машину следующим образом:</span><span class="sxs-lookup"><span data-stu-id="6cfe2-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="6cfe2-124">Tooyour SSH виртуальных Машин с соответствующими учетными данными hello.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-124">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="6cfe2-125">диск ОС hello tooverify был изменен, используйте `df -h`.</span><span class="sxs-lookup"><span data-stu-id="6cfe2-125">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="6cfe2-126">Hello следующий пример выходных данных показан основной раздел hello (*sda1/dev/*) теперь составляет 50 ГБ:</span><span class="sxs-lookup"><span data-stu-id="6cfe2-126">hello following example output shows hello primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="6cfe2-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6cfe2-127">Next steps</span></span>
<span data-ttu-id="6cfe2-128">Если требуется дополнительное хранилище, вы также [добавить tooa дисков данных виртуальной Машины с Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="6cfe2-128">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="6cfe2-129">Дополнительные сведения о шифровании диска см. в разделе [шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="6cfe2-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
