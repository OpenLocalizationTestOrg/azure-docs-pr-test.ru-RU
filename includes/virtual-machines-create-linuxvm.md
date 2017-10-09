
1. Войдите в tooyour подписку Azure с помощью hello действия, приведенные в [подключение tooAzure из hello Azure CLI 1.0](../articles/xplat-cli-connect.md).

2. Убедитесь, что вы находитесь в режиме развертывания классический hello, следующим образом:

    ```azurecli
    azure config mode asm
    ```

3. Информация hello образа Linux, которые должны tooload из доступных образов hello следующим образом:

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    В окне командной строки Windows вместо оператора grep используйте **find** .
   
4. Используйте `azure vm create` toocreate ВМ с образа Linux hello из предыдущего списка hello. На этом шаге создаются облачная служба и учетная запись хранения. Можно подключиться этой виртуальной Машины tooan существующей облачной службы с `-c` параметр. Создание toolog конечной точки SSH в виртуальной машине Linux toohello с hello `-e` параметр. Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью hello `Ubuntu-14_04_4-LTS` изображения в hello `West US` расположение и добавляет имя пользователя `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    Hello вывода будет примерно toohello следующий пример:

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Для виртуальной машины Linux, необходимо предоставить hello `-e` в диалоговом окне `vm create`. Нет возможности tooenable SSH после создания виртуальной машины hello. Дополнительные сведения о SSH чтения [как tooUse SSH с Linux в Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

5. Атрибуты hello hello ВМ можно проверить с помощью hello `azure vm show` команды. Hello следующий пример выводит сведения для виртуальной Машины с именем hello `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. Запустить ВМ с hello `azure vm start` следующим образом:

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>Дальнейшие действия
Сведения о всех этих команд виртуальной машины Azure CLI 1.0 чтения hello [использование hello Azure CLI 1.0 с помощью API развертывания классический hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

