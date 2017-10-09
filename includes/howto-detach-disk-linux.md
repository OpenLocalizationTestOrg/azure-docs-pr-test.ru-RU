Если вам больше не требуется диск, который является вложенного tooa виртуальной машины (VM), можно легко отключить ее. При отсоединении диска от виртуальной Машины hello hello диск не удалено из хранилища. Если требуется toouse hello существующие данные на диске hello, вам может быть повторно присоединена toohello одной виртуальной Машины, так и любой другой.  

> [!NOTE]
> Виртуальная машина в Azure использует различные типы дисков, такие как диск с операционной системой, локальный временный диск и дополнительные диски данных. Дополнительные сведения см. в статье [О дисках и виртуальных жестких дисках для виртуальных машин Azure](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Невозможно отсоединить диск операционной системы, пока не будут также удалены hello виртуальной Машины.

## <a name="find-hello-disk"></a>Найти диск hello
Перед тем как отсоединить диск от виртуальной Машины необходимо toofind out hello номер LUN, который является идентификатор hello диск toobe отсоединена. toodo, выполните следующие действия:

1. Откройте Azure CLI и [подключения tooyour подписки Azure](../articles/xplat-cli-connect.md). Убедитесь, что вы находитесь в режиме управления службами Azure (`azure config mode asm`).
2. Узнайте, какие диски, присоединенные tooyour виртуальной Машины. Hello следующий пример выводит диски для виртуальной Машины с именем hello `myVM`:

    ```azurecli
    azure vm disk list myVM
    ```

    Hello вывода будет примерно toohello следующий пример:

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. Обратите внимание, hello LUN или hello **логический номер устройства** для нужных toodetach диска hello.

## <a name="remove-operating-system-references-toohello-disk"></a>Удалите диск toohello ссылки операционной системы
Перед отсоединением hello диск от виртуальной машине Linux hello, следует убедиться, что все разделы на диске hello не используются. Убедитесь в этой операционной системе и hello не пытаться tooremount их после перезагрузки. Эти действия отменить конфигурации hello, скорее всего, созданной при [присоединение](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello диска.

1. Используйте hello `lsscsi` идентификатор диска hello toodiscover команды. Вы можете установить `lsscsi` с помощью `yum install lsscsi` (в дистрибутивах на основе Red Hat) или `apt-get install lsscsi` (в дистрибутивах на основе Debian). Можно найти идентификатор hello диска, который вы ищете, используя номер LUN hello. Номер последней Hello в кортеже hello в каждой строке — hello LUN. В следующий пример из hello `lsscsi`, LUN 0 соответствует слишком*иметь идентификатор/dev/sdc*

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. Используйте `fdisk -l <disk>` toodiscover hello секций, связанных с toobe диска hello отсоединена. Hello следующий пример показывает hello выходные `/dev/sdc`:

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. Отключите каждой секции, перечисленные для hello диска. Hello следующий пример отсоединяет диск `/dev/sdc1`:

    ```bash
    sudo umount /dev/sdc1
    ```

4. Используйте hello `blkid` команда toodiscovery hello UUID для всех секций. Hello вывода будет примерно toohello следующий пример:

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. Удалить записи из hello **/etc/fstab** файла, связанного с путей hello устройств или UUID для всех секций, toobe диск hello отсоединена.  Записи в этом примере могут быть такими:

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    или
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a>Отсоединить диск hello
Обнаружив hello номера LUN дисковых hello и ссылки на удаленные hello операционной системы, вы будете готовы toodetach его:

1. Отсоединение hello выбранный диск из виртуальной машины hello, выполнив команду hello `azure vm disk detach
   <virtual-machine-name> <LUN>`. Hello следующий пример отсоединяет LUN `0` из виртуальной Машины с именем hello `myVM`:
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. Можно проверить, если диск hello получен отсоединяется, запустив `azure vm disk list` еще раз. Следующий пример проверяет Hello hello виртуальной Машины с именем `myVM`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Hello выходных данных примерно toohello следующий пример, в котором показано, что диск hello данных больше не подключен:

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

Hello отсоединить диск остается в хранилище, но больше не является tooa подключенных виртуальных машин.

