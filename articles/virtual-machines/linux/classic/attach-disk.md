---
title: "aaaAttach tooa диска виртуальной Машины Linux в Azure | Документы Microsoft"
description: "Узнайте, как tooattach данных на диске tooa виртуальных Машин Linux с помощью hello классического развертывания модели и инициализируется hello диск, поэтому он будет готов к использованию"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a>Как tooAttach tooa диска данных виртуальной машины Linux
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. В разделе как слишком[присоединить диск данных с помощью модели развертывания диспетчера ресурсов hello](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Можно присоединить пустые диски и диски, содержащие данные tooyour виртуальных машинах Azure. В обоих случаях диски — это VHD-файлы, которые размещаются в учетной записи хранения Azure. Как и при добавлении любой компьютер Linux tooa диска после присоединения диска hello требуется tooinitialize и отформатировать его, поэтому он будет готов к использованию. Этой статьи описаны присоединении пустые диски и диски, уже содержащий данных tooyour виртуальные машины, а также как toothen инициализация и форматирование нового диска.

> [!NOTE]
> Это лучший подход toouse, один или несколько разделения toostore дисков данных виртуальной машины. При создании виртуальной машины Azure у нее есть диск для операционной системы и временный диск. **Не используйте hello временный диск toostore постоянных данных.** Как hello названия, он предоставляет только временное хранилище. Этот диск не обеспечивает избыточности или резервного копирования, поскольку он не размещается в хранилище Azure.
> временный диск Hello обычно управляется hello Azure Linux Agent и автоматическое подключение слишком**/mnt/resource** (или **/mnt** Ubuntu изображений). На Здравствуйте другой стороны, диск данных может называться ядре Linux hello примерно `/dev/sdc`, и необходимо toopartition, форматирования и подключить этот ресурс. В разделе hello [руководство пользователя агента Azure Linux] [ Agent] подробные сведения.
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a>Инициализация нового диска данных в Linux
1. Tooyour SSH виртуальной Машины. Дополнительные сведения см. в разделе [как toolog на tooa виртуальной машине под управлением Linux][Logon].
2. Затем следует записать идентификатор устройства hello toofind для tooinitialize диска данных hello. Существует два способа toodo:
   
    ) Grep для устройств SCSI в hello записывает в журнал, например, как hello следующую команду:
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    Для последних Ubuntu распределений, может потребоваться toouse `sudo grep SCSI /var/log/syslog` так, как ведение журнала слишком`/var/log/messages` могут быть отключены по умолчанию.
   
    Можно определить идентификатор hello hello последний диск, который был добавлен в отображаемые сообщения hello.
   
    ![Получение сообщений hello диска](./media/attach-disk/scsidisklog.png)
   
    ИЛИ
   
    b) используйте hello `lsscsi` toofind команду out hello идентификатор устройства. `lsscsi` можно установить с помощью `yum install lsscsi` (Red Hat в основе распределения) или `apt-get install lsscsi` (Debian в основе распределения). Можно найти диск hello, вы ищете, его *lun* или **логический номер устройства**. Например, hello *lun* для hello дисков вы можете легко увидеть из `azure vm disk list <virtual-machine>` как:

    ```azurecli
    azure vm disk list myVM
    ```

    Hello выходные данные выглядят аналогично toohello следующее:

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    Сравнение этих данных с помощью hello выходные данные `lsscsi` hello же образцы виртуальной машины:
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    Номер последней Hello в кортеже hello в каждой строке — hello *lun*. Дополнительные сведения см. в `man lsscsi`.
3. В строке приветствия типа hello следующая команда toocreate устройства:
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. При появлении запроса введите  **n**  toocreate секции.

    ![Создание устройства](./media/attach-disk/fdisknewpartition.png)

5. При появлении запроса введите **p** toomake hello секции hello основного раздела. Тип **1** toomake его hello первую секцию, а затем введите введите значение по умолчанию hello tooaccept цилиндр hello. В некоторых системах можно отображать значения по умолчанию hello hello первым и hello последнего секторов, вместо цилиндр hello. Вы можете tooaccept эти значения по умолчанию.

    ![Создание раздела](./media/attach-disk/fdisknewpartdetails.png)


6. Тип **p** toosee hello сведения о диске hello, во время разбиения.

    ![Просмотр сведений о диске](./media/attach-disk/fdiskpartitiondetails.png)


7. Тип **w** toowrite параметрах hello hello диска.

    ![Запись изменений на дисках hello](./media/attach-disk/fdiskwritedisk.png)

8. Теперь можно создавать на новую секцию hello hello файловой системы. Добавьте код номеров устройства toohello hello секции (в следующий пример hello `/dev/sdc1`). Hello следующий пример создает ext4 раздел на /dev/sdc1:
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Создание файловой системы](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > Системы SuSE Linux Enterprise 11 поддерживают доступ только для чтения в файловых системах ext4. Для этих систем рекомендуется tooformat hello новая файловая система ext3 вместо ext4.

9. Сделайте каталог toomount hello новая файловая система, следующим образом:
   
    ```bash
    sudo mkdir /datadrive
    ```

10. Наконец можно подключить диск hello, следующим образом:
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    Hello диск данных становится готова toouse как **/datadrive**.
   
    ![Создать диск hello hello каталога и подключения](./media/attach-disk/mkdirandmount.png)

11. Добавьте hello нового диска слишком/и т. д/fstab:
   
    tooensure hello диск будет подключена снова автоматически, после перезагрузки, он должен быть добавлен файл/etc/fstab toohello. Кроме того настоятельно рекомендуется этого hello UUID (глобально уникальный идентификатор) используется в/etc/fstab toorefer toohello диск, а не просто имя (т. е. /dev/sdc1) устройства hello. Использование hello UUID позволяет избежать hello неправильной диска, подключенного tooa заданное место в случае, если hello ОС обнаружении ошибки во время загрузки и все остальные диски с данными, затем назначено их идентификаторы устройств. toofind Здравствуйте UUID hello новый диск, можно использовать hello **блок идентификатором blkid** программы:
   
    ```bash
    sudo -i blkid
    ```
   
    Hello выходные данные выглядят аналогично toohello в следующем примере:
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > Неправильное редактирование hello **/etc/fstab** файла может привести к невозможности загрузки системы. Если нет уверенности, сведения о этот файл, как изменять tooproperly см toohello распространения документации. Также рекомендуется, прежде чем изменять создается резервная копия файл/etc/fstab hello.

    Затем откройте hello **/etc/fstab** файл в текстовом редакторе:

    ```bash
    sudo vi /etc/fstab
    ```

    В этом примере мы используем значение hello UUID для hello новый **/dev/sdc1** устройства, который был создан в предыдущих шагах hello и hello монтирования **/datadrive**. Добавьте следующие строки toohello конец hello hello **/etc/fstab** файла:

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    Или в системах на базе ОС SuSE Linux, может потребоваться toouse немного другой формат:

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > Hello `nofail` параметр гарантирует, что hello, Виртуальная машина, даже если hello файловой системы повреждены или hello диск не существует во время загрузки. Без этого параметра могут возникнуть поведение, как описано в [нельзя SSH tooLinux виртуальной Машины из-за ошибки tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).

    Теперь можно проверить, что подключено hello файловой системе надлежащим образом отключением и затем снова подключать hello файловой системы, т. е. При использовании точки подключения пример hello `/datadrive` в hello ранее шаги:

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    Если hello `mount` команда выведет сообщение об ошибке, проверьте hello файле/etc/fstab для правильного синтаксиса. При создании дополнительных дисков данных и разделов также введите их в файл /etc/fstab отдельно.

    Сделать доступным для записи hello диска с помощью следующей команды:

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > Впоследствии удалении диска данных без необходимости редактирования fstab может привести к tooboot toofail hello виртуальной Машины. Если это обычное дело большинством дистрибутивов предоставляют либо hello `nofail` и/или `nobootwait` fstab параметры, позволяющие tooboot системы даже в случае сбоя диска hello toomount во время загрузки. Дополнительные сведения об этих параметрах см. в документации дистрибутива.

### <a name="trimunmap-support-for-linux-in-azure"></a>Поддержка операций TRIM и UNMAP для Linux в Azure
Некоторые версии Linux ядра поддержки TRIM и отмене СОПОСТАВЛЕНИЯ операций toodiscard неиспользуемые блоки на диске hello. Эти операции, в первую очередь используются в tooinform стандартное хранилище Azure, которая удалена страницы становятся недействительными и может быть удален. Удаление страниц позволит сократить затраты, если вы создаете большие файлы, а затем удаляете их.

Существует два способа tooenable TRIM поддержки в ВМ Linux. Как обычно см. на распределение hello рекомендованный подход:

* Используйте hello `discard` подключить параметр в `/etc/fstab`, например:

    ```sh
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
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a>Дальнейшие действия
Можно прочитать подробнее об использовании ВМ Linux в hello в следующих статьях:

* [Как toolog на tooa виртуальной машине под управлением Linux][Logon]
* [Как toodetach диск от виртуальной машины Linux](detach-disk.md)
* [С помощью Azure CLI hello hello классической модели развертывания](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Настройка программного RAID-массива в Linux](../configure-raid.md)
* [Настройка диспетчера логических томов на виртуальной машине Linux в Azure](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
