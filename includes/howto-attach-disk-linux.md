
Дополнительные сведения о дисках см. в разделе [О дисках и виртуальных жестких дисках для виртуальных машин Azure](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>Подключение пустого диска
1. Откройте Azure CLI 1.0 и [подключения tooyour подписки Azure](../articles/xplat-cli-connect.md). Убедитесь, что вы находитесь в режиме управления службами Azure (`azure config mode asm`).
2. Введите `azure vm disk attach-new` toocreate и присоединить новый диск, как показано в следующий пример hello. Замените *myVM* с именем hello вашей виртуальной машины Linux и укажите размер hello hello диска в ГБ, что является *100 ГБ* в этом примере:

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. После создания и присоединенного диска данных hello, это отображается в выходных данных hello `azure vm disk list <virtual-machine-name>` как показано в следующий пример hello:
   
    ```azurecli
    azure vm disk list TestVM
    ```

    Hello вывода будет примерно toohello следующий пример:

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>Подключение существующего диска
Для подключения существующего диска требуется VHD-файл в учетной записи хранения.

1. Откройте Azure CLI 1.0 и [подключения tooyour подписки Azure](../articles/xplat-cli-connect.md). Убедитесь, что вы находитесь в режиме управления службами Azure (`azure config mode asm`).
2. Проверьте, если hello VHD, вы хотите tooattach уже отправлен tooyour подписки Azure.
   
    ```azurecli
    azure vm disk list
    ```

    Hello вывода будет примерно toohello следующий пример:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Если не удается найти диск hello, требуется toouse, локальные подписки tooyour виртуального жесткого диска может быть отправлен с помощью `azure vm disk create` или `azure vm disk upload`. Пример `disk create` бы как hello в следующем примере:
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    Hello вывода будет примерно toohello следующий пример:

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   Можно также использовать `azure vm disk upload` tooupload VHD tooa конкретной учетной записи хранения. Прочитать больше о hello команды toomanage диски данных Azure виртуальной машины [здесь](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

4. Теперь можно присоединить hello требуемого VHD tooyour виртуальной машины:
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   Убедитесь, что tooreplace *myVM* с именем hello вашей виртуальной машины и *myVHD* с вашего нужного виртуального жесткого диска.

5. Вы можете проверить диск hello вложенного toohello виртуальную машину с `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Hello вывода будет примерно toohello следующий пример:

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> После добавления диска данных и вы перейдете требуется toolog на виртуальной машине toohello инициализировать диск hello hello виртуальная машина может использовать hello диска для хранения данных (см. шаги hello следующие дополнительные сведения на toodo инициализация диска hello).
> 
> 

