---
title: "хранилище файлов Azure на виртуальных машинах Linux с помощью SMB aaaMount | Документы Microsoft"
description: "Как toomount хранилище файлов Azure на виртуальных машинах Linux с помощью SMB с hello Azure CLI 2.0"
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="0d099-103">Подключение хранилища файлов Azure на виртуальных машинах Linux с помощью протокола SMB</span><span class="sxs-lookup"><span data-stu-id="0d099-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="0d099-104">В этой статье показано, как подключить hello tooutilize службы хранилища Azure файла на виртуальной Машине Linux с помощью SMB с hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="0d099-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="0d099-105">Хранилище файлов Azure предлагает общих файловых ресурсов в облаке hello, с помощью стандартного протокола SMB hello.</span><span class="sxs-lookup"><span data-stu-id="0d099-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="0d099-106">Можно также выполнить следующие действия с hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d099-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0d099-107">Существуют следующие требования Hello.</span><span class="sxs-lookup"><span data-stu-id="0d099-107">hello requirements are:</span></span>

- <span data-ttu-id="0d099-108">[учетная запись Azure](https://azure.microsoft.com/pricing/free-trial/);</span><span class="sxs-lookup"><span data-stu-id="0d099-108">[an Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
- <span data-ttu-id="0d099-109">[файлы открытого и закрытого ключа SSH](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="0d099-109">[SSH public and private key files](mac-create-ssh-keys.md)</span></span>

## <a name="quick-commands"></a><span data-ttu-id="0d099-110">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="0d099-110">Quick Commands</span></span>

* <span data-ttu-id="0d099-111">Группа ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0d099-111">A resource group</span></span>
* <span data-ttu-id="0d099-112">Виртуальная сеть Azure.</span><span class="sxs-lookup"><span data-stu-id="0d099-112">An Azure virtual network</span></span>
* <span data-ttu-id="0d099-113">Группа безопасности сети с входящим трафиком SSH.</span><span class="sxs-lookup"><span data-stu-id="0d099-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="0d099-114">Подсеть.</span><span class="sxs-lookup"><span data-stu-id="0d099-114">A subnet</span></span>
* <span data-ttu-id="0d099-115">Учетная запись хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="0d099-115">An Azure storage account</span></span>
* <span data-ttu-id="0d099-116">Ключи учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="0d099-116">Azure storage account keys</span></span>
* <span data-ttu-id="0d099-117">Общая папка хранилища файлов Azure.</span><span class="sxs-lookup"><span data-stu-id="0d099-117">An Azure File storage share</span></span>
* <span data-ttu-id="0d099-118">Виртуальная машина Linux.</span><span class="sxs-lookup"><span data-stu-id="0d099-118">A Linux VM</span></span>

<span data-ttu-id="0d099-119">Замените все примеры параметров своими параметрами.</span><span class="sxs-lookup"><span data-stu-id="0d099-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="0d099-120">Создайте каталог для локального подключения hello</span><span class="sxs-lookup"><span data-stu-id="0d099-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="0d099-121">Подключить файл hello хранилища общей папки SMB toohello точки подключения</span><span class="sxs-lookup"><span data-stu-id="0d099-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="0d099-122">Сохранение подключения hello после перезагрузки</span><span class="sxs-lookup"><span data-stu-id="0d099-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="0d099-123">toodo таким образом, добавьте следующие строки toohello hello `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="0d099-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0d099-124">Подробное пошаговое руководство</span><span class="sxs-lookup"><span data-stu-id="0d099-124">Detailed walkthrough</span></span>

<span data-ttu-id="0d099-125">Хранилище файлов предлагает общих файловых ресурсов в облаке hello, использующих hello стандартного протокола SMB.</span><span class="sxs-lookup"><span data-stu-id="0d099-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="0d099-126">С hello последний выпуск хранилища файлов можно также подключить общий файловый ресурс с любой ОС, которая поддерживает SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="0d099-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="0d099-127">При использовании подключения SMB в Linux, вы получаете легко резервные копии tooa надежный, постоянный архивирования место хранения, поддерживаемый соглашения об уровне ОБСЛУЖИВАНИЯ.</span><span class="sxs-lookup"><span data-stu-id="0d099-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="0d099-128">Перенос файлов из монтирования SMB tooan виртуальная машина, размещенная в хранилище файлов — журналы toodebug хорошим способом.</span><span class="sxs-lookup"><span data-stu-id="0d099-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="0d099-129">Это потому, что общий ресурс SMB же hello могут быть подключены локально tooyour рабочей станции Windows, Mac или Linux.</span><span class="sxs-lookup"><span data-stu-id="0d099-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="0d099-130">SMB не hello наилучшим решением для потоковой передачи Linux или журналы приложений в режиме реального времени, так как протокол SMB hello не построен toohandle таких обязанностей интенсивной ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="0d099-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="0d099-131">Вместо SMB для сбора выходных данных журналов Linux и приложений лучше использовать специальный единый инструмент, работающий на уровне ведения журналов, например Fluentd.</span><span class="sxs-lookup"><span data-stu-id="0d099-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="0d099-132">Для Подробное пошаговое руководство мы создание необходимых компонентов hello необходимости toofirst создать hello общей папки хранилища, а затем подключать через SMB на виртуальной Машине Linux.</span><span class="sxs-lookup"><span data-stu-id="0d099-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="0d099-133">Создание группы ресурсов с [Создание группы az](/cli/azure/group#create) toohold hello общей папки.</span><span class="sxs-lookup"><span data-stu-id="0d099-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="0d099-134">Группа ресурсов с именем toocreate `myResourceGroup` в hello расположение «West US», используйте следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="0d099-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="0d099-135">Создать учетную запись хранилища Azure с [создания учетной записи хранилища az](/cli/azure/storage/account#create) toostore hello сами файлы.</span><span class="sxs-lookup"><span data-stu-id="0d099-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="0d099-136">toocreate учетной записи хранилища с именем mystorageaccount с помощью хранилища Standard_LRS hello SKU, hello используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="0d099-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="0d099-137">Показать hello ключи учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0d099-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="0d099-138">При создании учетной записи хранилища, hello ключи учетной записи создаются попарно, чтобы они могут быть повернуты без нарушения работы службы.</span><span class="sxs-lookup"><span data-stu-id="0d099-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="0d099-139">При переключении toohello второго ключа в паре "hello", вы создаете новую пару ключей.</span><span class="sxs-lookup"><span data-stu-id="0d099-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="0d099-140">Новых ключей учетной записи хранения всегда создаются попарно, убедитесь, что всегда существует по крайней мере один неиспользуемое пространство учетной записи ключа готов tooswitch для.</span><span class="sxs-lookup"><span data-stu-id="0d099-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="0d099-141">Просмотреть ключи учетной записи хранения hello с hello [список ключей учетной записи хранилища az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="0d099-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="0d099-142">Здравствуйте, ключи учетной записи с именем hello `mystorageaccount` , перечислены в hello в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="0d099-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="0d099-143">tooextract один ключ, используйте hello `--query` флаг.</span><span class="sxs-lookup"><span data-stu-id="0d099-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="0d099-144">Hello следующий пример извлекает первый ключ hello (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="0d099-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="0d099-145">Создание общей папки хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="0d099-145">Create hello File storage share.</span></span>

    <span data-ttu-id="0d099-146">Hello общей папки хранилища содержит общий ресурс SMB с hello [создать общую папку хранилища az](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="0d099-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="0d099-147">Квота Hello всегда выражается в гигабайтах (ГБ).</span><span class="sxs-lookup"><span data-stu-id="0d099-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="0d099-148">Передачи в одном из разделов hello из предыдущего hello `az storage account keys list` команды.</span><span class="sxs-lookup"><span data-stu-id="0d099-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="0d099-149">Создайте папку с именем mystorageshare с квотой 10 ГБ, используя следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="0d099-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="0d099-150">Создайте каталог точек подключения.</span><span class="sxs-lookup"><span data-stu-id="0d099-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="0d099-151">Создает локальный каталог в hello Linux файл системы toomount hello в общей папке SMB.</span><span class="sxs-lookup"><span data-stu-id="0d099-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="0d099-152">Запись или чтение из каталога hello локального подключения, направляются toohello общий ресурс SMB, размещенного в хранилище файлов.</span><span class="sxs-lookup"><span data-stu-id="0d099-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="0d099-153">toocreate локального каталога в/mnt/mymountdirectory, hello используйте следующий пример:</span><span class="sxs-lookup"><span data-stu-id="0d099-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="0d099-154">Подключите локального каталога общей папки SMB toohello hello.</span><span class="sxs-lookup"><span data-stu-id="0d099-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="0d099-155">Укажите имя пользователя учетной записи хранилища и ключ учетной записи хранения для учетных данных подключения hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0d099-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="0d099-156">Сохранение hello подключения SMB работу после перезагрузки.</span><span class="sxs-lookup"><span data-stu-id="0d099-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="0d099-157">После перезагрузки виртуальной Машины с Linux hello hello подключенного общей папки SMB отключается во время завершения работы.</span><span class="sxs-lookup"><span data-stu-id="0d099-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="0d099-158">hello tooremount общей папке SMB, во время загрузки, добавьте строку toohello/etc/fstab Linux.</span><span class="sxs-lookup"><span data-stu-id="0d099-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="0d099-159">Linux использует hello fstab файл toolist hello файловых систем, он должен toomount во время процесса загрузки hello.</span><span class="sxs-lookup"><span data-stu-id="0d099-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="0d099-160">Добавление общей папки SMB hello гарантирует, что в этой общей папки хранилища hello является постоянно подключенных файловой системы для виртуальной Машины с Linux hello.</span><span class="sxs-lookup"><span data-stu-id="0d099-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="0d099-161">Добавление общей папки SMB tooa для hello файла хранения новой виртуальной Машины можно при использовании облачных init.</span><span class="sxs-lookup"><span data-stu-id="0d099-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="0d099-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0d099-162">Next steps</span></span>

- [<span data-ttu-id="0d099-163">С помощью toocustomize init облака виртуальной Машины Linux во время создания</span><span class="sxs-lookup"><span data-stu-id="0d099-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="0d099-164">Добавить диск tooa ВМ Linux</span><span class="sxs-lookup"><span data-stu-id="0d099-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="0d099-165">Шифрование дисков на виртуальной Машине Linux с помощью hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0d099-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
