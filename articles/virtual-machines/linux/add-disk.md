---
title: "Добавление диска в виртуальную машину Linux с помощью Azure CLI | Документация Майкрософт"
description: "Узнайте, как добавить постоянный диск в виртуальную машину Linux с помощью Azure CLI 1.0 и Azure CLI 2.0."
keywords: "виртуальная машина Linux, добавление диска ресурсов"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 3005a066-7a84-4dc5-bdaa-574c75e6e411
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 02/02/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 185dd276cd79cb7053605d651e8ecdc7fd1e7636
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-disk-to-a-linux-vm"></a><span data-ttu-id="fec43-104">Добавление диска к виртуальной машине Linux</span><span class="sxs-lookup"><span data-stu-id="fec43-104">Add a disk to a Linux VM</span></span>
<span data-ttu-id="fec43-105">Из этой статьи вы узнаете, как добавить в виртуальную машину постоянный диск, на котором можно хранить данные. Эти данные сохранятся даже после повторной подготовки виртуальной машины (например, в ходе обслуживания или изменения размера).</span><span class="sxs-lookup"><span data-stu-id="fec43-105">This article shows how to attach a persistent disk to your VM so that you can preserve your data - even if your VM is reprovisioned due to maintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="fec43-106">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="fec43-106">Quick Commands</span></span>
<span data-ttu-id="fec43-107">В следующем примере к виртуальной машине `myVM` в группе ресурсов `myResourceGroup` подключается диск на `50` ГБ:</span><span class="sxs-lookup"><span data-stu-id="fec43-107">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="fec43-108">Использование управляемых дисков:</span><span class="sxs-lookup"><span data-stu-id="fec43-108">To use managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="fec43-109">Использование неуправляемых дисков:</span><span class="sxs-lookup"><span data-stu-id="fec43-109">To use unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="fec43-110">Подключение управляемого диска</span><span class="sxs-lookup"><span data-stu-id="fec43-110">Attach a managed disk</span></span>

<span data-ttu-id="fec43-111">Используя Управляемые диски, вы сможете сосредоточиться на виртуальных машинах и дисках, не беспокоясь об учетных записях хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="fec43-111">Using managed disks enables you to focus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="fec43-112">Вы можете быстро создать и подключить управляемый диск к виртуальной машине, используя одну и ту же группу ресурсов Azure, или создать диски в любом количестве, а затем подключить их.</span><span class="sxs-lookup"><span data-stu-id="fec43-112">You can quickly create and attach a managed disk to a VM using the same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-to-a-vm"></a><span data-ttu-id="fec43-113">Подключение нового диска к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="fec43-113">Attach a new disk to a VM</span></span>

<span data-ttu-id="fec43-114">Если вам просто нужен новый диск в виртуальной машине, можно использовать команду `az vm disk attach`.</span><span class="sxs-lookup"><span data-stu-id="fec43-114">If you just need a new disk on your VM, you can use the `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="fec43-115">Подключение существующего диска</span><span class="sxs-lookup"><span data-stu-id="fec43-115">Attach an existing disk</span></span> 

<span data-ttu-id="fec43-116">Во многих случаях подключаются созданные диски.</span><span class="sxs-lookup"><span data-stu-id="fec43-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="fec43-117">Сначала нужно найти идентификатор диска и передать его в команду `az vm disk attach`.</span><span class="sxs-lookup"><span data-stu-id="fec43-117">You first find the disk id and then pass that to the `az vm disk attach` command.</span></span> <span data-ttu-id="fec43-118">В следующем примере используется диск, созданный с помощью команды `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="fec43-118">The following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find the disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="fec43-119">Результат выглядит примерно следующим образом (для форматирования результатов можно использовать параметр `-o table` для любой команды):</span><span class="sxs-lookup"><span data-stu-id="fec43-119">The output looks something like the following (you can use the `-o table` option to any command to format the output in ):</span></span>

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Empty",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": null,
    "storageAccountId": null
  },
  "diskSizeGb": 50,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/rasquill-script/providers/Microsoft.Compute/disks/myDataDisk",
  "location": "westus",
  "name": "myDataDisk",
  "osType": null,
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-02T23:35:47.708082+00:00",
  "type": "Microsoft.Compute/disks"
}
```


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="fec43-120">Подключение неуправляемого диска</span><span class="sxs-lookup"><span data-stu-id="fec43-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="fec43-121">Вы можете очень быстро подключить новый диск, если у вас не вызывает проблем создание диска в той же учетной записи хранения, которая используется для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="fec43-121">Attaching a new disk is quick if you do not mind creating a disk in the same storage account as your VM.</span></span> <span data-ttu-id="fec43-122">Чтобы создать и присоединить новый диск (ГБ) для своей виртуальной машины, введите `azure vm disk attach-new`.</span><span class="sxs-lookup"><span data-stu-id="fec43-122">Type `azure vm disk attach-new` to create and attach a new GB disk for your VM.</span></span> <span data-ttu-id="fec43-123">Если учетная запись хранения не определяется явным образом, любой создаваемый диск помещается в ту же учетную запись хранения, что и диск операционной системы.</span><span class="sxs-lookup"><span data-stu-id="fec43-123">If you do not explicitly identify a storage account, any disk you create is placed in the same storage account where your OS disk resides.</span></span> <span data-ttu-id="fec43-124">В следующем примере к виртуальной машине `myVM` в группе ресурсов `myResourceGroup` подключается диск на `50` ГБ:</span><span class="sxs-lookup"><span data-stu-id="fec43-124">The following example attaches a `50`GB disk to the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-to-the-linux-vm-to-mount-the-new-disk"></a><span data-ttu-id="fec43-125">Подключение к виртуальной машине Linux для подключения нового диска</span><span class="sxs-lookup"><span data-stu-id="fec43-125">Connect to the Linux VM to mount the new disk</span></span>
> [!NOTE]
> <span data-ttu-id="fec43-126">В этом разделе для подключения к виртуальной машине используются имена пользователей и пароли.</span><span class="sxs-lookup"><span data-stu-id="fec43-126">This topic connects to a VM using usernames and passwords.</span></span> <span data-ttu-id="fec43-127">Чтобы использовать пары открытых и закрытых ключей для взаимодействия с виртуальной машиной, см. статью [об использовании ключей SSH для Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fec43-127">To use public and private key pairs to communicate with your VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="fec43-128">Чтобы разбить диск на разделы, отформатировать и подключить его к виртуальной машине Linux, к ВМ Azure нужно подключиться по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="fec43-128">You need to SSH into your Azure VM to partition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="fec43-129">Если вы не знакомы с подключением по протоколу **ssh**, команда имеет вид `ssh <username>@<FQDNofAzureVM> -p <the ssh port>`. В конечном итоге она выглядит вот так:</span><span class="sxs-lookup"><span data-stu-id="fec43-129">If you're not familiar with connecting with **ssh**, the command takes the form `ssh <username>@<FQDNofAzureVM> -p <the ssh port>`, and looks like the following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="fec43-130">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="fec43-130">Output</span></span>

```bash
The authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) to the list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome to Ubuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

* Documentation:  https://help.ubuntu.com/

System information as of Fri May 22 21:02:32 UTC 2015

System load: 0.37              Memory usage: 2%   Processes:       207
Usage of /:  41.4% of 1.94GB   Swap usage:   0%   Users logged in: 0

Graph this data and manage this system at:
  https://landscape.canonical.com/

Get cloud support with Ubuntu Advantage Cloud Guest:
  http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ops@myVM:~$
```

<span data-ttu-id="fec43-131">После того как вы подключились к своей виртуальной машине, вы можете присоединить диск.</span><span class="sxs-lookup"><span data-stu-id="fec43-131">Now that you're connected to your VM, you're ready to attach a disk.</span></span>  <span data-ttu-id="fec43-132">Сначала найдите диск, используя `dmesg | grep SCSI` (для обнаружения нового диска можно использовать и другой способ).</span><span class="sxs-lookup"><span data-stu-id="fec43-132">First find the disk, using `dmesg | grep SCSI` (the method you use to discover your new disk may vary).</span></span> <span data-ttu-id="fec43-133">В этом случае отобразится примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="fec43-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="fec43-134">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="fec43-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="fec43-135">а в контексте этого раздела диск `sdc` является именно тем диском, который мы ищем.</span><span class="sxs-lookup"><span data-stu-id="fec43-135">and in the case of this topic, the `sdc` disk is the one that we want.</span></span> <span data-ttu-id="fec43-136">Теперь разобьем диск с помощью `sudo fdisk /dev/sdc`, предположив, что в нашем случае был диск `sdc`, установим его как основной диск в разделе 1 и примем остальные значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="fec43-136">Now partition the disk with `sudo fdisk /dev/sdc` -- assuming that in your case the disk was `sdc`, and make it a primary disk on partition 1, and accept the other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="fec43-137">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="fec43-137">Output</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide to write them.
After that, of course, the previous content won't be recoverable.

Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

Command (m for help): n
Partition type:
   p   primary (0 primary, 0 extended, 4 free)
   e   extended
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-10485759, default 2048):
Using default value 2048
Last sector, +sectors or +size{K,M,G} (2048-10485759, default 10485759):
Using default value 10485759
```

<span data-ttu-id="fec43-138">Создайте раздел, введя в командной строке `p` :</span><span class="sxs-lookup"><span data-stu-id="fec43-138">Create the partition by typing `p` at the prompt:</span></span>

```bash
Command (m for help): p

Disk /dev/sdc: 5368 MB, 5368709120 bytes
255 heads, 63 sectors/track, 652 cylinders, total 10485760 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x2a59b123

   Device Boot      Start         End      Blocks   Id  System
/dev/sdc1            2048    10485759     5241856   83  Linux

Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.
```

<span data-ttu-id="fec43-139">Запишите файловую систему на раздел с помощью команды **mkfs** , указав тип вашей файловой системы и имя устройства.</span><span class="sxs-lookup"><span data-stu-id="fec43-139">And write a file system to the partition by using the **mkfs** command, specifying your filesystem type and the device name.</span></span> <span data-ttu-id="fec43-140">В этом разделе мы будем использовать указанные `ext4` и `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="fec43-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="fec43-141">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="fec43-141">Output</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=1342177280
40 block groups
32768 blocks per group, 32768 fragments per group
8192 inodes per group
Superblock backups stored on blocks:
    32768, 98304, 163840, 229376, 294912, 819200, 884736
Allocating group tables: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and filesystem accounting information: done
```

<span data-ttu-id="fec43-142">Теперь создадим каталог для подключения файловой системы, используя `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="fec43-142">Now we create a directory to mount the file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="fec43-143">А для подключения каталога используйте `mount`:</span><span class="sxs-lookup"><span data-stu-id="fec43-143">And you mount the directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="fec43-144">Теперь диск данных готов для использования как `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="fec43-144">The data disk is now ready to use as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="fec43-145">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="fec43-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="fec43-146">Чтобы обеспечить автоматическое повторное подключение диска после перезагрузки, его необходимо добавить в файл /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="fec43-146">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="fec43-147">Кроме того, для ссылки на диск настоятельно рекомендуется использовать в файле /etc/fstab идентификатор UUID (глобальный уникальный идентификатор), а не просто имя устройства (например, `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="fec43-147">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="fec43-148">Если операционная система обнаруживает ошибку диска во время загрузки, использование UUID позволяет избежать подключения ошибочного диска в это расположение.</span><span class="sxs-lookup"><span data-stu-id="fec43-148">If the OS detects a disk error during boot, using the UUID avoids the incorrect disk being mounted to a given location.</span></span> <span data-ttu-id="fec43-149">Остальные диски с данными затем получают те же идентификаторы устройств.</span><span class="sxs-lookup"><span data-stu-id="fec43-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="fec43-150">Чтобы найти UUID нового диска, используйте программу **blkid** :</span><span class="sxs-lookup"><span data-stu-id="fec43-150">To find the UUID of the new drive, use the **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="fec43-151">Результат будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="fec43-151">The output looks similar to the following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="fec43-152">Некорректное изменение файла **/etc/fstab** может привести к невозможности загрузить систему.</span><span class="sxs-lookup"><span data-stu-id="fec43-152">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="fec43-153">Если у вас есть сомнения, см. инструкции по правильному изменению этого файла в документации дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="fec43-153">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="fec43-154">Также рекомендуется перед внесением изменений создать резервную копию файла /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="fec43-154">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="fec43-155">Затем откройте файл **/etc/fstab** в текстовом редакторе:</span><span class="sxs-lookup"><span data-stu-id="fec43-155">Next, open the **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="fec43-156">В этом примере мы используем значение UUID для нового устройства **/dev/sdc1**, созданного на предыдущих шагах, и точку подключения **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="fec43-156">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="fec43-157">Добавьте следующую строку в конец файла **/etc/fstab** :</span><span class="sxs-lookup"><span data-stu-id="fec43-157">Add the following line to the end of the **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="fec43-158">Если вы позднее удалите диск данных без редактирования файла fstab, виртуальная машина может не загрузиться.</span><span class="sxs-lookup"><span data-stu-id="fec43-158">Later removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="fec43-159">Большинство дистрибутивов содержат `nofail` или `nobootwait` параметры fstab.</span><span class="sxs-lookup"><span data-stu-id="fec43-159">Most distributions provide either the `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="fec43-160">Эти параметры позволяют системе загружаться, даже если диск не подключится во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="fec43-160">These options allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="fec43-161">Дополнительные сведения об этих параметрах см. в документации дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="fec43-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="fec43-162">Параметр **nofail** обеспечивает запуск виртуальной машины даже в том случае, если файловая система повреждена или отсутствует диск во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="fec43-162">The **nofail** option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="fec43-163">Без этого параметра может возникнуть ситуация, описанная в записи блога [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/) (Не удается подключиться к виртуальной машине Linux по протоколу SSH из-за ошибок FSTAB).</span><span class="sxs-lookup"><span data-stu-id="fec43-163">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="fec43-164">Поддержка операций TRIM и UNMAP для Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="fec43-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="fec43-165">Некоторые ядра Linux поддерживают операции TRIM и UNMAP для отмены неиспользуемых блоков на диске.</span><span class="sxs-lookup"><span data-stu-id="fec43-165">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="fec43-166">Это особенно удобно использовать в хранилище уровня "Стандартный", чтобы сообщать Azure о том, что удаленные страницы больше не действительны и могут быть удалены.</span><span class="sxs-lookup"><span data-stu-id="fec43-166">This is primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="fec43-167">Это позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="fec43-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="fec43-168">Существует два способа включить поддержку операций TRIM в виртуальной машине Linux.</span><span class="sxs-lookup"><span data-stu-id="fec43-168">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="fec43-169">Как обычно, обратитесь к документации дистрибутива, чтобы выбрать рекомендуемый метод.</span><span class="sxs-lookup"><span data-stu-id="fec43-169">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="fec43-170">Используйте параметр подключения `discard` в `/etc/fstab`. Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="fec43-170">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="fec43-171">В некоторых случаях параметр `discard` может негативно влиять на производительность.</span><span class="sxs-lookup"><span data-stu-id="fec43-171">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="fec43-172">Кроме того, вы можете вручную выполнить команду `fstrim` из командной строки или добавить ее в crontab для регулярного выполнения.</span><span class="sxs-lookup"><span data-stu-id="fec43-172">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="fec43-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="fec43-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="fec43-174">**RHEL или CentOS**</span><span class="sxs-lookup"><span data-stu-id="fec43-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="fec43-175">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="fec43-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="fec43-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fec43-176">Next Steps</span></span>
* <span data-ttu-id="fec43-177">Помните, для того чтобы после перезапуска виртуальная машина получила доступ к новому диску, информацию о нем необходимо прописать в файле [fstab](http://en.wikipedia.org/wiki/Fstab) .</span><span class="sxs-lookup"><span data-stu-id="fec43-177">Remember, that your new disk is not available to the VM if it reboots unless you write that information to your [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="fec43-178">Ознакомьтесь с рекомендациями по [оптимизации производительности виртуальной машины Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , чтобы правильно настроить виртуальную машину Linux.</span><span class="sxs-lookup"><span data-stu-id="fec43-178">To ensure your Linux VM is configured correctly, review the [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="fec43-179">Увеличьте емкость хранилища, добавив дополнительные диски, и [настройте RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="fec43-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

