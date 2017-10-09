
1. <span data-ttu-id="83651-101">Войдите в tooyour подписку Azure с помощью hello действия, приведенные в [подключение tooAzure из hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="83651-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="83651-102">Убедитесь, что вы находитесь в режиме развертывания классический hello, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="83651-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="83651-103">Информация hello образа Linux, которые должны tooload из доступных образов hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="83651-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="83651-104">В окне командной строки Windows вместо оператора grep используйте **find** .</span><span class="sxs-lookup"><span data-stu-id="83651-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="83651-105">Используйте `azure vm create` toocreate ВМ с образа Linux hello из предыдущего списка hello.</span><span class="sxs-lookup"><span data-stu-id="83651-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="83651-106">На этом шаге создаются облачная служба и учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="83651-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="83651-107">Можно подключиться этой виртуальной Машины tooan существующей облачной службы с `-c` параметр.</span><span class="sxs-lookup"><span data-stu-id="83651-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="83651-108">Создание toolog конечной точки SSH в виртуальной машине Linux toohello с hello `-e` параметр.</span><span class="sxs-lookup"><span data-stu-id="83651-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="83651-109">Hello следующий пример создает Виртуальную машину с именем `myVM` с помощью hello `Ubuntu-14_04_4-LTS` изображения в hello `West US` расположение и добавляет имя пользователя `ops`:</span><span class="sxs-lookup"><span data-stu-id="83651-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="83651-110">Hello вывода будет примерно toohello следующий пример:</span><span class="sxs-lookup"><span data-stu-id="83651-110">hello output is similar toohello following example:</span></span>

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
   > <span data-ttu-id="83651-111">Для виртуальной машины Linux, необходимо предоставить hello `-e` в диалоговом окне `vm create`.</span><span class="sxs-lookup"><span data-stu-id="83651-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="83651-112">Нет возможности tooenable SSH после создания виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="83651-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="83651-113">Дополнительные сведения о SSH чтения [как tooUse SSH с Linux в Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="83651-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="83651-114">Атрибуты hello hello ВМ можно проверить с помощью hello `azure vm show` команды.</span><span class="sxs-lookup"><span data-stu-id="83651-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="83651-115">Hello следующий пример выводит сведения для виртуальной Машины с именем hello `myVM`:</span><span class="sxs-lookup"><span data-stu-id="83651-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="83651-116">Запустить ВМ с hello `azure vm start` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="83651-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="83651-117">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83651-117">Next steps</span></span>
<span data-ttu-id="83651-118">Сведения о всех этих команд виртуальной машины Azure CLI 1.0 чтения hello [использование hello Azure CLI 1.0 с помощью API развертывания классический hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="83651-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

