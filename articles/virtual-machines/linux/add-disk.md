---
title: "Здравствуйте, aaaAdd ВМ tooLinux диска с помощью Azure CLI | Документы Microsoft"
description: "Узнайте tooadd tooyour дисков для долгосрочного хранения виртуальных Машин Linux с hello Azure CLI 1.0 и 2.0."
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
ms.openlocfilehash: 0dc5236be62d96b70dd47a7f621f626a037e22aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-disk-tooa-linux-vm"></a><span data-ttu-id="bae10-104">Добавить диск tooa ВМ Linux</span><span class="sxs-lookup"><span data-stu-id="bae10-104">Add a disk tooa Linux VM</span></span>
<span data-ttu-id="bae10-105">В этой статье показано tooattach a постоянного места на диске tooyour виртуальной Машины, чтобы их можно сохранить данные — даже если ВМ выполняется повторная Подготовка из-за toomaintenance или изменения размера.</span><span class="sxs-lookup"><span data-stu-id="bae10-105">This article shows how tooattach a persistent disk tooyour VM so that you can preserve your data - even if your VM is reprovisioned due toomaintenance or resizing.</span></span> 

## <a name="quick-commands"></a><span data-ttu-id="bae10-106">Быстрые команды</span><span class="sxs-lookup"><span data-stu-id="bae10-106">Quick Commands</span></span>
<span data-ttu-id="bae10-107">Следующий пример присоединяет Hello `50`toohello ГБ диска виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="bae10-107">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

<span data-ttu-id="bae10-108">toouse управляемый дисков.</span><span class="sxs-lookup"><span data-stu-id="bae10-108">toouse managed disks:</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

<span data-ttu-id="bae10-109">неуправляемые toouse диски:</span><span class="sxs-lookup"><span data-stu-id="bae10-109">toouse unmanaged disks:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a><span data-ttu-id="bae10-110">Подключение управляемого диска</span><span class="sxs-lookup"><span data-stu-id="bae10-110">Attach a managed disk</span></span>

<span data-ttu-id="bae10-111">С помощью управляемых дисков можно toofocus на виртуальные машины и их диски, не беспокоясь об учетных записях хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="bae10-111">Using managed disks enables you toofocus on your VMs and their disks without worrying about Azure Storage accounts.</span></span> <span data-ttu-id="bae10-112">Можно быстро создать и присоединить управляемого диска виртуальной Машины с помощью tooa hello одной группе ресурсов Azure, или можно создать любое количество дисков, а затем подключите их.</span><span class="sxs-lookup"><span data-stu-id="bae10-112">You can quickly create and attach a managed disk tooa VM using hello same Azure resource group, or you can create any number of disks and then attach them.</span></span>


### <a name="attach-a-new-disk-tooa-vm"></a><span data-ttu-id="bae10-113">Подключите новый tooa диска виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="bae10-113">Attach a new disk tooa VM</span></span>

<span data-ttu-id="bae10-114">Если необходимо просто нового диска на виртуальной Машине, можно использовать hello `az vm disk attach` команды.</span><span class="sxs-lookup"><span data-stu-id="bae10-114">If you just need a new disk on your VM, you can use hello `az vm disk attach` command.</span></span>

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a><span data-ttu-id="bae10-115">Подключение существующего диска</span><span class="sxs-lookup"><span data-stu-id="bae10-115">Attach an existing disk</span></span> 

<span data-ttu-id="bae10-116">Во многих случаях подключаются созданные диски.</span><span class="sxs-lookup"><span data-stu-id="bae10-116">In many cases you attach disks that have already been created.</span></span> <span data-ttu-id="bae10-117">Сначала найти диска с идентификатором hello и затем передать этот toohello `az vm disk attach` команды.</span><span class="sxs-lookup"><span data-stu-id="bae10-117">You first find hello disk id and then pass that toohello `az vm disk attach` command.</span></span> <span data-ttu-id="bae10-118">Hello следующий пример использует дисков, созданных с помощью `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span><span class="sxs-lookup"><span data-stu-id="bae10-118">hello following example uses a disk created with `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.</span></span>

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

<span data-ttu-id="bae10-119">Hello выходные данные выглядят примерно hello следующим образом (можно использовать hello `-o table` параметр вывода tooany команды tooformat hello в):</span><span class="sxs-lookup"><span data-stu-id="bae10-119">hello output looks something like hello following (you can use hello `-o table` option tooany command tooformat hello output in ):</span></span>

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


## <a name="attach-an-unmanaged-disk"></a><span data-ttu-id="bae10-120">Подключение неуправляемого диска</span><span class="sxs-lookup"><span data-stu-id="bae10-120">Attach an unmanaged disk</span></span>

<span data-ttu-id="bae10-121">Подключение нового диска занимает мало времени, если создание диска в hello же учетной записи хранилища виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bae10-121">Attaching a new disk is quick if you do not mind creating a disk in hello same storage account as your VM.</span></span> <span data-ttu-id="bae10-122">Тип `azure vm disk attach-new` toocreate и присоединить новый диск ГБ для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bae10-122">Type `azure vm disk attach-new` toocreate and attach a new GB disk for your VM.</span></span> <span data-ttu-id="bae10-123">Если учетной записи хранилища не определить явным образом, любой созданный диск помещается в hello же учетной записи хранилища, где находится на диске операционной системы.</span><span class="sxs-lookup"><span data-stu-id="bae10-123">If you do not explicitly identify a storage account, any disk you create is placed in hello same storage account where your OS disk resides.</span></span> <span data-ttu-id="bae10-124">Следующий пример присоединяет Hello `50`toohello ГБ диска виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="bae10-124">hello following example attaches a `50`GB disk toohello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a><span data-ttu-id="bae10-125">Подключение нового диска ВМ Linux toomount hello toohello</span><span class="sxs-lookup"><span data-stu-id="bae10-125">Connect toohello Linux VM toomount hello new disk</span></span>
> [!NOTE]
> <span data-ttu-id="bae10-126">В этом разделе подключается tooa виртуальной Машины с использованием имен пользователей и паролей.</span><span class="sxs-lookup"><span data-stu-id="bae10-126">This topic connects tooa VM using usernames and passwords.</span></span> <span data-ttu-id="bae10-127">toouse toocommunicate пары открытого и закрытого ключей с ВМ, в разделе [как tooUse SSH с Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bae10-127">toouse public and private key pairs toocommunicate with your VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 
> 
> 

<span data-ttu-id="bae10-128">Требуется tooSSH в toopartition вашей виртуальной Машине Azure, форматирования и подключить новый диск, чтобы ВМ Linux можно было использовать.</span><span class="sxs-lookup"><span data-stu-id="bae10-128">You need tooSSH into your Azure VM toopartition, format, and mount your new disk so your Linux VM can use it.</span></span> <span data-ttu-id="bae10-129">Если вы не знакомы с подключением с **ssh**, hello команда принимает форму hello `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`и выглядит hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bae10-129">If you're not familiar with connecting with **ssh**, hello command takes hello form `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`, and looks like hello following:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

<span data-ttu-id="bae10-130">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="bae10-130">Output</span></span>

```bash
hello authenticity of host 'mypublicdns.westus.cloudapp.azure.com (191.239.51.1)' can't be established.
ECDSA key fingerprint is bx:xx:xx:xx:xx:xx:xx:xx:xx:x:x:x:x:x:x:xx.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.westus.cloudapp.azure.com,191.239.51.1' (ECDSA) toohello list of known hosts.
ops@mypublicdns.westus.cloudapp.azure.com's password:
Welcome tooUbuntu 14.04.2 LTS (GNU/Linux 3.16.0-37-generic x86_64)

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

hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

ops@myVM:~$
```

<span data-ttu-id="bae10-131">Теперь, когда вы подключены tooyour ВМ, вы будете готовы tooattach диска.</span><span class="sxs-lookup"><span data-stu-id="bae10-131">Now that you're connected tooyour VM, you're ready tooattach a disk.</span></span>  <span data-ttu-id="bae10-132">Сначала найти hello диск с использованием `dmesg | grep SCSI` (метод hello использовать toodiscover могут различаться на новый диск).</span><span class="sxs-lookup"><span data-stu-id="bae10-132">First find hello disk, using `dmesg | grep SCSI` (hello method you use toodiscover your new disk may vary).</span></span> <span data-ttu-id="bae10-133">В этом случае отобразится примерно следующее:</span><span class="sxs-lookup"><span data-stu-id="bae10-133">In this case, it looks something like:</span></span>

```bash
dmesg | grep SCSI
```

<span data-ttu-id="bae10-134">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="bae10-134">Output</span></span>

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

<span data-ttu-id="bae10-135">и в случае hello этого раздела hello `sdc` диск является hello, нам нужно.</span><span class="sxs-lookup"><span data-stu-id="bae10-135">and in hello case of this topic, hello `sdc` disk is hello one that we want.</span></span> <span data-ttu-id="bae10-136">Создать разделы на диске hello сейчас с `sudo fdisk /dev/sdc` — при условии, что в вашей вариантов hello диск был `sdc`и сделать его основной диск на секции 1 и примите другие значения по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="bae10-136">Now partition hello disk with `sudo fdisk /dev/sdc` -- assuming that in your case hello disk was `sdc`, and make it a primary disk on partition 1, and accept hello other defaults.</span></span>

```bash
sudo fdisk /dev/sdc
```

<span data-ttu-id="bae10-137">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="bae10-137">Output</span></span>

```bash
Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
Building a new DOS disklabel with disk identifier 0x2a59b123.
Changes will remain in memory only, until you decide toowrite them.
After that, of course, hello previous content won't be recoverable.

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

<span data-ttu-id="bae10-138">Создание раздела hello, введя `p` в строке приветствия:</span><span class="sxs-lookup"><span data-stu-id="bae10-138">Create hello partition by typing `p` at hello prompt:</span></span>

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
hello partition table has been altered!

Calling ioctl() toore-read partition table.
Syncing disks.
```

<span data-ttu-id="bae10-139">И записи файловой системы toohello раздела с помощью hello **mkfs** команду, указав имя файловой системы типа и hello устройства.</span><span class="sxs-lookup"><span data-stu-id="bae10-139">And write a file system toohello partition by using hello **mkfs** command, specifying your filesystem type and hello device name.</span></span> <span data-ttu-id="bae10-140">В этом разделе мы будем использовать указанные `ext4` и `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="bae10-140">In this topic, we're using `ext4` and `/dev/sdc1` from above:</span></span>

```bash
sudo mkfs -t ext4 /dev/sdc1
```

<span data-ttu-id="bae10-141">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="bae10-141">Output</span></span>

```bash
mke2fs 1.42.9 (4-Feb-2014)
Discarding device blocks: done
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
Stride=0 blocks, Stripe width=0 blocks
327680 inodes, 1310464 blocks
65523 blocks (5.00%) reserved for hello super user
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

<span data-ttu-id="bae10-142">Теперь создадим каталог toomount hello файл системы с помощью `mkdir`:</span><span class="sxs-lookup"><span data-stu-id="bae10-142">Now we create a directory toomount hello file system using `mkdir`:</span></span>

```bash
sudo mkdir /datadrive
```

<span data-ttu-id="bae10-143">И подключить hello каталога с использованием `mount`:</span><span class="sxs-lookup"><span data-stu-id="bae10-143">And you mount hello directory using `mount`:</span></span>

```bash
sudo mount /dev/sdc1 /datadrive
```

<span data-ttu-id="bae10-144">Hello диск данных становится готова toouse как `/datadrive`.</span><span class="sxs-lookup"><span data-stu-id="bae10-144">hello data disk is now ready toouse as `/datadrive`.</span></span>

```bash
ls
```

<span data-ttu-id="bae10-145">Выходные данные</span><span class="sxs-lookup"><span data-stu-id="bae10-145">Output</span></span>

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

<span data-ttu-id="bae10-146">tooensure hello диск будет подключена снова автоматически, после перезагрузки, он должен быть добавлен файл/etc/fstab toohello.</span><span class="sxs-lookup"><span data-stu-id="bae10-146">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="bae10-147">Кроме того, настоятельно рекомендуется, hello UUID (глобально уникальный идентификатор) используется в/etc/fstab toorefer toohello диска вместо просто hello имя устройства (такие как `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="bae10-147">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (such as, `/dev/sdc1`).</span></span> <span data-ttu-id="bae10-148">Если hello ОС обнаружении ошибки во время загрузки, с помощью hello UUID позволяет избежать hello неправильной диска, подключенного tooa заданное место.</span><span class="sxs-lookup"><span data-stu-id="bae10-148">If hello OS detects a disk error during boot, using hello UUID avoids hello incorrect disk being mounted tooa given location.</span></span> <span data-ttu-id="bae10-149">Остальные диски с данными затем получают те же идентификаторы устройств.</span><span class="sxs-lookup"><span data-stu-id="bae10-149">Remaining data disks would then be assigned those same device IDs.</span></span> <span data-ttu-id="bae10-150">toofind hello UUID hello новый диск, используйте hello **блок идентификатором blkid** программы:</span><span class="sxs-lookup"><span data-stu-id="bae10-150">toofind hello UUID of hello new drive, use hello **blkid** utility:</span></span>

```bash
sudo -i blkid
```

<span data-ttu-id="bae10-151">Hello выходные данные выглядят аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="bae10-151">hello output looks similar toohello following:</span></span>

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> <span data-ttu-id="bae10-152">Неправильное редактирование hello **/etc/fstab** файла может привести к невозможности загрузки системы.</span><span class="sxs-lookup"><span data-stu-id="bae10-152">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="bae10-153">Если нет уверенности, сведения о этот файл, как изменять tooproperly см toohello распространения документации.</span><span class="sxs-lookup"><span data-stu-id="bae10-153">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="bae10-154">Также рекомендуется, прежде чем изменять создается резервная копия файл/etc/fstab hello.</span><span class="sxs-lookup"><span data-stu-id="bae10-154">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>
> 
> 

<span data-ttu-id="bae10-155">Затем откройте hello **/etc/fstab** файл в текстовом редакторе:</span><span class="sxs-lookup"><span data-stu-id="bae10-155">Next, open hello **/etc/fstab** file in a text editor:</span></span>

```bash
sudo vi /etc/fstab
```

<span data-ttu-id="bae10-156">В этом примере мы используем значение hello UUID для hello новый **/dev/sdc1** устройства, который был создан в предыдущих шагах hello и hello монтирования **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="bae10-156">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="bae10-157">Добавьте следующие строки toohello конец hello hello **/etc/fstab** файла:</span><span class="sxs-lookup"><span data-stu-id="bae10-157">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> <span data-ttu-id="bae10-158">Позже удалении диска данных без необходимости редактирования fstab может привести к tooboot toofail hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bae10-158">Later removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="bae10-159">Большинством дистрибутивов предоставляют либо hello `nofail` и/или `nobootwait` fstab параметры.</span><span class="sxs-lookup"><span data-stu-id="bae10-159">Most distributions provide either hello `nofail` and/or `nobootwait` fstab options.</span></span> <span data-ttu-id="bae10-160">Эти параметры позволяют tooboot системы даже в случае сбоя диска hello toomount во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="bae10-160">These options allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="bae10-161">Дополнительные сведения об этих параметрах см. в документации дистрибутива.</span><span class="sxs-lookup"><span data-stu-id="bae10-161">Consult your distribution's documentation for more information on these parameters.</span></span>
> 
> <span data-ttu-id="bae10-162">Hello **nofail** параметр гарантирует, что hello, Виртуальная машина, даже если hello файловой системы повреждены или hello диск не существует во время загрузки.</span><span class="sxs-lookup"><span data-stu-id="bae10-162">hello **nofail** option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="bae10-163">Без этого параметра могут возникнуть поведение, как описано в [нельзя SSH tooLinux виртуальной Машины из-за ошибки tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span><span class="sxs-lookup"><span data-stu-id="bae10-163">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="bae10-164">Поддержка операций TRIM и UNMAP для Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="bae10-164">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="bae10-165">Некоторые версии Linux ядра поддержки TRIM и отмене СОПОСТАВЛЕНИЯ операций toodiscard неиспользуемые блоки на диске hello.</span><span class="sxs-lookup"><span data-stu-id="bae10-165">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="bae10-166">Это полезно в tooinform стандартное хранилище Azure, которая удалена страницы становятся недействительными и может быть удален.</span><span class="sxs-lookup"><span data-stu-id="bae10-166">This is primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="bae10-167">Это позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.</span><span class="sxs-lookup"><span data-stu-id="bae10-167">This can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="bae10-168">Существует два способа tooenable TRIM поддержки в ВМ Linux.</span><span class="sxs-lookup"><span data-stu-id="bae10-168">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="bae10-169">Как обычно см. на распределение hello рекомендованный подход:</span><span class="sxs-lookup"><span data-stu-id="bae10-169">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="bae10-170">Используйте hello `discard` подключить параметр в `/etc/fstab`, например:</span><span class="sxs-lookup"><span data-stu-id="bae10-170">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* <span data-ttu-id="bae10-171">В некоторых случаях hello `discard` параметра может негативно сказаться на производительности.</span><span class="sxs-lookup"><span data-stu-id="bae10-171">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="bae10-172">Кроме того, можно запустить hello `fstrim` вручную команды из командной строки hello, или добавьте его tooyour crontab toorun регулярно:</span><span class="sxs-lookup"><span data-stu-id="bae10-172">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="bae10-173">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="bae10-173">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="bae10-174">**RHEL или CentOS**</span><span class="sxs-lookup"><span data-stu-id="bae10-174">**RHEL/CentOS**</span></span>

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="bae10-175">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="bae10-175">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="bae10-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bae10-176">Next Steps</span></span>
* <span data-ttu-id="bae10-177">Помните, что новый диск не доступные toohello ВМ Если будет перезагружен, если только не используется, tooyour сведения [fstab](http://en.wikipedia.org/wiki/Fstab) файла.</span><span class="sxs-lookup"><span data-stu-id="bae10-177">Remember, that your new disk is not available toohello VM if it reboots unless you write that information tooyour [fstab](http://en.wikipedia.org/wiki/Fstab) file.</span></span>
* <span data-ttu-id="bae10-178">ВМ Linux tooensure настроен неправильно, просмотрите hello [оптимизации производительности компьютера Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) рекомендации.</span><span class="sxs-lookup"><span data-stu-id="bae10-178">tooensure your Linux VM is configured correctly, review hello [Optimize your Linux machine performance](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) recommendations.</span></span>
* <span data-ttu-id="bae10-179">Увеличьте емкость хранилища, добавив дополнительные диски, и [настройте RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) для повышения производительности.</span><span class="sxs-lookup"><span data-stu-id="bae10-179">Expand your storage capacity by adding additional disks and [configure RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional performance.</span></span>

