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
# <a name="add-a-disk-tooa-linux-vm"></a>Добавить диск tooa ВМ Linux
В этой статье показано tooattach a постоянного места на диске tooyour виртуальной Машины, чтобы их можно сохранить данные — даже если ВМ выполняется повторная Подготовка из-за toomaintenance или изменения размера. 

## <a name="quick-commands"></a>Быстрые команды
Следующий пример присоединяет Hello `50`toohello ГБ диска виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:

toouse управляемый дисков.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

неуправляемые toouse диски:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="attach-a-managed-disk"></a>Подключение управляемого диска

С помощью управляемых дисков можно toofocus на виртуальные машины и их диски, не беспокоясь об учетных записях хранения Azure. Можно быстро создать и присоединить управляемого диска виртуальной Машины с помощью tooa hello одной группе ресурсов Azure, или можно создать любое количество дисков, а затем подключите их.


### <a name="attach-a-new-disk-tooa-vm"></a>Подключите новый tooa диска виртуальной Машины

Если необходимо просто нового диска на виртуальной Машине, можно использовать hello `az vm disk attach` команды.

```azurecli
az vm disk attach -g myResourceGroup --vm-name myVM --disk myDataDisk \
  --new --size-gb 50
```

### <a name="attach-an-existing-disk"></a>Подключение существующего диска 

Во многих случаях подключаются созданные диски. Сначала найти диска с идентификатором hello и затем передать этот toohello `az vm disk attach` команды. Hello следующий пример использует дисков, созданных с помощью `az disk create -g myResourceGroup -n myDataDisk --size-gb 50`.

```azurecli
# find hello disk id
diskId=$(az disk show -g myResourceGroup -n myDataDisk --query 'id' -o tsv)
az vm disk attach -g myResourceGroup --vm-name myVM --disk $diskId
```

Hello выходные данные выглядят примерно hello следующим образом (можно использовать hello `-o table` параметр вывода tooany команды tooformat hello в):

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


## <a name="attach-an-unmanaged-disk"></a>Подключение неуправляемого диска

Подключение нового диска занимает мало времени, если создание диска в hello же учетной записи хранилища виртуальной Машины. Тип `azure vm disk attach-new` toocreate и присоединить новый диск ГБ для виртуальной Машины. Если учетной записи хранилища не определить явным образом, любой созданный диск помещается в hello же учетной записи хранилища, где находится на диске операционной системы. Следующий пример присоединяет Hello `50`toohello ГБ диска виртуальной Машины с именем `myVM` в группе ресурсов hello с именем `myResourceGroup`:

```azurecli
az vm unmanaged-disk attach -g myResourceGroup -n myUnmanagedDisk --vm-name myVM \
  --new --size-gb 50
```

## <a name="connect-toohello-linux-vm-toomount-hello-new-disk"></a>Подключение нового диска ВМ Linux toomount hello toohello
> [!NOTE]
> В этом разделе подключается tooa виртуальной Машины с использованием имен пользователей и паролей. toouse toocommunicate пары открытого и закрытого ключей с ВМ, в разделе [как tooUse SSH с Linux в Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
> 
> 

Требуется tooSSH в toopartition вашей виртуальной Машине Azure, форматирования и подключить новый диск, чтобы ВМ Linux можно было использовать. Если вы не знакомы с подключением с **ssh**, hello команда принимает форму hello `ssh <username>@<FQDNofAzureVM> -p <hello ssh port>`и выглядит hello следующим образом:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com -p 22
```

Выходные данные

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

Теперь, когда вы подключены tooyour ВМ, вы будете готовы tooattach диска.  Сначала найти hello диск с использованием `dmesg | grep SCSI` (метод hello использовать toodiscover могут различаться на новый диск). В этом случае отобразится примерно следующее:

```bash
dmesg | grep SCSI
```

Выходные данные

```bash
[    0.294784] SCSI subsystem initialized
[    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
[    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
[    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
[ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
```

и в случае hello этого раздела hello `sdc` диск является hello, нам нужно. Создать разделы на диске hello сейчас с `sudo fdisk /dev/sdc` — при условии, что в вашей вариантов hello диск был `sdc`и сделать его основной диск на секции 1 и примите другие значения по умолчанию hello.

```bash
sudo fdisk /dev/sdc
```

Выходные данные

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

Создание раздела hello, введя `p` в строке приветствия:

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

И записи файловой системы toohello раздела с помощью hello **mkfs** команду, указав имя файловой системы типа и hello устройства. В этом разделе мы будем использовать указанные `ext4` и `/dev/sdc1`:

```bash
sudo mkfs -t ext4 /dev/sdc1
```

Выходные данные

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

Теперь создадим каталог toomount hello файл системы с помощью `mkdir`:

```bash
sudo mkdir /datadrive
```

И подключить hello каталога с использованием `mount`:

```bash
sudo mount /dev/sdc1 /datadrive
```

Hello диск данных становится готова toouse как `/datadrive`.

```bash
ls
```

Выходные данные

```bash
bin   datadrive  etc   initrd.img  lib64       media  opt   root  sbin  sys  usr  vmlinuz
boot  dev        home  lib         lost+found  mnt    proc  run   srv   tmp  var
```

tooensure hello диск будет подключена снова автоматически, после перезагрузки, он должен быть добавлен файл/etc/fstab toohello. Кроме того, настоятельно рекомендуется, hello UUID (глобально уникальный идентификатор) используется в/etc/fstab toorefer toohello диска вместо просто hello имя устройства (такие как `/dev/sdc1`). Если hello ОС обнаружении ошибки во время загрузки, с помощью hello UUID позволяет избежать hello неправильной диска, подключенного tooa заданное место. Остальные диски с данными затем получают те же идентификаторы устройств. toofind hello UUID hello новый диск, используйте hello **блок идентификатором blkid** программы:

```bash
sudo -i blkid
```

Hello выходные данные выглядят аналогично toohello следующее:

```bash
/dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
/dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
/dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
```

> [!NOTE]
> Неправильное редактирование hello **/etc/fstab** файла может привести к невозможности загрузки системы. Если нет уверенности, сведения о этот файл, как изменять tooproperly см toohello распространения документации. Также рекомендуется, прежде чем изменять создается резервная копия файл/etc/fstab hello.
> 
> 

Затем откройте hello **/etc/fstab** файл в текстовом редакторе:

```bash
sudo vi /etc/fstab
```

В этом примере мы используем значение hello UUID для hello новый **/dev/sdc1** устройства, который был создан в предыдущих шагах hello и hello монтирования **/datadrive**. Добавьте следующие строки toohello конец hello hello **/etc/fstab** файла:

```bash
UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
```

> [!NOTE]
> Позже удалении диска данных без необходимости редактирования fstab может привести к tooboot toofail hello виртуальной Машины. Большинством дистрибутивов предоставляют либо hello `nofail` и/или `nobootwait` fstab параметры. Эти параметры позволяют tooboot системы даже в случае сбоя диска hello toomount во время загрузки. Дополнительные сведения об этих параметрах см. в документации дистрибутива.
> 
> Hello **nofail** параметр гарантирует, что hello, Виртуальная машина, даже если hello файловой системы повреждены или hello диск не существует во время загрузки. Без этого параметра могут возникнуть поведение, как описано в [нельзя SSH tooLinux виртуальной Машины из-за ошибки tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)

### <a name="trimunmap-support-for-linux-in-azure"></a>Поддержка операций TRIM и UNMAP для Linux в Azure
Некоторые версии Linux ядра поддержки TRIM и отмене СОПОСТАВЛЕНИЯ операций toodiscard неиспользуемые блоки на диске hello. Это полезно в tooinform стандартное хранилище Azure, которая удалена страницы становятся недействительными и может быть удален. Это позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.

Существует два способа tooenable TRIM поддержки в ВМ Linux. Как обычно см. на распределение hello рекомендованный подход:

* Используйте hello `discard` подключить параметр в `/etc/fstab`, например:

    ```bash
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```
* В некоторых случаях hello `discard` параметра может негативно сказаться на производительности. Кроме того, можно запустить hello `fstrim` вручную команды из командной строки hello, или добавьте его tooyour crontab toorun регулярно:
  
    **Ubuntu**
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    **RHEL или CentOS**

    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a>Устранение неполадок
[!INCLUDE [virtual-machines-linux-lunzero](../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Дальнейшие действия
* Помните, что новый диск не доступные toohello ВМ Если будет перезагружен, если только не используется, tooyour сведения [fstab](http://en.wikipedia.org/wiki/Fstab) файла.
* ВМ Linux tooensure настроен неправильно, просмотрите hello [оптимизации производительности компьютера Linux](optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) рекомендации.
* Увеличьте емкость хранилища, добавив дополнительные диски, и [настройте RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) для повышения производительности.

