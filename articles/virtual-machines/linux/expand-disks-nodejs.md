---
title: "Расширение диска операционной системы на виртуальной машине Linux с помощью Azure CLI 1.0 | Документация Майкрософт"
description: "Узнайте, как расширить виртуальный диск операционной системы на виртуальной машине Linux с использованием Azure CLI 1.0 и модели развертывания Resource Manager."
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
ms.openlocfilehash: 0aedcd70b54c2ed47ec327ccf0529a48351353c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-the-azure-cli-with-the-azure-cli-10"></a><span data-ttu-id="18d78-103">Расширение дисков операционной системы на виртуальной машине Linux с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="18d78-103">Expand OS disk on a Linux VM using the Azure CLI with the Azure CLI 1.0</span></span>
<span data-ttu-id="18d78-104">Как правило, размер виртуального жесткого диска по умолчанию для операционной системы на виртуальной машине Linux в Azure составляет 30 ГБ.</span><span class="sxs-lookup"><span data-stu-id="18d78-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="18d78-105">Вы можете [добавить диски данных](add-disk.md), чтобы предоставить дополнительное место для хранения, а также расширить диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="18d78-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand the OS disk.</span></span> <span data-ttu-id="18d78-106">В этой статье подробно описано, как расширить диск ОС виртуальной машины Linux, использующей неуправляемые диски, с помощью Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="18d78-106">This article details how to expand the OS disk for a Linux VM using unmanaged disks with the Azure CLI 1.0.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="18d78-107">Версии интерфейса командной строки для выполнения задачи</span><span class="sxs-lookup"><span data-stu-id="18d78-107">CLI versions to complete the task</span></span>
<span data-ttu-id="18d78-108">Вы можете выполнить задачу, используя одну из следующих версий интерфейса командной строки.</span><span class="sxs-lookup"><span data-stu-id="18d78-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="18d78-109">[Azure CLI 1.0](#prerequisites) — интерфейс командной строки для классической модели развертывания и модели развертывания Resource Manager (в этой статье).</span><span class="sxs-lookup"><span data-stu-id="18d78-109">[Azure CLI 1.0](#prerequisites) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="18d78-110">[Azure CLI 2.0](expand-disks.md) — интерфейс командной строки следующего поколения для модели развертывания с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="18d78-110">[Azure CLI 2.0](expand-disks.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18d78-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="18d78-111">Prerequisites</span></span>
<span data-ttu-id="18d78-112">Вам потребуется установить [последнюю версию Azure CLI 1.0](../../cli-install-nodejs.md) и войти в [учетную запись Azure](https://azure.microsoft.com/pricing/free-trial/) в режиме Resource Manager, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="18d78-112">You need the [latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in to an [Azure account](https://azure.microsoft.com/pricing/free-trial/) using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="18d78-113">В следующих примерах замените имена параметров собственными значениями.</span><span class="sxs-lookup"><span data-stu-id="18d78-113">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="18d78-114">Примеры имен параметров: *myResourceGroup* и *myVM*.</span><span class="sxs-lookup"><span data-stu-id="18d78-114">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

## <a name="expand-os-disk"></a><span data-ttu-id="18d78-115">Расширение диска операционной системы</span><span class="sxs-lookup"><span data-stu-id="18d78-115">Expand OS disk</span></span>

1. <span data-ttu-id="18d78-116">Нельзя выполнять операции с виртуальными жесткими дисками на работающей виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="18d78-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="18d78-117">В следующем примере завершается работа и отменяется распределение виртуальной машины *myVM*, входящей в группу ресурсов с именем *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="18d78-117">The following example stops and deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="18d78-118">Операция `azure vm stop` не освобождает вычислительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="18d78-118">`azure vm stop` does not release the compute resources.</span></span> <span data-ttu-id="18d78-119">Чтобы освободить вычислительные ресурсы, используйте `azure vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="18d78-119">To release compute resources, use `azure vm deallocate`.</span></span> <span data-ttu-id="18d78-120">Для расширения виртуального жесткого диска следует отменить распределение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="18d78-120">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="18d78-121">Обновите размер неуправляемого диска ОС, используя команду `azure vm set`.</span><span class="sxs-lookup"><span data-stu-id="18d78-121">Update the size of the unmanaged OS disk using the `azure vm set` command.</span></span> <span data-ttu-id="18d78-122">В следующем примере выполняется обновление виртуальной машины *myVM*, входящей в группу ресурсов с именем *myResourceGroup*, до *50* ГБ.</span><span class="sxs-lookup"><span data-stu-id="18d78-122">The following example updates the VM named *myVM* in the resource group named *myResourceGroup* to be *50* GB:</span></span>

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. <span data-ttu-id="18d78-123">Запустите виртуальную машину следующим образом:</span><span class="sxs-lookup"><span data-stu-id="18d78-123">Start your VM as follows:</span></span>

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="18d78-124">Подключитесь к виртуальной машине по протоколу SSH, используя соответствующие учетные данные.</span><span class="sxs-lookup"><span data-stu-id="18d78-124">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="18d78-125">Чтобы проверить, изменился ли размер диска операционной системы, используйте `df -h`.</span><span class="sxs-lookup"><span data-stu-id="18d78-125">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="18d78-126">В следующем примере выходных данных показано, что теперь размер основного раздела (*/dev/sda1*) составляет 50 ГБ:</span><span class="sxs-lookup"><span data-stu-id="18d78-126">The following example output shows the primary partition (*/dev/sda1*) is now 50 GB:</span></span>

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a><span data-ttu-id="18d78-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18d78-127">Next steps</span></span>
<span data-ttu-id="18d78-128">Если вам требуется дополнительное место для хранения, можно также [добавить диски данных в виртуальную машину Linux](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="18d78-128">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="18d78-129">Дополнительные сведения о шифровании диска см. в статье [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md) (Шифрование дисков на виртуальной машине Linux с помощью Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="18d78-129">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
