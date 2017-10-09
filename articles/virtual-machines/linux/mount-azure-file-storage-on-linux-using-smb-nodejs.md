---
title: "хранилище файлов Azure на виртуальных машинах Linux по протоколу SMB с помощью Azure CLI 1.0 aaaMount | Документы Microsoft"
description: "Как toomount хранилище файлов Azure на виртуальных машинах Linux с помощью SMB"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="84451-103">Подключение хранилища файлов Azure на виртуальных машинах Linux по протоколу SMB с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="84451-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="84451-104">В этой статье показано, как toomount хранилища Azure File на виртуальной Машине Linux с помощью hello протокола Server Message Block (SMB).</span><span class="sxs-lookup"><span data-stu-id="84451-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="84451-105">Хранилище файлов предлагает общих файловых ресурсов в облаке hello через hello стандартного протокола SMB.</span><span class="sxs-lookup"><span data-stu-id="84451-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="84451-106">Существуют следующие требования Hello.</span><span class="sxs-lookup"><span data-stu-id="84451-106">hello requirements are:</span></span>

* <span data-ttu-id="84451-107">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="84451-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* <span data-ttu-id="84451-108">[файлы открытого и закрытого ключей Secure Shell (SSH)](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="84451-108">[Secure Shell (SSH) public and private key files](mac-create-ssh-keys.md)</span></span>

## <a name="cli-versions-toouse"></a><span data-ttu-id="84451-109">Toouse версии CLI</span><span class="sxs-lookup"><span data-stu-id="84451-109">CLI versions toouse</span></span>
<span data-ttu-id="84451-110">Hello задачу можно выполнить с помощью одного из hello следующие версии интерфейса командной строки (CLI):</span><span class="sxs-lookup"><span data-stu-id="84451-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="84451-111">[Azure CLI 1.0](#quick-commands) — нашей CLI для hello классический и ресурса управления развертывания моделей (в этой статье)</span><span class="sxs-lookup"><span data-stu-id="84451-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="84451-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-нашей нового поколения CLI для модели развертывания hello ресурсов управления</span><span class="sxs-lookup"><span data-stu-id="84451-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="84451-113">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="84451-113">Quick commands</span></span>
<span data-ttu-id="84451-114">Задача hello tooaccomplish быстро, выполните действия hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="84451-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="84451-115">Более подробные сведения и контекста, начинаются с Привет [«Подробное пошаговое руководство»](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) раздела.</span><span class="sxs-lookup"><span data-stu-id="84451-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="84451-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="84451-116">Prerequisites</span></span>
* <span data-ttu-id="84451-117">Группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="84451-117">A resource group</span></span>
* <span data-ttu-id="84451-118">Виртуальная сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="84451-118">An Azure virtual network</span></span>
* <span data-ttu-id="84451-119">Группа безопасности сети с входящим трафиком SSH.</span><span class="sxs-lookup"><span data-stu-id="84451-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="84451-120">Подсеть.</span><span class="sxs-lookup"><span data-stu-id="84451-120">A subnet</span></span>
* <span data-ttu-id="84451-121">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="84451-121">An Azure storage account</span></span>
* <span data-ttu-id="84451-122">Ключи учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="84451-122">Azure storage account keys</span></span>
* <span data-ttu-id="84451-123">Общая папка хранилища файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="84451-123">An Azure File storage share</span></span>
* <span data-ttu-id="84451-124">Виртуальная машина Linux.</span><span class="sxs-lookup"><span data-stu-id="84451-124">A Linux VM</span></span>

<span data-ttu-id="84451-125">Замените все примеры параметров своими параметрами.</span><span class="sxs-lookup"><span data-stu-id="84451-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="84451-126">Создайте каталог для локального подключения hello</span><span class="sxs-lookup"><span data-stu-id="84451-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="84451-127">Подключить файл hello хранилища общей папки SMB toohello точки подключения</span><span class="sxs-lookup"><span data-stu-id="84451-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="84451-128">Сохранение подключения hello после перезагрузки</span><span class="sxs-lookup"><span data-stu-id="84451-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="84451-129">Добавить слишком следующей строкой hello`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="84451-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="84451-130">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="84451-130">Detailed walkthrough</span></span>

<span data-ttu-id="84451-131">Хранилище файлов предлагает общих файловых ресурсов в облаке hello, использующих hello стандартного протокола SMB.</span><span class="sxs-lookup"><span data-stu-id="84451-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="84451-132">С hello последний выпуск хранилища файлов можно также подключить общий файловый ресурс с любой ОС, которая поддерживает SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="84451-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="84451-133">При использовании подключения SMB в Linux, вы получаете легко резервные копии tooa надежный, постоянный архивирования место хранения, поддерживаемый соглашения об уровне ОБСЛУЖИВАНИЯ.</span><span class="sxs-lookup"><span data-stu-id="84451-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="84451-134">Перенос файлов из монтирования SMB tooan виртуальная машина, размещенная в хранилище файлов — журналы toodebug хорошим способом.</span><span class="sxs-lookup"><span data-stu-id="84451-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="84451-135">Это потому, что общий ресурс SMB же hello могут быть подключены локально tooyour рабочей станции Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="84451-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="84451-136">SMB не hello наилучшим решением для потоковой передачи Linux или журналы приложений в режиме реального времени, так как протокол SMB hello не построен toohandle таких обязанностей интенсивной ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="84451-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="84451-137">Вместо SMB для сбора выходных данных журналов Linux и приложений лучше использовать специальный единый инструмент, работающий на уровне ведения журналов, например Fluentd.</span><span class="sxs-lookup"><span data-stu-id="84451-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="84451-138">Для Подробное пошаговое руководство мы создание необходимых компонентов hello необходимости toofirst создать hello общей папки хранилища, а затем подключать через SMB на виртуальной Машине Linux.</span><span class="sxs-lookup"><span data-stu-id="84451-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="84451-139">Создайте учетную запись хранилища Azure с помощью hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="84451-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="84451-140">Показать hello ключи учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="84451-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="84451-141">При создании учетной записи хранилища, hello ключи учетной записи создаются попарно, чтобы они могут быть повернуты без нарушения работы службы.</span><span class="sxs-lookup"><span data-stu-id="84451-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="84451-142">При переключении toohello второго ключа в паре "hello", вы создаете новую пару ключей.</span><span class="sxs-lookup"><span data-stu-id="84451-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="84451-143">Новых ключей учетной записи хранения всегда создаются попарно, убедитесь, что всегда существует по крайней мере один неиспользуемое пространство ключей готов tooswitch для.</span><span class="sxs-lookup"><span data-stu-id="84451-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="84451-144">ключи учетной записи хранения hello tooshow использовать hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="84451-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="84451-145">Создание общей папки хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="84451-145">Create hello File storage share.</span></span>

    <span data-ttu-id="84451-146">Hello общей папки хранилища содержит общий ресурс SMB hello.</span><span class="sxs-lookup"><span data-stu-id="84451-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="84451-147">Квота Hello всегда выражается в гигабайтах (ГБ).</span><span class="sxs-lookup"><span data-stu-id="84451-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="84451-148">toocreate hello общей папки хранилища, выполните следующий код hello.</span><span class="sxs-lookup"><span data-stu-id="84451-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="84451-149">Создайте каталог hello точки подключения.</span><span class="sxs-lookup"><span data-stu-id="84451-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="84451-150">Необходимо создать локальный каталог в hello Linux файл системы toomount hello в общей папке SMB.</span><span class="sxs-lookup"><span data-stu-id="84451-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="84451-151">Запись или чтение из каталога hello локального подключения, направляются toohello общий ресурс SMB, размещенного в хранилище файлов.</span><span class="sxs-lookup"><span data-stu-id="84451-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="84451-152">каталог toocreate hello, hello используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="84451-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="84451-153">Подключите hello в общей папке SMB, с помощью hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="84451-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="84451-154">Сохранение hello подключения SMB работу после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="84451-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="84451-155">После перезагрузки виртуальной Машины с Linux hello hello подключенного общей папки SMB отключается во время завершения работы.</span><span class="sxs-lookup"><span data-stu-id="84451-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="84451-156">tooremount hello общий ресурс SMB во время загрузки, необходимо добавить строку toohello/etc/fstab Linux.</span><span class="sxs-lookup"><span data-stu-id="84451-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="84451-157">Linux использует hello fstab файл toolist hello файловых систем, он должен toomount во время процесса загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="84451-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="84451-158">Добавление общей папки SMB hello гарантирует, что в этой общей папки хранилища hello является постоянно подключенных файловой системы для виртуальной Машины с Linux hello.</span><span class="sxs-lookup"><span data-stu-id="84451-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="84451-159">Добавление общей папки SMB tooa для hello файла хранения новой виртуальной Машины можно при использовании облачных init.</span><span class="sxs-lookup"><span data-stu-id="84451-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="84451-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="84451-160">Next steps</span></span>

- [<span data-ttu-id="84451-161">С помощью toocustomize init облака виртуальной Машины Linux во время создания</span><span class="sxs-lookup"><span data-stu-id="84451-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="84451-162">Добавить диск tooa ВМ Linux</span><span class="sxs-lookup"><span data-stu-id="84451-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="84451-163">Шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="84451-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
